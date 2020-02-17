---
title: Skapa och hantera appinnehåll
seo-title: Skapa och hantera appinnehåll
description: Att hantera appinnehåll kräver en gemensam insats från utvecklare, innehållsförfattare och administratörer.  Författare hanterar sidor, som i sin tur är baserade på mallar och komponenter som genererats av apputvecklare.
seo-description: Att hantera appinnehåll kräver en gemensam insats från utvecklare, innehållsförfattare och administratörer.  Författare hanterar sidor, som i sin tur är baserade på mallar och komponenter som genererats av apputvecklare.
uuid: ca049bad-9be8-47aa-b010-298258feda26
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 5c8971ab-b07c-4131-b4cb-f34c52425014
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Skapa och hantera appinnehåll{#creating-and-managing-app-content}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Att hantera appinnehåll kräver en gemensam insats från [utvecklare](#developer), [författare](#author) och [administratörer](#administrator). Författare hanterar sidor, som i sin tur är baserade på mallar och komponenter som genererats av apputvecklare.

Slutligen publicerar administratörer det uppdaterade programinnehållet strategiskt.

>[!NOTE]
>
>**Krav**:
>
>Vid [driftsättning och underhåll](/help/sites-deploying/deploy.md)bekantades utvecklarna med AEM:s system med komponenter och mallar.

## Panelen Hantera sidinnehåll {#the-manage-page-content-tile}

>[!CAUTION]
>
>Om du inte använder en färdig appmall måste du konfigurera en Content Sync-hanterare för att kunna aktivera nytt appinnehåll för publicering.
>
>Mer information finns i avsnittet [Mobil med innehållssynkronisering](/help/mobile/phonegap-contentsync.md) i Developer&#39;s.

Här kan du skapa, redigera och ta bort innehåll i AEM Mobile på ungefär samma sätt som i AEM Sites.

I rutan **** Hantera sidinnehåll visas antalet sidor med hanterat innehåll och senast ändrade för en viss nyttolast. Du kan fördjupa innehållet för att skapa, kopiera, flytta, ta bort och uppdatera sidor genom att klicka på varje post i rutan.

När innehållet har uppdaterats kan administratörer publicera en nyttolast för innehållsuppdatering Over-the-Air (OTA) till kunder via panelen **Hantera innehållspaket.**

![chlimage_1-161](assets/chlimage_1-161.png)

Välj något av innehållspaketen i listan om du vill skapa eller redigera innehåll, till exempel skapa, redigera eller ta bort sidor, ändra navigerings- och sidordning, skapa eller uppdatera innehåll som text och media.

Observera att *allt är innehåll*, vilket innebär att programformat, text, media, sidor, navigering och målgruppsanpassning för innehåll kan redigeras och uppdateras i OTA, utan att man behöver besöka en app-butik.

*För att kunna redigera AEM Mobile-innehåll behöver AEM-författare *en god förståelse för AEM:s gränssnitt för innehållsredigering: Skapa [sidor i AEM.](/help/sites-authoring/qg-page-authoring.md)

## Panelen Hantera innehållspaket {#the-manage-content-packages-tile}

Här kan *AEM-administratörer* snabbt och enkelt uppdatera sina appar för att leverera engagerande upplevelser och aktuellt innehåll som ökar varumärkesengagemanget och uppfyller affärsmålen utan att behöva skicka in något nytt till utvecklare eller appbutiker.

![chlimage_1-162](assets/chlimage_1-162.png)

När *AEM-författare* har lagt till eller ändrat innehåll via panelen Hantera innehåll kan *AEM-administratörer* skicka ut ändringarna till kunder med en innehållspaketuppdatering.

Med åtgärden Innehållspaket kan *AEM Author* skapa och redigera sidinnehåll medan utvecklingsteamet gör ändringar i utformningen och implementeringen av ett värdprogram, inklusive navigering, format, logik på serversidan, mallar och komponenter, och sedan skickar ut ändringarna till kunder utan att behöva skicka in dem till olika butiker för distribution igen.

**Publicera nytt eller uppdaterat innehåll**

Välj ett innehållspaket i rutan, i det här exemplet det engelska paketet. Observera att en dialogruta för innehållsuppdatering innehåller information om den aktuella konfigurationen för *innehållssynkronisering* . Om appinnehåll har ändrats sedan en tidigare uppdatering visas statusen *Väntande*, enligt nedan.

![chlimage_1-163](assets/chlimage_1-163.png)

Välj sedan **scenåtgärden** längst upp till höger för att skapa den nya innehållsuppdateringen. Lägg till rätt uppdateringsinformation och tryck på Klar.

![chlimage_1-164](assets/chlimage_1-164.png)

Hanteraren för *innehållssynkronisering* skapar sedan de nödvändiga paketen genom att bilda en delta (ett paket med *endast* det som har ändrats). När det är klart har uppdateringsinnehållspaketet mellanlagrats enligt nedan.

Genom att mellanlagra en uppdatering av innehållet kan flera uppdateringar göras innan de publiceras till OTA för mobila enheter.

>[!NOTE]
>
>Det mellanlagrade innehållet kan verifieras med appen AEM Verify innan det publiceras.
>
>Se [Mobile Quickstart för AEM Verify](/help/mobile/phonegap-mobile-quickstart.md) för mer information om appen AEM Verify.

![chlimage_1-165](assets/chlimage_1-165.png)

När du är redo att leverera nytt innehåll till appanvändarna med Content Sync OTA väljer du **Publicera** enligt nedan.

![chlimage_1-166](assets/chlimage_1-166.png)

### Nästa steg {#the-next-steps}

När du har lärt dig mer om att skapa och hantera appinnehåll i programkontrollpanelen kan du läsa följande resurser för andra redigeringsroller:

* [Hantera programpanel](/help/mobile/phonegap-app-details-tile.md)
* [Redigera appmetadata](/help/mobile/phonegap-editmetadata.md)
* [Programdefinitioner](/help/mobile/phonegap-app-definitions.md)
* [Skapa ett nytt program med guiden Skapa app](/help/mobile/phonegap-create-new-app.md)
* [Importera en befintlig hybridapp](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Additional Resources {#additional-resources}

Mer information om roller och ansvar för en administratör och utvecklare finns i resurserna nedan:

* [Utveckla för Adobe PhoneGap Enterprise med AEM](/help/mobile/developing-in-phonegap.md)
* [Administrera innehåll för Adobe PhoneGap Enterprise med AEM](/help/mobile/administer-phonegap.md)
