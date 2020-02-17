---
title: AEM till Creative Cloud-mappar för att dela bästa praxis
description: Konfigurera Adobe Experience Manager (AEM) så att användare i AEM Resurser kan utbyta mappar med Adobe Creative Cloud-användare (CC).
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# AEM till Creative Cloud-mappar för att dela bästa praxis {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>Funktionen för mappdelning från AEM till Creative Cloud är föråldrad. Adobe rekommenderar starkt att du använder nyare funktioner som [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) eller [AEM-datorprogrammet](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html). Lär dig mer om [AEM och Creative Cloud-integration](/help/assets/aem-cc-integration-best-practices.md).

Adobe Experience Manager (AEM) kan konfigureras så att användare i AEM Resurser kan dela mappar med användare i Adobe Creative Cloud-program, så att de är tillgängliga som delade mappar i Adobe Creative Cloud Resurser-tjänsten. Funktionen kan användas för utbyte av filer mellan kreativa team och AEM Assets-användare, särskilt när de kreativa användarna inte har tillgång till AEM Assets-instansen (de finns inte i företagsnätverket).

Den här typen av integrering kan användas i följande fall, särskilt när du arbetar med användare som inte har direkt åtkomst till AEM Resurser:

* AEM Assets-användare delar en uppsättning specifika resurser med användare av Adobe Creative Cloud Files (t.ex. en översikt och en uppsättning godkända resurser för designarbete för en ny marknadsföringsaktivitet)
* AEM Resurser-användare får tillgång till nya filer som skapats av användare av Adobe Creative Cloud-program.

>[!NOTE]
>
>Innan du läser det här dokumentet kan du läsa de övergripande [arbetssätten för integrering med](/help/assets/aem-cc-integration-best-practices.md) AEM och Creative Cloud för att få en översikt över ämnet på en högre nivå.

## Översikt {#overview}

AEM till Creative Cloud-mappdelning är beroende av att mappar och filer delas på serversidan mellan AEM Assets och Creative Cloud-konton. Kreatörer som använder Creative Cloud-datorprogrammet på sina datorer kan dessutom göra delade mappar tillgängliga direkt på sina skivor med hjälp av Adobe CreativeSync-tekniken.

I följande diagram visas en översikt över integreringen.

![chlimage_1-179](assets/chlimage_1-406.png)

Integreringen innehåller följande element:

* **AEM Assets-server** som distribueras i företagsnätverket (hanterade tjänster eller lokalt): Mappdelning initieras här.
* **Adobe Marketing Cloud Assets bastjänst**: Fungerar som mellanhand mellan AEM och Creative Cloud-lagringstjänster. Administratören för det företag som använder integreringen behöver upprätta en förtroenderelation mellan Marketing Cloud-organisationen och AEM Assets-instansen. De [definierar också en lista över godkända Creative Cloud-medarbetare](https://marketing.adobe.com/resources/help/en_US/mcloud/t_admin_add_cc_user.html), som AEM Assets-användare kan dela mappar för att öka säkerheten.

* **Webbtjänster** för Creative Cloud Assets (lagring och webbgränssnittet för Creative Cloud Files): Här kan specifika Creative Cloud-appanvändare, som har en AEM Resurser-mapp delad, acceptera inbjudan och se mappen i sitt Creative Cloud-konto.
* **Creative Cloud-datorprogrammet**: (Valfritt) Ger direkt åtkomst till delade mappar/filer från den kreativa användarens skrivbord via synkronisering med Creative Cloud Assets-lagring.

## Egenskaper och begränsningar {#characteristics-and-limitations}

* **** Envägsspridning av ändringar: Filändringarna sprids endast i en riktning - från systemet (AEM eller Creative Cloud Assets), där resursen ursprungligen skapades (överfördes). Integreringen ger ingen helautomatiserad tvåvägssynkronisering mellan de två systemen.
* **Versionshantering:**

   * AEM skapar bara versioner av en resurs vid uppdateringar om filen har sitt ursprung i AEM och uppdateras där.
   * Creative Cloud Assets har en egen [versionsfunktion](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) som är avsedd för uppdateringar av Work in Progress (d.v.s. lagrar uppdateringar i upp till 10 dagar)

* **** Utrymmesbegränsningar: Storleken på och mängden filer som utbyts begränsas av den specifika [Creative Cloud Assets-kvoten](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) för kreativa användare (beroende på prenumerationsnivå) och en begränsning på 5 GB maximal filstorlek. Utrymmet begränsas dessutom av den tillgångskvot som organisationen har i bastjänsten Adobe Marketing Cloud Assets.

* **** Utrymmeskrav: Filerna i delade mappar måste också lagras fysiskt i AEM och sedan i Creative Cloud-kontot, med en cachelagrad kopia i bastjänsten för Marketing Cloud Assets.
* **** Nätverk och bandbredd: Filerna i delade mappar och alla uppdateringar måste transporteras över nätverket mellan systemen. Du bör se till att endast relevanta filer och uppdateringar delas.
* **Mapptyp**: Delning av en resursmapp av den typen `sling:OrderedFolder`stöds inte i samband med delning i Adobe Marketing Cloud. Om du vill dela en mapp ska du inte markera alternativet Ordnad när du skapar den i AEM Resurser.

## God praxis {#best-practices}

De bästa sätten att utnyttja AEM till Creative Cloud-mappdelning är:

* **** Volymeffekter: Mappdelning i AEM/Creative Cloud bör användas för att dela ett mindre antal filer, till exempel filer som är relevanta för en viss kampanj eller aktivitet. Om du vill dela större uppsättningar resurser, som alla godkända resurser i organisationen, använder du andra distributionsmetoder (till exempel AEM Assets Brand Portal) eller AEM-datorprogrammet.

* **** Undvik delning av djupa hierarkier: Delningen fungerar rekursivt och medger inte selektiv delning. Normalt bör endast mappar utan undermappar, eller med en mycket kort hierarki, som en undermappsnivå, användas för delning.
* **** Separata mappar för envägsdelning: Separata mappar bör användas för att dela det slutliga materialet från AEM Assets till Creative Cloud-filer och för att dela kreativa resurser tillbaka från Creative Cloud-filer till AEM Assets. Tillsammans med en bra namnkonvention för dessa mappar skapar den en lättbegriplig arbetsmiljö för både AEM Assets- och Creative Cloud-användare.
* **** Undvik PIA i den delade mappen: Delad mapp ska inte användas för pågående arbete - använd en separat mapp i Creative Cloud Files för att utföra arbete som kräver ändringar av filen ofta.
* **** Starta nytt arbete utanför den delade mappen: Nya designer (kreativa filer) bör startas i den separata Pågående arbete-mappen i Creative Cloud Files, och när de är klara att delas med AEM Resurser-användare bör de flyttas eller sparas i den delade mappen.
* **** Förenkla delningsstrukturen: För en mer hanterbar driftsättning kan du tänka på att förenkla delningsstrukturen. I stället för att dela med alla kreativa användare bör AEM Assets-mapparna endast delas med teamrepresentanter, som en creative director eller teamchef. Chefen på den kreativa sidan skulle få det slutliga materialet, bestämma om arbetstilldelning och sedan låta designers arbeta i sina egna Creative Cloud-konton på PIA-resurser. De kan använda samarbetsfunktionerna i Creative Cloud för att koordinera arbetet och slutligen välja och placera resurser som är redo att delas tillbaka till AEM Assets i deras kreativa färdiga delade mapp.

I följande diagram visas ett exempel på hur du skapar nya designer baserat på befintliga slutliga resurser från AEM Assets.

![chlimage_1-180](assets/chlimage_1-407.png)
