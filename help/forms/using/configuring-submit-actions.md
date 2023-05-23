---
title: Konfigurera åtgärden Skicka
seo-title: Configuring the Submit action
description: Med Forms kan du konfigurera en skicka-åtgärd för att definiera hur ett anpassat formulär ska bearbetas när det har skickats in. Du kan använda inbyggda skicka-åtgärder eller skriva egna från grunden.
uuid: 4368d648-88ea-4f84-a051-46296a1a084e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9d8d7044-ffce-4ab4-9543-a2d2f9da31e3
docset: aem65
feature: Adaptive Forms
exl-id: 04efb4ad-cff6-4e05-bcd2-98102f052452
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 0%

---

# Konfigurera åtgärden Skicka{#configuring-the-submit-action}

## Introduktion till att skicka åtgärder {#introduction-to-submit-actions}

En sändningsåtgärd utlöses när en användare klickar på knappen Skicka i ett anpassat formulär. Du kan konfigurera åtgärden skicka i anpassningsbara formulär. Med adaptiva formulär kan du skicka in ett antal åtgärder direkt. Du kan kopiera och utöka standardåtgärderna för att skicka och skapa en egen sändningsåtgärd. Baserat på dina krav kan du dock skriva och registrera din egen skicka-åtgärd för att bearbeta data i det skickade formuläret. Skicka-åtgärden kan använda [synkron eller asynkron överföring](../../forms/using/asynchronous-submissions-adaptive-forms.md).

Du kan konfigurera en skicka-åtgärd i **Inlämning** i egenskaperna för den adaptiva formulärbehållaren i sidlisten.

![Konfigurera Skicka-åtgärd](assets/thank-you-setting.png)

Konfigurera Skicka-åtgärd

Standardåtgärderna för att skicka in anpassningsbara formulär är:

* Skicka till REST-slutpunkt
* Skicka e-post
* Skicka PDF via e-post
* Anropa en Forms Workflow
* Skicka med formulärdatamodell
* Forms Portal Submit Action
* Anropa ett AEM arbetsflöde

>[!NOTE]
>
>Åtgärden Skicka PDF via e-post gäller endast för adaptiva formulär som använder XFA-mall som formulärmodell.

>[!NOTE]
>
>Se till att [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>finns. Katalogen krävs för att temporärt lagra bilagor. Om katalogen inte finns skapar du den.

>[!CAUTION]
>
>Om du [prefill](../../forms/using/prepopulate-adaptive-form-fields.md) en formulärmall, formulärdatamodell eller schemabaserad adaptiv form med XML- eller JSON-data som klagomål till ett schema (XML-schema, JSON-schema, formulärmall eller formulärdatamodell) som inte innehåller data &lt;afdata>, &lt;afbounddata>och &lt;/afunbounddata> taggar, så är data i oavgränsade fält (oavgränsade fält) adaptiva formulärfält utan [bindref](../../forms/using/prepopulate-adaptive-form-fields.md) egenskap) för det adaptiva formuläret har gått förlorat.

Du kan skriva en anpassad skicka-åtgärd för anpassade formulär för att uppfylla ditt användningssätt. Mer information finns i [Skriva anpassad skickaåtgärd för anpassningsbara formulär](../../forms/using/custom-submit-action-form.md).

## Skicka till REST-slutpunkt {#submit-to-rest-endpoint}

The **Skicka till REST-slutpunkt** Skicka-alternativet skickar data som fylls i formuläret till en konfigurerad bekräftelsesida som en del av HTTP GET-begäran. Du kan lägga till namnet på fälten som ska begäras. Begäran har följande format:

`{fieldName}={request parameter name}`

Som visas i bilden nedan `param1` och `param2` skickas som parametrar med värden som kopierats från **textruta** och **numeric box** fält för nästa åtgärd.

Du kan också **Aktivera begäran om POST** och ange en URL för att skicka begäran. Om du vill skicka data till Experience Manager-servern som är värd för formuläret använder du en relativ sökväg som motsvarar rotsökvägen för Experience Manager-servern. Exempel: /content/forms/af/SampleForm.html. Om du vill skicka data till en annan server använder du den absoluta sökvägen.

![Konfigurerar åtgärden Skicka för resterande slutpunkt](assets/action-config.png)

Konfigurerar åtgärden Skicka för resterande slutpunkt

>[!NOTE]
Om du vill skicka fälten som parametrar i en REST-URL måste alla fält ha olika elementnamn, även om fälten placeras på olika paneler.

### Bokför skickade data till en resurs eller extern slutpunkt för vila  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

Använd **Skicka till REST-slutpunkt** åtgärd för att skicka skickade data till en rest-URL. URL:en kan vara en intern (servern som formuläret återges på) eller en extern server.

Om du vill skicka data till en intern server anger du sökvägen till resursen. Data bokförs som resurssökväg. Till exempel /content/restEndPoint. För sådana efterfrågningar används autentiseringsinformationen i förfrågan.

Ange en URL om du vill skicka data till en extern server. URL-adressen har formatet https://host:port/path_to_rest_end_point. Se till att du konfigurerar sökvägen så att den hanterar POSTENS begäran anonymt.

![Mappning för fältvärden skickas som Tack-sidan-parametrar](assets/post-enabled-actionconfig.png)

I exemplet ovan har användaren angett information i `textbox` hämtas med parameter `param1`. Syntax för att bokföra data som samlats in med `param1` är:

`String data=request.getParameter("param1");`

På samma sätt är parametrar som du använder för att bokföra XML-data och bifogade filer `dataXml` och `attachments`.

Du kan till exempel använda de här två parametrarna i skriptet för att tolka data till en slutpunkt. Du använder följande syntax för att lagra och analysera data:

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

I det här exemplet `data` lagrar XML-data, och `att` lagrar data för bifogade filer.

## Skicka e-post {#send-email}

The **Skicka e-post** skickar en åtgärd ett e-postmeddelande till en eller flera mottagare när formuläret har skickats. E-postmeddelandet som genereras kan innehålla formulärdata i ett fördefinierat format.

>[!NOTE]
Alla formulärfält måste ha olika elementnamn, även om de finns på olika paneler), för att kunna inkludera formulärdata i ett e-postmeddelande.

## Skicka PDF via e-post {#send-pdf-via-email}

The **Skicka PDF via e-post** skicka-åtgärd skickar ett e-postmeddelande med ett PDF som innehåller formulärdata till en eller flera mottagare när formuläret har skickats.

>[!NOTE]
Den här överföringsåtgärden är tillgänglig för XFA-baserade adaptiva formulär och XSD-baserade adaptionsformulär som har dokumentmallen.

## Anropa en Forms Workflow {#invoke-a-forms-workflow}

The **Skicka till Forms Workflow** Skicka-alternativet skickar en XML-datafil och eventuella bifogade filer till en befintlig JEE-process i Adobe eller AEM Forms.

Mer information om hur du konfigurerar åtgärden Skicka till Forms Workflow finns i [Skicka och bearbeta formulärdata med hjälp av formulärarbetsflöden](../../forms/using/submit-form-data-livecycle-process.md).

## Skicka med formulärdatamodell {#submit-using-form-data-model}

The **Skicka med formulärdatamodell** skicka-åtgärd skriver skickade adaptiva formulärdata för det angivna datamodellsobjektet i en formulärdatamodell till sin datakälla. När du konfigurerar skicka-åtgärden kan du välja ett datamodellsobjekt vars skickade data du vill skriva tillbaka till dess datakälla.

Dessutom kan du skicka en bifogad fil med hjälp av en formulärdatamodell och en DoR-fil (Document of Record) till datakällan.

Mer information om formulärdatamodell finns i [AEM Forms dataintegrering](../../forms/using/data-integration.md).

## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** gör formulärdata tillgängliga via en AEM Forms Portal.

Mer information om Forms Portal och skicka-åtgärden finns i [Komponenten Utkast och inskickat material](../../forms/using/draft-submission-component.md).

## Anropa ett AEM arbetsflöde {#invoke-an-aem-workflow}

The **[!UICONTROL Invoke an AEM Workflow]** Åtgärden Skicka associerar ett anpassat formulär med ett [AEM](/help/sites-developing/workflows-models.md). När ett formulär skickas startar det associerade arbetsflödet automatiskt på författarinstansen. Du kan spara datafilen, bifogade filer och postdokument i mappen relativt eller under arbetsflödets eller variabelns nyttolast. Om arbetsflödet är markerat för extern datalagring är variabelalternativet tillgängligt och inte nyttolastalternativet. Du kan välja i listan över variabler som är tillgängliga för arbetsflödesmodellen. Om arbetsflödet markeras för extern datalagring i ett senare skede och inte när arbetsflödet skapas, kontrollerar du att de variabelkonfigurationer som krävs finns på plats.

Innan du använder **Anropa ett AEM arbetsflöde** skicka-åtgärd, [konfigurera inställningarna för Experience Manager DS](../../forms/using/configuring-the-processing-server-url-.md). Mer information om hur du skapar ett AEM arbetsflöde finns i [Formulärbaserade arbetsflöden i OSGi](../../forms/using/aem-forms-workflow.md).

Åtgärden Skicka placerar följande på arbetsflödets nyttolastplats. Observera dock att endast alternativet Variabel visas om arbetsflödesmodellen är markerad för extern datalagring, och inte nyttolastalternativet.

* **Datafil**: Den innehåller data som skickats till den adaptiva formen. Du kan använda **[!UICONTROL Data File Path]** om du vill ange filens namn och sökväg i förhållande till nyttolasten. Till exempel `/addresschange/data.xml` sökväg skapar en mapp med namnet `addresschange` och placerar den i förhållande till nyttolasten. Du kan också bara ange `data.xml` om du bara vill skicka skickade data utan att skapa en mapphierarki. Använd variabelalternativet och välj variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

>[!NOTE]
Variabler kan användas oavsett om arbetsflödesmodellen är markerad för extern datalagring eller inte.

* **Bifogade filer**: Du kan använda **[!UICONTROL Attachment Path]** om du vill ange mappnamnet för lagring av de bilagor som överförts till det adaptiva formuläret. Mappen skapas i förhållande till nyttolasten. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

* **Dokument**: Det innehåller det dokument med post som genererats för det adaptiva formuläret. Du kan använda **[!UICONTROL Document of Record Path]** om du vill ange namnet på filen Dokument för post och sökvägen till filen i förhållande till nyttolasten. Till exempel `/addresschange/DoR.pdf` sökväg skapar en mapp med namnet `addresschange` i förhållande till nyttolasten och placerar `DoR.pdf` i förhållande till nyttolast. Du kan också bara ange `DoR.pdf` om du bara vill spara postdokument utan att skapa en mapphierarki. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

## Förtroende på serversidan i adaptiv form {#server-side-revalidation-in-adaptive-form}

I alla onlinesystem för datainhämtning lägger utvecklare vanligtvis in JavaScript-valideringar på klientsidan för att tillämpa några få affärsregler. Men i moderna webbläsare kan slutanvändarna kringgå valideringarna och skicka in dokument manuellt med hjälp av olika tekniker, till exempel DevTools Console för webbläsare. Sådana tekniker gäller också för adaptiva formulär. En formulärutvecklare kan skapa olika valideringslogik, men tekniskt sett kan slutanvändarna kringgå dessa valideringslogik och skicka ogiltiga data till servern. Ogiltiga data skulle bryta mot de affärsregler som en formulärförfattare har infört.

Med funktionen för omvalidering på serversidan kan du även köra de valideringar som en författare av adaptiva formulär har tillhandahållit när de utformar ett adaptivt formulär på servern. Det förhindrar att inskickade data äventyras och affärsregelöverträdelser som representeras i form av formulärvalidering.

### Vad ska valideras på servern? {#what-to-validate-on-server-br}

Alla valideringar av ett anpassningsbart formulär som körs på servern är:

* Obligatoriskt
* Valideringsbildsats
* Valideringsuttryck

### Aktivera validering på serversidan {#enabling-server-side-validation-br}

Använd **Återvalidera på servern** under Adaptiv formulärbehållare i sidofältet för att aktivera eller inaktivera validering på serversidan för det aktuella formuläret.

![Aktivera validering på serversidan](assets/revalidate-on-server.png)

Aktivera validering på serversidan

Om slutanvändaren åsidosätter dessa valideringar och skickar formulären utför servern valideringen igen. Om valideringen misslyckas vid serverslutet stoppas skicka-transaktionen. Slutanvändaren får originalformuläret igen. Insamlade data och skickade data visas för användaren som ett fel.

>[!NOTE]
Validering på serversidan validerar formulärmodellen. Vi rekommenderar att du skapar ett separat klientbibliotek för validering och inte blandar det med andra saker som formatering av HTML och DOM-manipulering i samma klientbibliotek.

### Stöd för anpassade funktioner i valideringsuttryck {#supporting-custom-functions-in-validation-expressions-br}

Ibland finns det komplexa valideringsregler, men det exakta valideringsskriptet finns i anpassade funktioner och författaren anropar dessa anpassade funktioner från fältvalideringsuttryck. Om du vill att det här anpassade funktionsbiblioteket ska vara känt och tillgängligt vid validering på serversidan kan formulärförfattaren konfigurera namnet på AEM klientbibliotek under **Grundläggande** fliken med egenskaper för adaptiv formulärbehållare enligt nedan.

![Stöd för anpassade funktioner i valideringsuttryck](assets/clientlib-cat.png)

Stöd för anpassade funktioner i valideringsuttryck

Författaren kan konfigurera customJavaScript-bibliotek per anpassat formulär. I biblioteket behåller du bara återanvändbara funktioner som är beroende av jquery- och underscore.js-bibliotek från tredje part.

## Felhantering vid sändning {#error-handling-on-submit-action}

Konfigurera anpassade felsidor som 404.jsp och 500.jsp som en del av riktlinjerna för säkerhet och skärpa i Experience Manager. Dessa hanterare anropas när ett formulär 404- eller 500-fel skickas. Hanterarna anropas också när dessa felkoder aktiveras på noden Publicera.

Mer information finns i [Anpassa sidor som visas av felhanteraren](/help/sites-developing/customizing-errorhandler-pages.md).
