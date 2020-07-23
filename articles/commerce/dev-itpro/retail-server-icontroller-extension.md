---
# required metadata

title: Create a new Retail Server API
description: This topic explains how to create a new Retail Server API.
author: mugunthanm
manager: AnnBe
ms.date: 07/22/2020
ms.topic: article
ms.prod: 
ms.service: dynamics-365-commerce
ms.technology: 

# optional metadata

# ms.search.form: 
# ROBOTS: 
audience: Developer
# ms.devlang: 
ms.reviewer: rhaertle
ms.search.scope: Operations, Retail
# ms.tgt_pltfrm: 
ms.custom: 28021
ms.assetid: 
ms.search.region: Global
# ms.search.industry: 
ms.author: mumani
ms.search.validFrom: 2019-08-2019
ms.dyn365.ops.version: AX 10.0.11

---

# Create a new Retail Server extension API

[!include [banner](../includes/banner.md)]

This document explains how to create a new Retail Server application programming interface (API), and how to expose it so that POS or other clients can consume it. Modification of the existing Retail Server APIs isn't supported.

The Retail software development kit (SDK) includes only a few samples of end-to-end Retail Server extensions that include the Commerce Runtime (CRT). You can use these samples as templates to start your extensions. You can find the sample extensions in the RetailSDK\\SampleExtensions\\RetailServer folder.

## End-to-end sample repository in the Retail SDK

| Sample extension<br>(RetailSDK\\SampleExtensions\\RetailServer) | CRT sample<br>(RetailSDK\\SampleExtensions\\CommerceRuntime) | POS sample<br>(RetailSDK\\POS\\Extensions) |
|---------------------------------------------|--------------------------------------------|----------------------------------------|
| Extensions.StoreHoursSample                 | Extensions.StoreHoursSample                | StoreHoursSample                       |
| Extensions.SalesTransactionSignatureSample  | Extensions.SalesTransactionSignatureSample | SalesTransactionSignatureSample        |
| Extensions.PrintPackingSlipSample           | Extensions.PrintPackingSlipSample          |                                        |
| Extensions.CrossLoyaltySample               | Extensions.CrossLoyaltySample              |                                        |

## Create a new RS API

Follow the steps in this section to create a new RS extension

### Extension class diagram

![Commerce Scale Unit extension class diagram](media/RSExtensionClass.png)

The following illustration shows the class structure of the extension.

### Steps to create the new RS API:

1.	Before you create the Retail server (RS) extension, create the CRT extension. Retail Server APIs should have no logic except logic that calls the CRT with the parameters.
2.	Create a new C# class library project that uses the Microsoft .NET Framework version 4.6.1 or use any of the existing Retail server sample in the Retail SDK as a template.
3.	In the RS extension project, add a reference to your CRT extension library or project. This reference lets you call the CRT request and response and entities. 
4.	In the RS extension project add the **Microsoft.Dynamics.Commerce.Hosting.Contracts** package using NuGet package manager. The NuGet packages can be found in RetailSDK\pkgs folder.
5.	Create a new controller class and extend it form IController. This controller class will contain the method that must be exposed by the RS API. Inside the controller class, add methods to call the CRT request. Don’t extend the new controller class form existing controller class like CustomerController, ProductController etc. Extension classes must extend only form IController class.
6.	Add the Route Prefix attribute on the controller class to expose the controller class.
```C#
[RoutePrefix("SimpleExtension")]  
```
7.	Bind Entity attribute is required on a controller class if you are creating a new controller and exposing an entity. 
Sample code on how to create a simple RS API to return entity, string, and bool value. CRT request/response used in the sample is not included here, please check the CRT extension doc for that.

```C#
/**
 * SAMPLE CODE NOTICE
 * 
 * THIS SAMPLE CODE IS MADE AVAILABLE AS IS.  MICROSOFT MAKES NO WARRANTIES, WHETHER EXPRESS OR IMPLIED,
 * OF FITNESS FOR A PARTICULAR PURPOSE, OF ACCURACY OR COMPLETENESS OF RESPONSES, OF RESULTS, OR CONDITIONS OF MERCHANTABILITY.
 * THE ENTIRE RISK OF THE USE OR THE RESULTS FROM THE USE OF THIS SAMPLE CODE REMAINS WITH THE USER.
 * NO TECHNICAL SUPPORT IS PROVIDED.  YOU MAY NOT DISTRIBUTE THIS CODE UNLESS YOU HAVE A LICENSE AGREEMENT WITH MICROSOFT THAT ALLOWS YOU TO DO SO.
 */
 
/// <summary>
    /// New extended controller.
    /// </summary>
    [RoutePrefix("SimpleExtension")]  
    [BindEntity(typeof(SimpleEntity))]
                                  
    public class SimpleExtensionController : IController
    {
        /// <summary>
        /// The action to get the string value.
        /// </summary>
        /// <param name="context">The context parameters.</param>
        /// <param name="stringValue">The string value parameters.</param>
        /// <returns>The string value.</returns>
        [HttpPost]
        [Authorization(CommerceRoles.Customer, CommerceRoles.Employee)]
        public async Task<string> GetStringValue(IEndpointContext context, string stringValue)
        {
            GetStringValueResponse resp = await context.ExecuteAsync<GetStringValueResponse>
                                     (new GetStringValueRequest(stringValue)).ConfigureAwait(false);
            return resp.StringValue;
        }

        /// <summary>
        /// The action to get the bool value.
        /// </summary>
        /// <param name="context">The context parameters.</param>
        /// <param name="boolValue">The string value parameters.</param>
        /// <returns>The bool value.</returns>
        [HttpPost]
        [Authorization(CommerceRoles.Customer, CommerceRoles.Employee)]
        public async Task<bool> GetBoolValue(IEndpointContext context, string boolValue)
        {
            GetBoolValueResponse resp = await context.ExecuteAsync<GetBoolValueResponse>
                                       (new GetBoolValueRequest(boolValue)).ConfigureAwait(false);
            return resp.BoolValue;
        }


        
      /// <summary>
        /// The action to get the simple entity.
        /// </summary>
        /// <param name="context">The context parameters.</param>
        /// <param name="name">The name parameters.</param>
        /// <returns>The simple entity.</returns>
        [HttpPost]
        [Authorization(CommerceRoles.Customer, CommerceRoles.Employee)]
        public async Task<SimpleEntity> GetSimpleEntity(IEndpointContext context, string name)
        {
            GetSimpleEntityResponse resp = await context.ExecuteAsync<GetSimpleEntityResponse>
                                           (new GetSimpleEntityRequest(name)).ConfigureAwait(false);
            return resp.SimpleEntityObj;
        }
    }

```
The Retail server APIs support different authorization (roles), access to the controller method will be permitted based on the Authorization roles specified in the controller method Authorizations attribute.

Supported Authorization roles:

```C#

//
    // Summary:
    // Represents the type of logon type.
    [DataContract]
    public static class CommerceRoles
    {
        //
        // Summary:
        //     Anonymous Role.
        [DataMember]
        public const string Anonymous = "Anonymous";
        //
        // Summary:
        //     SharePoint Role used by Connector.
        [DataMember]
        public const string Storefront = "Storefront";
        //
        // Summary:
        //     Employee Role.
        [DataMember]
        public const string Employee = "Employee";
        //
        // Summary:
        //     Customer Role.
        [DataMember]
        public const string Customer = "Customer";
        //
        // Summary:
        //     Represents the Device level of authentication.
        [DataMember]
        public const string Device = "Device";
        //
        // Summary:
        //     Represents Application level of authentication.
        [DataMember]
        public const string Application = "Application";
        //
        // Summary:
        //     The list of all possible Microsoft.Dynamics.Commerce.Runtime.DataModel.CommerceRoles
        //     values.
        public static readonly string[] All;
    }

```

5.	Build the extension project, and drop the binary into the \RetailServer\webroot\bin\Ext folder.
6.	Update the Commerce Scale Unit web.config file in the \RetailServer\webroot folder by adding the new extension library name in the extensionComposition section.

```XML
<extensionComposition>
<!-- Please use fully qualified assembly names for ALL if you need to support loading from the Global Assembly Cache.
If you host in an application with a bin folder, this is not required. -->
<add source="assembly" value="SimpleExtensionSample" >
</extensionComposition>

```

7.	In Microsoft Internet Information Services (IIS), restart Commerce Scale Unit to load the new extension.
8.	To verify that the extension was successfully loaded, you can browse the RS metadata, and confirm that your entities and methods appear in the list.
To browse the metadata, open a URL in the following format in a web browser:
https://RS-URL/Commerce/$metadata
9.	To call the RS extension in your client, you must generate the Commerce proxy. You can then use the proxy to call your new RS APIs from the client.
