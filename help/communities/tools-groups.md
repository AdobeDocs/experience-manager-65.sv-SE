---
title: Gruppmallar
seo-title: Group Templates
description: Åtkomst till konsolen Gruppmallar
seo-description: How to access the Group Templates console
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# Gruppmallar {#group-templates}

Konsolen Gruppmallar liknar konsolen [Webbplatsmallar](/help/communities/sites.md) konsol. Båda är skisser för en uppsättning färdiga sidor och funktioner som utgör en communitysajt. Skillnaden är att en webbplatsmall är för huvudcommunityn och en gruppmall är för en community-grupp, en undercommunity som är kapslad i huvudcommunityn.

En community-grupp ingår i en webbplatsmall genom att inkludera [Funktionen Grupper](/help/communities/functions.md#groups-function) (som inte får vara den första eller enda funktionen i mallen).

Från och med Communities [funktionspaket 1](/help/communities/deploy-communities.md#latestfeaturepack)kan du kapsla in grupper genom att inkludera funktionen Grupper i en gruppmall.

När en åtgärd vidtas för att skapa en ny community-grupp väljs gruppens mall (struktur). Valet beror på hur funktionen Grupper konfigurerades när den lades till i plats- eller gruppmallen.

>[!NOTE]
>
>Konsolerna för att skapa [communitysajter](/help/communities/sites-console.md), [mallar för communitysajter](/help/communities/sites.md), [communitygruppsmallar](/help/communities/tools-groups.md) och [communityfunktioner](/help/communities/functions.md) används endast i författarmiljön.

## Konsolen Gruppmallar {#group-templates-console}

Så här når du gruppmallskonsolen i AEM Author-miljön:

* Välj **verktyg | Communities | Gruppmallar,** från global navigering.

Den här konsolen visar mallarna från vilka en [communitywebbplats](/help/communities/sites-console.md) kan skapas och tillåter att nya gruppmallar skapas.

![Mallen Community-grupper](assets/groups-template.png)

## Skapa gruppmall {#create-group-template}

Om du vill börja skapa en ny gruppmall väljer du `Create`.

Då öppnas panelen Platsredigeraren som innehåller tre underpaneler:

### Grundläggande information {#basic-info}

![site-basic-info](assets/site-basic-info.png)

På panelen Grundläggande information konfigureras ett namn, en beskrivning och huruvida mallen är aktiverad eller inaktiverad:

* **Nytt gruppmallsnamn**

   Mallens namn-ID.

* **Beskrivning**

   Mallbeskrivningen.

* **Handikappade/aktiverade**

   En växlingsväxling som styr om mallen kan refereras.

#### Miniatyrbild {#thumbnail}

![webbplatsminiatyr](assets/site-thumbnail.png)

(Valfritt) Markera ikonen Överför bild om du vill visa en miniatyrbild tillsammans med namnet och beskrivningen för användare som skapar communitywebbplatser.

#### Struktur {#structure}

>[!CAUTION]
>
>Om du arbetar med AEM 6.1 Communities FP4 eller tidigare ska du inte lägga till en gruppfunktion i en gruppmall.
>
>Funktionen för kapslade grupper är tillgänglig från och med Communities [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Det är fortfarande inte tillåtet att lägga till en gruppfunktion som den första eller enda funktionen i en mall.

![Gruppmallsredigerare](assets/template-editor.png)

Om du vill lägga till communityfunktioner drar du från höger sida till vänster i den ordning som länkarna på webbplatsmenyn ska visas. Format används på mallen när webbplatsen skapas.

Om du till exempel vill ha ett forum drar du forumfunktionen från biblioteket och släpper under mallverktyget. Detta resulterar i att dialogrutan för forumkonfiguration öppnas. Se [function console](/help/communities/functions.md) om du vill ha information om konfigurationsdialogrutorna.

Fortsätt dra och släpp av andra communityfunktioner som önskas för en undergruppswebbplats (grupp) som är baserad på den här mallen.

![dragningsfunktioner](assets/dragfunctions.png)

När alla önskade funktioner har släppts i mallbyggarområdet och konfigurerats väljer du **Spara** i det övre högra hörnet.

## Redigera gruppmall {#edit-group-template}

När du visar communitygrupper i huvudgruppen [Konsolen Gruppmallar](#group-templates-console)kan du välja en befintlig gruppmall för redigering.

Om du redigerar en gruppmall påverkas inte communitywebbplatser som redan skapats från mallen. Det går att direkt [redigera en communitywebbplats](/help/communities/sites-console.md#modify-structure)i stället.

Den här processen ger samma paneler som [skapa en gruppmall](#create-group-template).
