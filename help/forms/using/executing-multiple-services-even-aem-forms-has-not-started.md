---
title: Körning av flera tjänster trots att AEM Forms inte har startat.
description: Även om AEM Forms inte har startat helt, så behandlas flera tjänster.
exl-id: 4ec40412-15b1-434b-a919-2cf23f48077c
source-git-commit: faa628ac4a4631564141f68f3efc9d69a67e5c40
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Körning av flera tjänster trots att AEM Forms inte har startat helt{#steps-to-resolve-error-after-installing-service-pack}


## Problem {#issue}

När användaren startar om AEM Forms fortsätter de aktuella samtalsprocesserna, till exempel återgivning av PDF-dokument. Detta gör att omstarten av AEM Forms-servern inte startar korrekt.

## Gäller för {#applies-to}

Lösningen gäller AEM Forms på JEE Server och AEM Forms på OSGi Server.

## Lösning {#solution}

Lös problemet genom att lägga till ett argument `Dcom.adobe.livecycle.dsc.deferServiceStart=true` till [gruppfil](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) när servern startas.
