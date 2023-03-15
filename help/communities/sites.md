---
title: Webbplatsmallar
seo-title: Site Templates
description: Åtkomst till konsolen Platsmallar
seo-description: How to access the Site Templates console
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
role: Admin
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Webbplatsmallar {#site-templates}

Konsolen Platsmallar liknar [Gruppmallar](tools-groups.md) konsolen, som fokuserar på funktioner av intresse för gemenskapsgrupper.

>[!NOTE]
>
>Konsolerna för att skapa [communitysajter](sites-console.md), [mallar för communitysajter](sites.md), [communitygruppsmallar](tools-groups.md) och [communityfunktioner](functions.md) används endast i författarmiljön.

## Konsol för webbplatsmallar {#site-templates-console}

I författarmiljön kan du nå webbcommunitywebbplatskonsolen:

* Från global navigering: **[!UICONTROL Tools > Communities > Site Templates]**

Den här konsolen visar mallarna från vilka en [communitywebbplats](sites-console.md) kan skapas och tillåter att nya webbplatsmallar skapas.

![site-template](assets/site-template.png)

## Skapa platsmall {#create-site-template}

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

Om du till exempel vill ha en hemsida drar du funktionen Sida från biblioteket och släpper under mallbyggaren. Detta resulterar i att dialogrutan för sidkonfiguration öppnas. Se [function console](functions.md) om du vill ha information om konfigurationsdialogrutorna.

Fortsätt att dra och släppa andra communityfunktioner som du vill ha för en community-webbplats som baseras på den här mallen.

Sidfunktionen ger en tom sida. Med gruppfunktionen kan du skapa en gruppwebbplats (subcommunity) på communitywebbplatsen.

>[!CAUTION]
>
>Funktionen groups måste *not* vara *först eller bara* i platsstrukturen.
>
>Alla andra funktioner, till exempel [sidfunktion](functions.md#page-function), måste inkluderas och listas först.

![webbplatsredigerare](assets/site-editor.png)

### Gruppmallar för gruppfunktion {#group-templates-for-groups-function}

När du inkluderar en gruppfunktion i platsmallen, kräver konfigurationen att du anger vilka gruppmallsalternativ som tillåts när en ny grupp skapas i publiceringsmiljön.

>[!CAUTION]
>
>Funktionen Grupper måste *not* vara *först eller bara* i platsstrukturen.

![platsfunktioner](assets/site-functions.png)

Genom att välja två eller flera mallar för communitygrupper får gruppadministratören välja när en ny grupp faktiskt skapas i communityn.

![site-function](assets/site-functions1.png)

## Redigera webbplatsmall {#edit-site-template}

När du visar webbplatsmallar i huvudmappen [Konsol för webbplatsmallar](#site-templates-console)kan du välja en befintlig platsmall för redigering.

Den här processen ger samma paneler som [skapa en webbplatsmall](#create-site-template).
