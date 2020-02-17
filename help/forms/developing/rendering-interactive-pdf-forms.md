---
title: Återgivning av interaktiva PDF-formulär
seo-title: Återgivning av interaktiva PDF-formulär
description: 'null'
seo-description: 'null'
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Återgivning av interaktiva PDF-formulär {#rendering-interactive-pdf-forms}

Forms-tjänsten återger interaktiva PDF-formulär till klientenheter, vanligtvis webbläsare, för att samla in information från användarna. När ett interaktivt formulär har återgetts kan användaren ange data i formulärfält och klicka på en Skicka-knapp som finns i formuläret för att skicka tillbaka information till Forms-tjänsten. Adobe Reader eller Acrobat måste vara installerat på den dator där webbläsaren körs för att ett interaktivt PDF-formulär ska kunna visas.

>[!NOTE]
>
>Skapa en formulärdesign innan du kan återge ett formulär med Forms-tjänsten. Vanligtvis skapas en formulärdesign i Designer och sparas som en XDP-fil. Mer information om hur du skapar en formulärdesign finns i [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

**Exempellåneansökan**

Ett exempel på en låneansökan läggs in för att visa hur Forms-tjänsten använder interaktiva formulär för att samla in information från användarna. Med det här programmet kan en användare fylla i ett formulär med de data som krävs för att skydda ett lån och sedan skicka data till Forms-tjänsten. I följande diagram visas låneansökans logiska flöde.

![ri_ri_finsrv_loanapp_v1](assets/ri_ri_finsrv_loanapp_v1.png)

I följande tabell beskrivs stegen i det här diagrammet.

<table>
 <thead>
  <tr>
   <th><p>Steg</p></th>
   <th><p>Beskrivning</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Java- <code>GetLoanForm</code> servern anropas från en HTML-sida. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Java- <code>GetLoanForm</code> serverns gränssnitt använder sig av Forms-tjänstens klient-API för att återge låneformuläret till klientens webbläsare. (Se <a href="#render-an-interactive-pdf-form-using-the-java-api">Återge ett interaktivt PDF-formulär med Java API</a>.)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>När användaren fyller i låneformuläret och klickar på skicka-knappen skickas data till <code>HandleData</code> Java-servern. (Se <i>"Låneblankett"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Java- <code>HandleData</code> serverns gränssnitt använder API:t för Forms-tjänstens klient för att bearbeta formuläröverföringen och hämta formulärdata. Data lagras sedan i en företagsdatabas. (Se <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Hantera skickade formulär</a>.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Ett bekräftelseformulär återges i webbläsaren. Data som användarens för- och efternamn sammanfogas med formuläret innan det återges. (Se <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Fylla i formulär i förväg med flödeslayouter</a>.)</p></td>
  </tr>
 </tbody>
</table>

**Låneblankett**

Denna interaktiva låneblankett återges av exempellånets `GetLoanForm` Java-serverdel.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Bekräftelseformulär**

Formuläret återges av exempellånets `HandleData` Java-server.

![ri_ri_confirm](assets/ri_ri_confirm.png)

Java- `HandleData` serverns formulär fylls i i förväg med användarens för- och efternamn samt mängden. När formuläret har fyllts i i i förväg skickas det till klientens webbläsare. (Se [Fylla i formulär i förväg med flödeslayouter](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Java Servlets**

Exempellåneansökan är ett exempel på ett Forms-tjänstprogram som finns som en Java-server. En Java-server är ett Java-program som körs på en J2EE-programserver, t.ex. WebSphere, och som innehåller API-kod för Forms-tjänstens klient.

I följande kod visas syntaxen för en Java-server med namnet GetLoanForm:

```as3
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

Vanligtvis placerar du inte Forms Service Client-API-kod i en Java-servers `doGet` - eller `doPost` -metod. Det är bättre programmeringspraxis att placera den här koden i en separat klass, instansiera klassen inifrån `doPost` metoden (eller `doGet` metoden) och anropa lämpliga metoder. För kodreaktion begränsas dock kodexemplen i det här avsnittet till ett minimum och kodexempel placeras i `doPost` metoden.

>[!NOTE]
>
>Mer information om Forms-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

**Sammanfattning av steg**

Så här återger du ett interaktivt PDF-formulär:

1. Inkludera projektfiler.
1. Skapa ett API-objekt för Forms Client.
1. Ange URI-värden.
1. Bifoga filer i formuläret (valfritt).
1. Återge ett interaktivt PDF-formulär.
1. Skriv formulärdataströmmen till klientens webbläsare.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett API-objekt för FormsClient**

Innan du programmässigt kan utföra en API-åtgärd för Form Service Client måste du skapa ett API-objekt för Forms Client. Om du använder Java API skapar du ett `FormsServiceClient` objekt. Skapa ett `FormsService` objekt om du använder webbtjänstens API:t för Forms.

**Ange URI-värden**

Du kan ange URI-värden som krävs av Forms-tjänsten för att återge ett formulär. En formulärdesign som sparas som en del av ett Forms-program kan refereras med hjälp av innehållets rot-URI-värde `repository:///`. Ta till exempel följande formulärdesign med namnet *Loan.xdp* som finns i ett Forms-program med namnet *FormsApplication*:

![ri_ri_formdatabase](assets/ri_ri_formrepository.png)

Om du vill komma åt den här formulärdesignen anger du `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` som formulärnamn (den första parametern som skickas till `renderPDFForm` metoden) och `repository:///` som URI-värde för innehållsroten.

>[!NOTE]
>
>Mer information om hur du skapar ett formulärprogram med Workbench finns i [Workbench-hjälpen](https://www.adobe.com/go/learn_aemforms_workbench_63).

Sökvägen till en resurs som finns i ett Forms-program är:

`Applications/Application-name/Application-version/Folder.../Filename`

Följande värden visar några exempel på URI-värden:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

När du återger ett interaktivt formulär kan du definiera URI-värden, till exempel mål-URL:en som formulärdata ska skickas till. Mål-URL:en kan definieras på något av följande sätt:

* Klicka på knappen Skicka när du designar formulärdesignen i Designer
* Genom att använda Forms-tjänstens klient-API

Om mål-URL:en definieras i formulärdesignen ska du inte åsidosätta den med Forms-tjänstens klient-API. Det innebär att om du anger mål-URL:en med API:t för Forms återställs den angivna URL:en i formulärdesignen till den som anges med API:t. Om du vill skicka PDF-formuläret till mål-URL:en som anges i formulärdesignen anger du mål-URL:en automatiskt till en tom sträng.

Om du har ett formulär som innehåller en skicka-knapp och en beräkningsknapp (med ett motsvarande skript som körs på servern) kan du programmässigt definiera den URL som formuläret skickas till för att köra skriptet. Använd knappen Skicka i formulärdesignen för att ange den URL som formulärdata ska skickas till. (Se [Beräkna formulärdata](/help/forms/developing/calculating-form-data.md).)

>[!NOTE]
>
>I stället för att ange ett URL-värde för att referera till en XDP-fil kan du även skicka en `com.adobe.idp.Document` instans till Forms-tjänsten. Instansen `com.adobe.idp.Document` innehåller en formulärdesign. (Se [Skicka dokument till formulärtjänsten](/help/forms/developing/passing-documents-forms-service.md).)

**Bifoga filer i formuläret**

Du kan bifoga filer till ett formulär. När du återger ett PDF-formulär med bifogade filer, kan användarna hämta de bifogade filerna i Acrobat via rutan för bifogade filer. Du kan bifoga olika filtyper till ett formulär, t.ex. en textfil, eller till en binär fil, t.ex. en JPG-fil.

>[!NOTE]
>
>Det är valfritt att bifoga bifogade filer till ett formulär.

**Återge ett interaktivt PDF-formulär**

Om du vill återge ett formulär använder du en formulärdesign som har skapats i Designer och sparats som en XDP- eller PDF-fil. Du kan även återge ett formulär som har skapats med Acrobat och sparats som en PDF-fil. Om du vill återge ett interaktivt PDF-formulär anropar du `FormsServiceClient` objektets `renderPDFForm` metod eller `renderPDFForm2` metod.

I `renderPDFForm` används ett `URLSpec` objekt. Innehållsroten till XDP-filen skickas till Forms-tjänsten med hjälp av `URLSpec` objektets `setContentRootURI` metod. Formulärdesignnamnet ( `formQuery`) skickas som ett separat parametervärde. De två värdena sammanfogas för att få den absoluta referensen till formulärdesignen.

Metoden accepterar `renderPDFForm2` en `com.adobe.idp.Document` instans som innehåller XDP- eller PDF-dokumentet som ska återges.

>[!NOTE]
>
>Alternativet för taggad PDF-körning kan inte anges om indatadokumentet är ett PDF-dokument. Om indatafilen är en XDP-fil kan alternativet taggad PDF anges.

## Återge ett interaktivt PDF-formulär med Java API {#render-an-interactive-pdf-form-using-the-java-api}

Återge ett interaktivt PDF-formulär med hjälp av Forms API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar, i Java-projektets klassökväg.

1. Skapa ett API-objekt för FormsClient

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa ett `FormsServiceClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.

1. Ange URI-värden

   * Skapa ett `URLSpec` objekt som lagrar URI-värden med hjälp av dess konstruktor.
   * Anropa `URLSpec` objektets `setApplicationWebRoot` metod och skicka ett strängvärde som representerar programmets webbrot.
   * Anropa `URLSpec` objektets `setContentRootURI` metod och skicka ett strängvärde som anger innehållets rot-URI-värde. Kontrollera att formulärdesignen finns i innehållets rot-URI. Annars genereras ett undantag av Forms-tjänsten. Om du vill referera till databasen anger du `repository:///`.
   * Anropa `URLSpec` objektets `setTargetURL` metod och skicka ett strängvärde som anger det mål-URL-värde som formulärdata ska skickas till. Om du definierar mål-URL:en i formulärdesignen kan du skicka en tom sträng. Du kan också ange den URL dit ett formulär skickas för att utföra beräkningar.

1. Bifoga filer i formuläret

   * Skapa ett `java.util.HashMap` objekt för att lagra bifogade filer med hjälp av dess konstruktor.
   * Anropa `java.util.HashMap` objektets `put` metod för varje fil som ska kopplas till det återgivna formuläret. Skicka följande värden till den här metoden:

      * Ett strängvärde som anger namnet på den bifogade filen, inklusive filnamnstillägget.
   * Ett `com.adobe.idp.Document` objekt som innehåller den bifogade filen.
   >[!NOTE]
   >
   >Upprepa det här steget för varje fil som ska bifogas formuläret. Det här steget är valfritt och du kan skicka det `null` om du inte vill skicka bifogade filer.

1. Återge ett interaktivt PDF-formulär

   Anropa `FormsServiceClient` objektets `renderPDFForm` metod och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som är en del av ett formulärprogram måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Ett `com.adobe.idp.Document` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du ett tomt `com.adobe.idp.Document` objekt.
   * Ett `PDFFormRenderSpec` objekt som lagrar körningsalternativ. Det här är en valfri parameter och du kan ange `null` om du inte vill ange körningsalternativ.
   * Ett `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten.
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

## Återge ett interaktivt PDF-formulär med webbtjänstens API {#render-an-interactive-pdf-form-using-the-web-service-api}

Återge ett interaktivt PDF-formulär med Forms API (webbtjänsten):

1. Inkludera projektfiler

   * Skapa Java-proxyklasser som använder Forms-tjänstens WSDL.
   * Inkludera Java-proxyklasserna i klassökvägen.

1. Skapa ett API-objekt för FormsClient

   Skapa ett `FormsService` objekt och ange autentiseringsvärden.

1. Ange URI-värden

   * Skapa ett `URLSpec` objekt som lagrar URI-värden med hjälp av dess konstruktor.
   * Anropa `URLSpec` objektets `setApplicationWebRoot` metod och skicka ett strängvärde som representerar programmets webbrot.
   * Anropa `URLSpec` objektets `setContentRootURI` metod och skicka ett strängvärde som anger innehållets rot-URI-värde. Kontrollera att formulärdesignen finns i innehållets rot-URI. Annars genereras ett undantag av Forms-tjänsten. Om du vill referera till databasen anger du `repository:///`.
   * Anropa `URLSpec` objektets `setTargetURL` metod och skicka ett strängvärde som anger det mål-URL-värde som formulärdata ska skickas till. Om du definierar mål-URL:en i formulärdesignen kan du skicka en tom sträng. Du kan också ange den URL dit ett formulär skickas för att utföra beräkningar.

1. Bifoga filer i formuläret

   * Skapa ett `java.util.HashMap` objekt för att lagra bifogade filer med hjälp av dess konstruktor.
   * Anropa `java.util.HashMap` objektets `put` metod för varje fil som ska kopplas till det återgivna formuläret. Skicka följande värden till den här metoden:

      * Ett strängvärde som anger namnet på den bifogade filen, inklusive filnamnstillägget
   * Ett `BLOB` objekt som innehåller den bifogade filen
   >[!NOTE]
   >
   >Upprepa det här steget för varje fil som ska bifogas formuläret.

1. Återge ett interaktivt PDF-formulär

   Anropa `FormsService` objektets `renderPDFForm` metod och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som är en del av ett formulärprogram måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Ett `BLOB` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du `null`.
   * Ett `PDFFormRenderSpec` objekt som lagrar körningsalternativ. Det här är en valfri parameter och du kan ange `null` om du inte vill ange körningsalternativ.
   * Ett `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten.
   * Ett `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.
   * Ett tomt `com.adobe.idp.services.holders.BLOBHolder` objekt som fylls i av metoden. Detta används för att lagra det återgivna PDF-formuläret.
   * Ett tomt `javax.xml.rpc.holders.LongHolder` objekt som fylls i av metoden. (Det här argumentet lagrar antalet sidor i formuläret.)
   * Ett tomt `javax.xml.rpc.holders.StringHolder` objekt som fylls i av metoden. (Det här argumentet lagrar språkets värde.)
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

**Skriv formulärdataströmmen till klientens webbläsare**

När Forms-tjänsten återger ett formulär returneras en formulärdataström som du måste skriva till klientens webbläsare. När formuläret skrivs till webbläsaren visas det för användaren.
