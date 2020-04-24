---
title: Använd anslutna resurser för att dela DAM-resurser i redigeringsarbetsflödet för [!DNL Adobe Experience Manager Sites].
description: Använd resurser som är tillgängliga på en [!DNL Adobe Experience Manager Assets]-fjärrdistribution när du skapar webbsidor på en annan Experience Manager-webbplatsdistribution.
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# Använd Connected Assets när du vill dela DAM-resurser i [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

I stora företag kan den infrastruktur som krävs för att skapa webbplatser vara distribuerad. Ibland kan funktionerna för att skapa webbplatser och de digitala resurser som används för att skapa webbplatserna finnas i olika distributioner. Det kan bero på geografiskt spridda befintliga distributioner som måste fungera tillsammans eller förvärv som har lett till en heterogen infrastruktur som moderbolaget vill använda tillsammans.

[!DNL Adobe Experience Manager Sites] erbjuder funktioner för att skapa webbsidor och är det DAM-system (Digital Asset Management) som tillhandahåller de resurser som krävs för webbplatserna. [!DNL Adobe Experience Manager Assets] [!DNL Experience Manager] har nu stöd för ovanstående användningsexempel genom integrering [!DNL Experience Manager Sites] och [!DNL Experience Manager Assets].

## Översikt över Connected Assets {#overview-of-connected-assets}

When editing pages in Page Editor, the authors can seamlessly search, browse, and embed assets from a different [!DNL Experience Manager Assets] deployment. To do an [!DNL Experience Manager] administrator do a one-time integration of a local deployment of [!DNL Experience Manager Sites] with a different (remote) deployment of [!DNL Experience Manager Assets].

For the [!DNL Sites] authors, the remote assets are available as read-only local assets. Funktionen stöder enkel sökning och användning av ett fåtal fjärresurser i taget. Om du vill göra många fjärresurser tillgängliga för lokal distribution på en gång bör du överväga att migrera resurserna samtidigt. See [Experience Manager Assets migration guide](/help/assets/assets-migration-guide.md).

### Förutsättningar och distributioner som stöds {#prerequisites}

Innan du använder eller konfigurerar den här funktionen bör du kontrollera följande:

* Användarna ingår i lämpliga användargrupper för varje distribution.
* Ett av de kriterier som stöds för Adobe Experience Manager-distributionstyper är uppfyllt. [!DNL Experience Manager] 6.5 [!DNL Assets] works with [!DNL Experience Manager] as a Cloud Service. For more information, see [Connected Assets functionality in Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Experience Manager Sites] as a Cloud Service | Experience Manager 6.5 [!DNL Sites] on AMS | Experience Manager 6.5 [!DNL Sites] on-premise |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]som molntjänst ** | Stöds | Stöds | Stöds |
   | **Experience Manager 6.5[!DNL Assets]on AMS** | Stöds | Stöds | Stöds |
   | **Experience Manager 6.5[!DNL Assets]on-premise** | Stöds ej | Stöds ej | Stöds ej |

### Filformat som stöds {#mimetypes}

Författare kan söka efter bilder och följande typer av dokument i Content Finder och använda resurserna i Page Editor. Dokument kan läggas till i `Download`-komponenten och bilder kan läggas till i `Image`-komponenten. Authors can also add the remote assets in any custom Experience Manager component that extends the default `Download` or `Image` components. Listan över format som stöds är:

* **Bildformat**: De bildformat som stöds av [Image-komponenten](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/image.html) stöds av Anslutna resurser. [!DNL Dynamic Media] images are not supported.
* **Dokumentformat**: Se [Dokumentformat som stöds i Connected Assets](assets-formats.md#supported-document-formats).

### Användare och grupper som krävs {#users-and-groups-involved}

De olika roller som krävs för att konfigurera och använda funktionen och motsvarande användargrupper beskrivs nedan. Lokalt omfång används för de fall då en webbsida skapas av en författare. Fjärromfång används för DAM-distributionen som är värd för de nödvändiga resurserna. The [!DNL Sites] author fetches these remote assets.

| Roll | Omfång | Användargrupp | Användarnamn i genomgång | Krav |
|---|---|---|---|---|
| [!DNL Sites] administrator | Lokalt | Experience Manager administrator | `admin` | Set up Experience Manager, configure integration with the remote [!DNL Assets] deployment. |
| DAM-användare | Lokalt | Författare | `ksaner` | Används för att visa och duplicera de hämtade resurserna i `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Lokalt | Author (with read access on the remote DAM and author access on local [!DNL Sites]) | `ksaner` | End user are [!DNL Sites] authors who use this integration to improve their content velocity. Författarna söker efter och bläddrar bland resurser i fjärrversionen av DAM med hjälp av Content Finder och använder de bilder som behövs på lokala webbsidor. Autentiseringsuppgifterna för `ksaner` DAM-användaren används. |
| [!DNL Assets] administrator | Fjärr | Experience Manager Administrator | `admin` on remote Experience Manager | Konfigurerar CORS (Cross-Origin Resource Sharing). |
| DAM-användare | Fjärr | Författare | `ksaner` on remote Experience Manager | Skapa roll för fjärrdistributionen av Experience Manager. Söker efter och bläddrar bland resurser i Connected Assets med hjälp av Content Finder. |
| DAM-distributör (teknisk användare) | Fjärr | paketbyggare och webbplatsförfattare | `ksaner` on remote Experience Manager | This user present on the remote deployment is used by Experience Manager local server (not the Site author role) to fetch the remote assets, on behalf of [!DNL Sites] author. Den här rollen är inte densamma som de två `ksaner`-rollerna ovan och den tillhör en annan användargrupp. |

## Configure a connection between [!DNL Sites] and [!DNL Assets] deployments {#configure-a-connection-between-sites-and-assets-deployments}

En Experience Manager-administratör kan skapa den här integreringen. Once created, the permissions required to use it are established via user groups that are defined on the [!DNL Sites] deployment and on the DAM deployment.

To configure Connected Assets and local [!DNL Sites] connectivity, follow these steps.

1. Access an existing [!DNL Experience Manager Sites] deployment or create a deployment using the following command:

   1. Kör följande kommando på en terminal i JAR-filens mapp för att skapa varje Experience Manager-server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Efter några minuter startas Experience Manager-servern. Consider this [!DNL Experience Manager Sites] deployment as the local machine for web page authoring, say at `https://[local_sites]:4502`.

1. Ensure that the users and roles with local scope exist on the Experience Manager Sites deployment and on the [!DNL Experience Manager Assets] deployment on AMS. Create a technical user on [!DNL Assets] deployment and add to the user group mentioned in [users and groups involved](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Access the local [!DNL Experience Manager Sites] deployment at `https://[local_sites]:4502`. Click **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Connected Assets Configuration]** and provide the following values:

   1. [!DNL Experience Manager Assets] location is `https://[assets_servername_ams]:[port]`.
   1. Autentiseringsuppgifter för en DAM-distributör (teknisk användare).
   1. In **[!UICONTROL Mount Point]** field, enter the local Experience Manager path where Experience Manager fetches the assets. Till exempel, mappen `remoteassets`.
   1. Adjust the values of **[!UICONTROL Original Binary transfer optimization Threshold]** depending on your network. En resursåtergivning med en storlek som är större än detta tröskelvärde överförs asynkront.
   1. Select **[!UICONTROL Datastore Shared with Connected Assets]**, if you use a datastore to store your assets and the Datastore is the common storage between both Experience Manager deployments. I det här fallet spelar tröskelvärdet ingen roll eftersom resursernas binärfiler finns i datalagret och de inte överförs.
      ![En typisk konfiguration för Connected Assets](assets/connected-assets-typical-config.png)
   *Bild: En typisk konfiguration för Connected Assets.*

1. Inaktivera arbetsflödets startprogram eftersom resurserna redan har bearbetats och återgivningarna hämtas. Adjust the launcher configurations on the local ([!DNL Experience Manager Sites]) deployment to exclude the `connectedassets` folder, in which the remote assets are fetched.

   1. On [!DNL Experience Manager Sites] deployment, click **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.

   1. Search for Launchers with workflows as **[!UICONTROL DAM Update Asset]** and **[!UICONTROL DAM Metadata Writeback]**.

   1. Select the workflow launcher and click **[!UICONTROL Properties]** on the action bar.

   1. In the Properties wizard, change the **[!UICONTROL Path]** fields as the following mappings to update their regular expressions to exclude the mount point **[!UICONTROL connectedassets]**.
   | Före | Efter |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Alla återgivningar som är tillgängliga på Experience Manager-fjärrdistributionen hämtas när författare hämtar en resurs. Om du vill skapa fler återgivningar av en hämtad resurs hoppar du över det här konfigurationssteget. The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. Add the [!DNL Experience Manager Sites] instance as one of the **[!UICONTROL Allowed Origins]** on the remote [!DNL Experience Manager Assets] CORS configuration.

   1. Logga in med administratörsuppgifterna. Search for `Cross-Origin`. Access **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

   1. Om du till [!DNL Experience Manager Sites] exempel vill skapa en CORS-konfiguration klickar du på ![ikonen aem_assets_add_icon](assets/aem_assets_add_icon.png) bredvid **[!UICONTROL Adobe Granite-resursdelningspolicy]** för korsursprung.

   1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local [!DNL Sites], that is, `https://[local_sites]:[port]`. Spara konfigurationen.

## Använda fjärresurser {#use-remote-assets}

Webbplatsförfattare använder Content Finder för att ansluta till DAM-instansen. Författarna kan bläddra bland, söka efter och dra fjärresurserna till en komponent. Om du vill autentisera med DAM-fjärrdistributionen bör du ha DAM-användarens autentiseringsuppgifter som du fått av administratören till hands.

Författare kan använda resurserna som finns på både den lokala DAM-instansen och fjärrinstansen av DAM på samma webbsida. Använd Content Finder för att växla mellan att söka i det lokala DAM-systemet eller söka i det fjärranslutna DAM-systemet.

Only those tags of remote assets are fetched that have an exact corresponding tag along with the same taxonomy hierarchy, available on the local [!DNL Sites] instance. Alla andra taggar tas bort. Författare kan söka efter fjärrresurser med hjälp av alla taggar som finns i Experience Manager-fjärrdistributionen, eftersom Experience Manager erbjuder en fulltextsökning.

### Genomgång av användningen {#walk-through-of-usage}

Använd konfigurationen ovan när du vill prova redigeringsfunktionen och se hur den fungerar. Använd de dokument eller bilder du vill ha på den fjärranslutna DAM-distributionen.

1. Navigate to the [!DNL Assets] user interface on the remote deployment by accessing **[!UICONTROL Assets]** > **[!UICONTROL Files]** from [!DNL Experience Manager] workspace. Du kan även få åtkomst till `https://[assets_servername_ams]:[port]/assets.html/content/dam` i en webbläsare. Ladda upp de resurser du vill ha.
1. On the [!DNL Sites] instance, in the profile activator in the upper-right corner, click **[!UICONTROL Impersonate as]**. Provide `ksaner` as user name, select the option provided, and click **[!UICONTROL OK]**.
1. Open a We.Retail website page at **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Redigera sidan. Du kan även öppna `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` i en webbläsare när du vill redigera en sida.

   Click **[!UICONTROL Toggle Side Panel]** on upper-left corner of the page.

1. Open the [!UICONTROL Assets] tab and click **[!UICONTROL Log in to Connected Assets]**.
1. Ange inloggningsuppgifterna, `ksaner` som användarnamn och `password` som lösenord. This user has authoring permissions on both the [!DNL Experience Manager] deployments.
1. Sök efter resursen som du har lagt till i DAM. Fjärresurserna visas i den vänstra panelen. Filtrera efter bilder eller dokument och filtrera efter olika typer av dokument som stöds. Dra bilderna till en `Image`-komponent och dokument till en `Download`-komponent.

   The fetched assets are read-only on the local [!DNL Experience Manager Sites] deployment. You can still use the options provided by your [!DNL Experience Manager Sites] components to edit the fetched asset. Redigering med komponenter är icke-destruktiv.

   ![Alternativ för att filtrera dokumenttyper och bilder vid sökning efter resurser på DAM-fjärrdistribution](assets/filetypes_filter_connected_assets.png)

   *Bild: Alternativ för att filtrera dokumenttyper och bilder vid sökning efter resurser på DAM-fjärrdistribution.*

1. En Sites-författare meddelas om en resurs hämtas asynkront och om en hämtningsåtgärd misslyckas. Under eller efter redigeringen kan författare se detaljerad information om hämtningsåtgärder och fel i användargränssnittet för [asynkrona jobb](/help/assets/asynchronous-jobs.md).

   ![Meddelande om asynkron hämtning av resurser som sker i bakgrunden.](assets/assets_async_transfer_fails.png)

   *Bild: Meddelande om asynkron hämtning av resurser som sker i bakgrunden.*

1. When publishing a page, [!DNL Experience Manager] displays a complete list of assets that are used in the page. Kontrollera att fjärresurserna har hämtats vid publiceringen. Se [användargränssnittet för asynkrona jobb](/help/assets/asynchronous-jobs.md) om du vill kontrollera status för varje hämtad resurs.

   >[!NOTE]
   >
   >Sidan publiceras även om en eller flera fjärresurser inte hämtats. Komponenten som använder fjärresursen publiceras tom. The [!DNL Experience Manager] notification area displays notification for errors that show in async jobs page.

>[!CAUTION]
>
>När de hämtade fjärresurserna har använts på en webbsida är de sökbara och användbara för alla som har behörighet att komma åt den lokala mappen där de hämtade resurserna lagras (`connectedassets` i ovanstående genomgång). The assets are also searchable and visible in the local repository via [!UICONTROL Content Finder].

De hämtade resurserna kan användas som andra lokala resurser, förutom att associerade metadata inte kan redigeras.

## Begränsningar {#limitations}

**Behörigheter och hantering av resurser**

* Lokala resurser synkroniseras inte med de ursprungliga resurserna i fjärrdistributionen. Ändringar, borttagningar eller återkallande av behörigheter i DAM-distributionen sprids inte längre ned i kedjan.
* Lokala resurser är skrivskyddade kopior. Experience Manager-komponenter gör icke-förstörande redigeringar av resurser. Inga andra redigeringar tillåts.
* Lokalt hämtade resurser är endast tillgängliga för redigeringsändamål. Det går inte att använda arbetsflöden för resursuppdatering och metadata kan inte redigeras.
* Endast bilder och dokumentformaten i listan stöds. [!DNL Dynamic Media] resurser, innehållsfragment och Experience Fragments stöds inte.
* Metadatascheman hämtas inte.
* All [!DNL Sites] authors have read permissions on the fetched copies, even if they do not have access to the remote DAM deployment.
* Det finns inte API-stöd för att anpassa integreringen.
* Funktionen stöder smidig sökning och användning av fjärresurser. Om du vill göra många fjärresurser tillgängliga i den lokala distributionen på en gång bör du överväga att migrera resurserna. Se [Handbok för resursmigrering](assets-migration-guide.md).
* It is not possible to use a remote asset as a page thumbnail on [!UICONTROL Page Properties] user interface. You can set a thumbnail of a web page in [!UICONTROL Page Properties] user interface from the [!UICONTROL Thumbnail] by clicking [!UICONTROL Select Image].

**Konfigurera och licensiera**

* [!DNL Experience Manager Assets] deployment on AMS is supported.
* [!DNL Experience Manager Sites] kan ansluta till en enda [!DNL Experience Manager Assets] databas åt gången.
* A license of [!DNL Experience Manager Assets] working as remote repository.
* One or more licenses of [!DNL Experience Manager Sites] working as local authoring deployment.

**Användning**

* De enda funktioner som stöds är sökning efter fjärresurser och att dra fjärresurserna till den lokala sidan för att skapa innehåll.
* Tidsgränsen för hämtning är 5 sekunder. Författare kan ha problem med att hämta resurser, till exempel om det råder nätverksproblem. Authors can re-attempt by dragging the remote asset from [!UICONTROL Content Finder] to [!UICONTROL Page Editor].
* Enkla redigeringar som är icke-destruktiva och redigering som stöds via [!DNL Experience Manager]-komponenten kan tillämpas på hämtade resurser. `Image` Resurserna är skrivskyddade.

## Felsöka problem {#troubleshoot}

Följ dessa steg för att felsöka vanliga fel:

* Om du inte kan söka efter fjärresurser via Content Finder kontrollerar du att de roller och behörigheter som krävs finns på plats.
* En resurs som hämtats från en DAM-fjärrdistribution kanske inte publiceras på en webbsida av följande skäl: Den finns inte i fjärrdistributionen, lämplig behörighet saknas för att hämta den eller nätverksfel. Kontrollera att resursen inte tagits bort från DAM-fjärrdistributionen eller att behörigheterna inte har ändrats, kontrollera att lämpliga villkor är uppfyllda, försök lägga till resursen på sidan igen och publicera den på nytt. Kontrollera i [listan över asynkrona jobb](/help/assets/asynchronous-jobs.md) om fel uppstod vid hämtning av resurser.
