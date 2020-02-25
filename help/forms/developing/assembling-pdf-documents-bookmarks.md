---
title: Sammanställa PDF-dokument med bokmärken
seo-title: Sammanställa PDF-dokument med bokmärken
description: 'null'
seo-description: 'null'
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Sammanställa PDF-dokument med bokmärken {#assembling-pdf-documents-with-bookmarks}

Du kan sätta ihop ett PDF-dokument som innehåller bokmärken. Anta till exempel att du har ett PDF-dokument som inte innehåller bokmärken och du vill ändra det genom att ange bokmärken. Med Assembler-tjänsten kan du skicka ett PDF-dokument som inte innehåller bokmärken och få tillbaka ett PDF-dokument som innehåller bokmärken.

Bokmärken innehåller följande egenskaper:

* En titel som visas som text på skärmen.
* En åtgärd som anger vad som händer när en användare klickar på bokmärket. Den typiska åtgärden för ett bokmärke är att flytta till en annan plats i det aktuella dokumentet eller öppna ett annat PDF-dokument, även om andra åtgärder kan anges.

Anta att följande DDX-dokument används för den här diskussionen.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

Observera att källattributet är tilldelat värdet i det här DDX-dokumentet `Loan.pdf`. Det här DDX-dokumentet anger att ett enda PDF-dokument skickas till Assembler-tjänsten. När du sammanställer ett PDF-dokument med bokmärken måste du ange ett XML-dokument för bokmärken som beskriver bokmärkena i resultatdokumentet. Om du vill ange ett XML-dokument för bokmärken kontrollerar du att `Bookmarks` elementet har angetts i ditt DDX-dokument.

I det här exemplet på DDX-dokument anger `Bookmarks` elementet `doc2` som värde. Det här värdet anger att indatamappningen som skickas till Assembler-tjänsten innehåller en nyckel med namnet `doc2`. Värdet för `doc2` nyckeln är ett `com.adobe.idp.Document` värde som representerar XML-dokumentet för bokmärket. (Se&quot;Bokmärkesspråk&quot; i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).)

I det här avsnittet används följande språk för XML-bokmärken för att sätta ihop ett PDF-dokument som innehåller bokmärken.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <Bookmarks xmlns="https://ns.adobe.com/pdf/bookmarks" version="1.0">
       <Bookmark>
          <Action>
             <Launch NewWindow="true">
                <File Name="C:\Adobe\LoanDetails.pdf" />
             </Launch>
          </Action>
         <Title>Open the Loan document</Title>
       </Bookmark>
 <Bookmark>
          <Action>
             <Launch>
                <Win Name="C:\WINDOWS\notepad.exe" />
             </Launch>
          </Action>
     <Title>Launch NotePad</Title>
       </Bookmark>
 </Bookmarks>
```

Lägg märke till det Action-element som definierar åtgärden som utförs när en användare klickar på bokmärket i det här XML-bokmärkesdokumentet. Under elementet Action (Åtgärd) är det Launch-element som startar program, t.ex. NotePad, och öppnar filer, t.ex. PDF-filer. Om du vill öppna en PDF-fil måste du använda det File-element som anger vilken fil som ska öppnas. I t.ex. den XML-fil för bokmärke som anges i det här avsnittet heter filen som öppnas LoanDetails.pdf.

>[!NOTE]
>
>Fullständig information om vilka åtgärder som stöds finns i&quot; `Action` element&quot; i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

Med tanke på det DDX-dokument som anges i det här avsnittet och XML-bokmärkesfilen som indata sammanställer Assembler-tjänsten ett PDF-dokument som innehåller följande bokmärken.

![aw_aw_bmark](assets/aw_aw_bmark.png)

När en användare klickar på *Öppna bokmärket Lånedetaljer* öppnas filen LoanDetails.pdf. På samma sätt startas NotePad när användaren klickar på bokmärket *Launch NotePad* .

>[!NOTE]
>
>Innan du läser det här avsnittet bör du känna till hur du sammanställer PDF-dokument med hjälp av tjänsten Assembler. I det här avsnittet beskrivs inte begrepp, till exempel att skapa ett samlingsobjekt som innehåller indatadokument eller att lära sig hur du extraherar resultaten från det returnerade samlingsobjektet. (Se [Programmatisk sammansättning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>Mer information om tjänsten Assembler finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DDX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Sammanfattning av steg {#summary-of-steps}

Gör så här om du vill sätta ihop ett PDF-dokument som innehåller bokmärken:

1. Inkludera projektfiler.
1. Skapa en PDF Assembler-klient.
1. Referera till ett befintligt DDX-dokument.
1. Referera till ett PDF-dokument som bokmärken läggs till i.
1. Referera till XML-dokumentet för bokmärket.
1. Lägg till PDF-dokumentet och bokmärkets XML-dokument i en kartsamling.
1. Ange körningsalternativ.
1. Sammanställ PDF-dokumentet.
1. Spara PDF-dokumentet som innehåller bokmärken.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (krävs om AEM Forms distribueras på JBoss)
* jbossall-client.jar (krävs om AEM Forms distribueras på JBoss)

Om AEM Forms används på en annan J2EE-programserver än JBoss måste du ersätta filerna adobe-utilities.jar och jbossall-client.jar med JAR-filer som är specifika för J2EE-programservern som AEM Forms distribueras på. Information om platsen för alla AEM Forms JAR-filer finns i [Inkludera Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)för AEM Forms.

**Skapa en PDF Assembler-klient**

Innan du programmässigt kan utföra en Assembler-åtgärd måste du skapa en Assembler-tjänstklient.

**Referera till ett befintligt DDX-dokument**

Det måste finnas referenser till ett DDX-dokument för att du ska kunna sammanställa ett PDF-dokument. Det här DDX-dokumentet måste innehålla `Bookmarks` elementet, som instruerar Assembler-tjänsten att sätta ihop ett PDF-dokument som innehåller bokmärken. (Se DDX-dokumentet som visades tidigare i det här avsnittet för ett exempel.)

**Referera till ett PDF-dokument som bokmärken läggs till i**

Referera till ett PDF-dokument som bokmärken läggs till i. Det spelar ingen roll om det refererade PDF-dokumentet redan innehåller bokmärken. Om `Bookmarks` elementet är underordnat PDF-källelementet ersätter bokmärkena dem som redan finns i PDF-källan. Om du vill behålla de befintliga bokmärkena måste du se till att `Bookmarks` det är en jämställd version av PDF-källelementet. Ta till exempel följande exempel:

```as3
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Referera till XML-dokument för bokmärken**

Om du vill montera ett PDF-dokument som innehåller nya bokmärken måste du referera till ett XML-dokument för bokmärken. Bokmärkets XML-dokument skickas till Assembler-tjänsten i samlingsobjektet för kartor. (Se ett exempel i det XML-dokument för bokmärken som visades tidigare i det här avsnittet.)

>[!NOTE]
>
>Se&quot;Bokmärkesspråk&quot; i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Lägga till PDF-dokumentet och bokmärkets XML-dokument i en kartsamling**

Du måste lägga till både det PDF-dokument som bokmärken läggs till i och det XML-dokument för bokmärken i samlingen Karta. Därför innehåller Map-samlingsobjektet två element: ett PDF-dokument och ett XML-dokument med bokmärken.

**Ange körningsalternativ**

Du kan ställa in körningsalternativ som styr beteendet för Assembler-tjänsten när den utför ett jobb. Du kan till exempel ange ett alternativ som instruerar Assembler-tjänsten att fortsätta bearbeta ett jobb om ett fel uppstår. Mer information om de körningsalternativ du kan ange finns i klassreferensen `AssemblerOptionSpec` i API-referens [för](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Sammanställ PDF-dokumentet**

Om du vill montera ett PDF-dokument som innehåller nya bokmärken använder du Assembler-tjänstens `invokeDDX` åtgärd. Orsaken till att du måste använda `invokeDDX` åtgärden i motsats till andra Assembler-åtgärder som t.ex. `invokeOneDocument` är att Assembler-tjänsten kräver ett XML-bokmärkesdokument som skickas inom Map-samlingsobjektet. Det här objektet är en parameter i `invokeDDX` åtgärden.

**Spara PDF-dokumentet som innehåller bokmärken**

Du måste extrahera resultaten från det returnerade mappningsobjektet och spara motsvarande PDF-dokument. (Se&quot;Extrahera resultaten&quot; i [Programmatisk sammansättning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Sammanställa PDF-dokument med bokmärken med Java API {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Sammanställa ett PDF-dokument med bokmärken med hjälp av Assembler Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en PDF Assembler-klient.

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper. (Se [Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Skapa ett `AssemblerServiceClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.

1. Referera till ett befintligt DDX-dokument.

   * Skapa ett `java.io.FileInputStream` objekt som representerar DDX-dokumentet med hjälp av dess konstruktor och skicka ett strängvärde som anger platsen för DDX-filen.
   * Skapa ett `com.adobe.idp.Document` objekt med hjälp av dess konstruktor och skicka `java.io.FileInputStream` objektet.

1. Referera till ett PDF-dokument som bokmärken läggs till i.

   * Skapa ett `java.io.FileInputStream` objekt med hjälp av dess konstruktor och skicka PDF-dokumentets plats.
   * Skapa ett `com.adobe.idp.Document` objekt med hjälp av dess konstruktor och skicka det `java.io.FileInputStream` objekt som innehåller PDF-dokumentet.

1. Referera till XML-dokumentet för bokmärket.

   * Skapa ett `java.io.FileInputStream` objekt med hjälp av dess konstruktor och skicka platsen för XML-filen som representerar bokmärkets XML-dokument.
   * Skapa ett `com.adobe.idp.Document` objekt och skicka `java.io.FileInputStream` objektet som innehåller PDF-dokumentet.

1. Lägg till PDF-dokumentet och bokmärkets XML-dokument i en kartsamling.

   * Skapa ett `java.util.Map` objekt som används för att lagra både PDF-indatadokumentet och XML-bokmärkesdokumentet.
   * Lägg till PDF-indatadokumentet genom att anropa `java.util.Map` objektets `put` metod och skicka följande argument:

      * Ett strängvärde som representerar nyckelnamnet. Detta värde måste matcha värdet för PDF-källelementet som anges i DDX-dokumentet.
      * Ett `com.adobe.idp.Document` objekt som innehåller PDF-indatadokumentet.
   * Lägg till bokmärkets XML-dokument genom att anropa `java.util.Map` objektets `put` metod och skicka följande argument:

      * Ett strängvärde som representerar nyckelnamnet. Värdet måste matcha värdet för källelementet för bokmärken som anges i DDX-dokumentet.
      * Ett `com.adobe.idp.Document` objekt som innehåller bokmärkets XML-dokument.


1. Ange körningsalternativ.

   * Skapa ett `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärsbehov genom att anropa en metod som tillhör `AssemblerOptionSpec` objektet. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar, anropar du `AssemblerOptionSpec` objektets `setFailOnError` metod och skickar `false`.

1. Sammanställ PDF-dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` metod och skicka följande obligatoriska värden:

   * Ett `com.adobe.idp.Document` objekt som representerar det DDX-dokument som ska användas
   * Ett `java.util.Map` objekt som innehåller både PDF-indatadokumentet och XML-dokumentet för bokmärket.
   * Ett `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objekt som anger körningsalternativen, inklusive standardteckensnitt och jobbloggsnivå
   Metoden returnerar `invokeDDX` ett `com.adobe.livecycle.assembler.client.AssemblerResult` objekt som innehåller resultatet av jobbet och eventuella undantag som inträffade.

1. Spara PDF-dokumentet som innehåller bokmärken.

   Utför följande åtgärder för att hämta det nya PDF-dokumentet:

   * Anropa `AssemblerResult` objektets `getDocuments` metod. Detta returnerar ett `java.util.Map` objekt.
   * Upprepa genom `java.util.Map` objektet tills du hittar det resulterande `com.adobe.idp.Document` objektet. (Du kan använda det PDF-resultatelement som anges i DDX-dokumentet för att hämta dokumentet.)
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att extrahera PDF-dokumentet.

**Se även**

[Snabbstart (SOAP-läge): Sammanställa PDF-dokument med bokmärken med Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Sammanställa PDF-dokument med bokmärken med hjälp av webbtjänstens API {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Sammanställa ett PDF-dokument med bokmärken med Assembler Service API (webbtjänsten):

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
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod och skicka bytearrayen, startpositionen och den strömlängd som ska läsas.
   * Fyll objektet `BLOB` genom att tilldela dess `MTOM` fält med innehållet i bytearrayen.

1. Referera till ett PDF-dokument som bokmärken läggs till i.

   * Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Objektet används `BLOB` för att lagra PDF-indata.
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar platsen för PDF-indatadokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod och skicka bytearrayen, startpositionen och den strömlängd som ska läsas.
   * Fyll objektet `BLOB` genom att tilldela dess `MTOM` fält med innehållet i bytearrayen.

1. Referera till XML-dokumentet för bokmärket.

   * Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Objektet används `BLOB` för att lagra XML-dokumentet för bokmärket.
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar platsen för PDF-indatadokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod och skicka bytearrayen, startpositionen och den strömlängd som ska läsas.
   * Fyll objektet `BLOB` genom att tilldela dess `MTOM` fält med innehållet i bytearrayen.

1. Lägg till PDF-dokumentet och bokmärkets XML-dokument i en kartsamling.

   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Det här samlingsobjektet används för att lagra PDF-indatadokumenten och XML-bokmärkesdokumentet.
   * Skapa ett `MyMapOf_xsd_string_To_xsd_anyType_Item` objekt för varje PDF-inmatningsdokument och ett XML-bokmärkesdokument.
   * Tilldela ett strängvärde som representerar nyckelnamnet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `key` fält. Detta värde måste matcha värdet för PDF-källelementet som anges i DDX-dokumentet.
   * Tilldela det `BLOB` objekt som lagrar PDF-dokumentet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `value` fält.
   * Lägg till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektet i `MyMapOf_xsd_string_To_xsd_anyType` objektet. Anropa `MyMapOf_xsd_string_To_xsd_anyType` objektets `Add` metod och skicka `MyMapOf_xsd_string_To_xsd_anyType` objektet. (Utför den här åtgärden för varje PDF-indatadokument och för bokmärkets XML-dokument.)

1. Ange körningsalternativ.

   * Skapa ett `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärskrav genom att tilldela ett värde till en datamedlem som tillhör `AssemblerOptionSpec` objektet. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar tilldelar du `false` till `AssemblerOptionSpec` objektets `failOnError` datamedlem.

1. Sammanställ PDF-dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` metod och skicka följande värden:

   * Ett `BLOB` objekt som representerar DDX-dokumentet
   * Arrayen `MyMapOf_xsd_string_To_xsd_anyType` som innehåller indatadokumenten
   * Ett `AssemblerOptionSpec` objekt som anger körningsalternativ
   Metoden returnerar ett `invokeDDX` `AssemblerResult` objekt som innehåller resultatet av jobbet och eventuella undantag som kan ha inträffat.

1. Spara PDF-dokumentet som innehåller bokmärken.

   Utför följande åtgärder för att hämta det nya PDF-dokumentet:

   * Få åtkomst till `AssemblerResult` objektets `documents` fält, som är ett `Map` objekt som innehåller PDF-dokumentets resultat.
   * Iterera genom objektet tills du hittar den tangent som matchar namnet på det resulterande dokumentet. `Map` Sedan konverterar du arraymedlemmens `value` till en `BLOB`.
   * Extrahera de binära data som representerar PDF-dokumentet genom att komma åt objektets `BLOB` `MTOM` fält. Detta returnerar en array med byte som du kan skriva till en PDF-fil.

**Se även**

[Anropa AEM-formulär med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
