---
title: Hantera apppanel
seo-title: Manage App Tile
description: Följ den här sidan om du vill veta mer om Hantera apppanel på appinstrumentpanelen som gör det möjligt att ändra information om programmet.
seo-description: Follow this page to learn about the Manage App Tile on the app dashboard that provides the ability to modify details about the Application.
uuid: bde75ecd-8694-427c-9b16-2c4ab2fd4d8b
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: a87834c9-247c-49fa-9978-a969230db91c
exl-id: 8bcf70ef-94d2-4958-90b5-bc375b360916
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 0%

---

# Hantera apppanel{#manage-app-tile}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

The **Hantera program** På panelen App Dashboard kan du ändra information om programmet. Om du vill öppna informationssidan klickar du på länken för information i panelen Hantera app. På sidan Hantera program kan du redigera inställningarna för PhoneGap Application Configuration (config.xml) och förbereda programmet för att skickas till olika programarkiv.

![chlimage_1-116](assets/chlimage_1-116.png)

## Om Hantera programpanel {#understanding-the-manage-app-tile}

Du kan gå på djupet i varje ruta i **Hantera program** om du vill visa eller redigera detaljer genom att klicka på ... i det nedre högra hörnet.

### Fliken Grundläggande {#the-basic-tab}

Du kan redigera **Namn**, **Upphovsman**, **Kort beskrivning** och **Beskrivning** för din app från den här fliken.

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

Alla leverantörsapplikationsbutiker, t.ex. Apple App Store eller Google Play Store, kräver en eller flera skärmdumpar av mobilappen för att kunna visa din applikationsinformation för kunderna. Skärmbilderna kan ha strikta krav när det gäller dimensioner och innehåll (de måste egentligen representera programmet). AEM Apps har stöd för att välja och hantera skärmbilderna för de plattformar som stöds och visa de portdimensioner som krävs i respektive leverantörs programbutik.

>[!NOTE]
>
>Med appen AEM Verifiera kan du skicka skärmbilder direkt till din appinformation i AEM.
>
>Se [Mobile Quickstart för AEM verifiera](/help/mobile/phonegap-mobile-quickstart.md) för mer information.

![chlimage_1-118](assets/chlimage_1-118.png)

### Metadata {#metadata}

>[!NOTE]
>
>När du känner till **Hantera program** platta, se [Redigera appmetadata](/help/mobile/phonegap-editmetadata.md) för att visa och redigera metadata.

#### Vanliga metadata {#common-metadata}

Alla program bör ha associerade metadata som hjälper dig att konfigurera olika aspekter av programmet. Sidan Hantera program är indelad i två olika områden som är relaterade till metadatainsamling. Plattformsspecifika metadata och vanliga metadata.

Det finns en gemensam konfiguration och metadata för alla plattformar.

I det här avsnittet definierar du URL:en för Content Update Server, landningssidan för ditt mobilprogram, PhoneGap-versionen för kompilering, programversion, namn, beskrivning och mer.

**App-version** är programmets arbetsversion. Det bästa sättet är att använda en 3-decimalteckning och börja under 1.0.0 före den första versionen.

**PhoneGap-version** är den version i vilken du vill kompilera programmet med PhoneGap. Bästa sättet är att hålla jämna steg med den aktuella versionen för att vara säker på att du får de senaste och bästa funktionerna och felkorrigeringarna.

**URL för Content Update Server** är den URL som ditt program använder för att anropa ContentSync-uppdateringar. Den måste anges till din dispatcher-URL eller, om inte en dispatcher används, till en av dina publiceringsinstanser som ska användas för ContentSync-uppdateringar av programmet.

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>Det här avsnittet kan vara tomt om det inte finns data som fyller i fälten.
>
>Överst i detaljvyn visas programversion, PhoneGap-version och URL för uppdatering. Varje värde kan anges i avsnittet Vanliga metadata. Program-ID kan dock inte redigeras.

#### Plattformsmetadata {#platform-metadata}

Alla plattformar som definieras i PhoneGap config.xml kan innehålla anpassade plattformsegenskaper. En AEM måste bidra med innehållsstrukturen för att kunna hämta dessa egenskaper. Ett exempel på plattformsspecifika egenskaper finns för iOS.

Metadata för alla konfigurerade plattformar visas nu samtidigt på fliken Avancerat i panelen Hantera program.

>[!NOTE]
>
>Plattformens metadataavsnitt används inte av PhoneGap under en CLI- eller Remote PhoneGap-version, utan AEM försöker hämta metadata för plattformar så att de kan användas senare när de skickas till målleverantörens programbutik.

För plattformar som inte AEM förstår går det fortfarande att utöka användargränssnittet för att hämta metadata som senare kan exporteras och användas under programinlämningsprocessen.

#### iOS-metadata {#ios-metadata}

Apple AppStore kräver ytterligare metadata för att du ska kunna skicka in programmet för distribution. iOS metadataavsnitt försöker samla in den information som Apple iTMSTTransporter-verktyg kan använda för att publicera metadata på det associerade Apple-utvecklarkontot.

För att få tillgång till de Apple-specifika metadata måste du först skapa ditt program på [https://itunesconnect.apple.com](https://itunesconnect.apple.com/). När du skapar ditt program genererar Apple metadata, vilket krävs i metadataavsnittet för iOS, om du vill använda verktyget Apple iTMSTTransporter för att validera och överföra metadata till itunesconnect.apple.com. Om du bara vill få fram metadata för att samla in behöver du inte nödvändigtvis fylla i iOS-specifika metadata. Du kan fortfarande exportera metadata som sammanfogar iOS-metadata och gemensamma metadata och samla alla skärmbilder i en zip-fil som kan laddas ned när som helst.

Den hämtade zip-filen innehåller en itmsp-fil som kan inspekteras för metadata.xml. ActionScript-filen innehåller exporterade metadata (i filen metadata.xml), tillsammans med alla associerade skärmbilder.

Exportfunktionen används för att underlätta insamling av skärmbilder och metadata som kan skickas till programutgivaren för indata till den leverantörsspecifika programbutiken.

![chlimage_1-120](assets/chlimage_1-120.png)

#### Android-metadata {#android-metadata}

När du väljer Android-plattformen finns det inga anpassade metadata som kan ställas in. När du klickar på nedladdningsknappen som zip-fil skapas en egenskapsfil som innehåller alla metadata och associerade skärmbilder.

Exportfunktionen används för att underlätta insamling av skärmbilder och metadata som kan skickas till programutgivaren för indata till den leverantörsspecifika programbutiken.

![chlimage_1-121](assets/chlimage_1-121.png)

### URL för Content Update Server {#content-update-server-url}

En av de viktigaste funktionerna i AEM är möjligheten att låta ett mobilprogram begära nytt innehåll via ContentSync, där innehållet kan vara HTML-resurser, sidor, video, bilder, text och mycket mer. När en innehållsförfattare har uppdaterat innehållet och sedan publicerat det gör servern innehållsuppdateringen tillgänglig för det mobilprogram som ska laddas ned.

Egenskapen URL för Content Update Server är den URL som måste peka på en publiceringsinstans. antingen direkt eller via avsändaren eller CDN. Formatet på URL:en är helt enkelt:

`https://[hostname]:[port]`

>[!NOTE]
>
>Om din Author-serverinstans replikeras till flera publiceringsserverinstanser (gemensam arkitektur för AEM) får varje publiceringsserver samma uppdateringsinnehåll eftersom uppdateringen är baserad på författaren och replikerad till alla publiceringsinstanser. I princip stöds belastningsutjämning och failover fullt ut.

### Fliken Plugins {#the-plugins-tab}

The **Plugins** beskriver de plugin-program som är associerade med din app. Den här informationen kommer att användas för att hämta rätt plugin-program under ett bygge.

![chlimage_1-122](assets/chlimage_1-122.png)

### Fliken Skärmbilder {#the-screenshots-tab}

The **Skärmbilder** På -fliken visas de skärmbildupplösningar som stöds på olika plattformar.

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>Information om hur du lägger till och tar bort skärmbilder finns i [Redigera appmetadata](/help/mobile/phonegap-editmetadata.md).

### Fliken Autentisering {#the-authentication-tab}

The **Autentisering** På -fliken kan du välja en OAuth-klient som ska associeras med ditt program och göra det möjligt för en utvecklare att använda Adobe Experience Manager OAuth-autentisering.

![chlimage_1-124](assets/chlimage_1-124.png)

### Nästa steg {#the-next-steps}

När du har lärt dig mer om hur du hanterar apppaneler på programkontrollpanelen kan du läsa följande resurser för andra redigeringsroller:

* [Redigera appmetadata](/help/mobile/phonegap-editmetadata.md)
* [Programdefinitioner](/help/mobile/phonegap-app-definitions.md)
* [Skapa ett nytt program med guiden Skapa app](/help/mobile/phonegap-create-new-app.md)
* [Importera en befintlig hybridapp](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Innehållstjänster](/help/mobile/develop-content-as-a-service.md)

### Ytterligare resurser {#additional-resources}

Mer information om roller och ansvar för en administratör och utvecklare finns i resurserna nedan:

* [Utveckla för Adobe PhoneGap Enterprise med AEM](/help/mobile/developing-in-phonegap.md)
* [Administrera innehåll för Adobe PhoneGap Enterprise med AEM](/help/mobile/administer-phonegap.md)
