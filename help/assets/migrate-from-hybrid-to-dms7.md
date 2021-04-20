---
title: Migrera från Dynamic Media - hybrid-läge till Dynamic Media - S7-läge
description: Lär dig hur du migrerar din instans av Dynamic Media - hybrid-läge till Dynamic Media - S7-läge
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: Business Practitioner, Administrator
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
feature: Scene7 mode,Hybrid mode
translation-type: tm+mt
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# Om att gå från Dynamic Media-Hybrid till Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid är en äldre version av Dynamic Media som är integrerad med Adobe Experience Manager. Hybridversionen introducerades först i AEM (Adobe Experience Manager) 6.1. Även om Adobe har stöd för hybridläge är det inte det rekommenderade läget (Dynamic Media-Scene7 är det rekommenderade läget). Det stöder inte heller nya funktioner som Smart beskärning och panoramabilder. Det gör Dynamic Media-Scene7.

Ytterligare viktiga skillnader mellan Dynamic Media-Hybrid och Dynamic Media-Scene7 är följande:

* URL-adressernas struktur.
* Inmatning av videor.
* Skapa och lagra bildåtergivningar.
* Molnkonfiguration och autentiseringsuppgifter (etablering).

Det finns två alternativ när du går från Dynamic Media-Hybrid till Dynamic Media-Scene7. Det första alternativet är att bara tillhandahålla en ny instans av Dynamic Media-Scene7 på AEM. Det andra alternativet är att migrera din befintliga instans av Dynamic Media-Hybrid till Dynamic Media-Scene7. Det här alternativet visar tabellformuläret nedanför de steg och överväganden som du kan göra under flyttningen.

>[!IMPORTANT]
>
>Adobe rekommenderar att du inte migrerar en Dynamic Media-Hybrid-implementering till Dynamic Media-Scene7 i direktproduktionsinstanser.

## Alternativ 1 - Etablera en ny instans av Dynamic Media-Scene7 på AEM {#provision-new-dms7}

Överväg att börja om från början med en ny, etablerad instans av Dynamic Media-Scene7 på Adobe Experience Manager. Förutom att lägga in och bearbeta mediefiler via Dynamic Media Cloud Service rekommenderar vi att Adobe granskar resursanvändningen, arbetsflödena och komponenterna. I många fall kan anpassade komponenter och arbetsflöden ersättas med nya, körklara funktioner.

## Alternativ 2 - Migrera din befintliga instans av Dynamic Media-Hybrid till Dynamic Media-Scene7 {#process-for-migrating}

| Steg | Uppgift | Överväganden |
|---|---|---|
| 1 | Clone Dynamic Media-Hybrid Author instance. | Du bör behålla din befintliga instans av Dynamic Media-Hybrid Author för reservsyften tills de återstående stegen i migreringsprocessen har slutförts. |
| 2 | Starta klonad författarinstans i Dynamic Media-Scene7-läge. |  |
| 3 | Konfigurera Dynamic Media med inloggningsuppgifter för Dynamic Media-Scene7 i Adobe Experience Manager-Cloud Services. | Adobe måste godkänna etableringen av Dynamic Media-Scene7. Du kommer att ha samtidiga miljöer för Dynamic MediaM-Hybrid och Dynamic Media-Scene7 som kommer att stödjas under en begränsad tid. |
| 4 | Skapa migreringspaket för att importera resurser efter behov.<br>Ta bort de lokala PTIFF-filer som skapades vid första intaget till Dynamic Media-Hybrid. | Om alla resurser finns tillgängliga i din Dynamic Media-Hybrid-instans finns det redan en klon av dem. Därför behövs inget paket. |
| 5 | Kör resursuppdateringsarbetsflöde för att synkronisera resurser till Dynamic Media Cloud Service. | Adobe rekommenderar att uppdateringsarbetsflödet görs i grupper för att tillåta komprimering. |
| 6 | Migrera inställningar för visningsprogram, bilder och video. |  |
| 7 | Gå igenom varje resurs som refereras till av Web Content Management och uppdatera deras associerade URL:er. |  |
| 8 | Migrera anpassade arbetsflöden för att stödja det nya läget Dynamic Media-Scene7 (manuella uppdateringar). |  |
| 9 | Verifiera överföring och konfiguration av Web Content Management. |  |
| 10 | Efter verifieringen får du ett godkännande för att inaktivera Dynamic Media-Hybrid Author (behåll som en fallback). |  |
| 11 | Ta bort instansen av Dynamic Media-Hybrid Author efter cirka en månads lyckad användning av Dynamic Media-Scene7. |  |
