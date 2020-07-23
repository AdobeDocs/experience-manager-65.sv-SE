---
title: Aktivitetstrender
seo-title: Aktivitetstrender
description: Lägga till en del av en lista över communityaktiviteter på en sida
seo-description: Lägga till en del av en lista över communityaktiviteter på en sida
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
translation-type: tm+mt
source-git-commit: 17088abc71bb820693259088c8a9b938a43cd9d3
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 2%

---


# Aktivitetstrender {#activity-trends}

## Introduktion {#introduction}

Komponenten `Community Activity List` gör det möjligt att lägga till trendinformation om inlägg och vyer från medlemmar samt inlägg och vyer av innehåll.

Dokumentet beskriver:

* Lägga till `Community Activity List` komponenten på en [communitywebbplats](/help/communities/overview.md#community-sites).

* Konfigurationsinställningar för `Community Activity List` komponenten.

### Krav {#requirement}

Data för `Community Activity List` programmet är bara tillgängliga när Adobe Analytics har licens och konfigurerats för communitywebbplatsen.

Se [Analytics Configuration for Communities Features](/help/communities/analytics.md).

### Lägga till en lista med communityaktiviteter på en sida {#adding-a-community-activity-list-to-a-page}

Om du vill lägga till en `Community Activity List` komponent på en sida i redigeringsläge letar du reda på komponenten

* `Communities / Community Activity List`

och dra den till rätt plats på en sida.

Mer information finns i Grunderna för [communitykomponenter](/help/communities/basics.md).

När komponenten placeras på en sida i en community-webbplats är det så här den visas:

![communityaktivitet](assets/community-activity.png)

### Konfigurerar lista över communityaktiviteter  {#configuring-community-activity-list}

Markera den monterade `Community Activity List` komponent som du vill öppna och välj den `Configure` ikon som öppnar redigeringsdialogrutan.

![chlimage_1-55](assets/chlimage_1-55.png)

Under fliken **Kommentarer** anger du om och hur kommentarer för överförda filer ska visas:

![chlimage_1-56](assets/chlimage_1-56.png)

* **Typ**

   Ange om data ska visas för communitymedlemmar eller användargenererat innehåll (UGC).

   Välj  från:

   * `Members`
   * `Content`

   Standardvärdet är `Members`.

* **Visa titel**

   En beskrivande rubrik som ska visas ovanför data, till exempel `Trending Content`.
Standard är ingen titel.

* **Visa antal**

   Antalet objekt som ska listas.
Standardvärdet är 10.

* **Typ av aktivitet**

   Välj något av följande:

   * `Views`(sidbesök)
   * `Posts`(skapa UGC)
   * `Follows`
   * `Likes`

   Standardvärdet är Vyer.

* **Tidsperiod**

   Välj något av följande:

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`

   Standardvärdet är `Total`.

* **Kontextbana**

   Gör det möjligt att omfång aktiviteten till en delmängd av platsen, t.ex. en viss blogg.
Standard är hela communitywebbplatsen.

* **Medlemsräkningsaggregering**

   När du avmarkerar det här alternativet (inaktiverat) räknas endast inlägg på den översta nivån. Om till exempel kontexten är rotsidan (standardinställningen) visas ingen aktivitet `Activity Type` `Posts` i någon av dem eftersom det inte går att publicera innehåll på rotsidan. När du markerar det här alternativet inkluderas antalet på alla underordnade sidor.
Standard är markerat.

### Exempelsida med 4 komponenter {#example-page-with-components}

**Konfiguration för besökare** : Typ = Medlemmar, aktivitetstyp = Vyer

**Top Contributors** config: Typ = Medlemmar, aktivitetstyp = Bokföring

**Konfiguration för det övre innehållet** : Typ = Innehåll, aktivitetstyp = Vyer,

**Trending Content** config: Typ = innehåll, aktivitetstyp = inlägg

![chlimage_1-57](assets/chlimage_1-57.png)

