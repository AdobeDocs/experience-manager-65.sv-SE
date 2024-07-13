---
title: Konfigurera AEM Assets-integrering med Experience Cloud
description: Lär dig hur du konfigurerar AEM Assets-integrering med Experience Cloud.
contentOwner: AG
feature: Asset Management
role: User, Architect, Admin
exl-id: d167cf97-6829-45a7-ba46-2239d530b060
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 1%

---

# Konfigurera AEM Assets-integrering med Experience Cloud {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

Om du är kund hos Adobe Experience Cloud kan du synkronisera dina mediefiler inom Adobe Experience Manager Assets med Adobe Creative Cloud, och tvärtom. Du kan också synkronisera dina resurser med Experience Cloud och omvänt. Du kan konfigurera synkroniseringen via [!DNL Adobe I/O]. Det uppdaterade namnet för [!DNL Adobe Marketing Cloud] är [!DNL Adobe Experience Cloud].

Det arbetsflöde som ska användas för att konfigurera den här integreringen är:

1. Skapa en autentisering i [!DNL Adobe I/O] med en offentlig gateway och hämta ett program-ID.
1. Skapa en profil på din AEM Assets-instans med program-ID:t.
1. Använd den här konfigurationen för att synkronisera dina resurser.

I backend autentiserar AEM din profil med gatewayen och synkroniserar sedan data mellan Assets och Experience Cloud.

>[!NOTE]
>
>Den här funktionen är inaktuell i [!DNL Assets]. Sök efter ersättningar i [AEM och Creative Cloud-integrering ](/help/assets/aem-cc-integration-best-practices.md). [Kontakta Adobe kundsupport](https://www.adobe.com/account/sign-in.supportportal.html) om du har frågor.

<!-- Hiding this for now via cqdoc-16834.
![Flow of data when AEM Assets and Creative Cloud are integrated](assets/chlimage_1-48.png)

>[!NOTE]
>
>Sharing assets between Adobe Experience Cloud and Adobe Creative Cloud requires administrator privileges on the AEM instance.
-->

## Skapa ett program {#create-an-application}

1. Logga in på [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/) för att få åtkomst till Adobe Developer gatewaygränssnitt.

   >[!NOTE]
   >
   >Du måste ha administratörsbehörighet för att skapa ett program-ID.

1. I den vänstra rutan navigerar du till **[!UICONTROL Developer Tools]** > **[!UICONTROL Applications]** för att visa en lista med program.
1. Klicka på **[!UICONTROL Add]** ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png) för att skapa ett program.
1. I listan **[!UICONTROL Client Credentials]** väljer du **[!UICONTROL Service Account (JWT Assertion)]**, som är en server-till-server-kommunikationstjänst för serverautentisering.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Ange ett namn för programmet och en valfri beskrivning.
1. I listan **[!UICONTROL Organization]** väljer du den organisation som du vill synkronisera resurser för.
1. Välj **[!UICONTROL dam-read]**, **[!UICONTROL dam-sync]**, **[!UICONTROL dam-write]** och **[!UICONTROL cc-share]** i listan **[!UICONTROL Scope]**.
1. Klicka på **[!UICONTROL Create]**. Ett meddelande meddelar att programmet har skapats.

   ![Meddelande om att programmet har skapats för att integrera AEM Assets med Creative Cloud](assets/chlimage_1-50.png)

1. Kopiera **[!UICONTROL Application ID]** som genereras för det nya programmet.

   >[!CAUTION]
   >
   >Se till att du inte oavsiktligt kopierar **[!UICONTROL Application Secret]** i stället för **[!UICONTROL Application ID]**.

## Lägg till en ny konfiguration i Experience Cloud {#add-a-new-configuration}

1. Klicka på AEM logotyp i användargränssnittet för den lokala AEM Assets-instansen och navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**.

1. Leta reda på tjänsten **[!UICONTROL Adobe Experience Cloud]**. Om det inte finns några konfigurationer klickar du på **[!UICONTROL Configure Now]**. Om det finns konfigurationer klickar du på **[!UICONTROL Show Configurations]** och sedan på `+` för att lägga till en ny konfiguration.

   >[!NOTE]
   >
   >Använd ett Adobe ID-konto som har administratörsbehörighet för organisationen.

1. I dialogrutan **[!UICONTROL Create Configuration]** anger du en rubrik och ett namn för den nya konfigurationen och klickar på **[!UICONTROL Create]**.

   ![Namnge en ny konfiguration för integrering av AEM Assets och Creative Cloud](assets/aem-ec-integration-config1.png)

1. Ange URL:en för AEM Assets i fältet **[!UICONTROL Tenant URL]**. Tidigare, om URL-adressen har definierats som `https://<tenant_id>.marketing.adobe.com`, ändrar du den till `https://<tenant_id>.experiencecloud.adobe.com`.

   1. Navigera till **Verktyg > Cloud Service > Äldre Cloud Service**. Klicka på **Visa konfigurationer** under Adobe Experience Cloud.
   1. Välj den befintliga konfiguration som ska redigeras. Redigera konfigurationen och ersätt `marketing.adobe.com` till `experiencecloud.adobe.com`.
   1. Spara konfigurationen. Testa replikeringsagenterna för MAC-synkronisering.

1. Klistra in det program-ID som du kopierade i slutet av proceduren [skapa ett program](#create-an-application) i fältet **[!UICONTROL Client ID]**.

   ![Ange de program-ID-värden som krävs för att integrera AEM Assets och Creative Cloud](assets/cloudservices_tenant_info.png)

1. Under **[!UICONTROL Synchronization]** markerar du **[!UICONTROL Enabled]** för att aktivera synkronisering och klickar på **[!UICONTROL OK]**. Om du väljer **inaktiverad** fungerar synkroniseringen i en riktning.

1. Klicka på **[!UICONTROL Display Public Key]** på konfigurationssidan för att visa den offentliga nyckel som genererats för din instans. Du kan också klicka på **[!UICONTROL Download Public Key for OAuth Gateway]** om du vill hämta filen som innehåller den offentliga nyckeln. Öppna sedan filen för att visa den offentliga nyckeln.

## Aktivera synkronisering {#enable-synchronization}

1. Visa den offentliga nyckeln med någon av följande metoder som nämns i det sista steget i proceduren [lägg till en ny konfiguration i Experience Cloud](#add-a-new-configuration). Klicka på **[!UICONTROL Display Public Key]**.

1. Kopiera den offentliga nyckeln och klistra in den i fältet **[!UICONTROL Public Key]** i konfigurationsgränssnittet för programmet som du skapade i [skapa ett program](#create-an-application).

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. Klicka på **[!UICONTROL Update]**. Synkronisera dina resurser med AEM Assets-instansen nu.

## Testa synkroniseringen {#test-the-synchronization}

1. Klicka på den AEM logotypen i användargränssnittet för den lokala AEM Assets-instansen och navigera till **[!UICONTROL Tools]**> **[!UICONTROL Deployment]**> **[!UICONTROL Replication]**för att hitta de replikeringsprofiler som har skapats för synkronisering.
1. Klicka på **[!UICONTROL Agents on author]** på sidan **[!UICONTROL Replication]**.
1. I listan med profiler klickar du på standardreplikeringsprofilen för din organisation för att öppna den.
1. Klicka på **[!UICONTROL Test Connection]** i dialogrutan.

   ![Testa anslutningen och ange standardreplikeringsprofilen för organisationen](assets/chlimage_1-54.png)

1. När replikeringen är klar kontrollerar du om det finns ett meddelande om att åtgärden lyckades i slutet av testresultaten.

## Lägg till användare i Experience Cloud {#add-users-to-experience-cloud}

1. Logga in på Experience Cloud med administratörsautentiseringsuppgifter.
1. Gå till **[!UICONTROL Administration]** från skenorna och klicka sedan på **[!UICONTROL Launch Enterprise Dashboard]**.
1. Öppna sidan **[!UICONTROL User Management]** genom att klicka på **[!UICONTROL Users]** i fältet.
1. Klicka på **Lägg till** ![aem_assets_add_icon](assets/aem_assets_add_icon.png) i verktygsfältet.
1. Lägg till en eller flera användare som du vill ska kunna dela resurser med Creative Cloud.

<!-- TBD: Check.
   >[!NOTE]
   >
   >Only the users that you add to Experience Cloud can share assets from AEM Assets to Creative Cloud.

-->

## Utbyt resurser mellan AEM Assets och Experience Cloud {#exchange-assets-between-aem-and-experience-cloud}

1. Logga in på AEM Assets.
1. Skapa en mapp i Assets-konsolen och överför resurser till den. Skapa till exempel en mapp **mc-demo** och överför en resurs till den.
1. Markera mappen och klicka på **Dela** ![assets_share](assets/do-not-localize/assets_share.png).
1. Välj **[!UICONTROL Adobe Experience Cloud]** på menyn och klicka på **[!UICONTROL Share]**. Ett meddelande meddelar att mappen delas med Experience Cloud.

   >[!NOTE]
   >
   >Delning av en Assets-mapp av typen `sling:OrderedFolder` stöds inte vid delning i Adobe Experience Cloud. Om du vill dela en mapp ska du inte markera alternativet **[!UICONTROL Ordered]** när du skapar den i AEM Assets.

1. Uppdatera AEM Assets användargränssnitt. Mappen som du skapade i Assets-konsolen för den lokala AEM Assets-instansen kopieras till användargränssnittet i Experience Cloud. Resursen som du överför till mappen i AEM Assets visas i kopian av mappen i Experience Cloud efter att den har bearbetats av AEM server.
1. Du kan också överföra en resurs i den replikerade kopian av mappen i Experience Cloud. När resursen har bearbetats visas den i den delade mappen i AEM Assets.

<!-- Removing as per PM guidance via https://jira.corp.adobe.com/browse/CQDOC-16834?focusedCommentId=22881523&page=com.atlassian.jira.plugin.system.issuetabpanels:comment-tabpanel#comment-22881523.

## Exchange assets between AEM Assets and Creative Cloud {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
>
>The AEM to Creative Cloud Folder Sharing feature is deprecated. Customers are strongly advised to use newer capabilities, like [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) or [AEM desktop app](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html). Learn more in [AEM and Creative Cloud Integration Best Practices](/help/assets/aem-cc-integration-best-practices.md).

AEM Assets lets you share folders containing assets with Adobe Creative Cloud users.

1. In the Assets console, select the folder to share with Creative Cloud.
1. From the toolbar, click **[!UICONTROL Share]** ![assets_share](assets/do-not-localize/assets_share.png).
1. From the list, select the **[!UICONTROL Adobe Creative Cloud]** option.

   >[!NOTE]
   >
   >The options are available for users with read permissions on the root. Users must have the required permission to access the replication agent information of Marketing Cloud.

1. In the **[!UICONTROL Creative Cloud Sharing]** page, add the user to share the folder with and choose a role for the user. Click **[!UICONTROL Save]** and click **[!UICONTROL OK]**.

1. Log on to Creative Cloud with the credentials of the user you shared the folder with. The shared folder is available in Creative Cloud.

The AEM Assets-Marketing Cloud synchronization is designed in a way that the user machine instance from where the asset is uploaded retains the right to modify the asset. Only these changes are propagated to the other instance.

For example, if an asset is uploaded from an AEM Assets (on premises) instance, the changes to the asset from this instance are propagated to the Marketing Cloud instance. However, the changes done from the Marketing Cloud instance to the same asset aren’t propagated to the AEM instance and conversely for asset uploaded from Marketing Cloud.
-->

>[!MORELIKETHIS]
>
>* [Bästa praxis för integrering mellan Assets och Creative Cloud](/help/assets/aem-cc-integration-best-practices.md)
