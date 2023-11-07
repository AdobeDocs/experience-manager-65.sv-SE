---
title: Arbeta med arbetsytan i AEM Forms
seo-title: Working with AEM Forms workspace
description: Kom igång med AEM Forms arbetsyta med en snabb översikt av processarbetsflödena.
seo-description: Get started with AEM Forms workspace with this quick overview of the process workflows.
uuid: 36381e7b-1533-459c-80de-92e806a49cd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 866cd9cb-6661-4b0f-a3af-e39453e6e51b
docset: aem65
exl-id: 0bedcbd9-2cf8-47da-9440-c773982e550c
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 0%

---

# Arbeta med arbetsytan i AEM Forms{#working-with-aem-forms-workspace}

## Introduktion {#introduction}

AEM Forms arbetsyta ingår i AEM Forms. Arbetsytan underlättar återgivning av HTML Forms förutom PDF forms. Nu kan ni engagera er i affärsprocesser från mobilgränssnitt och webbapplikationer.

AEM Forms arbetsyta är dessutom mycket anpassningsbar med utvecklingsmetoderna HTML och JavaScript™. Det är ett komponentbaserat program som enkelt kan integreras med andra webbprogram.

Mer information finns i [Introduktion till AEM Forms arbetsyta](/help/forms/using/introduction-html-workspace.md).

## Getting Familiar {#getting-familiar}

Följ genomgången för att lära dig hur man skapar en blankettapplikation som automatiserar en affärsprocess. Du kan skapa, hantera och testa ett program med arbetsytan i Workbench, Designer och AEM Forms efter genomgången. Mer information om implementering finns i [Skapa ditt första AEM Forms-program](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html).

## Funktionell översikt {#functional-overview}

Du kan använda AEM Forms arbetsyta för att utföra följande uppgifter:

**Påbörja en affärsprocess:** AEM Forms arbetsyta kategoriserar dina processer så som de har utformats och konfigurerats av din organisation. Du kan använda de kategorier du använder ofta till att snabbt komma åt kategorierna. När du påbörjar en process fyller du vanligtvis i ett formulär för att påbörja en affärsprocess som styr arbetsflödet för formulär. Mer information finns i [Startar processer](/help/forms/using/starting-processes.md).

**Visa och agera på uppgifter:** När du visar dina Att göra-listor kan du se uppgifter från en affärsprocess som är tilldelade dig, eller till grupper som du tillhör eller som är delade uppgifter för andra användare. Du kan öppna, arbeta med och slutföra uppgifter efter behov. Vanligtvis innebär det att tillhandahålla information, godkänna ett formulär eller avslå ett formulär. Mer information finns i [Arbeta med att göra-listor](/help/forms/using/todo-lists.md).

**Spåra uppgifter**: Om du vill spåra dina uppgifter använder du fliken Spåra i AEM Forms arbetsyta. Du kan söka efter aktiva eller slutförda processer som du har påbörjat eller deltagit i. Du kan visa uppgifter, uppdrag och formulär som ingår i processen. Du kan också starta nya processer med formulärdata från en process som du tidigare har initierat. Mer information finns i [Spåra processer](/help/forms/using/tracking-processes.md).

## Nytt erbjudande på AEM Forms arbetsyta {#new-offering-of-aem-forms-workspace}

**Stöd för gruppgodkännande av uppgifter**:

Du kan godkänna flera uppgifter av samma typ. När du har valt en uppgift för godkännande är det bara de uppgifter som har samma process, med samma uppgiftsnamn och samma flödesalternativ, som är aktiverade. Se [Arbeta med Att göra-listor](/help/forms/using/todo-lists.md) för implementeringsinformation.

## Migrera från Flex Workspace till AEM Forms {#migrating-from-flex-workspace-to-aem-forms-workspace}

Flex Workspace stöds inte för AEM Forms-kunder. Alla kunder som använder Flex Workspace bör gå över till AEM Forms Workspace.

I AEM Forms-arbetsytan har standardtjänsterna för återgivning och sändning, i standardåtgärdsprofilen, som är kopplad till XDP-formulär ändrats och nya tjänster introducerats. Mer information finns i [Ny renderings- och skicka-tjänst](/help/forms/using/new-render-submit-service.md). Om du vill migrera befintliga processer som fungerar med XDP-formulär och använda dessa tjänster kan du följa [dessa steg](new-render-submit-service.md).

**Anpassa Flex Workspace med AEM Forms arbetsyta**

Mappningen mellan olika typer av anpassningar i båda arbetsytorna är följande.

<table>
 <tbody>
  <tr>
   <td><strong>Typ av anpassning </strong></td>
   <td><strong>Omfattande anpassningar </strong></td>
   <td><strong>Motsvarande scenario för anpassning av arbetsytan i AEM Forms</strong></td>
  </tr>
  <tr>
   <td>Anpassning av lokalisering</td>
   <td>
    <ol>
     <li>Ändra språkinställning för arbetsytan</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">Ändra språkområde för arbetsytan i AEM Forms</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Anpassa teman</td>
   <td>
    <ol>
     <li>Ersätta bilder</li>
     <li>Ändra färger</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">Ändra organisationslogotyp</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">Ändra färgschema</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Anpassa layout</td>
   <td>
    <ol>
     <li>Förenkla arbetsytans användargränssnitt<br /> </li>
     <li>Skapa en ny inloggningsskärm</li>
     <li>Skapa en anpassad godkännandebehållare</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">Arbeta med återanvändbara komponenter</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">Skapa en inloggningsskärm</a></li>
     <li>Godkännandebehållaren är inaktuell.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

En del av funktionerna i Flex Workspace som inte är tillgängliga på AEM Forms-arbetsytan är: meddelanden och meddelanden, välkomstsida, godkännandebehållare och alternativ för att hantera kolumnrubriker. En fullständig lista finns på [Funktioner i Flex Workspace som inte finns på AEM Forms arbetsyta](/help/forms/using/features-flex-workspace-available-html.md).

## Utveckla med AEM Forms arbetsyta {#developing-with-aem-forms-workspace}

### Arkitektur {#architecture}

AEM Forms arbetsyta är en HTML- och JavaScript™-baserad webbapplikation som körs på CRX™. När Workspace URL öppnas i en webbläsare öppnas en CRX™-resurs och programmet återges som en HTML-sida i webbläsaren. JavaScript-biblioteken och den anpassade JavaScript-koden hanterar programmets interna och externa funktioner, till exempel användargränssnitt, användarinteraktion och kommunikation med AEM Forms-servern. Mer information finns i AEM Forms arbetsyta [arkitektur](/help/forms/using/html-workspace-architecture.md).

### Anpassning av arbetsytan i AEM Forms {#aem-forms-workspace-customization}

AEM Forms arbetsyta har stöd för en mängd anpassningar för att uppdatera användargränssnittets layout, utseende, funktioner och mycket annat. Anpassningarna innefattar att uppdatera ett eller flera av följande:

* Användargränssnittets utseende
* Funktioner som använder semantiska anpassningar
* Återanvända HTML-komponenter i andra webbprogram

The [anpassning](introduction-customizing-html-workspace.md#types-of-customizations) I artikeln förklaras vilka typer av sådana anpassningar som finns.

### Konfigurera utvecklarmiljön {#set-up-the-developer-environment}

AEM Forms arbetsyta innehåller ett CRX-paket som distribuerats på CRX, ett SDK-arkiv som innehåller den fullständiga källkoden, JavaScript-bibliotek från tredje part och byggskript för AEM Forms arbetsyta. Använd dessa för att konfigurera utvecklingsmiljön för att utföra de anpassningar som nämns ovan. Mer information finns i [Skapar AEM Forms arbetsytekod](introduction-customizing-html-workspace.md#building-html-workspace-code).

Du kan anpassa en stor del av gränssnittet och viktiga funktioner som teckensnitt, färgscheman, logotyp, inloggningsskärmen, feldialogrutor, integrering med tredjepartsprogram och återanvändning av komponenter i tredjepartsprogram. Du kan också förbättra innehållet som visas på sidan Uppgiftssammanfattning, visa bilder för åtgärder för uppgiftsvägar och även ändra de lågnivåmodeller och vyer för Backbone som skapar AEM Forms-arbetsyteprogrammet.

### HTML-återgivning av XDP Forms {#html-rendering-of-xdp-forms}

Som standard återges ett XDP-formulär i PDF-format på en stationär dator och i HTML-format på en surfplatta för en ny process. Det går alltid att återge ett XDP-formulär i HTML-format. Mer information finns i [Nya tjänster för återgivning och sändning](/help/forms/using/new-render-submit-service.md).

[Mobile Forms](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) funktion, som fungerar med [profiler](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html), möjliggör HTML-återgivning av XDP-formulär. Som standard använder&quot;Återge nytt HTML-formulär&quot; `default.html` som du kan ändra. Du kan också lägga till anpassade ändringar som inträffar innan ett XDP-formulär återges i HTML-format.

## AEM Forms arbetsyta {#aem-forms-workspace-app}

Om du vill arbeta med dina affärsprocesser på en mobil enhet kan du använda AEM Forms-appen för arbetsytor i AEM Forms. Mer information finns i [Översikt över AEM Forms arbetsyta](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html).
