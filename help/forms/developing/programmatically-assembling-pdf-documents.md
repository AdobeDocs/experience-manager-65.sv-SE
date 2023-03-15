---
title: Programmisk sammanställning av PDF-dokument
seo-title: Programmatically Assembling PDF Documents
description: Använd API:t för Assembler-tjänsten för att samla ihop flera PDF-dokument till ett enda PDF-dokument med hjälp av Java API och Web Service API.
seo-description: Use the Assembler service API to assemble multiple PDF documents into a single PDF document using the Java API and the Web Service API.
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
role: Developer
exl-id: 7d6fd230-e477-4286-9fb3-18a3474e3e48
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 0%

---

# Programmisk sammanställning av PDF-dokument {#programmatically-assembling-pdf-documents}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

Du kan använda Assembler Service API för att samla ihop flera PDF-dokument till ett enda PDF-dokument. Följande bild visar tre PDF-dokument som sammanfogas till ett enda PDF-dokument.

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

Om du vill samla ihop två eller flera PDF-dokument till ett enda PDF-dokument behöver du ett DX-dokument. Ett DDX-dokument beskriver det PDF-dokument som Assembler-tjänsten skapar. DX-dokumentet instruerar alltså Assembler-tjänsten vilka åtgärder som ska utföras.

Anta att följande DDX-dokument används för den här diskussionen.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

Det här DDX-dokumentet sammanfogar två PDF-dokument med namnet *map.pdf* och *vägbeskrivning.pdf* till ett enda dokument i PDF.

>[!NOTE]
>
>Om du vill se ett DX-dokument som demonterar ett PDF-dokument går du till [Dela upp PDF-dokument programmatiskt](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>Mer information om Assembler-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Att tänka på när Assembler-tjänsten anropas med webbtjänster {#considerations-when-invoking-assembler-service-using-web-services}

När du lägger till sidhuvuden och sidfötter när du sammanställer stora dokument kan du stöta på ett `OutOfMemory` och filerna kommer inte att sättas ihop. Om du vill minska risken för det här problemet lägger du till en `DDXProcessorSetting` -element till ditt DDX-dokument, vilket visas i följande exempel.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

Du kan lägga till det här elementet som ett underordnat element till `DDX` element eller som underordnad till `PDF result` -element. Standardvärdet för den här inställningen är 0 (noll), vilket inaktiverar kontrollpunkten och DDX fungerar som om `DDXProcessorSetting` elementet finns inte. Om du har hittat ett `OutOfMemory` kan du behöva ange ett heltal som är mellan 500 och 5000. Ett litet kontrollpunktsvärde resulterar i mer frekventa kontrollpunkter.

## Sammanfattning av steg {#summary-of-steps}

Gör så här om du vill samla ihop ett dokument från flera PDF-dokument i ett PDF:

1. Inkludera projektfiler.
1. Skapa en PDF Assembler-klient.
1. Referera till ett befintligt DDX-dokument.
1. Referera PDF-dokument för indata.
1. Ange körningsalternativ.
1. Sammanställ PDF-indatadokumenten.
1. Extrahera resultaten.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

Om AEM Forms körs på en annan J2EE-programserver än JBoss måste du ersätta filerna adobe-utilities.jar och jbossall-client.jar med JAR-filer som är specifika för J2EE-programservern där AEM Forms är distribuerad.

**Skapa en PDF Assembler-klient**

Innan du programmässigt kan utföra en Assembler-åtgärd måste du skapa en Assembler-klient.

**Referera till ett befintligt DDX-dokument**

Ett DDX-dokument måste refereras till för att du ska kunna montera ett PDF-dokument. Ta till exempel det DX-dokument som introducerades i det här avsnittet. Det här DDX-dokumentet instruerar Assembler-tjänsten att sammanfoga två PDF-dokument till ett enda PDF-dokument.

**PDF-dokument för referensindata**

Referera indatadokument i PDF som du vill skicka till Assembler-tjänsten. Om du till exempel vill skicka två indatadokument med namnet Karta och Riktningar för PDF måste du skicka motsvarande PDF-filer.

Både filen map.pdf och filen Directions.pdf måste placeras i ett samlingsobjekt. Nyckelns namn måste matcha PDF-källattributets värde i DDX-dokumentet. Det spelar ingen roll vad namnet på filen PDF är om nyckeln och källattributet i DDX-dokumentet matchar.

>[!NOTE]
>
>An `AssemblerResult` -objektet, som innehåller ett samlingsobjekt, returneras om du anropar `invokeDDX` operation. Den här åtgärden används när du skickar två eller flera PDF-indatadokument till Assembler-tjänsten. Om du bara skickar ett indatavärde PDF till Assembler-tjänsten och bara förväntar dig ett returdokument, ska du anropa `invokeOneDocument` operation. När den här åtgärden anropas returneras ett enda dokument. Mer information om hur du använder den här åtgärden finns i [Sammanställa krypterade PDF-dokument](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**Ange körningsalternativ**

Du kan ställa in körningsalternativ som styr beteendet för Assembler-tjänsten när den utför ett jobb. Du kan till exempel ange ett alternativ som instruerar Assembler-tjänsten att fortsätta bearbeta ett jobb om ett fel uppstår. Mer information om de körningsalternativ du kan ange finns i `AssemblerOptionSpec` klassreferens i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Sammanställa PDF-indatadokument**

När du har skapat tjänstklienten, refererat till en DDX-fil, skapat ett samlingsobjekt som lagrar indatadokument i PDF och angett körningsalternativ, kan du starta DDX-åtgärden. När du använder det DDX-dokument som anges i det här avsnittet sammanfogas filerna map.pdf och direction.pdf till ett PDF-dokument.

**Extrahera resultaten**

Assembler-tjänsten returnerar en `java.util.Map` -objekt, som kan hämtas från `AssemblerResult` och som innehåller åtgärdsresultat. Den returnerade `java.util.Map` -objektet innehåller de resulterande dokumenten och eventuella undantag.

I följande tabell sammanfattas några av de nyckelvärden och objekttyper som kan finnas i den returnerade `java.util.Map` -objekt.

<table>
 <thead>
  <tr>
   <th><p>Nyckelvärde</p></th>
   <th><p>Objekttyp</p></th>
   <th><p>Beskrivning</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p>Innehåller de resulterande dokument som anges i ett DDX-resultatelement</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>Innehåller alla undantag för dokumentet</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>Innehåller jobbloggen</p></td>
  </tr>
 </tbody>
</table>

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Dela upp PDF-dokument programmatiskt](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Sammanställa PDF-dokument med Java API {#assemble-pdf-documents-using-the-java-api}

Sammanställa ett PDF-dokument med hjälp av Assembler Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en PDF Assembler-klient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `AssemblerServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Referera till ett befintligt DDX-dokument.

   * Skapa en `java.io.FileInputStream` som representerar DDX-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för DDX-filen.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Referera PDF-dokument för indata.

   * Skapa en `java.util.Map` objekt som används för att lagra indatadokument i PDF genom att använda en `HashMap` konstruktor.
   * För varje indatadokument i PDF skapar du en `java.io.FileInputStream` genom att använda dess konstruktor och skicka indatadokumentets plats i PDF.
   * För varje indatadokument i PDF skapar du en `com.adobe.idp.Document` -objektet och skicka `java.io.FileInputStream` som innehåller dokumentet PDF.
   * Lägg till en post i `java.util.Map` genom att anropa dess `put` och skicka följande argument:

      * Ett strängvärde som representerar nyckelnamnet. Detta värde måste matcha värdet för källelementet PDF som anges i DDX-dokumentet.
      * A `com.adobe.idp.Document` objekt (eller `java.util.List` -objekt som anger flera dokument) som innehåller PDF-källdokumentet.

1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärsbehov genom att anropa en metod som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera tjänsten Assembler att fortsätta bearbeta ett jobb när ett fel inträffar, ska du anropa `AssemblerOptionSpec` objektets `setFailOnError` metod och skicka `false`.

1. Sammanställ PDF-indatadokumenten.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` och skicka följande obligatoriska värden:

   * A `com.adobe.idp.Document` objekt som representerar det DDX-dokument som ska användas
   * A `java.util.Map` objekt som innehåller indatafilerna för PDF som ska monteras
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objekt som anger körningsalternativ, inklusive standardteckensnitt och jobbloggsnivå

   The `invokeDDX` returnerar en `com.adobe.livecycle.assembler.client.AssemblerResult` som innehåller resultatet av jobbet och eventuella undantag som inträffade.

1. Extrahera resultaten.

   Utför följande åtgärder för att hämta det nya PDF-dokumentet:

   * Anropa `AssemblerResult` objektets `getDocuments` -metod. Detta returnerar `java.util.Map` -objekt.
   * Iterera genom `java.util.Map` tills du hittar resultatet `com.adobe.idp.Document` -objekt. (Du kan använda resultatelementet PDF som anges i DDX-dokumentet för att hämta dokumentet.)
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att extrahera PDF-dokumentet.

   >[!NOTE]
   >
   >If `LOG_LEVEL` har angetts för att skapa en logg, du kan extrahera loggen med `AssemblerResult` objektets `getJobLog` -metod.

**Se även**

[Snabbstart (SOAP-läge): Sammanställa ett PDF-dokument med Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Sammanställa PDF-dokument med hjälp av webbtjänstens API {#assemble-pdf-documents-using-the-web-service-api}

Sammanställa PDF-dokument med Assembler Service API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för DDX-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` med bytearrayens innehåll.

1. Referera PDF-dokument för indata.

   * För varje indatadokument i PDF skapar du en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra indatadokumentet i PDF.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för indata-PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.
   * Skapa en `MyMapOf_xsd_string_To_xsd_anyType` -objekt. Det här samlingsobjektet används för att lagra indatadokument i PDF.
   * För varje indatadokument i PDF skapar du en `MyMapOf_xsd_string_To_xsd_anyType_Item` -objekt. Om du t.ex. använder två indata-PDF-dokument skapar du två `MyMapOf_xsd_string_To_xsd_anyType_Item` objekt.
   * Tilldela ett strängvärde som representerar nyckelnamnet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `key` fält. Detta värde måste matcha värdet för källelementet PDF som anges i DDX-dokumentet. (Utför den här åtgärden för varje dokument i PDF.)
   * Tilldela `BLOB` objekt som lagrar PDF-dokumentet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `value` fält. (Utför den här åtgärden för varje dokument i PDF.)
   * Lägg till `MyMapOf_xsd_string_To_xsd_anyType_Item` objekt till `MyMapOf_xsd_string_To_xsd_anyType` -objekt. Anropa `MyMapOf_xsd_string_To_xsd_anyType` objektets `Add` och skicka `MyMapOf_xsd_string_To_xsd_anyType` -objekt. (Utför den här åtgärden för varje dokument i PDF.)

1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärskrav genom att tilldela ett värde till en datamedlem som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar tilldelar du `false` till `AssemblerOptionSpec` objektets `failOnError` datamedlem.

1. Sammanställ PDF-indatadokumenten.

   Anropa `AssemblerServiceClient` objektets `invoke` och skicka följande värden:

   * A `BLOB` -objekt som representerar DDX-dokumentet.
   * The `mapItem` -array som innehåller indatadokumenten i PDF. Dess nycklar måste matcha PDF källfilernas namn och dess värden måste vara `BLOB` objekt som motsvarar dessa filer.
   * An `AssemblerOptionSpec` objekt som anger körningsalternativ.

   The `invoke` returnerar en `AssemblerResult` som innehåller resultatet av jobbet och eventuella undantag som kan ha inträffat.

1. Extrahera resultaten.

   Utför följande åtgärder för att hämta det nya PDF-dokumentet:

   * Öppna `AssemblerResult` objektets `documents` fält, vilket är ett `Map` -objekt som innehåller de resulterande PDF-dokumenten.
   * Iterera genom `Map` tills du hittar nyckeln som matchar namnet på det resulterande dokumentet. Sätt sedan den arraymedlemmens `value` till `BLOB`.
   * Extrahera de binära data som representerar PDF-dokumentet genom att öppna dess `BLOB` objektets `MTOM` -egenskap. Detta returnerar en array med byte som du kan skriva ut till en PDF-fil.

   >[!NOTE]
   >
   >If `LOG_LEVEL` har angetts för att skapa en logg, du kan extrahera loggen genom att hämta värdet för `AssemblerResult` objektets `jobLog` datamedlem.

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
