---
title: Aktivitetstrender
description: Lägga till en del av en lista över communityaktiviteter på en sida
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Aktivitetstrender {#activity-trends}

## Introduktion {#introduction}

Med komponenten `Community Activity List` kan du lägga till trendinformation om inlägg och vyer från medlemmar och inlägg och vyer av innehåll.

Dokumentet beskriver:

* Lägger till komponenten `Community Activity List` till en [community-webbplats](/help/communities/overview.md#community-sites).

* Konfigurationsinställningar för komponenten `Community Activity List`.

### Krav {#requirement}

Data för `Community Activity List` är bara tillgängliga när Adobe Analytics är licensierat och konfigurerat för communitywebbplatsen.

Se [Analyskonfiguration för communityfunktioner](/help/communities/analytics.md).

### Lägga till en lista med communityaktiviteter på en sida {#adding-a-community-activity-list-to-a-page}

Om du vill lägga till en `Community Activity List`-komponent på en sida i redigeringsläge letar du reda på komponenten `Communities / Community Activity List` och drar den till rätt plats på en sida.

Mer information finns på [Grunderna för communitykomponenter](/help/communities/basics.md).

När komponenten placeras på en sida i en community-webbplats är det så här den visas:

![community-activity](assets/community-activity.png)

### Konfigurerar lista över communityaktiviteter  {#configuring-community-activity-list}

Markera den monterade `Community Activity List`-komponenten och välj sedan `Configure` -ikonen så att du kan öppna redigeringsdialogrutan.

![konfigurera](assets/configure-new.png)

Under fliken **Kommentarer** anger du om och hur kommentarer för överförda filer ska visas:

![egenskaper](assets/activity-list-properties.png)

* **Typ**

  Ange om data ska visas för communitymedlemmar eller användargenererat innehåll (UGC).

  Välj bland:

   * `Members`
   * `Content`

  Standardvärdet är `Members`.

* **Visa titel**

  En beskrivande titel som ska visas ovanför data, till exempel `Trending Content`.
Standard är ingen titel.

* **Visningsantal**

  Antalet objekt som ska listas.
Standardvärdet är 10.

* **Aktivitetstyp**

  Välj något av följande:

   * `Views`(sidbesök)
   * `Posts`(skapar UGC)
   * `Follows`
   * `Likes`

  Standardvärdet är Vyer.

* **Tidsperiod**

  Välj något av följande:

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1)`
   * `Total`

  Standardvärdet är `Total`.

* **Kontextsökväg**

  På så sätt kan du omsluta aktiviteten till en delmängd av platsen, t.ex. en viss blogg.
Standard är hela communitywebbplatsen.

* **Sammansättning av medlemsantal**

  När du avmarkerar det här alternativet (inaktiverat) räknas endast inlägg på den översta nivån. Om kontexten till exempel är rotsidan (standardvärdet), visar `Activity Type` av `Posts` aldrig någon aktivitet eftersom det inte går att publicera innehåll på rotsidan. När du markerar det här alternativet inkluderas antalet på alla underordnade sidor.
Standard är markerat.

### Exempelsida med fyra komponenter {#example-page-with-components}

**De vanligaste besökarna** config: Type = Medlemmar, aktivitetstyp = Vyer

**Top Contributors** config: Type = Members, Activity type = Posts

**Konfiguration för översta innehåll**: Typ = Innehåll, Typ = Vyer,

**Trending Content** config: Type = Content, Activity type = Posts

![komponenter](assets/activity-list-components.png)
