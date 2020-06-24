---
title: AEM Livefyre - recept
seo-title: AEM Livefyre - recept
description: Stegvisa instruktioner om vanliga användningsområden för Adobe Experience Manager Livefyre.
seo-description: Stegvisa instruktioner om vanliga användningsområden för Adobe Experience Manager Livefyre.
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
translation-type: tm+mt
source-git-commit: 072898f18d418eac8e9d9e94453db34d62dd3ed9
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 0%

---


# AEM Livefyre - recept{#aem-livefyre-recipes}

Stegvisa instruktioner om vanliga användningsområden för Adobe Experience Manager Livefyre.

## Kuratera användargenererat innehåll med färdiga Livefyre AEM-komponenter och visa med Livefyre Media Wall {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

Media Wall strömmar socialt och inbyggt Livefyre-innehåll till en social vägg i realtid. Det finns flera sätt att implementera medieväggning i AEM beroende på hur du använder datorn och vilka krav som ställs.

AEM Livefyre-paketet är en färdig implementering, medan den traditionella integreringen gör det möjligt att skapa anpassade Livefyre AEM-komponenter.

### AEM-integrering {#aem-integration}

Paketet Livefyre Adobe Experience Manager finns för AEM 6.1, 6.2SP1, 6.3, 6.4 och 6.4 SP1. AEM 5.x och 6.0 stöds inte. Mer information finns i [Integrera med Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

Om du vill se vilka Livefyre-appar som stöds kan du läsa [AEM Support Matrix för Livefyre-appar](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Traditionell implementering (för anpassade AEM-komponenter) {#traditional-implementation-for-customized-aem-components}

Det finns tre sätt att implementera Livefyre i en anpassad AEM-komponent eller andra CMS-system som WordPress, Sitecore eller DemandWare. En traditionell Livefyre-integrering är en CMS-agnostikversion.

**Metod 1: App-implementering för Designer**

* **Vad:** Det enklaste och snabbaste sättet att integrera en Livefyre-app. Du kan utforma, konfigurera och generera en anpassad JavaScript-inbäddningskod för att integrera en Media Wall App på en sida på några minuter.
* **Hur:**  [Skapa, förhandsgranska, publicera och bädda in en medieväggsapp](https://docs.adobe.com/content/help/en/livefyre/using/apps/c-create-an-app.html)

* **Exempel:** [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**Metod 2: SDK-implementering**

* **Vad:** [Livefyre.js](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) är huvudbiblioteket som driver Apps och Auth på en webbplats. Den definierar det globala *objektet window.Livefyre* och en offentlig metod, *Livefyre.require*, som kan användas för att läsa in andra Livefyre JavaScript-bibliotek som hjälper till med inbäddning av Livefyre-appar och integrering med andra användarautentiseringsplattformar.

* **Hur**: [Använda Livefyre JavaScript SDK:s streamhub-wallpackage](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-media-wall-integration.html)

* **Exempel**: [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

Mer information om avancerade anpassningar med SDK finns i [StreamHub SDKs](https://github.com/Livefyre/streamhub-sdk).

**Metod 3: API-implementering**

* För att skapa anpassade upplevelser och datavisualiseringar kan Livefyre-appar skapas från grunden genom att konsumera Livefyre och sociala data med [Bootstrap och Stream API](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Se till att du följer [visningsriktlinjerna för Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html), [Facebook](https://en.facebookbrand.com/guidelines/brand)och [Instagram](https://en.instagram-brand.com/) när du skapar användargränssnittet för UGC.

### Integrering av medieväggsautentisering {#media-wall-authentication-integration}

För medieväggsintegreringar som kräver verifiering, se:

* [Anpassa Single Sign on Integration](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) för AEM Identity Management
* [Identitetsintegrering](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) för autentiseringsplattformar från tredje part

### Använd skiftläge - översikt {#use-case-overview}

Som AEM-kund vill jag strukturera UGC med de färdiga Livefyre AEM-komponenterna och visa med Livefyre Media Wall:

Steg som ska implementeras:

1. [Komma igång](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Konfigurera AEM att använda Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Dra och släpp AEM Media Wall-komponenten på sidan](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [Konfigurera strömmar och lägg till regler för att strukturera UGC och visa på Media Wall-komponenten](https://docs.adobe.com/content/help/en/livefyre/using/streams/c-streams.html)

Utbildningsvideor om hur du direktuppspelar UGC finns i [Skapa automatiska innehållsströmmar och Sök socialt innehåll i Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

### Kundexempel {#customer-examples}

* [CNN Media Wall](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [PGA Tour Media Wall](https://www.pgatour.com/social-hub.html)

För att skapa anpassade upplevelser och datavisualiseringar kan Livefyre-appar skapas från grunden genom att konsumera Livefyre och sociala data med [Bootstrap och Stream API](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Information om vilka Livefyre-appar som kräver autentisering finns i [Identitetsintegrering](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) för autentiseringsplattformar från tredje part.

* [PGA Tour Media Wall](https://www.pgatour.com/social-hub.html)
* [TimeOut](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## Integrera Livefyre-kommentarer med AEM Components eller traditionell Livefyre-integrering {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### AEM-integrering {#aem-integration-1}

Paketet Livefyre Adobe Experience Manager är tillgängligt för AEM 6.1, 6.2SP1, 6.3, 6.4 och 6.4 SP1. AEM 5.x och 6.0 stöds inte. Mer information finns i [Integrera med Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

### Traditionell implementering (för anpassade AEM-komponenter) {#traditional-implementation-for-customized-aem-components-1}

Det finns tre sätt att implementera Livefyre Comments App i en anpassad AEM-komponent eller andra CMS-system som WordPress, Sitecore eller DemandWare. En traditionell Livefyre-integrering är en CMS-agnostikversion.

**Metod 1: App-implementering för Designer**

* **Vad:** Det enklaste och snabbaste sättet att integrera en Livefyre-app. Du kan utforma, konfigurera och generera en anpassad JavaScript-inbäddningskod för att integrera en Media Wall App på en sida på några minuter.
* **Hur:** [Skapa, förhandsgranska, publicera och bädda in en kommentarapp](https://docs.adobe.com/content/help/en/livefyre/using/apps/c-create-an-app.html)

* **Exempel:** [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**Metod 2: SDK-implementering**

* **Vad:** [Livefyre.js](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) är huvudbiblioteket som driver Apps och Auth på en webbplats. Den definierar det globala *objektet window.Livefyre* och en offentlig metod, *Livefyre.require*, som kan användas för att läsa in andra Livefyre JavaScript-bibliotek som hjälper till med inbäddning av Livefyre-appar och integrering med andra användarautentiseringsplattformar.

* **Hur:**

   * Skapa en samling/app med [CollectionMeta-token](https://docs.adobe.com/content/help/en/livefyre/implementation/getting-started/implementation-process/c-collectionmeta-tokent.html).
   * Integrera [kommentarappen](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/comments/c-comments-integration.html) i webbplatser med hjälp av kodstrukturen Livefyre.js.

* **Exempel:**  [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

Mer information om avancerade anpassningar med SDK finns i [StreamHub SDKs](https://github.com/Livefyre/streamhub-sdk).

**Metod 3: API-implementering**

* För att skapa anpassade upplevelser och datavisualiseringar kan Livefyre-appar skapas från grunden genom att konsumera Livefyre och sociala data med [Bootstrap och Stream API](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

### Kommentarer App Authentication Integration {#comments-app-authentication-integration}

* [Anpassa Single Sign on Integration](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) för AEM Identity Management
* [Identitetsintegrering](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) för autentiseringsplattformar från tredje part

### Kundexempel {#customer-examples-1}

* [Poise (Kimberly Klark)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Använd integreringen Livefyre AEM Assets för att importera UGC i AEM Assets {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Livefyre Setup (for UGC Curation and Rights Management):**

1. [Konfigurera strömmar och Lägg till regler för att strukturera UGC i biblioteksmappar](https://docs.adobe.com/content/help/en/livefyre/using/streams/c-streams.html)för Livefyre-resurser.

   1. Utbildningsvideor om hur du direktuppspelar UGC finns i [Skapa automatiska innehållsströmmar och Sök socialt innehåll i Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Samla, ordna och hantera välstrukturerade användargenererat innehåll i biblioteksmapparna](https://docs.adobe.com/content/help/en/livefyre/using/library/assets/c-assets.html)för Livefyre-resurser.

   1. Utbildningsvideor om hur du skapar och hanterar mappar i resursbiblioteket i Livefyre Studio finns i [Arbeta med resurser i Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Begär rättigheter för välstrukturerad UGC med Livefyre Studio](https://docs.adobe.com/content/help/en/livefyre/using/rights-requests/c-how-requesting-rights-works.html).

**AEM-inställningar (för import av UGC till AEM Assets):**

1. [Komma igång](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Konfigurera AEM att använda Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [Importera användargenererat innehåll som strukturerats av Livefyre i AEM Assets](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Tourism Australia](https://www.australia.com/en-us)

## Integrera Livefyre-recensioner med AEM Components eller traditionell Livefyre-integrering {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### AEM-integrering {#aem-integration-2}

Paketet Livefyre Adobe Experience Manager är tillgängligt för AEM 6.1, 6.2SP1, 6.3, 6.4 och 6.4 SP1. AEM 5.x och 6.0 stöds inte. Mer information finns i [Integrera med Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

Komponenten Reviews stöds inte för AEM 6.1. Kontrollera [AEM-supportmatrisen för alla Livefyre-appar](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Traditionell implementering (för anpassade AEM-komponenter) {#traditional-implementation-for-customized-aem-components-2}

Det finns två sätt att implementera Livefyre Reviews App i en anpassad AEM-komponent eller andra CMS-system som WordPress, Sitecore eller DemandWare. En traditionell Livefyre-integrering är en CMS-agnostikversion.

**Metod 1: SDK-implementering**

* **Vad:** [Livefyre.js](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) är huvudbiblioteket som driver Apps och Auth på en webbplats. Den definierar det globala *objektet window.Livefyre* och en offentlig metod, *Livefyre.require*, som kan användas för att läsa in andra Livefyre JavaScript-bibliotek som hjälper till med inbäddning av Livefyre-appar och integrering med andra användarautentiseringsplattformar.

* **Hur:**

   * Skapa en [CollectionMeta-token](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-reviews-integration.html) för att ange de metadata som ska lagras i samlingen för granskningar.
   * Integrera [granskningsappar](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-reviews-integration.html) i webbplatser med kodstrukturen *Livefyre.js* .

* **Exempel:**  [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

Mer information om avancerade anpassningar med SDK finns i [StreamHub SDKs](https://github.com/Livefyre/streamhub-sdk).

**Metod 2: API-implementering**

* För att skapa anpassade upplevelser och datavisualiseringar kan Livefyre-appar skapas från grunden genom att konsumera Livefyre och sociala data med hjälp av Bootstrap och Stream API.

Ytterligare API:er för klassificering och granskning finns [här](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews).

### Kommentarer App Authentication Integration {#comments-app-authentication-integration-1}

* [Anpassa Single Sign on Integration](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) för AEM Identity Management
* [Identitetsintegrering](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) för autentiseringsplattformar från tredje part

### Kundexempel {#customer-examples-2}

* [TimeOut](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [minrecept](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)

