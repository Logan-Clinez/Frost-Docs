---
description: >-
  You can add servers to interact with via your application by following the
  documentation on this page.
---

# Adding Servers

## Example Code <a href="#example-code" id="example-code"></a>

{% tabs %}
{% tab title="TypeScript" %}
```typescript
import { RCEManager, RCEIntent } from "rce.js";

const rce = new RCEManager();
await rce.init({
    // ...
}, {
    // ...
});

await rce.servers.addMany([
    {
        identifier: "my-solo-duo-trio-3x",
        serverId: 1234567,
        region: "US",
        intents: [RCEIntent.All], // All, ConsoleMessages, ServiceState, ServiceSensors
        playerRefreshing: true,
        radioRefreshing: true,
        extendedEventRefreshing: true,
        state: ["trio", "3x"]
    },
    {
        identifier: "my-zerg-2x",
        serverId: 7654321,
        region: "EU",
        intents: [RCEIntent.ConsoleMessages],
        state: ["zerg", "2x"]
    },
    // ...
]);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const { RCEManager, RCEIntent } = require("rce.js");

const rce = new RCEManager();
await rce.init({
    // ...
}, {
    // ...
});

await rce.servers.addMany([
    {
        identifier: "my-solo-duo-trio-3x",
        serverId: 1234567,
        region: "US",
        intents: [RCEIntent.All], // All, ConsoleMessages, ServiceState, ServiceSensors
        playerRefreshing: true,
        radioRefreshing: true,
        extendedEventRefreshing: true,
        state: ["trio", "3x"]
    },
    {
        identifier: "my-zerg-2x",
        serverId: 7654321,
        region: "EU",
        intents: [RCEIntent.ConsoleMessages],
        state: ["zerg", "2x"]
    },
    // ...
]);
```
{% endtab %}
{% endtabs %}

You can also add one server at a time using the following method:

{% tabs %}
{% tab title="TypeScript" %}
```typescript
import { RCEManager, RCEIntent } from "rce.js";

const rce = new RCEManager();
await rce.init({
    // ...
}, {
    // ...
});

await rce.servers.add({
    identifier: "solo-only-3x",
    serverId: 1111111,
    region: "EU",
    intents: [RCEIntent.All],
    state: ["solo", "3x"]
});
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const { RCEManager, RCEIntent } = require("rce.js");

const rce = new RCEManager();
await rce.init({
    // ...
}, {
    // ...
});

await rce.servers.add({
    identifier: "solo-only-3x",
    serverId: 1111111,
    region: "EU",
    intents: [RCEIntent.All],
    state: ["solo", "3x"]
});
```
{% endtab %}
{% endtabs %}

## Server Options <a href="#server-options" id="server-options"></a>

Below is a brief explanation of each option when defining new server(s).

<details>

<summary>Identifier</summary>

The identifier is a unique string which allows rce.js to identify the correct server(s) events are being received for or commands are being sent to. We suggest using a UUID for this!

**Type**: String

**Required**: Yes

</details>

<details>

<summary>Server ID</summary>

The server ID is the ID you see in the URL when on the G-PORTAL manage server page, this is the ID required for rce.js to communicate with G-PORTAL.

**Type:** Number | Number\[]

**Required:** Yes

</details>

<details>

<summary>Region</summary>

The region is the region your rust server is based in, this can only be two options, either "US" or "EU". This is also required for rce.js to communicate with G-PORTAL.

**Type:** "US" | "EU"

**Required:** Yes

</details>

<details>

<summary>Intents</summary>

The intents are needed so rce.js knows which WebSocket subscriptions to subscribe to with G-PORTAL, it can potentially save needless subscriptions!

**Type:** RCEIntent\[]

**Required**: Yes

**Explanation**

**ALL** - Subscribe to all subscriptions

**ConsoleMessages** - Subscribe to Console Messages, this is needed to receive console logs from G-PORTAL

**ServiceState** - Subscribe to Service State, this is needed for rce.js to know when your server is online, offline, or restarting. It is also better for error handling!

**ServiceSensors** - Subscribe to Service Sensors, this is needed if you want notifications of how much CPU and RAM your rust server is using

</details>

<details>

<summary>State</summary>

The state is an array of anything you wish to implement. For example, you can add "pvp" in your state array and check later in your code is the state array includes "pvp" to make your application behave differently if the server is a PvP-only server. You can use the state for anything.

**Type**: Any\[]

**Required**: No

**Default:** \[]

</details>

<details>

<summary>Player Refreshing</summary>

If enabled, the player list in your rust server will be checked every one minute and the connected players will be cached in rce.js - it will also enable a few events.

**Type:** Boolean

**Required:** No

**Default:** False

</details>

<details>

<summary>Radio Refreshing</summary>

If enabled, any active radio frequencies in your rust server will be checked every thirty seconds and will enable events for when a frequency is gained or lost. This option is also required to emit Oil Rig and Small Oil Rig events.

**Type:** Boolean

**Required:** No

**Default:** False

</details>

<details>

<summary>Extended Events</summary>

If enabled, every one minute, debris fields will be checked for in your rust server and will emit a Bradley APC Debris event or Patrol Helicopter Debris event.

**Type:** Boolean

**Required:** No

**Default:** False

</details>
