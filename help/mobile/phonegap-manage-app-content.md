---
title: Skapa och hantera appinnehåll
description: Att hantera appinnehåll kräver en gemensam insats från utvecklare, innehållsförfattare och administratörer. Författarna hanterar sidor, som bygger på mallar och komponenter som genereras av apputvecklare.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 9d350935-129a-40d3-89f4-2e6f69676e5e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 1%

---

# Skapa och hantera appinnehåll{#creating-and-managing-app-content}

{{ue-over-mobile}}

Hantering av appinnehåll kräver en gemensam åtgärd från [utvecklare](#developer), innehållsförfattare[författare](#author) och [administratörer](#administrator). Författarna hanterar sidor, som bygger på mallar och komponenter som genereras av apputvecklare.

Slutligen publicerar administratörer det uppdaterade programinnehållet strategiskt.

>[!NOTE]
>
>**Förutsättning**:
>
>I [Distribuera och underhålla](/help/sites-deploying/deploy.md) kände utvecklarna till systemkomponenter och mallar i Adobe Experience Manager (AEM).

## Panelen Hantera sidinnehåll {#the-manage-page-content-tile}

>[!CAUTION]
>
>Om du inte använder en färdig programmall måste du konfigurera en Content Sync-hanterare för att kunna publicera nytt appinnehåll på OTA.
>
>Mer information finns i avsnittet [Mobil med innehållssynkronisering](/help/mobile/phonegap-contentsync.md) i utvecklarens avsnitt.

Här kan du skapa, redigera och ta bort innehåll i AEM Mobile på ungefär samma sätt som i AEM Sites.

På **panelen Hantera sidinnehåll** visas antalet sidor med hanterat innehåll och senast ändrade sidor för en viss nyttolast. Du kan fördjupa innehållet för att skapa, kopiera, flytta, ta bort och uppdatera sidor genom att klicka på varje post i rutan.

När innehållet har uppdaterats kan administratörer publicera en nyttolast för innehållsuppdatering via AIR (OTA) till kunder via panelen **Hantera innehållspaket.**

![chlimage_1-161](assets/chlimage_1-161.png)

Välj något av innehållspaketen i listan om du vill skapa eller redigera innehåll, till exempel skapa, redigera eller ta bort sidor, ändra navigerings- och sidordning, skapa eller uppdatera innehåll som text och media.

Obs! *Allt är innehåll*, vilket innebär att programformat, kopia (text), media, sidor, navigering och målanpassning av innehåll kan redigeras och uppdateras i OTA, utan att du behöver besöka en appbutik.

För att redigera AEM Mobile-innehåll behöver *AEM författare *en god förståelse för AEM gränssnitt för redigering av innehåll: [Redigeringssidor i AEM.](/help/sites-authoring/qg-page-authoring.md)

## Panelen Hantera innehållspaket {#the-manage-content-packages-tile}

Här kan *AEM administratörer* snabbt och enkelt uppdatera sina appar för att leverera engagerande upplevelser och aktuellt innehåll som ökar varumärkesengagemanget och uppfyller affärsmålen utan att behöva skicka in något nytt till utvecklare eller appbutiker.

![chlimage_1-162](assets/chlimage_1-162.png)

När *AEM författare* har lagt till eller ändrat innehåll via panelen Hantera innehåll kan *AEM Administratörer* skicka ut ändringarna till kunder med en innehållspaketuppdatering.

Med åtgärden Innehållspaket kan *AEM författare* skapa och redigera sidinnehåll medan utvecklingsteamet gör ändringar i en värdprogramdesign och implementering, inklusive navigering, format, logik på serversidan, mallar och komponenter, och sedan skickar ut ändringarna till kunder utan att behöva skicka in dem till olika butiker för distribution igen.

**Så här publicerar du nytt eller uppdaterat innehåll**

Välj ett innehållspaket i rutan, i det här exemplet det engelska paketet. Observera att en dialogruta för innehållsuppdatering visar den relevanta konfigurationen för *Innehållssynkronisering*. Om appinnehåll har ändrats sedan en tidigare uppdatering visas statusen *Väntande* enligt nedan.

![chlimage_1-163](assets/chlimage_1-163.png)

Välj sedan åtgärden **Stage** längst upp till höger för att skapa innehållsuppdateringen. Lägg till rätt uppdateringsinformation och tryck på Klar.

![chlimage_1-164](assets/chlimage_1-164.png)

Hanteraren *Innehållssynkronisering* skapar sedan de nödvändiga paketen genom att skapa en delta (ett paket med *endast* som har ändrats). När det är klart har uppdateringsinnehållspaketet mellanlagrats enligt nedan.

Genom att mellanlagra en uppdatering av innehållet kan flera uppdateringar göras innan de publiceras till OTA för mobila enheter.

>[!NOTE]
>
>Det mellanlagrade innehållet kan verifieras med AEM Verifiera-appen före publicering.
>
>Se [Mobile Quickstart för AEM Verify](/help/mobile/phonegap-mobile-quickstart.md) för mer information om AEM Verifiera app.

![chlimage_1-165](assets/chlimage_1-165.png)

När du är redo att leverera nytt innehåll till appanvändarna med OTA för innehållssynkronisering väljer du **Publish** enligt nedan.

![chlimage_1-166](assets/chlimage_1-166.png)

### Nästa steg {#the-next-steps}

När du har lärt dig mer om att skapa och hantera appinnehåll i programkontrollpanelen kan du läsa följande resurser för andra redigeringsroller:

* [Hantera programpanel](/help/mobile/phonegap-app-details-tile.md)
* [Redigera appmetadata](/help/mobile/phonegap-editmetadata.md)
* [Programdefinitioner](/help/mobile/phonegap-app-definitions.md)
* [Skapa ett nytt program med guiden Skapa app](/help/mobile/phonegap-create-new-app.md)
* [Importera en befintlig hybridapp](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Ytterligare resurser {#additional-resources}

Mer information om roller och ansvar för en administratör och utvecklare finns i resurserna nedan:

* [Utveckla för Adobe PhoneGap Enterprise med AEM](/help/mobile/developing-in-phonegap.md)
* [Administrera innehåll för Adobe PhoneGap Enterprise med AEM](/help/mobile/administer-phonegap.md)
