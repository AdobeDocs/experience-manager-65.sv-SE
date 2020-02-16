---
title: Gruppmallar
seo-title: Gruppmallar
description: Åtkomst till konsolen Gruppmallar
seo-description: Åtkomst till konsolen Gruppmallar
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Gruppmallar{#group-templates}

Konsolen Gruppmallar liknar konsolen [Platsmallar](/help/communities/sites.md) . Båda är skisser för en uppsättning färdiga sidor och funktioner som utgör en communitysajt. Skillnaden är att en webbplatsmall är för huvudcommunityn och en gruppmall är för en community-grupp, en undercommunity som är kapslad i huvudcommunityn.

En communitygrupp ingår i en webbplatsmall genom att inkludera funktionen [](/help/communities/functions.md#groups-function) Grupper (som kanske inte är den första eller enda funktionen i mallen).

Från och med [funktionspaket 1](/help/communities/deploy-communities.md#latestfeaturepack)för Communities är det möjligt att kapsla in grupper genom att inkludera funktionen Groups i en gruppmall.

När en åtgärd vidtas för att skapa en ny community-grupp väljs gruppens mall (struktur). Valet beror på hur funktionen Grupper konfigurerades när den lades till i plats- eller gruppmallen.

>[!NOTE]
>
>Konsolerna för att skapa [communitysajter](/help/communities/sites-console.md), [communitymallar](/help/communities/sites.md), mallar [för](/help/communities/tools-groups.md) communitygrupper [och](/help/communities/functions.md) communityfunktionerär endast avsedda att användas i författarmiljön.

## Konsolen Gruppmallar {#group-templates-console}

Så här når du gruppmallskonsolen i AEM Author-miljön:

* Välj **verktyg| Communities| Gruppmallar,** från global navigering.

Den här konsolen visar mallarna som en [communitywebbplats](/help/communities/sites-console.md) kan skapas från och tillåter att nya gruppmallar skapas.

![Mallen Community-grupper](assets/groups-template.png)

## Skapa gruppmall {#create-group-template}

Om du vill börja skapa en ny gruppmall väljer du `Create`

Då öppnas panelen Platsredigeraren som innehåller tre underpaneler:

### Grundläggande information {#basic-info}

![chlimage_1-137](assets/chlimage_1-137.png)

På panelen Grundläggande information konfigureras ett namn, en beskrivning och huruvida mallen är aktiverad eller inaktiverad:

* **Nytt gruppmallsnamn** för mallens namn-ID

* **Beskrivning**

   mallbeskrivningen

* **Handikappade/aktiverade**

   en växlingsväxling som styr om mallen kan refereras

#### Miniatyrbild {#thumbnail}

![chlimage_1-138](assets/chlimage_1-138.png)

(Valfritt) Markera ikonen Överför bild om du vill visa en miniatyrbild tillsammans med namnet och beskrivningen för användare som skapar communitywebbplatser.

#### Struktur {#structure}

>[!CAUTION]
>
>Om du arbetar med AEM 6.1 Communities FP4 eller tidigare ska du inte lägga till någon gruppfunktion i en gruppmall.
>
>Funktionen för kapslade grupper är tillgänglig från och med Communities [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Det är fortfarande inte tillåtet att lägga till en gruppfunktion som den första eller enda funktionen i en mall.

![Gruppmallsredigerare](assets/template-editor.png)

Om du vill lägga till communityfunktioner drar du från höger sida till vänster i den ordning som länkarna på webbplatsmenyn ska visas. Format används på mallen när webbplatsen skapas.

Om du till exempel vill ha ett forum drar du forumfunktionen från biblioteket och släpper under mallverktyget. Detta resulterar i att dialogrutan för forumkonfiguration öppnas. Mer information om konfigurationsdialogrutorna finns i [funktionskonsolen](/help/communities/functions.md) .

Fortsätt dra och släpp av andra communityfunktioner som önskas för en undergruppswebbplats (grupp) som är baserad på den här mallen.

![dragningsfunktioner](assets/dragfunctions.png)

När alla önskade funktioner har släppts i mallbyggarområdet och konfigurerats väljer du **Spara **i det övre högra hörnet.

## Redigera gruppmall {#edit-group-template}

När du visar communitygrupper i huvudkonsolen [](#group-templates-console)Gruppmallar kan du välja en befintlig gruppmall för redigering.

Om du redigerar en gruppmall påverkas inte communitywebbplatser som redan skapats från mallen. Det går att [redigera strukturen för en community-webbplats](/help/communities/sites-console.md#modify-structure)direkt i stället.

I den här processen finns samma paneler som när du [skapar en gruppmall](#create-group-template).
