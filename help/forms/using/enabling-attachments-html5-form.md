---
title: Aktivera bilagor för ett HTML5-formulär
description: Som standard är bilagesupport för HTML5-formulär inaktiverat.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: HTML5 Forms
exl-id: 68912260-179a-4d1b-b944-0a1777c021ac
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Aktivera bilagor för ett HTML5-formulär {#enabling-attachments-for-an-html-form}

Du kan överföra, förhandsgranska och skicka bilagor med HTML5-formulär. Som standard är stöd för bifogade filer inaktiverat. Så här aktiverar du stöd för bifogade filer:

1. Skapa en [egen profil](/help/forms/using/custom-profile.md) med `mfAttachmentOptions` flervälj strängsegenskap. Varje sträng i `mfAttachmentOptions` egenskapen måste ha en `property=value` format för att konfigurera alternativ för widgeten för bifogade filer. The `property` och `value` kan ha något av följande värden:

   | Egenskap | Värde |
   |--- |---|
   | multiSelect | true eller false (true som standard) |
   | fileSizeLimit | Antal i MB (2 MB som standard). Exempel: 5. |
   | buttonText | Knapptext för popup-fönster (&quot;Bifoga&quot; som standard) |
   | acceptera | kommaavgränsad lista över filtyper som ska accepteras (&quot;ljud/&amp;ast;, video/&amp;ast;, bild/&amp;ast;, text/&amp;ast;, .pdf&quot; som standard) |

   Till exempel:

   ![konfigurera alternativ](assets/mfAttachmentOptions.png)

   Om det behövs kan du även ange fler anpassade alternativ för `mfAttachmentOptions` -egenskap.

   >[!NOTE]
   >
   >I Microsoft Internet Explorer 9 kan användare bifoga filer som är större än den angivna gränsen. Det är ett känt problem.

1. Använd [metadataredigerare](/help/forms/using/manage-form-metadata.md) för att välja den anpassade profil som du har skapat ovan för formulär i HTML 5.
1. Rendera formulärmallen med en anpassad profil och ikonen för bilagor visas i formulärverktygsfältet.

   >[!NOTE]
   >
   >Formulärportalen har en anpassad profil med funktioner för utkast och bilagor aktiverade. Mer information om **Spara som utkast** profil, se [Spara HTML5-formulär som ett utkast](/help/forms/using/saving-html5-form-draft.md).

1. Klicka på ikonen för bifogade filer, så visas en dialogruta för val av bifogade filer. Bläddra och markera den bifogade filen och klicka på **Bifoga**.

   >[!NOTE]
   >
   >Klicka på namnet på den bifogade filen om du vill förhandsgranska den.

   >[!NOTE]
   >
   >Filförhandsvisningsalternativet är inte tillgängligt för anonyma användare.

## Bifogad filinlämningsformat {#attachment-submission-format}

När bilagor är aktiverade skickar HTML5-formuläret multipart-data. Flerdelsdata har två delar **dataXml** och **bilagor**.

>[!NOTE]
>
>För bakåtkompatibilitet, om `mfAllowAttachments` om alternativet är inaktiverat, skickar inte HTML5-formulären data som består av flera delar. Det skickar enkel data xml i **application/xml** format.

Om flaggan mfAllowAttachments är aktiverad visas [skicka tjänstproxytjänst](/help/forms/using/service-proxy.md) skickar också multipart-data med dataXml och bilagor.
