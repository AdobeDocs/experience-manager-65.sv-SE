---
title: '[!DNL Experience Manager Assets] integrering med [!DNL Adobe Workfront]'
description: Introduktion till integrering mellan [!DNL Assets] och [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 57e2bffe-8094-4557-99c8-7b482681687e
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager Assets] integrering med [!DNL Adobe Workfront] {#assets-integration-overview}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=en) |
| AEM 6.5 | Den här artikeln |

[!DNL Adobe Workfront] är ett program för arbetshantering som hjälper dig att hantera hela arbetscykeln på ett och samma ställe. Integrationen mellan [!DNL Workfront] och [!DNL Adobe Experience Manager Assets] gör att organisationer kan förbättra innehållets hastighet och time-to-market genom att knyta samman arbete och hantering av digitala resurser. När man arbetar i Workfront får man tillgång till dokument och bilder.

The [!DNL Workfront for Experience Manager enhanced connector] möjliggör förbättrade affärsprocesser med kompletta arbetsflöden och ger personaliserade kundupplevelser från början till slut och central lagring. Adobe har en standardanslutning och en förbättrad anslutning för att integrera de två lösningarna. Se funktionerna nedan för en jämförelse och se [nyheter i [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] gör att din organisation kan:

* Skapa automatiskt länkade Experience Manager-mappar i Workfront och ordna mapparna baserat på Workfront Portfolio, Program och Projekt.
* Synkronisera Workfront-projektmetadata med länkade Experience Manager-mappar.
* Experience Manager metadatauppdateringar med nya versioner.
* Ange objektstatus för Workfront baserat på konfigurerbara villkor med hjälp av arbetsflöden i Experience Manager.
* Publicera material i Experience Manager eller Brand Portal.

Se plattformsstödet och [krav för den förbättrade anslutningen](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe kräver installation och konfiguration av [!DNL Adobe Workfront for Experience Manager enhanced connector] endast via certifierade partners eller [!DNL Adobe Professional Services]. Om den distribueras och konfigureras utan en certifierad partner eller [!DNL Adobe Professional Services], stöds den inte av Adobe.
>
>* Adobe kan släppa uppdateringar av [!DNL Adobe Workfront] och [!DNL Adobe Experience Manager] som gör denna koppling redundant, Om detta inträffar kan kunderna behöva gå över från att använda denna koppling.
>
>* Adobe har stöd för utökade anslutningsversioner 1.7.4 och senare. Tidigare förhandsversioner och anpassade versioner stöds inte. Om du vill kontrollera den utökade anslutningsversionen går du till `digital.hoodoo` grupp tillgänglig i den vänstra rutan i [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en).
>
>* Se [Partnercertifieringsprov för Workfront för Experience Manager Assets förbättrad anslutning](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Mer information om provet finns i [Provguide](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## Jämför olika integreringar mellan [!DNL Assets] och [!DNL Workfront] {#feature-parity-matrix}

Nedan beskrivs de funktioner som är tillgängliga genom olika typer av integreringar mellan [!DNL Assets] och [!DNL Workfront].

| Funktion | Beskrivning | [!DNL Workfront] och [!DNL Assets Essentials] *Ingen anslutning (OTB)* | [!DNL Workfront for Experience Manager enhanced connector] *Kräver anslutning* | Workfront och [!DNL Experience Manager as a Cloud Service] *Ingen anslutning (OTB)* |
|----|----|----|-----|-----|
| Distributionsmetoder | Lämpliga för vilka [!DNL Assets] erbjuder. | Assets Essentials | Adobes hanterade tjänster, lokala | Cloud Service |
| **Allmänt** |
| Skicka digitala filer från [!DNL Workfront] till [!DNL Assets] | Den senaste versionen av ett WF-dokument kan överföras till AEM Assets som länkas som en ny version av dokumentet. | ✓ | ✓ | ✓ |
| Länka AEM mappar manuellt till Workfront-objekt | Befintliga AEM kan länkas som en Workfront-mapp och dess underordnade resurser länkas som nya Workfront-dokument. | ✓ | ✓ | ✓ |
| Länk [!DNL Assets] till Workfront Objects | Befintliga resurser i AEM kan länkas till ett nytt Workfront-dokument eller som en ny version av ett befintligt dokument. | ✓ | ✓ | ✓ |
| Resurser som läggs till i länkade mappar skickas automatiskt till AEM | Om ett dokument läggs till i en länkad mapp överförs den associerade resursen automatiskt till AEM Assets som en ny resurs. | ✓ | ✓ | ✓ |
| Hämta länkade AEM Assets inifrån Workfront | När en resurs är länkad i Workfront kan användaren hämta resursens byte. | ✓ | ✓ | ✓ |
| Sök efter AEM Assets inifrån Workfront | Med AEM Assets-väljaren i Workfront kan du göra fulltextsökningar efter resurser. | ✓ | ✓ | ✓ |
| Sök efter AEM mappar i Workfront | Med AEM Assets-väljaren i Workfront kan du söka i fulltext efter mappar. | ✓ | ✓ | ✓ |
| Visa och navigera AEM mapphierarki inifrån Workfront | Med AEM Assets-väljaren i Workfront kan du bläddra i AEM Assets-hierarkin som begränsas av användarens tillhörande åtkomstkontroller och behörigheter som anges i AEM. | ✓ | ✓ | ✓ |
| Spåra resursversioner AEM tidslinjer | Bevara dokumentversionshistorik mellan Workfront och AEM. | ✓ | ✓ | ✓ |
| Avlänka resurser från AEM Assets i Workfront | En befintlig länkad resurs från AEM kan tas bort från det associerade Workfront-dokumentet. Originalresursen i AEM tas inte bort. | ✓ | ✓ | ✓ |
| Lägg till ny versionshanterad resurs i AEM Assets från Workfront | När en nytillagd version läggs till i ett dokument i Workfront kan användaren skicka den nya versionen till AEM för att ersätta den befintliga versionen. | ✓ | ✓ | ✓ |
| Resurser länkade i Workfront när användaren klickades på AEM | Användare dirigeras till AEM för att förhandsgranska en länkad resurs i Workfront. | ✓ | ✓ | Kommande |
| Skapa automatiskt länkade AEM i Workfront | Skapa automatiskt länkade AEM i Workfront med projektstatus. Konfigurera AEM automatiskt baserat på Workfront Portfolio, Program och Projekt. | Nej | ✓ | Nej |
| Navigera direkt till AEM från Workfront | Tillåt användare att navigera till tillgängliga AEM som konfigurerats i Workfront. | ✓ | Nej | ✓ |
| Skapa länkade AEM mappar i Workfront | Skapa länkade AEM i Workfront manuellt med hjälp av alternativet på fliken Dokument. | ✓ | Nej | ✓ |
| Synkronisering av kommentarer | Synkronisera kommentarer automatiskt för resurser från [!DNL Workfront] till [!DNL Assets] | Nej | ✓ | Nej |
| Stöd för flera Workfront-miljöer som ansluter till en enda AEM | Användare från flera Workfront-miljöer kan ansluta till en enda AEM. | ✓ | Nej | ✓ |
| Stöd för flera AEM miljöer som ansluter till en enda Workfront-miljö | Användare i en och samma Workfront-miljö kan skicka eller länka resurser mellan flera AEM miljöer. | ✓ | ✓ | ✓ |
| **Metadata** |
| Mappa metadata för Workfront-resurser till AEM Assets | Workfront-objekt och anpassade formuläregenskaper kan mappas till AEM metadataegenskaper för resurser. Värden överförs vid första överföring/länk. | ✓ | ✓ | ✓ |
| Skapa automatiskt anpassad Forms för dokument i Workfront | Bifoga skräddarsydda blanketter i Workfront dokument, uppgifter och ärenden med hjälp AEM arbetsflöden. | Nej | ✓ | Nej |
| Automatisk dubbelriktad uppdatering av metadata mellan AEM Assets och Workfront | Uppdatera automatiskt metadata mellan AEM Assets och Workfront. Resursen måste initialt skickas från Workfront till AEM och Workfront-resursens metadata måste mappas till AEM för att dubbelriktade metadatauppdateringar ska fungera korrekt. | Nej | ✓ | Nej |
| Vy i realtid i Workfront för mappade metadata till AEM | Visa de uppdaterade mappade metadata som AEM i Workfront dokumentinformation och dokumentsammanfattningspaneler. | ✓ | Nej | ✓ |
| Realtidspush av uppdaterade Workfront-metadata för AEM | Uppdatera automatiskt mappade Workfront-metadata till AEM utan att behöva återanvända en resurs eller en ny version av en resurs. | ✓ | Nej | ✓ |
| Mappa Workfront-metadata till AEM Assets-mappar | Synkronisera Workfront projektmetadata med länkade AEM. | Nej | ✓ | ✓ |
| AEM metadatauppdateringar med nya versioner | En konfiguration i AEM kan göras för att avgöra om en nyversion av en resurs i Workfront också ska pushas med ändringar i dess metadata. | Nej | ✓ | Nej |
| Uppdatera AEM metadata automatiskt vid ändringar i anpassad Forms i Workfront | AEM kan du prenumerera på uppdateringar av dokumentformulären i Workfront. Därför ändras värdena för mappade AEM metadatafält om du uppdaterar Workfront-dokumentets anpassade formulärmetadata. | Nej | ✓ | Nej |
| **Arbetsflöden (färdiga)** |
| Skapa ny korrekturversion på länkade resurser | När en resurs länkas i Workfront kan ett korrektur genereras automatiskt. | Nej | Egen | Nej |
| Ange status för Workfront-objekt | Ange Workfront objektstatusbaserade konfigurerbara villkor med hjälp av AEM arbetsflöden | Nej | ✓ | Kommande |
| Publicera resurser i AEM Publish Environment eller Brand Portal | Ge Workfront-användare möjlighet att automatiskt publicera länkade resurser i en AEM-publiceringsmiljö eller Brand Portal. | Nej | ✓ | Kommande |
