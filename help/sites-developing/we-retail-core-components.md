---
title: Provar kärnkomponenter i We.Retail
seo-title: Trying out Core Components in We.Retail
description: Provar kärnkomponenter i We.Retail
seo-description: null
uuid: 8d1cea0b-99d9-49b2-b275-41f14864b1ff
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: af3cd818-61cf-4da1-bfb5-87540911ddd5
exl-id: b5f2be67-c93c-4dbc-acc0-3edd8f1a282f
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 2%

---

# Provar kärnkomponenter i We.Retail{#trying-out-core-components-in-we-retail}

De centrala komponenterna är moderna, flexibla komponenter som är enkla att utöka och som gör det enkelt att integrera i projekten. Kärnkomponenterna har byggts kring flera viktiga designprinciper, som HTML, användbarhet, färdig installation, konfigurerbarhet, versionshantering och utbyggbarhet. Vi.Retail har byggts på kärnkomponenter.

## Prova {#trying-it-out}

1. Börja AEM med exempelinnehållet i Web.Retail och öppna [Komponentkonsol](/help/sites-authoring/default-components-console.md).

   **Global navigering -> Verktyg -> Komponenter**

1. När du öppnar rälen i komponentkonsolen kan du filtrera efter en viss komponentgrupp. Kärnkomponenterna finns i

   * `.core-wcm`: Standardkärnkomponenterna
   * `.core-wcm-form`: Baskomponenter för att skicka in formulär

   Välj `.core-wcm`.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Observera att alla kärnkomponenter namnges **v1**, som återspeglar att detta är den första versionen av denna kärnkomponent. Regelbundna versioner kommer att släppas på marknaden i framtiden, vilket blir versionskompatibelt med AEM och gör det enkelt att uppgradera så att du kan utnyttja de senaste funktionerna.
1. Klicka **Text (v1)**.

   Se **Resurstyp** för komponenten är `/apps/core/wcm/components/text/v1/text`. Kärnkomponenter finns under `/apps/core/wcm/components` och versionshanteras per komponent.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Klicka på **Dokumentation** om du vill visa utvecklardokumentationen för komponenten.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Återgå till komponentkonsolen. Filter för gruppen **Vi.butik** och väljer **Text** -komponenten.
1. Se **Resurstyp** pekar på en komponent enligt `/apps/weretail` men **Resurssupertyp** återgår till kärnkomponenten `/apps/core/wcm/components/text/v1/text`.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Klicka på **Live-användning** för att se vilka sidor den här komponenten används på. Klicka på den första **Tack** sida för att redigera sidan.

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. På sidan Tack markerar du textkomponenten och klickar på ikonen Avbryt arv på komponentens Redigera-meny.

   [Vi.Retail har en global webbplatsstruktur](/help/sites-developing/we-retail-globalized-site-structure.md) där innehåll överförs från språkmallsidor till [live-kopior via en mekanism som kallas arv](/help/sites-administering/msm.md). Arvet måste därför avbrytas för att användaren ska kunna redigera text manuellt.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Bekräfta annulleringen genom att klicka på **Ja**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. När arvet har avbrutits och du väljer textkomponenterna finns det många fler alternativ. Klicka på** Redigera**.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. Nu kan du se vilka redigeringsalternativ som är tillgängliga för textkomponenten.

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. Från **Sidinformation** menyval **Redigera mall**.
1. Klicka på knappen **Policy** ikonen för textkomponenten i **Layoutbehållare** på sidan.

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. Med huvudkomponenterna kan mallskapare konfigurera vilka egenskaper som är tillgängliga för sidförfattarna. Dessa innehåller funktioner som tillåtna inklistringskällor, formateringsalternativ, tillgängliga styckeformat osv.

   Sådana designdialogrutor är tillgängliga för många viktiga komponenter och fungerar tillsammans med mallredigeraren. När de är aktiverade är de tillgängliga för författaren via komponentredigerarna.

   ![chlimage_1-172](assets/chlimage_1-172.png)

## Ytterligare information {#further-information}

Mer information om kärnkomponenterna finns i redigeringsdokumentet [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) för en översikt över de viktigaste komponenternas och utvecklardokumentets funktioner [Utveckla kärnkomponenter](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) för en teknisk översikt.

Du kanske också vill undersöka ytterligare [redigerbara mallar](/help/sites-developing/we-retail-editable-templates.md). Se redigeringsdokumentet [Skapa sidmallar](/help/sites-authoring/templates.md) eller utvecklardokumentsidan [Mallar - redigerbara](/help/sites-developing/page-templates-editable.md) om du vill ha fullständig information om redigerbara mallar.
