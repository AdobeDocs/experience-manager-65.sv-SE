---
title: Adobe Experience Manager till Adobe Creative Cloud-mappen där du kan dela med dig av bästa praxis
description: Konfigurera Adobe Experience Manager så att användare i Experience Manager Assets kan utbyta mappar med Adobe Creative Cloud-användare (CC).
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 0%

---


# Adobe Experience Manager till Adobe Creative Cloud-mappdelning {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>Mappdelningsfunktionen Experience Manager till Creative Cloud är föråldrad. Adobe rekommenderar starkt att du använder nyare funktioner som [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) eller [Experience Manager](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html). Läs mer om de bästa sätten att integrera [Experience Manager och Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

Adobe Experience Manager kan konfigureras så att användare i Resurser kan dela mappar med användare i Adobe Creative Cloud-program, så att de är tillgängliga som delade mappar i Adobe Creative Cloud Resurser-tjänsten. Funktionen kan användas för att utbyta filer mellan kreativa team och Assets-användare, särskilt när de kreativa användarna inte har tillgång till Assets-instansen (de finns inte i företagsnätverket).

Den här typen av integrering kan användas i följande fall, särskilt när du arbetar med användare som inte har direkt åtkomst till Assets:

* Resursanvändare delar en uppsättning specifika resurser med användare av Adobe Creative Cloud Files (t.ex. en översikt och en uppsättning godkända resurser för designarbete för en ny marknadsföringsaktivitet)
* Resurser som användare får ta emot nya filer som skapats av användare av Adobe Creative Cloud-program.

>[!NOTE]
>
>Innan du läser det här dokumentet kan du gå igenom de effektivaste strategierna [för integrering mellan](/help/assets/aem-cc-integration-best-practices.md) Experience Manager och Creative Cloud för att få en översikt över ämnet på en högre nivå.

## Översikt {#overview}

Experience Manager till Creative Cloud-mappdelning är beroende av att mappar och filer delas på serversidan mellan Assets- och Creative Cloud-konton. Kreatörer som använder Creative Cloud-datorprogrammet på sina datorer kan dessutom göra delade mappar tillgängliga direkt på sina skivor med hjälp av Adobe CreativeSync-tekniken.

I följande diagram visas en översikt över integreringen.

![chlimage_1-179](assets/chlimage_1-406.png)

Integreringen innehåller följande element:

* **Experience Manager Assets-server** som distribueras i företagsnätverket (hanterade tjänster eller lokalt): Mappdelning initieras här.
* **Adobe Marketing Cloud Assets core service**: fungerar som en mellanhand mellan Experience Manager och Creative Cloud-lagringstjänster. Administratören för det företag som använder integreringen måste upprätta en förtroenderelation mellan Marketing Cloud-organisationen och Assets-instansen. De [definierar också en lista över godkända Creative Cloud-medarbetare](https://docs.adobe.com/content/help/en/core-services/interface/assets/t-admin-add-cc-user.html), som Assets-användare kan dela mappar för att öka säkerheten.

* **Webbtjänster** för Creative Cloud Assets (lagring och webbgränssnittet för Creative Cloud Files): Det är här specifika Creative Cloud-appanvändare, som har en resursmapp delad, kan acceptera inbjudan och se mappen i sitt Creative Cloud-konto.
* **Creative Cloud-datorprogrammet**: (Valfritt) Ger direkt åtkomst till delade mappar/filer från den kreativa användarens skrivbord via synkronisering med Creative Cloud Assets-lagring.

## Egenskaper och begränsningar {#characteristics-and-limitations}

* **Envägsspridning av ändringar:** Filändringarna sprids endast i en riktning - från systemet (Experience Manager eller Creative Cloud Resurser), där resursen ursprungligen skapades (överfördes). Integreringen ger ingen helautomatiserad tvåvägssynkronisering mellan de två systemen.
* **Versionshantering:**

   * Experience Manager skapar bara versioner av en resurs vid uppdateringar om filen har sitt ursprung i Experience Manager och uppdateras där.
   * Creative Cloud Assets har en egen [versionsfunktion](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) som är avsedd för uppdateringar av Work in Progress (d.v.s. lagrar uppdateringar i upp till 10 dagar)

* **Utrymmesbegränsningar:** Storleken på och mängden filer som utbyts begränsas av den specifika [Creative Cloud Assets-kvoten](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) för kreativa användare (beroende på prenumerationsnivå) och en begränsning på 5 GB maximal filstorlek. Utrymmet begränsas dessutom av den tillgångskvot som organisationen har i huvudtjänsten Adobe Marketing Cloud Assets.

* **Utrymmeskrav:** Filerna i delade mappar måste också lagras fysiskt i Experience Manager och sedan i Creative Cloud-kontot, med en cachelagrad kopia i bastjänsten för Marketing Cloud Assets.
* **Nätverk och bandbredd:** Filerna i delade mappar och alla uppdateringar måste transporteras över nätverket mellan systemen. Du bör se till att endast relevanta filer och uppdateringar delas.
* **Mapptyp**: Delning av en resursmapp av den typen `sling:OrderedFolder`stöds inte i samband med delning i Adobe Marketing Cloud. Om du vill dela en mapp ska du inte markera alternativet Ordnad när du skapar den i Resurser.

## Best practices {#best-practices}

De bästa sätten att utnyttja Experience Manager till Creative Cloud-mappdelning är:

* **Volymeffekter:** Mappdelning mellan Experience Manager och Creative Cloud bör användas för att dela ett mindre antal filer, till exempel filer som är relevanta för en viss kampanj eller aktivitet. Om du vill dela större uppsättningar av resurser, som alla godkända resurser i organisationen, använder du andra distributionsmetoder (till exempel Resurser - varumärksportal) eller datorprogrammet Experience Manager.

* **Undvik delning av djupa hierarkier:** Delningen fungerar rekursivt och medger inte selektiv delning. Normalt bör endast mappar utan undermappar, eller med en mycket kort hierarki, som en undermappsnivå, användas för delning.
* **Separata mappar för envägsdelning:** Separata mappar bör användas för att dela det slutliga materialet från Assets till Creative Cloud-filer och för att dela kreativa resurser tillbaka från Creative Cloud-filer till Assets. Tillsammans med en bra namnkonvention för dessa mappar skapar den en lättbegriplig arbetsmiljö för Assets- och Creative Cloud-användare.
* **Undvik PIA i den delade mappen:** Delad mapp ska inte användas för pågående arbete - använd en separat mapp i Creative Cloud Files för att utföra arbete som kräver ändringar av filen ofta.
* **Starta nytt arbete utanför den delade mappen:** Nya designer (kreativa filer) bör startas i den separata Pågående arbete-mappen i Creative Cloud Files, och när de är klara att delas med Assets-användare bör de flyttas eller sparas i den delade mappen.
* **Förenkla delningsstrukturen:** För en mer hanterbar driftsättning kan du tänka på att förenkla delningsstrukturen. I stället för att dela med alla kreativa användare bör Assets-mapparna endast delas med teamrepresentanter, som en creative director eller teammanager. Chefen på den kreativa sidan skulle få det slutliga materialet, bestämma om arbetstilldelning och sedan låta designers arbeta i sina egna Creative Cloud-konton på PIA-resurser. De kan använda samarbetsfunktionerna i Creative Cloud för att samordna arbetet och slutligen välja och lägga resurser som är redo att dela tillbaka till Assets i deras kreativa färdiga delade mapp.

I följande diagram visas ett exempel på hur du skapar nya designer baserat på befintliga slutliga resurser från Assets.

![chlimage_1-180](assets/chlimage_1-407.png)
