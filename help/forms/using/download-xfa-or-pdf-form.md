---
title: Hämta en XFA- eller PDF-formulärmall
seo-title: Hämta en XFA- eller PDF-formulärmall
description: Du kan exportera formulär från databasen till det lokala systemet och migrera de hämtade formulären till en ny databas.
seo-description: Du kan exportera formulär från databasen till det lokala systemet och migrera de hämtade formulären till en ny databas.
uuid: 5f7fbd14-cb9d-4749-8708-7efe49df89d7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 6699e0e7-fd42-41ae-86a2-3b940d905111
role: Administratör
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---


# Hämta en XFA eller en PDF-formulärmall {#download-an-xfa-or-a-pdf-form-template}

Med nedladdningsåtgärden kan du, som namnet antyder, exportera formulär från databasen till det lokala systemet. I kombination med överföringsåtgärden hjälper den här åtgärden dig att migrera dina formulär från en databas till en annan.

I AEM Forms stöds nedladdningsåtgärden för följande resurstyper:

* Formulärmallar (XFA Forms)
* PDF forms
* Dokument (platta PDF-filer)

AEM Forms stöder nedladdning av dessa formulärtyper individuellt eller i en mapp som innehåller ett eller flera formulär som stöds.

Förutom dessa resurser kan du hämta resurstypen `Resource` om den finns i en mapp. Den här funktionaliteten gör att du kan hämta den resurs som refereras av ett XFA-formulär tillsammans med formuläret.

## Hämta ett eller flera formulär {#download-one-or-more-forms}

1. Logga in på AEM Forms användargränssnitt på `https://<server>:<port>/aem/forms.html`.

1. Navigera till platsen för resursen som du vill hämta.

1. Markera resursen. Klicka på ikonen **[!UICONTROL Download]** ![aem6forms_download](assets/aem6forms_download.png) i verktygsfältet.

   >[!NOTE]
   >
   >Du kan bara välja ett formulär för hämtning. Om du vill hämta flera formulär måste du hämta dem som en mapp.

1. Klicka på **[!UICONTROL Download]** i dialogrutan som visas.

   AEM Forms genererar en ZIP-fil som innehåller den valda filen eller den valda mappen.

   Om du hämtar en mapp hämtas de resurser i mappen som stöds i deras befintliga hierarki.

   ZIP-filen sparas i mappen `Downloads` på datorn.

## Relaterade överväganden för överföringsåtgärden {#related-considerations-for-the-upload-operation}

* Du kan överföra ZIP-filen till en annan plats i samma databas eller till en annan databas
* Hierarkin för resurserna i en mapp behålls under överföringen
* Alla metadataändringar som gjorts i det hämtade materialet innan det har hämtats återspeglas vid överföringen

