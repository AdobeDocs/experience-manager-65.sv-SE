---
title: Beräknar formulärdata
seo-title: Calculating Form Data
description: Använd tjänsten Forms för att beräkna värden som en användare anger i ett formulär och visa resultaten. Forms-tjänsten beräknar värdena med Java API och Web Service API.
seo-description: Use the Forms service to calculate values that a user enters into a form and display the results. Forms service calculates the values using the Java API and Web Service API.
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
role: Developer
exl-id: 28abf044-6c8e-4578-ae2e-54cdbd694c5f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 0%

---

# Beräknar formulärdata {#calculating-form-data}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

Forms-tjänsten kan beräkna de värden som en användare anger i ett formulär och visa resultaten. Om du vill beräkna formulärdata måste du utföra två uppgifter. Först skapar du ett formulärdesignskript som beräknar formulärdata. En formulärdesign har stöd för tre typer av skript. En skripttyp körs på klienten, en annan på servern och den tredje typen körs på både servern och klienten. Skripttypen som beskrivs i det här avsnittet körs på servern. Serverberäkningar stöds för omformningar av HTML, PDF och formulärguiden (utgått).

Som en del av formulärdesignprocessen kan du använda beräkningar och skript för att ge en bättre användarupplevelse. Beräkningar och skript kan läggas till i de flesta formulärfält och objekt. Du måste skapa ett formulärdesignskript för att kunna utföra beräkningsåtgärder på data som användaren matar in i ett interaktivt formulär.

Användaren anger värden i formuläret och klickar på knappen Beräkna för att visa resultatet. I följande process beskrivs ett exempelprogram som gör att en användare kan beräkna data:

* Användaren kommer åt en HTML-sida med namnet StartLoan.html som fungerar som webbprogrammets startsida. Den här sidan anropar en Java-server med namnet `GetLoanForm`.
* The `GetLoanForm` för att återge ett låneformulär. Det här formuläret innehåller ett skript, interaktiva fält, en beräkningsknapp och en skicka-knapp.
* Användaren anger värden i formulärets fält och klickar på knappen Beräkna. Formuläret skickas till `CalculateData` Java Servlet där skriptet körs. Formuläret skickas tillbaka till användaren med beräkningsresultaten visade i formuläret.
* Användaren fortsätter att ange och beräkna värden tills ett tillfredsställande resultat visas. När användaren är nöjd klickar han/hon på knappen Skicka för att bearbeta formuläret. Formuläret skickas till en annan Java-server med namnet `ProcessForm` som ansvarar för att hämta skickade data. (Se [Hantera skickade Forms](/help/forms/developing/rendering-forms.md#handling-submitted-forms).)


I följande diagram visas programmets logikflöde.

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

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
   <td><p>The <code>GetLoanForm</code> Java Servlet anropas från startsidan för HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>The <code>GetLoanForm</code> Java Servlet använder Forms klient-API för att återge låneformuläret till klientens webbläsare. Skillnaden mellan återgivning av ett formulär som innehåller ett skript som är konfigurerat att köras på servern och återgivning av ett formulär som inte innehåller något skript är att du måste ange målplatsen som används för att köra skriptet. Om ingen målplats anges körs inte ett skript som är konfigurerat att köras på servern. Tänk dig till exempel programmet som introducerades i det här avsnittet. The <code>CalculateData</code> Java Servlet är målplatsen där skriptet körs.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Användaren anger data i interaktiva fält och klickar på knappen Beräkna. Formuläret skickas till <code>CalculateData</code> Java Servlet, där skriptet körs. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Formuläret återges i webbläsaren med beräkningsresultaten i formuläret. </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Användaren klickar på knappen Skicka när värdena är tillräckliga. Formuläret skickas till en annan Java-server med namnet <code>ProcessForm</code>.</p></td>
  </tr>
 </tbody>
</table>

Vanligtvis innehåller ett formulär som skickas som PDF-innehåll skript som körs på klienten. Serverberäkningar kan dock också utföras. En Skicka-knapp kan inte användas för att beräkna skript. I det här fallet utförs inte beräkningar eftersom Forms-tjänsten anser att interaktionen är fullständig.

För att illustrera användningen av ett formulärdesignskript undersöker det här avsnittet ett enkelt interaktivt formulär som innehåller ett skript som är konfigurerat att köras på servern. I följande diagram visas en formulärdesign som innehåller ett skript som lägger till värden som en användare anger i de första två fälten och som visar resultatet i det tredje fältet.

![cf_cf_caldata](assets/cf_cf_caldata.png)

**S.** Ett fält med namnet NumericField1 **B.** Ett fält med namnet NumericField2 **C.** Ett fält med namnet NumericField3

Skriptet i den här formulärdesignen har följande syntax:

```javascript
     NumericField3 = NumericField2 + NumericField1
```

I den här formulärdesignen är knappen Beräkna en kommandoknapp och skriptet finns i knappens `Click` -händelse. När en användare anger värden i de två första fälten (NumericField1 och NumericField2) och klickar på knappen Beräkna, skickas formuläret till Forms-tjänsten där skriptet körs. Forms-tjänsten återger formuläret till klientenheten med resultatet av beräkningen som visas i fältet NumericField3.

>[!NOTE]
>
>Mer information om hur du skapar ett formulärdesignskript finns i [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

>[!NOTE]
>
>Mer information om tjänsten Forms finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Sammanfattning av steg {#summary-of-steps}

Utför följande uppgifter för att beräkna formulärdata:

1. Inkludera projektfiler.
1. Skapa ett Forms Client API-objekt.
1. Hämta ett formulär som innehåller ett beräkningsskript.
1. Skriv tillbaka formulärdataströmmen till klientens webbläsare

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett Forms Client API-objekt**

Innan du programmässigt kan utföra en API-åtgärd för Forms-tjänstklienten måste du skapa en Forms-tjänstklient. Om du använder Java API skapar du en `FormsServiceClient` -objekt. Om du använder Forms webbtjänst-API skapar du en `FormsServiceService` -objekt.

**Hämta ett formulär som innehåller ett beräkningsskript**

Du använder API:t för Forms-tjänstklienten för att skapa programlogik som hanterar ett formulär som innehåller ett skript som är konfigurerat att köras på servern. Processen liknar hantering av ett skickat formulär. (Se [Hantera skickade Forms](/help/forms/developing/handling-submitted-forms.md).)

Kontrollera att bearbetningstillståndet som är associerat med det skickade formuläret är `1` `(Calculate)`, vilket innebär att Forms-tjänsten utför en beräkningsåtgärd för formulärdata och att resultaten måste skrivas tillbaka till användaren. I så fall körs ett skript som är konfigurerat att köras på servern automatiskt.

**Skriv tillbaka formulärdataströmmen till klientens webbläsare**

När du har verifierat bearbetningstillståndet som är kopplat till ett skickat formulär är `1`måste du skriva tillbaka resultaten till klientens webbläsare. När formuläret visas visas det beräknade värdet i respektive fält.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Beräkna formulärdata med Java API](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[Beräkna formulärdata med webbtjänstens API](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[Snabbstart för Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[Återger interaktiv PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)
[Skapa webbprogram som återger Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Beräkna formulärdata med Java API {#calculate-form-data-using-the-java-api}

Beräkna formulärdata med Forms API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar, i Java-projektets klassökväg.

1. Skapa ett Forms Client API-objekt

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `FormsServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta ett formulär som innehåller ett beräkningsskript

   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och anropa `javax.servlet.http.HttpServletResponse` objektets `getInputStream` -metoden inifrån konstruktorn.
   * Anropa `FormsServiceClient` objektets `processFormSubmission` och skicka följande värden:

      * The `com.adobe.idp.Document` som innehåller formulärdata.
      * Ett strängvärde som anger miljövariabler inklusive alla relevanta HTTP-huvuden. Du måste ange vilken innehållstyp som ska hanteras genom att ange ett eller flera värden för `CONTENT_TYPE` systemvariabel. Om du till exempel vill hantera XML- och PDF-data anger du följande strängvärde för den här parametern: `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * Ett strängvärde som anger `HTTP_USER_AGENT` rubrikvärde; till exempel `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` objekt som lagrar körningsalternativ.

      The `processFormSubmission` returnerar en `FormsResult` objekt som innehåller resultaten av formuläröverföringen.

   * Kontrollera att bearbetningstillståndet som är associerat med ett skickat formulär är `1` genom att anropa `FormsResult` objektets `getAction` -metod. Om den här metoden returnerar värdet `1`beräkningarna utfördes och data kan skrivas tillbaka till klientens webbläsare.


1. Skriv tillbaka formulärdataströmmen till klientens webbläsare

   * Skapa en `javax.servlet.ServletOutputStream` som används för att skicka en formulärdataström till klientens webbläsare.
   * Skapa en `com.adobe.idp.Document` genom att anropa `FormsResult` objekt&quot;s `getOutputContent` -metod.
   * Skapa en `java.io.InputStream` genom att anropa `com.adobe.idp.Document` objektets `getInputStream` -metod.
   * Skapa en bytearray och fylla den med formulärdataströmmen genom att anropa `InputStream` objektets `read` och skicka bytearrayen som ett argument.
   * Anropa `javax.servlet.ServletOutputStream` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` -metod.

**Se även**


[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Beräkna formulärdata med webbtjänstens API {#calculate-form-data-using-the-web-service-api}

Beräkna formulärdata med Forms API (webbtjänst):

1. Inkludera projektfiler

   * Skapa Java-proxyklasser som använder Forms tjänst-WSDL.
   * Inkludera Java-proxyklasserna i klassökvägen.

1. Skapa ett Forms Client API-objekt

   Skapa en `FormsService` och ange autentiseringsvärden.

1. Hämta ett formulär som innehåller ett beräkningsskript

   * Skapa en `BLOB` genom att använda dess konstruktor.
   * Skapa en `java.io.InputStream` genom att använda `javax.servlet.http.HttpServletResponse` objektets `getInputStream` -metod.
   * Skapa en `java.io.ByteArrayOutputStream` genom att använda dess konstruktor och skicka längden på `java.io.InputStream` -objekt.
   * Kopiera innehållet i `java.io.InputStream` objektet i `java.io.ByteArrayOutputStream` -objekt.
   * Skapa en bytearray genom att anropa `java.io.ByteArrayOutputStream` objektets `toByteArray` -metod.
   * Fyll i `BLOB` genom att anropa dess `setBinaryData` och skicka bytearrayen som ett argument.
   * Skapa en `RenderOptionsSpec` genom att använda dess konstruktor. Ange språkvärdet genom att anropa `RenderOptionsSpec` objektets `setLocale` och skickar ett strängvärde som anger språkvärdet.
   * Anropa `FormsServiceClient` objektets `processFormSubmission` och skicka följande värden:

      * The `BLOB` som innehåller formulärdata.
      * Ett strängvärde som anger miljövariabler inkluderade alla relevanta HTTP-huvuden. Du kan till exempel ange följande strängvärde: `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * Ett strängvärde som anger `HTTP_USER_AGENT` rubrikvärde; till exempel `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` objekt som lagrar körningsalternativ. Mer information, .
      * En tom `BLOBHolder` objekt som fylls i av metoden.
      * En tom `javax.xml.rpc.holders.StringHolder` objekt som fylls i av metoden.
      * En tom `BLOBHolder` objekt som fylls i av metoden.
      * En tom `BLOBHolder` objekt som fylls i av metoden.
      * En tom `javax.xml.rpc.holders.ShortHolder` objekt som fylls i av metoden.
      * En tom `MyArrayOf_xsd_anyTypeHolder` objekt som fylls i av metoden. Den här parametern används för att lagra bifogade filer som skickas tillsammans med formuläret.
      * En tom `FormsResultHolder` objekt som fylls i av metoden med det formulär som skickas.

      The `processFormSubmission` metoden fyller i `FormsResultHolder` parametern med resultaten av formuläröverföringen. The `processFormSubmission` returnerar en `FormsResult` objekt som innehåller resultaten av formuläröverföringen.

   * Kontrollera att bearbetningstillståndet som är associerat med ett skickat formulär är `1` genom att anropa `FormsResult` objektets `getAction` -metod. Om den här metoden returnerar värdet `1`beräkningarna utfördes och data kan skrivas tillbaka till klientens webbläsare.


1. Skriv tillbaka formulärdataströmmen till klientens webbläsare

   * Skapa en `javax.servlet.ServletOutputStream` som används för att skicka en formulärdataström till klientens webbläsare.
   * Skapa en `BLOB` objekt som innehåller formulärdata genom att anropa `FormsResult` objektets `getOutputContent` -metod.
   * Skapa en bytearray och fylla i den genom att anropa `BLOB` objektets `getBinaryData` -metod. Den här aktiviteten tilldelar innehållet i `FormsResult` till bytearrayen.
   * Anropa `javax.servlet.http.HttpServletResponse` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` -metod.

**Se även**
[Anropa AEM Forms med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
