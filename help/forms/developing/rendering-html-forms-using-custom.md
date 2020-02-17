---
title: Återge HTML-formulär med anpassade CSS-filer
seo-title: Återge HTML-formulär med anpassade CSS-filer
description: 'null'
seo-description: 'null'
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Återge HTML-formulär med anpassade CSS-filer {#rendering-html-forms-using-custom-css-files}

Forms-tjänsten återger HTML-formulär som svar på en HTTP-begäran från en webbläsare. När du återger ett HTML-formulär kan Forms-tjänsten referera till en anpassad CSS-fil. Du kan skapa en anpassad CSS-fil som uppfyller dina affärskrav och referera till den CSS-filen när du använder Forms-tjänsten för att återge HTML-formulär.

Forms-tjänsten tolkar den anpassade CSS-filen tyst. Det innebär att Forms-tjänsten inte rapporterar fel som kan uppstå om den anpassade CSS-filen inte uppfyller CSS-standarderna. I det här fallet ignorerar Forms-tjänsten formatet och fortsätter med de återstående formaten som finns i CSS-filen.

I följande lista anges format som stöds i en anpassad CSS-fil:

* **Väljarliknande par** på klassnivå: Om det finns i en anpassad CSS-fil används väljare som används som klassformat i HTML-formuläret. Oanvända klassformat ignoreras.
* **Väljarstilspar** på identifierarnivå: Alla identifierarformat används om de används i HTML-formuläret.
* **Elementnivåväljarliknande par**: Alla elementformat används om de används i HTML-formuläret.
* **Formatprioritet**: Formatprioritet (som important) stöds och kan användas i en anpassad CSS-fil.
* **Medietyp**: Ett eller flera väljarliknande par kan kapslas in i @media-format för att definiera medietypen. Tjänsten Forms kontrollerar inte om den angivna medietypen stöds. Den medietyp som anges i den anpassade CSS-filen sammanfogas i HTML-formuläret.

Du kan hämta en CSS-exempelfil med FormsIVS-programmet. Ladda upp formuläret, markera det på sidan Testa formulärdesign och klicka på GenerateCSS. Du behöver inte ange HTML-omformningstypen innan du klickar på knappen. Välj sedan Spara. Du kan redigera den här CSS-filen så att den uppfyller dina affärskrav.

>[!NOTE]
>
>Innan du återger ett HTML-formulär som använder en anpassad CSS-fil är det viktigt att du har en god förståelse för att återge HTML-formulär. (Se [Återge formulär som HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Mer information om Forms-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Sammanfattning av steg {#summary-of-steps}

Så här återger du ett HTML-formulär som använder en CSS-fil:

1. Inkludera projektfiler.
1. Skapa ett Forms Java API-objekt.
1. Referera till CSS-filen.
1. Återge ett HTML-formulär.
1. Skriv formulärdataströmmen till klientens webbläsare.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett Forms Java API-objekt**

Innan du programmässigt kan utföra en åtgärd som stöds av Forms-tjänsten måste du skapa ett Forms-klientobjekt.

**Referera till CSS-filen**

Om du vill återge ett HTML-formulär som använder en anpassad CSS-fil måste du referera till en befintlig CSS-fil.

**Återge ett HTML-formulär**

Om du vill återge ett HTML-formulär måste du ange en formulärdesign som har skapats i Designer och sparats som en XDP-fil. Du måste också välja en HTML-omformningstyp. Du kan till exempel ange HTML-omformningstypen som återger en dynamisk HTML för Internet Explorer 5.0 eller senare.

Återgivning av ett HTML-formulär kräver också värden, t.ex. URI-värden som behövs för att återge andra formulärtyper.

**Skriv formulärdataströmmen till klientens webbläsare**

När Forms-tjänsten återger ett HTML-formulär returneras ett formulärdataflöde som du måste skriva till klientens webbläsare för att göra HTML-formuläret synligt för användaren.

**Se även**

[Återge ett HTML-formulär som använder en CSS-fil med Java API](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Återgivning av interaktiva PDF-formulär](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Återger formulär som HTML](/help/forms/developing/rendering-forms-html.md)

[Skapa webbprogram som återger formulär](/help/forms/developing/creating-web-applications-renders-forms.md)

## Återge ett HTML-formulär som använder en CSS-fil med Java API {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Återge ett HTML-formulär som använder en anpassad CSS-fil med hjälp av Forms API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar, i Java-projektets klassökväg.

1. Skapa ett Forms Java API-objekt

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa ett `FormsServiceClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.

1. Referera till CSS-filen

   * Skapa ett `HTMLRenderSpec` objekt med hjälp av dess konstruktor.
   * Om du vill återge HTML-formuläret som använder en anpassad CSS-fil anropar du `HTMLRenderSpec` objektets `setCustomCSSURI` metod och skickar ett strängvärde som anger platsen och namnet på CSS-filen.

1. Återge ett HTML-formulär

   Anropa `FormsServiceClient` objektets `(Deprecated) (Deprecated) renderHTMLForm` metod och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som är en del av ett formulärprogram måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Ett `TransformTo` uppräkningsvärde som anger HTML-inställningstypen. Om du till exempel vill återge ett HTML-formulär som är kompatibelt med dynamisk HTML för Internet Explorer 5.0 eller senare anger du `TransformTo.MSDHTML`.
   * Ett `com.adobe.idp.Document` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du ett tomt `com.adobe.idp.Document` objekt.
   * Det objekt `HTMLRenderSpec` som lagrar körningsalternativ för HTML.
   * Ett strängvärde som anger `HTTP_USER_AGENT` rubrikvärdet, till exempel `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Ett `URLSpec` objekt som lagrar de URI-värden som krävs för att återge ett HTML-formulär.
   * Ett `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter, och du kan ange `null` om du inte vill bifoga filer till formuläret.
   Metoden returnerar `(Deprecated) renderHTMLForm` ett `FormsResult` objekt som innehåller en formulärdataström som måste skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa ett `com.adobe.idp.Document` objekt genom att anropa `FormsResult` objektets `getOutputContent` metod.
   * Hämta innehållstypen för `com.adobe.idp.Document` objektet genom att anropa dess `getContentType` metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metod och skicka `com.adobe.idp.Document` objektets innehållstyp.
   * Skapa ett `javax.servlet.ServletOutputStream` objekt som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.h\ttp.HttpServletResponse` objektets `getOutputStream` metod.
   * Skapa ett `java.io.InputStream` objekt genom att anropa `com.adobe.idp.Document` objektets `getInputStream` metod.
   * Skapa en bytearray och fyll i den med formulärdataströmmen genom att anropa `InputStream` objektets `read` metod och skicka bytearrayen som ett argument.
   * Anropa `javax.servlet.ServletOutputStream` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` metoden.

**Se även**

[Återge HTML-formulär med anpassade CSS-filer](#rendering-html-forms-using-custom-css-files)

[Snabbstart (SOAP-läge): Återge ett HTML-formulär som använder en CSS-fil med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Återge ett HTML-formulär som använder en CSS-fil med webbtjänstens API {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Återge ett HTML-formulär som använder en anpassad CSS-fil med Forms API (webbtjänsten):

1. Inkludera projektfiler

   * Skapa Java-proxyklasser som använder Forms-tjänstens WSDL.
   * Inkludera Java-proxyklasserna i klassökvägen.

1. Skapa ett Forms Java API-objekt

   Skapa ett `FormsService` objekt och ange autentiseringsvärden.

1. Referera till CSS-filen

   * Skapa ett `HTMLRenderSpec` objekt med hjälp av dess konstruktor.
   * Om du vill återge HTML-formuläret som använder en anpassad CSS-fil anropar du `HTMLRenderSpec` objektets `setCustomCSSURI` metod och skickar ett strängvärde som anger platsen och namnet på CSS-filen.

1. Återge ett HTML-formulär

   Anropa `FormsService` objektets `(Deprecated) renderHTMLForm` metod och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som är en del av ett formulärprogram måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Ett `TransformTo` uppräkningsvärde som anger HTML-inställningstypen. Om du till exempel vill återge ett HTML-formulär som är kompatibelt med dynamisk HTML för Internet Explorer 5.0 eller senare anger du `TransformTo.MSDHTML`.
   * Ett `BLOB` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du `null`. (Se [Fylla i formulär i förväg med flödeslayouter](/help/forms/development/rendering-forms-rendering-forms preiating-forms-flowable-layouts-preiating.md#prepopulating-forms-with-flowable-layouts).)
   * Det objekt `HTMLRenderSpec` som lagrar körningsalternativ för HTML.
   * Ett strängvärde som anger `HTTP_USER_AGENT` rubrikvärdet, till exempel `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Du kan skicka en tom sträng om du inte vill ange det här värdet.
   * Ett `URLSpec` objekt som lagrar de URI-värden som krävs för att återge ett HTML-formulär.
   * Ett `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter, och du kan ange `null` om du inte vill bifoga filer till formuläret.
   * Ett tomt `com.adobe.idp.services.holders.BLOBHolder` objekt som fylls i av `(Deprecated) renderHTMLForm` metoden. Det här parametervärdet lagrar det återgivna formuläret.
   * Ett tomt `com.adobe.idp.services.holders.BLOBHolder` objekt som fylls i av `(Deprecated) renderHTMLForm` metoden. Den här parametern lagrar XML-data för utdata.
   * Ett tomt `javax.xml.rpc.holders.LongHolder` objekt som fylls i av `(Deprecated) renderHTMLForm` metoden. Det här argumentet lagrar antalet sidor i formuläret.
   * Ett tomt `javax.xml.rpc.holders.StringHolder` objekt som fylls i av `(Deprecated) renderHTMLForm` metoden. Det här argumentet lagrar språkets värde.
   * Ett tomt `javax.xml.rpc.holders.StringHolder` objekt som fylls i av `(Deprecated) renderHTMLForm` metoden. Det här argumentet lagrar det HTML-återgivningsvärde som används.
   * Ett tomt `com.adobe.idp.services.holders.FormsResultHolder` objekt som innehåller resultatet av den här åtgärden.
   Metoden `(Deprecated) renderHTMLForm` fyller i det `com.adobe.idp.services.holders.FormsResultHolder` objekt som skickas som det sista argumentvärdet med en formulärdataström som måste skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa ett `FormResult` objekt genom att hämta värdet för `com.adobe.idp.services.holders.FormsResultHolder` objektets `value` datamedlem.
   * Skapa ett `BLOB` objekt som innehåller formulärdata genom att anropa `FormsResult` objektets `getOutputContent` metod.
   * Hämta innehållstypen för `BLOB` objektet genom att anropa dess `getContentType` metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metod och skicka `BLOB` objektets innehållstyp.
   * Skapa ett `javax.servlet.ServletOutputStream` objekt som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` metod.
   * Skapa en bytearray och fyll i den genom att anropa `BLOB` objektets `getBinaryData` metod. Den här aktiviteten tilldelar innehållet i `FormsResult` objektet till bytearrayen.
   * Anropa `javax.servlet.http.HttpServletResponse` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` metoden.

**Se även**

[Återge HTML-formulär med anpassade CSS-filer](#rendering-html-forms-using-custom-css-files)

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
