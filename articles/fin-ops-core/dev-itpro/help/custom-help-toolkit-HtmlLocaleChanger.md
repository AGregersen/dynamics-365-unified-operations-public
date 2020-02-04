---
# required metadata

title: Custom Help Toolkit
description: This topic describes the components in the custom help toolkit for Finance and Operations apps. 
author: edupont04
manager: AnnBe
ms.date: 01/14/2020
ms.topic: article
ms.service: dynamics-ax-platform

# optional metadata

# ms.search.form: 
# ROBOTS: 
audience: IT Pro
# ms.devlang: 
ms.reviewer: tfehr
ms.search.scope: Core, Operations
# ms.tgt_pltfrm: 
# ms.custom: 
# ms.assetid: 
ms.search.region: Global
# ms.search.industry: 
ms.author: edupont
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: Operations

---

# Custom Help Toolkit: The HTML Locale Changer tool

[!include [banner](../includes/banner.md)]

The custom help toolkit includes the **HTML Locale Changer** tool that you can use to process HTML files that are generated with the [HTML From Repos Generator tool](custom-help-toolkit-HtmlFromRepoGenerator.md) for further processing.  


## <a name="htmllocale"></a>Use the HTML Locale Changer tool to align locales

The **HTML Locale Changer** tool can update your HTML files with a new value for *ms.locale*. For example, if you have HTML files for German (Germany) and you want to make the same content available in German (Austria), then you can run the tool to change the setting from *ms.locale: de-de* to *ms.locale:de-at*.  

Here is the syntax for HtmlLocaleChanger.exe:  

```
HtmlLocaleChanger.exe -h <path> -v <true|false>
```

Here is an explanation of the parameters:

|Parameter   |Description  |
|------------|-------------|
|h|Specifies the path to the HTML files that you want to process. |
|v|True to enable verbose logging; otherwise false.|

### Examples

The following example changes the locale <!--from *de-de* to *de-at*--> with verbose logging:

```
HtmlLocaleChanger.exe -h D:\D365-Operations\de -v
```

## See also

[Deploying Custom Help](deploy.md)  
[Example of Deploying Custom Help on Azure](walkthrough-help-azure.md)  
[Language and locale descriptors in across product and Help](language-locale.md)  
[Convert Dynamics AX custom Help for use in Dynamics 365](migrate-dynamicsax2012.md)  
