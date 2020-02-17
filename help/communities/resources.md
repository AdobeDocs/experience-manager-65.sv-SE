---
title: Resurskonsol för aktivering
seo-title: Resurskonsol för aktivering
description: Resurskonsolen är den plats där aktiveringshanterare skapar, hanterar och tilldelar resurser till medlemmar på en aktiveringscommunitywebbplats
seo-description: Resurskonsolen är den plats där aktiveringshanterare skapar, hanterar och tilldelar resurser till medlemmar på en aktiveringscommunitywebbplats
uuid: 52445b39-c339-4b39-8004-eb36de99bced
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1ef15e76-fe7c-4ced-a20d-c0a9385e3ee4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Resurskonsol för aktivering {#enablement-resources-console}

För AEM Communities är resurskonsolen där [Enabled Managers](users.md) skapar, hanterar och tilldelar resurser till medlemmar på en community för aktivering.

## Krav {#requirements}

Innan du lägger till aktiveringsresurser för en community-webbplats måste AEM-instanserna vara korrekt konfigurerade, inklusive:

* SCORM
* FFmpeg

Mer information finns i [Konfigurera aktivering](enablement.md).

>[!CAUTION]
>
>Om SCORM har installerats efter att en community-webbplats har skapats måste eventuella aktiveringsresurser som finns innan SCORM har installerats återskapas.

>[!NOTE]
>
>I och med releasen av [AEM 6.3](deploy-communities.md#latestfeaturepack) och motsvarande funktionspaket för Communities [AEM 6.2 FP3](deploy-communities.md#latestfeaturepack) och [AEM 6.1 FP7](https://docs.adobe.com/content/docs/en/aem/6-1/deploy/communities.html#Latest) behöver inte längre aktiveringsfunktionen en [MySQL-databas](mysql.md).

##  Terminologi {#terminology}

### Resurs {#resource}

Resurser är avgörande för en community [för](overview.md#enablement-community)aktivering. Det är det material som medlemmarna tilldelas för att förbättra sina färdigheter.

En resurs egenskaper:

* Kan vara av typen
   * Bild (JPG, PNG, GIF, BMP)
   * Video (MP4)
   * Flash (SWF)
   * Dokument (PDF)
   * Quiz (SCORM)
* Kan refereras från en eller flera utbildningsvägar

### Utbildningsväg {#learning-path}

En inlärningsväg är en logisk uppsättning aktiveringsresurser som grupperats tillsammans för att det ska vara enkelt att tilldela medlemmar.

### Medlemsgrupp {#members-group}

När en communitywebbplats skapas används det namn som tilldelats webbplatsen för URL:en när de [platsspecifika användargrupperna](users.md) som konfigurerats med olika behörigheter för olika roller skapas. Alla automatiskt skapade grupper har prefix `Community *<site-name>*`.

En sådan användargrupp är `Community *<site-name>* Members` grupp, som identifierar registrerade användare i publiceringsmiljön som communitymedlemmar. Ett exempel finns i självstudiekursen [Komma igång med AEM Communities for Enablement](getting-started-enablement.md) .

För [engagemangscommunityn](overview.md#egagementcommunity)är det rimligt att låta besökare på webbplatsen registrera sig själva eller använda social inloggning, då de automatiskt läggs till i medlemsgruppen.

För [aktiveringsgrupper](overview.md#enablement-community)bör du göra webbplatsen privat, vilket sedan kräver att en administratör lägger till användare i medlemsgruppen.

## Åtkomst till aktiveringsresurser för en community-webbplats {#accessing-a-community-site-s-enablement-resources}

### Navigera till Communities Resources {#navigate-to-communities-resources}

För att nå Resurskonsolen i redigeringsmiljön

* Från global navigering: **[!UICONTROL Navigering > Communities > Resources]**

![chlimage_1-163](assets/chlimage_1-163.png)

### Välj en communitywebbplats {#select-a-community-site}

Webbkonsolen Communities Resources visar alla communitysajter.

Aktiveringsresurser skapas för en specifik community-webbplats efter att du har valt webbplatsen från resurskonsolen.

När en specifik communitywebbplats har valts är alla befintliga aktiveringsresurser och utbildningsvägar tillgängliga för hantering och ändring, och nya aktiveringsresurser och inlärningsvägar kan skapas.

![chlimage_1-164](assets/chlimage_1-164.png)

#### Sök {#search-features}

![chlimage_1-165](assets/chlimage_1-165.png)

Välj växlingsikonen för sidopanelen för att söka efter en aktiveringsresurs eller utbildningsväg. När du väljer det här alternativet öppnas en sökpanel till vänster i konsolen och innehåller en textruta där sökord kan anges.

![chlimage_1-166](assets/chlimage_1-166.png)

#### Markeringsläge {#selection-mode}

Om du vill markera flera aktiveringsresurser, markerar du den första genom att hålla markören över kortet och sedan markera kryssmarkeringsikonen. När du har valt ett annat kort läggs det till i markeringsgruppen. Om du väljer en andra gång avmarkeras kortet.

![chlimage_1-167](assets/chlimage_1-167.png)

## Skapa en resurs {#create-a-resource}

![chlimage_1-168](assets/chlimage_1-168.png)

Lägga till en ny aktiveringsresurs på communitywebbplatsen

* Markera `Create` ikonen
* På undermenyn som visas väljer du `Resource`

Detta startar en stegvis process för

* Beskriver resursen (namn, kortbild och text)
* Välja resursinnehåll
* Välja en omslagsbild för resursen
* Identifiera resurskontakter
* Tilldela resurser till medlemmar

När resursen är en del av en kurs, en inlärningsväg, ska medlemmar endast tilldelas inlärningsvägen. Tilldelningar kan läggas till efter att aktiveringsresursen har skapats.

### 1 Grundläggande information {#basic-info}

![chlimage_1-169](assets/chlimage_1-169.png)

* **[!UICONTROL Lägg till bild]**

   (*valfritt*) En bild som ska visas på kortet för aktiveringsresursen på medlemmens tilldelningssida samt på resurskonsolen. Bilden väljs från serverns lokala filsystem. Om ingen bild anges skapas en miniatyrbild för den överförda resursen.

   ***Obs***: den rekommenderade bildstorleken är inte bara 480 x 480 pixlar. På grund av kortens responsiva design för olika webbläsardimensioner varierar visningsstorleken mellan 220 x 165 pixlar och 400 x 165 pixlar.

* **[!UICONTROL Platsnamn]**

   (*skrivskyddat*) Den communitywebbplats som resursen läggs till i.

* **[!UICONTROL Resursnamn&amp;stämpel;senaste;]**

   (*obligatoriskt*) Resursens visningsnamn. Ett giltigt nodnamn skapas från visningsnamnet.

* **[!UICONTROL Taggar]**

   (*valfritt*) Du kan välja en eller flera taggar som associerar aktiveringsresursen med en eller flera kataloger. Se [Tagga aktiveringsresurser](tag-resources.md).

* **[!UICONTROL Visa i katalog]**

   Om alternativet inte är markerat visas inte aktiveringsresursen i någon katalog. Om det här alternativet är markerat visas aktiveringsresursen i alla kataloger, såvida den inte [förfiltrerats](catalog-developer-essentials.md#pre-filters) eller medlemsfiltren från användargränssnittet. Standard är avmarkerat.

* **[!UICONTROL Beskrivning]**

   (*valfritt*) Beskrivning som ska visas för aktiveringsresursen.

* **[!UICONTROL Liten resurs]**

   (*valfritt*) Välj bland AEM-resurser. En miniatyrbild som representerar resursen i publiceringsmiljön, t.ex. i en katalog.

* **[!UICONTROL Stor resurs]**

   (*valfritt*) Välj bland AEM-resurser. En stor bild som representerar resursen i publiceringsmiljön, till exempel på huvudsidan för en resurs.

* **[!UICONTROL Innehållsfragmentresurs]**

   (*valfritt*) Välj bland AEM-resurser. Ett innehållsfragment som kan refereras i publiceringsmiljön, men som inte används som standard.

* Markera **[!UICONTROL nästa]**

### 2 Lägg till innehåll {#add-content}

![chlimage_1-170](assets/chlimage_1-170.png)

Det ser ut som om flera aktiveringsresurser kan väljas, men bara en är tillåten.

Markera `'+' icon`i det övre högra hörnet när du vill börja välja resursen genom att identifiera källan.

![chlimage_1-171](assets/chlimage_1-171.png)

* **[!UICONTROL Överföring från mina lokala filer]**&#x200B;Överföring från det lokala filsystemet använder den inbyggda filläsaren för att välja och överföra en fil. Filtyper som stöds är SCORM.zip (HTML5 eller SWF), MP4-video, SWF, PDF och bildtyper (JPG, PNG, GIF, BMP). Filnamnet blir namnet på resursen som läggs till i resursbiblioteket.

* **[!UICONTROL Bläddra bland resursbibliotek]** Välj från resursbibliotek. Markeringen begränsas till de som visas på communitywebbplatsen.

* **[!UICONTROL Lägg till en extern URL]**

   Ange en länk till utbildningsmaterialet.

   I den dialogruta som öppnas anger du:

   * **[!UICONTROL Titel]**

      Namnet på resursen för aktiveringsresursen.

   * **[!UICONTROL Webbadress]**

      URL:en till en resurs.

* **[!UICONTROL Lägg till en Adobe Connect-URL]**

   Ange en länk till en Adobe Connect-session.

   I den dialogruta som öppnas anger du:

   * **[!UICONTROL Titel]**

      Namnet på resursen för aktiveringsresursen.

   * **[!UICONTROL Webbadress]**

      URL:en till en Adobe Connect-session.

* **[!UICONTROL Definiera en extern resurs]**

   Ange den plats där materialet ska presenteras. Värdena för resultatstatus och poängställning anges manuellt (se [Rapporter](reports.md)). En överförd omslagsbild kan användas för att ge ytterligare information.

   I den dialogruta som öppnas anger du:

   * **[!UICONTROL Titel]**

      Namnet på resursen för aktiveringsresursen.

   * **[!UICONTROL Plats]**

      Platsen för en fysisk plats, till exempel ett klassrum.

#### Exempel på en videoresurs som lagts till {#example-of-an-added-video-resource}

![chlimage_1-172](assets/chlimage_1-172.png)

* **[!UICONTROL Resursförsättsbild]**

   Omslagsbilden är en bild som visas när aktiveringsresursen visas för första gången. Omslagsbilden visas t.ex. när en videoresurs ännu inte spelas upp. Om en anpassad bild inte överförs visas en standardbild. För videoresurser kan det vara möjligt att [generera en miniatyrbild](enablement.md#ffmpeg), men bara när den har överförts och inte när videon refereras till som en URL-adress. För platsresurser kan bilden användas för att ge ytterligare information.

   Den rekommenderade storleken för omslagsbilden är 640 x 360 px.

* Markera **[!UICONTROL nästa]**

### 3 inställningar {#settings}

![chlimage_1-173](assets/chlimage_1-173.png)

>[!NOTE]
>
>Lärare ska inte registreras direkt i aktiveringsresurser som ska refereras från en inlärningsväg. Eleverna behöver bara vara inskrivna i kursen.
>
>Om en medlem är registrerad i både en resurs och en utbildningsväg som refererar till den resursen, kommer deras tilldelningar att visa både den enskilda resursen och resursen i utbildningsvägen.

* **[!UICONTROL Sociala inställningar]**

   Inställningarna styr om eleverna kan ange indata för aktiveringsresursen eller inte. De [modereringsinställningar](sites-console.md#moderation) som gäller för den överordnade communitywebbplatsen.

   * **[!UICONTROL Tillåt kommentarer]**

      Om det här alternativet är markerat kan medlemmar kommentera resursen. Standard är markerat.

   * **[!UICONTROL Tillåt klassificeringar]**

      Om det här alternativet är markerat kan medlemmar betygsätta resursen. Standard är markerat.

   * **[!UICONTROL Tillåt anonym åtkomst]**

      Om det här alternativet är markerat kan anonyma webbplatsbesökare visa resursen i en katalog när communitywebbplatsen även tillåter anonym åtkomst. Standard är avmarkerat.

* **[!UICONTROL Förfallodatum]**
   *(Valfritt)* Ett datum då uppdraget ska vara slutfört kan väljas.

* **[!UICONTROL Resursförfattare]**
   *(Valfritt)* Författaren till aktiveringsresursen. Använd listrutan för att välja bland de användare som är medlemmar i [medlemsgruppen](#members-group).

* **[!UICONTROL Resurskontakt&amp;stämpel;ast;]**
   *(Obligatoriskt)* En person som medlemmen kan kontakta angående aktiveringsresursen. Använd listrutan för att välja bland de användare som är medlemmar i [medlemsgruppen](#members-group).

* **[!UICONTROL Resursexpert]**
   *(Valfritt)* En person som medlemmen kan kontakta och som har kunskaper om aktiveringsresursen. Använd listrutan för att välja bland användare som är medlemmar i [medlemsgruppen](#members-group).

### 4 uppdrag {#assignments}

![chlimage_1-174](assets/chlimage_1-174.png)

* **[!UICONTROL Lägg till tilldelningar]** Använd listrutan för att välja bland [medlemmarna](#members-group) - användarna och användargrupperna (med fet stil) - som ska registreras som elev. När medlemmar loggar in på communitywebbplatsen visas de aktiveringsresurser (och utbildningsvägar) som de är inskrivna i på deras [uppdragssida](functions.md#assignments-function) .

* välj **[!UICONTROL Skapa]**

![chlimage_1-175](assets/chlimage_1-175.png)

Aktiveringsresursen har skapats och återgår till resurskonsolen med den nyligen skapade resursen markerad. Från den här konsolen går det att [hantera resursen](#managing-a-resource).

## Skapa en utbildningsväg {#create-a-learning-path}

![chlimage_1-176](assets/chlimage_1-176.png)

Lägga till en ny utbildningsväg till communitywebbplatsen

* Markera `Create` ikonen
* På undermenyn som visas väljer du `Learning Path`

Detta startar en stegvis process för

* Identifiera inlärningsvägen
* Erbjuda en kortbild som representerar inlärningsvägen för eleverna
* Referera till aktiveringsresurser som ska ingå i utbildningsvägen
* Om du vill kan du beställa resurserna
* Möjlighet att identifiera inlärningsvägar som krävs
* Identifiera en kontaktperson för utbildningsvägar
* Registrerar medlemmar

För aktiveringsresurser som ingår i en inlärningsväg ska tilldelningarna endast göras för inlärningsvägen och inte för de enskilda resurserna.

### Grundläggande information {#basic-info-1}

![chlimage_1-177](assets/chlimage_1-177.png)

* **[!UICONTROL Lägg till bild]**

   (*valfritt*) En bild som ska visas på kortet för utbildningssökvägen på medlemmens uppdragssida samt på Resurskonsolen. Bilden väljs från serverns lokala filsystem. Om ingen bild anges skapas en miniatyrbild för den överförda resursen.

   ***Obs***: den rekommenderade bildstorleken inte längre bara är 480 x 480 pixlar. På grund av kortens responsiva design för olika webbläsardimensioner varierar visningsstorleken mellan 220 x 165 pixlar och 400 x 165 pixlar.

* **[!UICONTROL Platsnamn]**

   (*skrivskyddat*) Den communitywebbplats som resursen läggs till i.

* **[!UICONTROL Namn på utbildningssökväg]**

   (*obligatoriskt*) Visningsnamnet för utbildningssökvägen. Ett giltigt nodnamn skapas från visningsnamnet.

* **[!UICONTROL Taggar]**

   (*valfritt*) Du kan välja en eller flera taggar som associerar utbildningsvägen med en eller flera kataloger. Se [Tagga aktiveringsresurser](tag-resources.md).

* **[!UICONTROL Visa i katalog]**

   Om du inte markerar det här alternativet visas inte utbildningssökvägen i någon katalog. Om det här alternativet är markerat visas utbildningssökvägen i alla kataloger, såvida den inte är [förfiltrerad](catalog-developer-essentials.md#pre-filters) eller medlemsfiltren från användargränssnittet. Om du visar inlärningsvägen i en katalog får READ indirekt åtkomst till alla resurser som finns i den. Standard är avmarkerat.

* **[!UICONTROL Beskrivning]**

   (*valfritt*) Beskrivning som ska visas för aktiveringsresursen.

* **[!UICONTROL Liten resurs]**

   (*valfritt*) Välj bland AEM-resurser. En miniatyrbild som representerar resursen i publiceringsmiljön, t.ex. i en katalog.

* **[!UICONTROL Stor resurs]**

   (*valfritt*) Välj bland AEM-resurser. En stor bild som representerar resursen i publiceringsmiljön, till exempel på huvudsidan för en resurs.

* **[!UICONTROL Innehållsfragmentresurs]**

   (*valfritt*) Välj bland AEM-resurser. Ett innehållsfragment som kan refereras i publiceringsmiljön, men som inte används som standard.

* Markera **[!UICONTROL nästa]**

### Lägg till krav {#add-prerequisites}

![chlimage_1-178](assets/chlimage_1-178.png)

* **[!UICONTROL Nödvändiga utbildningsvägar]**(*valfritt*) När andra publicerade utbildningsvägar väljs måste de slutföras innan en elev kan välja den här utbildningsvägen.

* Markera **[!UICONTROL nästa]**

### Lägg till resurser {#add-resources}

![chlimage_1-179](assets/chlimage_1-179.png)

* **[!UICONTROL Använd beställning i utbildningsväg]**

   (*valfritt*) Om värdet är På är den ordning som eleverna måste gå igenom inlärningsvägen i den ordning som aktiveringsresurserna läggs till. Standardvärdet är Av.

* **[!UICONTROL Resurser]**

   En eller flera resurser som valts bland *publicerade *aktiveringsresurser som skapats för den aktuella communitywebbplatsen.

>[!NOTE]
>
>Du kan bara välja resurser på samma nivå som utbildningsvägen. För en inlärningsväg som skapats i en grupp är t.ex. endast resurserna på gruppnivå tillgängliga. för en inlärningsväg som skapats på en community-webbplats finns resurserna på den webbplatsen tillgängliga för tillägg till inlärningsvägen.

* Välj **[!UICONTROL Nästa]**.

###  Inställningar {#settings-1}

![chlimage_1-180](assets/chlimage_1-180.png)

* **[!UICONTROL Lägg till registreringar]**

   Använd listrutan för att välja bland de medlemmar och medlemsgrupper (med fet stil) som är medlemmar i communityns [medlemsgrupp](#members-group). Du behöver inte lägga till uppdrag när du först skapar inlärningsbanan. Du kan ändra egenskaperna för utbildningsvägar för att lägga till deltagare vid ett senare tillfälle.

* **[!UICONTROL Lär dig sökvägskontakt&amp;stämpel;ast;]**

   *(Obligatoriskt)* En person som medlemmen kan kontakta angående utbildningsvägen. Använd listrutan för att välja bland de användare som är medlemmar i communityns [medlemsgrupp](#members-group).

* Välj **[!UICONTROL Skapa]**

>[!NOTE]
>
>Aktiveringsresurser som refereras från inlärningssökvägen ska inte innehålla samma uppgifter (inlärningsresurser), om det finns några.
>
>Om en medlem är registrerad i både en aktiveringsresurs och en utbildningsväg som refererar till den resursen, kommer deras tilldelningar att visa både den enskilda resursen och resursen i utbildningsvägen.

## Hantera en resurs {#managing-a-resource}

Hantera en enda aktiveringsresurs

* Från Resurskonsolen
* Välj den community-webbplats som innehåller resursen
* Välj resurs

För den valda aktiveringsresursen är det möjligt att:

* Visa egenskaper (standard)
* Redigera egenskaper
* Ta bort
* Publicera
* Avpublicera

Om du vill överföra en ny version av aktiveringsresursen rekommenderar vi att du skapar en ny resurs och sedan avregistrerar medlemmar från den gamla versionen och registrerar dem i den nya versionen.

### Redigera resurs {#edit-resource}

![chlimage_1-181](assets/chlimage_1-181.png)

Om du väljer pennikonen blir de steg som visas för att skapa en aktiveringsresurs tillgängliga så att all information som anges kan ändras.

Om den enda ändringen är att ändra uppdrag i steget Inställningar, kommer ändringarna att publiceras om du sparar dem. Om några andra ändringar görs måste resursen uttryckligen publiceras innan sparandet börjar.

### Ta bort resurs {#delete-resource}

![chlimage_1-182](assets/chlimage_1-182.png)

Genom att markera kontrollkanarikonen blir aktiveringsresursen `Delete`d efter bekräftelse.

### Publicera {#publish}

![chlimage_1-183](assets/chlimage_1-183.png)

Innan eleverna kan se en tilldelad aktiveringskurs måste den publiceras:

* Välj världsikonen för att `Publish`
* Välj **[!UICONTROL Publicera]** igen i dialogrutan som öppnas
* Välj **[!UICONTROL Stäng]**

Även om det står i dialogrutan att åtgärden står i kö publiceras den ofta omedelbart.

### Avpublicera {#unpublish}

![chlimage_1-184](assets/chlimage_1-184.png)

Om du tillfälligt vill göra aktiveringsresurserna oåtkomliga för medlemmar i publiceringsmiljön utan att ta bort dem använder du världsikonen `Unpublish`för resursen.

### Rapport {#report}

![chlimage_1-185](assets/chlimage_1-185.png)

Ikonen Rapport ger åtkomst till de rapporter som skapas när eleverna interagerar med sina tilldelade aktiveringsresurser i publiceringsmiljön. Rapporten varierar beroende på resurstypen.

För alla utbildningsvägar är det möjligt att visa en rapport som baseras antingen på resurser eller studerande ( `User Report`).

![chlimage_1-186](assets/chlimage_1-186.png)

Den här rapporten gäller specifikt för den aktuella aktiveringsresursen eller utbildningsvägen. Hur detaljerad rapportering som ges beror på om [Adobe Analytics](analytics.md) är licensierat och aktiverat för communitywebbplatsen eller inte. Rapporterna om [tidslinje](#timeline), [visningsengagemang](#viewer-engagement)och [engagemang via enhet](#engagement-by-device) importeras från Adobe Analytics utifrån [avsökningsintervallet](analytics.md#report-importer).

För alla aktiveringsresurser, oavsett om Adobe Analytics är aktiverat eller inte, finns det rapporter om status [och](#assignee-status) graderingar [för](#ratings) tilldelningsmottagaren samt en [rapportsammanfattningstabell](#report-summary) .

![chlimage_1-187](assets/chlimage_1-187.png)

#### Tidslinje {#timeline}

Analysens tidslinjerapport visar när händelser inträffar över tid för den här aktiveringsresursen:

* **Vyer**

   En vy är när en elev besöker sidan med resursinformation

* **Spelar**

   En uppspelning är när alLearner interagerar med resursen, till exempel spelar upp en video eller öppnar en PDF-fil

* **Klassificeringar**

   En klassificering är när en studerande ger en resurs en stjärngradering

* **Kommentarer**

   En kommentar är när alLearner lägger till en kommentar

Den lodräta axeln är antalet händelser.

Den vågräta axeln är kalendertid.

[Adobe Analytics krävs](sites-console.md#analytics).

#### Engagemang för visningsprogram {#viewer-engagement}

Analytics Viewer Engagement-rapporten visar, för videoresurser, antalet studerande som har tittat på resursen och, om de inte har spelats upp till slutet, vid vilken tidpunkt eleverna slutade spela upp den.

Den lodräta axeln är antalet deltagare som har tittat på resursen.

Den vågräta axeln är varaktigheten för den här resursen.

[Marketing Cloud-organisationsnummer krävs](sites-console.md#enablement).

#### Engagemang per enhet {#engagement-by-device}

Analytics Engagement by Device-rapporten beskriver, för videoresurser, hur många visningar som spelats upp från både dator och mobil.

[Marketing Cloud-organisationsnummer krävs](sites-console.md#enablement).

#### Tilldelningsstatus {#assignee-status}

Statusrapporten för den tilldelade personen, som baseras på antalet studerande, beskriver hur många som har

* **Inte startat**
* **Pågår**
* **Slutförd**

#### Klassificeringar {#ratings}

Klassificeringsrapporten baseras på antalet studerande som har klassificerat aktiveringsresursen och visar antalet stjärngraderingar följt av en sammanfattning av det totala antalet betyg och det genomsnittliga omdömet.

#### Rapportsammanfattning {#report-summary}

Rapportsammanfattningen är en tabelllista för en aktiveringsresurs

* Alla som interagerat med resursen
   * Deras status
   * Om de har tilldelats resursen
      * I stället för att hitta resursen i en katalog
   * Antal kommentarer
   * Den angivna klassificeringen, om sådan finns

Resursrapport för utbildningsvägar: Rapportsammanfattningen är en tabelllista

* Varje resurs som ingår i utbildningsvägen
   * Publiceringsstatus
   * Antal vyer
   * Antal uppspelningar
   * Genomsnittlig värdering
   * Format
   * Storlek
   * Namn på användarwebbplats

För utbildningsvägar Användarrapport är rapportsammanfattningen en tabelllista

* Varje studerande som har tilldelats en utbildningsväg
   * Antal slutförda resurser
   * Deras status

Du kan justera visningen av tabellen genom att markera kolumner med hjälp av `Show / hide columns` väljaren.

#### Hämta rapport som CSV {#download-report-as-csv}

Tabellen Rapportsammanfattning kan laddas ned i CSV-format med en knapp högst upp i konsolen.

* för en aktiveringsresurs: `Download Resource Report as CSV` knapp
* för en inlärningsväg: `Download Learning Path Report as CSV` knapp

Den fullständiga rapportsammanfattningen hämtas oavsett vilka kolumner som valts för visning.
