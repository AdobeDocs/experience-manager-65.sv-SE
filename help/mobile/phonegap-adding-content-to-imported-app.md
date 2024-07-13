---
title: Är din hybridapp redo för AEM Mobile?
description: Lär dig mer om hybridappar. En app i Experience Manager är vanligtvis uppdelad i två delar. "shell" och "content" och den här sidan ger mer information om dessa ämnen.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
pagetitle: Is your hybrid app ready for AEM Mobile?
exl-id: 4625890c-2b76-4c78-88e8-23741bc09f5b
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# Är din hybridapp redo för Adobe Experience Manager Mobile?{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Så du har importerat din Hybrid PhoneGap- eller Cordova-app till AEM, nu vad? Du kanske vill lägga till innehåll som är redigerbart i appen. För att kunna utföra den här uppgiften behöver du en allmän förståelse för strukturen i en AEM. En app i AEM delas vanligtvis in i två delar. Gränssnittet och innehållet. Gränssnittet innehåller statiska delar av programmet, t.ex. konfigurationsfilerna för PhoneGap, appramverket och navigeringskontrollerna. Innehållet i det importerade arkivet lagras som en del av skalet. I det här dokumentet är gränssnittet allt icke-AEM innehåll i din Hybrid PhoneGap-app som skapats av apputvecklaren.

Innehåll avser de komponenter, mallar och redigerade sidor som skapas i AEM som skapats av AEM. Innehåll kategoriseras antingen som utvecklarinnehåll eller som redigerat innehåll. Komponenter, designer och sidmallar betraktas som designinnehåll eftersom de har skapats av en utvecklare. Författare är sidor som har byggts med hjälp av komponenter och mallar. Dessa sidor görs vanligtvis av en Designer eller en Marketer.

Om du vill lägga till skapade AEM-sidor i Hybrid-appen måste det finnas en samordning mellan apputvecklaren och AEM. Var som helst i appen där du vill lägga till redigerat innehåll måste apputvecklaren ordna dessa sidor i en struktur som kan läggas över i Experience Manager. Apputvecklaren måste kunna ge utvecklaren av Experience Manager sökvägen till den plats där det Experience Manager-skapade innehållet läggs till. Ange sedan en platshållarsida i Hybrid-appen som ersätts efter att Experience Manager-utvecklaren har skrivit sidinnehållet.

För att göra förklaringen enklare att följa används AEM Experience Cloud: AEM Mobile Hybrid Reference för att förklara begreppen. Hybridreferensappen består av en välkomstsida med en sidomeny.

![chlimage_1-76](assets/chlimage_1-76.png)

I det här exemplet kommer programmets välkomstsida att skapas. Tittar på källan [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). Observera att apputvecklaren har definierat en välkomstsida och angett en mall för sidan som återges av appen. På den här sidan måste apputvecklaren och AEM utvecklare koordinera. Sökvägen till välkomstsidmallen i Hybrid Reference App definieras som &#39;&#39;content/mobileapps/hybrid-reference-app/en/welcome.template.html&#39;&#39;. Den här sökvägen är viktig eftersom AEM utvecklare skapar sin välkomstsida i AEM med samma sökväg.

![chlimage_1-77](assets/chlimage_1-77.png)

Det är viktigt att hybridappen och det AEM innehållet använder samma sökväg eftersom det är beroende av möjligheten att täcka över innehåll med hjälp av Innehållssynkronisering för att lägga till nya sidor i Hybrid-appen. När Hybrid-appen importeras till AEM ställs Content Sync-konfigurationer in som en del av importprocessen.

![chlimage_1-78](assets/chlimage_1-78.png)

När du laddar ned Source från appkontrollpanelen körs dessa ContentSync-skript för att samla ihop ett arkiv av din Hybrid-app.

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync hämtar först&quot;skal&quot; för appen, där allt apputvecklat innehåll från Hybrid-appen lagras. Sedan hämtas programmets innehåll. Om det nu finns sidor i gränssnittet som har samma sökväg som i content, ersätts sidorna under shell med sidorna under content. Om en sida skapas i AEM som har samma sökväg som content/mobileapps/hybrid-reference-app/en/welcome.template.html när ContentSync körs i exemplet med Hybrid-referensappen, kommer den då att täcka över sidan som ingick i Hybrid-referensappen. Det överlappar det som finns AEM på den platsen. Övertäckningen hanteras av ContentSync, så för någon som använder appen ser uppdateringarna av appen med AEM redigerat innehåll sömlöst ut och kräver ingen ombyggnad av appen. Därför visas välkomstsidan så här när du kör programmet:

![chlimage_1-80](assets/chlimage_1-80.png)
