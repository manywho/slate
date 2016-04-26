# Connect

This section contains information on how you can connect/integrate ManyWho to various other applications and platforms. Typically there are two parts to any integration:

1. **Service**: Links ManyWho to the underlying database, identity management system, file store, logic, social networking, code, etc of the underlying platform.
2. **UI**: Embedding the ManyWho user experience directly into the application/platform. In some cases, the connected/integrated platform may provide additional UI components or may offer UI itself.

This section is broken down into each supported application/platform.

## Building a Service

#### Requirements
- Java IDE (IntelliJ IDEA Ultimate is recommended, for integration with Jersey)
- Maven 3
- JDK 8 or higher

#### Creating a Project

There is a Maven archetype available that will create a basic Service, along with some example actions, types and controller endpoints. Follow these instructions to install it inside IntelliJ:

1. Create a new project of type **Maven**, ticking the **Create from archetype** box, then clicking the **Add archetype** button and supplying the following details:
    - **GroupId**: com.manywho.services
    - **ArtifactId**: example-archetype
    - **Version**: 1.4.0
2. On the next screen, give your service a relevant group ID and artifact ID that follows the standard Java convention, e.g. com.manywho.services.github (replacing your TLD, company name and the name of your service)

3. IntelliJ will now be running the Maven goal to create the project from the archetype. When it finishes, click Enable auto-import on the popup at the top right and you should be good to go!

#### Adding the Grizzly Configuration
Using the Grizzly server to run the service locally is the best option, as it's pretty easy to debug inside IntelliJ. It's fairly easy to set up, following these instructions:

1. On the **Run** menu, choose **Edit Configurations**
2. Click the + button at the top left, choose **Application**, and give it the name *Run*
3. Under **Configuration > Main class**, point to your service's **Application** class
4. Click **OK**, and your service should now run under Grizzly when you launch it by clicking the **Debug** button

### How to: Build a Service

In this tutorial, we will be building a service that integrates with GitHub. We'll start right from generating the basic project template, and finish off with a service that loads, saves, and hits actions on the GitHub API.

The tutorial will assume you are using IntelliJ IDEA Ultimate Edition, and have Maven 3 and JDK 8 or higher installed.

#### Creating the Service Base

Follow the instruction on the Building a Service page to get the base structure of your service set up.

#### Building the Describe Response

Every service needs to return a Describe response from its /metadata endpoint. This response tells ManyWho what the service supports (i.e. Database, Identity, Logic, Files and Social). The Java SDK provides a simple builder class so it's super easy to create a describe response.

1. Open up **DescribeController** from inside the **controllers** package
2. Our GitHub service will provide the following:
    - Database (for loading a list of user repositories)
    - Identity (for logging into a Flow using GitHub)
    - Logic (for forking a repository)
3. Add a call to `setProvidesIdentity(true)` inside the `describe()` method, so it looks like this:

```java
public DescribeServiceResponse describe(ServiceRequest serviceRequest) {
    return new DescribeServiceBuilder()
            .setProvidesDatabase(true)
            .setProvidesIdentity(true)
            .setProvidesLogic(true)
            .setCulture(new Culture("EN", "US"))
            .createDescribeService()
            .createResponse();
}
```

#### Create a GitHub Application

We'll need an application on GitHub so that we can authorize users through OAuth2 and make calls on their behalf. You can create a new application on GitHub for free [here](https://github.com/settings/applications/new), and make sure the **Callback URL** is https://flow.manywho.com/api/run/1/oauth2. Make a note of the generated **Client ID** and **Client Secret**, as we'll need them later.

### Adding Authentication (Identity)

As the GitHub API is built around authorizing calls using OAuth2, we'll integrate an identity provider into our service that ManyWho can use to log into a Flow, which means that we can make calls on behalf of the logged in user without having to store tokens anywhere or ask them for their password.

##### Creating the OAuth2 Provider

Each service that integrates with OAuth2 for authorization needs to have a Provider class, that gives the SDK's OAuth2 library the correct secrets and where to request tokens.

1. Create a new package inside **com.manywho.services.github** called **oauth2**
2. Inside this new package, create a class called **GitHubProvider**
3. Make the new class extend **AbstractOauth2Provider**, which is a base class in the SDK for creating a provider in services that implement OAuth2
4. Press **Ctrl+I** then **Enter** to implement the required methods from the interface
5. Fill in the details based on this example:

```java
public class GitHubProvider extends AbstractOauth2Provider {
    @Override
    public String getName() {
        return "GitHub";
    }
 
    @Override
    public String getClientId() {
        return ""; // This value should be your Client ID from your application (https://github.com/settings/applications/new)
    }
 
    @Override
    public String getClientSecret() {
        return ""; // This value should be your Client Secret from your application (https://github.com/settings/applications/new)
    }
 
    @Override
    public String getRedirectUri() {
        return "https://flow.manywho.com/api/run/1/oauth2";
    }
 
    @Override
    public String getAccessTokenEndpoint() {
        return "https://github.com/login/oauth/access_token";
    }
 
    @Override
    public String getAuthorizationUrl(OAuthConfig config) {
        return String.format("https://github.com/login/oauth/authorize?client_id=%s&redirect_uri=%s", config.getApiKey(), config.getCallback());
    }
}
```

##### Creating the AuthService

1. Create a new package inside **com.manywho.services.github** called **services**
2. Inside this new package, create a class called **AuthService**, and paste in the following code

```java
public class AuthService {
    public AuthenticatedWhoResult authenticateWithGitHub(OauthProvider oauthProvider, OAuthService oauthService, AuthenticationCredentials authenticationCredentials) throws Exception {
        Token accessToken = oauthService.getAccessToken(null, new Verifier(authenticationCredentials.getCode()));
 
        return createAuthenticatedWhoResult(oauthProvider, accessToken.getToken());
    }
 
    private AuthenticatedWhoResult createAuthenticatedWhoResult(OauthProvider oauthProvider, String token) throws IOException {
        User user = new UserService(createGitHubClient(token)).getUser();
 
        return new AuthenticatedWhoResult() {{
            setDirectoryId(oauthProvider.getName());
            setDirectoryName(oauthProvider.getName());
            setEmail(user.getEmail());
            setFirstName(user.getName());
            setIdentityProvider(oauthProvider.getName());
            setLastName(user.getName());
            setStatus(AuthenticationStatus.Authenticated);
            setTenantName(oauthProvider.getClientId());
            setToken(token);
            setUserId(String.valueOf(user.getId()));
            setUsername(user.getLogin());
        }};
    }
 
    protected GitHubClient createGitHubClient(String token) {
        return new GitHubClient().setOAuth2Token(token);
    }
}
```

Basically, in the code we just pasted, the `authenticateWithGitHub()` method will be called from inside the **AuthController** (which we'll create in a minute), it calls out to the GitHub API to fetch the logged in user (using the GitHub Java library) and it returns an AuthenticatedWhoResult object that contains all of the logged-in user's information ready to be used inside a Flow.

Finally, we'll need to add the **AuthService** into the application binder, so that it can be injected into other classes by Jersey:

1. Open up **ApplicationBinder** in the root of the main package (**com.manywho.services.github**)
2. Inside the **configure()** method, add a new line that binds any calls to **AuthService** to an instance of **AuthService**, like so

```java
@Override
protected void configure() {
    bind(AuthService.class).to(AuthService.class);
}
```

##### Creating the AuthController

1. Create a new class in the **controllers** package called **AuthController**
2. Make the new class extend **AbstractOauth2Controller**, which is a base controller class in the ManyWho SDK for services that wish to implement authorization using OAuth2
3. Press **Ctrl+I** then **Enter** to implement the required `authentication()` method
4. Press **Alt+Insert** then click **Constructor** to implement the required constructor that inherits from the **AbstractOauth2Controller** class
5. Now add a new field of type **AuthService** called **authService**, and annotate it with the **@Inject** annotation (so Jersey will automatically supply an instance into the class at runtime)
6. Finally, add a new method called **authentication** that returns an **AuthenticatedWhoResult**, and takes a single **AuthenticationCredentials** parameter
7. Inside this method, return the result of a call to `authService.authenticateWithGitHub(oauth2Provider, getOauthService(), authenticationCredentials);`
8. Your **AuthController** class should now look like this:

```java
public class AuthController extends AbstractOauth2Controller {
    @Inject
    private AuthService authService;
 
    public AuthController(AbstractOauth2Provider oauth2Provider) {
        super(oauth2Provider);
    }
 
    @Override
    public AuthenticatedWhoResult authentication(AuthenticationCredentials authenticationCredentials) throws Exception {
        return authService.authenticateWithGitHub(oauth2Provider, getOauthService(), authenticationCredentials);
    }
}
```

### Creating the Describe

Every service is required to implement describe functionality. The /metdata endpoint of a service informs ManyWho on the capabilities of the service along with anything the service provides (e.g. Types), the describe response can implement several properties:

Name | Description
---- | -----------
ProvidesDatabase | Set to true if the service supports loading & saving via requests sent from Load & Save elements in a flow
ProvidesIdentity | Set to true if the service can be used as an identity provider for a flow i.e. allows a user to login using a 3rd party service like Google or Facebook
ProvidesLogic | Set to true if the service supports actions that can be executed via Message elements in a flow, listening to items, providing notifications to a flow, or voting
ProvidesFiles	 | Set to true if the service supports file management

##### Install

The service describe response also has an Install property that allows you to provide custom Types back to ManyWho that are specific to your service e.g. the JIRA service provides an **Issue Type** that has various properties such as Name, Type, Assignee, etc.
By default any classes in your service that extend AbstractType (from the Java SDK) will be automatically included in the describe response. You can manually add Types to the describe response install in case you need to provide dynamically generated Types as install time.

<aside class="notice">
<b>How to</b><br/>
An example of building a describe response can be found in: How to Build a Service
</aside>

### Creating an Action

An action is a method that interacts with a Service that performs a task, like "Send an Email" or "Assign a Task to this user".

Actions created using the Java SDK all extend the **AbstractAction** class and are automatically included in the Describe response when the Service installed in ManyWho. They can be added into a Service by creating a class like this:

**Action Template**
```java
package com.manywho.services.actions;
 
import com.manywho.sdk.entities.describe.DescribeValue;
import com.manywho.sdk.entities.describe.DescribeValueCollection;
import com.manywho.sdk.enums.ContentType;
import com.manywho.sdk.services.describe.actions.AbstractAction;
 
public class Example extends AbstractAction {
    @Override
    public String getUriPart() {
        return "category/name";
    }
 
    @Override
    public String getDeveloperName() {
        return "Action Name";
    }
 
    @Override
    public String getDeveloperSummary() {
        return "This is an example action for a Service";
    }
 
    @Override
    public DescribeValueCollection getServiceInputs() {
        return new DescribeValueCollection() {{
            add(new DescribeValue("Example String", ContentType.String, true));
            add(new DescribeValue("Example Object", ContentType.Object, true, null, ExampleOne.NAME));
        }};
    }
 
    @Override
    public DescribeValueCollection getServiceOutputs() {
        return new DescribeValueCollection() {{
            add(new DescribeValue("Created?", ContentType.Boolean, true));
        }};
    }
}
```

#### Required Fields

Field | Description | Example
----- | ----------- | -------
URI Part | Tells ManyWho the URI endpoint for the message action | *"tasks/assign"*
Developer Name | This is the name of the action that will be displayed in the Draw tool | Assign Task
Developer Summary | A short summary of what the action does that will be displayed in the Draw tool | Assign a task in Salesforce to a User
Service Inputs | A collection of values that the action can be given, both optional and required | *See code above*
Service Outputs | A collection of values that the action sends back to ManyWho that can be used in the Flow afterwards (can be empty) | *See code above*

#### Implementing the Endpoint

As building a Service using the Java SDK uses the JAX-RS standard for building REST APIs, it's super easy to add an endpoint for an action - all you need is a method in a controller that has the correct annotations.

Say we want to add an endpoint for the example action above, we will need:

- A controller for the action's "category" (e.g. TasksController)
- A method in that controller for the action (e.g. assignTask)
    - It must be annotated with the @Path, @POST, @Consumes("application/json") and @Produces("application/json") annotations
    - It must take a **ServiceRequest** object as the first parameter
    - It must return a **ServiceResponse** object
- A way of interacting with the API (Services are a nice way of keeping code SOLID)

**Example Endpoint**
```java
package com.manywho.services.controllers;
 
import com.manywho.sdk.entities.run.elements.config.ServiceRequest;
import com.manywho.sdk.entities.run.elements.config.ServiceResponse;
import com.manywho.sdk.enums.InvokeType;
import com.manywho.sdk.services.controllers.AbstractController;
import com.manywho.services.services.TaskService;
 
import javax.ws.rs.Consumes;
import javax.ws.rs.POST;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;
 
@Path("/tasks")
@Consumes("application/json")
@Produces("application/json")
public class ExampleController extends AbstractController {
 
    @Inject
    private TaskService taskService;
 
    @Path("/assign")
    @POST
    public ServiceResponse assignTask(ServiceRequest serviceRequest) throws Exception {
        this.taskService.assignTask(serviceRequest);
 
        return new ServiceResponse(InvokeType.Forward, serviceRequest.getToken());
    }
}
```

<aside class="notice">
<b>Note</b><br/>
After installing a Service that provides an Action into a ManyWho tenant the Action can be executed by adding a Message element to a Flow
</aside>

### Creating a Type

Types created the Java SDK all extend the **AbstractType** class and are automatically included in the Describe response when the service is installed in ManyWho. A basic Type be added into a Service by creating a class like this:

**Example Type**
```java
package com.manywho.services.types;
 
import com.manywho.sdk.entities.draw.elements.type.TypeElementProperty;
import com.manywho.sdk.entities.draw.elements.type.TypeElementPropertyCollection;
import com.manywho.sdk.enums.ContentType;
import com.manywho.sdk.services.describe.types.AbstractType;
 
public class ExampleOne extends AbstractType {
    public final static String NAME = "Example Type";
 
    @Override
    public String getDeveloperName() {
        return NAME;
    }
 
    @Override
    public TypeElementPropertyCollection getProperties() {
        return new TypeElementPropertyCollection() {{
            add(new TypeElementProperty("Property One", ContentType.String));
            add(new TypeElementProperty("Example Two", ContentType.Object, ExampleTwo.NAME));
        }};
    }
}
```

#### Fields

Field | Description | Required?
----- | ----------- | ---------
Developer Name | This is the name of the type that will be displayed in the Draw tool. Make sure to change the **NAME** field, so the type can continue to be easily reference from other types and actions | ✔
Properties | A collection of **TypeElementProperty** objects that define the properties for a type | ✔
Bindings | A collection of **TypeElementBinding** objects that define the bindings to use a type in a Database load/save/delete | ✘

### Debugging a Service

Debugging a service locally against the ManyWho platform running in the cloud is extremely useful as you won't have to deploy your service to use it. You can do this by using [ngrok](https://ngrok.com/) which creates a tunnel between your local machine and the internet. After setting up ngrok you can debug your service by installing it into your ManyWho tenant using the ngrok url.

### Errors & Exceptions

The ManyWho Java SDK provides 2 exception types that you should throw if an error occurs: **ServiceProblemException** and **ApiProblemException**.

<aside class="notice">
<b>Note</b><br/>
"Regular" exception types such as Argument, ArgumentNull, etc will be automatically transformed into ServiceProblemExceptions and returned to ManyWho as an "error" response.
</aside>

#### ServiceProblemException

This exception can be avoided as the SDK will handle it, however if you need to throw a ServiceProblemException is should be used for when something goes wrong in your service. For example if an incorrect configuration value was sent to the service, or if an invalid filter was sent to the load endpoint.

#### ApiProblemException

This exception should be thrown when a 3rd party API that your service connects to either fails or returns an error. For example JIRA API returns an error when your service attempts to create a new issue, the error message from JIRA should be passed to the ApiProblemException along with any other relevant details i.e. response body, response headers, etc

<aside class="notice">
<b>Note</b><br/>
The **message** value of the exception is what will be seen by users running the flow. The other properties will be available in the UI debugger.
</aside>

### Deploying to Heroku

If you created a service from the example archetype (1.4.0 upwards), then your service has built-in support for deploying to, and running on Heroku! An example Procfile is included in the root of your service, so a simple "git push heroku master" should get you up and running.

If your service isn't built using the example archetype then simply adding the following Procfile should work:

**Procfile**
```bash
web: java -Dserver.port=${PORT:-8080} ${JAVA_OPTS} -jar target/artifact-1.0-SNAPSHOT.jar
```
