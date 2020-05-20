---
title: Hämta digitala resurser från [!DNL Adobe Experience Manager].
description: Lär dig hur du hämtar resurser från [!DNL Adobe Experience Manager] och aktiverar eller inaktiverar hämtningsfunktionen.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---


# Download assets from [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Du kan hämta resurser, inklusive statiska och dynamiska återgivningar. Du kan också skicka e-postmeddelanden med länkar till resurser direkt från [!DNL Adobe Experience Manager Assets]. Hämtade resurser paketeras i en ZIP-fil. Den komprimerade ZIP-filen har en maximal filstorlek på 1 GB för exportjobbet. Högst 500 resurser per exportjobb tillåts.

>[!NOTE]
>
>Mottagare av e-postmeddelanden måste vara medlemmar i gruppen för att få åtkomst till länken för ZIP-hämtning i e-postmeddelandet. `dam-users` För att kunna hämta resurserna måste medlemmarna ha behörighet att starta arbetsflöden som utlöser hämtning av resurser.

Om du vill hämta resurser går du till en resurs, markerar resursen och klickar på **[!UICONTROL Download]** i verktygsfältet. I den dialogruta som visas anger du dina hämtningsalternativ.

Det går inte att hämta resurstyperna Bilduppsättningar, Snurra uppsättningar, Blandade medieuppsättningar och Carousel-uppsättningar.

![Tillgängliga alternativ vid hämtning av resurser från Experience Manager Assets](assets/asset_download_dialog.png)

*Bild: Tillgängliga alternativ när du hämtar resurser från[!DNL Experience Manager Assets].*

Följande är de tillgängliga export- och nedladdningsalternativen. Dynamiska renderingar är unika för [!DNL Dynamic Media] erbjudandet. Med det här alternativet kan du generera nya återgivningar i realtid, utöver den resurs du valt. Alternativet är bara tillgängligt om du har [!DNL Dynamic Media] aktiverat.

| Export- eller nedladdningsalternativ | Beskrivningar |
|---|---|
| [!UICONTROL Assets] | Välj alternativet om du vill hämta resursen i dess ursprungliga format utan några återgivningar. |
| [!UICONTROL Renditions] | En återgivning är den binära representationen av en resurs. Resurser har en primär representation - den som utgörs av den överförda filen. De kan ha valfritt antal representationer. <br> Med det här alternativet kan du välja de återgivningar du vill hämta. Vilka renderingar som är tillgängliga beror på vilken resurs du väljer. |
| [!UICONTROL Dynamic Renditions] | En dynamisk återgivning genererar andra återgivningar i realtid. När du väljer det här alternativet väljer du också de återgivningar som du vill skapa dynamiskt genom att välja i listan [Bildförinställning](image-presets.md) . <br>Du kan dessutom välja storlek och måttenhet, format, färgrymd, upplösning och alla bildmodifierare (t.ex. för att invertera bilden) |
| [!UICONTROL Email] | Ett e-postmeddelande skickas till användaren. Standardmallar för e-post finns på följande platser:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Mallar som du anpassar under distributionen bör finnas på följande platser: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Du kan lagra klientspecifika anpassade mallar på följande platser:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
| [!UICONTROL Create separate folder for each asset] | Välj alternativet att bevara mapphierarkin när resurser hämtas. Som standard ignoreras mapphierarkin och alla resurser hämtas i en mapp i det lokala filsystemet. |

Alternativet Återgivningar är tillgängligt om resursen har några återgivningar. Alternativet Delresurser är tillgängligt om den ursprungliga tillgången har delresurser.

När du väljer en mapp att hämta hämtas hela resurshierarkin under mappen. Om du vill inkludera varje resurs som du hämtar (inklusive resurser i underordnade mappar som är kapslade under den överordnade mappen) i en enskild mapp väljer du **[!UICONTROL Create separate folder for each asset]**.

## Aktivera resurshämtningsserver {#enable-asset-download-servlet}

Med standardservleten i [!DNL Experience Manager] kan autentiserade användare godtyckligt skicka stora, samtidiga hämtningsbegäranden för att skapa ZIP-filer med resurser som är synliga för dem och som kan överbelasta servern och nätverket. För att minska de potentiella DoS-riskerna som orsakas av den här funktionen är `AssetDownloadServlet` OSGi-komponenten inaktiverad som standard för publiceringsinstanser.

Om du vill tillåta hämtning av resurser från DAM, till exempel när du använder Assets Share Commons eller någon annan portalliknande implementering, aktiverar du servleten manuellt via en OSGi-konfiguration. Adobe rekommenderar att du anger en så låg hämtningsstorlek som möjligt utan att det påverkar kraven för den dagliga hämtningen. Ett högt värde kan påverka prestandan.

1. Skapa en mapp med en namnkonvention som anger publiceringsmiljön som mål (`config.publish`): `/apps/<your-app-name>/config.publish`. Mer information om hur du definierar konfigurationsegenskaper för ett körningsläge finns i [Körningslägen](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).

1. Skapa en fil av typen `nt:file` med namnet i konfigurationsmappen `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Fyll `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` med följande: Anger en maximal storlek (i byte) för hämtningen som värdet för `asset.download.prezip.maxcontentsize`. Nedanstående exempel konfigurerar den maximala storleken för ZIP-nedladdningen till högst 100 kB.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Inaktivera resurshämtningsserver {#disable-asset-download-servlet}

Du `Asset Download Servlet` kan inaktivera funktionen på en [!DNL Experience Manager] publiceringsinstans genom att uppdatera dispatcherns konfiguration för att blockera eventuella hämtningsbegäranden. Servern kan även inaktiveras manuellt via OSGi-konsolen direkt.

1. Om du vill blockera resurshämtningsbegäranden via en dispatcherkonfiguration redigerar du `dispatcher.any` konfigurationen och lägger till en regel i [filteravsnittet](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter). `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Inaktivera OSGi-komponenten på en Publish-instans genom att navigera till OSGi-konsolen på `http://[aem_server]:[port]/system/console/components`. Leta reda på `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` och klicka **[!UICONTROL Disable]**.

>[!MORELIKETHIS]
>
>* [Hämta DRM-skyddade resurser](drm.md).
>* [Hämta resurser med Experience Manager-datorprogrammet på Win- eller Mac-datorer](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html).
>* [Hämta resurser med Adobe Assets Link inifrån de Adobe Creative Cloud-program](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html)som stöds.

