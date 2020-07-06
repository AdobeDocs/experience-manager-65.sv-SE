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
source-git-commit: cb141914428f42a9755b5479ab1652c8ca51f640
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 0%

---


# Utveckla med CRXDE Lite{#developing-with-crxde-lite}

I det här avsnittet beskrivs hur du utvecklar ditt AEM-program med CRXDE Lite.

Mer information om olika utvecklingsmiljöer finns i översiktsdokumentationen.

CRXDE Lite är inbäddat i AEM och gör att du kan utföra standardutvecklingsuppgifter i webbläsaren. Med CRXDE Lite kan du skapa ett projekt, skapa och redigera filer (som .jsp och .java), mappar, mallar, komponenter, dialogrutor, noder, egenskaper och paket när du loggar.
CRXDE Lite rekommenderas när du inte har direktåtkomst till AEM-servern, när du utvecklar ett program genom att utöka eller ändra körklara komponenter och Java-paket eller när du inte behöver en dedikerad felsökare, kodkomplettering och syntaxmarkering.

>[!NOTE]
>
>Från och med AEM 6.5.5.0 är anonym åtkomst av CRXDE Lite inte längre möjlig.
>Användarna dirigeras om till inloggningsskärmen.


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

![chlimage_1-18](assets/crx-interface.jpg)

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
   <td><p><strong>Fliken Hem</strong> : Med kan du söka efter innehåll och/eller dokumentation och få tillgång till utvecklarresurser (dokumentation, utvecklarblogg, kunskapsbas) och support (Adobes hemsida och supportcenter).<br /> </p> <p>Dubbelklicka på en fil i <strong>Utforskaren</strong> för att visa dess innehåll. som till exempel en .jsp- eller .java-fil. Du kan sedan ändra den och spara ändringarna.</p> <p>När en fil har redigerats i <strong>redigeringsrutan</strong> är följande verktyg tillgängliga i verktygsfältet:<br /> </p> - <strong>Visa i träd: </strong>visar filen i databasträdet.<br /> - <strong>Sök/ersätt ...</strong>: sök och ersätt.<br /> <br /> Om du dubbelklickar på statusraden i <strong>rutan Redigera</strong> öppnas dialogrutan <strong>Gå till rad</strong> så att du kan ange ett visst radnummer att gå till.<br /> </td>
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
   <td>Verktyg<br /> </td>
   <td><p>Listruta med följande verktyg:</p> <p>- <strong>Serverkonfiguration ...</strong>: för åtkomst till Felix Console.</p> <p>- <strong>Fråga ...</strong>: för att fråga databasen.</p> <p>- <strong>Behörigheter ...</strong>: för att öppna behörighetshantering, där du kan visa och lägga till behörigheter.</p> <p>- <strong>Testa åtkomstkontroll ...</strong>: en plats där du kan testa behörigheten för en viss sökväg och/eller huvudman.</p> <p>- <strong>Exportera nodtyp</strong>: om du vill exportera nodtyper i systemet som slutnotation.</p> <p>- <strong>Importera nodtyp ...</strong>: om du vill importera nodtyper med hjälp av slutnotation.</p> <p>- <strong>Installera SiteCatalyst-felsökaren ...</strong>: anvisningar om hur du installerar Analytics Debugger.</p> </td>
  </tr>
  <tr>
   <td>Inloggningswidget<br /> </td>
   <td><p>Visar de inloggade användarna och arbetsytan de är inloggade på, t.ex. admin@crx.default.</p> <p>Klicka på den för att logga in eller logga in igen som en specifik användare. Om du inte anger en arbetsyta att logga in på loggas du in på standardarbetsytan, crx.default.</p> <p>Om du vill bläddra i databasen som anonym användare använder du <strong>anonym</strong> som inloggningsnamn och eventuellt lösenord (t.ex. blanksteg eller punkt).<br /> </p> <p>Om din auktorisering inte längre är giltig (t.ex. har upphört att gälla) visas "<strong>Obehörig - inloggning...</strong>" i inloggningswidgeten. Klicka på den för att logga in igen.</p> </td>
  </tr>
 </tbody>
</table>

## Skapa en mapp {#creating-a-folder}

Så här skapar du en mapp med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I navigeringsrutan högerklickar du på den mapp som du vill skapa den nya mappen i, väljer **Skapa ...** och sedan **Skapa mapp ...**.

1. Ange mappens **namn** och klicka på **OK**.

1. Klicka på **Spara alla** för att spara ändringarna på servern.

## Creating a Template {#creating-a-template}

Så här skapar du en mall med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I navigeringsrutan högerklickar du på den mapp där du vill skapa mallen, väljer **Skapa ...** och sedan **Skapa mall ...**.

1. Ange mallens **etikett**, **titel**, **beskrivning**, **resurstyp** och **rankning** . Klicka på **Nästa**.

1. Det här steget är valfritt: Ange **tillåtna banor**. Klicka på **Nästa**

1. Det här steget är valfritt: Ange **tillåtna överordnade**. Klicka på **Nästa**.

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
1. I navigeringsrutan högerklickar du på den mapp där du vill skapa komponenten, väljer **Skapa ...** och sedan **Skapa komponent ...**.

1. Ange komponentens **etikett**, **titel**, **beskrivning**, **superresurstyp** och **grupp** . Klicka på **Nästa**.

1. Det här steget är valfritt: Ange komponentegenskaperna **Behållare,** **Ingen dekoration**, **Cellnamn** och **Dialogrutesökväg**. Klicka på **Nästa**.

1. Det här steget är valfritt: Ange egenskapen **Tillåtna överordnade komponenter**. Klicka på **Nästa**.

1. Det här steget är valfritt: Ange egenskapen **Allowed Children**. Click **OK**.

1. Klicka på **Spara alla** för att spara ändringarna på servern.

Det skapar:

* En nod av typen `cq:Component`
* Komponentegenskaper
* Ett .jsp-komponentskript

## Skapa en dialogruta {#creating-a-dialog}

Så här skapar du en dialogruta med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I navigeringsrutan högerklickar du på den komponent där du vill skapa dialogrutan, väljer **Skapa ...** och sedan **Skapa dialogruta ...**.

1. Ange **etiketten** och **titeln**. Click **OK**.

1. Klicka på **Spara** alla för att spara ändringarna på servern.

En dialogruta med följande struktur skapas:

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

Nu kan du anpassa dialogrutan efter dina behov genom att ändra egenskaper eller skapa nya noder.

Du kan också använda Dialogruteredigeraren för att redigera en dialogruta. Om du dubbelklickar på dialognoden i CRXDE Lite öppnas redigeraren. Mer information om Dialog Editor finns [här](/help/sites-developing/dialog-editor.md).

## Skapa en nod {#creating-a-node}

Så här skapar du en nod med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I navigeringsrutan högerklickar du på den nod där du vill skapa den nya noden, väljer **Skapa ...** och sedan **Skapa nod ...**.
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
1. I navigeringsrutan högerklickar du på den komponent där du vill skapa skriptet, väljer **Skapa ...** och sedan **Skapa fil ...**.

1. Ange **filnamnet** inklusive filnamnstillägget. Click **OK**.

1. Den nya filen öppnas som en flik i rutan Redigera.
1. Redigera filen.
1. Klicka på **Spara alla** för att spara ändringarna.

## Exportera och importera nodtyper {#exporting-and-importing-node-types}

Med CRXDE Lite kan du importera och/eller exportera nodtypsdefinitioner i [CND-notation](https://jackrabbit.apache.org/jcr/node-type-notation.html)(Compact Namespace and Node Type Definition).

Så här exporterar du en nodtypsdefinition:

1. Öppna CRXDE Lite i webbläsaren.
1. Välj önskad nod.
1. Välj **Verktyg** och sedan **Exportera nodtyp**.

1. Definitionen visas i syntaxen i webbläsaren. Spara informationen om det behövs.

Så här importerar du en nodtypsdefinition:

1. Öppna CRXDE Lite i webbläsaren.
1. Välj **Verktyg** och sedan **Importera nodtyp...**.

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
