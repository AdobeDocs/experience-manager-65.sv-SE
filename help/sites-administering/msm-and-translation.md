---
title: Webbplatsadministration
seo-title: Webbplatsadministration
description: Lär dig hur du hanterar flerspråkiga webbplatser i AEM.
seo-description: Lär dig hur du hanterar flerspråkiga webbplatser i AEM.
uuid: a32d458b-a5ad-46ef-a68c-4717c63b4bdd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: fabaa3e8-1657-4ed4-abb2-990117bec39c
translation-type: tm+mt
source-git-commit: 0885fb6eb6b6a6b8fefd522b2656c8f64e0a537e

---


# Webbplatsadministration{#website-administration}

Följande administrationsverktyg finns för att hantera webbplatser och sidor:

* Med Multi Site Manager (MSM) kan du använda samma webbplatsinnehåll på flera platser samtidigt som du kan använda olika varianter:

   * [Återanvända innehåll: Multi Site Manager och Live Copy](/help/sites-administering/msm.md)

* Översättning gör att du kan automatisera översättning av sidinnehåll, resurser och användargenererat innehåll för att skapa och underhålla flerspråkiga webbplatser:

   * [Översätta innehåll för flerspråkiga webbplatser](/help/sites-administering/translation.md)

* Dessa två funktioner kan kombineras för att passa för webbplatser som är både [flerspråkiga och flerspråkiga](#multinational-and-multilingual-sites).

## Flerspråkiga och flerspråkiga webbplatser {#multinational-and-multilingual-sites}

Ni kan effektivt skapa innehåll för multinationella och flerspråkiga webbplatser genom att kombinera Multi Site Manager och arbetsflödet för översättning. Skapa en huvudwebbplats på ett språk, för ett visst land, och använd sedan innehållet som grund för de andra webbplatserna, med översättning där det behövs:

* [Översätt](/help/sites-administering/translation.md) mallwebbplatsen till olika språk.

* Använd [Multi Site Manager](/help/sites-administering/msm.md) för att:

   * Återanvänd innehåll från huvudwebbplatsen och översättningarna för att skapa webbplatser för andra länder och kulturer.
   * Se till att begränsa användningen av Multi Site Manager till innehåll på ett språk, t.ex. engelsk master -> Engelsk språkgren på landsplatser, fransk master -> franska språkgrenar på landsplatser.
   * Om det behövs frigör du element från live-kopiorna för att lägga till lokaliseringsinformation.

I följande diagram visas hur huvudbegreppen överlappar (men inte alla nivåer/element som berörs):

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>I detta fall, och på liknande sätt, hanterar inte MSM de olika språkversionerna som sådana.
>
>* [MSM](/help/sites-administering/msm.md) hanterar distributionen av översatt innehåll från en ritning (t.ex. en global master) till live-kopiorna (t.ex. de lokala webbplatserna) inom ett språks gränser.
>* Funktionerna för [översättningsintegrering](/help/sites-administering/translation.md) i AEM, tillsammans med översättningshanteringstjänster från tredje part, hanterar språken och översätter innehåll till dessa olika språk.
>
>
För mer avancerade användningsområden kan MSM användas även av flerspråkiga mallsidor.

>[!NOTE]
>
>För alla användningsfall rekommenderas följande metodtips:
>
>* [Best Practices for MSM](/help/sites-administering/msm-best-practices.md); särskilt:
   >
   >   
   * [Skapa webbplats](/help/sites-administering/msm-best-practices.md#create-site)
   >   * [MSM och flerspråkiga webbplatser](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [Best Practices for Translation](/help/sites-administering/tc-bp.md)

