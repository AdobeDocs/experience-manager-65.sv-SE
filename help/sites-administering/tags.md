---
title: Administrera taggar
seo-title: Administrera taggar
description: Lär dig hur du administrerar taggar i AEM.
seo-description: Lär dig hur du administrerar taggar i AEM.
uuid: 77e1280a-feea-4edd-94b6-4fb825566c42
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 69253ee9-8c28-436b-9331-6fb875f64cba
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Administrera taggar {#administering-tags}

Taggar är ett snabbt och enkelt sätt att klassificera innehåll på en webbplats. De kan ses som nyckelord eller etiketter (metadata) som gör att innehåll kan hittas snabbare som ett resultat av en sökning.

I Adobe Experience Manager (AEM) kan en tagg vara en egenskap för

* en innehållsnod för en sida (se [Använda taggar](/help/sites-authoring/tags.md))

* en metadatanod för en resurs (se [Hantera metadata för digitala resurser](/help/assets/metadata.md))

Förutom sidor och resurser används taggar för AEM Communities-funktioner

* användargenererat innehåll (se [Tagga UGC)](/help/communities/tag-ugc.md)

* Aktivera resurser (se [Tagga aktiveringsresurser](/help/communities/functions.md#catalog-function))

## Märkordsfunktioner {#tag-features}

Några av funktionerna i taggarna i AEM är:

* Taggar kan grupperas i olika namnutrymmen. Sådana hierarkier tillåter att taxonomier skapas. Dessa taxonomier är globala i hela AEM.
* Huvudbegränsningen för nyligen skapade taggar är att de måste vara unika inom ett specifikt namnutrymme.
* En taggs namn får inte innehålla separationstecken för taggsökväg (de kommer inte att visas om sådana finns)

   * kolon `:` - avgränsar namnutrymmestaggen
   * snedstreck `/` - avgränsar undertaggar

* Taggar kan användas av författare och webbplatsbesökare. Oavsett vem som skapat dem blir alla typer av taggar tillgängliga för markering, både när du tilldelar till en sida och när du söker.
* Taggar kan skapas och deras taxonomi ändras av medlemmar i gruppen&quot;tagghanterare&quot; och medlemmar som har ändringsbehörighet till `/content/cq:tags`.

   * En tagg som innehåller underordnade taggar kallas behållartagg
   * En tagg som inte är en behållartagg kallas för en lövtagg
   * Ett taggnamnutrymme är antingen en lövtagg eller behållartagg

* Taggar används av [sökkomponenten](https://helpx.adobe.com/experience-manager/core-components/using/quick-search.html) för att underlätta sökning efter innehåll.
* Taggar används av [Teaser-komponenten](https://helpx.adobe.com/experience-manager/core-components/using/teaser.html), som övervakar en användares taggmoln för att tillhandahålla riktat innehåll.
* Om taggning är en viktig aspekt av ditt innehåll

   * se till att paketera taggar med de sidor där de används
   * kontrollera att [taggbehörigheter](#setting-tag-permissions) aktiverar läsåtkomst

## Taggningskonsolen {#tagging-console}

Taggningskonsolen används för att skapa och hantera taggar och deras taxonomier. Ett av målen är att undvika att ha många liknande taggar som i princip gäller samma sak: till exempel sidor och sidor eller skor och skor.

Taggar hanteras genom att gruppera i namnutrymmen, granska användningen av befintliga taggar innan du skapar nya och ordna om taggen utan att koppla från det aktuella innehållet.

Så här kommer du åt taggningskonsolen:

* on author
* logga in med administratörsbehörighet
* från global navigering

   * select **`Tools`**
   * select **`General`**
   * select **`Tagging`**

![managing_tags_using_thetagasminister_console](assets/managing_tags_usingthetagasministrationconsolea.png)

### Skapa ett namnutrymme {#creating-a-namespace}

Om du vill skapa ett nytt namnutrymme väljer du **`Create Namespace`** ikonen .

Namnutrymmet är i sig en tagg och behöver inte innehålla några undertaggar. Om du vill fortsätta skapa en taxonomi [skapar du undertaggar](#creating-tags), som i sin tur kan vara antingen lövtaggar eller behållartaggar.

![chlimage_1-183](assets/chlimage_1-183a.png) ![creating_tags_andnamespaces](assets/creating_tags_andnamespacesa.png)

* **Titel**
   *(obligatoriskt)* En visningsrubrik för namnutrymmet.

* **Namn**
   *(valfritt)* Ett namn för namnutrymmet. Om inget anges skapas ett giltigt nodnamn från titeln. Se [TaggID](/help/sites-developing/framework.md#tagid).

* **Beskrivning**
   *(valfritt)* En beskrivning av namnutrymmet.

När den obligatoriska informationen har angetts

* välj **Skapa**

### Åtgärder för taggar {#operations-on-tags}

Om du väljer ett namnutrymme eller en annan tagg blir följande åtgärder tillgängliga:

* [Visa egenskaper](#viewing-tag-properties)
* [Referenser](#showing-tag-references)
* [Skapa tagg](#creating-tags)
* [Redigera](#editing-tags)
* [Flytta](#moving-tags)
* [Sammanfoga](#merging-tags)
* [Publicera](#publishing-tags)
* [Avpublicera](#unpublishing-tags)
* [Ta bort](#deleting-tags)

![chlimage_1-184](assets/chlimage_1-184.png)

När webbläsarfönstret inte är tillräckligt brett för att visa alla ikoner grupperas ikonerna längst till höger tillsammans under en **`... More`** ikon, som visar en listruta med ikoner för dolda åtgärder när de är markerade.

![chlimage_1-185](assets/chlimage_1-185.png)

### Välja en namnområdestagg {#selecting-a-namespace-tag}

Om namnutrymmet inte innehåller några taggar visas egenskaperna till höger när det är markerat, annars visas de underordnade taggarna. Varje markerad tagg visar antingen de taggar den innehåller eller dess egenskaper om den inte har underordnade taggar.

Om du vill markera taggen för åtgärder, och om du vill markera flera, markerar du bara ikonen bredvid titeln. Om du väljer titeln visas endast egenskaper eller så öppnas taggen för att visa dess innehåll.

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### Visa taggegenskaper {#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

När du markerar ett namnutrymme eller en annan tagg visas information om **`View Properties`** , tidpunkten för den senaste redigeringen och antalet referenser när du markerar `name`ikonen. Om den publiceras visas den tidpunkt den senast publicerades och utgivarens id. Den här informationen visas i en kolumn till vänster om taggkolumnerna.

![chlimage_1-189](assets/chlimage_1-189.png)

### Visar taggreferenser {#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

När ett namnutrymme eller en annan tagg är markerad och du väljer ikonen **Referenser** för att identifiera innehållet som taggen har tillämpats på.

Den inledande visningen är antalet taggar som används.

![chlimage_1-191](assets/chlimage_1-191.png)

Genom att markera pilen till höger om antalet listas referensnamnen.

Sökvägen till referensen visas som ett verktygstips när du håller pekaren över en referens.

![chlimage_1-192](assets/chlimage_1-192.png)

### Skapa taggar {#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

När ett namnutrymme eller en annan tagg är markerad (genom att markera ikonen bredvid titeln) kan en underordnad tagg skapas för den aktuella taggen genom att markera **`Create Tag`** -ikonen.

![chlimage_1-194](assets/chlimage_1-194.png)

* **Titel***(obligatoriskt) *En visningsrubrik för taggen.

* **Namn***(valfritt) *Ett namn för taggen. Om inget anges skapas ett giltigt nodnamn från titeln. Se [TaggID](/help/sites-developing/framework.md#tagid).

* **Beskrivning***(valfritt) *En beskrivning av taggen.

När den obligatoriska informationen har angetts

* välj **Skapa**

### Redigera taggar {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

När du markerar ett namnutrymme eller en annan tagg kan du ändra titeln, beskrivningen och ange lokalisering för titeln genom att välja ikonen **`Edit`**.

När du har redigerat väljer du **Spara**.

Mer information om hur du lägger till språköversättningar finns i avsnittet [Hantera taggar på olika språk](#managing-tags-in-different-languages).

![chlimage_1-196](assets/chlimage_1-196.png)

### Flytta taggar {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

När ett namnutrymme eller en annan tagg är markerad kan tagghanterare och utvecklare rensa upp taxonomin genom att flytta taggen till en ny plats eller byta namn på den genom att markera ikonen. **`Move`** När den markerade taggen är en behållartagg flyttas även alla underordnade taggar om du flyttar taggen.

>[!NOTE]
>
>Vi rekommenderar att författare endast får [redigera](#editing-tags) taggens `title`namn, inte flytta eller byta namn på taggar.

![chlimage_1-198](assets/chlimage_1-198.png)

* **Bana**
   *(skrivskyddat)* Den aktuella sökvägen till den markerade taggen.

* **Gå till** Bläddra till den nya sökvägen under vilken du vill flytta taggen.

* **Byt namn till** Inledande visar `name`taggens aktuella namn. Du `name`kan ange ett nytt värde.

* välj **Spara**

### Sammanfoga taggar {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

Du kan använda sammanfogningstaggar när en taxonomi har dubbletter. När tagg A sammanfogas med tagg B kommer alla sidor som taggas med tagg A att taggas med tagg B och tagg A är inte längre tillgängliga för författare.

När du markerar ett namnutrymme eller en annan tagg öppnas en panel där du kan välja sökvägen som du vill sammanfoga med om du väljer **ikonen Sammanfoga** .

![chlimage_1-200](assets/chlimage_1-200.png)

* **Bana**
   *(skrivskyddat)* Sökvägen till taggen som markerats för att sammanfogas med en annan tagg.

* **Lägg samman i** Bläddra för att välja sökvägen till taggen som ska sammanfogas i.

>[!NOTE]
>
>Efter sammanfogningen kommer den **bana** som ursprungligen valdes (praktiskt taget) inte längre att finnas.
>
>När en refererad tagg flyttas eller sammanfogas tas taggen inte bort fysiskt så att det går att behålla referenser.

### Publiceringstaggar {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

När ett namnutrymme eller en annan tagg är markerad aktiverar du taggen i publiceringsmiljön genom att markera **ikonen Publicera** . Precis som för sidinnehåll publiceras bara den markerade taggen, oavsett om det är en behållartagg eller inte.

Om du vill publicera en taxonomi (ett namnutrymme och undertaggar) är det bästa sättet att skapa ett [paket](/help/sites-administering/package-manager.md) med namnutrymmet (se [Taxonomirotnod](/help/sites-developing/framework.md#taxonomy-root-node)). Var noga med att [tillämpa behörigheter](#setting-tag-permissions) på namnutrymmet innan du skapar paketet.

### Avpublicerar taggar {#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

När du markerar ett namnutrymme eller en annan tagg och väljer ikonen **Avpublicera** inaktiveras taggen i redigeringsmiljön och tas bort från publiceringsmiljön. Om den markerade taggen är en behållartagg inaktiveras alla dess underordnade taggar i redigeringsmiljön och tas bort från publiceringsmiljön, vilket liknar `Delete`åtgärden.

### Ta bort taggar {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

När du markerar ett namnutrymme eller en annan tagg tas taggen bort permanent om du väljer **ikonen Ta bort** . Om taggen publicerades tas den även bort från publiceringsmiljön. Om den markerade taggen är en behållartagg tas även alla dess underordnade taggar bort.

## Ange taggbehörigheter {#setting-tag-permissions}

Taggbehörigheterna är [&quot;säkra (som standard)&quot;](/help/sites-administering/production-ready.md); en bra metod för publiceringsmiljön som kräver att läsbehörighet uttryckligen tillåts för taggar. Detta görs genom att skapa ett paket av taggnamnutrymmet efter att behörigheter har angetts för författaren och installera paketet på alla publiceringsinstanser.

* on author instance

   * logga in med administratörsbehörighet
   * tillgång till [säkerhetskonsolen](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

      * till exempel gå till http://localhost:4502/useradmin
   * i den vänstra rutan markerar den grupp (eller användare) för vilken [läsbehörighet](/help/sites-administering/security.md#permissions) ska beviljas
   * i den högra rutan letar du reda på **Path **to the Tag Namespace

      * for example, `/content/cq:tags/mycommunity`
   * markera `checkbox`i kolumnen **Läs**
   * välj **Spara**



![chlimage_1-204](assets/chlimage_1-204.png)

* se till att alla publiceringsinstanser har samma behörigheter

   * ett sätt är att [skapa ett paket](/help/sites-administering/package-manager.md#package-manager) med namnutrymmet vid författaren

      * på `Advanced` -flik, för `AC Handling` val `Overwrite`
   * replikera paketet

      * välj `Replicate` från pakethanteraren


## Hantera taggar på olika språk {#managing-tags-in-different-languages}

En taggs `title`egenskap kan översättas till flera språk. När taggen har översatts `title`kan den visas beroende på användarspråk eller sidspråk.

### Definiera taggtitlar på flera språk {#defining-tag-titles-in-multiple-languages}

Nedan beskrivs hur du översätter `title`taggen **Djur** från engelska till tyska och franska.

Börja med att markera taggen under **Stock Photography** -namnutrymmet och markera ikonen **`Edit`**i (se avsnittet [Redigera taggar](#editing-tags) ).

På panelen Redigera tagg kan du välja språk som taggtiteln ska lokaliseras till.

När varje språk är markerat visas en textruta där den översatta titeln kan anges.

När alla översättningar har angetts väljer du **Spara** för att avsluta redigeringsläget.

![chlimage_1-205](assets/chlimage_1-205.png)

I allmänhet hämtas det språk som valts för taggen från sidspråket, när det är tillgängligt. När [ `tag` widgeten](/help/sites-developing/building.md#tagging-on-the-client-side) används i andra fall (till exempel i formulär eller i dialogrutor) beror taggspråket på sammanhanget.

I stället för att använda sidspråkinställningen använder taggningskonsolen språkinställningen. I taggningskonsolen för taggen Animals visas Animaux för en användare som anger språket som franska i sina användaregenskaper.

Mer information om hur du lägger till ett nytt språk i dialogrutan finns i [Lägga till ett nytt språk i dialogrutan](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog)Redigera tagg.

>[!NOTE]
>
>I taggmolnet och meta-nyckelorden i standardsidkomponenten används den lokaliserade taggen `titles`baserat på sidspråket, om det är tillgängligt.

## Resurser {#resources}

* [Tagga för utvecklare](/help/sites-developing/tags.md)

   Information om taggningsramverket samt hur du utökar och inkluderar taggar i anpassade program.

* [Klassiskt gränssnitt, taggningskonsol](/help/sites-administering/classic-console.md)

