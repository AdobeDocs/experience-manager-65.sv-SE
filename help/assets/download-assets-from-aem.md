---
title: Hämta resurser
description: Lär dig hur du hämtar resurser från [!DNL Adobe Experience Manager] och aktivera eller inaktivera nedladdningsfunktionen.
contentOwner: AG
role: User
feature: Asset Management,Asset Distribution
exl-id: 6bda9e52-5a6e-446e-99c7-96793482c190
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Hämta resurser från [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/download-assets-from-aem.html?lang=en) |
| AEM 6.5 | Den här artikeln |

Du kan hämta resurser, inklusive statiska och dynamiska återgivningar. Du kan även skicka e-postmeddelanden med länkar till resurser direkt från [!DNL Adobe Experience Manager Assets]. Hämtade resurser paketeras i en ZIP-fil. Den komprimerade ZIP-filen har en maximal filstorlek på 1 GB för exportjobbet. Högst 500 resurser per exportjobb tillåts.

>[!NOTE]
>
>Alla användare som har läsbehörighet på `/var/dam/share` platsen kan komma åt den nedladdningslänk som delas i e-postmeddelandet.
>
>Alla användare som har läsbehörighet till `/var/dam/jobs/download` plats kan hämta resurser.
>
>Det går inte att hämta resurstyperna - Bilduppsättningar, Snurra uppsättningar, Blandade medieuppsättningar och Carousel-uppsättningar.

<!--
OLD content of the above NOTE, changed wrt CQDOC-18661.
>The email recipients must be members of the `dam-users` group to access the ZIP download link in the email message.
>
-->

**Så här hämtar du resurser:**

1. Klicka på logotypen i det övre vänstra hörnet. Klicka på **[!UICONTROL Navigation]**.
1. På [!UICONTROL Navigation] sida, klicka **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Navigera till en mapp som innehåller resurser som du vill hämta.
1. Markera mappen eller välj en eller flera resurser i mappen.
1. I verktygsfältet klickar du på **[!UICONTROL Download]**.
1. I dialogrutan Hämta väljer du de hämtningsalternativ som du vill använda.

   | Alternativet Exportera eller ladda ned | Beskrivning |
   |---|---|
   | **[!UICONTROL Create separate folder for each asset]** | Välj det här alternativet om du vill inkludera varje resurs som du hämtar, inklusive resurser, i underordnade mappar som är kapslade under resursens överordnade mapp i en mapp på den lokala datorn. När det här alternativet inte är markerat ignoreras mapphierarkin som standard och alla resurser hämtas till en mapp på den lokala datorn. |
   | **[!UICONTROL Email]** | Ett e-postmeddelande skickas till användaren. Standardmallar för e-post finns på följande platser:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Mallar som du anpassar under distributionen finns på följande platser: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Du kan lagra klientspecifika anpassade mallar på följande platser:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Asset(s)]** | Välj det här alternativet om du vill hämta resursen i dess ursprungliga form utan några återgivningar.<br>Alternativet för deltillgångar är tillgängligt om den ursprungliga tillgången har deltillgångar. |
   | **[!UICONTROL Rendition(s)]** | En återgivning är den binära representationen av en resurs. Resurser har en primär representation - den som utgörs av den överförda filen. De kan ha ett valfritt antal representationer. <br> Med det här alternativet kan du välja de återgivningar du vill hämta. Vilka återgivningar som är tillgängliga beror på vilken resurs du väljer. Alternativet är tillgängligt om resursen har några återgivningar. |
   | **[!UICONTROL Smart Crops]** | Välj det här alternativet om du vill hämta alla smarta beskärningsåtergivningar för den valda resursen från AEM. En ZIP-fil med renderingarna Smart Crop skapas och hämtas till din lokala dator. |
   | **[!UICONTROL Dynamic Rendition(s)]** | Välj det här alternativet om du vill generera en serie alternativa återgivningar i realtid. När du väljer det här alternativet väljer du också de återgivningar som du vill skapa dynamiskt genom att välja bland [Bildförinställning](image-presets.md) lista. <br>Du kan dessutom välja storlek och måttenhet, format, färgrymd, upplösning och alla valfria bildmodifierare, t.ex. invertering av bilden. Alternativet är bara tillgängligt om du har [!DNL Dynamic Media] aktiverat. |

1. Klicka på **[!UICONTROL Download]**.

När du väljer en mapp att hämta hämtas hela resurshierarkin under mappen. Om du vill inkludera alla resurser som du hämtar (inklusive resurser i underordnade mappar som är kapslade under den överordnade mappen) i en enskild mapp väljer du **[!UICONTROL Create separate folder for each asset]**.

## Aktivera resurshämtningsserver {#enable-asset-download-servlet}

Standardservleten i [!DNL Experience Manager] gör att autentiserade användare kan skicka godtyckligt stora, samtidiga hämtningsbegäranden för att skapa ZIP-filer med resurser som är synliga för dem och som kan överbelasta servern och nätverket. För att minska de potentiella DoS-riskerna som den här funktionen medför `AssetDownloadServlet` OSGi-komponenten är inaktiverad som standard för publiceringsinstanser.

Om du vill tillåta hämtning av resurser från DAM, till exempel när du använder Assets Share Commons eller någon annan portalliknande implementering, aktiverar du servleten manuellt med hjälp av en OSGi-konfiguration. Adobe rekommenderar att du anger en så låg hämtningsstorlek som möjligt utan att det påverkar den dagliga hämtningen. Ett högt värde kan påverka prestandan.

1. Skapa en mapp med en namnkonvention som anger publiceringskörningsläget som mål (`config.publish`): `/apps/<your-app-name>/config.publish`. Information om hur du definierar konfigurationsegenskaper för ett körningsläge finns i [Körningslägen](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).
1. Skapa en fil av typen i konfigurationsmappen `nt:file` namngiven `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Fylla `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` med följande. Anger en maximal storlek (i byte) för hämtningen som värdet av `asset.download.prezip.maxcontentsize`. Nedanstående exempel konfigurerar den maximala storleken för ZIP-nedladdningen till högst 100 kB.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

Som standard är `GET` förfrågningar om att ladda ned filer, [!DNL Experience Manager] begränsar ZIP-arkivets hämtningsstorlek till 50 MB. Nedladdningar som initierats via `POST` begäranden eller användargränssnittet påverkas inte av den här gränsen.

## Inaktivera resurshämtningsserver {#disable-asset-download-servlet}

The `Asset Download Servlet` kan inaktiveras på en [!DNL Experience Manager] Publicera instanser genom att uppdatera dispatcherns konfiguration för att blockera alla förfrågningar om hämtning av resurser. Servern kan även inaktiveras manuellt via OSGi-konsolen direkt.

1. Om du vill blockera resurshämtningsbegäranden via en dispatcher-konfiguration redigerar du `dispatcher.any` konfigurera och lägga till en regel i [filtersektion](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter). `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Om du vill inaktivera OSGi-komponenten på en Publish-instans öppnar du OSGi-konsolen på `http://[aem_server]:[port]/system/console/components`. Sök `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` och klicka **[!UICONTROL Disable]**.

>[!MORELIKETHIS]
>
>* [Hämta resurser med Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)
>* [Hämta DRM-skyddade resurser](drm.md).
>* [Hämta resurser med datorprogrammet Experience Manager på Win eller Mac](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets).
>* [Hämta resurser med Adobe Assets Link inifrån de Adobe Creative Cloud-appar som stöds](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html).
