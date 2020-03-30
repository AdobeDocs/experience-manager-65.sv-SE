---
title: Konfigurera Microsoft Dynamics 365 för arbetsflödet för bostadslån på referensplatsen Web.Finance
seo-title: Konfigurera Microsoft Dynamics 365 för arbetsflödet för bostadslån på referensplatsen Web.Finance
description: Lär dig hur du kan utnyttja Microsoft® Dynamics 365-tjänsterna med hjälp av adaptiva formulär för heminteckningsarbetsflödet på webbplatsen Web.Finance Reference
seo-description: Lär dig hur du kan utnyttja Microsoft® Dynamics 365-tjänsterna med hjälp av adaptiva formulär för heminteckningsarbetsflödet på webbplatsen Web.Finance Reference
uuid: a0656d90-84c7-46d1-9a16-dadcc19ff9ef
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: Configuration
discoiquuid: 6b31397a-fb06-4043-9368-59fb4fce8afa
translation-type: tm+mt
source-git-commit: f323b490c37effc3cbb36c793b62fa788eca9545

---


# Konfigurera Microsoft Dynamics 365 för arbetsflödet för bostadslån på referensplatsen Web.Finance {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

Lär dig hur du kan utnyttja Microsoft® Dynamics 365-tjänsterna med hjälp av adaptiva formulär för heminteckningsarbetsflödet på webbplatsen Web.Finance Reference

## Översikt {#overview}

Microsoft® Dynamics 365 är en CRM- och ERP-programvara (Customer Relationship Management) som innehåller företagslösningar för att skapa och hantera kundkonton, kontakter, leads, möjligheter och ärenden.

AEM Forms tillhandahåller en molntjänst för integrering av Dynamics 365 med [Forms Data Integration](/help/forms/using/data-integration.md) -modulen. Scenariot [Home Mortgage som genomsöks med Microsoft® Dynamics](/help/forms/using/finance-reference-site-walkthrough.md#home-mortgage-application-walkthrough-with-microsoft-dynamics) visar hur en kund använder referenswebbplatsen We.Finance för att ansöka om ett lån när webbplatsen använder Microsoft® Dynamics for Forms Data Integration. Innan du kan använda genomgången av Home Mortgage-programmet med Microsoft® Dynamics-scenariot måste du konfigurera Microsoft® Dynamics 365 så att det används med referenswebbplatsen We.Finance.

## Förutsättningar {#prerequisites}

Innan du börjar konfigurera och konfigurera Dynamics 365 måste du se till att du har:

* [Ställ in och konfigurera AEM Forms-referenswebbplatser](/help/forms/using/setup-reference-sites.md).

* AEM 6.3 Forms Service Pack 1 och senare
* Microsoft® Dynamics 365-konto
* Registrerat program för tjänsten Dynamics 365 med Microsoft® Azure Active Directory
* Klient-ID och klienthemlighet för det registrerade programmet

## Länka inteckningsberäkningen till webbplatsens startsida {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. Gå till följande sida på författarinstansen:

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. Bläddra nedåt till Hemmedarbetarkalkylatorn.
1. Markera den högra kolumnens panel (räknare) och tryck för att visa snabbmenyn. Tryck på Konfigurera på snabbmenyn. Dialogrutan Redigera AEM Forms Container visas.

   ![kalkylatorconfigurepanel](assets/calculatorconfigurepanel.png)

1. I dialogrutan Redigera AEM Forms Container bläddrar du till resursen och väljer home-hypotekskalkylator på följande väg och trycker sedan på **Bekräfta**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. Tryck på **Klar**.
1. Publicera den redigerade sidan.

   >[!NOTE]
   >
   >Bindningen av beräkningsfälten med FDM är förkonfigurerad via referenspaketet för We.Finance. Om du vill visa bindningen kan du öppna formuläret i redigeringsläget och se de binda referenserna för fältet.

1. Om du vill skapa en anpassad enhet för lagring av ansökningspost för bostadslåneprogram importerar du AEMFormsFSIRefsite_1_0.zip-lösningspaketet till din Microsoft® Dynamics-instans:

   1. Hämta paketet från:

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. Importera lösningspaketet till Microsoft® Dynamics-instansen. Gå till **Inställningar** > **Lösningar** i din Microsoft® Dynamics-instans och tryck sedan på **Importera**.

1. Om du vill ställa in kontaktinformation för användare som används i refsite importerar du Sarah Rose Contact.CSV-paketet till din Microsoft® Dynamics-instans:

   1. Hämta paketet från:

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. Importera paketet till din Microsoft® Dynamics-instans. I din Microsoft® Dynamics-instans går du till **Försäljning** > **Kontakter** och trycker sedan på **Importera data**.

