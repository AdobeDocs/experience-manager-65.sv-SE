---
title: Migrera från Dynamic Media - hybrid-läge till Dynamic Media - S7-läge
description: Lär dig hur du migrerar en instans av Dynamic Media - hybrid-läge till Dynamic Media - S7-läge
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 7aba1f3b492a07fe502f95535a94c8054a044eb5

---


# Om att gå från Dynamic Media-Hybrid till Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid är en äldre version av Dynamic Media-integrering med Adobe Experience Manager. Hybridversionen introducerades först i AEM (Adobe Experience Manager) 6.1. Även om Adobe fortfarande stöder hybridläge är det inte det rekommenderade läget (Dynamic Media-Scene7 är det rekommenderade läget). Det stöder inte heller nya funktioner som Smart beskärning och panoramabilder. Dynamic Media-Scene7 gör det.

Ytterligare viktiga skillnader mellan Dynamic Media-Hybrid och Dynamic Media-Scene7 är följande:

* URL-adressernas struktur.
* Inmatning av videor.
* Skapa och lagra bildåtergivningar.
* Molnkonfiguration och autentiseringsuppgifter (etablering).

Det finns två alternativ när du går från Dynamic Media-Hybrid till Dynamic Media-Scene7. Det första alternativet är att tillhandahålla en ny instans av Dynamic Media-Scene7 på AEM. Det andra alternativet är att migrera din befintliga instans av Dynamic Media-Hybrid till Dynamic Media-Scene7. Det här alternativet visar tabellformuläret nedanför de steg och överväganden som du kan göra under flyttningen.

>[!IMPORTANT]
>
>Adobe rekommenderar att du inte migrerar en Dynamic Media-Hybrid-implementering till Dynamic Media-Scene7 för direktproduktion.

## Alternativ 1 - Etablera en ny instans av Dynamic Media-Scene7 på AEM {#provision-new-dms7}

Överväg att börja om från början med en ny, etablerad instans av Dynamic Media-Scene7 på Adobe Experience Manager. Förutom att mata in och bearbeta resurser via Dynamic Media Cloud Service rekommenderar vi att Adobe granskar resursanvändning, arbetsflöden och komponenter. I många fall kan anpassade komponenter och arbetsflöden ersättas med nya, körklara funktioner.

## Alternativ 2 - Migrera din befintliga instans av Dynamic Media-Hybrid till Dynamic Media-Scene7 {#process-for-migrating}

| Steg | Uppgift | Överväganden |
|---|---|---|
| 1 | Clone Dynamic Media-Hybrid Author instance. | Du bör behålla din befintliga instans av Dynamic Media-Hybrid Author i reserv tills de återstående stegen i migreringsprocessen har slutförts. |
| 2 | Starta klonad författarinstans i läget Dynamic Media-Scene7. |  |
| 3 | Konfigurera Dynamic Media med autentiseringsuppgifter för Dynamic Media-Scene7 i Adobe Experience Manager Cloud Services. | Adobe måste godkänna Dynamic Media-Scene7-etableringen. Du kommer att ha samtidiga miljöer för Dynamic MediaM-Hybrid och Dynamic Media-Scene7 som kommer att stödjas under en begränsad tid. |
| 4 | Skapa migreringspaket för att importera resurser efter behov.<br>Ta bort de lokala PTIFF-filer som skapades vid första intaget till Dynamic Media-Hybrid. | Om alla resurser finns tillgängliga i din Dynamic Media-Hybrid-instans finns det redan en klon som innehåller alla resurser. Därför behövs inget paket. |
| 5 | Kör arbetsflödet för resursuppdatering för att synkronisera resurser till tjänsten Dynamic Media Cloud. | Adobe rekommenderar att uppdateringsarbetsflödet utförs i grupper för att tillåta komprimering. |
| 6 | Migrera inställningar för visningsprogram, bilder och video. |  |
| 7 | Gå igenom varje resurs som refereras till av Web Content Management och uppdatera deras associerade URL:er. |  |
| 8 | Migrera anpassade arbetsflöden för att stödja det nya läget Dynamic Media-Scene7 (manuella uppdateringar). |  |
| 9 | Verifiera överföring och konfiguration av Web Content Management. |  |
| 10 | Efter verifieringen får du ett godkännande för att inaktivera Dynamic Media-Hybrid Author (behåll som en reservversion). |  |
| 11 | Ta bort Dynamic Media-Hybrid Author-instansen efter ungefär en månads lyckad användning av Dynamic Media-Scene7. |  |
