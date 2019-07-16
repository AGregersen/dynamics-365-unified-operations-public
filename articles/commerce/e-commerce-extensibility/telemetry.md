---
# required metadata

title: Telemetry
description: The Dynamics 365 e-commerce SDK comes with a custom telemetrylogger, which provides the ability to log at various levels to multiple different resources while maintaining a unified context on both the server and the client.
author: SamJarawan
manager: JeffBl
ms.date: 08/30/2019
ms.topic: article
ms.prod: 
ms.service: Dynamics365Operations
ms.technology: 

# optional metadataA

# ms.search.form: 
audience: Developer
# ms.devlang: 
ms.reviewer: josaw
ms.search.scope: Retail, Core, Operations
# ms.tgt_pltfrm: 
ms.custom: 
ms.assetid: 
ms.search.region: Global
# ms.search.industry: 
ms.author: SamJar
ms.search.validFrom: 2019-08-30
ms.dyn365.ops.version: 

---
# Telemetry Logger
The Dynamics 365 e-commerce SDK comes with a custom telemetrylogger, which provides the ability to log at various levels to multiple different resources while maintaining a unified context on both the server and the client.

## Accessing the Logger
The SDK logger is available by default to all react components by simply accessing it with the `telemetry` prop:

``` js
// Inside a module view
this.props.telemetry
```

There are instances where you will want to access the logger in a shared component, rather than having to pass down the logger through the props of every component within your module, we have provided a utility HOC `WithContext()` within the SDK repository which allows you to inject the logger directly into your component.

By default, the SDK logger will log all events to an Application Insights instance. When running on a development environment, all logs will also be displayed on the console.

## Trace Logging

Logging of messages, ranging in importance from debug statements to critical errors, can be accomplished with the trace logging portion of the SDK logger. The trace logger uses the following logging methods/levels:

``` ts
enum LogLevel {
    Trace = 'trace',
    Debug = 'debug',
    Information = 'information',
    Warning = 'warning',
    Error = 'error',
    Critical = 'critical',
    None = 'none'
}
```

### Trace Logging APIs

The primary API used to log a trace message is:

``` ts
telemetry.log(
    logLevel: LogLevel,                 // One of the log levels listed in the enum above
    messageTemplate: string,            // A string that follows a message template format (see below for more info)
    logOptions?: TelemetryLogOptions    // Object wrapping up the optional parameters for the log statement
)
```

The trace logging system uses message templates to enforce a structured logging system of telemetry. This means that the logs will be capturable and renderable in both human- and machine- friendly formats. The `messageTemplate` argument to the `.log` call will use what are called 'named holes' for any event data. When writing trace log messages, you can write human-readable messages, and anywhere where you want to include event data, mark that place in the message template with `{<name>}`, where `<name>` is what you want to call the data that will go there. The actual value that will fill that named hole will be provided in the `logOptions.values` parameter. The `logOptions` parameter contains any of the optional parameters that should be included for a trace log:

``` ts
type TelemetryLogOptions = {
    values?: unknown[];       // Holds any arguments that are meant for placeholders in the message template
    customTags?: string[];    // Array of custom tags to add to log. Custom tags can be used to group message in the telemetry back-end
    exception?: Error;        // Exception that can be attached to the log. Will contain details like stack trace info
};
```

The benefits of this structured logging system is that when rendering the log messages for a human to read, the system can replace the named holes with the values provided. But when sending and storing the message, or when processing the telemetry by a machine, the event data can be kept separate, and used for things like aggregation or filtering specific messages, without requiring any string parsing. More information on structured logging and message templates can be found at https://messagetemplates.org/.

Here are some examples of trace log calls:

``` ts
telemetry.log(LogLevel.Debug, "{user} says {word}", {values: ["Sam", "Hi!"]});
// Output: "Sam says Hi!"

telemetry.log(LogLevel.Debug, "Customer {customer} purchased item {productID}", {values: [12345, 321]});
// Output: "Customer 12345 purchased item 321

telemetry.log(LogLevel.Debug, "Module {id} threw error {code} while rendering", {values: [123, 404], customTags: ["Module Error"], exception: error});
// Output: "Module 123 threw error 404 while rendering
// The customTags and exception will be attached to the log call, and can be viewed in the telemetry back-end
```

There are also wrapper methods that simplify the logging calls, but they are only able to log strings. There is one for each log level:

``` ts
this.props.telemetry.trace("This will log at log level 'trace'");
this.props.telemetry.debug("This will log at log level 'debug'");
this.props.telemetry.information("This will log at log level 'information'");
this.props.telemetry.warning("This will log at log level 'warning'");
this.props.telemetry.error("This will log at log level 'error");
this.props.telemetry.critical("This will log at log level 'critical");
```

If you want to include additional strings or other objects in the wrapper methods, you can add them to the message by passing them as arguments at the end of the call. All additional arguments will be converted to strings, and joined with the first string message and separated by a comma:

```ts
this.props.telemetry.trace("This is the first message", "This is the second message", {some object})

// Output will be: "This is the first message,This is the second message,{.toString result of {some object}}"
```

The console logs are controlled by a query string called ```?debug=true```

## Exception Logging

Logging of `Error` objects (and classes inheriting from them) can be done through the `.exception(Error)` API:

```ts
this.props.telemetry.exception(new Error("Something is broken!"));
```

### .error vs .exception

Due to their similar naming, and the fact that it is possible to log `Error` objects using `.error()` by passing them as additional arguments, there may be some confusion around when you should use `.error()` or `.exception()` to log an error in your application.

The best guidance is to use `.exception()` when you want to log an actual `Error` object, and to use `.error()` when you just want to log a string message saying an error has occured in your business logic. The reason for this is that in the AppInsights backend, `.exception()` logs are more easily correlated with issues, and allow for faster debugging when a real issue arises. The messages from `.error()` are simply treated as another trace log, and may require a more detailed analysis of the logs to find the issue than if you used `.exception()`, which impacts the time it takes to recognize an issue has occurred. In addition `.exception()` allows for better tracking across different requests, and therefore supports things like automatic alerting when an issue begins to affect a large number of requests.

## Business Intelligence Logging

Logging of business intelligence events, such as a product being added to a cart or a checkout action, can be accomplished with the business intelligence portion of the SDK logger. The business intelligence logger supports the following event types:

``` ts
enum TelemetryEvent {
    PageView = 'PageView',
    ProductPageView = 'ProductPageView',
    AddToCart = 'AddToCart',
    CheckOut = 'CheckOut',
    Purchase = 'Purchase',
    Custom = 'Custom'
}
```

Each event type has a required payload, or content, that must be sent when the event is logged. The payloads are defined as:

``` ts
type TelemetryEventContent =
    | IPageViewInfo         // Required for PageView events
    | IProductUnit[]        // Required for ProductPageView, AddToCart, Checkout events
    | IProductTransaction   // Required for Purchase events
    | ICustomEvent;         // Required for CustomEvent events

interface IPageViewInfo {
    title: string;
    location?: string;
    page?: string;
}

interface IProductUnit {
    productInfo: IProductInfo;
    quantity: number;
}

interface IProductInfo {
    id: string;
    name: string;
    brand?: string;
    category?: string;
    variant?: string;
    price?: number;
    currencyCode?: string;
}

IProductTransaction {
    id: string;
    affiliation?: string;
    revenue?: number;
    tax?: number;
    shippingCost?: number;
    products?: IProductUnit[];
}

interface ICustomEvent {
    contentCategory: string;
    contentAction?: {};
}
```

You can log a business intelligence event by calling `telemetry.logEvent({TelemetryEvent}, {TelemetryEventContent})`. For example:

``` ts
const product: IProductUnit = {
            productInfo: {
              id: 'id_coffee',
              name: 'Coffee',
              price: 6.5,
              currencyCode: 'USD',
            },
            quantity: 3
        };

const transaction: IProductTransaction = {
            id: transid,
            revenue: 15,
            tax: 3,
            shippingCost: 5,
            products: [product]
        };

this.props.telemetry.logEvent(TelemetryEvent.AddToCart, [product]);
this.props.telemetry.logEvent(TelemetryEvent.CheckOut, [product]);
this.props.telemetry.logEvent(TelemetryEvent.Purchase, transaction);
```

### Registering a new Business Intelligence logger

To register a BI event logger, you need to add a following block to the initialization.json:

``` ts static
    "telemetryEventLoggers": [
        {
            "key": "console-event-logger",
            "path": "telemetry/event-loggers/console-event-logger",
            "enabled": true
        }
    ]
```

The key can be an arbitrary name while the path needs to point to where the logger code lives. You need to set the enabled to true to make it active.
Currently, we provide support for Google Tag Manager as one of the logging targets. To use it, you need to install the telemetry package and enable it via the initialization.json. In the future, we will add support for more systems to log to, such as Application Insights or Google Analytics. Multiple business intelligence loggers will be able to be registered with the SDK logger, so that a single call to the `telemetry.logEvent({TelemetryEvent}, {TelemetryEventContent})` API will write the event to multiple systems.
