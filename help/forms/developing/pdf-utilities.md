---
title: Arbeta med PDF-verktyg
seo-title: Arbeta med PDF-verktyg
description: 'null'
seo-description: 'null'
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Arbeta med PDF-verktyg {#working-with-pdf-utilities}

**Om PDF Utilities Service**

Tjänsten PDF Utilities kan konvertera mellan PDF- och XDP-filformat, ställa in och hämta PDF-dokumentegenskaper samt hantera XMP-metadata. Innan du konverterar ett PDF-dokument till ett annat format är det till exempel praktiskt att kontrollera egenskaperna för dokumentet för att avgöra vilken tjänståtgärd som ska anropas för konverteringen.

Du kan utföra följande uppgifter med PDF-verktygstjänsten:

* Konvertera PDF-dokument till XDP-dokument.
* Konvertera XDP-dokument till PDF-dokument. (Se [Konvertera XDP-dokument till PDF-dokument](pdf-utilities.md#converting-xdp-documents-into-pdf-documents).)
* Hämta PDF-dokumentegenskaper. (Se [Hämta PDF-dokumentegenskaper](pdf-utilities.md#retrieving-pdf-document-properties).)
* Spara ett PDF-dokument och optimera det för snabb webbvisning. (Se [Ställa in sparningslägen](pdf-utilities.md#setting-pdf-document-save-modes)för PDF-dokument.)

>[!NOTE]
>
>Mer information om tjänsten PDF Utilities finns i [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Konvertera PDF-dokument till XDP-dokument {#converting-pdf-documents-into-xdp-documents}

Du kan använda PDF Utilities Java och webbtjänstens API:er för att programmässigt konvertera PDF-dokument till XDP-dokument.

>[!NOTE]
>
>Mer information om tjänsten PDF Utilities finns i [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Så här konverterar du ett PDF-dokument till ett XDP-dokument:

1. Inkludera projektfiler.
1. Skapa en PDFUtilityService-klient.
1. Anropa konverteringsåtgärden PDF till XDP.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en PDFUtilityService-klient**

Innan du kan utföra en programmässig PDF Utilities-åtgärd måste du skapa en PDFUtilityService-klient. Med Java API kan du uppnå detta genom att skapa ett `PDFUtilityServiceClient` objekt. Med webbtjänstens API kan du uppnå detta genom att använda ett `PDFUtilityServiceService` objekt.

**Anropa konverteringsåtgärden PDF till XDP**

När du har skapat tjänstklienten kan du anropa konverteringsåtgärden PDF till XDP.

**Se även**

[Konvertera PDF-dokument till XDP-dokument med Java API](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Konvertera PDF-dokument till XDP-dokument med webbtjänstens API](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Konvertera PDF-dokument till XDP-dokument med Java API {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Konvertera PDF-dokument till XDP-dokument med PDF Utilities API(Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-pdfutility-client.jar, i Java-projektets klassökväg.

1. Skapa en PDFUtilityService-klient

   Skapa ett `PDFUtilityServiceClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Anropa konverteringsåtgärden PDF till XDP

   Om du vill utföra konverteringen anropar du `PDFUtilityServiceClient` objektets `convertPDFtoXDP` metod och skickar ett `com.adobe.idp.Document` objekt som representerar PDF-filen. Metoden returnerar ett `com.adobe.idp.Document` objekt som representerar den nya XDP-filen.

**Se även**

[Konvertera PDF-dokument till XDP-dokument](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Konvertera PDF-dokument till XDP-dokument med webbtjänstens API {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Konvertera PDF-dokument till XDP-dokument med PDF Utilities API (webbtjänst):

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som använder PDF Utilities-tjänstens WSDL-fil.
   * Referera till Microsoft .NET-klientsammansättningen.

1. Skapa en PDFUtilityService-klient

   Skapa ett `PDFUtilityServiceService` objekt med hjälp av din proxyklasskonstruktor.

1. Anropa konverteringsåtgärden PDF till XDP

   Anropa `PDFUtilityServiceService` objektets `convertPDFtoXDP` metod och skicka ett `BLOB` objekt som representerar PDF-filen. Metoden returnerar ett `BLOB` objekt som representerar den nya XDP-filen.

**Se även**

[Konvertera PDF-dokument till XDP-dokument](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Skapa en .NET-klientsammansättning som använder Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Konvertera XDP-dokument till PDF-dokument {#converting-xdp-documents-into-pdf-documents}

Du kan använda PDF Utilities Java och webbtjänstens API:er för att programmässigt konvertera XDP-dokument till PDF-dokument.

>[!NOTE]
>
>Mer information om tjänsten PDF Utilities finns i [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-1}

Så här konverterar du ett XDP-dokument till ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en PDFUtilityService-klient.
1. Anropa konverteringsåtgärden XDP till PDF.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en PDFUtilityService-klient**

Innan du kan utföra en programmässig PDF Utilities-åtgärd måste du skapa en PDFUtilityService-klient. Med Java API kan du uppnå detta genom att skapa ett `PDFUtilityServiceClient` objekt. Med webbtjänstens API kan du uppnå detta genom att använda ett `PDFUtilityServiceService` objekt.

**Anropa konverteringsåtgärden XDP till PDF**

När du har skapat tjänstklienten kan du anropa konverteringsåtgärden XDP till PDF.

**Se även**

[Konvertera XDP-dokument till PDF-dokument med Java API](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Konvertera XDP-dokument till PDF-dokument med webbtjänstens API](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Konvertera XDP-dokument till PDF-dokument med Java API {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Konvertera XDP-dokument till PDF-dokument med PDF Utilities API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-pdfutility-client.jar, i Java-projektets klassökväg.

1. Skapa en PDFUtilityService-klient

   Skapa ett `PDFUtilityServiceClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Anropa konverteringsåtgärden XDP till PDF

   Om du vill utföra konverteringen anropar du `PDFUtilityServiceClient` objektets `convertXDPtoPDF` metod och skickar ett `com.adobe.idp.Document` objekt som representerar XDP-filen. Metoden returnerar ett `com.adobe.idp.Document` objekt som representerar den nya PDF-filen.

**Se även**

[Konvertera XDP-dokument till PDF-dokument](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Konvertera XDP-dokument till PDF-dokument med webbtjänstens API {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Konvertera XDP-dokument till PDF-dokument med PDF Utilities API (web service API):

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som använder PDF Utilities-tjänstens WSDL-fil.
   * Referera till Microsoft .NET-klientsammansättningen.

1. Skapa en PDFUtilityService-klient

   Skapa ett `PDFUtilityServiceService` objekt med hjälp av din proxyklasskonstruktor.

1. Anropa konverteringsåtgärden XDP till PDF

   Om du vill utföra konverteringen anropar du `PDFUtilityServiceService` objektets `convertXDPtoPDF` metod och skickar ett `BLOB` objekt som representerar XDP-filen. Metoden returnerar ett `BLOB` objekt som representerar den nya PDF-filen.

**Se även**

[Konvertera XDP-dokument till PDF-dokument](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Skapa en .NET-klientsammansättning som använder Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Hämtar PDF-dokumentegenskaper {#retrieving-pdf-document-properties}

Du kan använda PDF Utilities Java och webbtjänstens API:er för att hämta PDF-dokumentegenskaper programmatiskt, t.ex. om dokumentet är ett ifyllbart formulär eller den lägsta Acrobat-version som krävs för att läsa dokumentet.

>[!NOTE]
>
>Mer information om tjänsten PDF Utilities finns i [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Sammanfattning av steg {#summary_of_steps-2}

Så här hämtar du PDF-dokumentegenskaper:

1. Inkludera projektfiler.
1. Skapa en PDFUtilityService-klient.
1. Anropa hämtningsåtgärden för egenskaper.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en PDFUtilityService-klient**

Innan du kan utföra en programmässig PDF Utilities-åtgärd måste du skapa en PDFUtilityService-klient. Med Java API kan du uppnå detta genom att skapa ett `PDFUtilityServiceClient` objekt. Med webbtjänstens API:er uppnås detta med hjälp av ett `PDFUtilityServiceService` objekt.

**Anropa hämtningsåtgärden för egenskaper**

När du har skapat tjänstklienten kan du anropa hämtningsåtgärden för egenskaper.

**Se även**

[Hämta PDF-dokumentegenskaper med Java API](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Hämta PDF-dokumentegenskaper med webbtjänstens API](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Hämta PDF-dokumentegenskaper med Java API {#retrieve-pdf-document-properties-using-the-java-api}

Hämta PDF-dokumentegenskaper med PDF Utilities API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-pdfutility-client.jar, i Java-projektets klassökväg.

1. Skapa en PDFUtilityService-klient

   Skapa ett `PDFUtilityServiceClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Anropa hämtningsåtgärden för egenskaper

   Om du vill utföra konverteringen anropar du `PDFUtilityServiceClient` objektets `getPDFProperties` metod och skickar följande:

   * Ett `com.adobe.idp.Document` objekt som representerar PDF-dokumentet.
   * Ett `PDFPropertiesOptionSpec` objekt som innehåller de egenskaper som ska utvärderas.
   Metoden returnerar ett `PDFPropertiesResult` objekt som innehåller resultatet av frågan.

**Se även**

[Hämtar PDF-dokumentegenskaper](pdf-utilities.md#retrieving-pdf-document-properties)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Hämta PDF-dokumentegenskaper med webbtjänstens API {#retrieve-pdf-document-properties-using-the-web-service-api}

Hämta PDF-dokumentegenskaper med PDF Utilities webbtjänst-API:

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som använder PDF Utilities-tjänstens WSDL-fil.
   * Referera till Microsoft .NET-klientsammansättningen.

1. Skapa en PDFUtilityService-klient

   Skapa ett `PDFUtilityServiceService` objekt med hjälp av din proxyklasskonstruktor.

1. Anropa hämtningsåtgärden för egenskaper

   Om du vill utföra konverteringen anropar du `PDFUtilityServiceService` objektets `getPDFProperties` metod och skickar följande:

   * Ett `BLOB` objekt som representerar PDF-dokumentet.
   * Ett `PDFPropertiesOptionSpec` objekt som innehåller de egenskaper som ska utvärderas.
   Metoden returnerar ett `PDFPropertiesResult` objekt som innehåller resultatet av frågan.

**Se även**

[Hämtar PDF-dokumentegenskaper](pdf-utilities.md#retrieving-pdf-document-properties)

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Skapa en .NET-klientsammansättning som använder Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Ställa in sparningsläge för PDF-dokument {#setting-pdf-document-save-modes}

Du kan använda Java- och webbtjänstens API:er för PDF-verktygstjänsten för att programmässigt ange ett sparläge för ett PDF-dokument. När du använder PDF-verktygstjänsten för att ange ett sparningsläge, anger PDF-verktygstjänsten bara sparningsläget och sparar inte PDF-dokumentet. PDF-dokumentet sparas när det skickas till en annan tjänståtgärd. Du kan till exempel använda tjänsten PDF Utilities för att ange ett specifikt sparningsläge och skicka det till krypteringstjänsten, där PDF-dokumentet faktiskt sparas och krypteras.

>[!NOTE]
>
>Mer information om tjänsten PDF Utilities finns i [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-3}

Så här anger du sparalternativ för PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en PDFUtilityService-klient.
1. Ange sparningsläge.
1. Anropa sparåtgärden.
1. Skicka PDF-dokumentet till en annan åtgärd.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en PDFUtilityService-klient**

Innan du kan utföra en programmässig PDF Utilities-åtgärd måste du skapa en PDFUtilityService-klient. Med Java API kan du uppnå detta genom att skapa ett `PDFUtilityServiceClient` objekt. Med webbtjänstens API:er uppnås detta med hjälp av ett `PDFUtilityServiceService` objekt.

**Ange sparningsläge**

Du kan välja något av följande alternativ för att spara:

* `INCREMENTAL`: Spara stegvis för att minska tidsåtgången
* `FAST_WEB_VIEW`: spara för snabb webbvisning
* `FULL`: Spara med fullständig sparning (utan optimeringar)

**Anropa åtgärden Spara stil**

När du har skapat tjänstklienten kan du anropa hämtningsåtgärden för egenskaper.

**Skicka PDF-dokumentet till en annan AEM Forms-åtgärd**

När PDF Utilities-tjänsten har angett det sparade läget skickar du PDF-dokumentet till en annan AEM Forms-åtgärd. När PDF-dokumentet har returnerats från den åtgärden sparas det i det angivna läget. Om du till exempel använder tjänsten PDF Utilities för att ange `FAST_WEB_VIEW` läge och sedan skickar PDF-dokumentet till krypteringstjänstens `encryptUsingPassword` åtgärd, krypteras det returnerade PDF-dokumentet med ett lösenord och sparas i `FAST_WEB_VIEW` läget.

>[!NOTE]
>
>Snabbstart som är associerat med det här avsnittet anger `FAST_WEB_VIEW` läget och skickar sedan PDF-dokumentet till krypteringstjänstens `encryptUsingPassword` åtgärd.

**Se även**

[Ange alternativ för att spara PDF-dokument med Java API](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Ange alternativ för att spara PDF-dokument med hjälp av webbtjänstens API](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Kryptera PDF-dokument med ett lösenord](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Ange alternativ för att spara PDF-dokument med Java API {#set-pdf-document-save-options-using-the-java-api}

Ange sparalternativ för PDF-dokument med PDF Utilities API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-pdfutility-client.jar, i Java-projektets klassökväg.

1. Skapa en PDFUtilityService-klient

   Skapa ett `PDFUtilityServiceClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Ange sparningsläge

   * Skapa ett `PDFUtilitySaveMode` objekt med hjälp av dess konstruktor.
   * Ange sparningsläget genom att anropa `PDFUtilitySaveMode` objektets `setSaveStyle` metod och skicka ett strängvärde som anger sparningsläget. Om du till exempel vill spara för snabb webbvisning skickar du `FAST_WEB_VIEW`.

1. Anropa åtgärden Spara stil

   Anropa `PDFUtilityServiceClient` objektets `setSaveMode` metod och skicka följande värden:

   * Ett `com.adobe.idp.Document` objekt som representerar PDF-dokumentet.
   * Ett `PDFUtilitySaveMode` objekt som innehåller det sparade format som ska användas.
   * Ett booleskt värde som används för att avgöra om tidigare inställningar ska åsidosättas.
   Metoden returnerar ett `com.adobe.idp.Document` objekt som är formaterat med det angivna sparformatet.

1. Skicka PDF-dokumentet till en annan AEM Forms-åtgärd

   * Skicka det returnerade `com.adobe.idp.Document` objektet till en annan AEM Forms-åtgärd.

**Se även**

[Ställa in sparningsläge för PDF-dokument](pdf-utilities.md#setting-pdf-document-save-modes)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ange alternativ för att spara PDF-dokument med hjälp av webbtjänstens API {#set-pdf-document-save-options-using-the-web-service-api}

Ange alternativ för att spara PDF-dokument med PDF Utilities AP (webbtjänst):

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som använder PDF Utilities-tjänstens WSDL-fil.
   * Referera till Microsoft .NET-klientsammansättningen.

1. Skapa en PDFUtilityService-klient

   Skapa ett `PDFUtilityServiceService` objekt med hjälp av din proxyklasskonstruktor.

1. Ange sparningsläge

   * Skapa ett `PDFUtilitySaveMode` objekt med hjälp av dess konstruktor.
   * Ange sparningsläget genom att tilldela ett strängvärde till `PDFUtilitySaveMode` objektets `saveStyle` metod som anger sparningsläget. Om du till exempel vill spara för snabb webbvisning anger du `FAST_WEB_VIEW`.

1. Anropa åtgärden Spara stil

   Anropa `PDFUtilityServiceService` objektets `setSaveMode` metod och skicka följande värden:

   * Ett `BLOB` objekt som representerar PDF-dokumentet.
   * Ett `PDFUtilitySaveMode` objekt som innehåller det sparade format som ska användas.
   * Ett booleskt värde som används för att avgöra om tidigare inställningar ska åsidosättas.
   Metoden returnerar ett `BLOB` objekt som är formaterat med det angivna sparformatet. Du kan sedan spara objektet som ett PDF-dokument.

1. Skicka PDF-dokumentet till ett annat formulär

   * Skicka det returnerade `BLOB` objektet till en annan AEM Forms-åtgärd.

**Se även**

[Ställa in sparningsläge för PDF-dokument](pdf-utilities.md#setting-pdf-document-save-modes)

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Skapa en .NET-klientsammansättning som använder Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Sanera PDF-dokument {#sanitizing-pdf-documents}

Du kan använda Java-API:erna för PDF-verktyg för att programmässigt konvertera PDF-dokument till XDP-dokument.

>[!NOTE]
>
>Mer information om tjänsten PDF Utilities finns i [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-4}

Så här sanerar du PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en PDFUtilityService-klient.
1. Anropa saneringsåtgärden.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du vill skapa ett klientprogram med Java inkluderar du de JAR-filer som behövs.

**Skapa en PDFUtilityService-klient**

Innan du programmässigt kan utföra en saneringsåtgärd måste du skapa en PDFUtilityService-klient. Med Java API kan du uppnå detta genom att skapa ett `PDFUtilityServiceClient` objekt.

**Anropa konverteringsåtgärden PDF till XDP**

När du har skapat tjänstklienten kan du anropa saneringsåtgärden.

**Se även**

[Konvertera PDF-dokument till XDP-dokument med Java API](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Konvertera PDF-dokument till XDP-dokument med webbtjänstens API](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Sanera PDF-dokument med Java API {#sanitize-pdf-documents-using-the-java-api}

Sanera dokument med PDF Utilities API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-pdfutility-client.jar, i Java-projektets klassökväg.

1. Skapa en PDFUtilityService-klient

   Skapa ett `PDFUtilityServiceClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Anropa konverteringsåtgärden PDF till XDP

   Om du vill utföra konverteringen anropar du `PDFUtilityServiceClient` objektets `convertPDFtoXDP` metod och skickar ett `com.adobe.idp.Document` objekt som representerar PDF-filen. Metoden returnerar ett `com.adobe.idp.Document` objekt som representerar den nya XDP-filen.

**Se även**

[Sanera PDF-dokument](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
