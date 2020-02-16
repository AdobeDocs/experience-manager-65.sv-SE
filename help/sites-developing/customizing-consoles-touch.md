---
title: Anpassa konsolerna
seo-title: Anpassa konsolerna
description: AEM innehåller olika mekanismer som gör att du kan anpassa konsolerna i din redigeringsinstans
seo-description: AEM innehåller olika mekanismer som gör att du kan anpassa konsolerna i din redigeringsinstans
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# Anpassa konsolerna {#customizing-the-consoles}

>[!CAUTION]
>
>I det här dokumentet beskrivs hur du anpassar konsoler i det moderna, pekaktiverade användargränssnittet och det gäller inte det klassiska användargränssnittet.

I AEM finns olika mekanismer som gör att du kan anpassa konsolerna (och [sidredigeringsfunktionerna](/help/sites-developing/customizing-page-authoring-touch.md)) i din redigeringsinstans.

* Med ClientlibsClientlibs kan du utöka standardimplementeringen för att få nya funktioner, samtidigt som du återanvänder standardfunktioner, objekt och standardmetoder. När du anpassar kan du skapa ett eget klientbibliotek under `/apps.` Det kan t.ex. innehålla den kod som krävs för den anpassade komponenten.

* OverlaysOverlays baseras på noddefinitioner och gör att du kan täcka över standardfunktionerna (i `/libs`) med dina egna anpassade funktioner (i `/apps`). När du skapar en övertäckning krävs inte en 1:1-kopia av originalet, eftersom sammanslagningen av försäljningsresurser tillåter arv.

Dessa kan användas på många sätt för att utöka dina AEM-konsoler. En liten markering beskrivs nedan (på en hög nivå).

>[!NOTE]
>
>Mer information finns i:
>
>* Använda och skapa [klientlibs](/help/sites-developing/clientlibs.md).
>* Använda och skapa [övertäckningar](/help/sites-developing/overlays.md).
>* [Granit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>
>
Det här avsnittet behandlas också i [AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html) -sessionen - [Anpassa användargränssnittet för AEM 6.0](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html).

>[!CAUTION]
>
>Du ***får*** inte ändra något i `/libs` banan.
>
>Detta beror på att innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan mycket väl skrivas över när du använder en snabbkorrigering eller ett funktionspaket).
>
>Den rekommenderade metoden för konfiguration och andra ändringar är:
>
>1. Återskapa önskat objekt (t.ex. som det finns i `/libs`) under `/apps`
   >
   >
1. Gör ändringar i `/apps`
>



Följande plats i `/libs` strukturen kan till exempel överlappas:

* Konsoler (alla konsoler baserade på GRA-sidor). till exempel:

   * `/libs/wcm/core/content`

>[!NOTE]
>
>Mer information finns i artikeln [Troubleshooting AEM TouchUI issues](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)i kunskapsbasen.

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

1. Du kan skapa egna komponenter och inkludera motsvarande klientbibliotek för anpassade åtgärder. Exempel: en **åtgärd från Befordra till Twitter** på:

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

   Med hjälp av egenskaper på den här noden kan du definiera vilka som `groups` får utföra den specifika åtgärden;
till exempel `administrators`

### Anpassa kolumner i listvyn {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>Den här funktionen är optimerad för kolumner med textfält; för andra datatyper är det möjligt att täcka över `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` in `/apps`.

Så här anpassar du kolumnerna i listvyn:

1. Lägg över listan med tillgängliga kolumner.

   * På noden:

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * Lägg till nya kolumner eller ta bort befintliga.
   Mer information finns i [Använda övertäckningar (och Samla resurser)](/help/sites-developing/overlays.md) .

1. Valfritt:

   * Om du vill lägga till ytterligare data måste du skriva en [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) med en
      `pageInfoProviderType` -egenskap.
   Se till exempel klassen/paketet som bifogas (från GitHub) nedan.

1. Nu kan du markera kolumnen i listvyns kolumnkonfigurator.

### Filtreringsresurser {#filtering-resources}

När du använder en konsol är ett vanligt användningsfall när användaren måste välja bland resurser (t.ex. sidor, komponenter, resurser osv.). Detta kan vara en lista som författaren till exempel måste välja ett objekt från.

För att hålla listan i en rimlig storlek och även relevant för användningsfallet kan ett filter implementeras i form av ett anpassat predikat. Mer information finns i [den här artikeln](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) .
