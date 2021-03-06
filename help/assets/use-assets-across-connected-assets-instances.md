---
title: Använd Connected Assets när du vill dela DAM-resurser i [!DNL Sites]
description: Använd resurser som är tillgängliga på en fjärrdator [!DNL Adobe Experience Manager Assets] distribution när du skapar webbsidor på en annan [!DNL Adobe Experience Manager Sites] distribution.
contentOwner: AK
mini-toc-levels: 2
role: User, Admin, Leader
feature: Connected Assets,User and Groups
exl-id: 4ceb49d8-b619-42b1-81e7-c3e83d4e6e62
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '3686'
ht-degree: 17%

---

# Använd Connected Assets när du vill dela DAM-resurser i [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/use-assets-across-connected-assets-instances.html?lang=en) |
| AEM 6.5 | Den här artikeln |


I stora företag kan den infrastruktur som krävs för att skapa webbplatser vara distribuerad. Ibland kan funktionerna för att skapa webbplatser och de digitala resurser som används för att skapa webbplatserna finnas i olika distributioner. En orsak kan vara att befintliga distributioner som krävs för att fungera tillsammans distribueras geografiskt. En annan orsak kan vara förvärv som leder till heterogen infrastruktur, inklusive olika [!DNL Experience Manager] versioner som huvudföretaget vill använda tillsammans.

Funktionen för anslutna resurser har stöd för ovanstående användningsfall genom att integrera [!DNL Experience Manager Sites] och [!DNL Experience Manager Assets]. Användare kan skapa webbsidor i [!DNL Sites] som använder digitala resurser från en separat [!DNL Assets] distributioner.

>[!NOTE]
>
>Konfigurera bara anslutna resurser när du behöver använda de resurser som är tillgängliga på en fjärrdistribution av DAM på en separat webbplatsdistribution för att skapa webbsidor.

## Översikt över Connected Assets {#overview-of-connected-assets}

Vid redigering av sidor i [!UICONTROL Page Editor] som målmål kan författarna söka, bläddra bland och bädda in resurser från ett annat [!DNL Assets] driftsättning som fungerar som en källa till resurser. Administratörerna skapar en engångsintegrering av en distribution av [!DNL Experience Manager] med [!DNL Sites] med en annan driftsättning av [!DNL Experience Manager] med [!DNL Assets] funktioner. Man kan också använda Dynamic Media-bilder på webbplatsens webbsidor med hjälp av uppkopplade resurser och utnyttja Dynamic Media funktioner, som smart beskärning och bildförinställningar.

För [!DNL Sites] författare är fjärrresurserna tillgängliga som skrivskyddade lokala resurser. Funktionen stöder smidig sökning och åtkomst till fjärrresurser i Site Editor. För andra användningsområden där det kan krävas att hela resursen är tillgänglig på Sites bör du överväga att migrera resurserna satsvis i stället för att utnyttja anslutna resurser. Se [Migreringsguide för Experience Manager Assets](/help/assets/assets-migration-guide.md).

### Förutsättningar och distributioner som stöds {#prerequisites}

Innan du använder eller konfigurerar den här funktionen bör du kontrollera följande:

* Användarna ingår i rätt användargrupper för varje distribution.
* För [!DNL Adobe Experience Manager] distributionstyper, ett av villkoren är uppfyllt. [!DNL Experience Manager] 6.5 [!DNL Assets] fungerar med [!DNL Experience Manager] as a Cloud Service. Mer information om hur den här funktionen fungerar i [!DNL Experience Manager] som [!DNL Cloud Service], se [Anslutna resurser i Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] som [!DNL Cloud Service] | [!DNL Experience Manager] 6.5 [!DNL Sites] på AMS | [!DNL Experience Manager] 6.5 [!DNL Sites] lokal |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]som[!DNL Cloud Service]** | Stöds | Stöds | Stöds |
   | **[!DNL Experience Manager]6.5 [!DNL Assets] på AMS** | Stöds | Stöds | Stöds |
   | **[!DNL Experience Manager]6.5 [!DNL Assets] lokal** | Stöds ej | Stöds ej | Stöds ej |

### Filformat som stöds {#mimetypes}

Författare söker efter bilder och följande typer av dokument i Content Finder och drar de sökbara resurserna i Page Editor. Dokument läggs till i `Download` och bilder till `Image` -komponenten. Författare kan även lägga till fjärrresurserna i valfri anpassad [!DNL Experience Manager] som utökar standardkomponenten `Download` eller `Image` -komponenter. De format som stöds är:

* **Bildformat**: Formaten som [Bildkomponent](assets-formats.md#supported-raster-image-formats) stöder.
* **Dokumentformat**: Se [dokumentformat som stöds](assets-formats.md#supported-document-formats).

### Användare och grupper som krävs {#users-and-groups-involved}

De olika roller som krävs för att konfigurera och använda funktionen och motsvarande användargrupper beskrivs nedan. Lokalt omfång används för de fall där en författare skapar en webbsida. Fjärromfång används för DAM-distributionen som är värd för de nödvändiga resurserna. The [!DNL Sites] författaren hämtar dessa fjärrresurser.

| Roll | Omfång | Användargrupp | Användarnamn i genomgång | Beskrivningar |
|---|---|---|---|---|
| [!DNL Sites] administratör | Lokalt | [!DNL Experience Manager] `administrators` | `admin` | Konfigurera [!DNL Experience Manager] och konfigurera integrering med fjärrkontrollen [!DNL Assets] distribution. |
| DAM-användare | Lokalt | `Authors` | `ksaner` | Används för att visa och duplicera de hämtade resurserna i `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Lokalt | <ul><li>`Authors` (med läsåtkomst på fjärr-DAM och författaråtkomst på lokal [!DNL Sites]) </li> <li>`dam-users` på lokal [!DNL Sites]</li></ul> | `ksaner` | Slutanvändaren är [!DNL Sites] författare som använder den här integreringen för att förbättra innehållets hastighet. Författarna söker efter och bläddrar bland resurser i fjärr-DAM med [!UICONTROL Content Finder] och använda de bilder som behövs på lokala webbsidor. Autentiseringsuppgifterna för `ksaner` DAM-användaren används. |
| [!DNL Assets] administratör | Fjärr | [!DNL Experience Manager] `administrators` | `admin` på fjärrkontrollen [!DNL Experience Manager] | Konfigurerar CORS (Cross-Origin Resource Sharing). |
| DAM-användare | Fjärr | `Authors` | `ksaner` på fjärrkontrollen [!DNL Experience Manager] | Författarroll på fjärrkontrollen [!DNL Experience Manager] distribution. Söker efter och bläddrar bland resurser i Connected Assets med hjälp av [!UICONTROL Content Finder]. |
| DAM-distributör (teknisk användare) | Fjärr | [!DNL Sites] `Authors` | `ksaner` på fjärrkontrollen [!DNL Experience Manager] | Den här användaren som finns på fjärrdistributionen används av [!DNL Experience Manager] lokal server (inte [!DNL Sites] författarroll) för att hämta fjärrresurserna, för [!DNL Sites] författare. Den här rollen är inte densamma som de två `ksaner`-rollerna ovan och den tillhör en annan användargrupp. |

### Arkitektur för anslutna resurser {#connected-assets-architecture}

Med Experience Manager kan du ansluta en fjärrdistribution av DAM som en källa till flera Experience Manager [!DNL Sites] distributioner. Du kan ansluta högst fyra [!DNL Sites] distributioner till en fjärr-DAM. Du kan dock ansluta en [!DNL Sites] driftsättning med endast en fjärrdistribution av DAM.

Följande diagram visar vilka scenarier som stöds:

![Arkitektur för anslutna resurser](assets/connected-assets-architecture.png)

I följande diagram visas ett scenario som inte stöds:

![Arkitektur för anslutna resurser](assets/connected-assets-architecture-unsupported.png)

## Konfigurera en anslutning mellan [!DNL Sites] och [!DNL Assets] distributioner {#configure-a-connection-between-sites-and-assets-deployments}

An [!DNL Experience Manager] administratören kan skapa den här integreringen. Behörigheterna som krävs för att använda det skapas via användargrupper när de har skapats. Användargrupperna definieras på [!DNL Sites] driftsättning och driftsättning av DAM.

Konfigurera anslutna resurser och lokala [!DNL Sites] anslutning, följ dessa steg:

1. Åtkomst till en befintlig [!DNL Sites] distribuera eller skapa en distribution med följande kommando:

   1. I JAR-filens mapp kör du följande kommando på en terminal för att skapa varje [!DNL Experience Manager] server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Efter några minuter har [!DNL Experience Manager] servern har startats. Tänk på det här [!DNL Sites] distribuera som lokal dator för webbsidesutveckling, till exempel på `https://[local_sites]:4502`.

1. Se till att användare och roller med rätt omfång finns på [!DNL Sites] distribution och [!DNL Assets] driftsättning på AMS. Skapa en teknisk användare på [!DNL Assets] distribution och tillägg till användargruppen som anges i [berörda användare och grupper](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Åtkomst till lokala [!DNL Sites] distribution på `https://[local_sites]:4502`. Klicka på **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Connected Assets Configuration]** och ange följande värden:

   1. A **[!UICONTROL Title]** av konfigurationen.
   1. **[!UICONTROL Remote DAM URL]** är URL:en för [!DNL Assets] plats i formatet `https://[assets_servername]:[port]`.
   1. Autentiseringsuppgifter för en DAM-distributör (teknisk användare).
   1. I **[!UICONTROL Mount Point]** anger du lokala [!DNL Experience Manager] sökväg där [!DNL Experience Manager] hämtar resurserna. Till exempel, mappen `remoteassets`. Resurserna som hämtas från DAM lagras i den här mappen på [!DNL Sites] distribution.
   1. **[!UICONTROL Local Sites URL]** är platsen för [!DNL Sites] distribution. [!DNL Assets] för distribution används det här värdet för att behålla referenser till de digitala resurserna som hämtas av det här [!DNL Sites] distribution.
   1. Autentiseringsuppgifter för [!DNL Sites] teknisk användare.
   1. Värdet för **[!UICONTROL Original Binary transfer optimization Threshold]** anges om de ursprungliga resurserna (inklusive återgivningarna) överförs synkront eller inte. Resurser med mindre filstorlek kan enkelt hämtas medan resurser med relativt större filstorlek är bäst synkroniserade asynkront. Värdet beror på dina nätverksfunktioner.
   1. Välj **[!UICONTROL Datastore Shared with Connected Assets]**, om du använder ett datalager för att lagra dina resurser och datalagret delas mellan båda distributionerna. I det här fallet spelar tröskelvärdet ingen roll eftersom faktiska tillgångsbinärfiler är tillgängliga i datalagret och inte överförs.

   ![En typisk konfiguration för funktionen för anslutna resurser](assets/connected-assets-typical-config.png)

   *Bild: En typisk konfiguration för funktionen Anslutna resurser.*

1. Befintliga digitala resurser på [!DNL Assets] distributionen har redan bearbetats och återgivningarna genereras. Dessa återgivningar hämtas med den här funktionen så du behöver inte generera om återgivningarna. Inaktivera arbetsflödets startprogram för att förhindra återgivning av återgivningar. Justera startkonfigurationerna på ([!DNL Sites]) distribution för att exkludera `connectedassets` (resurserna hämtas i den här mappen).

   1. På [!DNL Sites] distribution, klicka **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.

   1. Sök efter startprogram med arbetsflöden som **[!UICONTROL DAM Update Asset]** och **[!UICONTROL DAM Metadata Writeback]**.

   1. Välj startprogrammet för arbetsflödet och klicka på **[!UICONTROL Properties]** i åtgärdsfältet.

   1. I [!UICONTROL Properties] guide, ändra **[!UICONTROL Path]** fält som följande mappningar för att uppdatera deras reguljära uttryck för att utesluta monteringspunkten **[!UICONTROL connectedassets]**.

   | Före | Efter |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Alla återgivningar som är tillgängliga på fjärrdistributionen hämtas när författare hämtar en resurs. Om du vill skapa fler återgivningar av en hämtad resurs hoppar du över det här konfigurationssteget. The [!UICONTROL DAM Update Asset] arbetsflödet aktiveras och skapar fler återgivningar. Dessa återgivningar är bara tillgängliga på den lokala [!DNL Sites] och inte på fjärrdistributionen av DAM.

1. Lägg till [!DNL Sites] distribution som ett tillåtet ursprung i CORS-konfigurationen på [!DNL Assets] distribution. Mer information finns i [förstå CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html).

1. Konfigurera [Stöd för samma webbplats-cookie](/help/sites-administering/same-site-cookie-support.md).

Du kan kontrollera anslutningen mellan konfigurerade [!DNL Sites] driftsättning och [!DNL Assets] distribution.

![Anslutningstest för konfigurerade anslutna resurser [!DNL Sites]](assets/connected-assets-multiple-config.png)
*Bild: Anslutningstest för konfigurerade anslutna resurser [!DNL Sites].*

## Använda Dynamic Media-resurser {#dynamic-media-assets}


Med sammankopplade resurser kan du använda bildresurser som bearbetats av [!DNL Dynamic Media] från fjärrdistribution av DAM på Sites-sidor och utnyttja Dynamic Media-funktioner, som smarta beskärnings- och bildförinställningar.

Används [!DNL Dynamic Media] med anslutna resurser:

1. Konfigurera [!DNL Dynamic Media] på fjärrdistribution av DAM med Sync-läge aktiverat.
1. Konfigurera [Anslutna resurser](#configure-a-connection-between-sites-and-assets-deployments).
1. Konfigurera [!DNL Dynamic Media] på Sites-instansen med samma företagsnamn som konfigurerats på fjärr-DAM. Webbplatsdistributionen måste ha skrivskyddad åtkomst till Dynamic Media-kontot för att kunna arbeta med anslutna resurser. Se därför till att inaktivera synkroniseringsläget i Dynamic Media-konfigurationen på platsinstansen.

>[!CAUTION]
>
>Med sammankopplade resurser och [!DNL Dynamic Media] konfiguration, du kan inte använda [!DNL Dynamic Media] för att bearbeta lokala resurser som finns på [!DNL Sites] distribution.

## Konfigurera [!DNL Dynamic Media] {#configure-dynamic-media}

Konfigurera [!DNL Dynamic Media] på [!DNL Assets] och [!DNL Sites] distributioner:

1. Aktivera och konfigurera [!DNL Dynamic Media] som global konfiguration på fjärrkontrollen [!DNL Assets] driftsättning. Information om hur du konfigurerar Dynamic Media finns i [Konfigurera Dynamic Media](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services).<br/>
På fjärrkontrollen [!DNL Assets] distribution, in [!UICONTROL Dynamic Media sync mode], markera **[!UICONTROL Enabled by default]**.

1. Skapa konfiguration för anslutna resurser enligt beskrivningen i [Konfigurera anslutning mellan platser och distributioner av resurser](#configure-a-connection-between-sites-and-assets-deployments). Välj även **[!UICONTROL Fetch Original Rendition for Dynamic Media Connected Assets]** alternativ.

1. Konfigurera [!DNL Dynamic Media] på lokal [!DNL Sites] och fjärranslutning [!DNL Assets] distributioner. Följ instruktionerna för att [konfigurera [!DNL Dynamic Media]](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services).

   * Använd samma företagsnamn i alla konfigurationer.
   * På lokal [!DNL Sites], in [!UICONTROL Dynamic Media sync mode], markera **[!UICONTROL Disabled by default]**. The [!DNL Sites] distributionen måste ha skrivskyddad åtkomst till [!DNL Dynamic Media] konto.
   * På lokal [!DNL Sites], i **[!UICONTROL Publish Assets]** alternativ, markera **[!UICONTROL Selective Publish]**. Markera inte **[!UICONTROL Sync All Content]**.

1. Aktivera [[!DNL Dynamic Media] stöd i Image Core Component](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html#dynamic-media). Den här funktionen aktiverar standardinställningen [Bildkomponent](https://www.aemcomponents.dev/content/core-components-examples/library/page-authoring/image.html) att visa [!DNL Dynamic Media] bilder när [!DNL Dynamic Media] bilder används av författare på webbsidor på lokala [!DNL Sites] distribution.

## Använda fjärresurser {#use-remote-assets}

Webbplatsens författare använder Content Finder för att ansluta till DAM-distributionen. Författarna kan bläddra bland, söka efter och dra fjärresurserna till en komponent. Om du vill autentisera till fjärr-DAM ska du se till att de autentiseringsuppgifter som administratören har angett är tillgängliga.

Författare kan använda resurserna som finns på den lokala DAM-resursen och den fjärranslutna DAM-distributionen på en enda webbsida. Använd Content Finder för att växla mellan att söka i det lokala DAM-systemet eller söka i det fjärranslutna DAM-systemet.

Endast de taggar för fjärrresurser som har en exakt motsvarande tagg tillsammans med samma taxonomihierarki, som finns på den lokala [!DNL Sites] distribution. Alla andra taggar tas bort. Författare kan söka efter fjärrresurser med hjälp av alla taggar som finns på fjärrkontrollen [!DNL Experience Manager] driftsättning eftersom den erbjuder fulltextsökning.

### Genomgång av användningen {#walk-through-of-usage}

Använd konfigurationen ovan när du vill prova redigeringsfunktionen och se hur den fungerar. Använd de dokument eller bilder du vill ha på den fjärranslutna DAM-distributionen.

1. Navigera till [!DNL Assets] -gränssnittet på fjärrdistributionen genom åtkomst **[!UICONTROL Assets]** > **[!UICONTROL Files]** från [!DNL Experience Manager] arbetsyta. Du kan även få åtkomst till `https://[assets_servername_ams]:[port]/assets.html/content/dam` i en webbläsare. Ladda upp de resurser du vill ha.
1. På [!DNL Sites] distribution, i profilaktiveraren i det övre högra hörnet, klicka på **[!UICONTROL Impersonate as]**. Ange `ksaner` som användarnamn, markera det angivna alternativet och klicka på **[!UICONTROL OK]**.
1. Öppna en We.Retail-webbsida på **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Redigera sidan. Du kan även öppna `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` i en webbläsare när du vill redigera en sida.

   Klicka på **[!UICONTROL Toggle Side Panel]** överst till vänster på sidan.

1. Öppna [!UICONTROL Assets] -flik (Remote Content Finder) och klicka på **[!UICONTROL Log in to Connected Assets]**.
1. Ange inloggningsuppgifterna, `ksaner` som användarnamn och `password` som lösenord. Den här användaren har redigeringsbehörighet för båda [!DNL Experience Manager] distributioner.
1. Sök efter resursen som du har lagt till i DAM. Fjärresurserna visas i den vänstra panelen. Filtrera efter bilder eller dokument och filtrera efter olika typer av dokument som stöds. Dra bilderna till en `Image`-komponent och dokument till en `Download`-komponent.

   De hämtade resurserna är skrivskyddade på den lokala [!DNL Sites] distribution. Du kan fortfarande använda alternativen som finns i [!DNL Sites] -komponenter för att redigera den hämtade resursen. Redigering med komponenter är icke-destruktiv.

   ![Alternativ för att filtrera dokumenttyper och bilder vid sökning efter resurser på DAM-fjärrdistribution](assets/filetypes_filter_connected_assets.png)

   *Bild: Alternativ för att filtrera dokumenttyper och bilder vid sökning efter resurser på DAM-fjärrdistribution.*

1. En webbplatsförfattare får ett meddelande om en resurs original hämtas asynkront och om någon hämtningsåtgärd misslyckas. Under utvecklingen eller till och med efter redigeringen kan författarna se detaljerad information om hämtningsuppgifter och fel i [asynkrona jobb](/help/sites-administering/asynchronous-jobs.md) användargränssnitt.

   ![Meddelande om asynkron hämtning av resurser som sker i bakgrunden.](assets/assets_async_transfer_fails.png)

   *Bild: Meddelande om asynkron hämtning av resurser som sker i bakgrunden.*

1. När en sida publiceras [!DNL Experience Manager] visar en fullständig lista över resurser som används på sidan. Kontrollera att fjärresurserna har hämtats vid publiceringen. Information om hur du kontrollerar statusen för varje hämtad resurs finns i [asynkrona jobb](/help/sites-administering/asynchronous-jobs.md) användargränssnitt.

   >[!NOTE]
   >
   >Även om en eller flera fjärrresurser inte hämtas helt publiceras sidan. The [!DNL Experience Manager] I meddelandeområdet visas ett meddelande om fel som visas på sidan för asynkrona jobb.

>[!CAUTION]
>
>När de hämtade fjärrresurserna har använts på en webbsida är de sökbara och användbara för alla som har behörighet att komma åt den lokala mappen. De hämtade resurserna lagras i den lokala mappen (`connectedassets` i ovanstående genomgång). Resurserna är också sökbara och synliga i det lokala datalagret via [!UICONTROL Content Finder].

De hämtade resurserna kan användas som andra lokala resurser, förutom att associerade metadata inte kan redigeras.

### Kontrollera hur en resurs används på olika webbsidor {#asset-usage-references}

[!DNL Experience Manager] gör att DAM-användare kan kontrollera alla referenser till en resurs. Det hjälper till att förstå och hantera användningen av en resurs på en fjärransluten dator [!DNL Sites] och i sammansatta resurser. Många som skapar webbsidor på [!DNL Experience Manager Sites] kan använda en resurs på en fjärransluten [!DNL Assets] på olika webbsidor. För att förenkla resurshanteringen och inte leda till brutna referenser är det viktigt för DAM-användarna att kontrollera användningen av en resurs på lokala webbplatser och fjärrwebbsidor. The [!UICONTROL References] i en resurs [!UICONTROL Properties] visas lokala referenser och fjärrreferenser för resursen.

Så här visar och hanterar du referenser på [!DNL Assets] -distribution, följ dessa steg:

1. Välj en resurs i [!DNL Assets] Konsol och klicka **[!UICONTROL Properties]** i verktygsfältet.
1. Klicka på fliken **[!UICONTROL References]**. Se **[!UICONTROL Local References]** för användning av tillgången på [!DNL Assets] distribution. Se **[!UICONTROL Remote References] för användning av tillgången på [!DNL Sites] distribution där resursen hämtades med funktionen för anslutna resurser.

   ![Fjärrreferenser på sidan Resursegenskaper](assets/connected-assets-remote-reference.png)

1. Referenserna för [!DNL Sites] sidor visar totalt antal referenser för varje lokal [!DNL Sites]. Det kan ta en stund att hitta alla referenser och visa det totala antalet referenser.
1. Listan med referenser är interaktiv och DAM-användare kan klicka på en referens för att öppna referenssidan. Om fjärrreferenser av någon anledning inte kan hämtas visas ett meddelande som informerar användaren om felet.
1. Användare kan flytta eller ta bort resursen. När du flyttar eller tar bort en resurs visas det totala antalet referenser för alla markerade resurser/mappar i en varningsdialogruta. När du tar bort en resurs för vilken referenserna ännu inte har hämtats visas en varningsdialogruta.

   ![varning om force delete](assets/delete-referenced-asset.png)

### Hantera uppdateringar av resurser i fjärr-DAM {#manage-updates-in-remote-dam}

Efter [konfigurera en anslutning](#configure-a-connection-between-sites-and-assets-deployments) mellan fjärr-DAM och [!DNL Sites] distribuerar, blir resurserna på fjärr-DAM tillgängliga på [!DNL Sites] distribution. Du kan sedan uppdatera, ta bort, byta namn på och flytta åtgärder på fjärr-DAM-resurser eller -mappar. Uppdateringarna, med viss fördröjning, är automatiskt tillgängliga på [!DNL Sites] distribution. Dessutom, om en resurs på en fjärr-DAM används på en lokal [!DNL Experience Manager Sites] sidan visas uppdateringarna av resursen på fjärr-DAM på [!DNL Sites] sida.

När du flyttar en resurs från en plats till en annan bör du se till att du [justera referenser](/help/assets/manage-assets.md) så att resursen visas på [!DNL Sites] sida. Om du flyttar en resurs till en plats som inte är tillgänglig från den lokala [!DNL Sites] distributionen, kan resursen inte visas i Sites-distributionen.

Du kan även uppdatera metadataegenskaperna för en resurs på en fjärr-DAM och ändringarna är tillgängliga på den lokala [!DNL Sites] distribution.

[!DNL Sites] författare kan förhandsgranska de tillgängliga uppdateringarna på [!DNL Sites] distribuera och publicera sedan ändringarna igen för att göra dem tillgängliga på [!DNL Experience Manager] publiceringsinstans.

[!DNL Experience Manager] visar en visuell indikator för förfallen status för resurser i `Remote Assets Content Finder` för att hindra webbplatsförfattare från att använda resursen på en [!DNL Sites] sida. Om du använder en resurs med en utgången status på en [!DNL Sites] sidan, resursen visas inte på [!DNL Experience Manager] publiceringsinstans.

>[!NOTE]
>
>Uppdateringarna av resurser i fjärr-DAM är tillgängliga för [!DNL Sites] distribution endast om fjärr-DAM och [!DNL Sites] distributioner är aktiverade [!DNL Experience Manager].

## Vanliga frågor {#frequently-asked-questions}

+++**Ska du konfigurera anslutna resurser om du behöver använda resurser som är tillgängliga på din [!DNL Sites] distribution?**

I så fall behöver du inte konfigurera anslutna resurser. Du kan använda resurser som finns på [!DNL Sites] distribution.

+++

+++**När behöver du konfigurera funktionen för anslutna resurser?**

Konfigurera bara funktionen för anslutna resurser när du behöver använda resurserna som finns på en fjärr-DAM-distribution på en [!DNL Sites] distribution.

+++

+++**Hur många [!DNL Sites] kan du ansluta till en fjärr-DAM-distribution efter att ha konfigurerat anslutna resurser?**

Du kan ansluta högst fyra [!DNL Sites] distributioner till en fjärr-DAM-distribution efter konfigurering av anslutna resurser. Mer information finns i [Arkitektur för anslutna resurser](#connected-assets-architecture).

+++

+++**Hur många fjärr-DAM-distributioner kan du ansluta till en [!DNL Sites] distribueras efter konfigurering av anslutna resurser?**

Du kan ansluta en fjärr-DAM-distribution till en [!DNL Sites] efter konfigurering av anslutna resurser. Mer information finns i [Arkitektur för anslutna resurser](#connected-assets-architecture).

+++

+++**Kan du använda Dynamic Media-resurser från dina [!DNL Sites] distribueras efter konfigurering av anslutna resurser?**

När du har konfigurerat anslutna resurser [!DNL Dynamic Media] resurser är tillgängliga på [!DNL Sites] i skrivskyddat läge. Därför kan du inte använda [!DNL Dynamic Media] för att bearbeta resurser på [!DNL Sites] distribution. Mer information finns i [Konfigurera en anslutning mellan platser och Dynamic Media-distributioner](#dynamic-media-assets).

+++

+++**Kan du använda material för formaten Image och Document från DAM-fjärrdistributionen på [!DNL Sites] distribueras efter konfigurering av anslutna resurser?**

Ja, du kan använda resurserna för formaten Image och Document från DAM-fjärrdistributionen på [!DNL Sites] efter konfigurering av anslutna resurser.

+++

+++**Kan ni använda innehållsfragment och videomaterial från den fjärranslutna DAM-distributionen på [!DNL Sites] distribueras efter konfigurering av anslutna resurser?**

Nej, du kan inte använda innehållsfragment och videomaterial från fjärr-DAM-distributionen på [!DNL Sites] efter konfigurering av anslutna resurser.

+++

+++**Kan du använda Dynamic Media-resurser från fjärr-DAM-distributionen på [!DNL Sites] distribueras efter konfigurering av anslutna resurser?**

Ja, du kan konfigurera och använda Dynamic Media-bildresurser från fjärrdistributionen av DAM på [!DNL Sites] efter konfigurering av anslutna resurser. Mer information finns i [Konfigurera en anslutning mellan platser och Dynamic Media-distributioner](#dynamic-media-assets).

+++

+++**När du har konfigurerat anslutna resurser, kan du uppdatera, ta bort, byta namn på och flytta åtgärder på fjärr-DAM-resurser eller -mappar?**

Ja, när du har konfigurerat anslutna resurser kan du uppdatera, ta bort, byta namn på och flytta resurser eller mappar i fjärr-DAM. Uppdateringarna, med viss fördröjning, är automatiskt tillgängliga i Sites-distributionen. Mer information finns i [Hantera uppdateringar av resurser i fjärr-DAM](#handling-updates-to-remote-assets).

+++

+++**När du har konfigurerat anslutna resurser, kan du lägga till eller ändra resurser i [!DNL Sites] driftsätta och göra dem tillgängliga på fjärrdistribution av DAM?**

Du kan lägga till resurser i [!DNL Sites] distribution, men dessa resurser kan inte göras tillgängliga för den fjärranslutna DAM-distributionen.

+++

## Begränsningar och bästa metoder {#tip-and-limitations}

* Konfigurera [Assets Insight](/help/assets/asset-insights.md) på [!DNL Sites] -instans.

### Tillstånd och resurshantering {#permissions-and-managing-assets}

* Lokala resurser är skrivskyddade kopior. [!DNL Experience Manager] -komponenter gör icke-förstörande redigeringar av resurser. Inga andra redigeringar tillåts.
* Lokalt hämtade resurser är endast tillgängliga för redigeringsändamål. Det går inte att använda arbetsflöden för resursuppdatering och metadata kan inte redigeras.
* Endast bilder och dokumentformaten i listan stöds. [!DNL Content Fragments] och [!DNL Experience Fragments] stöds inte.
* [!DNL Experience Manager] hämtar inte metadatamatcheman. Det innebär att alla hämtade metadata inte visas. Om schemat uppdateras separat på [!DNL Sites] distributionen visas alla metadataegenskaper.
* Alla [!DNL Sites] författare har läsbehörighet för de hämtade kopiorna, även om författare inte har åtkomst till den fjärranslutna DAM-distributionen.
* Det finns inte API-stöd för att anpassa integreringen.
* Funktionen stöder smidig sökning och användning av fjärresurser. Om du vill göra många fjärresurser tillgängliga i den lokala distributionen på en gång bör du överväga att migrera resurserna. Se [Handbok för resursmigrering](assets-migration-guide.md).
* Det går inte att använda en fjärrresurs som sidminiatyr på [!UICONTROL Page Properties] användargränssnitt. Du kan ange en miniatyrbild för en webbsida i [!UICONTROL Page Properties] användargränssnittet från [!UICONTROL Thumbnail] genom att klicka [!UICONTROL Select Image].

### Konfigurera och licensiera {#setup-licensing}

* [!DNL Assets] distribution på [!DNL Adobe Managed Services] stöds.
* [!DNL Sites] kan ansluta till en enda [!DNL Assets] driftsättning i taget.
* En licens för [!DNL Assets] du måste arbeta som fjärrdatabas.
* En eller flera licenser av [!DNL Sites] måste fungera som lokal redigeringsdistribution.

### Användning {#usage}

* Användare kan söka efter fjärrresurser och dra dem på den lokala sidan när de redigerar. Inga andra funktioner stöds.
* Tidsgränsen för hämtning är 5 sekunder. Författare kan ha problem med att hämta resurser, till exempel om det råder nätverksproblem. Författare kan försöka igen genom att dra fjärrresursen från [!UICONTROL Content Finder] till [!UICONTROL Page Editor].
* Enkla redigeringar som är icke-destruktiva och redigering som stöds via `Image`-komponenten kan tillämpas på hämtade resurser. Resurserna är skrivskyddade.
* Det enda sättet att hämta resursen på nytt är att dra den till en sida. Det finns inget API-stöd eller andra metoder för att hämta om en resurs för att uppdatera den.
* Om tillgångarna tas ur bruk från DAM används de fortfarande [!DNL Sites] sidor.
* Fjärrreferensposterna för en resurs hämtas asynkront. Referenserna och det totala antalet är inte i realtid och det kan vara en skillnad om en webbplatsförfattare använder resursen medan en DAM-användare visar referensen. DAM-användare kan uppdatera sidan och försöka igen om några minuter för att få fram det totala antalet.

## Felsöka problem {#troubleshoot}

Följ de här stegen för att felsöka vanliga fel:

* Om du inte kan söka efter fjärrresurser från [!UICONTROL Content Finder]kontrollerar du att de roller och behörigheter som krävs finns på plats.

* En resurs som hämtats från fjärr-DAM kanske inte publiceras på en webbsida av en eller flera orsaker. Den finns inte på fjärrservern, saknar behörighet att hämta den eller så kan nätverksfel vara orsaken. Se till att resursen inte tas bort från fjärr-DAM. Se till att rätt behörigheter finns och att kraven är uppfyllda. Försök lägga till resursen på sidan igen och publicera den på nytt. Kontrollera i [listan över asynkrona jobb](/help/sites-administering/asynchronous-jobs.md) om fel uppstod vid hämtning av resurser.

* Om du inte har åtkomst till fjärr-DAM-distributionen från den lokala [!DNL Sites] ska du se till att cookies mellan webbplatser tillåts och [Stöd för samma webbplats-cookie](/help/sites-administering/same-site-cookie-support.md) är konfigurerad. Om cookies mellan webbplatser blockeras kan du distribuera [!DNL Experience Manager] kan inte autentiseras. Till exempel: [!DNL Google Chrome] i Incognito-läge kan blockera cookies från tredje part. Tillåt cookies i [!DNL Chrome] klickar du på ögonikonen i adressfältet, navigerar till **Webbplatsen fungerar inte** > **Blockerad** markerar du fjärr-DAM-URL:en och tillåter inloggningstokencookie. Alternativt, se [aktivera cookies från tredje part](https://support.google.com/chrome/answer/95647).

   ![Cookie-fel i Chrome-webbläsare i Incognito-läge](assets/chrome-cookies-incognito-dialog.png)

* Om fjärrreferenser inte hämtas och leder till ett felmeddelande, kontrollerar du om [!DNL Sites] är tillgänglig och kontrollerar om det finns problem med nätverksanslutningen. Försök igen senare för att kontrollera. [!DNL Assets] distributionsförsök två gånger för att upprätta en anslutning med [!DNL Sites] och rapporterar sedan ett fel.

   ![det gick inte att hämta resursfjärrreferenser](assets/reference-report-failure.png)



