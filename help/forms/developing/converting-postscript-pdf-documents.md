---
title: Konvertera PostScript till PDF-dokument
seo-title: Konvertera PostScript till PDF-dokument
description: 'null'
seo-description: 'null'
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konvertera PostScript till PDF-dokument {#converting-postscript-to-pdf-documents}

## Om Distiller Service {#about-the-distiller-service}

Tjänsten Distiller® konverterar PostScript®-, Encapsulated PostScript- (EPS) och PRN-filer till kompakta, tillförlitliga och säkrare PDF-filer i nätverket. Distiller-tjänsten används ofta för att konvertera stora volymer tryckta dokument till elektroniska dokument, till exempel fakturor och kontoutdrag. När man konverterar dokument till PDF kan man också skicka en pappersversion och en elektronisk version av ett dokument till sina kunder.

>[!NOTE]
>
>Mer information om Distiller-tjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

## Konvertera PostScript till PDF-dokument {#converting-postscript-to-pdf-documents-inner}

I det här avsnittet beskrivs hur du kan använda Distiller Service API (Java och webbtjänst) för att programmässigt konvertera PostScript- (PS), Encapsulated PostScript- (EPS) och PRN-filer till PDF-dokument.

>[!NOTE]
>
>Mer information om Distiller-tjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Om du vill konvertera PostScript-filer till PDF-dokument måste något av följande vara installerat på den server som är värd för AEM Forms: Återdistribuerbart paket för Acrobat 9 eller Microsoft Visual C++ 2005.

### Sammanfattning av steg {#summary-of-steps}

Så här konverterar du någon av de typer som stöds till ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en Distiller-tjänstklient.
1. Hämta filen som ska konverteras.
1. Anropa skapandet av PDF-filen.
1. Spara PDF-dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en Distiller-tjänstklient**

Innan du programmässigt kan utföra en Distiller-tjänståtgärd måste du skapa en Distiller-tjänstklient. Om du använder Java API skapar du ett `DistillerServiceClient` objekt. Om du använder webbtjänstens API skapar du ett `DistillerServiceService` objekt.

**Hämta filen som ska konverteras**

Du måste hämta filen som du vill konvertera. Om du till exempel vill konvertera en PS-fil till ett PDF-dokument måste du hämta PS-filen.

**Anropa skapandet av PDF-filen**

När du har skapat tjänstklienten kan du sedan starta PDF-genereringsåtgärden. Den här åtgärden kräver information om dokumentet som ska konverteras, inklusive sökvägen till måldokumentet.

**Spara PDF-dokumentet**

Du kan spara PDF-dokumentet som en PDF-fil.

**Se även**

[Konvertera en PostScript-fil till PDF med Java API](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Konvertera en PostScript-fil till PDF med webbtjänstens API](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Output Service API](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Konvertera en PostScript-fil till PDF med Java API {#convert-a-postscript-file-to-pdf-using-the-java-api}

Konvertera en PostScript-fil till PDF-dokument med Distiller Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-distiller-client.jar, i Java-projektets klassökväg.

1. Skapa en Distiller-tjänstklient.

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa ett `DistillerServiceClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.

1. Hämta filen som ska konverteras.

   * Skapa ett `java.io.FileInputStream` objekt som representerar filen som ska konverteras med hjälp av konstruktorn och skicka ett strängvärde som anger filens plats.
   * Skapa ett `com.adobe.idp.Document` objekt med hjälp av dess konstruktor och skicka `java.io.FileInputStream` objektet.

1. Anropa skapandet av PDF-filen.

   Anropa `DistillerServiceClient` objektets `createPDF` metod och skicka följande värden:

   * Det `com.adobe.idp.Document` objekt som representerar PS-, EPS- eller PRN-filen som ska konverteras
   * Ett `java.lang.String` objekt som innehåller namnet på filen som ska konverteras
   * Ett `java.lang.String` objekt som innehåller namnet på de Adobe PDF-inställningar som ska användas
   * Ett `java.lang.String` objekt som innehåller namnet på skyddsinställningarna som ska användas
   * Ett valfritt `com.adobe.idp.Document` objekt som innehåller inställningar som ska användas när PDF-dokumentet genereras
   * Ett valfritt `com.adobe.idp.Document` objekt som innehåller metadatainformation som ska användas i PDF-dokumentet
   Metoden returnerar `createPDF` ett `CreatePDFResult` objekt som innehåller det nya PDF-dokumentet och en loggfil som kan genereras. Loggfilen innehåller vanligen fel- eller varningsmeddelanden som genereras av konverteringsbegäran.

1. Spara PDF-dokumentet.

   Utför följande åtgärder för att hämta det nya PDF-dokumentet:

   * Anropa `CreatePDFResult` objektets `getCreatedDocument` metod. Detta returnerar ett `com.adobe.idp.Document` objekt.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att extrahera PDF-dokumentet.
   Utför på samma sätt följande åtgärder för att hämta loggdokumentet.

   * Anropa `CreatePDFResult` objektets `getLogDocument` metod. Detta returnerar ett `com.adobe.idp.Document` objekt.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att extrahera loggdokumentet.


**Se även**

[Sammanfattning av steg](converting-postscript-pdf-documents.md#summary-of-steps)

[Snabbstart (SOAP-läge): Konvertera en PostScript-fil till ett PDF-dokument med Java API](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Konvertera en PostScript-fil till PDF med webbtjänstens API {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Konvertera en PostScript-fil till PDF-dokument med Distiller Service API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen för servern som är värd för AEM Forms.

1. Skapa en Distiller-tjänstklient.

   * Skapa ett `DistillerServiceClient` objekt med hjälp av dess standardkonstruktor.
   * Skapa ett `DistillerServiceClient.Endpoint.Address` objekt med hjälp av `System.ServiceModel.EndpointAddress` konstruktorn. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/DistillerService?blob=mtom`.). Du behöver inte använda attributet `lc_version` . Det här attributet används när du skapar en tjänstreferens. Ange dock `?blob=mtom` att MTOM ska användas.
   * Skapa ett `System.ServiceModel.BasicHttpBinding` objekt genom att hämta värdet för `DistillerServiceClient.Endpoint.Binding` fältet. Sänd returvärdet till `BasicHttpBinding`.
   * Ställ in `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela användarnamnet för AEM-formulär till fältet `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta filen som ska konverteras.

   * Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Det här `BLOB` objektet används för att lagra filen som ska konverteras till ett PDF-dokument.
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar filens plats och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod och skicka bytearrayen, startpositionen och den strömlängd som ska läsas.
   * Fyll objektet `BLOB` genom att tilldela dess `MTOM` egenskap med innehållet i bytearrayen.

1. Anropa skapandet av PDF-filen.

   Anropa `DistillerServiceService` objektets `CreatePDF2` metod och skicka följande obligatoriska värden:

   * Det `BLOB` objekt som representerar PS-filen som ska konverteras
   * En sträng som innehåller sökvägen till filen som ska konverteras
   * Ett strängobjekt som innehåller de Adobe PDF-inställningar som ska användas (till exempel `Standard`)
   * Ett strängobjekt som innehåller de skyddsinställningar som ska användas (till exempel `No Securit`y)
   * Ett valfritt `BLOB` objekt som innehåller inställningar som ska användas när PDF-dokumentet genereras
   * Ett valfritt `BLOB` objekt som innehåller metadatainformation som ska användas i PDF-dokumentet
   * En `BLOB` utdataparameter som används för att lagra PDF-dokumentet
   * En `BLOB` utdataparameter som används för att lagra loggen

1. Spara PDF-dokumentet.

   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för det signerade PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i det `BLOB` objekt som returnerades av `CreatePDF2` metoden (parametern output). Fyll i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa ett `System.IO.BinaryWriter` objekt genom att anropa dess konstruktor och skicka `System.IO.FileStream` objektet.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` metod och skicka bytearrayen.

**Se även**

[Sammanfattning av steg](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Anropa AEM-formulär med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM-formulär med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
