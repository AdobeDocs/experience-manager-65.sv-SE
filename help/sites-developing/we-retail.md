---
title: Implementering av referens för Vi.butik
seo-title: Implementering av referens för Vi.butik
description: Vi.Retail är en förhandstitt på teknik för en referensimplementering som visar det rekommenderade sättet att konfigurera en onlinenärvaro med AEM
seo-description: Vi.Retail är en förhandstitt på teknik för en referensimplementering som visar det rekommenderade sättet att konfigurera en onlinenärvaro med AEM
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# Implementering av referens för Vi.butik{#we-retail-reference-implementation}

## Introduktion {#introduction}

Vi.Retail är en referensimplementering och exempelinnehåll som illustrerar det rekommenderade sättet att skapa en onlinenärvaro med Adobe Experience Manager.

Vi.Retail använder de senaste AEM-teknikerna som HTML, responsiva layouter, redigerbara mallar, kärnkomponenter med mera.

Även om sajten är en vertikal butiksskylt kan den konfigureras på alla vertikala ytor, och endast produktkatalogen och kundvagnsfunktionerna är butiksspecifika.

## Funktioner {#features}

Som AEM:s standardimplementering av referenser presenterar vi några av de mest kraftfulla funktionerna i AEM.

| **Funktion** | **Beskrivning** | **Intresserad?** |
|---|---|---|
| [Globaliserad webbplatsstruktur](/help/sites-administering/tc-bp.md) | Vi.Retail innehåller språkmallar som kopieras live till landsspecifika sajter. | [Prova!](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [Responsiv layout](/help/sites-authoring/responsive-layout.md) | Alla sidor har en responsiv layout som anpassas dynamiskt efter skärm- och enhetsstorlek. | [Prova!](/help/sites-developing/we-retail-responsive-layout.md) |
| [Redigerbara mallar](/help/sites-developing/page-templates-editable.md) | Alla sidor är baserade på redigerbara mallar, som gör att icke-utvecklare kan anpassa och anpassa mallarna. | [Prova!](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML-mallspråk](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) | Alla komponenter är baserade på HTML |  |
| [eCommerce-funktioner](/help/sites-developing/ecommerce.md) | Innehåller en produktkatalog |  |
| [Communities](/help/communities/overview.md) | Låt besökarna delta i communitydiskussioner, läsa bloggar och mycket mer |  |
| [Kärnkomponenter](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) | Alla komponenter baseras på de nya kärnkomponenterna och är mer användbara och användarkonfigurerbara. | [Prova!](/help/sites-developing/we-retail-core-components.md) |
| [Innehållsfragment](/help/assets/content-fragments.md) | Avsnittet&quot;We.Retail Experiences&quot; visar möjligheterna att återanvända innehåll via innehållsfragment. | [Prova dem!](/help/sites-developing/we-retail-content-fragments.md) |
| [Upplevelsefragment](/help/sites-authoring/experience-fragments.md) | Ett Experience Fragment är en grupp med en eller flera komponenter, inklusive innehåll och layout, som kan refereras till på sidor. | [Prova dem!](/help/sites-developing/we-retail-experience-fragments.md) |

## Komma igång {#getting-started}

Vi.Retail levereras som AEM:s exempelinnehåll. Om du vill använda programmet [startar du bara AEM som vanligt](/help/sites-deploying/deploy.md#getting-started)och ser till att exempelinnehållet inte är inaktiverat.

>[!CAUTION]
>
>Vi.Retail ska inte installeras på produktionsinstanser. Produktionsinstanser ska startas i `nosamplecontent`[körläge](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>Vi.Retail baseras på den senaste AEM-tekniken och stöder därför inte [klassisk gränssnittsutveckling](/help/sites-classic-ui-authoring/home.md).

### Senaste version {#latest-version}

Även om vi.Retail distribueras med AEM-versionen kan uppdateringar av innehållet och dess funktioner göras efter releasen. Det är därför möjligt att [hämta den senaste versionen från GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) och sedan [överföra](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) och [installera](/help/sites-administering/package-manager.md#installing-packages) den som ett paket på din AEM-instans.

### Steg 1 {#first-steps}

1. När AEM har startats (och/eller vi.Retail har installerats) är webbplatsen **We.Retail** tillgänglig i [webbplatskonsolen](/help/sites-authoring/basic-handling.md#global-navigation).
1. Följande sida kan till exempel öppnas och ska se ut som i [bilagan](#appendix) nedan:

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## Vi.Retail &amp; Geometrixx {#we-retail-geometrixx}

Geometrixx och dess många tävlingsbidrag fungerade som exempelinnehåll i tidigare versioner av AEM. Sedan version 6.3 har We.Retail varit det exempelinnehåll som levererats med AEM och fungerar som den nya standardimplementeringen av referenser.

Vi.Detaljhandeln är tekniskt sett mer robust och utnyttjar den senaste AEM-tekniken för att vara mer flexibel och skalbar, samtidigt som vi demonstrerar de senaste funktionerna i produkten.

### Funktionsjämförelse {#feature-comparison}

Tabellen nedan ger en översikt över de viktigaste funktionerna som är tillgängliga i We.Retail jämfört med Geometrixx.

* **Tillgängliga** innebär att exempel på funktionen finns i exempelinnehållet.
* **Inte tillgängligt** betyder att exempel på funktionen inte är tillgängliga i exempelinnehållet, men inte betyder att själva funktionen inte är det.

| **Funktion** | **Vi.butik** | **Geometrixx** |
|---|---|---|
| Globaliserad webbplatsstruktur | Språkmallsidor som live-kopieras till landsspecifika webbplatser | Inte tillgängligt |
| Innehållsfragment | Tillgänglig | Inte tillgängligt |
| Upplevelsefragment | Tillgänglig | Inte tillgängligt |
| Responsiv layout | För alla sidor | Endast Geometrixx-media |
| Redigerbara mallar | För alla sidor | Inte tillgängligt |
| HTL | Alla komponenter | Begränsad |
| Målinriktning | För alla sidor | Endast geometrixx utomhus |
| Skärmar | Tillgänglig | Inte tillgängligt |
| Mobil | Inte tillgängligt | Tillgänglig |
| Manuscript | Inte tillgängligt | Tillgänglig |
| Carousel, nedladdning, diagramkomponenter | Inte tillgängligt | Tillgänglig |
| Kolumnkontroll | Ersatt av layoutbehållare | Tillgänglig |
| Formulär | Inte tillgängligt | Tillgänglig |
| Campaign | Inga e-postexempel | Tillgänglig |

>[!NOTE]
>
>Denna förteckning skall vara fullständig, men skall inte anses uttömmande.

## Contribute {#contribute}

Vi.Retail har släppts som ett öppen källkodsprojekt och den senaste versionen av källkoden kan hämtas från GitHub.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-sample-we-retail-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)

Den senaste versionen kan också [laddas ned direkt](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest) som ett installerbart paket.

Om du råkar ut för problem kan du rapportera [GitHub-problem](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

Du kan fritt göra gaffel eller bidra med [pull-förfrågningar](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls).

## Förhandsgranska {#preview}

Förhandsgranskning av välkomstsidan för Vi.Retail:

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)

