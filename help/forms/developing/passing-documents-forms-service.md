---
title: Skicka dokument till FormsService
seo-title: Skicka dokument till FormsService
description: 'null'
seo-description: 'null'
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Skicka dokument till formulärtjänsten {#passing-documents-to-the-formsservice}

AEM Forms-tjänsten återger interaktiva PDF-formulär till klientenheter, vanligtvis webbläsare, för att samla in information från användarna. Ett interaktivt PDF-formulär baseras på en formulärdesign som vanligtvis sparas som en XDP-fil och skapas i Designer. Från och med AEM Forms kan du skicka ett `com.adobe.idp.Document` objekt som innehåller formulärdesignen till Forms-tjänsten. Forms-tjänsten återger sedan formulärdesignen som finns i `com.adobe.idp.Document` objektet.

En fördel med att skicka ett `com.adobe.idp.Document` objekt till Forms-tjänsten är att andra serviceåtgärder returnerar en `com.adobe.idp.Document` instans. Det innebär att du kan hämta en `com.adobe.idp.Document` instans från en annan tjänståtgärd och återge den. Anta till exempel att en XDP-fil lagras i en Content Services-nod (utgått) med namnet `/Company Home/Form Designs`, vilket visas i följande bild.

Du kan hämta Loan.xdp via programkod från Content Services (utgått) och skicka XDP-filen till Forms-tjänsten inom ett `com.adobe.idp.Document` objekt.

>[!NOTE]
>
>Mer information om Forms-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Sammanfattning av steg {#summary-of-steps}

Utför följande uppgifter om du vill skicka ett dokument som hämtats från innehållstjänster (borttaget) till Forms-tjänsten:

1. Inkludera projektfiler.
1. Skapa ett formulär och ett API-objekt för dokumenthanteringsklienten.
1. Hämta formulärdesignen från Content Services (utgått).
1. Återge det interaktiva PDF-formuläret.
1. Utför en åtgärd med formulärdataströmmen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

**Skapa ett formulär och ett API-objekt för dokumenthanteringsklienten**

Skapa ett API-objekt för Forms-klienten innan du programmässigt kan utföra en åtgärd i API:t för Forms-tjänsten. Eftersom det här arbetsflödet hämtar en XDP-fil från Content Services (utgått) skapar du också ett API-objekt för dokumenthantering.

**Hämta formulärdesignen från innehållstjänster (borttagen)**

Hämta XDP-filen från Content Services (utgått) med Java- eller webbtjänstens API. XDP-filen returneras i en `com.adobe.idp.Document` instans (eller en `BLOB` instans om du använder webbtjänster). Du kan sedan skicka `com.adobe.idp.Document` instansen till Forms-tjänsten.

**Återge ett interaktivt PDF-formulär**

Om du vill återge ett interaktivt formulär skickar du den `com.adobe.idp.Document` instans som returnerades från Content Services (utgått) till Forms-tjänsten.

>[!NOTE]
>
>Du kan skicka en `com.adobe.idp.Document` som innehåller formulärdesignen till Forms-tjänsten. Två nya metoder som heter `renderPDFForm2` och `renderHTMLForm2` godkänner ett `com.adobe.idp.Document` objekt som innehåller en formulärdesign.

**Utför en åtgärd med formulärdataströmmen**

Beroende på vilken typ av klientprogram du använder kan du skriva formuläret till en webbläsare eller spara formuläret som en PDF-fil. Ett webbaserat program skriver vanligtvis formuläret i webbläsaren. Ett skrivbordsprogram sparar dock vanligtvis formuläret som en PDF-fil.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Skicka dokument till Forms Service med Java API {#pass-documents-to-the-forms-service-using-the-java-api}

Skicka ett dokument som hämtats från Content Services (utgått) med Forms-tjänsten och Content Services (utgått) API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar och adobe-contentservices-client.jar, i Java-projektets klassökväg.

1. Skapa ett formulär och ett API-objekt för dokumenthanteringsklienten

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper. (Se [Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Skapa ett `FormsServiceClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.
   * Skapa ett `DocumentManagementServiceClientImpl` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.

1. Hämta formulärdesignen från innehållstjänster (borttagen)

   Anropa `DocumentManagementServiceClientImpl` objektets `retrieveContent` metod och skicka följande värden:

   * Ett strängvärde som anger den lagringsplats där innehållet läggs till. Standardbutiken är `SpacesStore`. Detta värde är en obligatorisk parameter.
   * Ett strängvärde som anger den fullständigt kvalificerade sökvägen för innehållet som ska hämtas (till exempel `/Company Home/Form Designs/Loan.xdp`). Detta värde är en obligatorisk parameter.
   * Ett strängvärde som anger versionen. Det här värdet är en valfri parameter och du kan skicka en tom sträng. I det här fallet hämtas den senaste versionen.
   Metoden returnerar `retrieveContent` ett `CRCResult` objekt som innehåller XDP-filen. Hämta en `com.adobe.idp.Document` instans genom att anropa `CRCResult` objektets `getDocument` metod.

1. Återge ett interaktivt PDF-formulär

   Anropa `FormsServiceClient` objektets `renderPDFForm2` metod och skicka följande värden:

   * Ett `com.adobe.idp.Document` objekt som innehåller formulärdesignen som hämtats från innehållstjänster (borttagen).
   * Ett `com.adobe.idp.Document` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du ett tomt `com.adobe.idp.Document` objekt.
   * Ett `PDFFormRenderSpec` objekt som lagrar körningsalternativ. Det här värdet är en valfri parameter, och du kan ange `null` om du inte vill ange körningsalternativ.
   * Ett `URLSpec` objekt som innehåller URI-värden. Det här värdet är en valfri parameter som du kan ange `null`.
   * Ett `java.util.HashMap` objekt som lagrar bifogade filer. Det här värdet är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.
   Metoden returnerar `renderPDFForm` ett `FormsResult` objekt som innehåller en formulärdataström som måste skrivas till klientens webbläsare.

1. Utför en åtgärd med formulärdataströmmen

   * Skapa ett `com.adobe.idp.Document` objekt genom att anropa `FormsResult` objektets `getOutputContent` metod.
   * Hämta innehållstypen för `com.adobe.idp.Document` objektet genom att anropa dess `getContentType` metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metod och skicka `com.adobe.idp.Document` objektets innehållstyp.
   * Skapa ett `javax.servlet.ServletOutputStream` objekt som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` metod.
   * Skapa ett `java.io.InputStream` objekt genom att anropa `com.adobe.idp.Document` objektets `getInputStream` metod.
   * Skapa en bytearray och fyll i den med formulärdataströmmen genom att anropa `InputStream` objektets `read` metod. Skicka bytearrayen som ett argument.
   * Anropa `javax.servlet.ServletOutputStream` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` metoden.

**Se även**

[Snabbstart (SOAP-läge): Skicka dokument till Forms Service med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Skicka dokument till Forms Service med hjälp av webbtjänstens API {#pass-documents-to-the-forms-service-using-the-web-service-api}

Skicka ett dokument som hämtats från Content Services (utgått) med Forms-tjänsten och Content Services (utgått) API (webbtjänsten):

1. Inkludera projektfiler

   Skapa ett Microsoft .NET-projekt som använder MTOM. Eftersom det här klientprogrammet anropar två AEM Forms-tjänster skapar du två tjänstreferenser. Använd följande WSDL-definition för den tjänstreferens som är kopplad till Forms-tjänsten: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Använd följande WSDL-definition för den tjänstreferens som är kopplad till dokumenthanteringstjänsten: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Eftersom `BLOB` datatypen är gemensam för båda tjänstreferenserna kvalificerar du datatypen fullständigt `BLOB` när du använder den. I motsvarande snabbstart för webbtjänsten är alla `BLOB` instanser kvalificerade.

   >[!NOTE]
   >
   >Ersätt `localhost`med IP-adressen för servern som är värd för AEM Forms.

1. Skapa ett formulär och ett API-objekt för dokumenthanteringsklienten

   * Skapa ett `FormsServiceClient` objekt med hjälp av dess standardkonstruktor.
   * Skapa ett `FormsServiceClient.Endpoint.Address` objekt med hjälp av `System.ServiceModel.EndpointAddress` konstruktorn. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/FormsService?WSDL`). Du behöver inte använda attributet `lc_version` . Det här attributet används när du skapar en tjänstreferens.)
   * Skapa ett `System.ServiceModel.BasicHttpBinding` objekt genom att hämta värdet för `FormsServiceClient.Endpoint.Binding` fältet. Sänd returvärdet till `BasicHttpBinding`.
   * Ställ in `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela användarnamnet för AEM-formulär till fältet `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.
   >[!NOTE]
   >
   >Upprepa dessa steg för `DocumentManagementServiceClient`tjänstklienten.

1. Hämta formulärdesignen från innehållstjänster (borttagen)

   Hämta innehåll genom att anropa `DocumentManagementServiceClient` objektets `retrieveContent` metod och skicka följande värden:

   * Ett strängvärde som anger den lagringsplats där innehållet läggs till. Standardbutiken är `SpacesStore`. Detta värde är en obligatorisk parameter.
   * Ett strängvärde som anger den fullständigt kvalificerade sökvägen för innehållet som ska hämtas (till exempel `/Company Home/Form Designs/Loan.xdp`). Detta värde är en obligatorisk parameter.
   * Ett strängvärde som anger versionen. Det här värdet är en valfri parameter och du kan skicka en tom sträng. I det här fallet hämtas den senaste versionen.
   * En strängutdataparameter som lagrar värdet för bläddringslänken.
   * En `BLOB` utdataparameter som lagrar innehållet. Du kan använda den här utdataparametern för att hämta innehållet.
   * En `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` utdataparameter som lagrar innehållsattribut.
   * En `CRCResult` utdataparameter. I stället för att använda det här objektet kan du använda parametern `BLOB` output för att hämta innehållet.

1. Återge ett interaktivt PDF-formulär

   Anropa `FormsServiceClient` objektets `renderPDFForm2` metod och skicka följande värden:

   * Ett `BLOB` objekt som innehåller formulärdesignen som hämtats från innehållstjänster (borttagen).
   * Ett `BLOB` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du ett tomt `BLOB` objekt.
   * Ett `PDFFormRenderSpec` objekt som lagrar körningsalternativ. Det här värdet är en valfri parameter, och du kan ange `null` om du inte vill ange körningsalternativ.
   * Ett `URLSpec` objekt som innehåller URI-värden. Det här värdet är en valfri parameter som du kan ange `null`.
   * Ett `Map` objekt som lagrar bifogade filer. Det här värdet är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.
   * En lång utdataparameter som används för att lagra sidantalet.
   * En strängutdataparameter som används för att lagra språkvärdet.
   * En `FormsResult` utdataparameter som används för att lagra det interaktiva PDF-formuläret `.`
   Metoden returnerar `renderPDFForm2` ett `FormsResult` objekt som innehåller det interaktiva PDF-formuläret.

1. Utför en åtgärd med formulärdataströmmen

   * Skapa ett `BLOB` objekt som innehåller formulärdata genom att hämta värdet för `FormsResult` objektets `outputContent` fält.
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för det interaktiva PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i det `BLOB` objekt som hämtats från `FormsResult` objektet. Fyll i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa ett `System.IO.BinaryWriter` objekt genom att anropa dess konstruktor och skicka `System.IO.FileStream` objektet.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` metod och skicka bytearrayen.

**Se även**

[Anropa AEM-formulär med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
