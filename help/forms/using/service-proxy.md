---
title: Tjänstproxy för HTML5-formulär
seo-title: Tjänstproxy för HTML5-formulär
description: Tjänstproxy för HTML5-formulär är en konfiguration som registrerar en proxy för överföringstjänsten. Om du vill konfigurera tjänstproxy anger du URL:en för överföringstjänsten via parametern submitServiceProxy för begäran.
seo-description: Tjänstproxy för HTML5-formulär är en konfiguration som registrerar en proxy för överföringstjänsten. Om du vill konfigurera tjänstproxy anger du URL:en för överföringstjänsten via parametern submitServiceProxy för begäran.
uuid: 42d6c1da-3945-469d-b429-c33e563ed70c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 081f7c17-4e5d-4c7e-a5c3-5541a29b9d55
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---


# Proxy för HTML5-formulärtjänst{#html-forms-service-proxy}

Tjänstproxy för HTML5-formulär är en konfiguration som registrerar en proxy för överföringstjänsten. Om du vill konfigurera tjänstproxy anger du URL:en för överföringstjänsten via parametern request *submitServiceProxy*.

## Fördelar med tjänstproxy {#benefits-of-service-proxy-br}

Tjänstproxyn eliminerar följande:

* Arbetsflödet för HTML5-formulär kräver att skicka in tjänsten &quot;/content/xfaforms/submission/default&quot; för HTML5-formuläranvändarna. Den exponerar AEM servrar för en större, oavsiktlig publik.
* Tjänst-URL:en är inbäddad i formulärets körningsmodell. Det går inte att ändra tjänstens URL-sökväg.
* Inlämningen är en tvåstegsprocess. För att skicka in formulärdata krävs minst två resor till servern. Ökar därmed belastningen på servern.
* HTML5-formulär skickar data i begäran om POST i stället för PDF-begäran. För arbetsflöden som omfattar både PDF- och HTML5-formulär krävs två olika metoder för att bearbeta inskickade data.

### Topologier {#topologies-br}

HTML5-formulär kan använda följande topologier för att ansluta till AEM servrar.

* En topologi där AEM Server- eller HTML5-formulär skickar data via POST till servern.
* En topologi där proxyservern skickar POST till servern.

![Proxytopologier för HTML5-formulärtjänst](assets/topology.png)

Proxytopologier för HTML5-formulärtjänst

HTML5-formulär ansluts till AEM servrar för att köra serverbaserade skript, webbtjänster och överföringar. XFA-miljön för HTML5-formulären använder Ajax-anrop på &quot;/bin/xfaforms/submit&quot;-slutpunkten med olika parametrar för att ansluta till AEM servrar. HTML5-formulär ansluter AEM servrar för att utföra följande åtgärder:

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
* Om proxyn skickar data, skickar proxytjänsten alla parametrar utom submitUrl till slutpunkten */bin/xfaforms/submit* och tar emot xml-byte i svarsströmmen. Sedan skickar proxytjänsten data-xml-byte till submitUrl för bearbetning.

* HTML5-formulär kontrollerar serverns anslutning och tillgänglighet innan de skickar data (begäran om POST) till en server. HTML-formulär skickar en tom huvudbegäran till servern för att verifiera anslutningen och tillgängligheten. Om servern är tillgänglig skickar HTML5-formuläret data (begäran om POST) till servern. Om servern inte är tillgänglig visas ett felmeddelande *Det gick inte att ansluta till servern*. Avancerad identifiering förhindrar att användarna behöver fylla i formuläret på ett enkelt sätt. Proxyservern hanterar huvudbegäran och genererar inget undantag.
