## States

**States** are running instances of a flow. They contain a lot of useful data, like all the values and the current step that a user is on.

#### Lifetime

States are persisted in the platform in two ways - ephemerally and permanently, depending on your requirements.

##### Ephemeral States

<aside class="success">Recommended for use in <strong>Development, Testing & Staging</strong></aside>
<aside class="notice">Created when using <strong>Run</strong> in the Draw Tool</aside>

Ephemeral states are states that are stored in our cache, but have no guarantees on their lifetime. They will only be available to join or use until our cache cluster needs to reclaim space for newer states, which could be at any time.

This type of state is fine for using while you are building or testing flows, as they're only short-term and will be automatically cleaned up.

##### Permanent States

<aside class="success">Recommended for use in <strong>Production</strong></aside>
<aside class="notice">Created when using <strong>Publish</strong> in the Draw Tool</aside>

Permanent states are states that are saved in our database for longer-term storage. While the state is still in progress and hasn't reached it's final step, it will be available for joining. Once a state has reached it's final step, it is considered "done" and the state will then be deleted after 3 days.

#### Expiration

States can be set to expire, either in the Draw Tool or the Build Tool. After a state expires, anyone who tries to join or progress through it will receive the message *"The state with ID 12345 has now expired"* and will no longer be able to interact with or view it.

##### Setting an Expiration

When creating a new flow or editing an existing one, you can set the **Expire After** field to the number of seconds that the state should last for.

