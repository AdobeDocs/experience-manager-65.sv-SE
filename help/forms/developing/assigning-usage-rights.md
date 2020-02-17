---
title: Tilldela användningsrättigheter
seo-title: Tilldela användningsrättigheter
description: 'null'
seo-description: 'null'
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Tilldela användningsrättigheter {#assigning-usage-rights}

## Om Acrobat Reader DC-tilläggstjänsten {#about-the-acrobat-reader-dc-extensions-service}

Med Acrobat Reader DC-tilläggstjänsten kan din organisation enkelt dela interaktiva PDF-dokument genom att utöka funktionaliteten i Adobe Reader. Tilläggstjänsten Acrobat Reader DC har fullt stöd för alla PDF-dokument, till och med PDF 1.7. Det fungerar med Adobe Reader 7.0 och senare. Tjänsten lägger till användarrättigheter i ett PDF-dokument och aktiverar funktioner som inte är tillgängliga när ett PDF-dokument öppnas med Adobe Reader. Tredjepartsanvändare behöver inte några extra program eller plugin-program för att kunna arbeta med upphovsrättsaktiverade dokument.

Du kan utföra följande uppgifter med hjälp av tilläggstjänsten i Acrobat Reader DC:

* Använd användningsbehörighet för PDF-dokument. Mer information finns i [Använda användningsrättigheter i PDF-dokument](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* Ta bort användningsrättigheter från PDF-dokument. Mer information finns i [Ta bort användningsrättigheter från PDF-dokument](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* Hämta information om autentiseringsuppgifter. Mer information finns i [Hämta information om autentiseringsuppgifter](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Mer information om Acrobat Reader DC-tilläggstjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

## Tillämpa användningsrättigheter på PDF-dokument {#applying-usage-rights-to-pdf-documents}

Du kan lägga till användningsrättigheter i PDF-dokument med Acrobat Reader DC-tilläggen för Java Client API och webbtjänsten. Användningsrättigheterna gäller funktioner som är tillgängliga som standard i Acrobat men inte i Adobe Reader, t.ex. möjligheten att lägga till kommentarer i ett formulär eller att fylla i formulärfält och spara formuläret. PDF-dokument som har användarrättigheter är aktiverade. En användare som öppnar ett rättighetsaktiverat dokument i Adobe Reader kan utföra åtgärder som är aktiverade för det specifika dokumentet.

>[!NOTE]
>
>När du tillämpar användningsrättigheter på PDF-dokument med hjälp av `applyUsageRights` metoden, som är en del av Java API:t, kan du ange `isModeFinal` parametern för `ReaderExtensionsOptionSpec` objektet till `false`. Detta resulterar i att de bearbetade formulärräknarna inte uppdateras och att prestandan förbättras. Om du inte är orolig för att uppdatera räknaren för bearbetade formulär rekommenderar vi att du anger parametern `isModeFinal` till `false`.

>[!NOTE]
>
>Mer information om Acrobat Reader DC-tilläggstjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Gör så här om du vill lägga till användningsrättigheter i ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.
1. Hämta ett PDF-dokument.
1. Ange användningsrättigheter att använda.
1. Använd användningsbehörighet för PDF-dokumentet.
1. Spara det aktiverade PDF-dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett klientobjekt för Acrobat Reader DC-tillägg**

För att programmässigt kunna utföra en tilläggsåtgärd i Acrobat Reader DC måste du skapa ett klientobjekt för tjänsten Acrobat Reader DC extensions. Om du använder Java API:t för Acrobat Reader DC-tilläggen skapar du ett `ReaderExtensionsServiceClient` objekt. Skapa ett `ReaderExtensionsServiceService` objekt om du använder webbtjänstens API för Acrobat Reader DC-tillägg.

**Hämta ett PDF-dokument**

Du måste hämta ett PDF-dokument för att kunna tillämpa användningsrättigheter. PDF-dokument med aktiverade rättigheter innehåller en ordlista med användningsrättigheter. När Adobe Reader öppnar ett dokument som innehåller en sådan ordlista aktiveras de användningsrättigheter som anges i ordlistan endast för det dokumentet. Om dokumentet inte innehåller någon användarrättighetsordlista skapar Acrobat Reader DC-tilläggstjänsten en sådan. Om den redan innehåller en ordlista skriver Acrobat Reader DC-tilläggstjänsten över befintliga användningsrättigheter med de som du anger. Ordlistan anger vilka användarrättigheter som är aktiverade. När en användare öppnar dokumentet i Adobe Reader tillåts bara de användningsrättigheter som anges i ordlistan.

**Ange användningsbehörighet att använda**

Vilka användarrättigheter du kan ange avgörs av de autentiseringsuppgifter du köper från Adobe Systems Incorporated. Autentiseringsuppgifterna ger vanligtvis behörighet att ange en grupp användarrättigheter, t.ex. de som gäller interaktiva formulär. Varje behörighet ger rätt att skapa ett visst antal rättighetsaktiverade PDF-dokument. Med en utvärderingsautentisering får man skapa ett obegränsat antal utkast till dokument.

>[!NOTE]
>
>Om du försöker tilldela en användningsbehörighet som inte tillåts av dina autentiseringsuppgifter, kommer du att orsaka ett undantag.

**Använd användningsbehörighet för PDF-dokumentet**

Om du vill tillämpa användarbehörighet för ett PDF-dokument refererar du till aliaset för de autentiseringsuppgifter som du använder för att tillämpa användarrättigheter (en autentiseringsuppgift installeras vanligtvis under installationen av AEM Forms). Du måste även ange det PDF-dokument som användningsrättigheterna ska tillämpas på. Mer information om hur du konfigurerar en autentiseringsuppgift finns i installations- och distributionsguiden för programservern.

**Spara det aktiverade PDF-dokumentet**

När Acrobat Reader DC-tilläggstjänsten har tillämpat användarrättigheter på ett PDF-dokument kan du spara det aktiverade PDF-dokumentet som en PDF-fil.

**Se även**

[Använd användningsrättigheter med Java API](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Använd användningsrättigheter med webbtjänstens API](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för tjänsten Acrobat Reader DC Extensions Service API](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Använd användningsrättigheter med Java API {#apply-usage-rights-using-the-java-api}

Tillämpa användningsrättigheter på ett PDF-dokument med Acrobat Reader DC Extensions API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-reader-extensions-client.jar, i Java-projektets klassökväg.

1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa ett `ReaderExtensionsServiceClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.

1. Hämta ett PDF-dokument.

   * Skapa ett `java.io.FileInputStream` objekt som representerar PDF-dokumentet med hjälp av dess konstruktor och skicka ett strängvärde som anger PDF-dokumentets plats.
   * Skapa ett `com.adobe.idp.Document` objekt med hjälp av dess konstruktor och skicka `java.io.FileInputStream` objektet.

1. Ange användningsrättigheter att använda.

   * Skapa ett `UsageRights` objekt som representerar användarrättigheter med hjälp av konstruktorn.
   * För varje användningsbehörighet som ska användas anropar du en motsvarande metod som tillhör `UsageRights` objektet. Om du till exempel vill lägga till `enableFormFillIn` användningsrättigheten anropar du `UsageRights` objektets `enableFormFillIn` metod och skickar `true`. (Upprepa det här steget för varje användningsbehörighet).

1. Använd användningsbehörighet för PDF-dokumentet.

   * Skapa ett `ReaderExtensionsOptionSpec` objekt med hjälp av dess konstruktor. Det här objektet innehåller körningsalternativ som krävs av Acrobat Reader DC-tilläggstjänsten. När du anropar den här konstruktorn måste du ange följande värden:

      * Det objekt `UsageRights` som innehåller användningsrättigheterna som ska tillämpas på dokumentet.
      * Ett strängvärde som anger ett meddelande som användaren ser när det aktiverade PDF-dokumentet öppnas i Adobe Reader 7.x. Det här meddelandet visas inte i Adobe Reader 8.0.
   * Tillämpa användningsbehörighet för PDF-dokumentet genom att anropa `ReaderExtensionsServiceClient` objektets `applyUsageRights` metod och skicka följande värden:

      * Det objekt `com.adobe.idp.Document` som innehåller PDF-dokumentet som användningsrättigheterna tillämpas på.
      * Ett strängvärde som anger det alias för autentiseringsuppgiften som gör att du kan tillämpa användningsbehörighet.
      * Ett strängvärde som anger motsvarande lösenordsvärde. (Den här parametern ignoreras för närvarande. Du kan gå `null`.)
   * Det objekt `ReaderExtensionsOptionSpec` som innehåller körningsalternativ.
   Metoden returnerar `applyUsageRights` ett `com.adobe.idp.Document` objekt som innehåller det aktiverade PDF-dokumentet.

1. Spara det aktiverade PDF-dokumentet.

   * Skapa ett `java.io.File` objekt och kontrollera att filtillägget är .pdf.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att kopiera innehållet i `com.adobe.idp.Document` objektet till filen (se till att du använder det `com.adobe.idp.Document` objekt som returnerades av `applyUsageRights` metoden).

**Se även**

[Tillämpa användningsrättigheter på PDF-dokument](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Snabbstart (SOAP-läge):Tillämpa användningsrättigheter med Java API](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Använd användningsrättigheter med webbtjänstens API {#apply-usage-rights-using-the-web-service-api}

Tillämpa användningsrättigheter på ett PDF-dokument med Acrobat Reader DC Extensions API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen för servern som är värd för AEM Forms.

1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.

   * Skapa ett `ReaderExtensionsServiceClient` objekt med hjälp av dess standardkonstruktor.
   * Skapa ett `ReaderExtensionsServiceClient.Endpoint.Address` objekt med hjälp av `System.ServiceModel.EndpointAddress` konstruktorn. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Se till att du anger `?blob=mtom`.)
   * Skapa ett `System.ServiceModel.BasicHttpBinding` objekt genom att hämta värdet för `ReaderExtensionsServiceClient.Endpoint.Binding` fältet. Sänd returvärdet till `BasicHttpBinding`.
   * Ställ in `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela användarnamnet för AEM-formulär till fältet `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta ett PDF-dokument.

   * Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Objektet används `BLOB` för att lagra ett PDF-dokument som har användningsbehörighet.
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll objektet `BLOB` genom att tilldela dess `MTOM` egenskap med innehållet i bytearrayen.

1. Ange användningsrättigheter att använda.

   * Skapa ett `UsageRights` objekt som representerar användarrättigheter med hjälp av konstruktorn.
   * För varje användningsbehörighet som ska användas tilldelar du värdet `true` till motsvarande datamedlem som tillhör `UsageRights` objektet. Om du till exempel vill lägga till `enableFormFillIn` användningsrättigheten tilldelar du `true` objektets `UsageRights` `enableFormFillIn` datamedlem. (Upprepa det här steget för varje användningsbehörighet).

1. Använd användningsbehörighet för PDF-dokumentet.

   * Skapa ett `ReaderExtensionsOptionSpec` objekt med hjälp av dess konstruktor. Det här objektet innehåller körningsalternativ som krävs av Acrobat Reader DC-tilläggstjänsten.
   * Tilldela `UsageRights` objektet till `ReaderExtensionsOptionSpec` objektets `usageRights` datamedlem.
   * Tilldela ett strängvärde som anger det meddelande som användaren ser när det rättighetsaktiverade PDF-dokumentet öppnas i Adobe Reader till `ReaderExtensionsOptionSpec` objektets `message` datamedlem.
   * Tillämpa användningsbehörighet för PDF-dokumentet genom att anropa `ReaderExtensionsServiceClient` objektets `applyUsageRights` metod och skicka följande värden:

      * Det objekt `BLOB` som innehåller PDF-dokumentet som användningsrättigheterna tillämpas på.
      * Ett strängvärde som anger det alias för autentiseringsuppgiften som gör att du kan tillämpa användningsbehörighet.
      * Ett strängvärde som anger motsvarande lösenordsvärde. (Den här parametern ignoreras för närvarande. Du kan gå `null`.)
   * Det objekt `ReaderExtensionsOptionSpec` som innehåller körningsalternativ.
   Metoden returnerar `applyUsageRights` ett `BLOB` objekt som innehåller det aktiverade PDF-dokumentet.

1. Spara det aktiverade PDF-dokumentet.

   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för det rättighetsaktiverade PDF-dokumentet.
   * Skapa en bytearray som lagrar datainnehållet i det `BLOB` objekt som returnerades av `applyUsageRights` metoden. Fyll i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa ett `System.IO.BinaryWriter` objekt genom att anropa dess konstruktor och skicka `System.IO.FileStream` objektet.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` metod och skicka bytearrayen.

**Se även**

[Tillämpa användningsrättigheter på PDF-dokument](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Anropa AEM-formulär med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM-formulär med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Ta bort användningsrättigheter från PDF-dokument {#removing-usage-rights-from-pdf-documents}

Du kan ta bort användarrättigheter från ett rättighetsaktiverat dokument. Det är också nödvändigt att ta bort användarrättigheter från ett rättighetsaktiverat PDF-dokument för att kunna utföra andra AEM Forms-åtgärder på det. Du måste till exempel signera (eller certifiera) ett PDF-dokument digitalt innan du anger användningsbehörighet. Om du vill utföra åtgärder på ett rättighetsaktiverat dokument måste du därför ta bort användningsbehörighet från PDF-dokumentet, utföra andra åtgärder, som att signera dokumentet digitalt och sedan återanvända användningsbehörighet för dokumentet.

>[!NOTE]
>
>Mer information om Acrobat Reader DC-tilläggstjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-1}

Så här tar du bort användningsrättigheter från ett rättighetsaktiverat PDF-dokument:

1. Inkludera projektfiler.
1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.
1. Hämta ett rättighetsaktiverat PDF-dokument.
1. Ta bort användningsrättigheter från PDF-dokumentet.
1. Spara PDF-dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett klientobjekt för Acrobat Reader DC-tillägg**

Innan du programmässigt kan utföra en tilläggsåtgärd i Acrobat Reader DC måste du skapa ett klientobjekt för Acrobat Reader DC-tilläggsprogrammet. Om du använder Java API skapar du ett `ReaderExtensionsServiceClient` objekt. Skapa ett `ReaderExtensionsServiceService` objekt om du använder webbtjänstens API för Acrobat Reader DC-tillägg.

**Hämta ett rättighetsaktiverat PDF-dokument**

Hämta ett rättighetsaktiverat PDF-dokument för att ta bort användningsrättigheter.

**Ta bort användningsrättigheter från PDF-dokumentet**

När du har hämtat ett rättighetsaktiverat PDF-dokument kan du ta bort användningsbehörighet. När du har tagit bort användningsrättigheterna har PDF-dokumentet inga ytterligare funktioner när det visas i Adobe Reader.

**Spara PDF-dokumentet**

Du kan spara PDF-dokumentet som inte längre innehåller användningsrättigheter som en PDF-fil. När PDF-dokumentet har sparats som en PDF-fil kan det visas i Adobe Reader eller Acrobat.

**Se även**

[Ta bort användningsrättigheter med Java API](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Ta bort användningsrättigheter med webbtjänstens API](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för tjänsten Acrobat Reader DC Extensions Service API](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Tillämpa användningsrättigheter på PDF-dokument](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Ta bort användningsrättigheter med Java API {#remove-usage-rights-using-the-java-api}

Ta bort användningsrättigheter från ett rättighetsaktiverat PDF-dokument med Acrobat Reader DC Extensions API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-reader-extensions-client.jar, i Java-projektets klassökväg.

1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.

   Skapa ett `ReaderExtensionsServiceClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Hämta ett PDF-dokument.

   * Skapa ett `java.io.FileInputStream` objekt som representerar det rättighetsaktiverade PDF-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger PDF-dokumentets plats.
   * Skapa ett `com.adobe.idp.Document` objekt med hjälp av dess konstruktor och skicka `java.io.FileInputStream` objektet.

1. Ta bort användningsrättigheter från PDF-dokumentet.

   Ta bort användningsrättigheter från PDF-dokumentet genom att anropa `ReaderExtensionsServiceClient` objektets `removeUsageRights` metod och skicka det `com.adobe.idp.Document` objekt som innehåller det aktiverade PDF-dokumentet. Den här metoden returnerar ett `com.adobe.idp.Document` objekt som innehåller ett PDF-dokument som inte har användningsbehörighet.

1. Använd användningsbehörighet för PDF-dokumentet.

   * Skapa ett `java.io.File` objekt och kontrollera att filtillägget är .PDF.
   * Anropa `Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` objektet till filen (se till att du använder det `Document` objekt som returnerades av `removeUsageRights` metoden).

**Se även**

[Ta bort användningsrättigheter från PDF-dokument](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Snabbstart (SOAP-läge): Ta bort användningsrättigheter från ett PDF-dokument med Java API](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ta bort användningsrättigheter med webbtjänstens API {#remove-usage-rights-using-the-web-service-api}

Ta bort användningsrättigheter från ett rättighetsaktiverat PDF-dokument med hjälp av Acrobat Reader DC-tilläggs-API:t (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen för servern som är värd för AEM Forms.

1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.

   * Skapa ett `ReaderExtensionsServiceClient` objekt med hjälp av dess standardkonstruktor.
   * Skapa ett `ReaderExtensionsServiceClient.Endpoint.Address` objekt med hjälp av `System.ServiceModel.EndpointAddress` konstruktorn. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Se till att du anger `?blob=mtom`.)
   * Skapa ett `System.ServiceModel.BasicHttpBinding` objekt genom att hämta värdet för `ReaderExtensionsServiceClient.Endpoint.Binding` fältet. Sänd returvärdet till `BasicHttpBinding`.
   * Ställ in `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela användarnamnet för AEM-formulär till fältet `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta ett PDF-dokument.

   * Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Objektet används `BLOB` för att lagra det rättighetsaktiverade PDF-dokumentet från vilket användningsrättigheterna tas bort.
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod och skicka bytearrayen, startpositionen och den strömlängd som ska läsas.
   * Fyll objektet `BLOB` genom att tilldela dess `MTOM` egenskap med innehållet i bytearrayen.

1. Ta bort användningsrättigheter från PDF-dokumentet.

   Ta bort användningsrättigheter från PDF-dokumentet genom att anropa `ReaderExtensionsServiceClient` objektets `removeUsageRights` metod och skicka det `BLOB` objekt som innehåller det aktiverade PDF-dokumentet. Den här metoden returnerar ett `BLOB` objekt som innehåller ett PDF-dokument som inte har användningsbehörighet.

1. Använd användningsbehörighet för PDF-dokumentet.

   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar PDF-filens plats.
   * Skapa en bytearray som lagrar datainnehållet i det `BLOB` objekt som returnerades av `removeUsageRights` metoden. Fyll i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa ett `System.IO.BinaryWriter` objekt genom att anropa dess konstruktor och skicka `System.IO.FileStream` objektet.

**Se även**

[Ta bort användningsrättigheter från PDF-dokument](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Anropa AEM-formulär med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM-formulär med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Hämtar information om autentiseringsuppgifter {#retrieving-credential-information}

Du kan hämta information om de autentiseringsuppgifter som användes för att tillämpa användarrättigheter på ett rättighetsaktiverat PDF-dokument. Genom att hämta information om en autentiseringsuppgift, kan du få information som det datum efter vilket certifikatet inte längre är giltigt.

>[!NOTE]
>
>Mer information om Acrobat Reader DC-tilläggstjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-2}

Så här hämtar du information om de autentiseringsuppgifter som användes för att tillämpa användningsrättigheter på ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.
1. Hämta ett rättighetsaktiverat PDF-dokument.
1. Hämta information om autentiseringsuppgifterna.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett klientobjekt för Acrobat Reader DC-tillägg**

Innan du programmässigt kan utföra en tilläggsåtgärd i Acrobat Reader DC måste du skapa ett klientobjekt för Acrobat Reader DC-tilläggsprogrammet. Om du använder Java API skapar du ett `ReaderExtensionsServiceClient` objekt. Skapa ett `ReaderExtensionsServiceService` objekt om du använder webbtjänstens API för Acrobat Reader DC-tillägg.

**Hämta ett rättighetsaktiverat PDF-dokument**

Du måste hämta ett rättighetsaktiverat PDF-dokument för att kunna hämta information om autentiseringsuppgifterna. Du kan även hämta information om en autentiseringsuppgift genom att ange dess alias; Om du vill hämta information om en autentiseringsuppgift som användes för att tillämpa användarrättigheter på ett visst rättighetsaktiverat PDF-dokument måste du hämta dokumentet.

**Hämta information om autentiseringsuppgifterna**

När du har hämtat ett rättighetsaktiverat PDF-dokument kan du få information om de autentiseringsuppgifter som användes för att tillämpa användningsrättigheterna på det. Du kan få följande information om autentiseringsuppgifterna:

* Meddelandet som visas i Adobe Reader när det aktiverade PDF-dokumentet öppnas.
* Det datum efter vilket autentiseringsuppgifterna inte längre är giltiga.
* Det datum före vilket autentiseringsuppgifterna inte är giltiga.
* De användningsrättigheter som har angetts för det här rättighetsaktiverade PDF-dokumentet.
* Antalet gånger som autentiseringsuppgifterna har använts.

**Se även**

[Ta bort användningsrättigheter med Java API](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Ta bort användningsrättigheter med webbtjänstens API](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för tjänsten Acrobat Reader DC Extensions Service API](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Hämta autentiseringsuppgifter med Java API {#retrieve-credential-information-using-the-java-api}

Hämta inloggningsinformation med Acrobat Reader DC Extensions API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-reader-extensions-client.jar, i Java-projektets klassökväg.

1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.

   Skapa ett `ReaderExtensionsServiceClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Hämta ett PDF-dokument.

   * Skapa ett `java.io.FileInputStream` objekt som representerar det rättighetsaktiverade PDF-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för det rättighetsaktiverade PDF-dokumentet.
   * Skapa ett `com.adobe.idp.Document` objekt med hjälp av dess konstruktor och skicka `java.io.FileInputStream` objektet.

1. Ta bort användningsrättigheter från PDF-dokumentet.

   * Hämta information om de autentiseringsuppgifter som används för att tillämpa användningsrättigheter på PDF-dokumentet genom att anropa `ReaderExtensionsServiceClient` objektets `getDocumentUsageRights` metod och skicka det `com.adobe.idp.Document` objekt som innehåller det rättighetsaktiverade PDF-dokumentet. Den här metoden returnerar ett `GetUsageRightsResult` objekt som innehåller autentiseringsuppgifter.
   * Hämta det datum efter vilket autentiseringsuppgifterna inte längre är giltiga genom att anropa `GetUsageRightsResult` objektets `getNotAfter` metod. Den här metoden returnerar ett `java.util.Date` objekt som representerar det datum efter vilket autentiseringsuppgifterna inte längre är giltiga.
   * Hämta meddelandet som visas i Adobe Reader när det aktiverade PDF-dokumentet öppnas genom att anropa `GetUsageRightsResult` objektets `getMessage` metod. Den här metoden returnerar ett strängvärde som representerar meddelandet.

**Se även**

[Hämtar information om autentiseringsuppgifter](assigning-usage-rights.md#retrieving-credential-information)

[Snabbstart (SOAP-läge): Hämta autentiseringsinformation med Java API](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Hämta autentiseringsuppgifter med webbtjänstens API {#retrieve-credential-information-using-the-web-service-api}

Hämta inloggningsinformation med Acrobat Reader DC Extensions API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen för servern som är värd för AEM Forms.

1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.

   * Skapa ett `ReaderExtensionsServiceClient` objekt med hjälp av dess standardkonstruktor.
   * Skapa ett `ReaderExtensionsServiceClient.Endpoint.Address` objekt med hjälp av `System.ServiceModel.EndpointAddress` konstruktorn. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Se till att du anger `?blob=mtom`.)
   * Skapa ett `System.ServiceModel.BasicHttpBinding` objekt genom att hämta värdet för `ReaderExtensionsServiceClient.Endpoint.Binding` fältet. Sänd returvärdet till `BasicHttpBinding`.
   * Ställ in `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela användarnamnet för AEM-formulär till fältet `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta ett PDF-dokument.

   * Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Objektet används `BLOB` för att lagra ett rättighetsaktiverat PDF-dokument.
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det rättighetsaktiverade PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod och skicka bytearrayen, startpositionen och den strömlängd som ska läsas.
   * Fyll objektet `BLOB` genom att tilldela dess `MTOM` egenskap med innehållet i bytearrayen.

1. Ta bort användningsrättigheter från PDF-dokumentet.

   * Hämta information om de autentiseringsuppgifter som används för att tillämpa användningsrättigheter på PDF-dokumentet genom att anropa `ReaderExtensionsServiceClient` objektets `getDocumentUsageRights` metod och skicka det `com.adobe.idp.Document` objekt som innehåller det rättighetsaktiverade PDF-dokumentet. Den här metoden returnerar ett `GetUsageRightsResult` objekt som innehåller autentiseringsuppgifter.
   * Hämta datumet efter vilket autentiseringsuppgiften inte längre är giltig genom att hämta värdet för `GetUsageRightsResult` objektets `notAfter` datamedlem. Datatypen för den här datamedlemmen är `System.DateTime`.
   * Hämta meddelandet som visas när det aktiverade PDF-dokumentet öppnas i Adobe Reader genom att hämta värdet för `GetUsageRightsResult` objektets `message` datamedlem. Datatypen för den här datamedlemmen är en sträng.
   * Hämta antalet gånger som autentiseringsuppgiften används genom att hämta värdet för `GetUsageRightsResult` objektets `useCount` datamedlem. Datatypen för den här datamedlemmen är ett heltal.

**Se även**

[Hämtar information om autentiseringsuppgifter](assigning-usage-rights.md#retrieving-credential-information)

[Anropa AEM-formulär med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM-formulär med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
