---
title: Hantera skickade formulär
seo-title: Hantera skickade formulär
description: 'null'
seo-description: 'null'
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Hantera skickade formulär {#handling-submitted-forms}

Webbaserade tillämpningar där användaren kan fylla i interaktiva formulär kräver att informationen skickas tillbaka till servern. Med hjälp av Forms-tjänsten kan du hämta data som användaren har angett i ett interaktivt formulär. När du har hämtat data kan du bearbeta dem för att uppfylla dina affärskrav. Du kan till exempel lagra data i en databas, skicka data till ett annat program, skicka data till en annan tjänst, sammanfoga data i en formulärdesign, visa data i en webbläsare och så vidare.

Formulärdata skickas till Forms-tjänsten som antingen XML- eller PDF-data, vilket är ett alternativ som ställs in i Designer. Ett formulär som skickas som XML kan användas för att extrahera enskilda fältdatavärden. Det innebär att du kan extrahera värdet för varje formulärfält som användaren har angett i formuläret. Ett formulär som skickas som PDF-data är binära data, inte XML-data. Du kan spara formuläret som en PDF-fil eller skicka formuläret till en annan tjänst. Om du vill extrahera data från ett formulär som har skickats som XML och sedan använda formulärdata för att skapa ett PDF-dokument anropar du en annan AEM Forms-åtgärd. (Se [Skapa PDF-dokument med skickade XML-data](/help/forms/developing/creating-pdf-documents-submitted-xml.md))

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
   <td><p>Java- <code>HandleData</code> serverns programlogik för hämtning av data.</p></td>
  </tr>
 </tbody>
</table>

## Hantera skickade XML-data {#handling-submitted-xml-data}

När formulärdata skickas som XML kan du hämta XML-data som representerar skickade data. Alla formulärfält visas som noder i ett XML-schema. Nodvärdena motsvarar de värden som användaren fyllt i. Överväg ett låneformulär där varje fält i formuläret visas som en nod i XML-data. Värdet för varje nod motsvarar värdet som användaren fyller i. Anta att en användare fyller i låneformuläret med data som visas i följande formulär.

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

Följande bild visar motsvarande XML-data som hämtas med hjälp av API:t för Forms-tjänstklienten.

![hs_hs_loandata](assets/hs_hs_loandata.png)

Fälten i låneformuläret. Dessa värden kan hämtas med Java XML-klasser.

>[!NOTE]
>
>Formulärdesignen måste vara korrekt konfigurerad i Designer för att data ska kunna skickas som XML-data. Om du vill konfigurera formulärdesignen så att den skickar XML-data kontrollerar du att knappen Skicka som finns i formulärdesignen är inställd på att skicka XML-data. Mer information om hur du ställer in knappen Skicka för att skicka XML-data finns i [AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Hantera skickade PDF-data {#handling-submitted-pdf-data}

Överväg ett webbprogram som anropar Forms-tjänsten. När Forms-tjänsten återger ett interaktivt PDF-formulär till en webbläsare fyller användaren i formuläret och skickar tillbaka det som PDF-data. När Forms-tjänsten tar emot PDF-data kan den skicka PDF-data till en annan tjänst eller spara dem som en PDF-fil. I följande diagram visas programmets logikflöde.

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
   <td><p>Forms-tjänsten återger ett interaktivt PDF-formulär till klientens webbläsare.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Användaren fyller i ett interaktivt formulär och klickar på en skicka-knapp. Formuläret skickas tillbaka till Forms-tjänsten som PDF-data. Det här alternativet anges i Designer.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Forms-tjänsten sparar PDF-data som en PDF-fil. </p></td>
  </tr>
 </tbody>
</table>

## Hantera skickade URL UTF-16-data {#handling-submitted-url-utf-16-data}

Om formulärdata skickas som URL UTF-16-data kräver klientdatorn Adobe Reader eller Acrobat 8.1 eller senare. Om formulärdesignen innehåller en skicka-knapp med URL-kodade data (HTTP Post) och datakodningsalternativet är UTF-16, måste formulärdesignen ändras i en textredigerare som Anteckningar. Du kan ställa in kodningsalternativet på antingen `UTF-16LE` eller `UTF-16BE` för skicka-knappen. Designer har inte den här funktionen.

>[!NOTE]
>
>Mer information om Forms-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Sammanfattning av steg {#summary-of-steps}

Gör så här för att hantera skickade formulär:

1. Inkludera projektfiler.
1. Skapa ett API-objekt för Forms Client.
1. Hämta formulärdata.
1. Kontrollera om formuläröverföringen innehåller bifogade filer.
1. Bearbeta skickade data.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett API-objekt för FormsClient**

Innan du programmässigt kan utföra en API-åtgärd för Form Service Client måste du skapa en Forms-tjänstklient. Om du använder Java API skapar du ett `FormsServiceClient` objekt. Skapa ett `FormsService` objekt om du använder webbtjänstens API:t för Forms.

**Hämta formulärdata**

Om du vill hämta skickade formulärdata anropar du `FormsServiceClient` objektets `processFormSubmission` metod. När du anropar den här metoden måste du ange innehållstypen för det skickade formuläret. När data skickas från en webbläsare till Forms-tjänsten kan de skickas som antingen XML- eller PDF-data. Om du vill hämta data som anges i formulärfält kan dessa data skickas som XML-data.

Du kan även hämta formulärfält från ett formulär som har skickats som PDF-data genom att ange följande körningsalternativ:

* Skicka följande värde till `processFormSubmission` metoden som innehållstypparameter: `CONTENT_TYPE=application/pdf`.
* Ange `RenderOptionsSpec` objektets `PDFToXDP` värde till `true`
* Ange `RenderOptionsSpec` objektets `ExportDataFormat` värde till `XMLData`

Du anger innehållstypen för det skickade formuläret när du anropar `processFormSubmission` metoden. Följande lista anger tillämpliga värden för innehållstyp:

* **text/xml**: Representerar innehållstypen som ska användas när ett PDF-formulär skickar formulärdata som XML.
* **application/x-www-form-urlencoded**: Representerar innehållstypen som ska användas när ett HTML-formulär skickar data som XML.
* **application/pdf**: Representerar innehållstypen som ska användas när ett PDF-formulär skickar data som PDF.

>[!NOTE]
>
>Du kommer att märka att det finns tre motsvarande snabbstarter kopplade till avsnittet Hantera skickade formulär. Med hjälp av snabbstarten för Java API kan du hantera skickade PDF-formulär som en PDF-fil. Innehållstypen som anges i snabbstarten är `application/pdf`. I hanteringen av PDF-formulär som skickas som XML med Java API-snabbstarten visas hur inskickade XML-data från ett PDF-formulär hanteras. Innehållstypen som anges i snabbstarten är `text/xml`. På samma sätt visar Hantering av HTML-formulär som har skickats som XML med Java API-snabbstarten hur du hanterar skickade XML-data som har skickats från ett HTML-formulär. Innehållstypen som anges i snabbstarten är application/x-www-form-urlencoded.

Du hämtar formulärdata som har registrerats i Forms-tjänsten och fastställer bearbetningstillståndet. Det vill säga, när data skickas till Forms-tjänsten behöver det inte innebära att Forms-tjänsten är klar med databehandlingen och att data är klara att bearbetas. Data kan till exempel skickas till Forms-tjänsten så att en beräkning kan utföras. När beräkningen är klar återges formuläret tillbaka till användaren med beräkningsresultaten visade. Innan du bearbetar skickade data bör du bestämma om Forms-tjänsten har slutfört databearbetningen.

Forms-tjänsten returnerar följande värden för att ange om bearbetningen av data har slutförts:

* **** 0 (Skicka): Skickade data kan nu bearbetas.
* **** 1 (Beräkna): Forms-tjänsten utförde en beräkningsåtgärd för data och resultaten måste återges för användaren.
* **** 2 (Validera): Formulärtjänstens validerade formulärdata och resultaten måste återges för användaren.
* **** 3 (Nästa): Den aktuella sidan har ändrats med resultat som måste skrivas till klientprogrammet.
* **4 (föregående**): Den aktuella sidan har ändrats med resultat som måste skrivas till klientprogrammet.

>[!NOTE]
>
>Beräkningar och valideringar måste återges för användaren. (Se [Beräkna formulärdata](/help/forms/develop/rendering-forms-rendering-forms calculate-form-data-calculate-form-data-calculate-form-data-calculate-form.md#calculate-form-data)*.)*

**Kontrollera om formuläröverföringen innehåller bifogade filer**

Formulär som skickas till Forms-tjänsten kan innehålla bifogade filer. Med den inbyggda rutan för bifogade filer i Acrobat kan användaren t.ex. markera bifogade filer som ska skickas tillsammans med formuläret. Användaren kan också välja bifogade filer med hjälp av ett HTML-verktygsfält som återges med en HTML-fil.

När du har fastställt om ett formulär innehåller bifogade filer kan du bearbeta data. Du kan till exempel spara den bifogade filen i det lokala filsystemet.

>[!NOTE]
>
>Formuläret måste skickas som PDF-data för att du ska kunna hämta bifogade filer. Om formuläret skickas som XML-data skickas inga bifogade filer.

**Bearbeta skickade data**

Beroende på innehållstypen för inskickade data kan du extrahera enskilda formulärfältsvärden från inskickade XML-data eller spara inskickade PDF-data som en PDF-fil (eller skicka dem till en annan tjänst). Om du vill extrahera enskilda formulärfält konverterar du skickade XML-data till en XML-datakälla och hämtar sedan XML-datakällsvärden med hjälp av `org.w3c.dom` klasser.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Skicka dokument till formulärtjänsten](/help/forms/developing/passing-documents-forms-service.md)

[Skapa webbprogram som återger formulär](/help/forms/developing/creating-web-applications-renders-forms.md)

## Hantera skickade formulär med Java API {#handle-submitted-forms-using-the-java-api}

Hantera inskickade formulär med hjälp av Forms API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar, i Java-projektets klassökväg.

1. Skapa ett API-objekt för FormsClient

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa ett `FormsServiceClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.

1. Hämta formulärdata

   * Om du vill hämta formulärdata som har publicerats på en Java-server skapar du ett `com.adobe.idp.Document` objekt med hjälp av dess konstruktor och anropar `javax.servlet.http.HttpServletResponse` objektets `getInputStream` metod inifrån konstruktorn.
   * Skapa ett `RenderOptionsSpec` objekt med hjälp av dess konstruktor. Ange språkvärdet genom att anropa `RenderOptionsSpec` objektets `setLocale` metod och skicka ett strängvärde som anger språkvärdet.
   >[!NOTE]
   >
   >Du kan instruera Forms-tjänsten att skapa XDP- eller XML-data från inskickat PDF-innehåll genom att anropa `RenderOptionsSpec` objektets `setPDF2XDP` metod och skicka `true` samt även anropa `setXMLData` och skicka `true`. Du kan sedan anropa `FormsResult` objektets `getOutputXML` metod för att hämta XML-data som motsvarar XDP/XML-data. (Objektet `FormsResult` returneras av `processFormSubmission` metoden, som förklaras i nästa delsteg.)

   * Anropa `FormsServiceClient` objektets `processFormSubmission` metod och skicka följande värden:

      * Det `com.adobe.idp.Document` objekt som innehåller formulärdata.
      * Ett strängvärde som anger miljövariabler inklusive alla relevanta HTTP-huvuden. Ange den innehållstyp som ska hanteras. Om du vill hantera XML-data anger du följande strängvärde för den här parametern: `CONTENT_TYPE=text/xml`. Om du vill hantera PDF-data anger du följande strängvärde för den här parametern: `CONTENT_TYPE=application/pdf`.
      * Ett strängvärde som anger `HTTP_USER_AGENT` rubrikvärdet, till exempel . `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Det här parametervärdet är valfritt.
      * Ett `RenderOptionsSpec` objekt som lagrar körningsalternativ.
      Metoden returnerar `processFormSubmission` ett `FormsResult` objekt som innehåller resultaten av formuläröverföringen.

   * Avgör om Forms-tjänsten har slutfört bearbetningen av formulärdata genom att anropa `FormsResult` objektets `getAction` metod. Om den här metoden returnerar värdet `0`är data klara att bearbetas.



1. Kontrollera om formuläröverföringen innehåller bifogade filer

   * Anropa `FormsResult` objektets `getAttachments` metod. Den här metoden returnerar ett `java.util.List` objekt som innehåller filer som har skickats med formuläret.
   * Iterera genom objektet för `java.util.List` att avgöra om det finns bifogade filer. Om det finns bifogade filer är varje element en `com.adobe.idp.Document` instans. Du kan spara de bifogade filerna genom att anropa `com.adobe.idp.Document` objektets `copyToFile` metod och skicka ett `java.io.File` objekt.
   >[!NOTE]
   >
   >Det här steget gäller endast om formuläret skickas som PDF.

1. Bearbeta skickade data

   * Om datainnehållstypen är `application/vnd.adobe.xdp+xml` eller `text/xml`ska du skapa programlogik för att hämta XML-datavärden.

      * Skapa ett `com.adobe.idp.Document` objekt genom att anropa `FormsResult` objektets `getOutputContent` metod.
      * Skapa ett `java.io.InputStream` objekt genom att anropa `java.io.DataInputStream` konstruktorn och skicka `com.adobe.idp.Document` objektet.
      * Skapa ett `org.w3c.dom.DocumentBuilderFactory` objekt genom att anropa det statiska `org.w3c.dom.DocumentBuilderFactory` objektets `newInstance` metod.
      * Skapa ett `org.w3c.dom.DocumentBuilder` objekt genom att anropa `org.w3c.dom.DocumentBuilderFactory` objektets `newDocumentBuilder` metod.
      * Skapa ett `org.w3c.dom.Document` objekt genom att anropa `org.w3c.dom.DocumentBuilder` objektets `parse` metod och skicka `java.io.InputStream` objektet.
      * Hämta värdet för varje nod i XML-dokumentet. Ett sätt att utföra den här uppgiften är att skapa en anpassad metod som accepterar två parametrar: objektet och namnet på den nod vars värde du vill hämta `org.w3c.dom.Document` . Den här metoden returnerar ett strängvärde som representerar nodens värde. I kodexemplet som följer den här processen anropas den här anpassade metoden `getNodeText`. Innehållet i den här metoden visas.
   * Om datainnehållstypen är `application/pdf`skapar du programlogik för att spara skickade PDF-data som en PDF-fil.

      * Skapa ett `com.adobe.idp.Document` objekt genom att anropa `FormsResult` objektets `getOutputContent` metod.
      * Skapa ett `java.io.File` objekt med hjälp av dess offentliga konstruktor. Var noga med att ange PDF som filnamnstillägg.
      * Fyll i PDF-filen genom att anropa `com.adobe.idp.Document` objektets `copyToFile` metod och skicka `java.io.File` objektet.


**Se även**

[Snabbstart (SOAP-läge): Hantera PDF-formulär som skickats som XML med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[Snabbstart (SOAP-läge): Hantera HTML-formulär som skickats som XML med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[Snabbstart (SOAP-läge): Hantera PDF-formulär som skickas som PDF med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Hantera skickade PDF-data med webbtjänstens API {#handle-submitted-pdf-data-using-the-web-service-api}

Hantera ett skickat formulär med Forms API (webbtjänsten):

1. Inkludera projektfiler

   * Skapa Java-proxyklasser som använder Forms-tjänstens WSDL.
   * Inkludera Java-proxyklasserna i klassökvägen.

1. Skapa ett API-objekt för FormsClient

   Skapa ett `FormsService` objekt och ange autentiseringsvärden.

1. Hämta formulärdata

   * Om du vill hämta formulärdata som har skickats till en Java-server skapar du ett `BLOB` objekt med hjälp av dess konstruktor.
   * Skapa ett `java.io.InputStream` objekt genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getInputStream` metod.
   * Skapa ett `java.io.ByteArrayOutputStream` objekt med hjälp av dess konstruktor och skicka längden på `java.io.InputStream` objektet.
   * Kopiera innehållet i `java.io.InputStream` objektet till `java.io.ByteArrayOutputStream` objektet.
   * Skapa en bytearray genom att anropa `java.io.ByteArrayOutputStream` objektets `toByteArray` metod.
   * Fyll i `BLOB` objektet genom att anropa dess `setBinaryData` metod och skicka bytearrayen som ett argument.
   * Skapa ett `RenderOptionsSpec` objekt med hjälp av dess konstruktor. Ange språkvärdet genom att anropa `RenderOptionsSpec` objektets `setLocale` metod och skicka ett strängvärde som anger språkvärdet.
   * Anropa `FormsService` objektets `processFormSubmission` metod och skicka följande värden:

      * Det `BLOB` objekt som innehåller formulärdata.
      * Ett strängvärde som anger miljövariabler inklusive alla relevanta HTTP-huvuden. Ange den innehållstyp som ska hanteras. Om du vill hantera XML-data anger du följande strängvärde för den här parametern: `CONTENT_TYPE=text/xml`. Om du vill hantera PDF-data anger du följande strängvärde för den här parametern: `CONTENT_TYPE=application/pdf`.
      * Ett strängvärde som anger `HTTP_USER_AGENT` rubrikvärdet; till exempel `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Ett `RenderOptionsSpec` objekt som lagrar körningsalternativ.
      * Ett tomt `BLOBHolder` objekt som fylls i av metoden.
      * Ett tomt `javax.xml.rpc.holders.StringHolder` objekt som fylls i av metoden.
      * Ett tomt `BLOBHolder` objekt som fylls i av metoden.
      * Ett tomt `BLOBHolder` objekt som fylls i av metoden.
      * Ett tomt `javax.xml.rpc.holders.ShortHolder` objekt som fylls i av metoden.
      * Ett tomt `MyArrayOf_xsd_anyTypeHolder` objekt som fylls i av metoden. Den här parametern används för att lagra bifogade filer som skickas tillsammans med formuläret.
      * Ett tomt `FormsResultHolder` objekt som fylls i av metoden med det formulär som skickas.
      Metoden `processFormSubmission` fyller i `FormsResultHolder` parametern med resultaten av formuläröverföringen.

   * Avgör om Forms-tjänsten har slutfört bearbetningen av formulärdata genom att anropa `FormsResult` objektets `getAction` metod. Om den här metoden returnerar värdet `0`är formulärdata klara att bearbetas. Du kan hämta ett `FormsResult` objekt genom att hämta värdet för `FormsResultHolder` objektets `value` datamedlem.


1. Kontrollera om formuläröverföringen innehåller bifogade filer

   Hämta värdet för `MyArrayOf_xsd_anyTypeHolder` objektets `value` datamedlem ( `MyArrayOf_xsd_anyTypeHolder` objektet skickades till `processFormSubmission` metoden). Den här datamedlemmen returnerar en array med `Objects`. Varje element i `Object` arrayen är ett `Object`som motsvarar de filer som har skickats in tillsammans med formuläret. Du kan hämta varje element i arrayen och omvandla det till ett `BLOB` objekt.

1. Bearbeta skickade data

   * Om datainnehållstypen är `application/vnd.adobe.xdp+xml` eller `text/xml`ska du skapa programlogik för att hämta XML-datavärden.

      * Skapa ett `BLOB` objekt genom att anropa `FormsResult` objektets `getOutputContent` metod.
      * Skapa en bytearray genom att anropa `BLOB` objektets `getBinaryData` metod.
      * Skapa ett `java.io.InputStream` objekt genom att anropa `java.io.ByteArrayInputStream` konstruktorn och skicka bytearrayen.
      * Skapa ett `org.w3c.dom.DocumentBuilderFactory` objekt genom att anropa det statiska `org.w3c.dom.DocumentBuilderFactory` objektets `newInstance` metod.
      * Skapa ett `org.w3c.dom.DocumentBuilder` objekt genom att anropa `org.w3c.dom.DocumentBuilderFactory` objektets `newDocumentBuilder` metod.
      * Skapa ett `org.w3c.dom.Document` objekt genom att anropa `org.w3c.dom.DocumentBuilder` objektets `parse` metod och skicka `java.io.InputStream` objektet.
      * Hämta värdet för varje nod i XML-dokumentet. Ett sätt att utföra den här uppgiften är att skapa en anpassad metod som accepterar två parametrar: objektet och namnet på den nod vars värde du vill hämta `org.w3c.dom.Document` . Den här metoden returnerar ett strängvärde som representerar nodens värde. I kodexemplet som följer den här processen anropas den här anpassade metoden `getNodeText`. Innehållet i den här metoden visas.
   * Om datainnehållstypen är `application/pdf`skapar du programlogik för att spara skickade PDF-data som en PDF-fil.

      * Skapa ett `BLOB` objekt genom att anropa `FormsResult` objektets `getOutputContent` metod.
      * Skapa en bytearray genom att anropa `BLOB` objektets `getBinaryData` metod.
      * Skapa ett `java.io.File` objekt med hjälp av dess offentliga konstruktor. Var noga med att ange PDF som filnamnstillägg.
      * Skapa ett `java.io.FileOutputStream` objekt med hjälp av dess konstruktor och skicka `java.io.File` objektet.
      * Fyll i PDF-filen genom att anropa `java.io.FileOutputStream` objektets `write` metod och skicka bytearrayen.


**Se även**

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)