---
title: Implementering av referens för Vi.butik
description: Vi.Retail är en förhandstitt på teknik för en referensimplementering som visar det rekommenderade sättet att konfigurera en onlinenärvaro med AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 504c61c7-dcd3-412c-9239-d24a2b78e4b9
source-git-commit: 4b5b3ac41034bd4cc0f359b35cac0515b76ca64e
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---

# Implementering av referens för Vi.butik{#we-retail-reference-implementation}

## Introduktion {#introduction}

Vi.Retail är en referensimplementering och exempelinnehåll som illustrerar det rekommenderade sättet att konfigurera en onlinenärvaro med Adobe Experience Manager.

Vi.Retail använder de senaste Adobe Experience Manager-teknikerna (AEM) som HTML, responsiva layouter, redigerbara mallar, kärnkomponenter med mera.

Även om det visar en vertikal butiksadress kan sajten konfigureras på alla vertikala ytor, och endast produktkatalogen och kundvagnsfunktionerna är butiksspecifika.

## Funktioner {#features}

Som AEM standardimplementering av referenser visar vi nu några av de mest kraftfulla funktionerna i AEM.

| **Funktion** | **Beskrivning** | **Intresserad?** |
|---|---|---|
| [Globaliserad webbplatsstruktur](/help/sites-administering/tc-bp.md) | Vi.Retail innehåller språkmallar som kopieras live till landsspecifika sajter. | [Prova!](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [Responsiv layout](/help/sites-authoring/responsive-layout.md) | Alla sidor har en responsiv layout som anpassar sig dynamiskt till skärm- och enhetsstorlek. | [Prova!](/help/sites-developing/we-retail-responsive-layout.md) |
| [Redigerbara mallar](/help/sites-developing/page-templates-editable.md) | Alla sidor är baserade på redigerbara mallar, som gör att icke-utvecklare kan anpassa och anpassa mallarna. | [Prova!](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML mallspråk](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) | Alla komponenter är baserade på HTML |  |
| [eCommerce-funktioner](/help/commerce/cif-classic/developing/ecommerce.md) | Innehåller en produktkatalog |  |
| [Communities-webbplatser](/help/communities/overview.md) | Låt besökarna delta i communitydiskussioner, läsa bloggar och mycket mer |  |
| [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) | Alla komponenter baseras på de nya kärnkomponenterna och är mer användbara och användarkonfigurerbara. | [Prova!](/help/sites-developing/we-retail-core-components.md) |
| [Innehållsfragment](/help/assets/content-fragments/content-fragments.md) | Avsnittet&quot;We.Retail Experiences&quot; visar möjligheterna att återanvända innehåll med hjälp av innehållsfragment. | [Prova dem!](/help/sites-developing/we-retail-content-fragments.md) |
| [Experience Fragments](/help/sites-authoring/experience-fragments.md) | Ett Experience Fragment är en grupp med en eller flera komponenter, inklusive innehåll och layout, som kan refereras till på sidor. | [Prova dem!](/help/sites-developing/we-retail-experience-fragments.md) |

## Komma igång {#getting-started}

Vi.Retail levereras som AEM exempelinnehåll. Om du vill använda [starta AEM som vanligt](/help/sites-deploying/deploy.md#getting-started)kontrollerar du att exempelinnehållet inte är inaktiverat.

>[!CAUTION]
>
>Installera inte We.Retail på produktionsinstanser. Produktionsinstanser ska startas i `nosamplecontent` [körningsläge](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>Vi.Retail bygger på den senaste AEM tekniken och stöder därför inte [Skapa klassiskt användargränssnitt](/help/sites-classic-ui-authoring/classic-page-author-first-steps.md).

### Senaste version {#latest-version}

Även om vi.Retail distribueras tillsammans med AEM kan uppdateringar av innehållet och dess funktioner göras efter releasen. Det är därför möjligt att [ladda ned den senaste versionen från GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) och sedan [ladda upp](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) och [installera](/help/sites-administering/package-manager.md#installing-packages) det som ett paket i AEM.

### Steg 1 {#first-steps}

1. När AEM har startats (och/eller vi.Retail har installerats) är platsen **Vi.butik** finns i [Platskonsol](/help/sites-authoring/basic-handling.md#global-navigation).
1. Följande sida kan till exempel öppnas och ska se ut som i [appendix](#appendix) nedan:

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## Vi.Detaljhandel &amp; Geometrixx {#we-retail-geometrixx}

Geometrixx och dess många inkvisitioner fungerade som exempelinnehåll i tidigare versioner av AEM. Sedan version 6.3 har We.Retail varit det exempelinnehåll som levererats med AEM och fungerar som den nya standardimplementeringen av referenser.

Vi.Detaljhandeln är tekniskt sett mer robust och utnyttjar den senaste AEM tekniken för att vara mer flexibel och skalbar, samtidigt som vi visar på de senaste funktionerna i produkten.

### Funktionsjämförelse {#feature-comparison}

Tabellen nedan ger en översikt över de viktigaste funktionerna som är tillgängliga i We.Retail jämfört med Geometrixx.

* **Tillgänglig** betyder att exempel på funktionen finns i exempelinnehållet.
* **Inte tillgängligt** betyder att exempel på funktionen inte är tillgängliga i exempelinnehållet, men inte betyder att själva funktionen inte är det.

| **Funktion** | **Vi.butik** | **Geometrixx** |
|---|---|---|
| Globaliserad webbplatsstruktur | Språkmallsidor som live-kopieras till landsspecifika webbplatser | Inte tillgängligt |
| Innehållsfragment | Tillgänglig | Inte tillgängligt |
| Upplevelsefragment | Tillgänglig | Inte tillgängligt |
| Responsiv layout | För alla sidor | Endast Geometrixx Media |
| Redigerbara mallar | För alla sidor | Inte tillgängligt |
| HTL | Alla komponenter | Begränsad |
| Målinriktning | För alla sidor | Endast Geometrixx Outdoors |
| Skärmar | Tillgänglig | Inte tillgängligt |
| Mobil | Inte tillgängligt | Tillgänglig |
| Manuscript | Inte tillgängligt | Tillgänglig |
| Carousel-visningsprogram, nedladdningar och diagramkomponenter | Inte tillgängligt | Tillgänglig |
| Kolumnkontroll | Ersatt av layoutbehållare | Tillgänglig |
| Forms | Inte tillgängligt | Tillgänglig |
| Campaign | Inga e-postexempel | Tillgänglig |

>[!NOTE]
>
>Denna förteckning skall vara fullständig, men skall inte anses uttömmande.

## Contribute {#contribute}

Vi.Retail har släppts som ett öppen källkodsprojekt och den senaste versionen av källkoden kan hämtas från GitHub.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub.

* [Öppna aem-sample-we-retail-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* Hämta projektet som [en ZIP-fil](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/zip/refs/heads/master)

Den senaste versionen kan också [direkt nedladdad](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/tag/we.retail.reactor-4.0.0) som ett installerbart paket.

Om du råkar ut för problem kan du skicka en [GitHub-problem](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

Du kan vara fri från gaffel eller bidra med [pull-förfrågningar](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls).

## Förhandsgranska {#preview}

Förhandsgranskning av välkomstsidan för Vi.Retail:

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
