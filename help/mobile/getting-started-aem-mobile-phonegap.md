---
title: AEM Adobe PhoneGap
description: AEM integreras med PhoneGap så att du enkelt kan skapa appar med AEM sidor. Följ den här sidan för att komma igång med Adobe PhoneGap Enterprise.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

AEM integreras med PhoneGap så att du enkelt kan skapa appar med AEM sidor. Med PhoneGap kan användaren skapa verktygsappar som gör att användarna kan arbeta med innehållet. Med Innehållssynkronisering kan du skapa versionshanterade arkiv med sidor som kan paketeras med appar.

Vanligtvis ansvarar en ***AEM-administratör*** för att lägga till ett nytt program i AEM Mobile-katalogen, antingen genom att skapa ett program med hjälp av guiden Skapa eller genom att importera ett befintligt program.

Härifrån kan en ***AEM författare*** (eller *Marketer*) nu använda färdiga mallar och komponenter för att lägga till och redigera sidor, dra och släppa komponenter och lägga till media av alla typer från DAM, inklusive bilder, videor och textfragment (innehållsfragment).

Den verkliga kraften i AEM Mobile är att en *kunnig* ***AEM utvecklare*** kan utöka och skapa anpassade webbmallar och komponenter för att *AEM författaren* ska kunna skapa snygga och engagerande mobilupplevelser. Dessa mallar och komponenter är inte bara optimerade för mobilappsvärlden utan kommunicerar både med enheten och med AEM server (valfri fjärrserver) till slutpunkter för flerkanalstjänster.

>[!NOTE]
>
>När *AEM Author* tror att appen är klar kan deras intressenter först hämta appen med **[Adobe Verify](/help/mobile/phonegap-mobile-quickstart.md)** (som finns i både AppStore och PlayStore) för granskning och godkännande. När de har fått grönt ljus kan de släppa det nya eller uppdaterade innehållet direkt till sina användare via kontrollpanelen för innehållshantering i AEM Mobile ContentSync. En person kan ta på sig ett valfritt antal roller, det är upp till er och era styrningspolicyer.

## Förutsättningar {#prerequisites}

AEM Mobile är bara en av de två pelarna som utgör den kompletta AEM.

Innan du börjar arbeta med AEM Mobile och följer stegen i den här guiden bör du känna till AEM och AEM Mobile Control Center. Se:

[Komma igång med AEM](/help/sites-deploying/deploy.md)

[En genomgång av AEM Mobile Control Center](/help/mobile/phonegap-authoring-apps.md)

## QuickLinks for Authors {#quicklinks-for-authors}

Läs [Om du skriver för Adobe PhoneGap Enterprise i AEM](/help/mobile/phonegap.md) om du vill veta mer om en författares roller och ansvarsområden.

## QuickLinks for Developers {#quicklinks-for-developers}

Det finns exempelprogram som kan integreras med AEM Mobile och anpassas av utvecklaren. Klicka på [Utveckla Adobe PhoneGap Enterprise med AEM](/help/mobile/developing-in-phonegap.md).

I efterföljande kapitel får du lära dig mer om avancerade koncept som White Labeling you application, Localization, Internationalization, ContentSync, Targeting, Analytics med flera.

## QuickLinks för administratörer {#quicklinks-for-administrators}

Se [Administrera innehåll för Adobe PhoneGap Enterprise med AEM](/help/mobile/administer-phonegap.md) för att konfigurera och hantera ditt mobilprogram.

>[!NOTE]
>
>Med hybridmobilteknologier kan du skapa avancerade mobilappar som *körs offline och online* med AEM Mobile, faktiskt, så många kunder väljer att skapa appar som letar efter när de är online eller offline och beter sig därefter.
