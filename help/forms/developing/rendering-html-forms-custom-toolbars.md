---
title: Återge HTML-formulär med anpassade verktygsfält
seo-title: Återge HTML-formulär med anpassade verktygsfält
description: 'null'
seo-description: 'null'
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Återge HTML-formulär med anpassade verktygsfält {#rendering-html-forms-with-customtoolbars}

## Återge HTML-formulär med anpassade verktygsfält {#rendering-html-forms-with-custom-toolbars}

Med Forms-tjänsten kan du anpassa ett verktygsfält som återges med ett HTML-formulär. Ett verktygsfält kan anpassas för att ändra utseendet genom att åsidosätta CSS-standardformat och lägga till dynamiskt beteende genom att åsidosätta Java-skript. Ett verktygsfält anpassas med hjälp av en XML-fil med namnet fscmenu.xml. Som standard hämtar Forms-tjänsten den här filen från en internt angiven URI-plats.

>[!NOTE]
>
>Denna URI-plats finns i filen adobe-forms-core.jar som finns i filen adobe-forms-dsc.jar. Filen adobe-forms-dsc.jar finns i C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory). Du kan använda ett filextraheringsverktyg, till exempel Win RAR, för att öppna Adobe-filen.

Du kan kopiera fscmenu.xml från den här platsen, ändra den så att den uppfyller dina krav och sedan placera den på en anpassad URI-plats. Sedan anger du med API:t för Forms Service att körningsalternativen som resulterar i att Forms-tjänsten använder filen fscmenu.xml från den angivna platsen. Dessa åtgärder resulterar i att Forms-tjänsten återger ett HTML-formulär som har ett anpassat verktygsfält.

Förutom filen fscmenu.xml behöver du även följande filer:

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS är det Java-skript som associeras med varje nod. Det är nödvändigt att ange en för `div#fscmenu` noden och eventuellt för `ul#fscmenuItem` noder. JS-filerna implementerar grundläggande verktygsfältsfunktioner och standardfilerna fungerar.

fscCSS är en formatmall som är kopplad till en viss nod. Formaten i CSS-filerna anger verktygsfältets utseende. *fscVCSS* är en formatmall för ett lodrätt verktygsfält som visas till vänster om det återgivna HTML-formuläret. *fscIECSS* är en formatmall som används för HTML-formulär som återges i Internet Explorer.

Kontrollera att det finns referenser till alla ovanstående filer i filen fscmenu.xml. Det vill säga, i filen fscmenu.xml anger du URI-platser som pekar på dessa filer så att Forms-tjänsten kan hitta dem. Som standard är de här filerna tillgängliga på URI-platser som börjar med interna nyckelord `FSWebRoot` eller `ApplicationWebRoot`.

Om du vill anpassa verktygsfältet ersätter du nyckelorden med hjälp av det externa nyckelordet `FSToolBarURI`. Nyckelordet representerar den URI som skickas till Forms-tjänsten vid körning (den här metoden visas senare i det här avsnittet).

Du kan också ange de absoluta platserna för dessa JS- och CSS-filer, till exempel https://www.mycompany.com/scripts/misc/fscmenu.js. I så fall behöver du inte använda nyckelordet `FSToolBarURI` .

>[!NOTE]
>
>Vi rekommenderar inte att du blandar de sätt på vilka dessa filer refereras. Det innebär att alla URI:er ska refereras med antingen nyckelordet `FSToolBarURI` eller en absolut plats.

Du kan hämta JS- och CSS-filerna genom att öppna filen adobe-forms-&lt;appserver>.ear. I den här filen öppnar du adobe-forms-res.war. Alla dessa filer finns i WAR-filen. Filen adobe-forms-&lt;appserver>.ear finns i installationsmappen för AEM-formulär (C:\ is the installation directory). Du kan öppna adobe-forms-&lt;appserver>.ear med ett filextraheringsverktyg som WinRAR.

I följande XML-syntax visas ett exempel på filen fscmenu.xml.

```as3
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Home</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Upload Attachments</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Add ...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Delete ...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Download Attachments</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">None available</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>Den fetstilta texten representerar URI:er för CSS- och JS-filer som måste refereras.

Följande objekt beskriver hur du kan anpassa ett verktygsfält:

* Ändra värdena för `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` attributen (i filen fscmenu.xml) så att de återspeglar de anpassade placeringarna för de refererade filerna genom att använda någon av de metoder som beskrivs i det här avsnittet (till exempel `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Alla CSS- och JS-filer måste anges. Om ingen av filerna ändras anger du standardfilen på den anpassade platsen. Du kan hämta standardfilerna genom att öppna olika filer enligt beskrivningen i det här avsnittet.
* Det är tillåtet att ange en absolut referens (till exempel https://www.example.com/scripts/custom-vertical-fscmenu.css) för alla filer.
* De JS- och CSS-filer som krävs för `div#fscmenu` noden är viktiga för verktygsfältets funktion. Enskilda `ul#fscmenuItem` noder kan ha stöd för JS- eller CSS-filer.

**Ändra det lokala värdet**

När du anpassar ett verktygsfält kan du ändra det nationella värdet för verktygsfältet. Det innebär att du kan visa det på ett annat språk. I följande bild visas ett anpassat verktygsfält på franska.

>[!NOTE]
>
>Det går inte att skapa ett anpassat verktygsfält på mer än ett språk. Verktygsfält kan inte använda olika XML-filer baserade på språkinställningarna.

Om du vill ändra språkvärdet för ett verktygsfält kontrollerar du att filen fscmenu.xml innehåller det språk som du vill visa. Följande XML-syntax visar filen fscmenu.xml som används för att visa ett franskt verktygsfält.

```as3
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Accueil</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Ajouter...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Supprimer...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">Aucune disponible</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>I snabbstarter som är kopplade till det här avsnittet används den här XML-filen för att visa ett anpassat verktygsfält i franska, vilket visades i föregående bild.

Ange också ett giltigt språkvärde genom att anropa `HTMLRenderSpec` objektets `setLocale` metod och skicka ett strängvärde som anger språkvärdet. Skicka `fr_FR` till exempel för att ange franska. Forms-tjänsten levereras med lokaliserade verktygsfält.

>[!NOTE]
>
>Innan du återger ett HTML-formulär som använder ett anpassat verktygsfält måste du veta hur HTML-formulär återges. (Se [Återge formulär som HTML](/help/forms/developing/rendering-forms-html.md).)

Mer information om Forms-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Så här återger du ett HTML-formulär som innehåller ett anpassat verktygsfält:

1. Inkludera projektfiler.
1. Skapa ett Forms Java API-objekt.
1. Referera till en anpassad fscmenu XML-fil.
1. Återge ett HTML-formulär.
1. Skriv formulärdataströmmen till klientens webbläsare.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

**Skapa ett Forms Java API-objekt**

Innan du programmässigt kan utföra en åtgärd som stöds av Forms-tjänsten måste du skapa ett Forms-klientobjekt.

**Referera en anpassad fscmenu XML-fil**

Om du vill återge ett HTML-formulär som innehåller ett anpassat verktygsfält hänvisar du till en fscmenu XML-fil som beskriver verktygsfältet. (I det här avsnittet finns två exempel på en XML-fil för fscmenu.) Se även till att fscmenu.xml-filen anger platserna för alla refererade filer korrekt. Se till att alla filer refereras till antingen av nyckelordet eller av deras absoluta platser, som du nämnde tidigare i det här avsnittet `FSToolBarURI` .

**Återge ett HTML-formulär**

Om du vill återge ett HTML-formulär anger du en formulärdesign som har skapats i Designer och sparats som en XDP-fil. Välj även en HTML-omformningstyp. Du kan till exempel ange HTML-omformningstypen som återger en dynamisk HTML för Internet Explorer 5.0 eller senare.

Återgivning av ett HTML-formulär kräver också värden, t.ex. URI-värden för återgivning av andra formulärtyper.

**Skriv formulärdataströmmen till klientens webbläsare**

När Forms-tjänsten återger ett HTML-formulär returneras ett formulärdataflöde som du måste skriva till klientens webbläsare för att göra HTML-formuläret synligt för användarna.

**Se även**

[Återge ett HTML-formulär med ett anpassat verktygsfält med Java API](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Återge ett HTML-formulär med ett anpassat verktygsfält med hjälp av webbtjänstens API](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Återgivning av interaktiva PDF-formulär](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Återger formulär som HTML](/help/forms/developing/rendering-forms-html.md)

[Skapa webbprogram som återger formulär](/help/forms/developing/creating-web-applications-renders-forms.md)

### Återge ett HTML-formulär med ett anpassat verktygsfält med Java API {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Återge ett HTML-formulär som innehåller ett anpassat verktygsfält med hjälp av Forms Service API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar, i Java-projektets klassökväg.

1. Skapa ett Forms Java API-objekt

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa ett `FormsServiceClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.

1. Referera en anpassad fscmenu XML-fil

   * Skapa ett `HTMLRenderSpec` objekt med hjälp av dess konstruktor.
   * Om du vill återge ett HTML-formulär med ett verktygsfält anropar du `HTMLRenderSpec` objektets `setHTMLToolbar` metod och skickar ett `HTMLToolbar` uppräkningsvärde. Om du till exempel vill visa ett lodrätt HTML-verktygsfält skickar du `HTMLToolbar.Vertical`.
   * Ange platsen för fscmenu XML-filen genom att anropa `HTMLRenderSpec` objektets `setToolbarURI` metod och skicka ett strängvärde som anger URI-platsen för XML-filen.
   * Om det är tillämpligt anger du språkvärdet genom att anropa `HTMLRenderSpec` objektets `setLocale` -metod och skicka ett strängvärde som anger språkvärdet. Standardvärdet är engelska.
   >[!NOTE]
   >
   >Snabbstart som är associerad med det här avsnittet anger det här värdet till `fr_FR`*.*

1. Återge ett HTML-formulär

   Anropa `FormsServiceClient` objektets `renderHTMLForm` metod och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som är en del av ett formulärprogram måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Ett `TransformTo` uppräkningsvärde som anger HTML-inställningstypen. Om du till exempel vill återge ett HTML-formulär som är kompatibelt med dynamisk HTML för Internet Explorer 5.0 eller senare anger du `TransformTo.MSDHTML`.
   * Ett `com.adobe.idp.Document` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du ett tomt `com.adobe.idp.Document` objekt.
   * Det objekt `HTMLRenderSpec` som lagrar körningsalternativ för HTML.
   * Ett strängvärde som anger `HTTP_USER_AGENT` rubrikvärdet, till exempel `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Ett `URLSpec` objekt som lagrar URI-värden som krävs för att återge ett HTML-formulär.
   * Ett `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter, och du kan ange `null` om du inte vill bifoga filer till formuläret.
   Metoden returnerar `renderHTMLForm` ett `FormsResult` objekt som innehåller en formulärdataström som måste skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa ett `com.adobe.idp.Document` objekt genom att anropa `FormsResult` objektets `getOutputContent` metod.
   * Hämta innehållstypen för `com.adobe.idp.Document` objektet genom att anropa dess `getContentType` metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metod och skicka `com.adobe.idp.Document` objektets innehållstyp.
   * Skapa ett `javax.servlet.ServletOutputStream` objekt som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` metod.
   * Skapa ett `java.io.InputStream` objekt genom att anropa `com.adobe.idp.Document` objektets `getInputStream` metod.
   * Skapa en bytearray och fyll i den med formulärdataströmmen genom att anropa `InputStream` objektets `read` metod och skicka bytearrayen som ett argument.
   * Anropa `javax.servlet.ServletOutputStream` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` metoden.

**Se även**

[Snabbstart (SOAP-läge): Återge ett HTML-formulär med ett anpassat verktygsfält med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Återge ett HTML-formulär med ett anpassat verktygsfält med hjälp av webbtjänstens API {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Återge ett HTML-formulär som innehåller ett anpassat verktygsfält med hjälp av Forms Service API (webbtjänsten):

1. Inkludera projektfiler

   * Skapa Java-proxyklasser som använder Forms-tjänstens WSDL.
   * Inkludera Java-proxyklasserna i klassökvägen.

1. Skapa ett Forms Java API-objekt

   Skapa ett `FormsService` objekt och ange autentiseringsvärden.

1. Referera en anpassad fscmenu XML-fil

   * Skapa ett `HTMLRenderSpec` objekt med hjälp av dess konstruktor.
   * Om du vill återge ett HTML-formulär med ett verktygsfält anropar du `HTMLRenderSpec` objektets `setHTMLToolbar` metod och skickar ett `HTMLToolbar` uppräkningsvärde. Om du till exempel vill visa ett lodrätt HTML-verktygsfält skickar du `HTMLToolbar.Vertical`.
   * Ange platsen för fscmenu XML-filen genom att anropa `HTMLRenderSpec` objektets `setToolbarURI` metod och skicka ett strängvärde som anger URI-platsen för XML-filen.
   * Om det är tillämpligt anger du språkvärdet genom att anropa `HTMLRenderSpec` objektets `setLocale` -metod och skicka ett strängvärde som anger språkvärdet. Standardvärdet är engelska.
   >[!NOTE]
   >
   >Snabbstart som är associerad med det här avsnittet anger det här värdet till `fr_FR`*.*

1. Återge ett HTML-formulär

   Anropa `FormsService` objektets `renderHTMLForm` metod och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som är en del av ett formulärprogram måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Ett `TransformTo` uppräkningsvärde som anger HTML-inställningstypen. Om du till exempel vill återge ett HTML-formulär som är kompatibelt med dynamisk HTML för Internet Explorer 5.0 eller senare anger du `TransformTo.MSDHTML`.
   * Ett `BLOB` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du `null`.
   * Det objekt `HTMLRenderSpec` som lagrar körningsalternativ för HTML.
   * Ett strängvärde som anger `HTTP_USER_AGENT` rubrikvärdet, t.ex. `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Du kan skicka en tom sträng om du inte vill ange det här värdet.
   * Ett `URLSpec` objekt som lagrar URI-värden som krävs för att återge ett HTML-formulär.
   * Ett `java.util.HashMap` objekt som lagrar bifogade filer. Den här parametern är valfri och du kan ange `null` om du inte vill bifoga filer till formuläret.
   * Ett tomt `com.adobe.idp.services.holders.BLOBHolder` objekt som fylls i av `renderHTMLForm` metoden. Det här parametervärdet lagrar det återgivna formuläret.
   * Ett tomt `com.adobe.idp.services.holders.BLOBHolder` objekt som fylls i av `renderHTMLForm` metoden. Den här parametern lagrar XML-data för utdata.
   * Ett tomt `javax.xml.rpc.holders.LongHolder` objekt som fylls i av `renderHTMLForm` metoden. Det här argumentet lagrar antalet sidor i formuläret.
   * Ett tomt `javax.xml.rpc.holders.StringHolder` objekt som fylls i av `renderHTMLForm` metoden. Det här argumentet lagrar språkets värde.
   * Ett tomt `javax.xml.rpc.holders.StringHolder` objekt som fylls i av `renderHTMLForm` metoden. Det här argumentet lagrar det HTML-återgivningsvärde som används.
   * Ett tomt `com.adobe.idp.services.holders.FormsResultHolder` objekt som innehåller resultatet av den här åtgärden.
   Metoden `renderHTMLForm` fyller i det `com.adobe.idp.services.holders.FormsResultHolder` objekt som skickas som det sista argumentvärdet med en formulärdataström som måste skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa ett `FormResult` objekt genom att hämta värdet för `com.adobe.idp.services.holders.FormsResultHolder` objektets `value` datamedlem.
   * Skapa ett `BLOB` objekt som innehåller formulärdata genom att anropa `FormsResult` objektets `getOutputContent` metod.
   * Hämta innehållstypen för `BLOB` objektet genom att anropa dess `getContentType` metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metod och skicka `BLOB` objektets innehållstyp.
   * Skapa ett `javax.servlet.ServletOutputStream` objekt som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` metod.
   * Skapa en bytearray och fyll i den genom att anropa `BLOB` objektets `getBinaryData` metod. Den här aktiviteten tilldelar innehållet i `FormsResult` objektet till bytearrayen.
   * Anropa `javax.servlet.http.HttpServletResponse` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` metoden.

**Se även**

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
