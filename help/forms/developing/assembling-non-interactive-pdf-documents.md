---
title: Sammanställa icke-interaktiva PDF-dokument
seo-title: Assembling Non-Interactive PDF Documents
description: Använd ett icke-interaktivt PDF-formulär som indata för att sammanfoga ett icke-interaktivt PDF-dokument med Java API och Web Service API.
seo-description: Use a non-interactive PDF form as input to assemble a non-interactive PDF document using the Java API and Web Service API.
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
role: Developer
exl-id: 4677b9e5-3811-4de3-b4f4-9574b5898486
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 0%

---

# Sammanställa icke-interaktiva PDF-dokument {#assembling-non-interactive-pdf-documents}

Du kan sätta ihop ett icke-interaktivt PDF-dokument när du använder ett interaktivt PDF-formulär som indata. Anta alltså att du har ett formulär som användare kan använda för att ange data i sina fält. Du kan skicka formuläret till Assembler-tjänsten, vilket gör att Assembler-tjänsten returnerar ett PDF-dokument som hindrar användare från att ange data i sina fält. Det här dokumentet är ett icke-interaktivt PDF-formulär. Följande bild visar till exempel en låneansökan som representerar ett interaktivt formulär.

Anta att följande DDX-dokument används för den här diskussionen.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

Observera att källattributet är tilldelat värdet i det här DDX-dokumentet `inDoc`. I situationer där endast ett indatadokument i PDF skickas till Assembler-tjänsten och ett PDF-dokument returneras, och du anropar `invokeOneDocument` åtgärd, tilldela värdet `inDoc` till källattributet PDF. Vid anrop av `invokeOneDocument` operation, `inDoc` värde är en fördefinierad nyckel som måste anges i DDX-dokumentet.

Om du skickar två eller flera indatadokument till PDF till Assembler-tjänsten kan du däremot anropa `invokeDDX` operation. I det här fallet tilldelar du filnamnet för indata-PDF-dokumentet till `source` -attribut.

Det här DDX-dokumentet innehåller `NoXFA` som instruerar Assembler-tjänsten att returnera ett icke-interaktivt PDF-dokument.

Med Assembler-tjänsten kan du samla ihop icke-interaktiva PDF-dokument utan att Output-tjänsten är en del av installationen av AEM formulär, om PDF-indatadokumentet är baserat på ett Acrobat-formulär eller ett statiskt XFA-formulär. Om PDF-indatadokumentet är ett dynamiskt XFA-formulär måste utdatatjänsten ingå i installationen av AEM formulär. Om utdatatjänsten inte är en del av installationen av AEM formulär när ett dynamiskt XFA-formulär sätts ihop genereras ett undantag. Se [Skapa dokumentutdataströmmar](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>Innan du läser det här avsnittet bör du känna till hur du sammanställer PDF-dokument med hjälp av tjänsten Assembler. I det här avsnittet beskrivs inte koncept, t.ex. att skapa ett samlingsobjekt som innehåller indatadokument eller att lära sig hur du extraherar resultaten från det returnerade samlingsobjektet. (Se [Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Mer information om Assembler-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Sammanfattning av steg {#summary-of-steps}

Gör så här om du vill sätta ihop ett icke-interaktivt PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en PDF Assembler-klient.
1. Referera till ett befintligt DDX-dokument.
1. Referera till ett interaktivt PDF-dokument.
1. Ange körningsalternativ.
1. Sammanställ dokumentet PDF.
1. Spara det icke-interaktiva PDF-dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

Om AEM Forms körs på en annan J2EE-programserver än JBoss måste du ersätta filerna adobe-utilities.jar och jbossall-client.jar med JAR-filer som är specifika för J2EE-programservern som AEM Forms är distribuerad på.

**Skapa en Assembler-klient**

Innan du programmässigt kan utföra en Assembler-åtgärd måste du skapa en Assembler-tjänstklient.

**Referera till ett befintligt DDX-dokument**

Ett DDX-dokument måste refereras till för att du ska kunna montera ett PDF-dokument. Det här DDX-dokumentet måste innehålla `NoXFA` som instruerar Assembler-tjänsten att returnera ett icke-interaktivt PDF-dokument.

**Referera till ett interaktivt PDF-dokument**

Ett interaktivt PDF-dokument måste refereras till och skickas till Assembler-tjänsten för att du ska kunna få tillbaka ett icke-interaktivt PDF-dokument.

**Ange körningsalternativ**

Du kan ställa in körningsalternativ som styr beteendet för Assembler-tjänsten när den utför ett jobb. Du kan till exempel ange ett alternativ som instruerar Assembler-tjänsten att fortsätta bearbeta ett jobb om ett fel uppstår.

**Sammanställa dokumentet PDF**

När du har skapat Assembler-tjänstklienten, refererat till DDX-dokumentet, refererat till ett interaktivt PDF-dokument och angett körningsalternativ, kan du anropa `invokeOneDocument` operation. Eftersom bara ett indatadokument i PDF skickas till Assembler-tjänsten och ett enda dokument returneras, kan du använda `invokeOneDocument` i stället för `invokeDDX` operation.

**Spara det icke-interaktiva PDF-dokumentet**

Om bara ett enda PDF-dokument skickas till Assembler-tjänsten returnerar Assembler-tjänsten ett enstaka dokument i stället för ett samlingsobjekt. Det vill säga när du anropar `invokeOneDocument` returneras ett enda dokument. Eftersom det DDX-dokument som det här avsnittet refererar till innehåller anvisningar om hur du skapar ett icke-interaktivt PDF-dokument, returnerar Assembler-tjänsten ett icke-interaktivt PDF-dokument som kan sparas som en PDF-fil.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Sammanställa ett icke-interaktivt PDF-dokument med Java API {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Sammanställa ett icke-interaktivt PDF-dokument med hjälp av Assembler Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en Assembler-klient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `AssemblerServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Referera till ett befintligt DDX-dokument.

   * Skapa en `java.io.FileInputStream` -objekt som representerar DDX-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för DDX-filen.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Referera till ett interaktivt PDF-dokument.

   * Skapa en `java.io.FileInputStream` genom att använda dess konstruktor och skicka platsen för ett interaktivt PDF-dokument.
   * Skapa en `com.adobe.idp.Document` -objektet och skicka `java.io.FileInputStream` -objekt som innehåller dokumentet PDF. Detta `com.adobe.idp.Document` objektet skickas till `invokeOneDocument` -metod.

1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärsbehov genom att anropa en metod som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera tjänsten Assembler att fortsätta bearbeta ett jobb när ett fel inträffar, ska du anropa `AssemblerOptionSpec` objektets `setFailOnError` metod och skicka `false`.

1. Sammanställ dokumentet PDF.

   Anropa `AssemblerServiceClient` objektets `invokeOneDocument` och skicka följande värden:

   * A `com.adobe.idp.Document` -objekt som representerar DDX-dokumentet. Kontrollera att det här DDX-dokumentet innehåller värdet `inDoc` för källelementet PDF.
   * A `com.adobe.idp.Document` det objekt som innehåller det interaktiva PDF-dokumentet.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` -objekt som anger körningsalternativ, inklusive standardteckensnitt och jobbloggsnivå.

   The `invokeOneDocument` returnerar en `com.adobe.idp.Document` objekt som innehåller ett icke-interaktivt PDF-dokument.

1. Spara det icke-interaktiva PDF-dokumentet.

   * Skapa en `java.io.File` och se till att filnamnstillägget är .pdf.
   * Anropa `Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` till filen. Se till att du använder `Document` det objekt som `invokeOneDocument` returnerad metod.

* &quot;Snabbstart (SOAP-läge): Sammanställa ett icke-interaktivt PDF-dokument med Java API&quot;

## Sammanställa ett icke-interaktivt PDF-dokument med hjälp av webbtjänstens API {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Sammanställa ett icke-interaktivt PDF-dokument med Assembler Service API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en Assembler-klient.

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

1. Referera till ett interaktivt PDF-dokument.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra indatadokumentet i PDF. Detta `BLOB` objektet skickas till `invokeOneDocument` som ett argument.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för indata-PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärskrav genom att tilldela ett värde till en datamedlem som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar tilldelar du `false` till `AssemblerOptionSpec` objektets `failOnError` datamedlem.

1. Sammanställ dokumentet PDF.

   Anropa `AssemblerServiceClient` objektets `invokeOneDocument` och skicka följande värden:

   * A `BLOB` objekt som representerar DDX-dokumentet
   * A `BLOB` objekt som representerar det interaktiva PDF-dokumentet
   * An `AssemblerOptionSpec` objekt som anger körningsalternativ

   The `invokeOneDocument` returnerar en `BLOB` objekt som innehåller ett icke-interaktivt PDF-dokument.

1. Spara det icke-interaktiva PDF-dokumentet.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det icke-interaktiva PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `BLOB` det objekt som `invokeOneDocument` returnerad metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` fält.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

* &quot;Snabbstart (MTOM): Sammanställa ett icke-interaktivt PDF-dokument med hjälp av webbtjänstens API.&quot;

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
