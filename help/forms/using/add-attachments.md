---
title: Lägga till bilagor
description: Lägga till foton och anteckningar som anteckningar till dina uppgifter i AEM Forms-appen
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# Lägga till bilagor{#adding-attachments}

## Lägga till bilagor i formulär som har synkroniserats med AEM Forms Workflow Server (AEM Forms on JEE) {#adding-annotations}

Med AEM Forms-appen kan du bifoga bilder, anteckningar och textanteckningar i ditt formulär som synkroniseras med AEM Forms JEE-servern. Om formuläret läses in från en AEM Forms Workflow-server läggs dina bilagor till i formuläret. Du kan välja knappen för bifogade filer ![attachments-app](assets/attachments-app.png) om du vill se alla bilagor i ett formulär tillsammans. Det röda meddelandet anger antalet bilagor i formuläret. Om det inte finns några bifogade filer i formuläret kan du inte se knappen med röda meddelanden. Om det inte finns några bilagor i formuläret, när du markerar knappen för bilagor ![bifoga](assets/attch.png), får du alternativ för att bifoga foton eller klotter.

Dina alternativ är:

* **Galleri**: Gör att du kan lägga till en bild från de bilder som har sparats på enheten.

* **Kamera**: Gör att du kan ta en bild och lägga till den i formuläret.

* **Anteckningar**: Gör att du kan lägga till en klottra eller en textanteckning. Använd ![klottra](assets/scribble.png) för att lägga till en klocka, och ![tangentbord](assets/keyboard.png) om du vill lägga till en textanteckning.

>[!NOTE]
>
>Bifogade filer som läggs till av en användare visas för andra AEM Forms-appanvändare. Andra användare kan inte ta bort bilagor som lagts till av en användare.
>

### Skärmen Bifogade filer {#the-attachments-screen}

Om du vill se alla bilagor på en plats väljer du ![attachments-app](assets/attachments-app.png). Du kan lägga till, byta namn på och ta bort bifogade filer här.

![Alla bilagor på en plats](assets/attachments-screen.png)

Du kan använda **+** på skärmen Bifogade filer om du vill bifoga ytterligare en bild, klottra eller text.

### Lägga till ett foto {#adding-a-photograph}

Du kan använda kameran på din mobila enhet eller sparade bilder på enheten för att bifoga en bild i formuläret.

1. Markera knappen för bifogade filer ![bifoga](assets/attch.png) längst ned i fönstret.
1. Välj **Galleri** eller **Kamera** i popup-fönstret som visas.
1. Utför följande beroende på vilket alternativ du väljer:

   1. Om du väljer **Kamera**.

      Ta ett foto. Välj sedan **Använd** ![use-pic](assets/use-pic.png) -knappen.

      Eller välj **Återuppta** ![återta](assets/retake.png) för att ta om fotot.

   1. Om du väljer **Galleri**.

      Enhetens bildläsare visas. Markera den bild som du vill bifoga i bildwebbläsaren på enheten.

### Lägga till en anteckning {#adding-a-note}

The **Anteckningar** kan du lägga till frihandsskript och textbilagor i formuläret.

1. Markera knappen för bifogade filer ![bifoga](assets/attch.png) längst ned i fönstret.
1. Välj **Anteckningar** i popup-fönstret som visas.
1. Hämta ett frihandsskript i det användargränssnitt som startas.

   ![Klottra](assets/scribble-ui.png)

   Klottra

   Du kan använda följande alternativ i gränssnittet Klottra:

   * **Rensa**: Rensar skärmen.
   * **Knappen Klar**: Kopplar det aktuella klottret.
   * **Avbryt-knapp**: Ignorerar det aktuella skriptet och avslutar användargränssnittet i klotterprogrammet.
   * ![tangentbord](assets/keyboard.png): Rensar klottret och låter dig lägga till en textanteckning.

   ![Tangentbord i AEM Forms app scribble](assets/keyboard-inapp.png)

## Bifogade filer i formulär som synkroniseras med AEM Forms-servrar utan AEM Forms Workflow (AEM Forms on OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

Bifogade filer för mobilformulär som synkroniseras med AEM Forms OSGi-servrar fungerar på samma sätt som AEM Forms JEE-servrar.

Bilagor på formulärnivå stöds inte för adaptiva formulär som läses in i appen från en AEM Forms OSGi-server. Om du vill bifoga bilder eller textanteckningar aktiverar du bilagor på fältnivå i formuläret när du redigerar det. Dra och släpp den bifogade filkomponenten från komponentwebbläsaren i fältet.

Om det finns adaptiva formulär kan du visa de bifogade filerna i postdokumentet (DoR). Se, [Generera arkivdokument för icke-XFA adaptiva formulär](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).
