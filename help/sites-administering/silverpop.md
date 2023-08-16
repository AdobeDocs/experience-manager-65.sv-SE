---
title: Integrera med Silverpop Engage
seo-title: Integrating with Silverpop Engage
description: Lär dig integrera AEM med Silverpop Engage
seo-description: Learn how to integrate AEM with Silverpop Engage
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
exl-id: 6c4b8aaa-bda0-4066-a3fc-d91a5ab1621c
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 1%

---

# Integrera med Silverpop Engage{#integrating-with-silverpop-engage}

<!-- THIS ENTIRE TOPIC APPEARS OBSOLETE BECAUSE SILVERPOP NO LONGER EXISTS AND THERE ARE NO REDIRECTS FOR THE DOWNLOAD URL BELOW THAT IS 404.
>[!NOTE]
>
>Silverpop integration is **not** available out of the box. You must download the Silverpop integration package `https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content` from Package Share and install it on your instance. After you have installed the package, you can configure it as described in this document. -->

Genom att integrera AEM med Silverpop Engage kan du hantera och skicka e-postmeddelanden som skapats i AEM via Silverpop. Du kan också använda leadhanteringsfunktionerna i Silverpop via AEM på AEM sidor.

Integreringen ger dig följande funktioner:

* Möjlighet att skapa e-postmeddelanden i AEM och publicera dem på Silverpop för distribution.
* Möjlighet att ange åtgärd för ett AEM formulär för att skapa en Silverpop-prenumerant.

När Silverpop Engage har konfigurerats kan du publicera nyhetsbrev och e-postmeddelanden till Silverpop Engage.

## Skapa en Silverpop-konfiguration {#creating-a-silverpop-configuration}

Silverpop-konfigurationer kan läggas till via **Cloud Service**, **verktyg**, eller **API-slutpunkter**. Alla metoder beskrivs i det här avsnittet.

### Konfigurera Silverpop med hjälp av Cloud Service {#configuring-silverpop-via-cloudservices}

Så här skapar du en Silverpop-konfiguration i Cloud Service:

1. I AEM: tryck eller klicka **verktyg** > **Distribution** > **Cloud Service**. (Eller direkt åtkomst på `https://<hostname>:<port>/etc/cloudservices.html`.)
1. Klicka på under tredjepartstjänster **Silverop Engage** och sedan **Konfigurera**. Konfigurationsfönstret Silverpop öppnas.

   >[!NOTE]
   >
   >Silverpop Engage är inte tillgängligt som alternativ under tredjepartstjänster om du inte hämtar paketet från paketresursen.

1. Ange en titel och eventuellt ett namn och klicka på **Skapa**. Konfigurationsfönstret** Silverpop Settings** öppnas.
1. Ange användarnamn, lösenord och välj en API-slutpunkt i listrutan.
1. Klicka **Anslut till Silverpop.** När du har anslutit visas en dialogruta om att anslutningen lyckades. Klicka **OK** så att du stänger fönstret. Gå till Silverpop genom att klicka **Gå till Silverpop Engage**.
1. Silverpop har konfigurerats. Du kan redigera konfigurationen genom att klicka på **Redigera**.
1. Silverpop Engage-ramverket kan även konfigureras för anpassade åtgärder genom att tillhandahålla rubrik och namn (valfritt). Klicka på Skapa för att skapa ramverket för den redan konfigurerade Silverpop-anslutningen.

   Importerade datatilläggskolumner kan senare användas via komponenten AEM - **Text och personalisering**.

### Konfigurera Silverpop via verktyg {#configuring-silverpop-via-tools}

Så här skapar du en Silverpop-konfiguration i Verktyg:

1. I AEM: tryck eller klicka **verktyg** > **Distribution** > **Cloud Service**. Eller navigera direkt genom att gå till `https://<hostname>:<port>/misadmin#/etc`.
1. Välj **verktyg** sedan **Cloud Service, konfigurationer,** sedan **Silverpop Engage**.
1. Klicka **Nytt**.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. I **Skapa sida** -fönstret, ange **Titel** och **Namn** och klicka **Skapa**.
1. Ange konfigurationsinformationen enligt steg 4 i föregående procedur. Följ den proceduren så att du kan slutföra konfigurationen av Silverpop.

### Lägga till flera konfigurationer {#adding-multiple-configurations}

Så här lägger du till flera konfigurationer:

1. Klicka på på välkomstsidan **Cloud Service** och klicka **Silverpop Engage**. Klicka **Visa konfigurationer** som visas om en eller flera Silverpop-konfigurationer är tillgängliga. Alla tillgängliga konfigurationer visas.
1. Klicka på **+** signera bredvid Tillgängliga konfigurationer. Den öppnar **Skapa konfigurationer** -fönstret. Följ föregående konfigurationsprocedur så att du kan skapa en konfiguration.

### Konfigurera API-slutpunkter för anslutning till Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

För närvarande har AEM sex osäkra slutpunkter (Engage 1 - 6). Silverpop har nu två nya slutpunkter och ändrade slutpunkter för anslutningen för de befintliga.

Så här konfigurerar du API-slutpunkterna:

1. Gå till `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` på `https://<hostname>:<port>/crxde.`
1. Högerklicka och välj **Skapa** sedan **Skapa nod**.
1. Ange **Namn** as `sp-e0` och välja **Typ** as `cq:Widget`.
1. Lägg till två egenskaper i den nyligen tillagda noden:

   1. **Namn**: `text`, **Typ**: `String`, **Värde**: `Engage 0`
   1. **Namn**: `value`, **Typ**: `String`, **Värde**: `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   Klicka på Spara alla.

1. Skapa en till nod med **Namn** as `sp-e7` och **Typ** as `cq:Widget`.

   Lägg till två egenskaper i den nyligen tillagda noden:

   1. **Namn**: `text`, **Typ**: `String`, **Värde**: `Pilot`
   1. **Namn**: `value`, **Typ**: `String`, **Värde**: `https://apipilot.silverpop.com/XMLAPI`

1. Om du vill ändra de befintliga API-slutpunkterna (Engage 1 - 6) klickar du på var och en av dem en i taget och ersätter värdena enligt följande:

   | **Nodnamn** | **Befintligt slutpunktsvärde** | **Nytt slutpunktsvärde** |
   |---|---|---|
   | sp-e1 | `https://api.engage1.silverpop.com/XMLAPI` | `https://api1.silverpop.com` |
   | sp-e2 | `https://api.engage2.silverpop.com/XMLAPI` | `https://api2.silverpop.com` |
   | sp-e3 | `https://api.engage3.silverpop.com/XMLAPI` | `https://api3.silverpop.com` |
   | sp-e4 | `https://api.engage4.silverpop.com/XMLAPI` | `https://api4.silverpop.com` |
   | sp-e5 | `https://api.engage5.silverpop.com/XMLAPI` | `https://api5.silverpop.com` |
   | sp-e6 | `https://api.pilot.silverpop.com/XMLAPI` | `https://api6.silverpop.com` |

1. Klicka **Spara alla**. AEM är nu redo att ansluta till Silverpop över skyddade slutpunkter.

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)
