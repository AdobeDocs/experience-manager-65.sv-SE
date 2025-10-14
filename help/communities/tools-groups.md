---
title: Gruppmallar
description: Lär dig hur du kommer åt konsolen Gruppmallar för en uppsättning förkopplade sidor och funktioner som utgör en communityplats.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# Gruppmallar {#group-templates}

Konsolen Gruppmallar liknar konsolen [Platsmallar](/help/communities/sites.md). Båda är skisser för en uppsättning färdiga sidor och funktioner som utgör en communitysajt. Skillnaden är att en webbplatsmall är för huvudcommunityn och en gruppmall är för en community-grupp, en undercommunity som är kapslad i huvudcommunityn.

En communitygrupp ingår i en webbplatsmall genom att inkludera funktionen [Grupper](/help/communities/functions.md#groups-function) (som inte är den första eller enda funktionen i mallen).

Från och med [funktionspaketet &#x200B;](/help/communities/deploy-communities.md#latestfeaturepack) för Communities är det möjligt att kapsla grupper genom att inkludera funktionen Groups i en gruppmall.

När en åtgärd vidtas för att skapa en community-grupp väljs gruppens mall (struktur). Valet beror på hur funktionen Grupper konfigurerades när den lades till i plats- eller gruppmallen.

>[!NOTE]
>
>Konsolerna för att skapa [communitywebbplatser](/help/communities/sites-console.md), [mallar för communitywebbplatser](/help/communities/sites.md), [mallar för communitygrupper](/help/communities/tools-groups.md) och [communityfunktioner](/help/communities/functions.md) är endast avsedda att användas i författarmiljön.

## Konsolen Gruppmallar {#group-templates-console}

Så här når du konsolen för gruppmallar i AEM författarmiljö:

* Välj **verktyg | Communities | Gruppmallar,** från global navigering.

Den här konsolen visar de mallar från vilka en [community-plats](/help/communities/sites-console.md) kan skapas och tillåter att nya gruppmallar skapas.

![Mallen Community-grupper](assets/groups-template.png)

## Skapa gruppmall {#create-group-template}

Om du vill börja skapa en gruppmall väljer du `Create`.

Då öppnas panelen Webbplatsredigeraren som innehåller tre underpaneler:

### Grundläggande information {#basic-info}

![site-basic-info](assets/site-basic-info.png)

På panelen Grundläggande information konfigureras ett namn, en beskrivning och huruvida mallen är aktiverad eller inaktiverad:

* **Nytt gruppmallsnamn**

  Mallens namn-ID.

* **Beskrivning**

  Mallbeskrivningen.

* **Inaktiverad/aktiverad**

  En växlingsväxling som styr om mallen kan refereras.

#### Miniatyrbild {#thumbnail}

![platsens miniatyrbild](assets/site-thumbnail.png)

(Valfritt) Markera ikonen Överför bild om du vill visa en miniatyrbild tillsammans med namnet och beskrivningen för användare som skapar communitywebbplatser.

#### Struktur {#structure}

>[!CAUTION]
>
>Om du arbetar med AEM 6.1 Communities FP4 eller tidigare ska du inte lägga till en gruppfunktion i en gruppmall.
>
>Funktionen för kapslade grupper är tillgänglig från och med Communities [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Det är fortfarande inte tillåtet att lägga till en gruppfunktion som den första eller enda funktionen i en mall.

![Gruppmallsredigeraren](assets/template-editor.png)

Om du vill lägga till communityfunktioner drar du från höger sida till vänster i den ordning som länkarna på webbplatsmenyn ska visas. Format används på mallen när webbplatsen skapas.

Om du till exempel vill ha ett forum drar du forumfunktionen från biblioteket och släpper under mallverktyget. Detta resulterar i att dialogrutan för forumkonfiguration öppnas. Mer information om konfigurationsdialogrutorna finns i [funktionskonsolen](/help/communities/functions.md).

Fortsätt dra och släpp av andra communityfunktioner som du vill använda för en undercommunity-webbplats (grupp) som baseras på den här mallen.

![dra-funktioner](assets/dragfunctions.png)

När alla önskade funktioner har släppts i mallbyggarområdet och konfigurerats väljer du **Spara** i det övre högra hörnet.

## Redigera gruppmall {#edit-group-template}

När du visar communitygrupper i huvudkonsolen [Gruppmallar](#group-templates-console) går det att välja en befintlig gruppmall för redigering.

När du redigerar en gruppmall påverkas inte communitysajter som redan skapats från mallen. Det går att direkt [redigera strukturen för en community-webbplats](/help/communities/sites-console.md#modify-structure) i stället.

Den här processen innehåller samma paneler som [skapar en gruppmall](#create-group-template).
