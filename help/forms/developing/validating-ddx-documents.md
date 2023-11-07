---
title: Validerar DDX-dokument
seo-title: Validating DDX Documents
description: Validera ett DDX-dokument programmatiskt med Java API och Web Service API.
seo-description: Validate a DDX document programmatically using the Java API and the Web Service API.
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 0%

---

# Validerar DDX-dokument {#validating-ddx-documents}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

Du kan programmässigt validera ett DDX-dokument som används av Assembler-tjänsten. Med andra ord kan du med hjälp av API:t för Assembler-tjänsten avgöra om ett DDX-dokument är giltigt eller inte. Om du till exempel uppgraderade från en tidigare version av AEM Forms och vill vara säker på att ditt DDX-dokument är giltigt, kan du validera det med hjälp av Assembler-tjänst-API:t.

>[!NOTE]
>
>Mer information om Assembler-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Sammanfattning av steg {#summary-of-steps}

Så här validerar du ett DX-dokument:

1. Inkludera projektfiler.
1. Skapa en Assembler-klient.
1. Referera till ett befintligt DDX-dokument.
1. Ange körningsalternativ för att validera DDX-dokumentet.
1. Utför valideringen.
1. Spara valideringsresultaten i en loggfil.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

Om AEM Forms körs på en annan J2EE-programserver än JBoss måste du ersätta filerna adobe-utilities.jar och jbossall-client.jar med JAR-filer som är specifika för J2EE-programservern som AEM Forms är distribuerad på.

**Skapa en PDF Assembler-klient**

Innan du programmässigt kan utföra en Assembler-åtgärd måste du skapa en Assembler-tjänstklient.

**Referera till ett befintligt DDX-dokument**

Om du vill validera ett DDX-dokument måste du referera till ett befintligt DDX-dokument.

**Ange körningsalternativ för validering av DDX-dokumentet**

När du validerar ett DX-dokument måste du ange specifika körningsalternativ som instruerar Assembler-tjänsten att validera DX-dokumentet i stället för att köra det. Du kan också öka mängden information som Assembler-tjänsten skriver till loggfilen.

**Utför valideringen**

När du har skapat Assembler-tjänstklienten, refererat till DDX-dokumentet och angett körningsalternativ, kan du anropa `invokeDDX` åtgärd för att validera DDX-dokumentet. När du validerar DDX-dokumentet kan du skicka det `null` som map-parametern (den här parametern lagrar vanligtvis PDF-dokument som Assembler kräver för att utföra de åtgärder som anges i DDX-dokumentet).

Om valideringen misslyckas genereras ett undantag och loggfilen innehåller information som förklarar varför DDX-dokumentet är ogiltigt kan hämtas från `OperationException` -instans. Efter den grundläggande XML-tolkningen och schemakontrollen utförs valideringen mot DDX-specifikationen. Alla fel som finns i DDX-dokumentet anges i loggen.

**Spara valideringsresultaten i en loggfil**

Assembler-tjänsten returnerar valideringsresultaten som du kan skriva till en XML-loggfil. Hur detaljerad Assembler-tjänsten skriver till loggfilen beror på vilket körningsalternativ du anger.

**Se även**

[Validera ett DX-dokument med Java API](#validate-a-ddx-document-using-the-java-api)

[Validera ett DX-dokument med webbtjänstens API](#validate-a-ddx-document-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Validera ett DX-dokument med Java API {#validate-a-ddx-document-using-the-java-api}

Validera ett DX-dokument med Assembler Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en PDF Assembler-klient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `AssemblerServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Referera till ett befintligt DDX-dokument.

   * Skapa en `java.io.FileInputStream` -objekt som representerar DDX-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för DDX-filen.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ange körningsalternativ för att validera DDX-dokumentet.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange det körningsalternativ som instruerar Assembler-tjänsten att validera DDX-dokumentet genom att anropa `AssemblerOptionSpec` objektets setValidateOnly-metod och skicka `true`.
   * Ange mängden information som Assembler-tjänsten skriver till loggfilen genom att anropa `AssemblerOptionSpec` objektets `getLogLevel` och att skicka ett strängvärde uppfyller dina krav. När du validerar ett DX-dokument vill du att mer information ska skrivas till loggfilen som ska vara till hjälp vid valideringsprocessen. Därför kan du skicka värdet `FINE` eller `FINER`.

1. Utför valideringen.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` och skicka följande värden:

   * A `com.adobe.idp.Document` -objekt som representerar DDX-dokumentet.
   * Värdet `null` för det java.io.Map-objekt som vanligtvis lagrar PDF-dokument.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` -objekt som anger körningsalternativen.

   The `invokeDDX` returnerar en `AssemblerResult` -objekt som innehåller information som anger om DDX-dokumentet är giltigt.

1. Spara valideringsresultaten i en loggfil.

   * Skapa en `java.io.File` och se till att filnamnstillägget är .xml.
   * Anropa `AssemblerResult` objektets `getJobLog` -metod. Den här metoden returnerar en `com.adobe.idp.Document` -instans som innehåller valideringsinformation.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att kopiera innehållet i `com.adobe.idp.Document` till filen.

   >[!NOTE]
   >
   >Om DDX-dokumentet är ogiltigt kan du `OperationException` kastas. I catch-satsen kan du anropa `OperationException` objektets `getJobLog` -metod.

**Se även**

[Validerar DDX-dokument](#validating-ddx-documents)

[Snabbstart (SOAP-läge): Validera DDX-dokument med Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) (SOAP-läge)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Validera ett DX-dokument med webbtjänstens API {#validate-a-ddx-document-using-the-web-service-api}

Validera ett DX-dokument med Assembler Service API (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt localhost med formulärserverns IP-adress.

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
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` med bytearrayens innehåll.

1. Ange körningsalternativ för att validera DDX-dokumentet.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange det körningsalternativ som instruerar Assembler-tjänsten att validera DDX-dokumentet genom att tilldela värdet true till `AssemblerOptionSpec` objektets `validateOnly` datamedlem.
   * Ange mängden information som Assembler-tjänsten skriver till loggfilen genom att tilldela ett strängvärde till `AssemblerOptionSpec` objektets `logLevel` datamedlem. -metod När du validerar ett DX-dokument vill du att mer information ska skrivas till loggfilen som ska vara till hjälp vid valideringsprocessen. Därför kan du ange värdet `FINE` eller `FINER`. Mer information om alternativ för körning som du kan ange finns i `AssemblerOptionSpec` klassreferens i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Utför valideringen.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` och skicka följande värden:

   * A `BLOB` -objekt som representerar DDX-dokumentet.
   * Värdet `null` för `Map` objekt som vanligtvis lagrar PDF-dokument.
   * An `AssemblerOptionSpec` objekt som anger körningsalternativ.

   The `invokeDDX` returnerar en `AssemblerResult` -objekt som innehåller information som anger om DDX-dokumentet är giltigt.

1. Spara valideringsresultaten i en loggfil.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för loggfilen och läget som filen ska öppnas i. Kontrollera att filnamnstillägget är .xml.
   * Skapa en `BLOB` objekt som lagrar logginformation genom att hämta värdet för `AssemblerResult` objektets `jobLog` datamedlem.
   * Skapa en bytearray som lagrar innehållet i `BLOB` -objekt. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` fält.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

   >[!NOTE]
   >
   >Om DDX-dokumentet är ogiltigt kan du `OperationException` kastas. I catch-satsen kan du hämta värdet för `OperationException` objektets `jobLog` medlem.

**Se även**

[Validerar DDX-dokument](#validating-ddx-documents)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
