---
title: Konvertera mellan filformat och PDF
seo-title: Converting Between File Formats and PDF
description: Använd tjänsten Generate PDF för att konvertera inbyggda filformat till PDF. Tjänsten Generate PDF konverterar också PDF till andra filformat och optimerar storleken på PDF-dokument.
seo-description: Use the Generate PDF service to convert native file formats to PDF. Generate PDF service also converts PDF to other file formats and optimizes the size of PDF documents.
uuid: f72ad603-c996-4d48-9bfc-bed7bf776af6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 180cac3f-6378-42bc-9a47-60f9f08a7103
role: Developer
exl-id: 10535740-e3c2-4347-a88f-86706ad699b4
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '7848'
ht-degree: 0%

---

# Konvertera mellan filformat och PDF {#converting-between-file-formatsand-pdf}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

**Om tjänsten Generate PDF**

Tjänsten Generate PDF konverterar de ursprungliga filformaten till PDF. Dessutom konverteras PDF till andra filformat och storleken på PDF-dokument optimeras.

Tjänsten Generate PDF använder inbyggda program för att konvertera följande filformat till PDF. Om inget annat anges stöds endast de tyska, franska, engelska och japanska versionerna av dessa program. *Endast Windows* anger endast stöd för Windows Server® 2003 och Windows Server 2008.

* Microsoft Office 2003 och 2007 för att konvertera DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX, XPS och PUB (endast Windows)

>[!NOTE]
>
>Acrobat® 9.2 eller senare krävs för att konvertera Microsoft XPS-format till PDF.

* Autodesk AutoCAD 2005, 2006, 2007, 2008 och 2009 för att konvertera DWF, DWG och DXW (endast engelska)
* Corel WordPerfect 12 och X4 för att konvertera WPD, QPW, SHW (endast på engelska)
* OpenOffice 2.0, 2.4, 3.0.1 och 3.1 för konvertering av ODT, ODS, ODP, ODG, ODF, SXW, SXI, SXC, SXD, DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX och PUB

>[!NOTE]
>
Tjänsten Generate PDF stöder inte 64-bitarsversionerna av OpenOffice.

* Adobe Photoshop® CS2 för att konvertera PSD (endast Windows)

>[!NOTE]
>
Photoshop CS3 och CS4 stöds inte eftersom de inte stöder Windows Server 2003 eller Windows Server 2008.

* Adobe FrameMaker® 7.2 och 8 för att konvertera FM (endast Windows)
* Adobe PageMaker® 7.0 för att konvertera PMD, PM6, P65 och PM (endast Windows)
* Inbyggda format som stöds av tredjepartsprogram (kräver utveckling av installationsfiler som är specifika för programmet) (endast Windows)

Tjänsten Generate PDF konverterar följande standardbaserade filformat till PDF.

* Videoformat: SWF, FLV (endast Windows)
* Bildformat: JPEG, JPG, JP2, J2Kí, JPC, J2C, GIF, BMP, TIFF, TIF, PNG, JPF
* HTML (Windows, Sun™ Solaris™ och Linux®)

Tjänsten Generate PDF konverterar PDF till följande filformat (endast Windows):

* Encapsulated PostScript (EPS)
* HTML 3.2
* HTML 4.01 med CSS 1.0
* DOC (Microsoft Word-format)
* RTF
* Text (både tillgänglig och normal)
* XML
* PDF/A-1a som endast använder DeviceRGB-färgmodellen
* PDF/A-1b som endast använder DeviceRGB-färgmodellen

Tjänsten Generera PDF kräver att du utför följande administrativa uppgifter:

* Installera nödvändiga inbyggda program på den dator där AEM Forms finns
* Installera Adobe Acrobat Professional eller Acrobat Pro Extended 9.2 på den dator där AEM Forms finns
* Utför konfigurationsuppgifter efter installation

Dessa åtgärder beskrivs i Installera och distribuera AEM formulär med JBoss-tangenten.

Du kan utföra följande uppgifter med tjänsten Generate PDF:

* Konvertera från egna filformat till PDF.
* Konvertera HTML-dokument till PDF-dokument.
* Konvertera PDF-dokument till filformat.

>[!NOTE]
>
Mer information om tjänsten Generate PDF finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Konvertera Word-dokument till PDF-dokument {#converting-word-documents-to-pdf-documents}

I det här avsnittet beskrivs hur du kan använda Generate PDF API för att programmässigt konvertera ett Microsoft Word-dokument till ett PDF.

>[!NOTE]
>
Mer information om ytterligare filformat finns i [Stöd för fler filformat](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats).

>[!NOTE]
>
Mer information om tjänsten Generate PDF finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Så här konverterar du ett Microsoft Word-dokument till ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en Generate PDF-klient.
1. Hämta filen som ska konverteras till ett PDF-dokument.
1. Konvertera filen till ett PDF-dokument.
1. Hämta resultaten.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en Generera PDF-klient**

Skapa en Generate PDF service-klient innan du programmässigt utför en Generate PDF-åtgärd. Om du använder Java API skapar du en `GeneratePdfServiceClient` -objekt. Om du använder webbtjänstens API skapar du en `GeneratePDFServiceService` -objekt.

**Hämta filen som ska konverteras till ett PDF-dokument**

Hämta Microsoft Word-dokumentet som ska konverteras till ett PDF-dokument.

**Konvertera filen till ett PDF-dokument**

När du har skapat tjänstklienten Generate PDF kan du anropa `createPDF2` -metod. Den här metoden kräver information om dokumentet som ska konverteras, inklusive filtillägget.

**Hämta resultaten**

När filen har konverterats till ett PDF-dokument kan du hämta resultatet. När du till exempel har konverterat en Word-fil till ett PDF-dokument kan du hämta och spara dokumentet i PDF.

**Se även**

[Konvertera Word-dokument till PDF med Java API](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[Konvertera Word-dokument till PDF-dokument med hjälp av webbtjänstens API](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generera snabbstart för PDF Service API](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Konvertera Word-dokument till PDF med Java API {#convert-word-documents-to-pdf-documents-using-the-java-api}

Konvertera ett Microsoft Word-dokument till ett PDF-dokument med hjälp av API:t Generate PDF (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-generatepdf-client.jar, i Java-projektets klassökväg.

1. Skapa en Generate PDF-klient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `GeneratePdfServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta filen som ska konverteras till ett PDF-dokument.

   * Skapa en `java.io.FileInputStream` objekt som representerar Word-filen som ska konverteras med hjälp av dess konstruktor. Skicka ett strängvärde som anger filens plats.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Konvertera filen till ett PDF-dokument.

   Konvertera filen till ett PDF-dokument genom att anropa `GeneratePdfServiceClient` objektets `createPDF2` och skicka följande värden:

   * A `com.adobe.idp.Document` objekt som representerar den fil som ska konverteras.
   * A `java.lang.String` objekt som innehåller filtillägget.
   * A `java.lang.String` som innehåller de filtypsinställningar som ska användas vid konverteringen. Filtypsinställningarna innehåller konverteringsinställningar för olika filtyper, till exempel .doc eller .xls.
   * A `java.lang.String` -objekt som innehåller namnet på de PDF-inställningar som ska användas. Du kan till exempel ange `Standard`.
   * A `java.lang.String` objekt som innehåller namnet på de skyddsinställningar som ska användas.
   * Ett valfritt `com.adobe.idp.Document` objekt som innehåller inställningar som ska användas när dokumentet PDF genereras.
   * Ett valfritt `com.adobe.idp.Document` objekt som innehåller metadatainformation som ska användas i PDF-dokumentet.

   The `createPDF2` returnerar en `CreatePDFResult` som innehåller det nya PDF-dokumentet och en logginformation. Loggfilen innehåller vanligen fel- eller varningsmeddelanden som genererats av konverteringsbegäran.

1. Hämta resultaten.

   Så här hämtar du dokumentet från PDF:

   * Anropa `CreatePDFResult` objektets `getCreatedDocument` metod, som returnerar `com.adobe.idp.Document` -objekt.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att extrahera PDF-dokumentet från det objekt som skapades i föregående steg.

   Om du använde `createPDF2` för att få fram loggdokumentet (gäller inte konverteringar i HTML), utföra följande åtgärder:

   * Anropa `CreatePDFResult` objektets `getLogDocument` -metod. Detta returnerar en `com.adobe.idp.Document` -objekt.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att extrahera loggdokumentet.

**Se även**

[Sammanfattning av steg](converting-file-formats-pdf.md#summary-of-steps)

[Snabbstart (SOAP-läge): Konvertera ett Microsoft Word-dokument till ett PDF-dokument med Java API](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Konvertera Word-dokument till PDF-dokument med hjälp av webbtjänstens API {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

Konvertera ett Microsoft Word-dokument till ett PDF-dokument med hjälp av API:t Generate PDF (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en Generate PDF-klient.

   * Skapa en `GeneratePDFServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `GeneratePDFServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) Du behöver inte använda `lc_version` -attribut. Ange dock `?blob=mtom`.
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `GeneratePDFServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta filen som ska konverteras till ett PDF-dokument.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` används för att lagra filen som du vill konvertera till ett PDF-dokument.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för filen som ska konverteras och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` objekt genom att tilldela till dess `MTOM` egenskapen för bytearrayens innehåll.

1. Konvertera filen till ett PDF-dokument.

   Konvertera filen till ett PDF-dokument genom att anropa `GeneratePDFServiceService` objektets `CreatePDF2` och skicka följande värden:

   * A `BLOB` objekt som representerar filen som ska konverteras.
   * En sträng som innehåller filtillägget.
   * A `java.lang.String` som innehåller de filtypsinställningar som ska användas vid konverteringen. Filtypsinställningarna innehåller konverteringsinställningar för olika filtyper, till exempel .doc eller .xls.
   * Ett strängobjekt som innehåller de PDF-inställningar som ska användas. Du kan ange `Standard`.
   * Ett strängobjekt som innehåller de skyddsinställningar som ska användas. Du kan ange `No Security`.
   * Ett valfritt `BLOB` objekt som innehåller inställningar som ska användas när dokumentet PDF genereras.
   * Ett valfritt `BLOB` objekt som innehåller metadatainformation som ska användas i PDF-dokumentet.
   * En utdataparameter av typen `BLOB` som fylls i av `CreatePDF2` -metod. The `CreatePDF2` fyller i det här objektet med det konverterade dokumentet. (Det här parametervärdet krävs bara för webbtjänstanrop).
   * En utdataparameter av typen `BLOB` som fylls i av `CreatePDF2` -metod. The `CreatePDF2` -metoden fyller i det här objektet med loggdokumentet. (Det här parametervärdet krävs bara för webbtjänstanrop).

1. Hämta resultaten.

   * Hämta det konverterade PDF-dokumentet genom att tilldela `BLOB` objektets `MTOM` till en bytearray. Bytearrayen representerar det konverterade PDF-dokumentet. Se till att du använder `BLOB` objekt som används som utdataparameter för `createPDF2` -metod.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det konverterade PDF-dokumentet.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Sammanfattning av steg](converting-file-formats-pdf.md#summary-of-steps)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Konvertera HTML-dokument till PDF-dokument {#converting-html-documents-to-pdf-documents}

I det här avsnittet beskrivs hur du kan använda Generate PDF API för att programmässigt konvertera HTML-dokument till PDF-dokument.

>[!NOTE]
>
Mer information om tjänsten Generate PDF finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-1}

Så här konverterar du ett HTML-dokument till ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en Generate PDF-klient.
1. Hämta HTML-innehåll som ska konverteras till ett PDF-dokument.
1. Konvertera HTML-innehåll till ett PDF-dokument.
1. Hämta resultaten.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en Generera PDF-klient**

Innan du programmässigt kan utföra en Generate PDF-åtgärd måste du skapa en Generate PDF-tjänstklient. Om du använder Java API skapar du en `GeneratePdfServiceClient` -objekt. Om du använder webbtjänstens API skapar du en `GeneratePDFServiceService`.

**Hämta HTML-innehåll som ska konverteras till ett PDF-dokument**

Referera till HTML-innehåll som du vill konvertera till ett PDF-dokument. Du kan referera till HTML-innehåll som en HTML-fil eller HTML-innehåll som är tillgängligt via en URL.

**Konvertera HTML-innehåll till ett PDF-dokument**

När du har skapat tjänstklienten kan du anropa lämplig åtgärd för att skapa PDF. Den här åtgärden kräver information om dokumentet som ska konverteras, inklusive sökvägen till måldokumentet.

**Hämta resultaten**

När HTML-innehållet har konverterats till ett PDF-dokument kan du hämta resultatet och spara PDF-dokumentet.

**Se även**

[Konvertera HTML-innehåll till ett PDF-dokument med Java API](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[Konvertera HTML-innehåll till ett PDF-dokument med hjälp av webbtjänstens API](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generera snabbstart för PDF Service API](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Konvertera HTML-innehåll till ett PDF-dokument med Java API {#convert-html-content-to-a-pdf-document-using-the-java-api}

Konvertera ett HTML-dokument till ett PDF-dokument med hjälp av API:t Generate PDF (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-generatepdf-client.jar, i Java-projektets klassökväg.

1. Skapa en Generate PDF-klient.

   Skapa en `GeneratePdfServiceClient` genom att använda konstruktorn och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Hämta HTML-innehåll som ska konverteras till ett PDF-dokument.

   Hämta innehåll från HTML genom att skapa en strängvariabel och tilldela en URL som pekar på innehåll från HTML.

1. Konvertera HTML-innehåll till ett PDF-dokument.

   Anropa `GeneratePdfServiceClient` objektets `htmlToPDF2` och skicka följande värden:

   * A `java.lang.String` objekt som innehåller URL-adressen för den HTML-fil som ska konverteras.
   * A `java.lang.String` som innehåller de filtypsinställningar som ska användas vid konverteringen. Filtypsinställningarna kan innehålla spidernivåer.
   * A `java.lang.String` objekt som innehåller namnet på de skyddsinställningar som ska användas.
   * Ett valfritt `com.adobe.idp.Document` objekt som innehåller inställningar som ska användas när dokumentet PDF genereras. Om den här informationen inte anges väljs inställningarna automatiskt baserat på de tre föregående parametrarna.
   * Ett valfritt `com.adobe.idp.Document` objekt som innehåller metadatainformation som ska användas i PDF-dokumentet.

1. Hämta resultaten.

   The `htmlToPDF2` returnerar en `HtmlToPdfResult` objekt som innehåller det nya PDF-dokumentet som skapades. Utför följande åtgärder för att hämta det nya PDF-dokumentet:

   * Anropa `HtmlToPdfResult` objektets `getCreatedDocument` -metod. Detta returnerar en `com.adobe.idp.Document` -objekt.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att extrahera PDF-dokumentet från det objekt som skapades i föregående steg.

**Se även**

[Konvertera HTML-dokument till PDF-dokument](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[Snabbstart (SOAP-läge): Konvertera HTML-innehåll till ett PDF-dokument med Java API](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Snabbstart (SOAP-läge): Konvertera HTML-innehåll till ett PDF-dokument med Java API](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Konvertera HTML-innehåll till ett PDF-dokument med hjälp av webbtjänstens API {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

Konvertera HTML-innehåll till ett PDF-dokument med hjälp av API:t Generate PDF (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en Generate PDF-klient.

   * Skapa en `GeneratePDFServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `GeneratePDFServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) Du behöver inte använda `lc_version` -attribut. Ange dock `?blob=mtom`.
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `GeneratePDFServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta HTML-innehåll som ska konverteras till ett PDF-dokument.

   Hämta innehåll från HTML genom att skapa en strängvariabel och tilldela en URL som pekar på innehåll från HTML.

1. Konvertera HTML-innehåll till ett PDF-dokument.

   Konvertera HTML-innehåll till ett PDF-dokument genom att anropa `GeneratePDFServiceService` objektets `HtmlToPDF2` och skicka följande värden:

   * En sträng som innehåller det HTML-innehåll som ska konverteras.
   * A `java.lang.String` som innehåller de filtypsinställningar som ska användas vid konverteringen.
   * Ett strängobjekt som innehåller de skyddsinställningar som ska användas.
   * Ett valfritt `BLOB` objekt som innehåller inställningar som ska användas när dokumentet PDF genereras.
   * Ett valfritt `BLOB` objekt som innehåller metadatainformation som ska användas i PDF-dokumentet.
   * En utdataparameter av typen `BLOB` som fylls i av `CreatePDF2` -metod. The `CreatePDF2` fyller i det här objektet med det konverterade dokumentet. (Det här parametervärdet krävs bara för webbtjänstanrop).

1. Hämta resultaten.

   * Hämta det konverterade PDF-dokumentet genom att tilldela `BLOB` objektets `MTOM` till en bytearray. Bytearrayen representerar det konverterade PDF-dokumentet. Se till att du använder `BLOB` objekt som används som utdataparameter för `HtmlToPDF2` -metod.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det konverterade PDF-dokumentet.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Konvertera HTML-dokument till PDF-dokument](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Konvertera PDF-dokument till andra format än bildformat {#converting-pdf-documents-to-non-image-formats}

I det här avsnittet beskrivs hur du kan använda Generate PDF Java API och webbtjänstens API för att programmässigt konvertera ett PDF-dokument till en RTF-fil, som är ett exempel på ett icke-bildformat. Andra format som inte är bildformat är HTML, text, DOC och EPS. När du konverterar ett PDF-dokument till RTF-format bör du kontrollera att PDF-dokumentet inte innehåller några formulärelement, t.ex. en skicka-knapp. Formulärelement konverteras inte.

>[!NOTE]
>
Mer information om tjänsten Generate PDF finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-2}

Så här konverterar du ett PDF-dokument till någon av de typer som stöds:

1. Inkludera projektfiler.
1. Skapa en Generate PDF-klient.
1. Hämta det PDF-dokument som ska konverteras.
1. Konvertera dokumentet PDF.
1. Spara den konverterade filen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en Generera PDF-klient**

Innan du programmässigt kan utföra en Generate PDF-åtgärd måste du skapa en Generate PDF-tjänstklient. Om du använder Java API skapar du en `GeneratePdfServiceClient` -objekt. Om du använder webbtjänstens API skapar du en `GeneratePDFServiceService` -objekt.

**Hämta det PDF-dokument som ska konverteras**

Hämta dokumentet PDF för konvertering till ett format som inte är en bild.

**Konvertera PDF-dokumentet**

När du har skapat tjänstklienten kan du starta exportåtgärden i PDF. Den här åtgärden kräver information om dokumentet som ska konverteras, inklusive sökvägen till måldokumentet.

**Spara den konverterade filen**

Spara den konverterade filen. Om du till exempel konverterar ett PDF-dokument till en RTF-fil sparar du det konverterade dokumentet till en RTF-fil.

**Se även**

[Konvertera ett PDF-dokument till en RTF-fil med Java API](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[Konvertera ett PDF-dokument till en RTF-fil med webbtjänstens API](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generera snabbstart för PDF Service API](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Konvertera ett PDF-dokument till en RTF-fil med Java API {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

Konvertera ett PDF-dokument till en RTF-fil med hjälp av Java-API:t (Generate PDF):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-generatepdf-client.jar, i Java-projektets klassökväg.

1. Skapa en Generate PDF-klient.

   Skapa en `GeneratePdfServiceClient` genom att använda konstruktorn och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Hämta det PDF-dokument som ska konverteras.

   * Skapa en `java.io.FileInputStream` objekt som representerar det PDF-dokument som ska konverteras med hjälp av dess konstruktor. Skicka ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Konvertera dokumentet PDF.

   Anropa `GeneratePdfServiceClient` objektets `exportPDF2` och skicka följande värden:

   * A `com.adobe.idp.Document` objekt som representerar den PDF-fil som ska konverteras.
   * A `java.lang.String` som innehåller namnet på filen som ska konverteras.
   * A `java.lang.String` -objekt som innehåller namnet på Adobe PDF-inställningarna.
   * A `ConvertPDFFormatType` objekt som anger målfiltypen för konverteringen.
   * Ett valfritt `com.adobe.idp.Document` objekt som innehåller inställningar som ska användas när dokumentet PDF genereras.

   The `exportPDF2` returnerar en `ExportPDFResult` som innehåller den konverterade filen.

1. Konvertera dokumentet PDF.

   Utför följande åtgärder för att hämta den nya filen:

   * Anropa `ExportPDFResult` objektets `getConvertedDocument` -metod. Detta returnerar en `com.adobe.idp.Document` -objekt.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att extrahera det nya dokumentet.

**Se även**

[Sammanfattning av steg](converting-file-formats-pdf.md#summary-of-steps)

[Snabbstart (SOAP-läge): Konvertera HTML-innehåll till ett PDF-dokument med Java API](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Konvertera ett PDF-dokument till en RTF-fil med webbtjänstens API {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

Konvertera ett PDF-dokument till en RTF-fil med hjälp av API:t för Generate PDF (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en Generate PDf-klient.

   * Skapa en `GeneratePDFServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `GeneratePDFServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) Du behöver inte använda `lc_version` -attribut. Ange dock `?blob=mtom`.
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `GeneratePDFServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta det PDF-dokument som ska konverteras.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra ett PDF-dokument som konverteras.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` objekt genom att tilldela till dess `MTOM` egenskapen för bytearrayens innehåll.

1. Konvertera dokumentet PDF.

   Anropa `GeneratePDFServiceServiceWse` objektets `ExportPDF2` och skicka följande värden:

   * A `BLOB` objekt som representerar den PDF-fil som ska konverteras.
   * En sträng som innehåller sökvägen till filen som ska konverteras.
   * A `java.lang.String` -objekt som anger filens plats.
   * Ett strängobjekt som anger målfiltypen för konverteringen. Ange `RTF`.
   * Ett valfritt `BLOB` objekt som innehåller inställningar som ska användas när dokumentet PDF genereras.
   * En utdataparameter av typen `BLOB` som fylls i av `ExportPDF2` -metod. The `ExportPDF2` fyller i det här objektet med det konverterade dokumentet. (Det här parametervärdet krävs bara för webbtjänstanrop).

1. Spara den konverterade filen.

   * Hämta det konverterade RTF-dokumentet genom att tilldela `BLOB` objektets `MTOM` till en bytearray. Bytearrayen representerar det konverterade RTF-dokumentet. Se till att du använder `BLOB` objekt som används som utdataparameter för `ExportPDF2` -metod.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som representerar platsen för RTF-filen.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en RTF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Sammanfattning av steg](converting-file-formats-pdf.md#summary-of-steps)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Stöd för fler filformat {#adding-support-for-additional-native-file-formats}

I det här avsnittet beskrivs hur du lägger till stöd för fler inbyggda filformat. Här finns en översikt över interaktionen mellan Generate PDF-tjänsten och de inbyggda program som den här tjänsten använder för att konvertera inbyggda filformat till PDF.

I det här avsnittet förklaras även följande:

* Hur man ändrar det svar som tjänsten Generate PDF ger de inbyggda programmen som redan används för att konvertera inbyggda filformat till PDF
* Interaktionerna mellan tjänsten Generate PDF, komponenten Generate PDF Application Monitor (AppMon) och inbyggda program som Microsoft Word
* Rollerna som XML-grammatiken spelar i dessa interaktioner

### Komponentinteraktioner {#component-interactions}

Tjänsten Generate PDF konverterar de ursprungliga filformaten genom att anropa det program som är associerat med filformatet och sedan interagera med programmet för att skriva ut dokumentet med standardskrivaren. Standardskrivaren måste ställas in som Adobe PDF-skrivare.

Den här bilden visar vilka komponenter och drivrutiner som har inbyggt programstöd. Där omnämns också XML-grammatiken som påverkar interaktionen.

Komponentinteraktioner för intern filkonvertering

I det här dokumentet används termen *internt program* för att ange vilket program som används för att skapa ett internt filformat, t.ex. Microsoft Word.

*AppMon* är en företagskomponent som interagerar med ett systemspecifikt program på samma sätt som en användare navigerar genom de dialogrutor som visas i det programmet. Den XML-grammatik som används av AppMon för att instruera ett program, som Microsoft Word, att öppna och skriva ut en fil omfattar följande sekventiella uppgifter:

1. Öppna filen genom att välja Arkiv > Öppna
1. Kontrollera att dialogrutan Öppna visas. Om inte hanterar du felet
1. Ange filnamnet i fältet Filnamn och klicka sedan på knappen Öppna
1. Kontrollera att filen verkligen öppnas
1. Öppna dialogrutan Skriv ut genom att välja Arkiv > Skriv ut
1. Kontrollera att dialogrutan Skriv ut visas

AppMon använder Win32-standardAPI:er för att interagera med program från tredje part för att överföra gränssnittshändelser som tangenttryckningar och musklick, vilket är användbart för att styra programmen för att skapa PDF-filer från dem.

På grund av en begränsning med dessa Win32 API:er kan AppMon inte skicka dessa UI-händelser till vissa specifika typer av fönster, till exempel flytande menyrader (som finns i vissa program som TextPad) och vissa typer av dialogrutor vars innehåll inte kan hämtas med Win32 API:er.

Det är enkelt att se en flytande menyrad, men det är inte säkert att det går att identifiera särskilda typer av dialogrutor bara genom visuell kontroll. Du behöver ett tredjepartsprogram som Microsoft Spy++ (ingår i Microsoft Visual C++-utvecklingsmiljön) eller motsvarande WinID (som kan laddas ned kostnadsfritt från [https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID)) för att undersöka en dialogruta för att avgöra om AppMon kan interagera med den med Win32-standardprogrammeringsgränssnitt.

Om WinID kan extrahera dialoginnehåll som text, underfönster, fönsterklass-ID och så vidare, kan AppMon också göra det.

I den här tabellen visas vilken typ av information som används vid utskrift av originalfilformat.

<table>
 <thead>
  <tr>
   <th><p>Informationstyp</p></th>
   <th><p>Beskrivning</p></th>
   <th><p>Ändra/skapa poster relaterade till originalfiler </p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Administrativa inställningar </p></td>
   <td><p>Innehåller inställningar för PDF, skyddsinställningar och filtypsinställningar. </p><p>Filtypsinställningarna associerar filnamnstillägg med motsvarande systemspecifika program. Filtypsinställningarna anger även inbyggda programinställningar som används för att skriva ut inbyggda filer. </p></td>
   <td><p>Om du vill ändra inställningarna för ett inbyggt program som redan stöds anger systemadministratören filtypsinställningarna i administrationskonsolen. </p><p>Om du vill lägga till stöd för ett nytt inbyggt filformat måste du redigera filen manuellt. (Se <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">Lägga till eller ändra stöd för ett ursprungligt filformat</a>.) </p></td>
  </tr>
  <tr>
   <td><p>Skript </p></td>
   <td><p>Anger interaktioner mellan Generate PDF-tjänsten och ett systemspecifikt program. Sådana interaktioner dirigerar vanligtvis programmet till Adobe PDF-drivrutinen för att skriva ut en fil. </p><p>Skriptet innehåller instruktioner som instruerar det ursprungliga programmet att öppna specifika dialogrutor och som ger specifika svar på fält och knappar i dessa dialogrutor. </p></td>
   <td><p>Tjänsten Generate PDF innehåller skriptfiler för alla systemspecifika program som stöds. Du kan ändra dessa filer med ett XML-redigeringsprogram.</p><p>Om du vill lägga till stöd för ett nytt systemspecifikt program måste du skapa en ny skriptfil. (Se <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">Skapa eller ändra ytterligare en dialogrute-XML-fil för ett ursprungligt program</a>.) </p></td>
  </tr>
  <tr>
   <td><p>Allmänna instruktioner i dialogrutan </p></td>
   <td><p>Anger hur du ska svara på dialogrutor som är gemensamma för flera program. Sådana dialogrutor genereras av operativsystem, hjälpprogram (till exempel PDFMaker) och drivrutiner. </p><p>Filen som innehåller den här informationen är appmon.global.en_US.xml.</p></td>
   <td><p>Ändra inte filen. </p></td>
  </tr>
  <tr>
   <td><p>Programspecifika dialogruteinstruktioner</p></td>
   <td><p>Anger hur programspecifika dialogrutor ska besvaras. </p><p>Filen som innehåller den här informationen är giltig.<i>`[appname]`</i>.dialog.<i>`[locale]`</i>.xml (till exempel appmon.word.en_US.xml).</p></td>
   <td><p>Ändra inte filen. </p><p>Information om hur du lägger till dialogruteinstruktioner för ett nytt inbyggt program finns i <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">Skapa eller ändra ytterligare en dialogrute-XML-fil för ett ursprungligt program</a>.</p></td>
  </tr>
  <tr>
   <td><p>Ytterligare programspecifika dialogruteinstruktioner </p></td>
   <td><p>Anger åsidosättningar och tillägg till programspecifika dialogruteinstruktioner. I avsnittet visas ett exempel på sådan information. </p><p>Filen som innehåller den här informationen är giltig.<i>`[appname]`</i>.addition.<i>`[locale]`</i>.xml Ett exempel är appmon.addition.en_US.xml.</p></td>
   <td><p>Filer av den här typen kan skapas och ändras med ett XML-redigeringsprogram. (Se <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">Skapa eller ändra ytterligare en dialogrute-XML-fil för ett ursprungligt program</a>.) </p><p><strong>Viktigt</strong>: Du måste skapa ytterligare programspecifika dialogruteinstruktioner för varje systemspecifikt program som servern stöder. </p></td>
  </tr>
 </tbody>
</table>

### Om skript- och dialogrute-XML-filer {#about-the-script-and-dialog-xml-files}

Skript-XML-filer instruerar Generate PDF att navigera i programdialogrutor på samma sätt som en användare navigerar i programdialogrutorna. Skript-XML-filer instruerar även Generate PDF att svara på dialogrutor genom att utföra åtgärder som att trycka på knappar, markera eller avmarkera kryssrutor eller välja menyalternativ.

XML-filer i dialogrutor svarar däremot bara på dialogrutor med samma typ av åtgärder som används i XML-filer i skript.

#### Dialogruta och terminologi för fönsterelement {#dialog-box-and-window-element-terminology}

I det här avsnittet och i nästa avsnitt används olika terminologi för dialogrutor och de komponenter de innehåller, beroende på vilket perspektiv som beskrivs. Dialogrutekomponenter är objekt som knappar, fält och kombinationsrutor.

När det här avsnittet och nästa avsnitt beskriver dialogrutor och deras komponenter ur användarens perspektiv, termer som *dialogruta*, *knapp*, *fält* och *kombinationsruta* används.

När det här avsnittet och nästa avsnitt beskriver dialogrutor och deras komponenter utifrån deras interna representation är termen *window-element* används. Den interna representationen av fönsterelement är en hierarki, där varje fönsterelementinstans identifieras med etiketter. Fönsterelementinstansen beskriver också dess fysiska egenskaper och beteende.

Från användarens perspektiv visar dialogrutorna och deras komponenter olika beteenden, där vissa dialogruteelement är dolda tills de aktiveras. Från ett internt representationsperspektiv finns det ingen sådan beteendefråga. Den interna representationen av en dialogruta liknar till exempel komponenterna i den, med undantag för att komponenterna är kapslade i dialogrutan.

I det här avsnittet beskrivs XML-element som innehåller instruktioner för AppMon. Dessa element har namn som `dialog` -element och `window` -element. I det här dokumentet används ett teckensnitt med fast teckenbredd för att skilja på XML-element. The `dialog` -element används för att identifiera en dialogruta som en XML-skriptfil kan orsaka att den visas, antingen avsiktligt eller oavsiktligt. The `window` element identifierar ett fönsterelement (dialogruta eller komponenter i en dialogruta).

#### Hierarki {#hierarchy}

Bilden visar hierarkin för skript och dialogrute-XML. En skript-XML-fil överensstämmer med skriptet.xsd-schemat, som i XML-bemärkelse inkluderar window.xsd-schemat. På samma sätt överensstämmer en dialogrute-XML-fil med dialogs.xsd-schemat, som även innehåller window.xsd-schemat.

![as_as_xml_hierarki](assets/as_as_xml_hierarchy.png)

Hierarki för skript och dialogrute-XML

#### Skript-XML-filer {#script-xml-files}

A *script XML-fil* anger en serie steg som instruerar det inbyggda programmet att navigera till vissa fönsterelement och sedan ange svar på dessa element. De flesta svar är text eller tangenttryckningar som motsvarar de indata en användare skulle ge till ett fält, en kombinationsruta eller en knapp i motsvarande dialogruta.

Avsikten med Generate PDF-tjänstens stöd för skript-XML-filer är att instruera ett program att skriva ut en intern fil. Skript-XML-filer kan dock användas för att utföra alla åtgärder som en användare kan utföra när han eller hon interagerar med programmets dialogrutor.

Stegen i en skript-XML-fil körs i ordning, utan möjlighet till förgreningar. Det enda villkorstest som stöds är timeout/retry, vilket gör att ett skript avslutas om ett steg inte slutförs korrekt inom en viss tidsperiod och efter ett visst antal försök.

Förutom att steg är sekventiella utförs även instruktionerna i ett steg i ordning. Du måste se till att stegen och instruktionerna återspeglar den ordning i vilken användaren utför samma steg.

Varje steg i en skript-XML-fil identifierar det window-element som förväntas visas om instruktionerna för steget har utförts. Om en oväntad dialogruta visas när du kör ett skriptsteg söker tjänsten Generate PDF igenom XML-filer i dialogrutan enligt beskrivningen i nästa avsnitt.

#### Dialog-XML-filer {#dialog-xml-files}

När du kör inbyggda program visas olika dialogrutor, som visas oavsett om de inbyggda programmen är i synligt eller osynligt läge. Dialogrutorna kan genereras av operativsystemet eller av själva programmet. När inbyggda program körs under kontroll av tjänsten Generate PDF visas dialogrutorna för system och inbyggda program i ett osynligt fönster.

A *dialog-XML-fil* används för att ange hur tjänsten Generate PDF ska svara på systemdialogrutor eller systemdialogrutor. I dialogrutans XML-filer kan tjänsten Generate PDF svara på dialogrutor som inte efterfrågas på ett sätt som underlättar konverteringsprocessen.

När systemet eller det inbyggda programmet visar en dialogruta som inte hanteras av den XML-fil som för närvarande körs, söker tjänsten Generate PDF igenom XML-filer i dialogrutan i den här ordningen och stoppar när en matchning hittas:

* appmon.`[appname]`.additional.`[locale]`XML
* appmon.`[appname]`.`[locale]`.xml (Ändra inte den här filen.)
* appmon.global.`[locale]`.xml (Ändra inte den här filen.)

Om tjänsten Generate PDF hittar en matchning för dialogrutan stängs den av genom att den skickas med tangentbordet eller någon annan åtgärd som har angetts för dialogrutan. Om instruktionerna för dialogrutan anger ett avbrottsmeddelande avbryter tjänsten Generate PDF det jobb som körs och genererar ett felmeddelande. Ett sådant meddelande skulle anges i `abortMessage` i skriptets XML-grammatik.

Om tjänsten Generate PDF påträffar en dialogruta som inte beskrivs i någon av de tidigare listade filerna, infogar tjänsten Generate PDF dialogrutans bildtext i loggfilsposten. Tidsgränsen för det jobb som körs för närvarande har uppnåtts. Du kan sedan använda informationen i loggfilen för att skapa nya instruktioner i XML-filen för ytterligare dialogrutor för det ursprungliga programmet.

### Lägga till eller ändra stöd för ett ursprungligt filformat {#adding-or-modifying-support-for-a-native-file-format}

I det här avsnittet beskrivs de åtgärder du måste utföra för att stödja andra filformat eller för att ändra stödet för ett filformat som redan stöds.

Innan du kan lägga till eller ändra support måste du utföra följande åtgärder.

#### Välja ett verktyg för att identifiera fönsterelement {#choosing-a-tool-for-identifying-window-elements}

Dialogrutan och skriptets XML-filer kräver att du identifierar det fönsterelement (dialogruta, fält eller annan dialogrutekomponent) som dialogrutan eller skriptelementet svarar på. När ett skript till exempel anropar en meny för ett inbyggt program, måste skriptet identifiera det fönsterelement på den menyn som tangenttryckningar eller en åtgärd ska tillämpas på.

Du kan enkelt identifiera en dialogruta med den bildtext som visas i namnlisten. Du måste dock använda ett verktyg som Microsoft Spy++ för att identifiera element på lägre nivå i fönstret. Fönsterelementen på den lägre nivån kan identifieras med hjälp av en mängd olika attribut, som inte är uppenbara. Dessutom kan varje inbyggt program identifiera sitt fönsterelement på olika sätt. Det finns därför flera sätt att identifiera ett fönsterelement. Här är den föreslagna ordningen för att överväga identifiering av fönsterelement:

1. Beskrivningen är unik
1. Kontroll-ID, som kan vara unikt för en viss dialogruta
1. Klassnamn, som kan vara unika

Alla eller en kombination av dessa tre attribut kan användas för att identifiera ett fönster.

Om attributen inte kan identifiera en bildtext kan du i stället identifiera ett fönsterelement genom att använda dess index i förhållande till dess överordnade element. An *index* anger fönsterelementets position i förhållande till dess element på samma nivå. Index är ofta det enda sättet att identifiera kombinationsrutor.

Tänk på följande:

* Microsoft Spy++ visar bildtexter med ett et-tecken (&amp;) som identifierar bildtextens snabbtangent. Spy++ visar till exempel bildtexten för en utskriftsdialogruta som `Pri&nt`, vilket anger att snabbtangenten är *n*. Bildtexter i skript- och dialogrute-XML-filer måste utelämna et-tecken.
* Vissa bildtexter innehåller radbrytningar. tjänsten Generate PDF kan inte identifiera radbrytningar. Om en bildtext innehåller en radbrytning tar du med tillräckligt mycket av bildtexten för att skilja den från andra menyalternativ och använder sedan reguljära uttryck för den utelämnade delen. Ett exempel är ( `^Long caption title$`). (Se [Använda reguljära uttryck i bildtextattribut](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes).)
* Använd teckenentiteter (kallas även escape-sekvenser) för reserverade XML-tecken. Använd till exempel `&` för et-tecken, `<` och `>` för mindre än och större än symboler, `&apos;` för apostrofer, och `&quot;` för citattecken.

Om du tänker arbeta med dialogruta- eller skript-XML-filer bör du installera programmet Microsoft Spy++.

#### Uppackning av dialogrute- och skriptfiler {#unpackaging-the-dialog-and-script-files}

Dialogrutan och skriptfilerna finns i filen appmondata.jar. Innan du kan ändra någon av dessa filer eller lägga till nya skript- eller dialogfiler måste du packa upp den här JAR-filen. Anta till exempel att du vill lägga till stöd för programmet EditPlus. Du skapar två XML-filer med namnen appmon.editplus.script.en_US.xml och appmon.editplus.script.addition.en_US.xml. Dessa XML-skript måste läggas till i filen adobe-appmondata.jar på två platser, enligt vad som anges nedan:

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon. Filen adobe-livecycle-native-jboss-x86_win32.ear finns i exportmappen på `[AEM forms install directory]\configurationManager`. (om AEM Forms distribueras på en annan J2EE-programserver ersätter du filen adobe-livecycle-native-jboss-x86_win32.ear med den EAR-fil som motsvarar J2EE-programservern.)
* adobe-generatepdf-dsc.jar > adobe-appmondata.jar\com\adobe\appmon (filen adobe-appmondata.jar finns i filen adobe-generatepdf-dsc.jar). Filen adobe-generatepdf-dsc.jar finns i `[AEM forms install directory]\deploy` mapp.

När du har lagt till dessa XML-filer i filen adobe-appmondata.jar måste du distribuera om komponenten GeneratePDF. Så här lägger du till dialogrute- och skript-XML-filer i filen adobe-appmondata.jar:

1. Använd ett verktyg som WinZip eller WinRAR och öppna filen adobe-livecycle-native-jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > filen obe-appmondata.jar.
1. Lägg till dialogruta- och skript-XML-filer i filen appmondata.jar eller ändra befintliga XML-filer i filen. (Se [Skapa eller ändra en skript-XML-fil för ett internt program](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)och [Skapa eller ändra ytterligare en dialogrute-XML-fil för ett ursprungligt program](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).)
1. Öppna adobe-generatepdf-dsc.jar > adobe-appmondata.jar med ett verktyg som WinZip eller WinRAR.
1. Lägg till dialogruta- och skript-XML-filer i filen appmondata.jar eller ändra befintliga XML-filer i filen. (Se [Skapa eller ändra en skript-XML-fil för ett internt program](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)och [Skapa eller ändra ytterligare en dialogrute-XML-fil för ett ursprungligt program](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).) När du har lagt till XML-filerna i filen adobe-appmondata.jar lägger du in den nya filen adobe-appmondata.jar i filen adobe-generatepdf-dsc.jar.
1. Om du har lagt till stöd för ytterligare ett inbyggt filformat skapar du en systemmiljövariabel som anger programmets sökväg (se [Skapa en miljövariabel för att hitta det inbyggda programmet](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application).)

**Så här distribuerar du om komponenten GeneratePDF**

1. Logga in i Workbench.
1. Välj **Fönster** > **Visa vyer** > **Komponenter**. Den här åtgärden lägger till komponentvyn i Workbench.
1. Högerklicka på komponenten GeneratePDF och välj sedan **Stoppa komponent**.
1. När komponenten har stoppats högerklickar du och väljer Avinstallera komponent för att ta bort den.
1. Högerklicka på **Komponenter** ikon och markera **Installera komponent**.
1. Bläddra efter och välj den ändrade filen adobe-generatepdf-dsc.jar och klicka sedan på Öppna. Observera att en röd fyrkant visas bredvid komponenten GeneratePDF.
1. Expandera komponenten GeneratePDF, välj Tjänstbeskrivare och högerklicka sedan på GeneratePDFService och välj Aktivera tjänst.
1. Ange tillämpliga konfigurationsvärden i konfigurationsdialogrutan som visas. Om du lämnar dessa värden tomma används standardkonfigurationsvärdena.
1. Högerklicka på GeneratePDF och välj Start Component (Starta komponent).
1. Utöka aktiva tjänster. En grön pil visas bredvid tjänstnamnet om det körs. Annars är tjänsten i stoppat läge.
1. Om tjänsten är stoppad högerklickar du på tjänstnamnet och väljer Starta tjänst.

### Skapa eller ändra en skript-XML-fil för ett internt program {#creating-or-modifying-a-script-xml-file-for-a-native-application}

Om du vill dirigera filer till ett nytt originalprogram måste du skapa en skript-XML-fil för det programmet. Om du vill ändra hur tjänsten Generate PDF interagerar med ett program som redan stöds måste du ändra skriptet för det programmet.

Skriptet innehåller instruktioner som navigerar genom det inbyggda programmets fönsterelement och som ger specifika svar på dessa element. Filen som innehåller den här informationen är `appmon.`[appname]&quot; `.script.`[locale]`.xml`. Ett exempel är appmon.notepad.script.en_US.xml.

#### Identifiera steg som skriptet måste köra {#identifying-steps-the-script-must-execute}

Använd det inbyggda programmet för att bestämma vilka fönsterelement du måste navigera i och vilka svar du måste utföra för att skriva ut dokumentet. Lägg märke till de dialogrutor som är resultatet av ett svar. Stegen ser ut ungefär så här:

1. Välj Arkiv > Öppna.
1. Ange sökvägen och klicka sedan på Öppna.
1. Välj Arkiv > Skriv ut på menyraden.
1. Ange de egenskaper som krävs för skrivaren.
1. Välj Skriv ut och vänta tills dialogrutan Spara som visas. Dialogrutan Spara som krävs för att du ska kunna ange PDF-filens mål i tjänsten Generate PDF.

#### Identifiera dialogrutorna som anges i bildtextattribut {#identifying-the-dialogs-specified-in-caption-attributes}

Använd Microsoft Spy++ för att hämta identiteterna för fönsterelementegenskaper i det ursprungliga programmet. Du måste ha dessa identiteter för att kunna skriva skript.

#### Använda reguljära uttryck i bildtextattribut {#using-regular-expressions-in-caption-attributes}

Du kan använda reguljära uttryck i beskrivningsspecifikationer. Tjänsten Generate PDF använder `java.util.regex.Matcher` -klass som stöder reguljära uttryck. Verktyget har stöd för reguljära uttryck som beskrivs i `java.util.regex.Pattern`.

**Reguljärt uttryck som tar emot filnamnet som lagts till Anteckningar i banderollen Anteckningar**

```xml
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**Reguljärt uttryck som skiljer Skriv ut från Utskriftsformat**

```xml
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### Ordna elementen window och windowList {#ordering-the-window-and-windowlist-elements}

Du måste beställa `window` och `windowList` element enligt följande:

* Vid flera `window` -element visas som underordnade i `windowList` eller `dialog` element, beställa dessa `window` i fallande ordning, med längden på `caption` namn som anger positionen i ordningen.
* Vid flera `windowList` elementen visas i en `window` element, beställa dessa `windowList` i fallande ordning, med längden på `caption` den första `indexes/`-element som anger positionen i ordningen.

**Ordna fönsterelement i en dialogrutefil**

```xml
 <!-- The caption attribute in the following window element is 40 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <window caption="Unexpected Failure in DebugActiveProcess">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Adobe Acrobat - License Agreement">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Microsoft Visual.*Runtime Library">
     <…>
 </window>

 <!-- The caption attribute in the following window element is 28 characters long. It is the shortest caption in this example, so its parent window element appears after the others. -->
 <window caption="Adobe Acrobat - Registration">
     <…>
 </window>
```

**Ordna fönsterelement i ett windowList-element**

```xml
 <!-- The caption attribute in the following indexes element is 56 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <windowList>
     <window caption="Can&apos;t exit design mode because.* cannot be created"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
 <windowList>
     <window caption="Do you want to continue loading the project?"/>
     <window className="Button" caption="No" action="press"/>
 </windowList>
 <windowList>
     <window caption="The macros in this project are disabled"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
```

### Skapa eller ändra ytterligare en dialogrute-XML-fil för ett ursprungligt program {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

Om du skapar ett skript för ett internt program som inte stöds tidigare, måste du också skapa ytterligare en dialogrute-XML-fil för det programmet. Alla inbyggda program som AppMon använder får bara ha en ytterligare dialogrute-XML-fil. Ytterligare dialogrute-XML-fil krävs även om inga oombedda dialogrutor förväntas. Ytterligare dialogruta måste ha minst en `window` element, även om det `window` är bara en platshållare.

>[!NOTE]
>
I det här sammanhanget innebär termen ytterligare innehållet i `appmon.[applicationname].addition.[locale].xml` -fil. En sådan fil anger åsidosättningar och tillägg till XML-filen i dialogrutan.

Du kan också ändra XML-filen för ytterligare dialogrutor för ett internt program för följande syften:

* Så här åsidosätter du XML-filen i dialogrutor för ett program med ett annat svar
* Lägga till ett svar i en dialogruta som inte är adresserad i dialogrutans XML-fil för det programmet

Filnamnet som identifierar ytterligare en dialogXML-fil är `appmon.[appname].addition.[locale].xml`. Ett exempel är appmon.excel.addition.en_US.xml.

Namnet på XML-filen för ytterligare dialogrutor måste ha formatet `appmon.[applicationname].addition.[locale].xml`, där *programnamn* måste exakt matcha det programnamn som används i XML-konfigurationsfilen och i skriptet.

>[!NOTE]
>
Inget av de allmänna program som anges i konfigurationsfilen native2pdfconfig.xml har en primär dialogrute-XML-fil. Avsnittet [Lägga till eller ändra stöd för ett ursprungligt filformat](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) beskriver sådana specifikationer.

Du måste beställa `windowList` element som visas som underordnade i `window` -element. (Se [Ordna elementen window och windowList](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements).)

### Ändra den allmänna XML-filen i dialogrutan {#modifying-the-general-dialog-xml-file}

Du kan ändra den allmänna XML-filen i dialogrutan för att svara på dialogrutor som genereras av systemet eller för att svara på dialogrutor som är gemensamma för flera program.

#### Lägga till en filtypspost i XML-konfigurationsfilen {#adding-a-filetype-entry-in-the-xml-configuration-file}

I den här proceduren beskrivs hur du uppdaterar tjänstkonfigurationsfilen Generate PDF för att associera filtyper med systemspecifika program. Om du vill uppdatera den här konfigurationsfilen måste du använda administrationskonsolen för att exportera konfigurationsdata till en fil. Standardfilnamnet för konfigurationsdata är native2pdfconfig.xml.

**Uppdatera tjänstkonfigurationsfilen Generera PDF**

1. Välj **Startsida** > **Tjänster** > **Adobe PDF Generator** > **Konfigurationsfiler** och sedan markera **Exportera konfiguration**.
1. Ändra `filetype-settings` -element i filen native2pdfconfig.xml efter behov.
1. Välj **Startsida** > **Tjänster** > **Adobe PDF Generator** >**Konfigurationsfiler** och sedan markera **Importera konfiguration**. Konfigurationsdata importeras till tjänsten Generate PDF och ersätter tidigare inställningar.

>[!NOTE]
>
Programmets namn anges som värdet för `GenericApp` element `name` -attribut. Värdet måste exakt matcha motsvarande namn som anges i skriptet som du utvecklar för det programmet. På samma sätt visas `GenericApp` element `displayName` -attributet ska exakt matcha motsvarande skripts `expectedWindow` fönsterbeskrivning. En sådan motsvarighet utvärderas efter att eventuella reguljära uttryck som visas i `displayName` eller `caption` attribut.

I det här exemplet ändrades standardkonfigurationsdata som medföljde tjänsten Generate PDF så att Anteckningar (inte Microsoft Word) skulle användas för att bearbeta filer med filnamnstillägget .txt. Innan den här ändringen utfördes specificerades Microsoft Word som det ursprungliga program som ska bearbeta sådana filer.

**Ändringar för att dirigera textfiler till Notepad (native2pdfconfig.xml)**

```xml
 <filetype-settings>

 <!-- Some native app file types were omitted for brevity. -->
 <!-- The following GenericApp element specifies Notepad as the native application that should be used to process files that have a txt file name extension. -->
             <GenericApp
                 extensions="txt"
                 name="Notepad" displayName=".*Notepad"/>
             <GenericApp
                 extensions="wpd"
                 name="WordPerfect" displayName="Corel WordPerfect"/>
             <GenericApp extensions="pmd,pm6,p65,pm"
                 name="PageMaker" displayName="Adobe PageMaker"/>
             <GenericApp extensions="fm"
                 name="FrameMaker" displayName="Adobe FrameMaker"/>
             <GenericApp extensions="psd"
                 name="Photoshop" displayName="Adobe Photoshop"/>
         </settings>
     </filetype-settings>
```

#### Skapa en miljövariabel för att hitta det inbyggda programmet {#creating-an-environment-variable-to-locate-the-native-application}

Skapa en miljövariabel som anger platsen för det interna programmets körbara fil. Variabeln måste använda formatet `[applicationname]_PATH`, där *programnamn* måste exakt matcha det programnamn som används i XML-konfigurationsfilen och i skriptet, och där sökvägen till den körbara filen finns inom citattecken. Ett exempel på en sådan miljövariabel är `Photoshop_PATH`.

När du har skapat den nya systemvariabeln måste du starta om servern som tjänsten Generate PDF är distribuerad på.

**Skapa en systemvariabel i Windows XP-miljön**

1. Välj **Kontrollpanelen > System**.
1. I dialogrutan Systemegenskaper klickar du på **Avancerat** och sedan klicka på **Miljövariabler**.
1. Under Systemvariabler i dialogrutan Miljövariabler klickar du på **Nytt**.
1. I dialogrutan Ny systemvariabel, i **Variabelnamn** anger du ett namn som använder formatet `[applicationname]_PATH`.
1. I **Variabelvärde** skriver du den fullständiga sökvägen och filnamnet för programmets körbara fil och klickar sedan på **OK**. Skriv till exempel: `c:\windows\Notepad.exe`
1. I dialogrutan Miljövariabler klickar du på **OK**.

**Skapa en systemvariabel från kommandoraden**

1. I ett kommandoradsfönster skriver du variabeldefinitionen i det här formatet:

   ```shell
            [applicationname]_PATH=[Full path name]
   ```

   Skriv till exempel: `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. Starta en ny kommandoradsprompt så att systemvariabeln börjar gälla.

#### XML-filer {#xml-files}

AEM Forms innehåller XML-exempelfiler som gör att tjänsten Generate PDF kan använda Anteckningar för att bearbeta filer med filnamnstillägget .txt. Den här koden ingår i det här avsnittet. Dessutom måste du göra de andra ändringarna som beskrivs i det här avsnittet.

#### XML-fil för ytterligare dialogrutor {#additional-dialog-xml-file}

Det här exemplet innehåller ytterligare dialogrutor för programmet Anteckningar. De här dialogrutorna kan läggas till de som anges av tjänsten Generate PDF.

**Anteckningsdialogrutor (appmon.notepad.addition.en_US.xml)**

```xml
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd">
     <window caption="Caption Title">
         <windowList>
             <window className="Button" caption="OK" action="press"/>
         </windowList>
     </window>
 </dialogs>
```

#### Skript-XML-fil {#script-xml-file}

I det här exemplet anges hur tjänsten Generate PDF ska samverka med Anteckningar för att skriva ut filer med Adobe PDF-skrivaren.

**XML-fil för anteckningsskript (appmon.notepad.script.en_US.xml)**

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<!--
*
* ADOBE CONFIDENTIAL
* ___________________
* Copyright 2004 - 2005 Adobe Systems Incorporated
* All Rights Reserved.
*
* NOTICE:  All information contained herein is, and remains
* the property of Adobe Systems Incorporated and its suppliers,
* if any.  The intellectual and technical concepts contained
* herein are proprietary to Adobe Systems Incorporated and its
* suppliers and may be covered by U.S. and Foreign Patents,
* patents in process, and are protected by trade secret or copyright law.
* Dissemination of this information or reproduction of this material
* is strictly forbidden unless prior written permission is obtained
* from Adobe Systems Incorporated.
*-->

<!-- This file automates printing of text files via notepad to Adobe PDF printer. To see the complete hierarchy Adobe recommends using the Microsoft Spy++ which details the properties of windows necessary to write scripts. In this sample there are total of eight steps-->

<application name="Notepad" version="9.0" locale="en_US" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="scripts.xsd">

    <!-- In this step we wait for the application window to appear -->
    <step>
        <expectedWindow>
            <window caption=".*Notepad"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the application window and send File->Open menu bar, menu item commands and the expectation is the windows Open dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Open...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Open window and then select the 'Edit' widget and input the source path followed by clicking on the 'Open' button . The expectation of this 'action' is that the Open dialog will disappear -->
    <step>
        <acquiredWindow>
            <window caption="Open">
                <windowList>
                    <window className="ComboBoxEx32">
                        <windowList>
                            <window className="ComboBox">
                                <windowList>
                                <window className="Edit" action="inputSourcePath"/>
                                </windowList>
                            </window>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="Open" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open" action="disappear"/>
        </expectedWindow>
        <pause value="30"/>
    </step>

    <!-- In this step, we acquire the application window and send File->Print menu bar, menu item commands and the expectation is the windows Print dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Print...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print">
        </window>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Print dialog and click on the 'Preferences' button and the expected window in this case is the dialog with the caption '"Printing Preferences' -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General">
                        <windowList>
                            <window className="Button" caption="Preferences" action="press"/>
                        </windowList>
                    </window>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the dialog "Printing Preferences' and select the combo box which is the 10th child of window with caption '"Adobe PDF Settings' and select the first index. (Note: All indeces start with 0.) Besides this we uncheck the box which  has the caption '"View Adobe PDF results' and we click on the button OK. The expectation is that 'Printing Preferences' dialog disappears. -->
    <step>
        <acquiredWindow>
            <window caption="Printing Preferences">
                <windowList>
                    <window caption="Adobe PDF Settings">
                        <windowList>
                            <window className="Button" caption="View Adobe PDF results" action="uncheck"/>
                        </windowList>
                        <windowList>
                            <window className="Button" caption="Ask to Replace existing PDF file" action="uncheck"/>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="OK" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the 'Print' dialog and click on the Print button. The expectation is that the dialog with caption 'Print' disappears. In this case we use the regular expression '^Print$' for specifying the caption given there could be multiple dialogs with caption that includes the word Print. -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General"/>
                    <window className="Button" caption="^Print$" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print" action="disappear"/>
        </expectedWindow>
    </step>
    <step>
        <expectedWindow>
            <window caption="Save PDF File As"/>
        </expectedWindow>
    </step>
    <!-- Finally in this step, we acquire the dialog with caption "Save PDF File As" and in the Edit widget type the destination path for the output PDF file and click on the Save button. The expectation is that the dialog disappears-->
    <step>
        <acquiredWindow>
            <window caption="Save PDF File As">
                <windowList>
                    <window className="Edit" action="inputDestinationPath"/>
                </windowList>
                <windowList>
                    <window className="Button" caption="Save" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Save PDF File As" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- We can always set a retry count or a maximum time for a step. In case we surpass these limitations, PDF Generator generates this abort message and terminates processing. -->
    <abortMessage msg="15078"/>
</application>
```
