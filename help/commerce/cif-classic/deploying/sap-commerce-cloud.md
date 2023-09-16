---
title: Distribuera e-handel med SAP Commerce Cloud
description: Lär er hur ni driftsätter e-handel med SAP Commerce Cloud.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: ecbd0097-c407-4581-bab2-4729a71df4a3
source-git-commit: b00ed4ed146b89aece9af1d267c890a360a236e9
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# SAP COMMERCE CLOUD{#sap-commerce-cloud}

>[!NOTE]
>
>Den här sidan innehåller länkar till hybris webbplats. För vissa sidor behöver du ett konto för att logga in.

## Distribuera e-handel med SAP Commerce Cloud {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>Följande procedurer använder följande demonstrationskatalog för att illustrera distributionen:
>
>`Geometrixx Outdoors Site English (US)`

Distribuera [nödvändiga e-handelspaket](#packages-needed-for-ecommerce-with-hybris) tillhandahåller eCommerce-ramverkets alla funktioner, tillsammans med en referensimplementering av eCommerce-funktionaliteten i enlighet med en hybris-implementering (inklusive en demonstrationskatalog)

Detta finns tillgängligt under den engelska (USA) grenen ( `/content/geometrixx-outdoors/en_US`) på Geometrixx Outdoors webbplats:

* [Produktinformation](#productinformationwithcolorvariants) (med färgvarianter när det är lämpligt)

* [Innehållsöversikter för kundvagn](#shoppingcartcontentoverview)
* [Kundregistrering](#customersignup) och [Kundinloggning](#customersignin)

* [Tillgång till hybris Management Console](#accesstothehybrismanagementconsole)

### Tekniska krav - hybris Server {#technical-requirements-hybris-server}

hybris-tillägget i eCommerce Integration Framework har uppdaterats för att stödja Hybris 5 (som standard), samtidigt som bakåtkompatibiliteten med [Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* Stöder version 18.11 och senare.
>* Du behöver Java™ 7 för att köra [hybris 5-server.](https://www.sap.com/products/crm.html)
* hybris-tillägget, [Telco Accelerator](https://www.sap.com/products/crm.html), stöds inte av AEM.
>

### Paket som behövs för e-handel med hybris {#packages-needed-for-ecommerce-with-hybris}

För att installera e-handelsfunktioner behöver du:

* Din hybris-server
* AEM e-handelsramverk:

   * detta är en del av en AEM

* AEM Geometrixx-all-paket:

   * `cq-geometrixx-all-pkg`

* Innehållspaket AEM hybris:

   * `cq-hybris-content-6.3.2`
   * hybrisspecifik API-implementering
   * `cq-geometrixx-hybris-content-6.3.2`
   * en referensimplementering för att illustrera användningen av hybris ( `geometrixx-outdoors/en_US`)

### Installation av e-handel med hybris {#installation-of-ecommerce-with-hybris}

Så här installerar du en fullständig konfiguration (med demonstrationskatalogen Geometrixx Outdoors):

1. [Installera AEM](/help/sites-deploying/deploy.md).
1. Installera hela Geometrixx

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. Installera demonstrationsinnehållspaketen med [Pakethanteraren](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Ladda ned och bygg upp hybris Server](#download-and-build-your-hybris-server).
1. Skapa din katalog i din eCommerce-motor:

   1. [Ställ in Geometrixx utomhusbutik](#setup-the-geometrixx-outdoors-store).

1. [Upphovsman](/help/sites-authoring/qg-page-authoring.md) eventuella tilläggssidor som du behöver i AEM.

>[!CAUTION]
>
Användning av hybris-servern kräver en separat hybris-licens.

>[!NOTE]
>
För utvecklare [API-dokumentation](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) finns också för nedladdning.

### Ladda ned och bygg en hybris-server {#download-and-build-your-hybris-server}

Stegen i den här proceduren hämtar och bygger hybris-servern. Den gör också de initiala konfigurationer som krävs för kopplingarna mellan hybris och cq. Tillägget kan sedan användas med standardinställningarna.

>[!CAUTION]
>
Hybriversioner tidigare än 5.5.1 stöds inte.

>[!NOTE]
>
För att slutföra detta behöver du [Groovy](https://groovy-lang.org/) installerade på datorn.

1. Ladda ned **hybris Commerce Suite** distribution från hybris nedladdningsplats.

   >[!CAUTION]
   >
   Du behöver ett konto (från hybris) för att komma åt detta.

1. Zippa upp distributionsfilen på önskad plats (kallas &lt;hybris-root-directory>).
1. Kör följande från kommandoraden:

   ```shell
   cd <hybris-root-directory>/bin/platform
   . ./setantenv.sh
   ant clean all
   cd ../..
   ```

   >[!NOTE]
   >
   Vid körning:
   >
   `ant clean all`
   >
   Tryck `Return` vid behov.

1. Ladda ned följande filer till rotmappen för din extraherade hybris-distribution,

   ```
       <hybris-root-directory>
   ```


[Hämta fil](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   Använd följande setup.groovy för hybris 5.6.0 och senare.

   5.6.0 och senare

[Hämta fil](/help/sites-deploying/assets/setup-1.groovy)

1. Kör följande från kommandoraden till:

   * uppdatera hybris-serverns konfiguration (som krävs av tillägget)
   * återskapa hybris-servern med den ändrade konfigurationen
   * starta servern

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   Beroende på ditt system kan flera av dessa åtgärder ta flera minuter att slutföra.

1. I webbläsaren går du till **Administrationskonsol för hybris** vid:

   [http://localhost:9002](http://localhost:9002)

1. Klicka **Initiera** och bekräfta sedan initieringsåtgärden (allt eftersom befintliga data tas bort).

   Förloppet visas på konsolen med `FINISHED` som anger att åtgärden har slutförts.

   >[!NOTE]
   >
   Beroende på ditt system kan det ta flera minuter att slutföra detta.

### Konfigurera Geometrixx Outdoors Store {#setup-the-geometrixx-outdoors-store}

Den här proceduren överför och konfigurerar demonstrationsbutiken - Geometrixx Online.

1. Starta hybris-instansen. Kör följande från kommandoraden:

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. I webbläsaren går du till **Hanteringskonsol för hybris** vid:

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   Använd dessa autentiseringsuppgifter:
   * användarnamn: admin
   * lösenord: nimda

1. Expandera från sidofältsnavigeringen **System** och **verktyg**. Välj sedan **Importera** för att öppna **Guide: CSV-import** -fönstret.
1. I **Konfiguration** tab, **Överför** följande **Importera fil**:

[Hämta fil](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. Ange **Språkinställning** till:

   `en_US - English (United States)`

1. Öppna **Resurs** -fliken.
1. **Överför** följande **Media-Zip**:

[Hämta fil](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. Klicka **Starta** om du vill importera de angivna filerna. The **Resultat** -fliken visar alla loggposter.

1. Klicka **Klar** för att stänga importfönstret.

1. Välj **System** sedan **verktyg** sedan **Importera**.

1. **Överför** följande **Importera fil**:

[Hämta fil](/help/sites-deploying/assets/base-store.csv)

   Använd följande för hybris 5.7:

[Hämta fil](/help/sites-deploying/assets/base-store-5_7.csv)

1. Ange **Språkinställning** till:

   `en_US - English (United States)`

1. Klicka **Starta** om du vill importera de angivna filerna. The **Resultat** -fliken visar alla loggposter.

1. Klicka **Klar** för att stänga importfönstret.

1. Nu kan du använda produktcockpit för att visa de importerade katalogerna och produkterna:

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
