---
title: Importera och exportera resurser till AEM-formulär
seo-title: Importera och exportera resurser till AEM-formulär
description: Du kan importera och exportera adaptiva formulär och mallar från och till AEM-instanser. Detta gör det lättare att migrera formulär eller flytta dem mellan olika system.
seo-description: Du kan importera och exportera adaptiva formulär och mallar från och till AEM-instanser. Detta gör det lättare att migrera formulär eller flytta dem mellan olika system.
uuid: 937daedd-56f3-4e02-b695-b194b494d9bf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 69210727-dde3-495a-87b7-2e8173e6b664
docset: aem65
translation-type: tm+mt
source-git-commit: 5035c9630b5e861f4386e1b5ab4f4ae7a8d26149

---


# Importera och exportera resurser till AEM-formulär{#importing-and-exporting-assets-to-aem-forms}

Du kan flytta formulär och relaterade resurser, teman, dataordlistor, dokumentfragment och bokstäver mellan olika AEM Forms-instanser. En sådan rörelse krävs när du migrerar system eller flyttar formulär från en scenserver till en produktionsserver. För de resurser för vilka det finns stöd för att överföra och importera via användargränssnittet för AEM-formulär bör du använda användargränssnittet för formulär för att exportera eller importera. Du bör inte använda AEM Package Manager för att exportera eller importera sådana resurser.

>[!NOTE]
>
>* I AEM 6.4 Forms har strukturen och sökvägarna för crx-databaser ändrats. Om du importerar resurser från en tidigare version till AEM 6.4-formulär och formuläret har vissa beroenden av den äldre strukturen, måste du exportera beroendena manuellt. Mer information om förändringar i databasens struktur och sökvägar finns i [Databasomstrukturering i AEM](/help/sites-deploying/repository-restructuring.md).
>



## Hämta eller överföra resurser för formulär och dokument {#download-or-upload-forms-amp-documents-assets}

Med användargränssnittet i AEM Forms kan du exportera resurser från en AEM-instans genom att hämta dem som ett AEM CRX-paket eller binära filer. Du kan sedan importera det hämtade AEM CRX-paketet eller den binära filen till en annan AEM-instans.

Exportera och importera via användargränssnittet i AEM Forms stöds för alla resurser förutom för adaptiva formulärmallar och policyer för adaptivt formulärinnehåll. När du exporterar ett anpassat formulär från användargränssnittet i AEM Forms exporteras därför inte de relaterade anpassningsbara formulärmallarna och innehållsprofilerna automatiskt som andra relaterade resurser.

För dessa resurstyper måste du använda AEM Package Manager för att skapa ett CRX-paket på källans AEM-server och installera paketet på målservern. Mer information om hur du skapar och installerar paket finns i [Arbeta med paket](/help/sites-administering/package-manager.md).

### Hämta resurser för formulär och dokument {#download-forms-amp-documents-assets}

Så här hämtar du resurser för formulär och dokument:

1. Logga in på AEM Forms-instansen.
1. Tryck på Experience Manager ![adobeexperienceManager](assets/adobeexperiencemanager.png) -ikonen > ikonen ![för navigeringskompilering](assets/compass.png) > Formulär > Formulär och dokument.
1. Markera formulärresurserna och tryck på ikonen **Hämta** .
1. Välj något av följande alternativ i Hämta resurser och tryck sedan på **Hämta**.

   * **Hämta som CRX-paket:** Använd alternativet för att hämta och flytta alla valda resurser och relaterade beroenden från en AEM Forms-instans till en annan. Alla resurser och mappar hämtas som crx-paket. Alla formulärresurser, inklusive formulär som skapats i AEM (adaptiva formulär, interaktiv kommunikation och adaptiva formulärfragment), formuläruppsättningar, formulärmallar, PDF-dokument och resurser (XSD, XFS, bilder) kan hämtas som paket från AEM Forms UI.
Fördelen med att hämta resurser som paket är att det även hämtar resurser som har använts av den resurs som valts för hämtning. Om du till exempel har ett adaptivt formulär som använder en formulärmall, XSD och en bild. När du väljer det här adaptiva formuläret och hämtar det som paket innehåller det hämtade paketet även formulärmallen, XSD och bilden. Alla metadataegenskaper (inklusive anpassade egenskaper) som är kopplade till resursen hämtas också.

   * **Hämta resurser som binära filer:** Använd alternativet för att endast hämta formulärmallar (XDP), PDF-formulär (PDF), dokument (PDF) och resurser (bilder, scheman, formatmallar). Du kan redigera dessa resurser med externa program. Det hämtar formulärresurser som har binära filer, som XSD, XDP, bilder, PDF och XDP som en ZIP-fil.
Du kan inte hämta adaptiva formulär, interaktiv kommunikation, adaptiva formulärfragment, teman och formuläruppsättningar med alternativet **Hämta resurser som binära filer** . Om du vill hämta dessa resurser använder du **alternativet Hämta som CRX-paket** .
   De valda resurserna hämtas som ett arkiv (.zip-fil).

   >[!NOTE]
   >
   >Både AEM-paket och binära filer hämtas som arkiv (.zip-fil). Mallarna för resurserna hämtas inte tillsammans med resurserna. Du måste exportera resursmallarna separat.

### Överför resurser för formulär och dokument {#upload-forms-amp-documents-assets}

Så här överför du resurser för formulär och dokument:

>[!VIDEO](https://vimeo.com/)

1. Logga in på AEM Forms-instansen.
1. Tryck på Experience Manager ![adobeexperienceManager](assets/adobeexperiencemanager.png) -ikonen > ikonen ![för navigeringskompilering](assets/compass.png) > Formulär > Formulär och dokument.
1. Tryck på **Skapa** >**Filöverföring**. En dialogruta för att överföra formulär eller paket visas.
1. I dialogrutan bläddrar du till och väljer paketet eller arkivet som ska importeras. Du kan också välja PDF-dokument, XSD, bilder, formatmallar och XDP-formulär. Tryck på **Öppna**. Mappen eller filnamnet som du väljer får inte innehålla några specialtecken.

   Kontrollera i dialogrutan vilka resurser som överförs och tryck sedan på **Överför**.

   Om du överför en befintlig formulärresurs uppdateras resursen.

   >[!NOTE]
   >
   >Befintlig mapphierarki ersätts inte när du överför ett paket. Om du till exempel har ett anpassat formulär som heter &#39;Utbildning&#39; på platsen /content/dam/formSanddocuments på en server. Du hämtar det adaptiva formuläret och överför det till en annan server. Den andra servern har också en mapp med namnet &quot;Training&quot; på samma plats /content/dam/formSanddocuments. Överföringen misslyckas.

## Hämta eller överföra ett tema {#downloading-or-uploading-a-theme}

Med AEM Forms kan du skapa, ladda ned och ladda upp teman. Ett tema skapas som andra resurser som formulär, dokument och brev. Du kan skapa ett tema, hämta det och överföra det till en separat instans för att återanvända det. Mer information om teman finns i [Teman i AEM-formulär](../../forms/using/themes.md).

### Hämta ett tema {#downloading-a-theme}

Du kan exportera teman i AEM Forms som du kan använda i andra projekt eller instanser. Med AEM kan du hämta temat som en zip-fil som du kan överföra till instansen.

Så här hämtar du ett tema:

1. Logga in på AEM Forms-instansen.
1. Tryck på ikonen Experience Manager ![adobeexperienceManager](assets/adobeexperiencemanager.png) > ikonen ![för navigeringskompilering](assets/compass.png) > Formulär > Teman.
1. Välj temat och tryck på **Hämta**. Temat laddas ned som ett arkiv (.zip-fil).

### Överföra ett tema {#uploading-a-theme}

Du kan använda skapade teman med formatförinställningar i ditt projekt. Du kan importera temapaket som andra skapar genom att överföra dem till ditt projekt.

Så här överför du ett tema:

1. Navigera till **Formulär > Teman** i Experience Manager.
1. Klicka på **Skapa > Filöverföring** på sidan Teman.
1. I filöverföringsprompten bläddrar du till och väljer ett temapaket på datorn och klickar på **Överför**.
Det överförda temat är tillgängligt på temasidan.

1. Logga in på AEM Forms-instansen.
1. Tryck på ikonen Experience Manager ![adobeexperienceManager](assets/adobeexperiencemanager.png) > ikonen ![för navigeringskompilering](assets/compass.png) > Formulär > Teman.
1. Klicka på **Skapa** > **Filöverföring**. I filöverföringsprompten bläddrar du till och väljer ett temapaket på datorn och klickar på **Överför**. Temat överförs.

## Importera och exportera resurser i korrespondenshantering {#import-and-export-assets-in-correspondence-management}

Om du vill dela resurser, t.ex. dataordlistor, bokstäver och dokumentfragment, mellan två olika implementeringar av Correspondence Management, kan du skapa och dela .cmp-filer. En .cmp-fil kan innehålla en eller flera dataordlistor, bokstäver, dokumentfragment och formulär.

### Exportera dokumentfragment, bokstäver och/eller dataordlistor {#export-document-fragments-letters-and-or-data-dictionaries}

1. På bokstäverna, dokumentfragmenten eller dataordlistesidorna trycker du på och markerar de resurser du vill exportera till ett enskilt paket och trycker sedan på Kö för hämtning. Resurserna är anpassade för export.
1. Om det behövs upprepar du ovanstående steg för att lägga till bokstäver, dokumentfragment och dataordlistor.
1. Tryck på **Hämta**.
1. Korrespondenshantering visar dialogrutan Hämta resurser med en lista över resurser i exportlistan.

   ![export](assets/export.png)

1. Om du vill visa beroenden som exporteras trycker du på Lös. Eller gå vidare till nästa steg. Även om du inte trycker på Lös exporteras beroendena fortfarande.
1. Om du vill hämta .cmp-filen trycker du på **OK**.
1. Correspondence Management hämtar en .cmp-fil till datorn.

   Cmp-filen innehåller de exporterade resurserna. Du kan dela .cmp-filen med andra. Andra användare kan importera .cmp-filen till en annan server för att hämta alla resurser på den nya servern.

### Exportera alla Correspondence Management-resurser som ett paket {#export-all-the-correspondence-management-assets-as-a-package}

Använd det här alternativet om du vill hämta alla Correspondence Management-resurser och relaterade beroenden som ett paket från en AEM-formulärinstans.

Om till exempel Correspondence Management har en bokstav som använder en bild och text innehåller det hämtade paketet även bilden och texten som hör till bokstaven. Alla metadataegenskaper (inklusive anpassade egenskaper) som är kopplade till resursen hämtas också. När du har hämtat paketet (.cmp) kan du [importera paketet till en annan AEM Forms-instans](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p).

Så här hämtar du alla Correspondence Management-resurser och relaterade beroenden som ett paket:

1. Logga in på AEM Forms-servern som formuläranvändare.
1. Tryck på **Adobe Experience Manager** i fältet Global navigering.
1. Tryck på verktyg ( ![verktyg](assets/tools.png)) och sedan på **Formulär**.
1. Tryck på **Exportera Correspondence Management Assets**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   (&quot;Sidan Exportera alla resurser för hantering av korrespondenshantering visas med information om den senaste gången som du försökte exportera och en länk för att hämta det senast exporterade paketet.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Tryck på **Exportera** och tryck på **OK** i bekräftelsemeddelandet.

   När en gruppbearbetning har slutförts uppdateras den senaste körningsinformationen och länken för hämtning av paketet. Detta inkluderar information som administratörsinloggning och om batchkörningen lyckades eller misslyckades. Resurserna exporteras till ett paket och länken Hämta exporterade paket visas.

   >[!NOTE]
   >
   >Processen Exportera alla resurser kan inte avbrytas när den har initierats. När exportåtgärden pågår ska du inte skapa, ta bort, ändra eller publicera några resurser eller initiera processen Publicera alla resurser.a

1. Tryck på länken **Hämta exporterat paket** för att hämta paketfilen.

   Om du vill lägga till resurserna i paketet i en annan instans av Correspondence Management, [importerar du paketet till en AEM Forms-instans](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p).

### Importera dokumentfragment, bokstäver och/eller dataregister till Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

Du kan importera resurser som har exporterats till en .cmp-fil. En .cmp-fil kan innehålla en eller flera bokstäver, dataordlistor, dokumentfragment och beroende resurser.

>[!NOTE]
>
>Logga in med ett administratörskonto när du importerar gamla Correspondence Management-resurser för migrering. Mer information om hur du migrerar gamla Correspondence Management-resurser finns i [Migrera Correspondence Management-resurser till AEM 6.1-formulär](/help/forms/using/migration-utility.md).

1. Tryck på **Skapa > Filöverföring** och välj .cmp-filen på sidan med dataordlistor, bokstäver eller dokumentfragment.
1. Korrespondenshantering visar dialogrutan Importera resurser med listan över resurser som importeras. Tryck på **Importera**.

   När du har importerat resurserna uppdateras följande egenskaper för resurserna medan de andra egenskaperna är desamma:

   * Författare: Visar ID:t för användaren som importerade resursen till servern
   * Ändrad: Tidpunkten då resursen importerades till servern
   >[!NOTE]
   >
   >För att du ska kunna överföra XDP-filer (som en del av cmp-filen eller på annat sätt) måste du vara en del av en användargrupp som hanterar formulär. Kontakta administratören om du vill ha åtkomstbehörighet.

## Exportera ett arbetsflödesprogram {#export-a-workflow-application}

Du kan använda AEM-pakethanteraren för att exportera arbetsflödesprogram. Anges nedan:

1. Öppna pakethanteraren för AEM Forms. URL för pakethanteraren är https://&lt;server>:&lt;port>/crx/packmgr.
1. Klicka på **[!UICONTROL Skapa paket]**. The **[!UICONTROL New Package]** dialog box appears.
1. Ange namn, version och grupp för paketet. Click **[!UICONTROL OK]**.
1. Klicka på **[!UICONTROL Redigera]** och öppna fliken **[!UICONTROL Filter]** . Klicka på **[!UICONTROL Lägg till filter]**. Ange sökvägen till arbetsflödesprogrammet. Exempel: /etc/fd/dashboard/startpoints/homemortgage. Klicka på **[!UICONTROL Lägg till regel]**.

1. Öppna fliken **[!UICONTROL Avancerat]** . Välj **[!UICONTROL Sammanfoga]** eller **[!UICONTROL Skriv över]** i fältet ACL-hantering. Click **[!UICONTROL Save]**.
1. Skapa paketet genom att klicka på **[!UICONTROL Skapa]** .

   När paketet har skapats kan du hämta det och importera det till den andra servern. Arbetsflödesprogrammet visas på servern där paketet överförs.

   >[!NOTE]
   >
   >För att arbetsflödesprogrammet ska fungera på rätt sätt kan du även exportera motsvarande anpassningsbara formulär och arbetsflödesmodell med arbetsprogrammet.

## Mappar och ordna resurser {#folders-and-organizing-assets}

AEM Forms användargränssnitt använder mappar för att ordna resurser. De här mapparna används för att ordna resurser som skapats i användargränssnittet i AEM Forms. Du kan byta namn på, skapa undermappar och lagra resurser och dokument i dessa mappar. Genom att ordna dokument och resurser i en mapp kan du gruppera filerna tillsammans för enkel hantering. Du kan markera en mapp och välja att hämta eller ta bort den.

Så här skapar du en mapp:

### Skapa en mapp {#create-a-folder}

1. Logga in i användargränssnittet för AEM Forms på `https://<server>:<port>/aem/forms.html`.
1. Navigera till den plats där du vill skapa en mapp.
1. Tryck på Skapa > Mapp.
1. Ange följande information:

   * **Titel:** Visningsnamn för mappen
   * **Namn:** *(Obligatoriskt)* Det nodnamn under vilket du vill lagra mappen i databasen
   >[!NOTE]
   >
   >Som standard fylls värdet för namnfältet automatiskt i från titeln. Namnet får bara innehålla alfanumeriska tecken eller bindestreck (-) och understreck (_). Alla andra specialtecken som anges i titeln ersätts automatiskt med ett bindestreck och du uppmanas att bekräfta det nya namnet. Du kan välja att fortsätta med det föreslagna namnet eller redigera det ytterligare.

1. En ny mapp med den titel du har definierat visas på den aktuella platsen i resurslistan.

   Om det finns en mapp med det angivna namnet misslyckas överföringen med ett fel. Du kan visa felmeddelandet genom att hovra över ![felikonen aem6forms_error_alert](assets/aem6forms_error_alert.png) som visas bredvid namnfältet.

   Du kan trycka på den nyligen skapade mappen för att gå in i mappen och skapa resurser eller mappar i mappen. Du kan också markera en mapp och välja att placera den i kö för hämtning, ta bort den eller redigera namnet.

   ![editdeletedownloadafolder](assets/editdeletedownloadafolder.png)

### Skapa kopior av en eller flera resurser eller bokstäver {#create-copies-of-one-or-more-assets-or-letters}

Du kan använda befintliga resurser och bokstäver för att snabbt skapa resurser och bokstäver med liknande egenskaper, innehåll och ärvda resurser. Du kan kopiera och klistra in dataordlistor, dokumentfragment och brev.

Följ de här stegen för att skapa kopior av resurser och brev:

1. Markera en eller flera resurser/bokstäver på den relevanta sidan Resurser eller Bokstäver. Gränssnittet visar ikonen Kopiera.
1. Tryck på Kopiera. Gränssnittet visar ikonen Klistra in. Du kan också välja att gå/navigera i en mapp innan du klistrar in. Olika mappar kan innehålla resurser med samma namn. Mer information om mappar finns i [Mappar och ordna resurser](#folders-and-organizing-assets).
1. Tryck på Klistra in. Dialogrutan Klistra in visas. Systemet genererar automatiskt namn och titlar på de nya kopiorna av resurser/bokstäver, men du kan redigera namn och namn på resurserna/bokstäverna.

   Om du kopierar och klistrar in resurserna/bokstäverna på samma plats läggs suffixet&quot;-CopyXX&quot; till i det befintliga namnet på resursen/bokstaven. Om det inte finns någon titel för den kopierade resursen/bokstaven förblir det automatiskt genererade titelfältet tomt.

1. Om det behövs kan du redigera titeln och namnet som du vill spara kopian av resursen/bokstaven med.
1. Tryck på Klistra in. Nya kopior av de kopierade resurserna skapas.

## Sökning {#search-forms}

Med användargränssnittet för AEM Forms kan du söka efter ditt innehåll. I det övre fältet kan du trycka på Sök **[A]** om du vill söka efter resurser och dokument i ditt innehåll.

När du söker efter resurser visas sidopanelen i AEM Forms. Du kan också trycka på ![assets-browser-content-only](assets/assets-browser-content-only.png) > Filter **[B]** för att öppna sidopanelen. Du kan begränsa sökningen med hjälp av de olika filtren på sidopanelen. På sidopanelen kan du också spara dina sökningar.

![search_topbar](assets/search_topbar.png)

**S.** Sök **B.** Filter

![Panelen Sida - Filter](assets/search_sidepanel.png)

Panelen Sida - Filter

På sidopanelen kan du använda följande för att begränsa sökresultaten:

* Sökkatalog
* Taggar
* Sökvillkor; till exempel Ändrade datum, Publiceringsstatus, LiveCopy-status.

På sidopanelen kan du också spara sökinställningarna med valfria namn.

Mer information och instruktioner om hur du använder sökningar, filter, sparad sökning och sidopanelen finns i [Sök](/help/sites-authoring/search.md).
