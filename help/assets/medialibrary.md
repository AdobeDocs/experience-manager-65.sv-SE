---
title: Använd Media Library för grundläggande hantering av digitala resurser
description: '[!DNL Experience Manager Assets] och Media Library för resurshantering.'
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---


# Använd Media Library för grundläggande resurshantering {#manage-assets-using-media-library}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/medialibrary.html?lang=en) |
| AEM 6.5 | Den här artikeln |

Plattformen [!DNL Adobe Experience Manager] har olika funktioner för att hantera resurser. Med Media Library kan användarna överföra ett litet antal resurser till databasen, söka efter och använda dem på webbsidorna och utföra enkla resurshanteringsåtgärder på resurserna.

Media Library är en lättviktig DAM-lösning (Digital Asset Management) som medföljer licensen [!DNL Adobe Experience Manager Sites]. [!DNL Sites] är ett WCM-erbjudande (Web Content Management). Media Library fungerar med alla funktioner i Experience Manager.

[!DNL Adobe Experience Manager Assets]-licensen är tillgänglig separat för inköp. I [!DNL Experience Manager Assets] kan du hantera resurser på ett robust sätt via användningsexempel, anpassningar för metadata, scheman, sökning och användargränssnitt samt många andra funktioner utöver vad Media Library erbjuder.

## Licenskrav {#avail-media-library-license}

Kunder som har [!DNL Sites] licens har rätt att använda Media Library. Det fungerar med alla komponenter i [!DNL Experience Manager].

Media Library installeras som en del av Sites. Ingen ytterligare licens eller paket krävs utöver Sites-licens och -installation.

## [!DNL Assets] jämfört med Media Library {#assets-and-media-library}

Experience Manager Assets tillhandahåller DAM-funktionalitet i enterpriseklass. Assets-funktionaliteten levereras med [!DNL Experience Manager] i ett enda paket. Användare som inte har köpt någon Assets-licens har dock inte rätt att använda de avancerade DAM-funktionerna. Utan Assets-licens är endast [Media Library-funktioner](#use-media-library) tillgängliga.

Om du vill förhindra oavsiktlig användning av [!DNL Assets]-funktioner som du inte har licensierat tar du bort alla [!DNL Assets]-specifika arbetsflöden, komponenter, taxonomier, alternativ och [!DNL Assets]-administratören från [!DNL Experience Manager]. På så sätt förhindras användarna från att oavsiktligt använda [!DNL Assets]-funktioner som du inte har licensierat.

## Använd Media Library {#use-media-library}

Media Library har grundläggande DAM-funktioner för följande användningsområden:

* Webbsidor skapade med [!DNL Adobe Experience Manager Sites].
* Anpassningsbara formulär och kommunikation som skapats med [!DNL Adobe Experience Manager Forms].
* Digitala skärmupplevelser som skapats med [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] HTTP REST API:er för headless-åtgärder.

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

Om du vill använda Media Library-funktionen kan du använda standardanvändargränssnittet för [!DNL Experience Manager]. Media Library ingår i installationen av [!DNL Experience Manager Sites] och inget separat gränssnitt eller tillägg krävs. Med det befintliga gränssnittet har Media Library-användare rätt att utföra följande uppgifter:

* Skapa mappar för att ordna resurser.
* Överför resurser.
* Publish Assets.
* Redigera, flytta och kopiera resurser.
* Bläddra bland, filtrera och söka (inklusive likhetssökning) resurser.
* Lägg till värden i och redigera värdena i metadatafälten, förutom fältet Smarta taggar, som är tillgängliga på fliken [!UICONTROL Basic] på en resurs [!UICONTROL Properties] -sida som standard.
* Lägg till och ta bort statiska återgivningar.
* Hämta mappar, resurser och resursrenderingar.
* Skapa resursversioner.
* Skapa och utför granskningsåtgärder på resurser.
* Anteckna resurser.
* Lägg till resurser på [!DNL Sites] sidor via Content Finder.
* Använd [!DNL Content Fragments].
* Använd HTTP REST och GraphQL API:er för [!DNL Content Fragments] och refererade medieresurser, under Sites-licens.
* Integrering med Marketing Cloud.
* Anpassa och utöka gränssnittet för resurshantering.
* Gå till Query Builder (API) för att utöka sökfunktionen.
* Skapa statiska taggar.
* Skapa projekt och uppgifter.
* Activity stream (timeline).
* Kommentarer och kommentarer.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we do not have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>Många avancerade DAM-användningsfall uppfylls av [!DNL Experience Manager Assets]. Media Library-licens berättigar dig att endast fylla i de angivna användningsområdena med Media Library. Om ett användningsexempel inte finns med i listan ska du inte använda det med Media Library-licens. Kontakta Adobe kundsupport om du har frågor.

Observera att du inte kan använda smarta taggar, [!DNL Asset]-länk, [!DNL Asset]-väljare, bulktaggning, ändra resursarbetsflöden eller [!DNL Adobe Experience Manager] standardanvändargränssnitt för att få åtkomst till Media Library utan [!DNL Assets] licens.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [DAM-funktioner i [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5 Managed Services produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 Produktbeskrivning på plats](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)
