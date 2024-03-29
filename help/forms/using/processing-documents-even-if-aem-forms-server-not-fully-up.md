---
title: AEM Forms Server börjar bearbeta dokumenten även innan alla tjänster är igång.
description: AEM Forms Server börjar bearbeta dokumenten redan innan alla tjänster är igång på JEE Server och OSGi Server.
exl-id: 1a1bc1cb-e0ce-49a0-9b05-ae59f900cfb2
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# AEM Forms Server börjar bearbeta dokumenten även innan alla tjänster är igång{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## Problem {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

Innan AEM Forms Server är helt igång och alla program körs börjar AEM Forms Server bearbeta dokumenten.


## Gäller för {#applies-to}

Lösningen gäller AEM Forms på JEE Server och AEM Forms på OSGi Server.

## Lösning {#solution}

Lös problemet genom att lägga till ett argument `Dcom.adobe.livecycle.dsc.deferServiceStart=true` till [gruppfil](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) när servern startas.
