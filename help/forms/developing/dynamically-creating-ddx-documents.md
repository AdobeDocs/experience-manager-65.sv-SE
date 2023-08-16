---
title: Skapa DDX-dokument dynamiskt
seo-title: Dynamically Creating DDX Documents
description: Skapa ett DX-dokument dynamiskt med Java API och Web Service API. När du dynamiskt skapar ett DX-dokument kan du använda värden i DDX-dokumentet som hämtas under körning.
seo-description: Create a DDX document dynamically using the Java API and Web Service API. Dynamically creating a DDX document enables you to use values in the DDX document that are obtained during run-time.
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '2163'
ht-degree: 0%

---

# Skapa DDX-dokument dynamiskt {#dynamically-creating-ddx-documents}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

Du kan dynamiskt skapa ett DX-dokument som kan användas för att utföra en Assembler-åtgärd. När du dynamiskt skapar ett DX-dokument kan du använda värden i DDX-dokumentet som hämtas under körning. Om du vill skapa ett DDX-dokument dynamiskt använder du klasser som tillhör det programmeringsspråk som du använder. Om du till exempel utvecklar ditt klientprogram med Java använder du klasser som tillhör `org.w3c.dom.*`paket. Om du använder Microsoft .NET ska du också använda klasser som tillhör `System.Xml` namnutrymme.

Innan du kan skicka DDX-dokumentet till Assembler-tjänsten måste du konvertera XML-filen från en `org.w3c.dom.Document` instans till en `com.adobe.idp.Document` -instans. Om du använder webbtjänster konverterar du XML från den datatyp som används för att skapa XML (till exempel `XmlDocument`) till `BLOB` -instans.

Anta att följande DDX-dokument skapas dynamiskt för den här diskussionen.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Det här DDX-dokumentet demonterar ett PDF-dokument. Vi rekommenderar att du är bekant med att dela upp dokument i PDF.

>[!NOTE]
>
>Mer information om Assembler-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Sammanfattning av steg {#summary-of-steps}

Gör så här om du vill dela upp ett PDF-dokument med ett dynamiskt skapat DDX-dokument:

1. Inkludera projektfiler.
1. Skapa en PDF Assembler-klient.
1. Skapa DDX-dokumentet.
1. Konvertera DDX-dokumentet.
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

**Skapa en PDF Assembler-klient**

Skapa en Assembler-tjänstklient innan du programmässigt utför en Assembler-åtgärd.

**Skapa DDX-dokumentet**

Skapa ett DX-dokument med det programmeringsspråk som du använder. Om du vill skapa ett DDX-dokument som demonterar ett PDF-dokument måste du se till att det innehåller `PDFsFromBookmarks` -element. Konvertera den datatyp som används för att skapa DDX-dokumentet till en `com.adobe.idp.Document` -instans om du använder Java API. Om du använder webbtjänster konverterar du datatypen till `BLOB` -instans.

**Konvertera DDX-dokumentet**

Ett DX-dokument som skapas med `org.w3c.dom` måste konverteras till `com.adobe.idp.Document` -objekt. Om du vill utföra den här åtgärden när du använder Java API ska du använda Java XML-omformningsklasser. Om du använder webbtjänster konverterar du DDX-dokumentet till en `BLOB` -objekt.

**Referera ett PDF-dokument som ska demonteras**

Om du vill dela upp ett PDF-dokument refererar du till en PDF-fil som representerar det PDF-dokument som ska demonteras. När det skickas till Assembler-tjänsten returneras ett separat PDF-dokument för varje nivå 1-bokmärke i dokumentet.

**Ange körningsalternativ**

Du kan ställa in körningsalternativ som styr beteendet för Assembler-tjänsten när den utför ett jobb. Du kan till exempel ange ett alternativ som instruerar Assembler-tjänsten att fortsätta bearbeta ett jobb om ett fel uppstår. Om du vill ange körningsalternativ använder du en `AssemblerOptionSpec` -objekt.

**Dela upp PDF-dokumentet**

Dela upp PDF-dokumentet genom att anropa `invokeDDX` operation. Skicka DDX-dokumentet som skapades dynamiskt. Assembler-tjänsten returnerar uppdelade PDF-dokument i ett samlingsobjekt.

**Spara de upplösta PDF-dokumenten**

Alla uppdelade PDF-dokument returneras inom ett samlingsobjekt. Iterera genom samlingsobjektet och spara varje PDF-dokument som en PDF-fil.

**Se även**

[Skapa ett DDX-dokument dynamiskt med Java API](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Skapa ett DX-dokument dynamiskt med webbtjänstens API](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Dela upp PDF-dokument programmatiskt](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Skapa ett DDX-dokument dynamiskt med Java API {#dynamically-create-a-ddx-document-using-the-java-api}

Skapa ett DDX-dokument dynamiskt och demontera ett PDF-dokument med hjälp av Assembler Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en PDF Assembler-klient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `AssemblerServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Skapa DDX-dokumentet.

   * Skapa ett Java `DocumentBuilderFactory` genom att anropa `DocumentBuilderFactory` class&#39; `newInstance` -metod.
   * Skapa ett Java `DocumentBuilder` genom att anropa `DocumentBuilderFactory` objektets `newDocumentBuilder` -metod.
   * Ring `DocumentBuilder` objektets `newDocument` metod för att instansiera en `org.w3c.dom.Document` -objekt.
   * Skapa DX-dokumentets rotelement genom att anropa `org.w3c.dom.Document` objektets `createElement` -metod. Den här metoden skapar en `Element` som representerar rotelementet. Skicka ett strängvärde som representerar elementets namn till `createElement` -metod. Skicka returvärdet till `Element`. Ange sedan ett värde för det underordnade elementet genom att anropa dess `setAttribute` -metod. Slutligen lägger du till elementet i rubrikelementet genom att anropa rubrikelementets `appendChild` och skicka det underordnade elementobjektet som ett argument. Följande kodrader visar den här programlogiken:
     ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Skapa `PDFsFromBookmarks` genom att anropa `Document` objektets `createElement` -metod. Skicka ett strängvärde som representerar elementets namn till `createElement` -metod. Skicka returvärdet till `Element`. Ange ett värde för `PDFsFromBookmarks` element genom att anropa dess `setAttribute` -metod. Lägg till `PDFsFromBookmarks` -element till `DDX` genom att anropa DDX-elementets `appendChild` -metod. Skicka `PDFsFromBookmarks` elementobjekt som argument. Följande kodrader visar den här programlogiken:

     ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Skapa en `PDF` genom att anropa `Document` objektets `createElement` -metod. Skicka ett strängvärde som representerar elementets namn. Skicka returvärdet till `Element`. Ange ett värde för `PDF` element genom att anropa dess `setAttribute` -metod. Lägg till `PDF` -element till `PDFsFromBookmarks` genom att anropa `PDFsFromBookmarks` element `appendChild` -metod. Skicka `PDF` elementobjekt som argument. Följande kodrader visar den här programlogiken:

     ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Konvertera DDX-dokumentet.

   * Skapa en `javax.xml.transform.Transformer` genom att anropa `javax.xml.transform.Transformer` objektets statiska `newInstance` -metod.
   * Skapa en `Transformer` genom att anropa `TransformerFactory` objektets `newTransformer` -metod.
   * Skapa en `ByteArrayOutputStream` genom att använda dess konstruktor.
   * Skapa en `javax.xml.transform.dom.DOMSource` genom att använda dess konstruktor. Skicka `org.w3c.dom.Document` -objekt som representerar DDX-dokumentet.
   * Skapa en `javax.xml.transform.dom.DOMSource` genom att använda konstruktorn och skicka `ByteArrayOutputStream` -objekt.
   * Fyll i Java `ByteArrayOutputStream` genom att anropa `javax.xml.transform.Transformer` objektets `transform` -metod. Skicka `javax.xml.transform.dom.DOMSource` och `javax.xml.transform.stream.StreamResult` objekt.
   * Skapa en bytearray och tilldela storleken på `ByteArrayOutputStream` till bytearrayen.
   * Fylla i bytearrayen genom att anropa `ByteArrayOutputStream` objektets `toByteArray` -metod.
   * Skapa en `com.adobe.idp.Document` genom att använda dess konstruktor och skicka bytearrayen.

1. Referera ett PDF-dokument som ska demonteras.

   * Skapa en `java.util.Map` objekt som används för att lagra indatadokument i PDF genom att använda en `HashMap` konstruktor.
   * Skapa en `java.io.FileInputStream` genom att använda sin konstruktor och skicka platsen för det PDF-dokument som ska demonteras.
   * Skapa en `com.adobe.idp.Document` -objekt. Skicka `java.io.FileInputStream` objekt som innehåller det PDF-dokument som ska demonteras.
   * Lägg till en post i `java.util.Map` genom att anropa dess `put` och skicka följande argument:

      * Ett strängvärde som representerar nyckelnamnet. Detta värde måste matcha värdet för källelementet PDF som anges i DDX-dokumentet. (I DDX-dokumentet som skapas dynamiskt är värdet `AssemblerResultPDF.pdf`.)
      * A `com.adobe.idp.Document` objekt som innehåller det PDF-dokument som ska demonteras.

1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärsbehov genom att anropa en metod som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera tjänsten Assembler att fortsätta bearbeta ett jobb när ett fel inträffar, ska du anropa `AssemblerOptionSpec` objektets `setFailOnError` metod och skicka `false`.

1. Dela upp PDF-dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` och skicka följande värden:

   * A `com.adobe.idp.Document` objekt som representerar det dynamiskt skapade DDX-dokumentet
   * A `java.util.Map` objekt som innehåller det PDF-dokument som ska demonteras
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objekt som anger körningsalternativen, inklusive standardteckensnitt och jobbloggsnivå

   The `invokeDDX` returnerar en `com.adobe.livecycle.assembler.client.AssemblerResult` objekt som innehåller de uppdelade PDF-dokumenten och eventuella undantag som inträffat.

1. Spara de upplösta PDF-dokumenten.

   Gör så här för att få fram de uppdelade PDF-dokumenten:

   * Anropa `AssemblerResult` objektets `getDocuments` -metod. Den här metoden returnerar en `java.util.Map` -objekt.
   * Iterera genom `java.util.Map` tills du hittar resultatet `com.adobe.idp.Document` -objekt.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att extrahera PDF-dokumentet.

**Se även**

[Snabbstart (SOAP-läge): Skapa ett DDX-dokument dynamiskt med Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Skapa ett DX-dokument dynamiskt med webbtjänstens API {#dynamically-create-a-ddx-document-using-the-web-service-api}

Skapa ett DDX-dokument dynamiskt och demontera ett PDF-dokument med Assembler Service API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition när du anger en tjänstreferens: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en PDF Assembler-klient.

   * Skapa en `AssemblerServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `AssemblerServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Du behöver inte använda `lc_version` -attribut. Det här attributet används när du skapar en tjänstreferens.
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `AssemblerServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Skapa DDX-dokumentet.

   * Skapa en `System.Xml.XmlElement` genom att använda dess konstruktor.
   * Skapa DX-dokumentets rotelement genom att anropa `XmlElement` objektets `CreateElement` -metod. Den här metoden skapar en `Element` som representerar rotelementet. Skicka ett strängvärde som representerar elementets namn till `CreateElement` -metod. Ange ett värde för DDX-elementet genom att anropa dess `SetAttribute` -metod. Lägg slutligen till elementet i DDX-dokumentet genom att anropa `XmlElement` objektets `AppendChild` -metod. Skicka DDX-objektet som ett argument. Följande kodrader visar den här programlogiken:

     ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Skapa DDX-dokumentets `PDFsFromBookmarks` genom att anropa `XmlElement` objektets `CreateElement` -metod. Skicka ett strängvärde som representerar elementets namn till `CreateElement` -metod. Ange sedan ett värde för elementet genom att anropa dess `SetAttribute` -metod. Lägg till `PDFsFromBookmarks` element till rotelementet genom att anropa `DDX` element `AppendChild` -metod. Skicka `PDFsFromBookmarks` elementobjekt som argument. Följande kodrader visar den här programlogiken:

     ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Skapa DDX-dokumentets `PDF` genom att anropa `XmlElement` objektets `CreateElement` -metod. Skicka ett strängvärde som representerar elementets namn till `CreateElement` -metod. Ange sedan ett värde för det underordnade elementet genom att anropa dess `SetAttribute` -metod. Lägg till `PDF` -element till `PDFsFromBookmarks` genom att anropa `PDFsFromBookmarks` element `AppendChild` -metod. Skicka `PDF` elementobjekt som argument. Följande kodrader visar den här programlogiken:

     ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Konvertera DDX-dokumentet.

   * Skapa en `System.IO.MemoryStream` genom att använda dess konstruktor.
   * Fyll i `MemoryStream` -objektet med DDX-dokumentet genom att använda `XmlElement` -objekt som representerar DDX-dokumentet. Anropa `XmlElement` objektets `Save` och skicka `MemoryStream` -objekt.
   * Skapa en bytearray och fyll i den med data som finns i `MemoryStream` -objekt. I följande kod visas den här programlogiken:

     ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Skapa en `BLOB` -objekt. Tilldela bytearrayen till `BLOB` objektets `MTOM` fält.

1. Referera ett PDF-dokument som ska demonteras.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra indatadokumentet i PDF. Detta `BLOB` objektet skickas till `invokeOneDocument` som ett argument.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för indata-PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` egenskapen för bytearrayens innehåll.

1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärskrav genom att tilldela ett värde till en datamedlem som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar tilldelar du `false` till `AssemblerOptionSpec` objektets `failOnError` datamedlem.

1. Dela upp PDF-dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` och skicka följande värden:

   * A `BLOB` objekt som representerar det dynamiskt skapade DDX-dokumentet
   * The `mapItem` array som innehåller indata-PDF-dokumentet
   * An `AssemblerOptionSpec` objekt som anger körningsalternativ

   The `invokeDDX` returnerar en `AssemblerResult` som innehåller resultatet av jobbet och eventuella undantag som inträffade.

1. Spara de upplösta PDF-dokumenten.

   Gör så här för att hämta de nya PDF-dokumenten:

   * Öppna `AssemblerResult` objektets `documents` fält, vilket är ett `Map` objekt som innehåller de uppdelade PDF-dokumenten.
   * Iterera genom `Map` -objekt för att hämta varje resulterande dokument. Sedan, byta ut den arraymedlemmens `value` till `BLOB`.
   * Extrahera de binära data som representerar PDF-dokumentet genom att öppna dess `BLOB` objektets `MTOM` -egenskap. Detta returnerar en array med byte som du kan skriva ut till en PDF-fil.

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
