---
title: Aktivitetstrender
seo-title: Activity Trends
description: Lägga till en del av en lista över communityaktiviteter på en sida
seo-description: Adding a Community Activity List component to a page
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 1%

---

# Aktivitetstrender {#activity-trends}

## Introduktion {#introduction}

The `Community Activity List` -komponenten gör det möjligt att lägga till trendinformation om inlägg och vyer från medlemmar samt inlägg och vyer av innehåll.

Dokumentet beskriver:

* Lägga till `Community Activity List` till en [communitywebbplats](/help/communities/overview.md#community-sites).

* Konfigurationsinställningar för `Community Activity List` -komponenten.

### Krav {#requirement}

Data för `Community Activity List` är endast tillgängligt när Adobe Analytics har licens och konfigurerats för communitywebbplatsen.

Se [Analyskonfiguration för communityfunktioner](/help/communities/analytics.md).

### Lägga till en lista med communityaktiviteter på en sida {#adding-a-community-activity-list-to-a-page}

Lägga till en `Community Activity List` till en sida i redigeringsläge, leta reda på komponenten

* `Communities / Community Activity List`

och dra den till rätt plats på en sida.

Nödvändig information finns på [Grunderna för communitykomponenter](/help/communities/basics.md).

När komponenten placeras på en sida i en community-webbplats är det så här den visas:

![communityaktivitet](assets/community-activity.png)

### Konfigurerar lista över communityaktiviteter  {#configuring-community-activity-list}

Markera den monterade `Community Activity List` -komponenten som ska få åtkomst till och markera `Configure` som öppnar redigeringsdialogrutan.

![konfigurera](assets/configure-new.png)

Under **Kommentarer** anger du om och hur kommentarer för överförda filer ska visas:

![egenskaper](assets/activity-list-properties.png)

* **Typ**

   Ange om data ska visas för communitymedlemmar eller användargenererat innehåll (UGC).

   Välj  från:

   * `Members`
   * `Content`

   Standard är `Members`.

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

   Standard är `Total`.

* **Kontextbana**

   Gör det möjligt att omfång aktiviteten till en delmängd av platsen, t.ex. en viss blogg.
Standard är hela communitywebbplatsen.

* **Medlemsräkningsaggregering**

   När du avmarkerar det här alternativet (inaktiverat) räknas endast inlägg på den översta nivån. Om kontexten till exempel är rotsidan (standardvärdet), kan du `Activity Type` av `Posts` kommer aldrig att visa någon aktivitet eftersom det inte går att publicera innehåll på rotsidan. När du markerar det här alternativet inkluderas antalet på alla underordnade sidor.
Standard är markerat.

### Exempelsida med 4 komponenter {#example-page-with-components}

**De vanligaste besökarna** config: Typ = Medlemmar, aktivitetstyp = Vyer

**Främsta bidragsgivare** config: Typ = Medlemmar, aktivitetstyp = Bokföring

**Övre innehåll** config: Typ = Innehåll, aktivitetstyp = Vyer,

**Trendinnehåll** config: Typ = innehåll, aktivitetstyp = inlägg

![komponenter](assets/activity-list-components.png)
