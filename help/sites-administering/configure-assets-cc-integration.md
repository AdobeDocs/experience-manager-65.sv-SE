---
title: Konfigurera integrering av AEM Assets med Experience Cloud och Creative Cloud
seo-title: Konfigurera integrering av AEM Assets med Marketing Cloud och Creative Cloud
description: Lär dig hur du konfigurerar integreringen mellan AEM Assets med Experience Cloud och Creative Cloud.
seo-description: Lär dig hur du konfigurerar integreringen mellan AEM Assets med Experience Cloud och Creative Cloud.
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


# Konfigurera integrering av AEM Assets med Experience Cloud och Creative Cloud {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

Om du är kund hos Adobe Experience Cloud kan du synkronisera dina mediefiler i Adobe Experience Manager (AEM) Assets med Adobe Creative Cloud, och vice versa. Du kan också synkronisera dina resurser med Experience Cloud och vice versa. Du kan konfigurera synkroniseringen via Adobe I/O.

Det arbetsflöde som används för att konfigurera den här integreringen är:

1. Skapa en autentisering i Adobe I/O med en offentlig gateway och få ett program-ID.
1. Skapa en profil på din AEM Assets-instans med program-ID:t.
1. Använd den här konfigurationen för att synkronisera dina resurser i AEM Assets med Creative Cloud.

I backend autentiserar AEM din profil med gatewayen och synkroniserar sedan data mellan AEM Assets och Experience Cloud.

>[!CAUTION]
>
>Mappdelningsfunktionen AEM till Creative Cloud används inte i AEM Assets. Läs mer och hitta ersättningar i [AEM och Creative Cloud-integreringsmetodtips](/help/assets/aem-cc-integration-best-practices.md).

![Dataflöde när AEM Assets och Creative Cloud integreras](assets/chlimage_1-48.png)

Dataflöde när AEM Assets och Creative Cloud integreras

>[!NOTE]
>
>Om du vill dela resurser mellan Adobe Experience Cloud och Adobe Creative Cloud måste du ha administratörsbehörighet för AEM.

>[!CAUTION]
>
>Adobe Marketing Cloud har fått namnet Adobe Experience Cloud. I förfarandena nedan anges fortfarande Marketing Cloud för att återspegla det nuvarande gränssnittet. Dessa omnämnanden kommer att ändras vid ett senare datum.

## Skapa ett program {#create-an-application}

1. Logga in på [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/).

   >[!NOTE]
   >
   >Du måste ha administratörsbehörighet för att skapa ett program-ID.

1. I den vänstra rutan navigerar du till **[!UICONTROL Developer Tools]** > **[!UICONTROL Applications]** för att visa en lista med program.
1. Klicka på **[!UICONTROL Add]** aem_assets_addcircle_icon ![](assets/aem_assets_addcircle_icon.png) för att skapa ett program.
1. I **[!UICONTROL Client Credentials]** listan väljer du **[!UICONTROL Service Account (JWT Assertion)]**, som är en server-till-server-kommunikationstjänst för serverautentisering.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Ange ett namn för programmet och en valfri beskrivning.
1. I **[!UICONTROL Organization]** listan väljer du den organisation som du vill synkronisera resurser för.
1. I **[!UICONTROL Scope]** listan väljer du **[!UICONTROL dam-read]**, **[!UICONTROL dam-sync]**, **[!UICONTROL dam-write]** och **[!UICONTROL cc-share]**.
1. Klicka på **[!UICONTROL Create]**. Ett meddelande meddelar att programmet har skapats.

   ![Meddelande om att programmet har skapats för att integrera AEM Assets med Adobe CC](assets/chlimage_1-50.png)

1. Kopiera det **[!UICONTROL Application ID]** som genereras för det nya programmet.

   >[!CAUTION]
   >
   >Se till att du inte oavsiktligt kopierar **[!UICONTROL Application Secret]** istället för **[!UICONTROL Application ID]**.

## Lägg till en ny konfiguration i Marketing Cloud {#add-a-new-configuration-to-marketing-cloud}

1. Klicka på AEM logotyp i användargränssnittet för den lokala AEM Assets-instansen och navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**.

1. Leta reda på **[!UICONTROL Adobe Marketing Cloud]** tjänsten. Om det inte finns några konfigurationer klickar du på **[!UICONTROL Configure Now]**. Om det finns konfigurationer klickar du på **[!UICONTROL Show Configurations]** och sedan på `+` för att lägga till en ny konfiguration.

   >[!NOTE]
   >
   >Använd ett Adobe ID konto som har administratörsbehörighet för organisationen.

1. I **[!UICONTROL Create Configuration]** dialogrutan anger du en rubrik och ett namn för den nya konfigurationen och klickar på **[!UICONTROL Create]**.

   ![Namnge en ny konfiguration för integrering av AEM Assets och CC](assets/chlimage_1-51.png)

1. I **[!UICONTROL Tenant URL]** fältet anger du URL:en för AEM Assets.

   >[!CAUTION]
   >
   >Om du angav klientens URL när `https://<tenant_id>.marketing.adobe.com` du måste ändra den till `https://<tenant_id>.experiencecloud.adobe.com.` För att kunna göra det följer du stegen nedan:
   >
   >1. Navigera till **Verktyg > Cloud Service > Äldre Cloud Service**.
   1. Klicka på **Visa konfigurationer** under Adobe Marketing Cloud.
   1. Välj den konfiguration som skapades när AEM-MAC-CC-synkroniseringen konfigurerades.
   1. Redigera molntjänstkonfigurationen och ersätt **marketing.adobe.com** i fältet Klientadress till **experienceCloud.adobe.com**.
   1. Spara konfigurationen.
   1. Testa replikeringsagenterna för mac-sync.


1. I **[!UICONTROL Client ID]** fältet klistrar du in det program-ID som du kopierade i slutet av proceduren [Skapa ett program](/help/sites-administering/configure-assets-cc-integration.md#create-an-application).

   ![Ange de program-ID-värden som krävs för att integrera AEM Assets och Creative Cloud](assets/cloudservices_tenant_info.png)

1. Under **[!UICONTROL Synchronization]** Markera **[!UICONTROL Enabled]** för att aktivera synkronisering och klicka på **[!UICONTROL OK]**.

   >[!NOTE]
   Om du väljer **inaktiverad** fungerar synkroniseringen i en riktning.

1. Klicka på konfigurationssidan **[!UICONTROL Display Public Key]** för att visa den offentliga nyckel som genererats för instansen. Du kan också klicka på filen **[!UICONTROL Download Public Key for OAuth Gateway]** som innehåller den offentliga nyckeln. Öppna sedan filen för att visa den offentliga nyckeln.

## Aktivera synkronisering {#enable-synchronization}

1. Visa den offentliga nyckeln med någon av följande metoder som anges i det sista steget i proceduren [Lägg till en ny konfiguration i Marketing Cloud](/help/sites-administering/configure-assets-cc-integration.md#add-a-new-configuration-to-marketing-cloud). Klicka på **[!UICONTROL Display Public Key]**.

   ![chlimage_1-52](assets/chlimage_1-52.png)

1. Kopiera den offentliga nyckeln och klistra in den i fältet **[!UICONTROL Public Key]** i konfigurationsgränssnittet för det program du skapade i [Skapa ett program](/help/sites-administering/configure-assets-cc-integration.md#create-an-application).

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. Klicka på **[!UICONTROL Update]**. Synkronisera dina resurser med AEM Assets-instansen nu.

## Testa synkroniseringen {#test-the-synchronization}

1. Klicka på AEM logotyp i användargränssnittet för den lokala AEM Assets-instansen och navigera till **[!UICONTROL Tools]**> **[!UICONTROL Deployment]**> **[!UICONTROL Replication]**för att hitta de replikeringsprofiler som har skapats för synkronisering.
1. På sidan **[!UICONTROL Replication]** klickar du på **[!UICONTROL Agents on author]**.
1. I listan med profiler klickar du på standardreplikeringsprofilen för din organisation för att öppna den.
1. Klicka på **[!UICONTROL Test Connection]** i dialogrutan.

   ![Testa anslutningen och ange organisationens standardreplikeringsprofil](assets/chlimage_1-54.png)

1. När replikeringen är klar kontrollerar du om det finns ett meddelande om att åtgärden lyckades i slutet av testresultaten.

## Lägg till användare i Marketing Cloud {#add-users-to-marketing-cloud}

1. Logga in på Marketing Cloud med administratörsautentiseringsuppgifter.
1. Från skenorna går du till **[!UICONTROL Administration]** och sedan klickar/trycker du **[!UICONTROL Launch Enterprise Dashboard]**.
1. Öppna **[!UICONTROL Users]** sidan genom **[!UICONTROL User Management]** att klicka på den.
1. Klicka/tryck på **Lägg till** ![aem_assets_add_icon](assets/aem_assets_add_icon.png)i verktygsfältet.
1. Lägg till en eller flera användare som du vill ska kunna dela resurser med Creative Cloud.

   >[!NOTE]
   Endast de användare som du lägger till i Marketing Cloud kan dela resurser från AEM Assets till Creative Cloud.

## Växla tillgångar mellan AEM Assets och Marketing Cloud {#exchange-assets-between-aem-assets-and-marketing-cloud}

1. Logga in på AEM Assets.
1. Skapa en mapp i resurskonsolen och överför några resurser till den. Du kan till exempel skapa en mapp **mc-demo** och överföra en resurs till den.
1. Markera mappen och klicka på **Dela** ![resurser_dela](assets/assets_share.png).
1. Välj **[!UICONTROL Adobe Marketing Cloud]** och klicka på menyn **[!UICONTROL Share]**. Ett meddelande meddelar att mappen delas med Marketing Cloud.

   ![chlimage_1-55](assets/chlimage_1-55.png)

   >[!NOTE]
   Delning av en resursmapp av den typen `sling:OrderedFolder`stöds inte i samband med delning i Adobe Marketing Cloud. Om du vill dela en mapp ska du inte markera **[!UICONTROL Ordered]** alternativet när du skapar den i AEM Assets.

1. Uppdatera användargränssnittet i AEM Assets. Mappen som du skapade i resurskonsolen för den lokala AEM Assets-instansen kopieras till användargränssnittet för Marketing Cloud. Resursen som du överför till mappen i AEM Assets visas i kopian av mappen i Marketing Cloud efter att den har bearbetats av AEM server.
1. Du kan också överföra en resurs i den replikerade kopian av mappen i Marketing Cloud. När resursen har bearbetats visas den i den delade mappen i AEM Assets.

## Växla tillgångar mellan AEM Assets och Creative Cloud {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
Mappdelningsfunktionen AEM till Creative Cloud är föråldrad. Kunderna rekommenderas att använda nyare funktioner, som [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) eller [AEM](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html). Läs mer om [AEM och Creative Cloud Integration Best Practices](/help/assets/aem-cc-integration-best-practices.md).

Med AEM Assets kan du dela mappar som innehåller resurser med Adobe Creative Cloud-användare.

1. I resurskonsolen väljer du den mapp som ska delas med Creative Cloud.
1. Klicka på **[!UICONTROL Share]** assets_share ![](assets/assets_share.png)i verktygsfältet.
1. Välj **[!UICONTROL Adobe Creative Cloud]** alternativet i listan.

   >[!NOTE]
   Alternativen är tillgängliga för användare med läsbehörighet för roten. Användarna måste ha behörighet att komma åt replikeringsagentinformationen för Marketing Cloud.

1. Lägg till användaren som ska dela mappen på **[!UICONTROL Creative Cloud Sharing]** sidan och välj en roll för användaren. Klicka **[!UICONTROL Save]** och klicka **[!UICONTROL OK]**.

1. Logga in på Creative Cloud med inloggningsuppgifterna för den användare som du delade mappen med. Den delade mappen är tillgänglig i Creative Cloud.

Synkroniseringen mellan AEM Assets och Marketing Cloud är utformad så att användardatorinstansen som resursen överförs från behåller rätten att ändra resursen. Endast dessa ändringar sprids till den andra instansen.

Om till exempel en resurs överförs från en AEM Assets-instans (lokal), sprids ändringarna av resursen från den här instansen till instansen Marketing Cloud. Ändringar som görs från Marketing Cloud-instansen till samma resurs sprids dock inte till AEM och vice versa för resurser som överförs från Marketing Cloud.

>[!MORELIKETHIS]
* [Bästa praxis för integrering av AEM och Creative Cloud](/help/assets/aem-cc-integration-best-practices.md)
* [Metodtips för att dela AEM till Creative Cloud](/help/assets/aem-cc-folder-sharing-best-practices.md)

