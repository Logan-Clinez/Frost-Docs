---
description: >-
  RCE.JS includes it's own logger for information, warnings, debugging and
  errors. You can learn how to configure the logger here!
---

# Logger

## Configuration <a href="#configuration" id="configuration"></a>

By default the logger is set to ignore debugging to keep your logs less clustered, however you can change how the logger works.

The following log levels are available to set:

```
None | Info | Warn | Error | Debug
```

**None** - this will completely disable the logger

**Info** - this will log all important information, include warnings and errors

**Warn** - this will log only warnings and errors

**Error** - this will only log errors

**Debug** - this is the highest logger level and will log everything including debugging

{% hint style="info" %}
By default, the log level is **Info** when no value is provided
{% endhint %}

## Log File <a href="#log-file" id="log-file"></a>

Optionally, you may also provide a file-name to log ALL content to, this is very useful for debugging! Simply provide a "logFile" parameter in the LoggerOptions.

{% tabs %}
{% tab title="TypeScript" %}
```typescript
import { RCEManager, LogLevel } from "rce.js";

const rce = new RCEManager();
await rce.init({
    // ... Your AuthOptions
}, {
    logLevel: LogLevel.Info, // Change to your preferred level
    logFile: "rce.log" // Optional
});
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const { RCEManager, LogLevel } = require("rce.js");

const rce = new RCEManager();
await rce.init({
    // ... Your AuthOptions
}, {
    logLevel: LogLevel.Info, // Change to your preferred level
    logFile: "rce.log" // Optional
});
```
{% endtab %}
{% endtabs %}

## Custom Logger <a href="#custom-logger" id="custom-logger"></a>

{% hint style="info" %}
This will only work for **TypeScript**
{% endhint %}

For TypeScript users, there is a logger interface provided which can be used to create your own custom logger - see the below example.

Only the info, warn, error and debug methods are strictly required - beyond that, you can implement your own methods and styles too!

{% tabs %}
{% tab title="TypeScript" %}
```typescript
import { ILogger, LogLevel } from "rce.js";
import { inspect } from "util";

export default class MyCustomLogger implements ILogger {
    private level: LogLevel;
    
    public constructor(level: LogLevel) {
        this.level = level;
    }
    
    private format(content: any) {
        return typeof content === "string"
            ? content
            : inspect(content, { depth: 5 });
    }
    
    private has(level: LogLevel): boolean {
        return level >= this.level;
    }
    
    public debug(content: string) {
        if (!this.has(LogLevel.Debug)) return;
        
        console.log(`[DEBUG] ${this.format(content)}`);
    }
    
    public error(content: string) {
        if (!this.has(LogLevel.Error)) return;
        
        console.log(`[ERROR] ${this.format(content)}`);
    }
    
    public info(content: string) {
        if (!this.has(LogLevel.Info)) return;
        
        console.log(`[INFO] ${this.format(content)}`);
    }
    
    public warn(content: string) {
        if (!this.has(LogLevel.Warn)) return;
        
        console.log(`[WARN] ${this.format(content)}`);
    }
    
    // ...
}
```
{% endtab %}
{% endtabs %}

After creating your custom logger class, you can set rce.js to use it like below!

{% tabs %}
{% tab title="TypeScript" %}
```typescript
import { RCEManager, LogLevel } from "rce.js";
import MyCustomLogger from "./logger";

const rce = new RCEManager();
await rce.init({
    // AuthOptions ...
}, {
    instance: new MyCustomLogger(LogLevel.Info);
});
```
{% endtab %}
{% endtabs %}
