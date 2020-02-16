---
title: Klassiskt gränssnitt, taggningskonsol
seo-title: Klassiskt gränssnitt, taggningskonsol
description: Lär dig mer om den klassiska UI-taggningskonsolen.
seo-description: Lär dig mer om den klassiska UI-taggningskonsolen.
uuid: 51e29422-f967-424b-a7fd-4ca2ddc6b8a3
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: b279c033-bc93-4e62-81ad-123c40b9fdd2
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# Klassiskt gränssnitt, taggningskonsol{#classic-ui-tagging-console}

Det här avsnittet gäller för den klassiska UI-taggningskonsolen.

Den pekoptimerade UI-taggningskonsolen är [här](/help/sites-administering/tags.md#tagging-console).

Så här kommer du åt konsolen Klassisk UI-taggning:

* on author
* logga in med administratörsbehörighet
* bläddra till konsolen, till exempel [https://localhost:4502/tagging](https://localhost:4502/tagging)

![](assets/managing_tags_usingthetagasministrationconsole.png)

## Skapa taggar och namnutrymmen {#creating-tags-and-namespaces}

1. Beroende på vilken nivå du börjar på kan du skapa en tagg eller ett namnutrymme med **Nytt**:

   Om du väljer **Taggar** kan du skapa ett namnutrymme:

   ![](assets/creating_tags_andnamespaces.png)

   Om du väljer ett namnutrymme (till exempel **Demo**) kan du skapa en tagg i det namnutrymmet:

   ![](assets/creating_tags_andnamespacesinnewnamespace.png)

1. I båda fallen anger du

   * **Titel**(*obligatoriskt*) Visningsrubriken för taggen. Alla tecken kan anges, men du bör inte använda dessa specialtecken:

      * `colon (:)` - namnutrymmesavgränsare
      * `forward slash (/)` - avgränsare för undertagg
      Dessa tecken visas inte om de anges.

   * **Namn**(*obligatoriskt*) Taggens nodnamn.

   * **Beskrivning**(*valfritt*) En beskrivning av taggen.

   * välj **Skapa**


## Redigera taggar {#editing-tags}

1. Markera den tagg som du vill redigera i den högra rutan.
1. Click **Edit**.
1. Du kan ändra **Titel** och **Beskrivning**.
1. Stäng dialogrutan genom att klicka på **Spara** .

## Ta bort taggar {#deleting-tags}

1. Markera den tagg som du vill ta bort i den högra rutan.
1. Click **Delete**.
1. Stäng dialogrutan genom att klicka på **Ja** .

   Taggen ska inte längre listas.

## Aktivera och inaktivera taggar {#activating-and-deactivating-tags}

1. I den högra rutan markerar du namnutrymmet eller taggen som du vill aktivera (publicera) eller inaktivera (avpublicera).
1. Klicka på **Aktivera** eller **Inaktivera** efter behov.

## Lista - visa var taggar refereras {#list-showing-where-tags-are-referenced}

**List** öppnar ett nytt fönster med sökvägarna till alla sidor som använder den markerade taggen:

![](assets/list_showing_wheretagsarereferenced.png)

## Flytta taggar {#moving-tags}

För att tagga administratörer och utvecklare så att de kan rensa taxonomin eller byta namn på ett tagg-ID kan du flytta en tagg till en ny plats:

1. Öppna **taggningskonsolen** .
1. **Markera taggen och klicka på** Flytta... i det övre verktygsfältet (eller på snabbmenyn).
1. I dialogrutan **Flytta tagg** definierar du:

   * **till** målnoden.
   * **Byt namn till**, det nya nodnamnet.

1. Klicka på **Flytta**.

Dialogrutan **Flytta tagg** ser ut så här:

![](assets/move_tag.png)

>[!NOTE]
>
>Författare bör inte flytta taggar eller byta namn på ett tagg-ID. Vid behov bör författare endast [ändra taggtitlarna](#editing-tags).

## Sammanfoga taggar {#merging-tags}

Du kan använda sammanfogningstaggar när en taxonomi har dubbletter. När tagg A sammanfogas med tagg B kommer alla sidor som taggas med tagg A att taggas med tagg B och tagg A är inte längre tillgängliga för författare.

Så här sammanfogar du en tagg till en annan:

1. Öppna **taggningskonsolen** .
1. **Markera taggen och klicka på** Sammanfoga... i det övre verktygsfältet (eller på snabbmenyn).
1. I dialogrutan **Sammanfoga tagg** definierar du:

   * **till** målnoden.

1. Klicka på **Sammanfoga**.

Dialogrutan **Sammanfoga tagg** ser ut så här:

![](assets/mergetag.png)

## Räknar användning av taggar {#counting-usage-of-tags}

Så här ser du hur många gånger en tagg används:

1. Öppna **taggningskonsolen** .
1. Klicka på **Räkna användning** i det övre verktygsfältet: i kolumnen Antal visas resultatet.

## Hantera taggar på olika språk {#managing-tags-in-different-languages}

Den valfria `title`egenskapen för en tagg kan översättas till flera språk. Taggen `titles` kan sedan visas beroende på användarspråk eller sidspråk.

### Definiera taggtitlar på flera språk {#defining-tag-titles-in-multiple-languages}

Följande procedur visar hur du översätter `title`taggen **Djur** till engelska, tyska och franska:

1. Gå till **taggningskonsolen** .
1. Redigera taggen **Djur** under **Taggar** > **Stock Photography**.
1. Lägg till översättningarna på följande språk:

   * **Engelska**: Djur
   * **Tyska**: Tiere
   * **Franska**: Animaux

1. Spara ändringarna.

Dialogrutan ser ut så här:

![](assets/edit_tag.png)

Taggningskonsolen använder språkinställningen för användaren, så för taggen Animal visas Animaux för en användare som anger språket som franska i användaregenskaperna.

Om du vill lägga till ett nytt språk i dialogrutan läser du avsnittet [Lägga till ett nytt språk i dialogrutan](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) Redigera tagg i avsnittet **Tagga för utvecklare** .

### Visa taggtitlar i Sidegenskaper på ett visst språk {#displaying-tag-titles-in-page-properties-in-a-specified-language}

Som standard visas taggen `titles`i sidegenskaperna på sidspråket. Dialogrutan Tagg i sidegenskaperna har ett språkfält där du kan visa taggen `titles`på ett annat språk. I proceduren nedan beskrivs hur du visar taggen `titles`på franska:

1. Se föregående avsnitt för att lägga till den franska översättningen till **Djur** under **Taggar** > **Stock Photography**.
1. Öppna sidegenskaperna för sidan **Produkter** i den engelska grenen av webbplatsen **Geometrixx** .
1. Öppna dialogrutan **Taggar/nyckelord** (genom att välja den nedrullningsbara menyn till höger om visningsområdet Taggar/nyckelord) och välj det **franska** språket i den nedrullningsbara menyn i det nedre högra hörnet.
1. Bläddra med vänster-/högerpilarna tills du kan välja fliken **Stock Photography**

   Markera taggen **Djur** (**Animaux**) och markera utanför dialogrutan för att stänga den och lägga till taggen i sidegenskaperna.

   ![](assets/french_tag.png)

Som standard visas taggen `titles`enligt sidspråket i dialogrutan Sidegenskaper.

I allmänhet hämtas taggens språk från sidspråket om sidspråket är tillgängligt. När [ `tag` widgeten](/help/sites-developing/building.md#tagging-on-the-client-side) används i andra fall (till exempel i formulär eller i dialogrutor) beror taggspråket på sammanhanget.

>[!NOTE]
>
>I taggmolnet och meta-nyckelorden i standardsidkomponenten används den lokaliserade taggen `titles`baserat på sidspråket, om det är tillgängligt.