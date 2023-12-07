---
title: Hantera skickade Forms
description: Använd tjänsten Forms för att hämta inskickade data som har angetts i ett interaktivt formulär. Användaren kan skicka formulärdata i XML-, PDF- och URL UTF-16-format.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 419335b2-2aae-4e83-98ff-18e61b7efa9c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2894'
ht-degree: 0%

---

# Hantera skickade Forms {#handling-submitted-forms}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

Webbaserade tillämpningar där användaren kan fylla i interaktiva formulär kräver att informationen skickas tillbaka till servern. Med tjänsten Forms kan du hämta data som användaren har angett i ett interaktivt formulär. När du har hämtat data kan du bearbeta dem för att uppfylla dina affärskrav. Du kan till exempel lagra data i en databas, skicka data till ett annat program, skicka data till en annan tjänst, sammanfoga data i en formulärdesign, visa data i en webbläsare och så vidare.

Formulärdata skickas till Forms-tjänsten som antingen XML- eller PDF-data, vilket är ett alternativ som ställs in i Designer. Ett formulär som skickas som XML kan användas för att extrahera enskilda fältdatavärden. Det innebär att du kan extrahera värdet för varje formulärfält som användaren har angett i formuläret. Ett formulär som skickas som PDF data är binära data, inte XML-data. Du kan spara formuläret som en PDF-fil eller skicka det till en annan avdelning. Om du vill extrahera data från ett formulär som har skickats som XML och sedan använda formulärdata för att skapa ett PDF-dokument, anropar du en annan AEM Forms-åtgärd. (Se [Skapa PDF-dokument med inskickade XML-data](/help/forms/developing/creating-pdf-documents-submitted-xml.md))

I följande diagram visas data som skickas till en Java-server med namnet `HandleData` från ett interaktivt formulär som visas i en webbläsare.

![hs_hs_handlessubmit](assets/hs_hs_handlesubmit.png)

I följande tabell förklaras stegen i diagrammet.

<table>
 <thead>
  <tr>
   <th><p>Steg</p></th>
   <th><p>Beskrivning</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>En användare fyller i ett interaktivt formulär och klickar på formulärets Skicka-knapp.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Data skickas till <code>HandleData</code> Java Servlet som XML-data.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>The <code>HandleData</code> Java Servlet innehåller programlogik för att hämta data.</p></td>
  </tr>
 </tbody>
</table>

## Hantera skickade XML-data {#handling-submitted-xml-data}

När formulärdata skickas som XML kan du hämta XML-data som representerar skickade data. Alla formulärfält visas som noder i ett XML-schema. Nodvärdena motsvarar de värden som användaren fyllt i. Överväg ett låneformulär där varje fält i formuläret visas som en nod i XML-data. Värdet för varje nod motsvarar värdet som användaren fyller i. Anta att en användare fyller i låneformuläret med data som visas i följande formulär.

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

I följande bild visas motsvarande XML-data som hämtas med hjälp av Forms klienttjänstens API.

![hs_hs_loandata](assets/hs_hs_loandata.png)

Fälten i låneformuläret. Dessa värden kan hämtas med Java XML-klasser.

>[!NOTE]
>
>Formulärdesignen måste vara korrekt konfigurerad i Designer för att data ska kunna skickas som XML-data. Om du vill konfigurera formulärdesignen så att den skickar XML-data kontrollerar du att knappen Skicka som finns i formulärdesignen är inställd på att skicka XML-data. Mer information om hur du ställer in knappen Skicka för att skicka XML-data finns i [AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Hantera skickade PDF-data {#handling-submitted-pdf-data}

Överväg ett webbprogram som anropar Forms-tjänsten. När Forms-tjänsten återger ett interaktivt PDF-formulär till en webbläsare fyller användaren i formuläret och skickar tillbaka det som PDF data. När Forms-tjänsten tar emot data från PDF kan den skicka data från PDF till en annan tjänst eller spara dem som en PDF-fil. I följande diagram visas programmets logikflöde.

![hs_hs_saving_forms](assets/hs_hs_savingforms.png)

I följande tabell beskrivs stegen i det här diagrammet.

<table>
 <thead>
  <tr>
   <th><p>Steg</p></th>
   <th><p>Beskrivning</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>En webbsida innehåller en länk till en Java-server som anropar Forms-tjänsten.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Forms-tjänsten återger ett interaktivt PDF-formulär till webbläsaren.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Användaren fyller i ett interaktivt formulär och klickar på en skicka-knapp. Formuläret skickas tillbaka till Forms-tjänsten som PDF data. Det här alternativet anges i Designer.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Forms-tjänsten sparar data i PDF som en PDF-fil. </p></td>
  </tr>
 </tbody>
</table>

## Hantera skickade URL UTF-16-data {#handling-submitted-url-utf-16-data}

Om formulärdata skickas som URL UTF-16-data kräver klientdatorn Adobe Reader eller Acrobat 8.1 eller senare. Om formulärdesignen innehåller en skicka-knapp med URL-kodade data (HTTP Post) och datakodningsalternativet är UTF-16, måste formulärdesignen ändras i en textredigerare som Anteckningar. Du kan ställa in kodningsalternativet på antingen `UTF-16LE` eller `UTF-16BE` för skicka-knappen. Designer har inte den här funktionen.

>[!NOTE]
>
>Mer information om tjänsten Forms finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Sammanfattning av steg {#summary-of-steps}

Utför följande uppgifter för att hantera skickade formulär:

1. Inkludera projektfiler.
1. Skapa ett Forms Client API-objekt.
1. Hämta formulärdata.
1. Kontrollera om formuläröverföringen innehåller bifogade filer.
1. Bearbeta skickade data.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett Forms Client API-objekt**

Innan du programmässigt kan utföra en API-åtgärd för Forms-tjänstklienten måste du skapa en Forms-tjänstklient. Om du använder Java API skapar du en `FormsServiceClient` -objekt. Om du använder Forms webbtjänst-API skapar du en `FormsService` -objekt.

**Hämta formulärdata**

Om du vill hämta skickade formulärdata anropar du `FormsServiceClient` objektets `processFormSubmission` -metod. När du anropar den här metoden måste du ange innehållstypen för det skickade formuläret. När data skickas från en webbläsare till Forms-tjänsten kan de skickas som antingen XML- eller PDF-data. Om du vill hämta data som anges i formulärfält kan dessa data skickas som XML-data.

Du kan även hämta formulärfält från ett formulär som har skickats som PDF-data genom att ange följande körningsalternativ:

* Skicka följande värde till `processFormSubmission` som innehållstypparametern: `CONTENT_TYPE=application/pdf`.
* Ange `RenderOptionsSpec` objektets `PDFToXDP` värde till `true`
* Ange `RenderOptionsSpec` objektets `ExportDataFormat` värde till `XMLData`

Du anger innehållstypen för det skickade formuläret när du anropar `processFormSubmission` -metod. I följande lista anges tillämpliga värden för innehållstyp:

* **text/xml**: Representerar innehållstypen som ska användas när ett PDF-formulär skickar formulärdata som XML.
* **application/x-www-form-urlencoded**: Representerar innehållstypen som ska användas när ett HTML-formulär skickar data som XML.
* **application/pdf**: Representerar innehållstypen som ska användas när ett PDF-formulär skickar data som PDF.

>[!NOTE]
>
>Du kommer att märka att det finns tre motsvarande snabbstarter kopplade till avsnittet Hantera skickade Forms. Hanteringen av PDF forms som har skickats som PDF med Java API-snabbstarten visar hur inskickade PDF-data hanteras. Innehållstypen som anges i snabbstarten är `application/pdf`. I PDF forms Hantera som skickas som XML med Java API-snabbstarten visas hur inskickade XML-data från ett PDF-formulär hanteras. Innehållstypen som anges i snabbstarten är `text/xml`. På samma sätt visar Hantera HTML-formulär som har skickats som XML med Java API-snabbstarten hur du hanterar skickade XML-data som har skickats från ett HTML-formulär. Innehållstypen som anges i snabbstarten är application/x-www-form-urlencoded.

Du hämtar formulärdata som har skickats till Forms-tjänsten och fastställer bearbetningstillståndet. Det vill säga, när data skickas till Forms-tjänsten behöver det inte innebära att Forms-tjänsten är klar med databehandlingen och att data är klara att bearbetas. Data kan till exempel skickas till Forms så att en beräkning kan utföras. När beräkningen är klar återges formuläret tillbaka till användaren med beräkningsresultaten visade. Innan du bearbetar inskickade data bör du ta reda på om Forms-tjänsten har slutfört databearbetningen.

Forms-tjänsten returnerar följande värden för att ange om databearbetningen är klar:

* **0 (Skicka):** Skickade data är klara att bearbetas.
* **1 (Beräkna):** Forms-tjänsten utförde en beräkningsåtgärd för data och resultaten måste återges för användaren.
* **2 (Validera):** Forms-tjänsten validerade formulärdata och resultaten måste återges för användaren.
* **3 (Nästa):** Den aktuella sidan har ändrats med resultat som måste skrivas till klientprogrammet.
* **4 (föregående**): Den aktuella sidan har ändrats med resultat som måste skrivas till klientprogrammet.

>[!NOTE]
>
>Beräkningar och valideringar måste återges för användaren. (Se [Beräknar formulärdata](/help/forms/developing/calculating-form-data.md#calculating-form-data).

**Kontrollera om formuläröverföringen innehåller bifogade filer**

Forms som skickas till Forms kan innehålla bifogade filer. Med Acrobat inbyggda bilagefanel kan man t.ex. markera bifogade filer som ska skickas tillsammans med formuläret. Användaren kan också markera bifogade filer med hjälp av verktygsfältet HTML som återges med en HTML-fil.

När du har fastställt om ett formulär innehåller bifogade filer kan du bearbeta data. Du kan till exempel spara den bifogade filen i det lokala filsystemet.

>[!NOTE]
>
>Formuläret måste skickas som data i PDF för att du ska kunna hämta bifogade filer. Om formuläret skickas som XML-data skickas inga bifogade filer.

**Bearbeta skickade data**

Beroende på innehållstypen för inskickade data kan du extrahera enskilda formulärfältsvärden från inskickade XML-data eller spara inskickade PDF-data som en PDF-fil (eller skicka dem till en annan tjänst). Om du vill extrahera enskilda formulärfält konverterar du inskickade XML-data till en XML-datakälla och hämtar sedan XML-datakällsvärden med hjälp av `org.w3c.dom` -klasser.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Skicka dokument till Forms](/help/forms/developing/passing-documents-forms-service.md)

[Skapa webbprogram som återger Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Hantera skickade formulär med Java API {#handle-submitted-forms-using-the-java-api}

Hantera inskickade formulär med Forms API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar, i Java-projektets klassökväg.

1. Skapa ett Forms Client API-objekt

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `FormsServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta formulärdata

   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och anropa `javax.servlet.http.HttpServletResponse` objektets `getInputStream` -metoden inifrån konstruktorn.
   * Skapa en `RenderOptionsSpec` genom att använda dess konstruktor. Ange språkvärdet genom att anropa `RenderOptionsSpec` objektets `setLocale` och skickar ett strängvärde som anger språkvärdet.

   >[!NOTE]
   >
   >Du kan instruera Forms att skapa XDP- eller XML-data från inskickat PDF-innehåll genom att anropa `RenderOptionsSpec` objektets `setPDF2XDP` metod och att skicka `true` och även ringa `setXMLData` och skicka `true`. Du kan sedan anropa `FormsResult` objektets `getOutputXML` metod för att hämta XML-data som motsvarar XDP/XML-data. (Med `FormsResult` objektet returneras av `processFormSubmission` som förklaras i nästa delsteg.)

   * Anropa `FormsServiceClient` objektets `processFormSubmission` och skicka följande värden:

      * The `com.adobe.idp.Document` som innehåller formulärdata.
      * Ett strängvärde som anger miljövariabler inklusive alla relevanta HTTP-huvuden. Ange den innehållstyp som ska hanteras. Om du vill hantera XML-data anger du följande strängvärde för den här parametern: `CONTENT_TYPE=text/xml`. Om du vill hantera PDF data anger du följande strängvärde för den här parametern: `CONTENT_TYPE=application/pdf`.
      * Ett strängvärde som anger `HTTP_USER_AGENT` rubrikvärde, till exempel . `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Det här parametervärdet är valfritt.
      * A `RenderOptionsSpec` objekt som lagrar körningsalternativ.

     The `processFormSubmission` returnerar en `FormsResult` objekt som innehåller resultaten av formuläröverföringen.

   * Kontrollera om Forms-tjänsten har bearbetat formulärdata genom att anropa `FormsResult` objektets `getAction` -metod. Om den här metoden returnerar värdet `0`är data färdiga att bearbetas.

1. Kontrollera om formuläröverföringen innehåller bifogade filer

   * Anropa `FormsResult` objektets `getAttachments` -metod. Den här metoden returnerar en `java.util.List` objekt som innehåller filer som har skickats med formuläret.
   * Iterera genom `java.util.List` -objekt för att avgöra om det finns bifogade filer. Om det finns bifogade filer är varje element ett `com.adobe.idp.Document` -instans. Du kan spara de bifogade filerna genom att anropa `com.adobe.idp.Document` objektets `copyToFile` metod och skicka en `java.io.File` -objekt.

   >[!NOTE]
   >
   >Det här steget gäller endast om formuläret skickas in som PDF.

1. Bearbeta skickade data

   * Om datainnehållstypen är `application/vnd.adobe.xdp+xml` eller `text/xml`skapar du programlogik för att hämta XML-datavärden.

      * Skapa en `com.adobe.idp.Document` genom att anropa `FormsResult` objektets `getOutputContent` -metod.
      * Skapa en `java.io.InputStream` genom att anropa `java.io.DataInputStream` konstruktorn och skickar `com.adobe.idp.Document` -objekt.
      * Skapa en `org.w3c.dom.DocumentBuilderFactory` genom att anropa det statiska `org.w3c.dom.DocumentBuilderFactory` objektets `newInstance` -metod.
      * Skapa en `org.w3c.dom.DocumentBuilder` genom att anropa `org.w3c.dom.DocumentBuilderFactory` objektets `newDocumentBuilder` -metod.
      * Skapa en `org.w3c.dom.Document` genom att anropa `org.w3c.dom.DocumentBuilder` objektets `parse` metoden och skicka `java.io.InputStream` -objekt.
      * Hämta värdet för varje nod i XML-dokumentet. Ett sätt att utföra den här uppgiften är att skapa en anpassad metod som accepterar två parametrar: `org.w3c.dom.Document` och namnet på noden vars värde du vill hämta. Den här metoden returnerar ett strängvärde som representerar nodens värde. I kodexemplet som följer den här processen anropas den här anpassade metoden `getNodeText`. Innehållet i den här metoden visas.

   * Om datainnehållstypen är `application/pdf`skapar du programlogik för att spara inskickade PDF-data som en PDF-fil.

      * Skapa en `com.adobe.idp.Document` genom att anropa `FormsResult` objektets `getOutputContent` -metod.
      * Skapa en `java.io.File` genom att använda dess public-konstruktor. Ange PDF som filnamnstillägg.
      * Fylla i PDF-filen genom att anropa `com.adobe.idp.Document` objektets `copyToFile` metoden och skicka `java.io.File` -objekt.

**Se även**

[Snabbstart (SOAP-läge): Hantera PDF forms som skickats som XML med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[Snabbstart (SOAP-läge): Hantera HTML-formulär som skickats som XML med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[Snabbstart (SOAP-läge): Hantera PDF forms som har skickats som PDF med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Hantera skickade PDF-data med webbtjänstens API {#handle-submitted-pdf-data-using-the-web-service-api}

Hantera inskickade formulär med Forms API (webbtjänst):

1. Inkludera projektfiler

   * Skapa Java-proxyklasser som använder Forms tjänst-WSDL.
   * Inkludera Java-proxyklasserna i klassökvägen.

1. Skapa ett Forms Client API-objekt

   Skapa en `FormsService` och ange autentiseringsvärden.

1. Hämta formulärdata

   * Skapa en `BLOB` genom att använda dess konstruktor.
   * Skapa en `java.io.InputStream` genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getInputStream` -metod.
   * Skapa en `java.io.ByteArrayOutputStream` genom att använda dess konstruktor och skicka längden på `java.io.InputStream` -objekt.
   * Kopiera innehållet i `java.io.InputStream` objektet i `java.io.ByteArrayOutputStream` -objekt.
   * Skapa en bytearray genom att anropa `java.io.ByteArrayOutputStream` objektets `toByteArray` -metod.
   * Fyll i `BLOB` genom att anropa dess `setBinaryData` och skicka bytearrayen som ett argument.
   * Skapa en `RenderOptionsSpec` genom att använda dess konstruktor. Ange språkvärdet genom att anropa `RenderOptionsSpec` objektets `setLocale` och skickar ett strängvärde som anger språkvärdet.
   * Anropa `FormsService` objektets `processFormSubmission` och skicka följande värden:

      * The `BLOB` som innehåller formulärdata.
      * Ett strängvärde som anger miljövariabler inklusive alla relevanta HTTP-huvuden. Ange den innehållstyp som ska hanteras. Om du vill hantera XML-data anger du följande strängvärde för den här parametern: `CONTENT_TYPE=text/xml`. Om du vill hantera PDF data anger du följande strängvärde för den här parametern: `CONTENT_TYPE=application/pdf`.
      * Ett strängvärde som anger `HTTP_USER_AGENT` rubrikvärde, till exempel `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` objekt som lagrar körningsalternativ.
      * En tom `BLOBHolder` objekt som fylls i av metoden.
      * En tom `javax.xml.rpc.holders.StringHolder` objekt som fylls i av metoden.
      * En tom `BLOBHolder` objekt som fylls i av metoden.
      * En tom `BLOBHolder` objekt som fylls i av metoden.
      * En tom `javax.xml.rpc.holders.ShortHolder` objekt som fylls i av metoden.
      * En tom `MyArrayOf_xsd_anyTypeHolder` objekt som fylls i av metoden. Den här parametern används för att lagra bifogade filer som skickas tillsammans med formuläret.
      * En tom `FormsResultHolder` objekt som fylls i av metoden med det formulär som skickas.

     The `processFormSubmission` metoden fyller i `FormsResultHolder` parametern med resultaten av formuläröverföringen.

   * Kontrollera om Forms-tjänsten har bearbetat formulärdata genom att anropa `FormsResult` objektets `getAction` -metod. Om den här metoden returnerar värdet `0`är formulärdata färdiga att bearbetas. Du kan få en `FormsResult` genom att hämta värdet för `FormsResultHolder` objektets `value` datamedlem.

1. Kontrollera om formuläröverföringen innehåller bifogade filer

   Hämta värdet för `MyArrayOf_xsd_anyTypeHolder` objektets `value` datamedlem ( `MyArrayOf_xsd_anyTypeHolder` objektet skickades till `processFormSubmission` metod). Den här datamedlemmen returnerar en array med `Objects`. Varje element i `Object` är en `Object`som motsvarar de filer som har skickats in tillsammans med formuläret. Du kan hämta varje element i arrayen och omvandla det till en `BLOB` -objekt.

1. Bearbeta skickade data

   * Om datainnehållstypen är `application/vnd.adobe.xdp+xml` eller `text/xml`skapar du programlogik för att hämta XML-datavärden.

      * Skapa en `BLOB` genom att anropa `FormsResult` objektets `getOutputContent` -metod.
      * Skapa en bytearray genom att anropa `BLOB` objektets `getBinaryData` -metod.
      * Skapa en `java.io.InputStream` genom att anropa `java.io.ByteArrayInputStream` och skickar bytearrayen.
      * Skapa en `org.w3c.dom.DocumentBuilderFactory` genom att anropa det statiska `org.w3c.dom.DocumentBuilderFactory` objektets `newInstance` -metod.
      * Skapa en `org.w3c.dom.DocumentBuilder` genom att anropa `org.w3c.dom.DocumentBuilderFactory` objektets `newDocumentBuilder` -metod.
      * Skapa en `org.w3c.dom.Document` genom att anropa `org.w3c.dom.DocumentBuilder` objektets `parse` metoden och skicka `java.io.InputStream` -objekt.
      * Hämta värdet för varje nod i XML-dokumentet. Ett sätt att utföra den här uppgiften är att skapa en anpassad metod som accepterar två parametrar: `org.w3c.dom.Document` och namnet på noden vars värde du vill hämta. Den här metoden returnerar ett strängvärde som representerar nodens värde. I kodexemplet som följer den här processen anropas den här anpassade metoden `getNodeText`. Innehållet i den här metoden visas.

   * Om datainnehållstypen är `application/pdf`skapar du programlogik för att spara inskickade PDF-data som en PDF-fil.

      * Skapa en `BLOB` genom att anropa `FormsResult` objektets `getOutputContent` -metod.
      * Skapa en bytearray genom att anropa `BLOB` objektets `getBinaryData` -metod.
      * Skapa en `java.io.File` genom att använda dess public-konstruktor. Ange PDF som filnamnstillägg.
      * Skapa en `java.io.FileOutputStream` genom att använda konstruktorn och skicka `java.io.File` -objekt.
      * Fylla i PDF-filen genom att anropa `java.io.FileOutputStream` objektets `write` och skicka bytearrayen.

**Se även**

[Anropa AEM Forms med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
