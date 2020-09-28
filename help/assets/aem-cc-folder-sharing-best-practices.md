---
title: Mappdelning [!DNL Adobe Creative Cloud] enligt vedertagna rutiner
description: Konfigurera [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] för utbyte av mappar med Adobe Creative Cloud-användare (CC).
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] till [!DNL Adobe Creative Cloud] mappdelning {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>Funktionen [!DNL Experience Manager] till [!DNL Creative Cloud] mappdelning är föråldrad. Adobe rekommenderar starkt att du använder nyare funktioner som [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) eller [Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html). Läs mer om god praxis [för integrering av](/help/assets/aem-cc-integration-best-practices.md)Experience Manager och Creative Cloud.

[!DNL Adobe Experience Manager] kan konfigureras så att användare i kan [!DNL Assets] dela mappar med [!DNL Adobe Creative Cloud] appanvändarna, så att de är tillgängliga som delade mappar i [!DNL Adobe Creative Cloud] resurstjänsten. Funktionen kan användas för utbyte av filer mellan kreativa team och [!DNL Assets] användare, särskilt när de kreativa användarna inte har tillgång till [!DNL Assets] distributionen (de finns inte i företagsnätverket).

Den här typen av integrering kan användas i följande fall, särskilt när du arbetar med användare som inte har direkt åtkomst till [!DNL Assets]:

* [!DNL Assets] -användare delar en uppsättning specifika digitala resurser med användare av [!DNL Adobe Creative Cloud] filer (t.ex. en kreativ översikt och en uppsättning godkända resurser för designarbete för en ny marknadsföringsaktivitet).
* [!DNL Assets] -användare får nya filer skapade av [!DNL Adobe Creative Cloud] appanvändare.

>[!NOTE]
>
>Innan du läser det här dokumentet kan du läsa de övergripande [arbetssätten för integrering mellan](/help/assets/aem-cc-integration-best-practices.md) Experience Manager och Creative Cloud för att få en översikt över integreringen.

## Översikt {#overview}

[!DNL Experience Manager] för att kunna dela mappar måste mappar och filer på serversidan delas mellan [!DNL Creative Cloud] och [!DNL Assets] [!DNL Creative Cloud] konton. Kreatörer som använder datorprogrammet på sina datorer kan dessutom göra de delade mapparna tillgängliga direkt på sina skivor med hjälp av [!DNL Creative Cloud] [!DNL Adobe CreativeSync] teknik.

I följande diagram visas en översikt över integreringen.

![chlimage_1-179](assets/chlimage_1-406.png)

Integreringen innehåller följande element:

* **[!DNL Experience Manager Assets]** distribueras i företagsnätverket (hanterade tjänster eller lokalt): Mappdelning initieras här.
* **[!DNL Adobe Marketing Cloud Assets]bastjänst**: Fungerar som mellanhand mellan [!DNL Experience Manager] - och [!DNL Creative Cloud] lagringstjänster. En administratör för en organisation som använder integreringen måste upprätta ett förtroendeförhållande mellan organisationen Marketing Cloud och [!DNL Assets] distributionen. De [definierar också en lista över godkända medarbetare](https://docs.adobe.com/content/help/en/core-services/interface/assets/t-admin-add-cc-user.html)i Creative Cloud som [!DNL Assets] användare kan dela mappar för att öka säkerheten.

* **[!DNL Creative Cloud]Resurser för webbtjänster** (webgränssnittet för lagring och [!DNL Creative Cloud] filer): Det är här specifika användare av appen Creative Cloud, som har en [!DNL Assets] mapp delad med, kan acceptera inbjudan och se mappen i sitt Creative Cloud-konto.
* **Creative Cloud-datorprogram**: (Valfritt) Möjliggör direkt åtkomst till delade mappar/filer från den kreativa användarens skrivbord via synkronisering med [!DNL Creative Cloud] Assets-lagring.

## Egenskaper och begränsningar {#characteristics-and-limitations}

* **Envägsspridning av ändringar:** Filändringarna sprids endast i en riktning - från systemet ([!DNL Experience Manager] eller [!DNL Creative Cloud Assets]) där resursen ursprungligen skapades (överfördes). Integreringen ger ingen helautomatiserad tvåvägssynkronisering mellan de två systemen.
* **Versionshantering:**

   * [!DNL Experience Manager] skapar bara versioner av en resurs vid uppdateringar om filen har sitt ursprung i [!DNL Experience Manager] och uppdateras där.
   * [!DNL Creative Cloud] Resurserna har en egen [versionshanteringsfunktion](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) som är inriktad på uppdateringar för pågående arbete (lagrar i princip uppdateringar i upp till 10 dagar)

* **Utrymmesbegränsningar:** Storleken på och mängden filer som utväxlas begränsas av den specifika [Creative Cloud Assets-kvoten](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) för kreativa användare (beroende på prenumerationsnivå) och en begränsning på 5 GB. Utrymmet begränsas dessutom av den tillgångskvot som organisationen har i Adobe Marketing Cloud Assets bastjänst.

* **Utrymmeskrav:** Filerna i delade mappar måste också lagras fysiskt i [!DNL Experience Manager] och sedan i [!DNL Creative Cloud] konto, med en cachelagrad kopia i [!DNL Marketing Cloud Assets] huvudtjänsten.
* **Nätverk och bandbredd:** Filerna i delade mappar och alla uppdateringar måste transporteras över nätverket mellan systemen. Du bör se till att endast relevanta filer och uppdateringar delas.
* **Mapptyp**: Delning av en [!DNL Assets] mapp av den typen `sling:OrderedFolder`stöds inte i samband med delning i [!DNL Adobe Marketing Cloud]. Om du vill dela en mapp ska du inte markera [!DNL Assets]alternativet när du skapar den i [!UICONTROL Ordered] .

## Best practices {#best-practices}

De bästa sätten att utnyttja delning från [!DNL Experience Manager] till [!DNL Creative Cloud] mapp är:

* **Volymeffekter:** [!DNL Experience Manager] och [!DNL Creative Cloud] Mappdelning bör användas för att dela ett mindre antal filer, t.ex. relevanta för en viss kampanj eller aktivitet. Om du vill dela större uppsättningar resurser, som alla godkända resurser i organisationen, använder du andra distributionsmetoder (till exempel [!DNL Assets Brand Portal]) eller [!DNL Experience Manager] skrivbordsprogram.
* **Undvik delning av djupa hierarkier:** Delningen fungerar rekursivt och medger inte selektiv delning. Normalt bör endast mappar utan undermappar, eller med en mycket kort hierarki, som en undermappsnivå, användas för delning.
* **Separata mappar för envägsdelning:** Separata mappar bör användas för att dela det slutliga materialet från [!DNL Assets] till [!DNL Creative Cloud] filer och för att dela det kreativa materialet från [!DNL Creative Cloud] filer till [!DNL Assets]. Tillsammans med en bra namnkonvention för de här mapparna skapar den en lättbegriplig arbetsmiljö för [!DNL Assets] både användare och [!DNL Creative Cloud] användare.
* **Undvik PIA i den delade mappen:** Delad mapp ska inte användas för pågående arbete - använd en separat mapp i Creative Cloud-filer för att utföra arbete som kräver att filen ändras ofta.
* **Starta nytt arbete utanför den delade mappen:** Nya designer (kreativa filer) bör startas i den separata Pågående arbete-mappen i Creative Cloud-filer, och när de är klara att delas med [!DNL Assets] användare bör de flyttas eller sparas i den delade mappen.
* **Förenkla delningsstrukturen:** För en mer hanterbar driftsättning kan du tänka på att förenkla delningsstrukturen. I stället för att dela med alla kreativa användare ska [!DNL Assets] mapparna endast delas med teamrepresentanter, som en creative director eller teammanager. Chefen på den kreativa sidan skulle få det slutliga materialet, besluta om arbetstilldelning och sedan låta designers arbeta i sina egna Creative Cloud-konton på PIA-resurser. De kan använda samarbetsfunktionerna i Creative Cloud för att samordna arbetet och slutligen välja och placera resurser som är redo att delas tillbaka till [!DNL Assets] sin kreativa, färdiga delade mapp.

I följande diagram visas ett exempel på hur du skapar nya designer baserat på befintliga slutliga resurser från [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
