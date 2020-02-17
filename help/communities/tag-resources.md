---
title: Aktiveringsresurser för taggning
seo-title: Aktiveringsresurser för taggning
description: Om du taggar aktiveringsresurser kan du filtrera resurser och utbildningssökvägar när medlemmar bläddrar i kataloger
seo-description: Om du taggar aktiveringsresurser kan du filtrera resurser och utbildningssökvägar när medlemmar bläddrar i kataloger
uuid: daf8a4f4-486b-498c-99e9-d1533a830e64
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c012d639-c6e6-4f73-bbd8-78a4baa38c17
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Aktiveringsresurser för taggning {#tagging-enablement-resources}

## Översikt {#overview}

Om du taggar aktiveringsresurser kan du filtrera resurser och utbildningssökvägar när medlemmar bläddrar i [kataloger](functions.md#catalog-function).

I grund och botten:

* [Skapa ett taggnamnutrymme](../../help/sites-administering/tags.md#creating-a-namespace) för varje katalog

   * [Ange taggbehörigheter](../../help/sites-administering/tags.md#setting-tag-permissions)

      * Endast för communitymedlemmar (sluten community)

         * Tillåt läsåtkomst för [communityplatsens medlemsgrupp](users.md#publish-group-roles)
      * För alla webbplatsbesökare, oavsett om de är inloggade eller anonyma (öppen community)

         * Tillåt läsåtkomst för `Everyone`gruppen
   * [Publicera taggarna](../../help/sites-administering/tags.md#publishing-tags)



* [Definiera omfattningen av taggar för en community-webbplats](sites-console.md#tagging)

   * [Konfigurera kataloger som finns i platsens struktur](functions.md#catalog-function)

      * Kan lägga till taggar i kataloginstansen för att styra listan med taggar som finns i gränssnittsfiltren
      * Kan lägga till [förfilter](catalog-developer-essentials.md#pre-filters)för att begränsa katalogernas inkluderade resurser

* [Publicera communitywebbplatsen](sites-console.md#publishing-the-site)
* [Använd taggar för aktiveringsresurser](resources.md#create-a-resource) så att de kan filtreras kategoriserat
* [Publicera aktiveringsresurserna](resources.md#publish)

## Taggar för communitywebbplats {#community-site-tags}

När du skapar eller redigerar en community-webbplats anger [taggningsinställningen](sites-console.md#tagging) omfattningen för de taggar som är tillgängliga för funktioner på webbplatsen genom att markera en delmängd av de befintliga taggnamnutrymmena.

Även om taggar kan skapas och läggas till på communitywebbplatsen när som helst, bör du utforma en taxonomi i förväg, ungefär som när du utformar en databas. Se [Använda taggar](../../help/sites-authoring/tags.md).

När du senare lägger till taggar i en befintlig communitywebbplats måste du spara redigeringen innan du kan lägga till den nya taggen i en katalogfunktion i platsens struktur.

För en communitywebbplats måste du aktivera läsåtkomst för medlemmar i communityn efter att webbplatsen har publicerats och taggarna har publicerats. Se [Ange taggbehörigheter](../../help/sites-administering/tags.md#setting-tag-permissions).

Så här visas det i CRXDE när en administratör tillämpar läsbehörigheter på `/etc/tags/ski-catalog` gruppen `Community Enable Members`.

![chlimage_1-420](assets/chlimage_1-420.png)

## Namnutrymmen för katalogtaggar {#catalog-tag-namespaces}

Katalogfunktionen använder taggar för att definiera sig själv. När du konfigurerar katalogfunktionen på en communitywebbplats definieras den uppsättning taggnamnutrymmen som du väljer bland av omfånget för de taggnamnutrymmen som angetts för communitywebbplatsen.

Katalogfunktionen innehåller en tagginställning som definierar taggarna som finns i katalogens filtergränssnitt. Inställningen Alla namnutrymmen hänvisar till omfånget för de taggnamnutrymmen som har valts för communitywebbplatsen.

![chlimage_1-421](assets/chlimage_1-421.png)

## Tillämpa taggar på aktiveringsresurser {#applying-tags-to-enablement-resources}

Aktiveringsresurser och utbildningsvägar visas i alla kataloger när `Show in Catalog` det är markerat. Om du lägger till taggar i resurser och utbildningsvägar kan du förfiltrera i specifika kataloger och filtrera i kataloggränssnittet.

Du kan begränsa aktiveringsresurser och utbildningsvägar till specifika kataloger genom att skapa [förfilter](catalog-developer-essentials.md#pre-filters).

Med kataloggränssnittet kan besökare använda ett taggfilter i listan över resurser och utbildningssökvägar som visas i katalogen.

Administratören som använder taggarna i aktiveringsresurserna måste känna till de taggnamnutrymmen som är associerade med katalogerna samt taxonomin för att kunna välja en undertagg för mer detaljerad kategorisering.

Om ett `ski-catalog` namnutrymme till exempel skapades och angavs för en katalog med namnet `Ski Catalog`kan det ha två underordnade taggar: `lesson-1` och `lesson-2`.

Alla aktiveringsresurser som är taggade med något av följande:

* skidkatalog:
* skidkatalog:lektion-1
* skidkatalog:lektion-2

visas i `Ski Catalog` efter att aktiveringsresursen har publicerats.

![chlimage_1-422](assets/chlimage_1-422.png)

## Visa katalog vid publicering {#viewing-catalog-on-publish}

När allt har konfigurerats från författarmiljön och publicerats kan upplevelsen av att använda katalogen för att hitta aktiveringsresurser upplevas i publiceringsmiljön.

Om inga taggnamnutrymmen visas i listrutan kontrollerar du att behörigheterna har angetts korrekt i publiceringsmiljön.

Om taggnamnutrymmen har lagts till och saknas kontrollerar du att taggarna och webbplatsen har publicerats på nytt.

Om inga aktiveringsresurser visas efter att du har valt en tagg när du visar katalogen kontrollerar du att en tagg från katalogens namnutrymmen används för aktiveringsresursen.

![chlimage_1-423](assets/chlimage_1-423.png)

