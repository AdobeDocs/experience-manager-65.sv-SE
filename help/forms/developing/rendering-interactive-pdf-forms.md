---
title: Återger interaktiv PDF forms
description: Använd tjänsten Forms för att återge interaktiv PDF forms till klientenheter, vanligtvis webbläsare, för att samla in information från användare. Du kan använda Forms tjänst för att återge interaktiva formulär med Java API och Web Service API.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d9f32939-c2c0-4531-b15e-f63941c289e3
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '2483'
ht-degree: 0%

---

# Återger interaktiv PDF forms {#rendering-interactive-pdf-forms}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

Forms-tjänsten återger interaktiv PDF forms till klientenheter, vanligtvis webbläsare, för att samla in information från användare. När ett interaktivt formulär har återgetts kan användaren ange data i formulärfält och klicka på en Skicka-knapp som finns i formuläret för att skicka tillbaka information till Forms-tjänsten. Adobe Reader eller Acrobat måste vara installerade på den dator som är värd för klientwebbläsaren för att ett interaktivt PDF-formulär ska kunna visas.

>[!NOTE]
>
>Skapa en formulärdesign innan du kan återge ett formulär med Forms-tjänsten. Vanligtvis skapas en formulärdesign i Designer och sparas som en XDP-fil. Mer information om hur du skapar en formulärdesign finns i [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

**Exempellåneansökan**

Ett exempel på en låneansökan läggs in för att visa hur Forms-tjänsten använder interaktiva blanketter för att samla in information från användarna. Med det här programmet kan en användare fylla i ett formulär med de data som krävs för att skydda ett lån och sedan skicka data till Forms-tjänsten. I följande diagram visas låneansökans logiska flöde.

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
   <td><p>The <code>GetLoanForm</code> Java Servlet anropas från HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>The <code>GetLoanForm</code> Java Servlet använder Forms klient-API:t för att återge låneformuläret till klientens webbläsare. (Se <a href="#render-an-interactive-pdf-form-using-the-java-api">Återge ett interaktivt PDF-formulär med Java API</a>.)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>När användaren fyller i låneformuläret och klickar på skicka-knappen skickas data till <code>HandleData</code> Java Servlet. (Se <i>"Låneblankett"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>The <code>HandleData</code> Java Servlet använder Forms klient-API:t för att bearbeta formuläröverföringen och hämta formulärdata. Data lagras sedan i en företagsdatabas. (Se <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Hantera skickade Forms</a>.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Ett bekräftelseformulär återges i webbläsaren. Data som användarens för- och efternamn sammanfogas med formuläret innan det återges. (Se <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Förifyll Forms med flödeslayouter</a>.)</p></td>
  </tr>
 </tbody>
</table>

**Låneblankett**

Det här interaktiva låneformuläret återges av exempellåneansökans `GetLoanForm` Java Servlet.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Bekräftelseformulär**

Det här formuläret återges av exempelprogrammets `HandleData` Java Servlet.

![ri_ri_confirm](assets/ri_ri_confirm.png)

The `HandleData` Java Servlet fyller i formuläret i förväg med användarens för- och efternamn samt mängden. När formuläret har fyllts i i i förväg skickas det till klientens webbläsare. (Se [Förifyll Forms med flödeslayouter](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Java Servlets**

Exempellåneansökan är ett exempel på en Forms-tjänstapplikation som finns som en Java-server. En Java-server är ett Java-program som körs på en J2EE-programserver, t.ex. WebSphere, och som innehåller API-kod för Forms-tjänstklienten.

I följande kod visas syntaxen för en Java-server med namnet GetLoanForm:

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

Normalt placerar du inte Forms klient-API-kod i Java-serverns `doGet` eller `doPost` -metod. Det är bättre programmeringspraxis att placera den här koden i en separat klass, instansiera klassen inifrån `doPost` metod (eller `doGet` och anropa lämpliga metoder. För kodförkortning begränsas dock kodexemplen i det här avsnittet till ett minimum och kodexempel placeras i `doPost` -metod.

>[!NOTE]
>
>Mer information om tjänsten Forms finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

**Sammanfattning av steg**

Så här återger du ett interaktivt PDF-formulär:

1. Inkludera projektfiler.
1. Skapa ett Forms Client API-objekt.
1. Ange URI-värden.
1. Bifoga filer i formuläret (valfritt).
1. Återge ett interaktivt PDF-formulär.
1. Skriv formulärdataströmmen till klientens webbläsare.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett Forms Client API-objekt**

Innan du programmässigt kan utföra en API-åtgärd för Forms-tjänstklienten måste du skapa ett Forms Client API-objekt. Om du använder Java API skapar du en `FormsServiceClient` -objekt. Om du använder Forms webbtjänst-API skapar du en `FormsService` -objekt.

**Ange URI-värden**

Du kan ange URI-värden som krävs av Forms-tjänsten för att återge ett formulär. En formulärdesign som sparas som en del av ett Forms-program kan refereras med hjälp av innehållets rot-URI-värde `repository:///`. Ta till exempel följande formulärdesign med namnet *Loan.xdp* som finns i ett Forms-program med namnet *FormsApplication*:

![ri_ri_formdatabase](assets/ri_ri_formrepository.png)

Om du vill komma åt den här formulärdesignen anger du `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` som formulärnamnet (den första parametern som skickas till `renderPDFForm` metod) och `repository:///` som innehållsrots-URI-värde.

>[!NOTE]
>
>Mer information om hur du skapar ett Forms-program med Workbench finns i [Workbench - hjälp](https://www.adobe.com/go/learn_aemforms_workbench_63).

Sökvägen till en resurs i ett Forms-program är:

`Applications/Application-name/Application-version/Folder.../Filename`

Följande värden visar några exempel på URI-värden:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

När du återger ett interaktivt formulär kan du definiera URI-värden, t.ex. mål-URL:en som formulärdata ska skickas till. Mål-URL:en kan definieras på något av följande sätt:

* Klicka på knappen Skicka när du designar formulärdesignen i Designer
* Genom att använda Forms klient-API för tjänster

Om mål-URL:en definieras i formulärdesignen, ska du inte åsidosätta den med Forms klient-API. Det innebär att om du anger mål-URL:en med Forms API återställs den angivna URL:en i formulärdesignen till den som anges med API:t. Om du vill skicka formuläret PDF till den mål-URL som anges i formulärdesignen, anger du mål-URL:en automatiskt till en tom sträng.

Om du har ett formulär som innehåller en skicka-knapp och en beräkningsknapp (med ett motsvarande skript som körs på servern) kan du programmässigt definiera den URL som formuläret skickas till för att köra skriptet. Använd knappen Skicka i formulärdesignen för att ange den URL som formulärdata ska skickas till. (Se [Beräknar formulärdata](/help/forms/developing/calculating-form-data.md).)

>[!NOTE]
>
>I stället för att ange ett URL-värde för att referera till en XDP-fil kan du även skicka en `com.adobe.idp.Document` till tjänsten Forms. The `com.adobe.idp.Document` -instansen innehåller en formulärdesign. (Se [Skicka dokument till Forms](/help/forms/developing/passing-documents-forms-service.md).)

**Bifoga filer i formuläret**

Du kan bifoga filer till ett formulär. När du återger ett PDF-formulär med bifogade filer kan användare hämta de bifogade filerna i Acrobat med hjälp av rutan för bifogade filer. Du kan bifoga olika filtyper till ett formulär, t.ex. en textfil, eller till en binär fil, t.ex. en JPG-fil.

>[!NOTE]
>
>Det är valfritt att bifoga bifogade filer till ett formulär.

**Återge ett interaktivt PDF-formulär**

Om du vill återge ett formulär använder du en formulärdesign som har skapats i Designer och sparats som en XDP- eller PDF-fil. Du kan även återge ett formulär som har skapats med Acrobat och sparats som en PDF-fil. Om du vill återge ett interaktivt PDF-formulär anropar du `FormsServiceClient` objektets `renderPDFForm` metod eller `renderPDFForm2` -metod.

The `renderPDFForm` använder `URLSpec` -objekt. Innehållsroten till XDP-filen skickas till Forms-tjänsten med `URLSpec` objektets `setContentRootURI` -metod. Formulärdesignens namn ( `formQuery`) skickas som ett separat parametervärde. De två värdena sammanfogas för att få den absoluta referensen till formulärdesignen.

The `renderPDFForm2` metoden accepterar `com.adobe.idp.Document` -instans som innehåller XDP- eller PDF-dokumentet som ska återges.

>[!NOTE]
>
>Körningsalternativet PDF med märkord kan inte anges om indatadokumentet är ett PDF-dokument. Om indatafilen är en XDP-fil kan du ange alternativet PDF med märkord.

## Återge ett interaktivt PDF-formulär med Java API {#render-an-interactive-pdf-form-using-the-java-api}

Återge ett interaktivt PDF-formulär med Forms API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar, i Java-projektets klassökväg.

1. Skapa ett Forms Client API-objekt

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `FormsServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Ange URI-värden

   * Skapa en `URLSpec` objekt som lagrar URI-värden med hjälp av dess konstruktor.
   * Anropa `URLSpec` objektets `setApplicationWebRoot` och skicka ett strängvärde som representerar programmets webbrot.
   * Anropa `URLSpec` objektets `setContentRootURI` och skicka ett strängvärde som anger innehållets rot-URI-värde. Kontrollera att formulärdesignen finns i innehållets rot-URI. Annars genereras ett undantag. Om du vill referera till databasen anger du `repository:///`.
   * Anropa `URLSpec` objektets `setTargetURL` och skicka ett strängvärde som anger det mål-URL-värde som formulärdata ska skickas till. Om du definierar mål-URL:en i formulärdesignen kan du skicka en tom sträng. Du kan också ange den URL dit ett formulär ska skickas för att utföra beräkningar.

1. Bifoga filer i formuläret

   * Skapa en `java.util.HashMap` -objekt för att lagra bifogade filer med hjälp av dess konstruktor.
   * Anropa `java.util.HashMap` objektets `put` metod för varje fil som ska bifogas det återgivna formuläret. Skicka följande värden till den här metoden:

      * Ett strängvärde som anger namnet på den bifogade filen, inklusive filnamnstillägget.

   * A `com.adobe.idp.Document` objekt som innehåller den bifogade filen.

   >[!NOTE]
   >
   >Upprepa det här steget för varje fil som ska bifogas formuläret. Det här steget är valfritt och du kan godkänna det `null` om du inte vill skicka bifogade filer.

1. Återge ett interaktivt PDF-formulär

   Anropa `FormsServiceClient` objektets `renderPDFForm` och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som ingår i ett Forms-program måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du en tom `com.adobe.idp.Document` -objekt.
   * A `PDFFormRenderSpec` objekt som lagrar körningsalternativ. Det här är en valfri parameter och du kan ange `null` om du inte vill ange körningsalternativ.
   * A `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten.
   * A `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.

   The `renderPDFForm` returnerar en `FormsResult` objekt som innehåller en formulärdataström som måste skrivas till klientens webbläsare.

1. Skriv formulärdataströmmen till klientens webbläsare

   * Skapa en `com.adobe.idp.Document` genom att anropa `FormsResult` objekt `getOutputContent` -metod.
   * Hämta innehållstypen för `com.adobe.idp.Document` genom att anropa dess `getContentType` -metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metoden och skicka innehållstypen för `com.adobe.idp.Document` -objekt.
   * Skapa en `javax.servlet.ServletOutputStream` som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` -metod.
   * Skapa en `java.io.InputStream` genom att anropa `com.adobe.idp.Document` objektets `getInputStream` -metod.
   * Skapa en bytearray och fylla den med formulärdataströmmen genom att anropa `InputStream` objektets `read` och skicka bytearrayen som ett argument.
   * Anropa `javax.servlet.ServletOutputStream` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` -metod.

## Återge ett interaktivt PDF-formulär med hjälp av webbtjänstens API {#render-an-interactive-pdf-form-using-the-web-service-api}

Återge ett interaktivt PDF-formulär med Forms API (webbtjänst):

1. Inkludera projektfiler

   * Skapa Java-proxyklasser som använder Forms tjänst-WSDL.
   * Inkludera Java-proxyklasserna i klassökvägen.

1. Skapa ett Forms Client API-objekt

   Skapa en `FormsService` och ange autentiseringsvärden.

1. Ange URI-värden

   * Skapa en `URLSpec` objekt som lagrar URI-värden med hjälp av dess konstruktor.
   * Anropa `URLSpec` objektets `setApplicationWebRoot` och skicka ett strängvärde som representerar programmets webbrot.
   * Anropa `URLSpec` objektets `setContentRootURI` och skicka ett strängvärde som anger innehållets rot-URI-värde. Kontrollera att formulärdesignen finns i innehållets rot-URI. Annars genereras ett undantag. Om du vill referera till databasen anger du `repository:///`.
   * Anropa `URLSpec` objektets `setTargetURL` och skicka ett strängvärde som anger det mål-URL-värde som formulärdata ska skickas till. Om du definierar mål-URL:en i formulärdesignen kan du skicka en tom sträng. Du kan också ange den URL dit ett formulär ska skickas för att utföra beräkningar.

1. Bifoga filer i formuläret

   * Skapa en `java.util.HashMap` -objekt för att lagra bifogade filer med hjälp av dess konstruktor.
   * Anropa `java.util.HashMap` objektets `put` metod för varje fil som ska bifogas det återgivna formuläret. Skicka följande värden till den här metoden:

      * Ett strängvärde som anger namnet på den bifogade filen, inklusive filnamnstillägget

   * A `BLOB` objekt som innehåller den bifogade filen

   >[!NOTE]
   >
   >Upprepa det här steget för varje fil som ska bifogas formuläret.

1. Återge ett interaktivt PDF-formulär

   Anropa `FormsService` objektets `renderPDFForm` och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget. Om du refererar till en formulärdesign som ingår i ett Forms-program måste du ange den fullständiga sökvägen, till exempel `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` objekt som innehåller data som ska sammanfogas med formuläret. Om du inte vill sammanfoga data skickar du `null`.
   * A `PDFFormRenderSpec` objekt som lagrar körningsalternativ. Det här är en valfri parameter och du kan ange `null` om du inte vill ange körningsalternativ.
   * A `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten.
   * A `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.
   * En tom `com.adobe.idp.services.holders.BLOBHolder` objekt som fylls i av metoden. Det här används för att lagra det återgivna PDF-formuläret.
   * En tom `javax.xml.rpc.holders.LongHolder` objekt som fylls i av metoden. (Detta argument lagrar antalet sidor i formuläret.)
   * En tom `javax.xml.rpc.holders.StringHolder` objekt som fylls i av metoden. (Det här argumentet lagrar språkets värde.)
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

**Skriv formulärdataströmmen till klientens webbläsare**

När Forms-tjänsten återger ett formulär returneras en formulärdataström som du måste skriva till klientens webbläsare. När formuläret skrivs till webbläsaren visas det för användaren.
