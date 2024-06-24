---
title: Konverterar PDF till PostScript- och bildfiler
description: Använd tjänsten Convert PDF för att konvertera PDF-dokument till PostScript och till flera bildformat (JPEG, JPEG 2000, PNG och TIFF) med Java API och Web Service API.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2774'
ht-degree: 0%

---

# Konverterar PDF till PostScript- och bildfiler {#converting-pdf-to-postscript-andimage-files}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

**Om tjänsten Convert PDF**

Med tjänsten Konvertera PDF kan du konvertera PDF-dokument till PostScript och till flera bildformat (JPEG, JPEG 2000, PNG och TIFF). Att konvertera ett PDF-dokument till PostScript är användbart för oövervakad serverbaserad utskrift på en PostScript-skrivare. Det är praktiskt att konvertera ett PDF-dokument till en flersidig TIFF-fil när du arkiverar dokument i innehållshanteringssystem som inte stöder PDF.

Du kan utföra följande uppgifter med hjälp av tjänsten Konvertera PDF:

* Konvertera PDF-dokument till PostScript.
* Konvertera PDF-dokument till bildformat.

>[!NOTE]
>
>Mer information om tjänsten Convert PDF finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Konverterar PDF-dokument till PostScript {#converting-pdf-documents-to-postscript}

I det här avsnittet beskrivs hur du kan använda API:t för Konvertera PDF-tjänst (Java och webbtjänst) för att programmässigt konvertera PDF-dokument till PostScript-filer. Dokumentet PDF som konverteras till en PostScript-fil måste vara ett icke-interaktivt PDF-dokument. Det innebär att om du försöker konvertera ett interaktivt PDF-dokument till en PostScript-fil genereras ett undantag.

>[!NOTE]
>
>Mer information om tjänsten Convert PDF finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Så här konverterar du ett PDF-dokument till en PostScript-fil:

1. Inkludera projektfiler.
1. Skapa en Convert PDF-tjänstklient.
1. Referera PDF-dokumentet som ska konverteras till en PostScript-fil.
1. Ange alternativ för konvertering vid körning.
1. Konvertera PDF-dokumentet till en PostScript-fil.
1. Spara PostScript-filen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du ta med proxyfilerna.

**Skapa en Konvertera PDF-klient**

Innan du programmässigt kan utföra en Convert PDF service-åtgärd måste du skapa en Convert PDF service client. Om du använder Java API skapar du en `ConvertPdfServiceClient` -objekt. Om du använder webbtjänstens API skapar du en `ConvertPDFServiceService` -objekt.

I det här avsnittet används webbtjänstfunktioner som introducerades i AEM Forms. För att få tillgång till nya funktioner måste du skapa proxyobjektet med `lc_version` -attribut. (Se &quot;Åtkomst av nya funktioner med hjälp av webbtjänster&quot; i [Anropa AEM Forms med Web Services](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**Referera PDF-dokumentet till en PostScript-fil**

Referera det PDF-dokument som du vill konvertera till en PostScript-fil. Som tidigare nämnts i det här avsnittet måste PDF-dokumentet vara ett icke-interaktivt PDF-dokument. Om du försöker konvertera ett interaktivt PDF-dokument till en PostScript-fil genereras ett undantag.

**Ange alternativ för konvertering vid körning**

När du konverterar ett PDF-dokument till en PostScript-fil kan du definiera körningsalternativ som anger vilken PostScript-typ som skapas. Du kan till exempel definiera en PostScript-fil på nivå 3.

Vanligtvis återspeglar den genererade PostScript-filen storleken på det inmatade PDF-dokumentet. Om du väljer `ShrinkToFit` (vilket minskar PostScript-filens utdata så att de passar in på sidan) kommer du inte att se någon skillnad mellan indatadokumentet och den genererade PostScript-filen. The `ShrinkToFit` fungerar bara om du väljer att skriva ut med en mindre sidstorlek än det inmatade PDF-dokumentet. Om du vill välja en mindre sidstorlek definierar du `PageSize` alternativ. Du bör dessutom ange `RotateAndCenter` alternativ till `true` för att få rätt PostScript-utdata.

Om du väljer `ExpandToFit` (som utökar PostScript-filens utdata så att de passar in på sidan) fungerar det bara om du väljer att skriva ut med en större sidstorlek än indatadokumentet i PDF. Om du vill välja en större sidstorlek definierar du `PageSize` alternativ. Du bör dessutom ange `RotateAndCenter` alternativ till `true` för att få rätt PostScript-utdata.

>[!NOTE]
>
>Mer information om de körningsvärden du kan ange finns i `ToPSOptionsSpec` klassreferens i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Konvertera PDF-dokumentet till en PostScript-fil**

När du har skapat tjänstklienten och angett körningsalternativ kan du anropa PostScript-konverteringsåtgärden. Den här åtgärden kräver information om dokumentet som ska konverteras, inklusive den PostScript-nivå som ska användas för måldokumentet.

**Spara PostScript-filen**

När du har konverterat PDF-dokumentet till PostScript kan du spara utdata som en PostScript-fil.

**Se även**

[Konvertera ett PDF-dokument till PS med Java API](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Konvertera ett PDF-dokument till PS med webbtjänstens API](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Convert PDF Service API](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Konvertera ett PDF-dokument till PS med Java API {#convert-a-pdf-document-to-ps-using-the-java-api}

Konvertera ett PDF-dokument till PostScript med hjälp av Java (Convert PDF Service API):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-convertpdf-client.jar, i Java-projektets klassökväg.

1. Skapa en Convert PDF-klient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `ConvertPdfServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Referera PDF-dokumentet som ska konverteras till en PostScript-fil.

   * Skapa en `java.io.FileInputStream` genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för det PDF-dokument som ska konverteras.
   * Skapa en `com.adobe.idp.Document` som lagrar PDF-dokumentet med hjälp av `com.adobe.idp.Document` konstruktor. Skicka `java.io.FileInputStream` -objekt som innehåller dokumentet PDF.

1. Ange alternativ för konvertering vid körning.

   * Skapa en `ToPSOptionsSpec` genom att anropa dess konstruktor.
   * Ange körningsalternativ genom att anropa en lämplig metod som tillhör `ToPSOptionsSpec` -objekt. Om du till exempel vill definiera PostScript-nivån som skapas, anropar du `ToPSOptionsSpec` objektets `setPsLevel` metod och skicka en `PSLevel` uppräkningsvärde som anger PostScript-nivån. Information om alla körningsvärden som du kan ange finns i `ToPSOptionsSpec` klassreferens i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Konvertera PDF-dokumentet till en PostScript-fil.

   Anropa `ConvertPdfServiceClient`objektets `toPS2` och skicka följande värden:

   * A `com.adobe.idp.Document` som representerar det PDF-dokument som ska konverteras till en PostScript-fil.
   * A `ToPSOptionsSpec` -objekt som anger alternativ för PostScript-körning.

   The `toPS2` returnerar en `Document` som innehåller det nya PostScript-dokumentet.

1. Spara PostScript-filen.

   * Skapa en `java.io.File` och se till att filnamnstillägget är .ps.
   * Anropa `Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` till filen (se till att du använder `Document` objekt som returneras av `toPS2` metod).

**Se även**

[Sammanfattning av steg](converting-pdf-postscript-image-files.md#summary-of-steps)

[Snabbstart (SOAP): Konvertera ett PDF-dokument till PostScript med Java API](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Konvertera ett PDF-dokument till PS med webbtjänstens API {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Konvertera ett PDF-dokument till PostScript med hjälp av API:t för konvertering av PDF (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en Convert PDF-klient.

   * Skapa en `ConvertPdfServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `ConvertPdfServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Du behöver inte använda `lc_version` -attribut. Ange dock `?blob=mtom`.
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `ConvertPdfServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Referera PDF-dokumentet som ska konverteras till en PostScript-fil.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra ett PDF-dokument som konverteras till en PostScript-fil.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det PDF-dokument som ska konverteras och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Ange alternativ för konvertering vid körning.

   * Skapa en `ToPSOptionsSpec` genom att anropa dess konstruktor.
   * Ange körningsalternativ genom att tilldela ett värde till `ToPSOptionsSpec` objektets datamedlem. Om du till exempel vill definiera PostScript-nivån som skapas tilldelar du en `PSLevel` uppräkningsvärde till `ToPSOptionsSpec` objektets `psLevel` datamedlem.

1. Konvertera PDF-dokumentet till en PostScript-fil.

   Anropa `GeneratePDFServiceService` objektets `toPS2` och skicka följande värden:

   * A `BLOB` objekt som representerar det PDF-dokument som ska konverteras till en PostScript-fil
   * A `ToPSOptionsSpec` objekt som anger körningsalternativ

   När konverteringen är klar extraherar du de binära data som representerar PostScript-dokumentet genom att öppna dess `BLOB` objektets `MTOM` -egenskap. Detta returnerar en bytearray som du kan skriva ut till en PostScript-fil.

1. Spara PostScript-filen.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för PS-filen.
   * Skapa en bytearray som lagrar datainnehållet i `BLOB` objekt som returneras av `encryptPDFUsingPassword` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` fält.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv innehållet i bytearrayen till PostScript-filen genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Sammanfattning av steg](converting-pdf-postscript-image-files.md#summary-of-steps)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Konvertera PDF-dokument till bildformat {#converting-pdf-documents-to-image-formats}

Du kan använda tjänsten Konvertera PDF för att programmässigt konvertera PDF-dokument till bildformat, som JPEG, JPEG 2000, TIFF och PNG. Genom att konvertera ett PDF-dokument till en bildfil kan du använda PDF-dokumentet som en bildfil. Du kan till exempel placera bilden i ett innehållshanteringssystem för företag för lagring.

När du konverterar ett PDF-dokument till en bild skapas en separat bild för varje i dokumentet med hjälp av tjänsten Konvertera PDF. Det vill säga, om dokumentet har 20 sidor, skapas 20 bildfiler med tjänsten Convert PDF. När du konverterar ett PDF-dokument till ett bildformat kan du skapa enskilda bilder för varje sida i PDF-dokumentet eller en enda bildfil för hela PDF-dokumentet.

>[!NOTE]
>
>Mer information om tjänsten Convert PDF finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-1}

Så här konverterar du ett PDF-dokument till någon av de typer som stöds:

1. Inkludera projektfiler.
1. Skapa en Convert PDF-tjänstklient.
1. Hämta det PDF-dokument som ska konverteras.
1. Ange körningsalternativ.
1. Konvertera PDF till en bild.
1. Hämta bildfilerna från en samling.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du ta med proxyfilerna.

**Skapa en Konvertera PDF-klient**

Innan du programmässigt kan utföra en Convert PDF service-åtgärd måste du skapa en Convert PDF service client. Om du använder Java API skapar du en `ConvertPdfServiceClient` -objekt. Om du använder webbtjänstens API skapar du en `ConvertPDFServiceService` -objekt.

**Hämta det PDF-dokument som ska konverteras**

Hämta dokumentet PDF för att konvertera till en bild. Du kan inte konvertera ett interaktivt PDF-dokument till en bild. Om du försöker göra det genereras ett undantag. Om du vill konvertera ett interaktivt PDF-dokument till en bildfil måste du förenkla PDF-dokumentet innan du konverterar det. (Se [Förenklar dokument i PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**Ange körningsalternativ**

Ange körningsalternativ som bildformat och upplösningsvärden. Mer information om körningsvärden finns i `ToImageOptionsSpec` klassreferens i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Konvertera PDF till en bild**

När du har skapat tjänstklienten och angett körningsalternativ kan du konvertera PDF-dokumentet till en bild. Ett samlingsobjekt som innehåller bilderna returneras.

**Hämta bildfilerna från en samling**

Du kan hämta bildfiler från ett samlingsobjekt som returneras av tjänsten Convert PDF. Varje element i samlingen är en `com.adobe.idp.Document` instans (eller en `BLOB` om du använder webbtjänster) som du kan spara som en bildfil, till exempel en JPG.

Bildfilens format beror på `ImageConvertFormat` körningsalternativ. Det vill säga om du ställer in `ImageConvertFormat` körningsalternativ till `ImageConvertFormat.JPEG`kan du spara bildfiler som JPG filer.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Convert PDF Service API](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Konvertera ett PDF-dokument till bildfiler med Java API {#convert-a-pdf-document-to-image-files-using-the-java-api}

Konvertera ett PDF-dokument till ett bildformat med hjälp av Java (Convert PDF service API):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-convertpdf-client.jar, i Java-projektets klassökväg.

1. Skapa en Convert PDF-klient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `ConvertPdfServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta det PDF-dokument som ska konverteras.

   * Skapa en `java.io.FileInputStream` objekt som representerar det PDF-dokument som ska konverteras med hjälp av dess konstruktor och som skickar ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ange körningsalternativ.

   * Skapa en `ToImageOptionsSpec` genom att använda dess konstruktor.
   * Anropa metoder som tillhör det här objektet efter behov. Ange till exempel bildtypen genom att anropa `setImageConvertFormat` metod och skicka en `ImageConvertFormat` enum-värde som anger formattypen.

   >[!NOTE]
   >
   >Ange `ImageConvertFormat` uppräkningsvärde är obligatoriskt.

1. Konvertera PDF till en bild.

   Anropa `ConvertPdfServiceClient` objektets `toImage2` och skicka följande värden:

   * A `com.adobe.idp.Document` objekt som representerar den PDF-fil som ska konverteras.
   * A `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` som innehåller de olika inställningarna för målbildens format.

   The `toImage2` returnerar en `java.util.List` objekt som innehåller bilder. Varje element i samlingen är en `com.adobe.idp.Document` -instans.

1. Hämta bildfilerna från en samling.

   Iterera genom `java.util.List` -objekt för att avgöra om det finns bilder. Varje element är en `com.adobe.idp.Document` -instans. Spara bilden genom att starta `com.adobe.idp.Document` objektets `copyToFile` metod och skicka en `java.io.File` -objekt.

**Se även**

[Snabbstart (SOAP): Konvertera ett PDF-dokument till JPEG med Java API](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Konvertera ett PDF-dokument till bildfiler med hjälp av webbtjänstens API {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Konvertera ett PDF-dokument till ett bildformat med hjälp av API:t för konvertering av PDF (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en konverteringsklient för PDF.

   * Skapa en `ConvertPdfServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `ConvertPdfServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Du behöver inte använda `lc_version` -attribut. Ange dock `?blob=mtom`.
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `ConvertPdfServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta det PDF-dokument som ska konverteras.

   * Skapa en `BLOB` genom att använda dess konstruktor. Detta `BLOB` -objektet används för att lagra PDF-formuläret.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som anger var PDF-formuläret finns och i vilket läge filen ska öppnas.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Bestämma bytearrayens storlek genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Ange körningsalternativ.

   * Skapa en `ToImageOptionsSpec` genom att använda dess konstruktor.
   * Anropa metoder som tillhör det här objektet efter behov. Ange till exempel bildtypen genom att anropa `setImageConvertFormat` metod och skicka en `ImageConvertFormat` uppräkningsvärde som anger formattypen.

   >[!NOTE]
   >
   >Ange `ImageConvertFormat` uppräkningsvärde är obligatoriskt.

1. Konvertera PDF till en bild.

   Anropa `ConvertPDFServiceService` objektets `toImage2` och skicka följande värden:

   * A `BLOB` objekt som representerar filen som ska konverteras
   * A `ToImageOptionsSpec` objekt som innehåller de olika inställningarna för målbildens format

   The `toImage2` returnerar en `MyArrayOfBLOB` -objekt som innehåller de nyskapade bildfilerna.

1. Hämta bildfilerna från en samling.

   * Ange antalet element i `MyArrayOfBLOB` genom att hämta värdet för dess `Count` fält. Varje element är en `BLOB` som innehåller bilden.
   * Iterera genom `MyArrayOfBLOB` och spara varje bildfil.

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
