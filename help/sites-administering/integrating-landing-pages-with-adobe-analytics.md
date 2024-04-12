---
title: Integrera landningssidor med Adobe Analytics
description: Lär dig integrera landningssidor med Adobe Analytics.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: da3f7b7e-87e5-446a-9a77-4b12b850a381
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 1%

---

# Integrera landningssidor med Adobe Analytics{#integrating-landing-pages-with-adobe-analytics}

AEM har integrerat landningssidornas lösning med [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) genom att använda följande CTA-komponenter (Call-to-action):

1. Klicka genom komponent
1. Komponent för grafisk länk

Dessa komponenter visar vissa attribut som kan mappas via Adobe Analytics-variabler (trafik, konverteringsvariabler) och success-händelser för att skicka information till Adobe Analytics.

## Förutsättningar {#prerequisites}

Adobe rekommenderar att du går igenom [integrering med AEM-Adobe Analytics](/help/sites-administering/adobeanalytics.md) för att förstå hur integreringen fungerar.

## Komponenter tillgängliga för mappning {#components-available-for-mapping}

AEM **Utlysning** komponenter - **ClickThroughLink** och **GraphicalLink** - som visas här i sidosparken kan mappas till Adobe Analytics-variabler.

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### Mappa landningssidkomponenter till Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

Så här mappar du landningssidans komponenter till Adobe Analytics:

1. När du har skapat Adobe Analytics-konfigurationen och skapat ett ramverk väljer du lämplig rapporteringssvit i listrutan. Detta leder till att Adobe Analytics-variablerna hämtas och visas i innehållssökaren.
1. Dra och släpp CTA-komponenter (Call to Action) från sidosparken till mappningsområdet mitt på sidan, beroende på vad som är lämpligt.

<table>
 <tbody>
  <tr>
   <td><strong>Komponentnamn</strong></td>
   <td><strong>Exponerade attribut</strong></td>
   <td><strong>Betydelse av attribut</strong></td>
  </tr>
  <tr>
   <td><strong>CTA Click Through Link</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td>
   <td>Etiketten på länken eller texten i länken </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td>
   <td>Destinationen du tar när du klickar på länken </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td>
   <td>Klickhändelsen </td>
  </tr>
  <tr>
   <td><strong>CTA Graphical Link</strong></td>
   <td><i>eventdata.clicktroughImageLabel</i> <br /> </td>
   <td>CTA-bildens titel </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageTarget</i> <br /> </td>
   <td>Målet dit du är tagen när du klickar på bilden som innehåller en länk</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageAsset</i> <br /> </td>
   <td>Sökvägen till bildresursen i databasen </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clicktroughImageClick</i> <br /> </td>
   <td>Klickhändelsen</td>
  </tr>
 </tbody>
</table>

1. Mappa dessa exponerade attribut med eventuella Adobe Analytics-variabler från innehållssökaren. Ramverket är nu klart att användas.
1. Nu kan du skapa en landningssida eller öppna en befintlig landningssida med befintliga CTA-komponenter och klicka på **Cloud Service** tabba in **Sidegenskaper** från sidosparken (i det pekoptimerade användargränssnittet väljer du **Öppna egenskaper** och klicka **Cloud Service**) och konfigurera ramverket som ska användas med landningssidan. Välj ramverket i listrutan.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. När du har konfigurerat ramverket med landningssidan kan du nu använda de instrumenterade komponenterna och alla klick på CTA registreras i Adobe Analytics.
