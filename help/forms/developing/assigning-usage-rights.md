---
title: Tilldela användningsrättigheter
description: Använd Acrobat Reader DC-tilläggens Java Client API och Web Service API för att lägga till och ta bort användningsrättigheter från PDF-dokument.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 6af148eb-427a-4b54-9c5f-8750736882d8
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '3897'
ht-degree: 0%

---

# Tilldela användningsrättigheter {#assigning-usage-rights}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

## Om Acrobat Reader DC-tilläggstjänsten {#about-the-acrobat-reader-dc-extensions-service}

Med Acrobat Reader DC Extensions kan man enkelt utbyta interaktiva PDF-dokument genom att utöka funktionaliteten i Adobe Reader. Acrobat Reader DC-tilläggstjänsten stöder alla PDF-dokument, till och med PDF 1.7. Det fungerar med Adobe Reader 7.0 och senare. Tjänsten lägger till användarrättigheter i ett PDF-dokument och aktiverar funktioner som vanligtvis inte är tillgängliga när ett PDF-dokument öppnas med Adobe Reader. Tredjepartsanvändare behöver inte några extra program eller plugin-program för att kunna arbeta med upphovsrättsaktiverade dokument.

Du kan utföra följande uppgifter med hjälp av Acrobat Reader DC-tilläggstjänsten:

* Använd användarrättigheter för PDF-dokument. Mer information finns i [Använda användningsbehörighet för PDF-dokument](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* Ta bort användningsrättigheter från PDF-dokument. Mer information finns i [Ta bort användningsrättigheter från PDF-dokument](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* Hämta information om autentiseringsuppgifter. Mer information finns i [Hämtar information om autentiseringsuppgifter](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Mer information om tjänsten Acrobat Reader DC Extensions finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Använda användningsbehörighet för PDF-dokument {#applying-usage-rights-to-pdf-documents}

Du kan lägga till användarrättigheter i PDF-dokument med Acrobat Reader DC-tilläggens Java Client API och webbtjänst. Användningsrättigheterna gäller funktioner som är tillgängliga som standard i Acrobat men inte i Adobe Reader, t.ex. möjligheten att lägga till kommentarer i ett formulär eller att fylla i formulärfält och spara formuläret. PDF-dokument som har användarrättigheter är aktiverade. En användare som öppnar ett rättighetsaktiverat dokument i Adobe Reader kan utföra åtgärder som är aktiverade för det specifika dokumentet.

>[!NOTE]
>
>När användarrättigheter tillämpas på PDF-dokument med `applyUsageRights` -metoden, som är en del av Java API:t, kan du ange `isModeFinal` parametern för `ReaderExtensionsOptionSpec` objekt till `false`. Detta resulterar i att de bearbetade formulärräknarna inte uppdateras och att prestandan förbättras. Om du inte är orolig för att uppdatera räknaren för bearbetade formulär bör du ställa in `isModeFinal` parameter till `false`.

>[!NOTE]
>
>Mer information om tjänsten Acrobat Reader DC Extensions finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Gör så här om du vill lägga till användarrättigheter i ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.
1. Hämta ett PDF-dokument.
1. Ange användningsrättigheter att använda.
1. Använd användningsbehörighet för PDF-dokumentet.
1. Spara det rättighetsaktiverade PDF-dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett klientobjekt för Acrobat Reader DC-tillägg**

Om du vill utföra en programstyrd Acrobat Reader DC extensions service-åtgärd måste du skapa ett klientobjekt för Acrobat Reader DC extensions-tjänsten. Om du använder Java API för Acrobat Reader DC-tillägg skapar du en `ReaderExtensionsServiceClient` -objekt. Om du använder webbtjänstens API för Acrobat Reader DC-tillägg skapar du en `ReaderExtensionsServiceService` -objekt.

**Hämta ett PDF-dokument**

Hämta ett PDF-dokument om du vill använda användningsrättigheter. PDF-dokument med aktiverade rättigheter innehåller en ordlista med användningsrättigheter. När Adobe Reader öppnar ett dokument som innehåller en sådan ordlista aktiveras de användningsrättigheter som anges i ordlistan endast för det dokumentet. Om dokumentet inte innehåller någon användarrättighetsordlista skapar Acrobat Reader DC-tjänsten en sådan. Om den redan innehåller en ordlista skriver Acrobat Reader DC-tilläggstjänsten över befintliga användningsrättigheter med de som du anger. Ordlistan anger vilka användarrättigheter som är aktiverade. När en användare öppnar dokumentet i Adobe Reader tillåts bara de användningsrättigheter som anges i ordlistan.

**Ange användningsbehörighet att använda**

Vilka användarrättigheter du kan ange avgörs av en inloggningsinformation som du köper från Adobe Systems Incorporated. Autentiseringsuppgifterna ger vanligtvis behörighet att ange en grupp användarrättigheter, t.ex. de som gäller interaktiva formulär. Varje inloggningsinformation ger rätt att skapa ett visst antal rättighetsaktiverade PDF-dokument. Med en utvärderingsautentisering får man rätt att skapa ett obegränsat antal utkast till dokument.

>[!NOTE]
>
>Om du försöker tilldela en användningsbehörighet som inte tillåts av dina autentiseringsuppgifter, kommer du att orsaka ett undantag.

**Använd användningsbehörighet för PDF-dokumentet**

Om du vill tillämpa användarrättigheter på ett PDF-dokument refererar du till aliaset för de autentiseringsuppgifter som du använder för att tillämpa användarrättigheter (en autentiseringsuppgift installeras vanligtvis under installationen av AEM Forms). Du måste också ange det PDF-dokument som användarrättigheterna gäller för. Mer information om hur du konfigurerar en autentiseringsuppgift finns i installations- och distributionsguiden för programservern.

**Spara det rättighetsaktiverade PDF-dokumentet**

När Acrobat Reader DC Extensions-tjänsten har tillämpat användarrättigheter på ett PDF-dokument kan du spara det rättighetsaktiverade PDF-dokumentet som en PDF-fil.

**Se även**

[Använd användningsrättigheter med Java API](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Använd användningsrättigheter med webbtjänstens API](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för Acrobat Reader DC Extensions Service](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Använd användningsrättigheter med Java API {#apply-usage-rights-using-the-java-api}

Använd användarrättigheter för ett PDF-dokument med hjälp av Acrobat Reader DC Extensions API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, som adobe-reader-extensions-client.jar, i Java-projektets klassökväg.

1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `ReaderExtensionsServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta ett PDF-dokument.

   * Skapa en `java.io.FileInputStream` objekt som representerar PDF-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ange användningsrättigheter att använda.

   * Skapa en `UsageRights` objekt som representerar användarrättigheter med hjälp av konstruktorn.
   * Anropa en motsvarande metod som tillhör `UsageRights` -objekt. Om du till exempel vill lägga till `enableFormFillIn` användningsbehörighet, anropa `UsageRights` objektets `enableFormFillIn` metod och skicka `true`. (Upprepa det här steget för varje användningsbehörighet).

1. Använd användningsbehörighet för PDF-dokumentet.

   * Skapa en `ReaderExtensionsOptionSpec` genom att använda dess konstruktor. Det här objektet innehåller körningsalternativ som krävs av Acrobat Reader DC-tilläggstjänsten. När du anropar den här konstruktorn måste du ange följande värden:

      * The `UsageRights` objekt som innehåller användningsrättigheterna som ska tillämpas på dokumentet.
      * Ett strängvärde som anger ett meddelande som en användare ser när det rättighetsaktiverade PDF-dokumentet öppnas i Adobe Reader 7.x. Meddelandet visas inte i Adobe Reader 8.0.

   * Använd användningsbehörighet för PDF-dokumentet genom att anropa `ReaderExtensionsServiceClient` objektets `applyUsageRights` och skicka följande värden:

      * The `com.adobe.idp.Document` -objekt som innehåller det PDF-dokument som användningsrättigheterna tillämpas på.
      * Ett strängvärde som anger det alias för autentiseringsuppgiften som gör att du kan tillämpa användningsbehörighet.
      * Ett strängvärde som anger motsvarande lösenordsvärde. (Den här parametern ignoreras för närvarande. Du kan skicka `null`.)

   * The `ReaderExtensionsOptionSpec` objekt som innehåller körningsalternativ.

   The `applyUsageRights` returnerar en `com.adobe.idp.Document` -objekt som innehåller det rättighetsaktiverade PDF-dokumentet.

1. Spara det rättighetsaktiverade PDF-dokumentet.

   * Skapa en `java.io.File` och se till att filtillägget är .pdf.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att kopiera innehållet i `com.adobe.idp.Document` till filen (se till att du använder `com.adobe.idp.Document` objekt som returneras av `applyUsageRights` metod).

**Se även**

[Använda användningsbehörighet för PDF-dokument](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Snabbstart (SOAP-läge):Tillämpa användningsrättigheter med Java API](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Använd användningsrättigheter med webbtjänstens API {#apply-usage-rights-using-the-web-service-api}

Använd användarrättigheter för ett PDF-dokument med hjälp av Acrobat Reader DC Extensions API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.

   * Skapa en `ReaderExtensionsServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `ReaderExtensionsServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Se till att du anger `?blob=mtom`.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `ReaderExtensionsServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta ett PDF-dokument.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra ett PDF-dokument som har användarbehörighet.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` med bytearrayens innehåll.

1. Ange användningsrättigheter att använda.

   * Skapa en `UsageRights` objekt som representerar användarrättigheter med hjälp av konstruktorn.
   * Tilldela värdet för varje användningsbehörighet `true` till motsvarande datamedlem som tillhör `UsageRights` -objekt. Om du till exempel vill lägga till `enableFormFillIn` användarbehörighet, tilldela `true` till `UsageRights` objektets `enableFormFillIn` datamedlem. (Upprepa det här steget för varje användningsbehörighet).

1. Använd användningsbehörighet för PDF-dokumentet.

   * Skapa en `ReaderExtensionsOptionSpec` genom att använda dess konstruktor. Det här objektet innehåller körningsalternativ som krävs av Acrobat Reader DC-tilläggstjänsten.
   * Tilldela `UsageRights` objekt till `ReaderExtensionsOptionSpec` objektets `usageRights` datamedlem.
   * Tilldela ett strängvärde som anger det meddelande som en användare ser när det rättighetsaktiverade PDF-dokumentet öppnas i Adobe Reader till `ReaderExtensionsOptionSpec` objektets `message` datamedlem.
   * Använd användningsbehörighet för PDF-dokumentet genom att anropa `ReaderExtensionsServiceClient` objektets `applyUsageRights` och skicka följande värden:

      * The `BLOB` -objekt som innehåller det PDF-dokument som användningsrättigheterna tillämpas på.
      * Ett strängvärde som anger det alias för autentiseringsuppgiften som gör att du kan tillämpa användningsbehörighet.
      * Ett strängvärde som anger motsvarande lösenordsvärde. (Den här parametern ignoreras för närvarande. Du kan skicka `null`.)

   * The `ReaderExtensionsOptionSpec` objekt som innehåller körningsalternativ.

   The `applyUsageRights` returnerar en `BLOB` -objekt som innehåller det rättighetsaktiverade PDF-dokumentet.

1. Spara det rättighetsaktiverade PDF-dokumentet.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för det rättighetsaktiverade PDF-dokumentet.
   * Skapa en bytearray som lagrar datainnehållet i `BLOB` objekt som returneras av `applyUsageRights` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Använda användningsbehörighet för PDF-dokument](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Ta bort användningsrättigheter från PDF-dokument {#removing-usage-rights-from-pdf-documents}

Du kan ta bort användarrättigheter från ett rättighetsaktiverat dokument. Det är också nödvändigt att ta bort användarrättigheter från ett PDF-dokument med aktiverade rättigheter för att kunna utföra andra AEM Forms-åtgärder på det. Du måste till exempel signera (eller certifiera) ett PDF-dokument digitalt innan du anger användningsbehörighet. Om du vill utföra åtgärder på ett rättighetsaktiverat dokument måste du därför ta bort användningsbehörighet från dokumentet i PDF, utföra andra åtgärder, t.ex. signera dokumentet digitalt och sedan återanvända användningsbehörighet för dokumentet.

>[!NOTE]
>
>Mer information om tjänsten Acrobat Reader DC Extensions finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-1}

Så här tar du bort användarrättigheter från ett PDF-dokument som har aktiverats för rättigheter:

1. Inkludera projektfiler.
1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.
1. Hämta ett rättighetsaktiverat PDF-dokument.
1. Ta bort användningsrättigheter från PDF-dokumentet.
1. Spara dokumentet PDF.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett klientobjekt för Acrobat Reader DC-tillägg**

Innan du programmässigt kan utföra en Acrobat Reader DC-tilläggstjänståtgärd måste du skapa ett klientobjekt för Acrobat Reader DC-tilläggstjänsten. Om du använder Java API skapar du en `ReaderExtensionsServiceClient` -objekt. Om du använder webbtjänstens API för Acrobat Reader DC-tillägg skapar du en `ReaderExtensionsServiceService` -objekt.

**Hämta ett rättighetsaktiverat PDF-dokument**

Hämta ett rättighetsaktiverat PDF-dokument för att ta bort användningsrättigheter.

**Ta bort användningsrättigheter från PDF-dokumentet**

När du har hämtat ett rättighetsaktiverat PDF-dokument kan du ta bort användningsrättigheterna. När du har tagit bort användningsrättigheterna har PDF-dokumentet inga ytterligare funktioner när det visas i Adobe Reader.

**Spara PDF-dokumentet**

Du kan spara det PDF-dokument som inte längre innehåller användningsrättigheter som en PDF-fil. När dokumentet har sparats som en PDF-fil kan det visas i Adobe Reader eller Acrobat.

**Se även**

[Ta bort användningsrättigheter med Java API](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Ta bort användningsrättigheter med webbtjänstens API](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för Acrobat Reader DC Extensions Service](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Använda användningsbehörighet för PDF-dokument](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Ta bort användningsrättigheter med Java API {#remove-usage-rights-using-the-java-api}

Ta bort användarrättigheter från ett rättighetsaktiverat PDF-dokument med hjälp av Acrobat Reader DC Extensions API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-reader-extensions-client.jar, i Java-projektets klassökväg.

1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.

   Skapa en `ReaderExtensionsServiceClient` genom att använda konstruktorn och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Hämta ett PDF-dokument.

   * Skapa en `java.io.FileInputStream` objekt som representerar det rättighetsaktiverade PDF-dokumentet genom att använda konstruktorn och skicka ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ta bort användningsrättigheter från PDF-dokumentet.

   Ta bort användningsrättigheter från PDF genom att anropa `ReaderExtensionsServiceClient` objektets `removeUsageRights` metoden och skicka `com.adobe.idp.Document` -objekt som innehåller det rättighetsaktiverade PDF-dokumentet. Den här metoden returnerar en `com.adobe.idp.Document` objekt som innehåller ett PDF-dokument som inte har användningsbehörighet.

1. Använd användningsbehörighet för PDF-dokumentet.

   * Skapa en `java.io.File` och se till att filtillägget är .PDF.
   * Anropa `Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` till filen (se till att du använder `Document` objekt som returneras av `removeUsageRights` metod).

**Se även**

[Ta bort användningsrättigheter från PDF-dokument](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Snabbstart (SOAP-läge): Ta bort användningsrättigheter från ett PDF-dokument med Java API](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ta bort användningsrättigheter med webbtjänstens API {#remove-usage-rights-using-the-web-service-api}

Ta bort användningsrättigheter från ett rättighetsaktiverat PDF-dokument med Acrobat Reader DC Extensions API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.

   * Skapa en `ReaderExtensionsServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `ReaderExtensionsServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Se till att du anger `?blob=mtom`.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `ReaderExtensionsServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta ett PDF-dokument.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` används för att lagra det rättighetsaktiverade PDF-dokumentet från vilket användarrättigheter tas bort.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` med bytearrayens innehåll.

1. Ta bort användningsrättigheter från PDF-dokumentet.

   Ta bort användningsrättigheter från PDF genom att anropa `ReaderExtensionsServiceClient` objektets `removeUsageRights` metoden och skicka `BLOB` -objekt som innehåller det rättighetsaktiverade PDF-dokumentet. Den här metoden returnerar en `BLOB` objekt som innehåller ett PDF-dokument som inte har användningsbehörighet.

1. Använd användningsbehörighet för PDF-dokumentet.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen PDF.
   * Skapa en bytearray som lagrar datainnehållet i `BLOB` objekt som returneras av `removeUsageRights` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.

**Se även**

[Ta bort användningsrättigheter från PDF-dokument](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Hämtar information om autentiseringsuppgifter {#retrieving-credential-information}

Du kan hämta information om de autentiseringsuppgifter som användes för att tillämpa användarrättigheter på ett PDF-dokument med aktiverade rättigheter. Genom att hämta information om en autentiseringsuppgift, kan du få information som det datum efter vilket certifikatet inte längre är giltigt.

>[!NOTE]
>
>Mer information om tjänsten Acrobat Reader DC Extensions finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-2}

Så här hämtar du information om de autentiseringsuppgifter som användes för att tillämpa användarrättigheter på ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.
1. Hämta ett rättighetsaktiverat PDF-dokument.
1. Hämta information om autentiseringsuppgifterna.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett klientobjekt för Acrobat Reader DC-tillägg**

Innan du programmässigt kan utföra en Acrobat Reader DC-tilläggstjänståtgärd måste du skapa ett klientobjekt för Acrobat Reader DC-tilläggstjänsten. Om du använder Java API skapar du en `ReaderExtensionsServiceClient` -objekt. Om du använder webbtjänstens API för Acrobat Reader DC-tillägg skapar du en `ReaderExtensionsServiceService` -objekt.

**Hämta ett rättighetsaktiverat PDF-dokument**

Hämta ett rättighetsaktiverat PDF-dokument om du vill hämta information om autentiseringsuppgifterna. Du kan även hämta information om en autentiseringsuppgift genom att ange dess alias. Om du vill hämta information om en autentiseringsuppgift som användes för att tillämpa användarrättigheter på ett visst rättighetsaktiverat PDF-dokument måste du dock hämta dokumentet.

**Hämta information om autentiseringsuppgifterna**

När du har hämtat ett rättighetsaktiverat PDF-dokument kan du få information om de autentiseringsuppgifter som användes för att tillämpa användarrättigheter på det. Du kan få följande information om autentiseringsuppgifterna:

* Det meddelande som visas i Adobe Reader när dokumentet för aktiverade rättigheter öppnas i PDF.
* Det datum efter vilket autentiseringsuppgifterna inte längre är giltiga.
* Det datum före vilket autentiseringsuppgifterna inte är giltiga.
* De användningsrättigheter som har angetts för det här rättighetsaktiverade PDF-dokumentet.
* Antalet gånger som autentiseringsuppgifterna har använts.

**Se även**

[Ta bort användningsrättigheter med Java API](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Ta bort användningsrättigheter med webbtjänstens API](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för Acrobat Reader DC Extensions Service](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Hämta inloggningsinformation med Java API {#retrieve-credential-information-using-the-java-api}

Hämta autentiseringsuppgifter med Acrobat Reader DC Extensions API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-reader-extensions-client.jar, i Java-projektets klassökväg.

1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.

   Skapa en `ReaderExtensionsServiceClient` genom att använda konstruktorn och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Hämta ett PDF-dokument.

   * Skapa en `java.io.FileInputStream` objekt som representerar det rättighetsaktiverade PDF-dokumentet genom att använda konstruktorn och skicka ett strängvärde som anger platsen för det rättighetsaktiverade PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ta bort användningsrättigheter från PDF-dokumentet.

   * Hämta information om de autentiseringsuppgifter som används för att tillämpa användningsrättigheter på PDF-dokumentet genom att anropa `ReaderExtensionsServiceClient` objektets `getDocumentUsageRights` metoden och skicka `com.adobe.idp.Document` -objekt som innehåller det rättighetsaktiverade PDF-dokumentet. Den här metoden returnerar en `GetUsageRightsResult` objekt som innehåller autentiseringsuppgifter.
   * Hämta det datum efter vilket autentiseringsuppgifterna inte längre är giltiga genom att anropa `GetUsageRightsResult` objektets `getNotAfter` -metod. Den här metoden returnerar en `java.util.Date` objekt som representerar det datum efter vilket autentiseringsuppgifterna inte längre är giltiga.
   * Hämta meddelandet som visas i Adobe Reader när dokumentet för aktiverade rättigheter öppnas via PDF genom att anropa `GetUsageRightsResult` objektets `getMessage` -metod. Den här metoden returnerar ett strängvärde som representerar meddelandet.

**Se även**

[Hämtar information om autentiseringsuppgifter](assigning-usage-rights.md#retrieving-credential-information)

[Snabbstart (SOAP-läge): Hämta inloggningsinformation med Java API](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Hämta autentiseringsuppgifter med webbtjänstens API {#retrieve-credential-information-using-the-web-service-api}

Hämta autentiseringsinformation med Acrobat Reader DC Extensions API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett klientobjekt för Acrobat Reader DC-tillägg.

   * Skapa en `ReaderExtensionsServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `ReaderExtensionsServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Se till att du anger `?blob=mtom`.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `ReaderExtensionsServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta ett PDF-dokument.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra ett PDF-dokument som har aktiverats för behörighet.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det rättighetsaktiverade PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` med bytearrayens innehåll.

1. Ta bort användningsrättigheter från PDF-dokumentet.

   * Hämta information om de autentiseringsuppgifter som används för att tillämpa användningsrättigheter på PDF-dokumentet genom att anropa `ReaderExtensionsServiceClient` objektets `getDocumentUsageRights` metoden och skicka `com.adobe.idp.Document` -objekt som innehåller det rättighetsaktiverade PDF-dokumentet. Den här metoden returnerar en `GetUsageRightsResult` objekt som innehåller autentiseringsuppgifter.
   * Hämta datumet efter vilket autentiseringsuppgifterna inte längre är giltiga genom att hämta värdet för `GetUsageRightsResult` objektets `notAfter` datamedlem. Datatypen för den här datamedlemmen är `System.DateTime`.
   * Hämta meddelandet som visas när det rättighetsaktiverade PDF-dokumentet öppnas i Adobe Reader genom att hämta värdet för `GetUsageRightsResult` objektets `message` datamedlem. Datatypen för den här datamedlemmen är en sträng.
   * Hämta antalet gånger som autentiseringsuppgiften används genom att hämta värdet för `GetUsageRightsResult` objektets `useCount` datamedlem. Datatypen för den här datamedlemmen är ett heltal.

**Se även**

[Hämtar information om autentiseringsuppgifter](assigning-usage-rights.md#retrieving-credential-information)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
