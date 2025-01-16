---
description: >-
  Later in your application, you may want to remove servers from the RCE
  Manager, which we have you covered on!
---

# Removing Servers

## Remove Server <a href="#remove-server" id="remove-server"></a>

{% tabs %}
{% tab title="TypeScript" %}
```typescript
import { RCEManager } from "rce.js";

const rce = new RCEManager();
await rce.init({
    // ...
}, {
    // ...
});

rce.servers.remove("solo-only-2x");
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const { RCEManager } = require("rce.js");

const rce = new RCEManager();
await rce.init({
    // ...
}, {
    // ...
});

rce.servers.remove("solo-only-2x");
```
{% endtab %}
{% endtabs %}
