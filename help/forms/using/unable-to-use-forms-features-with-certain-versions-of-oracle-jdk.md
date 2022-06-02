---
title: Det går inte att använda Experience Manager Forms med vissa versioner av Oracle-JDK
seo-title: Unable to use Experience Manager Forms with certain versions of Oracle JDK
description: Det går inte att använda Experience Manager Forms med vissa versioner av Oracle-JDK
seo-description: Unable to use Experience Manager Forms with certain versions of Oracle JDK
source-git-commit: 91b012f8024350effc19613bcecfc42dee4130d9
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 3%

---

# Det går inte att använda Experience Manager Forms med vissa versioner av Oracle-JDK {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

Problemet gäller följande versioner:

* Experience Manager 6.3 Forms
* Experience Manager 6.4 Forms
* Experience Manager 6.5 Forms

## Problem {#issue}

Användaren stöter på följande undantag:
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## Orsak {#reason}

Undantaget inträffar när du kör Experience Manager Forms med Oracle JDK-version (Java Development Kit) som är större än eller lika med följande versioner:

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

Ovannämnda och senare versioner av Java innehåller nya XML-bearbetningsgränser i JVM (Java Virtual Machine) som gör att vissa Forms-specifika åtgärder misslyckas.

## Tillfällig lösning {#workaround}

1. Stoppa Experience Manager Forms Server.
1. Konfigurera följande JVM-argument för programservern:

   `-Djdk.xml.xpathExprOpLimit=2000`

   Den ställer in systemegenskapen i JVM till ett rimligt högt värde så att standardgränsen inte nås.

1. Starta Experience Manager Forms Server.
