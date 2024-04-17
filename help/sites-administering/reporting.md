---
title: Rapportering
description: Lär dig hur du arbetar med rapportering i Adobe Experience Manager (AEM).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 2a0bf59d-8829-4142-9cb4-dcef90f53ae9
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2782'
ht-degree: 0%

---

# Rapportering {#reporting}

Adobe Experience Manager (AEM) ger dig möjlighet att övervaka och analysera instansens tillstånd och innehåller ett urval standardrapporter som kan konfigureras för dina individuella behov:

* [Komponentrapport](#component-report)
* [Diskanvändning](#disk-usage)
* [Hälsokontroll](#health-check)
* [Sidaktivitetsrapport](#page-activity-report)
* [Användargenererad innehållsrapport](#user-generated-content-report)
* [Användarrapport](#user-report)
* [Instansrapport för arbetsflöde](#workflow-instance-report)
* [Arbetsflödesrapport](#workflow-report)

>[!NOTE]
>
>Rapporterna är bara tillgängliga i det klassiska användargränssnittet. Systemövervakning och rapportering i det moderna användargränssnittet finns i [Kontrollpanel för åtgärder.](/help/sites-administering/operations-dashboard.md)

Alla rapporter finns på **verktyg** konsol. Välj **Rapporter** i den vänstra rutan dubbelklickar du på önskad rapport i den högra rutan så att du kan öppna den för visning, konfiguration eller båda.

Nya instanser av en rapport kan också skapas från **verktyg** konsol. Välj **Rapporter** i den vänstra rutan och sedan **Nytt...** i verktygsfältet. Definiera en **Titel** och **Namn**, väljer den rapporttyp som du behöver och klickar sedan på **Skapa**. Den nya rapportinstansen visas i listan. Dubbelklicka på den här för att öppna och dra sedan en komponent från sidosparken så att du kan skapa den första kolumnen och starta rapportdefinitionen.

>[!NOTE]
>
>Förutom de AEM standardrapporter som finns tillgängliga direkt kan du [utveckla egna (nya) rapporter](/help/sites-developing/dev-reports.md).

## Grunderna i anpassning av rapporter {#the-basics-of-report-customization}

Det finns olika format för rapporter. I följande rapporter används kolumner som kan anpassas enligt följande avsnitt:

* [Komponentrapport](#component-report)
* [Sidaktivitetsrapport](#page-activity-report)
* [Användargenererad innehållsrapport](#user-generated-content-report)
* [Användarrapport](#user-report)
* [Instansrapport för arbetsflöde](#workflow-instance-report)

>[!NOTE]
>
>Följande rapporter har sina egna format och anpassningar:
>
>
>* [Hälsokontroll](#health-check) använder urvalsfält för att ange data som du vill rapportera om.
>* [Diskanvändning](#disk-usage) använder länkar för att gå igenom databasstrukturen.
>* [Arbetsflöde](/help/sites-administering/reporting.md#workflow-report) ger en översikt över arbetsflödena som körs på instansen.
>
>Följande procedurer för kolumnkonfiguration är därför inte lämpliga. Mer information finns i beskrivningarna av de enskilda rapporterna.

### Markera och placera datakolumner {#selecting-and-positioning-the-data-columns}

Kolumner kan läggas till, flyttas på eller tas bort från alla rapporter, antingen som standard eller anpassade.

The **Komponenter** -fliken (som är tillgänglig på rapportsidan) listar alla datakategorier som kan markeras som kolumner.

Så här ändrar du datamarkeringen:

* om du vill lägga till en kolumn drar du den önskade komponenten från sidosparken och släpper den i önskad position

   * en grön bock anger när positionen är giltig och ett par pilar anger exakt var den är placerad
   * en röd no go-symbol anger när positionen är ogiltig

* om du vill flytta en kolumn klickar du på rubriken, håller ned och drar till den nya positionen
* Om du vill ta bort en kolumn klickar du på kolumnrubriken, håller ned och drar uppåt i rapportrubrikområdet (ett rött minustecken anger att positionen inte är giltig). Släpp musknappen så begär dialogrutan Ta bort komponenter en bekräftelse på att du verkligen vill ta bort kolumnen.

### Nedrullningsbar meny för kolumn {#column-drop-down-menu}

Varje kolumn i rapporten har en listruta. Detta visas när muspekaren flyttas över kolumntitelcellen.

En pilspets visas längst till höger i titelcellen (ska inte blandas ihop med pilhuvudet direkt till höger om den titeltext som anger [aktuell sorteringsmekanism](#sorting-the-data)).

![reportcolumnsort](assets/reportcolumnsort.png)

Vilka alternativ som är tillgängliga på menyn beror på hur kolumnen är konfigurerad (vilket sker under projektutvecklingen). Alla ogiltiga alternativ är nedtonade (nedtonade).

### Sortera data {#sorting-the-data}

Data kan sorteras efter en viss kolumn genom att antingen:

* klicka på rätt kolumnrubrik. Sorteringen växlar mellan stigande och fallande, vilket anges med en pilspets omedelbart bredvid titeltexten
* använder [kolumnens nedrullningsbara meny](#column-drop-down-menu) för att välja **Sortera stigande** eller **Sortera fallande**. Återigen indikeras detta med en pilspets omedelbart intill titeltexten

### Grupper och det aktuella dataramarmet {#groups-and-the-current-data-chart}

I lämpliga kolumner kan du välja **Gruppera efter den här kolumnen** från [kolumnens nedrullningsbara meny](#column-drop-down-menu). Detta grupperar data efter varje distinkt värde i den kolumnen. Du kan markera mer än en kolumn som ska grupperas. Alternativet är nedtonat (nedtonat) när data i kolumnen inte är lämpliga. Det innebär att alla poster är distinkta och unika, så att inga grupper kan formas. Till exempel kolumnen Användar-ID i användarrapporten.

När minst en kolumn har grupperats visas ett cirkeldiagram över **Aktuella data** genereras baserat på den här grupperingen. Om flera kolumner är grupperade visas detta i diagrammet.

![reportuser](assets/reportuser.png)

När du för markören över cirkeldiagrammet visas det sammanlagda värdet för det aktuella segmentet. Här används den mängd som för närvarande är definierad för kolumnen, t.ex. antal, minimum, medel.

### Filter och aggregat {#filters-and-aggregates}

I lämpliga kolumner kan du även konfigurera **Filterinställningar** och/eller **Aggregat** från [kolumnens nedrullningsbara meny](#column-drop-down-menu).

#### Filter {#filters}

Med Filterinställningar kan du ange villkor för poster som ska visas. De tillgängliga operatorerna är:

* `contains`
* `equals`

![reportfilter](assets/reportfilter.png)

Så här anger du ett filter:

1. Välj den operator som du vill använda i listrutan.
1. Ange texten som ska filtreras.
1. Klicka **Använd**.

Så här inaktiverar du filtret:

1. Ta bort filtertexten.
1. Klicka **Använd**.

#### Aggregat {#aggregates}

Du kan också välja en aggregeringsmetod (dessa kan variera beroende på vilken kolumn som är vald):

![reportagregate](assets/reportaggregate.png)

### Kolumnegenskaper {#column-properties}

Det här alternativet är bara tillgängligt när [Allmän kolumn](#generic-column) har använts i [Användarrapport](#user-report).

### Historiska data {#historic-data}

En tabell över hur data ändras över tid finns nedan **Historiska data**. Detta kommer från ögonblicksbilder som tagits med regelbundna intervall.

Data:

* Insamlat av, om tillgängligt, den första sorterade kolumnen, i annat fall den första kolumnen (icke-grupperad)
* Grupperad efter lämplig kolumn

Rapporten kan genereras:

1. Ange **Gruppering** i den obligatoriska kolumnen.
1. **Redigera** konfigurationen så att du kan definiera ögonblicksbilder per timme eller dag.
1. **Slutför...** Definitionen som startar samlingen av ögonblicksbilder.

   Den röda/gröna reglageknappen längst upp till vänster anger när ögonblicksbilder samlas in.

Det resulterande diagrammet visas längst ned till höger:

![reportrens](assets/reporttrends.png)

När datainsamlingen startar kan du välja:

* **Period**

  Du kan välja från- och till-datum för rapportdata som ska visas.

* **Intervall**

  Månad, Vecka, Dag, Timme kan väljas för rapportens skala och aggregering.

  Om det t.ex. finns dagliga ögonblicksbilder för februari 2011:

   * Om intervallet är inställt på `Day`visas varje fixering som ett värde i diagrammet.
   * Om intervallet är inställt på `Month`, sammanställs alla ögonblicksbilder för februari till ett enda värde (visas som en enda punkt i diagrammet).

Välj dina behov och klicka sedan på **Gå** för att tillämpa dem på rapporten. Om du vill uppdatera visningen när fler ögonblicksbilder har gjorts klickar du på **Gå** igen.

![chlimage_1-43](assets/chlimage_1-43.png)

När ögonblicksbilder samlas in kan du:

* Använd **Slutför...** igen för att initiera om samlingen.

  **Slutför** &quot;fryser&quot; rapportens struktur (d.v.s. kolumnerna som är tilldelade rapporten och som är grupperade, sorterade, filtrerade osv.) och börjar ta ögonblicksbilder.

* Öppna **Redigera** så att du kan välja **Inga ögonblicksbilder av data** för att avsluta samlingen tills det behövs.

  **Redigera** aktiverar eller inaktiverar bara tagning av ögonblicksbilder. Om ögonblicksbilder aktiveras igen används rapportens tillstånd när den senast var klar för att ta ytterligare ögonblicksbilder.

>[!NOTE]
>
>Fixeringar lagras under `/var/reports/...` där resten av sökvägen speglar sökvägen för respektive rapport och ID som skapades när rapporten var klar.
>
>
>Gamla ögonblicksbilder kan rensas manuellt om du är säker på att du inte längre behöver dessa förekomster.

>[!NOTE]
>
>De förkonfigurerade rapporterna är inte prestandakrävande, men det rekommenderas ändå att du använder dagliga ögonblicksbilder i en produktionsmiljö. Om det är möjligt kan du köra dessa dagliga ögonblicksbilder vid en tidpunkt på dagen när det inte finns mycket aktivitet på webbplatsen. Detta kan definieras med `Daily snapshots (repconf.hourofday)` parameter för **Konfiguration av CQ-rapportering dag**. Se [OSGI-konfiguration](/help/sites-deploying/configuring-osgi.md) om du vill ha mer information om hur du konfigurerar detta.

#### Visningsgränser {#display-limits}

Rapporten med historiska data kan också ändra utseendet något på grund av begränsningar som kan anges enligt antalet resultat för den valda perioden.

Varje vågrät linje kallas en serie (och motsvarar en post i teckenförklaringen). Varje lodrät punktkolumn representerar de aggregerade fixeringarna.

![chlimage_1-44](assets/chlimage_1-44.png)

Det finns begränsningar som du kan ange för att hålla diagrammet rent under längre tidsperioder. Följande gäller för standardrapporterna:

* vågrät serie - både standard- och systemmaximum är `9`

* lodräta aggregerade ögonblicksbilder - standard är `35` (per horisontella serier)

Så när (lämpliga) gränser överskrids:

* punkterna inte visas
* teckenförklaringen för det historiska datatecknet kan visa ett annat antal poster än det aktuella datatecknet

![chlimage_1-45](assets/chlimage_1-45.png)

Anpassade rapporter kan även visa **Totalt** värde för alla serier. Detta visas som en serie (vågrät linje och post i teckenförklaringen).

>[!NOTE]
>
>För anpassade rapporter kan gränserna anges på ett annat sätt.

### Redigera (rapport) {#edit-report}

The **Redigera** knappen öppnar **Redigera rapport** Dialogruta.

Detta är en plats där perioden för insamling av ögonblicksbilder för [Historiska data](#historic-data) är definierad, men olika andra inställningar kan också definieras:

![reportedit](assets/reportedit.png)

* **Titel**

  Du kan definiera en egen titel.

* **Beskrivning**

  Du kan definiera en egen beskrivning.

* **Rotsökväg** (*endast aktiv för vissa rapporter*)

  Använd det här om du vill begränsa rapporten till en (under) del av databasen.

* **Rapportbearbetning**

   * **uppdatera data automatiskt**

     Rapportdata uppdateras varje gång du uppdaterar rapportdefinitionen.

   * **uppdatera data manuellt**

     Det här alternativet kan användas för att förhindra fördröjningar som orsakas av automatiska uppdateringsåtgärder när det finns stora datamängder.

     Om du väljer det här alternativet måste rapportdata uppdateras manuellt när någon del av rapportkonfigurationen har ändrats. Det innebär också att när du ändrar någon aspekt av konfigurationen, tas rapporttabellen bort.

     När det här alternativet är markerat **[Läs in data](#load-data)** visas (bredvid **Redigera** på rapporten). **Läs in data** läser in data och uppdaterar rapportdata som visas.

* **Fixeringar**
Du kan definiera hur ofta ögonblicksbilder ska göras, varje dag, varje timme eller inte alls.

### Läs in data {#load-data}

The **Läs in data** knappen visas bara när **uppdatera data manuellt** har valts från **[Redigera](#edit-report)**.

![chlimage_1-46](assets/chlimage_1-46.png)

Klicka **Läs in data** läser in data igen och uppdaterar rapporten som visas.

Om du väljer att uppdatera data manuellt innebär det att:

1. När du ändrar rapportkonfigurationen tas rapportdatatabellen bort.

   Om du till exempel ändrar sorteringsmekanismen för en kolumn visas inte data.

1. Om du vill att rapportdata ska visas igen måste du klicka **Läs in data** för att läsa in data igen.

### Slutför (rapport) {#finish-report}

När du **Slutför** rapporten:

* Rapportdefinitionen *vid den tidpunkten* används för att ta ögonblicksbilder. Därefter kan du fortsätta arbeta med en rapportdefinition eftersom den är skild från ögonblicksbilderna.
* Alla befintliga ögonblicksbilder tas bort.
* Nya ögonblicksbilder samlas in för [Historiska data](#historic-data).

I den här dialogrutan kan du definiera eller uppdatera din egen titel och beskrivning för den resulterande rapporten.

![reportfinish](assets/reportfinish.png)

## Rapporttyper {#report-types}

### Komponentrapport {#component-report}

Komponentrapporten innehåller information om hur din webbplats använder komponenterna.

[Informationskolumner](#selecting-and-positioning-the-data-columns) om:

* Författare
* Komponentsökväg
* Komponenttyp
* Senast ändrad
* Sida

Det innebär att du kan se följande:

* Vilka komponenter som används och var de används.

  Användbart vid testning.

* Hur instanser av en viss komponent distribueras.

  Detta kan vara intressant om specifika sidor (dvs.&quot;stora sidor&quot;) har prestandaproblem.

* Identifiera delar av sajten med frekventa/mindre frekventa ändringar.
* Se hur sidinnehåll utvecklas över tid.

Alla komponenter ingår, produktstandard och projektspecifik. Använda **Redigera** kan användaren också ange en **Rotsökväg** som definierar rapportens startpunkt - alla komponenter under den roten beaktas för rapporten.

![reportcomponent](assets/reportcomponent.png) ![reportcompentall](assets/reportcompentall.png)

### Diskanvändning {#disk-usage}

Diskanvändningsrapporten innehåller information om de data som lagras i din databas.

Rapporten börjar i databasens rot ( / ) genom att klicka på en viss gren som du kan gå ned i databasen (den aktuella sökvägen visas i rapportrubriken).

![diskus](assets/reportdiskusage.png)

### Hälsokontroll {#health-check}

Den här rapporten analyserar den aktuella begärandeloggen:

`<cq-installation-dir>/crx-quickstart/logs/request.log`

För att hjälpa dig att identifiera de mest dyra förfrågningarna inom en viss period.

Om du vill generera rapporten kan du ange följande:

* **Period (timmar)**

  Antalet timmar (tidigare) som ska analyseras.

  Standard: `24`

* **max. Resultat**

  Maximalt antal utdatarader.

  Standard: `50`

* **max. Begäranden**

  Maximalt antal begäranden som ska analyseras.

  Standard: `-1` (all)

* **E-postadress**

  Skicka resultat till en e-postadress.

  Valfritt; Standard: tomt

* **Kör dagligen (hh:mm)**

  Ange en tidpunkt då rapporten ska köras automatiskt varje dag.

  Valfritt; Standard: tomt

![reporthealth](assets/reporthealth.png)

### Sidaktivitetsrapport {#page-activity-report}

Sidaktivitetsrapporten innehåller en lista över sidor och åtgärder som har utförts på dem.

[Informationskolumner](#selecting-and-positioning-the-data-columns) om:

* Sida
* Tid
* Typ
* Användare

Betydelse som du kan övervaka:

* De senaste ändringarna.
* Författare som arbetar med specifika sidor.
* Sidor som inte har ändrats nyligen kan behöva åtgärdas.
* Sidor som ändras oftast eller oftast.
* De flesta/minst aktiva användarna.

Sidaktivitetsrapporten hämtar all information från granskningsloggen. Som standard är rotsökvägen konfigurerad till granskningsloggen på `/var/audit/com.day.cq.wcm.core.page`.

![reportpageaktivitet](assets/reportpageactivity.png)

### Användargenererad innehållsrapport {#user-generated-content-report}

Den här rapporten innehåller information om användargenererat innehåll, t.ex. kommentarer, omdömen eller forum.

[Informationskolumner](#selecting-and-positioning-the-data-columns) den:

* Datum
* IP-adress
* Sida
* Referent
* Typ
* Användar-ID

Gör att du kan:

* Se vilka sidor som får flest kommentarer.
* Få en översikt över alla kommentarer som specifika besökare lämnar webbplatsen, kanske problemen är relaterade.
* Se om nytt innehåll ger upphov till kommentarer genom att övervaka när kommentarer görs på en sida.

![reportusercontent](assets/reportusercontent.png)

### Användarrapport {#user-report}

Den här rapporten innehåller information om alla användare som har registrerat ett konto och/eller en profil. Den kan omfatta både författare inom organisationen och externa besökare.

[Informationskolumner](#selecting-and-positioning-the-data-columns) (om tillgängligt) om:

* Ålder
* Land
* Domän
* E-post
* Efternamn
* Kön
* [Allmän](#generic-column)
* Förnamn
* Info
* Ränta
* Språk
* NTLM Hashcode
* Användar-ID

Gör att du kan:

* Se användarnas demografiska spridning.
* Rapportera om anpassade fält som du har lagt till i profilerna.

![reportusercanned](assets/reportusercanned.png)

#### Allmän kolumn {#generic-column}

The **Allmän** -kolumnen är tillgänglig i användarrapporten så att du kan komma åt anpassad information, vanligtvis från [användarprofiler](/help/sites-administering/identity-management.md#profiles-and-user-accounts); till exempel [Favoritfärg enligt anvisningarna under Lägg till fält i profildefinitionen](/help/sites-administering/identity-management.md#adding-fields-to-the-profile-definition).

Dialogrutan Allmän kolumn öppnas när du gör något av följande:

* Dra den allmänna komponenten från sidosparken till rapporten.
* Markera kolumnegenskaperna för en befintlig allmän kolumn.

![reportusrgenericcolm](assets/reportusrgenericcolm.png)

Från **Definitioner** -flik som du kan definiera:

* **Titel**

  Din egen rubrik för den generiska kolumnen.

* **Egenskap**

  Egenskapsnamnet som lagrats i databasen, vanligtvis i användarens profil.

* **Bana**

  Vanligtvis hämtas egenskapen från `profile`.

* **Typ**

  Välj fälttyp från `String`, `Number`, `Integer`, `Date`.

* **Standardaggregering**

  Detta definierar den mängd som används som standard om kolumnen delas upp i en rapport med minst en grupperad kolumn. Välj önskad mängd från `Count`, `Minimum`, `Average`, `Maximum`, `Sum`.

  Till exempel: *Antal* för `String` fält betyder att antalet distinkta `String` värden visas för kolumnen i aggregerat läge.

I **Utökad** kan du även definiera de aggregat och filter som är tillgängliga:

![reportusrgenericcolmextented](assets/reportusrgenericcolmextented.png)

### Instansrapport för arbetsflöde {#workflow-instance-report}

Detta ger en kortfattad översikt som ger information om de enskilda instanserna av arbetsflöden, både som körs och slutförda.

[Informationskolumner](#selecting-and-positioning-the-data-columns) om:

* Slutförd
* Varaktighet
* Initierare
* Modell
* Nyttolast
* Startat
* Status

Det innebär att du kan:

* Övervaka arbetsflödenas genomsnittliga varaktighet. Om detta sker regelbundet kan det lyfta fram problem med arbetsflödet.

![reportworkflowintance](assets/reportworkflowintance.png)

### Arbetsflödesrapport {#workflow-report}

Här finns viktig statistik om arbetsflödena som körs på instansen.

![rapportarbetsflöde](assets/reportworkflow.png)

## Använda rapporter i en publiceringsmiljö {#using-reports-in-a-publish-environment}

När du har konfigurerat rapporterna efter dina specifika krav kan du aktivera dem för att överföra konfigurationen till publiceringsmiljön.

>[!CAUTION]
>
>Om du vill **Historiska data** för publiceringsmiljön, och **Slutför** rapporten om redigeringsmiljön innan sidan aktiveras.

Rapporten finns sedan tillgänglig under

`/etc/reports`

Rapporten User-Generated Content finns under:

`http://localhost:4503/etc/reports/ugcreport.html`

Nu rapporteras data som samlats in från publiceringsmiljön.

Eftersom ingen rapportkonfiguration är tillåten i publiceringsmiljön kan **Redigera** och **Slutför** är inte tillgängliga. Du kan dock välja **Period** och **Intervall** för **Historiska data** rapporterar om ögonblicksbilder samlas in.

![rapportersucgpublish](assets/reportsucgpublish.png)

>[!CAUTION]
>
>Åtkomst till dessa rapporter kan vara ett säkerhetsproblem. Därför rekommenderar Adobe att du konfigurerar Dispatcher så att `/etc/reports` är inte tillgängligt för externa besökare. Se [Säkerhetschecklista](security-checklist.md) för mer information.

## Behörigheter krävs för att köra rapporter {#permissions-needed-for-running-reports}

Behörigheterna som krävs beror på åtgärden:

* Rapportdata samlas in med den aktuella användarens behörigheter.
* Historiska data samlas in med behörigheten för användaren som slutförde rapporten.

I en AEM är följande behörigheter förinställda för rapporterna:

* **Användarrapport**

  `user administrators` - läsa och skriva

* **Sidaktivitetsrapport**

  `contributors` - läsa och skriva

* **Komponentrapport**

  `contributors` - läsa och skriva

* **Användargenererad innehållsrapport**

  `contributors` - läsa och skriva

* **Instansrapport för arbetsflöde**

  `workflow-users` - läsa och skriva

Alla medlemmar i `administrators` gruppen har de rättigheter som krävs för att skapa rapporter.
