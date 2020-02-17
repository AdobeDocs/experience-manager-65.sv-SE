---
title: Introduktion till utveckling av anpassningsbara formulär
seo-title: Introduktion till utveckling av anpassningsbara formulär
description: AEM Forms har ett lättanvänt men ändå kraftfullt gränssnitt för framtagning av adaptiva formulär. Den innehåller en mängd komponenter och verktyg som du kan använda för att skapa formulär.
seo-description: AEM Forms har ett lättanvänt men ändå kraftfullt gränssnitt för framtagning av adaptiva formulär. Den innehåller en mängd komponenter och verktyg som du kan använda för att skapa formulär.
uuid: 3b150507-41b9-47c2-a94c-f85b903b2274
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: ba70921e-db7e-43f6-902c-1065d3b13aef
docset: aem65
translation-type: tm+mt
source-git-commit: 709d8fe467f5449eb1e844a49126535a4a4a6e7a

---


# Introduktion till utveckling av anpassningsbara formulär {#introduction-to-authoring-adaptive-forms}

## Översikt {#overview}

Med adaptiva formulär kan du skapa formulär som är engagerande, responsiva, dynamiska och anpassningsbara. AEM Forms har ett intuitivt användargränssnitt och färdiga komponenter för att skapa och arbeta med adaptiva formulär. Du kan välja att skapa ett anpassat formulär baserat på en formulärmodell eller ett schema eller utan en formulärmodell. Det är viktigt att du noga väljer den formulärmodell som inte bara passar dina behov, utan som utökar dina befintliga infrastrukturinvesteringar och resurser. Du kan välja mellan följande alternativ för att skapa ett anpassat formulär:

* **Använda en formulärdatamodell**
   [Med dataintegrering](../../forms/using/data-integration.md) kan ni integrera enheter och tjänster från olika datakällor i en formulärdatamodell som ni kan använda för att skapa anpassade formulär. Välj formulärdatamodell om det adaptiva formulär du skapar inbegriper hämtning och skrivning av data från och till flera datakällor.

* **Att använda en XDP-formulärmall**&#x200B;är en idealisk formulärmodell om du har investeringar i XFA-baserade eller XDP-formulär. Det är ett direkt sätt att konvertera XFA-baserade formulär till anpassningsbara formulär. Alla befintliga XFA-regler behålls i de tillhörande adaptiva formulären. De färdiga adaptiva formulären har stöd för XFA-konstruktioner, till exempel valideringar, händelser, egenskaper och mönster.

* **Om du använder en XSD (XML Schema Definition) eller ett JSON Schema** XML- och JSON-schema representerar detta strukturen i vilken data produceras eller används av företagets back-end-system. Du kan koppla schemat till ett anpassat formulär och använda dess element för att lägga till dynamiskt innehåll i det anpassningsbara formuläret. Elementen i schemat kommer att vara tillgängliga för användning på fliken Datamodellobjekt i innehållsläsaren när du redigerar adaptiva formulär.

* **Om du använder inga eller utan en formulärmodell** Adaptiva formulär som skapas med det här alternativet används ingen formulärmodell. Data-XML som genereras från sådana formulär har en platt struktur med fält och motsvarande värden.

Mer information om hur du skapar ett adaptivt formulär finns i [Skapa ett adaptivt formulär](../../forms/using/creating-adaptive-form.md).

## Gränssnitt för redigering av anpassningsbara formulär {#adaptive-form-authoring-ui}

Det pekoptimerade användargränssnittet för att skapa anpassningsbara formulär är intuitivt och ger:

* Dra-och-släpp-funktioner
* Standardformulärkomponenter
* Integrerad databas för resurser

När du skapar ett nytt eller redigerar ett befintligt anpassat formulär använder du följande gränssnittselement:

* [Sidebar](#sidebar)
* [Verktygsfältet Sida](#page-toolbar)
* [Komponentverktygsfältet](#component-toolbar)
* [Adaptiv formulärsida](#af-page)

![Gränssnitt för redigering av anpassningsbara formulär](assets/formeditor.png)

******S. Sidofält** B. Sida, verktygsfält **C.** Adaptiv formulärsida

### Sidebar {#sidebar}

Med sidofältet kan du

* Se formulärinnehåll som paneler, komponenter, fält och layout.
* Redigera komponentegenskaper.
* Sök, visa och använd resurser i din AEM Digital Asset Management-databas (DAM).
* Lägg till komponenter i formuläret.

![Sidebar](assets/sidebar-comps.png)

******** S. Innehållsläsaren **B. Egenskapsläsaren** C.**Resurser, webbläsare** D. Komponentwebbläsare

<!--Click to enlarge

](assets/sidebar-comps-1.png) -->

Sidlisten innehåller följande webbläsare:

* **Innehållsläsaren** I innehållsläsaren kan du se

   * **Formulärobjekt** visar formulärets objekthierarki. Författaren kan navigera till en viss formulärkomponent genom att trycka på det elementet i formulärobjektträdet. Författaren kan söka efter objekt och ordna om dem från det här trädet.

   * **Datamodellsobjekt**Här kan du se formulärmodellens hierarki.
Det gör att du kan dra och släppa formulärmodellelement i det anpassade formuläret. De tillagda elementen konverteras automatiskt till formulärkomponenter samtidigt som deras ursprungliga egenskaper behålls. Du kan se datamodellsobjekt när formuläret använder XML-schema, JSON-schema eller XDP-mall.

* **Egenskapswebbläsaren**

   Gör att du kan redigera egenskaperna för en komponent. Egenskaperna ändras enligt en komponent. Så här visar du egenskaper för den adaptiva formulärbehållaren:

   Markera en komponent, tryck sedan på ![fältnivå](assets/field-level.png) > **Adaptiv formulärbehållare** och tryck sedan på ![cmpr](assets/cmppr.png).

* **Resursläsaren**

   Segmenterar olika typer av innehåll, t.ex. bilder, dokument, sidor, filmer och så vidare.

* **Komponentwebbläsare**

   Innehåller komponenter som du kan använda för att skapa ett anpassat formulär. Du kan dra komponenter från till det adaptiva formuläret för att lägga till formulärelement och konfigurera tillagda element enligt kraven. I följande tabell beskrivs komponenterna i komponentwebbläsaren.

<table>
 <tbody>
  <tr>
   <th><strong>Komponent</strong></th>
   <th><strong>Funktionalitet</strong></th>
  </tr>
  <tr>
   <td>Adobe Sign-block</td>
   <td>Lägger till ett textblock med platshållare för fält som ska fyllas i vid signering med Adobe Sign.</td>
  </tr>
  <tr>
   <td>Knapp</td>
   <td>Lägger till en knapp som du kan konfigurera för att utföra åtgärder som att spara, återställa, gå vidare, gå till föregående och så vidare.</td>
  </tr>
  <tr>
   <td>Captcha</td>
   <td>Lägger till CAPTCHA-validering med Google reCAPTCHA-tjänsten. Mer information finns i <a href="../../forms/using/captcha-adaptive-forms.md" target="_blank">Använda CAPTCHA i adaptiva formulär</a>.</td>
  </tr>
  <tr>
   <td>Diagram</td>
   <td>Lägger till ett diagram som du kan använda i adaptiva formulär och dokument för visuell representation av tvådimensionella data i repeterbara paneler och tabellrader.</td>
  </tr>
  <tr>
   <td>Kryssruta</td>
   <td>Lägger till en kryssruta.</td>
  </tr>
  <tr>
   <td>Datumindatafält</td>
   <td>Använd datumindatafält i formuläret för att låta kunderna fylla i dag, månad och år separat i tre rutor. Du kan anpassa komponentens utseende och känsla och ändra datumformatet. Du kan till exempel låta kunderna ange datum i formaten MM/DD/ÅÅÅÅ eller DD/MM/ÅÅÅÅ.</td>
  </tr>
  <tr>
   <td>Datumväljaren</td>
   <td>Lägger till ett kalenderfält för att välja ett datum.</td>
  </tr>
  <tr>
   <td>Dokumentfragment</td>
   <td>Gör att du kan lägga till återanvändbara komponenter i en korrespondens.</td>
  </tr>
  <tr>
   <td>Dokumentfragmentgrupp</td>
   <td>Gör att du kan lägga till en grupp med relaterade dokumentfragment som du kan använda i en brevmall som en enskild enhet.</td>
  </tr>
  <tr>
   <td>Nedrullningsbar lista</td>
   <td>Lägger till en nedrullningsbar lista - en eller flera markeringar</td>
  </tr>
  <tr>
   <td>E-post</td>
   <td><p>Lägger till ett fält för att hämta e-postadressen. E-postkomponenten validerar som standard e-postadresser med följande reguljära uttryck.</p> <p><code>^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:.[a-zA-Z0-9-]+)*$</code></p> </td>
  </tr>
  <tr>
   <td>Bifogad fil</td>
   <td><p>Lägger till en knapp som gör att användare kan bläddra bland och bifoga stöddokument till ett formulär.</p> <p><strong>Obs! Komponenten </strong>för bifogad fil har stöd för en fördefinierad uppsättning filformat i adaptiva formulär som är aktiverade för Adobe Sign. Mer information finns i <a href="https://helpx.adobe.com/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text">Filformat</a>som stöds.</p> </td>
  </tr>
  <tr>
   <td>Lista över bifogade filer</td>
   <td>Lägger till ett fält som visar alla bifogade filer som har överförts med komponenten Bifogad fil.</td>
  </tr>
  <tr>
   <td>Sidfot<br /> </td>
   <td>Lägger till sidhuvudet som vanligtvis innehåller en företagslogotyp, formulärets rubrik och sammanfattning.<br /> </td>
  </tr>
  <tr>
   <td>Sidhuvud</td>
   <td>Lägger till sidfoten som vanligtvis innehåller copyrightinformation och länkar till andra sidor. </td>
  </tr>
  <tr>
   <td>Bild</td>
   <td>Gör att du kan infoga en bild.</td>
  </tr>
  <tr>
   <td>Bildval</td>
   <td>Gör att kunderna kan välja en bild som ger information. Ni kan använda informationen för att tillhandahålla personaliserade tjänster till era kunder.</td>
  </tr>
  <tr>
   <td>Knappen Nästa</td>
   <td>Lägger till en knapp för att navigera till nästa panel i ett formulär.</td>
  </tr>
  <tr>
   <td>Numerisk ruta</td>
   <td>Lägger till ett fält för att hämta numeriska värden</td>
  </tr>
  <tr>
   <td>Numerisk stege</td>
   <td>Använd Numeric Stepper i formuläret för att låta kunderna ange ett numeriskt värde som de kan öka eller minska baserat på ett fördefinierat steg.</td>
  </tr>
  <tr>
   <td>Panel</td>
   <td><p>Lägger till en panel eller underpanel.</p> <p>Du kan också lägga till en panelkomponent från den överordnade panelens verktygsfält med knappen <span class="uicontrol">Lägg till underordnad panel</code> . På samma sätt kan du lägga till ett panelspecifikt verktygsfält med knappen <span class="uicontrol">Lägg till panelverktygsfält</code> . Du kan konfigurera placeringen av panelens verktygsfält med hjälp av dialogrutan Redigera panel.</code></code></p> </td>
  </tr>
  <tr>
   <td>Lösenordsruta</td>
   <td>Lägger till ett fält för att hämta ett lösenord.</td>
  </tr>
  <tr>
   <td>Knappen Föregående</td>
   <td>Lägger till en knapp som användare behöver för att gå tillbaka till föregående sida eller panel.</td>
  </tr>
  <tr>
   <td>Alternativknapp</td>
   <td>Lägger till alternativknappar.</td>
  </tr>
  <tr>
   <td>Knappen Återställ</td>
   <td>Lägger till en knapp för att återställa formulärfält.</td>
  </tr>
  <tr>
   <td>Spara-knapp</td>
   <td>Lägger till en knapp för att spara formulärdata.</td>
  </tr>
  <tr>
   <td>(Borttagen) Klottsignatur</td>
   <td>Lägger till ett fält för att hämta skriptsignaturer.</td>
  </tr>
  <tr>
   <td>Avgränsare</td>
   <td>Gör att panelerna i formuläret kan delas upp visuellt.</td>
  </tr>
  <tr>
   <td>Signatursteg</td>
   <td>Visar informationen i formuläret och signaturfälten som användaren kan använda för att verifiera och signera formuläret.</td>
  </tr>
  <tr>
   <td>Text</td>
   <td>Gör att du kan ange statisk text.</td>
  </tr>
  <tr>
   <td>Skicka-knapp</td>
   <td>Lägger till en skicka-knapp för att skicka formuläret till den konfigurerade skicka-åtgärden.</td>
  </tr>
  <tr>
   <td>Sammanfattningssteg</td>
   <td>Skickar formuläret och visar en sammanfattning som författarna anger när formuläret har skickats. </td>
  </tr>
  <tr>
   <td>Byt</td>
   <td>Lägger till en växel som utför en åtgärd för att växla eller aktivera/inaktivera. Du kan inte lägga till fler än två alternativ i komponenten Switch. Eftersom en switch bara kan ha två värden: På eller av är obligatoriskt inte tillämpligt. Minst ett värde sparas oavsett användarens indata. <br /> </td>
  </tr>
  <tr>
   <td>Tabell</td>
   <td>Lägger till en tabell där du kan ordna data i rader och kolumner. </td>
  </tr>
  <tr>
   <td>Telefonnummer</td>
   <td><p>Lägger till ett fält för att hämta telefonnummer. Med telefonkomponenten kan författare konfigurera någon av följande telefonnummertyper. Varje typ är associerad med ett reguljärt standarduttryck för validering.</p>
    <ul>
     <li>Type International valideras av <code>^[+][0-9]{0,14}$</code>.</li>
     <li>Typen USPhoneNumber valideras av <code>{'+1 ('999') '999-9999}</code>.</li>
     <li>Typen UKPhoneNumber valideras av <code>text{'+'99 999 999 9999}</code>.</li>
     <li>Typen Anpassad innehåller inget standardvalideringsmönster. Den får värdet för den senast valda telefonnummertypen. Du kan också ange ett eget valideringsmönster.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Villkor<br /> </td>
   <td>Lägger till ett fält som författare kan använda för att ange villkoren som användare ska granska innan formuläret fylls i.</td>
  </tr>
  <tr>
   <td>Textruta </td>
   <td><p>Lägger till en textruta där en användare kan ange nödvändig information. </p> <p>Komponenten Textruta accepterar som standard bara oformaterad text. Du kan aktivera en textrutekomponent för att acceptera RTF. En RTF-aktiverad textkomponent innehåller alternativ för att lägga till rubriker, ändra teckenformat (fet, kursiv, stryka under tecknen), skapa sorterade och osorterade listor, ändra textbakgrund och textfärg samt lägga till hyperlänkar. Aktivera alternativet Tillåt RTF<strong> i komponentegenskaperna om du vill aktivera RTF-text för</strong> en textruta.</p> </td>
  </tr>
  <tr>
   <td>Titel</td>
   <td>Anger en rubrik för det adaptiva formuläret.</td>
  </tr>
  <tr>
   <td>Verifiera steg</td>
   <td><p>Lägger till en platshållare som visar det ifyllda formuläret för verifiering av användaren.</p> <p><strong>Obs</strong>:Adaptiv form som innehåller Verifiera-komponenten stöder inte anonyma användare. Du bör inte heller använda komponenten Verify i ett adaptivt formulärfragment.</p> </td>
  </tr>
 </tbody>
</table>

#### Bästa tillvägagångssätt vid arbete med komponenter {#best-practices}

Här följer några tips och viktiga saker att komma ihåg när du arbetar med adaptiva formulärkomponenter:

* Varje komponent har tillhörande egenskaper som styr dess utseende och funktion. Om du vill konfigurera egenskaperna för en komponent trycker du på komponenten och trycker på ![cmpr](assets/cmppr.png) för att öppna komponentegenskaperna i egenskapsläsaren.
* En komponent identifieras med sitt elementnamn. När du trycker på ![cmpr](assets/cmppr.png)kan du ändra komponentens namn genom att ändra fältvärdet för **[!UICONTROL elementnamnet]** i egenskapsläsaren. Endast bokstäver, siffror, bindestreck (-) och understreck (_) godkänns i fältet Elementnamn. Andra specialtecken tillåts inte och elementnamnet måste börja med en bokstav.

* Du kan ändra egenskapen Title för en adaptiv formulärkomponent infogad i formulärredigeraren utan att öppna egenskapsgranskaren så länge titeln visas i formuläret. Så här gör du:

   1. Tryck för att markera en komponent som har en **[!UICONTROL Title]** -egenskap och vars **[!UICONTROL Hide title]** -egenskap är inaktiverad.

   1. Tryck på ![aem_6_3_edit](assets/aem_6_3_edit.png) för att göra titeln redigerbar.

   1. Ändra titeln och tryck på Retur-tangenten eller var som helst utanför komponenten för att spara ändringarna. Tryck på Esc för att ignorera ändringarna.

* Vissa adaptiva formulärkomponenter som e-post och telefon innehåller färdiga valideringsmönster. Du kan dock ange anpassad validering genom att uppdatera fältet **[!UICONTROL Valideringsmönster]** under dragspelsfliken Mönster i komponentegenskaperna. Mer information om standardvalideringar finns i komponentbeskrivningarna i tabellen ovan.

* Anpassningsbara formulärfält, t.ex. Numerisk ruta och E-post, kan konfigureras så att de innehåller speciella HTML5-indatatyper. När de här fälten är i fokus på mobila enheter och surfplattor visas särskilda alfabet, siffror och tecken som är vanliga för inmatningsinformation i fälten. Det gör det lättare för användarna att ange information snabbt utan att behöva växla mellan teckenuppsättningar på knappsatsen. Om du vill tillåta specialiserade indata för en komponent aktiverar du kryssrutan **[!UICONTROL Använd HTML-typnummer]** i komponentegenskaperna.

* Du kan aktivera en textrutekomponent för att acceptera RTF. Om du vill aktivera RTF-text för en textruta markerar du kryssrutan **[!UICONTROL Tillåt RTF]** i komponentegenskaperna.

* Du kan aktivera komponenterna Textruta, E-post och Telefon för att autofylla värden för fält som namn, adress, kreditkort, telefon och e-post från informationen som lagras i webbläsarens autofyllningsinställningar. Om du vill aktivera den här funktionen väljer du **[!UICONTROL Aktivera automatisk ifyllning]** i komponentegenskaperna och väljer ett **[!UICONTROL autofyllningsattribut]**. När en användare fyller i ett anpassat formulär föreslås värdena från profilen för automatisk ifyllning i webbläsaren eller baserat på de värden som användaren tidigare fyllt i. Observera att Autofyll fungerar om autofyllningsinställningarna i användarens webbläsare är aktiverade.

* Ange värden för alternativknappar och kryssruteobjekt i `{value}={text}` format i komponentegenskaper.
* Komponenten för bifogad fil tillåter som standard att användaren bara kan bifoga en fil. Du kan dock konfigurera komponentegenskaperna så att de stöder flera bifogade filer. Om en användare dessutom bifogar flera filer med samma filnamn kan de bifogade filerna orsaka problem. Därför rekommenderar vi att du kopplar en unik identifierare till varje bifogad fil när formuläret skickas. Så här gör du:

   1. På din AEM Forms-server går du till **Adobe Experience Manager > Verktyg > Åtgärder > Webbkonsol**.
   1. Sök efter och tryck på **tjänsten** Adaptive Forms Configuration.
   1. Aktivera **Gör filnamn unika** i dialogrutan Adaptiv formulärkonfigurationstjänst. Som standard är den inaktiverad.

* Om du vill att användare ska kunna bifoga en PDF-fil med Safari-webbläsaren kontrollerar du att **application/pdf** har lagts till i egenskapen Filtyper som stöds i komponenten för bifogade filer. Anpassningsbara formulär som skapats med tidigare AEM Forms-version kan innehålla **.pdf** i stället för **application/pdf** i egenskapen Filtyper som stöds.

Mer information om adaptiva formulär finns i [Bästa tillvägagångssätt för att arbeta med adaptiva formulär](/help/forms/using/adaptive-forms-best-practices.md).

>[!NOTE]
>
>Anpassade formulärkomponenter har inte stöd för höger till vänster-språk. Till exempel hebreiska.

### Verktygsfältet Sida {#page-toolbar}

Verktygsfältet längst upp på sidan innehåller alternativ som gör att du kan förhandsgranska formuläret, ändra formuläregenskaper och redigera formulärlayouten. Du kan förhandsgranska formuläret när du redigerar det och göra ändringar i det. I verktygsfältet visas:

* **Växla panelen** Sida vid ![sida](assets/toggle-side-panel.png): Här kan du visa eller dölja sidofältet.

* **Sidinformation** ![temaalternativ](assets/theme-options.png): Gör att du kan visa sidegenskaper, publicera/avpublicera ett formulär, starta ett formulärarbetsflöde och öppna formuläret i klassiskt gränssnitt.

* **Emulatorns** ![linjal](assets/ruler.png): Gör att du kan emulera formulärutseendet för olika visningsstorlekar, till exempel surfplattor och telefoner.

* **Redigera**: Här kan du välja andra lägen, till exempel: **Redigera, Formatera, Utvecklare** och **Design**.

   * **Redigera**: Här kan du redigera egenskaperna för formuläret och dess komponenter. Du kan till exempel lägga till en komponent, släppa en bild och ange obligatoriska fält.
   * **Format**: Gör att du kan formatera utseendet på komponenter i formuläret. I stilläge kan du till exempel markera en panel och ange dess bakgrundsfärg.

   * **Utvecklare**: Låter en utvecklare:

      * Upptäck vad formulären består av.
      * Felsök vad som händer var och när, vilket i sin tur hjälper till att lösa problem.
   * **Design**.  Gör att du kan aktivera eller inaktivera anpassade komponenter eller komponenter som inte finns med i sidofältet.


* **Förhandsgranska**: Gör att du kan förhandsgranska hur formuläret ser ut när du publicerar det.

### Komponentverktygsfältet {#component-toolbar}

![Komponentverktygsfältet i pekrörelsegränssnittet](assets/component-toolbar.png)

När du markerar en komponent visas ett verktygsfält där du kan arbeta med den. Du får alternativ för att klippa ut, klistra in, flytta och ange egenskaper för komponenterna. Dina alternativ är:

A.**Konfigurera**: När du trycker på **Konfigurera** visas komponentegenskaperna i sidofältet. Om du konfigurerar dessa egenskaper kan du anpassa datainhämtningen. Du kan ändra komponentens elementnamn och ange etikettexten i komponentens rubrikfält. Med elementnamnet kan du hämta värden som användarna anger med komponenten. I komponentegenskaperna anger du komponentens beteende och hanterar användarindata. Konfigurera egenskaperna i sidofältet för att hämta användardata och använda dem för vidare bearbetning. Med egenskaper för adaptiv formulärbehållare kan du ange klientbibliotek, layouter, teman, inställningar för dokumentdokument, inställningar för att spara, inställningar för överföring och metadatainställningar.

B.**Copy**: Du kan använda kopieringsalternativet för att kopiera en komponent och klistra in den på andra platser i formuläret. När du klistrar in en komponent får den inklistrade komponenten ett nytt elementnamn men behåller den kopierade komponentens egenskaper.

C.**Cut**: Du kan använda alternativet Klipp ut för att flytta en komponent från en plats till en annan i det adaptiva formuläret.

D. **Ta bort**: Gör att du kan ta bort komponenten från formuläret.

E. **Infoga**: Gör att du kan infoga en komponent ovanför den markerade komponenten.

F. **Klistra in**: Gör att du kan klistra in komponenten som du klipper ut eller kopierar med alternativen som beskrivs ovan.

G. **Redigera regler**: Gör att du kan öppna regelredigeraren. Mer information finns i [Regelredigeraren](../../forms/using/rule-editor.md).

H. **Grupp**: Gör att du kan markera flera komponenter om du vill klippa ut, kopiera eller klistra in mer än en komponent tillsammans.

Jag. **Överordnad**: Gör att du kan välja en komponents överordnade. Ett textfält ligger till exempel i ett underavsnitt som finns i ett avsnitt. Avsnittet finns i stödlinjens rotpanel och den adaptiva formulärbehållaren är överordnad en stödlinjens rotpanel. För en komponent kan du se alla alternativ med hierarkin sorterad längst ned.

Om du till exempel trycker på **Överordnad** för en textruta ser du:

* Underavsnitt
* Avsnitt
* guideRootPanel
* Adaptiv formulärbehållare

J. **Övriga**: Innehåller fler alternativ för att arbeta med den markerade komponenten.

* Visa SOM-uttryck
* Spara en panel som fragment (endast för paneler)
* Lägg till underordnad panel (endast för paneler)
* Verktygsfältet Lägg till panel (endast för paneler)
* Ersätt (inte för paneler)

### Adaptiv formulärsida {#af-page}

Den anpassningsbara formulärsidan är det faktiska formuläret. Det är som alla andra WCM-sidor som modelleras som WCM- `cq:Page` komponent. Följande bild visar innehållsstrukturen i ett typiskt anpassat formulär.

![Innehållsstruktur för en WCM-sida med anpassat formulär](assets/afstructure.png)

Innehållsstrukturen innehåller vanligtvis följande primära komponenter:

* **guideContainer**: Roten i ett adaptivt formulär, som markeras som **Start av adaptivt formulär** i det adaptiva formulärgränssnittet. I den här komponenten kan du ange:

   * *Mobil layout för det adaptiva formuläret*: Definierar formulärets utseende på mobila enheter.
   * *Tack*! Definierar sidan där användaren omdirigeras efter att formuläret har skickats.
   * *Skicka åtgärd*: Definierar hur formuläret ska bearbetas på servern när användaren skickar formuläret.
   * *Format*: Anger sökvägen till CSS-filen som används för att anpassa formulärets utseende.

* **** rootPanel: Rotpanelen i ett adaptivt formulär. Den kan innehålla underpaneler under objektnoden. Varje panel, inklusive rotpanelen, kan ha en tillhörande layout. Panelens layout bestämmer hur formuläret placeras. I dragspelslayouten placeras till exempel objekten som dragspelssteg.

* **** verktygsfält: En adaptiv formulärbehållare har ett associerat globalt verktygsfält som är globalt för formuläret. Det här verktygsfältet kan läggas till med åtgärden **Lägg till verktygsfält** i redigeringsfältet, som gör att författare kan lägga till åtgärder som Skicka, Spara, Återställ och så vidare.

* **** resurser: Den här noden innehåller ytterligare information som används för formulärredigering. Exempel: formulärmodellinformation, lokaliseringsinformation osv.).

