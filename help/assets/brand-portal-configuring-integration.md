---
title: Konfigurera AEM Assets-integrering med varumärkesportalen
seo-title: Konfigurera AEM Assets-integrering med varumärkesportalen
description: Lär dig hur du integrerar AEM Assets med varumärkesportalen för publicering av resurser och samlingar på varumärkesportalen.
seo-description: Lär dig hur du integrerar AEM Assets med varumärkesportalen för publicering av resurser och samlingar på varumärkesportalen.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: 9c73abc3291f2847c705cb649d2993fb186b0993

---


# Konfigurera AEM Assets-integrering med varumärkesportalen {#configure-aem-assets-integration-with-brand-portal}

Om du är kund hos Adobe Experience Manager (AEM) Assets Brand Portal kan du integrera AEM Assets med varumärkesportalen för att möjliggöra publicering av resurser på varumärkesportalen. Du kan konfigurera den här integreringen med gränssnittet i Adobe.io.

Skapa först ett program, som innehåller en autentiseringsmekanism, i den offentliga gatewayen för Marketing Cloud. Skapa sedan en profil i din AEM Resurser-instans med det program-ID som du får från gatewayen.

Använd den här konfigurationen för att publicera resurser från AEM Assets till varumärkesportalen. I bakgrunden autentiserar AEM-servern din profil med gatewayen och integrerar sedan AEM Assets med Brand Portal.

>[!NOTE]
>
>Användargränssnittet för konfigurering av autentiseringsintegreringar finns i [https://legacy-oauth.cloud.adobe.io/](https://legacy-oauth.cloud.adobe.io/), som tidigare fanns på [https://marketing.adobe.com/developer/](https://marketing.adobe.com/developer/).

## Skapa JWT-program {#create-jwt-application}

1. Logga in på [https://legacy-oauth.cloud.adobe.io/](https://legacy-oauth.cloud.adobe.io/) med ditt Adobe ID. **Sidan JWT-program** öppnas.

   >[!NOTE]
   >
   >Du kan bara skapa ett program-ID om du är systemadministratör för din organisation. Klientorganisationen är det tekniska namnet för din organisation som är registrerad hos Adobe Marketing Cloud.

1. Välj **[!UICONTROL Lägg till program]** för att skapa ett program.
1. Ange ett namn för programmet och en valfri beskrivning.
1. I listan **[!UICONTROL Organisation]** väljer du den organisation som du vill synkronisera resurser för.
1. Välj **[!UICONTROL dam-read]** , **[!UICONTROL dam-sync]**, **[!UICONTROL dam-write]** och **[!UICONTROL cc-share]** i listan **[!UICONTROL Scope]**.
1. Click **[!UICONTROL Add]**. Ett JWT-tjänstprogram skapas. Du kan redigera programmet och sedan spara.
1. Kopiera det program-ID som genereras för det nya programmet.

   >[!NOTE]
   >
   >Se till att du inte oavsiktligt kopierar programhemligheten i stället för program-ID.

## Skapa en ny molnkonfiguration {#create-a-new-cloud-configuration}

1. På **[!UICONTROL navigeringssidan]** i den lokala AEM Resurser-instansen klickar du på ikonen **[!UICONTROL Verktyg]** till vänster.

1. Gå till **[!UICONTROL molntjänster]>[!UICONTROL Äldre molntjänster]**.

   ![AEM Tools](assets/aem-tools.png)

1. I **[!UICONTROL molntjänster]** kan du hitta tjänsten **[!UICONTROL Assets Brand Portal]** i **[!UICONTROL Adobe Experience Cloud]**.

   ![Adobe Experience Cloud Services](assets/experience-cloud-services.png)

1. Klicka på länken **[!UICONTROL Konfigurera nu]** under tjänsten för att visa dialogrutan **[!UICONTROL Skapa konfiguration]** .
1. I dialogrutan **[!UICONTROL Skapa konfiguration]** anger du en rubrik och ett namn för den nya konfigurationen och klickar på **[!UICONTROL Skapa]**.

   ![bp-config](assets/bp-config.png)

1. I dialogrutan **[!UICONTROL AEM Assets Brand Portal Replication]** anger du organisationens URL i fältet **[!UICONTROL Klient-URL]** .
1. I fältet **[!UICONTROL Klient-ID]** klistrar du in det program-ID som du kopierade i slutet av proceduren [Skapa ett program](/help/assets/brand-portal-configuring-integration.md#create-jwt-application). Välj **[!UICONTROL OK]**.

   ![public-folder-publish](assets/public-folder-publish.png)

1. Om du vill göra resurserna (publicerade från AEM) tillgängliga för alla användare av varumärkesportalen markerar du kryssrutan Publicera i **[!UICONTROL gemensam mapp]** .

   >[!NOTE]
   >
   >Alternativet att aktivera publicering av **[!UICONTROL gemensamma mappar]** är tillgängligt i AEM 6.3.2.1 och senare.

1. På sidan Konfiguration **[!UICONTROL av]** varumärkesportal klickar du på **[!UICONTROL Visa offentlig nyckel]** för att visa den offentliga nyckel som genererats för instansen.

   ![display-public-key](assets/display-public-key.png)

   Du kan också klicka på **[!UICONTROL Hämta offentlig nyckel för OAuth Gateway]** för att hämta filen som innehåller den offentliga nyckeln. Öppna sedan filen för att visa den offentliga nyckeln.

## Aktivera integrering {#enable-integration}

1. Visa den offentliga nyckeln med någon av följande metoder som nämns i det sista steget i proceduren [Lägg till en ny konfiguration i Marketing Cloud](/help/assets/brand-portal-configuring-integration.md#create-a-new-cloud-configuration).

   * Klicka på knappen **[!UICONTROL Visa offentlig nyckel]** för att visa nyckeln.
   * Öppna den hämtade filen som innehåller nyckeln.

1. Öppna gränssnittet för Marketing Cloud Developer Connection och klicka på det program du skapade i [Skapa ett program](/help/assets/brand-portal-configuring-integration.md#create-jwt-application).
1. Klistra in den offentliga nyckeln i fältet **[!UICONTROL Offentlig nyckel]** i konfigurationsgränssnittet
1. Click **[!UICONTROL Save]**. Ett meddelande bekräftar att programmet har uppdaterats.

## Testa integreringen {#test-the-integration}

1. På **[!UICONTROL navigeringssidan]** i den lokala AEM Resurser-instansen klickar du på ikonen **[!UICONTROL Verktyg]** till vänster.

1. Navigera till **[!UICONTROL Distribution]** > **[!UICONTROL Replikering]**.

   ![distribumentreplikering](assets/deploymentreplication.png)

1. På sidan **[!UICONTROL Replikering]** klickar du på **[!UICONTROL Agenter på författaren]**.

   ![agent_on_author](assets/agents_on_author.png)

1. Kontrollera anslutningen mellan AEM Author och Brand Portal genom att öppna någon av de fyra replikeringsagenterna och klicka på **[!UICONTROL Testa anslutning]**.

   >[!NOTE]
   >
   >Replikeringsagenterna arbetar parallellt och delar jobbdistributionen jämnt, vilket ökar publiceringshastigheten fyra gånger den ursprungliga hastigheten. När molntjänsten har konfigurerats krävs ingen ytterligare konfiguration för att aktivera de replikeringsagenter som aktiveras som standard för att aktivera parallell publicering av flera resurser.

   >[!NOTE]
   >
   >Undvik att inaktivera någon av replikeringsagenterna eftersom det kan göra att replikeringen av vissa resurser misslyckas.

   ![aem_assets_parallelpublishing](assets/aem_assets_parallelpublishing.png)

1. Titta på testresultatens nedre del för att kontrollera att replikeringen lyckades.

   ![replication_completed](assets/replication_succeeded.png)

När replikeringen är klar kan du publicera resurser, mappar och samlingar på varumärkesportalen. Mer information finns i:

* [Publicera resurser och mappar på varumärkesportalen](/help/assets/brand-portal-publish-folder.md)
* [Publicera samlingar på varumärkesportalen](/help/assets/brand-portal-publish-collection.md)

## Publicera resurser på varumärkesportalen {#publish-assets-to-brand-portal}

När replikeringen är klar kan du publicera resurser, mappar och samlingar på varumärkesportalen. Så här publicerar du resurser på varumärkesportalen:

>[!NOTE]
>
>Adobe rekommenderar att publiceringen staggats, helst under icke-topp-timmar, så att AEM-författaren inte tar upp för mycket resurser.

1. I resurskonsolen markerar du de resurser/mappar som du vill publicera och klickar på **[!UICONTROL Snabbpublicering]** i verktygsfältet.

   Du kan också välja de resurser du vill publicera på varumärkesportalen.

   ![publish2bp-2](assets/publish2bp.png)

1. Det finns två tillgängliga alternativ för att publicera resurserna på varumärkesportalen:
   * [Publicera resurser direkt](#publish-to-bp-now)
   * [Publicera resurser senare](#publish-to-bp-now)

### Publicera resurser nu {#publish-to-bp-now}

Gör något av följande om du vill publicera de markerade resurserna på varumärkesportalen:

* Välj **[!UICONTROL Snabbpublicering]** i verktygsfältet. Välj sedan **[!UICONTROL Publicera på varumärkesportalen]** på menyn.

* Välj **[!UICONTROL Hantera publikation]** i verktygsfältet.

   1. Välj sedan **[!UICONTROL Publicera på varumärkesportal]** i **[!UICONTROL Åtgärd]** och välj **[!UICONTROL Now]** i **[!UICONTROL Scheduling]**. Click **[!UICONTROL Next]**.

   2. Bekräfta ditt val inom **[!UICONTROL Omfattning]** och klicka på **[!UICONTROL Publicera på varumärkesportalen]**.

Ett meddelande visas som anger att resurserna har placerats i kö för publicering på varumärkesportalen. Logga in på gränssnittet för varumärkesportalen för att se de publicerade resurserna.

### Publicera resurser senare {#publish-to-bp-later}

Så här schemalägger du publicering av resurser på varumärkesportalen till ett senare datum eller en senare tidpunkt:

1. När du har valt resurser/mappar att publicera väljer du **[!UICONTROL Hantera publikation]** i verktygsfältet högst upp.

1. På sidan **[!UICONTROL Hantera publikation]** väljer du **[!UICONTROL Publicera på varumärkesportal]** från **[!UICONTROL åtgärd]** och väljer **[!UICONTROL Senare]** från **[!UICONTROL Schemaläggning]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Välj ett **[!UICONTROL aktiveringsdatum]** och ange tid. Click **[!UICONTROL Next]**.

1. Välj ett **aktiveringsdatum** och ange tid. Click **Next**.

1. Ange en **[!UICONTROL arbetsflödesrubrik]** i **[!UICONTROL arbetsflöden]**. Klicka på **[!UICONTROL Publicera senare]**.

   ![publicerat arbetsflöde](assets/publishworkflow.png)

Logga sedan in på Brand Portal för att se om de publicerade resurserna finns tillgängliga i gränssnittet för varumärkesportalen.

![bp_landing_page](assets/bp_landing_page.png)
