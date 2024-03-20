---
title: Arbeta med PDF/A-dokument
description: Använd tjänsten DocConverter för att avgöra om ett PDF-dokument är ett PDF/A-dokument och konvertera PDF-dokument till PDF/A-dokument.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 966c3554-25df-4467-866e-11c43cc15b58
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 0%

---

# Arbeta med PDF/A-dokument {#working-with-pdf-a-documents}

**Om tjänsten DocConverter**

Tjänsten DocConverter kan konvertera PDF-dokument till PDA/A-dokument. Du kan utföra följande uppgifter med den här tjänsten:

* Konvertera PDF-dokument till PDF/A-dokument. (Se [Konvertera dokument till PDF/A-dokument](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* Kontrollera om PDF-dokument är PDF/A-dokument. (Se [Programmerat fastställa PDF/A-överensstämmelse](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>Mer information om tjänsten DocConverter finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Konvertera dokument till PDF/A-dokument {#converting-documents-to-pdf-a-documents}

Du kan använda tjänsten DocConverter för att konvertera ett PDF-dokument till ett PDF/A-dokument. Eftersom PDF/A är ett arkiveringsformat för långtidsbevaring av dokumentets innehåll, bäddas alla teckensnitt in och filen är okomprimerad. Därför är ett PDF/A-dokument vanligtvis större än ett PDF-standarddokument. Ett PDF/A-dokument innehåller inte heller ljud- och videoinnehåll. Innan du konverterar ett PDF-dokument till ett PDF/A-dokument måste du kontrollera att PDF-dokumentet inte är ett PDF/A-dokument.

Specifikationen PDF/A-1 består av två överensstämmelsenivåer, nämligen A och B. Den största skillnaden mellan de två är stöd för logisk struktur (hjälpmedel), som inte krävs för överensstämmelsenivå B. Oavsett överensstämmelsenivå anger PDF/A-1 att alla teckensnitt är inbäddade i det genererade PDF/A-dokumentet. För närvarande stöds endast PDF/A-1b vid validering (och konvertering).

PDF/A är standard för arkivering av PDF-dokument, men det är inte obligatoriskt att använda PDF/A för arkivering om ett standarddokument från PDF uppfyller företagets krav. Syftet med standarden PDF/A är att upprätta en PDF fil som är avsedd för långtidsarkivering och dokumentarkivering.

>[!NOTE]
>
>Mer information om tjänsten DocConverter finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Så här konverterar du ett PDF-dokument till ett PDF/A-dokument:

1. Inkludera projektfiler.
1. Skapa en DocConvert-klient
1. Referera ett PDF-dokument som ska konverteras till ett PDF/A-dokument.
1. Ange spårningsinformation.
1. Konvertera dokumentet.
1. Spara PDF/A-dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du ta med proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (krävs om AEM Forms körs på JBoss Application Server)
* jbossall-client.jar (krävs om AEM Forms körs på JBoss Application Server)

Mer information om var dessa JAR-filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Skapa en DocConvert-klient**

Innan du programmässigt kan utföra en DocConverter-åtgärd måste du skapa en DocConverter-klient. Om du använder Java API skapar du en `DocConverterServiceClient` -objekt. Om du använder webbtjänstens API:t DocConverter skapar du en `DocConverterServiceService` -objekt.

**Referera ett PDF-dokument som ska konverteras till ett PDF/A-dokument**

Hämta ett PDF-dokument som ska konverteras till ett PDF/A-dokument. Om du försöker konvertera ett PDF-dokument, t.ex. ett Acrobat-formulär, till ett PDF/A-dokument genereras ett undantag.

**Ange spårningsinformation**

Du kan ange ett körningsalternativ som avgör hur mycket information som spåras under konverteringsprocessen. Det innebär att du kan ange nio olika nivåer som anger hur mycket information tjänsten DocConverter spårar när ett PDF-dokument konverteras till ett PDF/A-dokument.

**Konvertera dokumentet**

När du har skapat DocConverter-tjänstklienten kan du konvertera dokumentet i PDF och ange ett körningsalternativ som anger hur mycket information som ska spåras. Du kan konvertera PDF-dokumentet till ett PDF/A-dokument.

**Spara PDF/A-dokumentet**

Du kan spara PDF/A-dokumentet som en PDF-fil.

**Se även**

[Konvertera dokument till PDF/A-dokument med Java API](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Konvertera dokument till PDF/A-dokument med webbtjänstens API](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Programmerat fastställa PDF/A-överensstämmelse](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Konvertera dokument till PDF/A-dokument med Java API {#convert-documents-to-pdf-a-documents-using-the-java-api}

Konvertera ett PDF-dokument till ett PDF/A-dokument med Java API:

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-docconverter-client.jar, i Java-projektets klassökväg.

1. Skapa en DocConvert-klient

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `DocConverterServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Referera ett PDF-dokument som ska konverteras till ett PDF/A-dokument

   * Skapa en `java.io.FileInputStream` objekt som representerar det PDF-dokument som ska konverteras med hjälp av dess konstruktor och som skickar ett strängvärde som anger platsen för PDF-filen.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ange spårningsinformation

   * Skapa en `PDFAConversionOptionSpec` genom att använda dess konstruktor.
   * Ange informationsspårningsnivå genom att anropa `PDFAConversionOptionSpec` objektets `setLogLevel` och skickar ett strängvärde som anger spårningsnivån. Skicka till exempel värdet `FINE`. Mer information om de olika värdena finns i `setLogLevel` metoden i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Konvertera dokumentet

   Konvertera PDF-dokumentet till ett PDF/A-dokument genom att anropa `DocConverterServiceClient` objektets `toPDFA` och skicka följande värden:

   * The `com.adobe.idp.Document` objekt som innehåller det PDF-dokument som ska konverteras
   * The `PDFAConversionOptionSpec` objekt som anger spårningsinformation

   The `toPDFA` returnerar en `PDFAConversionResult` objekt som innehåller PDF/A-dokumentet.

1. Spara PDF/A-dokumentet

   * Hämta PDF/A-dokumentet genom att anropa `PDFAConversionResult` objektets `getPDFA` -metod. Den här metoden returnerar en `com.adobe.idp.Document` objekt som representerar PDF/A-dokumentet.
   * Skapa en `java.io.File` objekt som representerar PDF/A-filen. Kontrollera att filnamnstillägget är .pdf.
   * Fyll filen med PDF/A-data genom att anropa `com.adobe.idp.Document` objektets `copyToFile` metoden och skicka `java.io.File` -objekt.

**Se även**

[Arbeta med PDF/A-dokument](pdf-a-documents.md#working-with-pdf-a-documents)

[Snabbstart (SOAP-läge): Konvertera ett dokument till ett PDF/A-dokument med Java API](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Konvertera dokument till PDF/A-dokument med webbtjänstens API {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Konvertera ett PDF-dokument till ett PDF/A-dokument med hjälp av DocConverter API (webbtjänsten):

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som använder DocConverter WSDL.
   * Referera till Microsoft .NET-klientsammansättningen.

1. Skapa en DocConvert-klient

   * Skapa en `DocConverterServiceService` genom att anropa dess standardkonstruktor.
   * Ange `DocConverterServiceService` objektets `Credentials` datamedlem med en `System.Net.NetworkCredential` värde som anger användarnamnet och lösenordsvärdet.

1. Referera ett PDF-dokument som ska konverteras till ett PDF/A-dokument

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra PDF-dokumentet som konverteras till ett PDF/A-dokument.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `binaryData` med bytearrayens innehåll.

1. Ange spårningsinformation

   * Skapa en `PDFAConversionOptionSpec` genom att använda dess konstruktor.
   * Ange informationsspårningsnivå genom att tilldela ett värde som anger spårningsnivån till `PDFAConversionOptionSpec` objektets `logLevel` datamedlem. Tilldela till exempel värdet `FINE` till denna datamedlem.

1. Konvertera dokumentet

   Konvertera PDF-dokumentet till ett PDF/A-dokument genom att anropa `DocConverterServiceService` objektets `toPDFA` och skicka följande värden:

   * The `BLOB` objekt som innehåller det PDF-dokument som ska konverteras
   * The `PDFAConversionOptionSpec` objekt som anger spårningsinformation

   The `toPDFA` returnerar en `PDFAConversionResult` objekt som innehåller PDF/A-dokumentet.

1. Spara PDF/A-dokumentet

   * Skapa en `BLOB` objekt som lagrar PDF/A-dokumentet genom att hämta värdet för `PDFAConversionResult` objektets `PDFADocument` datamedlem.
   * Skapa en bytearray som lagrar innehållet i `BLOB` objekt som returneras med `PDFAConversionResult` -objekt. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `binaryData` datamedlem.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för PDF/A-dokumentet.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Arbeta med PDF/A-dokument](pdf-a-documents.md#working-with-pdf-a-documents)

[Anropa AEM Forms med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Skapa en .NET-klientsammansättning som använder Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Programmerat fastställa PDF/A-överensstämmelse {#programmatically-determining-pdf-a-compliancy}

Du kan använda tjänsten DocConverter för att avgöra om ett PDF-dokument är PDF/A-kompatibelt. Mer information om ett PDF/A-dokument och hur du konverterar ett PDF-dokument till ett PDF/A-dokument finns i [Konvertera dokument till PDF/A-dokument](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>Mer information om tjänsten DocConverter finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-1}

Utför följande steg för att fastställa kompatibiliteten för PDF/A:

1. Inkludera projektfiler.
1. Skapa en DocConvert-klient
1. Referera till ett PDF-dokument som används för att fastställa kompatibiliteten mellan PDF och A.
1. Ange körningsalternativ.
1. Hämta information om PDF-dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du ta med proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (krävs om AEM Forms körs på JBoss Application Server)
* jbossall-client.jar (krävs om AEM Forms körs på JBoss Application Server)

Mer information om var dessa JAR-filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Skapa en DocConvert-klient**

Innan du programmässigt kan utföra en DocConverter-åtgärd måste du skapa en DocConverter-klient. Om du använder Java API skapar du en `DocConverterServiceClient` -objekt. Om du använder webbtjänstens API:t DocConverter skapar du en `DocConverterServiceService` -objekt.

**Referera till ett PDF-dokument som används för att fastställa kompatibiliteten mellan PDF och A**

Ett PDF-dokument måste refereras och skickas till DocConverter-tjänsten för att avgöra om PDF-dokumentet är PDF/A-kompatibelt.

**Ange körningsalternativ**

Du kan ange ett körningsalternativ som avgör hur mycket information som spåras under konverteringsprocessen. Det innebär att du kan ange nio olika nivåer som anger hur mycket information tjänsten DocConverter spårar när ett PDF-dokument konverteras till ett PDF/A-dokument.

**Hämta information om PDF-dokumentet**

När du har skapat DocConverter-tjänstklienten, refererat till PDF-dokumentet och angett körningsalternativ, kan du avgöra om PDF-dokumentet är ett PDF/A-kompatibelt dokument.

**Se även**

[Kontrollera kompatibiliteten PDF/A med Java API](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Kontrollera kompatibiliteten PDF/A med hjälp av webbtjänstens API](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Kontrollera kompatibiliteten PDF/A med Java API {#determine-pdf-a-compliancy-using-the-java-api}

Kontrollera kompatibiliteten PDF/A med Java API:

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-docconverter-client.jar, i Java-projektets klassökväg.

1. Skapa en DocConvert-klient

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `DocConverterServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Referera till ett PDF-dokument som används för att fastställa kompatibiliteten mellan PDF och A

   * Skapa en `java.io.FileInputStream` objekt som representerar det PDF-dokument som ska konverteras med hjälp av dess konstruktor och som skickar ett strängvärde som anger platsen för PDF-filen.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ange körningsalternativ

   * Skapa en `PDFAValidationOptionSpec` genom att använda dess konstruktor.
   * Ange efterlevnadsnivån genom att anropa `PDFAValidationOptionSpec` objektets `setCompliance` metod och att skicka `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Ange informationsspårningsnivå genom att anropa `PDFAValidationOptionSpec` objektets `setLogLevel` och skickar ett strängvärde som anger spårningsnivån. Skicka till exempel värdet `FINE`. Mer information om de olika värdena finns i `setLogLevel` metoden i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Hämta information om PDF-dokumentet

   Kontrollera PDF/A-kompatibiliteten genom att anropa `DocConverterServiceClient` objektets `isPDFA` och skicka följande värden:

   * The `com.adobe.idp.Document` -objekt som innehåller dokumentet PDF.
   * The `PDFAValidationOptionSpec` objekt som anger körningsalternativ.

   The `isPDFA` returnerar en `PDFAValidationResult` objekt som innehåller resultatet av den här åtgärden.

**Se även**

[Arbeta med PDF/A-dokument](pdf-a-documents.md#working-with-pdf-a-documents)

[Snabbstart (SOAP-läge): Kontrollera PDF/A-kompatibilitet med Java API](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Kontrollera kompatibiliteten PDF/A med hjälp av webbtjänstens API {#determine-pdf-a-compliancy-using-the-web-service-api}

Kontrollera kompatibiliteten PDF/A med hjälp av webbtjänstens API:

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som använder DocConverter WSDL.
   * Referera till Microsoft .NET-klientsammansättningen.

1. Skapa en DocConvert-klient

   * Skapa en `DocConverterServiceService` genom att anropa dess standardkonstruktor.
   * Ange `DocConverterServiceService` objektets `Credentials` datamedlem med en `System.Net.NetworkCredential` värde som anger användarnamnet och lösenordsvärdet.

1. Referera till ett PDF-dokument som används för att fastställa kompatibiliteten mellan PDF och A

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra PDF-dokumentet som konverteras till ett PDF/A-dokument.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `binaryData` med bytearrayens innehåll.

1. Ange körningsalternativ

   * Skapa en `PDFAValidationOptionSpec` genom att använda dess konstruktor.
   * Ange kompatibilitetsnivå genom att tilldela `PDFAValidationOptionSpec` objektets `compliance` datamedlem med värdet `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * Ange informationsspårningsnivå genom att tilldela `PDFAValidationOptionSpec` objektets `resultLevel` datamedlem med värdet `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. Hämta information om PDF-dokumentet

   Kontrollera PDF/A-kompatibiliteten genom att anropa `DocConverterServiceService` objektets `isPDFA` och skicka följande värden:

   * The `BLOB` -objekt som innehåller dokumentet PDF.
   * The `PDFAValidationOptionSpec` objekt som innehåller körningsalternativ.

   The `isPDFA` returnerar en `PDFAValidationResult` objekt som innehåller resultatet av den här åtgärden.

**Se även**

[Arbeta med PDF/A-dokument](pdf-a-documents.md#working-with-pdf-a-documents)

[Anropa AEM Forms med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Skapa en .NET-klientsammansättning som använder Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
