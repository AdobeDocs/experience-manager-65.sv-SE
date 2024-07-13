---
title: AEM - Commerce-integrering med Commerce integration framework - frågor och svar
description: AEM - Commerce-integrering med Commerce integration framework - frågor och svar
exl-id: d541607f-c4c9-4dd5-aadf-64d4cb5f9f2a
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# AEM - Commerce-integrering med Commerce integration framework - frågor och svar

## 1. Används CIF GraphQL endast för e-handel eller är det tillgängligt för att fråga innehåll som har skapats AEM JCR?

Adobe har antagit Adobe Commerce GraphQL API:er som sin officiella e-handels-API för alla e-handelsrelaterade data. AEM använder därför GraphQL för att utbyta affärsdata med Adobe Commerce och med valfri e-handelsmotor via I/O Runtime. Det här GraphQL-API:t är oberoende av hur GraphQL-API AEM åtkomst till innehållsfragment.

## 2. Kan produktresurser (bilder) lagras och refereras från AEM via Adobe Commerce Admin? Hur kan resurser från Dynamic Media förbrukas?

Det finns ingen officiell integrering med AEM Assets - Adobe Commerce. Det finns en partnerkoppling tillgänglig på [Marketplace](https://marketplace.magento.com/partner/bounteous_ecomm).

Du kan också som tillfällig lösning lagra produktresurser (bilder) i AEM Assets, men du måste lagra resursens URL-adresser manuellt i Adobe Commerce. Dynamic Media är en del av AEM Assets och fungerar på samma sätt.

## 3. Spelar det någon roll var e-handelslösningen används? (Lokalt eller i molnet)

Nej, det spelar ingen roll var er handelslösning är installerad. CIF och det AEM butiksarbetet oavsett distributionsmodell. Om lösningen distribueras med den rekommenderade E2E-referensarkitekturen kan E2E-tester köras mot nyckeltal för prestanda som representerar en typisk företagsprofil. Denna process ger ytterligare information som kan användas som riktmärke.

## 4. Hur skapas katalogsidor eller produktsidor i AEM? Hur kvarstår de i AEM?

Katalogsidor och produktsidor skapas och cachelagras dynamiskt i AEM baserat på generiska katalog- och produktsidmallar. Inga produkt- eller katalogdata importeras och lagras i AEM.

## 5. När ni uppdaterar produktdata i er e-handelslösning, är detta en reell satsning på AEM? Eller är det en gruppbearbetning?

Det CIF tillägg som används med AEM gör att data kan flöda från e-handelslösningen till AEM on-demand. Det här arbetsflödet är alltså inte en push-process i realtid eller en batchprocess när det finns en uppdatering i e-handelslösningen.

## 6. Vilken katalogstorlek AEM med CIF stöd?

Stöd för katalogstorlek beror på några ytterligare aspekter som du måste tänka på. Hur stor är cachekvoten för katalogdata och sidor? Hur många samtidiga förfrågningar förväntar du dig under högtider? Hur skalbar är API:erna för era e-handelslösningar?

## 7. Hur fungerar PIM i detta ramverk?

PIM-data exponeras för AEM och kunder via GraphQL-förfrågningar. Adobe rekommendation är att integrera PIM med e-handelsmotorn (Adobe Commerce eller andra) så att PIM-data sedan kan hämtas från e-handelsmotorn.

## 8. Cachelagra även priser och andra data via Dispatcher. Blir det ofta en cachedomål?

Dynamiska data som pris eller lager cachelagras inte på Dispatcher. Dynamiska data hämtas på klientsidan med webbkomponenter direkt via GraphQL API:er. Endast statiska data (som produkt- eller kategoridata) cachelagras på Dispatcher. Om produktdata ändras behövs cacheogiltigförklaring.

## 9. Hur fungerar cacheminnet för AEM Dispatcher med AEM och e-handel?

Adobe rekommenderar att du ställer in TTL-baserad cacheogiltigförklaring för sidor som cachelagrats på Dispatcher. För dynamisk information som pris eller aktie rekommenderar Adobe att du återger datumet på klientsidan. Mer information om ogiltigförklaring av TTL-baserad cache finns i [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html)

## 10. Finns det någon rekommendation om enhetlig sökning AEM innehåll med Commerce?

En referensimplementering av produktsökningar tillhandahålls, men ingen enhetlig sökning med innehåll. Den här funktionen är kundspecifik och bättre på projektspecifik nivå.

## 11. Hur fungerar Sök med AEM och e-handel med CIF?

CIF innehåller sökfältet och komponenterna för sökresultat. Sökfältskomponenten skickar en GraphQL-begäran med söktermen till e-handelslösningen som sedan returnerar en produktlista som innehåller produktnamn, pris, SLUG och så vidare. Sökresultatkomponenten visar sedan sökresultaten i en gallerivy på en sökresultatsida som skapats i AEM. Sökfunktionen har stöd för grundläggande textsökning. Använd SLUG/url-tangenten för att skapa en referens till PDP.

## 12. Hur kan produktdata användas i MSM eller översättningar?

Produktdata är redan översatta i PIM eller Adobe Commerce. AEM - Adobe Commerce Integration har stöd för anslutning till flera Adobe Commerce butiker och butiksvyer. I en MSM-konfiguration är vanligtvis en AEM plats länkad till en Adobe Commerce-butiksvy.

## 13. Finns det något sätt att förbättra produktinformationen med kommersiell text? I så fall, var görs detta? I AEM eller i e-handelslösningen?

Adobe rekommenderar att man hanterar marknadsföringsrelaterade data och innehåll i AEM. Dekorera produktdata från er e-handelslösning med ytterligare attribut med hjälp av innehållsfragment eller skapa och länka Experience Fragments för ostrukturerat innehåll till era produkter.

## 14. Hur ser ett företag till att PCI-kompatibiliteten följs när det använder AEM för hela presentationslagret?

Adobe rekommenderar att abstrakta betalningsmetoder används. Om du gör det kommer webbläsarklienten att kommunicera direkt med betalgatewayleverantören så att Adobe inte håller eller godkänner kortinnehavarens datum eller handelslösningarna. Den här metoden kräver endast en nivå 3 PCI-kompatibilitet. Det finns dock ytterligare saker att tänka på som helt PCI-kompatibla, till exempel hur medarbetarna interagerar med systemet och data. Mer information om Adobe Commerce PCI-kompatibilitet finns i [PCI-kompatibilitet](https://business.adobe.com/products/magento/pci-compliance.html)

## 15. Om jag använder molnversionerna AEM och Adobe Commerce, är denna gemensamma lösning PCI-kompatibel?

Ja, självutvärderingsformulär D och försäkran om överensstämmelse finns tillgängliga på begäran.

## 16. Hur begär jag en I/O Runtime-licens?

Du kan begära en utvärderingslicens för att använda I/O-miljön [här](https://adobeio.typeform.com/to/obqgRm).
