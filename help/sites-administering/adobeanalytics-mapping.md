---
title: Mappa komponentdata med Adobe Analytics-egenskaper
description: Lär dig hur du mappar komponentdata med SiteCatalyster.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: c7c0c705-ec16-40f5-ad08-193f82d01263
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Mappa komponentdata med Adobe Analytics-egenskaper{#mapping-component-data-with-adobe-analytics-properties}

Lägg till komponenter i ramverket som samlar in data som ska skickas till Adobe Analytics. Komponenter som är utformade för att samla analysdata lagrar data i lämplig **CQ-variabel**. När du lägger till en sådan komponent i ett ramverk visas en lista med CQ-variabler så att du kan använda var och en av dem **Analysvariabel**.

![aa-11](assets/aa-11.png)

När **AEM** är öppen. Analysvariablerna visas i innehållssökaren.

![aa-12](assets/aa-12.png)

Du kan mappa flera Analytics-variabler med samma **CQ-variabel**.

![chlimage_1-68](assets/chlimage_1-68.png)

Mappade data skickas till Adobe Analytics när sidan läses in och följande villkor uppfylls:

* Sidan är kopplad till ramverket.
* Sidan använder de komponenter som har lagts till i ramverket.

Använd följande procedur för att mappa CQ-komponentvariabler med Adobe Analytics rapportegenskaper.

1. I **AEM** drar du en spårningskomponent från sidosparken till ramverket. Dra till exempel **Sida** -komponenten från **Allmänt** kategori.

   ![aa-13](assets/aa-13.png)

   Det finns flera standardkomponentgrupper: **Allmänt**, **Handel**, **Communities** och **Övriga**. Din AEM kan vara konfigurerad att visa olika grupper och komponenter.

1. Om du vill mappa Adobe Analytics-variabler med variabler som är definierade i komponenten drar du i en **Analysvariabel** från innehållssökaren till ett fält i spårningskomponenten. Dra till exempel `Page Name (pageName)` till `pagedata.title`.

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >Det Report Suite-ID (RSID) som har valts för ramverket avgör vilka Adobe Analytics-variabler som visas i innehållssökaren.

1. Upprepa de två föregående stegen för andra komponenter och variabler.

   >[!NOTE]
   >
   >Du kan mappa flera Analytics-variabler (till exempel `props`, `eVars`, `events`) till samma CQ-variabel (till exempel `pagedata.title`)

   >[!CAUTION]
   >
   >Vi rekommenderar starkt följande:
   >
   >* `eVars` och `props` mappas till CQ-variabler som börjar med antingen `pagedata.X` eller `eventdata.X`
   >* Händelser bör mappas till variabler som börjar med `eventdata.events.X`

1. Om du vill göra ramverket tillgängligt på publiceringsinstansen av webbplatsen öppnar du **Sida** sidosparkflik och klicka **Aktivera Framework.**

## Mappa produktrelaterade variabler {#mapping-product-related-variables}

AEM använder en konvention för att namnge produktrelaterade variabler och händelser som ska mappas till Adobe Analytics produktrelaterade egenskaper:

| CQ-variabel | Analysvariabel | Beskrivning |
|--- |--- |--- |
| `product.category` | `product.category` (konverteringsvariabel) | Produktkategorin. |
| `product.sku` | `product.sku` (konverteringsvariabel) | Produktens sku. |
| `product.quantity` | `product.quantity` (konverteringsvariabel) | Antalet produkter som köpts. |
| `product.price` | `product.price` (konverteringsvariabel) | Produktpriset. |
| `product.events.<eventName>` | Vilka lyckade händelser som ska kopplas till produkten i din rapport. | `product.events` är prefixet för namngivna händelser *eventName.* |
| `product.evars.<eVarName>` | Konverteringsvariabler ( `eVar`) för att associera med produkten. | `product.evars` är prefixet för eVar-variabler med namnet *eVarName.* |

Flera AEM Commerce-komponenter använder dessa variabelnamn.

>[!NOTE]
>
>Mappa inte egenskapen Adobe Analytics Products till en CQ-variabel. Konfigurering av produktrelaterade mappningar enligt beskrivningen i tabellen motsvarar i princip mappning av variabeln Produkter.

### Kontrollera rapporter om Adobe Analytics {#checking-reports-on-adobe-analytics}

1. Logga in på Adobe Analytics webbplats med samma inloggningsuppgifter som AEM.
1. Se till att det RSID som du valde är det som användes i föregående steg.
1. I **Rapporter** (till vänster på sidan) väljer **Anpassad konvertering** sedan **Anpassad konvertering 1-10** och markera variabeln som motsvarar `eVar7`

1. Beroende på vilken version av Adobe Analytics du använder måste du vänta i genomsnitt 45 minuter tills rapporten uppdateras med det sökord som används, till exempel eggplant i exemplet

## Använda Content Finder (cf#) med Adobe Analytics-ramverk {#using-the-content-finder-cf-with-adobe-analytics-frameworks}

När du först öppnar ett Adobe Analytics-ramverk innehåller innehållssökaren fördefinierade Analytics-variabler under:

* Trafik
* Konvertering
* Händelser

När ett RSID är markerat läggs alla variabler som tillhör det RSID till i listan.\
The `cf#` behövs för att mappa Analytics-variabler till CQ-variablerna som finns i de olika spårningskomponenterna. Se Konfigurera ett ramverk för grundläggande spårning.

Beroende på vilken vy som har valts för ramverket fylls innehållssökaren i av antingen Analytics-variabler (i AEM) eller CQ-variabler (i analysvyn).

Listan kan ändras på följande sätt:

1. När **AEM** kan listan filtreras beroende på vilken variabeltyp som väljs med hjälp av de tre filterknapparna:

   * If *ingen knapp* om du väljer det här alternativet visas hela listan.
   * Om **Trafik** om knappen är markerad visas endast de variabler som hör till trafikavsnittet.
   * Om **Konvertering** om du väljer det här alternativet visas endast de variabler som hör till avsnittet Konvertering.
   * Om **Händelser** om du väljer det här alternativet visas endast de variabler som hör till händelseavsnittet.

   >[!NOTE]
   >
   >Endast en filterknapp kan vara aktiv samtidigt.

   1. Listan har också en sökfunktion som filtrerar elementen efter den text som anges i sökfältet.
   1. Om ett filteralternativ är aktiverat när du söker efter element i listan, filtreras även de resultat som visas enligt den aktiva knappen.
   1. Listan kan läsas in igen när som helst med hjälp av pilknappen.
   1. Om flera RSID är markerade i ramverket visas alla variabler i listan med alla etiketter som används i de markerade RSID:erna.

1. I Adobe Analytics-vyn visar Content Finder alla CQ-variabler som tillhör spårningskomponenterna som dras i CQ-vyn.

   * I fallet med **Ladda ned komponent** är *endast en dragd* i CQ-vyn (som har två mappningsbara variabler *eventdata.downloadLink* och *eventdata.events.startDownload*) kommer Content Finder att se ut så här när du växlar till Adobe Analytics-vyn:

   ![aa-22](assets/aa-22.png)

   * Variablerna kan dras&amp;släppas till alla Adobe Analytics-variabler som tillhör någon av de tre variabelavsnitten (**Trafik**, **Konvertering** och **Händelser**).

   * När du drar en ny spårningskomponent till ramverket i CQ-vyn läggs de CQ-variabler som tillhör komponenten automatiskt till i Content Finder(cf#) i Adobe Analytics-vyn.

   >[!NOTE]
   >
   >Endast en CQ-variabel kan mappas till en Adobe Analytics-variabel åt gången.

## Använda AEM vy och analysvy {#using-aem-view-and-analytics-view}

Vid en given tidpunkt kan man växla mellan två sätt att visa Adobe Analytics-mappningarna när man befinner sig på en ramverkssida. De två vyerna ger en bättre översikt över mappningarna inom ramverket, från två olika perspektiv.

### AEM {#aem-view}

![aa-23](assets/aa-23.png)

Om du tar bilden ovan som exempel visas **AEM** har följande egenskaper:

1. Det här är standardvyn när ramverket öppnas.
1. Vänster sida: innehållssökaren (cf#) fylls i med Adobe Analytics-variabler baserat på de RSID(n) som valts.
1. Flikrubriker (**AEM** och **Analysvy**): använd dessa för att växla mellan de två vyerna.

1. **AEM**:

   1. Om ramverket har komponenter som ärvs från dess överordnade, visas de här tillsammans med variablerna som mappas till komponenterna.

      1. Ärvda komponenter är låsta.
      1. Om du vill låsa upp en ärvd komponent dubbelklickar du på hänglåset bredvid komponentens namn
      1. Om du vill återställa arvet tar du bort den olåsta komponenten. Därefter återfår den sin låsta status.

   1. **Dra komponenterna hit för att inkludera dem i analysramverket**: Komponenter kan dras från Sidekick och släppas här.
   1. Du kan hitta alla komponenter som för närvarande ingår i analysramverket:

      1. Om du vill lägga till en komponent drar du den från sidosparkens komponentflik
      1. Om du vill ta bort en komponent och alla dess mappningar väljer du Ta bort på komponentens snabbmeny och accepterar sedan borttagningen i bekräftelsedialogrutan.
      1. Tänk på att en komponent bara kan tas bort från ramverket som den skapades i och inte kan tas bort från underordnade ramverk i traditionell mening (de kan bara skrivas över).

### Analysvy {#analytics-view}

![aa-24](assets/aa-24.png)

1. Du kommer åt den här vyn genom att växla till **Analysvy** -fliken i ramverket.
1. Vänster sida: Content Finder (cf#) ifyllt av CQ-variabler baserat på de komponenter som dras till ramverket i CQ-vyn.
1. Flikrubriker (**AEM** och **Analysvy**): använd dessa för att växla mellan de två vyerna.

1. De tre tabellerna (Traffic, Conversion, Event) innehåller alla tillgängliga Adobe Analytics-variabler. som tillhör de markerade RSID:erna. Mappningarna som visas här ska vara desamma som i AEM:

   * **Trafik**:

      * Trafikvariabel ( `prop1`) mappas till en CQ-variabel ( `eventdata.downloadLink`)

      * När komponenten har en Padlock bredvid sig innebär det att den ärvs från ett överordnat ramverk och därför inte kan redigeras

   * **Konvertering**:

      * Konverteringsvariabel ( `eVar1`) mappas till en CQ-variabel ( `pagedata.title`)

      * Konverteringsvariabel ( `eVar3`) mappas till ett JavaScript-uttryck som lagts till internt genom att dubbelklicka på CQ-variabelfältet och ange koden manuellt

   * **Händelse**:

      * Händelsevariabel ( `event1`) mappas till en CQ-händelse ( `eventdata.events.pageView`)

>[!NOTE]
>
>CQ-variabelkolumnen för en tabell kan även fyllas i genom att dubbelklicka på fältet och lägga till text. Dessa fält accepterar JavaScript som indata.
>
>Till exempel bredvid `prop3` du kan lägga till:
>     `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
skicka *title* av en sida sammanfogad med *platshållare* använda *:* (kolon) och prefix med *Adobe* as `prop3`
>

>[!CAUTION]
>
Endast en CQ-variabel kan mappas till en Adobe Analytics-variabel åt gången.
