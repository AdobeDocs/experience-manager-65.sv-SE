---
title: Ändra sidans nollinnehåll i Designer
seo-title: Ändra sidans nollinnehåll i Designer
description: Vet du hur du kan ändra meddelandet som visas på sidnoll i en XFA PDF när du visar det i ett visningsprogram som inte är från Adobe PDF?
seo-description: Vet du hur du kan ändra meddelandet som visas på sidnoll i en XFA PDF när du visar det i ett visningsprogram som inte är från Adobe PDF?
uuid: ac23fb21-3f15-48ea-aeeb-4ecc12b771ac
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 56b6a573-8aba-43e7-acb7-c2da45869d95
docset: aem65
translation-type: tm+mt
source-git-commit: 3cbcd23254e16231a199276aa2f9e70d6ff39b34
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---


# Ändra sidans nollinnehåll i Designer {#changing-page-zero-content-in-designer}

Sidans nollinnehåll visas som standard när ett visningsprogram som inte är från Adobe PDF, t.ex. standardvisningsprogrammet för PDF i [!DNL Chrome] eller [!DNL Firefox], inte kan läsa innehållet i PDF/XFA-formuläret. Standardmeddelandet Sidan är noll visas nedan.

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms] version av Designer låter dig ändra meddelandet som visas på sidan noll. Gör så här om du vill ändra sidans nollmeddelande:

1. Kontrollera att du har [!DNL AEM Forms]-versionen av Designer installerad. Du kan kontrollera versionen från Om-skärmen i Designer.

1. Öppna formuläret som du vill ändra sidans nollinnehåll för.

1. Klicka på **[!UICONTROL File]** > **[!UICONTROL Form Properties]**.

1. I dialogrutan [!UICONTROL Form Properties] klickar du på ![plus](assets/plus.png) (plusikonen) för att lägga till en anpassad egenskap.

1. Ange **_pagezerocontent** som namn på egenskapen.
1. Lägg till det nya sidans nollmeddelande i RTF-format som värde. Till exempel:


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. Spara formuläret som PDF.

1. Visa PDF-formuläret i webbläsaren för att bekräfta att meddelandet har uppdaterats. Exempelvärdet ovan ser ut så här:

   ![ändrat meddelande](assets/changedmessage.png)

>[!NOTE]
>
>Den anpassade egenskap som du just skapade kanske inte visas korrekt i dialogrutan Formuläregenskaper när du öppnar formuläret igen. Det fungerar dock bra och formuläret visar det uppdaterade sidnollmeddelandet.
