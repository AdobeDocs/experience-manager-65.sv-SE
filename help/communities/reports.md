---
title: Rapportkonsol
description: Lär dig hur du använder olika rapporter som du kan få tillgång till på flera sätt i Adobe Experience Manager Author-miljön.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
source-git-commit: 00b6f2f03470aca7f87717818d0dfcd17ac16bed
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# Rapportkonsol {#reports-console}

## Översikt {#overview}

För AEM Communities finns det olika rapporter som du kan få åtkomst till på flera sätt från författarmiljön.

De olika rapporterna är i allmänhet följande:

* [Vyrapport](#views-report)

  Ger en översikt över vad communitymedlemmar och besökare tycker om communitysajter.

* [Inläggsrapport](#posts-report)

  Ger en översikt över olika typer av inlägg från communitymedlemmar på alla communitysajter.

Tabellrapporter kan exporteras i CSV-format för efterföljande bearbetning.

## Rapporteringskonsoler {#reporting-consoles}

### Rapporter om communitysajter {#reports-for-community-sites}

* Från global navigering: **[!UICONTROL Navigation]** > **[!UICONTROL Communities]** >  **[!UICONTROL Reports]**

* Välj bland:

   * **[!UICONTROL Assignments Report]**

      * Generera en rapport för den valda communityplatsen, användaren eller gruppen och tilldelningen.

   * **[!UICONTROL Posts Report]**

      * Generera en rapport för den valda communityplatsen, innehållstypen och tidsperioden.

   * **[!UICONTROL Views Report]**

      * generera en rapport för den valda communityplatsen, innehållstypen och tidsperioden.

![rapporter](assets/reports1.png)

## Vyrapport {#views-report}

Med hjälp av vykonsolen kan rapporter genereras på sidvyer av communityfunktioner under en viss tidsperiod.

![view-report](assets/view-report.png)

Välj villkor för rapporten:

* **[!UICONTROL Site]**

  Välj en community-webbplats.

* **[!UICONTROL Content Type]**

  Välj Allt innehåll eller någon av funktionerna på webbplatsen.

* **[!UICONTROL Time frame]**

  Välj något av följande:

   * De senaste 7 dagarna
   * De senaste 30 dagarna
   * De senaste 90 dagarna
   * Förra året

Välj **[!UICONTROL Generate]** för att skapa rapporten.

![generera vyer](assets/generate-views.png)

## Inläggsrapport {#posts-report}

På postkonsolen kan rapporter skapas om antalet inlägg i communityfunktioner under en viss tidsperiod.

![postrapport](assets/posts-report.png)

Välj villkor för rapporten:

* **[!UICONTROL Site]**

  Välj en community-webbplats.

* **[!UICONTROL Content Type]**

  Välj Allt innehåll eller någon av funktionerna på webbplatsen.

* **[!UICONTROL Time frame]**

  Välj något av följande:

   * De senaste 7 dagarna
   * De senaste 30 dagarna
   * De senaste 90 dagarna
   * Förra året

Välj **[!UICONTROL Generate]** för att skapa rapporten.

![generate-report](assets/generate-posts-report.png)

## Felsökning {#troubleshooting}

### Inga communitywebbplatser har angetts {#no-community-sites-listed}

Om det inte finns några communitysajter i listan kontrollerar du att Adobe Analytics har aktiverats för en webbplats. Om du väljer rapporter om tilldelningar måste du se till att tilldelningsfunktionen finns i communityplatsens struktur.

### Rapporterna visas inte i AEM Author-instansen {#reports-do-not-show-in-aem-author-instance}

Om rapporter inte visas i AEM Author-instansen kontrollerar du om anpassningarna finns, t.ex. URL-mappning i Publish-instansen. Om URL-mappning endast görs på AEM publiceringsinstans på communitywebbplatsen, kontrollerar du att samma har konfigurerats i AEM Author-instans i **Trend Report Social Component Factory för webbplats** konfiguration.

![URL-mappning AEM författare](assets/sitetrend.png)
