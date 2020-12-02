---
title: Konfigurera AEM Assets-integrering med Experience Cloud och Creative Cloud
seo-title: Konfigurera AEM Assets-integrering med Marketing Cloud och Creative Cloud
description: Lär dig hur du konfigurerar AEM Assets-integrering med Experience Cloud och Creative Cloud.
seo-description: Lär dig hur du konfigurerar AEM Assets-integrering med Experience Cloud och Creative Cloud.
uuid: ec36ea0e-607f-4c73-89df-e095067fccd4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 82a8e807-a2df-4fe3-a68c-2dabc9328eca
docset: aem65
translation-type: tm+mt
source-git-commit: c7f06670ca8b488a661fde7a133bce6886ee7f5d
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 1%

---


# Konfigurera AEM Assets-integrering med Experience Cloud och Creative Cloud {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

Om du är kund hos Adobe Experience Cloud kan du synkronisera dina mediefiler i Adobe Experience Manager (AEM) Assets med Adobe Creative Cloud, och vice versa. Du kan också synkronisera dina resurser med Experience Cloud och vice versa. Du kan konfigurera synkroniseringen via Adobe I/O.

Det arbetsflöde som ska användas för att konfigurera den här integreringen är:

1. Skapa en autentisering i Adobe I/O med en offentlig gateway och få ett program-ID.
1. Skapa en profil på din AEM Assets-instans med program-ID:t.
1. Använd den här konfigurationen för att synkronisera dina resurser inom AEM Assets med Creative Cloud.

I backend autentiserar AEM din profil med gatewayen och synkroniserar sedan data mellan AEM Assets och Experience Cloud.

>[!CAUTION]
>
>Mappdelningsfunktionen AEM till Creative Cloud används inte i AEM Assets. Läs mer och hitta ersättningar i [Bästa praxis för integrering av AEM och Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

![Dataflöde när AEM Assets och Creative Cloud är integrerade](assets/chlimage_1-48.png)

Dataflöde när AEM Assets och Creative Cloud är integrerade

>[!NOTE]
>
>Om du vill dela resurser mellan Adobe Experience Cloud och Adobe Creative Cloud måste du ha administratörsbehörighet för AEM.

>[!CAUTION]
>
>Adobe Marketing Cloud har fått namnet Adobe Experience Cloud. I förfarandena nedan anges fortfarande Marketing Cloud för att återspegla det nuvarande gränssnittet. Dessa omnämnanden kommer att ändras vid ett senare datum.

## Skapa ett program {#create-an-application}

1. Gå till Adobe Developer gateway-gränssnittet genom att logga in på [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/).

   >[!NOTE]
   >
   >Du måste ha administratörsbehörighet för att skapa ett program-ID.

1. I den vänstra rutan navigerar du till **[!UICONTROL Developer Tools]** > **[!UICONTROL Applications]** för att visa en lista med program.
1. Klicka på **[!UICONTROL Add]** ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png) för att skapa ett program.
1. I listan **[!UICONTROL Client Credentials]** väljer du **[!UICONTROL Service Account (JWT Assertion)]**, som är en server-till-server-kommunikationstjänst för serverautentisering.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Ange ett namn för programmet och en valfri beskrivning.
1. I listan **[!UICONTROL Organization]** väljer du den organisation som du vill synkronisera resurser för.
1. I listan **[!UICONTROL Scope]** väljer du **[!UICONTROL dam-read]**, **[!UICONTROL dam-sync]**, **[!UICONTROL dam-write]** och **[!UICONTROL cc-share]**.
1. Klicka på **[!UICONTROL Create]**. Ett meddelande meddelar att programmet har skapats.

   ![Meddelande om att programmet har skapats för att integrera AEM Assets med Adobe CC](assets/chlimage_1-50.png)

1. Kopiera **[!UICONTROL Application ID]** som genereras för det nya programmet.

   >[!CAUTION]
   >
   >Se till att du inte oavsiktligt kopierar **[!UICONTROL Application Secret]** i stället för **[!UICONTROL Application ID]**.

## Lägg till en ny konfiguration i Marketing Cloud {#add-a-new-configuration-to-marketing-cloud}

1. Klicka på den AEM logotypen i användargränssnittet för den lokala AEM Assets-instansen och navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**.

1. Leta reda på tjänsten **[!UICONTROL Adobe Marketing Cloud]**. Om det inte finns några konfigurationer klickar du på **[!UICONTROL Configure Now]**. Om det finns konfigurationer klickar du på **[!UICONTROL Show Configurations]** och sedan på `+` för att lägga till en ny konfiguration.

   >[!NOTE]
   >
   >Använd ett Adobe ID-konto som har administratörsbehörighet för organisationen.

1. I dialogrutan **[!UICONTROL Create Configuration]** anger du en titel och ett namn för den nya konfigurationen och klickar på **[!UICONTROL Create]**.

   ![Namnge en ny konfiguration för integrering av AEM Assets och CC](assets/chlimage_1-51.png)

1. I fältet **[!UICONTROL Tenant URL]** anger du URL:en för AEM Assets.

   >[!CAUTION]
   >
   >Om du angav klientens URL som `https://<tenant_id>.marketing.adobe.com` måste du ändra den till `https://<tenant_id>.experiencecloud.adobe.com.` för att kunna göra detta, följer du stegen nedan:
   >
   >1. Navigera till **Verktyg > Cloud Services > Äldre Cloud Services**.
   1. Klicka på **Visa konfigurationer** under Adobe Marketing Cloud.
   1. Välj den konfiguration som skapades när AEM-MAC-CC-synkroniseringen konfigurerades.
   1. Redigera molntjänstkonfigurationen och ersätt **marketing.adobe.com** i fältet för klientens URL till **experience.adobe.com**.
   1. Spara konfigurationen.
   1. Testa replikeringsagenterna för mac-sync.


1. Klistra in det program-ID som du kopierade i slutet av proceduren [Skapa ett program](/help/sites-administering/configure-assets-cc-integration.md#create-an-application) i fältet **[!UICONTROL Client ID]**.

   ![Ange de program-ID-värden som krävs för att integrera AEM Assets och Creative Cloud](assets/cloudservices_tenant_info.png)

1. Under **[!UICONTROL Synchronization]** markerar du **[!UICONTROL Enabled]** för att aktivera synkronisering och klickar på **[!UICONTROL OK]**.

   >[!NOTE]
   Om du väljer **inaktiverad** fungerar synkroniseringen i en riktning.

1. Klicka på **[!UICONTROL Display Public Key]** på konfigurationssidan för att visa den offentliga nyckel som genererats för din instans. Du kan också klicka på **[!UICONTROL Download Public Key for OAuth Gateway]** för att hämta filen som innehåller den offentliga nyckeln. Öppna sedan filen för att visa den offentliga nyckeln.

## Aktivera synkronisering {#enable-synchronization}

1. Visa den offentliga nyckeln med någon av följande metoder som anges i det sista steget i proceduren [Lägg till en ny konfiguration i Marketing Cloud](/help/sites-administering/configure-assets-cc-integration.md#add-a-new-configuration-to-marketing-cloud). Klicka på **[!UICONTROL Display Public Key]**.

   ![chlimage_1-52](assets/chlimage_1-52.png)

1. Kopiera den offentliga nyckeln och klistra in den i fältet **[!UICONTROL Public Key]** i konfigurationsgränssnittet för det program du skapade i [Skapa ett program](/help/sites-administering/configure-assets-cc-integration.md#create-an-application).

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. Klicka på **[!UICONTROL Update]**. Synkronisera dina resurser med AEM Assets-instansen nu.

## Testa synkroniseringen {#test-the-synchronization}

1. Klicka på den AEM logotypen i användargränssnittet för den lokala AEM Assets-instansen och navigera till **[!UICONTROL Tools]**> **[!UICONTROL Deployment]**> **[!UICONTROL Replication]**för att hitta de replikeringsprofiler som har skapats för synkronisering.
1. På sidan **[!UICONTROL Replication]** klickar du på **[!UICONTROL Agents on author]**.
1. I listan med profiler klickar du på standardreplikeringsprofilen för din organisation för att öppna den.
1. Klicka på **[!UICONTROL Test Connection]** i dialogrutan.

   ![Testa anslutningen och ange organisationens standardreplikeringsprofil](assets/chlimage_1-54.png)

1. När replikeringen är klar kontrollerar du om det finns ett meddelande om att åtgärden lyckades i slutet av testresultaten.

## Lägg till användare i Marketing Cloud {#add-users-to-marketing-cloud}

1. Logga in på Marketing Cloud med administratörsautentiseringsuppgifter.
1. Gå till **[!UICONTROL Administration]** från skenorna och klicka/tryck sedan på **[!UICONTROL Launch Enterprise Dashboard]**.
1. Öppna sidan **[!UICONTROL User Management]** genom att klicka på **[!UICONTROL Users]** på listen.
1. Klicka/tryck på **Lägg till** ![aem_assets_add_icon](assets/aem_assets_add_icon.png) i verktygsfältet.
1. Lägg till en eller flera användare som du vill ska kunna dela resurser med Creative Cloud.

   >[!NOTE]
   Endast de användare som du lägger till i Marketing Cloud kan dela resurser från AEM Assets till Creative Cloud.

## Växla resurser mellan AEM Assets och Marketing Cloud {#exchange-assets-between-aem-assets-and-marketing-cloud}

1. Logga in på AEM Assets.
1. Skapa en mapp i resurskonsolen och överför några resurser till den. Skapa till exempel en mapp **mc-demo** och överför en resurs till den.
1. Markera mappen och klicka på **Dela** ![assets_share](assets/assets_share.png).
1. Välj **[!UICONTROL Adobe Marketing Cloud]** på menyn och klicka på **[!UICONTROL Share]**. Ett meddelande meddelar att mappen delas med Marketing Cloud.

   ![chlimage_1-55](assets/chlimage_1-55.png)

   >[!NOTE]
   Delning av en resursmapp av typen `sling:OrderedFolder` stöds inte vid delning i Adobe Marketing Cloud. Om du vill dela en mapp ska du inte markera alternativet **[!UICONTROL Ordered]** när du skapar den i AEM Assets.

1. Uppdatera AEM Assets användargränssnitt. Mappen som du skapade i resurskonsolen för din lokala AEM Assets-instans kopieras till användargränssnittet för Marketing Cloud. Resursen som du överför till mappen i AEM Assets visas i kopian av mappen i Marketing Cloud efter att den har bearbetats av AEM server.
1. Du kan också överföra en resurs i den replikerade kopian av mappen i Marketing Cloud. När resursen har bearbetats visas den i den delade mappen i AEM Assets.

## Växla resurser mellan AEM Assets och Creative Cloud {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
Mappdelningsfunktionen AEM till Creative Cloud är föråldrad. Kunderna rekommenderas att använda nyare funktioner, som [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) eller [AEM datorprogram](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html). Läs mer i [Bästa praxis för integrering av AEM och Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

Med AEM Assets kan du dela mappar som innehåller resurser med Adobe Creative Cloud-användare.

1. I resurskonsolen väljer du den mapp som ska delas med Creative Cloud.
1. Klicka på **[!UICONTROL Share]** ![assets_share](assets/assets_share.png) i verktygsfältet.
1. Välj alternativet **[!UICONTROL Adobe Creative Cloud]** i listan.

   >[!NOTE]
   Alternativen är tillgängliga för användare med läsbehörighet för roten. Användarna måste ha behörighet att komma åt replikeringsagentinformationen för Marketing Cloud.

1. På sidan **[!UICONTROL Creative Cloud Sharing]** lägger du till användaren som ska dela mappen med och väljer en roll för användaren. Klicka på **[!UICONTROL Save]** och klicka på **[!UICONTROL OK]**.

1. Logga in på Creative Cloud med inloggningsuppgifterna för den användare som du delade mappen med. Den delade mappen är tillgänglig i Creative Cloud.

Synkroniseringen mellan AEM Assets och Marketing Cloud är utformad så att användardatorinstansen som resursen överförs från behåller rätten att ändra resursen. Endast dessa ändringar sprids till den andra instansen.

Om en resurs till exempel överförs från en AEM Assets-instans (lokalt), sprids ändringarna av resursen från den här instansen till instansen Marketing Cloud. Ändringar som görs från Marketing Cloud-instansen till samma resurs sprids dock inte till AEM och vice versa för resurser som överförs från Marketing Cloud.

>[!MORELIKETHIS]
* [Bästa praxis för integrering av AEM och Creative Cloud](/help/assets/aem-cc-integration-best-practices.md)
* [Metodtips för att dela AEM till Creative Cloud](/help/assets/aem-cc-folder-sharing-best-practices.md)

