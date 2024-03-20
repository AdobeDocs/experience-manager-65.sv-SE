---
title: AEM Brackets Extension
description: Lär dig hur du använder Adobe Experience Manager-tillägget för Brackets.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 1%

---

# AEM Brackets Extension{#aem-brackets-extension}

## Ökning {#overview}

Tillägget AEM Brackets ger ett smidigt arbetsflöde för att redigera AEM komponenter och klientbibliotek och utnyttjar kraften i [Parenteser](https://brackets.io/) kodredigeraren som ger åtkomst från kodredigeraren till Photoshop-filer och -lager. Den enkla synkronisering som tillägget ger (ingen Maven eller filvalv krävs) ökar utvecklarens effektivitet och hjälper även gränssnittsutvecklare med begränsade AEM att delta i projekt. Det här tillägget har även stöd för [HTML-mallspråk (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html), vilket minskar komplexiteten i JSP och gör komponentutvecklingen enklare och säkrare.

![chlimage_1-53](assets/chlimage_1-53a.png)

### Funktioner {#features}

De viktigaste funktionerna i AEM Brackets Extension är:

* Automatisk synkronisering av ändrade filer till AEM.
* Manuell dubbelriktad synkronisering av filer och mappar.
* Fullständig innehållspaketsynkronisering av projektet.
* HTML-kodkomplettering för uttryck och `data-sly-*` blockprogramsatser.

Brackets innehåller dessutom många användbara funktioner för AEM teckensnittsutvecklare:

* Photoshop filstöd för att extrahera information från en PSD-fil, som lager, mått, färger, teckensnitt, texter och så vidare.
* Kodtips från PSD för att enkelt återanvända den extraherade informationen i koden.
* Stöd för CSS-preprocessorer, som LESS och SCSS.
* Och hundratals tillägg som täcker mer specifika behov.

## Installation {#installation}

### Parenteser {#brackets}

AEM Brackets Extension har stöd för Brackets version 1.0 eller senare.

Hämta den senaste Brackets-versionen från [hakparenteser.io](https://brackets.io/).

### Tillägget {#the-extension}

Så här installerar du tillägget:

1. Öppna Brackets. På menyn **Fil**, markera **Extension Manager...**
1. Retur **AEM** i sökfältet och leta efter **AEM Brackets Extension**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. Klicka **Installera**.
1. Stäng dialogrutan och Extension Manager när installationen är klar.

## Komma igång {#getting-started}

### Innehållspaketprojektet {#the-content-package-project}

När tillägget har installerats kan du börja utveckla AEM komponenter genom att öppna en innehållspaketmapp från filsystemet med hakparenteser.

Projektet måste innehålla minst

1. a `jcr_root` mapp (till exempel `myproject/jcr_root`)

1. a `filter.xml` fil (till exempel `myproject/META-INF/vault/filter.xml`); för mer information om strukturen på `filter.xml` filen finns i [Filterdefinition för arbetsyta](https://jackrabbit.apache.org/filevault/filter.html).

In Brackets&#39; **Fil** meny, välja **Öppna mapp...** och välj antingen `jcr_root` eller den överordnade projektmappen.

>[!NOTE]
>
>Om du inte har ett eget projekt med ett innehållspaket kan du testa [HTL TodoMVC-exempel](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). På GitHub klickar du på **Ladda ned ZIP**, extrahera filerna lokalt och enligt instruktionerna ovan öppnar du `jcr_root` i Brackets. Följ sedan stegen nedan för att konfigurera **Projektinställningar** och slutligen överföra hela paketet till din AEM genom att göra en **Exportera innehållspaket** enligt instruktionerna längre ned i avsnittet Fullständig synkronisering av innehållspaket.
>
>Efter dessa steg bör du kunna komma åt `/content/todo.html` URL-adressen till din AEM-utvecklingsinstans och du kan börja göra ändringar i koden i hakparenteser och se hur ändringarna synkroniserades direkt till den AEM servern när du gjort en uppdatering i webbläsaren.

### Projektinställningar {#project-settings}

Om du vill synkronisera ditt innehåll till och från en AEM utvecklingsinstans måste du definiera dina projektinställningar. Detta kan du göra genom att gå till **AEM** meny och välja **Projektinställningar...**

![chlimage_1-55](assets/chlimage_1-55a.png)

Med projektinställningarna kan du definiera följande:

1. Server-URL (till exempel `http://localhost:4502`)
1. Om servrar som inte har ett giltigt HTTPS-certifikat ska tolereras (håll inte markerat om det inte krävs)
1. Användarnamnet som används för att synkronisera innehåll (till exempel `admin`)
1. Användarens lösenord (till exempel `admin`)

## Synkroniserar innehåll {#synchronizing-content}

Tillägget AEM Brackets ger följande typer av innehållssynkronisering för filer och mappar som tillåts av filtreringsreglerna som definieras i `filter.xml`:

### Automatisk synkronisering av ändrade filer {#automated-synchronization-of-changed-files}

Detta synkroniserar endast ändringar från hakparenteser till AEM, men inte tvärtom.

### Manuell dubbelriktad synkronisering {#manual-bidirectional-synchronization}

Öppna snabbmenyn i projektutforskaren genom att högerklicka på en fil eller mapp och på **Exportera till server** eller **Importera från server** finns.

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>Om den markerade posten ligger utanför `jcr_root` mapp, **Exportera till server** och **Importera från server** sammanhangsbaserade menyposter är inaktiverade.

### Fullständig synkronisering av innehållspaket {#full-content-package-synchronization}

I **AEM** -menyn, **Exportera innehållspaket** eller **Importera innehållspaket** kan du synkronisera hela projektet med servern.

![chlimage_1-57](assets/chlimage_1-57a.png)

### Synkroniseringsstatus {#synchronization-status}

I AEM Brackets Extension finns en meddelandeikon i verktygsfältet till höger om Brackets-fönstret, som anger status för den senaste synkroniseringen:

* grön - alla filer har synkroniserats
* blue - en synkroniseringsåtgärd pågår
* gult - vissa av filerna synkroniserades inte
* röd - ingen av filerna synkroniserades

Om du klickar på meddelandeikonen öppnas dialogrutan Synkroniseringsstatus med en lista över all status för varje synkroniserad fil.

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>Endast innehåll som markerats som inkluderat av filtreringsreglerna från `filter.xml` synkroniseras, oavsett vilken synkroniseringsmetod som används.
>
>Dessutom `.vltignore` filer kan användas för att utesluta innehåll från synkronisering till och från databasen.

## Redigera HTML-kod {#editing-htl-code}

AEM Brackets Extension innehåller även vissa funktioner för automatisk komplettering som underlättar skrivandet av HTML-attribut och -uttryck.

### Automatisk komplettering av attribut {#attribute-auto-completion}

1. I ett HTML-attribut skriver du `sly`. Attributet fylls i automatiskt till `data-sly-`.
1. Markera HTL-attributet i listrutan.

### Automatisk komplettering av uttryck {#expression-auto-completion}

Inom ett uttryck `${}`, vanliga variabelnamn slutförs automatiskt.

## Mer information {#more-information}

AEM Brackets Extension är ett öppen källkodsprojekt som hanteras av GitHub av [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud) under Apache License, version 2.0:

* Koddatabas: [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Apache License, version 2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

Kodredigeraren Brackets är även ett öppen källkodsprojekt som hanteras av GitHub av [Adobe Systems Incorporated](https://github.com/adobe) organisation:

* Koddatabas: [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

Du kan bidra!
