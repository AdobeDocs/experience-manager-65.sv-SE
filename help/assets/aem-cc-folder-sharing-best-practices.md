---
title: Mappdelning till [!DNL Adobe Creative Cloud] bästa praxis
description: Konfigurera [!DNL Adobe Experience Manager] för att tillåta användare att [!DNL Experience Manager Assets] för att utbyta mappar med Adobe Creative Cloud-användare.
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] till [!DNL Adobe Creative Cloud] mappdelning {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>The [!DNL Experience Manager] till [!DNL Creative Cloud] Mappdelningsfunktionen är föråldrad. Adobe rekommenderar att du använder nyare funktioner som [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) eller [Experience Manager datorprogram](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Läs mer i [Bästa praxis för integrering mellan Experience Manager och Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] kan konfigureras för att tillåta användare i [!DNL Assets] för att dela mappar med användare av [!DNL Adobe Creative Cloud] appar, så de är tillgängliga som delade mappar i [!DNL Adobe Creative Cloud] tillgångstjänst. Funktionen kan användas för utbyte av filer mellan olika team och [!DNL Assets] -användare, särskilt när de kreativa användarna inte har tillgång till [!DNL Assets] distribution (de finns inte i företagsnätverket).

Den här typen av integrering kan användas i följande fall, särskilt när du arbetar med användare som inte har direkt åtkomst till [!DNL Assets]:

* [!DNL Assets] -användare delar en uppsättning specifika digitala resurser med användare av [!DNL Adobe Creative Cloud] filer (t.ex. en kreativ översikt och en uppsättning godkända resurser för designarbete för en ny marknadsföringsaktivitet).
* [!DNL Assets] användare tar emot nya filer skapade av [!DNL Adobe Creative Cloud] appanvändare.

>[!NOTE]
>
>Innan du läser det här dokumentet kan du granska det övergripande [Bästa praxis för integrering mellan Experience Manager och Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) för en översikt över integreringen.

## Översikt {#overview}

[!DNL Experience Manager] till [!DNL Creative Cloud] mappdelning är beroende av att mappar och filer på serversidan delas mellan [!DNL Assets] och [!DNL Creative Cloud] konton. Kreatörer som använder [!DNL Creative Cloud] skrivbordsappen på sina datorer kan även göra de delade mapparna tillgängliga direkt på sina diskar med [!DNL Adobe CreativeSync] teknik.

I följande diagram visas en översikt över integreringen.

![chlimage_1-179](assets/chlimage_1-406.png)

Integreringen innehåller följande element:

* **[!DNL Experience Manager Assets]** distribueras i företagsnätverket (Managed Services eller lokalt): Mappdelning initieras här.
* **[!DNL Adobe Experience Cloud Assets]bastjänst**: Fungerar som mellanhand mellan [!DNL Experience Manager] och [!DNL Creative Cloud] lagringstjänster. En administratör för en organisation som använder integreringen måste upprätta en förtroenderelation mellan Experience Cloud och [!DNL Assets] distribution. De [Definiera en lista över godkända medarbetare i Creative Cloud](https://experienceleague.adobe.com/docs/core-services/interface/services/assets/t-admin-add-cc-user.html), som [!DNL Assets] -användare kan dela mappar för att öka säkerheten.

* **[!DNL Creative Cloud]Assets web services** (lagring och [!DNL Creative Cloud] filer (webbgränssnitt): Här är specifika Creative Cloud-appanvändare, som [!DNL Assets] mappen delades, skulle kunna acceptera inbjudan och visa mappen i Creative Cloud-kontoarkivet.
* **Creative Cloud datorprogram**: (Valfritt) Tillåter direktåtkomst till delade mappar/filer från den kreativa användarens skrivbord via synkronisering med [!DNL Creative Cloud] Resurslagring.

## Egenskaper och begränsningar {#characteristics-and-limitations}

* **Envägsspridning av ändringar:** Filändringarna sprids endast i en riktning - från systemet ([!DNL Experience Manager] eller [!DNL Creative Cloud Assets]), där resursen ursprungligen skapades (överfördes). Integreringen ger ingen helautomatiserad tvåvägssynkronisering mellan de två systemen.
* **Versionshantering:**

   * [!DNL Experience Manager] skapar bara versioner av en resurs vid uppdateringar om filen har sitt ursprung i [!DNL Experience Manager] och uppdateras där.
   * [!DNL Creative Cloud] Resurserna har sina egna [versionsfunktion](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) som är avsett för uppdateringar av Work in Progress (lagrar uppdateringar i princip i upp till tio dagar)

* **Utrymmesbegränsningar:** Storleken på och mängden filer som utbyts begränsas av de specifika [Creative Cloud Assets-kvot](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) för kreativa användare (beroende på prenumerationsnivå) och en begränsning på 5 GB maximal filstorlek. Utrymmet begränsas också av organisationens tillgångskvot i Adobe Experience Cloud Assets bastjänst.

* **Utrymmeskrav:** Filerna i delade mappar måste också lagras fysiskt i [!DNL Experience Manager] och sedan [!DNL Creative Cloud] konto, med en cachelagrad kopia i [!DNL Experience Cloud Assets] bastjänst.
* **Nätverk och bandbredd:** Filerna i delade mappar och alla uppdateringar måste transporteras över nätverket mellan systemen. Se till att endast relevanta filer och uppdateringar delas.
* **Mapptyp**: Dela en [!DNL Assets] typmapp `sling:OrderedFolder`, stöds inte i samband med delning i [!DNL Adobe Experience Cloud]. Om du vill dela en mapp när du skapar den i [!DNL Assets]markerar du inte [!UICONTROL Ordered] alternativ.

## God praxis {#best-practices}

Bästa tillvägagångssätt för att använda [!DNL Experience Manager] till [!DNL Creative Cloud] mappdelning inkluderar:

* **Volymeffekter:** [!DNL Experience Manager] och [!DNL Creative Cloud] Mappdelning bör användas för att dela ett mindre antal filer, t.ex. relevanta för en viss kampanj eller aktivitet. Om du vill dela större uppsättningar resurser, som alla godkända resurser i organisationen, använder du andra distributionsmetoder (till exempel [!DNL Assets Brand Portal]) eller [!DNL Experience Manager] datorprogram.
* **Undvik delning av djupa hierarkier:** Delningen fungerar rekursivt och tillåter inte selektiv delning. Normalt bör endast mappar utan undermappar, eller med en ytlig hierarki, som en undermappsnivå, användas för delning.
* **Separata mappar för envägsdelning:** Separata mappar bör användas för att dela det slutliga materialet från [!DNL Assets] till [!DNL Creative Cloud] filer och för att dela kreativa resurser tillbaka från [!DNL Creative Cloud] filer till [!DNL Assets]. Tillsammans med en bra namnkonvention för de här mapparna skapar den en lättbegriplig arbetsmiljö för [!DNL Assets] och [!DNL Creative Cloud] användare.
* **Undvik PIA i den delade mappen:** Använd inte en delad mapp för pågående arbete - använd en separat mapp i Creative Cloud-filer för att utföra arbete som kräver att filen ändras ofta.
* **Starta nytt arbete utanför den delade mappen:** Nya designer (kreativa filer) ska startas i den separata Pågående arbete-mappen i Creative Cloud-filer och när de ska delas med [!DNL Assets] -användare bör de flyttas eller sparas i den delade mappen.
* **Förenkla delningsstrukturen:** Om du vill ha en mer hanterbar driftsättning kan du förenkla delningsstrukturen. Istället för att dela med andra användare [!DNL Assets] bör endast delas med teamrepresentanter, som creative director eller teammanager. Chefen på den kreativa sidan skulle få det slutliga materialet, besluta om arbetstilldelning och sedan låta designers arbeta i sina egna Creative Cloud-konton på PIA-resurser. De kan använda samarbetsfunktionerna i Creative Cloud för att samordna arbetet och slutligen välja och lägga resurser som är redo att delas tillbaka till [!DNL Assets] till deras kreativa färdiga delade mapp.

I följande diagram visas ett exempel på hur du skapar design baserat på befintliga slutliga resurser från [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
