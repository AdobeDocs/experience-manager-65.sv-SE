---
title: Mappdelning enligt  [!DNL Adobe Creative Cloud] god praxis
description: Konfigurera [!DNL Adobe Experience Manager] så att användare i [!DNL Experience Manager Assets] kan utbyta mappar med Adobe Creative Cloud-användare.
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] till [!DNL Adobe Creative Cloud] mappdelning {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>Mappdelningsfunktionen [!DNL Experience Manager] till [!DNL Creative Cloud] är föråldrad. Adobe rekommenderar att du använder nyare funktioner som [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) eller [Experience Manager-datorprogrammet](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Läs mer i [Bästa praxis för integrering mellan Experience Manager och Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] kan konfigureras så att användare i [!DNL Assets] kan dela mappar med användare i [!DNL Adobe Creative Cloud]-program, så att de är tillgängliga som delade mappar i [!DNL Adobe Creative Cloud]-resurstjänsten. Funktionen kan användas för utbyte av filer mellan kreativa team och [!DNL Assets] användare, särskilt när de kreativa användarna inte har tillgång till distributionen av [!DNL Assets] (de finns inte i företagsnätverket).

Den här typen av integrering kan användas i följande fall, särskilt när du arbetar med användare som inte har direkt åtkomst till [!DNL Assets]:

* [!DNL Assets]-användare delar en uppsättning specifika digitala resurser med användare av [!DNL Adobe Creative Cloud]-filer (till exempel en kreativ översikt och en uppsättning godkända resurser för designarbete för en ny marknadsföringsaktivitet).
* [!DNL Assets] användare tar emot nya filer som skapats av [!DNL Adobe Creative Cloud] appanvändare.

>[!NOTE]
>
>Innan du läser det här dokumentet kan du läsa den övergripande [integreringen mellan Experience Manager och Creative Cloud ](/help/assets/aem-cc-integration-best-practices.md) för att få en översikt över integreringen.

## Ökning {#overview}

Mappdelning mellan [!DNL Experience Manager] och [!DNL Creative Cloud] är beroende av att mappar och filer delas på serversidan mellan [!DNL Assets]- och [!DNL Creative Cloud]-konton. Kreatörer, som använder datorprogrammet [!DNL Creative Cloud] på sina datorer, kan också göra de delade mapparna tillgängliga direkt på sina diskar med hjälp av tekniken [!DNL Adobe CreativeSync].

I följande diagram visas en översikt över integreringen.

![chlimage_1-179](assets/chlimage_1-406.png)

Integreringen innehåller följande element:

* **[!DNL Experience Manager Assets]** har distribuerats i företagsnätverket (Managed Services eller lokalt): Mappdelning initieras här.
* **[!DNL Adobe Experience Cloud Assets]bastjänst**: Fungerar som mellanhand mellan [!DNL Experience Manager] och [!DNL Creative Cloud] lagringstjänster. En administratör för en organisation som använder integreringen måste upprätta en förtroenderelation mellan Experience Cloud-organisationen och distributionen [!DNL Assets]. De [definierar även en lista över godkända medarbetare i Creative Cloud](https://experienceleague.adobe.com/docs/core-services/interface/services/assets/t-admin-add-cc-user.html) som användare av [!DNL Assets] kan dela mappar för att öka säkerheten.

* **[!DNL Creative Cloud]Assets webbtjänster** (webgränssnittet för lagring och [!DNL Creative Cloud] filer): Det är här specifika Creative Cloud-appanvändare, som en [!DNL Assets]-mapp delades med, kan acceptera inbjudan och se mappen i Creative Cloud-kontoarkivet.
* **Creative Cloud-datorprogrammet**: (Valfritt) Tillåter direktåtkomst till delade mappar/filer från den kreativa användarens skrivbord via synkronisering med [!DNL Creative Cloud] Assets-lagring.

## Egenskaper och begränsningar {#characteristics-and-limitations}

* **Envägsspridning av ändringar:** Filändringar sprids endast i en riktning - från systemet ([!DNL Experience Manager] eller [!DNL Creative Cloud Assets]), där resursen ursprungligen skapades (överfördes). Integreringen ger ingen helautomatiserad tvåvägssynkronisering mellan de två systemen.
* **Versionshantering:**

   * [!DNL Experience Manager] skapar bara versioner av en resurs vid uppdateringar om filen har sitt ursprung i [!DNL Experience Manager] och uppdateras där.
   * [!DNL Creative Cloud] Assets har en egen [versionsfunktion](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) som är avsedd för uppdateringar av Work in Progress (i princip lagrar uppdateringar i upp till tio dagar)

* **Utrymmesbegränsningar:** Storlekar och volymer av filer som utväxlas begränsas av den specifika [Creative Cloud Assets-kvoten](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) för kreativa användare (beror på prenumerationsnivå) och en begränsning på 5 GB. Utrymmet begränsas också av den tillgångskvot som organisationen har i Adobe Experience Cloud Assets bastjänst.

* **Utrymmeskrav:** Filerna i delade mappar måste också lagras fysiskt i [!DNL Experience Manager] och sedan i [!DNL Creative Cloud]-kontot, med en cachelagrad kopia i bastjänsten [!DNL Experience Cloud Assets].
* **Nätverk och bandbredd:** Filerna i delade mappar och alla uppdateringar måste transporteras över nätverket mellan systemen. Se till att endast relevanta filer och uppdateringar delas.
* **Mapptyp**: Delning av en [!DNL Assets]-mapp av typen `sling:OrderedFolder` stöds inte vid delning i [!DNL Adobe Experience Cloud]. Om du vill dela en mapp ska du inte markera alternativet [!UICONTROL Ordered] när du skapar den i [!DNL Assets].

## God praxis {#best-practices}

De bästa sätten att använda mappdelning mellan [!DNL Experience Manager] och [!DNL Creative Cloud] är bland annat:

* **Volymeffekter:** [!DNL Experience Manager] och [!DNL Creative Cloud] Mappdelning bör användas för att dela ett mindre antal filer, t.ex. relevanta för en viss kampanj eller aktivitet. Om du vill dela större uppsättningar resurser, som alla godkända resurser i organisationen, använder du andra distributionsmetoder (till exempel [!DNL Assets Brand Portal]) eller skrivbordsappen [!DNL Experience Manager].
* **Undvik delning av djupa hierarkier:** Delningen fungerar rekursivt och tillåter inte selektiv delning. Normalt bör endast mappar utan undermappar, eller med en ytlig hierarki, som en undermappsnivå, användas för delning.
* **Separata mappar för envägsdelning:** Separata mappar ska användas för att dela det slutliga materialet från [!DNL Assets] till [!DNL Creative Cloud] filer och för att dela det kreativa materialet tillbaka från [!DNL Creative Cloud]-filer till [!DNL Assets]. Tillsammans med en bra namnkonvention för de här mapparna skapas en lättbegriplig arbetsmiljö för [!DNL Assets] - och [!DNL Creative Cloud] -användare.
* **Undvik pågående arbete i den delade mappen:** Använd inte en delad mapp för pågående arbete - använd en separat mapp i Creative Cloud-filer för att utföra arbete som kräver många ändringar i filen.
* **Starta nytt arbete utanför den delade mappen:** Nya designer (kreativa filer) ska startas i den separata Pågående arbete-mappen i Creative Cloud-filer, och när de är klara att delas med [!DNL Assets] -användare bör de flyttas eller sparas i den delade mappen.
* **Förenkla delningsstrukturen:** Om du vill ha en mer hanterbar driftkonfiguration kan du överväga att förenkla delningsstrukturen. I stället för att dela med alla kreativa användare bör [!DNL Assets]-mappar endast delas med teamrepresentanter, som en creative director eller teammanager. Chefen på den kreativa sidan skulle få det slutliga materialet, besluta om arbetstilldelning och sedan låta designers arbeta i sina egna Creative Cloud-konton på PIA-resurser. De kan använda samarbetsfunktionerna i Creative Cloud för att koordinera arbetet och slutligen markera och placera resurser som är klara att delas tillbaka till [!DNL Assets] i sin kreativa, färdiga delade mapp.

I följande diagram visas ett exempel på hur du skapar designer baserat på befintliga slutliga resurser från [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
