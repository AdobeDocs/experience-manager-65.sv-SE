---
title: Integrering av [!DNL Experience Manager Assets] med  [!DNL Adobe Workfront]
description: Introduktion till integrering mellan  [!DNL Assets] och [!DNL Workfront]
role: Admin,Leader,Architect
feature: Workfront Integrations and Apps
exl-id: 57e2bffe-8094-4557-99c8-7b482681687e
hide: true
solution: Experience Manager, Workfront
source-git-commit: 5ccac0aadce3971e66da052d393cbd33b61e94f7
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---

# Integrering av [!DNL Adobe Experience Manager Assets] med [!DNL Adobe Workfront] {#assets-integration-overview}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=en) |
| AEM 6.5 | Den här artikeln |

[!DNL Adobe Workfront] är ett program för arbetshantering som hjälper dig att hantera hela arbetscykeln på ett och samma ställe. Integrationen mellan [!DNL Workfront] och [!DNL Adobe Experience Manager Assets] gör att organisationer kan förbättra innehållets hastighet och time-to-market genom att knyta samman arbete och hantering av digitala resurser. När man arbetar i Workfront får man tillgång till dokument och bilder.

[!DNL Workfront for Experience Manager enhanced connector] möjliggör förbättrade affärsprocesser med kompletta arbetsflöden och ger personaliserade klientupplevelser från början till slut och central lagring. Adobe har en standardanslutning och en förbättrad anslutning för att integrera de två lösningarna. Se funktionerna som stöds nedan för en jämförelse och se [vad som är nytt i  [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

Med [!DNL Workfront for Experience Manage enhanced connector] kan din organisation:

* Skapa automatiskt länkade Experience Manager-mappar i Workfront och ordna mapparna baserat på Workfront Portfolio, Program och Projekt.
* Synkronisera Workfront-projektmetadata med länkade Experience Manager-mappar.
* Experience Manager metadatauppdateringar med nya versioner.
* Ange objektstatus för Workfront baserat på konfigurerbara villkor med hjälp av arbetsflöden i Experience Manager.
* Publish-material till Experience Manager eller till Brand Portal.

Se plattformsstödet och [förutsättningarna för den förbättrade anslutningen](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe kräver att [!DNL Adobe Workfront for Experience Manager enhanced connector] distribueras och konfigureras endast via certifierade partners eller [!DNL Adobe Professional Services]. Om den distribueras och konfigureras utan en certifierad partner eller [!DNL Adobe Professional Services] stöds den inte av Adobe.
>
>* Adobe kan släppa uppdateringar till [!DNL Adobe Workfront] och [!DNL Adobe Experience Manager] som gör den här kopplingen överflödig. Om detta inträffar kan kunderna behöva gå över från att använda den här kopplingen.
>
>* Adobe har stöd för utökade anslutningsversioner 1.7.4 och senare. Tidigare förhandsversioner och anpassade versioner stöds inte. Om du vill kontrollera den utökade anslutningsversionen går du till gruppen `digital.hoodoo` som finns i den vänstra rutan i [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en).
>
>* Se [Partnercertifieringsprov för Workfront för Experience Manager Assets förbättrade anslutningsprogram](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Mer information om provet finns i [Handbok för prov](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Jämför olika integreringar mellan [!DNL Assets] och [!DNL Workfront] {#feature-parity-matrix}

Nedan följer information om de funktioner som är tillgängliga genom olika typer av integreringar mellan [!DNL Assets] och [!DNL Workfront].

| Funktion | Beskrivning | [!DNL Workfront] och [!DNL Assets Essentials] *Ingen koppling (ej i kartong)* | [!DNL Workfront for Experience Manager enhanced connector] *Kräver anslutning* | Workfront och [!DNL Experience Manager as a Cloud Service] *Ingen koppling (färdig)* |
|----|----|----|-----|-----|
| Distributionsmetoder | Lämpligt för vilket [!DNL Assets]-erbjudande. | Assets Essentials | Adobe Managed Services, lokal | Cloud Service |
| **Allmänt** |
| Skicka digitala filer från [!DNL Workfront] till [!DNL Assets] | Den senaste versionen av ett WF-dokument kan överföras till AEM Assets som är länkat som en ny version av dokumentet. | ✓ | ✓ | ✓ |
| Länka AEM mappar manuellt till Workfront-objekt | Befintliga AEM kan länkas som en Workfront-mapp och dess underordnade resurser länkas som nya Workfront-dokument. | ✓ | ✓ | ✓ |
| Länka [!DNL Assets] till Workfront-objekt | Befintliga AEM kan länkas till ett nytt Workfront-dokument eller som en ny version av ett befintligt dokument. | ✓ | ✓ | ✓ |
| Assets som läggs till i länkade mappar skickas automatiskt till AEM | Om ett dokument läggs till i en länkad mapp överförs den associerade resursen automatiskt till AEM Assets som en ny resurs. | ✓ | ✓ | ✓ |
| Hämta länkade AEM Assets inifrån Workfront | När en resurs är länkad i Workfront kan användaren hämta resursens byte. | ✓ | ✓ | ✓ |
| Sök efter AEM Assets inifrån Workfront | Med AEM Assets-väljaren i Workfront kan du göra fulltextsökningar efter resurser. | ✓ | ✓ | ✓ |
| Sök efter AEM mappar i Workfront | Med AEM Assets-väljaren i Workfront kan du söka i fulltext efter mappar. | ✓ | ✓ | ✓ |
| Visa och navigera AEM mapphierarki inifrån Workfront | Med AEM Assets-väljaren i Workfront kan du bläddra i den AEM Assets-hierarki som begränsas av   användarens associerade åtkomstkontroller och behörigheter som anges i AEM. | ✓ | ✓ | ✓ |
| Spåra resursversioner AEM tidslinjer | Bevara dokumentversionshistorik mellan Workfront och AEM. | ✓ | ✓ | ✓ |
| Avlänka Assets från AEM Assets i Workfront | En befintlig länkad resurs från AEM kan tas bort från det associerade Workfront-dokumentet. Originalresursen i AEM tas inte bort. | ✓ | ✓ | ✓ |
| Lägg till ny versionshanterad resurs i AEM Assets från Workfront | När en nytillagd version läggs till i ett dokument i Workfront kan användaren skicka den nya versionen till AEM för att ersätta den befintliga versionen. | ✓ | ✓ | ✓ |
| Assets länkad i Workfront när användaren klickar på Direkt AEM | Användare dirigeras till AEM för att förhandsgranska en länkad resurs i Workfront. | ✓ | ✓ | Kommande |
| Skapa automatiskt länkade AEM i Workfront | Skapa automatiskt länkade AEM i Workfront med hjälp av projektstatus. Konfigurera AEM automatiskt baserat på Workfront Portfolio, Program och Projekt. | Nej | ✓ | Nej |
| Navigera direkt till AEM från Workfront | Tillåt användare att navigera till tillgängliga AEM som konfigurerats i Workfront. | ✓ | Nej | ✓ |
| Skapa länkade AEM mappar i Workfront | Skapa länkade AEM i Workfront manuellt med hjälp av alternativet på fliken Dokument. | ✓ | Nej | ✓ |
| Synkronisering av kommentarer | Synkronisera kommentarer automatiskt för resurser från [!DNL Workfront] till [!DNL Assets] | Nej | ✓ | Nej |
| Stöd för flera Workfront-miljöer som ansluter till en enda AEM | Användare från flera Workfront-miljöer kan ansluta till en enda AEM. | ✓ | Nej | ✓ |
| Stöd för flera AEM miljöer som ansluter till en enda Workfront-miljö | Användare i en och samma Workfront-miljö kan skicka eller länka resurser mellan flera olika AEM miljöer. | ✓ | ✓ | ✓ |
| **Metadata** |
| Mappa metadata för Workfront-resurser till AEM Assets | Workfront-objekt och anpassade formuläregenskaper kan mappas till AEM metadataegenskaper för resurser. Värden överförs vid den initiala överföringen/länken. | ✓ | ✓ | ✓ |
| Skapa automatiskt anpassad Forms för dokument i Workfront | Bifoga skräddarsydda blanketter i Workfront dokument, uppgifter och ärenden med hjälp AEM arbetsflöden. | Nej | ✓ | Nej |
| Automatisk dubbelriktad uppdatering av metadata mellan AEM Assets och Workfront | Uppdatera automatiskt metadata mellan AEM Assets och Workfront. Resursen måste initialt skickas från Workfront till AEM och Workfront-resursens metadata måste mappas till AEM resurser för att dubbelriktade metadatauppdateringar ska fungera korrekt. | Nej | ✓ | Nej |
| Vy i realtid i Workfront för mappade metadata till AEM | Visa de uppdaterade mappade metadata som AEM i Workfront dokumentinformation och dokumentsammanfattningspaneler. | ✓ | Nej | ✓ |
| Realtidspush av uppdaterade Workfront-metadata för AEM | Uppdatera automatiskt mappade Workfront-metadata till AEM utan att behöva återanvända en resurs eller en ny version av en resurs. | ✓ | Nej | ✓ |
| Mappa Workfront-metadata till AEM Assets-mappar | Synkronisera Workfront projektmetadata med länkade AEM. | Nej | ✓ | ✓ |
| AEM metadatauppdateringar med nya versioner | En konfiguration i AEM kan göras för att avgöra om en nyversion av en resurs i Workfront också ska pushas med ändringar i dess metadata. | Nej | ✓ | Nej |
| Uppdatera AEM metadata automatiskt vid ändringar i anpassad Forms i Workfront | AEM kan du prenumerera på uppdateringar av dokumentformulären i Workfront. Detta innebär att eventuella uppdateringar av Workfront-dokumentets anpassade metadata redigerar värdena för de mappade AEM metadatafälten. | Nej | ✓ | Nej |
| **Arbetsflöden (färdiga)** |
| Skapa ny korrekturversion på länkade Assets | När en resurs länkas i Workfront kan ett korrektur genereras automatiskt. | Nej | Egen | Nej |
| Ange status för Workfront-objekt | Ange Workfront objektstatusbaserade konfigurerbara villkor med hjälp av AEM arbetsflöden | Nej | ✓ | Kommande |
| Publish Assets till AEM Publish Environment eller Brand Portal | Ge Workfront-användare möjlighet att automatiskt publicera länkade resurser i en AEM Publish-miljö eller Brand Portal. | Nej | ✓ | Kommande |
