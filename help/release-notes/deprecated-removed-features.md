---
title: Borttagna funktioner i Adobe Experience Manager 6.5.
description: Versionsinformation om borttagna funktioner i Adobe Experience Manager 6.5.
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 191c4b02274ca7e3e9d4622b72cd585870581f47
workflow-type: tm+mt
source-wordcount: '1742'
ht-degree: 2%

---

# Föråldrade och borttagna funktioner {#deprecated-and-removed-features}

<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->

Adobe utvärderar ständigt produktfunktioner för att så småningom förnya eller ersätta äldre funktioner med modernare alternativ för att förbättra det totala kundvärdet, alltid med noggrant övervägande av bakåtkompatibilitet.

Följande regler gäller för att informera om den förestående borttagningen eller ersättningen av Adobe Experience Manager (AEM)-funktioner:

1. Föråldringsanmälan kommer först. Funktionerna är fortfarande tillgängliga, men har inte förbättrats ytterligare.
1. Borttagning av föråldrade funktioner sker tidigast i följande större version. Faktiskt måldatum för borttagning meddelas senare.

Den här processen ger kunderna minst en releasecykel för att anpassa implementeringen till en ny version eller en efterföljare till en borttagningsfunktion, innan den faktiska borttagningen.

## Föråldrade funktioner {#deprecated-features}

I det här avsnittet visas funktioner som har markerats som borttagna i AEM 6.5. I allmänhet är funktioner som är planerade att tas bort i en framtida version först inaktuella, med ett alternativ.

Kunderna rekommenderas att granska om de använder funktionen/funktionen i den aktuella distributionen och planera för att ändra implementeringen så att den använder det alternativ som erbjuds.

| Område | Funktion | Ersättning | Version (SP) |
|---|---|---|---|
|   |   |   |   |
| Sites | Tjänsten **Adobe AEM Managed Polling Configuration**: `com.day.cq.polling.importer.impl.ManagedPollConfigImpl` | Tjänsten **Adobe AEM Analytics Report Sling Importer**. Se Ansluta till Adobe Analytics och skapa bildrutor - [Konfigurera importintervallet](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval) | 6.5.19.0 |
| Screens | ActiveMQ i Adobe Experience Manager (AEM). ActiveMQ användes för kommunikation mellan två AEM Publish-instanser. | Adobe rekommenderar att man nu använder en belastningsutjämnare. | 6.5.18.0 |
| Upplev fragmentegenskaper för **Status för sociala medier**. |   | 6.5.11.0 |
| [!DNL Sites] | Mallar för innehållsfragment, för att skapa enkla innehållsfragment. | [Modellbaserade strukturerade innehållsfragment](/help/assets/content-fragments/content-fragments-models.md). | 6.5.11.0 |
| Integrering med Creative Cloud | AEM till mappdelning i Creative Cloud introducerades i AEM 6.2. Det ger kreativa användare åtkomst till resurser från AEM, så att de kan öppna dem i [!DNL Creative Cloud]-program och överföra nya filer eller spara ändringar i AEM. En ny funktion i Creative Cloud, Adobe Asset Link, ger en bättre användarupplevelse och kraftfullare åtkomst till AEM direkt inifrån Photoshop, InDesign och Illustrator. Adobe planerar inte att göra ytterligare förbättringar av integrationen mellan AEM och Creative Cloud Mappdelning. Funktionen ingår i AEM, men kunderna rekommenderas att använda ersättningslösningar. | Kunder rekommenderas att byta till nya integrationsfunktioner för Creative Cloud, som Adobe Asset Link eller AEM. |  |
| Assets | `AssetDownloadServlet` är inaktiverat som standard för publiceringsinstanserna. Mer information finns i [AEM checklista för säkerhet](/help/sites-administering/security-checklist.md). | Konfiguration som beskrivs i [AEM checklista för säkerhet](/help/sites-administering/security-checklist.md). |  |
| Integreringar | Skärmen **[!UICONTROL Experience Manager Cloud Services Opt-In]** är inaktuell eftersom integreringen av [!DNL Experience Manager] och [!DNL Adobe Target] har uppdaterats i [!DNL Experience Manager] 6.5. Integreringen stöder Adobe Target Standard API. API:t använder autentisering via Adobe IMS och [!DNL Adobe I/O Runtime]. Den stöder den växande rollen för Adobe Launch till instrumentets [!DNL Experience Manager] sidor för analys och personalisering. Guiden för deltagande är funktionellt irrelevant. | Konfigurera systemanslutningar, Adobe IMS-autentisering och [!DNL Adobe I/O Runtime] integreringar via respektive [!DNL Experience Manager] molntjänster. | 6.5.7.0 |
| Kopplingar | Adobe JCR Connector för Microsoft® SharePoint 2010 och Microsoft® SharePoint 2013 är föråldrad för [!DNL Experience Manager] 6.5. | Ej tillämpligt |  |
| Dynamic Tag Manager (DTM) | Integrationen med DTM är föråldrad. | Växla till att använda Adobe Experience Platform Launch som tagghanterare. |   |
| Adobe Target | Om du lägger till möjligheten för AEM att ansluta till Adobe Target-tjänsten med det [!DNL Adobe I/O]-baserade API:t för Adobe Target Standard (Rest API) i AEM 6.5 är XML-metoden (Target Classic API) föråldrad. | Konfigurera om integreringen till [använd det nya API:t](/help/sites-administering/target.md). |  |
| Adobe Target | Den `mbox.js`-baserade integrationen med Adobe Target i AEM används inte längre. | Växla till `at.js` 1.x. |  |
| Commerce | [CIF REST](https://github.com/adobe/commerce-cif-api) tillhandahölls 2018 som en uppsättning mikrotjänster för att möjliggöra integreringar mellan AEM och e-handelsmotorer. Efter att Adobe förvärvat Adobe Commerce (tidigare Magento) i mitten av 2018 beslutade Adobe att ändra sitt tillvägagångssätt av två skäl. Commerce har en egen uppsättning Commerce API:er (REST och GraphQL) och det är inte bra att underhålla två uppsättningar API:er. Marknadstrender tyder på att kunderna var på väg mot GraphQL eftersom det är ett effektivare sätt att fråga data. 2019 lanserade Adobe den nya Commerce integrationa frameworken med Commerce GraphQL API:er som källa för sanningen. Adobe planerar inte att göra några ytterligare investeringar i CIF REST. Kunder rekommenderas att använda ersättningslösningen. | För AEM-Commerce-integreringar växlar du till [AEM CIF-arkitekturen](https://github.com/adobe/aem-cif-project-archetype) och [AEM CIF kärnkomponenterna](https://github.com/adobe/aem-core-cif-components). Se AEM och Adobe Commerce-integrering [med Commerce integration framework](/help/commerce/cif/integrating/magento.md). Stöd för tredjepartsintegrering (andra än Commerce) med det nya tillvägagångssättet ligger på Adobe roadmap. |  |
| komponenter (AEM Sites) | Adobe planerar inte att göra fler förbättringar av de flesta av Foundation Components som lagras i `/libs/foundation/components`. Leta efter egenskapen `cq:deprecated` och `cq:deprecatedReason` i komponentmappen. AEM 6.5 innehåller Foundation Components, och kunder som uppgraderar från tidigare versioner kan fortsätta använda dem som de är. Foundation Components stöds även om de är inaktuella. | Adobe rekommenderar att du använder kärnkomponenterna för framtida projekt. Befintliga webbplatser kan förbli oförändrade eller använda [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) för att omforma webbplatsen till att använda kärnkomponenter. |  |
| komponenter (AEM Sites) | Designimporterarkomponenterna `/libs/wcm/designimporter/components` har markerats som inaktuella från och med 6.5. Adobe planerar inte att göra ytterligare förbättringar av designimportörens implementering. | Adobe planerar att tillhandahålla en alternativ implementering av användningsexemplet i framtida releaser. |  |
| Foundation | Granite Offloading Framework. Adobe planerar inte att göra ytterligare förbättringar av avlastningsramverket som infördes i CQ 5.6.1 för att externalisera bearbetningen av tillgångar. | Adobe arbetar med nästa generations molnbaserade ramverk för avlastning. |  |
| Utvecklare | `Hobbes.js`. Adobe planerar inte att göra fler förbättringar av testningsramverket för användargränssnittet i `hobbes.js`. | Adobe rekommenderar att man använder Selenium automation. |  |
| Utvecklare | jQuery UI-klientbibliotek. Adobe planerar inte att ytterligare underhålla och uppdatera jQuery UI-klientbiblioteket som levereras som en del av distributionen (QuickStart). | Adobe rekommenderar att kunder som fortfarande behöver jQuery-gränssnittet för sin kod lägger till det i sin projektkodbas. |  |
| Utvecklare | jQuery Animation-klientbibliotek (`granite.jquery.animation`). Adobe planerar inte att ytterligare underhålla och uppdatera jQuery Animation-klientbiblioteket som levereras som en del av distributionen (QuickStart). | Adobe rekommenderar att kunder som fortfarande behöver jQuery Animations för sin kod lägger till den i sin projektkodbas. |  |
| Utvecklare | Klientbibliotek för hanteringsfält. Adobe planerar inte att underhålla och uppdatera Handlebar-klientbiblioteket som levereras som en del av distributionen (QuickStart) ytterligare. | Adobe rekommenderar att kunder som fortfarande behöver `Handlebars` för sin kod lägger till den i sin projektkodbas. |  |
| Utvecklare | Advokatklientbiblioteket. Adobe planerar inte att vidare underhålla och uppdatera juristklientbiblioteket som levereras som en del av distributionen (QuickStart). | Adobe rekommenderar att kunder som fortfarande kräver att Lawndog lägger till koden i sin projektkodbas. |  |
| Utvecklare | `Granite.Sling.js`-klientbibliotek. Adobe planerar inte att ytterligare förbättra klientbiblioteket Granite.Sling.js som levereras som en del av distributionen (QuickStart). | Adobe rekommenderar att kunder som förlitar sig på att biblioteket kan koda om för att inte längre använda det. |  |
| Utvecklare | Använda YUI för att komprimera/minimera JavaScript-klientbibliotek. Adobe planerar inte att uppdatera YUI-biblioteket ytterligare. Fram till AEM 6.4 var YUI standard att miniatyrgranska JavaScript med möjlighet att växla till Google Closure Compiler (GCC). Från och med AEM 6.5 är GCC standard. | Adobe rekommenderar att man uppgraderar till AEM 6.5 för att gå över till GCC för implementering |  |
| Utvecklare | Klassisk dialogruteredigerare i CRXDE Lite. Adobe planerar inte att ytterligare förbättra den klassiska dialogruteredigeraren för användargränssnittet som levereras som en del av distributionen (QuickStart) | Det finns ingen ersättning. |  |
| Forms | AEM Forms integrering med AEM Mobile är föråldrad. | Det finns ingen ersättare. |
| Utvecklare | Klassisk dialogruteredigerare i CRXDE Lite. Adobe planerar inte att ytterligare förbättra den klassiska dialogruteredigeraren för användargränssnittet som levereras som en del av distributionen (QuickStart) | Det finns ingen ersättning. |  |
| Utvecklare | Klientbibliotek med Lodash/underscore. Adobe planerar inte att ytterligare underhålla och uppdatera Lodash-/understreckklientbiblioteket som levereras som en del av distributionen (QuickStart). | Adobe rekommenderar att kunder som fortfarande behöver Lodash/underscore för sin kod lägger till den i sin projektkodbas. |  |

## Borttagna funktioner {#removed-features}

I det här avsnittet visas funktioner som har tagits bort från AEM 6.5. Tidigare versioner hade dessa funktioner markerats som föråldrade.

| Område | Funktion | Ersättning | Version (SP) |
|--- |--- |--- |--- |
| Commerce | AEM CIF Classic har tagits bort. | Du bör migrera till [AEM CIF](/help/commerce/cif/migration.md). Om du fortfarande behöver CIF Classic har ett kompatibilitetspaket skapats, [kontakta Adobe kundsupport](https://experienceleague.adobe.com/sv?support-solution=General#support). | 6.5.22.0 |
| Integrering med [!DNL Experience Cloud] | Du kan synkronisera dina resurser med [!DNL Experience Cloud] genom att konfigurera via [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] kallades tidigare [!DNL Adobe Experience Cloud]. | [Kontakta Adobe kundsupport](https://experienceleague.adobe.com/sv?support-solution=General#support) om du har frågor. |  |
| Analytics Activity Map | Den version av Activity Map som ingår i AEM. | På grund av säkerhetsändringar i Adobe Analytics API är det inte längre möjligt att använda den version av Activity Map som ingår i AEM. Använd plugin-programmet [ActivityMap från Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=sv-SE). |  |
| Integreringar | ExactTarget-integrering har tagits bort från standarddistributionen (Quickstart) och är inte längre tillgänglig. | Ingen ersättning. |  |
| Integreringar | Integreringen av Salesforce Force API har tagits bort från standarddistributionen (Quickstart) och är nu ett extra paket att installera från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | Funktionen är fortfarande tillgänglig. |
| Forms | Stöd för Bridge-tjänsten Adobe Central Migration har tagits bort eftersom Adobe Central inte längre stöds. | Ingen ersättning. |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Ingen ersättning. |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Ingen ersättning |  |
| Forms | Uppgradering från LiveCycle ES4 SP1 till AEM 6.5 Forms på JEE är inte tillgänglig | Se [tillgängliga uppgraderingssökvägar](../forms/using/upgrade.md) i uppgraderingsdokumentationen för AEM Forms. |  |
| Forms | UPD-baserat klusterstöd har tagits bort från AEM Forms på JEE | Du kan bara använda TCP-baserad klustring i AEM Forms på JEE. Om du uppgraderar en UDP-multicast-server från en tidigare version till AEM 5.5 Forms på JEE utförs manuella konfigurationer för att växla till TCP-baserad gemfire-klustring. Mer information finns i [Uppgradera till AEM 6.5-formulär på JEE](../forms/using/upgrade-forms-jee.md) |  |
| Utvecklare | Firebug Lite har tagits bort från standarddistributionen (Quickstart) | Använd de inbyggda webbläsarkonsolerna för utvecklare |
| Utvecklare | Ta bort stöd för `customJavaScriptPath` i HTML Client Library Manager. | Ingen ersättning |  |
| [!DNL Assets] | Funktionen för avlastning av resurser har tagits bort i [!DNL Adobe Experience Manager] 6.5. | Det finns ingen ersättning. |  |
| Cache | `system/console/slingjsp` har tagits bort och är inte längre tillgänglig i AEM 6.5. | Klasser och något cacheminne lagras under paketet Apache Sling Commons FileSystem ClassLoader. Du kan kontrollera paketnumret i AEM webbkonsol och ta bort cachemappen direkt från filsystemet (`crx-quickstart/launchpad/felix/bundle<ID>`). |  |
| Screens | Aktiveringsq bundle support och relaterade konfigurationer har tagits bort. |  |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
