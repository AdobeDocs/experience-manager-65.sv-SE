---
title: Återge Forms baserat på fragment
seo-title: Rendering Forms Based on Fragments
description: Använd tjänsten Forms för att återge formulär som är baserade på fragment som skapats med Designer.
seo-description: Use the Forms service to render forms that are based on fragments created using Designer.
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
role: Developer
exl-id: febf5350-3fc5-48c0-8bc5-198daff15936
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2209'
ht-degree: 0%

---

# Återge Forms baserat på fragment {#rendering-forms-based-on-fragments}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

## Återge Forms baserat på fragment {#rendering-forms-based-on-fragments-inner}

Forms-tjänsten kan återge formulär som är baserade på fragment som du skapar med Designer. A *fragment* är en återanvändbar del av ett formulär och sparas som en separat XDP-fil som kan infogas i flera formulärdesigner. Ett fragment kan t.ex. innehålla ett adressblock eller juridisk text.

Med fragment blir det enklare och snabbare att skapa och underhålla stora mängder formulär. När du skapar ett nytt formulär infogar du en referens till det önskade fragmentet och fragmentet visas i formuläret. Fragmentreferensen innehåller ett delformulär som pekar på den fysiska XDP-filen. Mer information om hur du skapar formulärdesigner baserade på fragment finns i [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Ett fragment kan innehålla flera delformulär som är kapslade i en urvalsuppsättning med delformulär. Alternativa delformulärsuppsättningar styr visningen av delformulär baserat på dataflödet från en dataanslutning. Du använder villkorssatser för att avgöra vilket delformulär i uppsättningen som visas i det levererade formuläret. Varje delformulär i en uppsättning kan t.ex. innehålla information för en viss geografisk plats och delformuläret som visas kan bestämmas utifrån användarens plats.

A *skriptfragment* innehåller återanvändbara JavaScript-funktioner eller -värden som lagras separat från ett visst objekt, till exempel en datumparser eller ett webbtjänstanrop. Dessa fragment innehåller ett enda skriptobjekt som visas som underordnat variabler på paletten Hierarki. Fragment kan inte skapas från skript som är egenskaper för andra objekt, till exempel händelseskript som validate, calculate eller initialize.

Här är några fördelar med att använda fragment:

* **Återanvändning av innehåll**: Du kan använda fragment för att återanvända innehåll i flera formulärdesigner. När du behöver använda en del av samma innehåll i flera formulär är det snabbare och enklare att använda ett fragment än att kopiera eller återskapa innehållet. Genom att använda fragment säkerställs också att de delar av en formulärdesign som används ofta har ett konsekvent innehåll och utseende i alla referensformulär.
* **Globala uppdateringar**: Du kan använda fragment för att göra globala ändringar i flera formulär endast en gång i en fil. Du kan ändra innehåll, skriptobjekt, databindningar, layout eller format i ett fragment, och alla XDP-formulär som refererar till fragmentet återger ändringarna.
* Ett vanligt element i många formulär kan till exempel vara ett adressblock som innehåller ett nedrullningsbart listobjekt för landet. Om du behöver uppdatera värdena för listruteobjektet måste du öppna många formulär för att kunna göra ändringarna. Om du inkluderar adressblocket i ett fragment behöver du bara öppna en fragmentfil för att kunna göra ändringarna.
* Om du vill uppdatera ett fragment i ett PDF-formulär måste du spara om formuläret i Designer.
* **Skapa delade formulär**: Du kan använda fragment för att dela skapandet av formulär mellan flera resurser. Blankettutvecklare med expertis inom skript eller andra avancerade funktioner i Designer kan utveckla och dela fragment som utnyttjar skriptning och dynamiska egenskaper. Formulärdesigners kan använda dessa fragment för att utforma formulärdesigner och säkerställa att alla delar av ett formulär har ett konsekvent utseende och funktion i flera formulär som utformats av flera personer.

### Sammanställa en formulärdesign med fragment {#assembling-a-form-design-assembled-using-fragments}

Du kan sätta ihop en formulärdesign som skickas till Forms-tjänsten baserat på flera fragment. Använd Assembler-tjänsten om du vill sätta ihop flera fragment. Ett exempel på hur du använder sammansättningstjänsten för att skapa en formulärdesign som används av andra Forms-tjänster (utdatatjänsten) finns i [Skapa PDF-dokument med fragment](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). I stället för att använda Output-tjänsten kan du utföra samma arbetsflöde med Forms-tjänsten.

När du använder Assembler-tjänsten skickar du en formulärdesign som har sammanställts med fragment. Den formulärdesign som skapades refererar inte till andra fragment. I det här avsnittet behandlas däremot överföring av en formulärdesign som refererar till andra fragment till tjänsten Forms. Formulärdesignen har dock inte monterats av Assembler. Den skapades i Designer.

>[!NOTE]
>
>Mer information om tjänsten Forms finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om hur du skapar ett webbaserat program som återger formulär baserade på fragment finns i [Skapa webbprogram som återger Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

### Sammanfattning av steg {#summary-of-steps}

Så här återger du ett formulär baserat på fragment:

1. Inkludera projektfiler.
1. Skapa ett Forms Client API-objekt.
1. Ange URI-värden.
1. Återge formuläret.
1. Skriv formulärdataströmmen till klientens webbläsare.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett Forms Client API-objekt**

Innan du programmässigt kan utföra en API-åtgärd för Forms-tjänstklienten måste du skapa en Forms-tjänstklient.

**Ange URI-värden**

Om du vill återge ett formulär baserat på fragment måste du se till att Forms-tjänsten kan hitta både formuläret och de fragment (XDP-filer) som formulärdesignen refererar till. Anta till exempel att formuläret heter PO.xdp och att det här formuläret använder två fragment som heter FooterUS.xdp och FooterCanada.xdp. I så fall måste Forms-tjänsten kunna hitta alla tre XDP-filerna.

Du kan ordna ett formulär och dess fragment genom att placera formuläret på en plats och fragmenten på en annan plats. Du kan också placera alla XDP-filer på samma plats. I det här avsnittet förutsätts att alla XDP-filer finns i AEM Forms-databasen. Mer information om hur du placerar XDP-filer i AEM Forms-databasen finns i [Skriver resurser](/help/forms/developing/aem-forms-repository.md#writing-resources).

När du återger ett formulär baserat på fragment måste du bara referera till själva formuläret och inte till fragmenten. Du måste till exempel referera till PO.xdp och inte FooterUS.xdp eller FooterCanada.xdp. Se till att du placerar fragmenten på en plats där Forms-tjänsten kan hitta dem.

**Återge formuläret**

Ett formulär som är baserat på fragment kan återges på samma sätt som icke-fragmenterade formulär. Det innebär att du kan återge formuläret som PDF, HTML eller stödlinjer (borttagna). Exemplet i det här avsnittet återger ett formulär baserat på fragment som ett interaktivt PDF-formulär. (Se [Återger interaktiv PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md).)

**Skriv formulärdataströmmen till klientens webbläsare**

När Forms-tjänsten återger ett formulär returneras en formulärdataström som du måste skriva till klientens webbläsare. När formuläret skrivs till webbläsaren visas det för användaren.

**Se även**

[Återge formulär baserade på fragment med Java API](#render-forms-based-on-fragments-using-the-java-api)

[Återge formulär baserade på fragment med hjälp av webbtjänstens API](#render-forms-based-on-fragments-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Återger interaktiv PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Skapa webbprogram som återger Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Återge formulär baserade på fragment med Java API {#render-forms-based-on-fragments-using-the-java-api}

Återge ett formulär baserat på fragment med Forms API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar, i Java-projektets klassökväg.

1. Skapa ett Forms Client API-objekt

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `FormsServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Ange URI-värden

   * Skapa en `URLSpec` objekt som lagrar URI-värden med hjälp av dess konstruktor.
   * Anropa `URLSpec` objektets `setApplicationWebRoot` och skicka ett strängvärde som representerar programmets webbrot.
   * Anropa `URLSpec` objektets `setContentRootURI` och skicka ett strängvärde som anger innehållets rot-URI-värde. Kontrollera att formulärdesignen och fragmenten finns i innehållets rot-URI. Annars genereras ett undantag. Om du vill referera till databasen anger du `repository://`.
   * Anropa `URLSpec` objektets `setTargetURL` och skicka ett strängvärde som anger det mål-URL-värde som formulärdata ska skickas till. Om du definierar mål-URL:en i formulärdesignen kan du skicka en tom sträng. Du kan också ange den URL dit ett formulär skickas för att utföra beräkningar.

1. Återge formuläret

   Anropa `FormsServiceClient` objektets `renderPDFForm` och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som ingår i ett Forms-program måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du en tom `com.adobe.idp.Document` -objekt.
   * A `PDFFormRenderSpec` objekt som lagrar körningsalternativ.
   * A `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten för att återge ett formulär baserat på fragment.
   * A `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.

   The `renderPDFForm` returnerar en `FormsResult` objekt som innehåller en formulärdataström som måste skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa en `com.adobe.idp.Document` genom att anropa `FormsResult` objekt&quot;s `getOutputContent` -metod.
   * Hämta innehållstypen för `com.adobe.idp.Document` genom att anropa dess `getContentType` -metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metoden och skicka innehållstypen för `com.adobe.idp.Document` -objekt.
   * Skapa en `javax.servlet.ServletOutputStream` som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` -metod.
   * Skapa en `java.io.InputStream` genom att anropa `com.adobe.idp.Document` objektets `getInputStream` -metod.
   * Skapa en bytearray som fyller i den med formulärdataströmmen genom att anropa `InputStream` objektets `read`och skicka bytearrayen som ett argument.
   * Anropa `javax.servlet.ServletOutputStream` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` -metod.

**Se även**

[Återge Forms baserat på fragment](#rendering-forms-based-on-fragments)

[Snabbstart (SOAP-läge): Återge ett formulär baserat på fragment med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Återge formulär baserade på fragment med hjälp av webbtjänstens API {#render-forms-based-on-fragments-using-the-web-service-api}

Återge ett formulär baserat på fragment med Forms API (webbtjänst):

1. Inkludera projektfiler

   * Skapa Java-proxyklasser som använder Forms tjänst-WSDL.
   * Inkludera Java-proxyklasserna i klassökvägen.

1. Skapa ett Forms Client API-objekt

   Skapa en `FormsService` och ange autentiseringsvärden.

1. Ange URI-värden

   * Skapa en `URLSpec` objekt som lagrar URI-värden med hjälp av dess konstruktor.
   * Anropa `URLSpec` objektets `setApplicationWebRoot` och skicka ett strängvärde som representerar programmets webbrot.
   * Anropa `URLSpec` objektets `setContentRootURI` och skicka ett strängvärde som anger innehållets rot-URI-värde. Kontrollera att formulärdesignen finns i innehållets rot-URI. Annars genereras ett undantag. Om du vill referera till databasen anger du `repository://`.
   * Anropa `URLSpec` objektets `setTargetURL` och skicka ett strängvärde som anger det mål-URL-värde som formulärdata ska skickas till. Om du definierar mål-URL:en i formulärdesignen kan du skicka en tom sträng. Du kan också ange den URL dit ett formulär skickas för att utföra beräkningar.

1. Återge formuläret

   Anropa `FormsService` objektets `renderPDFForm` och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som ingår i ett Forms-program måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du `null`.
   * A `PDFFormRenderSpec` objekt som lagrar körningsalternativ. Observera att alternativet PDF med märkord inte kan anges om indatadokumentet är ett PDF-dokument. Om indatafilen är en XDP-fil kan du ange alternativet PDF med märkord.
   * A `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten.
   * A `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.
   * En tom `com.adobe.idp.services.holders.BLOBHolder` objekt som fylls i av metoden. Den här parametern används för att lagra det återgivna formuläret.
   * En tom `javax.xml.rpc.holders.LongHolder` objekt som fylls i av metoden. Det här argumentet lagrar antalet sidor i formuläret.
   * En tom `javax.xml.rpc.holders.StringHolder` objekt som fylls i av metoden. Det här argumentet lagrar språkets värde.
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

[Återge Forms baserat på fragment](#rendering-forms-based-on-fragments)

[Anropa AEM Forms med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
