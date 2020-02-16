---
title: Lägga till bilagor
seo-title: Lägga till bilagor
description: Lägga till foton och anteckningar som anteckningar i din uppgift i appen AEM Forms
seo-description: Lägga till foton och anteckningar som anteckningar i din uppgift i appen AEM Forms
uuid: 3d2738b4-fd43-44ec-8eaf-a2ad4b7e5af5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: d5976ed2-4482-495c-bf77-6d192379cfef
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Lägga till bilagor{#adding-attachments}

## Lägga till bilagor i formulär som synkroniserats med AEM Forms Workflow Server (AEM Forms on JEE) {#adding-annotations}

Med appen AEM Forms kan du bifoga bilder, anteckningar och textanteckningar i ditt formulär som synkroniseras med AEM Forms JEE-servern. Om formuläret läses in från en AEM Forms Workflow-server läggs dina bilagor till i formuläret. Du kan trycka på knappen Bifogade ![bilagor-app](assets/attachments-app.png) om du vill visa alla bifogade filer i ett formulär tillsammans. Det röda meddelandet anger antalet bilagor i formuläret. Om det inte finns några bifogade filer i formuläret kan du inte se knappen med röda meddelanden. Om det inte finns några bifogade filer i formuläret får du alternativ för att bifoga foton eller ![klotter när du trycker på knappen Bifogade](assets/attch.png).

Dina alternativ är:

* **Galleri**: Gör att du kan lägga till en bild från de bilder du har sparat på enheten.

* **Kamera**: Gör att du kan ta en bild och lägga till den i formuläret.

* **Anteckningar**: Gör att du kan lägga till en klottra eller en textanteckning. Använd ![klottra](assets/scribble.png) för att lägga till ett klottrigt och ![tangentbord](assets/keyboard.png) för att lägga till en textanteckning.

>[!NOTE]
>
>Bifogade filer som läggs till av en användare visas för andra AEM Forms-appanvändare. Andra användare kan inte ta bort bilagor som lagts till av en användare.


### Skärmen Bifogade filer {#the-attachments-screen}

Om du vill se alla bilagor på en plats trycker du på ![appen](assets/attachments-app.png)för bilagor. Du kan lägga till, byta namn på och ta bort bifogade filer här.

![Alla bilagor på en plats](assets/attachments-screen.png)

Du kan använda **+** -knappen på skärmen Bifogade filer för att bifoga ytterligare en bild, klottra eller text.

### Lägga till ett foto {#adding-a-photograph}

Du kan använda kameran på din mobila enhet eller sparade bilder på enheten för att bifoga en bild i formuläret.

1. Tryck på knappen Bifogad fil ![längst ned](assets/attch.png) i fönstret.
1. Tryck på **Gallery** eller **Camera** i popup-fönstret som visas.
1. Utför följande beroende på vilket alternativ du väljer:

   1. Om du väljer **Kamera**.

      Ta ett foto. Tryck sedan på knappen **Använd** ![use-pic](assets/use-pic.png) .

      Du kan också trycka på **Återuppta** ![om du vill ta fotot igen](assets/retake.png) .

   1. Om du väljer **Galleri**.

      Enhetens bildläsare visas. Tryck på den bild du vill bifoga i bildwebbläsaren på enheten.

### Lägga till en anteckning {#adding-a-note}

Med alternativet **Anteckningar** kan du lägga till frihandsskript och textbilagor i formuläret.

1. Tryck på knappen Bifogad fil ![längst ned](assets/attch.png) i fönstret.
1. Tryck på **Anteckningar** i popup-fönstret som visas.
1. Hämta ett frihandsskript i det användargränssnitt som startas.

   ![Klottra](assets/scribble-ui.png)

   Klottra

   Du kan använda följande alternativ i gränssnittet Klottra:

   * **Rensa**: Rensar skärmen.
   * **Knappen** Klar: Kopplar det aktuella klottret.
   * **Avbryt-knapp**: Ignorerar det aktuella klottret och avslutar användargränssnittet i klottret.
   * ![tangentbord](assets/keyboard.png): Rensar klottret och låter dig lägga till en textanteckning.
   ![Tangentbord i appen AEM Forms](assets/keyboard-inapp.png)

## Bifogade filer i formulär som synkroniseras med AEM Forms-servrar utan AEM Forms Workflow (AEM Forms on OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

Bifogade filer för mobilformulär som synkroniseras med AEM Forms OSGi-servrar fungerar på samma sätt som JEE-servrarna för AEM Forms.

Bilagor på formulärnivå stöds inte för adaptiva formulär som läses in i appen från en AEM Forms OSGi-server. Om du vill bifoga bilder eller textanteckningar aktiverar du bilagor på fältnivå i formuläret när du redigerar det. Dra och släpp den bifogade filkomponenten från komponentwebbläsaren i fältet.

När det gäller anpassningsbara formulär kan du visa de bifogade filerna i postdokumentet (DoR). Se [Generera arkivdokument för icke-XFA adaptiva formulär](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)

