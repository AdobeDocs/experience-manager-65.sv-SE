---
title: Aktivera bilagor för ett HTML5-formulär
seo-title: Aktivera bilagor för ett HTML5-formulär
description: Bifogade filer i HTML5-formulär är som standard inaktiverade.
seo-description: Bifogade filer i HTML5-formulär är som standard inaktiverade.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: Mobile Forms
exl-id: 68912260-179a-4d1b-b944-0a1777c021ac
source-git-commit: 6e2a0f053a1f6989524e9ae2b1dcb001b0397ac6
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# Aktivera bilagor för ett HTML5-formulär {#enabling-attachments-for-an-html-form}

Du kan överföra, förhandsgranska och skicka bilagor med HTML5-formulär. Som standard är stöd för bifogade filer inaktiverat. Så här aktiverar du stöd för bifogade filer:

1. Skapa en [anpassad profil](/help/forms/using/custom-profile.md) med en `mfAttachmentOptions` flervalsegenskap. Varje sträng i egenskapen `mfAttachmentOptions` måste ha ett `property=value`-format för att kunna konfigurera alternativ för widgeten för bifogade filer. `property` och `value` kan ha något av följande värden:

   | Egenskap | Värde |
   |--- |---|
   | multiSelect | true eller false (true som standard) |
   | fileSizeLimit | Antal i MB (2 MB som standard). Exempel: 5. |
   | buttonText | Knapptext för popup-fönster (&quot;Bifoga&quot; som standard) |
   | acceptera | kommaavgränsad lista över filtyper som ska accepteras (&quot;ljud/&amp;ast;, video/&amp;ast;, bild/&amp;ast;, text/&amp;ast;, .pdf&quot; som standard) |

   Till exempel:

   ![konfigurera alternativ](assets/mfAttachmentOptions.png)

   Om det behövs kan du även ange fler anpassade alternativ för egenskapen `mfAttachmentOptions`.

   >[!NOTE]
   >
   >I Microsoft Internet Explorer 9 kan användare bifoga filer som är större än den angivna gränsen. Det är ett känt problem.

1. Använd [metadataredigeraren](/help/forms/using/manage-form-metadata.md) för att välja den anpassade profil som du har skapat ovan för HTML 5-formulär.
1. Rendera formulärmallen med en anpassad profil och ikonen för bilagor visas i formulärverktygsfältet.

   >[!NOTE]
   >
   >Formulärportalen har en anpassad profil med funktioner för utkast och bilagor aktiverade. Mer information om profilen **Spara som utkast** finns i [Spara HTML5-formulär som ett utkast](/help/forms/using/saving-html5-form-draft.md).

1. Klicka på ikonen för bifogade filer, så visas en dialogruta för val av bifogade filer. Bläddra och markera den bifogade filen och klicka på **Bifoga**.

   >[!NOTE]
   >
   >Om du vill förhandsgranska en bifogad fil klickar du på namnet på den bifogade filen.

   >[!NOTE]
   >
   >Filförhandsvisningsalternativet är inte tillgängligt för anonyma användare.

## Bifogad filinlämningsformat {#attachment-submission-format}

När bilagor är aktiverade skickar HTML5-formulär multipart-data. Flerdelsdata har två delar **dataXml** och **bilagor**.

>[!NOTE]
>
>För bakåtkompatibilitet gäller att om `mfAllowAttachments`-alternativet är inaktiverat skickar HTML5-formulären inte multipart-data. Det skickar enkel data-xml i formatet **application/xml**.

Om mfAllowAttachments-flaggan är aktiverad skickar [tjänstproxytjänsten](/help/forms/using/service-proxy.md) även multipart-data med dataXml och bilagor.
