---
title: Hantera innehållsfragment
seo-title: Hantera innehållsfragment
description: Innehållsfragment lagras som resurser, så hanteras främst från resurskonsolen.
seo-description: Innehållsfragment lagras som resurser, så hanteras främst från resurskonsolen.
uuid: 675e1a6b-2583-488f-bbb4-210daed3e1b0
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: 21a18d60-f3fe-4048-9949-8416b5cb4596
docset: aem65
feature: Content Fragments
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '1491'
ht-degree: 10%

---


# Hantera innehållsfragment{#managing-content-fragments}

Innehållsfragment lagras som **Resurser**, så hanteras primärt från konsolen **Resurser**.

>[!NOTE]
>
>Innehållsfragment används sedan med redigeringssidor; se [Sidredigering med innehållsfragment](/help/sites-authoring/content-fragments.md).

## Skapa innehållsfragment {#creating-content-fragments}

### Skapa en innehållsmodell {#creating-a-content-model}

[Modellskanning ](/help/assets/content-fragments/content-fragments-models.md) av innehållsfragment kan aktiveras och skapas innan innehållsfragment med strukturerat innehåll skapas.

>[!NOTE]
>
>Mer information om mallar finns i [Utveckla innehållsfragment](/help/sites-developing/customizing-content-fragments.md). används för enkla innehållsfragment.

### Skapa ett innehållsfragment {#creating-a-content-fragment}

Metoden för att skapa ett innehållsfragment är (i princip) densamma för både enkla och strukturerade fragment:

1. Navigera till mappen **Resurser** där du vill skapa fragmentet.
1. Välj **Skapa** och sedan **Innehållsfragment** för att öppna guiden.
1. I det första steget i guiden måste du ange grunden för det nya fragmentet.

   * Detta kan vara en:

      * [Mall](/help/sites-developing/content-fragment-templates.md)  - till exempel  **Enkelt fragment**

      * [Modell](/help/assets/content-fragments/content-fragments-models.md)  - använd för att skapa ett fragment som kräver strukturerat innehåll. till exempel  **** flygplatsmodellen
   * Alla tillgängliga mallar och modeller visas.

   Efter markeringen använder du **Nästa** för att fortsätta.

   ![cfm-6420-15](assets/cfm-6420-15.png)

1. Ange följande i steget **Egenskaper**:

   * **Grundläggande**

      * **Titel**

         Fragmenttiteln.

         Obligatorisk.

      * **Beskrivning**

      * **Taggar**
   * **Avancerat**

      * **Namn**

         Namnet; används för att skapa URL:en.

         Obligatoriskt. hämtas automatiskt från titeln, men kan uppdateras.


1. Välj **Skapa** för att slutföra åtgärden och **Öppna** sedan fragmentet för redigering eller gå tillbaka till konsolen med **Klar**.

## Åtgärder för ett innehållsfragment {#actions-for-a-content-fragment}

I konsolen **Resurser** finns en rad åtgärder tillgängliga för dina innehållsfragment, antingen:

* Från verktygsfältet; när du har valt fragmentet är alla lämpliga åtgärder tillgängliga.
* Som [snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions); en delmängd av åtgärder som är tillgängliga för de enskilda fragmentkorten.

![cfm-6420-17](assets/cfm-6420-17.png)

Markera fragmentet för att visa verktygsfältet med tillämpliga åtgärder:

* **Hämta**

   * Spara fragmentet som en ZIP-fil; du kan definiera om element, variationer och metadata ska inkluderas.

* **Skapa**
* **Utcheckning**
* **Egenskaper**

   * Gör att du kan visa och/eller redigera fragmentets metadata.

* **Redigera**

   * Gör att du kan [öppna fragmentet för redigering av innehåll](/help/assets/content-fragments/content-fragments-variations.md) tillsammans med dess element, variationer, tillhörande innehåll och metadata.

* **Hantera taggar**
* **Till samling**

   * Lägg till fragmentet i en samling.
   * Detta kan också göras när [en samling kopplas till fragmentet](/help/assets/content-fragments/content-fragments-assoc-content.md#adding-associated-content).

* **Kopiera**/**klistra in**

* **Flytta**
* **Snabbpublicering**
* **Hantera publikation**
* **Ta bort**

>[!NOTE]
>
>Många av dessa är [standardåtgärder för Assets](/help/assets/manage-assets.md) och/eller [AEM skrivbordsappen](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html).

## Öppna fragmentredigeraren {#opening-the-fragment-editor}

Så här öppnar du fragmentet för redigering:

>[!CAUTION]
>
>Om du vill redigera ett innehållsfragment behöver du [de behörigheter som krävs](/help/sites-developing/customizing-content-fragments.md#asset-permissions). Kontakta systemadministratören om du har problem.

1. Använd konsolen **Resurser** för att navigera till platsen för ditt innehållsfragment.
1. Öppna fragmentet för redigering, antingen genom att:

   * Klicka/tryck på fragment- eller fragment-länken (detta beror på konsolvyn).
   * Markera fragmentet och **Redigera** i verktygsfältet.

   Fragmentredigeraren öppnas:

   ![cfm-6420-18](assets/cfm-6420-18.png)

   >[!NOTE]
   >
   >1. Ett meddelande visas när fragmentet redan refereras på en innehållssida.
   >2. Sidpanelen kan döljas/visas med ikonen **Växla sidpanel**.


1. Navigera genom de tre lägena med ikonerna på sidopanelen:

   * Variationer: [Redigera innehållet](#editing-the-content-of-your-fragment) och [Hantera dina variationer](#creating-and-managing-variations-within-your-fragment)

   * [Anteckningar](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
   * [Associerat innehåll](#associating-content-with-your-fragment)
   * [Metadata](#viewing-and-editing-the-metadata-properties-of-your-fragment)

   ![cfm-10](assets/cfm-10.png)

1. När du har gjort ändringarna använder du **Spara** eller **Avbryt** efter behov.

   >[!NOTE]
   >
   >Både **Spara** och **Avbryt** avslutar redigeraren. Mer information om hur båda alternativen fungerar för innehållsfragment finns i [Spara, Avbryt och Versioner](#save-cancel-and-versions).

## Spara, Avbryt och Versioner {#save-cancel-and-versions}

>[!NOTE]
>
>Versioner kan också [skapas, jämföras och återställas från tidslinjen](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

Redigeraren har två alternativ:

* **Spara**

   Sparar de senaste ändringarna och avslutar redigeraren.

   >[!CAUTION]
   >
   >Om du vill redigera ett innehållsfragment behöver du [de behörigheter som krävs](/help/sites-developing/customizing-content-fragments.md#asset-permissions). Kontakta systemadministratören om du har problem.

   >[!NOTE]
   >
   >Det går att vara kvar i redigeraren och göra en serie ändringar innan du väljer **Spara**.

   >[!CAUTION]
   >
   >Förutom att bara spara ändringarna uppdaterar **Spara** alla referenser och ser till att dispatchern rensas efter behov. Dessa ändringar kan ta tid att bearbeta. På grund av detta kan prestandan påverkas på ett stort/komplext/tungt belastat system.
   >
   >
   >Tänk på detta när du använder **Spara** och ange sedan snabbt fragmentredigeraren igen för att göra och spara ytterligare ändringar.

* **Avbryt**

   Redigeraren avslutas utan att de senaste ändringarna sparas.

När du redigerar ditt innehållsfragment skapar AEM automatiskt versioner för att säkerställa att tidigare innehåll kan återställas om du **avbryter** dina ändringar:

1. När ett innehållsfragment öppnas för redigering AEM söker efter den cookie-baserade token som anger om det finns en *redigeringssession*:

   1. Om token hittas betraktas fragmentet som en del av den befintliga redigeringssessionen.
   2. Om token är *inte* tillgänglig och användaren börjar redigera innehåll, skapas en version och en token för den nya redigeringssessionen skickas till klienten, där den sparas i en cookie.

2. När det finns en *aktiv* redigeringssession sparas innehållet som redigeras automatiskt var 600:e sekund (standard).

   >[!NOTE]
   >
   >Intervallet för att spara automatiskt kan konfigureras med hjälp av mekanismen `/conf`.
   >
   >
   >Standardvärde, se:
   >
   >
   >`/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. Om användaren väljer att **avbryta** redigeringen återställs den version som skapades i början av redigeringssessionen och token tas bort för att avsluta redigeringssessionen.
4. Om användaren väljer att **spara** redigeringarna sparas de uppdaterade elementen/varianterna och token tas bort för att avsluta redigeringssessionen.

## Redigera innehållet i fragmentet {#editing-the-content-of-your-fragment}

När du har öppnat fragmentet kan du använda fliken [Variationer](/help/assets/content-fragments/content-fragments-variations.md) för att skapa innehållet.

## Skapa och hantera variationer i fragment {#creating-and-managing-variations-within-your-fragment}

När du har skapat det Överordnad innehållet kan du skapa och hantera [Variationer](/help/assets/content-fragments/content-fragments-variations.md) av det innehållet.

## Koppla innehåll till fragment {#associating-content-with-your-fragment}

Du kan även [associera innehåll](/help/assets/content-fragments/content-fragments-assoc-content.md) med ett fragment. Detta ger en anslutning så att resurser (t.ex. bilder) kan användas (valfritt) med fragmentet när det läggs till på en innehållssida.

## Visa och redigera metadata (egenskaper) för fragmentet {#viewing-and-editing-the-metadata-properties-of-your-fragment}

Du kan visa och redigera egenskaperna för ett fragment på fliken [Metadata](/help/assets/content-fragments/content-fragments-metadata.md).

## Tidslinje för innehållsfragment {#timeline-for-content-fragments}

Förutom standardalternativen innehåller [Tidslinjen](/help/assets/manage-assets.md#timeline) både information och åtgärder som är specifika för innehållsfragment:

* Visa information om versioner, kommentarer och anteckningar
* Åtgärder för versioner

   * **[Återgå till den här versionen](#reverting-to-a-version)**  (välj ett befintligt fragment, sedan en specifik version)

   * **[Jämför med aktuell](#comparing-fragment-versions)**  (välj ett befintligt fragment och sedan en specifik version)

   * Lägg till en **etikett** och/eller **Kommentar** (välj ett befintligt fragment och sedan en specifik version)

   * **Spara som version**  (markera ett befintligt fragment och sedan uppilen längst ned på tidslinjen)

* Åtgärder för anteckningar

   * **Ta bort**

>[!NOTE]
>
>Kommentarerna är:
>
>* Standardfunktionalitet för alla resurser
>* Skapat i tidslinjen
>* Relaterat till fragmentresursen

>
>
Anteckningar (för innehållsfragment) är:
>
>* Anges i fragmentredigeraren
>* Specifik för ett markerat textsegment i fragmentet

>



Till exempel:

![cfm-6420-19-2019](assets/cfm-6420-19-2019.png)

## Jämföra fragmentversioner {#comparing-fragment-versions}

Åtgärden **Jämför med aktuell** är tillgänglig från [tidslinjen](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) när du har valt en specifik version.

Detta öppnas:

* **Aktuell** (senaste) version (vänster)

* den valda versionen **v&lt;*x.y*>** (höger)

De visas sida vid sida, där:

* Eventuella skillnader markeras

   * Borttagen text - röd
   * Infogad text - grön
   * Ersatt text - blå

* Med helskärmsikonen kan du öppna båda versionerna separat; växla sedan tillbaka till den parallella vyn
* Du kan **återställa** till den specifika versionen
* **** Donewill return you to the console

>[!NOTE]
>
>Du kan inte redigera fragmentinnehållet när du jämför fragment.

![cfm-6420-20](assets/cfm-6420-20.png)

## Återställer till version {#reverting-to-a-version}

Du kan återgå till en viss version av fragmentet:

* Direkt från [tidslinjen](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

   Välj önskad version och sedan åtgärden **Återställ till denna version**.

* När du jämför en version med den aktuella versionen](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) kan du **återställa** till den valda versionen.[

## Publicera och referera till ett fragment {#publishing-and-referencing-a-fragment}

>[!CAUTION]
>
>Om fragmentet är baserat på en modell bör du kontrollera att [modellen har publicerats](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
>
>Om du publicerar ett innehållsfragment för vilket modellen ännu inte har publicerats, visas detta i en urvalslista och modellen publiceras med fragmentet.

Innehållsfragment måste publiceras för användning i publiceringsmiljön. De kan publiceras:

* Efter skapande; från konsolen **Resurser**.
* När du [publicerar en sida som använder fragmentet](/help/sites-authoring/content-fragments.md#publishing); fragmentet kommer att listas i sidreferenserna.

>[!CAUTION]
>
>När ett fragment har publicerats och/eller refererats visar AEM en varning när en författare öppnar fragmentet för redigering igen. Detta är för att varna för att ändringar i avsnittet även påverkar de refererade sidorna.

## Ta bort ett fragment {#deleting-a-fragment}

Så här tar du bort ett fragment:

1. I konsolen **Resurser** navigerar du till platsen för innehållsfragmentet.
2. Markera fragmentet.

   >[!NOTE]
   >
   >Åtgärden **Ta bort** är inte tillgänglig som en snabbåtgärd.

3. Välj **Ta bort** från verktygsfältet.
4. Bekräfta åtgärden **Ta bort**.

   >[!CAUTION]
   >
   >Om fragmentet redan finns på en sida visas ett varningsmeddelande och du måste bekräfta att du vill fortsätta med **Tvinga borttagning**. Fragmentet, tillsammans med dess innehållskomponentfragment, tas bort från alla innehållssidor.

