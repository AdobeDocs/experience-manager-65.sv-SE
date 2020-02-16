---
title: Utveckla formulär (klassiskt användargränssnitt)
seo-title: Utveckla formulär (klassiskt användargränssnitt)
description: Lär dig utveckla formulär
seo-description: Lär dig utveckla formulär
uuid: 33859f29-edc5-4bd5-a634-35549f3b5ccf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 6ee3bd3b-51d1-462f-b12e-3cbe24898b85
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Utveckla formulär (klassiskt användargränssnitt){#developing-forms-classic-ui}

En formulärs grundläggande struktur är:

* Formulärstart
* Formulärelement
* Formulärslut

Allt detta görs med en serie standardkomponenter [för](/help/sites-authoring/default-components.md#form)formulär som finns i en AEM-standardinstallation.

Förutom att [utveckla nya komponenter](/help/sites-developing/developing-components-samples.md) för dina formulär kan du också:

* [Läs in formuläret i förväg med värden](#preloading-form-values)
* [Förhandsladda (vissa fält) fält med flera värden
   ](#preloading-form-fields-with-multiple-values)
* [Utveckla nya åtgärder](#developing-your-own-form-actions)
* [Utveckla nya begränsningar](#developing-your-own-form-constraints)
* [Visa eller dölja specifika formulärfält](#showing-and-hiding-form-components)

[Använda skript](#developing-scripts-for-use-with-forms) för att utöka funktionaliteten där det behövs.

>[!NOTE]
>
>Det här dokumentet fokuserar på att utveckla formulär med [Foundation Components](/help/sites-authoring/default-components-foundation.md) i det klassiska användargränssnittet. Adobe rekommenderar att du använder de nya [kärnkomponenterna](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) och [Dölj villkor](/help/sites-developing/hide-conditions.md) för formulärutveckling i det beröringskänsliga användargränssnittet.

## Förhandsladda formulärvärden {#preloading-form-values}

Formulärstartkomponenten innehåller ett fält för **Läs in sökväg**, en valfri sökväg som pekar mot en nod i databasen.

Läs in sökväg är sökvägen till nodegenskaper som används för att läsa in fördefinierade värden till flera fält i formuläret.

Detta är ett valfritt fält som anger sökvägen till en nod i databasen. När den här noden har egenskaper som matchar fältnamnen förinläses motsvarande fält i formuläret med egenskapsvärdet. Om det inte finns någon matchning innehåller fältet standardvärdet.

>[!NOTE]
>
>En [formuläråtgärd](#developing-your-own-form-actions) kan också ange från vilken resurs de initiala värdena ska läsas in. Detta görs med hjälp `FormsHelper#setFormLoadResource` av insidan `init.jsp`.
>
>Formuläret fylls i av författaren från den sökväg som angetts i startformulärkomponenten endast om detta inte anges.

### Förhandsladda formulärfält med flera värden {#preloading-form-fields-with-multiple-values}

Olika formulärfält har också **objektets inläsningssökväg**, vilket är en valfri sökväg som pekar på en nod i databasen.

Inläsningssökväg för **objekt** är sökvägen till nodegenskaper som används för att läsa in fördefinierade värden i det specifika fältet i formuläret, till exempel en [nedrullningsbar lista](/help/sites-authoring/default-components-foundation.md#dropdown-list), [kryssrutegrupp](/help/sites-authoring/default-components-foundation.md#checkbox-group) eller [alternativgrupp](/help/sites-authoring/default-components-foundation.md#radio-group).

#### Exempel - Förhandsladda en listruta med flera värden {#example-preloading-a-dropdown-list-with-multiple-values}

En nedrullningsbar lista kan konfigureras med ditt värdeintervall för val.

Du kan använda **objektets inläsningssökväg** för att få åtkomst till en lista från en mapp i databasen och läsa in dessa i fältet i förväg:

1. Skapa en ny systemstängningsmapp ( `sling:Folder`), till exempel `/etc/designs/<myDesign>/formlistvalues`

1. Lägg till en ny egenskap (till exempel `myList`) av typen flervärdessträng ( `String[]`) som innehåller listan med nedrullningsbara objekt. Innehåll kan också importeras med hjälp av ett skript, t.ex. med ett JSP-skript eller cURL i ett gränssnittsskript.

1. Använd den fullständiga sökvägen i fältet **Objektets inläsningssökväg** :
till exempel `/etc/designs/geometrixx/formlistvalues/myList`

Observera att om värdena i `String[]` är i följande format:

* `AL=Alabama`
* `AK=Alaska`
* *osv.*

genererar AEM listan som:

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

Den här funktionen kan till exempel användas på ett bra sätt i en flerspråkig inställning.

### Utveckla egna formuläråtgärder {#developing-your-own-form-actions}

Ett formulär behöver en åtgärd. En åtgärd definierar den åtgärd som utförs när formuläret skickas med användardata.

En rad åtgärder ingår i en AEM-standardinstallation, som beskrivs nedan:

`/libs/foundation/components/form/actions`

och i listan **Åtgärdstyp** för **Form** -komponenten:

![chlimage_1-8](assets/chlimage_1-8.png)

I det här avsnittet beskrivs hur du kan utveckla egna formuläråtgärder som ska tas med i listan.

Du kan lägga till en egen åtgärd under `/apps` följande:

1. Skapa en nod av typen `sling:Folder`. Ange ett namn som återspeglar den åtgärd som ska implementeras.

   Exempel:

   `/apps/myProject/components/customFormAction`

1. På den här noden definierar du följande egenskaper och klickar sedan på **Spara alla** för att behålla ändringarna:

   * `sling:resourceType` - ange som `foundation/components/form/action`

   * `componentGroup` - definiera som `.hidden`

   * Valfritt:

      * `jcr:title` - ange en valfri titel som visas i den nedrullningsbara listan. Om inget anges visas nodnamnet

      * `jcr:description` - ange en beskrivning av ditt val

1. Skapa en dialognod i mappen:

   1. Lägg till fält så att författaren kan redigera formulärdialogrutan när åtgärden har valts.

1. I mappen skapar du antingen:

   1. Ett postskript.
Skriptets namn är `post.POST.<extension>`t.ex. `post.POST.jsp`Post-skriptet anropas när ett formulär skickas för att bearbeta formuläret, det innehåller koden som hanterar data som kommer från formuläret `POST`.

   1. Lägg till ett framåt-skript som anropas när formuläret skickas.
Skriptets namn är `forward.<extension`>, t.ex. `forward.jsp`Skriptet kan definiera en sökväg. Den aktuella begäran vidarebefordras sedan till den angivna sökvägen.
   Det nödvändiga anropet är `FormsHelper#setForwardPath` (2 varianter). Ett typiskt fall är att utföra viss validering, eller logik, för att hitta målsökvägen och sedan gå vidare till den sökvägen, och låta standardservern Sling POST göra den faktiska lagringen i JCR.

   Det kan också finnas en annan server som utför själva bearbetningen, i så fall är det formuläråtgärden och den `forward.jsp` fungerar bara som&quot;limkod&quot;. Ett exempel på detta är poståtgärden på `/libs/foundation/components/form/actions/mail`som vidarebefordrar information till `<currentpath>.mail.html`platsen där en e-postserver finns.

   Så:

   * a `post.POST.jsp` är användbart för små åtgärder som utförs helt av själva åtgärden
   * medan funktionen `forward.jsp` är användbar när endast delegering krävs.
   Körningsordningen för skripten är:

   * När formuläret återges ( `GET`):

      1. `init.jsp`
      1. för alla fältbegränsningar: `clientvalidation.jsp`
      1. formulärets valideringRT: `clientvalidation.jsp`
      1. formuläret läses in via inläsningsresurs om det är inställt
      1. `addfields.jsp` vid återgivning `<form></form>`
   * vid hantering av ett formulär `POST`:

      1. `init.jsp`
      1. för alla fältbegränsningar: `servervalidation.jsp`
      1. formulärets valideringRT: `servervalidation.jsp`
      1. `forward.jsp`
      1. om en framåtriktad sökväg angavs ( `FormsHelper.setForwardPath`), vidarebefordrar du begäran och ringer sedan `cleanup.jsp`

      1. om ingen framåtriktad sökväg har angetts, ring `post.POST.jsp` (slutar här, ingen `cleanup.jsp` anropad)




1. Lägg till igen i mappen om du vill:

   1. Ett skript för att lägga till fält.
Skriptets namn är `addfields.<extension>`t.ex. `addfields.jsp`ett addfields-skript anropas omedelbart efter att HTML-koden för formulärstarten har skrivits. Detta gör att åtgärden kan lägga till anpassade inmatningsfält eller annan sådan HTML-kod i formuläret.

   1. Ett initieringsskript.
Skriptets namn är `init.<extension>`t.ex. `init.jsp`skriptet anropas när formuläret återges. Den kan användas för att initiera åtgärdsinformation. &quot;

   1. Ett rensningsskript.
Skriptets namn är `cleanup.<extension>`t.ex. `cleanup.jsp`det här skriptet kan användas för att rensa.

1. Använd **Forms** -komponenten i en parsys. Listrutan **Åtgärdstyp** innehåller nu din nya åtgärd.

   >[!NOTE]
   >
   >Så här visar du standardåtgärder som ingår i produkten:
   >
   >
   >`/libs/foundation/components/form/actions`

### Utveckla egna formulärbegränsningar {#developing-your-own-form-constraints}

Begränsningar kan införas på två nivåer:

* För [enskilda fält (se följande procedur)](#constraints-for-individual-fields)
* Som [global validering av formulär](#form-global-constraints)

#### Begränsningar för enskilda fält {#constraints-for-individual-fields}

Du kan lägga till egna begränsningar för ett enskilt fält (under `/apps`) enligt följande:

1. Skapa en nod av typen `sling:Folder`. Ange ett namn som återspeglar den begränsning som ska implementeras.

   Exempel:

   `/apps/myProject/components/customFormConstraint`

1. På den här noden definierar du följande egenskaper och klickar sedan på **Spara alla** för att behålla ändringarna:

   * `sling:resourceType` - ställs in på `foundation/components/form/constraint`

   * `constraintMessage` - ett anpassat meddelande som visas om fältet inte är giltigt, enligt villkoret, när formuläret skickas

   * Valfritt:

      * `jcr:title` - ange en valfri titel som visas i urvalslistan. Om inget anges visas nodnamnet
      * `hint` - ytterligare information för användaren om hur fältet används

1. I den här mappen kan du behöva följande skript:

   * Ett klientvalideringsskript:
Skriptets namn är `clientvalidation.<extension>`t.ex. `clientvalidation.jsp`anropas när formulärfältet återges. Den kan användas för att skapa klient-javascript för att validera fältet på klienten.

   * Ett servervalideringsskript:
Skriptnamnet är `servervalidation.<extension>`t.ex. `servervalidation.jsp`det anropas när formuläret skickas. Den kan användas för att validera fältet på servern efter att det har skickats.

>[!NOTE]
>
>Exempelbegränsningar finns under:
>
>`/libs/foundation/components/form/constraints`

#### Formulärglobala begränsningar {#form-global-constraints}

Den globala valideringen av formulär anges genom att en resurstyp konfigureras i startformulärkomponenten ( `validationRT`). Exempel:

`apps/myProject/components/form/validation`

Sedan kan du definiera:

* a `clientvalidation.jsp` - injiceras efter fältets klientvalideringsskript
* och a `servervalidation.jsp` - anropas även efter att den enskilda fältservern validerats på en `POST`.

### Visa och dölja formulärkomponenter {#showing-and-hiding-form-components}

Du kan konfigurera formuläret så att det visar eller döljer formulärkomponenter enligt värdet i andra fält i formuläret.

Att ändra synligheten för ett formulärfält är användbart när fältet bara behövs under specifika förhållanden. Till exempel frågar en fråga kunderna om de vill ha produktinformation som de får via e-post. När du väljer Ja visas ett textfält där kunden kan ange sin e-postadress.

Använd dialogrutan **Redigera visa/dölj regler** för att ange under vilka förhållanden en formulärkomponent visas eller döljs.

![showhideeditor](assets/showhideeditor.png)

Använd fälten högst upp i dialogrutan för att ange följande information:

* Om du anger villkor för att dölja eller visa komponenten.
* Om något eller alla villkor måste vara true för att komponenten ska kunna visas eller döljas.

Ett eller flera villkor visas under dessa fält. Ett villkor jämför värdet för en annan formulärkomponent (i samma formulär) med ett värde. Om det faktiska värdet i fältet uppfyller villkoret utvärderas villkoret som sant. Villkoren innehåller följande information:

* Titeln på det formulärfält som testas.
* En operator.
* Ett värde jämförs med fältvärdet.

En Radio Group-komponent med titeln `Receive email notifications?`** innehåller till exempel `Yes` - och `No` alternativknappar. En textfältskomponent med titeln `Email Address` använder följande villkor så att den är synlig om den `Yes` är markerad:

![showhidecondition](assets/showhidecondition.png)

I Javascript används värdet för elementnamnsegenskapen för att referera till fält. I föregående exempel är elementnamnsegenskapen för komponenten Grupp med alternativknappar `contact`. Följande kod motsvarar JavaScript-koden för det exemplet:

`((contact == "Yes"))`

**Så här visar eller döljer du en formulärkomponent:**

1. Redigera den specifika formulärkomponenten.

1. Välj **Visa/Dölj** för att öppna dialogrutan **Redigera visa/dölj regler** :

   * I den första listrutan väljer du **Visa** eller **Dölj** för att ange om villkoren ska avgöra om komponenten ska visas eller döljas.

   * I listrutan i slutet av den översta raden väljer du:

      * **all** - om alla villkor måste vara true för att komponenten ska kunna visas eller döljas
      * **any** - om bara ett eller flera villkor måste vara true för att komponenten ska kunna visas eller döljas
   * Markera en komponent, operator och ange sedan ett värde på villkorslinjen (en visas som standard).
   * Lägg till fler villkor om det behövs genom att klicka på **Lägg till villkor**.
   Exempel:

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Spara definitionen genom att klicka på **OK** .

1. När du har sparat definitionen visas länken **Redigera regler** bredvid alternativet **Visa/dölj** i egenskaperna för formulärkomponenten. Klicka på den här länken för att öppna dialogrutan **Redigera visa/dölj regler** för att göra ändringar.

   Klicka på **OK** för att spara alla ändringar.

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >Effekterna av Visa/dölj-definitioner kan ses och testas:
   >
   >
   >
   >    * i **förhandsgranskningsläget** i författarmiljön (en sida måste läsas in igen när du först växlar till förhandsgranskning)
      >
      >    
   * publiceringsmiljön


#### Hantera brutna komponentreferenser {#handling-broken-component-references}

Visa/dölj-villkor använder värdet för elementnamnsegenskapen för att referera till andra komponenter i formuläret. Konfigurationen Visa/Dölj är ogiltig när något av villkoren refererar till en komponent som har tagits bort eller har ändrat elementnamnsegenskapen. När detta inträffar måste du uppdatera villkoren manuellt, annars inträffar ett fel när formuläret läses in.

När konfigurationen Visa/Dölj är ogiltig anges konfigurationen bara som JavaScript-kod. Redigera koden för att korrigera problemen.Koden använder elementnamnsegenskapen som ursprungligen användes för att referera till komponenterna.

### Utveckla skript för användning med formulär {#developing-scripts-for-use-with-forms}

Mer information om API-elementen som kan användas när skript skrivs finns i [javadokartorna för formulär](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html).

Du kan använda detta för åtgärder som att anropa en tjänst innan formuläret skickas och att avbryta tjänsten om den misslyckas:

* Definiera valideringsresurstypen
* Inkludera ett skript för validering:

   * Ring webbtjänsten i din JSP och skapa ett `com.day.cq.wcm.foundation.forms.ValidationInfo` objekt med dina felmeddelanden. Om fel uppstår bokförs inte formulärdata.
