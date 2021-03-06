---
title: Ordna dina digitala resurser
description: Organisera dina digitala resurser, bilder, filer, mappar och så vidare med Experience Manager.
contentOwner: AG
role: User
feature: Asset Management,Search
exl-id: d6f815b5-e4fc-4f8c-a6c1-9e50035ab9f2
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Ordna dina digitala resurser {#organize-digital-assets}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/organize-assets.html?lang=en) |
| AEM 6.5 | Den här artikeln |
| AEM 6.4 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/organize-assets.html?lang=en) |

Alla digitala resurser, metadata och innehåll i Microsoft Office- och PDF-dokument extraheras och görs sökbara. Sökning möjliggör avancerad filtrering av resurser och respekterar fullt ut rätt behörigheter. Metadata beskrivs i detalj i metadata i Digital Asset Management.

[!DNL Experience Manager Assets] har stöd för flera sätt att ordna innehåll. Du kan ordna dem hierarkiskt med hjälp av mappar eller så kan du ordna dem på ett osorterat sätt, t.ex. med hjälp av taggar. Användare kan redigera taggar i DAM-redigeraren för mediefiler där underresurser, återgivningar och metadata visas.

## Ordna resurser i mappar {#organize-using-folders}

Det mest grundläggande sättet att ordna resurser är att spara dessa i mappar. Det motsvarar att ordna filer i mappar i vårt lokala filsystem. Mer information om hur du skapar och hanterar mappar finns i [Hantera resurser](manage-assets.md). Hur du namnger filer och mappar, hur du ordnar undermappar och hur du hanterar filerna i dessa mappar kan påverka hur dessa resurser bearbetas. Genom att använda enhetliga och lämpliga namngivningsstrategier för filer och mappar tillsammans med god metadatapraxis kan ni få ut det mesta av era digitala resurslager.

* I de flesta fall växer din databas för digitala resurser. Därför är det viktigt att formalisera metadataanvändning, mappstruktur och filnamngivning tidigt när du skapar innehåll.
* Använd endast mappar för att få en enhetlig lagringsstruktur för dina digitala resurser. Denna konsekvens hjälper er att hantera era resurser bättre. Resurser som placerats i följande typer av mappar kan till exempel hjälpa dig att använda rätt [profiler som ska användas för bearbetning av tillgångar](processing-profiles.md):

   * **Utvecklingsmappar**: innehåller digitala resurser som du arbetar med just nu.
   * **Klientmappar**: innehåller digitala resurser baserade på klienter eller projektnamn.
   * **Primära mappar**: innehåller digitala källresurser.
   * **Återgivningsmappar**: innehåller återgivningar och kopior av det ursprungliga digitala källmaterialet.
   * **Filstorleksmappar**: innehåller digitala resurser baserade på små, medelstora eller stora filstorlekar.
   * **Mellanlagringsmappar**: innehåller digitala resurser som är klara att publiceras live på din webbplats.
   * **MIME-typmappar**: innehåller digitala resurser som är specifika för MIME-typer, som bilder, dokument och multimedia.
   * **Arkivera mappar**: innehåller pensionerade digitala resurser.
   * **Datumbaserade mappar**: innehåller digitala resurser baserat på skapandedatum eller senaste ändringsdatum.

* Skapa en katalog med mappar som troligtvis inte ändras så att anpassningar och automatisering fortsätter att fungera. De tilldelade bearbetningsprofilerna fortsätter till exempel att fungera.
* Om en resurs redan har publicerats använder du [!DNL Experience Manager] om du vill flytta resursen till en annan mapp och publicera på nytt från den nya platsen är den ursprungliga publicerade resursplatsen fortfarande tillgänglig, tillsammans med den nyligen publicerade resursen. Den ursprungliga publicerade resursen är dock *vilse* till [!DNL Experience Manager] och kan inte avpubliceras. Därför bör du först avpublicera en resurs och sedan flytta den till en annan mapp.

## Ordna resurser med taggar {#use-tags-to-organize-assets}

Med taggar, som metadata, kan du enkelt söka efter resurser, skapa samlingar med hjälp av sökresultaten, öka rankningen för vissa resurser och använda AI-algoritmer i Adobe Sensei för att identifiera resurser.

[!DNL Adobe Experience Manager Assets] använder en självlärande algoritm för att skapa mycket beskrivande taggar som gör att du kan hitta rätt resurs med bara några klick. Smart taggning använder Adobe Sensei, vårt ramverk för artificiell intelligens och maskininlärning, som kan utbildas för att känna igen och använda både standard- och företagsspecifika taggar på bilder. Smarta taggar kan även identifiera innehåll, enskilda ord eller fraser och automatiskt använda beskrivande taggar på resurser

Mer information finns i följande artiklar:

* [Om taggar i Experience Manager](/help/sites-authoring/tags.md)
* [Redigera metadata för resurser](metadata.md)
* [Förbättrade smarta taggar i resurser](enhanced-smart-tags.md)

## Ordna som samlingar {#organize-as-collections}

Med resurssamlingar i [!DNL Experience Manager Assets]kan du effektivisera möjligheten att skapa, redigera och dela resurser mellan användare. Skapa flera typer av samlingar baserat på hur du använder dem, inklusive samlingar som innehåller en statisk referenslista över resurser, mappar och samlingar, samt samlingar som hämtar resurser baserat på sökvillkor.  Du kan också skapa samlingar med resurser från olika platser och dela dem med flera användare med olika åtkomstnivåer, behörighet att visa och redigera.

Mer information finns i [hantera samlingar](manage-collections.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## Ordna dina resurser så att de använder profiler {#organize-to-use-profiles}

En bearbetningsprofil innehåller [!DNL Assets] bearbetningskommandon som gäller för resurser som överförs till fördefinierade mappar. Profiler används för att automatisera bearbetningen av innehållet i en mapp eller nyligen överförda resurser. Du kan använda profiler för att ordna dina resurser bättre.

Genom att standardisera metadataanvändning, filnamngivning och mappstruktur säkerställer du att du kan tillämpa bearbetningsprofiler på mappar med större precision och enhetlighet när din pool med digitala resurser växer.

>[!MORELIKETHIS]
>
>* [Profiler för att bearbeta metadata, bilder och videoklipp](processing-profiles.md).
>* [Metadataprofiler](/help/assets/metadata-config.md#metadata-profiles).
>* [Videoprofiler](video-profiles.md).
>* [Dynamic Media bildprofiler](image-profiles.md).

