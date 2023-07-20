---
title: Installera funktionspaket 18912 för migrering av gruppresurser
description: Med funktionspaketet 18912 kan du antingen importera stora mängder mediefiler via FTP eller migrera mediefiler från Dynamic Media Classic till Dynamic Media på Adobe Experience Manager. Detta tillvalspaket finns tillgängligt från Adobe support.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: fc148a5f5e0fcaac2980dc73004fa92ac3b91fb3
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# Installera funktionspaket 18912 för migrering av gruppresurser{#installing-feature-pack-for-bulk-asset-migration}

Installation av funktionspaket 18912 är *valfri*.

Med funktionspaketet 18912 kan du massimportera mediefiler direkt till Dynamic Media - Scene7-läget i Adobe Experience Manager via FTP. Du kan också migrera resurser från Dynamic Media Classic till Dynamic Media - Scene7-läge på Experience Manager. Funktionspaketet är tillgängligt från [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>Du kan använda funktionspaketet för att massmigrera resurser på egen hand från Dynamic Media Classic till Dynamic Media - Scene7 i Experience Manager. Du kan också massmigrera resurser med FTP-funktionen i Dynamic Media Classic. Adobe har dock *not* rekommenderar att du använder någon av dessa metoder på grund av komplexiteten.
>
>Det här paketet med flyttningsfunktioner är *endast* stöds som en del av ett migreringsprojekt när det görs via [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Innan du installerar funktionspaketet skapar du en tjänstanvändare och skickar informationen till Adobe support.

Se även [Konfigurera Dynamic Media - Scene7-läge](/help/assets/config-dms7.md).

**Så här installerar du funktionspaket 18912 för migrering av gruppresurser:**

1. Gå till Experience Manager **[!UICONTROL Tool]** > **[!UICONTROL Security]** > **[!UICONTROL Users]** och markera **[!UICONTROL Create User]**. Den här tjänstanvändaren måste ha *läsa/skriva* behörigheter till `/content/dam.`
1. I **[!UICONTROL ID]** och **[!UICONTROL Password]** fält, ange användarnamn och lösenord, till exempel **FTP-användare**. Det här namnet visas på tidslinjen som den användare som skapade resursen. När en resurs överförs från FTP betraktas en resurs som skapad när den överförs till FTP-servern och överförs till Experience Manager.
1. Kontakt [Adobe kundsupport för Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support) för att begära åtkomst till funktionspaketet 18912 för nedladdning. Du kan behöva följande information när du kontaktar supporten:

   * Serverns IP-adress för din Author-instans, inklusive portnumret (portnumret är som standard 4502.)
   * Användarnamn och lösenord för Experience Manager-tjänsten från föregående steg.

1. Adobe kundsupport för Experience Manager ger dig FTP-inloggningsuppgifter och tillgång till funktionspaket 18912.
1. Installera funktionspaketet när du får funktionspaketet 18912.

   Se [Arbeta med paket](/help/sites-administering/package-manager.md) för mer information om hur du använder programvarudistribution och paket i Experience Manager.
