---
title: Installera [!DNL Workfront for Experience Manager enhanced connector]
description: Installera [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
source-git-commit: a589836c77fd919838dce60a1eaf676683c165c0
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Installera [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

En användare med administratörsåtkomst i [!DNL Adobe Experience Manager] installerar den utökade anslutningen. Innan du installerar bör du granska plattformsstödet och andra [krav för kopplingen](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!TIP]
>
>Söker du efter [!DNL Workfront for Experience Manager enhanced connector] dokumentation för AEM as a Cloud Service? Klicka [här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en).

>[!IMPORTANT]
>
>Adobe kräver installation och konfiguration av [!DNL Adobe Workfront for Experience Manager enhanced connector] endast via certifierade partners eller [!DNL Adobe Professional Services]. Om den distribueras och konfigureras utan en certifierad partner eller [!DNL Adobe Professional Services], stöds den inte av Adobe.
>
>Adobe kan släppa uppdateringar av [!DNL Adobe Workfront] och [!DNL Adobe Experience Manager] som gör denna koppling redundant, Om detta inträffar kan kunderna behöva gå över från att använda denna koppling.

Så här installerar du kopplingen:

1. Hämta anslutningen från [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [Konfigurera brandväggen](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).

1. Tillåt HTTP-huvuden med namnet i dispatchern `authorization`, `username`och `apikey`. Tillåt `GET`, `POST`och `PUT` förfrågningar till `/bin/workfront-tools`.

1. Kontrollera att följande sökvägar inte finns i [!DNL Experience Manager] databas:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. Installera paketet med [!UICONTROL Package Manager]. Mer information om hur du installerar paket finns i [Pakethanterarens dokumentation](/help/sites-administering/package-manager.md).

1. Skapa `wf-workfront-users` in [!DNL Experience Manager] Användargrupp och tilldela behörighet `jcr:all` till `/content/dam`.

En systemanvändare `workfront-tools` skapas automatiskt och de behörigheter som krävs hanteras automatiskt. Alla användare från [!DNL Workfront] som använder kopplingen läggs automatiskt till som en del av den här gruppen.

## Konfigurera anslutningen mellan [!DNL Experience Manager] och [!DNL Workfront] {#configure-connection}

Så här skapar du en anslutning till Workfront:

1. I [!DNL Experience Manager] väljer du **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]**.

1. Välj `workfront-tools` i den vänstra panelen och väljer **[!UICONTROL Create]** i det övre högra hörnet på sidan.

1. I **[!UICONTROL Workfront Connection]** kan du ange den information du behöver [!DNL Workfront] driftsättning och välj **[!UICONTROL Connect to Workfront]** alternativ. När anslutningen är klar [!DNL Workfront] anpassad integration av dokument skapas automatiskt i [!DNL Workfront] miljö.

   ![Anslut [!DNL Experience Manager] och [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Om du vill verifiera anslutningen öppnar du den i [!DNL Workfront] och verifiera att API-nyckeln är densamma och att anslutningen är **[!UICONTROL Enabled]**. Om du vill göra det väljer du **[!UICONTROL Setup]** > **[!UICONTROL Documents]** > **[!UICONTROL Custom Integrations]** in [!DNL Workfront].

## Uppdatera [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Med Experience Manager Assets kan du uppdatera [!DNL Workfront for Experience Manager enhanced connector] från en tidigare version till den senaste versionen.

Så här uppdaterar du [!DNL Workfront for Experience Manager enhanced connector] till den senaste versionen:

1. Hämta den senaste versionen av den förbättrade anslutningen från [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. Installera paketet med [!UICONTROL Package Manager]. Mer information om hur du installerar paket finns i [Pakethanterarens dokumentation](/help/sites-administering/package-manager.md).


