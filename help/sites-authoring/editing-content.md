---
title: Redigera sidinnehåll
seo-title: Redigera sidinnehåll
description: När sidan har skapats kan du redigera innehållet för att göra de uppdateringar du behöver
seo-description: När sidan har skapats kan du redigera innehållet för att göra de uppdateringar du behöver
uuid: 5b4f0a8f-5196-42ea-8413-203783a0b77b
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: f92ed674-5865-4a53-8c3a-369536861f14
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Redigera sidinnehåll{#editing-page-content}

När sidan har skapats (antingen ny eller som en del av en lansering eller en live-kopia) kan du redigera innehållet för att få de uppdateringar du behöver.

Innehåll läggs till med [komponenter](/help/sites-authoring/default-components-console.md) (lämpliga för innehållstypen) som kan dras till sidan. Du kan sedan redigera dem på plats, flytta eller ta bort dem.

>[!NOTE]
>
>Ditt konto behöver [rätt behörighet](/help/sites-administering/security.md) och [behörighet](/help/sites-administering/security.md#permissions) för att kunna redigera sidor.
>
>Om du råkar ut för problem rekommenderar vi att du kontaktar systemadministratören.

>[!NOTE]
>
>Om sidan och/eller mallen har konfigurerats på rätt sätt kan du använda [responsiv layout](/help/sites-authoring/responsive-layout.md) när du redigerar.

>[!NOTE]
>
>I **redigeringsläget** visas länkar i innehållet, men de är **inte tillgängliga**. Använd [förhandsgranskningsläget](#previewingpagestouchoptimizedui) om du vill navigera med länkarna i innehållet.

## Verktygsfältet Sida {#page-toolbar}

Verktygsfältet för sidan ger tillgång till lämplig funktionalitet, beroende på sidkonfigurationen.

![screen_shot_2018-03-22at11338](assets/screen_shot_2018-03-22at111338.png)

Verktygsfältet har många alternativ. Beroende på ditt aktuella sammanhang och din konfiguration kanske vissa alternativ inte är tillgängliga.

* **Växla sidopanel**

   Då öppnas/stängs sidopanelen, som innehåller [Resursläsaren](/help/sites-authoring/author-environment-tools.md#assets-browser), [Komponentbläddraren](/help/sites-authoring/author-environment-tools.md#components-browser)och [Innehållsträdet](/help/sites-authoring/author-environment-tools.md#content-tree).

   ![](do-not-localize/screen_shot_2018-03-22at111425.png)

* **Sidinformation**

   Ger åtkomst till menyn [Sidinformation](/help/sites-authoring/author-environment-tools.md#page-information) , inklusive sidinformation och åtgärder som kan vidtas på sidan, inklusive visning och redigering av sidinformation, visning av sidegenskaper samt publicering/avpublicering av sidan.

   ![](do-not-localize/screen_shot_2018-03-22at111437.png)

* **Emulator**

   Växlar verktygsfältet [för](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)emulatorn, som används för att emulera sidans utseende och känsla på en annan enhet. Detta aktiveras automatiskt i layoutläge.

   ![](do-not-localize/screen_shot_2018-03-22at111442.png)

* **ContextHub**

   Öppnar [kontextnavet](/help/sites-authoring/ch-previewing.md). Endast tillgängligt i förhandsgranskningsläget.

   ![screen_shot_2018-03-22at11543](assets/screen_shot_2018-03-22at111543.png)

* **Sidrubrik**

   Detta är enbart informativt.

   ![screen_shot_2018-03-22at11554](assets/screen_shot_2018-03-22at111554.png)

* **Lägesväljare**

   Visar det aktuella [läget](/help/sites-authoring/author-environment-tools.md#page-modes) och gör att du kan välja ett annat läge, t.ex. redigering, layout, tidsförvrängning eller mål.

   ![chlimage_1-120](assets/chlimage_1-120.png)

* **Förhandsgranska**

   Aktiverar [förhandsgranskningsläge](/help/sites-authoring/editing-content.md#preview-mode). Då visas sidan som den kommer att se ut när den publiceras.

   ![chlimage_1-121](assets/chlimage_1-121.png)

* **Anteckna**

   Gör att du kan lägga till [anteckningar](/help/sites-authoring/annotations.md) på sidan när du granskar en sida. Efter den första anteckningen växlar ikonen till ett nummer som anger antalet anteckningar på sidan.

   ![](do-not-localize/screen_shot_2018-03-22at111638.png)

### Statusmeddelande {#status-notification}

Om en sida är en del av ett [arbetsflöde](/help/sites-authoring/workflows.md) eller flera arbetsflöden visas den här informationen i ett meddelandefält högst upp på skärmen när sidan redigeras.

![screen_shot_2018-03-22at11739](assets/screen_shot_2018-03-22at111739.png)

>[!NOTE]
>
>Statusfältet är bara synligt för användarkonton med lämplig behörighet.

I meddelandet visas arbetsflödet som körs mot sidan. Om användaren är involverad i det aktuella arbetsflödessteget finns även alternativ som [påverkar arbetsflödets status](/help/sites-authoring/workflows-participating.md) och får mer information om arbetsflödet, som:

* **Fullständigt** - Öppnar dialogrutan **Fullständigt** arbetsobjekt

* **Delegera** - Öppnar dialogrutan **Fullständigt arbetsobjekt**

* **Visa information** - Öppnar fönstret **Detaljer** i arbetsflödet

Att slutföra och delegera arbetsflödessteg via meddelandefältet fungerar på samma sätt som när du [deltar i arbetsflöden](/help/sites-authoring/workflows-participating.md) från meddelandeinkorgen.

Om sidan har flera arbetsflöden visas antalet arbetsflöden till höger om meddelandet tillsammans med pilknapparna så att du kan bläddra igenom arbetsflödena.

![chlimage_1-122](assets/chlimage_1-122.png)

## Komponentplatshållare {#component-placeholder}

Komponentplatshållaren är en indikator som visar var en komponent placeras när du släpper den - ovanför den komponent som du håller pekaren över.

* När du lägger till en ny komponent på sidan (drar från komponentwebbläsaren):

   ![screen_shot_2018-03-22at11928](assets/screen_shot_2018-03-22at111928.png)

* När en befintlig komponent flyttas:

   ![screen_shot_2018-03-22at112445](assets/screen_shot_2018-03-22at112445.png)

## Infoga en komponent {#inserting-a-component}

### Infoga en komponent från komponentwebbläsaren {#inserting-a-component-from-the-components-browser}

Du kan lägga till en ny komponent med [komponentwebbläsaren](/help/sites-authoring/author-environment-tools.md#components-browser). Platshållaren [för](#component-placeholder) komponenten visar var komponenten kommer att placeras:

1. Kontrollera att sidan är i [**redigeringsläge **](/help/sites-authoring/author-environment-tools.md#page-modes).
1. Öppna [komponentwebbläsaren](/help/sites-authoring/author-environment-tools.md#components-browser).
1. Dra den önskade komponenten till [önskad plats](#component-placeholder).

1. [Redigera](#editmovecopypastedelete) komponenten.

>[!NOTE]
>
>Komponentwebbläsaren fyller hela skärmen på en mobil enhet. När du börjar dra en komponent stängs webbläsaren och sidan visas igen så att du kan montera komponenten.

### Infoga en komponent från styckesystemet {#inserting-a-component-from-the-paragraph-system}

Du kan lägga till en ny komponent genom att använda rutan **Dra komponenter här** i styckesystemet:

1. Kontrollera att sidan är i [**redigeringsläge **](/help/sites-authoring/author-environment-tools.md#page-modes).
1. Det finns två sätt att markera och lägga till en ny komponent från styckesystemet:

   * Välj alternativet **Infoga komponent** (+) antingen i verktygsfältet för en befintlig komponent eller i rutan **Dra komponenter hit** .
   ![screen_shot_2018-03-22at112536](assets/screen_shot_2018-03-22at112536.png)

   * Om du använder en stationär enhet kan du dubbelklicka på **Dra komponenter här** .
   Dialogrutan **Infoga ny komponent** öppnas så att du kan välja önskad komponent:

   ![screen_shot_2018-03-22at112650](assets/screen_shot_2018-03-22at112650.png)

1. Den markerade komponenten läggs till längst ned på sidan. [Redigera](#editmovecopypastedelete) komponenten efter behov.

### Infoga en komponent med Resursläsaren {#inserting-a-component-using-the-assets-browser}

Du kan också lägga till en ny komponent på sidan genom att dra en resurs från [resursläsaren](/help/sites-authoring/author-environment-tools.md#assets-browser). Då skapas automatiskt en ny komponent av lämplig typ (och som innehåller resursen).

Detta gäller för följande tillgångstyper (vissa kommer att vara beroende av sid-/styckesystem):

<table>
 <tbody>
  <tr>
   <th><strong>Resurstyp</strong></th>
   <th><strong>Resulterande komponenttyp</strong></th>
  </tr>
  <tr>
   <td>Bild</td>
   <td>Bild</td>
  </tr>
  <tr>
   <td>Dokument</td>
   <td>Hämta</td>
  </tr>
  <tr>
   <td>Produkt</td>
   <td>Produkt</td>
  </tr>
  <tr>
   <td>Video</td>
   <td>Flash</td>
  </tr>
  <tr>
   <td>Innehållsfragment</td>
   <td>Innehållsfragment<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Det här beteendet kan konfigureras för din installation. Mer information finns i [Konfigurera ett styckesystem så att en komponentinstans](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) skapas när du drar en resurs.

Så här skapar du en komponent genom att dra en av resurstyperna ovan:

1. Kontrollera att sidan är i [**redigeringsläge **](/help/sites-authoring/author-environment-tools.md#page-modes).
1. Öppna [resursläsaren](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. Dra den önskade resursen till önskad position. Platshållaren [för](#component-placeholder) komponenten visar var komponenten kommer att placeras.

   En komponent som passar resurstypen skapas på den önskade platsen, den innehåller den valda resursen.

1. [Redigera](#editmovecopypastedelete) komponenten vid behov.

>[!NOTE]
>
>På en mobil enhet fyller resursläsaren hela skärmen. När du börjar dra en resurs stängs webbläsaren och sidan visas igen så att du kan montera resursen.

Om du behöver göra en snabb ändring i en resurs när du bläddrar bland resurserna kan du starta [resursredigeraren](/help/assets/managing-assets-touch-ui.md) direkt från webbläsaren genom att klicka på redigeringsikonen bredvid resursens namn.

![screen_shot_2018-03-22at112735](assets/screen_shot_2018-03-22at112735.png)

## Redigera/konfigurera/kopiera/klipp/ta bort/klistra in {#edit-configure-copy-cut-delete-paste}

Om du väljer en komponent öppnas verktygsfältet. Detta ger åtkomst till olika åtgärder som kan utföras på komponenten.

De faktiska åtgärder som är tillgängliga för användaren visas som lämpliga och inte alla åtgärder beskrivs här.

![screen_shot_2018-03-22at112909](assets/screen_shot_2018-03-22at112909.png)

* **Redigera**

   [Beroende på komponenttypen](/help/sites-authoring/default-components.md) kan du [redigera komponentens](#edit-content)innehåll. Ofta finns det ett verktygsfält.

   ![](do-not-localize/screen_shot_2018-03-22at112936.png)

* **Konfigurera**

   [Beroende på komponenttypen](/help/sites-authoring/default-components.md) kan du redigera och konfigurera komponentens egenskaper. Ofta öppnas en dialogruta.

   ![](do-not-localize/screen_shot_2018-03-22at112955.png)

* **Kopiera**

   Komponenten kopieras då till Urklipp. När inklistringsåtgärden är klar finns den ursprungliga komponenten kvar.

   ![](do-not-localize/screen_shot_2018-03-22at113000.png)

* **Klipp ut**

   Komponenten kopieras då till Urklipp. När inklistringsåtgärden har utförts tas den ursprungliga komponenten bort.

   ![screen_shot_2018-03-22at113007](assets/screen_shot_2018-03-22at113007.png)

* **Ta bort**

   Då tas komponenten bort från sidan med din bekräftelse.

   ![](do-not-localize/screen_shot_2018-03-22at113012.png)

* **Infoga komponent**

   Då öppnas dialogrutan där du kan [lägga till en ny komponent](/help/sites-authoring/editing-content.md#inserting-a-component-from-the-paragraph-system).

   ![](do-not-localize/screen_shot_2018-03-22at113017.png)

* **Klistra in**

   Komponenten klistras in från Urklipp till sidan. Om originalet finns kvar beror på om du har använt kopian eller klippet.

   * Du kan klistra in på samma sida eller på en annan sida.
   * Det inklistrade objektet klistras in ovanför objektet där du väljer åtgärden Klistra in.
   * Åtgärden Klistra in visas bara om det finns innehåll i Urklipp.
   ![screen_shot_2018-03-22at113553](assets/screen_shot_2018-03-22at113553.png)

   >[!NOTE]
   >
   >Om du klistrar in på en annan sida som redan var öppen före klipp ut/kopiera-åtgärden, måste du uppdatera sidan för att se det inklistrade innehållet.

* **Grupp**

   På så sätt kan du markera flera komponenter samtidigt. Samma sak kan du göra på en stationär enhet genom att **Ctrl-klicka** eller **Kommando-klicka**.

   ![](do-not-localize/screen_shot_2018-03-22at113240.png)

* **Överordnad**

   Gör att du kan välja den överordnade komponenten för den markerade komponenten.

   ![screen_shot_2018-03-22at113028](assets/screen_shot_2018-03-22at113028.png)

* **Layout**

   På så sätt kan du ändra den markerade komponentens [layout](/help/sites-authoring/editing-content.md#edit-component-layout) . Detta gäller bara den markerade komponenten och aktiverar inte [layoutläget](/help/sites-authoring/author-environment-tools.md#page-modes) för hela sidan.

   ![](do-not-localize/screen_shot_2018-03-22at113044.png)

* **Konvertera till en upplevelsefragmentvariation**

   På så sätt kan du skapa ett nytt [upplevelsefragment](/help/sites-authoring/experience-fragments.md) från den valda komponenten eller lägga till det i ett befintligt upplevelsefragment.

   ![](do-not-localize/screen_shot_2018-03-22at113033.png)

## Redigera (innehåll) {#edit-content}

Det finns två sätt att lägga till och/eller redigera innehåll i komponenter:

* Öppna [komponentdialogrutan för redigering](#component-edit-dialog).
* [Dra och släpp en resurs](#draganddropintocomponent) från resursläsaren för att lägga till innehåll direkt.

### Dialogrutan Komponentredigering {#component-edit-dialog}

Du kan öppna en komponent och redigera innehållet med ikonen [Redigera (penna) i komponentverktygsfältet](#edit-configure-copy-cut-delete-paste).

De exakta redigeringsalternativen beror på komponenten. För vissa komponenter är [alla åtgärder bara tillgängliga i helskärmsläge](#edit-content-full-screen-mode). Exempel:

* [Textkomponent](/help/sites-authoring/rich-text-editor.md#main-pars-title-24)

   ![screen_shot_2018-03-22at120215](assets/screen_shot_2018-03-22at120215.png)

* Bildkomponent

   ![screen_shot_2018-03-22at120252](assets/screen_shot_2018-03-22at120252.png)

   >[!NOTE]
   >
   >Redigering fungerar inte på en tom bildkomponent.
   >
   >
   >Du måste [dra eller överföra en bild (med Konfigurera)](/help/sites-authoring/default-components-foundation.md#image) innan du kan börja redigera den.

* Bildkomponent - helskärm

   [Om du aktiverar helskärmsläget](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode) för bildkomponenten får du mer utrymme för redigering av bilden och dessutom visas extra redigeringsalternativ som **Starta karta** och **Återställ zoomning**. Med helskärmsläge kan du dessutom välja förinställningar för beskärning.

   ![screen_shot_2018-03-22at120529](assets/screen_shot_2018-03-22at120529.png)

* Komponenter som har konstruerats av mer än en grundläggande komponent, till exempel komponenten [](/help/sites-authoring/default-components-foundation.md#text-image)Text och bild, ber dig först bekräfta vilken uppsättning redigeringsalternativ du vill använda:

   ![chlimage_1-123](assets/chlimage_1-123.png)

### Dra och släpp resurser till komponent {#drag-and-drop-assets-into-component}

För specifika komponenttyper kan du dra och släppa resurser från resursläsaren direkt till komponenten för att uppdatera innehållet:

| **Resurstyp** | **Komponenttyp** |
|---|---|
| Bild | Bild |
| Dokument | Hämta |
| Produkt | Produkt |
| Video | Flash |
| Innehållsfragment | Innehållsfragment |

## Redigera (innehåll) helskärmsläge {#edit-content-full-screen-mode}

För alla komponenter går det att komma åt helskärmsläget med (och avsluta från):

![](do-not-localize/chlimage_1-20.png)

Komponenten **Text** :

![screen_shot_2018-03-22at121616](assets/screen_shot_2018-03-22at121616.png)

>[!NOTE]
>
>För vissa komponenter har helskärmsläget fler alternativ än den grundläggande redigeraren på plats.

## Flytta en komponent {#moving-a-component}

Så här flyttar du en styckekomponent:

1. Markera det stycke som ska flyttas genom att trycka och hålla ned eller klicka och hålla ned.
1. Dra stycket till den nya platsen. AEM anger var stycket kan placeras. Släpp den där du vill.

   ![screen_shot_2018-03-22at121821](assets/screen_shot_2018-03-22at121821.png)

1. Stycket flyttas.

>[!NOTE]
>
>Du kan också använda [Klipp ut och Klistra in](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) för att flytta en komponent.

## Redigera komponentlayout {#edit-component-layout}

I stället för att behöva växla från redigeringsläge till [layoutläge](/help/sites-authoring/responsive-layout.md) flera gånger för att justera en komponent, kan du välja åtgärden **Layout** för en komponent för att ändra komponentens layout och spara tid genom att inte behöva lämna redigeringsläget.

1. När du väljer en komponent i **redigeringsläget** för platskonsolen visas komponentens verktygsfält.

   ![screen_shot_2018-03-22at133756](assets/screen_shot_2018-03-22at133756.png)

   Justera komponentens layout genom att klicka på eller trycka på **Layout** .

   ![](do-not-localize/chlimage_1-21.png)

1. När Layout-åtgärden är markerad:

   * Storlekshandtagen för komponentvisningen.
   * Emulatorverktygsfältet visas högst upp på skärmen.
   * Layoutåtgärder i stället för standardredigeringsåtgärder visas i komponentverktygsfältet.
   ![screen_shot_2018-03-22at133843](assets/screen_shot_2018-03-22at133843.png)

   Nu kan du ändra komponentens layout på samma sätt som i [layoutläget](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode).

1. När du har gjort de nödvändiga layoutändringarna klickar du på **Stäng** på komponentens åtgärdsmeny för att sluta ändra komponentens layout. Komponentens verktygsfält återgår till det normala redigeringsläget.

   ![](do-not-localize/screen_shot_2018-03-22at133920.png)

>[!NOTE]
>
>Layoutåtgärden är begränsad i omfång till den markerade komponenten. Om du till exempel redigerar layouten för en komponent och sedan klickar på en annan komponent, visas standardverktygsfältet för redigering (inte verktygsfältet för layout) för den nyligen markerade komponenten och handtagen för storleksändring samt emulatorns verktygsfält.
>
>Om du behöver redigera den övergripande layouten för sidan, vilket påverkar flera komponenter, växlar du till [layoutläget](/help/sites-authoring/responsive-layout.md).

## Ärvda komponenter {#inherited-components}

Ärvda komponenter kan vara produkten av olika scenarier, bland annat:

* [Hantering av flera webbplatser](/help/sites-administering/msm.md)
* [Startar](/help/sites-authoring/launches.md) (baserat på live-kopia).
* Specifika komponenter, till exempel det ärvda styckesystemet i Geometrixx.

Du kan avbryta (och sedan återaktivera) arvet. Beroende på vilken komponent det gäller kan det här vara tillgängligt från:

* **Live Copy**

   Komponentens verktygsfält, om komponenten finns på en sida som är en del av en live-kopia eller en start (baserat på en live-kopia). Exempel:

   ![screen_shot_2018-03-22at134339](assets/screen_shot_2018-03-22at134339.png)

   Alternativet Avbryt arv är tillgängligt:

   ![](do-not-localize/screen_shot_2018-03-22at134406.png)

   Eller återaktivera arv om det redan har avbrutits:

   ![](do-not-localize/screen_shot_2018-03-22at134417.png)

   Åtgärden Överrullning är även tillgänglig i källan för utkast eller Live-kopia:

   ![](do-not-localize/screen_shot_2018-03-22at134516.png)

* **Ett ärvt styckesystem**

   Konfigurationsdialogrutan. Som med det ärvda styckesystemet:

   ![chlimage_1-124](assets/chlimage_1-124.png)

## Redigera sidmallen {#editing-the-page-template}

Om sidan är baserad på en [redigerbar mall](/help/sites-authoring/templates.md#editable-and-static-templates)kan du enkelt växla till [mallredigeraren](/help/sites-authoring/templates.md#editing-templates-template-authors) genom att välja **Redigera mall** på menyn [](/help/sites-authoring/author-environment-tools.md#page-information)Sidinformation.

Om sidan är baserad på en [statisk mall](/help/sites-authoring/templates.md#editable-and-static-templates)kan du växla till [designläge](/help/sites-authoring/default-components-designmode.md) med [sidlägesväljaren](/help/sites-authoring/author-environment-tools.md#page-modes) i verktygsfältet för att aktivera/inaktivera komponenter som ska användas på sidan.

Du kan enkelt se vilken mall sidan baseras på när du markerar sidan i [kolumnvyn](/help/sites-authoring/basic-handling.md#column-view) eller [listvyn](/help/sites-authoring/basic-handling.md#list-view).

## Live Copy-status {#live-copy-status}

I [läget](/help/sites-authoring/author-environment-tools.md#page-modes) Live Copy Status kan du snabbt se vilken status kopian har och vilka komponenter som inte ärvs:

* Grön kantlinje: Ärvd
* Rosa kantlinje: Arvet har annullerats

Exempel:

![screen_shot_2018-03-22at134820](assets/screen_shot_2018-03-22at134820.png)

## Lägga till anteckningar {#adding-annotations}

[Med anteckningar](/help/sites-authoring/annotations.md) kan granskare och andra författare ge feedback på ditt innehåll. De används ofta för granskning och validering.

## Förhandsgranska sidor {#previewing-pages}

Det finns två alternativ för att förhandsgranska en sida:

* [Förhandsgranskningsläge](#preview-mode) - en snabb förhandsgranskning på plats

* [Visa som publicerad](#view-as-published) - en fullständig förhandsgranskning som öppnar sidan på en ny flik

>[!NOTE]
>
>* Länkarna i innehållet är synliga, men inte tillgängliga i redigeringsläget.
>* Använd något av förhandsvisningsalternativen om du vill navigera med hjälp av länkarna.
>* Använd [kortkommandot](/help/sites-authoring/keyboard-shortcuts.md) för att växla mellan förhandsvisning och det senast markerade läget `Ctrl-Shift-M` .
>



>[!NOTE]
>
>WCM-lägets cookie är inställd för båda alternativen.

### Förhandsgranskningsläge {#preview-mode}

När du redigerar innehåll kan du förhandsgranska sidan i [förhandsgranskningsläget](/help/sites-authoring/author-environment-tools.md#page-modes). Det här läget:

* Döljer olika redigeringsmekanismer så att du snabbt kan se hur sidan kommer att se ut vid publiceringen.
* Gör att du kan använda länkar för att navigera.
* Uppdaterar **inte** sidinnehållet.

Vid redigering är förhandsgranskningsläget tillgängligt med hjälp av ikonen längst upp till höger i sidredigeraren:

![chlimage_1-125](assets/chlimage_1-125.png)

### Visa som publicerad {#view-as-published}

Alternativet **Visa som publicerad** finns på menyn [Sidinformation](/help/sites-authoring/author-environment-tools.md#page-information) . Sidan öppnas på en ny flik, innehållet uppdateras och sidan visas exakt som den kommer att visas i publiceringsmiljön.

## Låsa en sida {#locking-a-page}

Med AEM kan du låsa en sida så att ingen annan kan ändra innehållet. Det här är användbart när du gör många ändringar på en viss sida eller när du behöver frysa en sida en kort stund.

En sida kan låsas från:

* **Platskonsol**

   1. Markera sidan i [markeringsläge](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
   1. Välj låsikonen.
   ![screen_shot_2018-03-22at134928](assets/screen_shot_2018-03-22at134928.png)

* **Page Editor**

   1. Öppna menyn genom att klicka på ikonen **Sidinformation** .
   1. Välj alternativet **Lås sida** .

När konsolvyn är låst uppdateras informationen och när du redigerar en låssymbol visas den i verktygsfältet.

![screen_shot_2018-03-22at135010](assets/screen_shot_2018-03-22at135010.png)

>[!CAUTION]
>
>Du kan låsa en sida när du [personifierar en användare](/help/sites-administering/security.md#impersonating-another-user). En sida som är låst på det här sättet kan bara låsas upp av den användare som är imiterad eller av administratörsanvändaren.
>
>Sidorna kan inte låsas upp genom att den användare som låste sidan personifieras.

## Låsa upp en sida {#unlocking-a-page}

Att låsa upp en sida påminner mycket om att [låsa sidan](#locking-a-page). När sidan är låst ersätts låsalternativen av upplåsningsåtgärder.

På menyn Sidinformation visas **Lås upp** som ett alternativ och låsikonen i platskonsolen ersätts av en **Lås upp** -ikon.

![screen_shot_2018-03-22at134942](assets/screen_shot_2018-03-22at134942.png)

>[!CAUTION]
>
>Du kan låsa en sida när du [personifierar en användare](/help/sites-administering/security.md#impersonating-another-user). En sida som är låst på det här sättet kan bara låsas upp av den användare som är imiterad eller av administratörsanvändaren.
>
>Sidorna kan inte låsas upp genom att den användare som låste sidan personifieras.

## Ångra och göra om sidredigeringar {#undoing-and-redoing-page-edits}

Med följande ikoner kan du ångra eller göra om en åtgärd. Dessa visas i verktygsfältet när det är lämpligt:

![](do-not-localize/screen_shot_2018-03-23at093614.png)

>[!NOTE]
>
>Du kan även [använda kortkommandot](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) `Ctrl-Z` för att ångra sidredigeringsåtgärder.
>
>Kortkommandot `Ctrl-Y` är även tillgängligt för att göra om sidredigeringsåtgärder.

>[!NOTE]
>
>Se [Ångra och Gör om sidredigeringar - Teoriet](#undoing-and-redoing-page-edits-the-theory) innehåller alla detaljer om vad som är möjligt när du ångrar och gör om sidredigeringar.

## Ångra och göra om sidredigeringar - The Theory {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>Systemadministratören kan [konfigurera olika aspekter av funktionerna](/help/sites-administering/config-undo.md) Ångra/Gör om enligt kraven för din instans.

AEM lagrar en historik över åtgärder som du utför och i vilken ordning du utförde dem, så att du kan ångra flera åtgärder i den ordning som du utförde dem samt göra om dem för att återanvända en eller flera av åtgärderna om det behövs.

Om ett element på innehållssidan är markerat (till exempel en textkomponent) gäller kommandot ångra och gör om det markerade objektet.

Funktionen för kommandona ångra och gör om liknar den i andra program. Använd kommandona för att återställa webbsidans senaste status när du fattar beslut om innehållet. Om du till exempel flyttar ett textstycke till en annan plats på sidan kan du använda kommandot Ångra för att flytta tillbaka stycket. Om du sedan bestämmer dig för att den föregående positionen var bättre använder du kommandot gör om för att ångra.

>[!NOTE]
>
>Du kan:
>
>* Gör om åtgärder så länge du inte har gjort någon sidredigering sedan du använde Ångra.
>* Ångra högst 20 redigeringsåtgärder (standardinställning).
>* Använd även [kortkommandon](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) för att ångra och göra om.
>



Du kan använda Ångra och Gör om för följande typer av sidändringar:

* Lägga till, redigera, ta bort och flytta stycken
* In-place editing of paragraph content
* Kopiera, klippa ut och klistra in objekt på en sida

Formulärfält som formulärkomponenter återger ska inte ha värden som anges vid redigering av sidor. Kommandona Ångra och Gör om påverkar därför inte ändringar som du gör i värdena för dessa typer av komponenter. Du kan till exempel inte ångra valet av ett värde i en nedrullningsbar lista.

>[!NOTE]
>
>Särskilda behörigheter krävs för att ångra och göra om ändringar i filer och bilder.

>[!NOTE]
>
>Historiken för ändringar av filer och bilder varar i minst tio timmar. Efter den här gången kan du dock inte ångra ändringarna. Administratören kan ändra standardtiden på tio timmar.

