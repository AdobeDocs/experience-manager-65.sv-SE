---
title: Redigera sidinnehåll
description: Innehåll läggs till med komponenter som kan dras till sidan. Du kan sedan redigera dem på plats, flytta eller ta bort dem.
uuid: e7b65ceb-263c-46f2-91e3-11dec3a016fa
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: de321869-ebf9-41a1-8203-e12bdb088678
docset: aem65
exl-id: e1b5aea0-983c-4e7b-9d35-d7beeee45dc7
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 0%

---

# Redigera sidinnehåll{#editing-page-content}

När sidan har skapats (antingen ny eller som en del av en lansering eller en live-kopia) kan du redigera innehållet för att få de uppdateringar du behöver.

Innehåll läggs till med [komponenter](/help/sites-classic-ui-authoring/classic-page-author-default-components.md) (anpassat till innehållstypen) som kan dras till sidan. Du kan sedan redigera dem på plats, flytta eller ta bort dem.

>[!NOTE]
>
>Ditt konto behöver [lämpliga åtkomsträttigheter](/help/sites-administering/security.md) och [behörigheter](/help/sites-administering/security.md#permissions) om du vill redigera sidor, till exempel lägga till, redigera eller ta bort komponenter, göra anteckningar, låsa upp.
>
>Om du råkar ut för problem rekommenderar vi att du kontaktar systemadministratören.

## Sidekick {#sidekick}

Sidsparken är ett nyckelverktyg när du skapar sidor. Det flyter när du redigerar en sida, så det är alltid synligt.

Det finns flera flikar och ikoner, bland annat:

* Komponenter
* Sida
* Information
* Versioner
* Arbetsflöde
* Lägen
* Ställning
* Klientkontext
* Webbplatser

![chlimage_1-71](assets/chlimage_1-71.png)

Dessa ger tillgång till ett brett urval av funktioner, bland annat:

* [markera komponenter](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick)
* [visa referenser](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#showing-references)
* [åtkomst till granskningsloggen](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#audit-log)
* [byta läge](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
* [skapa](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#creating-a-new-version), [återställa](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick) och [jämföra](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#comparing-with-a-previous-version) versioner

* [publicera](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#publishing-a-page), [avpublicera](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#unpublishing-a-page) en sida

* [redigera sidegenskaper](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)

* [ställningar](/help/sites-authoring/scaffolding.md)

* [klientkontext](/help/sites-administering/client-context.md)

## Infoga en komponent {#inserting-a-component}

### Infoga en komponent {#inserting-a-component-1}

När du har öppnat sidan kan du börja lägga till innehåll. Det gör du genom att lägga till komponenter (kallas även stycken).

Så här infogar du en ny komponent:

1. Det finns flera sätt att välja den typ av stycke som du vill infoga:

   * Dubbelklicka på området med etiketten **Dra komponenter eller resurser hit..** - **Infoga ny komponent** verktygsfältet öppnas. Markera en komponent och klicka på **OK**.

   * Dra en komponent från det flytande verktygsfältet (kallas sidospark) för att infoga ett nytt stycke.
   * Högerklicka på ett befintligt stycke och välj **Nytt...** - verktygsfältet Infoga ny komponent öppnas. Markera en komponent och klicka på **OK**.

   ![screen_shot_2012-02-15at115605am](assets/screen_shot_2012-02-15at115605am.png)

1. I både sidesparken och **Infoga ny komponent** visas en lista med tillgängliga komponenter (stycketyper). Dessa kan delas upp i olika avsnitt (t.ex. Allmänt, Kolumner o.s.v.) som kan färdigställas efter behov.

   Beroende på din produktionsmiljö kan dessa alternativ skilja sig åt. Fullständig information om komponenter finns i [Standardkomponenter](/help/sites-classic-ui-authoring/classic-page-author-default-components.md).

1. Infoga komponenten som du vill ha på sidan. Dubbelklicka sedan på stycket så öppnas ett fönster där du kan konfigurera stycket och lägga till innehåll.

### Infoga en komponent med hjälp av Innehållssökning {#inserting-a-component-using-the-content-finder}

Du kan också lägga till en ny komponent på sidan genom att dra en resurs från [Content Finder](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder). Då skapas automatiskt en ny komponent av lämplig typ som innehåller resursen.

Detta gäller för följande tillgångstyper (vissa kommer att vara beroende av sid-/styckesystem):

| Resurstyp | Resulterande komponenttyp |
|---|---|
| Bild | Bild |
| Dokument | Ladda ned |
| Produkt | Produkt |
| Video | Flash |

>[!NOTE]
>
>Det här beteendet kan konfigureras för din installation. Se [Konfigurera ett styckesystem så att en komponentinstans skapas när en resurs dras](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) för mer information.

Så här skapar du en komponent genom att dra en av resurstyperna ovan:

1. Kontrollera att sidan finns i [**Redigera** läge](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes).
1. Öppna [Content Finder](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder).
1. Dra den önskade resursen till önskad position. The [platshållare för komponent](#componentplaceholder) visar var komponenten kommer att placeras.

   En komponent som passar resurstypen skapas på den önskade platsen, den innehåller den valda resursen.

1. [Redigera](#editmovecopypastedelete) komponenten om det behövs.

## Redigera en komponent (innehåll och egenskaper) {#editing-a-component-content-and-properties}

Om du vill redigera ett befintligt stycke gör du något av följande:

* **Dubbelklicka** det stycke som ska öppnas. Du ser samma fönster som när du skapade stycket med det befintliga innehållet. Gör ändringarna och klicka **OK**.

* **Högerklicka** stycket och klicka på **Redigera**.

* **Klicka** två gånger på stycket (ett långsamt dubbelklick) för att gå in i redigeringsläget på plats. Du kan redigera texten direkt på sidan i stället för i ett dialogrutefönster. I det här läget visas ett verktygsfält högst upp på sidan. Gör bara dina ändringar så sparas de automatiskt.

## Flytta en komponent {#moving-a-component}

Flytta ett stycke:

>[!NOTE]
>
>Du kan också använda [Klipp ut och klistra in](#cut-copy-paste-a-component) för att flytta en komponent.

1. Markera det stycke som ska flyttas:

   ![screen_shot_2012-02-15at115855am](assets/screen_shot_2012-02-15at115855am.png)

1. Dra stycket till den nya platsen - AEM anger var stycket kan flyttas med en grön bock. Släpp den där du vill.
1. Stycket flyttas:

   ![screen_shot_2012-02-15at120030pm](assets/screen_shot_2012-02-15at120030pm.png)

## Ta bort en komponent {#deleting-a-component}

Ta bort ett stycke:

1. Markera stycket och **högerklicka**:

   ![screen_shot_2012-02-15at120220pm](assets/screen_shot_2012-02-15at120220pm.png)

1. Välj **Ta bort** på menyn. AEM WCM begär en bekräftelse på att du vill ta bort stycket eftersom åtgärden inte kan ångras.
1. Klicka **OK**.

>[!NOTE]
>
>Om du har ställt in [Användaregenskaper som visar verktygsfältet Global redigering](/help/sites-classic-ui-authoring/author-env-user-props.md) Du kan även utföra vissa åtgärder på stycken med hjälp av **Kopiera**, **Klipp ut**, **Klistra in**, **Ta bort** tillgängliga knappar.
>
>Olika [kortkommandon](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) finns också.

## Klipp ut/kopiera/klistra in en komponent {#cut-copy-paste-a-component}

Som när [Ta bort en komponent](#deleting-a-component) du kan använda snabbmenyn för att kopiera, klippa ut och/eller klistra in en komponent

>[!NOTE]
>
>Om du har ställt in [Användaregenskaper som visar verktygsfältet Global redigering](/help/sites-classic-ui-authoring/author-env-user-props.md) Du kan även utföra vissa åtgärder på stycken med hjälp av **Kopiera**, **Klipp ut**, **Klistra in**, **Ta bort** tillgängliga knappar.
>
>Olika [kortkommandon](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) finns också.

>[!NOTE]
>
>Det går bara att klippa ut, kopiera och klistra in innehåll på samma sida.

## Ärvda komponenter {#inherited-components}

Ärvda komponenter kan vara produkten av olika scenarier, bland annat:

* [Hantering av flera webbplatser](/help/sites-administering/msm.md), även i kombination med [ställningar](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md#scaffolding-with-msm-inheritance).

* [Startar](/help/sites-classic-ui-authoring/classic-launches.md) (baserat på livecopy).
* Specifika komponenter, till exempel det ärvda styckesystemet i Geometrixx.

Du kan avbryta (och sedan återaktivera) arvet. Beroende på vilken komponent det gäller kan det här vara tillgängligt från:

1. **Live Copy**

   Om en komponent är en del av en livecopy eller en start visas den med en hänglåsikon. Du kan klicka på hänglåset för att avbryta arvet.

   * hänglåsikonen visas när komponenten är markerad, till exempel:

   ![chlimage_1-72](assets/chlimage_1-72.png)

   * hänglåset visas också i komponentdialogen, till exempel:

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. **Ett ärvt styckesystem**

   Konfigurationsdialogrutan. Som med det ärvda styckesystemet i Geometrixx:

   ![chlimage_1-74](assets/chlimage_1-74.png)

## Lägga till anteckningar {#adding-annotations}

[Anteckningar](/help/sites-classic-ui-authoring/classic-page-author-annotations.md) kan andra författare ge feedback på ditt innehåll. Detta används ofta för granskning och validering.

## Förhandsgranska sidor {#previewing-pages}

Det finns två ikoner i den nedre kanten av sidesparten som är viktiga för att förhandsgranska sidor:

![Sidosparens nedre kant med en vågrät rad på sju ikoner. Två av ikonerna i början av raden, redigeringsikonen och förhandsvisningsikonen, indikeras av en pennsymbol respektive en förstoringsglassymbol.](do-not-localize/chlimage_1-5.png)

* Pennikonen visar att du befinner dig i redigeringsläge där du kan lägga till, ändra, flytta eller ta bort innehåll.

  ![Redigeringsikonen indikeras av en pennsymbol.](do-not-localize/chlimage_1-6.png)

* Med förstoringsglaset kan du välja förhandsvisningsläge där sidan visas som den kommer att visas i publiceringsmiljön (en uppdatering av sidan behövs ibland):

  ![Ikonen för förhandsvisningsläge indikeras av en förstoringsglassymbol.](do-not-localize/chlimage_1-7.png)

  I förhandsgranskningsläget minskas sidosparken genom att klicka på nedpilsikonen för att återgå till redigeringsläget:

  ![En stapel med AEM som titel och en ikon för redigeringsläge till höger om titeln, som indikeras av en nedpilssymbol.](do-not-localize/chlimage_1-8.png)

## Sök och ersätt {#find-replace}

För större skalredigeringar av samma fras är **[Sök och ersätt](/help/sites-classic-ui-authoring/author-env-search.md#find-and-replace)** kan du söka efter och ersätta flera förekomster av en sträng i ett avsnitt på webbplatsen.

## Låsa en sida {#locking-a-page}

AEM kan du låsa en sida så att ingen annan kan ändra innehållet. Det här är användbart när du gör många ändringar på en viss sida eller när du behöver frysa en sida en kort stund.

>[!CAUTION]
>
>Låsning av en sida bör användas med försiktighet eftersom den enda person som kan låsa upp en sida är den person som låste den (eller ett konto med administratörsbehörighet).

Lås en sida:

1. I **Webbplatser** markerar du sidan som du vill låsa.
1. Dubbelklicka på sidan för att öppna den för redigering.
1. I **Sida** sidosparkflik, välja **Lås sida**:

   ![screen_shot_2012-02-08at15750pm](assets/screen_shot_2012-02-08at15750pm.png)

   Ett meddelande visar att sidan är låst för andra användare. I den högra rutan i **Webbplatser** konsol, AEM WCM visar sidan som låst och anger vilken användare som har låst sidan.

   ![screen_shot_2012-02-08at20657pm](assets/screen_shot_2012-02-08at20657pm.png)

## Låsa upp en sida {#unlocking-a-page}

Lås upp en sida:

1. I **Webbplatser** markerar du sidan som du vill låsa upp.
1. Dubbelklicka på sidan för att öppna den.
1. I **Sida** sidosparkflik, välja **Lås upp sida**.

## Ångra och göra om sidredigeringar {#undoing-and-redoing-page-edits}

Använd följande kortkommandon när innehållsramen på sidan är i fokus:

* Ångra: Ctrl+Z (Windows) eller Cmd+Z (Mac)
* Gör om: Ctrl+Y (Windows) eller Cmd+Y (Mac)

När du ångrar eller gör om borttagning, tillägg eller omplacering av ett eller flera stycken markeras de berörda styckena med blinkande (standardbeteende).

>[!NOTE]
>
>Se [Ångra och göra om sidredigeringar - The Theory](#undoing-and-redoing-page-edits-the-theory) om du vill ha fullständig information om vad som är möjligt när du ångrar och gör om sidredigeringar.

## Ångra och göra om sidredigeringar - The Theory {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>Systemadministratören kan [konfigurera olika aspekter av funktionerna Ångra/Gör om](/help/sites-administering/config-undo.md) enligt kraven för din instans.

AEM lagrar en historik över åtgärder som du utför och i vilken ordning du utförde dem. Du ångrar därför flera åtgärder i den ordning som du utförde dem. Sedan kan du använda gör om för att återanvända en eller flera av åtgärderna.

Om ett element på innehållssidan är markerat gäller kommandot ångra och gör om det markerade objektet, till exempel en textkomponent.

Funktionen för kommandona Ångra och Gör om liknar den i andra program. Använd kommandona för att återställa webbsidans senaste status när du fattar beslut om innehållet. Om du till exempel flyttar ett textstycke till en annan plats på sidan kan du använda kommandot Ångra för att flytta tillbaka stycket. Om du sedan bestämmer dig för att flytta stycket igen använder du kommandot gör om.

>[!NOTE]
>
>Du kan:
>
>* gör om åtgärder så länge du inte har gjort någon sidredigering sedan du använde Ångra.
>* Ångra högst 20 redigeringsåtgärder (standardinställning).
>* också använda [Kortkommandon](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) för att ångra och göra om.
>

Du kan använda Ångra och Gör om för följande typer av sidändringar:

* Lägga till, redigera, ta bort och flytta stycken
* Redigera styckeinnehåll direkt
* Kopiera, klippa ut och klistra in objekt på en sida
* Kopiera, klippa ut och klistra in objekt över sidor
* Lägga till, ta bort och ändra filer och bilder
* Lägga till, ta bort och ändra anteckningar och skisser
* Ändringar i ställningar
* Lägga till och ta bort referenser
* Ändra egenskapsvärden i komponentdialogrutor.

Formulärfält som formulärkomponenter återger ska inte ha värden som anges vid redigering av sidor. Kommandona Ångra och Gör om påverkar därför inte ändringar som du gör i värdena för dessa typer av komponenter. Du kan till exempel inte ångra valet av ett värde i en nedrullningsbar lista.

>[!NOTE]
>
>Särskilda behörigheter krävs för att ångra och göra om ändringar i filer och bilder. Ångra-historiken för ändringar av filer och bilder varar i minst några timmar. Efter den här gången kan du dock inte ångra ändringarna. Din administratör kan ange behörigheter och ändra standardtiden på tio timmar.
