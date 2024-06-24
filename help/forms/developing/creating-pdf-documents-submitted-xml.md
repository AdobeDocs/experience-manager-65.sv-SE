---
title: Skapa PDF-dokument med SubmitXML-data
description: Använd tjänsten Forms för att hämta formulärdata som användaren har angett i ett interaktivt formulär. Skicka formulärdata till en annan AEM Forms-tjänståtgärd och skapa ett PDF-dokument med hjälp av data.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d9d5b94a-9d10-4d90-9e10-5142f30ba4a3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 0%

---

# Skapa PDF-dokument med inskickade XML-data {#creating-pdf-documents-with-submittedxml-data}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

## Skapa PDF-dokument med inskickade XML-data {#creating-pdf-documents-with-submitted-xml-data}

Webbaserade tillämpningar där användarna kan fylla i interaktiva formulär kräver att data skickas tillbaka till servern. Med tjänsten Forms kan du hämta formulärdata som användaren har angett i ett interaktivt formulär. Sedan kan du skicka formulärdata till en annan AEM Forms-tjänståtgärd och skapa ett PDF-dokument med hjälp av data.

>[!NOTE]
>
>Innan du läser det här innehållet bör du ha en god förståelse för hur skickade formulär hanteras. Begrepp som förhållandet mellan en formulärdesign och inlämnade XML-data behandlas i Hantera inlämnade Forms.

Tänk på följande arbetsflöde som innefattar tre AEM Forms-tjänster:

* En användare skickar XML-data till Forms-tjänsten från ett webbaserat program.
* Forms-tjänsten används för att bearbeta skickade formulär och extrahera formulärfält. Formulärdata kan bearbetas. Data kan till exempel skickas till en företagsdatabas.
* Formulärdata skickas till utdatatjänsten för att skapa ett icke-interaktivt PDF-dokument.
* Det icke-interaktiva PDF-dokumentet lagras i Content Services (utgått).

I följande diagram visas arbetsflödet.

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

När användaren har skickat formuläret från klientens webbläsare lagras det icke-interaktiva PDF-dokumentet i Content Services (utgått). Följande bild visar ett PDF-dokument som lagras i Content Services (utgått).

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### Sammanfattning av steg {#summary-of-steps}

Gör så här om du vill skapa ett icke-interaktivt PDF-dokument med inskickade XML-data och lagra i PDF-dokumentet i Content Services (utgått):

1. Inkludera projektfiler.
1. Skapa Forms-, Output- och Document Management-objekt.
1. Hämta formulärdata med hjälp av tjänsten Forms.
1. Skapa ett icke-interaktivt PDF-dokument med hjälp av utdatatjänsten.
1. Lagra PDF-formuläret i innehållstjänster (borttaget) med hjälp av dokumenthanteringstjänsten.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa Forms-, Output- och Document Management-objekt**

Skapa ett Forms Client API-objekt innan du programmässigt utför en API-åtgärd för Forms-tjänster. Eftersom arbetsflödet anropar utdata- och dokumenthanteringstjänsterna skapar du både ett Output Client API-objekt och ett Document Management Client API-objekt.

**Hämta formulärdata med tjänsten Forms**

Hämta formulärdata som skickats till Forms-tjänsten. Du kan bearbeta inskickade data så att de uppfyller dina affärskrav. Du kan till exempel lagra formulärdata i en företagsdatabas. Om du vill skapa ett icke-interaktivt PDF-dokument skickas formulärdata till utdatatjänsten.

**Skapa ett icke-interaktivt PDF-dokument med hjälp av utdatatjänsten.**

Använd utdatatjänsten för att skapa ett icke-interaktivt PDF-dokument som är baserat på en formulärdesign och XML-formulärdata. I arbetsflödet hämtas formulärdata från Forms-tjänsten.

**Lagra PDF-formuläret i Content Services (utgått) med hjälp av tjänsten Document Management**

Använd API:t för dokumenthanteringstjänsten för att lagra ett PDF-dokument i innehållstjänster (borttaget).

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Skapa ett PDF-dokument med skickade XML-data med Java API {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Skapa ett PDF-dokument med inskickade XML-data med hjälp av Forms, Output och Document Management API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar, adobe-output-client.jar och adobe-contentservices-client.jar i Java-projektets klassökväg.

1. Skapa Forms-, Output- och Document Management-objekt

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `FormsServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.
   * Skapa en `OutputClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.
   * Skapa en `DocumentManagementServiceClientImpl` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta formulärdata med tjänsten Forms

   * Anropa `FormsServiceClient` objektets `processFormSubmission` och skicka följande värden:

      * The `com.adobe.idp.Document` som innehåller formulärdata.
      * Ett strängvärde som anger miljövariabler, inklusive alla relevanta HTTP-rubriker. Ange vilken innehållstyp som ska hanteras genom att ange ett eller flera värden för `CONTENT_TYPE` miljövariabel. Om du till exempel vill hantera XML-data anger du följande strängvärde för den här parametern: `CONTENT_TYPE=text/xml`.
      * Ett strängvärde som anger `HTTP_USER_AGENT` rubrikvärde, som `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` objekt som lagrar körningsalternativ.

     The `processFormSubmission` returnerar en `FormsResult` objekt som innehåller resultaten av formuläröverföringen.

   * Kontrollera om Forms-tjänsten har bearbetat formulärdata genom att anropa `FormsResult` objektets `getAction` -metod. Om den här metoden returnerar värdet `0`är data färdiga att bearbetas.
   * Hämta formulärdata genom att skapa en `com.adobe.idp.Document` genom att anropa `FormsResult` objektets `getOutputContent` -metod. (Det här objektet innehåller formulärdata som kan skickas till utdatatjänsten.)
   * Skapa en `java.io.InputStream` genom att anropa `java.io.DataInputStream` konstruktorn och skickar `com.adobe.idp.Document` -objekt.
   * Skapa en `org.w3c.dom.DocumentBuilderFactory` genom att anropa det statiska `org.w3c.dom.DocumentBuilderFactory` objektets `newInstance` -metod.
   * Skapa en `org.w3c.dom.DocumentBuilder` genom att anropa `org.w3c.dom.DocumentBuilderFactory` objektets `newDocumentBuilder` -metod.
   * Skapa en `org.w3c.dom.Document` genom att anropa `org.w3c.dom.DocumentBuilder` objektets `parse` metoden och skicka `java.io.InputStream` -objekt.
   * Hämta värdet för varje nod i XML-dokumentet. Ett sätt att utföra den här uppgiften är att skapa en anpassad metod som accepterar två parametrar: `org.w3c.dom.Document` och namnet på noden vars värde du vill hämta. Den här metoden returnerar ett strängvärde som representerar nodens värde. I kodexemplet som följer den här processen anropas den här anpassade metoden `getNodeText`. Innehållet i den här metoden visas.

1. Skapa ett icke-interaktivt PDF-dokument med hjälp av utdatatjänsten.

   Skapa ett PDF-dokument genom att anropa `OutputClient` objektets `generatePDFOutput` och skicka följande värden:

   * A `TransformationFormat` enum-värde. Om du vill generera ett dokument i PDF anger du `TransformationFormat.PDF`.
   * Ett strängvärde som anger formulärdesignens namn. Kontrollera att formulärdesignen är kompatibel med formulärdata som hämtas från Forms-tjänsten.
   * Ett strängvärde som anger innehållsroten där formulärdesignen finns.
   * A `PDFOutputOptionsSpec` objekt som innehåller körningsalternativ för PDF.
   * A `RenderOptionsSpec` objekt som innehåller alternativ för återgivning vid körning.
   * The `com.adobe.idp.Document` objekt som innehåller XML-datakällan som innehåller data som ska sammanfogas med formulärdesignen. Kontrollera att objektet returnerades av `FormsResult` objektets `getOutputContent` -metod.
   * The `generatePDFOutput` returnerar en `OutputResult` objekt som innehåller resultatet av åtgärden.
   * Hämta det icke-interaktiva PDF-dokumentet genom att anropa `OutputResult` objektets `getGeneratedDoc` -metod. Den här metoden returnerar en `com.adobe.idp.Document` -instans som representerar det icke-interaktiva PDF-dokumentet.

1. Lagra PDF-formuläret i Content Services (utgått) med hjälp av tjänsten Document Management

   Lägg till innehållet genom att anropa `DocumentManagementServiceClientImpl` objektets `storeContent` och skicka följande värden:

   * Ett strängvärde som anger den lagringsplats där innehållet läggs till. Standardarkivet är `SpacesStore`. Detta värde är en obligatorisk parameter.
   * Ett strängvärde som anger den fullständiga sökvägen för det utrymme där innehållet läggs till (till exempel `/Company Home/Test Directory`). Detta värde är en obligatorisk parameter.
   * Nodnamnet som representerar det nya innehållet (till exempel `MortgageForm.pdf`). Detta värde är en obligatorisk parameter.
   * Ett strängvärde som anger nodtypen. Om du vill lägga till nytt innehåll, till exempel en PDF-fil, anger du `{https://www.alfresco.org/model/content/1.0}content`. Detta värde är en obligatorisk parameter.
   * A `com.adobe.idp.Document` objekt som representerar innehållet. Detta värde är en obligatorisk parameter.
   * Ett strängvärde som anger kodningsvärdet (till exempel `UTF-8`). Detta värde är en obligatorisk parameter.
   * An `UpdateVersionType` uppräkningsvärde som anger hur versionsinformation ska hanteras (till exempel `UpdateVersionType.INCREMENT_MAJOR_VERSION` för att öka innehållsversionen. ) Det här värdet är en obligatorisk parameter.
   * A `java.util.List` -instans som anger aspekter som är relaterade till innehållet. Det här värdet är en valfri parameter och du kan ange `null`.
   * A `java.util.Map` objekt som lagrar innehållsattribut.

   The `storeContent` returnerar en `CRCResult` -objekt som beskriver innehållet. Använda `CRCResult` kan du till exempel hämta innehållets unika identifierarvärde. Om du vill utföra den här åtgärden anropar du `CRCResult` objektets `getNodeUuid` -metod.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
