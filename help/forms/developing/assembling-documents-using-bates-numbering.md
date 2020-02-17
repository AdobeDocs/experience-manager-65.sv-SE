---
title: Sammanställa dokument med hjälp av Bates-numrering
seo-title: Sammanställa dokument med hjälp av Bates-numrering
description: 'null'
seo-description: 'null'
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Sammanställa dokument med hjälp av Bates-numrering {#assembling-documents-using-bates-numbering}

Du kan sammanställa PDF-dokument som innehåller unika sididentifierare med hjälp av Bates-numrering. *Bates-numrering* är ett sätt att tillämpa unika identifieringsmetoder på en grupp med relaterade dokument. Varje sida i dokumentet (eller dokumentuppsättningen) tilldelas ett Bates-nummer som unikt identifierar sidan. Till exempel kan tillverkningsdokument som innehåller produktstruktur och som är kopplade till produktionen av en sammansättning innehålla en identifierare. Ett Bates-nummer innehåller ett numeriskt värde i följd samt ett valfritt prefix och suffix. Prefixet + numeriskt + suffix kallas för ett *bates-mönster*.

Följande bild visar ett PDF-dokument som innehåller en unik identifierare som finns i dokumentets sidhuvud.

![au_au_batesnumber](assets/au_au_batesnumber.png)

I det här avsnittet placeras den unika sididentifieraren i ett dokuments sidhuvud. Anta att följande DDX-dokument används.

```as3
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

Det här DDX-dokumentet sammanfogar två PDF-dokument med namnen *map.pdf* och *directs.pdf* till ett enda PDF-dokument. Det resulterande PDF-dokumentet innehåller ett sidhuvud som består av en unik sididentifierare. Dokumentet i ovanstående bild visar till exempel 000016.

>[!NOTE]
>
>Innan du läser det här avsnittet bör du känna till hur du sammanställer PDF-dokument med hjälp av tjänsten Assembler. I det här avsnittet beskrivs inte begreppen, till exempel att skapa ett samlingsobjekt som innehåller indatadokument eller att extrahera resultaten från det returnerade samlingsobjektet. (Se [Sammanställa PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)programmatiskt.)

>[!NOTE]
>
>Mer information om tjänsten Assembler finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DDX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Sammanfattning av steg {#summary-of-steps}

Gör så här om du vill sätta ihop ett PDF-dokument som innehåller en unik sididentifierare (Bates-numrering):

1. Inkludera projektfiler.
1. Skapa en PDF Assembler-klient.
1. Referera till ett befintligt DDX-dokument.
1. Referera PDF-indatadokument.
1. Ange det inledande Bates-nummervärdet.
1. Sammanställ PDF-indatadokumenten.
1. Extrahera resultaten.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (krävs om AEM Forms distribueras på JBoss)
* jbossall-client.jar (krävs om AEM Forms distribueras på JBoss)

Om AEM Forms används på en annan J2EE-programserver än JBoss måste du ersätta filerna adobe-utilities.jar och jbossall-client.jar med JAR-filer som är specifika för J2EE-programservern där AEM Forms används. Information om platsen för alla AEM Forms JAR-filer finns i [Inkludera Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)för AEM Forms.

**Skapa en PDF Assembler-klient**

Innan du programmässigt kan utföra en Assembler-åtgärd måste du skapa en Assembler-tjänstklient.

**Referera till ett befintligt DDX-dokument**

Det måste finnas referenser till ett DDX-dokument för att du ska kunna sammanställa ett PDF-dokument. Ta till exempel det DX-dokument som introducerades i det här avsnittet. Om du vill montera ett PDF-dokument som innehåller unika sididentifierare måste DDX-dokumentet innehålla `BatesNumber` elementet.

**Referens för PDF-indatadokument**

Indata-PDF-dokument måste refereras till för att det ska gå att sammanställa ett PDF-dokument. Exempelvis måste dokumenten map.pdf och direction.pdf refereras till för att sammanfoga dessa PDF-dokument till ett enda PDF-dokument.

**Ange det inledande Bates-nummervärdet**

Du kan ställa in det inledande Bates-numret så att det uppfyller dina affärskrav. Anta till exempel att det är ett krav att ställa in startvärdet på 000100. Om du inte anger startvärdet är värdet för den första sidan 00000.

**Sammanställa PDF-indata**

När du har skapat Assembler-tjänstklienten, refererar till det DDX-dokument som innehåller `BatesNumber` elementinformation, refererar till ett PDF-indatadokument och anger körningsalternativ, kan du anropa den `invokeDDX` åtgärd som resulterar i att Assembler-tjänsten sätter ihop ett PDF-dokument som innehåller unika sididentifierare.

**Extrahera resultaten**

Assembler-tjänsten returnerar ett samlingsobjekt som innehåller jobbresultaten. Du kan extrahera det resulterande PDF-dokumentet och eventuella undantag som genereras. I det här fallet finns ett krypterat PDF-dokument i samlingsobjektet.

>[!NOTE]
>
>Ett samlingsobjekt returneras om du anropar `invokeDDX` åtgärden. Den här åtgärden används när två eller flera PDF-indatadokument skickas till Assembler-tjänsten. Om du bara skickar ett PDF-indatadokument till Assembler-tjänsten bör du anropa `invokeOneDocument` åtgärden. Mer information om hur du använder den här åtgärden finns i [Sammanställa krypterade PDF-dokument](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Sammanställa dokument med Bates-numrering med Java API {#assemble-documents-with-bates-numbering-using-the-java-api}

Sammanställa ett PDF-dokument som använder unika sididentifierare (Bates-numrering) med Assembler Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en PDF Assembler-klient.

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa ett `AssemblerServiceClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.

1. Referera till ett befintligt DDX-dokument.

   * Skapa ett `java.io.FileInputStream` objekt som representerar DDX-dokumentet med hjälp av dess konstruktor och skicka ett strängvärde som anger platsen för DDX-filen.
   * Skapa ett `com.adobe.idp.Document` objekt med hjälp av dess konstruktor och skicka `java.io.FileInputStream` objektet.

1. Referera PDF-indatadokument.

   * Skapa ett `java.util.Map` objekt som används för att lagra PDF-indatadokument med hjälp av en `HashMap` konstruktor.
   * För varje PDF-indatadokument skapar du ett `java.io.FileInputStream` objekt med hjälp av dess konstruktor och skickar platsen för PDF-indatadokumentet. I så fall skickar du platsen för ett oskyddat PDF-dokument.
   * För varje PDF-indatadokument skapar du ett `com.adobe.idp.Document` objekt och skickar det `java.io.FileInputStream` objekt som innehåller PDF-dokumentet.
   * Lägg till en post i `java.util.Map` objektet genom att anropa dess `put` metod och skicka följande argument:

      * Ett strängvärde som representerar nyckelnamnet. Detta värde måste matcha värdet för PDF-källelementet som anges i DDX-dokumentet. Namnet på PDF-källfilen som anges i DDX-dokumentet som introduceras i det här avsnittet är till exempel Loan.pdf.
      * Ett `com.adobe.idp.Document` objekt som innehåller det oskyddade PDF-dokumentet.

1. Ange det inledande Bates-nummervärdet.

   * Skapa ett `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange det inledande Bates-numret genom att anropa `AssemblerOptionSpec` objektets `setFirstBatesNumber` och skicka ett numeriskt värde som anger det inledande värdet.

1. Sammanställ PDF-indatadokumenten.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` metod och skicka följande obligatoriska värden:

   * Ett `com.adobe.idp.Document` objekt som representerar DDX-dokumentet.
   * Ett `java.util.Map` objekt som innehåller den oskyddade indatafilen.
   * Ett `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objekt som anger körningsalternativen, inklusive standardteckensnitt och jobbloggsnivå.
   Metoden returnerar `invokeDDX` ett `com.adobe.livecycle.assembler.client.AssemblerResult` objekt som innehåller ett lösenordskrypterat PDF-dokument.

1. Extrahera resultaten.

   Utför följande åtgärder för att hämta det nya PDF-dokumentet:

   * Anropa `AssemblerResult` objektets `getDocuments` metod. Den här åtgärden returnerar ett `java.util.Map` objekt.
   * Upprepa genom `java.util.Map` objektet tills du hittar `com.adobe.idp.Document` objektet.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att extrahera PDF-dokumentet.

**Se även**

[Snabbstart (SOAP-läge): Sammanställa ett PDF-dokument med Bates-numrering med Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Sammanställa dokument med Bates-numrering med webbtjänstens API {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Sammanställa ett PDF-dokument som använder unika sididentifierare (Bates-numrering) med Assembler Service API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för DDX-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll objektet `BLOB` genom att tilldela dess `MTOM` fält med innehållet i bytearrayen.

1. Referera PDF-indatadokument.

   * För varje PDF-indatadokument skapar du ett `BLOB` objekt med hjälp av dess konstruktor. Objektet används `BLOB` för att lagra PDF-indatadokumentet.
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för PDF-indatadokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll objektet `BLOB` genom att tilldela dess `MTOM` egenskap med innehållet i bytearrayen.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Det här samlingsobjektet används för att lagra PDF-indatadokumenten.
   * Skapa ett `MyMapOf_xsd_string_To_xsd_anyType_Item` objekt för varje PDF-indatadokument. Om du till exempel använder två PDF-indatadokument skapar du två `MyMapOf_xsd_string_To_xsd_anyType_Item` objekt.
   * Tilldela ett strängvärde som representerar nyckelnamnet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `key` fält. Detta värde måste matcha värdet för PDF-källelementet som anges i DDX-dokumentet. (Utför den här åtgärden för varje PDF-indatadokument.)
   * Tilldela det `BLOB` objekt som lagrar PDF-dokumentet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `value` fält. (Utför den här åtgärden för varje PDF-indatadokument.)
   * Lägg till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektet i `MyMapOf_xsd_string_To_xsd_anyType` objektet. Anropa `MyMapOf_xsd_string_To_xsd_anyType` objektets `Add` metod och skicka `MyMapOf_xsd_string_To_xsd_anyType` objektet. (Utför den här åtgärden för varje PDF-indatadokument.)

1. Ange det inledande Bates-nummervärdet.

   * Skapa ett `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange det inledande Bates-numret genom att tilldela ett numeriskt värde till den `firstBatesNumber` datamedlem som tillhör `AssemblerOptionSpec` objektet.

1. Sammanställ PDF-indatadokumenten.

   Anropa `AssemblerServiceClient` objektets `invoke` metod och skicka följande värden:

   * Ett `BLOB` objekt som representerar DDX-dokumentet.
   * Det `MyMapOf_xsd_string_To_xsd_anyType` objekt som innehåller PDF-indatadokumenten. Nycklarna måste matcha namnen på PDF-källfilerna och deras värden måste vara de `BLOB` objekt som motsvarar dessa filer.
   * Ett `AssemblerOptionSpec` objekt som anger körningsalternativ.
   Metoden returnerar ett `invoke` `AssemblerResult` objekt som innehåller resultatet av jobbet och eventuella undantag som inträffade.

1. Extrahera resultaten.

   Utför följande åtgärder för att hämta det nya PDF-dokumentet:

   * Få åtkomst till `AssemblerResult` objektets `documents` fält, som är ett `Map` objekt som innehåller PDF-dokumentets resultat.
   * Iterera genom objektet tills du hittar den tangent som matchar namnet på det resulterande dokumentet. `Map` Sedan konverterar du arraymedlemmens `value` till en `BLOB`.
   * Extrahera de binära data som representerar PDF-dokumentet genom att få åtkomst till dess `BLOB` objektegenskap `MTOM` . Detta returnerar en array med byte som du kan skriva till en PDF-fil.

**Se även**

[Anropa AEM-formulär med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
