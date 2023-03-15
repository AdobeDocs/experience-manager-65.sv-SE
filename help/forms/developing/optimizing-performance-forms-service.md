---
title: Optimera Forms-tjänstens prestanda
seo-title: Optimizing the Performance of theForms Service
description: Ange körningsalternativ när du återger ett formulär och lagra XDP-filer i databasen för att optimera prestanda för Forms-tjänsten.
seo-description: Set run-time options when rendering a form and store XDP files in the repository to optimize the performance of the Forms service.
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
role: Developer
exl-id: 5a746c6c-bf6e-4b25-ba7c-a35edb1f55f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 0%

---

# Optimera prestanda för Forms-tjänsten {#optimizing-the-performance-of-theforms-service}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

## Optimera prestanda för Forms-tjänsten {#optimizing-the-performance-of-the-forms-service}

När du återger ett formulär kan du ange körningsalternativ som optimerar prestanda för Forms-tjänsten. En annan uppgift som du kan utföra för att förbättra prestandan för Forms-tjänsten är att lagra XDP-filer i databasen. I det här avsnittet beskrivs dock inte hur du utför den här uppgiften. (Se [Anropa en tjänst med ett Java-klientbibliotek](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>Mer information om tjänsten Forms finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Så här optimerar du prestanda för Forms-tjänsten när du återger ett formulär:

1. Inkludera projektfiler.
1. Skapa ett Forms Client API-objekt.
1. Ange alternativ för prestanda vid körning.
1. Återge formuläret.
1. Skriv formulärdataströmmen till klientens webbläsare.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett Forms Client API-objekt**

Innan du programmässigt kan utföra en API-åtgärd för Forms-tjänstklienten måste du skapa en Forms-tjänstklient. Om du använder Java API skapar du en `FormsServiceClient` -objekt. Om du använder Forms webbtjänst-API skapar du en `FormsService` -objekt.

**Ange alternativ för prestanda vid körning**

Du kan ställa in följande alternativ för prestandakörning för att förbättra prestandan för Forms-tjänsten:

* **Cache-lagring av formulär**: Du kan cachelagra ett formulär som återges som PDF i servercachen. Varje formulär cachelagras när det har skapats för första gången. Om det cachelagrade formuläret vid en efterföljande återgivning är nyare än formulärdesignens tidsstämpel hämtas formuläret från cachen. Genom att cache-lagra formulär förbättrar du prestanda för Forms-tjänsten eftersom den inte behöver hämta formulärdesignen från en databas.
* Det kan ta längre tid att återge formulärstödlinjer (inaktuella) än andra omformningstyper. Vi rekommenderar att du cache-lagrar formulärguider (borttagna) för att förbättra prestandan.
* **Fristående alternativ**: Om du inte behöver Forms-tjänsten för att utföra beräkningar på serversidan kan du ange alternativet Fristående till `true`, vilket resulterar i att formulär återges utan lägesinformation. Lägesinformation är nödvändig om du vill återge ett interaktivt formulär till en slutanvändare som sedan anger information i formuläret och skickar tillbaka formuläret till Forms. Forms-tjänsten utför sedan en beräkningsåtgärd och återger formuläret till användaren med de resultat som visas i formuläret. Om ett formulär utan statusinformation skickas tillbaka till Forms-tjänsten är endast XML-data tillgängliga och serversidesberäkningar utförs inte.
* **Linjäriserad PDF**: En linjäriserad PDF-fil ordnas för att möjliggöra effektiv inkrementell åtkomst i en nätverksmiljö. PDF-filen är giltig PDF i alla avseenden och kompatibel med alla befintliga visningsprogram och andra PDF-program. Det innebär att en linjär PDF kan visas medan den fortfarande hämtas.
* Det här alternativet förbättrar inte prestanda när ett PDF-formulär återges på klienten.
* **GuideRSL, alternativ**: Aktiverar generering av formulärguiden (borttagen) med hjälp av delade bibliotek vid körning. Det innebär att den första begäran hämtar en mindre SWF-fil, plus större delade bibliotek som lagras i webbläsarens cache. Mer information finns i RSL i Flex-dokumentationen.
* Du kan även förbättra prestanda för Forms-tjänsten genom att återge ett formulär på klienten. (Se [Återger Forms på klienten](/help/forms/developing/rendering-forms-client.md).)

**Återge formuläret**

Om du vill återge formuläret efter att du har angett prestandaalternativ använder du samma programlogik som att återge ett formulär utan prestandaalternativ.

**Skriv formulärdataströmmen till klientens webbläsare**

När Forms-tjänsten återger ett formulär returneras en formulärdataström som du måste skriva till klientens webbläsare. När formuläret skrivs till webbläsaren visas det för användaren.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Återger interaktiv PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Återger Forms som HTML](/help/forms/developing/rendering-forms-html.md)

[Skapa webbprogram som återger Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Optimera prestanda med Java API {#optimize-the-performance-using-the-java-api}

Rendera ett formulär med optimerade prestanda med Forms API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar, i Java-projektets klassökväg.

1. Skapa ett Forms Client API-objekt

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `FormsServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Ange alternativ för prestanda vid körning

   * Skapa en `PDFFormRenderSpec` genom att använda dess konstruktor.
   * Ange alternativet för formulärcache genom att anropa `PDFFormRenderSpec` objektets `setCacheEnabled` metod och att skicka `true`.
   * Ange alternativet linjär genom att anropa `PDFFormRenderSpec` objektets `setLinearizedPDF` metod och att skicka `true.`

1. Återge formuläret

   Anropa `FormsServiceClient` objektets `renderPDFForm` och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget.
   * A `com.adobe.idp.Document` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du en tom `com.adobe.idp.Document` -objekt.
   * A `PDFFormRenderSpec` objekt som lagrar körningsalternativ för att förbättra prestandan.
   * A `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten.
   * A `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.

   The `renderPDFForm` returnerar en `FormsResult` objekt som innehåller en formulärdataström som måste skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa en `javax.servlet.ServletOutputStream` som används för att skicka en formulärdataström till klientens webbläsare.
   * Skapa en `com.adobe.idp.Document` genom att anropa `FormsResult` objekt&quot;s `getOutputContent` -metod.
   * Skapa en `java.io.InputStream` genom att anropa `com.adobe.idp.Document` objektets `getInputStream` -metod.
   * Skapa en bytearray och fylla den med formulärdataströmmen genom att anropa `InputStream` objektets `read`och skicka bytearrayen som ett argument.
   * Anropa `javax.servlet.ServletOutputStream` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` -metod.

**Se även**

[Snabbstart (SOAP-läge): Optimera prestanda med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Optimera prestanda med hjälp av webbtjänstens API {#optimize-the-performance-using-the-web-service-api}

Rendera ett formulär med optimerade prestanda med Forms API (webbtjänst):

1. Inkludera projektfiler

   * Skapa Java-proxyklasser som använder Forms tjänst-WSDL.
   * Inkludera Java-proxyklasserna i klassökvägen.

1. Skapa ett Forms Client API-objekt

   Skapa en `FormsService` och ange autentiseringsvärden.

1. Ange alternativ för prestanda vid körning

   * Skapa en `PDFFormRenderSpec` genom att använda dess konstruktor.
   * Ange alternativet för formulärcache genom att anropa `PDFFormRenderSpec` objektets `setCacheEnabled` och skickar true.
   * Ange det fristående alternativet genom att anropa `PDFFormRenderSpec` objektets `setStandAlone` och skickar true.
   * Ange alternativet linjär genom att anropa `PDFFormRenderSpec` objektets `setLinearizedPDF` och skickar true.

1. Återge formuläret

   Anropa `FormsService` objektets `renderPDFForm` och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget.
   * A `BLOB` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du `null`.
   * A `PDFFormRenderSpecc` objekt som lagrar körningsalternativ.
   * A `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten.
   * A `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.
   * En tom `com.adobe.idp.services.holders.BLOBHolder` objekt som fylls i av metoden. Detta används för att lagra det återgivna PDF-formuläret.
   * En tom `javax.xml.rpc.holders.LongHolder` objekt som fylls i av metoden. (Det här argumentet lagrar antalet sidor i formuläret).
   * En tom `javax.xml.rpc.holders.StringHolder` objekt som fylls i av metoden. (Det här argumentet lagrar språkets värde).
   * En tom `com.adobe.idp.services.holders.FormsResultHolder` objekt som innehåller resultatet av den här åtgärden.

   The `renderPDFForm` metoden fyller i `com.adobe.idp.services.holders.FormsResultHolder` objekt som skickas som det sista argumentvärdet med en formulärdataström som måste skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa en `FormResult` genom att hämta värdet för `com.adobe.idp.services.holders.FormsResultHolder` objektets `value` datamedlem.
   * Skapa en `javax.servlet.ServletOutputStream` som används för att skicka en formulärdataström till klientens webbläsare.
   * Skapa en `BLOB` objekt som innehåller formulärdata genom att anropa `FormsResult` objektets `getOutputContent` -metod.
   * Skapa en bytearray och fylla i den genom att anropa `BLOB` objektets `getBinaryData` -metod. Den här aktiviteten tilldelar innehållet i `FormsResult` till bytearrayen.
   * Anropa `javax.servlet.http.HttpServletResponse` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` -metod.

**Se även**

[Anropa AEM Forms med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
