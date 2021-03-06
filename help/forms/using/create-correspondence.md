---
title: Skapa korrespondens
seo-title: Skapa korrespondens
description: När du har skapat en brevmall kan du använda den för att skapa korrespondens i AEM Forms genom att hantera data, innehåll och bilagor.
seo-description: När du har skapat en brevmall kan du använda den för att skapa korrespondens i AEM Forms genom att hantera data, innehåll och bilagor.
uuid: 48cf2b26-c9b4-4127-9ea0-1b36addbff60
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 87742cb2-357b-421f-b79d-e355887ddec0
docset: aem65
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3701'
ht-degree: 0%

---


# Skapa korrespondens{#create-correspondence}

## Skapa korrespondens i användargränssnittet Create Correspondence {#create-correspondence-in-the-create-correspondence-user-interface}

När en [brevmall har skapats i Correspondence Management](../../forms/using/create-letter.md) kan slutanvändaren/agenten/anspråksjusteraren öppna brevet i användargränssnittet Skapa korrespondens och skapa en korrespondens genom att ange data, konfigurera innehåll och hantera bilagor. Slutligen kan anspråksjusteraren eller agenten hantera innehållet i förhandsgranskningsläget och skicka brevet.

### Förhandsgranska korrespondens {#preview-a-correspondence}

Markera den bokstav du vill förhandsgranska genom att följa följande steg:

1. Tryck på **Välj** på sidan Bokstäver.
1. Välj lämplig bokstav genom att trycka på den.

   ![Markera brev](assets/1_selectletter.png)

   Markera brev

1. Om du har en dataordlistebaserad bokstav väljer du **Förhandsgranska** > **Förhandsgranska**. Du kan också välja en annan bokstav än en ordlista genom att välja **Förhandsgranska**. Du kan också hålla pekaren över en bokstav (utan att markera den) och förhandsgranska den genom att trycka på ikonen Förhandsgranska brev.

   >[!NOTE]
   >
   >Om ett datalexikon inte är associerat med bokstaven visas förhandsgranskningen av bokstaven. Om bokstaven är dataordlistebaserad visar Korrespondenshantering alternativen Förhandsvisa och Anpassad på menyn Förhandsvisa och du kan välja ett av de två alternativen. Du kan också koppla testdata till en datamordlista. När [Data Dictionary har associerade testdata](../../forms/using/data-dictionary.md#p-working-with-test-data-p) öppnas den normala förhandsvisningen när du väljer förhandsvisningsalternativet med testdata ifyllda.

1. Om du vill kunna återge en korrespondens medan du förhandsgranskar den, bör du antingen vara administratör eller en del av någon av följande grupper:

   * formulär-användare (för förhandsgranskning på författarinstans)
   * cm-agent-users (för återgivning vid publicering)

   Om du inte har de behörigheter som krävs ber du administratören om rätt åtkomst. Mer information om hur du skapar och lägger till användare i grupper finns i [Lägga till användare eller grupper i en grupp](/help/sites-administering/security.md). Om du försöker återge en korrespondens utan att ha rätt behörighet visas felsidan 404.

1. Om du har valt **Förhandsgranska** > **Anpassad** öppnas en dialogruta. I dialogrutan markerar du en datafil, som motsvarar dataordlistan, som du vill förhandsgranska bokstaven med och väljer sedan **Förhandsgranska**. En datafil skapas baserat på ett datalexikon för en viss bokstav. Mer information om datafilen finns i [Dataordlista](../../forms/using/data-dictionary.md#p-working-with-test-data-p).

   ![Förhandsgranska brev](assets/8_previewcustomdatafile.png)

1. Bokstaven HTML-förhandsgranskning (förhandsgranskning av mobilformulär) öppnas som standard med fliken Data i fokus.

   Mer information om mobilformulär och vilka funktioner de stöder finns i [Funktionsdifferentiering mellan Mobile Forms och PDF forms](https://helpx.adobe.com/livecycle/help/mobile-forms/feature-differentiation-mobile-forms-pdf.html).

   Det finns tre flikar: data, innehåll och bilagor. Om det inte finns några dataelement (platshållarvariabler och layoutfält) öppnas bokstaven direkt i med fliken Innehåll. Fliken Bifogade filer är bara tillgänglig när det finns bifogade filer eller när biblioteksåtkomst är aktiverat.

   >[!NOTE]
   >
   >Mer information om hur du växlar mellan HTML- och PDF-återgivningsläget för förhandsgranskning av bokstav finns i [Ändra återgivningsläget för bokstaven](#changerenditionmode). Mer information om PDF-stöd i Correspondence Management och AEM finns i [Avbrutet av webbläsarplugin-program för NPAPI och dess påverkan](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html) och [PDF forms till HTML5 Forms](https://helpx.adobe.com/aem-forms/kb/pdf-forms-to-html5-forms.html).

### Ange data {#enterdata}

Fyll i de tillgängliga layoutfälten och platshållarna på fliken Data.

1. Ange data- och innehållsvariablerna i fälten efter behov. Fyll i alla obligatoriska fält som är markerade med en asterisk (*) för att aktivera knappen **Skicka**.

   Tryck på ett datafältvärde i förhandsvisningen av HTML-bokstaven för att markera motsvarande datafält på fliken Data.

   ![Ange data i bokstaven](assets/2_enterdata.png) ![2_1_enterdata](assets/2_1_enterdata.png)

### Hantera innehåll {#managecontent}

På fliken Innehåll hanterar du innehåll som dokumentfragment och innehållsvariabler i brevet.

1. Välj **Innehåll**. Korrespondenshanteringen visar fliken Innehåll i brevet.

   ![Fliken Innehåll - markera modul i innehåll](assets/3_content.png)

1. Redigera innehållsmodulerna efter behov på fliken Innehåll. Om du vill fokusera på den relevanta innehållsmodulen i innehållshierarkin kan du antingen trycka på den relevanta raden eller det relevanta stycket i förhandsgranskningen av bokstaven eller trycka på innehållsmodulen direkt i innehållshierarkin.

   Till exempel raden&quot;Vi har granskat.. &quot; är markerat i bilden nedan och den relevanta innehållsmodulen är markerad på fliken Innehåll.

   ![4_highlightmoduleincontent](assets/4_highlightmoduleincontent.png)

   Genom att trycka på Markera valda moduler ( ![highlightselectedModulesincontentccr](assets/highlightselectedmodulesincontentccr.png)) längst upp till vänster i förhandsvisningen av HTML-bokstaven på fliken Innehåll eller Data kan du inaktivera eller aktivera funktioner för att gå till modulen Innehåll/data när relevant text, stycke eller datafält är markerat i förhandsvisningen av bokstaven.

   Mer information om vilka åtgärder som är tillgängliga för olika moduler i användargränssnittet Create Correspondence finns i [Åtgärder och information i användargränssnittet Create Correspondence](#actions-and-info-available-in-the-create-correspondence-content-tab).

1. Om du vill söka efter innehållsmoduler använder du fältet Sök. Ange det fullständiga eller delvisa namnet eller titeln på innehållsmodulen för att söka efter den i korrespondensen.
1. Tryck på visningsikonen ( ![visa](assets/display.png)) framför en lista, text, villkor eller målområde för att visa eller dölja den i bokstaven.
1. Om du vill redigera en textbunden eller redigerbar textmodul trycker du på motsvarande **redigeringsikon ( ![redigeringsmodul](assets/edittextmodule.png)) eller dubbelklickar på motsvarande textmodul i förhandsvisningen av bokstaven.**

   Systemet visar en textredigerare för att redigera och formatera texten.

   Standardstavningskontrollen i webbläsaren kontrollerar stavningen i textredigeraren. Om du vill hantera stavnings- och grammatikkontrollen kan du redigera stavningskontrollinställningarna i webbläsaren eller installera plugin-program/tillägg för webbläsaren för att kontrollera stavning och grammatik.

   Du kan också använda de olika kortkommandona i textredigeraren för att hantera, redigera och formatera text. Mer information om [kortkommandon för textredigeraren](/help/forms/using/keyboard-shortcuts.md#correspondence-management) i Kortkommandon för korrespondenshantering.

   ![5_edittextmodule](assets/5_edittextmodule.png)

   Du kanske vill återanvända ett av flera textstycken som finns i ett annat dokumentprogram. Du kan kopiera och klistra in text direkt, till exempel från MS Word, HTML-sidor eller andra program.

   Du kan kopiera och klistra in ett eller flera textstycken i en redigerbar textmodul. Du kan t.ex. ha ett MS Word-dokument med en punktlista över godkända bevis för uppehälle, som följande:

   ![pastetextmsword](assets/pastetextmsword.png)

   Du kan kopiera och klistra in texten direkt från MS Word-dokumentet i en redigerbar textmodul. Formateringen som punktlistor, teckensnitt och textfärger behålls i textmodulen.

   ![pastetexteditablemodul](assets/pastetexteditablemodule.png)

   >[!NOTE]
   >
   >Formateringen av inklistrad text har dock vissa [begränsningar](https://helpx.adobe.com/aem-forms/kb/cm-copy-paste-text-limitations.html).

   Du kan dra in text och siffror i brevet med tabbtangenten. Du kan till exempel använda tabbtangenten för att justera flera textkolumner i en lista till ett tabellformat.

   ![tabbar](assets/tabspaces.png)

   Exempel: Använda tabbtangenten för att justera flera textkolumner i ett tabellformat

   >[!NOTE]
   >
   >Mer information om hur du ställer in tabbavstånd för textmoduler och bokstäver finns i [Mer information om hur du använder tabbavstånd för att ordna text](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).

1. Infoga vid behov specialtecken i korrespondensen. Du kan till exempel använda paletten Specialtecken för att infoga:

   * Valutasymboler som €,¥ och £
   * Matematiska symboler som t.ex.¥, Ð och ^
   * Interpunktionssymboler som ‟ och&quot;

   ![specialtecken](assets/specialcharacters.png)

   Correspondence Management har inbyggt stöd för 210 specialtecken. Administratören kan [lägga till stöd för fler/anpassade specialtecken genom anpassning](../../forms/using/custom-special-characters.md).

1. Markera texten och tryck på Markera färg om du vill framhäva delar av texten i en redigerbar textbunden modul.

   ![letterbakgrundsfärg](assets/letterbackgroundcolor.png)

   Du kan antingen trycka direkt på en grundfärg `**[A]**` som finns på paletten Grundfärger eller trycka på **Välj** efter att du har använt reglaget `**[B]**` för att välja rätt färgton.

   Du kan också gå till fliken Avancerat och välja lämplig nyans, ljushet och mättnad `**[C]**` för att skapa den exakta färgen och sedan trycka på Välj `**[D]**` för att använda färgen för att markera texten.

   ![textbakgrundsfärg](assets/textbackgroundcolor.png)

1. Gör önskade ändringar av innehåll och format och tryck på **Spara**. Tryck på ![editnextmodulecr](assets/editnextmoduleccr.png) om du vill gå mellan redigerbara textmoduler, eller tryck på **Save and Next** om du vill spara ändringarna och gå till nästa redigerbara textmodul.
1. Systemet visar också de ofyllda variablerna för var och en av grenarna. Om det inte finns några ofyllda variabler visas ofyllda variabler som 0. Om det finns en ofylld variabel kan du trycka på en gren för att expandera den och leta reda på den ofyllda variabeln. Använd verktygsfältet Innehåll för att ta bort innehåll, öka/minska indrag för innehållet och infoga sidbrytningar före/efter innehållet.

   Du kan infoga sidbrytningar ovanför och under datamoduler även när de ingår i listor och villkor.

1. Tryck på Öppna/stäng innehållsvariabel ( ![opencontentvariables](assets/opencontentvariables.png)) för att öppna innehållsvariablerna och fylla i dem korrekt.
1. När du har fyllt i den ofyllda variabeln korrekt anges antalet ofyllda variabler till 0.

   I användargränssnittet Skapa korrespondens visas det ofyllda variabelantalet på varje nivå i hierarkin för en modul som innehåller minst en variabel. Om en modul innehåller ofyllda variabler visas antalet på variabel-, modul-, målområdes- och brevmallsnivå.

   Antal ofyllda variabler inkluderar:

   * Endast oskyddade dataordliste- och platshållarvariabler. Variabelantalet innehåller inte layoutvariabler eller variabler för skyddade dataordlistor.
   * Obligatoriska fält.
   * Layoutfält om de är obligatoriska och bundna till användaren.
   * Endast unika variabelinstanser. Om en modul, målområde eller brevmall innehåller två eller flera instanser av samma variabel, visas antalet som 1 (en). För var och en av förekomsterna visas dock antalet som 1.

   Antal ofyllda variabler inkluderar inte avmarkerade moduler. Om en modul ingår i en brevmall men inte i bokstaven visas inte antalet ofyllda variabler i den här modulen.

   För målområdet, modulen och variabeln visas antalet till höger om varje objekt i bokstavsmallen. För den fullständiga mallen visas dock antalet i statusfältet Skapa korrespondens.

   Modulerna i en brevmall visar det ofyllda variabelantalet enligt beskrivningen nedan:

   * **** TextVisar summan av de unika platshållarvariablerna och dataordlisteelementen i textmodulen.
   * **** VillkorVisar summan av de unika ofyllda villkorsvariablerna i villkoret och variablerna i de resulterande modulerna.
   * **List** Visar summan av alla unika ofyllda variabler som finns i modulerna som är tilldelade till listan.
   * **MålområdeVisar** summan av alla unika ofyllda variabler som finns i modulerna som tilldelats målområdet.

   Observera följande när det gäller variabler med standardvärden:

   * Ett booleskt variabelfält har som standard *false*. Variabeln anses dock vara ofylld. Det innebär att variabelantalet innehåller alla booleska variabelfält med värdet *false*.

   * Ett numeriskt variabelfält har standardvärdet *0 (noll)*. Variabeln anses dock vara ofylld. Det innebär att variabelantalet innehåller alla numeriska variabelfält med värdet *0 (noll)*.



#### Åtgärder och information som är tillgängliga på fliken Skapa korrespondensinnehåll {#actions-and-info-available-in-the-create-correspondence-content-tab}

**Målområde**

* Infoga tom rad: Infogar en ny tom rad.
* Infoga textbunden text: Infogar ny textmodul.
* Orderlås (info): Anger att ordningen för innehållet inte kan ändras.
* Ofyllda värden (info): Anger antalet ofyllda variabler i målområdet.

**Modul**

* Markering (ögonikon): Inkluderar\exkluderar modul från brevet.
* Hoppa över punkter (gäller för listmoduler och deras underordnade moduler): Hoppar över punkter i en viss modul.
* Sidbrytning före (gäller för underordnade moduler i målområdet): Infogar sidbrytning före modulen.
* Sidbrytning efter (gäller för underordnade moduler i målområdet): Infogar sidbrytning före modulen.
* Ofyllda värden (info): Anger antalet ofyllda variabler i målområdet.
* Redigera (endast textmoduler): Öppna RTF-redigeraren för att redigera textmodulen.
* Datapanelen (text- och villkorsmoduler): Öppna alla variabler i modulen.

**Listmodul**

* Infoga tom rad: Infogar en ny tom rad.
* Innehållsbibliotek: Öppnar innehållsbiblioteket för att lägga till moduler i listan.
* Listinställning (endast kapslad lista):
* Orderlås (info): Anger att ordningen för listobjekten inte kan ändras.

### Hantera bifogade filer {#manage-attachments}

1. Välj **Bifogade filer**. Korrespondenshanteringen visar de tillgängliga bifogade filerna, enligt inställningarna när brevmallen skapas.
1. Du kan välja att inte skicka en bifogad fil tillsammans med bokstaven genom att trycka på visningsikonen och du kan trycka på krysset i den bifogade filen för att ta bort den från bokstaven. För de bifogade filer som anges inaktiveras ikonerna Visa och Ta bort när du skapar en brevmall som Obligatorisk.
1. Tryck på biblioteksåtkomstikonen ( ![biblioteksåtkomst](assets/libraryaccess.png)) för att komma åt innehållsbiblioteket för att infoga DAM-resurser som bilagor.

   >[!NOTE]
   >
   >Ikonen Biblioteksåtkomst är bara tillgänglig när biblioteksåtkomst aktiverades när brevet redigerades.

1. Om ordningen på de bifogade filerna inte var låst när du skapade korrespondensen kan du ändra ordningen på de bifogade filerna genom att markera en bifogad fil och trycka på upp- och nedpilarna.

   Mer information finns i [Leverans av bifogad fil](#attachmentdelivery).

### Hantera innehåll i förhandsgranskning och skicka bokstaven {#manage-content-in-preview-and-submit-the-letter}

Du kan göra layout- och innehållsrelaterade ändringar för att se till att brevet ser ut som du tänkt dig och skicka det till olika postprocesser.

1. Om du vill markera allt redigerbart innehåll i brevet trycker du på **Markera redigerbara avsnitt**.

   Det redigerbara innehållet i bokstaven markeras med grå bakgrund.

   ![Markera redigerbart innehåll](assets/4_highlightmoduleincontent-1.png)

1. Redigera innehållsmodulerna efter behov på fliken Innehåll. Om du vill fokusera på den relevanta innehållsmodulen i innehållshierarkin kan du antingen trycka på den relevanta raden eller det relevanta stycket i förhandsgranskningen av bokstaven eller trycka på innehållsmodulen direkt i innehållshierarkin.

   Till exempel raden &quot;Att ge oss åtkomst..&quot; är markerat i bilden nedan och motsvarande innehållsmodul är markerad på fliken Innehåll.

   Genom att trycka på Markera valda moduler i innehåll ( ![highlightselectedModulesincontentccr](assets/highlightselectedmodulesincontentccr.png)) kan du inaktivera eller aktivera funktioner för att markera innehållsmodulen på fliken Innehåll när användaren knackar på relevant text, stycke eller datafält i förhandsgranskningen av bokstaven.

   Mer information om vilka åtgärder som är tillgängliga för olika moduler i användargränssnittet Create Correspondence finns i [Åtgärder och information i användargränssnittet Create Correspondence](#actions-and-info-available-in-the-create-correspondence-content-tab).

1. Om du vill lägga till en sidbrytning i brevet trycker du där du vill infoga en sidbrytning och väljer Sidbrytning före eller Sidbrytning efter ( ![sidbrytning före](assets/pagebreakbeforeafter.png)).

   En explicit sidbrytningsplatshållare infogas i brevet. Om du vill se hur en explicit sidbrytning påverkar bokstaven läser du i den förenklade PDF-förhandsgranskningen.

   >[!NOTE]
   >
   >Eftersom mobilformulär inte stöder sidbrytningar visas bara sidhuvuden och sidfötter en gång. Du kan dock uttryckligen ange att sidhuvuden och sidfötter i layouten (per sida) ska visas i förhandsvisningen av mobilformulär. Eventuella tomma sidor i brevet visas inte heller i förhandsgranskningen av mobilformulär.

   ![Explicit sidbrytning](assets/8_pagebreak.png)

1. Om du vill spara brevet som ett utkast, som du kan fortsätta att arbeta med senare, trycker du på Spara som utkast. Om du vill använda det här alternativet måste ditt brev vara [publicerat](../../forms/using/publishing-unpublishing-forms.md#publishanasset). Mer information finns i Utkastinstans under [Spara utkast och skicka bokstavsinstanser](#savingdrafts).

   ![saveasdraft](assets/saveasdraft.png)

   Dialogrutan Utkastbokstavsnamn visas med bokstavskod-ID. Du kan också redigera detta ID. Anteckna bokstaven-ID och tryck sedan på **Klar**. Du kan använda det här ID:t senare för att [läsa in utkastet till brev](submit-letter-topostprocess.md#reloaddraft) igen.

1. Om du vill förhandsgranska bokstaven som en förenklad PDF-fil med exakt layout och sidbrytningar så som den kommer att skickas, trycker du på ( ![preview](assets/preview.png)) Preview.

   Bokstaven visas som en förenklad PDF-fil. Den förenklade PDF-filen är den exakta representationen av brevet så som det kommer att skickas med rätt teckensnitt, brytningar och layout för brevet.

   >[!NOTE]
   >
   >Om du använder Mozilla Firefox- och HTML-återgivningstypen och vill förhandsgranska bokstaven som en förenklad PDF-fil måste du använda det inbyggda plugin-programmet för webbläsaren och inte plugin-programmet för Acrobat. Om du vill välja insticksprogrammet för webbläsaren går du till inställningarna för Mozilla Firefox och väljer Förhandsgranska i Firefox för innehållstypen PDF.

1. Om du tycker att den förenklade PDF-förhandsgranskningen är tillräcklig trycker du på **Skicka** för att skicka brevet. Du kan också ändra brevet genom att trycka på **Avsluta förhandsgranskning** för att gå tillbaka till förhandsgranskningen av brevet för att skapa korrespondens för att göra ändringar i brevet. När du trycker på Submit (Skicka), om konfigurationen Hantera bokstavsinstans är aktiverad på Publish-instansen, genereras instansen för att skicka brev.

   Mer information finns i Utkastinstans under Spara utkast och skicka brevinstanser.

   Du kan också spara brevet som ett utkast om du vill ändra det senare.

   När du har gjort de ändringar du vill kan du antingen skicka brevet från HTML5-förhandsgranskningen eller trycka på Förhandsgranska igen för att granska den förenklade PDF-utdatafilen.

   Mer information om skillnader mellan HTML5-formulär och PDF forms finns i [Funktionsskillnad mellan HTML5-formulär och PDF forms](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

## Spara utkast och skicka brev {#savingdrafts}

När ett brev återges i användargränssnittet Skapa korrespondens kan du spara brevet som om det visas.

Det finns två typer av bokstavsinstanser som kan sparas: Utkastinstans och Skicka-instans.

* **Utkastinstans**: Utkastinstansen fångar det aktuella läget för den bokstav du förhandsgranskar. Om du vill spara en utkastinstans måste du först kontrollera att bokstaven och alla resurser som den refererar till är i publicerat läge. Mer information om publicering av brev finns i [Publicera en resurs](../../forms/using/publishing-unpublishing-forms.md#publishanasset). Du måste publicera ett brev innan du kan spara det som ett utkast, eftersom du när du publicerar ett brev skapar en version av brevet, dess beroende resurser och data vid den tidpunkten. Den publicerade versionen av ett brev kan inte redigeras av dig eller en annan användare och kan återställas senare utan oväntade avvikelser från den publicerade versionen. Du kan gå tillbaka till den här instansen senare och fortsätta därifrån du gick.

* **Skicka instans**: Submit-förekomster används för att hämta status för brevet när det skickas. Instansen Submit lagrar PDF-läget för bokstavsinstansen efter att den har efterbearbetats tillsammans med de data som anges av användaren i användargränssnittet Create Correspondence.

Sådana instanser kan bara sparas när brevet visas på en publiceringsinstans. Som standard är sparandet av instanser inaktiverat. Gör så här om du vill att instanser av bokstäver ska kunna sparas:

1. I AEM öppnar du Adobe Experience Manager Web Console Configuration för servern med följande URL: https://&lt;server>:&lt;port>/&lt;kontextsökväg>/system/console/configMgr
1. Leta reda på **[!UICONTROL Correspondence Management Configurations]** och klicka på den.
1. Kontrollera **[!UICONTROL Manage Letter Instances on Publish]**-konfigurationen och klicka sedan på **[!UICONTROL Save]**.

När du har aktiverat funktionen för att spara bokstäver kan du välja var du vill spara bokstavsinstanserna. Det finns två alternativ för att spara bokstavsinstanser: Spara lokalt eller Fjärrspara.

### Spara lokalt {#local-save}

Bokstavsinstanser sparas på publiceringsinstansen och replikeras omvänt på författarinstansen.

### Spara {#remote-save}

Det här alternativet finns för personer som har problem med att spara användardata vid publiceringsinstanser, vilket vanligtvis är utanför företagets brandvägg. När fjärrsparning är aktiverat sparas inte bokstavsinstanserna i publiceringsinstansen, men de sparas på fjärrbasis på den bearbetningsförfattare som har angetts via SDK-konfigurationerna för LiveCycle-klienten.

#### Aktivera fjärrsparning {#enable-remote-save}

1. I AEM öppnar du Adobe Experience Manager Web Console Configuration för servern med följande URL: `https://<server>:<port>/<contextpath>/system/console/configMgr`
1. Sök efter **[!UICONTROL Correspondence Management Configurations]** och klicka på den.
1. Leta reda på konfigurationen **[!UICONTROL Remote Save]**, kontrollera den och klicka sedan på **[!UICONTROL Save]**.

#### Ange inställningar för bearbetningsförfattare {#specify-processing-author-settings}

1. I AEM öppnar du Adobe Experience Manager Web Console Configuration för servern med följande URL: `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![Konfiguration av Adobe Experience Manager Web Console](assets/2configmanager.png)

1. På den här sidan letar du upp SDK-konfigurationen för LiveCycle-klienten och expanderar den genom att klicka på den.

1. Ange namnet på servern, ange inloggningsinformationen och klicka sedan på **Spara** i URL:en för bearbetningsservern.

   ![Ange namn och inloggningsinformation för LiveCycle-servern](assets/3configmanager.png)

1. Ange vid behov användarnamnet och lösenordet som du vill använda för att få åtkomst till servern.

#### Leverans av bifogad fil {#attachmentdelivery}

* Brevbilagor är tillgängliga efter postprocessen i PDF-filen, som skapas efter att brevet skickats in.
* När brevet återges med hjälp av API:er på serversidan som en interaktiv eller icke-interaktiv PDF, innehåller den återgivna PDF-filen bifogade filer som PDF-bilagor.
* När en inläggsprocess som är kopplad till en brevmall läses in som en del av åtgärderna Skicka eller Fullständig korrespondens med användargränssnittet Skapa korrespondens, skickas bilagor som List&lt;com.adobe.idp.Document> i parametern AttachmentDocs.
* Färdiga leveransmekanismer som e-post och utskrift, levererar också bilagor tillsammans med PDF-filen med den genererade korrespondensen.

## Återgivningslägen för förhandsgranskning av brev: Förhandsgranskning av mobilformulär och PDF-förhandsgranskning {#rendition-modes-of-letter-preview-mobile-forms-preview-and-pdf-preview}

AEM Forms Correspondence Management visar en bokstav som HTML i användargränssnittet Create Correspondence. Korrespondenshanteringen har dock fortfarande stöd för att återgå till PDF-förhandsgranskning i stället för HTML-förhandsgranskning. Mer information om hur du växlar mellan förhandsgranskningsläget HTML och PDF finns i [Ändra återgivningsläget för bokstaven](#changerenditionmode).

Nedan följer de fördelar och funktioner som finns i HTML- och PDF-förhandsgranskning.

**Fördelar med mobilformulär/HTML-förhandsgranskning**

* **Tryck på ett datafältvärde för att markera motsvarande datafält**: I användargränssnittet Skapa korrespondens kan du trycka på ett datafältvärde i brevet för att markera motsvarande datafält på fliken Data. Mer information finns i [Ange data](#enterdata).

* **Stöd** för webbläsare: Webbläsare: ett stöd för att dra tillbaka NPAPI gradvis, vilket påverkar PDF-förhandsgranskning av brev. Förhandsgranskning av brev i HTML-/mobilformulär påverkas inte av detta.
* **Markera redigerbart innehåll i en bokstav**: I användargränssnittet Skapa korrespondens kan du trycka på Markera redigerbart innehåll för att markera allt redigerbart innehåll i brevet i grått. Mer information finns i [Hantera innehåll](#managecontent).

`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`
`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`  **Fördelar med PDF-förhandsgranskning**

* **Sidbrytning**: I PDF-förhandsgranskningen kan du se exakt hur sidbrytningarna i brevet påverkar utdata.
* **Slutlig förhandsgranskning**: I PDF-förhandsgranskningen kan du visa den exakta formateringen och utseendet på brevet så som det kommer att se ut i utskriften.

Mer information om skriptstöd i PDF forms finns i [Skriptstöd](https://help.adobe.com/en_US/livecycle/11.0/ScriptingSupport/index.html).

Mer information om skriptstöd i HTML5-formulär finns i [Skriptstöd för HTML5-formulär](/help/forms/using/scripting-support.md).

### Ändra återgivningsläge för bokstaven {#changerenditionmode}

Som standard använder gränssnittet Skapa korrespondens HTML- eller mobilformulär för att återge förhandsgranskningen av bokstaven. Förhandsgranskningen av mobilformulär har inga problem med återgivningen i någon webbläsare, eftersom webbläsarens inbyggda plugin-program används och inga ytterligare plugin-program krävs. Du kan ändra förhandsgranskningsläget för brev till PDF. Webbläsarbegränsningar kan dock skapa problem för olika funktioner i den interaktiva PDF-förhandsgranskningen av brevet.

Mer information om webbläsarkompatibilitet med förhandsgranskning av brev finns i [Avbryta plugin-program för NPAPI-webbläsare och dess effekt](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html).

Om du vill ändra förhandsgranskningsläget för brevet utför du följande steg:

1. Gå till `https://[system]:'port'/system/console/configMgr` och logga in som administratör om det behövs.
1. Gå till **[!UICONTROL Correspondence Management Configurations]** > **[!UICONTROL Rendition Type]** och välj **HTML-återgivning** (standard) eller **PDF-återgivning**.
1. Klicka på **[!UICONTROL Save]**.

