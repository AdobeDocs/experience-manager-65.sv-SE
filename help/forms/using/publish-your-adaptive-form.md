---
title: '"Självstudiekurs: Publicera ditt adaptiva formulär"'
seo-title: '"Självstudiekurs: Publicera ditt adaptiva formulär"'
description: Publicera det adaptiva formuläret som en AEM-sida, bädda in formuläret på en AEM Sites-sida eller bädda in det adaptiva formuläret på en extern webbsida
seo-description: Publicera det adaptiva formuläret som en AEM-sida, bädda in formuläret på en AEM Sites-sida eller bädda in det adaptiva formuläret på en extern webbsida
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: 709d8fe467f5449eb1e844a49126535a4a4a6e7a

---


# Självstudiekurs: Publicera ditt adaptiva formulär {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

Den här självstudiekursen är ett steg i serien [Create Your First Adaptive Form](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) . Vi rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga exemplet på självstudiekurser.

När det adaptiva formuläret är klart kan du publicera det för att göra det tillgängligt för slutanvändarna. Slutanvändarna kan öppna det publicerade formuläret på vilken enhet och webbläsare som helst. När ett adaptivt formulär publiceras kopieras formuläret och tillhörande innehåll från en AEM-författarinstans till en AEM-publiceringsinstans. Formuläret görs tillgängligt för slutanvändaren via publiceringsinstansen.

Du kan publicera ett anpassat formulär på följande sätt:

* [Publicera det adaptiva formuläret som en AEM-sida](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Bädda in det anpassningsbara formuläret på en AEM Sites-sida](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Bädda in det adaptiva formuläret på en extern webbsida (en icke-AEM-webbsida som ligger utanför AEM)](../../forms/using/publish-your-adaptive-form.md)

## Innan du startar {#before-you-start}

* **[Konfigurera en AEM Forms-publiceringsinstans](https://helpx.adobe.com/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**: Publiceringsinstansen är en offentlig instans av AEM Forms som körs i publiceringsläge. I en produktionsmiljö ligger publiceringsinstansen utanför organisationens brandvägg.
* **[Konfigurera replikering och omvänd replikering](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**: Vid replikering kopieras innehåll från författarinstansen till en publiceringsinstans och användarindata returneras (till exempel formulärindata) från publiceringsinstansen till författarinstansen.

## Publicera det adaptiva formuläret som en AEM-sida {#publish-the-adaptive-form-as-an-aem-page}

När det adaptiva formuläret publiceras som en AEM-sida innehåller hela webbsidan bara publicerade formulär. Du kan använda URL:en för det adaptiva formuläret för att länka det från en annan webbsida. Så här publicerar du det anpassningsbara formuläret **** shipping-address-add-update som en AEM-sida:

1. Logga in på AEM Forms författarinstans och leta upp formuläret shipping-address-add-update-form adaptive form i AEM Forms-gränssnittet.
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Välj adaptiv blankett för leverans-adress-add-update-form och tryck på **Publicera**. En dialogruta med resurser som är kopplade till det adaptiva formuläret visas. Tryck på **Publicera**. Det anpassningsbara formuläret publiceras och en dialogruta visas.
1. Öppna formuläret i publiceringsinstansen. Formuläret kan fyllas i och skickas av användaren.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Bädda in det anpassningsbara formuläret på en AEM Sites-sida {#embed-the-adaptive-form-in-an-aem-sites-page}

Med AEM Forms kan formulärutvecklare smidigt bädda in adaptiva formulär på en AEM Sites-sida. Det inbäddade adaptiva formuläret fungerar fullt ut och användarna kan fylla i och skicka formuläret utan att behöva lämna sidan. Det hjälper användaren att stanna kvar i sitt sammanhang för andra element på webbsidan och interagera samtidigt med formuläret.

AEM Forms innehåller en komponent, AEM Forms Container, som bäddar in ett adaptivt formulär på en AEM Sites-sida. Komponenten är som standard inte synlig i AEM Sites-behållaren. Utför följande steg för att aktivera komponenten AEM Forms Container och för att bädda in det adaptiva formuläret på en AEM Sites-sida:

1. Skapa och öppna en sida på webbplatsen We.Retail för redigering. Till exempel [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). Det anpassningsbara formuläret är inbäddat på webbplatssidan.

   Du kan även bädda in det adaptiva formuläret på en befintlig webbsida. Exempel: sidan ABOUT US [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Du sparar tid när du skapar en sida. Stegen nedan använder den nya sidan.

   Webbplatsen We.Retail levereras med AEM. Om du inte har installerat webbplatsen We.Retail går du till [We.Retail Reference Implementation](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) för att installera webbplatsen.

1. Tryck på ![egenskapens](assets/properties.png) sidinformation och välj alternativet **Redigera mall** på den nyligen skapade webbsidan för Vi.Retail. Sidmallen öppnas på en ny flik i webbläsaren.
1. Tryck inuti **layoutbehållarrutan** och tryck på ![feedhantering](assets/feedmanagement.png). Expandera dragspelsfliken **Allmänt** på fliken **Tillåtna komponenter** , markera alternativet **AEM-formulär** och tryck sedan på ![](https://helpx.adobe.com/content/dam/help/en/aem-forms/icons/AEM_6_3_Forms_save.PNG). AEM Forms Container-komponenten är aktiverad för sidan.

1. Öppna webbläsarfliken som innehåller sidan AEM Sites som öppnats i steg 1. Tryck på **Dra komponenter här** och tryck på **+.** I rutan **Infoga ny komponent** trycker du på **AEM-formulär.** Komponenten **AEM Forms Container** läggs till på sidan.
1. Tryck på behållarkomponenten för **AEM Forms** och tryck ![](https://helpx.adobe.com/content/dam/help/en/aem-forms/6-2/cmppr.png). En dialogruta med egenskaper för AEM Forms Container visas. I fältet **Resurssökväg** bläddrar du till och väljer formuläret shipping-address-add-update-form adaptive. Tryck ![](https://helpx.adobe.com/content/dam/help/en/aem-forms/icons/AEM_6_3_Forms_save.PNG). Det anpassningsbara formuläret är inbäddat på sidan.
1. Publicera både adaptiva formulär- och webbplatssidor. Här är några saker du bör hålla i minnet:

   * Om du publicerar AEM-webbplatssidan för första gången och den innehåller ett inbäddat formulär publicerar du webbplatssidan och det inbäddade formuläret.
   * Om du bara ändrar det inbäddade formuläret på en publicerad webbplatssida publicerar du det ursprungliga formuläret och ändringarna återspeglas på den publicerade webbplatssidan. Den publicerade webbplatssidan innehåller en referens till formuläret och behöver inte publicera om sidan.
   * Om du ändrar webbplatssidan och det inbäddade formuläret publicerar du webbplatssidan och formuläret igen.
   ![embed-in-aem-sites](assets/embed-in-aem-sites.png)

   Formuläret för ändring av leverans- och faktureringsadress har lagts till på en AEM Sites-sida.

## Bädda in det anpassningsbara formuläret på en extern webbsida {#embed-the-adaptive-form-in-an-external-webpage}

Du kan bädda in ett adaptivt formulär på en extern webbsida (en icke-AEM-webbsida som är värd utanför AEM) genom att infoga några rader JavaScript på den externa webbsidan. JavaScript-koden skickar en HTTP-begäran till AEM Forms-servern för det adaptiva formuläret och relaterade resurser och lägger till det adaptiva formuläret på webbsidan. Mer information finns i [Bädda in det adaptiva formuläret på en extern webbsida](/help/forms/using/embed-adaptive-form-external-web-page.md).
