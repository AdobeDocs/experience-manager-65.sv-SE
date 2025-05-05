---
title: 'Självstudiekurs: Publish ditt adaptiva formulär'
description: Publish det adaptiva formuläret som en AEM, bädda in formuläret på en AEM Sites-sida eller bädda in det i en extern webbsida
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

# Självstudiekurs: Publish ditt adaptiva formulär {#tutorial-publish-your-adaptive-form}

![Hero-image](do-not-localize/13-publish-your-adaptive-form-small.png)

Den här självstudiekursen är ett steg i serien [Create Your First Adaptive Form](https://helpx.adobe.com/se/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) . Vi rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga självstudiekurserna.

När det adaptiva formuläret är klart kan du publicera det för att göra det tillgängligt för slutanvändarna. Slutanvändarna kan öppna det publicerade formuläret på vilken enhet och webbläsare som helst. När ett anpassat formulär publiceras kopieras formuläret och det tillhörande innehållet från en AEM författarinstans till en AEM publiceringsinstans. Formuläret görs tillgängligt för slutanvändaren via publiceringsinstansen.

Du kan publicera ett anpassat formulär på följande sätt:

* [Publish adaptiva formulär som en AEM sida](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Bädda in det anpassningsbara formuläret på en AEM Sites-sida](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Bädda in det adaptiva formuläret på en extern webbsida (en icke-AEM webbsida som finns på andra AEM)](../../forms/using/publish-your-adaptive-form.md)

## Innan du börjar {#before-you-start}

* **[Konfigurera en AEM Forms-publiceringsinstans](https://helpx.adobe.com/se/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**: Publiceringsinstansen är en publik instans av AEM [!DNL Forms] som körs i publiceringsläge. I en produktionsmiljö ligger publiceringsinstansen utanför organisationens brandvägg.
* **[Konfigurera replikering och omvänd replikering](https://helpx.adobe.com/se/experience-manager/6-3/help/sites-deploying/replication.html)**: Replikering kopierar innehåll från författarinstansen till en publiceringsinstans och returnerar användarindata (till exempel formulärindata) från publiceringsinstansen till författarinstansen.

## Publish adaptiva formulär som en AEM sida {#publish-the-adaptive-form-as-an-aem-page}

När det adaptiva formuläret publiceras som en AEM sida innehåller hela webbsidan bara det publicerade formuläret. Du kan använda URL:en för det adaptiva formuläret för att länka det från en annan webbsida. Så här publicerar du det adaptiva formuläret **shipping-address-add-update-form** som en AEM sida:

1. Logga in på AEM [!DNL Forms] författarinstans och leta reda på formuläret shipping-address-add-update-form adaptive i AEM [!DNL Forms] UI.
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Välj adaptiv blankett för leverans-adress-add-update-form och välj **[!UICONTROL Publish]**. En dialogruta med resurser som är kopplade till det adaptiva formuläret visas. Välj **[!UICONTROL Publish]**. Det anpassningsbara formuläret publiceras och en dialogruta visas.
1. Öppna formuläret i publiceringsinstansen. Formuläret kan fyllas i och skickas av användaren.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Bädda in det anpassningsbara formuläret på en AEM Sites-sida {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] tillåter formulärutvecklare att sömlöst bädda in adaptiva formulär på en AEM [!DNL Sites] -sida. Det inbäddade adaptiva formuläret fungerar fullt ut och användarna kan fylla i och skicka formuläret utan att behöva lämna sidan. Det hjälper användaren att stanna kvar i sitt sammanhang för andra element på webbsidan och interagera samtidigt med formuläret.

AEM [!DNL Forms] tillhandahåller en komponent, AEM [!DNL Forms] Container, för att bädda in ett adaptivt formulär på en AEM [!DNL Sites] -sida. Komponenten är som standard inte synlig i AEM [!DNL Sites]. Utför följande steg för att aktivera AEM [!DNL Forms] Container-komponenten och bädda in det adaptiva formuläret på en AEM [!DNL Sites] -sida:

1. Skapa och öppna en sida på webbplatsen We.Retail för redigering. Exempel: [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). Det adaptiva formuläret är inbäddat på sidan [!DNL Sites].

   Du kan även bädda in det adaptiva formuläret på en befintlig webbsida. Detaljhandel [!DNL Site's]. Till exempel sidan OM USA [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Du sparar tid när du skapar en sida. Stegen nedan använder den nya sidan.

   Webbplatsen We.Retail levereras med AEM. Om du inte har installerat webbplatsen We.Retail ska du läsa [Implementering av referens för butik](https://helpx.adobe.com/se/experience-manager/6-3/help/sites-developing/we-retail.html) för att installera webbplatsen.

1. Välj sidinformation för ![egenskaper](assets/properties.png) och välj alternativet **[!UICONTROL Edit Template]** på den nyligen skapade webbsidan för webb.butik. Sidmallen öppnas på en ny flik i webbläsaren.
1. Markera i rutan **[!UICONTROL layout container]** och välj ![feedmanagement](assets/feedmanagement.png). Expandera dragspelet **[!UICONTROL General]** på fliken **[!UICONTROL Allowed Components]**, markera alternativet **[!UICONTROL AEM Form]** och välj ![save_icon](assets/save_icon.svg). AEM [!DNL Forms]-behållarkomponenten är aktiverad för sidan.

1. Öppna webbläsarfliken som innehåller AEM [!DNL Sites] sida som öppnats i steg 1. Markera rutan **[!UICONTROL Drag components here]** och välj **+.** I rutan **[!UICONTROL Insert New Component]** väljer du **[!UICONTROL AEM Form]**. Komponenten **[!UICONTROL AEM Forms Container]** läggs till på sidan.
1. Markera komponenten **[!UICONTROL AEM Forms container]** och välj ![configure-icon](assets/configure-icon.svg). En dialogruta med egenskaper för AEM [!DNL Forms]-behållare visas. I fältet **[!UICONTROL Asset Path]** bläddrar du till och väljer formuläret shipping-address-add-update-form adaptive. Välj ![save_icon](assets/save_icon.svg). Det anpassningsbara formuläret är inbäddat på sidan.
1. Publish både adaptiva formulär och sidan [!DNL Sites]. Här är några saker att tänka på:

   * Om du publicerar sidan AEM [!DNL Sites] för första gången och den innehåller ett inbäddat formulär publicerar du sidan [!DNL Sites] och det inbäddade formuläret.
   * Om du bara ändrar det inbäddade formuläret på en publicerad webbplatssida publicerar du det ursprungliga formuläret och ändringarna återspeglas på den publicerade webbplatssidan. Den publicerade webbplatssidan innehåller en referens till formuläret och behöver inte publicera om sidan.
   * Om du ändrar sidan [!DNL Sites] och det inbäddade formuläret publicerar du om sidan [!DNL Sites] och formuläret.

     ![embed-in-aem-sites](assets/embed-in-aem-sites.png)

   Formuläret för ändring av leverans- och faktureringsadress har lagts till på en AEM [!DNL Sites]-sida.

## Bädda in det anpassningsbara formuläret på en extern webbsida {#embed-the-adaptive-form-in-an-external-webpage}

Du kan bädda in ett adaptivt formulär på en extern webbsida (en icke-AEM webbsida som är värd utanför AEM) genom att infoga några rader med JavaScript på den externa webbsidan. JavaScript-koden skickar en HTTP-begäran till AEM [!DNL Forms]-servern för det adaptiva formuläret och relaterade resurser och lägger till det adaptiva formuläret på webbsidan. Detaljerade steg finns i [Bädda in det adaptiva formuläret på en extern webbsida](/help/forms/using/embed-adaptive-form-external-web-page.md).
