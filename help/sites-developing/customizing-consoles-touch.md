---
title: Anpassa konsolerna
description: AEM innehåller olika mekanismer som gör att du kan anpassa konsolerna i redigeringsinstansen
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 6e67f2b3-78b9-45f2-b496-61776b9fd9cc
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Anpassa konsolerna {#customizing-the-consoles}

>[!CAUTION]
>
>I det här dokumentet beskrivs hur du anpassar konsoler i det moderna, pekaktiverade användargränssnittet och det gäller inte det klassiska användargränssnittet.

AEM innehåller olika mekanismer som du kan använda för att anpassa konsolerna (och [sidredigeringsfunktioner](/help/sites-developing/customizing-page-authoring-touch.md)) i din redigeringsinstans.

* Med Clientlibs Clientlibs kan du utöka standardimplementeringen för att få nya funktioner, samtidigt som du återanvänder standardfunktioner, objekt och standardmetoder. När du anpassar kan du skapa en egen klientlib under `/apps.` Den kan till exempel innehålla den kod som krävs för den anpassade komponenten.

* Övertäckningsövertäckningar baseras på noddefinitioner och gör att du kan täcka över standardfunktionerna (i `/libs`) med din egen anpassade funktionalitet (i `/apps`). När du skapar en övertäckning krävs inte en 1:1-kopia av originalet, eftersom sammanslagningen av försäljningsresurser tillåter arv.

De kan användas på många sätt för att utöka dina AEM. En liten markering beskrivs nedan (på en hög nivå).

>[!NOTE]
>
>Mer information finns i:
>
>* Använda och skapa [klientlibs](/help/sites-developing/clientlibs.md).
>* Använda och skapa [övertäckningar](/help/sites-developing/overlays.md).
>* [Granit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>


>[!CAUTION]
>
>Du ***måste*** ändrar ingenting i dialogrutan `/libs` bana.
>
>Detta beror på innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan mycket väl skrivas över när du installerar en snabbkorrigering eller ett funktionspaket).
>
>Den rekommenderade metoden för konfiguration och andra ändringar är:
>
>1. Återskapa önskat objekt (d.v.s. som det finns i `/libs`) under `/apps`
>
>1. Gör ändringar i `/apps`
>

Följande plats i `/libs` struktur kan överlappas:

* konsoler (alla konsoler baserade på GRA-sidor), till exempel:

   * `/libs/wcm/core/content`

>[!NOTE]
>
>Läs artikeln i kunskapsbasen [Felsökning AEM TouchUI-problem](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)för fler tips och verktyg.

## Anpassa standardvyn för en konsol {#customizing-the-default-view-for-a-console}

Du kan anpassa standardvyn (kolumn, kort, lista) för en konsol:

1. Du kan ändra ordningen på vyerna genom att ersätta den önskade posten under:

   `/libs/wcm/core/content/sites/jcr:content/views`

   Den första posten blir standard.

   De tillgängliga noderna motsvarar de visningsalternativ som är tillgängliga:

   * `column`
   * `card`
   * `list`

1. I en övertäckning för list:

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   Definiera följande egenskap:

   * **Namn**: `sling:orderBefore`
   * **Typ**: `String`
   * **Värde**: `column`

### Lägg till ny åtgärd i verktygsfältet {#add-new-action-to-the-toolbar}

1. Du kan skapa egna komponenter och inkludera motsvarande klientbibliotek för anpassade åtgärder. Till exempel en **Befordra till Twitter** åtgärd vid:

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   Detta kan sedan anslutas till ett verktygsfältsobjekt på konsolen:

   `/apps/<yourProject>/admin/ext/launches`

   I markeringsläge:

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### Begränsa en verktygsfältåtgärd till en viss grupp {#restrict-a-toolbar-action-to-a-specific-group}

1. Du kan använda ett anpassat återgivningsvillkor om du vill täcka över standardåtgärden och ange särskilda villkor som måste uppfyllas innan den återges.

   Skapa till exempel en komponent som styr återgivningsvillkoren enligt grupp:

   `/apps/myapp/components/renderconditions/group`

1. Så här använder du åtgärden Skapa plats på webbplatskonsolen:

   `/libs/wcm/core/content/sites`

   Skapa övertäckningen:

   `/apps/wcm/core/content/sites`

1. Lägg sedan till återgivningsvillkoret för åtgärden:

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   Med hjälp av egenskaper på den här noden kan du definiera `groups` som kan utföra den specifika åtgärden, till exempel `administrators`

### Anpassa kolumner i listvyn {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>Den här funktionen är optimerad för kolumner med textfält. För andra datatyper är det möjligt att täcka över `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` in `/apps`.

Så här anpassar du kolumnerna i listvyn:

1. Lägg över listan med tillgängliga kolumner.

   * På noden:

     ```
            /apps/wcm/core/content/common/availablecolumns
     ```

   * Lägg till nya kolumner eller ta bort befintliga.

   Se [Använda övertäckningar (och Sling Resource Merger)](/help/sites-developing/overlays.md) för mer information.

1. Valfritt:

   * Om du vill lägga till ytterligare data måste du skriva en [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) med
     `pageInfoProviderType` -egenskap.

   Se till exempel klassen/paketet som bifogas (från GitHub) nedan.

1. Nu kan du markera kolumnen i listvyns kolumnkonfigurator.

### Filtreringsresurser {#filtering-resources}

När du använder en konsol är ett vanligt användningsfall när användaren måste välja bland resurser (till exempel sidor, komponenter, resurser och så vidare). Detta kan t.ex. vara en lista som författaren måste välja ett alternativ från.

För att hålla listan i en rimlig storlek och även relevant för användningsfallet kan ett filter implementeras i form av ett anpassat predikat. Se [den här artikeln](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) för mer information.
