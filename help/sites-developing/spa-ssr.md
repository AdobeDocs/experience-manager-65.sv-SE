---
title: SPA och serversidesrendering
seo-title: SPA och serversidesrendering
description: 'null'
seo-description: 'null'
uuid: 27e26e3f-65d4-4069-b570-58b8b9e2a1ae
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 844e5c96-2a18-4869-b4c8-2fb9efe0332a
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPA och serversidesrendering{#spa-and-server-side-rendering}

>[!NOTE]
>
>SPA-redigeraren är den rekommenderade lösningen för projekt som kräver SPA-ramverksbaserad rendering på klientsidan (t.ex. React eller Angular).

>[!NOTE]
>
>AEM 6.5.1.0 eller senare krävs för att återgivningsfunktionerna på SPA-serversidan ska kunna användas enligt beskrivningen i det här dokumentet.

## Översikt {#overview}

Single-page-applikationer (SPA) kan ge användaren en rik, dynamisk upplevelse som reagerar och beter sig på välbekanta sätt, ofta precis som ett systemspecifikt program. [Detta uppnås genom att kunden förlitar sig på att läsa in innehållet i förväg och sedan göra en reaktiv hantering av användarinteraktionen](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) och på så sätt minimera mängden kommunikation som krävs mellan klienten och servern.

Detta kan dock leda till längre inledande inläsningstider, särskilt om SPA-filen är stor och har mycket innehåll. För att optimera inläsningstiden kan en del av innehållet återges på serversidan. Serversidorendering (SSR) kan snabba upp den initiala inläsningen av sidan och sedan överföra ytterligare återgivning till klienten.

## När SSR ska användas {#when-to-use-ssr}

SSR krävs inte för alla projekt. Även om AEM helt stöder JS SSR för SPA rekommenderar Adobe inte att man implementerar det systematiskt för varje projekt.

När du beslutar dig för att implementera SSR måste du först uppskatta vilken ytterligare komplexitet, insats och kostnad som SSR innebär på ett realistiskt sätt för projektet, inklusive det långsiktiga underhållet. En SSR-arkitektur bör endast väljas när mervärdet klart överstiger de uppskattade kostnaderna.

SSR ger vanligtvis ett visst värde när det finns ett tydligt&quot;ja&quot; till någon av följande frågor:

* **** SEO: Krävs det fortfarande SSR för att webbplatsen ska kunna indexeras korrekt av sökmotorer som genererar trafik? Kom ihåg att de viktigaste sökmotorcrawlarna nu utvärderar JS.
* **** Sidhastighet: Ger SSR en mätbar hastighetsförbättring i realtidsmiljöer och ökar den övergripande användarupplevelsen?

Adobe rekommenderar att SSR implementeras endast när minst en av dessa två frågor besvaras med ett tydligt ja för ditt projekt. I följande avsnitt beskrivs hur du gör detta med Adobe I/O Runtime.

## Adobe I/O Runtime {#adobe-i-o-runtime}

Om du [är säker på att ditt projekt kräver SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr)rekommenderar vi att du använder Adobe I/O Runtime.

Mer information om Adobe I/O Runtime finns på

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) - en översikt över tjänsten
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) - för detaljerad dokumentation om plattformen

I följande avsnitt beskrivs hur Adobe I/O Runtime kan användas för att implementera SSR för SPA i två olika modeller:

* [AEM-drivet kommunikationsflöde](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Adobe I/O Runtime-driven Communication Flow](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe rekommenderar en separat instans av Adobe I/O Runtime för varje AEM-miljö (författare, publicering, scen osv.).

## AEM-drivet kommunikationsflöde {#aem-driven-communication-flow}

När du använder SSR innehåller [komponentens arbetsflöde](/help/sites-developing/spa-overview.md#workflow) för SPA i AEM en fas i vilken det inledande innehållet i appen genereras i Adobe I/O Runtime.

1. Webbläsaren begär SSR-innehåll från AEM.

1. AEM skickar modellen till Adobe I/O Runtime.

1. Adobe I/O Runtime returnerar det genererade innehållet.

1. AEM skickar den HTML som returneras av Adobe I/O Runtime via HTML-mallen för backend-sidkomponenten.

![serverside-rendering-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime-driven Communication Flow {#adobe-i-o-runtime-driven-communication-flow}

I föregående avsnitt beskrivs standardimplementeringen och den rekommenderade implementeringen av serversidesrendering med avseende på SPA i AEM, där AEM utför start- och serverdelningens av innehåll.

Alternativt kan SSR implementeras så att Adobe I/O Runtime är ansvarig för startkomponenten och effektivt kan vända kommunikationsflödet.

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
     <li>AEM hanterar vid behov inmatning av bibliotek</li>
     <li>Resurserna behöver bara underhållas på AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Inte bekant för SPA-utvecklare<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>via Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>Mer bekant för SPA-utvecklare<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Klientlib-resurser som krävs av programmet, t.ex. CSS och JavaScript, måste göras tillgängliga av AEM-utvecklaren via <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> egenskapen<br /> </li>
     <li>Resurserna måste synkroniseras mellan AEM och Adobe I/O Runtime<br /> </li>
     <li>Om du vill aktivera redigering av SPA kan det behövas en proxyserver för Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planering för SSR {#planning-for-ssr}

I allmänhet behöver bara en del av ett program återges på serversidan. Det vanliga exemplet är det innehåll som ska visas ovanför vikningen vid den första inläsningen av sidan återges på serversidan. Detta sparar tid genom att leverera till klienten, som redan har återgett innehåll. När användaren interagerar med SPA återges det extra innehållet av klienten.

När du funderar på att implementera serversidorendering för ditt SPA måste du kontrollera vilka delar av programmet som det är nödvändigt för.

## Utveckla en SPA med SSR {#developing-an-spa-using-ssr}

SPA-komponenter kan återges av klienten (i webbläsaren) eller serversidan. Webbläsaregenskaper som fönsterstorlek och plats finns inte på den återgivna serversidan. Därför bör SPA-komponenterna vara isomorfiska, utan att förutsäga var de kommer att återges.

För att kunna utnyttja SSR måste du driftsätta koden i både AEM och i Adobe I/O Runtime, som ansvarar för återgivningen på serversidan. Den mesta koden blir densamma, men serverspecifika åtgärder skiljer sig åt.

## SSR för SPA i AEM {#ssr-for-spas-in-aem}

SSR för SPA i AEM kräver Adobe I/O Runtime, vilket krävs för återgivning av programinnehållsserversidan. I programmets HTML anropas en resurs i Adobe I/O Runtime för att återge innehållet.

På samma sätt som AEM stöder ramverken för vinkelrät och React SPA direkt, stöds även serversidesrendering för appar med vinkelrät och React. Mer information finns i NPM-dokumentationen för båda ramverken.

* Reagera: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Vinkel: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

Ett enkelt exempel finns i appen [](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)We.Retail Journal. Det återger hela programserversidan. Även om detta inte är ett verkligt exempel visar det vad som behövs för att implementera SSR.

>[!CAUTION]
>
>Appen [](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) We.Retail Journal är endast avsedd som exempel och använder därför Node.js som ett enkelt exempel i stället för den rekommenderade Adobe I/O Runtime-modulen. Det här exemplet ska inte användas för något projektarbete.

>[!NOTE]
>
>Alla SPA-projekt på AEM bör baseras på [Maven Archetype för SPA Starter Kit](https://github.com/adobe/aem-spa-project-archetype).

## Använda Node.js {#using-node-js}

Adobe I/O Runtime rekommenderas för implementering av SSR för SPA i AEM.

För AEM-instanser på premesis är det också möjligt att implementera SSR med en anpassad Node.js-instans på samma sätt som beskrivs ovan. Även om Adobe stöder detta rekommenderar vi inte det.

>[!NOTE]
>
>Node.js stöds inte för Adobe-värdbaserade AEM-instanser.

>[!NOTE]
>
>Om SSR måste implementeras via Node.js rekommenderar Adobe en separat Node.js-instans för varje AEM-miljö (författare, publicering, scen osv.).
