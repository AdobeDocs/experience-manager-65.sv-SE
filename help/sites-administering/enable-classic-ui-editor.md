---
title: Redigerare
description: Lär dig hur du växlar tillbaka till den klassiska gränssnittsredigeraren.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# Redigerare{#editor}

Som standard har möjligheten att växla till det klassiska användargränssnittet från redigeraren inaktiverats.

Följ de här stegen om du vill aktivera alternativet **Öppna i klassiskt gränssnitt** på menyn **Sidinformation** igen.

1. Använd CRXDE Lite för att hitta följande nod:

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   Till exempel

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. Skapa en övertäckning med alternativet **Överläggsnod**, till exempel:

   * **Sökväg**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **Plats för övertäckning**: `/apps/`
   * **Matcha nodtyper**: aktiv (markera kryssrutan)

1. Lägg till följande text-egenskap med flera värden i den åsidosatta noden:

   `sling:hideProperties = ["granite:hidden"]`

1. Alternativet **Öppna i klassiskt gränssnitt** är igen tillgängligt på menyn **Sidinformation** när du redigerar sidor.

   ![öppnad i klassiskt användargränssnitt från sidinformation](assets/syui-03-2019-02-27-15-19-48.png)
