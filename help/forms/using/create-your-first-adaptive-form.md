---
title: "Självstudiekurs: Skapa ditt första adaptiva formulär"
description: Lär dig skapa interaktiva och responsiva blanketter i affärsklass.
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
exl-id: 77a05f83-ac9a-4221-85ac-439e82623a28
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 0%

---

# Självstudiekurs: Skapa ditt första anpassningsbara formulär {#tutorial-create-your-first-adaptive-form}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html) |
| AEM 6.5 | Den här artikeln |


![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## Introduktion {#introduction}

Söker du en mobilvänlig **formulärupplevelse** som förenklar registrering, ökar engagemanget och minskar handläggningstiden, **anpassningsbara formulär** passar dig perfekt. Adaptiva formulär ger en mobil, automatiserad och analysvänlig formulärupplevelse. Ni kan enkelt skapa formulär som är responsiva och interaktiva till sin natur, använda automatiserade processer för att minska administrativa och repetitiva uppgifter och använda dataanalys för att förbättra och personalisera den upplevelse kunderna har med era formulär.

Den här självstudiekursen ger ett komplett ramverk för att skapa ett anpassningsbart formulär. Självstudiekursen är indelad i ett användningsfall och i flera guider. Varje guide hjälper dig att lära dig mer och lägga till nya funktioner i det adaptiva formulär som skapas i den här kursen. Du har ett fungerande anpassningsbart formulär efter varje guide. Guiden för att skapa ett anpassat formulär är tillgänglig. Efterföljande guider kommer snart att vara tillgängliga. I slutet av den här självstudiekursen kan du:

* Skapa ett anpassningsbart formulär och en formulärdatamodell.
* Formatera den anpassningsbara formen.
* Använd redigerare för anpassade formulärregler för att skapa affärsregler.
* Testa och publicera ett adaptivt formulär.

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

Resan börjar med att man lär sig hur det fungerar:

En webbplats erbjuder en rad produkter för olika kunder. Kunderna går igenom portalen, väljer ut och beställer produkterna. Alla kunder skapar ett konto och tillhandahåller frakt- och faktureringsadresser. En befintlig kund, Sara Rose, vill lägga till sin leveransadress på webbplatsen. På webbplatsen finns ett onlineformulär där du kan lägga till och uppdatera leveransadresser.

Webbplatsen körs på Adobe Experience Manager (AEM) och använder AEM [!DNL Forms] för datainhämtning och -bearbetning. Formuläret för att lägga till och uppdatera adresser är ett anpassat formulär. Webbplatsen lagrar kundinformation i en databas. De använder formuläret för att lägga till och uppdatera adresser för att hämta och visa tillgängliga adresser. De använder också det adaptiva formuläret för att godkänna uppdaterade och nya adresser.

### Förutsättning {#prerequisite}

* Konfigurera en [AEM författarinstans](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#author-and-publish-installs)
* Installera [AEM Forms-tillägg](../../forms/using/installing-configuring-aem-forms-osgi.md) on author instance.
* Hämta JDBC-databasdrivrutin (JAR-fil) från databasprovidern. Exemplen i självstudiekursen är baserade på [!DNL MySQL] databas och användning [!DNL Oracle's] [MySQL JDBC-databasdrivrutin](https://dev.mysql.com/downloads/connector/j/5.1.html).

* Konfigurera en databas som innehåller kunddata med fälten som visas nedan. En databas behövs inte för att skapa ett anpassningsbart formulär. I den här självstudiekursen används en databas för att visa formulärdatamodell och beständighetsfunktioner för AEM [!DNL Forms].

![adaptiveformdata](assets/adaptiveformdata.png)

## Steg 1: Skapa ett anpassat formulär {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

Adaptiva former är ny generation, engagerande, responsiva, dynamiska och anpassningsbara till sin natur. Med hjälp av anpassningsbara formulär kan ni leverera personaliserade och målinriktade upplevelser. AEM [!DNL Forms] har en WYSIWYG-redigerare som du kan dra och släppa för att skapa anpassningsbara formulär. Mer information om adaptiva formulär finns i [Introduktion till utveckling av anpassningsbara formulär](../../forms/using/introduction-forms-authoring.md).

Mål:

* Skapa ett anpassningsbart formulär där kunden kan lägga till en leveransadress
* Layoutfält i ett anpassat formulär som visar och accepterar information från en kund
* Skapa en Skicka-åtgärd för att skicka ett e-postmeddelande med formulärinnehåll
* Förhandsgranska och skicka ett anpassat formulär

[![Se guiden](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## Steg 2: Skapa formulärdatamodell {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

En formulärdatamodell gör det möjligt att koppla ett anpassningsbart formulär till olika datakällor. AEM användarprofil, RESTful-webbtjänster, SOAP-baserade webbtjänster, OData-tjänster och relationsdatabaser. En formulärdatamodell är ett enhetligt datarepresentationsschema för affärsenheter och tjänster som är tillgängliga i anslutna datakällor. Du kan använda formulärdatamodellen med ett adaptivt formulär för att hämta, uppdatera, ta bort och lägga till data i anslutna datakällor.

Mål:

* Konfigurera webbplatsens databasinstans ([!DNL MySQL] databas) som datakällor
* Skapa formulärdatamodellen med [!DNL MySQL] databas som en datakälla
* Lägga till datamodellobjekt i formulärdatamodellen
* Konfigurera läs- och skrivtjänster för formulärdatamodellen
* Testa formulärdatamodell och konfigurerade tjänster med testdata

[![Se guiden](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## Steg 3: Använd regler för anpassningsbara formulärfält {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Anpassade formulär ger en redigerare som kan skriva regler för adaptiva formulärobjekt. Dessa regler definierar åtgärder som ska utlösas av formulärobjekt baserat på förinställda villkor, användarindata och användaråtgärder i formuläret. Det gör att man kan säkerställa att blanketterna blir korrekta och snabbare.

Mål:

* Skapa och tillämpa regler för anpassade formulärfält
* Använd regler för att aktivera datamodelltjänster för formulär för att uppdatera data till databasen

[![Se guiden](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## Steg 4: Formatera en anpassad blankett {#step-style-your-adaptive-form}

![adapative-form-style](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

Adaptiva formulär ger teman och en [redigerare](../../forms/using/themes.md) för att skapa teman för de adaptiva formulären. Ett tema innehåller formatinformation för komponenter och paneler, och du kan återanvända ett tema i olika former. Format innehåller egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet, justering och storlek. När du använder temat i formuläret återspeglas det angivna formatet i motsvarande komponenter i formuläret. Anpassningsbara formulär har även stöd för infogad formatering för format som är specifika för ett formulär.

Mål:

* Använda ett tema i ett anpassat formulär
* Skapa ett tema för anpassningsbara formulär med temaredigeraren
* Använda webbteckensnitt i ett anpassat tema

[![Se guiden](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## Steg 5: Publicera ditt anpassningsbara formulär {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

Du kan publicera anpassningsbara formulär som ett fristående formulär (single page application), som kan inkluderas i AEM [Sidan Platser](/help/forms/using/embed-adaptive-form-aem-sites.md), eller lista på en AEM [!DNL Site] använda [Forms Portal](../../forms/using/introduction-publishing-forms.md).

Mål:

* Publicera det adaptiva formuläret som en AEM sida
* Bädda in det anpassningsbara formuläret i en AEM [!DNL Sites] Sida
* Bädda in det adaptiva formuläret på en extern webbsida (en icke-AEM webbsida som finns på andra AEM)

[![Se guiden](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)
