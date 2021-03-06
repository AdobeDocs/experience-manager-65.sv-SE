---
title: Skapa och ordna sidor
description: Skapa och hantera sidor med AEM
translation-type: tm+mt
source-git-commit: 90364cdf6044616d43c1851b3def9b1f063449ca
workflow-type: tm+mt
source-wordcount: '2523'
ht-degree: 4%

---


# Skapa och ordna sidor {#creating-and-organizing-pages}

I det här avsnittet beskrivs hur du skapar och hanterar sidor med Adobe Experience Manager (AEM) så att du sedan kan [skapa innehåll](/help/sites-authoring/editing-content.md) på dessa sidor.

>[!NOTE]
>
>Ditt konto behöver [åtkomsträttigheter](/help/sites-administering/security.md) och [behörighet](/help/sites-administering/security.md#permissions) för att kunna utföra åtgärder på sidor som skapa, kopiera, flytta, redigera och ta bort.
>
>Om du råkar ut för problem rekommenderar vi att du kontaktar systemadministratören.

>[!NOTE]
>
>Det finns ett antal [kortkommandon](/help/sites-authoring/keyboard-shortcuts.md) som du kan använda från webbplatskonsolen för att ordna dina sidor mer effektivt.

## Organisera din webbplats {#organizing-your-website}

Som författare måste du ordna din webbplats inom AEM. Detta innebär att du skapar och namnger innehållssidorna så att:

* Du kan enkelt hitta dem i redigeringsmiljön
* Besökare på webbplatsen kan enkelt hitta dem i publiceringsmiljön

Du kan också använda [mappar](#creating-a-new-folder) för att ordna innehållet.

Strukturen på en webbplats kan ses som en trädstruktur som innehåller dina innehållssidor. Namnen på dessa innehållssidor används för att skapa URL-adresserna, medan titeln visas när sidinnehållet visas.

I följande exempel visas ett exempel från webbplatsen We.Retail, där du kan komma åt en vandrande kortsida ( `desert-sky-shorts`):

* Författarmiljö
   `https://localhost:4502/editor.html/content/we-retail/us/en/products/equipment/hiking/desert-sky-shorts.html`

* Publiceringsmiljö
   `https://localhost:4503/content/we-retail/us/en/products/equipment/hiking/desert-sky-shorts.html`

Beroende på instansens konfiguration kan det vara valfritt att använda `/content` i publiceringsmiljön.

```xml
 /content
 /we-retail
  /us
   /en
    /products
     /equipment
      /hiking
       /desert-sky-shorts
       /hiking-poles
       /...
      /running...
      /surfing...
      /...
     /seasonal...
     /...
    /about-us
    /experience
    /...
   /es...
  /de...
  /fr...
  /...
 /...
```

Den här strukturen kan visas Från konsolen **Platser**, där du kan [navigera bland sidorna på webbplatsen](/help/sites-authoring/basic-handling.md#navigating) och utföra åtgärder på sidorna. Du kan också skapa nya webbplatser och [nya sidor](#creating-a-new-page).

Du kan se grenen uppåt från vägbeskrivningar i sidhuvudsfältet:

![caop-01](assets/caop-01.png)

### Sidnamnkonventioner {#page-naming-conventions}

När du skapar en ny sida finns det två nyckelfält:

* **[Titel](#title)**:

   * Detta visas för användaren i konsolen och visas överst i sidinnehållet när det redigeras.
   * Detta fält är obligatoriskt.

* **[Namn](#name)**:

   * Detta används för att generera URI:n.
   * Användarindata för det här fältet är valfria. Om inget anges hämtas namnet från titeln. Mer information finns i följande avsnitt [Begränsningar för sidnamn och bästa praxis](/help/sites-authoring/managing-pages.md#page-name-restrictions-and-best-practices).

#### Begränsningar för sidnamn och bästa praxis {#page-name-restrictions-and-best-practices}

Sidans **titel** och **namn** kan skapas separat men hänger ihop:

* När du skapar en sida krävs bara fältet **Titel**. Om inget **namn** anges när sidan skapas, kommer AEM att generera ett namn från de första 64 tecknen i titeln (med den validering som anges nedan). Endast de första 64 tecknen används för att ge stöd åt de bästa sätten med namn på korta sidor.

* Om ett sidnamn anges manuellt av författaren gäller inte gränsen på 64 tecken, men andra tekniska begränsningar på sidnamnets längd kan förekomma.

>[!NOTE]
>
>När du definierar ett sidnamn är en bra tumregel att hålla sidnamnet så kort, men så uttrycksfullt och minnesvärt som möjligt så att det blir lätt att förstå för läsaren. Mer information finns i [W3C-formatguiden](https://www.w3.org/Provider/Style/TITLE.html) för `title`-elementet.
>
>Tänk också på att vissa webbläsare (t.ex. äldre versioner av IE) bara kan acceptera URL:er med en viss längd, så det finns också tekniska skäl att hålla sidnamnen korta.

När du skapar en ny sida kommer AEM att [validera sidnamnet enligt konventionerna](/help/sites-developing/naming-conventions.md) som AEM och JCR har infört.

Minsta tillåtna tecken är:

* &#39;a&#39; till &#39;z&#39;
* A till Z
* 0 till 9
* `_` (understreck)
* `-` (minus/bindestreck)

Fullständig information om alla tillåtna tecken finns i [namnkonventionen](/help/sites-developing/naming-conventions.md).

>[!NOTE]
>
>Om AEM körs på en [MongoMK persistence Manager-distribution](/help/sites-deploying/recommended-deploys.md) är sidnamnen begränsade till 150 tecken.

#### Titel {#title}

Om du bara anger en **sidtitel** när du skapar en ny sida härleds sidans **namn**[ i AEM från den här strängen och namnet valideras enligt konventionerna i AEM och JCR. ](/help/sites-developing/naming-conventions.md) Ett **titelfält** som innehåller ogiltiga tecken accepteras, men det härledda namnet kommer att ersätta ogiltiga tecken. Till exempel:

| Titel | Härlett namn |
|---|---|
| Schön | schoen.html |
| SC%&amp;*ç+ | sc---c-.html |

#### Namn {#name}

När du anger en sida **Namn** när du skapar en ny sida, kommer AEM att [validera namnet enligt konventionerna](/help/sites-developing/naming-conventions.md) som AEM och JCR har infört. Du kan inte skicka ogiltiga tecken i fältet **Namn**. När AEM upptäcker ogiltiga tecken markeras fältet med en förklaring.

![caop-02](assets/caop-02.png)

>[!NOTE]
>
>Du bör undvika att använda en kod med två bokstäver enligt ISO-639-1 som sidnamn, såvida det inte är en språkrot.
>
>Mer information finns i [Förbereda innehåll för översättning](/help/sites-administering/tc-prep.md).

### Mallar {#templates}

I AEM anger en mall en speciell typ av sida. En mall kommer att användas som bas för alla nya sidor som skapas.

Mallen definierar strukturen för en sida, inklusive en miniatyrbild och andra egenskaper. Du kan till exempel ha separata mallar för produktsidor, platskartor och kontaktinformation. Mallar består av [komponenter](#components).

AEM innehåller flera färdiga mallar. Vilka mallar som är tillgängliga beror på den enskilda webbplatsen. Nyckelfälten är:

* **Titel**
Den titel som visas på den slutliga webbsidan.

* **Namn**
Används när sidan namnges.

* ****
MallEn lista med mallar som är tillgängliga för att användas när den nya sidan genereras.

>[!NOTE]
>
>Om den är konfigurerad på din instans kan [mallförfattare skapa mallar med mallredigeraren](/help/sites-authoring/templates.md).

### Komponenter {#components}

Komponenterna är de element som AEM tillhandahåller så att du kan lägga till specifika typer av innehåll. AEM innehåller ett urval [körklara komponenter](/help/sites-authoring/default-components-console.md) som ger omfattande funktionalitet. Bland dessa finns:

* Text
* Bild
* Bildspel
* Video
* Och många fler

När du har skapat och öppnat en sida kan du [lägga till innehåll med komponenterna](/help/sites-authoring/editing-content.md#insertinganewparagraph), som är tillgängliga i [komponentwebbläsaren](/help/sites-authoring/author-environment-tools.md#componentbrowser).

>[!NOTE]
>
>[Komponentkonsolen](/help/sites-authoring/default-components-console.md) ger en översikt över komponenterna i din instans.

## Hantera sidor {#managing-pages}

### Skapar en ny sida {#creating-a-new-page}

Om du inte har skapat alla sidor åt dig i förväg måste du skapa en sida innan du kan börja skapa innehåll:

1. Öppna konsolen Platser (till exempel [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)).
1. Navigera till den plats där du vill skapa den nya sidan.
1. Öppna listrutan med **Skapa** i verktygsfältet och välj sedan **Sida** i listan:

   ![caop-03](assets/caop-03.png)

1. Från det första steget i guiden kan du antingen:

   * Välj den mall som du vill använda för att skapa den nya sidan och klicka/tryck sedan på **Nästa** för att fortsätta.

   * **Avbryt** om du vill avbryta processen.

   ![caop-04](assets/caop-04.png)

1. Från det sista steget i guiden kan du antingen:

   * Använd de tre flikarna för att ange de [sidegenskaper](/help/sites-authoring/editing-page-properties.md) som du vill tilldela den nya sidan och klicka/tryck sedan på **Skapa** för att skapa sidan.

   * Använd **Tillbaka** om du vill återgå till mallvalet.

   Nyckelfält är:

   * **Titel**:

      * Detta visas för användaren och är obligatoriskt.
   * **Namn**:

      * Detta används för att generera URI:n. Om inget anges hämtas namnet från titeln.
      * Om du anger en sida **Namn** när du skapar en ny sida, kommer AEM att [validera namnet enligt konventionerna](/help/sites-developing/naming-conventions.md) som AEM och JCR har infört.

      * Du **kan inte skicka ogiltiga tecken** i fältet **Namn**. När AEM upptäcker ogiltiga tecken markeras fältet och en förklaring visas som anger vilka tecken som behöver tas bort/ersättas.
   >[!NOTE]
   >
   >Se [Konventioner för sidnamngivning](#page-naming-conventions).

   Den information som krävs för att skapa en ny sida är **titeln**.

   ![caop-05](assets/caop-05.png)

1. Använd **Skapa** för att slutföra processen och skapa en ny sida. Bekräftelsedialogrutan frågar om du vill **öppna** sidan direkt eller återgå till konsolen (**Klar**):

   ![chlimage_1-118](assets/chlimage_1-118.png)

   >[!NOTE]
   >
   >Om du skapar en sida med ett namn som redan finns på den platsen, genereras automatiskt en variant av namnet genom att en siffra läggs till. Om `winter` till exempel redan finns blir en ny sida `winter0`.

1. Om du återgår till konsolen ser du den nya sidan:

   ![caop-06](assets/caop-06.png)

>[!CAUTION]
>
>När en sida har skapats går det inte att ändra dess mall, såvida du inte [skapar en startsida med en ny mall](/help/sites-authoring/launches-creating.md#create-launch-with-new-template), även om innehåll som redan finns försvinner.

### Öppna en sida för redigering {#opening-a-page-for-editing}

När du har skapat en sida eller navigerat till en befintlig sida (i konsolen) kan du öppna den för redigering:

1. Öppna konsolen **Platser**.
1. Navigera tills du hittar sidan som du vill redigera.
1. Välj sida genom att använda något av följande:

   * [Snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Markeringsläge ](/help/sites-authoring/basic-handling.md#navigatingandselectionmode) och verktygsfältet

   Välj sedan ikonen **Redigera**:

   ![screen_shot_2018-03-22at105355](assets/screen_shot_2018-03-22at105355.png)

1. Sidan öppnas och du kan [redigera sidan](/help/sites-authoring/editing-content.md#touchoptimizedui) efter behov.

>[!NOTE]
>
>Du kan bara navigera till andra sidor från sidredigeraren i förhandsgranskningsläget eftersom länkarna inte är aktiva i redigeringsläget.

### Kopiera och klistra in en sida {#copying-and-pasting-a-page}

Du kan kopiera en sida och alla dess underordnade sidor till en ny plats:

1. Navigera i konsolen **Platser** tills du hittar sidan som du vill kopiera.
1. Välj sida med någon av följande metoder:

   * [Snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Markeringsläge ](/help/sites-authoring/basic-handling.md#navigatingandselectionmode) och verktygsfältet

   Sedan sidikonen **Copy**:

   ![screen_shot_2018-03-22at105425](assets/screen_shot_2018-03-22at105425.png)

   >[!NOTE]
   >
   >Om du är i markeringsläge avslutas detta automatiskt så snart sidan kopieras.

1. Navigera till platsen för den nya kopian av sidan.
1. Ikonen **Klistra in** är tillgänglig med en nedåtpil direkt till höger:

   ![Klistra in](assets/paste-without-children.png)

   Du kan antingen:
   * Markera sidikonen **Klistra in**: En kopia av originalsidan och eventuella underordnade sidor skapas på den här platsen.
   * Markera listrutepilen för att visa alternativet **Klistra in utan underordnade**. En kopia av originalsidan kommer att skapas på denna plats. underordnade sidor kopieras inte.

   >[!NOTE]
   >
   >Om du kopierar sidan till en plats där det redan finns en sida med samma namn som originalet, kommer systemet automatiskt att generera en variant av namnet genom att lägga till en siffra. Om `winter` till exempel redan finns `winter` blir `winter1`.

### Flytta eller byta namn på en sida {#moving-or-renaming-a-page}

>[!NOTE]
>
>Om du byter namn på en sida gäller även [Sidnamngivningskonventioner](#page-naming-conventions) när du anger det nya sidnamnet.

>[!NOTE]
>
>En sida kan bara flyttas till en plats där mallen som sidan baseras på tillåts. Mer information finns i [Malltillgänglighet](/help/sites-developing/templates.md#template-availability).

Proceduren för att flytta eller byta namn på en sida är i princip densamma och hanteras av samma guide. Med den här guiden kan du:

* Byt namn på en sida utan att flytta den.
* Flytta sidan utan att byta namn på den.
* Flytta och byt namn samtidigt.

I AEM finns funktioner för att uppdatera interna länkar som refererar till sidan som byter namn/flyttas. Detta kan göras sida för sida för att ge full flexibilitet.

1. Navigera tills du hittar sidan som du vill flytta.
1. Välj sida med någon av följande metoder:

   * [Snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Markeringsläge ](/help/sites-authoring/basic-handling.md#navigatingandselectionmode) och verktygsfältet

   Välj sedan sidikonen **Flytta**:

   ![screen_shot_2018-03-22at105534](assets/screen_shot_2018-03-22at105534.png)

   Guiden Flytta sida öppnas.

1. Från **Ändra namn**-fasen i guiden kan du antingen:

   * Ange det namn du vill att sidan ska ha efter att den har flyttats och klicka/tryck sedan på **Nästa** för att fortsätta.

   * **Avbryt** om du vill avbryta processen.

   ![caop-07](assets/caop-07.png)

   Sidnamnet kan vara detsamma om du bara flyttar sidan.

   >[!NOTE]
   >
   >Om du flyttar en sida till en plats där det redan finns en sida med samma namn, kommer systemet automatiskt att generera en variant av namnet genom att lägga till en siffra. Om `winter` till exempel redan finns `winter` blir `winter1`.

1. Från **Välj mål**-fasen i guiden kan du antingen:

   * Använd [kolumnvyn](/help/sites-authoring/basic-handling.md#column-view) för att navigera till sidans nya plats:

      * Markera målet genom att klicka på målets miniatyrbild.
      * Klicka på **Nästa** för att fortsätta.
   * Använd **Tillbaka** för att återgå till sidnamnsspecifikationen.

   >[!NOTE]
   >
   >Som standard väljs den överordnade sidan för sidan som du flyttar/byter namn på som mål.

   ![caop-08](assets/caop-08.png)

   >[!NOTE]
   >
   >Om du flyttar en sida till en plats där det redan finns en sida med samma namn, kommer systemet automatiskt att generera en variant av namnet genom att lägga till en siffra. Om `winter` till exempel redan finns `winter` blir `winter1`.

1. Om sidan är länkad till eller refererad, eller har publicerats, visas informationen i steget **Justera/Publicera om**.

   Du kan ange vilka som ska justeras och/eller publiceras på nytt efter behov.

   >[!NOTE]
   >
   >Om sidan varken är länkad till eller refererad är det här steget inte tillgängligt.

   ![caop-09](assets/caop-09.png)

1. Om du väljer **Flytta** slutförs processen och du flyttar/byter namn på sidan efter behov.

>[!NOTE]
>
>Om sidan redan har publicerats avpubliceras den automatiskt när du flyttar den. Som standard publiceras den om när flytten är klar, men detta kan ändras genom att avmarkera fältet **Publicera om** i **Justera/Publicera**-steget.

>[!NOTE]
>
>Om det inte finns någon referens till sidan på något sätt hoppas steget **Justera/Publicera** över.

#### Asynkrona åtgärder {#asynchronous-actions}

Vanligtvis utförs en åtgärd för att flytta eller byta namn på en sida direkt. Detta betraktas som synkron bearbetning och ytterligare åtgärder i gränssnittet blockeras tills åtgärden är klar.

Om antalet sidor som påverkas ligger över en angiven gräns, kommer åtgärden att bearbetas asynkront, vilket gör att användaren kan fortsätta att redigera i gränssnittet utan att detta hindras av åtgärden för att flytta sidan eller byta namn.

* När du klickar på **Flytta** i det sista steget ovan kontrollerar AEM den konfigurerade gränsen.
* Om antalet sidor som påverkas ligger under gränsen utförs en synkron åtgärd.
* Om antalet sidor som påverkas ligger över gränsen utförs en asynkron åtgärd.
   * Användaren måste definiera när den asynkrona åtgärden ska utföras
      * **Kör** nu det asynkrona jobbet omedelbart.
      * **Med** Laterge kan användaren definiera när det asynkrona jobbet ska starta.

         ![Asynkron flyttning av sida](assets/asynchronous-page-move.png)

Status för asynkrona jobb kan kontrolleras i kontrollpanelen [**Async Jobs Status**](/help/sites-administering/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) på **Global navigering** -> **Verktyg** -> **Åtgärder** -> **Jobs**

>[!NOTE]
>
>Mer information om asynkron jobbbearbetning och hur du konfigurerar gränsen för åtgärder för att flytta/byta namn på sidor finns i dokumentet [Asynkrona jobb](/help/sites-administering/asynchronous-jobs.md) i användarhandboken för administration.

>[!NOTE]
>
>Asynkron bearbetning av sidflyttning kräver AEM 6.5.3.0 eller senare.

### Tar bort en sida {#deleting-a-page}

1. Navigera tills du ser sidan som du vill ta bort.
1. Använd [markeringsläget](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) för att markera önskad sida och använd sedan **Ta bort** i verktygsfältet:

   ![screen_shot_2018-03-22at105622](assets/screen_shot_2018-03-22at105622.png)

   >[!NOTE]
   >
   >Som en säkerhetsåtgärd är ikonen **Ta bort** inte tillgänglig som en snabbåtgärd.

1. En dialogruta öppnas där du uppmanas att bekräfta. Använd:

   * **Avbryt** om du vill avbryta åtgärden
   * **Bekräfta åtgärden genom att** ta bort:

      * Om sidan inte har några referenser tas sidan bort.
      * Om sidan innehåller referenser visas ett meddelande om att **en eller flera sidor refereras.** Du kan välja  **Tvinga** borttagning eller  **Avbryt**.

>[!NOTE]
>
>Om en sida redan har publicerats avpubliceras den automatiskt innan den tas bort.

### Låsa en sida {#locking-a-page}

Du kan [låsa/låsa upp en sida](/help/sites-authoring/editing-content.md#locking-a-page) från en konsol eller när du redigerar en enskild sida. Information om huruvida en sida är låst visas också på båda platserna.

![screen_shot_2018-03-22at105713](assets/screen_shot_2018-03-22at105713.png) ![screen_shot_2018-03-22at105720](assets/screen_shot_2018-03-22at105720.png)

### Skapar en ny mapp {#creating-a-new-folder}

Du kan skapa mappar som hjälper dig att ordna dina filer och sidor.

>[!NOTE]
>
>Mappar omfattas också av [sidnamngivningskonventionerna](#page-naming-conventions) när du anger det nya mappnamnet.

>[!CAUTION]
>
>* Mappar kan bara skapas direkt under **Platser** eller under andra mappar. De kan inte skapas under en sida.
>* Standardåtgärderna för att flytta, kopiera, klistra in, ta bort, publicera, avpublicera och visa/redigera egenskaper kan utföras på en mapp.
>* Det går inte att välja mappar i en live-kopia.

>



1. Öppna konsolen **Platser** och navigera till önskad plats.
1. Om du vill öppna alternativlistan väljer du **Skapa** i verktygsfältet
1. Välj **Mapp** för att öppna dialogrutan. Här anger du **Namn** och **Titel**:

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Välj **Skapa** för att skapa mappen.
