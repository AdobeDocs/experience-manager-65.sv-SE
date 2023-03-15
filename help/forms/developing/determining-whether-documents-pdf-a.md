---
title: Avgöra om dokument är PDF/A-kompatibla
seo-title: Determining Whether Documents Are PDF/A-Compliant
description: Använd Assembler-tjänsten för att avgöra om ett PDF-dokument är PDF/A-kompatibelt med Java API och Web Service API.
seo-description: Use the Assembler service to determine if a PDF document is PDF/A-compliant using the Java API and Web Service API.
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
role: Developer
exl-id: 096fd2ac-616f-484a-b093-9d98b2f87093
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 0%

---

# Avgöra om dokument är PDF/A-kompatibla {#determining-whether-documents-are-pdf-a-compliant}

Du kan avgöra om ett PDF-dokument är PDF/A-kompatibelt med hjälp av Assembler-tjänsten. Ett PDF/A-dokument finns som ett arkiveringsformat som är avsett för långtidsarkivering av dokumentets innehåll. Teckensnitten bäddas in i dokumentet och filen är okomprimerad. Därför är ett PDF/A-dokument vanligtvis större än ett PDF-standarddokument. Ett PDF/A-dokument innehåller inte heller ljud- och videoinnehåll.

Specifikationen PDF/A-1 består av två överensstämmelsenivåer, nämligen A och B. Den största skillnaden mellan de två nivåerna är det logiska strukturstödet (hjälpmedel), som inte krävs för överensstämmelsenivå B. Oavsett överensstämmelsenivå anger PDF/A-1 att alla teckensnitt är inbäddade i det genererade PDF/A-dokumentet. För närvarande stöds endast PDF/A-1b vid validering (och konvertering).

Anta att följande DDX-dokument används för den här diskussionen.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

I det här DDX-dokumentet `DocumentInformation` -elementet instruerar Assembler-tjänsten att returnera information om indatadokumentet i PDF. I `DocumentInformation` -element, `PDFAValidation` -elementet instruerar Assembler-tjänsten att ange om det inmatade PDF-dokumentet är PDF/A-kompatibelt.

Assembler-tjänsten returnerar information som anger om det inmatade PDF-dokumentet är PDF/A-kompatibelt i ett XML-dokument som innehåller en `PDFAConformance` -element. Om det inmatade PDF-dokumentet är PDF/A-kompatibelt är värdet för `PDFAConformance` element `isCompliant` attributet är `true`. Om PDF-dokumentet inte är PDF/A-kompatibelt är värdet för `PDFAConformance` element `isCompliant` attributet är `false`.

>[!NOTE]
>
>Eftersom DDX-dokumentet som anges i det här avsnittet innehåller en `DocumentInformation` -element returnerar Assembler-tjänsten XML-data i stället för ett PDF-dokument. Det vill säga att Assembler-tjänsten inte sammanställer eller disassemblerar ett PDF-dokument. returnerar information om indatadokumentet i PDF i ett XML-dokument.

>[!NOTE]
>
>Mer information om Assembler-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Sammanfattning av steg {#summary-of-steps}

Så här avgör du om ett PDF-dokument är PDF/A-kompatibelt:

1. Inkludera projektfiler.
1. Skapa en PDF Assembler-klient.
1. Referera till ett befintligt DDX-dokument.
1. Referera till ett PDF-dokument som används för att fastställa kompatibiliteten mellan PDF och A.
1. Ange körningsalternativ.
1. Hämta information om PDF-dokumentet.
1. Spara det returnerade XML-dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

Om AEM Forms körs på en annan J2EE-programserver än JBoss måste du ersätta filerna adobe-utilities.jar och jbossall-client.jar med JAR-filer som är specifika för J2EE-programservern som AEM Forms är distribuerad på. Information om platsen för alla AEM Forms JAR-filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Skapa en PDF Assembler-klient**

Innan du programmässigt kan utföra en Assembler-åtgärd måste du skapa en Assembler-tjänstklient.

**Referera till ett befintligt DDX-dokument**

Det måste finnas referenser till ett DDX-dokument för att en Assembler-tjänståtgärd ska kunna utföras. För att avgöra om ett inmatningsdokument är PDF/A-kompatibelt kontrollerar du att DDX-dokumentet innehåller `PDFAValidation` element i en `DocumentInformation` -element. The `PDFAValidation` -elementet instruerar Assembler-tjänsten att returnera ett XML-dokument som anger om det inmatade PDF-dokumentet är PDF/A-kompatibelt.

**Referera till ett PDF-dokument som används för att fastställa kompatibiliteten mellan PDF och A**

Ett PDF-dokument måste refereras och skickas till Assembler-tjänsten för att avgöra om PDF-dokumentet är PDF/A-kompatibelt.

**Ange körningsalternativ**

Du kan ställa in körningsalternativ som styr beteendet för Assembler-tjänsten när den utför ett jobb. Du kan till exempel ange ett alternativ som instruerar Assembler-tjänsten att fortsätta bearbeta ett jobb om ett fel uppstår. Mer information om de körningsalternativ du kan ange finns i `AssemblerOptionSpec` klassreferens i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Hämta information om PDF-dokumentet**

När du har skapat Assembler-tjänstklienten, refererat till DDX-dokumentet, refererat till ett interaktivt PDF-dokument och angett körningsalternativ, kan du anropa `invokeDDX` operation. Eftersom DDX-dokumentet innehåller `DocumentInformation` -element returnerar Assembler-tjänsten XML-data i stället för ett PDF-dokument.

**Spara det returnerade XML-dokumentet**

Det XML-dokument som Assembler-tjänsten returnerar anger om det inmatade PDF-dokumentet är PDF/A-kompatibelt. Om indatadokumentet PDF inte är PDF/A-kompatibelt returnerar Assembler-tjänsten ett XML-dokument som innehåller följande element:

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

Spara XML-dokumentet som en XML-fil så att du kan öppna filen och visa resultatet.

**Se även**

[Kontrollera om ett dokument är PDF/A-kompatibelt med Java API](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Kontrollera om ett dokument är PDF/A-kompatibelt med webbtjänstens API](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Kontrollera om ett dokument är PDF/A-kompatibelt med Java API {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Kontrollera om ett PDF-dokument är PDF/A-kompatibelt med hjälp av Assembler Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en PDF Assembler-klient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `AssemblerServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Referera till ett befintligt DDX-dokument.

   * Skapa en `java.io.FileInputStream` som representerar DDX-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för DDX-filen. Kontrollera att DDX-dokumentet innehåller `PDFAValidation` element som finns i en `DocumentInformation` -element.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Referera till ett PDF-dokument som används för att fastställa kompatibiliteten mellan PDF och A.

   * Skapa en `java.io.FileInputStream` genom att använda dess konstruktor och skicka platsen för ett PDF-dokument som används för att fastställa kompatibiliteten PDF/A.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` som innehåller dokumentet PDF.
   * Skapa en `java.util.Map` objekt som används för att lagra indata-PDF-dokumentet med hjälp av ett `HashMap` konstruktor.
   * Lägg till en post i `java.util.Map` genom att anropa dess `put` och skicka följande argument:

      * Ett strängvärde som representerar nyckelnamnet. Detta värde måste matcha värdet för källelementet som anges i DDX-dokumentet. Värdet för källelementet i DDX-dokumentet som introducerades i det här avsnittet är till exempel Loan.pdf.
      * A `com.adobe.idp.Document` som innehåller indatadokumentet PDF.

1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärsbehov genom att anropa en metod som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera tjänsten Assembler att fortsätta bearbeta ett jobb när ett fel inträffar, ska du anropa `AssemblerOptionSpec` objektets `setFailOnError` metod och skicka `false`.

1. Hämta information om PDF-dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` och skicka följande obligatoriska värden:

   * A `com.adobe.idp.Document` objekt som representerar det DDX-dokument som ska användas
   * A `java.util.Map` objekt som innehåller indatafilen för PDF som används för att fastställa kompatibiliteten för PDF/A
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objekt som anger körningsalternativ

   The `invokeDDX` returnerar en `com.adobe.livecycle.assembler.client.AssemblerResult` -objekt som innehåller XML-data som anger om PDF-indatadokumentet är PDF/A-kompatibelt.

1. Spara det returnerade XML-dokumentet.

   Gör så här för att hämta XML-data som anger om indata-PDF-dokumentet är ett PDF/A-dokument:

   * Anropa `AssemblerResult` objektets `getDocuments` -metod. Detta returnerar `java.util.Map` -objekt.
   * Iterera genom `java.util.Map` tills du hittar resultatet `com.adobe.idp.Document` -objekt.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att extrahera XML-dokumentet. Se till att du sparar XML-data som en XML-fil.

**Se även**

[Snabbstart (SOAP-läge): Kontrollera om ett dokument är PDF/A-kompatibelt med Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) (SOAP-läge)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Kontrollera om ett dokument är PDF/A-kompatibelt med webbtjänstens API {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Kontrollera om ett PDF-dokument är PDF/A-kompatibelt med Assembler Service API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server som är värd för AEM Forms.

1. Skapa en PDF Assembler-klient.

   * Skapa en `AssemblerServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `AssemblerServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Du behöver inte använda `lc_version` -attribut. Det här attributet används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `AssemblerServiceClient.Endpoint.Binding` fält. Sänd returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Referera till ett befintligt DDX-dokument.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra DDX-dokumentet.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för DDX-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Referera till ett PDF-dokument som används för att fastställa kompatibiliteten mellan PDF och A.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra indatadokumentet i PDF.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för indata-PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` med bytearrayens innehåll.
   * Skapa en `MyMapOf_xsd_string_To_xsd_anyType` -objekt. Samlingsobjektet används för att lagra dokumentet PDF.
   * Skapa en `MyMapOf_xsd_string_To_xsd_anyType_Item` -objekt.
   * Tilldela ett strängvärde som representerar nyckelnamnet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `key` fält. Detta värde måste matcha värdet för källelementet PDF som anges i DDX-dokumentet.
   * Tilldela `BLOB` objekt som lagrar PDF-dokumentet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `value` fält.
   * Lägg till `MyMapOf_xsd_string_To_xsd_anyType_Item` objekt till `MyMapOf_xsd_string_To_xsd_anyType` -objekt. Anropa `MyMapOf_xsd_string_To_xsd_anyType` object&#39; `Add` och skicka `MyMapOf_xsd_string_To_xsd_anyType` -objekt.

1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärskrav genom att tilldela ett värde till en datamedlem som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar tilldelar du `false` till `AssemblerOptionSpec` objektets `failOnError` datamedlem.

1. Hämta information om PDF-dokumentet.

   Anropa `AssemblerServiceService` objektets `invoke` och skicka följande värden:

   * A `BLOB` -objekt som representerar DDX-dokumentet.
   * The `MyMapOf_xsd_string_To_xsd_anyType` som innehåller indatadokumentet PDF. Dess nycklar måste matcha PDF källfilernas namn och dess värden måste vara `BLOB` objekt som motsvarar indatafilen för PDF.
   * An `AssemblerOptionSpec` objekt som anger körningsalternativ.

   The `invoke` returnerar en `AssemblerResult` -objekt som innehåller XML-data som anger om PDF-indatadokumentet är ett PDF/A-dokument.

1. Spara det returnerade XML-dokumentet.

   Gör så här för att hämta XML-data som anger om indata-PDF-dokumentet är ett PDF/A-dokument:

   * Öppna `AssemblerResult` objektets `documents` fält, vilket är ett `Map` -objekt som innehåller XML-data som anger om PDF-indatadokumentet är ett PDF/A-dokument.
   * Iterera genom `Map` -objekt för att hämta varje resulterande dokument. Sedan konverterar du den arraymedlemmens värde till en `BLOB`.
   * Extrahera de binära data som representerar XML-data genom att använda dess `BLOB` objektets `MTOM` fält. I det här fältet lagras en array med byte som du kan skriva till som en XML-fil.

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
