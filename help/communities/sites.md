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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Webbplatsmallar {#site-templates}

Konsolen Platsmallar liknar konsolen [Gruppmallar](tools-groups.md) , som är inriktad på funktioner som är av intresse för communitygrupper.

>[!NOTE]
>
>Konsolerna för att skapa [communitysajter](sites-console.md), [communitymallar](sites.md), mallar [för](tools-groups.md) communitygrupper [och](functions.md) communityfunktionerär endast avsedda att användas i författarmiljön.

## Konsol för webbplatsmallar {#site-templates-console}

För att nå webbcommunitywebbplatskonsolen i redigeringsmiljön

* Från global navigering: **[!UICONTROL Verktyg > Communities > Site Templates]**

Den här konsolen visar mallarna som en [community](sites-console.md) kan skapas från och som gör att nya webbplatsmallar kan skapas.

![chlimage_1-18](assets/chlimage_1-18.png)

## Skapa platsmall {#create-site-template}

Om du vill börja skapa en ny platsmall väljer du `Create`.

Då öppnas panelen Platsredigeraren som innehåller tre underpaneler:

### Grundläggande information {#basic-info}

![chlimage_1-19](assets/chlimage_1-19.png)

På panelen Grundläggande information konfigureras ett namn, en beskrivning och huruvida mallen är aktiverad eller inaktiverad:

* **[!UICONTROL Mallnamn]** för community-webbplats Mallens namn-ID

* **[!UICONTROL Beskrivning]** av communityplatsmall

* **[!UICONTROL Inaktiverad/aktiverad]** En växlingsväxling som styr om mallen kan refereras

### Miniatyrbild {#thumbnail}

![chlimage_1-20](assets/chlimage_1-20.png)

(Valfritt) Välj ikonen Överför bild om du vill visa en miniatyrbild tillsammans med namnet och beskrivningen för de som skapar communitysajterna.

### Struktur {#structure}

![chlimage_1-21](assets/chlimage_1-21.png)

Om du vill lägga till communityfunktioner drar du från höger sida till vänster i den ordning som länkarna på webbplatsmenyn ska visas. Format används på mallen när webbplatsen skapas.

Om du till exempel vill ha en hemsida drar du funktionen Sida från biblioteket och släpper under mallbyggaren. Detta resulterar i att dialogrutan för sidkonfiguration öppnas. Mer information om konfigurationsdialogrutorna finns i [funktionskonsolen](functions.md) .

Fortsätt att dra och släppa andra communityfunktioner som du vill ha för en community-webbplats som baseras på den här mallen.

Sidfunktionen ger en tom sida. Med gruppfunktionen kan du skapa en gruppwebbplats (subcommunity) på communitywebbplatsen.

>[!CAUTION]
>
>Gruppfunktionen får *inte* vara den *första eller enda* funktionen i platsstrukturen.
>
>Alla andra funktioner, till exempel [sidfunktionen](functions.md#page-function), måste inkluderas och listas först.

![chlimage_1-22](assets/chlimage_1-22.png)

### Gruppmallar för gruppfunktion {#group-templates-for-groups-function}

När du inkluderar en gruppfunktion i platsmallen, kräver konfigurationen att du anger vilka gruppmallsalternativ som tillåts när en ny grupp skapas i publiceringsmiljön.

>[!CAUTION]
>
>Funktionen Grupper får *inte* vara den *första eller enda* funktionen i platsstrukturen.

![chlimage_1-23](assets/chlimage_1-23.png)

Genom att välja två eller flera mallar för communitygrupper får gruppadministratören välja när en ny grupp faktiskt skapas i communityn.

![chlimage_1-24](assets/chlimage_1-24.png)

## Redigera webbplatsmall {#edit-site-template}

När du visar platsmallar i huvudkonsolen [för](#site-templates-console)platsmallar kan du välja en befintlig platsmall för redigering.

I den här processen finns samma paneler som när du [skapar en platsmall](#create-site-template).
