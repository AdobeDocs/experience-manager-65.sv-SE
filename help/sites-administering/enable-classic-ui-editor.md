---
title: Redigerare
seo-title: Redigerare
description: Lär dig hur du växlar tillbaka till den klassiska gränssnittsredigeraren.
seo-description: Lär dig hur du växlar tillbaka till den klassiska gränssnittsredigeraren.
uuid: ca8b07e7-014f-428e-82bd-87f3aae12f6e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 54903f3a-1e7e-4083-a2c9-b2ea4555d7fc
docset: aem65
translation-type: tm+mt
source-git-commit: 954c1d5b06b54d59f523483ce5c1af36c2083a76

---


# Redigerare{#editor}

Som standard har möjligheten att växla till det klassiska användargränssnittet från redigeraren inaktiverats.

Följ de här stegen för att aktivera alternativet **Öppna i Classic-gränssnitt** på menyn **Sidinformation** igen.

1. Använd CRXDE Lite för att hitta följande nod:

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   Exempel

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. Skapa en övertäckning med alternativet **Överläggsnod** ; till exempel:

   * **Sökväg**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **Överläggsplats**: `/apps/`
   * **Matcha nodtyper**: aktiv (markera kryssrutan)

1. Lägg till följande text-egenskap med flera värden i den åsidosatta noden:

   `sling:hideProperties = ["granite:hidden"]`

1. Alternativet **Öppna i klassiskt gränssnitt** är igen tillgängligt på menyn **Sidinformation** när du redigerar sidor.

   ![](assets/syui-03-2019-02-27-15-19-48.png)