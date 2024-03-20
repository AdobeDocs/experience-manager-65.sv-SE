---
title: Utveckla med CRXDE Lite
description: CRXDE Lite är inbäddat i Adobe Experience Manager (AEM) och gör att du kan utföra standardutvecklingsuppgifter i webbläsaren
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
docset: aem65
exl-id: 9e88ca55-ac3d-4857-b6b2-aeb732562664
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2118'
ht-degree: 0%

---

# Utveckla med CRXDE Lite{#developing-with-crxde-lite}

I det här avsnittet beskrivs hur du utvecklar ditt Adobe Experience Manager-program (AEM) med CRXDE Lite.

Mer information om olika utvecklingsmiljöer finns i översiktsdokumentationen.

CRXDE Lite är inbäddat i AEM och gör att du kan utföra standardutvecklingsuppgifter i webbläsaren. Med CRXDE Lite kan du skapa ett projekt, skapa och redigera filer (som .jsp och .java), mappar, mallar, komponenter, dialogrutor, noder, egenskaper och paket när du loggar.
CRXDE Lite rekommenderas när du inte har direktåtkomst till AEM. Eller när du utvecklar ett program genom att utöka eller ändra körklara komponenter och Java™-paket, eller när du inte behöver en dedikerad felsökare, kodkomplettering och syntaxmarkering.

>[!NOTE]
>
>Från och med AEM 6.5.5.0 är anonym tillgång för CRXDE Lite inte längre möjlig.
>Användarna dirigeras om till inloggningsskärmen.


>[!NOTE]
>
>Adobe rekommenderar att du använder [AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md) och [Tillägget AEM HTML-parenteser](/help/sites-developing/aem-brackets.md) under projektutvecklingen.

## Komma igång med CRXDE Lite {#getting-started-with-crxde-lite}

Så här kommer du igång med CRXDE Lite:

1. Installera AEM.
1. I webbläsaren anger du `https://<host>:<port>/crx/de`. Som standard är det `https://localhost:4502/crx/de`.
1. Ange **användarnamn** och **lösenord**. Som standard är det `admin` och `admin`.

1. Klicka **OK**.

Användargränssnittet CRXDE Lite ser ut så här i webbläsaren:

![chlimage_1-18](assets/crx-interface.jpg)

Nu kan du använda CRXDE Lite för att utveckla programmet.

## Översikt över användargränssnittet {#overview-of-the-user-interface}

CRXDE Lite har följande funktioner:

<table>
 <tbody>
  <tr>
   <td>Övre växlingsfält</td>
   <td>Växla snabbt mellan CRXDE Lite, Package Manager och Package Share.</td>
  </tr>
  <tr>
   <td>Widgeten Nodbana</td>
   <td><p>Visar sökvägen till den markerade noden.</p> <p>Du kan också använda den för att hoppa till en nod, ange sökvägen manuellt eller klistra in den någon annanstans och trycka på Retur.</p> <p>Den har även stöd för att söka efter noder med ett specifikt nodnamn. Ange namnet på noden som du vill söka efter och vänta (eller tryck på söksymbolen till höger). Du kan försöka att ange strängen, till exempel <em>oak</em> i widgeten för att se hur den fungerar. Om en viss nod eller noder läses in i utforskarrutan visas listan och du kan välja sökvägen och trycka på Retur för att navigera till den. Det fungerar bara för noder som läses in i CRXDE-klientprogrammet i webbläsaren. Om du vill söka i hela databasen använder du Verktyg och sedan Fråga.</p> </td>
  </tr>
  <tr>
   <td>Utforskarfönster</td>
   <td><p>Visar ett träd med alla noder i databasen.</p> <p>Klicka på en nod så att du kan visa dess egenskaper i <strong>Egenskaper</strong> -fliken. När du har klickat på en nod kan du välja en åtgärd i verktygsfältet. Klicka på noden igen för att byta namn på den.</p> <p>Trädnavigeringsfilter (binokulär ikon): gör att du kan filtrera noderna i databasen som namnet innehåller indatatexten för. Det gäller endast noder som har lästs in lokalt.<br /> </p> </td>
  </tr>
  <tr>
   <td>Redigeringsruta</td>
   <td><p><strong>Startsida</strong> -fliken: gör att du kan söka efter innehåll och/eller dokumentation och komma åt utvecklarresurser (dokumentation, utvecklarblogg, kunskapsbas) och support (Adobe hemsida och supportcenter).<br /> </p> <p>Dubbelklicka på en fil i <strong>Explorer</strong> så att du kan visa dess innehåll. Exempel: en .jsp- eller .java-fil. Du kan sedan ändra den och spara ändringarna.</p> <p>När en fil har redigerats i <strong>Redigera</strong> finns följande verktyg i verktygsfältet:<br /> </p> - <strong>Visa i träd: </strong>visar filen i databasträdet.<br /> - <strong>Sök/ersätt ...</strong>: gör sök eller ersätt.<br /> <br /> Dubbelklicka på statusraden i <strong>Redigera</strong> öppnar fönstret <strong>Gå till rad</strong> så att du kan ange ett visst radnummer att gå till.<br /> </td>
  </tr>
  <tr>
   <td>Fliken Egenskaper<br /> </td>
   <td>Visar egenskaperna för den nod som du har markerat. Du kan lägga till nya eller ta bort befintliga egenskaper.<br /> </td>
  </tr>
  <tr>
   <td>Fliken Åtkomstkontroll</td>
   <td><p>Visa behörigheter baserat på sökväg, databasnivå eller huvudnamn.</p> <p>Behörigheterna delas upp i</p> <p>- <strong>Tillämplig åtkomstkontrollprincip</strong>: De profiler som kan användas i markeringen.</p> <p>- <strong>Principer för lokal åtkomstkontroll</strong>: De profiler som används lokalt i markeringen.</p> <p>- <strong>Effektiva åtkomstkontrollprinciper</strong>: De principer som används för markeringen kan anges lokalt eller ärvas från överordnade noder.</p> <p>Obs! För att kunna se åtkomstkontrollsinformationen alls måste användaren som är inloggad på CRXDE Lite ha läsbehörighet till ACL-poster. Den anonyma användaren kan inte se den här informationen som standard - logga in som administratör för att se informationen, till exempel.</p> </td>
  </tr>
  <tr>
   <td>Fliken Replikering</td>
   <td><p>Visa nodens replikeringsstatus. Du kan replikera och replikera borttagningen av noden.</p> </td>
  </tr>
  <tr>
   <td>Fliken Konsol<br /> </td>
   <td><p><strong>Serverloggar</strong>:</p> <p>Visar loggmeddelanden. Du kan konfigurera loggnivån, rensa konsolen, fästa vid den valda rullningspositionen och aktivera eller inaktivera visningen av meddelanden.<br /> </p> <p><strong>Versionskontroll</strong>:</p> <p>Visar versionskontrollmeddelanden.<br /> </p> </td>
  </tr>
  <tr>
   <td>Fliken Bygginformation<br /> </td>
   <td>Visar information när ett paket byggs.<br /> </td>
  </tr>
  <tr>
   <td>Uppdatera<br /> </td>
   <td>Uppdaterar markeringen. Ändringar från andra användare uppdateras i din vy av databasen. De ändringar du har gjort påverkas inte.<br /> </td>
  </tr>
  <tr>
   <td>Spara alla</td>
   <td><p><strong>Spara alla</strong>:<br /> </p> <p>Sparar alla ändringar du har gjort. Tills du klickar på Spara är ändringarna temporära och försvinner när du avslutar konsolen.</p> <p><strong>Återställ</strong>:</p> <p>Ignorerar alla ändringar som du har gjort på den valda noden sedan den senaste sparaåtgärden och läser sedan in databasens status för den valda noden igen.</p> <p><strong>Återställ alla</strong>:</p> <p>Ignorerar alla ändringar som du har gjort i hela databasen sedan den senaste sparåtgärden och läser sedan in databasens status igen.</p> </td>
  </tr>
  <tr>
   <td>Skapa ...<br /> </td>
   <td><p>Listruta för att skapa följande under den valda noden:<br /> </p> <p>- <strong>Nod</strong>: en nod med en godtycklig nodtyp<br /> </p> <p>- <strong>Fil</strong>: nt:filnod och dess nt:resursundernod</p> <p>- <strong>Mapp</strong>: nt:mappnod</p> <p>- <strong>Mall</strong>: AEM</p> <p>- <strong>Komponent</strong>: AEM</p> <p>- <strong>Dialog</strong>: AEM</p> </td>
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
   <td>Byt namn ...<br /> </td>
   <td>Byter namn på den markerade noden.<br /> </td>
  </tr>
  <tr>
   <td>Blandningar ...<br /> </td>
   <td>Gör att du kan lägga till blandningstyper i nodtypen. Blandningstyperna används oftast för att lägga till avancerade funktioner som versionshantering, åtkomstkontroll, referenser och låsning till noden.</td>
  </tr>
  <tr>
   <td>verktyg<br /> </td>
   <td><p>Listruta med följande verktyg:</p> <p>- <strong>Serverkonfiguration...</strong>: för åtkomst till Felix Console.</p> <p>- <strong>Fråga ...</strong>: för att fråga databasen.</p> <p>- <strong>Behörigheter ...</strong>: för att öppna behörighetshantering, där du kan visa och lägga till behörigheter.</p> <p>- <strong>Testa åtkomstkontroll ...</strong>: en plats där du kan testa behörigheten för en viss sökväg och/eller huvudman.</p> <p>- <strong>Exportera nodtyp</strong>: om du vill exportera nodtyper i systemet som slutnotation.</p> <p>- <strong>Importera nodtyp..</strong>: om du vill importera nodtyper med slutnotation.</p> <p>- <strong>Installera SiteCatalyst Debugger ...</strong>: anvisningar om hur du installerar Analytics Debugger.</p> </td>
  </tr>
  <tr>
   <td>Inloggningswidget<br /> </td>
   <td><p>Visar de inloggade användarna och arbetsytan som de är inloggade på, till exempel admin@crx.default.</p> <p>Klicka på den för att logga in eller logga in igen som en specifik användare. Om du inte anger en arbetsyta att logga in på loggas du in på standardarbetsytan, crx.default.</p> <p>Om du vill bläddra i databasen som anonym användare använder du <strong>anonym</strong> som inloggningsnamn och lösenord (till exempel ett mellanslag eller en punkt).<br /> </p> <p>Om din auktorisering inte längre är giltig (t.ex. har upphört att gälla) visas "<strong>Obehörig - Logga in..</strong>". Klicka på den för att logga in igen.</p> </td>
  </tr>
 </tbody>
</table>

## Skapa en mapp {#creating-a-folder}

Så här skapar du en mapp med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I navigeringsrutan högerklickar du på den mapp som du vill skapa mappen under och väljer **Skapa ...** sedan **Skapa mapp...**.

1. Ange mappen **Namn** och klicka **OK**.

1. Klicka **Spara alla** för att spara ändringarna på servern.

## Skapa en mall {#creating-a-template}

Så här skapar du en mall med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. Högerklicka på den mapp där du vill skapa mallen i navigeringsrutan och välj **Skapa ...** sedan **Skapa mall...**.

1. Ange **Etikett**, **Titel**, **Beskrivning**, **Resurstyp** och **Rankning** av mallen. Klicka på **Nästa**.

1. Det här steget är valfritt: ange **Tillåtna sökvägar**. Klicka **Nästa**

1. Det här steget är valfritt: ange **Tillåtna överordnade**. Klicka på **Nästa**.

1. Det här steget är valfritt: ange **Tillåtna underordnade**. Klicka **OK**.

1. Klicka **Spara alla** för att spara ändringarna på servern.

Det skapar:

* En nod av typen `cq:Template` med mallegenskaper

* En underordnad nod av typen `cq:PageContent` med egenskaper för sidinnehåll

Du kan lägga till egenskaper i mallen: se [Skapa en egenskap](#creating-a-property) -avsnitt.

## Skapa en komponent {#creating-a-component}

Funktionen som beskrivs här är bara tillgänglig om CQ5 är installerat, det vill säga om nodtypen `cq:Component` är tillgängligt i databasen.

Så här skapar du en komponent med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. Högerklicka på den mapp där du vill skapa komponenten i navigeringsrutan och välj **Skapa ...** sedan **Skapa komponent...**.

1. Ange **Etikett**, **Titel**, **Beskrivning**, **Superresurstyp** och **Grupp** för komponenten. Klicka på **Nästa**.

1. Det här steget är valfritt: ange komponentegenskaperna **Är behållare,** **Ingen dekoration**, **Cellnamn** och **Dialogrutesökväg**. Klicka på **Nästa**.

1. Det här steget är valfritt: ange komponentegenskapen **Tillåtna överordnade**. Klicka på **Nästa**.

1. Det här steget är valfritt: ange komponentegenskapen **Tillåtna underordnade**. Klicka **OK**.

1. Klicka **Spara alla** för att spara ändringarna på servern.

Det skapar:

* En nod av typen `cq:Component`
* Komponentegenskaper
* Ett .jsp-komponentskript

## Skapa en dialogruta {#creating-a-dialog}

Så här skapar du en dialog med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. Högerklicka på komponenten där du vill skapa dialogrutan i navigeringsrutan och välj **Skapa ...** sedan **Skapa dialogruta...**.

1. Ange **Etikett** och **Titel**. Klicka **OK**.

1. Klicka **Spara alla** Spara ändringarna på servern.

En dialogruta med följande struktur skapas:

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

Nu kan du anpassa dialogrutan efter dina behov genom att ändra egenskaper eller skapa noder.

Du kan också använda Dialogruteredigeraren för att redigera en dialogruta. Om du dubbelklickar på dialognoden i CRXDE Lite öppnas redigeraren. Mer information om Dialog Editor finns [här](/help/sites-developing/dialog-editor.md).

## Skapa en nod {#creating-a-node}

Så här skapar du en nod med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. Högerklicka på noden där du vill skapa noden i navigeringsrutan och välj **Skapa ...** sedan **Skapa nod...**.
1. Ange **Namn** och **Typ**. Klicka **OK**.
1. Klicka **Spara alla** för att spara ändringarna på servern.

Nu kan du anpassa noden efter dina behov genom att ändra egenskaper eller skapa noder.

>[!NOTE]
>
>De flesta redigeringsåtgärderna, inklusive Skapa nod, sparar alla ändringar i minnet och lagrar dem bara i databasen när de sparas (med knappen &quot;Spara alla&quot;). Vissa åtgärder, till exempel move, sparas dock automatiskt.
>
>Valideringen av om den nyskapade noden tillåts av den överordnade nodens nodtyp utförs också av JCR-databasen först när ändringarna sparas. Om du får ett felmeddelande när du sparar en nod kontrollerar du om innehållsstrukturen är giltig (du kan till exempel inte skapa en `nt:unstructured` nod som underordnad `nt:folder` nod).

## Skapa en egenskap {#creating-a-property}

Så här skapar du en egenskap med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I navigeringsrutan markerar du den nod där du vill lägga till den nya egenskapen.
1. I **Egenskaper** i den nedre rutan anger du **Namn**, **Typ** och **Värde**. Klicka **Lägg till**.

1. Klicka **Spara alla** för att spara ändringarna på servern.

## Skapa ett skript {#creating-a-script}

Skapa ett skript:

1. Öppna CRXDE Lite i webbläsaren.
1. Högerklicka på den komponent där du vill skapa skriptet i navigeringsrutan och välj **Skapa ...** sedan **Skapa fil...**.

1. Ange filen **Namn** inklusive dess förlängning. Klicka **OK**.

1. Den nya filen öppnas som en flik i rutan Redigera.
1. Redigera filen.
1. Klicka **Spara alla** för att spara ändringarna.

## Exportera och importera nodtyper {#exporting-and-importing-node-types}

Med CRXDE Lite kan du importera och/eller exportera nodtypsdefinitioner i [CND-notation (Compact Namespace and Node Type Definition)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Så här exporterar du en nodtypsdefinition:

1. Öppna CRXDE Lite i webbläsaren.
1. Välj önskad nod.
1. Välj **verktyg** sedan **Exportera nodtyp**.

1. Definitionen visas i slutet av webbläsaren. Spara informationen, om det behövs.

Så här importerar du en nodtypsdefinition:

1. Öppna CRXDE Lite i webbläsaren.
1. Välj **verktyg** sedan **Importera nodtyp...**.

1. Ange CND-notation för definitionen i textrutan.
1. Kontrollera **Tillåt uppdatering** om du uppdaterar en befintlig definition.
1. Klicka **Importera**.

## Loggning {#logging}

Med CRXDE Lite kan du visa filen `error.log` som finns i filsystemet på `<crx-install-dir>/crx-quickstart/server/logs` och filtrera den med rätt loggnivå. Gör så här:

1. Öppna CRXDE Lite i webbläsaren.
1. I **Konsol** längst ned i fönstret väljer du **Serverloggar**.

1. Klicka på **Stoppa** -ikonen för att visa meddelandena.

Du kan:

* Justera loggparametrarna i Felix Console genom att klicka på **Loggningskonfigurationer** -ikon.
* Rensa meddelandena genom att klicka på knappen **Pensel** -ikon.
* Fäst meddelandet vid markeringen genom att klicka på knappen **Fäst** -ikon.
* Aktivera eller inaktivera visning av meddelanden genom att klicka på **Stoppa** -ikon.

## Åtkomstkontroll {#access-control}

>[!NOTE]
>
>Se [Administrera användare, grupper och åtkomsträttigheter](/help/sites-administering/user-group-ac-admin.md) för mer information.
