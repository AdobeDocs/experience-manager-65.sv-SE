---
title: Projekt
seo-title: Projects
description: Med projekt kan du gruppera resurser i en enhet vars gemensamma, delade miljö gör det enkelt att hantera dina projekt.
seo-description: Projects let you group resources into one entity whose common, shared environment makes it easy to manage your projects
uuid: 4b5b9d78-d515-46af-abe2-882da0a1c8ae
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: dee7ac7c-ca86-48e9-8d95-7826fa926c68
docset: aem65
exl-id: 632c0608-2ab8-4a5b-8251-cd747535449b
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 5%

---


# Projekt {#projects}

Med projekt kan du gruppera resurser i en enhet. En gemensam, delad miljö gör det enkelt att hantera projekt. De typer av resurser som du kan associera med ett projekt kallas för Plattor i AEM. Rutorna kan innehålla projekt- och teaminformation, resurser, arbetsflöden och andra typer av information, vilket beskrivs i detalj i [Projektpaneler.](#project-tiles)

Som användare kan du:

* Skapa och ta bort projekt
* Koppla innehåll- och resursmappar till ett projekt
* Ta bort innehållslänkar från projekt

## Åtkomstkrav {#access-requirements}

Projicerar en AEM standardfunktion och kräver ingen ytterligare konfiguration.

Men för användare i projekt som vill se andra användare/grupper medan de använder projekt, till exempel när de skapar projekt, skapar uppgifter/arbetsflöden eller visar och hanterar teamet, måste de användarna ha läsåtkomst på `/home/users` och `/home/groups`.

Det enklaste sättet är att ge **projekt-användare** gruppläsåtkomst till `/home/users` och `/home/groups`.

## Projektkonsol {#projects-console}

Projektkonsolen är den plats där du får åtkomst till och hanterar dina projekt i AEM.

![Projektkonsolen](assets/screen-shot_2019-03-05at125110.png)

Projektkonsolen liknar andra konsoler i AEM, ger möjlighet till ett antal åtgärder i enskilda projekt samt att justera visningen av projekten.

### Växla läge {#modes}

Du kan använda spårväljaren för att ändra mellan konsollägen.

![Järnvägsväljare](assets/projects-rail.png)

#### Endast innehåll {#content-only}

Endast innehåll är standardläge när konsolen öppnas. Den visar alla dina projekt.

#### Tidslinje {#timeline}

I tidslinjevyn kan du välja ett enskilt projekt och visa aktiviteten på det. Använda järnvägsväljaren eller snabbtangenten `alt+1` om du vill ändra till den här vyn.

![Tidslinjeläge](assets/project-timeline.png)

### Växla vy {#views}

Du kan använda vyväljaren för att ändra mellan att visa projekt som stora rutor (standard), för att visa dem som en lista eller i en kalender.

![Vyer](assets/projects-views.png)

### Filtrera din vy {#filter}

Du kan använda filtret för att växla mellan alla projekt och endast de som är aktiva.

![Filter](assets/projects-filter.png)

### Välja och visa projekt {#selecting}

Välj ett projekt genom att hålla muspekaren över projektrutan och klicka på bockmarkeringen.

Visa detaljerna för ett projekt genom att klicka på det för att detaljgranska det.

### Skapa nya projekt {#creating}

Klicka **Skapa** för att lägga till ett nytt projekt.

## Projektpaneler {#project-tiles}

Projekt består av olika typer av information som du vill hantera tillsammans. Informationen representeras av olika **Plattor**.

Du kan associera följande rutor med ditt projekt.

* [Assets](#assets)
* [Resurssamlingar](#asset-collections)
* [Erfarenheter](#experiences)
* [Länkar](#links)
* [Projektinformation](#project-info)
* [Team](#team)
* [Landningssidor](#landing-pages)
* [E-post](#emails)
* [Arbetsflöden](#workflows)
* [Launches](#launches)
* [Uppgifter](#tasks)

Klicka på den nedrullningsbara menyn i det övre högra hörnet av en ruta för att lägga till mer data i rutan.

Klicka på ellipsknappen längst ned till höger i en ruta för att öppna rutans data i dess associerade konsol.

### Assets {#assets}

I **Resurser** kan du samla alla resurser som du använder för ett visst projekt.

![Resurspanel](assets/project-tile-assets.png)

Du överför resurser direkt i rutan.

### Resurssamlingar {#asset-collections}

Precis som resurser kan du lägga till [resurssamlingar](/help/assets/manage-collections.md) direkt till projektet. Du definierar samlingar i Resurser.

![Resurssamlingsplatta](assets/project-tile-asset-collection.png)

Lägg till en samling genom att klicka på **Lägg till samling** och välja önskad samling i listan.

### Erfarenheter {#experiences}

The **Erfarenheter** kan du lägga till en mobilapp, en webbplats eller en publikation i projektet.

![Erfarenheter](assets/project-tile-experiences.png)

Ikonerna anger vilken typ av upplevelse som visas.

* Webbplats
* Mobilapplikation

### Länkar {#links}

The **Länkar** kan du koppla externa länkar till projektet.

![Länkplatta](assets/project-tile-links.png)

Du kan namnge länken med ett lättkänt namn och ändra miniatyrbilden.

### Projektinformation {#project-info}

The **Projektinformation** panel ger allmän information om projektet, inklusive en beskrivning, projektstatus (inaktiv eller aktiv), ett förfallodatum och medlemmar. Dessutom kan du lägga till en projektminiatyr, som visas på huvudprojektsidan.

![Projektinformationsruta](assets/project-tile-info.png)

### Översättningsjobb {#translation-job}

The **Översättningsjobb** Där du börjar en översättning och där du ser status för dina översättningar.

![Översättningsjobbpanel](assets/project-tile-translation.png)

Information om hur du konfigurerar översättningen finns i dokumentet [Skapa översättningsprojekt.](/help/assets/translation-projects.md)

### Team {#team}

I den här rutan kan du ange medlemmarna i projektteamet. När du redigerar kan du ange namnet på teammedlemmen och tilldela användarrollen.

![Teampanel](assets/project-tile-team.png)

Du kan lägga till och ta bort teammedlemmar från teamet. Dessutom kan du redigera [användarroll](#userroles) som tilldelats teammedlemmen.

### Landningssidor {#landing-pages}

The **Landningssidor** kan du begära en ny landningssida.

![Landing page tile](assets/project-tile-landing.png)

Arbetsflödet beskrivs i dokumentet[Skapa ett arbetsflöde för landningssida.](/help/sites-authoring/projects-with-workflows.md#request-landing-page-workflow)

### E-post {#emails}

The **E-post** hjälper dig att hantera e-postförfrågningar. Det börjar med **Begär e-post** arbetsflöde.

![E-postpanel](assets/project-tile-email.png)

Mer information finns i [Begär e-postarbetsflöde.](/help/sites-authoring/projects-with-workflows.md#request-email-workflow)

### Arbetsflöden {#workflows}

Du kan starta arbetsflöden för ditt projekt. Om något arbetsflöde körs visas deras status i **Arbetsflöden** platta.

![Arbetsflödespanel](assets/project-tile-workflows.png)

Beroende på vilket projekt du skapar finns det olika arbetsflöden tillgängliga.

Dessa beskrivs i [Arbeta med projektarbetsflöden.](/help/sites-authoring/projects-with-workflows.md)

### Launches {#launches}

The **Startar** visas alla starter som har begärts med en [Begär startarbetsflöde.](/help/sites-authoring/projects-with-workflows.md)

![Startar panel](assets/project-tile-launches.png)

### Uppgifter {#tasks}

Med uppgifter kan du övervaka status för projektrelaterade uppgifter, inklusive arbetsflöden. Uppgifterna behandlas i detalj på [Arbeta med uppgifter](/help/sites-authoring/task-content.md).

![Aktivitetspanelen](assets/project-tile-tasks.png)

## Projektmallar {#project-templates}

Mallar är grunden för ditt projekt. AEM innehåller dessa standardprojektmallar.

* **Medieprojekt** - Detta är ett referensexempelprojekt för medierelaterade aktiviteter. Den innehåller flera medierelaterade projektroller och innehåller även arbetsflöden för medieinnehåll.
* **[Fotoprojekt för produkt](/help/sites-authoring/managing-product-information.md)** - Det här är ett referensexempel för hantering av e-handelsrelaterade produktfotografier.
* **[Översättningsprojekt](/help/sites-administering/translation.md)** - Det här är ett referensexempel för hantering av översättningsrelaterade aktiviteter. Det innehåller grundläggande roller och arbetsflöden för hantering av översättning.
* **Enkelt projekt** - Det här är ett referensexempel för projekt som inte passar in i andra kategorier. Det innehåller tre grundläggande roller och fyra allmänna AEM arbetsflöden.

Beroende på vilken mall du väljer kan du välja mellan olika alternativ i projektet, t.ex. användarroller och arbetsflöden.

## Användarroller i ett projekt {#user-roles-in-a-project}

De olika användarrollerna definieras i projektmallen och används av två primära orsaker:

1. Behörigheter: Användarrollerna tillhör en av de tre kategorier som visas: observatör, redigerare, ägare. En fotograf eller copywriter har till exempel samma behörighet som en redigerare. Behörigheterna avgör vad en användare kan göra med innehållet i ett projekt.
1. Arbetsflöden: Arbetsflödena avgör vem som tilldelas uppgifter i ett projekt. Uppgifterna kan associeras med en projektroll. En uppgift kan t.ex. tilldelas fotografer så att alla gruppmedlemmar som har rollen fotograf får uppgiften.

Alla projekt har stöd för följande standardroller så att du kan administrera säkerhets- och kontrollbehörigheter.

| Roll | Beskrivning | Behörigheter | Gruppmedlemskap |
|---|---|---|---|
| Observer | En användare i den här rollen kan visa projektinformation, inklusive projektstatus. | Skrivskyddade behörigheter i ett projekt | `workflow-users` grupp |
| Redigerare | En användare med den här rollen kan överföra och redigera innehållet i ett projekt. | Läs- och skrivåtkomst för ett projekt, tillhörande metadata och relaterade resurser<br>Behörigheter att ladda upp en tagningslista, fotografera samt granska och godkänna material<br>Skrivbehörighet för `/etc/commerce`<br>Ändra behörighet för ett visst projekt | `workflow-users` grupp |
| Ägare | En användare med den här rollen kan skapa ett projekt, initiera arbete i ett projekt och flytta godkända resurser till produktionsmappen. Alla andra uppgifter i projektet kan också visas och utföras av ägaren. | Skrivbehörighet för `/etc/commerce` | `dam-users` grupp för att kunna skapa ett projekt<br>`project-administrators` grupp för att kunna skapa ett projekt och flytta resurser |

För kreativa projekt finns även andra roller, som fotografer. Du kan använda de här rollerna för att skapa anpassade roller för ett visst projekt.

### Skapa grupp automatiskt {#auto-group-creation}

När du skapar projektet och lägger till användare för de olika rollerna skapas grupper som är kopplade till projektet automatiskt för att hantera associerade behörigheter.

Ett projekt med namnet Myproject skulle till exempel ha tre grupper, **Myproject Owners**, **Myproject Editors** och **Myproject Observers**.

Om projektet tas bort tas dessa grupper bara bort om du väljer lämpligt alternativ [när du tar bort projektet.](/help/sites-authoring/touch-ui-managing-projects.md#deleting-a-project) En administratör kan även ta bort grupper manuellt i **verktyg** > **Säkerhet** > **Grupper**.

## Ytterligare resurser {#additional-resources}

Mer information om hur du använder projekt finns i följande ytterligare dokument:

* [Hantera projekt](/help/sites-authoring/touch-ui-managing-projects.md)
* [Arbeta med uppgifter](/help/sites-authoring/task-content.md)
* [Arbeta med projektarbetsflöden](/help/sites-authoring/projects-with-workflows.md)
* [Kreativt projekt- och PIM-integrering](/help/sites-authoring/managing-product-information.md)
