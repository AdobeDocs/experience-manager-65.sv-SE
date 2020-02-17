---
title: Återge formulär på klienten
seo-title: Återge formulär på klienten
description: 'null'
seo-description: 'null'
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Återge formulär på klienten {#rendering-forms-at-the-client}

## Återge formulär på klienten {#rendering-forms-at-the-client-inner}

Du kan optimera leveransen av PDF-innehåll och förbättra Forms-tjänstens förmåga att hantera nätverksbelastningen genom att använda klientåtergivningsfunktionen i Acrobat eller Adobe Reader. Den här processen kallas att återge ett formulär på klienten. Om du vill återge ett formulär på klienten måste klientenheten (vanligtvis en webbläsare) använda Acrobat 7.0 eller Adobe Reader 7.0 eller senare.

Ändringar i ett formulär som är ett resultat av skriptkörning på serversidan återspeglas inte i ett formulär som återges på klienten, såvida inte rotdelformuläret innehåller det `restoreState` attribut som är inställt på `auto`. Mer information om det här attributet finns i [Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Mer information om Forms-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Så här återger du ett formulär på klienten:

1. Inkludera projektfiler.
1. Skapa ett API-objekt för Forms Client.
1. Ange körningsalternativ för klientåtergivning.
1. Återge ett formulär på klienten.
1. Skriv formuläret till klientens webbläsare.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett API-objekt för FormsClient**

Innan du programmässigt kan utföra en API-åtgärd för Form Service Client måste du skapa en Forms-tjänstklient. Om du använder Java API skapar du ett `FormsServiceClient` objekt. Skapa ett `FormsService` objekt om du använder webbtjänstens API:t för Forms.

**Ange körningsalternativ för klientåtergivning**

Du måste ställa in körtidsalternativet för klientåtergivning så att ett formulär återges på klienten genom att ställa in alternativet för `RenderAtClient` körning på `true`. Detta resulterar i att formuläret levereras till klientenheten där det återges. Om `RenderAtClient` är `auto` (standardvärdet) avgör formulärdesignen om formuläret återges hos klienten. Formulärdesignen måste vara en formulärdesign med flödeslayout.

Ett valfritt körningsalternativ som du kan ange är `SeedPDF` . Med det här alternativet kombineras PDF-behållaren (PDF-startdokument) med formulärdesignen och XML-data. `SeedPDF` Både formulärdesignen och XML-data levereras till Acrobat eller Adobe Reader, där formuläret återges. Alternativet kan `SeedPDF` användas när klientdatorn inte har teckensnitt som används i formuläret, till exempel när en slutanvändare inte har licens att använda ett teckensnitt som formulärägaren har licens att använda.

Du kan använda Designer för att skapa en enkel dynamisk PDF-fil som kan användas som en startad PDF-fil. Följande steg krävs för att utföra den här uppgiften:

1. Ange om du behöver bädda in teckensnitt i den ursprungliga PDF-filen. Seed-PDF-filen måste innehålla ytterligare teckensnitt som krävs för att formuläret ska kunna återges. När du bäddar in teckensnitt i PDF-filen måste du se till att du inte bryter mot några teckensnittslicensavtal. I Designer kan du bestämma om du ska kunna bädda in teckensnitt som är juridiskt bindande. Om det finns teckensnitt som du inte kan bädda in i formuläret visas ett meddelande med en lista över de teckensnitt som du inte kan bädda in när du sparar. Det här meddelandet visas inte i Designer för statiska PDF-dokument.
1. Om du skapar dirigerad PDF-filen i Designer bör du åtminstone lägga till ett textfält som innehåller ett meddelande. Meddelandet ska riktas till användare av tidigare versioner av Adobe Reader som uppger att de behöver Acrobat 7.0 eller senare eller Adobe Reader 7.0 eller senare för att kunna läsa dokumentet.
1. Spara den ursprungliga PDF-filen som en dynamisk PDF-fil med filnamnstillägget PDF.

>[!NOTE]
>
>Du behöver inte definiera alternativet för inledande PDF-körning för att återge ett formulär på klienten. Om du inte anger en dirigerad PDF-fil skapar Forms-tjänsten en skalpdf som inte innehåller COS-objekt, men som innehåller en PDF-wrapper med det faktiska XDP-innehållet inbäddat. Stegen i det här avsnittet anger inte körningsalternativet för dirigerad PDF. Mer information om COS-objekt finns i referenshandboken för Adobe PDF.

**Återge ett formulär på klienten**

Om du vill återge ett formulär på klienten måste du se till att alternativen för klientåtergivning vid körning inkluderas i programlogiken för att återge ett formulär.

**Skriv formulärdataströmmen till klientens webbläsare**

Forms-tjänsten skapar en formulärdataström som du måste skriva till klientens webbläsare. När formuläret skrivs till webbläsaren återges det av Acrobat 7.0 eller Adobe Reader 7.0 eller senare och är synligt för användaren.

**Se även**

[Återge ett formulär på klienten med Java API](#render-a-form-at-the-client-using-the-java-api)

[Återge ett formulär på klienten med hjälp av webbtjänstens API](#render-a-form-at-the-client-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Skicka dokument till formulärtjänsten](/help/forms/developing/passing-documents-forms-service.md)

[Skapa webbprogram som återger formulär](/help/forms/developing/creating-web-applications-renders-forms.md)

### Återge ett formulär på klienten med Java API {#render-a-form-at-the-client-using-the-java-api}

Återge ett formulär på klienten med hjälp av Forms API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar, i Java-projektets klassökväg.

1. Skapa ett API-objekt för FormsClient

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa ett `FormsServiceClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.

1. Ange körningsalternativ för klientåtergivning

   * Skapa ett `PDFFormRenderSpec` objekt med hjälp av dess konstruktor.
   * Ange alternativet för `RenderAtClient` körning genom att anropa `PDFFormRenderSpec` objektets `setRenderAtClient` metod och skicka fasttextvärdet `RenderAtClient.Yes`.

1. Återge ett formulär på klienten

   Anropa `FormsServiceClient` objektets `renderPDFForm` metod och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som är en del av ett AEM Forms-program måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Ett `com.adobe.idp.Document` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du ett tomt `com.adobe.idp.Document` objekt.
   * Ett `PDFFormRenderSpec` objekt som lagrar körningsalternativ som krävs för att återge ett formulär på klienten.
   * Ett `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten för att återge ett formulär.
   * Ett `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.
   Metoden returnerar `renderPDFForm` ett `FormsResult` objekt som innehåller en formulärdataström som måste skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa ett `com.adobe.idp.Document` objekt genom att anropa `FormsResult` objektets `getOutputContent` metod.
   * Hämta innehållstypen för `com.adobe.idp.Document` objektet genom att anropa dess `getContentType` metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metod och skicka `com.adobe.idp.Document` objektets innehållstyp.
   * Skapa ett `javax.servlet.ServletOutputStream` objekt som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` metod.
   * Skapa ett `java.io.InputStream` objekt genom att anropa `com.adobe.idp.Document` objektets `getInputStream` metod.
   * Skapa en bytearray och fyll i den med formulärdataströmmen genom att anropa `InputStream` objektets `read` metod och skicka bytearrayen som ett argument.
   * Anropa `javax.servlet.ServletOutputStream` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` metoden.

**Se även**

[Snabbstart (SOAP-läge): Återge ett formulär på klienten med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Återge ett formulär på klienten med hjälp av webbtjänstens API {#render-a-form-at-the-client-using-the-web-service-api}

Återge ett formulär på klienten med Forms API (webbtjänsten):

1. Inkludera projektfiler

   * Skapa Java-proxyklasser som använder Forms-tjänstens WSDL.
   * Inkludera Java-proxyklasserna i klassökvägen.

1. Skapa ett API-objekt för FormsClient

   Skapa ett `FormsService` objekt och ange autentiseringsvärden.

1. Ange körningsalternativ för klientåtergivning

   * Skapa ett `PDFFormRenderSpec` objekt med hjälp av dess konstruktor.
   * Ange alternativet för `RenderAtClient` körning genom att anropa `PDFFormRenderSpec` objektets `setRenderAtClient` metod och skicka strängvärdet `RenderAtClient.Yes`.

1. Återge ett formulär på klienten

   Anropa `FormsService` objektets `renderPDFForm` metod och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som är en del av ett formulärprogram måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Ett `BLOB` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du `null`. (Se [Fylla i formulär i förväg med flödeslayouter](/help/forms/development/rendering-forms-rendering-forms preiating-forms-flowable-layouts-preiating.md#prepopulating-forms-with-flowable-layouts).)
   * Ett `PDFFormRenderSpec` objekt som lagrar körningsalternativ som krävs för att återge ett formulär på klienten.
   * Ett `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten.
   * Ett `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.
   * Ett tomt `com.adobe.idp.services.holders.BLOBHolder` objekt som fylls i av metoden. Den här parametern används för att lagra det återgivna PDF-formuläret.
   * Ett tomt `javax.xml.rpc.holders.LongHolder` objekt som fylls i av metoden. (Det här argumentet lagrar antalet sidor i formuläret).
   * Ett tomt `javax.xml.rpc.holders.StringHolder` objekt som fylls i av metoden. (Det här argumentet lagrar språkets värde).
   * Ett tomt `com.adobe.idp.services.holders.FormsResultHolder` objekt som innehåller resultatet av den här åtgärden.
   Metoden `renderPDFForm` fyller i det `com.adobe.idp.services.holders.FormsResultHolder` objekt som skickas som det sista argumentvärdet med en formulärdataström som måste skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa ett `FormResult` objekt genom att hämta värdet för `com.adobe.idp.services.holders.FormsResultHolder` objektets `value` datamedlem.
   * Skapa ett `BLOB` objekt som innehåller formulärdata genom att anropa `FormsResult` objektets `getOutputContent` metod.
   * Hämta innehållstypen för `BLOB` objektet genom att anropa dess `getContentType` metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metod och skicka `BLOB` objektets innehållstyp.
   * Skapa ett `javax.servlet.ServletOutputStream` objekt som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` metod.
   * Skapa en bytearray och fyll i den genom att anropa `BLOB` objektets `getBinaryData` metod. Den här aktiviteten tilldelar innehållet i `FormsResult` objektet till bytearrayen.
   * Anropa `javax.servlet.http.HttpServletResponse` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` metoden.

**Se även**

[Återge formulär på klienten](#rendering-forms-at-the-client)

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
