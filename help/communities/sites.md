---
title: Webbplatsmallar
seo-title: Webbplatsmallar
description: Åtkomst till konsolen Platsmallar
seo-description: Åtkomst till konsolen Platsmallar
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---


# Platsmallar {#site-templates}

Konsolen Webbplatsmallar påminner mycket om konsolen [Gruppmallar](tools-groups.md), som är inriktad på funktioner som är av intresse för communitygrupper.

>[!NOTE]
>
>Konsolerna för att skapa [communitywebbplatser](sites-console.md), [mallar för communitywebbplatser](sites.md), [mallar för communitygrupper](tools-groups.md) och [communityfunktioner](functions.md) får endast användas i författarmiljön.

## Konsol för webbplatsmallar {#site-templates-console}

I författarmiljön kan du nå webbcommunitywebbplatskonsolen:

* Från global navigering: **[!UICONTROL Tools > Communities > Site Templates]**

Den här konsolen visar de mallar från vilka en [community-plats](sites-console.md) kan skapas och tillåter att nya webbplatsmallar skapas.

![site-template](assets/site-template.png)

## Skapa webbplatsmall {#create-site-template}

Om du vill börja skapa en ny platsmall väljer du `Create`.

Då öppnas panelen Platsredigeraren som innehåller tre underpaneler:

### Grundläggande information {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

På panelen Grundläggande information konfigureras ett namn, en beskrivning och huruvida mallen är aktiverad eller inaktiverad:

* **[!UICONTROL Community Site Template Name]**

   Mallens namn-ID.

* **[!UICONTROL Community Site Template Description]**

   Mallbeskrivningen.

* **[!UICONTROL Disabled/Enabled]**

   En växlingsväxling som styr om mallen kan refereras.

### Miniatyrbild {#thumbnail}

![webbplatsminiatyr](assets/site-thumbnail.png)

(Valfritt) Välj ikonen Överför bild om du vill visa en miniatyrbild tillsammans med namnet och beskrivningen för de som skapar communitysajterna.

### Struktur {#structure}

![platsstruktur](assets/site-structure.png)

Om du vill lägga till communityfunktioner drar du från höger sida till vänster i den ordning som länkarna på webbplatsmenyn ska visas. Format används på mallen när webbplatsen skapas.

Om du till exempel vill ha en hemsida drar du funktionen Sida från biblioteket och släpper under mallbyggaren. Detta resulterar i att dialogrutan för sidkonfiguration öppnas. Mer information om konfigurationsdialogrutorna finns i [funktionskonsolen](functions.md).

Fortsätt att dra och släppa andra communityfunktioner som du vill ha för en community-webbplats som baseras på den här mallen.

Sidfunktionen ger en tom sida. Med gruppfunktionen kan du skapa en gruppwebbplats (subcommunity) på communitywebbplatsen.

>[!CAUTION]
>
>Gruppfunktionen får *inte* vara *först eller den enda*-funktionen i platsstrukturen.
>
>Alla andra funktioner, till exempel [sidfunktionen](functions.md#page-function), måste inkluderas och visas först.

![webbplatsredigerare](assets/site-editor.png)

### Gruppmallar för gruppfunktionen {#group-templates-for-groups-function}

När du inkluderar en gruppfunktion i platsmallen, kräver konfigurationen att du anger vilka gruppmallsalternativ som tillåts när en ny grupp skapas i publiceringsmiljön.

>[!CAUTION]
>
>Funktionen Groups får *inte* vara *först eller den enda funktionen* i platsstrukturen.

![platsfunktioner](assets/site-functions.png)

Genom att välja två eller flera mallar för communitygrupper får gruppadministratören välja när en ny grupp faktiskt skapas i communityn.

![site-function](assets/site-functions1.png)

## Redigera webbplatsmall {#edit-site-template}

När du visar platsmallar i huvudkonsolen [Platsmallar](#site-templates-console) går det att välja en befintlig platsmall för redigering.

Den här processen ger samma paneler som [när du skapar en platsmall](#create-site-template).
