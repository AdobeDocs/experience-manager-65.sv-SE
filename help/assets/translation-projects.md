---
title: Skapa översättningsprojekt
description: Lär dig hur du skapar översättningsprojekt i AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: d15273e9308926ca4745fc1045e2da9fe8ed91d4

---


# Skapa översättningsprojekt {#creating-translation-projects}

Om du vill skapa en språkkopia utlöser du ett av följande språkkopieringsarbetsflöden som finns under referenspåret i AEM-användargränssnittet.

* **Skapa och översätt**: I det här arbetsflödet kopieras resurser som ska översättas till språkroten för det språk som du vill översätta till. Beroende på vilka alternativ du väljer skapas dessutom ett översättningsprojekt för resurserna i projektkonsolen. Beroende på inställningarna kan översättningsprojektet startas manuellt eller köras automatiskt så fort översättningsprojektet skapas.

* **Uppdatera språkkopior**: Kör det här arbetsflödet för att översätta ytterligare en grupp resurser och inkludera den i en språkkopia för en viss språkinställning. I det här fallet läggs de översatta resurserna till i målmappen som redan innehåller tidigare översatta resurser.

>[!NOTE]
>
>Resursbinärfiler översätts bara om översättningstjänsten stöder översättning av binärfiler.

>[!NOTE]
>
>Om du startar ett översättningsarbetsflöde för komplexa resurser, som PDF- och InDesign-filer, skickas inte delresurserna eller återgivningarna (om sådana finns) för översättning.

## Skapa och översätta arbetsflöde {#create-and-translate-workflow}

Du använder arbetsflödet för att skapa och översätta för att generera språkkopior för ett visst språk för första gången. Arbetsflödet innehåller följande alternativ:

* Skapa endast struktur
* Skapa ett nytt översättningsprojekt
* Lägg till i befintligt översättningsprojekt

### Skapa endast struktur {#create-structure-only}

Använd alternativet **[!UICONTROL Skapa endast struktur]** om du vill skapa en målmappshierarki i målspråkets rot för att matcha källmappens hierarki i källspråkets rot. I det här fallet kopieras källresurserna till målmappen. Inget översättningsprojekt genereras emellertid.

1. I resursgränssnittet väljer du den källmapp som du vill skapa en struktur för i målspråkets rot.
1. Öppna rutan **[!UICONTROL Referenser]** och klicka/tryck på **[!UICONTROL Språkkopior]** under **[!UICONTROL Kopior]**.

   ![chlimage_1-57](assets/chlimage_1-57.png)

1. Klicka/tryck på **[!UICONTROL Skapa och översätt]** längst ned.

   ![chlimage_1-58](assets/chlimage_1-58.png)

1. From the **[!UICONTROL Target Languages]** list, select the language for which you want to create a folder structure.

   ![chlimage_1-59](assets/chlimage_1-59.png)

1. I **[!UICONTROL projektlistan]** väljer du bara **** Skapa struktur.

   ![chlimage_1-60](assets/chlimage_1-60.png)

1. Klicka/tryck på **[!UICONTROL Skapa]**. Den nya strukturen för målspråket listas under **[!UICONTROL Språkkopior]**.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Klicka på/tryck på strukturen i listan och klicka/tryck sedan på **[!UICONTROL Visa i resurser]** för att navigera till mappstrukturen i målspråket.

   ![chlimage_1-62](assets/chlimage_1-62.png)

### Skapa ett nytt översättningsprojekt {#create-a-new-translation-project}

Om du använder det här alternativet kopieras resurser som ska översättas till språkroten för det språk som du vill översätta till. Beroende på vilka alternativ du väljer skapas ett översättningsprojekt för resurserna i projektkonsolen. Beroende på inställningarna kan översättningsprojektet startas manuellt eller automatiskt så snart översättningsprojektet skapas.

1. I resursgränssnittet väljer du den källmapp som du vill skapa en språkkopia för.
1. Öppna rutan **[!UICONTROL Referenser]** och klicka/tryck på **[!UICONTROL Språkkopior]** under **[!UICONTROL Kopior]**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

1. Klicka/tryck på **[!UICONTROL Skapa och översätt]** längst ned.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. From the **[!UICONTROL Target Languages]** list, select the language(s) for which you want to create a folder structure.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Välj **[!UICONTROL Skapa ett nytt översättningsprojekt]** i listan **[!UICONTROL Projekt]**.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. In the **[!UICONTROL Project Title]** field, enter a title for the project.

   ![chlimage_1-67](assets/chlimage_1-67.png)

1. Klicka/tryck på **[!UICONTROL Skapa]**. Resurser från källmappen kopieras till målmapparna för de språkinställningar du valde i steg 4.

   ![chlimage_1-68](assets/chlimage_1-68.png)

1. Om du vill navigera till mappen markerar du språkkopian och klickar på **[!UICONTROL Visa i Resurser]**.

   ![chlimage_1-69](assets/chlimage_1-69.png)

1. Navigera till projektkonsolen. Översättningsmappen kopieras till projektkonsolen.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Öppna mappen för att visa översättningsprojektet.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Klicka/tryck på projektet för att öppna informationssidan.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Om du vill visa översättningsjobbets status klickar du på ellipsen längst ned i rutan **[!UICONTROL Översättningsjobb]** .

   ![chlimage_1-73](assets/chlimage_1-73.png)

   Mer information om jobbstatus finns i [Övervaka status för ett översättningsjobb](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Navigera till resursgränssnittet och öppna sidan Egenskaper för var och en av de översatta resurserna för att visa översatta metadata.

   ![visa översatta metadata på sidan Egenskaper för resurs](assets/translated-metadata-asset-properties.png)

   *Bild: Översatta metadata på sidan med resursegenskaper*


   >[!NOTE]
   >
   >Den här funktionen är tillgänglig både för resurser och mappar. När en resurs väljs i stället för en mapp kopieras hela mapphierarkin upp till språkroten för att skapa en språkkopia för resursen.

### Lägg till i befintligt översättningsprojekt {#add-to-existing-translation-project}

Om du använder det här alternativet körs översättningsarbetsflödet för resurser som du lägger till i källmappen efter att ha kört ett tidigare arbetsflöde för översättning. Endast resurser som nyligen lagts till kopieras till målmappen som innehåller tidigare översatta resurser. Inget nytt översättningsprojekt skapas i det här fallet.

1. Navigera till källmappen som innehåller oöversatta resurser i resursgränssnittet.
1. Select an asset you want to translate, and open the **[!UICONTROL Reference pane]**. The **[!UICONTROL Language Copies]** section displays the number of translation copies that are currently available.
1. Klicka/tryck på **[!UICONTROL Språkkopior]** under **[!UICONTROL Kopior]**. En lista över tillgängliga översättningskopior visas.
1. Klicka/tryck på **[!UICONTROL Skapa och översätt]** längst ned.

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. From the **[!UICONTROL Target Languages]** list, select the language(s) for which you want to create a folder structure.

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. I listan **[!UICONTROL Projekt]** väljer du **[!UICONTROL Lägg till i befintligt översättningsprojekt]** för att köra översättningsarbetsflödet i mappen.

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >Om du väljer alternativet **[!UICONTROL Lägg till i befintligt översättningsprojekt]** läggs ditt översättningsprojekt till i ett befintligt projekt endast om dina projektinställningar exakt matchar inställningarna för det befintliga projektet. Annars skapas ett nytt projekt.

1. I listan **[!UICONTROL Befintliga översättningsprojekt]** väljer du ett projekt som du vill lägga till resursen för översättning.

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Klicka/tryck på **[!UICONTROL Skapa]**. Resurserna som ska översättas läggs till i målmappen. The updated folder is listed under the **[!UICONTROL Language Copies]** section.

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. Navigera till projektkonsolen och öppna det befintliga översättningsprojektet som du har lagt till i.
1. Klicka/tryck på sidan med projektinformation för översättning.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Klicka på/tryck på ellipsen längst ned i rutan **Översättningsjobb** för att visa resurserna i översättningsarbetsflödet. I översättningsjobblistan visas även poster för metadata och taggar för resurser. Dessa poster anger att metadata och taggar för resurserna också översätts.

   >[!NOTE]
   >
   >Om du tar bort posten för taggar eller metadata översätts inga taggar eller metadata för resurserna.

   >[!NOTE]
   >
   >Om du använder maskinöversättning översätts inte resursens binärfiler.

   >[!NOTE]
   >
   >Om den resurs som du lägger till i översättningsjobbet innehåller delresurser, markerar du delresurserna och tar bort dem för översättningen för att fortsätta utan några fel.

1. Om du vill starta översättningen av resurserna klickar/trycker du på pilen på **[!UICONTROL översättningsjobbpanelen]** och väljer **[!UICONTROL Start]** i listan.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   Ett meddelande meddelar när översättningsjobbet påbörjas.

   ![chlimage_1-82](assets/chlimage_1-82.png)

1. Om du vill visa översättningsjobbets status klickar/trycker du på ellipsen längst ned i rutan **[!UICONTROL Översättningsjobb]** .

   ![chlimage_1-83](assets/chlimage_1-83.png)

   Mer information finns i [Övervaka status för ett översättningsjobb](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. När översättningen är klar ändras statusen till Klart för granskning. Navigera till resursgränssnittet och öppna sidan Egenskaper för var och en av de översatta resurserna för att visa översatta metadata.

## Uppdatera språkkopior {#update-language-copies}

Kör det här arbetsflödet för att översätta alla ytterligare resurser och inkludera dem i en språkkopia för en viss språkinställning. I det här fallet läggs de översatta resurserna till i målmappen som redan innehåller tidigare översatta resurser. Beroende på vilka alternativ du väljer skapas ett översättningsprojekt eller så uppdateras ett befintligt översättningsprojekt för de nya resurserna. Arbetsflödet för att uppdatera språkkopior innehåller följande alternativ:

* Skapa ett nytt översättningsprojekt
* Lägg till i befintligt översättningsprojekt

### Skapa ett nytt översättningsprojekt {#create-a-new-translation-project-1}

Om du använder det här alternativet skapas ett översättningsprojekt för den resursuppsättning som du vill uppdatera en språkkopia för.

1. I resursgränssnittet väljer du den källmapp där du lade till en resurs.
1. Open the **[!UICONTROL References]** pane, and click/tap **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]** to display the list of language copies.
1. Select the check box before **[!UICONTROL Language Copies]**, and then select the target folder corresponding to the appropriate locale.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. Klicka/tryck på **[!UICONTROL Uppdatera språkkopior]** längst ned.

   ![chlimage_1-85](assets/chlimage_1-85.png)

1. Välj **[!UICONTROL Skapa ett nytt översättningsprojekt]** i listan **[!UICONTROL Projekt]**.

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. In the **[!UICONTROL Project Title]** field, enter a title for the project.

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. Klicka/tryck på **[!UICONTROL Start]**.
1. Navigera till projektkonsolen. Översättningsmappen kopieras till projektkonsolen.

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Öppna mappen för att visa översättningsprojektet.

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. Klicka/tryck på projektet för att öppna informationssidan.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Om du vill starta översättningen av resurserna klickar du på pilen på **[!UICONTROL översättningsjobbpanelen]** och väljer **[!UICONTROL Start]** i listan.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   Ett meddelande meddelar när översättningsjobbet påbörjas.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Om du vill visa översättningsjobbets status klickar/trycker du på ellipsen längst ned i rutan **[!UICONTROL Översättningsjobb]** .

   ![chlimage_1-93](assets/chlimage_1-93.png)

   Mer information om jobbstatus finns i [Övervaka status för ett översättningsjobb](../sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Navigera till resursgränssnittet och öppna sidan Egenskaper för var och en av de översatta resurserna för att visa översatta metadata.

### Lägg till i befintligt översättningsprojekt {#add-to-existing-translation-project-1}

Om du använder det här alternativet läggs resursuppsättningen till i ett befintligt översättningsprojekt för att uppdatera språkkopian för det språkområde du väljer.

1. I resursgränssnittet väljer du den källmapp där du lade till en resursmapp.
1. Open the **[!UICONTROL References pane]**, and click/tap **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]** to display the list of language copies.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Select the check box before **[!UICONTROL Language Copies]**, which selects all language copies. Avmarkera andra kopior än den språkkopia (kopior) som motsvarar det eller de språk som du vill översätta till.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Klicka/tryck på **[!UICONTROL Uppdatera språkkopior]** längst ned.

   ![chlimage_1-96](assets/chlimage_1-96.png)

1. Välj **[!UICONTROL Lägg till i befintligt översättningsprojekt]** i listan **[!UICONTROL Projekt]**.

   ![chlimage_1-97](assets/chlimage_1-97.png)

1. I listan **[!UICONTROL Befintliga översättningsprojekt]** väljer du ett projekt som du vill lägga till resursen för översättning.

   ![chlimage_1-98](assets/chlimage_1-98.png)

1. Klicka/tryck på **[!UICONTROL Start]**.
1. Se steg 9-14 i [Lägg till i befintligt översättningsprojekt](translation-projects.md#add-to-existing-translation-project) för att slutföra resten av proceduren.

## Skapa tillfälliga språkkopior {#creating-temporary-language-copies}

När du kör ett översättningsarbetsflöde för att uppdatera en språkkopia med redigerade versioner av originalresurser bevaras den befintliga språkkopian tills du godkänner översatta resurser. AEM Resurser lagrar de nyligen översatta resurserna på en tillfällig plats och uppdaterar den befintliga språkkopian när du uttryckligen har godkänt resurserna. Om du avvisar resurserna ändras inte språkkopian.

1. Click/tap the source root folder under **[!UICONTROL Language Copies]** for which you already created a language copy, and then click/tap **[!UICONTROL Reveal in Assets]** to open the folder in AEM Assets.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. I resursgränssnittet markerar du en resurs som du redan har översatt och klickar/trycker på **[!UICONTROL redigeringsikonen]** i verktygsfältet för att öppna resursen i redigeringsläge.
1. Redigera resursen och spara sedan ändringarna.
1. Uppdatera språkkopian genom att utföra steg 2-14 i proceduren [Lägg till i befintligt översättningsprojekt](#add-to-existing-translation-project) .
1. Klicka på/tryck på ellipsen längst ned i rutan **[!UICONTROL Översättningsjobb]** . I listan över resurser på sidan **[!UICONTROL Översättningsjobb]** kan du tydligt visa den tillfälliga plats där den översatta versionen av resursen lagras.

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. Markera kryssrutan bredvid **[!UICONTROL Titel]**.
1. From the toolbar, click/tap **[!UICONTROL Accept Translation]** and then click/tap **[!UICONTROL Accept]** in the dialog to overwrite the translated asset in the target folder with the translated version of the edited asset.

   ![chlimage_1-102](assets/chlimage_1-102.png)

   >[!NOTE]
   >
   >Om du vill att översättningsarbetsflödet ska kunna uppdatera målresurserna, godkänner du både resursen och metadata.

   Klicka/tryck på **[!UICONTROL Avvisa översättning]** om du vill behålla den ursprungligen översatta versionen av resursen i målspråkets rot och avvisa den redigerade versionen.

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. Navigera till resurskonsolen och öppna sidan Egenskaper för var och en av de översatta resurserna för att visa översatta metadata.

Tips om hur du översätter metadata för resurser effektivt finns i [5 steg för effektiv översättning av metadata](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/).
