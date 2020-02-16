---
title: Sammanställa icke-interaktiva PDF-dokument
seo-title: Sammanställa icke-interaktiva PDF-dokument
description: 'null'
seo-description: 'null'
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Sammanställa icke-interaktiva PDF-dokument {#assembling-non-interactive-pdf-documents}

Du kan sätta ihop ett icke-interaktivt PDF-dokument när du använder ett interaktivt PDF-formulär som indata. Anta alltså att du har ett formulär som användare kan använda för att ange data i sina fält. Du kan skicka formuläret till Assembler-tjänsten, vilket gör att Assembler-tjänsten returnerar ett PDF-dokument som inte kan användas för att ange data i dess fält. Det här dokumentet är ett icke-interaktivt PDF-formulär. Följande bild visar till exempel en låneansökan som representerar ett interaktivt formulär.

Anta att följande DDX-dokument används för den här diskussionen.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

Observera att källattributet är tilldelat värdet i det här DDX-dokumentet `inDoc`. Om bara ett PDF-indatadokument skickas till Assembler-tjänsten och ett PDF-dokument returneras, och du anropar `invokeOneDocument` åtgärden, tilldelar du värdet `inDoc` till PDF-källattributet. När du anropar `invokeOneDocument` åtgärden är `inDoc` värdet en fördefinierad nyckel som måste anges i DDX-dokumentet.

Om du skickar två eller flera PDF-indatadokument till Assembler-tjänsten kan du däremot anropa `invokeDDX` åtgärden. I så fall tilldelar du filnamnet för PDF-indatadokumentet till `source` -attributet.

Det här DDX-dokumentet innehåller `NoXFA` elementet, som instruerar Assembler-tjänsten att returnera ett icke-interaktivt PDF-dokument.

Med Assembler-tjänsten kan du sammanställa icke-interaktiva PDF-dokument utan att Output-tjänsten ingår i AEM-formulärinstallationen om PDF-indatadokumentet är baserat på ett Acrobat-formulär eller ett statiskt XFA-formulär. Om PDF-indatadokumentet är ett dynamiskt XFA-formulär måste utdatatjänsten ingå i installationen av AEM-formulär. Om utdatatjänsten inte ingår i AEM-formulärsinstallationen när ett dynamiskt XFA-formulär sätts ihop genereras ett undantag. Se [Skapa dokumentutdataströmmar](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>Innan du läser det här avsnittet bör du känna till hur du sammanställer PDF-dokument med hjälp av tjänsten Assembler. I det här avsnittet beskrivs inte begrepp, till exempel att skapa ett samlingsobjekt som innehåller indatadokument eller att lära sig hur du extraherar resultaten från det returnerade samlingsobjektet. (Se [Sammanställa PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)programmatiskt.)

>[!NOTE]
>
>Mer information om tjänsten Assembler finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DDX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Sammanfattning av steg {#summary-of-steps}

Så här sammanställer du ett icke-interaktivt PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en PDF Assembler-klient.
1. Referera till ett befintligt DDX-dokument.
1. Referera till ett interaktivt PDF-dokument.
1. Ange körningsalternativ.
1. Sammanställ PDF-dokumentet.
1. Spara det icke-interaktiva PDF-dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (krävs om AEM Forms distribueras på JBoss)
* jbossall-client.jar (krävs om AEM Forms distribueras på JBoss)

Om AEM Forms används på en annan J2EE-programserver än JBoss måste du ersätta filerna adobe-utilities.jar och jbossall-client.jar med JAR-filer som är specifika för J2EE-programservern som AEM Forms distribueras på.

**Skapa en Assembler-klient**

Innan du programmässigt kan utföra en Assembler-åtgärd måste du skapa en Assembler-tjänstklient.

**Referera till ett befintligt DDX-dokument**

Det måste finnas referenser till ett DDX-dokument för att du ska kunna sammanställa ett PDF-dokument. Det här DDX-dokumentet måste innehålla `NoXFA` elementet, som instruerar Assembler-tjänsten att returnera ett icke-interaktivt PDF-dokument.

**Referera till ett interaktivt PDF-dokument**

Ett interaktivt PDF-dokument måste refereras till och skickas till Assembler-tjänsten för att få tillbaka ett icke-interaktivt PDF-dokument.

**Ange körningsalternativ**

Du kan ställa in körningsalternativ som styr beteendet för Assembler-tjänsten när den utför ett jobb. Du kan till exempel ange ett alternativ som instruerar Assembler-tjänsten att fortsätta bearbeta ett jobb om ett fel uppstår.

**Sammanställ PDF-dokumentet**

När du har skapat Assembler-tjänstklienten, refererat till DDX-dokumentet, refererat till ett interaktivt PDF-dokument och angett körningsalternativ, kan du anropa `invokeOneDocument` åtgärden. Eftersom bara ett PDF-indatadokument skickas till Assembler-tjänsten och ett dokument returneras, kan du använda `invokeOneDocument` åtgärden i stället för `invokeDDX` åtgärden.

**Spara det icke-interaktiva PDF-dokumentet**

Om bara ett PDF-dokument skickas till Assembler-tjänsten returnerar Assembler-tjänsten ett enstaka dokument i stället för ett samlingsobjekt. Det innebär att när `invokeOneDocument` åtgärden anropas returneras ett enda dokument. Eftersom det DDX-dokument som det här avsnittet refererar till innehåller instruktioner för att skapa ett icke-interaktivt PDF-dokument, returnerar Assembler-tjänsten ett icke-interaktivt PDF-dokument som kan sparas som en PDF-fil.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Sammanställa ett icke-interaktivt PDF-dokument med Java API {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Sammanställa ett icke-interaktivt PDF-dokument med Assembler Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en Assembler-klient.

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa ett `AssemblerServiceClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.

1. Referera till ett befintligt DDX-dokument.

   * Skapa ett `java.io.FileInputStream` objekt som representerar DDX-dokumentet med hjälp av dess konstruktor och skicka ett strängvärde som anger platsen för DDX-filen.
   * Skapa ett `com.adobe.idp.Document` objekt med hjälp av dess konstruktor och skicka `java.io.FileInputStream` objektet.

1. Referera till ett interaktivt PDF-dokument.

   * Skapa ett `java.io.FileInputStream` objekt med hjälp av dess konstruktor och skicka platsen för ett interaktivt PDF-dokument.
   * Skapa ett `com.adobe.idp.Document` objekt och skicka `java.io.FileInputStream` objektet som innehåller PDF-dokumentet. Detta `com.adobe.idp.Document` objekt skickas till `invokeOneDocument` metoden.

1. Ange körningsalternativ.

   * Skapa ett `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärsbehov genom att anropa en metod som tillhör `AssemblerOptionSpec` objektet. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar, anropar du `AssemblerOptionSpec` objektets `setFailOnError` metod och skickar `false`.

1. Sammanställ PDF-dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeOneDocument` metod och skicka följande värden:

   * Ett `com.adobe.idp.Document` objekt som representerar DDX-dokumentet. Kontrollera att det här DDX-dokumentet innehåller värdet `inDoc` för PDF-källelementet.
   * Ett `com.adobe.idp.Document` objekt som innehåller det interaktiva PDF-dokumentet.
   * Ett `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objekt som anger körningsalternativen, inklusive standardteckensnitt och jobbloggsnivå.
   Metoden returnerar `invokeOneDocument` ett `com.adobe.idp.Document` objekt som innehåller ett icke-interaktivt PDF-dokument.

1. Spara det icke-interaktiva PDF-dokumentet.

   * Skapa ett `java.io.File` objekt och kontrollera att filnamnstillägget är .pdf.
   * Anropa `Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` objektet till filen. Se till att du använder det `Document` objekt som `invokeOneDocument` metoden returnerade.

* &quot;Snabbstart (SOAP-läge): Sammanställa ett icke-interaktivt PDF-dokument med Java API&quot;

## Sammanställa ett icke-interaktivt PDF-dokument med webbtjänstens API {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Sammanställa ett icke-interaktivt PDF-dokument med Assembler Service API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen för servern som är värd för AEM Forms.

1. Skapa en Assembler-klient.

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

1. Referera till ett interaktivt PDF-dokument.

   * Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Objektet används `BLOB` för att lagra PDF-indatadokumentet. Detta `BLOB` objekt skickas till `invokeOneDocument` som ett argument.
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar platsen för PDF-indatadokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll objektet `BLOB` genom att tilldela dess `MTOM` fält med innehållet i bytearrayen.

1. Ange körningsalternativ.

   * Skapa ett `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärskrav genom att tilldela ett värde till en datamedlem som tillhör `AssemblerOptionSpec` objektet. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar tilldelar du `false` till `AssemblerOptionSpec` objektets `failOnError` datamedlem.

1. Sammanställ PDF-dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeOneDocument` metod och skicka följande värden:

   * Ett `BLOB` objekt som representerar DDX-dokumentet
   * Ett `BLOB` objekt som representerar det interaktiva PDF-dokumentet
   * Ett `AssemblerOptionSpec` objekt som anger körningsalternativ
   Metoden returnerar `invokeOneDocument` ett `BLOB` objekt som innehåller ett icke-interaktivt PDF-dokument.

1. Spara det icke-interaktiva PDF-dokumentet.

   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det icke-interaktiva PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i det `BLOB` objekt som `invokeOneDocument` metoden returnerade. Fyll i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` fält.
   * Skapa ett `System.IO.BinaryWriter` objekt genom att anropa dess konstruktor och skicka `System.IO.FileStream` objektet.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` metod och skicka bytearrayen.

* &quot;Snabbstart (MTOM): Sammanställa ett icke-interaktivt PDF-dokument med webbtjänstens API&quot;.

**Se även**

[Anropa AEM-formulär med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
