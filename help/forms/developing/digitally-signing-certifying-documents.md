---
title: Digitalt signera och certifiera dokument
description: Använd signaturtjänsten för att lägga till och ta bort fält för elektroniska underskrifter i ett PDF-dokument, hämta namn på fält för underskrifter i ett PDF-dokument, ändra fält för underskrifter, signera PDF-dokument digitalt, certifiera PDF-dokument, validera digitala signaturer i ett PDF-dokument, validera alla digitala signaturer i ett PDF-dokument och ta bort en digital signatur från ett signaturfält.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '16917'
ht-degree: 0%

---

# Digitalt signera och certifiera dokument {#digitally-signing-and-certifying-documents}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

**Om signaturtjänsten**

Med signaturtjänsten kan din organisation skydda säkerheten och sekretessen för Adobe PDF-dokument som den distribuerar och tar emot. Den här tjänsten använder digitala signaturer och certifiering för att säkerställa att endast avsedda mottagare kan ändra dokument. Eftersom säkerhetsfunktionerna tillämpas på själva dokumentet förblir dokumentet säkert och styrs under hela sin livscykel. Ett dokument förblir säkert även utanför brandväggen när det laddas ned offline och när det skickas tillbaka till organisationen.

>[!NOTE]
>
>Du kan skapa en anpassad underskriftshanterare för signaturtjänsten som anropas när vissa åtgärder anropas, till exempel signering av ett PDF-dokument.

**Namn på signaturfält**

Vissa åtgärder i Signature Service kräver att du anger namnet på det signaturfält där en åtgärd utförs. När du t.ex. signerar ett PDF-dokument anger du namnet på signaturfältet som ska signeras. Anta att det fullständiga namnet för ett signaturfält är `form1[0].Form1[0].SignatureField1[0]`. Du kan ange `SignatureField1[0]` i stället för `form1[0].Form1[0].SignatureField1[0]`.

Ibland leder en konflikt till att signaturtjänsten signerar (eller utför en annan åtgärd som kräver signaturfältets namn) fel fält. Den här konflikten är resultatet av namnet `SignatureField1[0]` visas på två eller flera ställen i samma dokument i PDF. Ta till exempel ett PDF-dokument som innehåller två signaturfält med namnet `form1[0].Form1[0].SignatureField1[0]` och `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` och du anger `SignatureField1[0]`. I det här fallet signerar signaturtjänsten det första signaturfältet som hittas samtidigt som alla signaturfält i dokumentet itereras.

Om det finns flera signaturfält i ett PDF-dokument rekommenderar vi att du anger signaturfältens fullständiga namn. Det vill säga, specificera `form1[0].Form1[0].SignatureField1[0]`i stället för `SignatureField1[0]`.

Du kan utföra följande uppgifter med hjälp av signaturtjänsten:

* Lägg till och ta bort fält för elektroniska underskrifter i ett PDF-dokument. (Se [Lägga till signaturfält](digitally-signing-certifying-documents.md#adding-signature-fields).)
* Hämta namnen på signaturfälten i ett PDF-dokument. (Se [Hämtar namn på signaturfält](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* Ändra signaturfält. (Se [Ändra signaturfält](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* Signera PDF-dokument digitalt. (Se [Signera PDF-dokument digitalt](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* Certifiera PDF-dokument. (Se [Certifiera PDF-dokument](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* Validera digitala signaturer i ett PDF-dokument. (Se [Verifierar digitala signaturer](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Validera alla digitala signaturer i ett PDF-dokument. (Se [Verifierar flera digitala signaturer](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Ta bort en digital signatur från ett signaturfält. (Se [Tar bort digitala signaturer](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>Mer information om signaturtjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)..

## Lägga till signaturfält {#adding-signature-fields}

Digitala signaturer visas i signaturfält, som är formulärfält som innehåller en grafisk representation av signaturen. Signaturfält kan vara synliga eller osynliga. Signerare kan använda ett befintligt signaturfält eller ett signaturfält kan läggas till programmatiskt. I båda fallen måste signaturfältet finnas innan ett PDF-dokument kan signeras.

Du kan programmässigt lägga till ett signaturfält med hjälp av Java API:t för signaturtjänsten eller API:t för signaturwebbtjänsten. Du kan lägga till mer än ett signaturfält i ett PDF-dokument, men varje signaturfältsnamn måste vara unikt.

>[!NOTE]
>
>I vissa dokumenttyper i PDF kan du inte lägga till ett signaturfält med programkod. Mer information om signaturtjänsten och hur du lägger till signaturfält finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Gör så här om du vill lägga till ett signaturfält i ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en signaturklient.
1. Hämta ett PDF-dokument som ett signaturfält läggs till i.
1. Lägg till ett signaturfält.
1. Spara PDF-dokumentet som en PDF-fil.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klassökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

**Skapa en signaturklient**

Innan du programmässigt kan utföra en signeringstjänståtgärd måste du skapa en signaturtjänstklient.

**Hämta ett PDF-dokument som ett signaturfält läggs till i**

Hämta ett dokument i PDF som ett signaturfält läggs till i.

**Lägg till ett signaturfält**

Om du vill lägga till ett signaturfält i ett PDF-dokument anger du koordinatvärden som identifierar signaturfältets plats. (Om du lägger till ett osynligt signaturfält är dessa värden inte obligatoriska.) Du kan också ange vilka fält i dokumentet PDF som ska låsas efter att en signatur har tillämpats på signaturfältet.

**Spara PDF-dokumentet som en PDF-fil**

När signaturtjänsten har lagt till ett signaturfält i PDF-dokumentet kan du spara dokumentet som en PDF-fil så att användare kan öppna det i Acrobat eller Adobe Reader.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Signera PDF-dokument digitalt](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Lägga till signaturfält med Java API {#add-signature-fields-using-the-java-api}

Lägg till ett signaturfält med signatur-API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-signatures-client.jar, i Java-projektets klassökväg.

1. Skapa en signaturklient

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `SignatureServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta ett PDF-dokument som ett signaturfält läggs till i

   * Skapa en `java.io.FileInputStream` objekt som representerar det PDF-dokument som ett signaturfält läggs till i med hjälp av dess konstruktor och genom att skicka ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Lägg till ett signaturfält

   * Skapa en `PositionRectangle` objekt som anger signaturfältets plats med hjälp av dess konstruktor. Ange koordinatvärden i konstruktorn.
   * Skapa en `FieldMDPOptions` objekt som anger de fält som låses när en elektronisk underskrift används i signaturfältet.
   * Lägg till ett signaturfält i ett PDF-dokument genom att anropa `SignatureServiceClient` objektets `addSignatureField` och skicka följande värden:

      * A `com.adobe.idp`. `Document` -objekt som representerar det PDF-dokument som ett signaturfält läggs till i.
      * Ett strängvärde som anger signaturfältets namn.
      * A `java.lang.Integer` värde som representerar det sidnummer till vilket ett signaturfält läggs till.
      * A `PositionRectangle` objekt som anger signaturfältets plats.
      * A `FieldMDPOptions` objekt som anger fält i dokumentet PDF som är låsta efter att en digital signatur har tillämpats på signaturfältet. Det här parametervärdet är valfritt och du kan skicka `null`.

   * A `PDFSeedValueOptions` -objekt som anger olika körningsvärden. Det här parametervärdet är valfritt och du kan skicka `null`.

     The `addSignatureField` returnerar en `com.adobe.idp`. `Document` -objekt som representerar ett PDF-dokument som innehåller ett signaturfält.

   >[!NOTE]
   >
   >Du kan anropa `SignatureServiceClient` objektets `addInvisibleSignatureField` metod för att lägga till ett osynligt signaturfält.

1. Spara PDF-dokumentet som en PDF-fil

   * Skapa en `java.io.File` och se till att filtillägget är .pdf.
   * Anropa `com.adobe.idp`. `Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` till filen. Se till att du använder `com.adobe.idp`. `Document` objekt som returneras av `addSignatureField` -metod.

**Se även**

[API-snabbstart för signaturtjänst](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Lägga till signaturfält med webbtjänstens API {#add-signature-fields-using-the-web-service-api}

Så här lägger du till ett signaturfält med signatur-API:t (webbtjänsten):

1. Inkludera projektfiler

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en signaturklient

   * Skapa en `SignatureServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `SignatureServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/SignatureService?WSDL`). Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `SignatureServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta ett PDF-dokument som ett signaturfält läggs till i

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra det PDF-dokument som ska innehålla ett signaturfält.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` med bytearrayens innehåll.

1. Lägg till ett signaturfält

   Lägg till ett signaturfält i PDF-dokumentet genom att anropa `SignatureServiceClient` objektets `addSignatureField` och skicka följande värden:

   * A `BLOB` -objekt som representerar det PDF-dokument som ett signaturfält läggs till i.
   * Ett strängvärde som anger signaturfältets namn.
   * Ett heltalsvärde som representerar sidnumret som ett signaturfält läggs till på.
   * A `PositionRect` objekt som anger signaturfältets plats.
   * A `FieldMDPOptions` objekt som anger fält i dokumentet PDF som är låsta efter att en digital signatur har tillämpats på signaturfältet. Det här parametervärdet är valfritt och du kan skicka `null`.
   * A `PDFSeedValueOptions` -objekt som anger olika körningsvärden. Det här parametervärdet är valfritt och du kan skicka `null`.

   The `addSignatureField` returnerar en `BLOB` -objekt som representerar ett PDF-dokument som innehåller ett signaturfält.

1. Spara PDF-dokumentet som en PDF-fil

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det PDF-dokument som ska innehålla signaturfältet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `BLOB` objekt som returneras av `addSignatureField` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `binaryData` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Hämtar namn på signaturfält {#retrieving-signature-field-names}

Du kan hämta namnen på alla signaturfält i ett PDF-dokument som du vill signera eller certifiera. Om du är osäker på vilka signaturfältsnamn som finns i ett PDF-dokument eller vill verifiera namnen, kan du hämta dem programmatiskt. Signaturtjänsten returnerar signaturfältets kvalificerade namn, till exempel `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>Mer information om signaturtjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Sammanfattning av steg {#summary_of_steps-1}

Gör så här för att hämta signaturfältsnamn:

1. Inkludera projektfiler.
1. Skapa en signaturklient.
1. Hämta det PDF-dokument som innehåller signaturfält.
1. Hämta signaturfältens namn.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klassökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

Mer information om var dessa JAR-filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Skapa en signaturklient**

Innan du programmässigt kan utföra en signeringstjänståtgärd måste du skapa en signaturtjänstklient.

**Hämta PDF-dokumentet som innehåller signaturfält**

Hämta ett PDF-dokument som innehåller signaturfält.

**Hämta namn på signaturfält**

Du kan hämta namn på signaturfält när du har hämtat ett PDF-dokument som innehåller ett eller flera signaturfält.

**Se även**

[Hämta namn på signaturfält med Java API](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[Hämta signaturfält med webbtjänstens API](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Lägga till signaturfält](digitally-signing-certifying-documents.md#adding-signature-fields)

### Hämta namn på signaturfält med Java API {#retrieve-signature-field-names-using-the-java-api}

Hämta namn på signaturfält med signatur-API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-signatures-client.jar, i Java-projektets klassökväg.

1. Skapa en signaturklient

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `SignatureServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta PDF-dokumentet som innehåller signaturfält

   * Skapa en `java.io.FileInputStream` objekt som representerar dokumentet som innehåller signaturfält i PDF genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för dokumentet i PDF.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Hämta namn på signaturfält

   * Hämta signaturfältsnamnen genom att anropa `SignatureServiceClient` objektets `getSignatureFieldList` metoden och skicka `com.adobe.idp.Document` -objekt som innehåller det PDF-dokument som innehåller signaturfält. Den här metoden returnerar en `java.util.List` objekt, i vilket varje element innehåller ett `PDFSignatureField` -objekt. Med det här objektet kan du få ytterligare information om ett signaturfält, till exempel om det är synligt.
   * Iterera genom `java.util.List` -objekt för att avgöra om det finns signaturfältsnamn. För varje signaturfält i PDF-dokumentet kan du få ett separat `PDFSignatureField` -objekt. Om du vill få fram namnet på signaturfältet anropar du `PDFSignatureField` objektets `getName` -metod. Den här metoden returnerar ett strängvärde som anger signaturfältets namn.

**Se även**

[Hämtar namn på signaturfält](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Snabbstart (SOAP läge): Hämta signaturfältnamn med Java API](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Hämta signaturfält med webbtjänstens API {#retrieve-signature-field-using-the-web-service-api}

Hämta namn på signaturfält med signatur-API:t (webbtjänst):

1. Inkludera projektfiler

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en signaturklient

   * Skapa en `SignatureServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `SignatureServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/SignatureService?WSDL`). Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `SignatureServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta PDF-dokumentet som innehåller signaturfält

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra det PDF-dokument som innehåller signaturfält.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält bytearrayens innehåll.

1. Hämta namn på signaturfält

   * Hämta signaturfältsnamnen genom att anropa `SignatureServiceClient` objektets `getSignatureFieldList` metoden och skicka `BLOB` -objekt som innehåller det PDF-dokument som innehåller signaturfält. Den här metoden returnerar en `MyArrayOfPDFSignatureField` samlingsobjekt där varje element innehåller `PDFSignatureField` -objekt.
   * Iterera genom `MyArrayOfPDFSignatureField` -objekt för att avgöra om det finns signaturfältsnamn. För varje signaturfält i PDF-dokumentet kan du få en `PDFSignatureField` -objekt. Om du vill få fram namnet på signaturfältet anropar du `PDFSignatureField` objektets `getName` -metod. Den här metoden returnerar ett strängvärde som anger signaturfältets namn.

**Se även**

[Hämtar namn på signaturfält](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Ändra signaturfält {#modifying-signature-fields}

Du kan ändra signaturfält som finns i ett PDF-dokument med hjälp av Java API och webbtjänstens API. När du ändrar ett signaturfält måste du ändra signaturfältets låsordlistevärden eller ordlistevärden för startvärde.

A *låsordlista för fält* anger en lista med fält som är låsta när signaturfältet signeras. Ett låst fält hindrar användaren från att göra ändringar i fältet. A *ordlista för startvärde* innehåller begränsad information som används när signaturen tillämpas. Du kan till exempel ändra behörigheter som styr vilka åtgärder som kan utföras utan att en signatur blir ogiltig.

Genom att ändra ett befintligt signaturfält kan du ändra PDF-dokumentet så att det återspeglar förändrade affärskrav. Ett nytt affärskrav kan till exempel kräva att alla dokumentfält låses efter att dokumentet har signerats.

I det här avsnittet beskrivs hur du ändrar ett signaturfält genom att ändra både fältets låsordlista och ordlistevärden för startvärde. Ändringar som görs i signaturfältet låser ordlistan så att alla fält i PDF-dokumentet låses när ett signaturfält signeras. Ändringar i ordlistan för dirigerade värden förbjuder vissa typer av ändringar i dokumentet.

>[!NOTE]
>
>Mer information om signaturtjänsten och ändring av signaturfält finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-2}

Gör så här om du vill ändra signaturfält i ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en signaturklient.
1. Hämta det PDF-dokument som innehåller det signaturfält som ska ändras.
1. Ange lexikonvärden.
1. Ändra signaturfältet.
1. Spara PDF-dokumentet som en PDF-fil.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klassökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

Mer information om var dessa JAR-filer finns i [Inkludera Java-biblioteksfiler för LiveCyclen](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Skapa en signaturklient**

Innan du programmässigt kan utföra en signeringstjänståtgärd måste du skapa en signaturtjänstklient.

**Hämta det PDF-dokument som innehåller signaturfältet som ska ändras**

Hämta ett PDF-dokument som innehåller det signaturfält som ska ändras.

**Ange lexikonvärden**

Om du vill ändra ett signaturfält tilldelar du värden till dess låsordlista för fält eller ordlista för startvärde. När du anger värden för signaturfält låses ordlistevärden, vilket innebär att du anger dokumentfält i PDF som är låsta när signaturfältet signeras. (I det här avsnittet beskrivs hur du låser alla fält.)

Följande ordlistevärden för dirigerade värden kan anges:

* **Versionskontroll**: Anger om spärrkontroll utförs när en signatur används i signaturfältet.
* **Certifikatalternativ**: Tilldelar värden till certifikatets startvärdesordlista. Innan du anger certifikatalternativ bör du bekanta dig med en ordlista för certifikatstartvärden. (Se [PDF Reference](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Sammanfattningsalternativ**: Tilldelar sammandragsalgoritmer som används för signering. Giltiga värden är SHA1, SHA256, SHA384, SHA512 och RIPEMD160.
* **Filter**: Anger det filter som används med signaturfältet. Du kan till exempel använda filtret Adobe.PPKLite. (Se [PDF Reference](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Flaggalternativ**: Anger de flaggvärden som är associerade med det här signaturfältet. Värdet 1 innebär att en signerare endast får använda de angivna värdena för posten. Värdet 0 innebär att andra värden är tillåtna. Här är bitpositionerna:

   * **1 (filter):** Den underskriftshanterare som ska användas för att signera signaturfältet
   * **2 (SubFilter):** En array med namn som anger godkända kodningar att använda vid signering
   * **3 (V)**: Det lägsta versionsnummer som krävs av underskriftshanteraren för att signera signaturfältet
   * **4 (skäl):** En array med strängar som anger möjliga orsaker till signering av ett dokument
   * **5 (PDFLegalWarnings):** En array med strängar som anger möjliga juridiska attesteringar

* **Juridiska attesteringar**: När ett dokument är certifierat skannas det automatiskt efter specifika typer av innehåll som kan göra det synliga innehållet i ett dokument tvetydigt eller vilseledande. En anteckning kan till exempel skymma text som är viktig för att förstå vad som certifieras. Skanningsprocessen genererar varningar som anger att den här typen av innehåll finns. Det innehåller även en ytterligare förklaring av innehållet som kan ha genererat varningar.
* **Behörigheter**: Anger behörigheter som kan användas i ett PDF-dokument utan att signaturen blir ogiltig.
* **Orsaker**: Anger varför det här dokumentet måste signeras.
* **Tidsstämpel**: Anger tidsstämplingsalternativ. Du kan till exempel ange URL:en för den tidsstämpelserver som används.
* **Version**: Anger det lägsta versionsnumret för den underskriftshanterare som ska användas för att signera signaturfältet.

**Ändra signaturfältet**

När du har skapat en signaturtjänstklient, hämtat det PDF-dokument som innehåller det signaturfält som ska ändras och angett värden för ordlista, kan du instruera signaturtjänsten att ändra signaturfältet. Signaturtjänsten returnerar sedan ett PDF-dokument som innehåller det ändrade signaturfältet. Det ursprungliga PDF-dokumentet påverkas inte.

**Spara PDF-dokumentet som en PDF-fil**

Spara det PDF-dokument som innehåller det ändrade signaturfältet som en PDF-fil så att användare kan öppna det i Acrobat eller Adobe Reader.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för signaturtjänst](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[Signera PDF-dokument digitalt](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Ändra signaturfält med Java API {#modify-signature-fields-using-the-java-api}

Ändra ett signaturfält med hjälp av signatur-API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-signatures-client.jar, i Java-projektets klassökväg.

1. Skapa en signaturklient

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `SignatureServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta det PDF-dokument som innehåller signaturfältet som ska ändras

   * Skapa en `java.io.FileInputStream` -objekt som representerar dokumentet som innehåller signaturfältet som ska ändras med hjälp av dess konstruktor och genom att skicka ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ange lexikonvärden

   * Skapa en `PDFSignatureFieldProperties` genom att använda dess konstruktor. A `PDFSignatureFieldProperties` objekt lagrar information om låsordlista för signaturfält och ordlista för startvärde.
   * Skapa en `PDFSeedValueOptionSpec` genom att använda dess konstruktor. Med det här objektet kan du ange ordlistevärden för startvärde.
   * Tillåt inte ändringar i PDF-dokumentet genom att anropa `PDFSeedValueOptionSpec` objektets `setMdpValue` metoden och skicka `MDPPermissions.NoChanges` uppräkningsvärde.
   * Skapa en `FieldMDPOptionSpec` genom att använda dess konstruktor. Med det här objektet kan du ange värden för låsning av signaturfält.
   * Lås alla fält i PDF-dokumentet genom att anropa `FieldMDPOptionSpec` objektets `setMdpValue` metoden och skicka `FieldMDPAction.ALL` uppräkningsvärde.
   * Ange information om startvärdesordlista genom att anropa `PDFSignatureFieldProperties` objektets `setSeedValue` metoden och skicka `PDFSeedValueOptionSpec` -objekt.
   * Ange information om låsning av signaturfält genom att anropa `PDFSignatureFieldProperties`objektets `setFieldMDP` metoden och skicka `FieldMDPOptionSpec` -objekt.

   >[!NOTE]
   >
   >Om du vill se alla ordlistevärden för dirigerade värden som du kan ange finns i `PDFSeedValueOptionSpec` klassreferens. (Se [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

1. Ändra signaturfältet

   Ändra signaturfältet genom att anropa `SignatureServiceClient` objektets `modifySignatureField` och skicka följande värden:

   * The `com.adobe.idp.Document` det objekt som lagrar dokumentet som innehåller det signaturfält som ska ändras
   * Ett strängvärde som anger signaturfältets namn
   * The `PDFSignatureFieldProperties` objekt som lagrar låsordlista för signaturfält och information om startvärdesordlista

   The `modifySignatureField` returnerar en `com.adobe.idp.Document` objekt som lagrar ett dokument i PDF som innehåller det ändrade signaturfältet.

1. Spara PDF-dokumentet som en PDF-fil

   * Skapa en `java.io.File` och se till att filnamnstillägget är .pdf.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att kopiera innehållet i `com.adobe.idp.Document` till filen. Se till att du använder `com.adobe.idp.Document` det objekt som `modifySignatureField` returnerad metod.

### Ändra signaturfält med webbtjänstens API {#modify-signature-fields-using-the-web-service-api}

Ändra ett signaturfält med hjälp av signatur-API:t (webbtjänst):

1. Inkludera projektfiler

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en signaturklient

   * Skapa en `SignatureServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `SignatureServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/SignatureService?WSDL`). Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `SignatureServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta det PDF-dokument som innehåller signaturfältet som ska ändras

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra det PDF-dokument som innehåller det signaturfält som ska ändras.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` egenskapen för bytearrayens innehåll.

1. Ange lexikonvärden

   * Skapa en `PDFSignatureFieldProperties` genom att använda dess konstruktor. Det här objektet lagrar information om låsordlista för signaturfält och ordlista för startvärde.
   * Skapa en `PDFSeedValueOptionSpec` genom att använda dess konstruktor. Med det här objektet kan du ange ordlistevärden för startvärde.
   * Tillåt inte ändringar i PDF-dokumentet genom att tilldela `MDPPermissions.NoChanges` uppräkningsvärde till `PDFSeedValueOptionSpec` objektets `mdpValue` datamedlem.
   * Skapa en `FieldMDPOptionSpec` genom att använda dess konstruktor. Med det här objektet kan du ange värden för låsning av signaturfält.
   * Lås alla fält i PDF-dokumentet genom att tilldela `FieldMDPAction.ALL` uppräkningsvärde till `FieldMDPOptionSpec` objektets `mdpValue` datamedlem.
   * Ange information om startvärdesordlista genom att tilldela `PDFSeedValueOptionSpec` objekt till `PDFSignatureFieldProperties` objektets `seedValue` datamedlem.
   * Ange information om låsning av signaturfält genom att tilldela `FieldMDPOptionSpec` objekt till `PDFSignatureFieldProperties` objektets `fieldMDP` datamedlem.

   >[!NOTE]
   >
   >Om du vill se alla ordlistevärden för dirigerade värden som du kan ange finns i `PDFSeedValueOptionSpec` klassreferens. (Se [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

1. Ändra signaturfältet

   Ändra signaturfältet genom att anropa `SignatureServiceClient` objektets `modifySignatureField` och skicka följande värden:

   * The `BLOB` det objekt som lagrar dokumentet som innehåller det signaturfält som ska ändras
   * Ett strängvärde som anger signaturfältets namn
   * The `PDFSignatureFieldProperties` objekt som lagrar låsordlista för signaturfält och information om startvärdesordlista

   The `modifySignatureField` returnerar en `BLOB` objekt som lagrar ett dokument i PDF som innehåller det ändrade signaturfältet.

1. Spara PDF-dokumentet som en PDF-fil

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det PDF-dokument som ska innehålla signaturfältet samt läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `BLOB` det objekt som `addSignatureField` returnerar metoden. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Signera PDF-dokument digitalt {#digitally-signing-pdf-documents}

Digitala signaturer kan användas i PDF-dokument för att ge en viss säkerhetsnivå. Digitala signaturer, precis som handskrivna signaturer, är ett sätt som signerare kan använda för att identifiera sig och göra programsatser om ett dokument. Den teknik som används för att digitalt signera dokument gör att både signeraren och mottagaren vet vad som signerats och vet att dokumentet inte har ändrats sedan det signerades.

PDF-dokument undertecknas med hjälp av teknik med öppen nyckel. En signerare har två nycklar: en offentlig nyckel och en privat nyckel. Den privata nyckeln lagras i en användares autentiseringsuppgifter som måste vara tillgängliga vid signeringen. Den offentliga nyckeln lagras i användarens certifikat som måste vara tillgängligt för mottagarna för att validera signaturen. Information om återkallade certifikat finns i listor över återkallade certifikat (CRL:er) och OCSP-svar (Online Certificate Status Protocol) som distribueras av certifikatutfärdare (CA:er). Tidpunkten för signering kan hämtas från en betrodd källa som kallas tidsstämpelutfärdare.

>[!NOTE]
>
>Innan du kan signera ett PDF-dokument digitalt måste du se till att du lägger till certifikatet i AEM Forms. Ett certifikat läggs till med administrationskonsolen eller programmatiskt med Trust Manager API. (Se [Importera autentiseringsuppgifter med Trust Manager API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Du kan signera PDF-dokument digitalt. När du signerar ett PDF-dokument digitalt måste du referera till en säkerhetsbehörighet som finns i AEM Forms. Autentiseringsuppgiften är den privata nyckel som används för signering.

Signaturtjänsten utför följande steg när ett PDF-dokument signeras:

1. Signaturtjänsten hämtar autentiseringsuppgifterna från förtroendelagret genom att skicka det alias som anges i begäran.
1. Truststore söker efter de angivna autentiseringsuppgifterna.
1. Autentiseringsuppgifterna returneras till signaturtjänsten och används för att signera dokumentet. Autentiseringsuppgiften cachelagras även mot aliaset för framtida begäranden.

Mer information om hur du hanterar säkerhetsuppgifter finns i *Installera och distribuera AEM Forms* guide för programservern.

>[!NOTE]
>
>Det finns skillnader mellan att underteckna och certifiera dokument. (Se [Certifiera PDF-dokument](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>Alla PDF-dokument har inte stöd för signering. Mer information om signaturtjänsten och digitalt signerade dokument finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Signaturtjänsten stöder inte XDP-filer med inbäddade PDF-data som indata till en åtgärd, till exempel certifiering av ett dokument. Den här åtgärden resulterar i att signaturtjänsten genererar en `PDFOperationException`. Du löser det här problemet genom att konvertera XDP-filen till en PDF-fil med tjänsten PDF Utilities och sedan skicka den konverterade PDF-filen till en Signature-tjänståtgärd. (Se [Arbeta med verktygen i PDF](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities).)

**Krypterings-HSM-autentiseringsuppgifter**

När du använder en Cipher Shield HSM-autentiseringsuppgift för att signera eller certifiera ett PDF-dokument, kan den nya autentiseringsuppgiften inte användas förrän J2EE-programservern som AEM Forms är distribuerad på har startats om. Du kan dock ange ett konfigurationsvärde, vilket gör att signerings- eller certifieringsåtgärden fungerar utan att J2EE-programservern startas om.

Du kan lägga till följande konfigurationsvärde i filen cknfastrc, som finns på /opt/nfast/cknfastrc (eller c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

När du har lagt till det här konfigurationsvärdet i cknfastrc-filen kan de nya autentiseringsuppgifterna användas utan att J2EE-programservern startas om.

    >[!OBS!]
    >
    > Du bör använda kommandot Ctrl + C för att starta om SDK:n. Om du startar om AEM SDK med alternativa metoder, till exempel genom att stoppa Java-processer, kan det leda till inkonsekvenser i den AEM utvecklingsmiljön.

**Underskriften är inte betrodd**

När du certifierar och signerar samma dokument i PDF visas en gul triangel mot den första signaturen när du öppnar dokumentet i PDF i Acrobat eller Adobe Reader, om den certifierande signaturen inte är tillförlitlig. Certifikatsignaturen måste vara betrodd för att den här situationen ska undvikas.

**Signera dokument som är XFA-baserade formulär**

Om du försöker signera ett XFA-baserat formulär med Signature service API, kan data saknas i `View` `Signed` `Version` i Acrobat. Ta till exempel följande arbetsflöde:

* Med hjälp av en XDP-fil som skapats med Designer kan du sammanfoga en formulärdesign som innehåller ett signaturfält och XML-data som innehåller formulärdata. Du använder Forms-tjänsten för att generera ett interaktivt PDF-dokument.
* Du signerar PDF-dokumentet med signaturtjänstens API.

### Sammanfattning av steg {#summary_of_steps-3}

Så här signerar du ett PDF-dokument digitalt:

1. Inkludera projektfiler.
1. Skapa en signaturtjänstklient.
1. Få PDF-dokumentet att signera.
1. Underteckna PDF-dokumentet.
1. Spara det signerade PDF-dokumentet som en PDF-fil.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klassökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

**Skapa en signaturklient**

Innan du programmässigt kan utföra en signeringstjänståtgärd måste du skapa en signaturtjänstklient.

**Få PDF-dokumentet att signera**

Om du vill signera ett PDF-dokument måste du skaffa ett PDF-dokument som innehåller ett signaturfält. Om ett PDF-dokument inte innehåller något signaturfält kan det inte signeras. Ett signaturfält kan läggas till med Designer eller via programmering.

**Signera PDF-dokumentet**

När du signerar ett PDF-dokument kan du ange körningsalternativ som används av signeringstjänsten. Du kan ange följande alternativ:

* Utseendealternativ
* Spärrkontroll
* Värden för tidsstämpling

Du anger utseendealternativ med en `PDFSignatureAppearanceOptionSpec` -objekt. Du kan till exempel visa datumet i en signatur genom att anropa `PDFSignatureAppearanceOptionSpec` objektets `setShowDate` metod och att skicka `true`.

Du kan också ange om en spärrkontroll ska utföras eller inte som avgör om det certifikat som används för att digitalt signera ett PDF-dokument har återkallats eller inte. Om du vill utföra spärrkontroll kan du ange ett av följande värden:

* **NoCheck**: Utför inte spärrkontroll.
* **BestEffort**: Försök alltid att kontrollera om alla certifikat i kedjan har återkallats. Om det uppstår något problem vid kontrollen antas återkallningen vara giltig. Om något fel inträffar antar du att certifikatet inte återkallas.
* **CheckIfAvailable:** Kontrollera om alla certifikat i kedjan har återkallats om det finns någon återkallningsinformation. Om något problem uppstår vid kontrollen antas återkallningen vara ogiltig. Om något fel inträffar antar du att certifikatet har återkallats och är ogiltigt. (Detta är standardvärdet.)
* **AlltidKontrollera**: Kontrollera om alla certifikat i kedjan har återkallats. Om det inte finns någon återkallningsinformation i något certifikat antas återkallningen vara ogiltig.

Om du vill göra en återkallningskontroll på ett certifikat kan du ange en URL till en server för listan över återkallade certifikat genom att använda en `CRLOptionSpec` -objekt. Om du vill utföra en spärrkontroll och inte anger en URL till en CRL-server, hämtar signaturtjänsten URL-adressen från certifikatet.

I stället för att använda en CRL-server kan du använda en OCSP-server (Online Certificate Status Protocol) när du utför spärrkontroll. När du använder en OCSP-server i stället för en CRL-server utförs spärrkontrollen oftast snabbare. (Se &quot;Online Certificate Status Protocol&quot; på [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

Du kan ställa in CRL- och OCSP-serverordningen som används av signaturtjänsten med Adobe-program och -tjänster. Om till exempel OCSP-servern är inställd först i Adobe-program och -tjänster kontrolleras OCSP-servern, som följs av CRL-servern. (Se Hantera certifikat och autentiseringsuppgifter med Trust Store i AAC-hjälpen.)

Om du anger att du inte ska utföra spärrkontroll kontrollerar inte signaturtjänsten om certifikatet som användes för att signera eller certifiera ett dokument har spärrats. CRL- och OCSP-serverinformation ignoreras alltså.

>[!NOTE]
>
>Även om en CRL eller en OCSP-server kan anges i certifikatet, kan du åsidosätta URL:en som anges i certifikatet genom att använda en `CRLOptionSpec` och `OCSPOptionSpec` -objekt. Om du till exempel vill åsidosätta CRL-servern kan du anropa `CRLOptionSpec` objektets `setLocalURI` -metod.

Tidsstämpling avser processen att spåra den tidpunkt då ett signerat eller certifierat dokument ändrades. När ett dokument har signerats bör det inte ändras, inte ens av dokumentägaren. Tidsstämpling gör det lättare att framtvinga giltigheten av ett undertecknat eller certifierat dokument. Du kan ange tidsstämplingsalternativ med en `TSPOptionSpec` -objekt. Du kan till exempel ange URL:en för en TSP-server (Time Stamping Provider).

>[!NOTE]
>
>I Java- och webbtjänsten går du igenom sektioner och motsvarande snabbstarter används spärrkontroll. Eftersom ingen information om CRL- eller OCSP-server har angetts hämtas serverinformationen från certifikatet som används för att digitalt signera PDF-dokumentet.

Om du vill signera ett PDF-dokument kan du ange det fullständiga, kvalificerade namnet på signaturfältet som ska innehålla den digitala signaturen, till exempel `form1[0].#subform[1].SignatureField3[3]`. När du använder ett XFA-formulärfält kan du även använda det partiella namnet på signaturfältet: `SignatureField3[3]`.

Du måste även referera till en säkerhetsuppgift för att digitalt signera ett PDF-dokument. Om du vill referera till en säkerhetsreferens anger du ett alias. Aliaset är en referens till en faktisk autentiseringsuppgift som kan finnas i en PKCS#12-fil (med filnamnstillägget .pfx) eller en maskinvarusäkerhetsmodul (HSM). Mer information om säkerhetsuppgifter finns i *Installera och distribuera AEM Forms* guide för programservern.

**Spara det signerade PDF-dokumentet**

När signeringstjänsten har signerat PDF-dokumentet digitalt kan du spara det som en PDF-fil så att användare kan öppna det i Acrobat eller Adobe Reader.

**Se även**

[Signera PDF-dokument digitalt med Java API](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[Signera PDF-dokument digitalt med webbtjänstens API](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Lägga till signaturfält](digitally-signing-certifying-documents.md#adding-signature-fields)

[Hämtar namn på signaturfält](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Signera PDF-dokument digitalt med Java API {#digitally-sign-pdf-documents-using-the-java-api}

Signera ett PDF-dokument digitalt med signatur-API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-signatures-client.jar, i Java-projektets klassökväg.

1. Skapa en signaturklient

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `SignatureServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Få PDF-dokumentet att signera

   * Skapa en `java.io.FileInputStream` objekt som representerar PDF-dokumentet som ska signeras digitalt med konstruktorn och som skickar ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Signera PDF-dokumentet

   Signera PDF-dokumentet genom att anropa `SignatureServiceClient` objektets `sign` och skicka följande värden:

   * A `com.adobe.idp.Document` objekt som representerar det PDF-dokument som ska signeras.
   * Ett strängvärde som representerar namnet på signaturfältet som ska innehålla den digitala signaturen.
   * A `Credential` objekt som representerar de autentiseringsuppgifter som används för att digitalt signera PDF-dokumentet. Skapa en `Credential` genom att anropa `Credential` objektets statiska `getInstance` och skickar ett strängvärde som anger aliasvärdet som motsvarar säkerhetsuppgifter.
   * A `HashAlgorithm` objekt som anger en statisk datamedlem som representerar hash-algoritmen som ska användas för att sammanfatta PDF-dokumentet. Du kan till exempel ange `HashAlgorithm.SHA1` om du vill använda SHA1-algoritmen.
   * Ett strängvärde som representerar orsaken till varför PDF-dokumentet signerades digitalt.
   * Ett strängvärde som representerar signerarens kontaktinformation.
   * A `PDFSignatureAppearanceOptions` som styr utseendet på den digitala signaturen. Du kan till exempel använda det här objektet för att lägga till en egen logotyp till en digital signatur.
   * A `java.lang.Boolean` objekt som anger om spärrkontroll ska utföras på signerarens certifikat.
   * An `OCSPOptionSpec` objekt som lagrar inställningar för stöd för OCSP (Online Certificate Status Protocol). Om spärrkontroll inte utförs används inte den här parametern och du kan ange `null`.
   * A `CRLPreferences` objekt som lagrar inställningar för listan över återkallade certifikat. Om spärrkontroll inte utförs används inte den här parametern och du kan ange `null`.
   * A `TSPPreferences` objekt som lagrar inställningar för stöd för tidsstämpelleverantör (TSP). Den här parametern är valfri och kan `null`. Mer information finns i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   The `sign` returnerar en `com.adobe.idp.Document` objekt som representerar det signerade PDF-dokumentet.

1. Spara det signerade PDF-dokumentet

   * Skapa en `java.io.File` och se till att filtillägget är .pdf.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod och skicka `java.io.File`för att kopiera innehållet i `Document` till filen. Se till att du använder `com.adobe.idp.Document` objekt som returneras av `sign` -metod.

**Se även**

[Signera PDF-dokument digitalt](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Snabbstart (SOAP): Signera ett PDF-dokument digitalt med Java API](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Signera PDF-dokument digitalt med webbtjänstens API {#digitally-signing-pdf-documents-using-the-web-service-api}

Så här signerar du ett PDF-dokument digitalt med signatur-API:t (webbtjänst):

1. Inkludera projektfiler

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en signaturklient

   * Skapa en `SignatureServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `SignatureServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/SignatureService?WSDL`). Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `SignatureServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Få PDF-dokumentet att signera

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra ett PDF-dokument som är signerat.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det PDF-dokument som ska signeras samt läget i vilket filen ska öppnas.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` egenskapen för bytearrayens innehåll.

1. Signera PDF-dokumentet

   Signera PDF-dokumentet genom att anropa `SignatureServiceClient` objektets `sign` och skicka följande värden:

   * A `BLOB` objekt som representerar det PDF-dokument som ska signeras.
   * Ett strängvärde som representerar namnet på signaturfältet som ska innehålla den digitala signaturen.
   * A `Credential` objekt som representerar de autentiseringsuppgifter som används för att digitalt signera PDF-dokumentet. Skapa en `Credential` genom att använda konstruktorn och ange aliaset genom att tilldela ett värde till `Credential` objektets `alias` -egenskap.
   * A `HashAlgorithm` objekt som anger en statisk datamedlem som representerar hash-algoritmen som ska användas för att sammanfatta PDF-dokumentet. Du kan till exempel ange `HashAlgorithm.SHA1` om du vill använda SHA1-algoritmen.
   * Ett booleskt värde som anger om hash-algoritmen används.
   * Ett strängvärde som representerar orsaken till varför PDF-dokumentet signerades digitalt.
   * Ett strängvärde som representerar signerarens plats.
   * Ett strängvärde som representerar signerarens kontaktinformation.
   * A `PDFSignatureAppearanceOptions` som styr utseendet på den digitala signaturen. Du kan till exempel använda det här objektet för att lägga till en egen logotyp till en digital signatur.
   * A `System.Boolean` objekt som anger om spärrkontroll ska utföras på signerarens certifikat. Om spärrkontrollen är klar bäddas den in i signaturen. Standardvärdet är `false`.
   * An `OCSPOptionSpec` objekt som lagrar inställningar för stöd för OCSP (Online Certificate Status Protocol). Om spärrkontroll inte utförs används inte den här parametern och du kan ange `null`. Mer information om det här objektet finns i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` objekt som lagrar inställningar för listan över återkallade certifikat. Om spärrkontroll inte utförs används inte den här parametern och du kan ange `null`.
   * A `TSPPreferences` objekt som lagrar inställningar för stöd för tidsstämpelleverantör (TSP). Den här parametern är valfri och kan `null`.

   The `sign` returnerar en `BLOB` objekt som representerar det signerade PDF-dokumentet.

1. Spara det signerade PDF-dokumentet

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för det signerade PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `BLOB` objekt som returneras av `sign` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Signera PDF-dokument digitalt](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Digital Signing Interactive Forms {#digitally-signing-interactive-forms}

Du kan signera ett interaktivt formulär som skapas av Forms-tjänsten. Ta till exempel följande arbetsflöde:

* Du sammanfogar ett XFA-baserat PDF-formulär som skapats med Designer och formulärdata i ett XML-dokument med hjälp av Forms-tjänsten. Forms-servern återger ett interaktivt formulär.
* Du signerar det interaktiva formuläret med hjälp av API:t för signaturtjänsten.

Resultatet är ett digitalt signerat interaktivt PDF-formulär. När du signerar ett PDF-formulär som är baserat på ett XFA-formulär ska du se till att du sparar PDF-filen som ett Adobe Static PDF. Om du försöker signera ett PDF-formulär som har sparats som ett Adobe dynamiskt PDF-formulär inträffar ett undantag. Eftersom du signerar formuläret som returneras från Forms-tjänsten måste du se till att formuläret innehåller ett signaturfält.

>[!NOTE]
>
>Innan du kan signera ett interaktivt formulär digitalt måste du se till att du lägger till certifikatet i AEM Forms. Ett certifikat läggs till med administrationskonsolen eller programmatiskt med Trust Manager API. (Se [Importera autentiseringsuppgifter med Trust Manager API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

När du använder API:t för Forms-tjänsten anger du `GenerateServerAppearance` körningsalternativ till `true`. Med det här körningsalternativet kan du vara säker på att utseendet på det formulär som genereras på servern förblir giltigt när det öppnas i Acrobat eller Adobe Reader. Vi rekommenderar att du anger det här körningsalternativet när du genererar ett interaktivt formulär som ska signeras med Forms API.

>[!NOTE]
>
>Innan du läser Digital Signing Interactive Forms rekommenderar vi att du är bekant med att signera PDF-dokument. (Se [Signera PDF-dokument digitalt](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### Sammanfattning av steg {#summary_of_steps-4}

Så här signerar du ett interaktivt formulär digitalt från Forms-tjänsten:

1. Inkludera projektfiler.
1. Skapa en Forms- och Signatures-klient.
1. Hämta det interaktiva formuläret med hjälp av tjänsten Forms.
1. Signera det interaktiva formuläret.
1. Spara det signerade PDF-dokumentet som en PDF-fil.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klassökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

Mer information om var dessa JAR-filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Skapa en Forms- och Signatures-klient**

Eftersom det här arbetsflödet anropar både Forms- och Signature-tjänsterna skapar du både en Forms-tjänstklient och en signaturtjänstklient.

**Hämta det interaktiva formuläret med hjälp av tjänsten Forms**

Du kan använda Forms-tjänsten för att hämta det interaktiva formuläret PDF för signering. Från och med AEM Forms kan du skicka `com.adobe.idp.Document` till den Forms-tjänst som innehåller det formulär som ska återges. Den här metodens namn är `renderPDFForm2`. Den här metoden returnerar en `com.adobe.idp.Document` objekt som innehåller formuläret som ska signeras. Du kan skicka det här `com.adobe.idp.Document` -instans till signaturtjänsten.

På samma sätt kan du skicka `BLOB` instans när Forms-tjänsten returnerar till signeringstjänsten.

>[!NOTE]
>
>Den snabbstart som är kopplad till sektionen Digital Signing Interactive Forms anropar `renderPDFForm2` -metod.

**Signera det interaktiva formuläret**

När du signerar ett PDF-dokument kan du ange alternativ för körning som används av signaturtjänsten. Du kan ange följande alternativ:

* Utseendealternativ
* Spärrkontroll
* Värden för tidsstämpling

Du anger utseendealternativ med en `PDFSignatureAppearanceOptionSpec` -objekt. Du kan till exempel visa datumet i en signatur genom att anropa `PDFSignatureAppearanceOptionSpec` objektets `setShowDate` metod och att skicka `true`.

**Spara det signerade PDF-dokumentet**

När signeringstjänsten har signerat PDF-dokumentet digitalt kan du spara det som en PDF-fil. PDF kan öppnas i Acrobat eller Adobe Reader.

**Se även**

[Signera ett interaktivt formulär digitalt med Java API](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[Signera ett interaktivt formulär digitalt med webbtjänstens API](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Signera PDF-dokument digitalt](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Återger interaktiv PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Signera ett interaktivt formulär digitalt med Java API {#digitally-sign-an-interactive-form-using-the-java-api}

Signera ett interaktivt formulär digitalt med Forms och Signature API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-signatures-client.jar och adobe-forms-client.jar, i Java-projektets klassökväg.

1. Skapa en Forms- och Signatures-klient

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `SignatureServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.
   * Skapa en `FormsServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta det interaktiva formuläret med hjälp av tjänsten Forms

   * Skapa en `java.io.FileInputStream` objekt som representerar PDF-dokumentet som ska skickas till Forms-tjänsten med hjälp av dess konstruktor. Skicka ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.
   * Skapa en `java.io.FileInputStream` -objekt som representerar XML-dokumentet som innehåller formulärdata som ska skickas till Forms-tjänsten med hjälp av dess konstruktor. Skicka ett strängvärde som anger platsen för XML-filen.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.
   * Skapa en `PDFFormRenderSpec` objekt som används för att ange körningsalternativ. Anropa `PDFFormRenderSpec` objektets `setGenerateServerAppearance` metod och skicka `true`.
   * Anropa `FormsServiceClient` objektets `renderPDFForm2` och skicka följande värden:

      * A `com.adobe.idp.Document` objekt som innehåller det PDF-formulär som ska återges.
      * A `com.adobe.idp.Document` objekt som innehåller data som ska sammanfogas med formuläret.
      * A `PDFFormRenderSpec` objekt som lagrar körningsalternativ.
      * A `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten. Du kan ange `null` för det här parametervärdet.
      * A `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.

     The `renderPDFForm2` returnerar en `FormsResult` objekt som innehåller en formulärdataström

   * Hämta formuläret PDF genom att anropa `FormsResult` objektets `getOutputContent` -metod. Den här metoden returnerar en `com.adobe.idp.Document` objekt som representerar det interaktiva formuläret.

1. Signera det interaktiva formuläret

   Signera PDF-dokumentet genom att anropa `SignatureServiceClient` objektets `sign` och skicka följande värden:

   * A `com.adobe.idp.Document` objekt som representerar det PDF-dokument som ska signeras. Kontrollera att objektet är `com.adobe.idp.Document` objekt som hämtas från Forms-tjänsten.
   * Ett strängvärde som representerar namnet på signaturfältet som är signerat.
   * A `Credential` objekt som representerar de autentiseringsuppgifter som används för att digitalt signera PDF-dokumentet. Skapa en `Credential` genom att anropa `Credential` objektets statiska `getInstance` -metod. Skicka ett strängvärde som anger aliasvärdet som motsvarar säkerhetsuppgifter.
   * A `HashAlgorithm` objekt som anger en statisk datamedlem som representerar hash-algoritmen som ska användas för att sammanfatta PDF-dokumentet. Du kan till exempel ange `HashAlgorithm.SHA1` om du vill använda SHA1-algoritmen.
   * Ett strängvärde som representerar orsaken till varför PDF-dokumentet signerades digitalt.
   * Ett strängvärde som representerar signerarens kontaktinformation.
   * A `PDFSignatureAppearanceOptions` som styr utseendet på den digitala signaturen. Du kan till exempel använda det här objektet för att lägga till en egen logotyp till en digital signatur.
   * A `java.lang.Boolean` objekt som anger om spärrkontroll ska utföras på signerarens certifikat.
   * An `OCSPPreferences` objekt som lagrar inställningar för stöd för OCSP (Online Certificate Status Protocol). Om spärrkontroll inte utförs används inte den här parametern och du kan ange `null`.
   * A `CRLPreferences` objekt som lagrar inställningar för listan över återkallade certifikat. Om spärrkontroll inte utförs används inte den här parametern och du kan ange `null`.
   * A `TSPPreferences` objekt som lagrar inställningar för stöd för tidsstämpelleverantör (TSP). Den här parametern är valfri och kan `null`.

   The `sign` returnerar en `com.adobe.idp.Document` objekt som representerar det signerade PDF-dokumentet.

1. Spara det signerade PDF-dokumentet

   * Skapa en `java.io.File` och se till att filnamnstillägget är .pdf.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod och skicka `java.io.File`för att kopiera innehållet i `Document` till filen. Se till att du använder `com.adobe.idp.Document` det objekt som `sign` returnerad metod.

**Se även**

[Digital Signing Interactive Forms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Snabbstart (SOAP): Signera ett PDF-dokument digitalt med Java API](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Signera ett interaktivt formulär digitalt med webbtjänstens API {#digitally-sign-an-interactive-form-using-the-web-service-api}

Signera ett interaktivt formulär digitalt med Forms och Signature API (webbtjänsten):

1. Inkludera projektfiler

   Skapa ett Microsoft .NET-projekt som använder MTOM. Eftersom klientprogrammet anropar två AEM Forms-tjänster skapar du två tjänstreferenser. Använd följande WSDL-definition för den tjänstreferens som är associerad med signaturtjänsten: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Använd följande WSDL-definition för den tjänstreferens som är kopplad till Forms-tjänsten: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   På grund av `BLOB` datatypen är gemensam för båda tjänstreferenserna, och kvalificera fullt ut `BLOB` datatyp när du använder den. I motsvarande webbtjänsts snabbstart är alla `BLOB` -instanser är kvalificerade.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en Forms- och Signatures-klient

   * Skapa en `SignatureServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `SignatureServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/SignatureService?WSDL`). Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `SignatureServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Upprepa dessa steg för Forms tjänstklient.

1. Hämta det interaktiva formuläret med hjälp av tjänsten Forms

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra ett PDF-dokument som är signerat.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det PDF-dokument som ska signeras samt läget i vilket filen ska öppnas.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` egenskapen för bytearrayens innehåll.
   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra formulärdata.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för XML-filen som innehåller formulärdata, och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` egenskapen för bytearrayens innehåll.
   * Skapa en `PDFFormRenderSpec` objekt som används för att ange körningsalternativ. Tilldela värdet `true` till `PDFFormRenderSpec` objektets `generateServerAppearance` fält.
   * Anropa `FormsServiceClient` objektets `renderPDFForm2` och skicka följande värden:

      * A `BLOB` objekt som innehåller det PDF-formulär som ska återges.
      * A `BLOB` objekt som innehåller data som ska sammanfogas med formuläret.
      * A `PDFFormRenderSpec` objekt som lagrar körningsalternativ.
      * A `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten. Du kan ange `null` för det här parametervärdet.
      * A `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.
      * En lång utdataparameter som används för att lagra antalet sidor i formuläret.
      * En strängutdataparameter som används för språkvärdet.
      * A `FormResult` värde som är en utdataparameter som används för att lagra det interaktiva formuläret.

   * Hämta formuläret PDF genom att anropa `FormsResult` objektets `outputContent` fält. Det här fältet lagrar en `BLOB` objekt som representerar det interaktiva formuläret.

1. Signera det interaktiva formuläret

   Signera PDF-dokumentet genom att anropa `SignatureServiceClient` objektets `sign` och skicka följande värden:

   * A `BLOB` objekt som representerar det PDF-dokument som ska signeras. Använd `BLOB` -instans som returneras av Forms-tjänsten.
   * Ett strängvärde som representerar namnet på signaturfältet som är signerat.
   * A `Credential` objekt som representerar de autentiseringsuppgifter som används för att digitalt signera PDF-dokumentet. Skapa en `Credential` genom att använda konstruktorn och ange aliaset genom att tilldela ett värde till `Credential` objektets `alias` -egenskap.
   * A `HashAlgorithm` objekt som anger en statisk datamedlem som representerar hash-algoritmen som ska användas för att sammanfatta PDF-dokumentet. Du kan till exempel ange `HashAlgorithm.SHA1` om du vill använda SHA1-algoritmen.
   * Ett booleskt värde som anger om hash-algoritmen används.
   * Ett strängvärde som representerar orsaken till varför PDF-dokumentet signerades digitalt.
   * Ett strängvärde som representerar signerarens plats.
   * Ett strängvärde som representerar signerarens kontaktinformation.
   * A `PDFSignatureAppearanceOptions` som styr utseendet på den digitala signaturen. Du kan till exempel använda det här objektet för att lägga till en egen logotyp till en digital signatur.
   * A `System.Boolean` objekt som anger om spärrkontroll ska utföras på signerarens certifikat. Om spärrkontrollen är klar bäddas den in i signaturen. Standardvärdet är `false`.
   * An `OCSPPreferences` objekt som lagrar inställningar för stöd för OCSP (Online Certificate Status Protocol). Om spärrkontroll inte utförs används inte den här parametern och du kan ange `null`. Mer information om det här objektet finns i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` objekt som lagrar inställningar för listan över återkallade certifikat. Om spärrkontroll inte utförs används inte den här parametern och du kan ange `null`.
   * A `TSPPreferences` objekt som lagrar inställningar för stöd för tidsstämpelleverantör (TSP). Den här parametern är valfri och kan `null`.

   The `sign` returnerar en `BLOB` objekt som representerar det signerade PDF-dokumentet.

1. Spara det signerade PDF-dokumentet

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för det signerade PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `BLOB` objekt som returneras av `sign` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Digital Signing Interactive Forms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Certifiera PDF-dokument {#certifying-pdf-documents}

Du kan skydda ett PDF-dokument genom att certifiera det med en viss typ av signatur som kallas för en certifierad signatur. En certifierad signatur skiljer sig från en digital signatur på följande sätt:

* Det måste vara den första signaturen som tillämpas på dokumentet i PDF. Det vill säga, när den certifierade signaturen tillämpas, måste alla andra signaturfält i dokumentet vara osignerade. Endast en certifierad signatur tillåts i ett PDF-dokument. Om du vill signera och certifiera ett PDF-dokument måste du certifiera det innan du signerar det. När du har certifierat ett PDF-dokument kan du signera ytterligare signaturfält digitalt.
* Författaren eller författaren till dokumentet kan ange att dokumentet kan ändras på vissa sätt utan att den certifierade signaturen blir ogiltig. Dokumentet kan t.ex. tillåta ifyllnad av formulär eller kommentarer. Om författaren anger att en viss ändring inte är tillåten, begränsar Acrobat användare från att ändra dokumentet på det sättet. Om sådana ändringar görs, t.ex. om ett annat program används, är den certifierade signaturen ogiltig och Acrobat skickar en varning när en användare öppnar dokumentet. (Med icke-certifierade signaturer förhindras inte ändringar och normala redigeringsåtgärder gör inte den ursprungliga signaturen ogiltig.)
* Vid tidpunkten för signering genomsöks dokumentet efter specifika typer av innehåll som kan göra innehållet i ett dokument tvetydigt eller vilseledande. En anteckning kan t.ex. dölja text på en sida som är viktig för att förstå vad som certifieras. En förklaring (juridisk attestering) kan ges om sådant innehåll.

Du kan certifiera PDF-dokument programmatiskt med hjälp av Java API:t för signaturtjänsten eller API:t för signaturwebbtjänsten. När du certifierar ett PDF-dokument måste du referera till en säkerhetsreferens som finns i tjänsten Credential. Mer information om säkerhetsuppgifter finns i *Installera och distribuera AEM Forms* guide för programservern.

>[!NOTE]
>
>När du certifierar och signerar samma dokument i PDF visas en gul triangel bredvid den första signeringssignaturen när du öppnar dokumentet i PDF i Acrobat eller Adobe Reader, om certifikatsignaturen inte är tillförlitlig. Certifikatsignaturen måste vara betrodd för att den här situationen ska undvikas.

>[!NOTE]
>
>När du använder en Cipher Shield HSM-autentiseringsuppgift för att signera eller certifiera ett PDF-dokument, kan den nya autentiseringsuppgiften inte användas förrän J2EE-programservern som AEM Forms är distribuerad på har startats om. Du kan dock ange ett konfigurationsvärde, vilket gör att signerings- eller certifieringsåtgärden fungerar utan att J2EE-programservern startas om.

Du kan lägga till följande konfigurationsvärde i filen cknfastrc, som finns på /opt/nfast/cknfastrc (eller c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

När du har lagt till det här konfigurationsvärdet i cknfastrc-filen kan de nya autentiseringsuppgifterna användas utan att J2EE-programservern startas om.

>[!NOTE]
>
>Mer information om signaturtjänsten och certifiering av ett dokument finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-5}

Så här certifierar du ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en signaturklient.
1. Hämta PDF-dokumentet som ska certifieras.
1. Certifiera PDF-dokumentet.
1. Spara det certifierade PDF-dokumentet som en PDF-fil.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klassökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

Mer information om var dessa JAR-filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Skapa en signaturklient**

Innan du programmässigt kan utföra en signeringsåtgärd måste du skapa en signaturklient.

**Hämta PDF-dokumentet för certifiering**

Om du vill certifiera ett PDF-dokument måste du skaffa ett PDF-dokument som innehåller ett signaturfält. Om ett PDF-dokument inte innehåller något signaturfält kan det inte certifieras. Ett signaturfält kan läggas till med Designer eller via programmering. Mer information om att lägga till ett signaturfält programmatiskt finns i [Lägga till signaturfält](digitally-signing-certifying-documents.md#adding-signature-fields).

**Certifiera PDF-dokumentet**

Om du vill certifiera ett PDF-dokument måste du ange följande indatavärden som används av signaturtjänsten för att certifiera ett PDF-dokument:

* **PDF dokument**: Ett dokument i PDF som innehåller ett signaturfält, som är ett formulärfält som innehåller en grafisk representation av den certifierade signaturen. Ett PDF-dokument måste innehålla ett signaturfält innan det kan certifieras. Ett signaturfält kan läggas till med Designer eller via programmering. (Se [Lägga till signaturfält](digitally-signing-certifying-documents.md#adding-signature-fields).)
* **Namn på signaturfält**: Det fullständiga, kvalificerade namnet på signaturfältet som är certifierat. Följande värde är ett exempel: `form1[0].#subform[1].SignatureField3[3]`. När du använder ett XFA-formulärfält kan du även använda det partiella namnet på signaturfältet: `SignatureField3[3]`. Om ett null-värde skickas för fältnamnet skapas och certifieras ett osynligt signaturfält dynamiskt.
* **Säkerhetsuppgifter**: En autentiseringsuppgift som används för att certifiera PDF-dokumentet. Den här säkerhetsreferensen innehåller ett lösenord och ett alias, som måste matcha ett alias som visas i den autentiseringsuppgift som finns i autentiseringsuppgiften. Aliaset är en referens till en faktisk autentiseringsuppgift som kan finnas i en PKCS#12-fil (med filnamnstillägget .pfx) eller en maskinvarusäkerhetsmodul (HSM).
* **Hash-algoritm**: En hash-algoritm som används för att sammanställa PDF-dokumentet.
* **Anledning till signering**: Ett värde som visas i Acrobat eller Adobe Reader så att andra användare vet varför PDF-dokumentet certifierades.
* **Undertecknarens plats**: Platsen för signeraren som anges av autentiseringsuppgifterna.
* **Kontaktinformation**: Undertecknarens kontaktinformation, till exempel adress och telefonnummer.
* **Behörighetsinformation**: Behörigheter som styr de åtgärder som en slutanvändare kan utföra på ett dokument utan att den certifierade signaturen blir ogiltig. Du kan till exempel ställa in behörigheten så att den certifierade signaturen blir ogiltig om du ändrar PDF-dokumentet.
* **Juridisk förklaring**: När ett dokument är certifierat skannas det automatiskt efter specifika typer av innehåll som kan göra innehållet i ett dokument tvetydigt eller vilseledande. En anteckning kan t.ex. dölja text på en sida som är viktig för att förstå vad som certifieras. Skanningsprocessen genererar varningar om dessa typer av innehåll. Det här värdet ger ytterligare en förklaring av innehållet som kan ha genererat varningar.
* **Utseendealternativ**: Alternativ som styr utseendet på den certifierade signaturen. Den certifierade signaturen kan t.ex. visa datuminformation.
* **Spärrkontroll**: Det här värdet anger om spärrkontroll utförs för signerarens certifikat. Standardinställningen för `false` innebär att spärrkontroll inte utförs.
* **OCSP-inställningar**: Inställningar för stöd för OCSP (Online Certificate Status Protocol), som ger information om statusen för den autentiseringsuppgift som används för att certifiera PDF-dokumentet. Du kan till exempel ange webbadressen till servern som innehåller information om de autentiseringsuppgifter som du använder för att logga in på PDF-dokumentet.
* **CRL-inställningar**: Inställningar för inställningar för listan över återkallade certifikat (CRL) om spärrkontroll utförs. Du kan till exempel ange att alltid ska kontrollera om en autentiseringsuppgift har återkallats.
* **Tidsstämpling**: Inställningar som definierar tidsstämpelinformation som används för den certifierade signaturen. En tidsstämpel anger att specifika data har upprättats före en viss tid. Denna kunskap hjälper till att bygga upp en förtroenderelation mellan signeraren och verifieraren.

**Spara det certifierade PDF-dokumentet som en PDF-fil**

När signaturtjänsten har certifierat PDF-dokumentet kan du spara det som en PDF-fil så att användare kan öppna det i Acrobat eller Adobe Reader.

**Se även**

[Certifiera PDF-dokument med Java API](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[Certifiera PDF-dokument med hjälp av webbtjänstens API](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Lägga till signaturfält](digitally-signing-certifying-documents.md#adding-signature-fields)

### Certifiera PDF-dokument med Java API {#certify-pdf-documents-using-the-java-api}

Certifiera ett PDF-dokument med signatur-API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-signatures-client.jar, i Java-projektets klassökväg.

1. Skapa en signaturklient

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `SignatureServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta PDF-dokumentet för certifiering

   * Skapa en `java.io.FileInputStream` objekt som representerar det PDF-dokument som ska certifieras med hjälp av dess konstruktor och som skickar ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Certifiera PDF-dokumentet

   Certifiera PDF-dokumentet genom att anropa `SignatureServiceClient` objektets `certify` och skicka följande värden:

   * The `com.adobe.idp.Document` objekt som representerar det PDF-dokument som ska certifieras.
   * Ett strängvärde som representerar namnet på signaturfältet som ska innehålla signaturen.
   * A `Credential` objekt som representerar de autentiseringsuppgifter som används för att certifiera PDF-dokumentet. Skapa en `Credential` genom att anropa `Credential` objektets statiska `getInstance` och skickar ett strängvärde som anger aliasvärdet som motsvarar säkerhetsuppgifter.
   * A `HashAlgorithm` objekt som anger en statisk datamedlem som representerar den hash-algoritm som används för att sammanställa PDF-dokumentet. Du kan till exempel ange `HashAlgorithm.SHA1` om du vill använda SHA1-algoritmen.
   * Ett strängvärde som representerar orsaken till varför PDF-dokumentet certifierades.
   * Ett strängvärde som representerar signerarens kontaktinformation.
   * A `MDPPermissions` objekt som anger åtgärder som kan utföras på dokumentet PDF som gör underskriften ogiltig.
   * A `PDFSignatureAppearanceOptions` som styr utseendet på den certifierade signaturen. Ändra signaturens utseende genom att anropa en metod, till exempel `setShowDate`.
   * Ett strängvärde som ger en förklaring till vilka åtgärder som gör underskriften ogiltig.
   * A `java.lang.Boolean` objekt som anger om spärrkontroll ska utföras på signerarens certifikat. Om spärrkontrollen är klar bäddas den in i signaturen. Standardvärdet är `false`.
   * A `java.lang.Boolean` objekt som anger om signaturfältet som certifieras är låst. Om fältet är låst markeras signaturfältet som skrivskyddat, dess egenskaper kan inte ändras och det kan inte rensas av någon som inte har de behörigheter som krävs. Standardvärdet är `false`.
   * An `OCSPPreferences` objekt som lagrar inställningar för stöd för OCSP (Online Certificate Status Protocol). Om spärrkontroll inte utförs används inte den här parametern och du kan ange `null`. Mer information om det här objektet finns i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` objekt som lagrar inställningar för listan över återkallade certifikat. Om spärrkontroll inte utförs används inte den här parametern och du kan ange `null`.
   * A `TSPPreferences` objekt som lagrar inställningar för stöd för tidsstämpelleverantör (TSP). När du t.ex. har skapat en `TSPPreferences` kan du ange TSP-serverns URL genom att anropa `TSPPreferences` objektets `setTspServerURL` -metod. Den här parametern är valfri och kan `null`. Mer information finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

   The `certify` returnerar en `com.adobe.idp.Document` -objekt som representerar det certifierade PDF-dokumentet.

1. Spara det certifierade PDF-dokumentet som en PDF-fil

   * Skapa en `java.io.File` och se till att filtillägget är .pdf.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att kopiera innehållet i `com.adobe.idp.Document` till filen.

**Se även**

[Certifiera PDF-dokument](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Snabbstart (SOAP): certifiera ett PDF-dokument med Java API](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Certifiera PDF-dokument med hjälp av webbtjänstens API {#certify-pdf-documents-using-the-web-service-api}

Certifiera ett PDF-dokument med hjälp av signatur-API:t (webbtjänst):

1. Inkludera projektfiler

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en signaturklient

   * Skapa en `SignatureServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `SignatureServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/SignatureService?WSDL`). Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `SignatureServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta PDF-dokumentet för certifiering

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra ett certifierat PDF-dokument.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det PDF-dokument som ska certifieras och läget i vilket filen ska öppnas.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` datamedlem innehållet i bytearrayen.

1. Certifiera PDF-dokumentet

   Certifiera PDF-dokumentet genom att anropa `SignatureServiceClient` objektets `certify` och skicka följande värden:

   * The `BLOB` objekt som representerar det PDF-dokument som ska certifieras.
   * Ett strängvärde som representerar namnet på signaturfältet som ska innehålla signaturen.
   * A `Credential` objekt som representerar de autentiseringsuppgifter som används för att certifiera PDF-dokumentet. Skapa en `Credential` genom att använda konstruktorn och ange aliaset genom att tilldela ett värde till `Credential` objektets `alias` -egenskap.
   * A `HashAlgorithm` objekt som anger en statisk datamedlem som representerar den hash-algoritm som används för att sammanställa PDF-dokumentet. Du kan till exempel ange `HashAlgorithm.SHA1` om du vill använda SHA1-algoritmen.
   * Ett booleskt värde som anger om hash-algoritmen används.
   * Ett strängvärde som representerar orsaken till varför PDF-dokumentet certifierades.
   * Ett strängvärde som representerar signerarens plats.
   * Ett strängvärde som representerar signerarens kontaktinformation.
   * An `MDPPermissions` objektets statiska datamedlem som anger åtgärder som kan utföras på det PDF-dokument som gör underskriften ogiltig.
   * Ett booleskt värde som anger om `MDPPermissions` objekt som skickades som föregående parametervärde.
   * Ett strängvärde som förklarar vilka åtgärder som gör underskriften ogiltig.
   * A `PDFSignatureAppearanceOptions` som styr utseendet på den certifierade signaturen. Skapa en `PDFSignatureAppearanceOptions` genom att använda dess konstruktor. Du kan ändra signaturens utseende genom att ange en av dess datamedlemmar.
   * A `System.Boolean` objekt som anger om spärrkontroll ska utföras på signerarens certifikat. Om spärrkontrollen är klar bäddas den in i signaturen. Standardvärdet är `false`.
   * A `System.Boolean` objekt som anger om signaturfältet som certifieras är låst. Om fältet är låst markeras signaturfältet som skrivskyddat, dess egenskaper kan inte ändras och det kan inte rensas av någon som inte har de behörigheter som krävs. Standardvärdet är `false`.
   * A `System.Boolean` -objekt som anger om signaturfältet är låst. Det vill säga, om du passerar `true` till föregående parameter och skicka sedan `true` till den här parametern.
   * An `OCSPPreferences` objekt som lagrar inställningar för OCSP-stöd (Online Certificate Status Protocol), som ger information om statusen för de autentiseringsuppgifter som används för att certifiera PDF-dokumentet. Om spärrkontroll inte utförs används inte den här parametern och du kan ange `null`.
   * A `CRLPreferences` objekt som lagrar inställningar för listan över återkallade certifikat. Om spärrkontroll inte utförs används inte den här parametern och du kan ange `null`.
   * A `TSPPreferences` objekt som lagrar inställningar för stöd för tidsstämpelleverantör (TSP). När du t.ex. har skapat en `TSPPreferences` -objektet kan du ange TSP:ens URL genom att ställa in `TSPPreferences` objektets `tspServerURL` datamedlem. Den här parametern är valfri och kan `null`.

   The `certify` returnerar en `BLOB` -objekt som representerar det certifierade PDF-dokumentet.

1. Spara det certifierade PDF-dokumentet som en PDF-fil

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det PDF-dokument som innehåller det certifierade PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `BLOB` objekt som returneras av `certify` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `binaryData` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Certifiera PDF-dokument](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifierar digitala signaturer {#verifying-digital-signatures}

Digitala signaturer kan verifieras för att säkerställa att ett signerat PDF-dokument inte ändras och att den digitala signaturen är giltig. När du verifierar en digital signatur kan du kontrollera signaturens status och dess egenskaper, t.ex. signerarens identitet. Innan du litar på en elektronisk underskrift bör du verifiera den. När du verifierar en digital signatur refererar du till ett PDF-dokument som innehåller en digital signatur.

Anta att undertecknarens identitet är okänd. När du öppnar PDF-dokumentet i Acrobat visas ett varningsmeddelande om att undertecknarens identitet är okänd, vilket visas på följande bild.

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

På samma sätt kan du, när du programmässigt verifierar en digital signatur, fastställa status för signerarens identitet. Om du till exempel verifierar den digitala signaturen i dokumentet som visas i föregående bild, blir resultatet att signerarens identitet är okänd.

>[!NOTE]
>
>Mer information om signaturtjänsten och verifiering av digitala signaturer finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-6}

Så här verifierar du en digital signatur:

1. Inkludera projektfiler.
1. Skapa en signaturklient.
1. Hämta det PDF-dokument som innehåller den signatur som ska verifieras.
1. Ange alternativ för PKI-körning.
1. Verifiera den digitala signaturen.
1. Fastställ signaturens status.
1. Identifiera undertecknarens identitet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

Följande JAR-filer måste läggas till i projektets klassökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

Mer information om var dessa JAR-filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Skapa en signaturklient**

Skapa en signaturtjänstklient innan du programmässigt utför en signeringstjänståtgärd.

**Hämta PDF-dokumentet som innehåller signaturen som ska verifieras**

Om du vill verifiera en signatur som används för att digitalt signera eller certifiera ett PDF-dokument, ska du hämta ett PDF-dokument som innehåller en signatur.

**Ange alternativ för PKI-körning**

Ange följande PKI-körningsalternativ som används av signaturtjänsten när signaturer verifieras i ett PDF-dokument:

* Verifieringstid
* Spärrkontroll
* Tidsstämplingsvärden

Som en del av inställningen av dessa alternativ kan du ange verifieringstid. Du kan till exempel välja aktuell tid (tiden på validerarens dator), vilket anger att den aktuella tiden ska användas. Information om de olika tidsvärdena finns i `VerificationTime` uppräkningsvärde i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Du kan också ange om spärrkontroll ska utföras som en del av verifieringsprocessen. Du kan till exempel utföra en spärrkontroll för att avgöra om certifikatet har återkallats. Mer information om alternativen för spärrkontroll finns i `RevocationCheckStyle` uppräkningsvärde i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Om du vill göra en återkallningskontroll på ett certifikat anger du en URL till en CRL-server (Certificate revocation List) med hjälp av en `CRLOptionSpec` -objekt. Om du inte anger en URL till en CRL-server hämtar signaturtjänsten URL:en från certifikatet.

I stället för att använda en CRL-server kan du använda en OCSP-server (Online Certificate Status Protocol) när du utför spärrkontroll. När du använder en OCSP-server i stället för en CRL-server utförs spärrkontrollen oftast snabbare. (Se [Statusprotokoll för onlinecertifikat](https://tools.ietf.org/html/rfc2560).)

Du kan ställa in CRL- och OCSP-serverordningen som används av signaturtjänsten med Adobe-program och -tjänster. Om till exempel OCSP-servern är inställd först i Adobe-program och -tjänster kontrolleras OCSP-servern, som följs av CRL-servern.

Om du inte utför spärrkontroll kontrollerar inte signaturtjänsten om certifikatet har spärrats. CRL- och OCSP-serverinformation ignoreras alltså.

>[!NOTE]
>
>Du kan åsidosätta URL:en som anges i certifikatet genom att använda en `CRLOptionSpec` och `OCSPOptionSpec` -objekt. Om du till exempel vill åsidosätta CRL-servern kan du anropa `CRLOptionSpec` objektets `setLocalURI` -metod.

Tidsstämpling är processen att spåra den tid då ett signerat eller certifierat dokument ändrades. När ett dokument har signerats kan ingen ändra det. Tidsstämpling gör det lättare att framtvinga giltigheten av ett undertecknat eller certifierat dokument. Du kan ange tidsstämplingsalternativ med en `TSPOptionSpec` -objekt. Du kan till exempel ange URL:en för en TSP-server (Time Stamping Provider).

>[!NOTE]
>
>I snabbstarten för Java och webbtjänsten anges verifieringstiden till `VerificationTime.CURRENT_TIME` och spärrkontroll är inställd på `RevocationCheckStyle.BestEffort`. Eftersom ingen CRL- eller OCSP-serverinformation har angetts hämtas serverinformationen från certifikatet.

**Verifiera den digitala signaturen**

Om du vill verifiera en signatur anger du det fullständiga, kvalificerade namnet på signaturfältet som innehåller signaturen, till exempel `form1[0].#subform[1].SignatureField3[3]`. När du använder ett XFA-formulärfält kan du även använda det partiella namnet på signaturfältet: `SignatureField3`.

Som standard begränsar signaturtjänsten den tid som ett dokument kan signeras efter valideringstiden till 65 min. Om en användare försöker verifiera en signatur vid den aktuella tidpunkten och signeringstiden är senare än den aktuella tiden och är inom 65 minuter, skapar inte signaturtjänsten något verifieringsfel.

>[!NOTE]
>
>Andra värden som du behöver när du verifierar en signatur finns i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Bestäm signaturens status**

Som en del av verifieringen av en digital signatur kan du kontrollera signaturens status.

**Bestämma signerarens identitet**

Du kan bestämma signerarens identitet, vilket kan vara något av följande värden:

* **Okänd**: Den här signeraren är okänd eftersom det inte går att utföra signerarverifieringen.
* **Betrodd**: Den här signeraren är betrodd.
* **Ej betrodd**: Den här signeraren är inte betrodd.

**Se även**

[Verifiera digitala signaturer med Java API](#verify-digital-signatures-using-the-java-api)

[Verifiera digitala signaturer med webbtjänstens API](#verify-digital-signatures-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verifiera digitala signaturer med Java API {#verify-digital-signatures-using-the-java-api}

Verifiera en digital signatur med hjälp av Signature Service API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-signatures-client.jar, i Java-projektets klassökväg.

1. Skapa en signaturklient

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `SignatureServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta PDF-dokumentet som innehåller signaturen som ska verifieras

   * Skapa en `java.io.FileInputStream` -objekt som representerar det PDF-dokument som innehåller underskriften som ska verifieras med hjälp av dess konstruktor. Skicka ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ange alternativ för PKI-körning

   * Skapa en `PKIOptions` genom att använda dess konstruktor.
   * Ställ in verifieringstiden genom att anropa `PKIOptions` objektets `setVerificationTime` metod och skicka en `VerificationTime` uppräkningsvärde som anger verifieringstiden.
   * Ange alternativet för spärrkontroll genom att anropa `PKIOptions` objektets `setRevocationCheckStyle` metod och skicka en `RevocationCheckStyle` uppräkningsvärde som anger om spärrkontroll ska utföras.

1. Verifiera den digitala signaturen

   Verifiera signaturen genom att anropa `SignatureServiceClient` objektets `verify2` och skicka följande värden:

   * A `com.adobe.idp.Document` objekt som innehåller ett digitalt signerat eller certifierat PDF-dokument.
   * Ett strängvärde som representerar signaturfältets namn som innehåller signaturen som ska verifieras.
   * A `PKIOptions` objekt som innehåller alternativ för PKI-körning.
   * A `VerifySPIOptions` -instans som innehåller SPI-information. Du kan ange `null` för parametern.

   The `verify2` returnerar en `PDFSignatureVerificationInfo` objekt som innehåller information som kan användas för att verifiera den digitala signaturen.

1. Bestäm signaturens status

   * Kontrollera signaturens status genom att anropa `PDFSignatureVerificationInfo` objektets `getStatus` -metod. Den här metoden returnerar en `SignatureStatus` objekt som anger signaturens status. Om t.ex. ett signerat PDF-dokument inte ändras returnerar den här metoden `SignatureStatus.DocumentSigNoChanges`.

1. Bestämma signerarens identitet

   * Bestäm signerarens identitet genom att anropa `PDFSignatureVerificationInfo` objektets `getSigner` -metod. Den här metoden returnerar en `IdentityInformation` -objekt.
   * Anropa `IdentityInformation` objektets `getStatus` metod för att fastställa signerarens identitet. Den här metoden returnerar en `IdentityStatus` uppräkningsvärde som anger identiteten. Om signeraren är betrodd returnerar den här metoden `IdentityStatus.TRUSTED`.

**Se även**

[Verifierar digitala signaturer](#verify-digital-signatures-using-the-java-api)

[Snabbstart (SOAP): Verifiera en digital signatur med Java API](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verifiera digitala signaturer med webbtjänstens API {#verify-digital-signatures-using-the-web-service-api}

Verifiera en digital signatur med hjälp av Signature Service API (webbtjänst):

1. Inkludera projektfiler

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en signaturklient

   * Skapa en `SignatureServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `SignatureServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/SignatureService?WSDL`). Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `SignatureServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta PDF-dokumentet som innehåller signaturen som ska verifieras

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` används för att lagra ett PDF-dokument som innehåller en digital eller certifierad signatur som ska verifieras.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för det signerade PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` egenskapen för bytearrayens innehåll.

1. Ange alternativ för PKI-körning

   * Skapa en `PKIOptions` genom att använda dess konstruktor.
   * Ange verifieringstid genom att tilldela `PKIOptions` objektets `verificationTime` datamedlem en `VerificationTime` uppräkningsvärde som anger verifieringstiden.
   * Ange alternativet för spärrkontroll genom att tilldela `PKIOptions` objektets `revocationCheckStyle` datamedlem en `RevocationCheckStyle` uppräkningsvärde som anger om spärrkontroll ska utföras.

1. Verifiera den digitala signaturen

   Verifiera signaturen genom att anropa `SignatureServiceClient` objektets `verify2` och skicka följande värden:

   * The `BLOB` objekt som innehåller ett digitalt signerat eller certifierat PDF-dokument.
   * Ett strängvärde som representerar signaturfältets namn som innehåller signaturen som ska verifieras.
   * A `PKIOptions` objekt som innehåller alternativ för PKI-körning.
   * A `VerifySPIOptions` -instans som innehåller SPI-information. Du kan ange `null` för parametern.

   The `verify2` returnerar en `PDFSignatureVerificationInfo` objekt som innehåller information som kan användas för att verifiera den digitala signaturen.

1. Bestäm signaturens status

   Bestäm signaturens status genom att hämta värdet för `PDFSignatureVerificationInfo` objektets `status` datamedlem. Denna datamedlem lagrar en `SignatureStatus` objekt som anger signaturens status. Om till exempel ett signerat PDF-dokument ändras visas `status` datamedlemmen lagrar värdet `SignatureStatus.DocumentSigNoChanges`.

1. Bestämma signerarens identitet

   * Bestäm signerarens identitet genom att hämta värdet för `PDFSignatureVerificationInfo` objektets `signer` datamedlem. Medlemmen returnerar en `IdentityInformation` -objekt.
   * Hämta `IdentityInformation` objektets `status` datamedlem som avgör undertecknarens identitet. Den här datamedlemmen returnerar en `IdentityStatus` uppräkningsvärde som anger identiteten. Om signeraren är betrodd returnerar den här medlemmen `IdentityStatus.TRUSTED`.

**Se även**

[Verifierar digitala signaturer](#verify-digital-signatures-using-the-java-api)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifierar flera digitala signaturer {#verifying-multiple-digital-signatures}

AEM Forms ger möjlighet att verifiera alla digitala signaturer i ett PDF-dokument. Anta att ett PDF-dokument innehåller flera digitala signaturer som ett resultat av en affärsprocess som kräver signaturer från flera signerare. Ta till exempel en finansiell transaktion som kräver både en lånesammans och en chefs underskrift. Du kan använda Java API:t för signaturtjänsten eller webbtjänstens API för att verifiera alla signaturer i PDF-dokumentet. När du verifierar flera digitala signaturer kan du kontrollera status och egenskaper för varje signatur. Innan du litar på en elektronisk underskrift bör du verifiera den. Vi rekommenderar att du är bekant med att verifiera en enda digital signatur.

>[!NOTE]
>
>Mer information om signaturtjänsten och verifiering av digitala signaturer finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-7}

Så här verifierar du flera digitala signaturer:

1. Inkludera projektfiler.
1. Skapa en signaturklient.
1. Hämta det PDF-dokument som innehåller signaturerna som ska verifieras.
1. Ange alternativ för PKI-körning.
1. Hämta alla digitala signaturer.
1. Upprepa med alla signaturer.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

Följande JAR-filer måste läggas till i projektets klassökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

Mer information om var dessa JAR-filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Skapa en signaturklient**

Skapa en signaturtjänstklient innan du programmässigt utför en signeringstjänståtgärd.

**Hämta PDF-dokumentet som innehåller signaturerna som ska verifieras**

Om du vill verifiera en signatur som används för att digitalt signera eller certifiera ett PDF-dokument, ska du hämta ett PDF-dokument som innehåller en signatur.

**Ange alternativ för PKI-körning**

Ange följande PKI-körningsalternativ som används av signaturtjänsten när alla signaturer i ett PDF-dokument verifieras:

* Verifieringstid
* Spärrkontroll
* Tidsstämplingsvärden

Som en del av inställningen av dessa alternativ kan du ange verifieringstid. Du kan till exempel välja aktuell tid (tiden på validerarens dator), vilket anger att den aktuella tiden ska användas. Information om de olika tidsvärdena finns i `VerificationTime` uppräkningsvärde i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Du kan också ange om spärrkontroll ska utföras som en del av verifieringsprocessen. Du kan till exempel utföra en spärrkontroll för att avgöra om certifikatet har återkallats. Mer information om alternativen för spärrkontroll finns i `RevocationCheckStyle` uppräkningsvärde i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Om du vill göra en återkallningskontroll på ett certifikat anger du en URL till en CRL-server (Certificate revocation List) med hjälp av en `CRLOptionSpec` -objekt. Om du inte anger en URL till en CRL-server hämtar signaturtjänsten URL:en från certifikatet.

I stället för att använda en CRL-server kan du använda en OCSP-server (Online Certificate Status Protocol) när du utför spärrkontroll. När du använder en OCSP-server i stället för en CRL-server utförs spärrkontrollen oftast snabbare. (Se [Statusprotokoll för onlinecertifikat](https://tools.ietf.org/html/rfc2560).)

Du kan ställa in CRL- och OCSP-serverordningen som används av signaturtjänsten med Adobe-program och -tjänster. Om till exempel OCSP-servern är inställd först i Adobe-program och -tjänster kontrolleras OCSP-servern, som följs av CRL-servern.

Om du inte utför spärrkontroll kontrollerar inte signaturtjänsten om certifikatet har spärrats. CRL- och OCSP-serverinformation ignoreras alltså.

>[!NOTE]
>
>Du kan åsidosätta URL:en som anges i certifikatet genom att använda en `CRLOptionSpec` och `OCSPOptionSpec` -objekt. Om du till exempel vill åsidosätta CRL-servern kan du anropa `CRLOptionSpec` objektets `setLocalURI` -metod.

Tidsstämpling är processen att spåra den tid då ett signerat eller certifierat dokument ändrades. När ett dokument har signerats kan ingen ändra det. Tidsstämpling gör det lättare att framtvinga giltigheten av ett undertecknat eller certifierat dokument. Du kan ange tidsstämplingsalternativ med en `TSPOptionSpec` -objekt. Du kan till exempel ange URL:en för en TSP-server (Time Stamping Provider).

>[!NOTE]
>
>I snabbstarten för Java och webbtjänsten anges verifieringstiden till `VerificationTime.CURRENT_TIME` och spärrkontroll är inställd på `RevocationCheckStyle.BestEffort`. Eftersom ingen CRL- eller OCSP-serverinformation har angetts hämtas serverinformationen från certifikatet.

**Hämta alla digitala signaturer**

Om du vill verifiera alla digitala signaturer i ett PDF-dokument hämtar du de digitala signaturerna från PDF-dokumentet. Alla signaturer returneras i en lista. Som en del av verifieringen av en digital signatur kontrollerar du signaturens status.

>[!NOTE]
>
>Till skillnad från när du verifierar en enda elektronisk underskrift behöver du inte ange signaturfältets namn när du verifierar flera underskrifter.

**Upprepa med alla signaturer**

Iterera genom varje signatur. Det vill säga, för varje signatur, verifiera den digitala signaturen och kontrollera signerarens identitet och status för varje signatur. (Se [Verifierar digitala signaturer](#verify-digital-signatures-using-the-java-api).)

>[!NOTE]
>
>Du behöver inte iterera igenom alla signaturer om kravet är hela dokumentet.

**Se även**

[Verifiera flera digitala signaturer med Java API](#verify-digital-signatures-using-the-java-api)

[Verifiera flera digitala signaturer med webbtjänstens API](#verify-digital-signatures-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verifiera flera digitala signaturer med Java API {#verify-multiple-digital-signatures-using-the-java-api}

Verifiera flera digitala signaturer med Signature Service API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-signatures-client.jar, i Java-projektets klassökväg.

1. Skapa en signaturklient

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `SignatureServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta PDF-dokumentet som innehåller signaturerna som ska verifieras

   * Skapa en `java.io.FileInputStream` objekt som representerar det PDF-dokument som innehåller flera digitala signaturer som ska verifieras med hjälp av dess konstruktor. Skicka ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ange alternativ för PKI-körning

   * Skapa en `PKIOptions` genom att använda dess konstruktor.
   * Ställ in verifieringstiden genom att anropa `PKIOptions` objektets `setVerificationTime` metod och skicka en `VerificationTime` uppräkningsvärde som anger verifieringstiden.
   * Ange alternativet för spärrkontroll genom att anropa `PKIOptions` objektets `setRevocationCheckStyle` metod och skicka en `RevocationCheckStyle` uppräkningsvärde som anger om spärrkontroll ska utföras.

1. Hämta alla digitala signaturer

   Anropa `SignatureServiceClient` objektets `verifyPDFDocument` och skicka följande värden:

   * A `com.adobe.idp.Document` objekt som innehåller ett PDF-dokument som innehåller flera digitala signaturer.
   * A `PKIOptions` objekt som innehåller alternativ för PKI-körning.
   * A `VerifySPIOptions` -instans som innehåller SPI-information. Du kan ange `null` för parametern.

   The `verifyPDFDocument` returnerar en `PDFDocumentVerificationInfo` objekt som innehåller information om alla digitala signaturer i PDF-dokumentet.

1. Upprepa med alla signaturer

   * Iterera genom alla signaturer genom att anropa `PDFDocumentVerificationInfo` objektets `getVerificationInfos` -metod. Den här metoden returnerar en `java.util.List` objekt där varje element är ett `PDFSignatureVerificationInfo` -objekt. Använd en `java.util.Iterator` objekt som ska itereras igenom signaturlistan.
   * Använda `PDFSignatureVerificationInfo` kan du utföra uppgifter som att fastställa signaturens status genom att anropa `PDFSignatureVerificationInfo` objektets `getStatus` -metod. Den här metoden returnerar en `SignatureStatus` objekt vars statiska datamedlem informerar dig om signaturens status. Om signaturen till exempel är okänd returnerar den här metoden `SignatureStatus.DocumentSignatureUnknown`.

**Se även**

[Verifierar flera digitala signaturer](#verifying-multiple-digital-signatures)

[Snabbstart (SOAP): Verifiera flera digitala signaturer med Java API](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Verifierar digitala signaturer](#verify-digital-signatures-using-the-java-api)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verifiera flera digitala signaturer med webbtjänstens API {#verifying-multiple-digital-signatures-using-the-web-service-api}

Verifiera flera digitala signaturer med Signature Service API (webbtjänst):

1. Inkludera projektfiler

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en signaturklient

   * Skapa en `SignatureServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `SignatureServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/SignatureService?WSDL`). Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `SignatureServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta PDF-dokumentet som innehåller signaturerna som ska verifieras

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet lagrar ett PDF-dokument som innehåller flera digitala signaturer som ska verifieras.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` egenskapen för bytearrayens innehåll.

1. Ange alternativ för PKI-körning

   * Skapa en `PKIOptions` genom att använda dess konstruktor.
   * Ange verifieringstid genom att tilldela `PKIOptions` objektets `verificationTime` datamedlem en `VerificationTime` uppräkningsvärde som anger verifieringstiden.
   * Ange alternativet för spärrkontroll genom att tilldela `PKIOptions` objektets `revocationCheckStyle` datamedlem en `RevocationCheckStyle` uppräkningsvärde som anger om spärrkontroll ska utföras.

1. Hämta alla digitala signaturer

   Anropa `SignatureServiceClient` objektets `verifyPDFDocument` och skicka följande värden:

   * A `BLOB` objekt som innehåller ett PDF-dokument som innehåller flera digitala signaturer.
   * A `PKIOptions` objekt som innehåller alternativ för PKI-körning.
   * A `VerifySPIOptions` -instans som innehåller SPI-information. Du kan ange null för den här parametern.

   The `verifyPDFDocument` returnerar en `PDFDocumentVerificationInfo` objekt som innehåller information om alla digitala signaturer i PDF-dokumentet.

1. Upprepa med alla signaturer

   * Iterera genom alla signaturer genom att hämta `PDFDocumentVerificationInfo` objektets `verificationInfos` datamedlem. Den här datamedlemmen returnerar en `Object` array där varje element är en `PDFSignatureVerificationInfo` -objekt.
   * Använda `PDFSignatureVerificationInfo` -objektet kan du utföra åtgärder som att fastställa signaturens status genom att hämta `PDFSignatureVerificationInfo` objektets `status` datamedlem. Den här datamedlemmen returnerar en `SignatureStatus` objekt vars statiska datamedlem informerar dig om signaturens status. Om signaturen till exempel är okänd returnerar den här metoden `SignatureStatus.DocumentSignatureUnknown`.

**Se även**

[Verifierar flera digitala signaturer](#verifying-multiple-digital-signatures)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Tar bort digitala signaturer {#removing-digital-signatures}

Digitala signaturer måste tas bort från ett signaturfält innan en nyare digital signatur kan användas. En digital signatur kan inte skrivas över. Om du försöker tillämpa en digital signatur på ett signaturfält som innehåller en signatur inträffar ett undantag.

>[!NOTE]
>
>Mer information om signaturtjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-8}

Så här tar du bort en digital signatur från ett signaturfält:

1. Inkludera projektfiler.
1. Skapa en signaturklient.
1. Hämta det PDF-dokument som innehåller en signatur som ska tas bort.
1. Ta bort den digitala signaturen från signaturfältet.
1. Spara PDF-dokumentet som en PDF-fil.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klassökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

Mer information om var dessa JAR-filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Skapa en signaturklient**

Innan du programmässigt kan utföra en signeringstjänståtgärd måste du skapa en signaturtjänstklient.

**Hämta PDF-dokumentet som innehåller en signatur som ska tas bort**

Om du vill ta bort en signatur från ett PDF-dokument måste du skaffa ett PDF-dokument som innehåller en signatur.

**Ta bort den digitala signaturen från signaturfältet**

Om du vill ta bort en digital signatur från ett PDF-dokument måste du ange namnet på signaturfältet som innehåller den digitala signaturen. Du måste också ha behörighet att ta bort den digitala signaturen, annars inträffar ett undantag.

**Spara PDF-dokumentet som en PDF-fil**

När signaturtjänsten har tagit bort en digital signatur från ett signaturfält kan du spara PDF-dokumentet som en PDF-fil så att användare kan öppna det i Acrobat eller Adobe Reader.

**Se även**

[Ta bort digitala signaturer med Java API](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[Ta bort digitala signaturer med webbtjänstens API](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Lägga till signaturfält](digitally-signing-certifying-documents.md#adding-signature-fields)

### Ta bort digitala signaturer med Java API {#remove-digital-signatures-using-the-java-api}

Ta bort en digital signatur med signatur-API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-signatures-client.jar, i Java-projektets klassökväg.

1. Skapa en signaturklient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `SignatureServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta PDF-dokumentet som innehåller en signatur som ska tas bort

   * Skapa en `java.io.FileInputStream` -objekt som representerar det PDF-dokument som innehåller signaturen som ska tas bort med hjälp av dess konstruktor och genom att skicka ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ta bort den digitala signaturen från signaturfältet

   Ta bort en digital signatur från ett signaturfält genom att anropa `SignatureServiceClient` objektets `clearSignatureField` och skicka följande värden:

   * A `com.adobe.idp.Document` -objekt som representerar det PDF-dokument som innehåller den signatur som ska tas bort.
   * Ett strängvärde som anger namnet på det signaturfält som innehåller den digitala signaturen.

   The `clearSignatureField` returnerar en `com.adobe.idp.Document` det objekt som representerar det PDF-dokument som den digitala signaturen har tagits bort från.

1. Spara PDF-dokumentet som en PDF-fil

   * Skapa en `java.io.File` och se till att filtillägget är .pdf.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` -metod. Skicka `java.io.File` objekt som kopierar innehållet i `com.adobe.idp.Document` till filen. Se till att du använder `Document` objekt som returneras av `clearSignatureField` -metod.

**Se även**

[Tar bort digitala signaturer](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Snabbstart (SOAP): Ta bort en digital signatur med Java API](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ta bort digitala signaturer med webbtjänstens API {#remove-digital-signatures-using-the-web-service-api}

Ta bort en elektronisk underskrift med hjälp av Signature API (webbtjänsten):

1. Inkludera projektfiler

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en signaturklient

   * Skapa en `SignatureServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `SignatureServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/SignatureService?WSDL`). Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `SignatureServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta PDF-dokumentet som innehåller en signatur som ska tas bort

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra ett PDF-dokument som innehåller en digital signatur som ska tas bort.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det signerade PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` med bytearrayens innehåll.

1. Ta bort den digitala signaturen från signaturfältet

   Ta bort den digitala signaturen genom att anropa `SignatureServiceClient` objektets `clearSignatureField` och skicka följande värden:

   * A `BLOB` objekt som innehåller det signerade PDF-dokumentet.
   * Ett strängvärde som representerar namnet på signaturfältet som innehåller den digitala signaturen som ska tas bort.

   The `clearSignatureField` returnerar en `BLOB` det objekt som representerar det PDF-dokument som den digitala signaturen har tagits bort från.

1. Spara PDF-dokumentet som en PDF-fil

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det PDF-dokument som innehåller ett tomt signaturfält och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `BLOB` objekt som returneras av `sign` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till PDF-filen genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Tar bort digitala signaturer](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
