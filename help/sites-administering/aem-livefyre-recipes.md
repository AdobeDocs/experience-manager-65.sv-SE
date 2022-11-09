---
title: AEM Livefyre-recept
seo-title: AEM Livefyre Recipes
description: Stegvisa instruktioner om vanliga användningsområden för Adobe Experience Manager Livefyre.
seo-description: Step-by-step instructions on common use cases for Adobe Experience Manager Livefyre.
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
exl-id: 7ccd67a7-9945-48c1-9986-f4eaf0f2b961
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 0%

---

# AEM Livefyre-recept{#aem-livefyre-recipes}

Stegvisa instruktioner om vanliga användningsområden för Adobe Experience Manager Livefyre.

## Kuratera användargenererat innehåll med hjälp av färdiga Livefyre-AEM och visning med Livefyre Media Wall {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

Media Wall strömmar socialt och inbyggt Livefyre-innehåll till en social vägg i realtid. Det finns flera sätt att implementera Media Wall i AEM beroende på hur du använder datorn och vilka krav som ställs.

AEM Livefyre-paketet är en körklar implementering, medan den traditionella integreringen gör det möjligt att skapa anpassade Livefyre-AEM.

### AEM {#aem-integration}

Livefyre Adobe Experience Manager-paketet finns för AEM 6.1, 6.2SP1, 6.3, 6.4 och 6.4 SP1. AEM 5.x och 6.0 stöds inte. Detaljerade anvisningar finns i [Integrera med Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

Om du vill se vilka Livefyre-appar som stöds går du till [AEM supportmatris för Livefyre-appar](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Traditionell implementering (för anpassade AEM) {#traditional-implementation-for-customized-aem-components}

Det finns tre sätt att implementera Livefyre i en anpassad AEM eller andra CMS-system som WordPress, Sitecore eller DemandWare. En traditionell Livefyre-integrering är en CMS-agnostikversion.

**Metod 1: App-implementering för Designer**

* **Vad:** Det enklaste och snabbaste sättet att integrera en Livefyre-app. Du kan utforma, konfigurera och generera en anpassad JavaScript-inbäddningskod för att integrera en Media Wall App på en sida på några minuter.
* **Hur:**  [Skapa, förhandsgranska, publicera och bädda in en medieväggsapp](https://experienceleague.adobe.com/docs/livefyre/using/apps/c-create-an-app.html)

* **Exempel:** [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**Metod 2: SDK-implementering**

* **Vad:** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) är huvudbiblioteket som driver Apps och Auth på en webbplats. Den definierar den globala *window.Livefyre* objekt och en enda offentlig metod, *Livefyre.require*, som kan användas för att läsa in andra Livefyre JavaScript-bibliotek som kan användas för att bädda in Livefyre-appar och integrera med andra användarautentiseringssystem.

* **Hur**: [Använda Livefyre JavaScript SDK:s streamhub-wallpackage](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-media-wall-integration.html)

* **Exempel**: [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

Avancerade anpassningar med SDK finns i [StreamHub SDKs](https://github.com/Livefyre/streamhub-sdk).

**Metod 3: API-implementering**

* För att skapa anpassade upplevelser och datavisualiseringar kan Livefyre-appar skapas från grunden genom att använda Livefyre och sociala data med [Bootstrap och Stream API](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Se till att du följer [Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html), [Facebook](https://en.facebookbrand.com/guidelines/brand)och [Instagram](https://en.instagram-brand.com/) visa riktlinjer när användargränssnittet för användargenererat innehåll skapas.

### Integrering av medieväggsautentisering {#media-wall-authentication-integration}

För medieväggsintegreringar som kräver verifiering, se:

* [Anpassa enkel inloggning vid integrering](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) för AEM Identity Management
* [Identitetsintegrering](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) för autentiseringsplattformar från tredje part

### Använd skiftläge - översikt {#use-case-overview}

Som AEM kund vill jag strukturera om användargenererat innehåll med hjälp av färdiga Livefyre-AEM och webbannonser med Livefyre Media Wall:

Steg som ska implementeras:

1. [Komma igång](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Konfigurera AEM att använda Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Dra och släpp AEM Media Wall-komponent på sidan](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [Konfigurera strömmar och lägg till regler för att strukturera UGC och visa på Media Wall-komponenten](https://experienceleague.adobe.com/docs/livefyre/using/streams/c-streams.html)

Utbildningsvideor om UGC för direktuppspelning finns på [Skapa automatiska innehållsströmmar och söka i socialt innehåll i Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

### Kundexempel {#customer-examples}

* [CNN Media Wall](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [PGA Tour Media Wall](https://www.pgatour.com/social-hub.html)

För att skapa anpassade upplevelser och datavisualiseringar kan Livefyre-appar skapas från grunden genom att använda Livefyre och sociala data med [Bootstrap och Stream API](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Information om vilka Livefyre-appar som kräver autentisering finns i [Identitetsintegrering](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) för autentiseringsplattformar från tredje part.

* [PGA Tour Media Wall](https://www.pgatour.com/social-hub.html)
* [TimeOut](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## Integrera Livefyre-kommentarer med AEM Components eller traditionell Livefyre-integrering {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### AEM {#aem-integration-1}

Livefyre Adobe Experience Manager-paketet finns för AEM 6.1, 6.2SP1, 6.3, 6.4 och 6.4 SP1. AEM 5.x och 6.0 stöds inte. Detaljerade anvisningar finns i [Integrera med Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

### Traditionell implementering (för anpassade AEM) {#traditional-implementation-for-customized-aem-components-1}

Det finns tre sätt att implementera Livefyre Comments-appen i en anpassad AEM eller andra CMS-system som WordPress, Sitecore eller DemandWare. En traditionell Livefyre-integrering är en CMS-agnostikversion.

**Metod 1: App-implementering för Designer**

* **Vad:** Det enklaste och snabbaste sättet att integrera en Livefyre-app. Du kan utforma, konfigurera och generera en anpassad JavaScript-inbäddningskod för att integrera en Media Wall App på en sida på några minuter.
* **Hur:** [Skapa, förhandsgranska, publicera och bädda in en kommentarapp](https://experienceleague.adobe.com/docs/livefyre/using/apps/c-create-an-app.html)

* **Exempel:** [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**Metod 2: SDK-implementering**

* **Vad:** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) är huvudbiblioteket som driver Apps och Auth på en webbplats. Den definierar den globala *window.Livefyre* objekt och en enda offentlig metod, *Livefyre.require*, som kan användas för att läsa in andra Livefyre JavaScript-bibliotek som kan användas för att bädda in Livefyre-appar och integrera med andra användarautentiseringssystem.

* **Hur:**

   * Skapa en samling/app med [CollectionMeta-token](https://experienceleague.adobe.com/docs/livefyre/implementation/getting-started/implementation-process/c-collectionmeta-tokent.html).
   * Integrera [Kommentarsapp](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/comments/c-comments-integration.html) till webbplatser med Livefyre.js bäddar in kodstrukturen.

* **Exempel:**  [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

Mer information om avancerade anpassningar med SDK finns i [StreamHub SDKs](https://github.com/Livefyre/streamhub-sdk).

**Metod 3: API-implementering**

* För att skapa anpassade upplevelser och datavisualiseringar kan Livefyre-appar skapas från grunden genom att använda Livefyre och sociala data med [Bootstrap och Stream API](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

### Kommentarer App Authentication Integration {#comments-app-authentication-integration}

* [Anpassa enkel inloggning vid integrering](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) för AEM Identity Management
* [Identitetsintegrering](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) för autentiseringsplattformar från tredje part

### Kundexempel {#customer-examples-1}

* [Poise (Kimberly Klark)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Använd integreringen med Livefyre AEM Assets för att importera UGC i AEM Assets {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Livefyre Setup (för UGC Curation och Rights Management):**

1. [Konfigurera strömmar och Lägg till regler för att strukturera UGC i biblioteksmappar för Livefyre-resurser](https://experienceleague.adobe.com/docs/livefyre/using/streams/c-streams.html).

   1. Utbildningsvideor om UGC för direktuppspelning finns på [Skapa automatiska innehållsströmmar och söka i socialt innehåll i Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Samla, ordna och hantera förvaltade användargenererat innehåll i biblioteksmappar för Livefyre-resurser](https://experienceleague.adobe.com/docs/livefyre/using/library/assets/c-assets.html).

   1. Utbildningsvideor om hur du skapar och hanterar mappar i resursbiblioteket för Livefyre Studio finns på [Arbeta med Assets i Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Begär rättigheter för förvaltad användargenererat innehåll med Livefyre Studio](https://experienceleague.adobe.com/docs/livefyre/using/rights-requests/c-how-requesting-rights-works.html).

**AEM (för import av UGC till AEM Assets):**

1. [Komma igång](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Konfigurera AEM att använda Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [Importera användargenererat innehåll (UGC) från Livefyre till AEM Assets](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Tourism Australia](https://www.australia.com/en-us)

## Integrera Livefyre-recensioner med AEM eller traditionell Livefyre-integrering {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### AEM {#aem-integration-2}

Livefyre Adobe Experience Manager-paketet finns för AEM 6.1, 6.2SP1, 6.3, 6.4 och 6.4 SP1. AEM 5.x och 6.0 stöds inte. Detaljerade anvisningar finns i [Integrera med Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

Komponenten Reviews stöds inte för AEM 6.1. Kontrollera [AEM supportmatris för alla Livefyre-appar](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Traditionell implementering (för anpassade AEM) {#traditional-implementation-for-customized-aem-components-2}

Det finns två sätt att implementera Livefyre Reviews App i en anpassad AEM eller andra CMS-system som WordPress, Sitecore eller DemandWare. En traditionell Livefyre-integrering är en CMS-agnostikversion.

**Metod 1: SDK-implementering**

* **Vad:** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) är huvudbiblioteket som driver Apps och Auth på en webbplats. Den definierar den globala *window.Livefyre* objekt och en enda offentlig metod, *Livefyre.require*, som kan användas för att läsa in andra Livefyre JavaScript-bibliotek som kan användas för att bädda in Livefyre-appar och integrera med andra användarautentiseringssystem.

* **Hur:**

   * Skapa recensioner [CollectionMeta-token](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-reviews-integration.html) om du vill ange metadata som ska lagras i granskningssamlingen.
   * Integrera [Granskningsapp](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-reviews-integration.html) till webbplatser med *Livefyre.js* bädda in kodstruktur

* **Exempel:**  [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

Mer information om avancerade anpassningar med SDK finns i [StreamHub SDKs](https://github.com/Livefyre/streamhub-sdk).

**Metod 2: API-implementering**

* För att skapa anpassade upplevelser och datavisualiseringar kan Livefyre-appar skapas från grunden genom att använda Livefyre och sociala data med API:t för Bootstrap och Stream.

Ytterligare API:er för omdömen och recensioner finns [här](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews).

### Kommentarer App Authentication Integration {#comments-app-authentication-integration-1}

* [Anpassa enkel inloggning vid integrering](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) för AEM Identity Management
* [Identitetsintegrering](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) för autentiseringsplattformar från tredje part

### Kundexempel {#customer-examples-2}

* [TimeOut](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [minrecept](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)
