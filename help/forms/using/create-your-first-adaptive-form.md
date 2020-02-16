---
title: '"Självstudiekurs: Skapa ditt första adaptiva formulär"'
seo-title: '"Självstudiekurs: Skapa ditt första adaptiva formulär"'
description: Lär dig skapa interaktiva och responsiva blanketter i affärsklass.
seo-description: Lär dig skapa interaktiva och responsiva blanketter i affärsklass.
uuid: ee351a3f-ea6a-4b4c-8045-4948ad51b7c1
topic-tags: introduction
discoiquuid: 1142bcd4-e3a7-41ce-a710-132ae6c21dbe
docset: aem65
translation-type: tm+mt
source-git-commit: d2d4e0d8b538c96a7a05be6ad1012343f49694b3

---


# Självstudiekurs:Skapa ditt första anpassningsbara formulär{#tutorial-create-your-first-adaptive-form}

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## Introduktion {#introduction}

Söker ni en mobilvänlig **formulärupplevelse** som förenklar registreringen, ökar engagemanget och minskar handläggningstiden, **anpassningsbara formulär** passar er perfekt? Adaptiva formulär ger en mobil, automatiserad och analysvänlig formulärupplevelse. Ni kan enkelt skapa formulär som är responsiva och interaktiva till sin natur, använda automatiserade processer för att minska administrativa och repetitiva uppgifter och använda dataanalys för att förbättra och personalisera den upplevelse kunderna har med era formulär.

Den här självstudiekursen ger ett komplett ramverk för att skapa ett anpassningsbart formulär. Självstudiekursen är ordnad i ett användningsfall och i flera guider. Varje guide hjälper dig att lära dig och lägga till nya funktioner i det adaptiva formulär som skapas i den här kursen. Du har ett fungerande anpassningsbart formulär efter varje guide. Guiden för att skapa ett anpassat formulär är tillgänglig. Efterföljande guider kommer snart att vara tillgängliga. I slutet av den här självstudiekursen kan du:

* Skapa ett anpassningsbart formulär och en formulärdatamodell.
* Formatera den anpassningsbara formen.
* Använd redigerare för anpassade formulärregler för att skapa affärsregler.
* Testa och publicera ett anpassningsbart formulär.

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

Resan börjar med att man lär sig hur det fungerar:

En webbplats erbjuder en rad produkter för olika kunder. Kunderna går igenom portalen, väljer ut och beställer produkterna. Alla kunder skapar ett konto och tillhandahåller frakt- och faktureringsadresser. En befintlig kund, Sara Rose, vill lägga till sin leveransadress på webbplatsen. På webbplatsen finns ett onlineformulär där du kan lägga till och uppdatera leveransadresser.

Webbplatsen körs med Adobe Experience Manager (AEM) och använder AEM Forms för datainhämtning och -bearbetning. Formuläret för adresstillägg och uppdatering är ett anpassat formulär. Webbplatsen lagrar kundinformation i en databas. De använder formuläret för att lägga till och uppdatera adresser för att hämta och visa tillgängliga adresser. De använder också det adaptiva formuläret för att godkänna uppdaterade och nya adresser.

### Förutsättning {#prerequisite}

* Konfigurera en AEM-författarinstans.
* Installera [tillägget](../../forms/using/installing-configuring-aem-forms-osgi.md) AEM Forms på författarinstansen.
* Hämta JDBC-databasdrivrutin (JAR-fil) från databasprovidern. Exemplen i självstudien är baserade på MySQL-databasen och använder Oracles JDBC-databasdrivrutin [](https://dev.mysql.com/downloads/connector/j/5.1.html)MySQL.

* Konfigurera en databas som innehåller kunddata med fälten som visas nedan. En databas behövs inte för att skapa ett anpassningsbart formulär. I den här självstudien används en databas för att visa formulärdatamodell och beständighetsfunktioner i AEM Forms.

![adaptiveformdata](assets/adaptiveformdata.png)

## Steg 1: Skapa ett anpassat formulär {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

Adaptiva former är ny generation, engagerande, responsiva, dynamiska och anpassningsbara till sin natur. Med hjälp av anpassningsbara formulär kan ni leverera personaliserade och målinriktade upplevelser. I AEM Forms finns en WYSIWYG-redigerare som du kan dra och släppa för att skapa anpassningsbara formulär. Mer information om adaptiva formulär finns i Introduktion [till utveckling av adaptiva formulär](../../forms/using/introduction-forms-authoring.md).

Mål:

* Skapa ett anpassningsbart formulär där kunden kan lägga till en leveransadress
* Layoutfält i ett anpassat formulär som visar och accepterar information från en kund
* Skapa en Skicka-åtgärd för att skicka ett e-postmeddelande med formulärinnehåll
* Förhandsgranska och skicka ett anpassat formulär

[![Se guiden](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## Steg 2: Skapa formulärdatamodell {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

En formulärdatamodell gör det möjligt att koppla ett anpassningsbart formulär till olika datakällor. Exempel: AEM-användarprofil, RESTful-webbtjänster, SOAP-baserade webbtjänster, OData-tjänster och relationsdatabaser. En formulärdatamodell är ett enhetligt datarepresentationsschema för affärsenheter och tjänster som är tillgängliga i anslutna datakällor. Du kan använda formulärdatamodellen med ett adaptivt formulär för att hämta, uppdatera, ta bort och lägga till data i anslutna datakällor.

Mål:

* Konfigurera webbplatsens databasinstans (MySQL-databas) som en datakälla
* Skapa formulärdatamodellen med MySQL-databasen som en datakälla
* Lägga till datamodellobjekt i formulärdatamodellen
* Konfigurera läs- och skrivtjänster för formulärdatamodellen
* Testa formulärdatamodell och konfigurerade tjänster med testdata

[![Se guiden](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## Steg 3: Tillämpa regler på anpassningsbara formulärfält {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Anpassade formulär ger en redigerare som kan skriva regler för adaptiva formulärobjekt. Dessa regler definierar åtgärder som ska utlösas av formulärobjekt baserat på förinställda villkor, användarindata och användaråtgärder i formuläret. Det gör att man kan säkerställa att blanketterna blir korrekta och snabbare.

Mål:

* Skapa och tillämpa regler för anpassade formulärfält
* Använd regler för att aktivera datamodelltjänster för formulär för att uppdatera data till databasen

[![Se guiden](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## Steg 4:Formatera ditt anpassningsbara formulär {#step-style-your-adaptive-form}

![](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

Anpassningsbara formulär innehåller teman och en [redigerare](../../forms/using/themes.md) för att skapa teman för de adaptiva formulären. Ett tema innehåller formatinformation för komponenter och paneler, och du kan återanvända ett tema i olika former. Format innehåller egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet, justering och storlek. När du använder temat i formuläret återspeglas det angivna formatet i motsvarande komponenter i formuläret. Anpassningsbara formulär har även stöd för infogad formatering för format som är specifika för ett formulär.

Mål:

* Använda ett tema i ett anpassat formulär
* Skapa ett tema för anpassningsbara formulär med temaredigeraren
*  Använda webbteckensnitt i ett anpassat tema

[![Se guiden](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## Steg 5: Testa ditt adaptiva formulär {#step-test-your-adaptive-form}

![11-test-your-adaptive-form](assets/11-test-your-adaptive-form.png)

Anpassningsbara formulär är en väsentlig del av kundinteraktionen. Det är viktigt att testa de adaptiva formulären med alla ändringar du gör i dem. Det är omständligt att testa alla fält i ett formulär. AEM Forms tillhandahåller en SDK (Calvin SDK) för att automatisera testning av adaptiva formulär. Med Calvin kan du automatisera testningen av dina anpassade formulär i webbläsaren.

Mål:

* Skapa testsvit för det anpassade formuläret
* Skapa testfall för anpassade formulär
* Kör testfall

[![Se guiden](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](testing-your-adaptive-form.md)

## Steg 6: Publicera ditt adaptiva formulär {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

Du kan publicera anpassningsbara formulär som ett fristående formulär (program för en sida), ta med på AEM- [webbplatssidan](/help/forms/using/embed-adaptive-form-aem-sites.md)eller en lista på en AEM-webbplats med hjälp av [Forms Portal](../../forms/using/introduction-publishing-forms.md).

Mål:

* Publicera det adaptiva formuläret som en AEM-sida
* Bädda in det anpassningsbara formuläret på en AEM Sites-sida
* Bädda in det adaptiva formuläret på en extern webbsida (en icke-AEM-webbsida som ligger utanför AEM)

[![Se guiden](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)