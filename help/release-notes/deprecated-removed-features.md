---
title: Borttagna funktioner i Adobe Experience Manager 6.5.
description: Versionsinformation om borttagna funktioner i Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 29f8e59e3fc9d3c089ee3b78c24638cd3cd2e96b
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 2%

---


# Föråldrade och borttagna funktioner {#deprecated-and-removed-features}

Adobe utvärderar ständigt produktfunktioner för att så småningom förnya eller ersätta äldre funktioner med modernare alternativ för att förbättra det totala kundvärdet, alltid med noggrant övervägande av bakåtkompatibilitet.

Följande regler gäller för att informera om den förestående borttagningen eller ersättningen av AEM-funktioner:

1. Föråldringsanmälan kommer först. Funktionerna är fortfarande tillgängliga, men har inte förbättrats ytterligare.
1. Borttagning av föråldrade funktioner sker tidigast i följande större version. Faktiskt måldatum för borttagning tillkännages.

Den här processen ger kunderna minst en releasecykel för att anpassa implementeringen till en ny version eller en efterföljare till en borttagningsfunktion, innan den faktiska borttagningen.

## Borttagna funktioner {#deprecated-features}

I det här avsnittet listas funktioner som har markerats som borttagna i AEM 6.5. I allmänhet är funktioner som ska tas bort i en framtida version först inaktuella, med ett alternativ.

Kunderna rekommenderas att granska om de använder funktionen/funktionen i den aktuella distributionen och planera för att ändra implementeringen så att den använder det alternativ som finns.

| Yta | Funktion | Ersättning |
|---|---|---|
| Integrering med Creative Cloud | AEM till Creative Cloud Mappdelning introducerades i AEM 6.2 som ett sätt för kreativa användare att få tillgång till resurser från AEM, så att de kan öppna dem i CC-program och överföra nya filer eller spara ändringar i AEM. En ny funktion i Creative Cloud-programmet, Adobe Asset Link, ger en mycket bättre användarupplevelse och kraftfullare åtkomst till resurser från AEM direkt inifrån Photoshop, InDesign och Illustrator. Adobe planerar inte att göra ytterligare förbättringar av AEM i integreringen av mappdelning i Creative Cloud. Funktionen ingår i AEM, men kunderna rekommenderas att använda ersättningslösningar. | Kunder rekommenderas att gå över till nya integreringsfunktioner i Creative Cloud, som Adobe Asset Link eller AEM-datorprogrammet. Mer information finns i Bästa praxis för integrering av AEM och Creative Cloud. |
| Assets | `AssetDownloadServlet` är inaktiverat som standard för publiceringsinstanserna. Mer information finns i [checklista](/help/sites-administering/security-checklist.md)för AEM-säkerhet. | Konfiguration som beskrivs i checklistan [för](/help/sites-administering/security-checklist.md)AEM-säkerhet. |
| Assets | Om en användare inte har tillräcklig behörighet (läs- och skrivbehörighet) `/content/dam/collections`kan användaren inte skapa en samling. | Följ användarens inställningar för åtkomstkontroll och se till att du har rätt behörigheter. |
| Adobe-Search &amp; Promote | Integreringen med Adobe Search &amp; Promote är föråldrad. Adobe planerar inte att förbättra integreringen av Search &amp; Promote ytterligare. Observera att integrering av Search &amp; Promote stöds inte alls medan den är föråldrad. |  |
| DTM-tagghanteraren | Integrationen med DTM (Dynamic Tag Manager) är föråldrad. | Växla till Adobe Experience Platform Launch som tagghanterare. |
| Adobe Target | Med möjligheten för AEM att ansluta till Adobe Target-tjänsten med hjälp av Adobe I/O-baserad Adobe Target Standard API (Rest API) i AEM 6.5 är Target Classic API (XML) föråldrat. | Konfigurera om integreringen för att [använda det nya API:t](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html). |
| Adobe Target | Användningen av den `mbox.js` baserade integrationen med Adobe Target i AEM är föråldrad. | Växla till `at.js` 1.x. |
| Handel | [CIF REST](https://github.com/adobe/commerce-cif-api) tillhandahölls 2018 som en uppsättning mikrotjänster för att möjliggöra integrering mellan AEM- och handelsmotorer. Efter att Adobe förvärvat Magento i mitten av 2018 beslutade Adobe att ändra sitt tillvägagångssätt av två skäl. Magento har en egen uppsättning Commerce API:er (REST och GraphQL) och det är inte bra att underhålla två uppsättningar API:er. Marknadstrender tyder på att kunderna var på väg mot GraphQL, eftersom det är ett effektivare sätt att fråga data. 2019 har Adobe släppt nya Commerce Integration Framework med Magento GraphQL API:er som källa för sanningen. Adobe planerar inte att göra några ytterligare investeringar i CIF REST. Vi rekommenderar starkt att man använder ersättningslösningen. | För AEM-Magento-integrationer växlar du till [AEM CIF-arkitekturen](https://github.com/adobe/aem-cif-project-archetype) och [AEM CIF Core-komponenterna](https://github.com/adobe/aem-core-cif-components). Se Integrering av AEM och Magento [med Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md). Stöd för integreringar med andra tredjepartsleverantörer (än Magento) med det nya tillvägagångssättet finns på vår färdplan. |
| Komponenter (AEM Sites) | Adobe planerar inte att göra ytterligare förbättringar av de flesta grundkomponenterna i `/libs/foundation/components`. Leta efter egenskapen `cq:deprecated` och `cq:deprecatedReason` i komponentmappen. AEM 6.5 innehåller Foundation Components, och kunder som uppgraderar från tidigare versioner kan fortsätta använda dem som de är. Foundation Components stöds också helt trots att de är inaktuella. | Adobe rekommenderar att du använder kärnkomponenterna för framtida projekt. Befintliga webbplatser kan vara som de är eller använda [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) för att omforma webbplatsen till att använda kärnkomponenter. |
| Komponenter (AEM Sites) | Komponenter för designimporteraren `/libs/wcm/designimporter/components` har markerats som borttagna från och med 6.5. Adobe planerar inte att ytterligare förbättra implementeringen av designimportören. | Adobe planerar att erbjuda en alternativ implementering av användningsexemplet i framtida versioner. |
| Foundation | Granite Offloading Framework. Adobe planerar inte att göra ytterligare förbättringar av avlastningsramverket som introducerades i CQ 5.6.1 för att externalisera materialbearbetningen. | Adobe arbetar på en ny generationens molnbaserade ramverk för avlastning. |
| Utvecklare | `Hobbes.js`. Adobe planerar inte att göra ytterligare förbättringar av testningsmiljön för `hobbes.js` användargränssnittet. | Adobe rekommenderar att kunderna använder Selenium automation. |
| Utvecklare | jQuery UI-klientbibliotek. Adobe planerar inte att ytterligare underhålla och uppdatera jQuery UI-klientbiblioteket som levereras som en del av distributionen (QuickStart) | Adobe rekommenderar att kunder som fortfarande behöver jQuery-gränssnittet för sin kod lägger till det i sin projektkodbas. |
| Utvecklare | jQuery Animation-klientbibliotek (`granite.jquery.animation`). Adobe planerar inte att ytterligare underhålla och uppdatera jQuery Animation-klientbiblioteket som levereras som en del av distributionen (QuickStart) | Adobe rekommenderar att kunder som fortfarande behöver jQuery Animations för sin kod lägger till den i sin projektkodbas. |
| Utvecklare | Klientbibliotek för hanteringsfält. Adobe planerar inte att underhålla och uppdatera Handlebar-klientbiblioteket som levereras som en del av distributionen (Quickstart) ytterligare | Adobe rekommenderar att kunder som fortfarande behöver Handlebars för sin kod lägger till den i sin projektkodbas. |
| Utvecklare | Advokatklientbiblioteket. Adobe planerar inte att vidare underhålla och uppdatera juristklientbiblioteket som levereras som en del av distributionen (Quickstart) | Adobe rekommenderar att kunder som fortfarande behöver Lawndog lägger till koden i sina projektkodbaser. |
| Utvecklare | `Granite.Sling.js` klientbibliotek. Adobe planerar inte att ytterligare förbättra klientbiblioteket Granite.Sling.js som levereras som en del av distributionen (Quickstart) | Adobe rekommenderar att kunder som förlitar sig på bibliotekets kapacitet att koda om för att inte längre använda det. |
| Utvecklare | Använda YUI för att komprimera/minimera JavaScript-klientbibliotek. Adobe planerar inte att uppdatera YUI-biblioteket ytterligare. Fram till AEM 6.4 var YUI standardinställning att minifiera JavaScript med alternativet att byta till Google Closure Compiler (GCC). Från och med AEM 6.5 är GCC standard. | Adobe rekommenderar kunder som uppgraderar till AEM 6.5 att gå över till GCC för implementering |
| Utvecklare | Klassiskt redigeringsprogram för användargränssnittsdialogrutor i CRXDE-listan. Adobe planerar inte att ytterligare förbättra den klassiska dialogruteredigeraren för användargränssnittet som levereras som en del av distributionen (QuickStart) | Det finns ingen ersättning. |
| Formulär | Integreringen av AEM Forms med AEM Mobile är föråldrad. | Det finns ingen ersättare. |

## Borttagna funktioner {#removed-features}

I det här avsnittet listas funktioner som har tagits bort från AEM 6.5. Tidigare versioner hade dessa funktioner markerats som föråldrade.

| Yta | Funktion | Ersättning |
|--- |--- |--- |
| Analytics Activity Map | Den version av Activity Map som ingår i AEM. | På grund av säkerhetsändringar i Adobe Analytics API är det inte längre möjligt att använda den version av Activity Map som ingår i AEM. Använd plugin-programmet [ActivityMap från Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |
| Integreringar | ExactTarget-integrering har tagits bort från standarddistributionen (Quickstart) och är inte längre tillgänglig. | Ingen ersättning. |
| Integreringar | Integreringen av Salesforce Force API har tagits bort från standarddistributionen (Quickstart) och är nu ett extra paket att installera från [programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | Funktionen är fortfarande tillgänglig. |
| Formulär | Stöd för tjänsten Adobe Central Migration Bridge har tagits bort eftersom Adobe Central-produkten inte längre stöds. | Ingen ersättning. |
| Formulär | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Ingen ersättning. |
| Formulär | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Ingen ersättning |
| Formulär | Uppgradering från LiveCycle ES4 SP1 till AEM 6.5 Forms on JEE är inte tillgänglig | Se [tillgängliga uppgraderingssökvägar](../forms/using/upgrade.md) i uppgraderingsdokumentationen för AEM Forms. |
| Formulär | UPD-baserat klusterstöd har tagits bort från AEM Forms på JEE | Du kan bara använda TCP-baserad klustring i AEM Forms på JEE. Om du uppgraderar en UDP-multicast-server från en tidigare version till AEM 5.5 Forms på JEE utförs manuella konfigurationer för att växla till TCP-baserad gemfire-klustring. Detaljerade instruktioner finns i [Uppgradera till AEM 6.5-formulär på JEE](../forms/using/upgrade-forms-jee.md) |
| Utvecklare | Firebug Lite har tagits bort från standarddistributionen (Quickstart) | Använd de inbyggda webbläsarkonsolerna för utvecklare |
| Utvecklare | Ta bort `customJavaScriptPath` stöd i HTML Client Library Manager. | Ingen ersättning |
| [!DNL Assets] | Funktionen för avlastning av resurser har tagits bort i [!DNL Adobe Experience Manager] 6.5. | Det finns ingen ersättning. |
| Cache | `system/console/slingjsp` är inte längre tillgängligt i AEM 6.5. | Klasser och något cacheminne lagras under paketet Apache Sling Commons FileSystem ClassLoader. Du kan kontrollera paketnumret i AEM Web Console och ta bort cachemappen direkt från filsystemet (`crx-quickstart/launchpad/felix/bundle<ID>`). |

## Förhandsmeddelande för nästa release {#pre-announcement-for-next-release}

Det här avsnittet används för att i förväg meddela kommande ändringar i framtida versioner. De förändringar som annonserats är ännu inte effektiva, men kommer att påverka kunderna. Funktionerna är till exempel inte föråldrade än, men påverkar användarna efter borttagning. Uppdateringarna tillhandahålls för planeringsändamål.

| Yta | Funktion | Meddelande |
|--- |--- |--- |
| Foundation | UI Framework | Adobe planerar att ta bort komponenterna i gränssnittet för Coral 2 under 2019. Coral UI 3 introducerades med AEM 6.2, och AEM 6.5 är helt baserat på Coral 3. Adobe rekommenderar kunder och partners som har byggt anpassade användargränssnitt med Coral 2 att ändra dem till Coral 3. Adobe tillhandahåller ett verktyg för att konvertera dialogrutor från Coral 2 till Coral 3 - [Läs mer](/help/sites-developing/dialog-conversion.md). |
