---
title: SPA- och serveråtergivning
description: Lär dig mer om SPA och serveråtergivning i Adobe Experience Manager.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: a80bc883-e0f6-4714-bd28-108262f96d77
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 0%

---

# SPA- och serveråtergivning{#spa-and-server-side-rendering}

>[!NOTE]
>
>SPA Editor är den rekommenderade lösningen för projekt som kräver SPA ramverksbaserad klientåtergivning (till exempel React eller Angular).

>[!NOTE]
>
>Adobe Experience Manager (AEM) 6.5.1.0 eller senare krävs för att använda de återgivningsfunktioner på SPA serversidan som beskrivs i det här dokumentet.

## Ökning {#overview}

Single page-applikationer (SPA) kan ge användaren en rik, dynamisk upplevelse som reagerar och beter sig på välbekanta sätt, ofta precis som ett systemspecifikt program. [Detta uppnås genom att klienten förlitar sig på att läsa in innehållet i förväg och sedan göra en grov förbättring av användarinteraktionen](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) och på så sätt minimera mängden kommunikation som krävs mellan klienten och servern, vilket gör appen mer reaktiv.

Detta kan dock leda till längre inledande inläsningstider, särskilt om SPA är stor och har mycket innehåll. För att optimera inläsningstiden kan en del av innehållet återges på serversidan. Med SSR-återgivning (server-side rendering) går sidans initiala belastning snabbare och skickar sedan vidare återgivning till klienten.

## Använd SSR {#when-to-use-ssr}

SSR krävs inte för alla projekt. Även om AEM stöder JS SSR fullt ut för SPA rekommenderar Adobe inte att man implementerar det systematiskt för varje projekt.

När du beslutar dig för att implementera SSR måste du först uppskatta vilken ytterligare komplexitet, insats och kostnad som SSR innebär på ett realistiskt sätt för projektet, inklusive det långsiktiga underhållet. En SSR-arkitektur bör endast väljas när mervärdet klart överstiger de uppskattade kostnaderna.

SSR ger vanligtvis ett visst värde när det finns ett tydligt&quot;ja&quot; till någon av följande frågor:

* **SEO:** Krävs det fortfarande SSR för att din webbplats ska kunna indexeras korrekt av sökmotorer som genererar trafik? Kom ihåg att de viktigaste sökmotorcrawlarna nu utvärderar JS.
* **Sidhastighet:** Ger SSR en mätbar hastighetsförbättring i realtidsmiljöer och förbättrar den övergripande användarupplevelsen?

Endast när minst en av dessa två frågor besvaras med ett tydligt&quot;ja&quot; för ditt projekt rekommenderar Adobe att SSR implementeras. I följande avsnitt beskrivs hur du gör detta med Adobe I/O Runtime.

## Adobe I/O Runtime {#adobe-i-o-runtime}

Om du [ är säker på att ditt projekt kräver implementering av SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr) rekommenderar Adobe att du använder Adobe I/O Runtime.

Mer information om Adobe I/O Runtime finns i:

* [https://developer.adobe.com/runtime/](https://developer.adobe.com/runtime/) - en översikt över tjänsten
* [https://developer.adobe.com/runtime/docs/](https://developer.adobe.com/runtime/docs/) - för detaljerad dokumentation om plattformen

I följande avsnitt beskrivs hur Adobe I/O Runtime kan användas för att implementera SSR för dina SPA i två olika modeller:

* [AEM kommunikationsflöde](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Adobe I/O Runtime-drivet kommunikationsflöde](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe rekommenderar en separat Adobe I/O Runtime-arbetsyta per miljö (stage, prod, testing osv.). Detta möjliggör typiska mönster för systemutvecklingscykler (SDLC) med olika versioner av ett enda program som distribueras till olika miljöer. Mer information finns i dokumentet [CI/CD for Project App Builder Applications](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/).
>
>En separat arbetsyta behövs inte per instans (författare, publicering) såvida det inte finns skillnader i körtidsimplementeringen per instanstyp.

## Fjärrrenderarkonfiguration {#remote-renderer-configuration}

AEM måste veta var det fjärråtergivna innehållet kan hämtas. Oavsett [vilken modell du väljer att implementera för SSR,](#adobe-i-o-runtime), måste du ange hur du ska AEM åtkomst till den här fjärråtergivningstjänsten.

Detta görs via **RemoteContentRenderer - Configuration Factory OSGi-tjänsten**. Sök efter strängen RemoteContentRenderer i webbkonsolens konsol på `http://<host>:<port>/system/console/configMgr`.

![Återgivningskonfiguration](assets/rendererconfig.png)

Följande fält är tillgängliga för konfigurationen:

* **Mönster för innehållssökväg** - Reguljärt uttryck som matchar en del av innehållet, om det behövs
* **URL för fjärrslutpunkt** - URL för slutpunkten som ansvarar för att generera innehållet
   * Använd det säkra HTTPS-protokollet om det inte finns i det lokala nätverket.
* **Ytterligare begärandehuvuden** - Ytterligare huvuden som ska läggas till i begäran som skickas till fjärrslutpunkten
   * Mönster: `key=value`
* **Timeout för begäran** - Timeout för fjärrvärdbegäran i millisekunder

>[!NOTE]
>
>Oavsett om du väljer att implementera det [AEM kommunikationsflödet](#aem-driven-communication-flow) eller det [Adobe I/O Runtime-drivna flödet](#adobe-i-o-runtime-driven-communication-flow) måste du definiera en fjärrkonfiguration för innehållsåtergivning.
>
>Den här konfigurationen måste också definieras om du väljer att [använda en anpassad Node.js-server.](#using-node-js)

>[!NOTE]
>
>Den här konfigurationen använder [Renderer för fjärrinnehåll](#remote-content-renderer), som har ytterligare tillgängliga tillägg och anpassningsalternativ.

## AEM kommunikationsflöde {#aem-driven-communication-flow}

När du använder SSR innehåller [komponentens interaktionsarbetsflöde](/help/sites-developing/spa-overview.md#workflow) för SPA i AEM en fas i vilken det inledande innehållet i appen genereras på Adobe I/O Runtime.

1. Webbläsaren begär SSR-innehåll från AEM.

1. AEM skickar modellen till Adobe I/O Runtime.

1. Adobe I/O Runtime returnerar det genererade innehållet.

1. AEM visar HTML som returneras av Adobe I/O Runtime via HTML-mallen för backend-sidkomponenten.

![serversidesåtergivning-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime-drivet kommunikationsflöde {#adobe-i-o-runtime-driven-communication-flow}

I det föregående avsnittet beskrivs standardimplementeringen och den rekommenderade implementeringen av serversidesåtergivning för SPA i AEM, där AEM utför startsvällning och -visning av innehåll.

Alternativt kan SSR implementeras så att Adobe I/O Runtime ansvarar för startkomponenten, vilket effektivt kan vända kommunikationsflödet.

Båda modellerna är giltiga och stöds av AEM. Man bör dock beakta fördelarna och nackdelarna med var och en av modellerna innan man implementerar en viss modell.

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrap</strong></th>
   <th><strong>Fördelar</strong></th>
   <th><strong>Nackdelar</strong></th>
  </tr>
  <tr>
   <th><strong>via AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM hanterar inmatning av bibliotek där det behövs</li>
     <li>Underhåll endast resurser på AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>SPA utvecklaren<br /> kanske inte känner till </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>via Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>Mer bekant för SPA utvecklare<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Klientlib-resurser som krävs av programmet, t.ex. CSS och JavaScript, måste göras tillgängliga av den AEM utvecklaren via egenskapen <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> <br /> </li>
     <li>Resurserna måste synkroniseras mellan AEM och Adobe I/O Runtime<br /> </li>
     <li>Om du vill aktivera redigering av SPA kan det behövas en proxyserver för Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planering för SSR {#planning-for-ssr}

Endast en del av ett program får återges på serversidan. Det vanliga exemplet är det innehåll som visas ovanför vikningen vid den första inläsningen av sidan återges på serversidan. Detta sparar tid genom att leverera till klienten, som redan har återgett innehåll. När användaren interagerar med SPA återges det extra innehållet av klienten.

När du funderar på att implementera serversidesåtergivning för SPA kan du kontrollera vilka delar av programmet som behövs.

## Utveckla en SPA med SSR {#developing-an-spa-using-ssr}

SPA kan återges av klienten (i webbläsaren) eller serversidan. Webbläsaregenskaper som fönsterstorlek och plats finns inte på den återgivna serversidan. SPA bör därför vara isomorfa, utan att man vet var de kommer att återges.

Om du vill använda SSR distribuerar du koden i AEM och på Adobe I/O Runtime, som ansvarar för återgivningen på serversidan. Den mesta koden blir densamma, men serverspecifika åtgärder är olika.

## SSR för SPA i AEM {#ssr-for-spas-in-aem}

SSR för SPA i AEM kräver Adobe I/O Runtime, vilket krävs för återgivning av programinnehållsserversidan. I programmets HTML anropas en resurs på Adobe I/O Runtime för att återge innehållet.

Precis som AEM stöder ramverken Angular och React SPA direkt, stöds även serversidesrendering för Angular- och React-appar. Mer information finns i NPM-dokumentationen för båda ramverken.

* Reagera: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

Ett enkelt exempel finns i [We.Retail Journal-appen](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal). Det återger hela programserversidan. Även om detta inte är ett verkligt exempel visar det vad som behövs för att implementera SSR.

>[!CAUTION]
>
>Appen [We.Retail Journal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) är endast avsedd som exempel och använder därför Node.js som ett enkelt exempel i stället för den rekommenderade Adobe I/O Runtime. Använd inte det här exemplet för något projektarbete.

>[!NOTE]
>
>Alla AEM ska använda [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html), som har stöd för SPA projekt med React eller Angular och som använder SPA SDK.

## Använda Node.js {#using-node-js}

Adobe I/O Runtime rekommenderas för implementering av SSR för SPA i AEM.

För premesis AEM-instanser är det också möjligt att implementera SSR med en anpassad Node.js-instans på samma sätt som beskrivs ovan. Även om detta stöds av Adobe rekommenderas det inte.

>[!NOTE]
>
>Node.js stöds inte för instanser med värdbaserade AEM i Adobe.

>[!NOTE]
>
>Om SSR måste implementeras via Node.js rekommenderar Adobe en separat Node.js-instans för varje AEM (författare, publicering, scen osv.).

## Renderare för fjärrinnehåll {#remote-content-renderer}

Den [Remote Content Renderer Configuration](#remote-content-renderer-configuration) som krävs för att använda SSR med SPA i AEM finns i en mer generaliserad renderingstjänst som kan utökas och anpassas efter dina behov.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` är en OSGi-tjänst som hämtar innehåll som återges på en fjärrserver, till exempel från Adobe I/O. Innehållet som skickas till fjärrservern baseras på den begärandeparameter som skickas.

`RemoteContentRenderingService` kan injiceras genom beroendeinvertering till antingen en anpassad Sling-modell eller en servlet när ytterligare innehållsmanipulering krävs.

Den här tjänsten används internt av [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

`RemoteContentRendererRequestHandlerServlet` kan användas för att ställa in konfigurationen för begäran programmatiskt. `DefaultRemoteContentRendererRequestHandlerImpl`, den angivna standardimplementeringen av begäranhanteraren, gör att du kan skapa flera OSGi-konfigurationer för att mappa en plats i innehållsstrukturen till en fjärrslutpunkt.

Implementera gränssnittet `RemoteContentRendererRequestHandler` om du vill lägga till en anpassad begärandehanterare. Se till att du ställer in `Constants.SERVICE_RANKING`-komponentegenskapen på ett heltal som är högre än 100, vilket är rankningen för `DefaultRemoteContentRendererRequestHandlerImpl`.

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Konfigurera OSGi-konfigurationen för standardhanteraren {#configure-default-handler}

Konfigurationen av standardhanteraren måste konfigureras enligt beskrivningen i avsnittet [Konfiguration av fjärrinnehållsrenderare](#remote-content-renderer-configuration).

### Användning av fjärråtergivning av innehåll {#usage}

Så här hämtar du en servlet och returnerar innehåll som kan injiceras på sidan:

1. Kontrollera att fjärrservern är tillgänglig.
1. Lägg till ett av följande kodfragment i HTML-mallen för en AEM.
1. Du kan också skapa eller ändra OSGi-konfigurationerna.
1. Bläddra i webbplatsens innehåll

Vanligtvis är HTML-mallen för en sidkomponent huvudmottagaren för en sådan funktion.

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Krav {#requirements}

Servlets använder Sling Model Exporter för att serialisera komponentdata. Som standard stöds både `com.adobe.cq.export.json.ContainerExporter` och `com.adobe.cq.export.json.ComponentExporter` som Sling Model-kort. Om det behövs kan du lägga till klasser som begäran ska anpassas till med `RemoteContentRendererServlet` och implementera `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. De ytterligare klasserna måste utöka `ComponentExporter`.
