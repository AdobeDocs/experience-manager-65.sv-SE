---
title: Skapa DDX-dokument dynamiskt
seo-title: Skapa DDX-dokument dynamiskt
description: 'null'
seo-description: 'null'
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Skapa DDX-dokument dynamiskt {#dynamically-creating-ddx-documents}

Du kan dynamiskt skapa ett DX-dokument som kan användas för att utföra en Assembler-åtgärd. När du dynamiskt skapar ett DX-dokument kan du använda värden i DDX-dokumentet som hämtas under körning. Om du vill skapa ett DDX-dokument dynamiskt använder du klasser som tillhör det programmeringsspråk som du använder. Om du till exempel utvecklar ditt klientprogram med Java ska du använda klasser som tillhör `org.w3c.dom.*`paketet. Om du använder Microsoft .NET ska du också använda klasser som tillhör `System.Xml` namnutrymmet.

Innan du kan skicka DDX-dokumentet till Assembler-tjänsten måste du konvertera XML-filen från en `org.w3c.dom.Document` instans till en `com.adobe.idp.Document` instans. Om du använder webbtjänster konverterar du XML från den datatyp som används för att skapa XML (till exempel `XmlDocument`) till en `BLOB` instans.

Anta att följande DDX-dokument skapas dynamiskt för den här diskussionen.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Det här DDX-dokumentet demonterar ett PDF-dokument. Vi rekommenderar att du är bekant med att dela upp PDF-dokument.

>[!NOTE]
>
>Mer information om tjänsten Assembler finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DDX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Sammanfattning av steg {#summary-of-steps}

Gör så här om du vill dela upp ett PDF-dokument med ett dynamiskt skapat DDX-dokument:

1. Inkludera projektfiler.
1. Skapa en PDF Assembler-klient.
1. Skapa DDX-dokumentet.
1. Konvertera DDX-dokumentet.
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

**Skapa en PDF Assembler-klient**

Skapa en Assembler-tjänstklient innan du programmässigt utför en Assembler-åtgärd.

**Skapa DDX-dokumentet**

Skapa ett DX-dokument med det programmeringsspråk som du använder. Om du vill skapa ett DX-dokument som demonterar ett PDF-dokument måste du se till att det innehåller `PDFsFromBookmarks` elementet. Konvertera den datatyp som används för att skapa DDX-dokumentet till en `com.adobe.idp.Document` instans om du använder Java API. Om du använder webbtjänster konverterar du datatypen till en `BLOB` instans.

**Konvertera DDX-dokumentet**

Ett DDX-dokument som skapas med hjälp av `org.w3c.dom` klasser måste konverteras till ett `com.adobe.idp.Document` objekt. Om du vill utföra den här åtgärden när du använder Java API ska du använda Java XML-omformningsklasser. Om du använder webbtjänster konverterar du DDX-dokumentet till ett `BLOB` objekt.

**Referera ett PDF-dokument som ska demonteras**

Om du vill demontera ett PDF-dokument refererar du till en PDF-fil som representerar det PDF-dokument som ska demonteras. När det skickas till Assembler-tjänsten returneras ett separat PDF-dokument för varje nivå 1-bokmärke i dokumentet.

**Ange körningsalternativ**

Du kan ställa in körningsalternativ som styr beteendet för Assembler-tjänsten när den utför ett jobb. Du kan till exempel ange ett alternativ som instruerar Assembler-tjänsten att fortsätta bearbeta ett jobb om ett fel uppstår. Om du vill ange körningsalternativ använder du ett `AssemblerOptionSpec` objekt.

**Dela upp PDF-dokumentet**

Disassemblera PDF-dokumentet genom att anropa `invokeDDX` åtgärden. Skicka DDX-dokumentet som skapades dynamiskt. Assembler-tjänsten returnerar omonterade PDF-dokument i ett samlingsobjekt.

**Spara de upplösta PDF-dokumenten**

Alla uppdelade PDF-dokument returneras inom ett samlingsobjekt. Upprepa genom samlingsobjektet och spara varje PDF-dokument som en PDF-fil.

**Se även**

[Skapa ett DDX-dokument dynamiskt med Java API](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Skapa ett DX-dokument dynamiskt med webbtjänstens API](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Dela upp PDF-dokument programmatiskt](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Skapa ett DDX-dokument dynamiskt med Java API {#dynamically-create-a-ddx-document-using-the-java-api}

Skapa ett DX-dokument dynamiskt och demontera ett PDF-dokument med Assembler Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en PDF Assembler-klient.

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa ett `AssemblerServiceClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.

1. Skapa DDX-dokumentet.

   * Skapa ett Java- `DocumentBuilderFactory` objekt genom att anropa `DocumentBuilderFactory` klassens `newInstance` metod.
   * Skapa ett Java- `DocumentBuilder` objekt genom att anropa `DocumentBuilderFactory` objektets `newDocumentBuilder` metod.
   * Anropa `DocumentBuilder` objektets `newDocument` metod för att instansiera ett `org.w3c.dom.Document` objekt.
   * Skapa DX-dokumentets rotelement genom att anropa `org.w3c.dom.Document` objektets `createElement` metod. Den här metoden skapar ett `Element` objekt som representerar rotelementet. Skicka ett strängvärde som representerar elementets namn till `createElement` metoden. Sänd returvärdet till `Element`. Sedan anger du ett värde för det underordnade elementet genom att anropa dess `setAttribute` metod. Lägg slutligen till elementet i rubrikelementet genom att anropa rubrikelementets `appendChild` metod och skicka det underordnade elementobjektet som ett argument. Följande kodrader visar den här programlogiken:
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Skapa `PDFsFromBookmarks` elementet genom att anropa `Document` objektets `createElement` metod. Skicka ett strängvärde som representerar elementets namn till `createElement` metoden. Sänd returvärdet till `Element`. Ange ett värde för `PDFsFromBookmarks` elementet genom att anropa dess `setAttribute` metod. Lägg till elementet `PDFsFromBookmarks` i `DDX` elementet genom att anropa DDX-elementets `appendChild` metod. Skicka elementobjektet `PDFsFromBookmarks` som ett argument. Följande kodrader visar den här programlogiken:

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Skapa ett `PDF` element genom att anropa `Document` objektets `createElement` metod. Skicka ett strängvärde som representerar elementets namn. Sänd returvärdet till `Element`. Ange ett värde för `PDF` elementet genom att anropa dess `setAttribute` metod. Lägg till `PDF` elementet i `PDFsFromBookmarks` elementet genom att anropa `PDFsFromBookmarks` elementets `appendChild` metod. Skicka elementobjektet `PDF` som ett argument. Följande kodrader visar programlogiken:

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Konvertera DDX-dokumentet.

   * Skapa ett `javax.xml.transform.Transformer` objekt genom att anropa `javax.xml.transform.Transformer` objektets statiska `newInstance` metod.
   * Skapa ett `Transformer` objekt genom att anropa `TransformerFactory` objektets `newTransformer` metod.
   * Skapa ett `ByteArrayOutputStream` objekt med hjälp av dess konstruktor.
   * Skapa ett `javax.xml.transform.dom.DOMSource` objekt med hjälp av dess konstruktor. Skicka det `org.w3c.dom.Document` objekt som representerar DDX-dokumentet.
   * Skapa ett `javax.xml.transform.dom.DOMSource` objekt med hjälp av dess konstruktor och skicka `ByteArrayOutputStream` objektet.
   * Fyll i Java- `ByteArrayOutputStream` objektet genom att anropa `javax.xml.transform.Transformer` objektets `transform` metod. Skicka `javax.xml.transform.dom.DOMSource` och `javax.xml.transform.stream.StreamResult` objekten.
   * Skapa en bytearray och tilldela storleken på `ByteArrayOutputStream` objektet till bytearrayen.
   * Fyll i bytearrayen genom att anropa `ByteArrayOutputStream` objektets `toByteArray` metod.
   * Skapa ett `com.adobe.idp.Document` objekt med hjälp av dess konstruktor och skicka bytearrayen.

1. Referera till ett PDF-dokument som ska demonteras.

   * Skapa ett `java.util.Map` objekt som används för att lagra PDF-indatadokument med hjälp av en `HashMap` konstruktor.
   * Skapa ett `java.io.FileInputStream` objekt med hjälp av dess konstruktor och skicka platsen för det PDF-dokument som ska demonteras.
   * Create a `com.adobe.idp.Document` object. Skicka det `java.io.FileInputStream` objekt som innehåller PDF-dokumentet som ska demonteras.
   * Lägg till en post i `java.util.Map` objektet genom att anropa dess `put` metod och skicka följande argument:

      * Ett strängvärde som representerar nyckelnamnet. Detta värde måste matcha värdet för PDF-källelementet som anges i DDX-dokumentet. (I DDX-dokumentet som skapas dynamiskt är värdet `AssemblerResultPDF.pdf`.)
      * Ett `com.adobe.idp.Document` objekt som innehåller det PDF-dokument som ska demonteras.

1. Ange körningsalternativ.

   * Skapa ett `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärsbehov genom att anropa en metod som tillhör `AssemblerOptionSpec` objektet. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar, anropar du `AssemblerOptionSpec` objektets `setFailOnError` metod och skickar `false`.

1. Disassemblera PDF-dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` metod och skicka följande värden:

   * Ett `com.adobe.idp.Document` objekt som representerar det dynamiskt skapade DDX-dokumentet
   * Ett `java.util.Map` objekt som innehåller det PDF-dokument som ska demonteras
   * Ett `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objekt som anger körningsalternativen, inklusive standardteckensnittet och jobbloggsnivån
   Metoden returnerar `invokeDDX` ett `com.adobe.livecycle.assembler.client.AssemblerResult` objekt som innehåller de uppdelade PDF-dokumenten och eventuella undantag som har inträffat.

1. Spara de upplösta PDF-dokumenten.

   Gör så här för att få fram de uppdelade PDF-dokumenten:

   * Anropa `AssemblerResult` objektets `getDocuments` metod. Den här metoden returnerar ett `java.util.Map` objekt.
   * Upprepa genom `java.util.Map` objektet tills du hittar det resulterande `com.adobe.idp.Document` objektet.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att extrahera PDF-dokumentet.

**Se även**

[Snabbstart (SOAP-läge): Skapa ett DDX-dokument dynamiskt med Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Skapa ett DX-dokument dynamiskt med webbtjänstens API {#dynamically-create-a-ddx-document-using-the-web-service-api}

Skapa ett DX-dokument dynamiskt och demontera ett PDF-dokument med Assembler Service API (webbtjänst):

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

1. Skapa DDX-dokumentet.

   * Skapa ett `System.Xml.XmlElement` objekt med hjälp av dess konstruktor.
   * Skapa DX-dokumentets rotelement genom att anropa `XmlElement` objektets `CreateElement` metod. Den här metoden skapar ett `Element` objekt som representerar rotelementet. Skicka ett strängvärde som representerar elementets namn till `CreateElement` metoden. Ange ett värde för DDX-elementet genom att anropa dess `SetAttribute` metod. Lägg slutligen till elementet i DDX-dokumentet genom att anropa `XmlElement` objektets `AppendChild` metod. Skicka DDX-objektet som ett argument. Följande kodrader visar den här programlogiken:

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Skapa DX-dokumentets `PDFsFromBookmarks` -element genom att anropa `XmlElement` objektets `CreateElement` metod. Skicka ett strängvärde som representerar elementets namn till `CreateElement` metoden. Ange sedan ett värde för elementet genom att anropa dess `SetAttribute` metod. Lägg till elementet `PDFsFromBookmarks` i rotelementet genom att anropa `DDX` elementets `AppendChild` metod. Skicka elementobjektet `PDFsFromBookmarks` som ett argument. Följande kodrader visar den här programlogiken:

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Skapa DX-dokumentets `PDF` -element genom att anropa `XmlElement` objektets `CreateElement` metod. Skicka ett strängvärde som representerar elementets namn till `CreateElement` metoden. Sedan anger du ett värde för det underordnade elementet genom att anropa dess `SetAttribute` metod. Lägg till `PDF` elementet i `PDFsFromBookmarks` elementet genom att anropa `PDFsFromBookmarks` elementets `AppendChild` metod. Skicka elementobjektet `PDF` som ett argument. Följande kodrader visar programlogiken:

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Konvertera DDX-dokumentet.

   * Skapa ett `System.IO.MemoryStream` objekt med hjälp av dess konstruktor.
   * Fyll objektet `MemoryStream` med DDX-dokumentet med hjälp av det `XmlElement` objekt som representerar DDX-dokumentet. Anropa `XmlElement` objektets `Save` metod och skicka `MemoryStream` objektet.
   * Skapa en bytearray och fyll i den med data som finns i `MemoryStream` objektet. I följande kod visas den här programlogiken:

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Create a `BLOB` object. Tilldela bytearrayen till `BLOB` objektets `MTOM` fält.

1. Referera till ett PDF-dokument som ska demonteras.

   * Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Objektet används `BLOB` för att lagra PDF-indatadokumentet. Detta `BLOB` objekt skickas till `invokeOneDocument` som ett argument.
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för PDF-indatadokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod och skicka bytearrayen, startpositionen och den strömlängd som ska läsas.
   * Fylla i objektet genom att tilldela dess `BLOB` `MTOM` egenskap innehållet i bytearrayen.

1. Ange körningsalternativ.

   * Skapa ett `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärskrav genom att tilldela ett värde till en datamedlem som tillhör `AssemblerOptionSpec` objektet. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar tilldelar du `false` till `AssemblerOptionSpec` objektets `failOnError` datamedlem.

1. Disassemblera PDF-dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` metod och skicka följande värden:

   * Ett `BLOB` objekt som representerar det dynamiskt skapade DDX-dokumentet
   * Arrayen `mapItem` som innehåller PDF-indatadokumentet
   * Ett `AssemblerOptionSpec` objekt som anger körningsalternativ
   Metoden returnerar ett `invokeDDX` `AssemblerResult` objekt som innehåller resultatet av jobbet och eventuella undantag som inträffade.

1. Spara de upplösta PDF-dokumenten.

   Utför följande åtgärder för att hämta de nya PDF-dokumenten:

   * Få åtkomst till `AssemblerResult` objektets `documents` fält, som är ett `Map` objekt som innehåller de uppdelade PDF-dokumenten.
   * Iterera genom objektet `Map` för att få fram varje resulterande dokument. Sedan konverterar du arraymedlemmens `value` till en `BLOB`.
   * Extrahera de binära data som representerar PDF-dokumentet genom att få åtkomst till dess `BLOB` objektegenskap `MTOM` . Detta returnerar en array med byte som du kan skriva till en PDF-fil.

**Se även**

[Anropa AEM-formulär med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM-formulär med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
