---
title: Återger Forms som HTML
seo-title: Rendering Forms as HTML
description: Använd tjänsten Forms för att återge formulär som HTML som svar på en HTTP-begäran från en webbläsare. Du kan använda Java API och Web Service API för att återge formulär som HTML.
seo-description: Use the Forms service to render forms as HTML in response to an HTTP request from a web browser. You can use the Java API and Web Service API to render forms as HTML.
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
role: Developer
exl-id: e6887e45-a472-41d4-9620-c56fd5b72b4c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4150'
ht-degree: 1%

---

# Återger Forms som HTML {#rendering-forms-as-html}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

Forms-tjänsten återger formulär som HTML som svar på en HTTP-begäran från en webbläsare. En fördel med att återge ett formulär som HTML är att den dator där klientwebbläsaren finns inte kräver Adobe Reader, Acrobat eller Flash Player (för formulärguider (borttagen)).

Om du vill återge ett formulär som HTML måste formulärdesignen sparas som en XDP-fil. En formulärdesign som sparas som en PDF-fil kan inte återges som HTML. När du utvecklar en formulärdesign i Designer som ska återges som HTML bör du tänka på följande kriterier:

* Använd inte ett objekts kantegenskaper till att rita linjer, rutor eller rutnät i formuläret. Alla webbläsare kan inte återge kanter på samma sätt som de visas i förhandsgranskningen i Det kan se ut som om objekt ligger ovanpå varandra, och vissa objekt kan även förskjuta andra objekt från deras lägen.
* Du kan använda linjer, rektanglar och cirklar för att definiera bakgrunden.
* Rita text något större än vad som krävs för att texten ska få plats. I vissa webbläsare visas inte texten läsbart.

>[!NOTE]
>
>När du återger ett formulär som innehåller TIFF-bilder med `FormServiceClient` objektets `(Deprecated) renderHTMLForm` och `renderHTMLForm2` -metoder är TIFF-bilderna inte synliga i det återgivna HTML-formuläret som visas i Internet Explorer- eller Mozilla Firefox-webbläsare. De här webbläsarna har inte inbyggt stöd för bilder i TIFF.

## HTML sidor {#html-pages}

När en formulärdesign återges som ett HTML-formulär återges varje delformulär på andra nivån som en HTML-sida (panel). Du kan visa ett delformulärs hierarki i Designer. Underordnade delformulär som tillhör rotdelformuläret (standardnamnet för ett rotdelformulär är formulär1) är paneldelformulär. I följande exempel visas delformulären för en formulärdesign.

```java
     form1
         Master Pages
         PanelSubform1
             NestedDynamicSubform
                 TextEdit1
         PanelSubform2
             TextEdit1
         PanelSubform3
             TextEdit1
         PanelSubform4
             TextEdit1
```

När formulärdesigner återges som HTML-formulär begränsas inte panelerna till någon viss sidstorlek. Om du har dynamiska delformulär bör de vara kapslade i paneldelformuläret. Dynamiska delformulär kan expandera till ett obegränsat antal HTML-sidor.

När ett formulär återges som ett HTML-formulär har sidstorlekar (som krävs för att numrera formulär som återges som PDF) ingen betydelse. Eftersom ett formulär med flödeslayout kan utvidgas till ett obegränsat antal HTML-sidor är det viktigt att undvika sidfötter på den överordnad sidan. En sidfot under innehållsområdet på en överordnad sida kan skriva över HTML-innehåll som flödar förbi en sidgräns.

Du måste gå från panel till panel med `xfa.host.pageUp` och `xfa.host.pageDown` metoder. Du ändrar sidor genom att skicka ett formulär till Forms och låta Forms-tjänsten återge formuläret till klientenheten, vanligtvis en webbläsare.

>[!NOTE]
>
>Processen med att skicka ett formulär till Forms-tjänsten och sedan låta Forms-tjänsten återge formuläret till klientenheten kallas för att skicka runt data till servern.

>[!NOTE]
>
>Om du vill anpassa utseendet på knappen för digital signatur i HTML måste du ändra följande egenskaper i filen fscdigsig.css (i filen adobe-forms-ds.ear > adobe-forms-ds.war):

**.fsc-ds-ssb**: Den här formatmallen används för tomma teckenfält.

**.fsc-ds-ssv**: Den här formatmallen kan användas för fält med giltiga tecken.

**.fsc-ds-ssc**: Den här formatmallen används för ett giltigt signeringsfält, men data har ändrats.

**.fsc-ds-ssi**: Den här formatmallen kan användas för ogiltiga signaturfält.

**.fsc-ds-popup-bg**: Den här formatmallsegenskapen används inte.

**.fsc-ds-popup-btn**: Den här formatmallsegenskapen används inte.

## Köra skript {#running-scripts}

En formulärförfattare anger om ett skript ska köras på servern eller klienten. Forms-tjänsten skapar en distribuerad händelsebearbetningsmiljö för att köra blankettintelligens som kan distribueras mellan klienten och servern med hjälp av `runAt` -attribut. Mer information om det här attributet och hur du skapar skript i formulärdesigner finns i [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Forms-tjänsten kan köra skript medan formuläret återges. Det innebär att du kan förifylla ett formulär med data genom att ansluta till en databas eller till webbtjänster som kanske inte är tillgängliga på klienten. Du kan också ange en knapps `Click` händelse som ska köras på servern så att klienten skickar data till servern. Detta gör att klienten kan köra skript som kan kräva serverresurser, t.ex. en företagsdatabas, medan en användare interagerar med ett formulär. För HTML-formulär kan formulärskript endast köras på servern. Därför måste du markera dessa skript som ska köras på `server` eller `both`.

Du kan utforma formulär som rör sig mellan sidor (paneler) genom att anropa `xfa.host.pageUp` och `xfa.host.pageDown` metoder. Skriptet placeras i en knapps `Click` -händelsen och `runAt` attribute is set to `Both`. Orsaken du väljer `Both` så att Adobe Reader eller Acrobat (för formulär som återges som PDF) kan ändra sidor utan att gå till servern, och HTML kan ändra sidor genom att skicka data till servern. Det innebär att ett formulär skickas till Forms och att ett formulär återges som HTML när den nya sidan visas.

Vi rekommenderar att du inte ger skriptvariabler och formulärfält samma namn, till exempel objekt. I vissa webbläsare, t.ex. Internet Explorer, går det inte att initiera en variabel med samma namn som ett formulärfält, vilket resulterar i ett skriptfel. Det är god praxis att ge formulärfält och skriptvariabler olika namn.

När du återger HTML-formulär som innehåller både sidnavigeringsfunktioner och formulärskript (t.ex. antar att ett skript hämtar fältdata från en databas varje gång formuläret återges), kontrollerar du att formulärskriptet finns i händelsen form:calculate i stället för i formatet:readyevent.

Formulärskript som finns i formen:ready-händelsen körs bara en gång under den inledande återgivningen av formuläret och körs inte för efterföljande sidhämtningar. Händelsen form:calculate körs däremot för varje sidnavigering där formuläret återges.

>[!NOTE]
På ett flersidigt formulär behålls inte ändringar som JavaScript gjort på en sida om du flyttar till en annan sida.

Du kan anropa egna skript innan du skickar in ett formulär. Den här funktionen fungerar i alla tillgängliga webbläsare. Den kan dock bara användas när användare återger det HTML-formulär som har dess `Output Type` egenskap inställd på `Form Body`. Det fungerar inte när `Output Type` är `Full HTML`. Mer information om hur du konfigurerar den här funktionen finns i Konfigurera formulär i administrationshjälpen.

Du måste definiera en callback-funktion som anropas innan formuläret skickas, där funktionens namn är `_user_onsubmit`. Det antas att funktionen inte genererar något undantag, eller att undantaget ignoreras om det gör det. Vi rekommenderar att du placerar JavaScript-funktionen i huvudet i html. Du kan emellertid deklarera det var som helst före slutet av de skripttaggar som innehåller `xfasubset.js`.

När formserver återger en XDP-fil som innehåller en nedrullningsbar lista skapas även två dolda textfält förutom att listrutan skapas. Dessa textfält lagrar data i den nedrullningsbara listan (ett lagrar alternativens visningsnamn och andra lagrar alternativens värden). Därför skickas alla data i den nedrullningsbara listan varje gång en användare skickar formuläret. Om du inte vill skicka så mycket data varje gång kan du skriva ett eget skript som inaktiverar det. Till exempel: Listrutan heter `drpOrderedByStateProv` och är omsluten under delformulärsrubriken. HTML-indataelementets namn blir `header[0].drpOrderedByStateProv[0]`. Namnet på de dolda fält som lagrar och skickar data i listrutan har följande namn: `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

Du kan inaktivera dessa indataelement på följande sätt om du inte vill publicera data. `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```java
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```java
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature
    function _user_onsubmit() {
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]");
    elems[0].disabled = true;
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]");
    elems[0].disabled = true;
    }
```

## XFA-delmängder {#xfa-subsets}

När du skapar formulärdesigner som ska återges som HTML måste du begränsa skripten till XFA-delmängden för skript i JavaScript-språket.

Skript som körs på klienten eller körs både på klienten och servern måste skrivas i XFA-delmängden. Skript som körs på servern kan använda den fullständiga XFA-skriptmodellen och även FormCalc. Mer information om hur du använder JavaScript finns i [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

När skript körs på klienten kan bara den aktuella panelen som visas använda skript. Du kan till exempel inte skriva skript mot fält som finns i panel A när panel B visas. När du kör skript på servern är alla paneler tillgängliga.

Du måste också vara försiktig när du använder SOM-uttryck (Scripting Object Model) i skript som körs på klienten. Endast en förenklad delmängd av SOM-uttryck stöds av skript som körs på klienten.

## Händelsetiming {#event-timing}

XFA-delmängden definierar XFA-händelser som mappas till HTML-händelser. Det finns en liten skillnad i beteendet när det gäller tidpunkten för beräkning och validering av händelser. I en webbläsare körs en fullständig calculate-händelse när du avslutar ett fält. Beräkningshändelser körs inte automatiskt när du ändrar ett fältvärde. Du kan tvinga fram en calculate-händelse genom att anropa `xfa.form.execCalculate` -metod.

I en webbläsare körs valideringshändelser bara när ett fält avslutas eller när ett formulär skickas. Du kan tvinga fram en validate-händelse med `xfa.form.execValidate` -metod.

Forms som visas i en webbläsare (till skillnad från Adobe Reader eller Acrobat) följer XFA null-testet (fel eller varningar) för obligatoriska fält.

* Om null-testet genererar ett fel och du avslutar ett fält utan att ange ett värde, visas en meddelanderuta och du flyttas till fältet efter att du klickat på OK.
* Om ett null-test ger en varning och du avslutar ett fält utan att ange ett värde, uppmanas du att klicka på OK eller Avbryt, så att du kan fortsätta utan att ange ett värde eller gå tillbaka till fältet för att ange ett värde.

Mer information om ett null-test finns i [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Formulärknappar {#form-buttons}

När du klickar på en skicka-knapp skickas formulärdata till Forms-tjänsten och det här är slutet på formulärbearbetningen. The `preSubmit` -händelsen kan ställas in för att köras på klienten eller servern. The `preSubmit` -händelsen körs före formuläröverföringen om den är konfigurerad att köras på klienten. I annat fall visas `preSubmit` -händelsen körs på servern när formuläret skickas. Mer information om `preSubmit` händelse, se [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Om en knapp inte har något klientskript kopplat till sig, skickas data till servern, beräkningar utförs på servern och HTML-formuläret genereras om. Om en knapp innehåller ett klientskript skickas inga data till servern och klientskriptet körs i webbläsaren.

## HTML 4.0 {#html-4-0-web-browser}

En webbläsare som bara har stöd för HTML 4.0 kan inte hantera XFA-deluppsättningens klientskriptmodell. När du skapar en formulärdesign som ska fungera i både HTML 4.0 och MSDHTML eller CSS2HTML kommer ett skript som är markerat för att köras på klienten att köras på servern. Anta till exempel att en användare klickar på en knapp som finns i ett formulär som visas i webbläsaren HTML 4.0. I sådana fall skickas formulärdata till servern där skriptet på klientsidan körs.

Du bör placera formulärlogiken i calculate-händelser som körs på servern i HTML 4.0 och på klienten för MSDHTML eller CSS2HTML.

## Underhåll presentationsändringar {#maintaining-presentation-changes}

När du förflyttar dig mellan HTML-sidor (paneler) behålls endast datastatus. Inställningar som bakgrundsfärg eller obligatoriska fältinställningar bevaras inte (om de skiljer sig från de ursprungliga inställningarna). Om du vill behålla presentationstillståndet måste du skapa fält (vanligen dolda) som representerar presentationstillståndet för fält. Om du lägger till ett skript i ett fälts `Calculate` om du ändrar presentationen baserat på dolda fältvärden, kan du bevara presentationstillståndet när du går fram och tillbaka mellan HTML-sidor (paneler).

Följande skript bevarar `fillColor` för ett fält baserat på värdet för `hiddenField`. Anta att det här skriptet finns i ett fälts `Calculate` -händelse.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
Statiska objekt visas inte i ett återgivet HTML-formulär när de är kapslade i en tabellcell. En cirkel och rektangel som är kapslad i en tabellcell visas till exempel inte i ett återgivningsformulär i HTML. Samma statiska objekt visas emellertid korrekt utanför tabellen.

## Signera HTML-formulär digitalt {#digitally-signing-html-forms}

Du kan inte signera ett HTML-formulär som innehåller ett fält för elektronisk underskrift om formuläret återges som en av följande HTML-omformningar:

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

Information om hur du signerar ett dokument digitalt finns i [Digitalt signera och certifiera dokument](/help/forms/developing/digitally-signing-certifying-documents.md)

## Rendera ett hjälpmedelsanpassat XHTML-formulär {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

Du kan återge ett fullständigt HTML-formulär som är kompatibelt med riktlinjerna för hjälpmedel. Det innebär att formuläret återges med fullständiga HTML-taggar i motsats till HTML som återges med body-taggar (inte en fullständig HTML-sida).

## Validerar formulärdata {#validating-form-data}

Vi rekommenderar att du begränsar användningen av valideringsregler för formulärfält när du återger formuläret som ett HTML-formulär. Vissa valideringsregler kanske inte stöds för HTML-formulär. När valideringsmönstret MM-DD-YYY används på en `Date/Time` fält som finns i en formulärdesign som återges som ett HTML-formulär fungerar inte korrekt, även om datumet är korrekt angivet. Det här valideringsmönstret fungerar emellertid korrekt för formulär som återges som PDF.

>[!NOTE]
Mer information om tjänsten Forms finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Sammanfattning av steg {#summary-of-steps}

Så här återger du ett HTML-formulär:

1. Inkludera projektfiler.
1. Skapa ett Forms Client API-objekt.
1. Ange körningsalternativ för HTML.
1. Återge ett HTML-formulär.
1. Skriv formulärdataströmmen till klientens webbläsare.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett Forms Client API-objekt**

Innan du programmässigt kan importera data till ett PDF formClient-API måste du skapa en tjänstklient för integrering av formulärdata. När du skapar en tjänstklient definierar du de anslutningsinställningar som krävs för att anropa en tjänst.

**Ange körningsalternativ för HTML**

Du anger körningsalternativ för HTML när du återger ett HTML-formulär. Du kan till exempel lägga till ett verktygsfält i ett HTML-formulär så att användare kan välja bifogade filer på klientdatorn eller hämta bifogade filer som återges med formuläret HTML. Som standard är verktygsfältet HTML inaktiverat. Om du vill lägga till ett verktygsfält i ett HTML-formulär måste du programmässigt ange körningsalternativ. Som standard består verktygsfältet HTML av följande knappar:

* `Home`: Tillhandahåller en länk till programmets webbrot.
* `Upload`: Innehåller ett användargränssnitt för att välja filer som ska bifogas det aktuella formuläret.
* `Download`: Innehåller ett användargränssnitt för att visa de bifogade filerna.

När ett verktygsfält i HTML visas i ett HTML-formulär kan användaren välja högst tio filer att skicka tillsammans med formulärdata. När filerna har skickats kan Forms-tjänsten hämta filerna.

När du återger ett formulär som HTML kan du ange ett användaragentvärde. Ett användaragentvärde ger information om webbläsare och system. Detta är ett valfritt värde och du kan skicka ett tomt strängvärde. När du återger ett HTML-formulär med Java API-snabbstarten visas hur du får ett användaragentvärde och använder det för att återge ett formulär som HTML.

HTTP-URL:er dit formulärdata skickas kan anges genom att ange mål-URL:en med hjälp av Forms Service Client-API:t eller anges i knappen Skicka i XDP-formulärdesignen. Om mål-URL:en anges i formulärdesignen ska du inte ange något värde med Forms Service Client API.

>[!NOTE]
Det är valfritt att återge ett HTML-formulär med ett verktygsfält.

>[!NOTE]
Om du återger ett AHTML-formulär bör du inte lägga till ett verktygsfält i formuläret.

**Återge ett HTML-formulär**

Om du vill återge ett HTML-formulär måste du ange en formulärdesign som har skapats i Designer och sparats som en XDP-fil. Du måste också välja en omformningstyp för HTML. Du kan till exempel ange HTML-omformningstypen som återger ett dynamiskt HTML för Internet Explorer 5.0 eller senare.

Återgivning av ett HTML-formulär kräver också värden, t.ex. URI-värden som krävs för att återge andra formulärtyper.

**Skriv formulärdataströmmen till klientens webbläsare**

När Forms-tjänsten återger ett HTML-formulär returneras en formulärdataström som du måste skriva till klientens webbläsare. När formuläret HTML skrivs till webbläsaren visas det för användaren.

**Se även**

[Återge ett formulär som HTML med Java API](#render-a-form-as-html-using-the-java-api)

[Återge ett formulär som HTML med hjälp av webbtjänstens API](#render-a-form-as-html-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Återger interaktiv PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Återge HTML Forms med anpassade verktygsfält](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Skapa webbprogram som återger Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Återge ett formulär som HTML med Java API {#render-a-form-as-html-using-the-java-api}

Återge ett HTML-formulär med Forms API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar, i Java-projektets klassökväg.

1. Skapa ett Forms Client API-objekt

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `FormsServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Ange körningsalternativ för HTML

   * Skapa en `HTMLRenderSpec` genom att använda dess konstruktor.
   * Om du vill återge ett HTML-formulär med ett verktygsfält anropar du `HTMLRenderSpec` objektets `setHTMLToolbar` metod och skicka en `HTMLToolbar` enum-värde. Om du till exempel vill visa ett lodrätt HTML-verktygsfält skickar du `HTMLToolbar.Vertical`.
   * Om du vill ange språkvärdet för formuläret HTML anropar du `HTMLRenderSpec` objektets `setLocale` och skicka ett strängvärde som anger språkvärdet. (Det här är en valfri inställning.)
   * Om du vill återge formuläret HTML i fullständiga HTML-taggar anropar du `HTMLRenderSpec` objektets `setOutputType` metod och skicka `OutputType.FullHTMLTags`. (Det här är en valfri inställning.)

   >[!NOTE]
   Forms återges inte korrekt i HTML när `StandAlone` option is `true` och `ApplicationWebRoot` refererar till en annan server än J2EE-programservern som är värd för AEM Forms ( `ApplicationWebRoot` värdet anges med `URLSpec` objekt som skickas till `FormsServiceClient` objektets `(Deprecated) renderHTMLForm` metod). När `ApplicationWebRoot` är en annan server från den som är värd för AEM Forms, måste värdet för webb-URI:n i administrationskonsolen anges som formulärets webbprogram-URI-värde. Detta kan du göra genom att logga in på administrationskonsolen, klicka på Tjänster > Forms och ange webbrots-URI som https://server-name:port/FormServer. Spara sedan inställningarna.

1. Återge ett HTML-formulär

   Anropa `FormsServiceClient` objektets `(Deprecated) renderHTMLForm` och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som ingår i ett Forms-program måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` uppräkningsvärde som anger inställningstypen HTML. Om du till exempel vill återge ett HTML-formulär som är kompatibelt med dynamiskt HTML för Internet Explorer 5.0 eller senare anger du `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du en tom `com.adobe.idp.Document` -objekt.
   * The `HTMLRenderSpec` objekt som lagrar körningsalternativ för HTML.
   * Ett strängvärde som anger `HTTP_USER_AGENT` rubrikvärde; till exempel `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` objekt som lagrar de URI-värden som krävs för att återge ett HTML-formulär.
   * A `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.

   The `(Deprecated) renderHTMLForm` returnerar en `FormsResult` objekt som innehåller en formulärdataström som kan skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa en `com.adobe.idp.Document` genom att anropa `FormsResult` objekt&quot;s `getOutputContent` -metod.
   * Hämta innehållstypen för `com.adobe.idp.Document` genom att anropa dess `getContentType` -metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metoden och skicka innehållstypen för `com.adobe.idp.Document` -objekt.
   * Skapa en `javax.servlet.ServletOutputStream` som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` -metod.
   * Skapa en `java.io.InputStream` genom att anropa `com.adobe.idp.Document` objektets `getInputStream` -metod.
   * Skapa en bytearray och fylla den med formulärdataströmmen genom att anropa `InputStream` objektets `read` och skicka bytearrayen som ett argument.
   * Anropa `javax.servlet.ServletOutputStream` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` -metod.

**Se även**

[Återger Forms som HTML](#rendering-forms-as-html)

[Snabbstart (SOAP-läge): Återge ett HTML-formulär med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Återge ett formulär som HTML med hjälp av webbtjänstens API {#render-a-form-as-html-using-the-web-service-api}

Återge ett HTML-formulär med Forms API (webbtjänst):

1. Inkludera projektfiler

   * Skapa Java-proxyklasser som använder Forms tjänst-WSDL.
   * Inkludera Java-proxyklasserna i klassökvägen.

1. Skapa ett Forms Client API-objekt

   Skapa en `FormsService` och ange autentiseringsvärden.

1. Ange körningsalternativ för HTML

   * Skapa en `HTMLRenderSpec` genom att använda dess konstruktor.
   * Om du vill återge ett HTML-formulär med ett verktygsfält anropar du `HTMLRenderSpec` objektets `setHTMLToolbar` metod och skicka en `HTMLToolbar` enum-värde. Om du till exempel vill visa ett lodrätt HTML-verktygsfält skickar du `HTMLToolbar.Vertical`.
   * Om du vill ange språkvärdet för formuläret HTML anropar du `HTMLRenderSpec` objektets `setLocale` och skicka ett strängvärde som anger språkvärdet. Mer information finns i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Om du vill återge formuläret HTML i fullständiga HTML-taggar anropar du `HTMLRenderSpec` objektets `setOutputType` metod och skicka `OutputType.FullHTMLTags`.

   >[!NOTE]
   Forms återges inte korrekt i HTML när `StandAlone` option is `true` och `ApplicationWebRoot` refererar till en annan server än J2EE-programservern som är värd för AEM Forms ( `ApplicationWebRoot` värdet anges med `URLSpec` objekt som skickas till `FormsServiceClient` objektets `(Deprecated) renderHTMLForm` metod). När `ApplicationWebRoot` är en annan server från den som är värd för AEM Forms, måste värdet för webb-URI:n i administrationskonsolen anges som formulärets webbprogram-URI-värde. Detta kan du göra genom att logga in på administrationskonsolen, klicka på Tjänster > Forms och ange webbrots-URI som https://server-name:port/FormServer. Spara sedan inställningarna.

1. Återge ett HTML-formulär

   Anropa `FormsService` objektets `(Deprecated) renderHTMLForm` och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som ingår i ett Forms-program måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` uppräkningsvärde som anger inställningstypen HTML. Om du till exempel vill återge ett HTML-formulär som är kompatibelt med dynamiskt HTML för Internet Explorer 5.0 eller senare anger du `TransformTo.MSDHTML`.
   * A `BLOB` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du `null`. (Se [Förifyll Forms med flödeslayouter](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts).)
   * The `HTMLRenderSpec` objekt som lagrar körningsalternativ för HTML.
   * Ett strängvärde som anger `HTTP_USER_AGENT` rubrikvärde; till exempel `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Du kan skicka en tom sträng om du inte vill ange det här värdet.
   * A `URLSpec` objekt som lagrar de URI-värden som krävs för att återge ett HTML-formulär. (Se [Ange URI-värden](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * A `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret. (Se [Bifoga filer i formuläret](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * En tom `com.adobe.idp.services.holders.BLOBHolder` objekt som fylls i av metoden. Det här parametervärdet lagrar det återgivna formuläret.
   * En tom `com.adobe.idp.services.holders.BLOBHolder` objekt som fylls i av metoden. Den här parametern lagrar XML-utdata.
   * En tom `javax.xml.rpc.holders.LongHolder` objekt som fylls i av metoden. Det här argumentet lagrar antalet sidor i formuläret.
   * En tom `javax.xml.rpc.holders.StringHolder` objekt som fylls i av metoden. Det här argumentet lagrar språkets värde.
   * En tom `javax.xml.rpc.holders.StringHolder` objekt som fylls i av metoden. Det här argumentet lagrar återgivningsvärdet som används för HTML.
   * En tom `com.adobe.idp.services.holders.FormsResultHolder` objekt som innehåller resultatet av den här åtgärden.

   The `(Deprecated) renderHTMLForm` metoden fyller i `com.adobe.idp.services.holders.FormsResultHolder` objekt som skickas som det sista argumentvärdet med en formulärdataström som måste skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa en `FormResult` genom att hämta värdet för `com.adobe.idp.services.holders.FormsResultHolder` objektets `value` datamedlem.
   * Skapa en `BLOB` objekt som innehåller formulärdata genom att anropa `FormsResult` objektets `getOutputContent` -metod.
   * Hämta innehållstypen för `BLOB` genom att anropa dess `getContentType` -metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metoden och skicka innehållstypen för `BLOB` -objekt.
   * Skapa en `javax.servlet.ServletOutputStream` som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` -metod.
   * Skapa en bytearray och fylla i den genom att anropa `BLOB` objektets `getBinaryData` -metod. Den här aktiviteten tilldelar innehållet i `FormsResult` till bytearrayen.
   * Anropa `javax.servlet.http.HttpServletResponse` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` -metod.

**Se även**

[Återger Forms som HTML](#rendering-forms-as-html)

[Anropa AEM Forms med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
