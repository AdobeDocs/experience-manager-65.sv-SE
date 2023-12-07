---
title: Återger formulärmall för HTML5-formulär
description: HTML5-formulärprofiler är kopplade till profilåtergivningar. Profilåtergivningar är JSP-sidor som ansvarar för att skapa HTML-representation av formuläret genom att anropa tjänsten Forms OSGi.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# Återger formulärmall för HTML5-formulär {#rendering-form-template-for-html-forms}

## Återgivningsslutpunkt {#render-endpoint}

HTML5-blanketter har samma innebörd som **Profiler** som visas som REST-slutpunkter för att aktivera mobil återgivning av formulärmallar. Dessa profiler har associerats **Profilåtergivning**. De är JSP-sidor som ansvarar för att generera HTML-representation av formuläret genom att anropa tjänsten Forms OSGi. JCR-sökvägen för profilnoden avgör URL:en för återgivningens slutpunkt. Standardslutpunkten för återgivningen som pekar på standardprofilen ser ut så här:

https://&lt;*värd*>:&lt;*port*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*sökväg till mappen som innehåller xdp-formuläret*>&amp;template=&lt;*xdp-namnet*>

Exempel: `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

För en anpassad profil ändras slutpunkten därefter. Slutpunkten för den anpassade profilen med namnet &quot;hrforms&quot; är till exempel:

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Om mallen finns i AEM i ett program som heter FormSubmission är URI:n:

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## Återgivningsparametrar {#render-parameters}

Begärandeparametrarna som stöds vid återgivning av formulär som HTML är:

<table>
 <tbody>
  <tr>
   <th><strong>Parameter </strong></th>
   <th><strong>Beskrivning</strong></th>
  </tr>
  <tr>
   <td>mall<br /> </td>
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
| dataRef | Den här parametern anger **absolut sökväg** av den datafil som sammanfogas med mallen. Den här parametern kan vara en URL till en vilotjänst som returnerar data i xml-format. |
| data | Den här parametern anger de UTF-8-kodade databyte som sammanfogas med mallen. Om den här parametern anges ignorerar HTML5-formuläret parametern dataRef. |

### Skicka återgivningsparametern {#passing-the-render-parameter}

HTML5-formulär har stöd för tre metoder för att skicka återgivningsparametrarna. Du kan skicka parametrar via URL:er, nyckelvärdepar och profilnod. I återgivningsparametern har nyckelvärdepar högsta prioritet följt av profilnod. Parametern URL-begäran har lägst prioritet.

* **Parametrar för URL-begäran**: Du kan ange återgivningsparametrar i URL:en. I parametrarna för URL-begäran är parametrarna synliga för slutanvändaren. Följande Skicka-URL innehåller mallparameter i URL:en: `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **Parametrar för SetAttribute-begäran**: Du kan ange återgivningsparametrarna som ett nyckelvärdepar. I parametrarna för SetAttribute-begäran är parametrarna inte synliga för slutanvändaren. Du kan vidarebefordra en begäran från en annan JSP till HTML5-formulärprofilsåtergivning för JSP och använda *setAttribute* på begäranobjekt för att skicka alla återgivningsparametrar. Den här metoden har högsta prioritet.

* **Parametrar för profilnodbegäran:** Du kan ange återgivningsparametrarna som nodegenskaper för en profilnod. I parametrarna för profilnodbegäran är parametrarna inte synliga för slutanvändaren. Profilnod är den nod där begäran skickas. Om du vill ange parametrar som nodegenskaper använder du CRXDE lite.

### Skicka parametrar {#submit-parameters}

HTML5-formulär skickar data; kör serverbaserade skript och webbtjänster på AEM servrar. Detaljerad information om parametrar som används för att köra serverbaserade skript och webbtjänster på AEM servrar finns i [HTML5 forms Service Proxy](/help/forms/using/service-proxy.md).
