---
title: "Självstudiekurs: Publicera ditt adaptiva formulär"
description: Publicera det adaptiva formuläret som en AEM sida, bädda in formuläret på en AEM Sites-sida eller bädda in det i en extern webbsida
contentOwner: khsingh
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---

# Självstudiekurs: Publicera ditt adaptiva formulär {#tutorial-publish-your-adaptive-form}

![Hero-image](do-not-localize/13-publish-your-adaptive-form-small.png)

Den här självstudiekursen är ett steg i [Skapa ditt första adaptiva formulär](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) serie. Vi rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga självstudiekurserna.

När det adaptiva formuläret är klart kan du publicera det för att göra det tillgängligt för slutanvändarna. Slutanvändarna kan öppna det publicerade formuläret på vilken enhet och webbläsare som helst. När ett anpassat formulär publiceras kopieras formuläret och det tillhörande innehållet från en AEM författarinstans till en AEM publiceringsinstans. Formuläret görs tillgängligt för slutanvändaren via publiceringsinstansen.

Du kan publicera ett anpassat formulär på följande sätt:

* [Publicera det adaptiva formuläret som en AEM sida](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Bädda in det anpassningsbara formuläret på en AEM Sites-sida](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Bädda in det adaptiva formuläret på en extern webbsida (en icke-AEM webbsida som finns på andra AEM)](../../forms/using/publish-your-adaptive-form.md)

## Innan du börjar {#before-you-start}

* **[Konfigurera en publiceringsinstans i AEM Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**: Publiceringsinstansen är en offentlig instans av AEM [!DNL Forms] som körs i publiceringsläge. I en produktionsmiljö ligger publiceringsinstansen utanför organisationens brandvägg.
* **[Konfigurera replikering och omvänd replikering](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**: Replikering kopierar innehåll från författarinstansen till en publiceringsinstans och returnerar användarindata (till exempel formulärindata) från publiceringsinstansen till författarinstansen.

## Publicera det adaptiva formuläret som en AEM sida {#publish-the-adaptive-form-as-an-aem-page}

När det adaptiva formuläret publiceras som en AEM sida innehåller hela webbsidan bara det publicerade formuläret. Du kan använda URL:en för det adaptiva formuläret för att länka det från en annan webbsida. Publicera **shipping-address-add-update-form** adaptiv form som en AEM sida:

1. Logga in på AEM [!DNL Forms] författarinstans och hitta formuläret shipping-address-add-update-form adaptive i AEM [!DNL Forms] Gränssnitt.
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Välj adaptiv blankett för leverans-adress-add-update och välj **[!UICONTROL Publish]**. En dialogruta med resurser som är kopplade till det adaptiva formuläret visas. Välj **[!UICONTROL Publish]**. Det anpassningsbara formuläret publiceras och en dialogruta visas.
1. Öppna formuläret i publiceringsinstansen. Formuläret kan fyllas i och skickas av användaren.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Bädda in det anpassningsbara formuläret på en AEM Sites-sida {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] gör att formulärutvecklare kan bädda in anpassningsbara formulär i en AEM [!DNL Sites] sida. Det inbäddade adaptiva formuläret fungerar fullt ut och användarna kan fylla i och skicka formuläret utan att behöva lämna sidan. Det hjälper användaren att stanna kvar i sitt sammanhang för andra element på webbsidan och interagera samtidigt med formuläret.

AEM [!DNL Forms] tillhandahålla en komponent, AEM [!DNL Forms] Behållare, bädda in ett anpassat formulär i en AEM [!DNL Sites] sida. Komponenten visas som standard inte i AEM [!DNL Sites] behållare. Gör följande för att aktivera AEM [!DNL Forms] Containerkomponenten och bädda in det adaptiva formuläret i en AEM [!DNL Sites] Sida:

1. Skapa och öppna en sida på webbplatsen We.Retail för redigering. Till exempel: [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). Det anpassningsbara formuläret är inbäddat i [!DNL Sites] sida.

   Du kan även bädda in det adaptiva formuläret i en befintlig Web.Retail [!DNL Site's] sida. Exempel: sidan ABOUT US [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Du sparar tid när du skapar en sida. Stegen nedan använder den nya sidan.

   Webbplatsen We.Retail levereras med AEM. Om du inte har installerat webbplatsen We.Retail kan du gå till [Implementering av referens för Vi.butik](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) installera platsen.

1. Välj ![egenskaper](assets/properties.png) sidinformation och välj **[!UICONTROL Edit Template]** på den nyligen skapade webbsidan We.Retail. Sidmallen öppnas på en ny flik i webbläsaren.
1. Markera inuti **[!UICONTROL layout container]** och markera ![feedhantering](assets/feedmanagement.png). I **[!UICONTROL Allowed Components]** -fliken, expandera **[!UICONTROL General]** accordion, välj **[!UICONTROL AEM Form]** och markera ![save_icon](assets/save_icon.svg). AEM [!DNL Forms] Behållarkomponenten är aktiverad för sidan.

1. Öppna webbläsarfliken som innehåller AEM [!DNL Sites] sida öppnad i steg 1. Välj **[!UICONTROL Drag components here]** och markera **+.** I **[!UICONTROL Insert New Component]** ruta, markera **[!UICONTROL AEM Form]**. The **[!UICONTROL AEM Forms Container]** läggs till på sidan.
1. Välj **[!UICONTROL AEM Forms container]** -komponent och markera ![configure-icon](assets/configure-icon.svg). En dialogruta med egenskaper för AEM [!DNL Forms] Behållaren visas. I **[!UICONTROL Asset Path]** bläddra och välj formuläret för leveransadress-add-update-form adaptive. Välj ![save_icon](assets/save_icon.svg). Det anpassningsbara formuläret är inbäddat på sidan.
1. Publicera både det adaptiva formuläret och [!DNL Sites] sida. Här är några saker att tänka på:

   * Om du publicerar AEM [!DNL Sites] -sidan för första gången och innehåller ett inbäddat formulär, publicera [!DNL Sites] sida och det inbäddade formuläret.
   * Om du bara ändrar det inbäddade formuläret på en publicerad webbplatssida publicerar du det ursprungliga formuläret och ändringarna återspeglas på den publicerade webbplatssidan. Den publicerade webbplatssidan innehåller en referens till formuläret och behöver inte publicera om sidan.
   * Om du ändrar [!DNL Sites] sida och det inbäddade formuläret, publicera om [!DNL Sites] sida och formulär.

     ![embed-in-aem-sites](assets/embed-in-aem-sites.png)

   Formuläret för ändring av leverans- och faktureringsadress har lagts till i en AEM [!DNL Sites] sida.

## Bädda in det anpassningsbara formuläret på en extern webbsida {#embed-the-adaptive-form-in-an-external-webpage}

Du kan bädda in ett adaptivt formulär på en extern webbsida (en icke-AEM webbsida som är värd utanför AEM) genom att infoga några rader med JavaScript på den externa webbsidan. JavaScript-koden skickar en HTTP-begäran till AEM [!DNL Forms] server för det adaptiva formuläret och relaterade resurser och lägger till det adaptiva formuläret på webbsidan. Detaljerade anvisningar finns i [bädda in det adaptiva formuläret på en extern webbsida](/help/forms/using/embed-adaptive-form-external-web-page.md).
