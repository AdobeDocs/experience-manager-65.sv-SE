---
title: Redigerare
seo-title: Editor
description: Lär dig hur du växlar tillbaka till den klassiska gränssnittsredigeraren.
seo-description: Learn how to switch back to the Classic UI Editor.
uuid: ca8b07e7-014f-428e-82bd-87f3aae12f6e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 54903f3a-1e7e-4083-a2c9-b2ea4555d7fc
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
source-git-commit: 1c89ac7c4740222a3f51abd677e0ce71a7004377
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 1%

---


# Redigerare{#editor}

Som standard har möjligheten att växla till det klassiska användargränssnittet från redigeraren inaktiverats.

Aktivera alternativet igen **Öppna i Classic UI** i **Sidinformation** gör du så här.

1. Använd CRXDE Lite för att hitta följande nod:

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   Till exempel

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. Skapa en övertäckning med **Överläggsnod** option; till exempel:

   * **Bana**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **Överläggsplats**: `/apps/`
   * **Matcha nodtyper**: aktiv (markera kryssrutan)

1. Lägg till följande text-egenskap med flera värden i den åsidosatta noden:

   `sling:hideProperties = ["granite:hidden"]`

1. The **Öppna i Classic UI** finns igen i **Sidinformation** när du redigerar sidor.

   ![öppna i klassiskt användargränssnitt från sidinformation](assets/syui-03-2019-02-27-15-19-48.png)
