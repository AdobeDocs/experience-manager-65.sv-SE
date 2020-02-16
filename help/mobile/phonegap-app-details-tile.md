---
title: Hantera apppanel
seo-title: Hantera apppanel
description: Följ den här sidan om du vill veta mer om Hantera apppanel på appinstrumentpanelen som gör det möjligt att ändra information om programmet.
seo-description: Följ den här sidan om du vill veta mer om Hantera apppanel på appinstrumentpanelen som gör det möjligt att ändra information om programmet.
uuid: bde75ecd-8694-427c-9b16-2c4ab2fd4d8b
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: a87834c9-247c-49fa-9978-a969230db91c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Hantera apppanel{#manage-app-tile}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Via **Hantera app** -panelen på appkontrollpanelen kan du ändra information om programmet. Om du vill öppna informationssidan klickar du på länken för information i panelen Hantera app. På sidan Hantera program kan du redigera inställningarna för PhoneGap Application Configuration (config.xml) och förbereda programmet för att skickas till olika programarkiv.

![chlimage_1-116](assets/chlimage_1-116.png)

## Om Hantera programpanel {#understanding-the-manage-app-tile}

Om du vill visa eller redigera information klickar du på&quot;..&quot; ( **Hantera app** -panel) kan du gå in i varje ruta i rutan Hantera app. i det nedre högra hörnet.

### Fliken Grundläggande {#the-basic-tab}

På den här fliken kan du redigera **appens namn**, **författare**, **kortbeskrivning** och **beskrivning** .

![chlimage_1-117](assets/chlimage_1-117.png)

### Fliken Avancerat {#the-advanced-tab}

Varje plattform för mobilapplikationer beskriver vilka data som samlas in, specifikt för varje applikationsbutik.

De plattformar som visas styrs av innehållet config.xml i PhoneGap:

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

Alla leverantörsapplikationsbutiker, t.ex. Apple App Store eller Google Play Store, kräver en eller flera skärmdumpar av mobilappen för att kunna visa din applikationsinformation för kunderna. Skärmbilderna kan ha strikta krav när det gäller dimensioner och innehåll (de måste egentligen representera programmet). AEM-appar har stöd för att välja och hantera skärmbilderna för de plattformar som stöds och visa de portdimensioner som krävs i respektive leverantörs programbutik.

>[!NOTE]
>
>Appen AEM Verify gör det möjligt att skicka skärmbilder direkt till appinformationen i AEM.
>
>Mer information finns i [Mobile Quickstart för AEM Verify](/help/mobile/phonegap-mobile-quickstart.md) .

![chlimage_1-118](assets/chlimage_1-118.png)

### Metadata {#metadata}

>[!NOTE]
>
>När du känner till **Hantera app** läser du [Redigera appmetadata](/help/mobile/phonegap-editmetadata.md) för att visa och redigera metadata.

#### Vanliga metadata {#common-metadata}

Alla program bör ha associerade metadata som hjälper dig att konfigurera olika aspekter av programmet. Sidan Hantera program är indelad i två olika områden som är relaterade till metadatainsamling. Plattformsspecifika metadata och vanliga metadata.

Det finns en gemensam konfiguration och metadata för alla plattformar.

I det här avsnittet definierar du URL:en för Content Update Server, landningssidan för ditt mobilprogram, PhoneGap-versionen för kompilering, programversion, namn, beskrivning och mer.

**Programversionen** är den fungerande versionen av ditt program. Det bästa sättet är att använda en 3-decimalteckning och börja under 1.0.0 före den första versionen.

**PhoneGap-versionen** är den version i vilken du vill kompilera programmet med PhoneGap. Bästa sättet är att hålla jämna steg med den aktuella versionen för att vara säker på att du får de senaste och bästa funktionerna och felkorrigeringarna.

**URL** för innehållsuppdateringsserver är den URL som programmet använder för att anropa ContentSync-uppdateringar. Den måste anges till din dispatcher-URL eller, om inte en dispatcher används, till en av dina publiceringsinstanser som ska användas för ContentSync-uppdateringar av programmet.

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>Det här avsnittet kan vara tomt om det inte finns data som fyller i fälten.
>
>Överst i detaljvyn visas programversion, PhoneGap-version och URL för uppdatering. Varje värde kan anges i avsnittet Vanliga metadata. Program-ID kan dock inte redigeras.

#### Plattformsmetadata {#platform-metadata}

Alla plattformar som definieras i PhoneGap config.xml kan innehålla anpassade plattformsegenskaper. En AEM-utvecklare måste bidra till innehållsstrukturen för att kunna hämta dessa egenskaper. Ett angivet exempel på plattformsspecifika egenskaper finns för iOS.

Metadata för alla konfigurerade plattformar visas nu samtidigt på fliken Avancerat i panelen Hantera program.

>[!NOTE]
>
>Plattformens metadataavsnitt används inte av PhoneGap under en CLI- eller Remote PhoneGap-version, utan istället försöker AEM hämta metadata för plattformar så att de kan användas senare när de skickas till målleverantörens programbutik.

För plattformar som inte kan förstås av AEM är det fortfarande möjligt för en AEM-utvecklare att utöka användargränssnittet för att hämta dessa metadata som senare kan exporteras och användas under ansökningsprocessen.

#### iOS-metadata {#ios-metadata}

Apple AppStore kräver ytterligare metadata för att du ska kunna skicka in programmet för distribution. Metadataavsnittet iOS försöker samla in den information som krävs och som kan användas av Apples iTMSTTransporter-verktyg för att publicera metadata till det associerade Apple-utvecklarkontot.

För att få tillgång till Apple-specifika metadata måste du först skapa programmet på [https://itunesconnect.apple.com](https://itunesconnect.apple.com/). När du skapar ditt program genererar Apple metadata, vilket krävs i iOS-metadataavsnittet, om du vill använda Apple iTMSTTransporter-verktyget för att validera och överföra metadata till itunesconnect.apple.com. Om du bara vill hämta metadata för att samla in behöver du inte nödvändigtvis fylla i i iOS-specifika metadata. Du kan fortfarande exportera metadata som sammanfogar iOS och vanliga metadata och samla alla skärmbilder i en ZIP-fil som du kan hämta när som helst.

Den hämtade zip-filen innehåller en itmsp-fil som kan inspekteras för metadata.xml. ActionScript-filen innehåller exporterade metadata (i filen metadata.xml), tillsammans med alla associerade skärmbilder.

Exportfunktionen används för att underlätta insamling av skärmbilder och metadata som kan skickas till programutgivaren för indata till den leverantörsspecifika programbutiken.

![chlimage_1-120](assets/chlimage_1-120.png)

#### Android-metadata {#android-metadata}

När du väljer Android-plattformen finns det inga anpassade metadata som kan ställas in. När du klickar på nedladdningsknappen som zip-fil skapas en egenskapsfil som innehåller alla metadata och associerade skärmbilder.

Exportfunktionen används för att underlätta insamling av skärmbilder och metadata som kan skickas till programutgivaren för indata till den leverantörsspecifika programbutiken.

![chlimage_1-121](assets/chlimage_1-121.png)

### URL för Content Update Server {#content-update-server-url}

En av de viktigaste funktionerna i AEM-appar är möjligheten att få ett mobilprogram att begära nytt innehåll via ContentSync, där innehållet kan vara HTML-resurser, sidor, video, bilder, text med mera. När en innehållsförfattare har uppdaterat innehållet och sedan publicerat det gör servern innehållsuppdateringen tillgänglig för det mobilprogram som ska laddas ned.

Egenskapen URL för Content Update Server är den URL som måste peka på en publiceringsinstans. antingen direkt eller via avsändaren eller CDN. Formatet på URL:en är helt enkelt:

`https://[hostname]:[port]`

>[!NOTE]
>
>Om din Author-serverinstans replikeras till flera publiceringsserverinstanser (gemensam arkitektur för AEM) får varje publiceringsserver samma uppdateringsinnehåll eftersom uppdateringen är baserad på författaren och replikerad till alla publiceringsinstanser. I princip stöds belastningsutjämning och failover fullt ut.

### Fliken Plugins {#the-plugins-tab}

Fliken **Plugins** beskriver de plugin-program som är associerade med din app. Den här informationen kommer att användas för att hämta rätt plugin-program under ett bygge.

![chlimage_1-122](assets/chlimage_1-122.png)

### Fliken Skärmbilder {#the-screenshots-tab}

På fliken **Skärmbilder** visas de skärmbildupplösningar som stöds på olika plattformar.

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>Mer information om hur du lägger till och tar bort skärmbilder finns i [Redigera appmetadata](/help/mobile/phonegap-editmetadata.md).

### Fliken Autentisering {#the-authentication-tab}

På fliken **Autentisering** kan du välja en OAuth-klient som ska associeras med ditt program och göra det möjligt för en utvecklare att använda OAuth-autentiseringen i Adobe Experience Manager.

![chlimage_1-124](assets/chlimage_1-124.png)

### Nästa steg {#the-next-steps}

När du har lärt dig mer om hur du hanterar apppaneler på programkontrollpanelen kan du läsa följande resurser för andra redigeringsroller:

* [Redigera appmetadata](/help/mobile/phonegap-editmetadata.md)
* [Programdefinitioner](/help/mobile/phonegap-app-definitions.md)
* [Skapa ett nytt program med guiden Skapa app](/help/mobile/phonegap-create-new-app.md)
* [Importera en befintlig hybridapp](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Innehållstjänster](/help/mobile/develop-content-as-a-service.md)

### Additional Resources {#additional-resources}

Mer information om roller och ansvar för en administratör och utvecklare finns i resurserna nedan:

* [Utveckla för Adobe PhoneGap Enterprise med AEM](/help/mobile/developing-in-phonegap.md)
* [Administrera innehåll för Adobe PhoneGap Enterprise med AEM](/help/mobile/administer-phonegap.md)

