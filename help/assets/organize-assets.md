---
title: Ordna dina digitala resurser
description: Ordna digitala resurser, bilder, filer, mappar och så vidare med Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# Ordna dina digitala resurser {#organize-digital-assets}

All digital assets, metadata and content of Microsoft Office and PDF documents are extracted and made searchable. Search allows sophisticated filtering on assets and fully respects the proper permissions. Metadata is covered in detail in metadata in Digital Asset Management.

AEM Assets har stöd för flera sätt att ordna innehåll. Du kan ordna dem hierarkiskt med hjälp av mappar eller så kan du ordna dem på ett osorterat sätt, t.ex. med hjälp av taggar. Användare kan redigera taggar i DAM-redigeraren för mediefiler där underresurser, återgivningar och metadata visas.

## Ordna resurser i mappar {#organize-using-folders}

Det mest grundläggande sättet att ordna resurser är att spara dessa i mappar. Det motsvarar att ordna filer i mappar i vårt lokala filsystem. Mer information om hur du skapar och hanterar mappar finns i [Hantera resurser](managing-assets-touch-ui.md). Hur du namnger filer och mappar, hur du ordnar undermappar och hur du hanterar filerna i dessa mappar kan påverka hur dessa resurser bearbetas. Genom att använda enhetliga och lämpliga namngivningsstrategier för filer och mappar tillsammans med god metadatapraxis kan ni få ut det mesta av era digitala resurslager.

* I de flesta fall växer din databas för digitala resurser. Därför är det viktigt att formalisera metadataanvändning, mappstruktur och filnamngivning tidigt när du skapar innehåll.
* Use folders only to impose a consistent storage structure for your digital assets. Denna konsekvens hjälper er att hantera era resurser bättre. Resurser som placeras i följande typer av mappar kan till exempel hjälpa dig att använda rätt [profiler för att bearbeta](processing-profiles.md)resurser:

   * **Development folders**: contains digital assets that you are currently working on.
   * **Client folders**: contains digital assets based on clients or project names.
   * **Huvudmappar**: innehåller digitala källresurser.
   * **Återgivningsmappar**: innehåller återgivningar och kopior av det ursprungliga digitala källmaterialet.
   * **Filstorleksmappar**: innehåller digitala resurser baserade på små, medelstora eller stora filstorlekar.
   * **Mellanlagringsmappar**: innehåller digitala resurser som är klara att publiceras live på din webbplats.
   * **MIME-typmappar**: innehåller digitala resurser som är specifika för MIME-typer, som bilder, dokument och multimedia.
   * **Arkivmappar**: innehåller pensionerade digitala resurser.
   * **Datumbaserade mappar**: innehåller digitala resurser baserat på skapandedatum eller senaste ändringsdatum.

* Skapa en katalog med mappar som troligtvis inte ändras så att anpassningar och automatisering fortsätter att fungera. De tilldelade bearbetningsprofilerna fortsätter till exempel att fungera.
* If an asset is already published, then you use AEM to move the asset to another folder, and re-publish from its new location, the original published asset location is still available, along with the newly re-published asset. The original published asset, however, is *lost* to AEM and cannot be unpublished. Therefore, as a best practice, first unpublish an asset and then move it to a different folder.

## Ordna resurser med taggar {#use-tags-to-organize-assets}

Med taggar, som metadata, kan du enkelt söka efter resurser, skapa samlingar med sökresultaten, öka rankningen för vissa resurser och använda AI-algoritmer i Adobe Sensei för att identifiera resurser.

Adobe Experience Manager Assets använder en självlärande algoritm för att skapa mycket beskrivande taggar som gör att du kan hitta rätt resurs med bara några klick. Smart taggning använder Adobe Sensei, vårt ramverk för artificiell intelligens och maskininlärning, som kan utbildas för att känna igen och använda både standard- och företagsspecifika taggar på bilder. Smarta taggar kan även identifiera innehåll, enskilda ord eller fraser och automatiskt använda beskrivande taggar på resurser

Mer information finns i följande artiklar:

* [Om taggar i AEM](/help/sites-authoring/tags.md)
* [Redigera metadata för resurser](meta-edit.md)
* [Förbättrade smarta taggar i resurser](enhanced-smart-tags.md)

## Ordna som samlingar {#organize-as-collections}

Med resurssamlingar i Experience Manager Assets kan ni effektivisera möjligheterna att skapa, redigera och dela resurser mellan användare. Create several types of collections based on the way you use them, including collections that contain a static reference list of assets, folders and collections, as well as collections that pull in assets based on search criteria.  You also can create collections with assets from different locations and share them with multiple users with different levels of access, viewing and editing privileges.

For more information, see [manage collections](managing-collections-touch-ui.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## Ordna dina resurser så att de använder profiler {#organize-to-use-profiles}

A processing profile contains Assets processing commands that apply to assets that get uploaded to pre-defined folders. Profiles are used to automate the processing of contents of a folder or freshly uploaded assets. You can leverage profiles to organize your assets better.

Standardizing metadata usage, file naming, and folder structure ensures that as your pool of digital assets grows, you can apply processing profiles to folders with greater precision and consistency.

For more information on various profiles that you can create and manage to process assets, see,

* [Profiles to process metadata, images, and videos](processing-profiles.md)
* [Metadataprofiler](metadata-profiles.md)
* [Video profiles](video-profiles.md)
* [Dynamiska mediebildprofiler](image-profiles.md)
