---
title: Sammanställa PDF-dokument med bokmärken
seo-title: Assembling PDF Documents with Bookmarks
description: Använd Assembler-tjänsten för att ändra ett PDF-dokument som innehåller bokmärken för att inkludera bokmärken med Java API och Web Service API.
seo-description: Use the Assembler service to modify a PDF document that does contain bookmarks to include bookmarks using the Java API and the Web Service API.
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
role: Developer
exl-id: 2b938410-f51b-420b-b5d4-2ed13ec29c5a
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 0%

---

# Sammanställa PDF-dokument med bokmärken {#assembling-pdf-documents-with-bookmarks}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

Du kan montera ett PDF-dokument som innehåller bokmärken. Anta till exempel att du har ett PDF-dokument som inte innehåller bokmärken och du vill ändra det genom att ange bokmärken. Med Assembler-tjänsten kan du skicka ett PDF-dokument som inte innehåller bokmärken och få tillbaka ett PDF-dokument som innehåller bokmärken.

Bokmärken innehåller följande egenskaper:

* En titel som visas som text på skärmen.
* En åtgärd som anger vad som händer när en användare klickar på bokmärket. En vanlig åtgärd för ett bokmärke är att flytta till en annan plats i det aktuella dokumentet eller öppna ett annat PDF-dokument, men andra åtgärder kan anges.

Anta att följande DDX-dokument används för den här diskussionen.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

Observera att källattributet är tilldelat värdet i det här DDX-dokumentet `Loan.pdf`. Det här DDX-dokumentet anger att ett enda PDF-dokument skickas till Assembler-tjänsten. När du sammanställer ett PDF-dokument med bokmärken måste du ange ett XML-dokument för bokmärken som beskriver bokmärkena i resultatdokumentet. Om du vill ange ett XML-dokument för bokmärken kontrollerar du att `Bookmarks` -elementet anges i ditt DDX-dokument.

I det här exemplet är DDX-dokumentet `Bookmarks` element specificeras `doc2` som värdet. Det här värdet anger att indatamappningen som skickas till Assembler-tjänsten innehåller en nyckel med namnet `doc2`. Värdet för `doc2` nyckel är en `com.adobe.idp.Document` det värde som representerar XML-dokumentet för bokmärket. (Se&quot;Bokmärkesspråk&quot; i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).)

I det här avsnittet används följande språk för XML-bokmärken för att sätta ihop ett PDF-dokument som innehåller bokmärken.

```xml
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

Lägg märke till det Action-element som definierar åtgärden som utförs när en användare klickar på bokmärket i det här XML-bokmärkesdokumentet. Under elementet Action (Åtgärd) är det Launch-element som startar program, till exempel NotePad, och öppnar filer, till exempel PDF-filer. Om du vill öppna en PDF-fil måste du använda det File-element som anger vilken fil som ska öppnas. I t.ex. den XML-fil för bokmärke som anges i det här avsnittet heter filen som öppnas LoanDetails.pdf.

>[!NOTE]
>
>Fullständig information om åtgärder som stöds finns i &quot; `Action` element&quot; i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

Med tanke på det DDX-dokument som anges i det här avsnittet och XML-filen för bokmärken som indata, sammanställer Assembler-tjänsten ett PDF-dokument som innehåller följande bokmärken.

![aw_aw_bmark](assets/aw_aw_bmark.png)

När en användare klickar på *Öppna låninformation* bokmärke öppnas filen LoanDetails.pdf. På samma sätt när användaren klickar på *Starta NotePad* bokmärke, NotePad har startats.

>[!NOTE]
>
>Innan du läser det här avsnittet bör du känna till hur du sammanställer PDF-dokument med hjälp av tjänsten Assembler. I det här avsnittet beskrivs inte begrepp, till exempel att skapa ett samlingsobjekt som innehåller indatadokument eller att lära sig hur du extraherar resultaten från det returnerade samlingsobjektet. (Se [Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>Mer information om Assembler-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Sammanfattning av steg {#summary-of-steps}

Gör så här om du vill sätta ihop ett PDF-dokument som innehåller bokmärken:

1. Inkludera projektfiler.
1. Skapa en PDF Assembler-klient.
1. Referera till ett befintligt DDX-dokument.
1. Referera till ett PDF-dokument som bokmärken läggs till i.
1. Referera till XML-dokumentet för bokmärket.
1. Lägg till PDF-dokumentet och bokmärkets XML-dokument i en kartsamling.
1. Ange körningsalternativ.
1. Sammanställ dokumentet PDF.
1. Spara det PDF-dokument som innehåller bokmärken.

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

Ett DDX-dokument måste refereras till för att du ska kunna montera ett PDF-dokument. Det här DDX-dokumentet måste innehålla `Bookmarks` -element, som instruerar Assembler-tjänsten att sätta ihop ett PDF som innehåller bokmärken. (Se DDX-dokumentet som visades tidigare i det här avsnittet för ett exempel.)

**Referera till ett PDF-dokument som bokmärken läggs till i**

Referera till ett PDF-dokument som bokmärken läggs till i. Det spelar ingen roll om det refererade PDF-dokumentet redan innehåller bokmärken. Om `Bookmarks` är ett underordnat element till källelementet i PDF och bokmärkena kommer att ersätta dem som redan finns i källan i PDF. Om du vill behålla de befintliga bokmärkena måste du dock se till att `Bookmarks` är en jämställd nivå i källelementet PDF. Ta till exempel följande exempel:

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Referera till XML-dokument för bokmärken**

Om du vill montera ett PDF som innehåller nya bokmärken måste du referera till ett XML-bokmärkesdokument. Bokmärkets XML-dokument skickas till Assembler-tjänsten i samlingsobjektet för kartor. (Se ett exempel i det XML-dokument för bokmärken som visades tidigare i det här avsnittet.)

>[!NOTE]
>
>Se&quot;Bokmärkesspråk&quot; i dialogrutan [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Lägg till PDF-dokumentet och bokmärkets XML-dokument i en kartsamling**

Du måste lägga till både det PDF-dokument som bokmärken läggs till i och bokmärkets XML-dokument i kartsamlingen. Därför innehåller Map-samlingsobjektet två element: ett PDF-dokument och ett XML-dokument för bokmärken.

**Ange körningsalternativ**

Du kan ställa in körningsalternativ som styr beteendet för Assembler-tjänsten när den utför ett jobb. Du kan till exempel ange ett alternativ som instruerar Assembler-tjänsten att fortsätta bearbeta ett jobb om ett fel uppstår. Mer information om de körningsalternativ du kan ange finns i `AssemblerOptionSpec` klassreferens i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Sammanställa dokumentet PDF**

Om du vill montera ett PDF-dokument som innehåller nya bokmärken använder du Assembler-tjänstens `invokeDDX` operation. Orsaken till att du måste använda `invokeDDX` till skillnad från andra Assembler-tjänster som `invokeOneDocument` Detta beror på att Assembler-tjänsten kräver ett XML-bokmärkesdokument som skickas inom Map-samlingsobjektet. Det här objektet är en parameter i `invokeDDX` operation.

**Spara PDF-dokumentet som innehåller bokmärken**

Du måste extrahera resultaten från det returnerade mappningsobjektet och spara motsvarande PDF-dokument. (Se&quot;Extrahera resultat&quot; i [Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Sammanställa PDF-dokument med bokmärken med Java API {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Sammanställa ett PDF-dokument med bokmärken med hjälp av Assembler Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en PDF Assembler-klient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper. (Se [Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Skapa en `AssemblerServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Referera till ett befintligt DDX-dokument.

   * Skapa en `java.io.FileInputStream` som representerar DDX-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för DDX-filen.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Referera till ett PDF-dokument som bokmärken läggs till i.

   * Skapa en `java.io.FileInputStream` genom att använda konstruktorn och skicka PDF-dokumentets placering.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` som innehåller dokumentet PDF.

1. Referera till XML-dokumentet för bokmärket.

   * Skapa en `java.io.FileInputStream` genom att använda dess konstruktor och skicka platsen för XML-filen som representerar bokmärkets XML-dokument.
   * Skapa en `com.adobe.idp.Document` -objektet och skicka `java.io.FileInputStream` som innehåller dokumentet PDF.

1. Lägg till PDF-dokumentet och bokmärkets XML-dokument i en kartsamling.

   * Skapa en `java.util.Map` objekt som används för att lagra både indata-PDF-dokumentet och bokmärkes-XML-dokumentet.
   * Lägg till indatadokumentet i PDF genom att anropa `java.util.Map` objektets `put` och skicka följande argument:

      * Ett strängvärde som representerar nyckelnamnet. Detta värde måste matcha värdet för källelementet PDF som anges i DDX-dokumentet.
      * A `com.adobe.idp.Document` som innehåller indatadokumentet PDF.
   * Lägg till XML-bokmärkesdokumentet genom att anropa `java.util.Map` objektets `put` och skicka följande argument:

      * Ett strängvärde som representerar nyckelnamnet. Värdet måste matcha värdet för källelementet för bokmärken som anges i DDX-dokumentet.
      * A `com.adobe.idp.Document` -objekt som innehåller bokmärkets XML-dokument.


1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärsbehov genom att anropa en metod som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera tjänsten Assembler att fortsätta bearbeta ett jobb när ett fel inträffar, ska du anropa `AssemblerOptionSpec` objektets `setFailOnError` metod och skicka `false`.

1. Sammanställ dokumentet PDF.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` och skicka följande obligatoriska värden:

   * A `com.adobe.idp.Document` objekt som representerar det DDX-dokument som ska användas
   * A `java.util.Map` -objekt som innehåller både indatadokumentet och XML-dokumentet för bokmärket.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objekt som anger körningsalternativ, inklusive standardteckensnitt och jobbloggsnivå

   The `invokeDDX` returnerar en `com.adobe.livecycle.assembler.client.AssemblerResult` som innehåller resultatet av jobbet och eventuella undantag som inträffade.

1. Spara det PDF-dokument som innehåller bokmärken.

   Utför följande åtgärder för att hämta det nya PDF-dokumentet:

   * Anropa `AssemblerResult` objektets `getDocuments` -metod. Detta returnerar `java.util.Map` -objekt.
   * Iterera genom `java.util.Map` tills du hittar resultatet `com.adobe.idp.Document` -objekt. (Du kan använda resultatelementet PDF som anges i DDX-dokumentet för att hämta dokumentet.)
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
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Referera till ett PDF-dokument som bokmärken läggs till i.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra indata PDF.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för indata-PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Referera till XML-dokumentet för bokmärket.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra XML-dokumentet för bokmärket.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för indata-PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Lägg till PDF-dokumentet och bokmärkets XML-dokument i en kartsamling.

   * Skapa en `MyMapOf_xsd_string_To_xsd_anyType` -objekt. Det här samlingsobjektet används för att lagra indata-PDF-dokument och bokmärkes-XML-dokument.
   * För varje inmatningsdokument i PDF och bokmärkes-XML-dokument skapar du ett `MyMapOf_xsd_string_To_xsd_anyType_Item` -objekt.
   * Tilldela ett strängvärde som representerar nyckelnamnet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `key` fält. Detta värde måste matcha värdet för källelementet PDF som anges i DDX-dokumentet.
   * Tilldela `BLOB` objekt som lagrar PDF-dokumentet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `value` fält.
   * Lägg till `MyMapOf_xsd_string_To_xsd_anyType_Item` objekt till `MyMapOf_xsd_string_To_xsd_anyType` -objekt. Anropa `MyMapOf_xsd_string_To_xsd_anyType` objektets `Add` och skicka `MyMapOf_xsd_string_To_xsd_anyType` -objekt. (Utför den här åtgärden för varje inmatningsdokument i PDF och för bokmärkets XML-dokument.)

1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärskrav genom att tilldela ett värde till en datamedlem som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar tilldelar du `false` till `AssemblerOptionSpec` objektets `failOnError` datamedlem.

1. Sammanställ dokumentet PDF.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` och skicka följande värden:

   * A `BLOB` objekt som representerar DDX-dokumentet
   * The `MyMapOf_xsd_string_To_xsd_anyType` array som innehåller indatadokumenten
   * An `AssemblerOptionSpec` objekt som anger körningsalternativ

   The `invokeDDX` returnerar en `AssemblerResult` som innehåller resultatet av jobbet och eventuella undantag som kan ha inträffat.

1. Spara det PDF-dokument som innehåller bokmärken.

   Utför följande åtgärder för att hämta det nya PDF-dokumentet:

   * Öppna `AssemblerResult` objektets `documents` fält, vilket är ett `Map` -objekt som innehåller de resulterande PDF-dokumenten.
   * Iterera genom `Map` tills du hittar nyckeln som matchar namnet på det resulterande dokumentet. Sätt sedan den arraymedlemmens `value` till `BLOB`.
   * Extrahera de binära data som representerar PDF-dokumentet genom att öppna dess `BLOB` objektets `MTOM` fält. Detta returnerar en array med byte som du kan skriva ut till en PDF-fil.

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
