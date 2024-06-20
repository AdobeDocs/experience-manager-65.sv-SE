---
title: Sammanställa dokument med Bates-numrering
description: Använd Bates-numrering för att sammanställa PDF-dokument med Java- och Web Service API.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2a4e21c4-f2f5-44cd-b8ed-7b572782a2f1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,  Document Services
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# Sammanställa dokument med Bates-numrering {#assembling-documents-using-bates-numbering}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

Du kan sätta ihop PDF-dokument som innehåller unika sididentifierare genom att använda Bates-numrering. *Bates-numrering* är en metod för att tillämpa unika identifieringsmetoder på en grupp av relaterade dokument. Varje sida i dokumentet (eller dokumentuppsättningen) tilldelas ett Bates-nummer som unikt identifierar sidan. Till exempel kan tillverkningsdokument som innehåller produktstruktur och som är kopplade till produktionen av en sammansättning innehålla en identifierare. Ett Bates-nummer innehåller ett numeriskt värde i följd samt ett valfritt prefix och suffix. Prefixet + numeriskt + suffix kallas *bates-mönster*.

Följande bild visar ett PDF-dokument som innehåller en unik identifierare i dokumentets sidhuvud.

![au_au_batesnumber](assets/au_au_batesnumber.png)

I det här avsnittet placeras den unika sididentifieraren i ett dokuments sidhuvud. Anta att följande DDX-dokument används.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="out.pdf">
        <Header>
         <Center>
             <StyledText>
                 <p font-size="20pt"><BatesNumber/></p>
             </StyledText>
         </Center>
     </Header>
           <PDF source="map.pdf" />
          <PDF source="directions.pdf" />
          </PDF>
 </DDX>
```

Det här DDX-dokumentet sammanfogar två PDF-dokument med namnet *map.pdf* och *vägbeskrivning.pdf* till ett enda dokument i PDF. Det resulterande PDF-dokumentet innehåller ett sidhuvud som består av en unik sididentifierare. Dokumentet i ovanstående bild visar till exempel 000016.

>[!NOTE]
>
>Innan du läser det här avsnittet bör du känna till hur du sammanställer PDF-dokument med hjälp av tjänsten Assembler. I det här avsnittet beskrivs inte begreppen, till exempel att skapa ett samlingsobjekt som innehåller indatadokument eller att extrahera resultaten från det returnerade samlingsobjektet. (Se [Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Mer information om Assembler-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Sammanfattning av steg {#summary-of-steps}

Gör så här om du vill sätta ihop ett PDF-dokument som innehåller en unik sididentifierare (Bates-numrering):

1. Inkludera projektfiler.
1. Skapa en PDF Assembler-klient.
1. Referera till ett befintligt DDX-dokument.
1. Referera PDF-dokument för indata.
1. Ange det inledande Bates-nummervärdet.
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

Om AEM Forms körs på en annan J2EE-programserver än JBoss måste du ersätta filerna adobe-utilities.jar och jbossall-client.jar med JAR-filer som är specifika för J2EE-programservern där AEM Forms är driftsatt. Information om platsen för alla AEM Forms JAR-filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Skapa en PDF Assembler-klient**

Innan du programmässigt kan utföra en Assembler-åtgärd måste du skapa en Assembler-tjänstklient.

**Referera till ett befintligt DDX-dokument**

Ett DDX-dokument måste refereras till för att du ska kunna montera ett PDF-dokument. Ta till exempel det DX-dokument som introducerades i det här avsnittet. Om du vill montera ett PDF-dokument som innehåller unika sididentifierare måste DDX-dokumentet innehålla `BatesNumber` -element.

**PDF-dokument för referensindata**

Det måste finnas referenser till indata-PDF-dokument för att du ska kunna samla ihop ett PDF-dokument. Exempelvis måste dokumenten map.pdf och direction.pdf refereras till för att samla ihop dessa PDF-dokument till ett enda PDF-dokument.

**Ange det inledande Bates-nummervärdet**

Du kan ställa in det inledande Bates-numret så att det uppfyller dina affärskrav. Anta till exempel att det är ett krav att ställa in startvärdet på 000100. Om du inte anger startvärdet är värdet för den första sidan 00000.

**Sammanställa PDF-indatadokument**

När du har skapat Assembler-tjänstklienten ska du referera till det DDX-dokument som innehåller `BatesNumber` elementinformation, referera till ett inmatningsdokument i PDF och ange körningsalternativ, kan du anropa `invokeDDX` som resulterar i att Assembler-tjänsten samlar ihop ett PDF-dokument som innehåller unika sididentifierare.

**Extrahera resultaten**

Assembler-tjänsten returnerar ett samlingsobjekt som innehåller jobbresultaten. Du kan extrahera det resulterande PDF-dokumentet och eventuella undantag som genereras. I det här fallet finns ett krypterat PDF-dokument i samlingsobjektet.

>[!NOTE]
>
>Ett samlingsobjekt returneras om du anropar `invokeDDX` operation. Den här åtgärden används när två eller flera indatadokument skickas till PDF till Assembler-tjänsten. Om du bara skickar ett indatadokument i PDF till Assembler-tjänsten bör du anropa `invokeOneDocument` operation. Mer information om hur du använder den här åtgärden finns i [Sammanställa krypterade PDF-dokument](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Sammanställa dokument med Bates-numrering med Java API {#assemble-documents-with-bates-numbering-using-the-java-api}

Sammanställa ett PDF-dokument som använder unika sididentifierare (Bates-numrering) med hjälp av Assembler Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en PDF Assembler-klient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `AssemblerServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Referera till ett befintligt DDX-dokument.

   * Skapa en `java.io.FileInputStream` -objekt som representerar DDX-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för DDX-filen.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Referera PDF-dokument för indata.

   * Skapa en `java.util.Map` objekt som används för att lagra indatadokument i PDF genom att använda en `HashMap` konstruktor.
   * För varje indatadokument i PDF skapar du en `java.io.FileInputStream` genom att använda dess konstruktor och skicka indatadokumentets plats i PDF. I så fall ska du skicka platsen för ett oskyddat PDF-dokument.
   * För varje indatadokument i PDF skapar du en `com.adobe.idp.Document` -objektet och skicka `java.io.FileInputStream` -objekt som innehåller dokumentet PDF.
   * Lägg till en post i `java.util.Map` genom att anropa dess `put` och skicka följande argument:

      * Ett strängvärde som representerar nyckelnamnet. Detta värde måste matcha värdet för källelementet PDF som anges i DDX-dokumentet. Namnet på källfilen i PDF som anges i DDX-dokumentet som introduceras i det här avsnittet är Loan.pdf.
      * A `com.adobe.idp.Document` objekt som innehåller det oskyddade PDF-dokumentet.

1. Ange det inledande Bates-nummervärdet.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange det inledande Bates-numret genom att anropa `AssemblerOptionSpec` objektets `setFirstBatesNumber` och skickar ett numeriskt värde som anger det inledande värdet.

1. Sammanställ PDF-indatadokumenten.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` och skicka följande obligatoriska värden:

   * A `com.adobe.idp.Document` -objekt som representerar DDX-dokumentet.
   * A `java.util.Map` objekt som innehåller indata för oskyddad PDF-fil.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` -objekt som anger körningsalternativ, inklusive standardteckensnitt och jobbloggsnivå.

   The `invokeDDX` returnerar en `com.adobe.livecycle.assembler.client.AssemblerResult` objekt som innehåller ett lösenordskrypterat PDF-dokument.

1. Extrahera resultaten.

   Utför följande åtgärder för att hämta det nya PDF-dokumentet:

   * Anropa `AssemblerResult` objektets `getDocuments` -metod. Den här åtgärden returnerar en `java.util.Map` -objekt.
   * Iterera genom `java.util.Map` tills du hittar `com.adobe.idp.Document` -objekt.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att extrahera PDF-dokumentet.

**Se även**

[Snabbstart (SOAP läge): Sammanställa ett PDF-dokument med Bates-numrering med Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Sammanställa dokument med Bates-numrering med webbtjänstens API {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Sammanställa ett PDF-dokument som använder unika sididentifierare (Bates-numrering) med Assembler Service API (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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

1. Referera till ett befintligt DDX-dokument.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra DDX-dokumentet.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för DDX-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Referera PDF-dokument för indata.

   * För varje indatadokument i PDF skapar du en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra indatadokumentet i PDF.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för indata-PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` med bytearrayens innehåll.
   * Skapa en `MyMapOf_xsd_string_To_xsd_anyType` -objekt. Det här samlingsobjektet används för att lagra PDF-indatadokument.
   * För varje indatadokument i PDF skapar du en `MyMapOf_xsd_string_To_xsd_anyType_Item` -objekt. Om du t.ex. använder två indata-PDF-dokument skapar du två `MyMapOf_xsd_string_To_xsd_anyType_Item` objekt.
   * Tilldela ett strängvärde som representerar nyckelnamnet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `key` fält. Detta värde måste matcha värdet för källelementet PDF som anges i DDX-dokumentet. (Utför den här åtgärden för varje dokument i PDF.)
   * Tilldela `BLOB` det objekt som lagrar PDF-dokumentet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `value` fält. (Utför den här åtgärden för varje dokument i PDF.)
   * Lägg till `MyMapOf_xsd_string_To_xsd_anyType_Item` objekt till `MyMapOf_xsd_string_To_xsd_anyType` -objekt. Anropa `MyMapOf_xsd_string_To_xsd_anyType` objektets `Add` och skicka `MyMapOf_xsd_string_To_xsd_anyType` -objekt. (Utför den här åtgärden för varje dokument i PDF.)

1. Ange det inledande Bates-nummervärdet.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange det inledande Bates-numret genom att tilldela ett numeriskt värde till `firstBatesNumber` datamedlem som tillhör `AssemblerOptionSpec` -objekt.

1. Sammanställ PDF-indatadokumenten.

   Anropa `AssemblerServiceClient` objektets `invoke` och skicka följande värden:

   * A `BLOB` -objekt som representerar DDX-dokumentet.
   * The `MyMapOf_xsd_string_To_xsd_anyType` objekt som innehåller indatadokumenten i PDF. Dess nycklar måste matcha PDF källfilernas namn och dess värden måste vara `BLOB` objekt som motsvarar dessa filer.
   * An `AssemblerOptionSpec` objekt som anger körningsalternativ.

   The `invoke` returnerar en `AssemblerResult` som innehåller resultatet av jobbet och eventuella undantag som inträffade.

1. Extrahera resultaten.

   Utför följande åtgärder för att hämta det nya PDF-dokumentet:

   * Öppna `AssemblerResult` objektets `documents` fält, vilket är ett `Map` -objekt som innehåller de resulterande PDF-dokumenten.
   * Iterera genom `Map` tills du hittar nyckeln som matchar namnet på det resulterande dokumentet. Byt sedan ut arraymedlemmens `value` till `BLOB`.
   * Extrahera de binära data som representerar PDF-dokumentet genom att öppna dess `BLOB` objektets `MTOM` -egenskap. Detta returnerar en array med byte som du kan skriva ut till en PDF-fil.

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
