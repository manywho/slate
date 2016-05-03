## Twilio

You can use the Twilio Service to build Flows that do interesting things with text messaging, text-to-speech, and speech-to-text. For more information on Twilio, you can visit their site here: [https://twilio.com](https://twilio.com). It can also be helpful to reference the Twilio developer documentation ([https://docs.twilio.com](https://docs.twilio.com)) if you need additional information on how things work.


### Installing the Twilio Service


#### Intro

In order to install the Twilio Service, you first need an active Twilio Account. To sign up for an account, please go here: [https://www.twilio.com/try-twilio](https://www.twilio.com/try-twilio).

Once you have an account, you can complete the Twilio Service installation below. All of the information you need is available in the **Account** area under the **API Credentials**.


**Text Messaging**

If you are going to use the Service to send/receive text messages, you should do the following:

1. Purchase a number that supports text messaging.
2. Under the **PROGRAMMABLE SMS** section, click on **PHONE NUMBERS**.
3. Click on the purchased phone number and view the **Messaging** tab. Provide the following:
    - **Configure with**: select *URL*
    - **Request URL**: `https://services.manywho.com/api/twilio/2/callback/status/message`
    - **Fallback URL**: `https://services.manywho.com/api/twilio/2/callback/status/message`
4. Click on **Save**

This will configure the number for asynchronous text messaging. Allowing your Flows to not only send texts, but also receive and process responses.


**Text-to-Speech**

If you are going to use the Service to build IVRs using text-to-speech, you should do the following:

1. Purchase a number that supports voice. You can re-use the number above.
2. Build a Flow that will be used to handle in-coming calls from your Twilio number.
2. Under the **PROGRAMMABLE VOICE** section, click on **PHONE NUMBERS**.
3. Click on the purchased phone number and view the **Voice** tab. Provide the following:
    - **Configure with**: select *URL*
    - **Request URL**: `https://services.manywho.com/api/twilio/2/callback/twiml/voice/flow/{tenantId}/{flowId}`
    - **Fallback URL**: `https://services.manywho.com/api/twilio/2/callback/twiml/voice/flow/{tenantId}/{flowId}`
4. Click on **Save**

The **{tenantId}** and **{flowId}** parameters can be retrieved from the URL for your Flow:

`https://flow.manywho.com/{tenantId}/play/default?flow-id={flowId}`


##### Features

Name | Description
---- | -----------
**Logic** | Twilio Service supports a number of logic features from starting an outbound call to sending and receiving text messages.


#### Configuration

When installing the Service, you should use the following settings:


**Connection Uri**

`https://services.manywho.com/api/twilio/2`


**Configuration Values**

Name | Type | Required | Description
---- | ---- | :------: | -----------
Account SID | String | ✔ | The AccountSID for your Twilio account. You can access this information from the Account area under the API Credentials.
Auth Token | Password | ✔ | The AuthToken for your Twilio account.


#### Types

The following Types are available for this Service. The Database column indicates if the Type can be Saved, Loaded, or Deleted using the Service. The Listening column indicates if Objects of this Type can be listened to.

Name | Description | Database | Listening
---- | ----------- | :------: | :-------:
**Call** | Used to make a Call | ✘ | ✘
**SMS** | Used to send text messages | ✘ | ✘
**MMS** | Used to send multi-media messages | ✘ | ✘
**Media** | The media associated with a MMS | ✘ | ✘
**Recording** | Contains the result of a call recording | ✘ | ✘


#### Actions

Some helpful summary information about the various Actions that can be performed.


##### Send SMS

Use this action to send/receive SMS messages.

<aside class="notice">
<b>Message Apps</b><br/>
If you create a Outcome Conditions for the SMS reply, this Action will act acynchronously. This means that when you execute this Action, the Flow will wait for the reply until the Outcome Condition is 'true'.
</aside>

**Inputs**

Name | Type | Required | Description
---- | ---- | :------: | -----------
**Message** | SMS | ✘ | The SMS message to send.

**Outputs**

Name | Type | Description
---- | ---- | -----------
**Reply** | SMS | The SMS message the user replied back with.


##### Send SMS (Simple)

Use this action to send/receive SMS messages without using the SMS object. Otherwise, this Action is identical to Send SMS.

<aside class="notice">
<b>Message Apps</b><br/>
If you create a Outcome Conditions for the Reply, this Action will act acynchronously. This means that when you execute this Action, the Flow will wait for the reply until the Outcome Condition is 'true'.
</aside>

**Inputs**

Name | Type | Required | Description
---- | ---- | :------: | -----------
**To** | String | ✘ | The phone number to send the text.
**From** | String | ✘ | The phone number associated with your Twilio Account. This is the number that supports text messaging.
**Body** | String | ✘ | The body of the text that will be sent to the **To** phone number.

**Outputs**

Name | Type | Description
---- | ---- | -----------
**Reply** | String | The body of the text received from the end user.


##### Send MMS

Use this action to send/receive MMS messages.

<aside class="notice">
<b>Message Apps</b><br/>
If you create a Outcome Conditions for the MMS reply, this Action will act acynchronously. This means that when you execute this Action, the Flow will wait for the reply until the Outcome Condition is 'true'.
</aside>

**Inputs**

Name | Type | Required | Description
---- | ---- | :------: | -----------
**Message** | MMS | ✘ | The MMS message to send. To send media with the MMS you can populate the List of Media objects accordingly.

**Outputs**

Name | Type | Description
---- | ---- | -----------
**Reply** | MMS | The MMS message the user replied back with.


##### Start Outbound Call

Use this action to start a call with the end user.

<aside class="notice">
<b>Text-to-Speech</b><br/>
Once the call has been started, Twilio will "join" the follow and begin rendering the Steps/Pages as TwiML (text-to-speech). Make sure you check out the documentation on creating a basic Twilio IVR to get details on this.
</aside>

**Inputs**

Name | Type | Required | Description
---- | ---- | :------: | -----------
**Call** | Call | ✘ | The call to start with the end user.


##### Start Outbound Call (Simple)

Use this action to start a call with the end user without using the Call object. Otherwise, this Action is identical to Send SMS.

<aside class="notice">
<b>Text-to-Speech</b><br/>
Once the call has been started, Twilio will "join" the follow and begin rendering the Steps/Pages as TwiML (text-to-speech). Make sure you check out the documentation on creating a basic Twilio IVR to get details on this.
</aside>

**Inputs**

Name | Type | Required | Description
---- | ---- | :------: | -----------
**To** | String | ✘ | The phone number to send the text.
**From** | String | ✘ | The phone number associated with your Twilio Account. This is the number that supports text messaging.
**Timeout** | Number | ✘ | The number of seconds to wait until the outbound call should timeout. The usual value is `60`.
**Record** | Boolean | ✘ | Indicates if the call should be recorded.


### Code

You can access the source code and developer details about implementation on GitHub.


**GitHub**

`https://github.com/manywho`


### Building an IVR

You can use the Twilio Service to create Flows that work exactly like an IVR. A few considerations:

1. You should use Steps for the content of each step in the IVR. Do not use any formatting as this can confuse the text-to-speech converter.
2. Any outcomes coming from the Step should have a Name that's a digit. If the user enters the digit into their phone, this is equivalent to a user clicking on the Outcome in the browser.
3. The Flow should be "public" as Twilio does not support any form of authentication.

You can always test your Flow in the browser before accessing it via Twilio.
