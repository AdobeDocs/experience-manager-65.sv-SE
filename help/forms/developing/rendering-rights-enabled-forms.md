---
title: Rendering Rights-aktiverad Forms
seo-title: Rendering Rights-Enabled Forms
description: Använd tjänsten Forms för att återge formulär som har användarrättigheter. Du kan återge behörighetsaktiverade formulär med Java API och Web Service API.
seo-description: Use the Forms service to render forms that have usage rights applied to them. You can render rights-enabled forms using the Java API and Web Service API.
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
role: Developer
exl-id: 012a3a9f-542c-4ed1-a092-572bfccbdf21
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 0%

---

# Rendering Rights-aktiverad Forms {#rendering-rights-enabled-forms}

Forms-tjänsten kan återge formulär som har användarrättigheter. Användningsrättigheterna gäller funktioner som är tillgängliga som standard i Acrobat men inte i Adobe Reader, t.ex. möjligheten att lägga till kommentarer i ett formulär eller att fylla i formulärfält och spara formuläret. Forms med användarrättigheter kallas för rättighetsaktiverade formulär. En användare som öppnar ett rättighetsaktiverat formulär i Adobe Reader kan utföra åtgärder som är aktiverade för det formuläret.

För att kunna lägga in användarrättigheter i ett formulär måste Acrobat Reader DC-tilläggstjänsten ingå i installationen av AEM formulär. Du måste också ha en giltig autentiseringsuppgift som gör att du kan tillämpa användarrättigheter på PDF-dokument. Det innebär att du måste konfigurera Acrobat Reader DC-tilläggstjänsten innan du kan återge ett rättighetsaktiverat formulär. (Se [Om Acrobat Reader DC-tilläggstjänsten](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>Om du vill återge ett formulär som innehåller användningsrättigheter måste du använda en XDP-fil som indata, inte en PDF-fil. Om du använder en PDF-fil som indata återges formuläret fortfarande, men det kommer inte att vara ett aktiverat formulär.

>[!NOTE]
>
>Du kan inte fylla i ett formulär i förväg med XML-data när du anger följande användningsbehörighet: `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles`, eller `enableDigitalSignatures`. (Se [Förifyll Forms med flödeslayouter](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>Mer information om tjänsten Forms finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Sammanfattning av steg {#summary-of-steps}

Så här återger du ett rättighetsaktiverat formulär:

1. Inkludera projektfiler.
1. Skapa ett Forms Client API-objekt.
1. Ange körningsalternativ för användningsrättigheter.
1. Återge ett rättighetsaktiverat formulär.
1. Skriv det aktiverade formuläret i webbläsaren.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett Forms Client API-objekt**

Innan du programmässigt kan utföra en API-åtgärd för Forms-tjänstklienten måste du skapa en Forms-tjänstklient.

**Ange körningsalternativ för användningsrättigheter**

Du måste ange alternativ för användningsbehörighet vid körning för att kunna återge ett rättighetsaktiverat formulär. Du måste också ange aliaset för de autentiseringsuppgifter som används för att tillämpa användarrättigheter på ett formulär. När du har angett aliasvärdet anger du vilken användningsbehörighet som ska gälla för formuläret.

**Återge ett rättighetsaktiverat formulär**

Om du vill återge ett rättighetsaktiverat formulär använder du samma programlogik som att återge ett formulär utan användarrättigheter. Den enda skillnaden är att du måste se till att körningsalternativen för användningsrättigheter inkluderas i programlogiken.

>[!NOTE]
>
>När du återger ett rättighetsaktiverat formulär med Forms webbtjänst-API:t kan du inte bifoga filer till formuläret.

**Skriv formulärdataströmmen till klientens webbläsare**

När Forms-tjänsten återger ett rättighetsaktiverat formulär returneras en formulärdataström som du måste skriva till klientens webbläsare. När formuläret har skrivits till webbläsaren visas det för användaren. En användare som visar det aktiverade formuläret i Adobe Reader kan utföra åtgärder som är aktiverade för det formuläret.

**Se även**

[Återge rättighetsaktiverade formulär med Java API](#render-rights-enabled-forms-using-the-java-api)

[Återge rättighetsaktiverade formulär med webbtjänstens API](#render-rights-enabled-forms-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Återger interaktiv PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Skapa webbprogram som återger Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Återge rättighetsaktiverade formulär med Java API {#render-rights-enabled-forms-using-the-java-api}

Återge ett rättighetsaktiverat formulär med Forms API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar, i Java-projektets klassökväg.

1. Skapa ett Forms Client API-objekt

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `FormsServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Ange körningsalternativ för användningsrättigheter

   * Skapa en `ReaderExtensionSpec` genom att använda dess konstruktor.
   * Ange alias för autentiseringsuppgifterna genom att anropa `ReaderExtensionSpec` objektets `setReCredentialAlias` och ange ett strängvärde som representerar aliasvärdet.
   * Ställ in varje användningsbehörighet genom att anropa motsvarande metod som tillhör `ReaderExtensionSpec` -objekt. Du kan dock bara ange användarbehörighet om du kan göra det med de referenser du anger. Det innebär att du inte kan ange en användningsbehörighet om du inte kan ange den i inloggningsuppgifterna. Till exempel. för att ställa in användarbehörighet som gör att användaren kan fylla i formulärfält och spara formuläret, anropa `ReaderExtensionSpec` objektets `setReFillIn` metod och skicka `true`.

   >[!NOTE]
   >
   >Du behöver inte anropa `ReaderExtensionSpec` objektets `setReCredentialPassword` -metod. Den här metoden används inte av Forms-tjänsten.

1. Återge ett rättighetsaktiverat formulär

   Anropa `FormsServiceClient` objektets `renderPDFFormWithUsageRights` och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som ingår i ett Forms-program måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du en tom `com.adobe.idp.Document` -objekt.
   * A `PDFFormRenderSpec` objekt som lagrar körningsalternativ.
   * A `ReaderExtensionSpec` objekt som lagrar körningsalternativ för användningsrättigheter.
   * A `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten.

   The `renderPDFFormWithUsageRights` returnerar en `FormsResult` objekt som innehåller en formulärdataström som måste skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa en `com.adobe.idp.Document` genom att anropa `FormsResult` objekt&quot;s `getOutputContent` -metod.
   * Hämta innehållstypen för `com.adobe.idp.Document` genom att anropa dess `getContentType` -metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metoden och skicka innehållstypen för `com.adobe.idp.Document` -objekt.
   * Skapa en `javax.servlet.ServletOutputStream` som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` -metod.
   * Skapa en `java.io.InputStream` genom att anropa `com.adobe.idp.Document` objektets `getInputStream` -metod.
   * Skapa en bytearray som fyller i den med formulärdataströmmen genom att anropa `InputStream` objektets `read` och skicka bytearrayen som ett argument.
   * Anropa `javax.servlet.ServletOutputStream` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` -metod.

**Se även**

[Snabbstart (SOAP-läge): Återge ett rättighetsaktiverat formulär med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Återge rättighetsaktiverade formulär med webbtjänstens API {#render-rights-enabled-forms-using-the-web-service-api}

Återge ett rättighetsaktiverat formulär med Forms API (webbtjänst):

1. Inkludera projektfiler

   * Skapa Java-proxyklasser som använder Forms tjänst-WSDL.
   * Inkludera Java-proxyklasserna i klassökvägen.

1. Skapa ett Forms Client API-objekt

   Skapa en `FormsService` och ange autentiseringsvärden.

1. Ange körningsalternativ för användningsrättigheter

   * Skapa en `ReaderExtensionSpec` genom att använda dess konstruktor.
   * Ange alias för autentiseringsuppgifterna genom att anropa `ReaderExtensionSpec` objektets `setReCredentialAlias` och ange ett strängvärde som representerar aliasvärdet.
   * Ställ in varje användningsbehörighet genom att anropa motsvarande metod som tillhör `ReaderExtensionSpec` -objekt. Du kan dock bara ange användarbehörighet om du kan göra det med de referenser du anger. Det innebär att du inte kan ange en användningsbehörighet om du inte kan ange den i inloggningsuppgifterna. Om du vill ange användarbehörighet som gör det möjligt för en användare att fylla i formulärfält och spara formuläret, anropar du `ReaderExtensionSpec` objektets `setReFillIn` metod och skicka `true`.

1. Återge ett rättighetsaktiverat formulär

   Anropa `FormsService` objektets `renderPDFFormWithUsageRights` och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som ingår i ett Forms-program måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data med formuläret måste du skicka ett `BLOB` -objekt som baseras på en tom XML-datakälla. Du kan inte skicka en `BLOB` -objekt som är null. I annat fall genereras ett undantag.
   * A `PDFFormRenderSpec` objekt som lagrar körningsalternativ.
   * A `ReaderExtensionSpec` objekt som lagrar körningsalternativ för användningsrättigheter.
   * A `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten.

   The `renderPDFFormWithUsageRights` returnerar en `FormsResult` objekt som innehåller en formulärdataström som måste skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa en `BLOB` objekt som innehåller formulärdata genom att anropa `FormsResult` objektets `getOutputContent` -metod.
   * Hämta innehållstypen för `BLOB` genom att anropa dess `getContentType` -metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metoden och skicka innehållstypen för `BLOB` -objekt.
   * Skapa en `javax.servlet.ServletOutputStream` som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` -metod.
   * Skapa en bytearray och fylla i den genom att anropa `BLOB` objektets `getBinaryData` -metod. Den här aktiviteten tilldelar innehållet i `FormsResult` till bytearrayen.
   * Anropa `javax.servlet.http.HttpServletResponse` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` -metod.

**Se även**

[Rendering Rights-aktiverad Forms](#rendering-rights-enabled-forms)

[Anropa AEM Forms med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
