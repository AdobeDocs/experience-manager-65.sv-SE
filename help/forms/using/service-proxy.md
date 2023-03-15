---
title: HTML 5-formulärtjänstproxy
seo-title: HTML5 forms service proxy
description: HTML5-formulärtjänstens proxy är en konfiguration som registrerar en proxy för överföringstjänsten. Om du vill konfigurera tjänstproxy anger du URL:en för överföringstjänsten via parametern submitServiceProxy för begäran.
seo-description: HTML5 forms Service Proxy is a configuration to register a proxy for the submission service. To configure Service Proxy, specify the URL of submission service through request parameter submissionServiceProxy.
uuid: 42d6c1da-3945-469d-b429-c33e563ed70c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 081f7c17-4e5d-4c7e-a5c3-5541a29b9d55
docset: aem65
feature: Mobile Forms
exl-id: 8f9b10ae-1600-49c2-a061-153a2a89c67e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---

# HTML 5-formulärtjänstproxy{#html-forms-service-proxy}

HTML5-formulärtjänstens proxy är en konfiguration som registrerar en proxy för överföringstjänsten. Om du vill konfigurera tjänstproxy anger du URL:en för överföringstjänsten via parametern request *submitServiceProxy*.

## Fördelar med tjänstproxy {#benefits-of-service-proxy-br}

Tjänstproxyn eliminerar följande:

* HTML 5-formulärarbetsflödet kräver att inskickningstjänsten &quot;/content/xfaforms/submission/default&quot; öppnas för HTML5-formuläranvändare. Den exponerar AEM servrar för en större, oavsiktlig publik.
* Tjänst-URL:en är inbäddad i formulärets körningsmodell. Det går inte att ändra tjänstens URL-sökväg.
* Inlämningen är en tvåstegsprocess. För att skicka in formulärdata krävs minst två resor till servern. Ökar därmed belastningen på servern.
* HTML5-formulär skickar data i begäran om POST i stället för på begäran av PDF. För arbetsflöden som omfattar både PDF och HTML 5-formulär krävs två olika metoder för att behandla inskickade data.

### Topologies {#topologies-br}

HTML5-formulär kan använda följande topologier för att ansluta till AEM servrar.

* En topologi där AEM Server eller HTML5-formulär skickar data via POST till servern.
* En topologi där proxyservern skickar POST till servern.

![Proxytopologier för HTML5-formulärtjänst](assets/topology.png)

Proxytopologier för HTML5-formulärtjänst

HTML5-formulär kan anslutas till AEM servrar för att köra serverbaserade skript, webbtjänster och överföringar. XFA-miljön för HTML5-formulären använder Ajax-anrop på &quot;/bin/xfaforms/submit&quot;-slutpunkten med olika parametrar för att ansluta till AEM. HTML5-formulär ansluter AEM servrar för att utföra följande åtgärder:

#### Kör serverbaserade skript och webbtjänster {#execute-server-sided-scripts-and-web-services}

De skript som är markerade för att köras på servern kallas för serverbaserade skript. I följande tabell visas alla parametrar som används i serverbaserade skript och webbtjänster.

<table>
 <tbody>
  <tr>
   <td><p><strong>Parameter</strong></p> </td>
   <td><p><strong>Beskrivning</strong></p> </td>
  </tr>
  <tr>
   <td><p>activity</p> </td>
   <td><p>Aktiviteten innehåller de händelser som utlöser begäran. Till exempel klicka, avsluta eller ändra</p> </td>
  </tr>
  <tr>
   <td><p>contextAs</p> </td>
   <td><p>contextSOM innehåller SOM-uttryck för objektet där händelser körs.</p> </td>
  </tr>
  <tr>
   <td><p>Mall</p> </td>
   <td><p>Mallen innehåller mallen som används för att återge formuläret.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>contentRoot innehåller mallens rotkatalog som används för att återge formuläret.</p> </td>
  </tr>
  <tr>
   <td><p>Data</p> </td>
   <td><p>Data innehåller byte med data som används för att återge formuläret.</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>formDom innehåller DOM för HTML5-formuläret i JSON-format.</p> </td>
  </tr>
  <tr>
   <td><p>packet</p> </td>
   <td><p>Paketet anges som formulär.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir innehåller den felsökningskatalog som används för att återge formuläret.</p> </td>
  </tr>
 </tbody>
</table>

#### Skicka data {#submit-data}

När du klickar på skicka-knappen skickar HTML5-formulär data till servern. I följande tabell visas alla parametrar som HTML5-formulär skickar till servern.

<table>
 <tbody>
  <tr>
   <td><p><strong>Parameter</strong></p> </td>
   <td><p><strong>Beskrivning</strong></p> </td>
  </tr>
  <tr>
   <td><p>Mall</p> </td>
   <td><p>Mall som används för att återge formuläret.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>mallens rotkatalog som används för att återge formuläret.</p> </td>
  </tr>
  <tr>
   <td><p>Data</p> </td>
   <td><p>byte som används för att återge formuläret.</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>DOM för HTML5-formuläret i JSON-format.</p> </td>
  </tr>
  <tr>
   <td><p>underordnad</p> </td>
   <td><p>URL:en där data-XML publiceras.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>Den felsökningskatalog som används för att återge formuläret.</p> </td>
  </tr>
 </tbody>
</table>

#### Hur skicka-proxyn fungerar? {#how-nbsp-the-nbsp-submit-proxy-works}

Skicka-tjänstproxyn fungerar som ett genomströmningsalternativ om det inte finns någon skicka-URL i request-parametern. Det fungerar som en genomströmning. Begäran skickas till slutpunkten för /bin/xfaforms/submit och svaret skickas till XFA-miljön.

Skicka-tjänstproxyn väljer en topologi om den skicka-URL:en finns i request-parametern.

* Om AEM skickar data fungerar proxytjänsten som en vidarekoppling. Begäran skickas till slutpunkten för /bin/xfaforms/submit och svaret skickas till XFA-miljön.
* Om proxyn skickar data, skickas alla parametrar utom submitUrl till */bin/xfaforms/submitAction* slutpunkt och tar emot xml-byte i svarsström. Sedan skickar proxytjänsten data-xml-byte till submitUrl för bearbetning.

* Innan data skickas (begäran om POST) till en server kontrollerar HTML5-formulär serverns anslutning och tillgänglighet. För att verifiera anslutning och tillgänglighet skickar HTML-formulär en tom huvudbegäran till servern. Om servern är tillgänglig skickar HTML5-formuläret data (POST request) till servern. Om servern inte är tillgänglig visas ett felmeddelande *Det gick inte att ansluta till servern,* visas. Avancerad identifiering förhindrar att användarna behöver fylla i formuläret på ett enkelt sätt. Proxyservern hanterar huvudbegäran och genererar inget undantag.
