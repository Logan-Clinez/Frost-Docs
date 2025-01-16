---
description: >-
  This library requires you to authenticate to G-PORTAL to interact with your
  Rust Console community server(s), so this step is mandatory!
---

# Authentication

{% hint style="warning" %}
It is important to call the "init()" method after creating a new class instance as this is the method which processes the authentication and connects to G-PORTAL!
{% endhint %}

## Authenticating <a href="#authenticating" id="authenticating"></a>

Don't worry! Your GPORTAL credentials are not stored and are only accessible in your own code. Your credentials are used to get the initial set of authentication tokens from GPORTAL.

{% tabs %}
{% tab title="TypeScript" %}
```typescript
import { FrostyManager, LogLevel } from "frosty-bot";

const frosty = new FrostyManager();
await frosty.init({
    username: "", // Your GPORTAL email address
    password: "" // Your GPORTAL password
}, {
    level: LogLevel.Info,
    file: "frosty.log"
});
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const { FrostyManager, LogLevel } from "frosty-bot";

const frosty = new FrostyManager();
await frosty.init({
    username: "", // Your GPORTAL email address
    password: "" // Your GPORTAL password
}, {
    level: LogLevel.Info,
    file: "frosty.log"
});
```
{% endtab %}
{% endtabs %}
