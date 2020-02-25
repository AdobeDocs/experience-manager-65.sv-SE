---
title: Utveckla med CRXDE Lite
seo-title: Utveckla med CRXDE Lite
description: CRXDE Lite är inbäddat i AEM och gör att du kan utföra standardutvecklingsuppgifter i webbläsaren
seo-description: CRXDE Lite är inbäddat i AEM och gör att du kan utföra standardutvecklingsuppgifter i webbläsaren
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# Utveckla med CRXDE Lite{#developing-with-crxde-lite}

I det här avsnittet beskrivs hur du utvecklar ditt AEM-program med CRXDE Lite.

Mer information om olika utvecklingsmiljöer finns i översiktsdokumentationen.

CRXDE Lite är inbäddat i AEM och gör att du kan utföra standardutvecklingsuppgifter i webbläsaren. Med CRXDE Lite kan du skapa ett projekt, skapa och redigera filer (som .jsp och .java), mappar, mallar, komponenter, dialogrutor, noder, egenskaper och paket när du loggar och integrerar med SVN.
CRXDE Lite rekommenderas när du inte har direktåtkomst till AEM-servern, när du utvecklar ett program genom att utöka eller ändra körklara komponenter och Java-paket eller när du inte behöver en dedikerad felsökare, kodkomplettering och syntaxmarkering.

>[!NOTE]
>
>Som standard har alla AEM-användare åtkomst till CRXDE Lite. Om du vill kan du [konfigurera åtkomstkontrollistor](/help/sites-administering/security.md#permissions-and-acls) för följande nod så att bara utvecklare kan komma åt CRX DE Lite:
>
>`/libs/granite/crxde`

>[!NOTE]
>
>Vi rekommenderar att du använder [AEM Developer Tools för Eclipse](/help/sites-developing/aem-eclipse.md) och [AEM HTL Brackets Extension](/help/sites-developing/aem-brackets.md) under projektutvecklingen.

## Komma igång med CRXDE Lite {#getting-started-with-crxde-lite}

Så här kommer du igång med CRXDE Lite:

1. Installera AEM.
1. Skriv `https://<host>:<port>/crx/de`i webbläsaren. Som standard är det `https://localhost:4502/crx/de`.
1. Ange ditt **användarnamn** och **lösenord**. Som standard är det `admin` och `admin`.

1. Click **OK**.

CRXDE Lite-användargränssnittet ser ut så här i webbläsaren:

![chlimage_1-18](assets/chlimage_1-18.png)

Nu kan du använda CRXDE Lite för att utveckla programmet.

## Översikt över användargränssnittet {#overview-of-the-user-interface}

CRXDE Lite har följande funktioner:

<table>
 <tbody>
  <tr>
   <td>Övre växlingsfält</td>
   <td>Gör att du snabbt kan växla mellan CRXDE Lite, Package Manager och Package Share.</td>
  </tr>
  <tr>
   <td>Widgeten Nodbana</td>
   <td><p>Visar sökvägen till den markerade noden.</p> <p>Du kan också använda den för att hoppa till en nod, ange sökvägen manuellt eller klistra in den någon annanstans och trycka på Retur.</p> <p>Det finns även stöd för att söka efter noder med ett specifikt nodnamn. Ange namnet på noden som du vill söka efter och vänta (eller tryck på söksymbolen till höger). Du kan försöka att ange, t.ex., strängen <em>läses</em> in i widgeten för att se hur den fungerar. Om en viss nod eller noder läses in i utforskarrutan visas listan och du kan välja sökvägen och klicka på Retur för att navigera till den. Observera att det bara fungerar för de noder som för närvarande är inlästa i CRXDE-klientprogrammet i webbläsaren. Om du vill söka i hela databasen använder du Verktyg och sedan Fråga.</p> </td>
  </tr>
  <tr>
   <td>Utforskarfönster</td>
   <td><p>Visar ett träd med alla noder i databasen.</p> <p>Klicka på en nod för att visa dess egenskaper på fliken <strong>Egenskaper</strong> . När du har klickat på en nod kan du välja en åtgärd i verktygsfältet. Klicka på noden igen för att byta namn på den.</p> <p>Trädnavigeringsfilter (binokulär ikon): Med kan du filtrera noderna i databasen som namnet innehåller indatatexten för. Det gäller endast noder som har lästs in lokalt.<br /> </p> </td>
  </tr>
  <tr>
   <td>Redigeringsruta</td>
   <td><p><strong>Fliken Hem</strong> : Med kan du söka efter innehåll och/eller dokumentation och få tillgång till utvecklarresurser (dokumentation, utvecklarblogg, kunskapsbas) och support (Adobes hemsida och supportcenter).<br /> </p> <p>Dubbelklicka på en fil i <strong>Utforskaren</strong> för att visa dess innehåll. som till exempel en .jsp- eller .java-fil. Du kan sedan ändra den och spara ändringarna.</p> <p>När en fil har redigerats i <strong>redigeringsrutan</strong> är följande verktyg tillgängliga i verktygsfältet:<br /> </p> - <strong>Visa i träd: </strong>visar filen i databasträdet.<br /> - <strong>Sök/ersätt ...</strong>: sök och ersätt.<br /> <br /> Dubbelklicka på statusraden i <strong>rutan Redigera</strong> , så öppnas dialogrutan <strong>Gå till rad</strong> där du kan ange ett visst radnummer att gå till.<br /> </td>
  </tr>
  <tr>
   <td>Fliken Egenskaper<br /> </td>
   <td>Visar egenskaperna för den nod som du har valt. Du kan lägga till nya eller ta bort befintliga egenskaper.<br /> </td>
  </tr>
  <tr>
   <td>Fliken Åtkomstkontroll</td>
   <td><p>Visa behörigheter baserat på aktuell sökväg, databasnivå eller säkerhetsobjekt.</p> <p>Behörigheterna delas upp i</p> <p>- <strong>Tillämplig åtkomstkontrollprincip</strong>: De profiler som kan tillämpas på den aktuella markeringen.</p> <p>- <strong>Lokala åtkomstkontrollprinciper</strong>: De aktuella principer som tillämpas lokalt på den aktuella markeringen.</p> <p>- <strong>Effektiva åtkomstkontrollprinciper</strong>: De aktuella principer som används för den aktuella markeringen kan anges lokalt eller ärvs från överordnade noder.</p> <p>Obs! För att kunna se åtkomstkontrollsinformationen alls måste användaren som är inloggad på CRXDE Lite ha behörighet att läsa ACL-poster. Den anonyma användaren kan inte se den här informationen som standard - logga in som, t.ex., administratör för att se informationen.</p> </td>
  </tr>
  <tr>
   <td>Fliken Replikering</td>
   <td><p>Visa den aktuella nodens replikeringsstatus. Du kan replikera och replikera borttagningen av den aktuella noden.</p> </td>
  </tr>
  <tr>
   <td>Fliken Konsol<br /> </td>
   <td><p><strong>Serverloggar</strong>:</p> <p>Visar loggmeddelanden. Du kan konfigurera loggnivån, rensa konsolen, fästa vid den valda rullningspositionen och aktivera/inaktivera visning av meddelanden.<br /> </p> <p><strong>Versionskontroll</strong>:</p> <p>Visar versionskontrollmeddelanden.<br /> </p> </td>
  </tr>
  <tr>
   <td>Fliken Bygginformation<br /> </td>
   <td>Visar information när ett paket byggs.<br /> </td>
  </tr>
  <tr>
   <td>Uppdatera<br /> </td>
   <td>Uppdaterar den aktuella markeringen. Ändringar från andra användare uppdateras i din vy av databasen. De ändringar du har gjort påverkas inte.<br /> </td>
  </tr>
  <tr>
   <td>Spara alla</td>
   <td><p><strong>Spara alla</strong>:<br /> </p> <p>Sparar alla ändringar du har gjort. Tills du klickar på Spara är ändringarna temporära och försvinner när du avslutar konsolen.</p> <p><strong>Återställ</strong>:</p> <p>Ignorerar alla ändringar som du har gjort på den valda noden sedan den senaste sparaåtgärden och läser sedan in databasens aktuella status för den valda noden igen.</p> <p><strong>Återställ alla</strong>:</p> <p>Ignorerar alla ändringar som du har gjort i hela databasen sedan den senaste sparåtgärden och läser sedan in databasens aktuella läge igen.</p> </td>
  </tr>
  <tr>
   <td>Skapa ...<br /> </td>
   <td><p>Listruta för att skapa följande under den valda noden:<br /> </p> <p>- <strong>Nod</strong>: en nod med en godtycklig nodtyp<br /> </p> <p>- <strong>Fil</strong>: nt:filnod och dess nt:resursundernod</p> <p>- <strong>Mapp</strong>: nt:mappnod</p> <p>- <strong>Mall</strong>: AEM-mall</p> <p>- <strong>Komponent</strong>: AEM-komponent</p> <p>- <strong>Dialog</strong>: AEM-dialogruta</p> </td>
  </tr>
  <tr>
   <td>Ta bort<br /> </td>
   <td>Tar bort den markerade noden.<br /> </td>
  </tr>
  <tr>
   <td>Kopiera</td>
   <td>Kopierar den markerade noden.<br /> </td>
  </tr>
  <tr>
   <td>Klistra in<br /> </td>
   <td>Klistrar in den kopierade noden under den markerade noden.<br /> </td>
  </tr>
  <tr>
   <td>Flytta ...<br /> </td>
   <td>Flyttar den markerade noden till den nod som anges i dialogrutan.</td>
  </tr>
  <tr>
   <td>Byt namn på ...<br /> </td>
   <td>Byter namn på den markerade noden.<br /> </td>
  </tr>
  <tr>
   <td>Blandningar ...<br /> </td>
   <td>Gör att du kan lägga till blandningstyper i nodtypen. Blandningstyperna används oftast för att lägga till avancerade funktioner som versionshantering, åtkomstkontroll, referenser och låsning till noden.</td>
  </tr>
  <tr>
   <td>Team<br /> </td>
   <td><p>Listruta där du utför vanliga versionskontrolluppgifter:</p> <p>- <strong>Uppdatera</strong> databasen från SVN-servern</p> <p>- <strong>Genomför</strong> lokala ändringar av SVN-servern</p> <p>- Visa <strong>status</strong> för aktuell nod</p> <p>- Visa <strong>rekursiv status</strong> för den aktuella nodens underträd</p> <p>- <strong>Checka</strong> ut en arbetskopia från SVN-servern</p> <p>- <strong>Exportera</strong> ett projekt från SVN-servern (utan att skapa en arbetskopia)</p> <p>- <strong>Importera</strong> ett projekt från databasen till SVN-servern<br /> </p> <p>Observera att du måste vara inloggad som användare med tillräcklig behörighet för att kunna utföra vissa av uppgifterna (särskilt de som skriver till den lokala databasen).<br /> </p> </td>
  </tr>
  <tr>
   <td>Verktyg<br /> </td>
   <td><p>Listruta med följande verktyg:</p> <p>- <strong>Serverkonfiguration ...</strong>: för åtkomst till Felix Console.</p> <p>- <strong>Fråga ...</strong>: för att fråga databasen.</p> <p>- <strong>Behörigheter ...</strong>: för att öppna behörighetshantering, där du kan visa och lägga till behörigheter.</p> <p>- <strong>Testa åtkomstkontroll ...</strong>: en plats där du kan testa behörigheten för en viss sökväg och/eller huvudman.</p> <p>- <strong>Exportera nodtyp</strong>: om du vill exportera nodtyper i systemet som slutnotation.</p> <p>- <strong>Importera nodtyp ...</strong>: om du vill importera nodtyper med hjälp av slutnotation.</p> <p>- <strong>Installera SiteCatalyst-felsökaren ...</strong>: anvisningar om hur du installerar Analytics Debugger.</p> </td>
  </tr>
  <tr>
   <td>Inloggningswidget<br /> </td>
   <td><p>Visar de inloggade användarna och arbetsytan de är inloggade på, t.ex. admin@crx.default.</p> <p>Klicka på den för att logga in eller logga in igen som en specifik användare. Om du inte anger en arbetsyta att logga in på loggas du in på standardarbetsytan, crx.default.</p> <p>Om du vill bläddra i databasen som anonym användare använder du <strong>anonym</strong> som inloggningsnamn och eventuellt lösenord (t.ex. blanksteg eller punkt).<br /> </p> <p>Om din auktorisering inte längre är giltig (t.ex. har upphört att gälla) visas "<strong>Obehörig - inloggning...</strong>" i inloggningswidgeten. Klicka på den för att logga in igen.</p> </td>
  </tr>
 </tbody>
</table>

## Skapa ett projekt {#creating-a-project}

Med CRXDE Lite kan du skapa ett projekt med tre klick. I projektguiden skapas ett nytt projekt under `/apps`, en del innehåll under `/conten`det och ett paket där allt innehåll under `/etc/packages`. Projektet kan användas direkt för att återge en exempelsida med **Hello World**, baserat på ett jsp-skript som återger en egenskap från databasen och anropar en Java-klass för att återge text.

Så här skapar du ett projekt med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. **Högerklicka på en nod i navigeringsrutan, välj** Skapa ...**och sedan**Skapa projekt ... .
Obs! Du kan högerklicka på valfri nod i trädnavigeringen, som de nya projektnoderna är, enligt design, skapade nedan `/apps,` och `/content` `/etc/packages`.

1. Definiera:

   * **Projektnamn** - projektnamnet används för att skapa nya noder och paketet, t.ex. `myproject`.

   * **Java Package** - Java-paketets namnprefix, t.ex. `com.mycompany`.

1. Klicka på **Skapa**.
1. Klicka på **Spara alla** för att spara ändringarna på servern.

Om du vill komma åt exempelsidan med **Hello World** pekar du i webbläsaren på:

`https://localhost:4502/content/<project-name>.html`

Sidan **Hello World** baseras på en innehållsnod som anropar ett jsp-skript via `sling:resourceType` egenskapen. Skriptet läser `jcr:title` egenskapen från databasen och hämtar brödtextinnehållet genom att anropa en metod i klassen SampleUtil, som är tillgänglig i projektpaketet.

Följande noder skapas:

* `/apps/<project-name>`: programbehållaren.
* `/apps/<project-name>/components`: komponentbehållaren, som innehåller exemplet html.jsp-fil, som används för att återge en sida.

* `/apps/<project-name>/src`: paketbehållaren, som innehåller ett exempelprojektpaket.

* `/apps/<project-name>/install`: den kompilerade paketbehållaren, som innehåller det kompilerade exempelprojektpaketet.
* `/content/<project-name>`: innehållsbehållaren.
* /etc/packages/&lt;java-suffix>/&lt;project-name>.zip, ett paket som innehåller allt projektprogram och allt innehåll. Du kan använda det för att återskapa projektet för vidare distribution (till exempel till andra miljöer) eller för delning via paketdelning.

Strukturen ser ut så här i CRXDE Lite med ett projekt som kallas **myproject** och ett java-paketsuffix som kallas **mycompany**:

![chlimage_1-19](assets/chlimage_1-19.png)

![chlimage_1-20](assets/chlimage_1-20.png)

## Skapa en mapp {#creating-a-folder}

Så här skapar du en mapp med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. **I navigeringsrutan högerklickar du på den mapp som du vill skapa den nya mappen i, väljer** Skapa ...**och sedan** Skapa mapp ... .

1. Ange mappens **namn** och klicka på **OK**.

1. Klicka på **Spara alla** för att spara ändringarna på servern.

## Creating a Template {#creating-a-template}

Så här skapar du en mall med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. **I navigeringsrutan högerklickar du på den mapp där du vill skapa mallen, väljer** Skapa ...**och sedan** Skapa mall ... .

1. Ange mallens **etikett**, **titel**, **beskrivning**, **resurstyp** och **rankning** . Click **Next**.

1. Det här steget är valfritt: Ange **tillåtna banor**. Click **Next**

1. Det här steget är valfritt: Ange **tillåtna överordnade**. Click **Next**.

1. Det här steget är valfritt: Ange **Tillåtna underordnade**. Click **OK**.

1. Klicka på **Spara alla** för att spara ändringarna på servern.

Det skapar:

* En nod av typen `cq:Template` med mallegenskaper

* En underordnad nod av typen `cq:PageContent` med sidinnehållsegenskaper

Du kan lägga till egenskaper i mallen: Se avsnittet [Skapa en egenskap](#creating-a-property) .

## Skapa en komponent {#creating-a-component}

Funktionen som beskrivs här är bara tillgänglig om CQ5 är installerat, det vill säga om nodtypen `cq:Component` är tillgänglig i databasen.

Så här skapar du en komponent med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. **I navigeringsrutan högerklickar du på den mapp där du vill skapa komponenten, väljer** Skapa ...**och sedan** Skapa komponent ... .

1. Ange komponentens **etikett**, **titel**, **beskrivning**, **superresurstyp** och **grupp** . Click **Next**.

1. Det här steget är valfritt: Ange komponentegenskaperna **Behållare,** **Ingen dekoration**, **Cellnamn** och **Dialogrutesökväg**. Click **Next**.

1. Det här steget är valfritt: Ange egenskapen **Tillåtna överordnade komponenter**. Click **Next**.

1. Det här steget är valfritt: Ange egenskapen **Allowed Children**. Click **OK**.

1. Klicka på **Spara alla** för att spara ändringarna på servern.

Det skapar:

* En nod av typen `cq:Component`
* Komponentegenskaper
* Ett .jsp-komponentskript

## Skapa en dialogruta {#creating-a-dialog}

Så här skapar du en dialogruta med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. **I navigeringsrutan högerklickar du på den komponent där du vill skapa dialogrutan, väljer** Skapa ...**och sedan** Skapa dialogruta ... .

1. Ange **etiketten** och **titeln**. Click **OK**.

1. Klicka på **Spara** alla för att spara ändringarna på servern.

En dialogruta med följande struktur skapas:

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

Nu kan du anpassa dialogrutan efter dina behov genom att ändra egenskaper eller skapa nya noder.

Du kan också använda Dialogruteredigeraren för att redigera en dialogruta. Om du dubbelklickar på dialognoden i CRXDE Lite öppnas redigeraren. Mer information om Dialog Editor finns [här](/help/sites-developing/dialog-editor.md).

## Skapa en nod {#creating-a-node}

Så här skapar du en nod med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. **I navigeringsrutan högerklickar du på den nod där du vill skapa den nya noden, väljer** Skapa ...**och sedan** Skapa nod ... .
1. Ange **namn** och **typ**. Click **OK**.
1. Klicka på **Spara alla** för att spara ändringarna på servern.

Nu kan du anpassa noden efter dina behov genom att ändra egenskaper eller skapa nya noder.

>[!NOTE]
>
>De flesta redigeringsåtgärderna, inklusive Skapa nod, sparar alla ändringar i minnet och lagrar dem bara i databasen när de sparas (med knappen &quot;Spara alla&quot;). Vissa åtgärder, till exempel move, sparas dock automatiskt.
>
>Valideringen av om den nyskapade noden tillåts av den överordnade nodens nodtyp utförs också av JCR-databasen först när ändringarna sparas. Om du får ett felmeddelande när du sparar en nod kontrollerar du om innehållsstrukturen är giltig (du kan t.ex. inte skapa en `nt:unstructured` nod som underordnad `nt:folder` nod).

## Skapa en egenskap {#creating-a-property}

Så här skapar du en egenskap med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I navigeringsrutan markerar du den nod där du vill lägga till den nya egenskapen.
1. På fliken **Egenskaper** i den nedre rutan anger du **Namn**, **Typ** och **Värde**. Click **Add**.

1. Klicka på **Spara alla** för att spara ändringarna på servern.

## Skapa ett skript {#creating-a-script}

Så här skapar du ett nytt skript:

1. Öppna CRXDE Lite i webbläsaren.
1. **I navigeringsrutan högerklickar du på den komponent där du vill skapa skriptet, väljer** Skapa ...**och sedan** Skapa fil ... .

1. Ange **filnamnet** inklusive filnamnstillägget. Click **OK**.

1. Den nya filen öppnas som en flik i rutan Redigera.
1. Redigera filen.
1. Klicka på **Spara alla** för att spara ändringarna.

## Hantera ett paket {#managing-a-bundle}

Med CRXDE Lite är det enkelt att skapa ett OSGI-paket, lägga till Java-klasser och bygga det. Paketet installeras sedan automatiskt och startas i OSGI-behållaren.

I det här avsnittet beskrivs hur du skapar ett `Test` paket med en `HelloWorld` Java-klass som visar **Hello World!** i webbläsaren när resursen begärs.

### Skapa ett paket {#creating-a-bundle}

Så här skapar du testpaketet med CRXDE Lite:

1. I CRXDE Lite skapar du `myapp` projekt med [projektguiden](#creating-a-project). Bland annat skapas följande noder:

   * `/apps/myapp/src`
   * `/apps/myapp/install`

1. `/apps/myapp/src`Högerklicka på mappen `Test` som ska innehålla **paketet, välj** Skapa ...**och sedan** Skapa paket ... .

1. Ange paketegenskaperna enligt följande:

   * Namn på symbolpaket: `com.mycompany.test.TestBundle`

   * Paketnamn: `Test Bundle`
   * Paketbeskrivning:

      ```
      This is my Test Bundle
      ```

   * Paket:

      ```
      com.mycompany.test
      ```
   Click **OK**.

1. Klicka på **Spara alla** för att spara ändringarna på servern.

Guiden skapar följande element:

* Noden `com.mycompany.test.TestBundle` av typen `nt:folder.` Det är paketbehållarnoden.

* Filen `com.mycompany.test.TestBundle.bnd`. Det fungerar som distributionsbeskrivare för ditt paket och består av en uppsättning rubriker.

* Mappstrukturerna:

   * `src/main/java/com/mycompany/test`. Den innehåller paketen och Java-klasserna.

   * `src/main/resources`. Den innehåller de resurser som används i paketet.

* The `Activator.java` file. Det är den valfria avlyssnarklassen som ska meddelas om start- och stopphändelser för paket.

I följande tabell visas alla egenskaper i Bnd-filen, deras värden och beskrivningar:

<table>
 <tbody>
  <tr>
   <td><strong>Egenskap</strong></td>
   <td><strong>Värde (när paket skapas)<br /> </strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>Exportera paket:</td>
   <td><p>*</p> <p>Obs! Detta värde måste anpassas för att återspegla paketets särart.</p> </td>
   <td>Rubriken Exportera paket definierar exporterade paket från paketet (kommaseparerade paketlistor). De exporterade paketen utgör den offentliga<br /> vyn av paketet.<br /> </td>
  </tr>
  <tr>
   <td>Import-paket:</td>
   <td><p>*</p> <p>Obs! Detta värde måste anpassas för att återspegla paketets särart.</p> </td>
   <td>Huvudet Importera paket definierar importerade paket för paketet (kommaavgränsad lista med paket)</td>
  </tr>
  <tr>
   <td>Privat paket:</td>
   <td><p>*</p> <p>Obs! Detta värde måste anpassas för att återspegla paketets särart.</p> </td>
   <td>Huvudet Privat paket definierar privata paket för paketet (kommaseparerade paketlistor). De privata paketen utgör den interna implementeringen.<br /> </td>
  </tr>
  <tr>
   <td>Paketnamn:</td>
   <td>Test Bundle</td>
   <td>Definierar ett kort, läsbart namn för paketet</td>
  </tr>
  <tr>
   <td>Paket - beskrivning:</td>
   <td>Det här är mitt testpaket</td>
   <td>Definierar en kort, läsbar beskrivning av paketet</td>
  </tr>
  <tr>
   <td>Bundle-SymbolicName:</td>
   <td>com.mycompany.test.TestBundle</td>
   <td>Anger ett unikt, icke-lokaliserbart namn för paketet</td>
  </tr>
  <tr>
   <td>Bundle-Version:</td>
   <td>1.0.0-ÖGONBLICKSBILD</td>
   <td>Anger paketets version</td>
  </tr>
  <tr>
   <td>Bundle-Activator:</td>
   <td>com.mincompany.test.Activator</td>
   <td>Anger namnet på den valfria avlyssnarklassen som ska meddelas om start- och stopphändelser för paket</td>
  </tr>
 </tbody>
</table>

Mer information om bend-formatet finns i [bnd utility](https://bndtools.org/) som används av CRXDE för att skapa OSGI-paket.

### Skapa en Java-klass {#creating-a-java-class}

Så här skapar du `HelloWorld` Java-klassen i Test Bundle:

1. Öppna CRXDE Lite i webbläsaren.
1. `Activator.java`I navigeringsrutan högerklickar du på noden som innehåller `/apps/myapp/src/com.mycompany.test.TestBundle/src/main/java` filen ( **), väljer** Skapa ...**och sedan** Skapa fil ... .

1. Ge filen ett namn `HelloWorld.java`. Click **OK**.

1. Filen öppnas i `HelloWorld.java` rutan Redigera.
1. Lägg till följande rader i `HelloWorld.java`:

    ```
      package com.mycompany.test;

      public class HelloWorld {
      public String getString(){
      return "Hello World!";
      }
      }
    ```

1. Klicka på **Spara alla** för att spara ändringarna på servern.

### Bygga ett paket {#building-a-bundle}

Så här skapar du testpaketet:

1. Öppna CRXDE Lite i webbläsaren.
1. Högerklicka på Bnd-filen i navigeringsrutan, välj **Verktyg** och sedan **Bundle**.

Guiden Build Bundle:

* Kompilerar Java-klasserna.
* Skapar .jar-filen som innehåller de kompilerade Java-klasserna och resurserna och placerar den i `myapp/install` mappen.
* Installerar och startar paketet i OSGI-behållaren.

Om du vill se effekten av testpaketet skapar du en komponent som använder Java-metoden HelloWorld.getString() och en resurs som återges av den här komponenten:

1. Skapa komponenten `mycomp` under `myapp/components`.

1. Redigera `mycomp.jsp` och ersätt koden med följande rader:

   ```
     <%@ page import="com.mycompany.test.HelloWorld"%><%
     %><%@ include file="/libs/foundation/global.jsp"%><%
     %><% HelloWorld hello = new HelloWorld();%><%
     %>
     <html>
     <body>
     <b><%= hello.getString() %></b><br>
     </body>
     </html>
   ```

1. Skapa resursen `test_node` av typen `nt:unstructured` under `/content`.

1. Skapa `test_node`följande egenskap: Namn = `sling:resourceType`, Typ = `String`, Värde = `myapp/components/mycomp`.

1. Klicka på **Spara alla** för att spara ändringarna på servern.

1. Begär `test_node`följande i webbläsaren: `https://<hostname>:<port>/content/test_node.html`.

1. En sida visas med **Hello World!** message.

## Exportera och importera nodtyper {#exporting-and-importing-node-types}

Med CRXDE Lite kan du importera och/eller exportera nodtypsdefinitioner i [CND-notation](https://jackrabbit.apache.org/jcr/node-type-notation.html)(Compact Namespace and Node Type Definition).

Så här exporterar du en nodtypsdefinition:

1. Öppna CRXDE Lite i webbläsaren.
1. Välj önskad nod.
1. Välj **Verktyg** och sedan **Exportera nodtyp**.

1. Definitionen visas i syntaxen i webbläsaren. Spara informationen om det behövs.

Så här importerar du en nodtypsdefinition:

1. Öppna CRXDE Lite i webbläsaren.
1. **Välj** Verktyg **och sedan** Importera nodtyp... .

1. Ange CND-notation för definitionen i textrutan.
1. Markera **Tillåt uppdatering** om du uppdaterar en befintlig definition.
1. Klicka på **Importera**.

## Loggning {#logging}

Med CRXDE Lite kan du visa filen `error.log` som finns i filsystemet på `<crx-install-dir>/crx-quickstart/server/logs` och filtrera den med rätt loggnivå. Gör så här:

1. Öppna CRXDE Lite i webbläsaren.
1. På fliken **Konsol** längst ned i fönstret väljer du **Serverloggar** i listrutan till höger.

1. Klicka på ikonen **Stopp** för att visa meddelandena.

Du kan:

* Justera loggparametrarna i Felix Console genom att klicka på ikonen **Loggningskonfigurationer** .
* Rensa meddelandena genom att klicka på **penselikonen** .
* Fäst meddelandet vid den aktuella markeringen genom att klicka på ikonen **Fäst** .
* Aktivera eller inaktivera visningen av meddelanden genom att klicka på **stoppikonen** .

## Åtkomstkontroll {#access-control}

>[!NOTE]
>
>Mer information finns i Administrera [användare, grupper och åtkomsträttigheter](/help/sites-administering/user-group-ac-admin.md) .
