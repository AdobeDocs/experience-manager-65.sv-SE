---
title: Skicka dokument till FormsService
description: Skicka ett com.adobe.idp.Document-objekt som innehåller formulärdesignen till tjänsten Forms. Forms-tjänsten återger formulärdesignen i objektet com.adobe.idp.Document.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 29c7ebda-407a-464b-a9db-054163f5b737
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 0%

---

# Skicka dokument till Forms {#passing-documents-to-the-formsservice}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

AEM Forms-tjänsten återger interaktiv PDF forms till klientenheter, vanligtvis webbläsare, för att samla in information från användare. Ett interaktivt PDF-formulär baseras på en formulärdesign som vanligtvis sparas som en XDP-fil och skapas i Designer. Från och med AEM Forms kan du skicka `com.adobe.idp.Document` objekt som innehåller formulärdesignen för Forms-tjänsten. Forms-tjänsten återger sedan formulärdesignen i `com.adobe.idp.Document` -objekt.

En fördel med att skicka en `com.adobe.idp.Document` objekt för Forms-tjänsten är att andra serviceåtgärder returnerar `com.adobe.idp.Document` -instans. Du kan alltså få en `com.adobe.idp.Document` -instans från en annan tjänståtgärd och återge den. Anta till exempel att en XDP-fil lagras i en Content Services-nod (utgått) med namnet `/Company Home/Form Designs`, vilket visas på följande bild.

Du kan hämta Loan.xdp programmatiskt från Content Services (utgått) (utgått) och skicka XDP-filen till Forms-tjänsten i en `com.adobe.idp.Document` -objekt.

>[!NOTE]
>
>Mer information om tjänsten Forms finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Sammanfattning av steg {#summary-of-steps}

Gör så här om du vill skicka ett dokument som hämtats från innehållstjänster (borttaget) till Forms-tjänsten:

1. Inkludera projektfiler.
1. Skapa ett Forms- och ett API-objekt för dokumenthanteringsklienten.
1. Hämta formulärdesignen från Content Services (utgått).
1. Återge det interaktiva PDF-formuläret.
1. Utför en åtgärd med formulärdataströmmen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

**Skapa ett Forms- och ett API-objekt för dokumenthanteringsklienten**

Skapa ett Forms Client API-objekt innan du programmässigt utför en API-åtgärd för Forms-tjänster. Eftersom det här arbetsflödet hämtar en XDP-fil från Content Services (utgått) skapar du också ett API-objekt för dokumenthantering.

**Hämta formulärdesignen från innehållstjänster (borttagen)**

Hämta XDP-filen från Content Services (utgått) med Java- eller webbtjänstens API. XDP-filen returneras inom en `com.adobe.idp.Document` instans (eller en `BLOB` om du använder webbtjänster). Du kan sedan skicka `com.adobe.idp.Document` till tjänsten Forms.

**Återge ett interaktivt PDF-formulär**

Om du vill återge ett interaktivt formulär skickar du `com.adobe.idp.Document` instans som returnerades från Content Services (utgått) till Forms-tjänsten.

>[!NOTE]
>
>Du kan skicka en `com.adobe.idp.Document` som innehåller formulärdesignen för Forms. Två nya metoder namngivna `renderPDFForm2` och `renderHTMLForm2` acceptera `com.adobe.idp.Document` objekt som innehåller en formulärdesign.

**Utför en åtgärd med formulärdataströmmen**

Beroende på vilken typ av klientprogram du använder kan du skriva formuläret till en webbläsare eller spara formuläret som en PDF-fil. Ett webbaserat program skriver vanligtvis formuläret i webbläsaren. I ett skrivbordsprogram sparas dock formuläret som en PDF-fil.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Skicka dokument till Forms-tjänsten med Java API {#pass-documents-to-the-forms-service-using-the-java-api}

Skicka ett dokument som hämtats från Content Services (utgått) med hjälp av Forms tjänst och Content Services (utgått) API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar och adobe-contentservices-client.jar, i Java-projektets klassökväg.

1. Skapa ett Forms- och ett API-objekt för dokumenthanteringsklienten

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper. (Se [Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Skapa en `FormsServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.
   * Skapa en `DocumentManagementServiceClientImpl` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta formulärdesignen från innehållstjänster (borttagen)

   Anropa `DocumentManagementServiceClientImpl` objektets `retrieveContent` och skicka följande värden:

   * Ett strängvärde som anger den lagringsplats där innehållet läggs till. Standardarkivet är `SpacesStore`. Detta värde är en obligatorisk parameter.
   * Ett strängvärde som anger den fullständiga, kvalificerade sökvägen för innehållet som ska hämtas (till exempel `/Company Home/Form Designs/Loan.xdp`). Detta värde är en obligatorisk parameter.
   * Ett strängvärde som anger versionen. Det här värdet är en valfri parameter och du kan skicka en tom sträng. I det här fallet hämtas den senaste versionen.

   The `retrieveContent` returnerar en `CRCResult` -objekt som innehåller XDP-filen. Hämta en `com.adobe.idp.Document` instans genom att anropa `CRCResult` objektets `getDocument` -metod.

1. Återge ett interaktivt PDF-formulär

   Anropa `FormsServiceClient` objektets `renderPDFForm2` och skicka följande värden:

   * A `com.adobe.idp.Document` objekt som innehåller formulärdesignen som hämtats från Content Services (borttagen).
   * A `com.adobe.idp.Document` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du en tom `com.adobe.idp.Document` -objekt.
   * A `PDFFormRenderSpec` objekt som lagrar körningsalternativ. Det här värdet är en valfri parameter som du kan ange `null` om du inte vill ange körningsalternativ.
   * A `URLSpec` objekt som innehåller URI-värden. Det här värdet är en valfri parameter som du kan ange `null`.
   * A `java.util.HashMap` objekt som lagrar bifogade filer. Det här värdet är en valfri parameter som du kan ange `null` om du inte vill bifoga filer till formuläret.

   The `renderPDFForm` returnerar en `FormsResult` objekt som innehåller en formulärdataström som måste skrivas till klientens webbläsare.

1. Utför en åtgärd med formulärdataströmmen

   * Skapa en `com.adobe.idp.Document` genom att anropa `FormsResult` objekt&quot;s `getOutputContent` -metod.
   * Hämta innehållstypen för `com.adobe.idp.Document` genom att anropa dess `getContentType` -metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metoden och skicka innehållstypen för `com.adobe.idp.Document` -objekt.
   * Skapa en `javax.servlet.ServletOutputStream` som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` -metod.
   * Skapa en `java.io.InputStream` genom att anropa `com.adobe.idp.Document` objektets `getInputStream` -metod.
   * Skapa en bytearray och fylla den med formulärdataströmmen genom att anropa `InputStream` objektets `read` -metod. Skicka bytearrayen som ett argument.
   * Anropa `javax.servlet.ServletOutputStream` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` -metod.

**Se även**

[Snabbstart (SOAP): skicka dokument till Forms-tjänsten med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Skicka dokument till Forms-tjänsten med hjälp av API:t för webbtjänsten {#pass-documents-to-the-forms-service-using-the-web-service-api}

Skicka ett dokument som hämtats från Content Services (utgått) med hjälp av API:t för Forms-tjänsten och innehållstjänster (utgått) (webbtjänsten):

1. Inkludera projektfiler

   Skapa ett Microsoft .NET-projekt som använder MTOM. Eftersom klientprogrammet anropar två AEM Forms-tjänster skapar du två tjänstreferenser. Använd följande WSDL-definition för den tjänstreferens som är kopplad till Forms-tjänsten: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Använd följande WSDL-definition för den tjänstreferens som är kopplad till dokumenthanteringstjänsten: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   På grund av `BLOB` datatypen är gemensam för båda tjänstreferenserna, och kvalificera fullt ut `BLOB` datatyp när du använder den. I motsvarande webbtjänsts snabbstart är alla `BLOB` -instanser är kvalificerade.

   >[!NOTE]
   >
   >Ersätt `localhost`med IP-adressen till den server där AEM Forms finns.

1. Skapa ett Forms- och ett API-objekt för dokumenthanteringsklienten

   * Skapa en `FormsServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `FormsServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/FormsService?WSDL`). Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `FormsServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Upprepa dessa steg för `DocumentManagementServiceClient`tjänstklient.

1. Hämta formulärdesignen från innehållstjänster (borttagen)

   Hämta innehåll genom att anropa `DocumentManagementServiceClient` objektets `retrieveContent` och skicka följande värden:

   * Ett strängvärde som anger den lagringsplats där innehållet läggs till. Standardarkivet är `SpacesStore`. Detta värde är en obligatorisk parameter.
   * Ett strängvärde som anger den fullständiga, kvalificerade sökvägen för innehållet som ska hämtas (till exempel `/Company Home/Form Designs/Loan.xdp`). Detta värde är en obligatorisk parameter.
   * Ett strängvärde som anger versionen. Det här värdet är en valfri parameter och du kan skicka en tom sträng. I det här fallet hämtas den senaste versionen.
   * En strängutdataparameter som lagrar värdet för bläddringslänken.
   * A `BLOB` utdataparameter som lagrar innehållet. Du kan använda den här utdataparametern för att hämta innehållet.
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` utdataparameter som lagrar innehållsattribut.
   * A `CRCResult` output-parameter. Du kan använda kommandot `BLOB` output-parameter för att hämta innehållet.

1. Återge ett interaktivt PDF-formulär

   Anropa `FormsServiceClient` objektets `renderPDFForm2` och skicka följande värden:

   * A `BLOB` objekt som innehåller formulärdesignen som hämtats från Content Services (borttagen).
   * A `BLOB` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du en tom `BLOB` -objekt.
   * A `PDFFormRenderSpec` objekt som lagrar körningsalternativ. Det här värdet är en valfri parameter som du kan ange `null` om du inte vill ange körningsalternativ.
   * A `URLSpec` objekt som innehåller URI-värden. Det här värdet är en valfri parameter som du kan ange `null`.
   * A `Map` objekt som lagrar bifogade filer. Det här värdet är en valfri parameter som du kan ange `null` om du inte vill bifoga filer till formuläret.
   * En lång utdataparameter som används för att lagra sidantalet.
   * En strängutdataparameter som används för att lagra språkvärdet.
   * A `FormsResult` utdataparameter som används för att lagra PDF-formuläret interaktivt `.`

   The `renderPDFForm2` returnerar en `FormsResult` objekt som innehåller det interaktiva PDF-formuläret.

1. Utför en åtgärd med formulärdataströmmen

   * Skapa en `BLOB` objekt som innehåller formulärdata genom att hämta värdet för `FormsResult` objektets `outputContent` fält.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för det interaktiva PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `BLOB` objektet har hämtats från `FormsResult` -objekt. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
