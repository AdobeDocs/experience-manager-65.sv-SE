---
title: Ordna dina digitala resurser
description: Ordna digitala resurser, bilder, filer, mappar och så vidare med Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Ordna dina digitala resurser {#organize-digital-assets}

Alla digitala resurser, metadata och innehåll i Microsoft Office- och PDF-dokument extraheras och görs sökbara. Sökning möjliggör avancerad filtrering av resurser och respekterar fullt ut rätt behörigheter. Metadata beskrivs i detalj i metadata i Digital Asset Management.

AEM Assets har stöd för flera sätt att ordna innehåll. Du kan ordna dem hierarkiskt med hjälp av mappar eller så kan du ordna dem på ett osorterat sätt, t.ex. med hjälp av taggar. Användare kan redigera taggar i DAM-redigeraren för mediefiler där underresurser, återgivningar och metadata visas.

## Ordna resurser i mappar {#organize-using-folders}

Det mest grundläggande sättet att ordna resurser är att spara dessa i mappar. Det motsvarar att ordna filer i mappar i vårt lokala filsystem. Mer information om hur du skapar och hanterar mappar finns i [Hantera resurser](managing-assets-touch-ui.md). Hur du namnger filer och mappar, hur du ordnar undermappar och hur du hanterar filerna i dessa mappar kan påverka hur dessa resurser bearbetas. Genom att använda enhetliga och lämpliga namngivningsstrategier för filer och mappar tillsammans med god metadatapraxis kan ni få ut det mesta av era digitala resurslager.

* I de flesta fall växer din databas för digitala resurser. Därför är det viktigt att formalisera metadataanvändning, mappstruktur och filnamngivning tidigt när du skapar innehåll.
* Använd endast mappar för att få en enhetlig lagringsstruktur för dina digitala resurser. Denna konsekvens hjälper er att hantera era resurser bättre. Resurser som placeras i följande typer av mappar kan till exempel hjälpa dig att använda rätt [profiler för att bearbeta](processing-profiles.md)resurser:

   * **Utvecklingsmappar** - innehåller digitala resurser som du för närvarande arbetar med.
   * **Klientmappar** - innehåller digitala resurser baserade på klienter eller projektnamn.
   * **Huvudmappar** - innehåller digitala källresurser.
   * **Återgivningsmappar** - innehåller återgivningar och kopior av det ursprungliga digitala källmaterialet.
   * **Filstorleksmappar** - innehåller digitala resurser baserade på små, medelstora eller stora filstorlekar.
   * **Mellanlagringsmappar** - innehåller digitala resurser som är klara att publiceras live på din webbplats.
   * **MIME-typmappar** - innehåller digitala resurser som är specifika för MIME-typer som bilder, dokument och multimedia.
   * **Arkivmappar** - innehåller kasserade digitala resurser.
   * **Datumbaserade mappar** - innehåller digitala resurser baserat på skapandedatum eller senaste ändringsdatum.

* Skapa en katalog med mappar som troligtvis inte ändras så att anpassningar och automatisering fortsätter att fungera. De tilldelade bearbetningsprofilerna fortsätter till exempel att fungera.
* Om en resurs redan är publicerad använder du AEM för att flytta resursen till en annan mapp och publicera den på nytt från den nya platsen, är den ursprungliga publicerade resursplatsen fortfarande tillgänglig tillsammans med den nyligen publicerade resursen. Den ursprungliga publicerade resursen *förloras* dock i AEM och kan inte avpubliceras. Därför bör du först avpublicera en resurs och sedan flytta den till en annan mapp.

## Ordna resurser med taggar {#use-tags-to-organize-assets}

Med taggar, som metadata, kan du enkelt söka efter resurser, skapa samlingar med hjälp av sökresultaten, öka rankningen för vissa resurser och använda AI-algoritmer i Adobe Sensei för att identifiera resurser.

Adobe Experience Manager Assets använder en självlärande algoritm för att skapa mycket beskrivande taggar som gör att du kan hitta rätt resurs med bara några klick. Smart taggning använder Adobe Sensei, vårt ramverk för artificiell intelligens och maskininlärning, som kan utbildas för att känna igen och använda både standard- och företagsspecifika taggar på bilder. Smarta taggar kan även identifiera innehåll, enskilda ord eller fraser och automatiskt använda beskrivande taggar på resurser

Mer information finns i följande artiklar:

* [Om taggar i AEM](/help/sites-authoring/tags.md)
* [Redigera metadata för resurser](meta-edit.md)
* [Förbättrade smarta taggar i resurser](enhanced-smart-tags.md)

## Ordna som samlingar {#organize-as-collections}

Med resurssamlingar i Experience Manager Assets kan ni effektivisera möjligheterna att skapa, redigera och dela resurser mellan användare. Skapa flera typer av samlingar baserat på hur du använder dem, inklusive samlingar som innehåller en statisk referenslista över resurser, mappar och samlingar, samt samlingar som hämtar resurser baserat på sökvillkor.  Du kan också skapa samlingar med resurser från olika platser och dela dem med flera användare med olika åtkomstnivåer, behörighet att visa och redigera.

Mer information finns i [Hantera samlingar](managing-collections-touch-ui.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## Ordna dina resurser så att de använder profiler {#organize-to-use-profiles}

En bearbetningsprofil innehåller resurshanteringskommandon som gäller för resurser som överförs till fördefinierade mappar. Profiler används för att automatisera bearbetningen av innehållet i en mapp eller nyligen överförda resurser. Du kan använda profiler för att ordna dina resurser bättre.

Genom att standardisera metadataanvändning, filnamngivning och mappstruktur säkerställer du att du kan tillämpa bearbetningsprofiler på mappar med större precision och enhetlighet när din pool med digitala resurser växer.

Mer information om olika profiler som du kan skapa och hantera för att bearbeta resurser finns i

* [Profiler för att bearbeta metadata, bilder och videoklipp](processing-profiles.md)
* [Metadataprofiler](metadata-profiles.md)
* [Videoprofiler](video-profiles.md)
* [Dynamiska mediebildprofiler](image-profiles.md)
