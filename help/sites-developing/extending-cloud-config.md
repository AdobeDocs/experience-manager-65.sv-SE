---
title: Cloud Service Configurations
description: Du kan utöka de befintliga instanserna för att skapa egna konfigurationer
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 20a19ee5-7113-4aca-934a-a42c415a8d93
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Cloud Service Configurations{#cloud-service-configurations}

Konfigurationer är utformade för att tillhandahålla logik och struktur för lagring av tjänstkonfigurationer.

Du kan utöka de befintliga instanserna för att skapa egna konfigurationer.

## Concepts {#concepts}

De principer som har använts vid utvecklingen av konfigurationerna har baserats på följande begrepp:

* Tjänster/adaptrar används för att hämta konfigurationer.
* Konfigurationer (till exempel egenskaper/stycken) ärvs från de överordnade.
* Refereras från analysnoder via sökväg.
* Enkelt att bygga ut.
* Har flexibiliteten att klara mer komplexa konfigurationer, som [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics).
* Stöd för beroenden (t.ex. [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) plugin-program behöver [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) konfiguration).

## Struktur {#structure}

Konfigurationens grundsökväg är:

`/etc/cloudservices`.

För varje typ av konfiguration tillhandahålls en mall och en komponent. Detta gör det möjligt att ha konfigurationsmallar som kan uppfylla de flesta behov efter att ha anpassats.

Så här konfigurerar du nya tjänster:

* Skapa en tjänst i

  `/etc/cloudservices`

* Under följande:

   * en konfigurationsmall
   * en konfigurationskomponent

Mallen och komponenten måste ärva `sling:resourceSuperType` från basmallen:

`cq/cloudserviceconfigs/templates/configpage`

Eller baskomponent

`cq/cloudserviceconfigs/components/configpage`

Tjänsteleverantören bör även tillhandahålla tjänstsidan:

`/etc/cloudservices/<service-name>`

### Mall {#template}

Din mall utökar basmallen:

`cq/cloudserviceconfigs/templates/configpage`

Och definiera `resourceType` som pekar på den anpassade komponenten.

```xml
/libs/cq/analytics/templates/sitecatalyst
sling:resourceSuperType = cq/cloudserviceconfigs/templates/configpage
allowedChildren = /libs/cq/analytics/templates/sitecatalyst
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
componentReference = cq/analytics/components/sitecatalyst
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/sitecatalystpage

/libs/cq/analytics/templates/generictracker
sling:resourceSuperType = cq/cloudservices/templates/configpage
allowedChildren = /libs/cq/analytics/templates/generictracker
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/generictrackerpage
```

### Komponenter {#components}

Komponenten bör utöka baskomponenten:

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

När du har konfigurerat mallen och komponenten kan du lägga till din konfiguration genom att lägga till undersidor under:

`/etc/cloudservices/<service-name>`

### Innehållsmodell {#content-model}

Innehållsmodellen lagras som `cq:Page` under:

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

Konfigurationerna lagras under undernoden `jcr:content`.

* Fasta egenskaper som definieras i en dialogruta ska lagras på `jcr:node` direkt.
* Dynamiska element (med `parsys` eller `iparsys`) använder du en undernod för att lagra komponentdata.

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

Referensdokumentation om API:t finns i [com.day.cq.wcm.webservicesupport](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html).

### AEM {#aem-integration}

Tillgängliga tjänster visas i **Cloud Services** -fliken i **Sidegenskaper** dialogruta (för alla sidor som ärver från `foundation/components/page` eller `wcm/mobile/components/page`).

Fliken innehåller även:

* en länk till den plats där du kan aktivera tjänsten
* välj en konfiguration (undernod till tjänsten) från ett sökvägsfält

#### Lösenordskryptering {#password-encryption}

När inloggningsuppgifter för tjänsten lagras bör alla lösenord krypteras.

Du kan uppnå detta genom att lägga till ett dolt formulärfält. Det här fältet ska ha anteckningen `@Encrypted` i egenskapsnamnet, det vill säga, för `password` fältet som namnet skulle skrivas som:

`password@Encrypted`

Egenskapen krypteras sedan automatiskt (med `CryptoSupport` på `EncryptionPostProcessor`.

>[!NOTE]
>
>Detta liknar standarden ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` anteckningar.

>[!NOTE]
>
>Som standard är `EcryptionPostProcessor` endast krypterar `POST` förfrågningar `/etc/cloudservices`.

#### Ytterligare egenskaper för tjänstsidans jcr:innehållsnoder {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>Egenskap</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>Referenssökväg till en komponent som ska inkluderas automatiskt på sidan.<br /> Detta används för ytterligare funktioner och JS-tillägg.<br /> Detta inkluderar komponenten på sidan där<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> ingår (normalt före <code>body</code> tagg).<br /> När det gäller Adobe Analytics och Adobe Target använder vi detta för att inkludera ytterligare funktioner, som JavaScript-anrop för att spåra besökares beteende.</td>
  </tr>
  <tr>
   <td>description</td>
   <td>Kort beskrivning av tjänsten.<br /> </td>
  </tr>
  <tr>
   <td>descriptionExtended</td>
   <td>Utökad beskrivning av tjänsten.</td>
  </tr>
  <tr>
   <td>rankning</td>
   <td>Tjänstrankning för användning i listor.</td>
  </tr>
  <tr>
   <td>selectableChildren</td>
   <td>Filter för att visa konfigurationer i dialogrutan för sidegenskaper.</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>URL till tjänstens webbplats.</td>
  </tr>
  <tr>
   <td>serviceUrlLabel</td>
   <td>Etikett för tjänst-URL.</td>
  </tr>
  <tr>
   <td>thumbnailPath</td>
   <td>Sökväg till miniatyrbild för tjänsten.</td>
  </tr>
  <tr>
   <td>visible</td>
   <td>Synlighet i dialogrutan för sidegenskaper. visas som standard (valfritt)</td>
  </tr>
 </tbody>
</table>

### Användningsexempel {#use-cases}

Dessa tjänster tillhandahålls som standard:

* [Spårarkodfragment](/help/sites-administering/external-providers.md) (Google, WebTrends osv.)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
<!-- Search&Promote is end of life as of September 1, 2022 * [Search&Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote) -->
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>Se även [Skapa en anpassad Cloud Service](/help/sites-developing/extending-cloud-config-custom-cloud.md).
