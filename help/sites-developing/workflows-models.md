---
title: Skapa arbetsflödesmodeller
seo-title: Skapa arbetsflödesmodeller
description: Du skapar en arbetsflödesmodell som definierar de steg som körs när en användare startar arbetsflödet.
seo-description: Du skapar en arbetsflödesmodell som definierar de steg som körs när en användare startar arbetsflödet.
uuid: 31071d3a-d6d5-4476-9ac0-7b335de406d9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c097b60f-bcdf-45de-babe-b4c2e2b746a1
docset: aem65
translation-type: tm+mt
source-git-commit: d12313003cb94b27c1ce64442a1f3394af529a0d

---


# Skapa arbetsflödesmodeller{#creating-workflow-models}

>[!CAUTION]
>
>Om du vill använda det klassiska användargränssnittet läser du [AEM 6.3-dokumentationen](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/workflows-models.html) .

Du skapar en [arbetsflödesmodell](/help/sites-developing/workflows.md#model) som definierar den serie steg som körs när en användare startar arbetsflödet. Du kan också definiera modellegenskaper, t.ex. om arbetsflödet är tillfälligt eller använder flera resurser.

När en användare startar ett arbetsflöde startas en instans; detta är motsvarande körningsmodell som skapas när du [synkroniserar](#sync-your-workflow-generate-a-runtime-model) dina ändringar.

## Skapa ett nytt arbetsflöde {#creating-a-new-workflow}

När du först skapar en ny arbetsflödesmodell innehåller den:

* Stegen, **Flödesstart** och **Flödesslut**.
Dessa representerar början och slutet av arbetsflödet. Dessa steg är obligatoriska och kan inte redigeras/tas bort.
* Ett exempel på **deltagarsteg** som heter **Steg 1**.
Det här steget är konfigurerat för att tilldela en arbetsuppgift till arbetsflödesinitieraren. Redigera eller ta bort det här steget och lägg till steg efter behov.

Så här skapar du ett nytt arbetsflöde med redigeraren:

1. Öppna konsolen **Arbetsflödesmodeller** ; via **Verktyg**, **Arbetsflöde**, **Modeller** eller, till exempel: [https://localhost:4502/aem/workflow](https://localhost:4502/aem/workflow)
1. Välj **Skapa** och sedan **Skapa modell**.
1. Dialogrutan **Lägg till arbetsflödesmodell** visas. Ange **Titel** och **Namn** (valfritt) innan du väljer **Klar**.
1. Den nya modellen visas i **konsolen Arbetsflödesmodeller** .
1. Välj ditt nya arbetsflöde och använd sedan [**Redigera **för att öppna det för konfiguration](#editinganexistingworkflow):   ![wf-01](assets/wf-01.png)

>[!NOTE]
>
>Om du skapar modeller programmatiskt (med ett crx-paket) kan du även skapa en undermapp i:
>
>`/var/workflow/models`

>Exempel, `/var/workflow/models/prototypes`
>Den här mappen kan sedan användas för [att hantera åtkomst till modellerna i den mappen](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that).

## Redigera ett arbetsflöde {#editing-a-workflow}

Du kan redigera alla befintliga arbetsflödesmodeller till:

* [definiera steg](#addingasteptoamodel-) och deras [parametrar](#configuring-a-workflow-step)
* konfigurera arbetsflödesegenskaper, inklusive [faser](#configuring-workflow-stages-that-show-workflow-progress), [om arbetsflödet är tillfälligt](#creatingatransientworkflow-) och/eller [använder flera resurser](#configuring-a-workflow-for-multi-resource-support)

Om du redigerar ett [**standardarbetsflöde och/eller äldre **arbetsflöde](#editing-a-default-or-legacy-workflow-for-the-first-time)(ej ikryssad) har du ett steg till som säkerställer att en[säker kopia](/help/sites-developing/workflows-best-practices.md#locations-workflow-models)görs innan ändringarna görs.

När uppdateringarna av arbetsflödet är klara måste du använda **Synkronisera** för att **generera en körningsmodell**. Mer information finns i [Synkronisera arbetsflödet](#sync-your-workflow-generate-a-runtime-model) .

### Synkronisera arbetsflödet - Skapa en körningsmodell {#sync-your-workflow-generate-a-runtime-model}

**Synkronisering** (direkt i redigeringsverktygsfältet) genererar en [körningsmodell](/help/sites-developing/workflows.md#runtime-model). Körningsmodellen är den modell som faktiskt används när en användare startar ett arbetsflöde. Om du inte **synkroniserar** dina ändringar är ändringarna inte tillgängliga vid körning.

När du (eller någon annan användare) gör några ändringar i arbetsflödet måste du använda **Synkronisera** för att generera en körningsmodell, även när enskilda dialogrutor (till exempel för steg) har egna sparalternativ.

När ändringarna synkroniseras med körningsmodellen (sparad) visas **Synkroniserad** i stället.

Vissa steg har obligatoriska fält och/eller inbyggd validering. När dessa villkor inte uppfylls visas ett fel när du försöker **synkronisera** modellen. Om ingen deltagare har definierats för ett **deltagarsteg** :

![wf-21](assets/wf-21.png)

### Redigera ett standardarbetsflöde eller äldre arbetsflöde för första gången {#editing-a-default-or-legacy-workflow-for-the-first-time}

När du öppnar en [standardmodell och/eller äldre modell](/help/sites-developing/workflows.md#workflow-types) för redigering:

* Stegwebbläsaren är inte tillgänglig (vänster sida).
* Det finns en **redigeringsåtgärd** i verktygsfältet (höger sida).
* Till att börja med visas modellen och dess egenskaper i skrivskyddat läge som:
   * Standardarbetsflöden finns i `/libs`
   * Äldre arbetsflöden finns i `/etc`Välja **redigering** :
* ta en kopia av arbetsflödet till `/conf`
* göra stegwebbläsaren tillgänglig
* gör att du kan göra ändringar

>[!NOTE]
Mer information finns [i Platser för arbetsflödesmodeller](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) .

![wf-22](assets/wf-22.png)

### Lägga till ett steg i en modell {#adding-a-step-to-a-model}

Du måste lägga till steg i modellen för att representera aktiviteten som ska utföras - varje steg utför en specifik aktivitet. Ett urval stegkomponenter är tillgängliga i en AEM-standardinstans.

När du redigerar en modell visas de tillgängliga stegen i de olika grupperna i **stegwebbläsaren**. Exempel:

![wf-10](assets/wf-10.png)

>[!NOTE]
Information om de komponenter i det primära steget som installeras med AEM finns i [Referens för](/help/sites-developing/workflows-step-ref.md)arbetsflödessteg.

Så här lägger du till steg i arbetsflödesmodellen:

1. Öppna en befintlig arbetsflödesmodell för redigering. Välj önskad modell i **modellkonsolen** för arbetsflöden och sedan **Redigera**.
1. Öppna stegwebbläsaren; med **växlingspanelen** längst till vänster i det övre verktygsfältet. Här kan du:

   * **Filtrera** efter specifika steg.
   * Använd listruteväljaren för att begränsa markeringen till en viss grupp steg.
   * Välj ikonen Visa beskrivning ( ![wf-stepinfo-icon](assets/wf-stepinfo-icon.png) ) om du vill visa mer information om det aktuella steget.
   ![wf-02](assets/wf-02.png)

1. Dra lämpliga steg till önskad plats i modellen.

   Exempel: ett **deltagarsteg**.

   När du har lagt till i flödet kan du [konfigurera steget](#configuring-a-workflow-step).

   ![wf-03](assets/wf-03.png)

1. Lägg till så många steg eller andra uppdateringar som behövs.

   Vid körning utförs stegen i den ordning som de visas i modellen. När du har lagt till stegkomponenter kan du dra dem till en annan plats i modellen.

   Du kan också kopiera, klippa ut, klistra in, gruppera eller ta bort befintliga steg; som med [sidredigeraren.](/help/sites-authoring/editing-content.md)

   Delade steg kan också komprimeras/expanderas med verktygsfältsalternativet: ![wf-collap-expand-toolbar-icon](assets/wf-collapseexpand-toolbar-icon.png)

1. Bekräfta ändringarna med **Synkronisera** (redigeringsverktygsfältet) för att generera körningsmodellen.

   Mer information finns i [Synkronisera arbetsflödet](#sync-your-workflow-generate-a-runtime-model) .

### Konfigurera ett arbetsflödessteg {#configuring-a-workflow-step}

Du kan **konfigurera** och anpassa ett arbetsflödesstegs beteende med hjälp av dialogrutorna **Stegegenskaper** .

1. Så här öppnar du dialogrutan **Stegegenskaper** för ett steg:

   * Klicka/tryck på **steget i arbetsflödesmodellen och välj **Konfigurera** i komponentverktygsfältet.

   * Dubbelklicka på steget.
   >[!NOTE]
   Information om de komponenter i det primära steget som installeras med AEM finns i [Referens för](/help/sites-developing/workflows-step-ref.md)arbetsflödessteg.

1. Konfigurera **stegegenskaperna** efter behov; Vilka egenskaper som är tillgängliga beror på stegtypen. Det kan också finnas flera tillgängliga flikar. Standardsteget för **deltagare** visas i ett nytt arbetsflöde som `Step 1`:

   ![wf-11](assets/wf-11.png)

1. Bekräfta uppdateringarna.
1. Bekräfta ändringarna med **Synkronisera** (redigeringsverktygsfältet) för att generera körningsmodellen.

   Mer information finns i [Synkronisera arbetsflödet](#sync-your-workflow-generate-a-runtime-model) .

### Skapa ett tillfälligt arbetsflöde {#creating-a-transient-workflow}

Du kan skapa en [tillfällig](/help/sites-developing/workflows.md#transient-workflows) arbetsflödesmodell när du skapar en ny modell, eller genom att redigera en befintlig:

1. Öppna arbetsflödesmodellen för [redigering](#editinganexistingworkflow).
1. Välj **Egenskaper** för arbetsflödesmodell i verktygsfältet.
1. Aktivera **tillfälligt arbetsflöde** (eller inaktivera om det behövs) i dialogrutan:

   ![wf-07](assets/wf-07.png)

1. Bekräfta ändringen med **Spara och stäng**; följt av **Synkronisera** (redigeringsverktygsfältet) för att generera körningsmodellen.

   Mer information finns i [Synkronisera arbetsflödet](#sync-your-workflow-generate-a-runtime-model) .

>[!NOTE]
När du kör ett arbetsflöde i [tillfälligt](/help/sites-developing/workflows.md#transient-workflows) läge sparas ingen arbetsflödeshistorik i AEM. Därför visas ingen information om arbetsflödet i [tidslinjen](/help/sites-authoring/basic-handling.md#timeline) . [](/help/sites-authoring/basic-handling.md#timeline)

## Göra arbetsflödesmodeller tillgängliga i Touch UI {#classic2touchui}

Om det finns en arbetsflödesmodell i det klassiska användargränssnittet, men den saknas på snabbmenyn för val i **[!UICONTROL tidslinjerskan]** i Touch UI, följer du konfigurationen för att göra den tillgänglig. Följande steg visar hur du använder arbetsflödesmodellen som kallas **[!UICONTROL Begär aktivering]**.

1. Bekräfta att modellen inte är tillgänglig i det beröringsaktiverade användargränssnittet. Få åtkomst till en resurs med `/assets.html/content/dam` sökväg. Välj en resurs. Öppna **[!UICONTROL tidslinjen]** i den vänstra listen. Klicka på **[!UICONTROL Starta arbetsflöde]** och bekräfta att **[!UICONTROL aktiveringsmodellen]** inte finns i popup-listan.

1. Navigera genom **[!UICONTROL Verktyg > Allmänt > Taggning]**. Välj **[!UICONTROL Arbetsflöde]**.

1. Välj **[!UICONTROL Skapa > Skapa tagg]**. Ange **[!UICONTROL Titel]** som `DAM` och **[!UICONTROL Namn]** som `dam`. Välj **[!UICONTROL Skicka]**.
   ![Skapa tagg i arbetsflödesmodell](assets/workflow_create_tag.png)

1. Navigera till **[!UICONTROL Verktyg > Arbetsflöde > Modeller]**. Välj **[!UICONTROL Begär aktivering]** och sedan **[!UICONTROL Redigera]**.

1. Välj **[!UICONTROL Redigera]**, öppna menyn **[!UICONTROL Sidinformation]** och gå sedan till fliken **[Grundläggande]** (om den inte redan är öppen) genom att välja **[!UICONTROL UICONTROL-Öppna egenskaper]** .

1. Lägg till `Workflow : DAM` i **[!UICONTROL taggfältet]** . Bekräfta markeringen med bocken.

1. Bekräfta tillägget av taggen med **[!UICONTROL Spara och stäng]**.
   ![Redigera sidegenskaper för modell](assets/workflow_model_edit_activation1.png)

1. Slutför processen med **[!UICONTROL Synkronisera]**. Arbetsflödet är nu tillgängligt i det Touch-aktiverade gränssnittet.

### Konfigurera ett arbetsflöde för stöd för flera resurser {#configuring-a-workflow-for-multi-resource-support}

Du kan konfigurera en arbetsflödesmodell för [Multi Resource Support](/help/sites-developing/workflows.md#multi-resource-support) när du skapar en ny modell, eller genom att redigera en befintlig:

1. Öppna arbetsflödesmodellen för [redigering](#editinganexistingworkflow).
1. Välj **Egenskaper** för arbetsflödesmodell i verktygsfältet.

1. Aktivera **Multi Resource Support** (eller inaktivera vid behov) i dialogrutan:

   ![wf-08](assets/wf-08.png)

1. Bekräfta ändringen med **Spara och stäng**; följt av **Synkronisera** (redigeringsverktygsfältet) för att generera körningsmodellen.

   Mer information finns i [Synkronisera arbetsflödet](#sync-your-workflow-generate-a-runtime-model) .

### Konfigurera arbetsflödessteg (som visar förlopp för arbetsflöde) {#configuring-workflow-stages-that-show-workflow-progress}

[Arbetsflödesfaser](/help/sites-developing/workflows.md#workflow-stages) hjälper dig att visualisera förloppet för ett arbetsflöde när du hanterar uppgifter.

>[!CAUTION]
Om arbetsflödesfaser definieras i **Sidegenskaper**, men inte används för något av arbetsflödesstegen, visas inga förlopp i förloppsindikatorn (oavsett aktuellt arbetsflödessteg).

De steg som ska vara tillgängliga definieras i arbetsflödesmodellerna. befintliga arbetsflödesmodeller kan uppdateras så att de innehåller scendefinitioner. Du kan definiera valfritt antal steg för arbetsflödesmodellen.

Så här definierar du **steg** för arbetsflödet:

1. Öppna arbetsflödesmodellen för redigering.
1. Välj **Egenskaper** för arbetsflödesmodell i verktygsfältet. Öppna sedan fliken **Steg** .
1. Lägg till (och placera) önskade **scener**. Du kan definiera valfritt antal steg för arbetsflödesmodellen.

   Exempel:

   ![wf-08-1](assets/wf-08-1.png)

1. Klicka på **Spara och stäng** för att spara egenskaperna.
1. Tilldela en fas till varje steg i arbetsflödesmodellen. Exempel:

   ![wf-09](assets/wf-09.png)

   En scen kan tilldelas till mer än ett steg. Exempel:

   | **Steg** | **Scen** |
   |---|---|
   | Steg 1 | Skapa |
   | Steg 2 | Skapa |
   | Steg 3 | Granska |
   | Steg 4 | Godkänn |
   | Steg 5 | Godkänn |
   | Steg 6 | Slutförd |

1. Bekräfta ändringarna med **Synkronisera** (redigeringsverktygsfältet) för att generera körningsmodellen.

   Mer information finns i [Synkronisera arbetsflödet](#sync-your-workflow-generate-a-runtime-model) .

## Exportera en arbetsflödesmodell i ett paket {#exporting-a-workflow-model-in-a-package}

Så här exporterar du en arbetsflödesmodell i ett paket:

1. Skapa ett nytt paket med [Pakethanteraren](/help/sites-administering/package-manager.md#package-manager):

   1. Navigera till Package Manager via **Tools**, **Deployment**, **Packages**.

   1. Klicka på **Skapa paket**.
   1. Ange **paketnamnet** och annan information efter behov.
   1. Click **OK**.

1. Klicka på **Redigera** i verktygsfältet i det nya paketet.

1. Öppna fliken **Filter** .

1. Välj **Lägg till filter** och ange sökvägen till arbetsflödesmodellens *design*:

   `/conf/global/settings/workflow/models/<*your-model-name*>`

   Klicka på **Klar**.

1. Välj **Lägg till filter** och ange sökvägen till arbetsflödesmodellen för *körning* :

   `/var/workflow/models/<*your-model-name*>`

   Klicka på **Klar**.

1. Lägg till ytterligare filter för anpassade skript som används av modellen.
1. Klicka på **Spara** för att bekräfta filterdefinitionerna.
1. Välj **Skapa** i verktygsfältet för paketdefinitionen.
1. Välj **Hämta** i paketets verktygsfält.

## Använda arbetsflöden för att bearbeta inskickade formulär {#using-workflows-to-process-form-submissions}

Du kan konfigurera ett formulär som ska bearbetas av det valda arbetsflödet. När användare skickar formuläret skapas en ny arbetsflödesinstans med data från formuläröverföringen som nyttolast.

Så här konfigurerar du arbetsflödet som ska användas med formuläret:

1. Skapa en ny sida och öppna den för redigering.
1. Lägg till en **formulärkomponent** på sidan.
1. **Konfigurera** komponenten **Formulärstart** som visas på sidan.
1. Använd **Starta arbetsflöde** för att välja önskat arbetsflöde bland de tillgängliga:

   ![wf-12](assets/wf-12.png)

1. Bekräfta den nya formulärkonfigurationen med krysset.

## Testa arbetsflöden {#testing-workflows}

Det är en god vana att testa ett arbetsflöde för att använda olika typer av nyttolast. inklusive typer som skiljer sig från den för vilken den har utvecklats. Om du t.ex. vill att ditt arbetsflöde ska hantera resurser testar du det genom att ange en sida som nyttolast och se till att den inte orsakar fel.

Testa till exempel ditt nya arbetsflöde på följande sätt:

1. [Starta arbetsflödesmodellen](/help/sites-administering/workflows-starting.md) från konsolen.
1. Definiera **nyttolasten** och bekräfta.

1. Utför de åtgärder som behövs så att arbetsflödet fortsätter.
1. Övervaka loggfilerna medan arbetsflödet körs.

Du kan också konfigurera AEM så att **DEBUG** -meddelanden visas i loggfilerna. Mer information finns i [Loggning](/help/sites-deploying/configure-logging.md) . När du är klar anger du **Loggnivå** till **Info** igen.

## Exempel {#examples}

### Exempel: Skapa ett (enkelt) arbetsflöde för att acceptera eller avvisa en begäran om publicering {#example-creating-a-simple-workflow-to-accept-or-reject-a-request-for-publication}

För att illustrera några av möjligheterna att skapa ett arbetsflöde skapar följande exempel en variant av `Publish Example` arbetsflödet.

1. [Skapa en ny arbetsflödesmodell](#creating-a-new-workflow).

   Det nya arbetsflödet kommer att innehålla:

   * **Flödesstart**
   * `Step 1`
   * **Flödesslut**

1. Ta bort `Step 1` (eftersom det är fel stegtyp för det här exemplet):

   * Klicka på steget och välj **Ta bort** i komponentens verktygsfält. Bekräfta åtgärden.

1. Dra ett **deltagarsteg** från alternativet **Arbetsflöde** i stegwebbläsaren till arbetsflödet och placera det mellan **Flödesstart** och **Flödesslut**.
1. Så här öppnar du egenskapsdialogrutan:

   * Klicka på deltagarsteget och välj **Konfigurera** i komponentverktygsfältet.
   * Dubbelklicka på deltagarsteget.

1. På fliken **Allmänt** anger du `Validate Content` både **Titel** och **Beskrivning**.
1. Öppna fliken **Användare/grupp** :

   * Aktivera **Meddela användare via e-post**.
   * Välj `Administrator` ( `admin`) för fältet **Användare/grupp** .
   >[!NOTE]
   För att e-postmeddelanden ska kunna skickas måste [informationen för e-posttjänsten och användarkontot konfigureras](/help/sites-administering/notification.md).

1. Bekräfta uppdateringarna med en bock.

   Du återgår till översikten över arbetsflödesmodellen där deltagarsteget har bytt namn till `Validate Content`.

1. Dra en **eller en delning** till arbetsflödet och placera den mellan `Validate Content` och **Flödesslut**.
1. Öppna **eller dela** för konfiguration.
1. Konfigurera:

   * **Vanliga**: Ange delningsnamnet.
   * **Gren 1**: välj **Standardflöde**.

   * **Gren 2**: kontrollera att **standardflöde** inte är markerat.

1. Bekräfta uppdateringarna av **ELLER Dela**.
1. Dra ett **deltagarsteg** till den vänstra grenen, öppna egenskaperna, ange följande värden och bekräfta sedan ändringarna:

   * **Titel**: `Reject Publish Request`

   * **Användare/grupp**:
till exempel `projects-administrators`

   * **Meddela användaren via e-post**: Aktivera om du vill att användaren ska meddelas via e-post.

1. Dra ett **processsteg** till den högra grenen, öppna egenskaperna, ange följande värden och bekräfta sedan ändringarna:

   * **Titel**: `Publish Page as Requested`

   * **Process**: välj `Activate Page`. Den här processen publicerar den valda sidan till utgivarinstanserna.

1. Klicka på **Synkronisera** (redigeringsverktygsfältet) för att generera körningsmodellen.

   Mer information finns i [Synkronisera arbetsflödet](#sync-your-workflow-generate-a-runtime-model) .

   Den nya arbetsflödesmodellen ser ut så här:

   ![wf-13](assets/wf-13.png)

1. Använd det här arbetsflödet på sidan så att användaren kan välja om han/hon vill **publicera sidan som begärd** eller **avvisa publiceringsbegäran** när han/hon går till **Slutför** steget **Validera innehåll**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

### Exempel: Definiera en regel för en OR-delning med ECMA-skript {#defineruleecmascript}

**Med de delade** stegen kan du lägga in villkorliga bearbetningssökvägar i arbetsflödet.

Så här definierar du en OR-regel:

1. Skapa två skript och spara dem i databasen, till exempel under:

   `/apps/myapp/workflow/scripts`

   >[!NOTE]
   Skripten måste ha en [funktion `check()`](#function-check) som returnerar ett booleskt värde.

1. Redigera arbetsflödet och lägg till **OR-delningen** i modellen.
1. Redigera egenskaperna för **grenen 1** i **ELLER Dela**:

   * Ange detta som **standardflöde** genom att ange **värdet** till `true`.

   * Ange sökvägen till skriptet som **Regel**. Exempel:
      `/apps/myapp/workflow/scripts/myscript1.ecma`
   >[!NOTE]
   Du kan ändra grenordningen om det behövs.

1. Redigera egenskaperna för **grenen 2** i **ELLER Dela**.

   * Ange sökvägen till det andra skriptet som **Regel**. Exempel:
      `/apps/myapp/workflow/scripts/myscript2.ecma`

1. Ange egenskaperna för de enskilda stegen i varje gren. Kontrollera att **Användare/grupp** är inställd.
1. Klicka på **Synkronisera** (redigeringsverktygsfältet) för att behålla ändringarna i körningsmodellen.

   Mer information finns i [Synkronisera arbetsflödet](#sync-your-workflow-generate-a-runtime-model) .

#### Funktionskontroll() {#function-check}

>[!NOTE]
Se [Använda ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).

Följande exempelskript returnerar `true` om noden finns `JCR_PATH` under `/content/we-retail/us/en`:

```
function check() {
    if (workflowData.getPayloadType() == "JCR_PATH") {
      var path = workflowData.getPayload().toString();
      var node = jcrSession.getItem(path);

      if (node.getPath().indexOf("/content/we-retail/us/en") >= 0) {
       return true;
      } else {
       return false;
      }
     } else {
      return false;
     }
}
```

### Exempel: Anpassad aktiveringsbegäran {#example-customized-request-for-activation}

Du kan anpassa alla färdiga arbetsflöden. Om du vill ha ett anpassat beteende lägger du över information om rätt arbetsflöde.

Exempel: **Aktiveringsbegäran**. Det här arbetsflödet används för att publicera sidor i **webbplatser** och aktiveras automatiskt när en innehållsförfattare inte har rätt replikeringsbehörighet. Mer information finns i [Anpassa sidredigering - Anpassa arbetsflödet](/help/sites-developing/customizing-page-authoring-touch.md#customizing-the-request-for-activation-workflow) för begäran om aktivering.
