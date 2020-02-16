---
title: Återger formulärmall för HTML5-formulär
seo-title: Återger formulärmall för HTML5-formulär
description: HTML5-formulärprofiler är kopplade till profilåtergivningar. Profilåtergivning är JSP-sidor som ansvarar för att generera HTML-återgivning av formuläret genom att anropa Forms OSGi-tjänsten.
seo-description: HTML5-formulärprofiler är kopplade till profilåtergivningar. Profilåtergivning är JSP-sidor som ansvarar för att generera HTML-återgivning av formuläret genom att anropa Forms OSGi-tjänsten.
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Återger formulärmall för HTML5-formulär {#rendering-form-template-for-html-forms}

## Återgivningsslutpunkt {#render-endpoint}

HTML5-formulär har en uppfattning om **profiler** som visas som REST-slutpunkter för att aktivera mobil återgivning av formulärmallar. Dessa profiler har associerad **profilrenderare**. De är JSP-sidor som ansvarar för att generera HTML-representation av formuläret genom att anropa Forms OSGi-tjänsten. JCR-sökvägen för profilnoden avgör URL:en för återgivningens slutpunkt. Standardslutpunkten för återgivningen som pekar på standardprofilen ser ut så här:

https://&lt;*host*>:&lt;*port*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*path of the folder containing form xdp*>&amp;template=&lt;*name of the xdp*>

Exempel, `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

För en anpassad profil ändras slutpunkten därefter. Slutpunkten för den anpassade profilen med namnet &quot;hrforms&quot; är till exempel:

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Om mallen finns i AEM-databasen i ett program som heter FormSubmission är URI:n:

```
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## Återgivningsparametrar {#render-parameters}

Begärandeparametrar som stöds vid återgivning av formulär som HTML är:

<table>
 <tbody>
  <tr>
   <th><strong>Parameter </strong></th>
   <th><strong>Beskrivning</strong></th>
  </tr>
  <tr>
   <td>template<br /> </td>
   <td>Den här parametern anger namnet på mallfilen.<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>Den här parametern anger sökvägen där mallen och de associerade resurserna finns. Den här sökvägen kan vara serverfilens systemsökväg eller en databassökväg eller en http- eller ftp-sökväg.<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>Den här parametern anger den URL som formulärdata xml skickas till.<br /> </td>
  </tr>
 </tbody>
</table>

### Sammanfoga data med formulärmall {#merge-data-with-form-template}

| Parameter | Beskrivning |
|---|---|
| dataRef | Den här parametern anger den **absoluta sökvägen** till datafilen som sammanfogas med mallen. Den här parametern kan vara en URL till en vilotjänst som returnerar data i xml-format. |
| data | Den här parametern anger de UTF-8-kodade databyte som sammanfogas med mallen. Om den här parametern anges ignorerar HTML5-formuläret parametern dataRef. |

### Skicka återgivningsparametern {#passing-the-render-parameter}

HTML5-formulär har stöd för tre metoder för att skicka återgivningsparametrarna. Du kan skicka parametrar via URL:er, nyckelvärdepar och profilnod. I återgivningsparametern har nyckelvärdepar högsta prioritet följt av profilnod. Parametern URL-begäran har lägst prioritet.

* **URL-frågeparametrar**: Du kan ange återgivningsparametrarna i URL:en. I parametrarna för URL-begäran är parametrarna synliga för slutanvändaren. Följande Skicka-URL innehåller mallparameter i URL:en: `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **Parametrar** för SetAttribute-begäran: Du kan ange återgivningsparametrarna som ett nyckelvärdepar. I parametrarna för SetAttribute-begäran är parametrarna inte synliga för slutanvändaren. Du kan vidarebefordra en begäran från andra JSP-program till JSP för HTML5-formulärprofiler och använda *setAttribute* för begäranobjektet för att skicka alla återgivningsparametrar. Den här metoden har högsta prioritet.

* **** Parametrar för profilnodbegäran: Du kan ange återgivningsparametrarna som nodegenskaper för en profilnod. I parametrarna för profilnodbegäran är parametrarna inte synliga för slutanvändaren. Profilnod är den nod där begäran skickas. Om du vill ange parametrar som nodegenskaper använder du CRXDE lite.

### Skicka parametrar {#submit-parameters}

HTML5-formulär skickar data; köra serverbaserade skript och webbtjänster på AEM-servrar. Detaljerad information om parametrar som används för att köra serverbaserade skript och webbtjänster på AEM-servrar finns i [HTML5 Forms Service Proxy](/help/forms/using/service-proxy.md).

**[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)**
