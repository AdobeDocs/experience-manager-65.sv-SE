---
title: Körning av flera tjänster trots att AEM Forms inte har startat.
description: Även om AEM Forms inte har startat helt, så behandlas flera tjänster.
source-git-commit: 6b24067c1808475044a612f21d5d4d2793c13e17
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Körning av flera tjänster trots att AEM Forms inte har startat helt{#steps-to-resolve-error-after-installing-service-pack}


## Problem {#issue}

När användaren startar om AEM Forms fortsätter de aktuella samtalsprocesserna, till exempel återgivning av PDF-dokument. Detta gör att omstarten av AEM Forms-servern inte startar korrekt.

## Gäller för {#applies-to}

Lösningen gäller AEM Forms på JEE Server och AEM Forms på OSGi Server.

## Lösning {#solution}

För att lösa problemet lägger användarna till ett argument `Dcom.adobe.livecycle.dsc.deferServiceStart=true` till [gruppfil](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) när servern startas.





