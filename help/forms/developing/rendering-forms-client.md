---
title: Återger Forms på klienten
seo-title: Rendering Forms at the Client
description: Optimera leveransen av PDF-innehåll och förbättra Forms-tjänstens förmåga att hantera nätverksbelastningen genom att använda klientsidesrenderingsfunktionen i Acrobat eller Adobe Reader
seo-description: Optimize the delivery of PDF content and improve the Forms service’s ability to handle network load by using the client-side rendering capability of Acrobat or Adobe Reader
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
role: Developer
exl-id: e485980d-f200-46b7-9284-c9996003aa47
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 0%

---

# Återger Forms på klienten {#rendering-forms-at-the-client}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

## Återger Forms på klienten {#rendering-forms-at-the-client-inner}

Du kan optimera leveransen av PDF-innehåll och förbättra Forms-tjänstens förmåga att hantera nätverksbelastningen genom att använda klientsidesrenderingsfunktionen i Acrobat eller Adobe Reader. Den här processen kallas att återge ett formulär på klienten. Om du vill återge ett formulär på klienten måste klientenheten (vanligtvis en webbläsare) använda Acrobat 7.0 eller Adobe Reader 7.0 eller senare.

Ändringar i ett formulär som är ett resultat av skriptkörning på serversidan återspeglas inte i ett formulär som återges på klienten såvida inte rotdelformuläret innehåller `restoreState` attribut som är inställt på `auto`. Mer information om det här attributet finns i [Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Mer information om tjänsten Forms finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Så här återger du ett formulär på klienten:

1. Inkludera projektfiler.
1. Skapa ett Forms Client API-objekt.
1. Ange körningsalternativ för klientåtergivning.
1. Återge ett formulär på klienten.
1. Skriv formuläret till webbläsaren.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett Forms Client API-objekt**

Innan du programmässigt kan utföra en API-åtgärd för Forms-tjänstklienten måste du skapa en Forms-tjänstklient. Om du använder Java API skapar du en `FormsServiceClient` -objekt. Om du använder Forms webbtjänst-API skapar du en `FormsService` -objekt.

**Ange körningsalternativ för klientåtergivning**

Ange körtidsalternativet för klientåtergivning för att återge ett formulär på klienten genom att ställa in `RenderAtClient` körningsalternativ till `true`. Detta resulterar i att formuläret levereras till klientenheten där det återges. If `RenderAtClient` är `auto` (standardvärdet) avgör formulärdesignen om formuläret återges hos klienten. Formulärdesignen måste vara en formulärdesign med flödeslayout.

Ett valfritt körningsalternativ som du kan ange är `SeedPDF` alternativ. The `SeedPDF` används för att kombinera PDF-behållaren (dirigerat PDF-dokument) med formulärdesignen och XML-data. Både formulärdesignen och XML-data levereras till Acrobat eller Adobe Reader, där formuläret återges. The `SeedPDF` kan användas när klientdatorn inte har teckensnitt som används i formuläret, till exempel när en slutanvändare inte har licens att använda ett teckensnitt som formulärägaren har licens att använda.

Du kan använda Designer för att skapa en enkel, dynamisk PDF-fil som kan användas som startvärdesfil för PDF. Följande steg krävs för att utföra den här uppgiften:

1. Ange om du behöver bädda in teckensnitt i startfilen för PDF. Filen för dirigerade PDF måste innehålla ytterligare teckensnitt som krävs för att formuläret ska kunna återges. När du bäddar in teckensnitt i startfilen måste du se till att du inte bryter mot några licensavtal för teckensnitt. I Designer kan du bestämma om du ska kunna bädda in teckensnitt som är juridiskt bindande. Om det finns teckensnitt som du inte kan bädda in i formuläret visas ett meddelande med en lista över de teckensnitt som du inte kan bädda in när du sparar. Det här meddelandet visas inte i Designer för statiska PDF-dokument.
1. Om du skapar startvärdesfilen PDF i Designer bör du åtminstone lägga till ett textfält som innehåller ett meddelande. Meddelandet bör riktas till användare av tidigare versioner av Adobe Reader som uppger att de behöver Acrobat 7.0 eller senare eller Adobe Reader 7.0 eller senare för att kunna visa dokumentet.
1. Spara startvärdesfilen PDF som en dynamisk PDF-fil med filnamnstillägget PDF.

>[!NOTE]
>
>Du behöver inte definiera startalternativet för PDF för att återge ett formulär på klienten. Om du inte anger en dirigerad PDF skapar Forms-tjänsten en skal-pdf som inte innehåller COS-objekt, men som innehåller en PDF-wrapper med det faktiska XDP-innehållet inbäddat. Stegen i det här avsnittet anger inte körningsalternativet för dirigerad PDF. Mer information om COS-objekt finns i referenshandboken för Adobe PDF.

**Återge ett formulär på klienten**

Om du vill återge ett formulär på klienten måste du se till att alternativen för klientåtergivning vid körning inkluderas i programlogiken för att återge ett formulär.

**Skriv formulärdataströmmen till klientens webbläsare**

Forms skapar en formulärdataström som du måste skriva till klientens webbläsare. När formuläret skrivs till webbläsaren återges det av Acrobat 7.0 eller Adobe Reader 7.0 eller senare och är synligt för användaren.

**Se även**

[Återge ett formulär på klienten med Java API](#render-a-form-at-the-client-using-the-java-api)

[Återge ett formulär på klienten med hjälp av webbtjänstens API](#render-a-form-at-the-client-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Skicka dokument till Forms](/help/forms/developing/passing-documents-forms-service.md)

[Skapa webbprogram som återger Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Återge ett formulär på klienten med Java API {#render-a-form-at-the-client-using-the-java-api}

Återge ett formulär på klienten med Forms API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar, i Java-projektets klassökväg.

1. Skapa ett Forms Client API-objekt

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `FormsServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Ange körningsalternativ för klientåtergivning

   * Skapa en `PDFFormRenderSpec` genom att använda dess konstruktor.
   * Ange `RenderAtClient` körningsalternativ genom att anropa `PDFFormRenderSpec` objektets `setRenderAtClient` och skicka enum-värdet `RenderAtClient.Yes`.

1. Återge ett formulär på klienten

   Anropa `FormsServiceClient` objektets `renderPDFForm` och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som ingår i ett AEM Forms-program måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du en tom `com.adobe.idp.Document` -objekt.
   * A `PDFFormRenderSpec` objekt som lagrar körningsalternativ som krävs för att återge ett formulär på klienten.
   * A `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten för att återge ett formulär.
   * A `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.

   The `renderPDFForm` returnerar en `FormsResult` objekt som innehåller en formulärdataström som måste skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa en `com.adobe.idp.Document` genom att anropa `FormsResult` objekt&quot;s `getOutputContent` -metod.
   * Hämta innehållstypen för `com.adobe.idp.Document` genom att anropa dess `getContentType` -metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metoden och skicka innehållstypen för `com.adobe.idp.Document` -objekt.
   * Skapa en `javax.servlet.ServletOutputStream` som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` -metod.
   * Skapa en `java.io.InputStream` genom att anropa `com.adobe.idp.Document` objektets `getInputStream` -metod.
   * Skapa en bytearray och fylla den med formulärdataströmmen genom att anropa `InputStream` objektets `read` och skicka bytearrayen som ett argument.
   * Anropa `javax.servlet.ServletOutputStream` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` -metod.

**Se även**

[Snabbstart (SOAP-läge): Återge ett formulär på klienten med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Återge ett formulär på klienten med hjälp av webbtjänstens API {#render-a-form-at-the-client-using-the-web-service-api}

Återge ett formulär på klienten med Forms API (webbtjänst):

1. Inkludera projektfiler

   * Skapa Java-proxyklasser som använder Forms tjänst-WSDL.
   * Inkludera Java-proxyklasserna i klassökvägen.

1. Skapa ett Forms Client API-objekt

   Skapa en `FormsService` och ange autentiseringsvärden.

1. Ange körningsalternativ för klientåtergivning

   * Skapa en `PDFFormRenderSpec` genom att använda dess konstruktor.
   * Ange `RenderAtClient` körningsalternativ genom att anropa `PDFFormRenderSpec` objektets `setRenderAtClient` metoden och skicka strängvärdet `RenderAtClient.Yes`.

1. Återge ett formulär på klienten

   Anropa `FormsService` objektets `renderPDFForm` och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som ingår i ett Forms-program måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du `null`. (Se [Förifyll Forms med flödeslayouter](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * A `PDFFormRenderSpec` objekt som lagrar körningsalternativ som krävs för att återge ett formulär på klienten.
   * A `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten.
   * A `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.
   * En tom `com.adobe.idp.services.holders.BLOBHolder` objekt som fylls i av metoden. Den här parametern används för att lagra det återgivna PDF-formuläret.
   * En tom `javax.xml.rpc.holders.LongHolder` objekt som fylls i av metoden. (Det här argumentet lagrar antalet sidor i formuläret).
   * En tom `javax.xml.rpc.holders.StringHolder` objekt som fylls i av metoden. (Det här argumentet lagrar språkets värde).
   * En tom `com.adobe.idp.services.holders.FormsResultHolder` objekt som innehåller resultatet av den här åtgärden.

   The `renderPDFForm` metoden fyller i `com.adobe.idp.services.holders.FormsResultHolder` objekt som skickas som det sista argumentvärdet med en formulärdataström som måste skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa en `FormResult` genom att hämta värdet för `com.adobe.idp.services.holders.FormsResultHolder` objektets `value` datamedlem.
   * Skapa en `BLOB` objekt som innehåller formulärdata genom att anropa `FormsResult` objektets `getOutputContent` -metod.
   * Hämta innehållstypen för `BLOB` genom att anropa dess `getContentType` -metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metoden och skicka innehållstypen för `BLOB` -objekt.
   * Skapa en `javax.servlet.ServletOutputStream` som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` -metod.
   * Skapa en bytearray och fylla i den genom att anropa `BLOB` objektets `getBinaryData` -metod. Den här aktiviteten tilldelar innehållet i `FormsResult` till bytearrayen.
   * Anropa `javax.servlet.http.HttpServletResponse` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` -metod.

**Se även**

[Återger Forms på klienten](#rendering-forms-at-the-client)

[Anropa AEM Forms med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
