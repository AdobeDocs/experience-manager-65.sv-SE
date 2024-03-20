---
title: Installera [!DNL Workfront for Experience Manager enhanced connector]
description: Installera [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
hide: true
solution: Experience Manager, Workfront
source-git-commit: 5ccac0aadce3971e66da052d393cbd33b61e94f7
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 1%

---

# Installera [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en) |
| AEM 6.5 | Den här artikeln |

En användare med administratörsåtkomst i [!DNL Adobe Experience Manager] installerar den utökade anslutningen. Läs mer om plattformsstödet och andra funktioner innan du installerar [krav för kopplingen](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe kräver installation och konfiguration av [!DNL Adobe Workfront for Experience Manager enhanced connector] endast via certifierade partners eller [!DNL Adobe Professional Services]. Om den distribueras och konfigureras utan en certifierad partner eller [!DNL Adobe Professional Services], stöds den inte av Adobe.
>
>* Adobe kan släppa uppdateringar av [!DNL Adobe Workfront] och [!DNL Adobe Experience Manager] som gör den här kopplingen överflödig. Om detta inträffar kan kunderna behöva gå över från att använda den här anslutningen.
>
>* Adobe har stöd för utökade anslutningsversioner 1.7.4 och senare. Tidigare förhandsversioner och anpassade versioner stöds inte. Om du vill kontrollera den utökade anslutningsversionen går du till `digital.hoodoo` grupp tillgänglig i den vänstra rutan i [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en).
>
>* Se [Partnercertifieringsprov för Workfront för Experience Manager Assets förbättrad anslutning](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Mer information om provet finns i [Provguide](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

Så här installerar du kopplingen:

1. Hämta anslutningen från [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. [Konfigurera brandväggen](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).
1. Tillåt HTTP-huvuden med namnet på Dispatcher `authorization`, `username`och `apikey`. Tillåt `GET`, `POST`och `PUT` förfrågningar till `/bin/workfront-tools`.
1. Kontrollera att följande sökvägar inte finns i [!DNL Experience Manager] databas:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. Installera paketet med [!UICONTROL Package Manager]. Mer information om hur du installerar paket finns i [Pakethanterarens dokumentation](/help/sites-administering/package-manager.md).
1. Skapa `wf-workfront-users` in [!DNL Experience Manager] Användargrupp och tilldela behörighet `jcr:all` till `/content/dam`.
1. Lägg till en anpassad egenskap i indexdefinitionen utanför rutan för **`ntFolderDamLucene(/oak:index/ntFolderDamLucene)`**. Utför följande steg:
   * Lägg till en **`nt:unstructured`** egenskap med namnet **`wfReferenceNumber`** till:
     `/oak:index/ntFolderDamLucene/indexRules/nt:folder/properties/wfReferenceNumber`.
   * Indexera om `index /oak:index/ntFolderDamLucene` genom att vända omindexeringsflaggan till `true`.

En systemanvändare `workfront-tools` skapas automatiskt och de behörigheter som krävs hanteras automatiskt. Alla användare från [!DNL Workfront] som använder kopplingen läggs automatiskt till som en del av den här gruppen.

## Konfigurera anslutningen mellan [!DNL Experience Manager] och [!DNL Workfront] {#configure-connection}

Så här skapar du en anslutning till Workfront:

1. I [!DNL Experience Manager], markera **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]**.

1. Välj `workfront-tools` i den vänstra panelen och väljer **[!UICONTROL Create]** i det övre högra hörnet på sidan.

1. I **[!UICONTROL Workfront Connection]** kan du ange den information du behöver [!DNL Workfront] driftsättning och välj **[!UICONTROL Connect to Workfront]** alternativ. När anslutningen är klar är [!DNL Workfront] anpassad integration av dokument skapas automatiskt i [!DNL Workfront] miljö.

   ![Anslut [!DNL Experience Manager] och [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Om du vill verifiera anslutningen öppnar du den i [!DNL Workfront] och verifiera att API-nyckeln är densamma och att anslutningen är **[!UICONTROL Enabled]**. Om du vill göra det väljer du **[!UICONTROL Setup]** > **[!UICONTROL Documents]** > **[!UICONTROL Custom Integrations]** in [!DNL Workfront].

## Uppdatera [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Med Experience Manager Assets kan du uppdatera [!DNL Workfront for Experience Manager enhanced connector] från en tidigare version till den senaste versionen.

Uppdatera [!DNL Workfront for Experience Manager enhanced connector] till den senaste versionen:

1. Hämta den senaste versionen av den förbättrade anslutningen från [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. Installera paketet med [!UICONTROL Package Manager]. Mer information om hur du installerar paket finns i [Pakethanterarens dokumentation](/help/sites-administering/package-manager.md).
