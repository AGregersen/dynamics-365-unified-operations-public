---
# required metadata

title: Container modules
description: This topic provides information about container modules in Microsoft Dynamics 365 for Commerce. Container modules can help control the layout when complex modules or pages are built out of small component modules.
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
# Container modules

Container modules can help you control the layout when you build complex modules or pages out of small component modules. For example, a container module might be a header, footer, or buy box module that has nested modules inside it.

Container modules can define "slots" that are surfaced to template authors. You can think of slots as regions inside the container module. Page authors can configure which modules go into each slot. The code of the container module is responsible for the HTML layout of the slots.

Configuration settings can also be exposed to page authors. In this way, page authors can do additional configuration of the layout of container modules. The container module is responsible for building a responsive design. A responsive design helps guarantee that the module will look good at any size, regardless of whether it's viewed on a mobile device screen or in a full web browser.

Container modules are created just like regular modules. However, in the MODULE\_NAME.definition.json file, you must change the **$type** value as shown here.

```
"$type": "containerModule"
```

There are two types of container modules: layout container modules and page container modules.

## Layout container modules

Layout container modules are useful when you must make a complex module out of multiple simple modules, and you want to control the layout of those simple modules. For example, you can use a header layout container module that is made up of required or optional sub-modules, such as search, sign-in, and navigation modules. The purpose of the layout container is to provide an adaptive layout.

## Page container modules

Page container modules contain the core structure for page authoring. For example, you can create a page container where slots are defined for the header area, main content area, and footer area. A page container is just a module that controls the layout of a set of named slots. A page container can be embedded only at the root of a page. Each page must have only one page container. This page container is defined in the master template.

Like layout container modules, page container modules can define named slots that are surfaced to template authors. Page authors can configure which modules go into each slot, and the rendering code for the container controls the layout of those slots. Configuration settings can also be exposed to page authors, so that they can do additional configuration of the layout.
