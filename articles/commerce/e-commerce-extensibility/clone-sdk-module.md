---
# required metadata

title: Modify a starter kit module
description: This topic provides information about the set of starter kit modules that the Microsoft Dynamics 365 for Commerce e-Commerce software development kit (SDK) includes for use on an e-Commerce site.
author: SamJarawan
manager: annbe
ms.date: 08/30/2019
ms.topic: article
ms.prod: 
ms.service: Dynamics365Operations
ms.technology: 

# optional metadata

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
# Modify a starter kit module

The Microsoft Dynamics 365 for Commerce e-Commerce SDK includes a set of starter kit modules that can be used on an e-Commerce site. Although these modules can't be modified directly, they can be cloned into a new module and then changed.

To clone a module and change it, use the **yarn msdyn365 clone SDK\_MODULE\_NAME NEW\_MODULE\_NAME** command-line interface (CLI) command. In this command, **SDK\_MODULE\_NAME** is the name of the module that you want to modify, and **NEW\_MODULE\_NAME** is the name of the new module. This command adds the source code for the module to the /src/modules/ directory and pulls in any required dependencies for the module.

The following example shows the command that is used to clone the **hero** SDK module so that you can change it.

```
yarn msdyn365 clone hero heroV2
```

It can take one to two minutes to clone the module, because all the dependencies must be pulled down. After the command has finished running, you can find the new module in the \\src\\modules\\ directory.

## Preview a module

To preview the new module in a local web browser, follow these steps.

1. At a command prompt, open the app, go to your root SDK folder, and run the **yarn start** command. Here is an example.

    ```
    c:\repos\MyEcommerceSite\yarn start
    ```

2. Open the following URL in a web browser: `https://localhost:4000/modules?type=heroV2`. Notice the module name in the **"type=MODULE\_NAME"** query string parameter.

You can now change the module code as you require.
