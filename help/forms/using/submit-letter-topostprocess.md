---
title: Post behandling av brev och interaktiv kommunikation
description: Med Post Bokföringsbearbetning i Correspondence Management kan ni skapa AEM- och Forms-postprocesser, som utskrift och e-post, och integrera dem med era brev.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 91ee4422-99c1-4907-a507-5968c6984f28
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---

# Post behandling av brev och interaktiv kommunikation{#post-processing-of-letters-and-interactive-communications}

## Post Processing {#post-processing}

Agenter kan associera och köra arbetsflöden för efterbearbetning av brev och interaktiv kommunikation. Du kan välja vilken Post-process som ska köras i egenskapsvyn i brevmallen. Du kan ställa in postprocesser för e-post, utskrift, fax eller arkivering av dina slutliga brev.

![Post-bearbetning](assets/ppoverview.png)

Om du vill associera postprocesser med brev eller interaktiv kommunikation måste du först konfigurera postprocesserna. Två typer av arbetsflöden kan utföras på skickade brev:

1. **Forms Workflow:** Detta är AEM Forms om arbetsflöden för processhantering i JEE. Instruktioner för att konfigurera [Forms Workflow](#formsworkflow).

1. **AEM Arbetsflöde:** AEM arbetsflöden kan också användas som efterbearbetning för skickade brev. Instruktioner för att konfigurera [AEM arbetsflöde](../../forms/using/aem-forms-workflow.md).

## Forms Workflow {#formsworkflow}

1. Öppna Adobe Experience Manager Web Console-konfiguration för servern med följande URL i AEM: `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![Konfigurationshanteraren](assets/2configmanager-1.png)

1. På den här sidan letar du upp AEM Forms Client SDK Configuration och expanderar den genom att klicka på den.
1. Ange namnet på din AEM Forms på JEE-servern i URL-adressen för servern, inloggningsinformation och klicka sedan på **Spara**.

   ![Ange LiveCyclets servernamn](assets/1cofigmanager.png)

1. Ange användarnamn och lösenord.
1. Kontrollera att sun.util.calendar har lagts till i Brandväggskonfiguration för deserialisering.

   Gå till Konfiguration av brandvägg för deserialisering och lägg till sun.util.endar under Tillåtslista klasser för paketprefix.

1. Nu är dina servrar mappade och postprocesserna i AEM Forms på JEE är tillgängliga i AEM användargränssnitt när du skapar brev.

   ![Skapa brevskärm med postprocesser listade](assets/0configmanager.png)

1. Om du vill autentisera en process/tjänst kopierar du processens namn och går tillbaka till Adobe Experience Manager Web Console Console Configurations > AEM Forms Client SDK Configuration och lägger till processen som en ny tjänst.

   Om listrutan på egenskapssidan för brevet till exempel visar processens namn som Forms Workflow -> ValidCCPostProcess/SaveXML lägger du till ett tjänstnamn som `ValidCCPostProcess/SaveXML`.

1. Om du vill använda AEM Forms i JEE-arbetsflöden för efterbearbetning ställer du in de parametrar och utdata som behövs. Standardvärden för parametrarna anges nedan.

   Gå till sidan Konfigurera Adobe Experience Manager Web Console > **[!UICONTROL Correspondence Management Configurations]** och ange följande parametrar:

   1. **inPDFDoc (dokumentparameter i PDF):** Ett PDF-dokument som indata. Den här inmatningen innehåller den återgivna bokstaven som indata. De angivna parameternamnen kan konfigureras. De kan konfigureras från Correspondence Management-konfigurationer från konfigurationen.
   1. **inXMLDoc (XML-dataparameter):** Ett XML-dokument som indata. Dessa indata innehåller data som användaren anger i form av XML.
   1. **inXDPDoc (XDP-dokumentparameter):** Ett XML-dokument som indata. Indata innehåller underliggande layout (XDP).
   1. **inAttachmentDocs (parametern Attachment Documents):** En listindataparameter. Indata innehåller alla bilagor som indata.
   1. **redirectURL (Redirect URL Output):** En utdatatyp som anger den URL som ska omdirigeras.

   Formulärarbetsflödet måste ha antingen dokumentparametern PDF eller XML-dataparametern som indata med samma namn som anges i **[!UICONTROL Correspondence Management Configurations]**. Detta krävs för att processen ska visas i listrutan Post Process.

## Inställningar för Publish-instansen {#settings-on-the-publish-instance}

1. logga in på `https://localhost:publishport/aem/forms`.
1. Navigera till **[!UICONTROL Letters]** om du vill visa det publicerade brevet som är tillgängligt på publiceringsinstansen.
1. Konfigurera AEM DS-inställningar. Se [Konfigurera AEM DS-inställningar](../../forms/using/configuring-the-processing-server-url.md).

>[!NOTE]
>
>När du använder arbetsflödena Forms eller AEM måste du konfigurera tjänsten DS-inställningar innan du skickar något från publiceringsservern. I annat fall ska inlämningen av blanketten misslyckas.

## Hämtning av bokstavsinstanser {#letter-instances-retrieval}

Sparade bokstavsinstanser kan hanteras ytterligare, t.ex. hämtning av bokstavsinstanser och borttagning av bokstavsinstanser, med hjälp av följande API:er som definieras i LetterInstanceService.

<table>
 <tbody>
  <tr>
   <td><strong>API på serversidan</strong></td>
   <td><strong>Åtgärdsnamn</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td><p>Public LetterInstanceVO</p> <p>getLetterInstance(String letterInstanceId)</p> <p>Aktiverar ICCException; </p> </td>
   <td>getLetterInstance</td>
   <td>Hämta angiven bokstavsinstans </td>
  </tr>
  <tr>
   <td>Public void deleteLetterInstance(String letterInstanceId) returnerar ICCException; </td>
   <td>deleteLetterInstance </td>
   <td>Den angivna bokstavsinstansen har tagits bort </td>
  </tr>
  <tr>
   <td>List getAllLetterInstances(Query) returnerar ICCException; </td>
   <td>getAllLetterInstances </td>
   <td>Denna API hämtar bokstavsinstanser baserat på indatametern. Frågeparametern kan skickas som null för att hämta alla bokstavsinstanser.<br /> </td>
  </tr>
  <tr>
   <td>Public Boolean letterInstanceExists(String letterInstanceName) returnerar ICCException; </td>
   <td>letterInstanceExists </td>
   <td>Kontrollera om det finns en LetterInstance med det angivna namnet </td>
  </tr>
 </tbody>
</table>

## Associera en postprocess med ett brev {#associating-a-post-process-with-a-letter}

I användargränssnittet för CCR utför du följande steg för att associera en postprocess med en bokstav:

1. Håll pekaren över en bokstav och välj **Visa egenskaper**.
1. Välj **Redigera**.
1. I listrutan Grundläggande egenskaper väljer du den inläggsprocess som ska associeras med brevet. Både AEM och Forms-relaterade efterbehandlingsprocesser listas i listrutan.
1. Välj **Spara**.
1. När du har konfigurerat brevet med Post Process, publicerar du brevet och eventuellt på publiceringsinstansen, anger du behandlings-URL:en AEM tjänsten DS Settings. Detta garanterar att efterbearbetningen körs på bearbetningsinstansen.

## Läsa in ett utkast  {#reloaddraft}

En förekomst av ett utkast till bokstav kan läsas in på nytt i användargränssnittet med följande URL:

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstaceID: Unikt ID för den skickade bokstavsinstansen.

Mer information om hur du sparar ett utkast finns i [Spara utkast och skicka brev](../../forms/using/create-correspondence.md#savingdrafts).
