---
title: Dela upp PDF-dokument programmatiskt
seo-title: Programmatically Disassembling PDF Documents
description: Använd Assembler-tjänsten för att dela upp ett enda PDF-dokument till flera PDF-dokument med Java API och Web Service API.
seo-description: Use the Assembler service to disassemble a single PDF document into multiple PDF documents using the Java API and the Web Service API.
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
role: Developer
exl-id: c5e712e0-5c3f-48cd-91cf-fd347222a6b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 0%

---

# Dela upp PDF-dokument programmatiskt {#programmatically-disassembling-pdf-documents}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

Du kan dela upp ett PDF-dokument genom att skicka det till Assembler-tjänsten. Vanligtvis är den här uppgiften användbar när PDF-dokumentet ursprungligen skapades från många enskilda dokument, till exempel en samling programsatser. På följande bild delas DocA in i flera resulterande dokument, där det första bokmärket på nivå 1 på en sida anger början på ett nytt resulterande dokument.

![pd_pd_pdfsfrombokmärken](assets/pd_pd_pdfsfrombookmarks.png)

Om du vill dela upp ett PDF-dokument måste du se till att `PDFsFromBookmarks` -elementet finns i DDX-dokumentet. The `PDFsFromBookmarks` -elementet är ett resultatelement och kan bara vara ett underordnat element till `DDX` -element. Den har ingen `result` eftersom det kan leda till att flera dokument genereras.

The `PDFsFromBookmarks` gör att ett dokument genereras för varje nivå 1-bokmärke i källdokumentet.

Anta att följande DDX-dokument används för den här diskussionen.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>Innan du läser det här avsnittet bör du känna till hur du sammanställer PDF-dokument med hjälp av tjänsten Assembler. (Se [Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>När du skickar ett enda PDF-dokument till Assembler-tjänsten och återgår till ett enda dokument kan du anropa `invokeOneDocument` operation. Om du vill dela upp ett PDF-dokument använder du `invokeDDX` eftersom även om ett indatadokument i PDF skickas till Assembler-tjänsten returnerar Assembler-tjänsten ett samlingsobjekt som innehåller ett eller flera dokument.

>[!NOTE]
>
>Mer information om Assembler-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Sammanfattning av steg {#summary-of-steps}

Gör så här om du vill dela upp ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en PDF Assembler-klient.
1. Referera till ett befintligt DDX-dokument.
1. Referera ett PDF-dokument som ska demonteras.
1. Ange körningsalternativ.
1. Dela upp PDF-dokumentet.
1. Spara de upplösta PDF-dokumenten.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

Om AEM Forms körs på en J2EE-programserver som stöds och som inte är JBoss, måste du ersätta adobe-utilities.jar och jbossall-client.jar med JAR-filer som är specifika för J2EE-programservern som AEM Forms är distribuerad på.

**Skapa en PDF Assembler-klient**

Innan du programmässigt kan utföra en Assembler-åtgärd måste du skapa en Assembler-tjänstklient.

**Referera till ett befintligt DDX-dokument**

Det måste finnas en referens till ett DDX-dokument för att du ska kunna dela upp ett PDF-dokument. Det här DDX-dokumentet måste innehålla `PDFsFromBookmarks` -element.

**Referera ett PDF-dokument som ska demonteras**

Om du vill dela upp ett PDF-dokument refererar du till en PDF-fil som representerar det PDF-dokument som ska demonteras. När det skickas till Assembler-tjänsten returneras ett separat PDF-dokument för varje nivå 1-bokmärke i dokumentet.

**Ange körningsalternativ**

Du kan ställa in körningsalternativ som styr beteendet för Assembler-tjänsten när den utför ett jobb. Du kan till exempel ange ett alternativ som instruerar Assembler-tjänsten att fortsätta bearbeta ett jobb om ett fel uppstår.

**Dela upp PDF-dokumentet**

När du har skapat Assembler-tjänstklienten, refererat till DDX-dokumentet, refererat till ett PDF-dokument som ska demonteras och angett körningsalternativ, kan du demontera ett PDF-dokument genom att anropa `invokeDDX` -metod. Under förutsättning att DDX-dokumentet innehåller instruktioner för att demontera PDF returnerar Assembler-tjänsten omonterade PDF-dokument i ett samlingsobjekt.

**Spara de upplösta PDF-dokumenten**

Alla uppdelade PDF-dokument returneras inom ett samlingsobjekt. Iterera genom samlingsobjektet och spara varje PDF-dokument som en PDF-fil.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Dela upp ett PDF-dokument med Java API {#disassemble-a-pdf-document-using-the-java-api}

Dela upp ett PDF-dokument med Assembler Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en PDF Assembler-klient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `AssemblerServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Referera till ett befintligt DDX-dokument.

   * Skapa en `java.io.FileInputStream` som representerar DDX-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för DDX-filen.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Referera ett PDF-dokument som ska demonteras.

   * Skapa en `java.util.Map` objekt som används för att lagra indatadokument i PDF genom att använda en `HashMap` konstruktor.
   * Skapa en `java.io.FileInputStream` genom att använda konstruktorn och skicka platsen för det PDF-dokument som ska demonteras.
   * Skapa en `com.adobe.idp.Document` -objektet och skicka `java.io.FileInputStream` objekt som innehåller det PDF-dokument som ska demonteras.
   * Lägg till en post i `java.util.Map` genom att anropa dess `put` och skicka följande argument:

      * Ett strängvärde som representerar nyckelnamnet. Detta värde måste matcha värdet för källelementet PDF som anges i DDX-dokumentet.
      * A `com.adobe.idp.Document` objekt som innehåller det PDF-dokument som ska demonteras.

1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärsbehov genom att anropa en metod som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera tjänsten Assembler att fortsätta bearbeta ett jobb när ett fel inträffar, ska du anropa `AssemblerOptionSpec` objektets `setFailOnError` metod och skicka `false`.

1. Dela upp PDF-dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` och skicka följande obligatoriska värden:

   * A `com.adobe.idp.Document` objekt som representerar det DDX-dokument som ska användas
   * A `java.util.Map` objekt som innehåller det PDF-dokument som ska demonteras
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objekt som anger körningsalternativen, inklusive standardteckensnitt och jobbloggsnivå

   The `invokeDDX` returnerar en `com.adobe.livecycle.assembler.client.AssemblerResult` objekt som innehåller de uppdelade PDF-dokumenten och eventuella undantag som inträffat.

1. Spara de upplösta PDF-dokumenten.

   Gör så här för att få fram de uppdelade PDF-dokumenten:

   * Anropa `AssemblerResult` objektets `getDocuments` -metod. Detta returnerar `java.util.Map` -objekt.
   * Iterera genom `java.util.Map` tills du hittar resultatet `com.adobe.idp.Document` -objekt.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att extrahera PDF-dokumentet.

**Se även**

[Dela upp PDF-dokument programmatiskt](#programmatically-disassembling-pdf-documents)

[Snabbstart (SOAP-läge): Dela upp ett PDF-dokument med Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Dela upp ett PDF-dokument med hjälp av webbtjänstens API {#disassemble-a-pdf-document-using-the-web-service-api}

Dela upp ett PDF-dokument med Assembler Service API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition när du anger en tjänstreferens: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server som är värd för AEM Forms.

1. Skapa en PDF Assembler-klient.

   * Skapa en `AssemblerServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `AssemblerServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Du behöver inte använda `lc_version` -attribut. Det här attributet används när du skapar en tjänstreferens.
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `AssemblerServiceClient.Endpoint.Binding` fält. Sänd returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Referera till ett befintligt DDX-dokument.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra DDX-dokumentet.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för DDX-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` med bytearrayens innehåll.

1. Referera ett PDF-dokument som ska demonteras.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra indatadokumentet i PDF. Detta `BLOB` objektet skickas till `invokeOneDocument` som ett argument.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för indata-PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält innehållet i bytearrayen.
   * Skapa en `MyMapOf_xsd_string_To_xsd_anyType` -objekt. Samlingsobjektet används för att lagra PDF som ska demonteras.
   * Skapa en `MyMapOf_xsd_string_To_xsd_anyType_Item` -objekt.
   * Tilldela ett strängvärde som representerar nyckelnamnet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `key` fält. Detta värde måste matcha värdet för källelementet PDF som anges i DDX-dokumentet.
   * Tilldela `BLOB` objekt som lagrar PDF-dokumentet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `value` fält.
   * Lägg till `MyMapOf_xsd_string_To_xsd_anyType_Item` objekt till `MyMapOf_xsd_string_To_xsd_anyType` -objekt. Anropa `MyMapOf_xsd_string_To_xsd_anyType` object&quot; `Add` och skicka `MyMapOf_xsd_string_To_xsd_anyType` -objekt.

1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärskrav genom att tilldela ett värde till en datamedlem som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar tilldelar du `false` till `AssemblerOptionSpec` objektets `failOnError` fält.

1. Dela upp PDF-dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` och skicka följande värden:

   * A `BLOB` det objekt som representerar DDX-dokumentet som demonterar PDF-dokumentet
   * The `MyMapOf_xsd_string_To_xsd_anyType` objekt som innehåller det PDF-dokument som ska demonteras
   * An `AssemblerOptionSpec` objekt som anger körningsalternativ

   The `invokeDDX` returnerar en `AssemblerResult` objekt som innehåller jobbresultaten och eventuella undantag som inträffade.

1. Spara de upplösta PDF-dokumenten.

   Gör så här för att hämta de nya PDF-dokumenten:

   * Öppna `AssemblerResult` objektets `documents` fält, vilket är ett `Map` objekt som innehåller de uppdelade PDF-dokumenten.
   * Iterera genom `Map` -objekt för att hämta varje resulterande dokument. Sedan måste du byta ut den arraymedlemmens `value` till `BLOB`.
   * Extrahera de binära data som representerar PDF-dokumentet genom att öppna dess `BLOB` objektets `MTOM` -egenskap. Detta returnerar en array med byte som du kan skriva ut till en PDF-fil.

**Se även**

[Dela upp PDF-dokument programmatiskt](#programmatically-disassembling-pdf-documents)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
