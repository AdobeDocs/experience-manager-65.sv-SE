---
title: Dela upp PDF-dokument programmatiskt
seo-title: Dela upp PDF-dokument programmatiskt
description: 'null'
seo-description: 'null'
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Dela upp PDF-dokument programmatiskt {#programmatically-disassembling-pdf-documents}

Du kan demontera ett PDF-dokument genom att skicka det till Assembler-tjänsten. Vanligtvis är den här uppgiften användbar när PDF-dokumentet ursprungligen skapades från många enskilda dokument, till exempel en samling programsatser. På följande bild delas DocA in i flera resulterande dokument, där det första bokmärket på nivå 1 på en sida anger början på ett nytt resulterande dokument.

![pd_pd_pdfsfrombokmärken](assets/pd_pd_pdfsfrombookmarks.png)

Om du vill demontera ett PDF-dokument kontrollerar du att `PDFsFromBookmarks` elementet finns i DDX-dokumentet. Elementet `PDFsFromBookmarks` är ett resultatelement och kan bara vara ett underordnat element till `DDX` elementet. Den har inget `result` attribut eftersom den kan generera flera dokument.

Elementet `PDFsFromBookmarks` gör att ett dokument genereras för varje nivå 1-bokmärke i källdokumentet.

Anta att följande DDX-dokument används för den här diskussionen.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>Innan du läser det här avsnittet bör du känna till hur du sammanställer PDF-dokument med hjälp av tjänsten Assembler. (Se [Sammanställa PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)programmatiskt.)

>[!NOTE]
>
>När du skickar ett PDF-dokument till Assembler-tjänsten och återgår till ett enda dokument kan du aktivera `invokeOneDocument` åtgärden. Om du vill demontera ett PDF-dokument använder du `invokeDDX` åtgärden eftersom Assembler-tjänsten returnerar ett samlingsobjekt som innehåller ett eller flera dokument även om ett PDF-indatadokument skickas till Assembler-tjänsten.

>[!NOTE]
>
>Mer information om tjänsten Assembler finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DDX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Sammanfattning av steg {#summary-of-steps}

Gör så här för att dela upp ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en PDF Assembler-klient.
1. Referera till ett befintligt DDX-dokument.
1. Referera till ett PDF-dokument som ska demonteras.
1. Ange körningsalternativ.
1. Disassemblera PDF-dokumentet.
1. Spara de upplösta PDF-dokumenten.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (krävs om AEM Forms distribueras på JBoss)
* jbossall-client.jar (krävs om AEM Forms distribueras på JBoss)

Om AEM Forms används på en J2EE-programserver som inte är JBoss måste du ersätta adobe-utilities.jar och jbossall-client.jar med JAR-filer som är specifika för J2EE-programservern där AEM Forms används.

**Skapa en PDF Assembler-klient**

Innan du programmässigt kan utföra en Assembler-åtgärd måste du skapa en Assembler-tjänstklient.

**Referera till ett befintligt DDX-dokument**

Det måste finnas en referens till ett DX-dokument för att du ska kunna demontera ett PDF-dokument. Det här DDX-dokumentet måste innehålla `PDFsFromBookmarks` elementet.

**Referera ett PDF-dokument som ska demonteras**

Om du vill demontera ett PDF-dokument refererar du till en PDF-fil som representerar det PDF-dokument som ska demonteras. När det skickas till Assembler-tjänsten returneras ett separat PDF-dokument för varje nivå 1-bokmärke i dokumentet.

**Ange körningsalternativ**

Du kan ställa in körningsalternativ som styr beteendet för Assembler-tjänsten när den utför ett jobb. Du kan till exempel ange ett alternativ som instruerar Assembler-tjänsten att fortsätta bearbeta ett jobb om ett fel uppstår.

**Dela upp PDF-dokumentet**

När du har skapat Assembler-tjänstklienten, refererat till DDX-dokumentet, refererat till ett PDF-dokument som ska demonteras och angett körningsalternativ, kan du demontera ett PDF-dokument genom att anropa `invokeDDX` metoden. Förutsatt att DDX-dokumentet innehåller instruktioner för att demontera PDF-dokumentet returnerar Assembler-tjänsten omonterade PDF-dokument i ett samlingsobjekt.

**Spara de upplösta PDF-dokumenten**

Alla uppdelade PDF-dokument returneras inom ett samlingsobjekt. Upprepa genom samlingsobjektet och spara varje PDF-dokument som en PDF-fil.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Dela upp ett PDF-dokument med Java API {#disassemble-a-pdf-document-using-the-java-api}

Disassemble a PDF document by using the Assembler Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en PDF Assembler-klient.

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa ett `AssemblerServiceClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.

1. Referera till ett befintligt DDX-dokument.

   * Skapa ett `java.io.FileInputStream` objekt som representerar DDX-dokumentet med hjälp av dess konstruktor och skicka ett strängvärde som anger platsen för DDX-filen.
   * Skapa ett `com.adobe.idp.Document` objekt med hjälp av dess konstruktor och skicka `java.io.FileInputStream` objektet.

1. Referera till ett PDF-dokument som ska demonteras.

   * Skapa ett `java.util.Map` objekt som används för att lagra PDF-indatadokument med hjälp av en `HashMap` konstruktor.
   * Skapa ett `java.io.FileInputStream` objekt med hjälp av dess konstruktor och skicka platsen för det PDF-dokument som ska demonteras.
   * Skapa ett `com.adobe.idp.Document` objekt och skicka det `java.io.FileInputStream` objekt som innehåller det PDF-dokument som ska demonteras.
   * Lägg till en post i `java.util.Map` objektet genom att anropa dess `put` metod och skicka följande argument:

      * Ett strängvärde som representerar nyckelnamnet. Detta värde måste matcha värdet för PDF-källelementet som anges i DDX-dokumentet.
      * Ett `com.adobe.idp.Document` objekt som innehåller det PDF-dokument som ska demonteras.

1. Ange körningsalternativ.

   * Skapa ett `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärsbehov genom att anropa en metod som tillhör `AssemblerOptionSpec` objektet. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar, anropar du `AssemblerOptionSpec` objektets `setFailOnError` metod och skickar `false`.

1. Disassemblera PDF-dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` metod och skicka följande obligatoriska värden:

   * Ett `com.adobe.idp.Document` objekt som representerar det DDX-dokument som ska användas
   * Ett `java.util.Map` objekt som innehåller det PDF-dokument som ska demonteras
   * Ett `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objekt som anger körningsalternativen, inklusive standardteckensnittet och jobbloggsnivån
   Metoden returnerar `invokeDDX` ett `com.adobe.livecycle.assembler.client.AssemblerResult` objekt som innehåller de uppdelade PDF-dokumenten och eventuella undantag som har inträffat.

1. Spara de upplösta PDF-dokumenten.

   Gör så här för att få fram de uppdelade PDF-dokumenten:

   * Anropa `AssemblerResult` objektets `getDocuments` metod. Detta returnerar ett `java.util.Map` objekt.
   * Upprepa genom `java.util.Map` objektet tills du hittar det resulterande `com.adobe.idp.Document` objektet.
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
   >Ersätt `localhost` med IP-adressen för servern som är värd för AEM Forms.

1. Skapa en PDF Assembler-klient.

   * Skapa ett `AssemblerServiceClient` objekt med hjälp av dess standardkonstruktor.
   * Skapa ett `AssemblerServiceClient.Endpoint.Address` objekt med hjälp av `System.ServiceModel.EndpointAddress` konstruktorn. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Du behöver inte använda attributet `lc_version` . Det här attributet används när du skapar en tjänstreferens.
   * Skapa ett `System.ServiceModel.BasicHttpBinding` objekt genom att hämta värdet för `AssemblerServiceClient.Endpoint.Binding` fältet. Sänd returvärdet till `BasicHttpBinding`.
   * Ställ in `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela användarnamnet för AEM-formulär till fältet `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Referera till ett befintligt DDX-dokument.

   * Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Objektet används `BLOB` för att lagra DDX-dokumentet.
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för DDX-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod och skicka bytearrayen, startpositionen och den strömlängd som ska läsas.
   * Fyll objektet `BLOB` genom att tilldela dess `MTOM` egenskap med innehållet i bytearrayen.

1. Referera till ett PDF-dokument som ska demonteras.

   * Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Objektet används `BLOB` för att lagra PDF-indatadokumentet. Detta `BLOB` objekt skickas till `invokeOneDocument` som ett argument.
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar platsen för PDF-indatadokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod och skicka bytearrayen, startpositionen och den strömlängd som ska läsas.
   * Fyll i `BLOB` objektet genom att tilldela dess `MTOM` fält innehållet i bytearrayen.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Samlingsobjektet används för att lagra PDF-filen som ska demonteras.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * Tilldela ett strängvärde som representerar nyckelnamnet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `key` fält. Detta värde måste matcha värdet för PDF-källelementet som anges i DDX-dokumentet.
   * Tilldela det `BLOB` objekt som lagrar PDF-dokumentet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `value` fält.
   * Lägg till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektet i `MyMapOf_xsd_string_To_xsd_anyType` objektet. Anropa `MyMapOf_xsd_string_To_xsd_anyType` objektets `Add` metod och skicka `MyMapOf_xsd_string_To_xsd_anyType` objektet.

1. Ange körningsalternativ.

   * Skapa ett `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärskrav genom att tilldela ett värde till en datamedlem som tillhör `AssemblerOptionSpec` objektet. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar, tilldelar du `false` till `AssemblerOptionSpec` objektets `failOnError` fält.

1. Disassemblera PDF-dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` metod och skicka följande värden:

   * Ett `BLOB` objekt som representerar det DX-dokument som demonterar PDF-dokumentet
   * Det `MyMapOf_xsd_string_To_xsd_anyType` objekt som innehåller PDF-dokumentet som ska demonteras
   * Ett `AssemblerOptionSpec` objekt som anger körningsalternativ
   Metoden returnerar `invokeDDX` ett `AssemblerResult` objekt som innehåller jobbresultaten och eventuella undantag som har inträffat.

1. Spara de upplösta PDF-dokumenten.

   Utför följande åtgärder för att hämta de nya PDF-dokumenten:

   * Få åtkomst till `AssemblerResult` objektets `documents` fält, som är ett `Map` objekt som innehåller de uppdelade PDF-dokumenten.
   * Iterera genom objektet `Map` för att få fram varje resulterande dokument. Sedan konverterar du arraymedlemmens `value` till en `BLOB`.
   * Extrahera de binära data som representerar PDF-dokumentet genom att få åtkomst till dess `BLOB` objektegenskap `MTOM` . Detta returnerar en array med byte som du kan skriva till en PDF-fil.

**Se även**

[Dela upp PDF-dokument programmatiskt](#programmatically-disassembling-pdf-documents)

[Anropa AEM-formulär med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
