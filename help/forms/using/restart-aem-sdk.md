---
title: Hur startar jag om AEM SDK?
description: De bästa sätten att starta om AEM SDK
role: Admin, Developer, User
feature: Adaptive Forms
source-git-commit: 5a8c0ce8c5c764bb7eeeb645527dbde6ccace497
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Starta om AEM SDK

Om du startar om AEM SDK genom att stoppa Java™-processerna kan det leda till inkonsekvenser i den AEM utvecklingsmiljön. Ett fel inträffar enligt följande:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Restart-aem-sdk-error](/help/forms/using/assets/restart-sdk-error.png)

## Lösning

Om du vill starta om AEM SDK går du till det aktiva kommandofönstret och trycker på `Ctrl + C` för att starta om SDK.

Du bör använda kommandot Ctrl + C för att starta om SDK:n. Om du startar om AEM SDK med alternativa metoder, till exempel genom att stoppa Java™-processer, kan det leda till inkonsekvenser i den AEM utvecklingsmiljön.
