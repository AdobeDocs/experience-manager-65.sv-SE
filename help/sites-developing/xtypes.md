---
title: Använda xtypes (Classic UI)
seo-title: Använda xtypes (Classic UI)
description: Läs mer om alla typer som är tillgängliga med AEM
seo-description: Läs mer om alla typer som är tillgängliga med AEM
uuid: 6497caa4-2f9b-4f21-9023-88d485fd1d78
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: adb70b43-1b0b-4302-905a-c7612675dabb
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Använda xtypes (Classic UI){#using-xtypes-classic-ui}

På den här sidan beskrivs alla typer som är tillgängliga med Adobe Experience Manager (AEM).

I ExtJS-språket är en xtype ett symboliskt namn som ges till en klass. Du kan läsa stycket&quot;Component XTypes&quot; i [översikten över ExtJS 2](https://www.sencha.com/learn/overview-of-extjs-2) för en detaljerad förklaring av vad en xtype är och hur den kan användas.

En fullständig information om alla tillgängliga widgetar i AEM finns i [widgetens API-dokumentation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

Om du vill ta reda på i vilka komponenter en viss Xtype används i AEM kan du använda följande Xpath-fråga i CRXDE genom att ersätta &quot;checkbox&quot; med den Xtype som du är intresserad av:

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>Den här sidan beskriver användningen av ExtJS-xtyper i det klassiska användargränssnittet.
>
>Adobe rekommenderar att du använder det moderna, [pekaktiverade användargränssnittet](/help/sites-developing/touch-ui-concepts.md) som är standard, baserat på användargränssnittet i [Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui) och användargränssnittet i [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

## xtypes {#xtypes}

Nedan finns en lista över tillgängliga typer i Adobe Experience Manager:

* anteckning

   [CQ.wcm.Anteckning](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Annotation)

   Dialogrutan är en speciell typ av fönster med ett formulär i brödtexten och en knappgrupp i sidfoten. Det används vanligtvis för att redigera innehåll, men kan även visa information.

* arraystore

   [CQ.Ext.data.ArrayStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayStore)

   Kallas tidigare&quot;SimpleStore&quot;.

   Liten hjälpklass som gör det enklare att skapa [CQ.Ext.data.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)Stores från Array-data. En ArrayStore konfigureras automatiskt med en [CQ.Ext.data.ArrayReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayReader).

* Asseteditor

   [CQ.dam.AssetEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.AssetEditor)

   Resursredigeraren som används i DAM Admin.

* assetreferenskoncesearchdialog

   [CQ.wcm.AssetReferenceSearchDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.AssetReferenceSearchDialog)

   AssetReferenceSearchDialog är en dialogruta som visas om en sida refererar till resurser eller taggar.

* blueprintconfig

   [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig)

   I BlueprintConfig finns en panel där du kan visa live-kopior av en utkast och redigera dessa blå egenskaper (synkroniseringsutlösare och synkroniseringsåtgärder ).

* blueprintstatus

   [CQ.wcm.msm.BlueprintStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus)

   Med BlueprintStatus kan du visa och redigera en utkast och dess Live-kopior-relationer. Bläddringen görs via en [CQ.wcm.msm.BlueprintStatus.Tree](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus.Tree)-utgåva via en [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig) och en [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties).

* box

   [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent)

   Basklass för alla [komponenter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component) som ska storleksanpassas som en ruta, med bredd och höjd.

   BoxComponent har automatiska rutmodelljusteringar för storlek och placering och fungerar korrekt i komponentåtergivningsmodellen.

* bläddringsdialogruta

   [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog)

   Med BrowseDialog kan användaren bläddra i databasen för att välja en sökväg. Det används vanligtvis via ett [BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField).

* webbläsarfält

   [CQ.form.BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField)

   **Föråldrat: Använd[CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)i stället**

* bulkeditor

   [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)

   I BulkEditor finns en sökmotor och ett rutnät som du kan använda för att redigera sökresultat.

   BulkEditor måste infogas i ett HTML-formulär (krävs för importfunktioner). Detta fungerar perfekt med en [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* bulkeditorform

   [CQ.wcm.BulkEditorForm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditorForm)

   BulkEditorForm innehåller [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor) omgivet av ett HTML-formulär. Det här är den fristående versionen av [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor). HTML-formulär krävs för importknappen.

* button

   [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)

   Klassen Simple Button

* knappgrupp

   [CQ.Ext.ButtonGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ButtonGroup)

   Behållare för en grupp knappar.

* diagram

   [CQ.Ext.chart.Chart](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart)

   Paketet CQ.Ext.chart ger möjlighet att visualisera data med flash-baserade diagram. Varje diagram binds direkt till en CQ.Ext.data.Store som möjliggör automatiska uppdateringar av diagrammet. Information om hur du ändrar utseendet på ett diagram finns i [konfigurationsalternativen chartStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) och [extraStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) .

*  kryssruta

   [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox)

   Ett kryssrutefält. Kan användas som ersättning för traditionella kryssrutefält.

* kryssrutegrupp

   [CQ.Ext.form.CheckboxGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.CheckboxGroup)

   En grupperingsbehållare för kontrollerna [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox) .

* klarkombino

   [CQ.form.ClearableComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ClearableComboBox)

   ClearableComboBox är en icke-redigerbar kombinationsruta med en utlösare som rensar dess värde.

* färgfält

   [CQ.form.ColorField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorField)

   Med ColorField kan användaren ange ett hex-färgvärde antingen direkt eller med [CQ.Ext.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorMenu).

* färglista

   [CQ.form.ColorList](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorList)

   Med ColorList kan användaren välja en färg i en redigerbar lista.

* färgmeny

   [CQ.Ext.menu.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.ColorMenu)

   En meny som innehåller en [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette) -komponent.

* färgpalett

   [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette)

   Enkel färgpalettklass för att välja färger. Paletten kan återges i vilken behållare som helst.

* kombinera

   [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)

   En kombinationsruta med stöd för automatisk komplettering, fjärrinläsning, sidinläsning och många andra funktioner.

   En ComboBox fungerar på ungefär samma sätt som ett vanligt HTML-fält med namnet &lt;select>. Skillnaden är att om du vill skicka [valueField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)måste du ange ett [hiddenName](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) för att skapa en dold inmatning.

* komponent

   [CQ.Ext.Component](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)

   Basklass för alla Ext-komponenter. Alla underklasser till Component kan delta i den automatiska EXT-komponentlivscykeln för att skapa, återge och destruera som tillhandahålls av [klassen Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) . Komponenter kan läggas till i en behållare med hjälp av alternativet [items](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) config när behållaren skapas.

* componentExtractor

   [CQ.wcm.ComponentExtractor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ComponentExtractor)

   Med ComponentExtractor kan användaren extrahera komponenter från en webbplats/sida.

* komponentväljare

   [CQ.form.ComponentSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentSelector)

   En grupperad, ordnad markering med tillgängliga komponenter.

* komponentmallar

   [CQ.form.ComponentStyles](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentStyles)

* compositefield

   [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)

   Basklass för panelbaserade, komplexa formulärfält som innehåller ett formulärfält eller en grupp av formulärfält.

* container

   [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)

   Basklass för alla [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent) som kan innehålla andra komponenter. Behållare hanterar grundbeteendet för objekt som innehåller objekt, nämligen att lägga till, infoga och ta bort objekt.

   De vanligaste behållarklasserna är [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel), [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) och [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel).

* contentfinder

   [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)

   ContentFinder är en speciell [visningsruta](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport) med två kolumner som innehåller den faktiska innehållssökaren till vänster och innehållsramen till höger.

* innehållfinderflik

   [CQ.wcm.ContentFinderTab](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinderTab)

   ContentFinderTab är en specialpanel med funktioner som används i flikpanelerna i [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder). Vanligtvis innehåller den ett sökformulär - rutan Fråga - och en datavy för att visa sökningen.

* cq.workflow.model.combo

   [CQ.wcm.WorkflowModelCombo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelCombo)

   WorkflowModelCombo är en anpassad [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) som visar en lista över tillgängliga arbetsflödesmodeller.

* cq.workflow.model.selector

   [CQ.wcm.WorkflowModelSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelSelector)

   WorkflowModelSelector kombinerar en WorkflowModelCombo med en miniatyrbild av arbetsflödet och knappar för att skapa och redigera arbetsflödesmodeller.

* createsiteguide

   [CQ.wcm.CreateSiteWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateSiteWizard)

   CreateSiteWizard är en steg-för-steg-guide för att skapa (MSM) platser.

* createversiondialog

   [CQ.wcm.CreateVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateVersionDialog)

   CreateVersionDialog är en dialogruta där du kan skapa en ny version av en sida.

* anpassad innehållpanel

   [CQ.CustomContentPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.CustomContentPanel)

   CustomContentPanel är en särskild panel som används i [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog): Innehållet hämtas från och skickas till en annan URL än de andra fälten i dialogrutan.

* cykel

   [CQ.Ext.CycleButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton)

   En specialiserad SplitButton som innehåller en meny med [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem) -element. Knappen bläddrar automatiskt genom varje menyalternativ vid klickning och höjer knappens [change](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) -händelse (eller anropar knappens [changeHandler](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) -funktion, om sådan finns) för det aktiva menyalternativet.

* datavy

   [CQ.Ext.DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView)

   En mekanism för att visa data med anpassade layoutmallar och formatering. DataView använder en [CQ.Ext.XTemplate](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.XTemplate) som sin interna mallmetod och är bunden till en [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) så att vyn uppdateras automatiskt när data i arkivet ändras för att återspegla ändringarna.

* datafält

   [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField)

   Innehåller ett datuminmatningsfält med listrutan [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) och automatisk datumvalidering.

* datemenu

   [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)

   En meny som innehåller en [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) -komponent.

* datepicker

   [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker)

   En popup-datumväljare. Den här klassen används av [klassen DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) för att tillåta bläddring och val av giltiga datum.

* datetime

   [CQ.form.DateTime](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DateTime)

   Med DateTime kan användaren ange ett datum och en tid genom att kombinera [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) och [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField).

* dialog

   [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)

   Dialogrutan är en speciell typ av fönster med ett formulär i brödtexten och en knappgrupp i sidfoten. Det används vanligtvis för att redigera innehåll, men kan även visa information.

* dialogfältange

   [CQ.form.DialogFieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DialogFieldSet)

   DialogFieldSet är en [FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet) som kan användas i [dialogrutor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* directstore

   [CQ.Ext.data.DirectStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectStore)

   Liten hjälpklass för att skapa en [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) som konfigurerats med en [CQ.Ext.data.DirectProxy](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectProxy) och [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) för att underlätta interaktionen med en [CQ.Ext.Direct](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Direct) Server-side [Provider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.direct.Provider) .

* visningsfält

   [CQ.Ext.form.DisplayField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DisplayField)

   Ett textfält som bara visas och som inte är validerat och inte har skickats.

* redigeringsfält

   [CQ.wcm.EditBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar)

   Med EditBar kan användaren redigera innehåll med knappar på ett fält.

   Även om det inte finns med här, innehåller EditBar alla medlemmar i [CQ.wcm.EditBase](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBase).

* redigerare

   [CQ.Ext.Editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Editor)

   Ett basredigeringsfält som hanterar visning/döljning vid behov och har inbyggd logik för storleksändring och händelsehantering.

* editorrid

   [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)

   Den här klassen utökar [klassen](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) GridPanel för cellredigering i markerade [kolumner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column). De redigerbara kolumnerna anges med en [redigerare](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel) i [kolumnkonfigurationen](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column).

* editrollover

   [CQ.wcm.EditRollover](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)

   Med EditRollover kan användaren redigera innehåll genom att dubbelklicka och få fler redigeringsåtgärder via en snabbmeny. Det redigerbara området markeras med en ram när muspekaren förs över innehållet.

* feedimporter

   [CQ.wcm.FeedImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FeedImporter)

   Med FeedImporter kan användaren importera RSS- eller Atom-flöden och skapa sidor för varje feed-post.

* fält

   [CQ.Ext.form.Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Field)

   Basklass för formulärfält som innehåller standardhändelsehantering, storleksändring, värdehantering och andra funktioner.

* fältuppsättning

   [CQ.Ext.form.FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet)

   Standardbehållare som används för att gruppera artiklar i ett [formulär](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FormPanel)....

* fileuploaddialogknapp

   [CQ.form.FileUploadDialogButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadDialogButton)

   FileUploadDialogButton skapar en knapp som öppnar en ny dialogruta för att överföra en fil via FileUploadField. Kan användas i redigeringsdialogrutor där överföringen måste ske i ett separat formulär.

* fileuploadfield

   [CQ.form.FileUploadField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadField)

   Med FileUploadField kan användaren välja en fil som ska överföras.

* findreplatdialog

   [CQ.wcm.FindReplaceDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FindReplaceDialog)

   FindReplaceDialog är en dialogruta där du kan söka efter och ersätta tokens på en sida och dess underordnade sidor.

* flash

   [CQ.Ext.FlashComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.FlashComponent)

* rutnät

   [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)

   Den här klassen representerar det primära gränssnittet för en komponentbaserad stödrasterkontroll som representerar data i tabellformat för rader och kolumner.

* groupingstore

   [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)

   En specialiserad butiksimplementering som möjliggör gruppering av poster i ett av de tillgängliga fälten. Detta används vanligtvis tillsammans med en [CQ.Ext.grid.GroupingView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GroupingView) för att bevisa datamodellen för en grupperad GridPanel.

* heavymovedialog

   [CQ.wcm.HeavyMoveDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.HeavyMoveDialog)

   Dialogrutan HeavyMoveDialog är en dialogruta där du kan flytta en sida och dess underordnade sidor. Dessutom kan du aktivera om tidigare aktiverade sidor (tung flyttning).

* hidden

   [CQ.Ext.form.Hidden](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Hidden)

   Ett enkelt dolt fält för lagring av dolda värden i formulär som måste skickas i formuläret som skickas.

* historybutton

   [CQ.HistoryButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.HistoryButton)

   HistoryButton är en liten hjälpklass som enkelt tillhandahåller bakåt- och framåtknappar. Vanligtvis krävs två relaterade instanser: Framåtknappsinstansen är en enkel knapp som är länkad till bakåtknappsinstansen som hanterar historiken.

* htmleditor

   [CQ.Ext.form.htmlEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor)

   Innehåller en lättviktig HTML-redigeringskomponent. Vissa verktygsfältsfunktioner stöds inte av Safari och döljs automatiskt vid behov. Dessa beskrivs i konfigurationsalternativen där det är lämpligt.

   Redigerarens knappar i verktygsfältet har knappbeskrivningar definierade i egenskapen [buttonTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor) .

* iframeDialog

   [CQ.IframeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframeDialog)

   En normal dialogruta som visar innehållet i en iframe och tillåter formulär i iframes.

* iframepanel

   [CQ.IframePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframePanel)

   En panel som innehåller en iframe. Gör det enkelt att skapa iframes, en inläsningshändelse för iframe och enkel åtkomst till innehållet i iframe.

* inlinetextfield

   [CQ.form.InlineTextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.InlineTextField)

   InlineField är ett textfält som visas som en etikett när det inte är i fokus.

* jsonstore

   [CQ.Ext.data.JsonStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonStore)

   Liten hjälpklass som gör det enklare att skapa [CQ.Ext.data.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)Lagrar från JSON-data. En JsonStore konfigureras automatiskt med en [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader).

* label

   [CQ.Ext.form.Label](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Label)

   Grundläggande etikettfält.

* språkDialogrutan

   [CQ.wcm.LanguageCopyDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LanguageCopyDialog)

   LanguageCopyDialog är en dialogruta där du kan kopiera språkträd.

* länkkontroll

   [CQ.wcm.LinkChecker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LinkChecker)

   LinkChecker är ett verktyg för att kontrollera externa länkar på en plats.

* listvy

   [CQ.Ext.list.ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView)

   CQ.Ext.list.ListView är en snabb och lättviktsimplementering av en [stödrasterliknande](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) vy.

* livecopyproperties

   [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)

   I LiveCopyProperties finns en panel där du kan visa och redigera Live Copy-egenskaper (relationsarv, synkroniseringsutlösare och synkroniseringsåtgärder ).

* lvbooleancolumn

   [CQ.Ext.list.BooleanColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.BooleanColumn)

   En kolumndefinitionsklass som återger booleska datafält. Mer information finns i alternativet [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) config i [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) .

* lvcolumn

   [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column)

   Den här klassen kapslar in kolumnkonfigurationsdata som ska användas vid initieringen av en [ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView).

* lvdatecolumn

   [CQ.Ext.list.DateColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)

   En kolumndefinitionsklass som återger ett godkänt datum enligt standardspråket eller ett konfigurerat [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn). Mer information finns i alternativet [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) config i [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) .

* lvnumbercolumn

   [CQ.Ext.list.NumberColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn)

   En klass för kolumndefinition som återger ett numeriskt datafält enligt en [formatsträng](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn) . Mer information finns i alternativet [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) config i [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) .

* mediabrowsedialog

   [CQ.MediaBrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.MediaBrowseDialog)

   **Föråldrat: Använd[Innehållssökning](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)för att bläddra bland media i stället.**

   MediaBrowseDialog är en dialogruta för att bläddra i mediebiblioteket.

* meny

   [CQ.Ext.menu.Menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Menu)

   Ett menyobjekt. Det här är den behållare som du kan lägga till menyalternativ i. Menyn kan också fungera som en basklass när du vill ha en speciell meny baserad på en annan komponent (till exempel [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu) ).

   Menyer kan innehålla [menyalternativ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)eller allmänna [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)komponenter.

* menyobjekt

   [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem)

   Basklassen för alla objekt som återges i menyer. BaseItem innehåller standardalternativ för återgivning, aktiverad tillståndshantering och baskonfigurering som delas av alla menykomponenter.

* menykontrollobjekt

   [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem)

   Lägger till ett menyalternativ som innehåller en kryssruta som standard, men som också kan ingå i en alternativgrupp.

* menuitem

   [CQ.Ext.menu.Item](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)

   En basklass för alla menyalternativ som kräver menyrelaterade funktioner (som undermenyer) och som inte är statiska visningsobjekt. Item utökar basfunktionerna i [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem) genom att lägga till menyspecifik aktivering och klickhantering.

* menuseparator

   [CQ.Ext.menu.Separator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Separator)

   Lägger till ett avgränsningsfält på en meny som används för att dela upp logiska grupper med menyalternativ. I allmänhet lägger du till en av dessa med &quot;-&quot; i anropet till add() eller i objektkonfigurationen i stället för att skapa en direkt.

* menutextitem

   [CQ.Ext.menu.TextItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.TextItem)

   Lägger till en statisk textsträng på en meny, som vanligtvis används som rubrikavgränsare eller gruppavgränsare.

* metadata

   [CQ.dam.form.Metadata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.form.Metadata)

   Metadata innehåller en uppsättning fält för att avgöra vilken information som krävs för ett metadatafält, t.ex. på resursredigeringssidor.

   Den innehåller följande fält:

* multifält

   [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)

   MultiField är en redigerbar lista med formulärfält för redigering av egenskaper med flera värden.

* mvt

   [CQ.form.MVT](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MVT)

   Multivariata testkomponenter kan användas för att definiera och redigera en uppsättning bilder som presenteras som olika banderoller. Klicka igenom prisstatistik per banner.

* meddelandeninkorg

   [CQ.wcm.NotificationInbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.NotificationInbox)

   Med NotificationInbox kan användaren prenumerera på WCM-åtgärder och hantera meddelanden.

* numberfield

   [CQ.Ext.form.NumberField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.NumberField)

   Numeriskt textfält med automatisk filtrering av tangenttryckningar och numerisk validering.

* offlineimportör

   [CQ.wcm.OfflineImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.OfflineImporter)

   OfflineImporter är ett verktyg för att importera och konvertera Microsoft Word-dokument till AEM-sidor. Med den här funktionen kan innehåll redigeras offline med en ordbehandlare.

* ownerdraw

   [CQ.form.OwnerDraw](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.OwnerDraw)

   OwnerDraw kan innehålla anpassad HTML-kod (antingen angiven direkt eller hämtad från en URL).

* sidindelning

   [CQ.Ext.PagingToolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.PagingToolbar)

   När antalet poster ökar, ökar tiden som krävs för att webbläsaren ska kunna återge dem. Sidindelning används för att minska mängden data som utbyts med klienten.

* panel

   [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)

   Panelen är en behållare som har specifika funktioner och strukturella komponenter som gör den till den perfekta byggstenen för programorienterade användargränssnitt.

   Paneler ärvs genom arv från [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container).

* paragraphreference

   [CQ.form.ParagraphReference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ParagraphReference)

   I styckereferensfältet kan du bläddra bland sidor och välja ett av deras stycken. Det består av ett utlösarfält och en tillhörande dialogruta för styckebläddring.

* password

   [CQ.form.Password](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Password)

   Lösenordet är som ett [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) men behåller sitt värde privat, vilket gör att användarna kan ange känsliga data.

* patinering

   [CQ.form.PathCompletion](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathCompletion)

   **Föråldrat: Använd[CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)i stället**

* pathfield

   [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)

   PathField är ett inmatningsfält som är utformat för sökvägar med sökvägsinmatning och en knapp för att öppna en [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog) för att bläddra i serverdatabasen. Den kan även bläddra bland sidstycken för avancerad länkgenerering.

* progress

   [CQ.Ext.ProgressBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)

   En komponent för en uppdateringsbar förloppsindikator. Förloppsindikatorn har stöd för två olika lägen: manuell och automatisk.

   I manuellt läge ansvarar du för att visa, uppdatera (via [updateProgress](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)) och rensa förloppsindikatorn efter behov från din egen kod. Den här metoden passar bäst när du vill visa förloppet.

* egenskapsrutnät

   [CQ.Ext.grid.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyGrid)

   En specialiserad stödrasterimplementering som är avsedd att efterlikna det traditionella egenskapsstödrastret, som vanligtvis visas i utvecklingsmiljöer. Varje rad i rutnätet representerar en egenskap för ett objekt, och data lagras som en uppsättning namn/värde-par i [CQ.Ext.grid.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyRecord)PropertyRecords.

* propgrid

   [CQ.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.PropertyGrid)

   PropertyGrid är ett generiskt stödraster som används för att visa och redigera egenskaper för objekt.

* snabbtips

   [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip)

   @xtype quicktip En anpassad verktygstipsklass för verktygstips som kan anges i kod och hanteras automatiskt av den globala instansen [CQ.Ext.QuickTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTips) . Mer användningsinformation och exempel finns i rubriken för klassen QuickTips.

* radio

   [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio)

   Enstaka radiofält. Samma som kryssruta, men det är till för att underlätta automatisk inställning av indatatyp. Radiogruppering hanteras automatiskt av webbläsaren om du ger varje alternativknapp i en grupp samma namn.

* radiogrupp

   [CQ.Ext.form.RadioGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.RadioGroup)

   En grupperingsbehållare för kontrollerna [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio) .

* referenserDialogruta

   [CQ.wcm.ReferencesDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ReferencesDialog)

   ReferencesDialog är en dialogruta där du kan visa referenser på en sida.

* restoretreedialog

   [CQ.wcm.RestoreTreeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreTreeDialog)

   RestoreTreeDialog är en dialogruta där du kan återställa en tidigare version av ett träd.

* restoreversiondialog

   [CQ.wcm.RestoreVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreVersionDialog)

   RestoreVersionDialog är en dialogruta där du kan återställa en tidigare version av en sida.

* richtext

   [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText)

   RichText innehåller ett formulärfält för redigering av formaterad textinformation (RTF).

   Komponenten RichText har för närvarande följande funktioner:

* rolloutplan

   [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)

   I RolloutPlan finns en dialogruta där du kan se hur en sida rullas ut. RolloutPlan startas av en [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard).

* rolloutwizard

   [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)

   RolloutWizard innehåller en guide för att rulla ut en sida. RolloutWizard startar en [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan).

* sökfält

   [CQ.form.SearchField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SearchField)

   SearchField innehåller ett sökfält som ger resultatet i en listruta som kan användas för att söka i databasen.

* markering

   [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection)

   Med markeringen kan användaren välja mellan flera alternativ. Alternativen kan ingå i konfigurationen eller läsas in från ett JSON-svar. Markeringen kan antingen återges som en listruta (markering) eller som en kombinationsruta (markering plus fritextpost).

* sidekick

   [CQ.wcm.Sidespark](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Sidekick)

   The Sidekick är en flytande hjälpreda som ger användaren tillgång till vanliga verktyg för sidredigering.

* siteadmin

   [CQ.wcm.SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)

   SiteAdmin är en konsol som tillhandahåller WCM-administrationsfunktioner.

* platteimportör

   [CQ.wcm.SiteImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteImporter)

   Med SiteImporter kan användaren importera hela webbplatser och skapa inledande projekt.

* sizefield

   [CQ.form.SizeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SizeField)

   Med SizeField kan användaren ange bredd och höjd (till exempel för en bild).

* reglage

   [CQ.Ext.Slider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Slider)

   Skjutreglage som har stöd för lodrät eller vågrät orientering, tangentbordsjusteringar, konfigurerbar fästning, axelklickning och animering. Kan läggas till som ett objekt i valfri behållare. Exempelanvändning:...

* bildspel

   [CQ.form.Slideshow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Slideshow)

   Bildspelet innehåller en komponent som kan användas för att definiera och redigera en uppsättning bilder och bildtitlar som kan visas som ett bildspel.

   Bildspelskomponenten är baserad på [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage) .

* smartfile

   [CQ.form.SmartFile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartFile)

   SmartFile är en intelligent filuppladdare.

   Om ett Flash-plugin-program (version >= 9) är installerat körs överföringarna med SWFupload-biblioteket, som är ett bekvämt sätt att hantera överföringar.

* smartimage

   [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage)

   SmartImage är en intelligent bildöverförare. Den innehåller verktyg för att bearbeta en överförd bild, till exempel ett verktyg för att definiera bildscheman och en bildpipett.

   Observera att komponenten främst är avsedd att användas på en separat dialogruteflik.

* spacer

   [CQ.Ext.Spacer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Spacer)

   Används för att skapa ett stort utrymme i en layout.

* snurra

   [CQ.form.Spinner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Spinner)

   Spinner är ett utlösarfält för numeriska värden, datum- eller tidsvärden. Värdet kan ökas och minskas med hjälp av upp- och nedutlösarna, rullningshjulet eller tangenterna.

* splitbutton

   [CQ.Ext.SplitButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.SplitButton)

   En delad knapp som innehåller en inbyggd listrutepil som kan utlösa en händelse separat från knappens standardklickningshändelse. Vanligtvis används detta för att visa en listruta som innehåller ytterligare alternativ till den primära knappåtgärden, men alla anpassade hanterare kan tillhandahålla implementeringen av pilklick.

* Statisk

   [CQ.Static](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Static)

   Static kan användas för att visa godtycklig text eller HTML.

* statistik

   [CQ.wcm.Statistics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Statistics)

   Statistik visar sidavbildningarna som ett diagram. Med widgeten kan du välja en period. Statistiken ska visas för.

* store

   [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)

   Klassen Store kapslar in en klientsidescache för [Record](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Record) -objekt som tillhandahåller indata för komponenter som [GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel), [ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)eller [DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView).

* förslagsfält

   [CQ.form.SuFöregeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SuggestField)

   SuggestField ger användaren förslag baserat på inmatningen.

* växlare

   [CQ.Switcher](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Switcher)

   Switcharen tillhandahåller en knappgrupp för sidhuvudsfältet i en konsol för att växla mellan webbplatser, digitala resurser, verktyg, arbetsflöde och säkerhet.

* tableedit

   [CQ.form.TableEdit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit)

   **Föråldrat: Använd[CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)i stället.**

* tableedit2

   [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)

   TableEdit2 innehåller en widget för att skapa tabeller.

* flikpanel

   [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)

   En enkel flikbehållare. TabPanels kan användas exakt som en standard- [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel) i layoutsyfte, men har även särskilt stöd för att innehålla underordnade komponenter ([`items`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)).

* taggar

   [CQ.tagging.TagInputField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tagging.TagInputField)

   ```
   CQ.tagging.TagInputField
   ```

   är en formulärwidget för att ange taggar. Den har en snabbmeny där du kan välja bland befintliga taggar, som innehåller automatisk komplettering och många andra funktioner.

* textområde

   [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea)

   Flerradigt textfält. Kan användas som ersättning för traditionella textområdesfält och lägger till stöd för automatisk storleksjustering.

* textknapp

   [CQ.TextButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.TextButton)

   TextButton innehåller en textlänk med funktionerna i en [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button).

* textfält

   [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)

   Grundläggande textfält. Kan användas som direkt ersättning för traditionella textinmatningar eller som basklass för mer avancerade inmatningskontroller (som [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea) och [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)).

* miniatyrbild

   [CQ.form.Thumbnail](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Thumbnail)

* tidsfält

   [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)

   Tillhandahåller ett tidsinmatningsfält med en tidslistruta och automatisk tidsvalidering. Exempelanvändning:...

* tips

   [CQ.Ext.Tip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tip)

   @xtype tip Det här är basklassen för [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip) och [CQ.Ext.Tooltip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tooltip) som innehåller den grundläggande layout och placering som alla tipsbaserade klasser kräver. Den här klassen kan användas direkt för enkla, statiskt positionerade tips.

* titleseparator

   [CQ.menu.TitleSeparator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.menu.TitleSeparator)

   Lägger till ett avgränsningsfält på en meny som används för att dela upp logiska grupper med menyalternativ. Avgränsaren kan även innehålla en titel.

* toolbar

   [CQ.Ext.Toolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Toolbar)

   Klassen Basic Toolbar. Trots att [`defaultType`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) for Toolbar är [`button`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)det kan verktygsfältselement (underordnade objekt för Toolbar-behållaren) vara praktiskt taget vilken typ av komponent som helst. Verktygsfältselement kan skapas explicit via deras konstruktorer.

* funktionsbeskrivning

   [CQ.Ext.ToolTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ToolTip)

   En standardimplementering av verktygstips som ger ytterligare information när du hovrar över ett målelement. @xtype-verktygstips.

* treegrid

   [CQ.tree.TreeGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tree.TreeGrid)

   @xtype treegrid

* treepanel

   [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)

   TreePanel innehåller trädstrukturerade gränssnittsrepresentationer av trädstrukturerade data.

   [TreeNodes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode)som läggs till i TreePanel-panelen kan innehålla metadata som används av programmet i deras [attribut](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode) -egenskap.

* trigger

   [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)

   Ger en praktisk omslutning för TextFields som lägger till en klickbar utlösarknapp (ser ut som en kombinationsruta som standard). Utlösaren har ingen standardåtgärd, så du måste tilldela en funktion för att implementera utlösarklickshanteraren genom att åsidosätta [onTriggerClick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField). Du kan skapa ett TriggerField direkt, eftersom det återges exakt som en kombinationsruta.

* uploaddialog

   [CQ.UploadDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UploadDialog)

   Med UploadDialog kan användaren överföra filer till databasen Skapar en ny UploadDialog.

* userinfo

   [CQ.UserInfo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UserInfo)

   Verktygsfältsobjekt som visar det aktuella användarnamnet och tillåter användaråtgärder som att redigera användaregenskaper och personifiering.

* visningsruta

   [CQ.Ext.Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport)

   En speciell behållare som representerar det visningsbara programområdet (webbläsarens visningsruta).

   Visningsrutan återger sig själv till dokumentets brödtext och anpassar sig automatiskt till storleken på webbläsarvisningsrutan och hanterar fönsterstorleksändring. Det kan bara finnas en visningsport som har skapats.

* window

   [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)

   En specialpanel som är avsedd att användas som programfönster. Fönster är flytande, [kan storleksändras](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)och [dragbara](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) som standard. Windows kan [maximeras](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) för att fylla visningsrutan, återställas till den tidigare storleken och kan [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)minimeras.

* xmlstore

   [CQ.Ext.data.XmlStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlStore)

   Liten hjälpklass som gör det enklare att skapa [CQ.Ext.data.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)Lagrar från XML-data. En XmlStore konfigureras automatiskt med en [CQ.Ext.data.XmlReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlReader).

   **cqinclude** Pseudo xtype som innehåller widgetdefinitioner från en annan sökväg i databasen. Det används oftast i siddialogrutor. Det finns ingen faktisk JavaScript-widgetklass för den här xtype-filen. Den bearbetas av funktionen formatData() i klassen CQ.Util. Mer information finns i den här artikeln i kunskapsbasen.
