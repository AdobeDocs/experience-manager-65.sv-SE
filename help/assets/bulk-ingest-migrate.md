---
title: Installerar funktionspaket 18912 för migrering av gruppresurser
description: Med funktionspaketet 18912 kan du antingen importera resurser gruppvis via FTP eller migrera resurser från Dynamic Media Classic till Dynamic Media AEM. Detta tillvalspaket finns tillgängligt från Adobe support.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
translation-type: tm+mt
source-git-commit: d6ae8bffa2d9d59f5656b9344d8826128f12885c
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 1%

---


# Installerar funktionspaket 18912 för migrering av gruppresurser{#installing-feature-pack-for-bulk-asset-migration}

Installationen av funktionspaket 18912 är *valfri*.

Med funktionspaket 18912 kan du antingen importera resurser i bulk direkt till Dynamic Media - Scene7-läge AEM via FTP, eller migrera resurser från Dynamic Media Classic till Dynamic Media - Scene7-läge på AEM. Funktionspaketet är tillgängligt från [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

>[!NOTE]
>
>Du kan använda funktionspaketet för att massmigrera resurser på egen hand från Dynamic Media Classic till Dynamic Media - Scene 7 i AEM eller massmigrera resurser med FTP-funktionen i Dynamic Media Classic, men Adobe rekommenderar *inte* den här metoden på grund av komplexiteten.
>
>Det innebär att paket med flyttningsfunktioner, som detta, endast *stöds* som en del av ett migreringsprojekt när de görs via [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

Innan du kan installera funktionspaketet måste du först skapa en tjänstanvändare och ange den informationen till Adobe support.

Se även [Konfigurera dynamiska media - Scene7-läge](/help/assets/config-dms7.md).

**Så här installerar du funktionspaket 18912 för migrering av gruppresurser**

1. I AEM går du till **[!UICONTROL Tools > Security > Users]** och väljer **[!UICONTROL Create User]**. Den här tjänstanvändaren måste ha *läs/skriv*-behörighet för `/content/dam.`
1. I fälten **[!UICONTROL ID]** och **[!UICONTROL Password]** anger du ett användarnamn och lösenord; till exempel **FTP-användare**. Det här namnet visas på tidslinjen som den användare som skapade resursen. När en resurs överförs från FTP betraktas en resurs som skapad när den överförs till FTP-servern och skickas till AEM.
1. Kontakta [Adobe Enterprise Customer Care för Experience Manager](https://helpx.adobe.com/se/contact/enterprise-support.ec.html) för att få tillgång till funktionspaket 18912 för nedladdning. Du kan behöva följande information när du kontaktar supporten:

   * Serverns IP-adress för din Author-instans, inklusive portnumret (portnumret är som standard 4502.)
   * AEM användarnamn och lösenord från föregående steg.

1. Adobe Enterprise Customer Care for AEM ger dig FTP-inloggningsuppgifter och tillgång till funktionspaket 18912.
1. Installera funktionspaketet när du får funktionspaketet 18912.

   Mer information om hur du använder programdistribution och paket i AEM finns i [Arbeta med paket](/help/sites-administering/package-manager.md).
