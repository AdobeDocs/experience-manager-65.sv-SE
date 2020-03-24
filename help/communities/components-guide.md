---
title: Community Components Guide
seo-title: Community Components Guide
description: Ett interaktivt utvecklingsverktyg för att komma igång med ramverket för sociala komponenter (SCF)
seo-description: Ett interaktivt utvecklingsverktyg för att komma igång med ramverket för sociala komponenter (SCF)
uuid: 120e56d1-b93c-4f92-bab4-6bb5e40e0ddf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a777a3f1-b39f-4d90-b9b6-02d3e321a86f
translation-type: tm+mt
source-git-commit: e8d8bf89971d3d9d5ec150308dda247aa53c77bb

---


# Community Components Guide {#community-components-guide}

Community Components Guide är ett interaktivt utvecklingsverktyg för ramverket för [sociala komponenter (SCF)](scf.md). Den innehåller en lista över tillgängliga AEM Communities-komponenter eller de mer komplexa funktioner som byggts av flera komponenter.

Förutom grundläggande information för varje komponent kan du med guiden experimentera med hur SCF-komponenterna/-funktionerna fungerar och hur de kan konfigureras eller anpassas.

Information om grundläggande utvecklingsfunktioner för varje komponent finns i [Grundläggande om funktioner och komponenter](essentials.md).

## Komma igång {#getting-started}

Handboken är avsedd att användas i utvecklingsinstallationer av författare (localhost:4502) och publicera (localhost:4503) instanser.

Webbplatsen Community Components nås via

* [https://&lt;server>:&lt;port>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

Interaktionen med komponenterna i Communities varierar beroende på:

* Servern (författare eller publicerad)
* Om besökaren är inloggad eller inte
* Om du är inloggad, de privilegier som tilldelats medlemmen
* Oavsett om standardmetoden för SRP, [JSRP](jsrp.md), används eller inte

Om du vill växla till redigeringsläge infogar du antingen `editor.html` eller `cf#` som det första sökvägssegmentet efter servernamnet:

* Standardgränssnitt:

   [https://&lt;server>:&lt;port>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* Klassiskt användargränssnitt:

   [https://&lt;server>:&lt;port>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>Länkarna på en sida är inte aktiva i redigeringsläge.
>
>Om du vill navigera till en komponentsida väljer du först Förhandsgranskningsläge för att aktivera länkarna.
>
>När komponentsidan visas i webbläsaren går du tillbaka till redigeringsläget för att öppna komponentens redigeringsdialogruta.
>
>Allmän redigeringsinformation finns i [snabbguiden till redigeringssidorna](../../help/sites-authoring/qg-page-authoring.md).
>
>Om du inte känner till AEM läser du dokumentationen om [grundläggande hantering](../../help/sites-authoring/basic-handling.md).

### Hemsida {#home-page}

Guiden innehåller en lista med de SCF-komponenter som är tillgängliga för förhandsgranskning och prototyper längs sidans vänstra sida.

Komponentguiden visas på en författarinstans i redigeringsläge:

![chlimage_1-404](assets/chlimage_1-404.png)

## Komponentsidor {#component-pages}

Markera en komponent i listan till vänster på sidan.

![chlimage_1-405](assets/chlimage_1-405.png)

Huvudtexten i guiden visar:

1. Titel: Namnet på den markerade komponenten
1. [Klientbibliotek](#client-side-libraries): En lista över en eller flera obligatoriska kategorier
1. [Inkluderbart](scf.md#add-or-include-a-communities-component): Om komponenten kan inkluderas dynamiskt kan läget aktiveras i redigeringsläget för författare:

   * Om den text som visas läggs till är: &quot;Den här komponenten inkluderas via dess parnod.&quot;
   * Om det ingår är texten som visas: &quot;Den här komponenten inkluderas dynamiskt.&quot;
   * Om den inte är inkluderbar visas ingen text

1. Exempelkomponent eller funktion: en aktiv instans av komponenten eller funktionen. Om en komponent ändras kan den ändras med ändringar i mallarna, CSS och data som finns i flikavsnittet.

>[!NOTE]
>
>När du har gjort ett val från vänster sida visas komponenten nedan, i stället för bredvid, listan med komponenter när webbläsarfönstret är för smalt.

### Författarinteraktioner {#author-interactions}

När du använder guiden för en författarinstans kan du uppleva hur en komponent konfigureras genom att öppna dess dialogruta. Information för utvecklare finns i avsnittet [Komponent- och Funktionsfunktioner](essentials.md) i dokumentationen, medan inställningarna för dialogrutorna beskrivs i avsnittet [Webbgruppskomponenter](author-communities.md) för författare.

I guiden Community Components (Community-komponenter) är vissa inställningar i komponentdialogrutorna överlagrade med [Inkluderbart](scf.md#add-or-include-a-communities-component) växlingsläge. Om du vill växla mellan att använda den befintliga resursen eller en resurs som ingår dynamiskt markerar du både komponenten och den inkluderbara texten i redigeringsläget och dubbelklickar för att öppna redigeringsdialogrutan:

![chlimage_1-406](assets/chlimage_1-406.png)

Under fliken **Mallar** :

![chlimage_1-407](assets/chlimage_1-407.png)

* **Inkludera den underordnade komponenten med sling:include**

   Om alternativet inte är markerat används den befintliga resursen i databasen (en jcr-nod som är underordnad en par-nod).

   * texten som visas är: &quot;Den här komponenten inkluderas via dess parnod.&quot;
   Om det här alternativet är markerat används sling för att dynamiskt inkludera en komponent i den underordnade nodens resourceType (en resurs som inte finns).

   * texten som visas är: &quot;Den här komponenten inkluderas dynamiskt.&quot;
   Standard är avmarkerat.

### Publicera interaktioner {#publish-interactions}

När du använder guiden för en publiceringsinstans är det möjligt att uppleva komponenterna och funktionerna som en besökare (inte inloggad) och som medlemmar med olika behörigheter när de loggas in.

>[!NOTE]
>
>Observera att om SRP lämnas som standard till [JSRP](jsrp.md)så syns bara den UGC som anges i publiceringsinstansen vid publiceringen och syns *inte* från [modereringskonsolen](moderate-ugc.md) på författarinstansen.

## Klientbibliotek {#client-side-libraries}

Klientsidans bibliotek (klientlibs) som anges för varje komponent är de som *måste* refereras till när komponenten placeras på en sida. Klientlibs är ett sätt att hantera och optimera nedladdningen av JavaScript och CSS som används för att återge komponenten i webbläsaren.

Mer information finns på [Clientlibs for Communities Components](clientlibs.md).

## Personifiering {#impersonation}

I författarinstansen, där en användare ofta är inloggad som administratör eller utvecklare, kan du använda textrutan till vänster om knappen **[!UICONTROL Personifiera]** för att antingen skriva användarnamnet eller välja i listrutan och sedan klicka på knappen. Klicka på Återställ för att logga ut och avsluta personifieringen.

Publiceringsinstansen behöver inte personifiera. Använd bara länken Login/Logout för att personifiera olika användare, till exempel [demoanvändare](tutorials.md#demo-users).

## Anpassning {#customization}

När det här alternativet är aktiverat är varje SCF-komponent tillgänglig för att skapa prototyper för eventuella anpassningar genom att tillfälligt ändra komponentens mall, CSS och data.

### Aktivera anpassning {#enabling-customization}

>[!NOTE]
>
>**Det här verktyget är skrivskyddat**. Ingen av de ändringar som gjorts i mallar, CSS eller data sparas i databasen.

Om du snabbt vill experimentera med anpassningar måste `scg:showIde`egenskapen läggas till i komponentsidans innehålls-JCR-nod och ställas in på true.

Använda kommentarkomponenten som exempel, på antingen författaren eller publiceringsinstansen, inloggad med administratörsbehörighet:

1. Bläddra till [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)

   Till exempel [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. Markera komponentens `jcr:content` nod

   Exempel: `/content/community-components/en/comments/jcr:content`

1. Lägg till en egenskap

   * **Namn**`scg:showIde`
   * **Typ**`String`
   * **Värde**`true`

1. Välj **[!UICONTROL Spara alla]**
1. Läs in kommentarsidan igen i stödlinjen

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. Observera att det nu finns tre flikar för Mallar, CSS och Data.

![chlimage_1-408](assets/chlimage_1-408.png) ![chlimage_1-409](assets/chlimage_1-409.png)

### Fliken Mallar {#templates-tab}

Välj fliken Mallar för att visa mallarna som är kopplade till komponenten.

I mallredigeraren kan lokala redigeringar kompileras och användas på exempelkomponentinstansen högst upp på sidan utan att komponenten i databasen påverkas.

När du kör kompileringen på lokala redigeringar markeras eventuella fel med en punkt i mellanrummet och texten markeras med röd.

### CSS-flik {#css-tab}

Välj fliken CSS om du vill visa CSS-koden som är kopplad till komponenten.

Om en komponent är en sammansättning av flera komponenter kan vissa CSS listas under någon av de andra komponenterna.

Med CSS Editor kan CSS ändras och tillämpas på exempelkomponentinstansen högst upp på sidan.

Du kan markera en regel för att markera delar av DOM med den regeln genom att klicka bredvid regeln i kolumnmarginalen.

### Fliken Data {#data-tab}

Välj fliken Data för att visa .social.json-slutpunktsdata. Dessa data kan redigeras och används på exempelkomponentinstansen.

Syntaxfel kan markeras i mellanrummet och markeras i redigeraren.
