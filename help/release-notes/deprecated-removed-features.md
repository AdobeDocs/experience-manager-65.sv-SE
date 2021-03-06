---
title: Borttagna funktioner i Adobe Experience Manager 6.5.
description: Versionsinformation om borttagna funktioner i Adobe Experience Manager 6.5.
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '1751'
ht-degree: 2%

---

# Föråldrade och borttagna funktioner {#deprecated-and-removed-features}

Adobe utvärderar ständigt produktfunktioner för att så småningom förnya eller ersätta äldre funktioner med modernare alternativ för att förbättra det totala kundvärdet, alltid med noggrant övervägande av bakåtkompatibilitet.

Följande regler gäller för att informera om den förestående borttagningen eller ersättningen av AEM:

1. Föråldringsanmälan kommer först. Funktionerna är fortfarande tillgängliga, men har inte förbättrats ytterligare.
1. Borttagning av föråldrade funktioner sker tidigast i följande större version. Faktiskt måldatum för borttagning tillkännages.

Den här processen ger kunderna minst en releasecykel för att anpassa implementeringen till en ny version eller en efterföljare till en borttagningsfunktion, innan den faktiska borttagningen.

## Föråldrade funktioner {#deprecated-features}

I det här avsnittet visas funktioner som har markerats som borttagna i AEM 6.5. I allmänhet är funktioner som ska tas bort i en framtida version först inaktuella, med ett alternativ.

Kunderna rekommenderas att granska om de använder funktionen/funktionen i den aktuella distributionen och planera för att ändra implementeringen så att den använder det alternativ som finns.

| Yta | Funktion | Ersättning | Version (SP) |
|---|---|---|---|
| [!DNL Sites] | Upplev fragmentegenskaper för **Status för sociala medier**. |  | 6.5.11.0 |
| [!DNL Sites] | Mallar för innehållsfragment, för att skapa enkla innehållsfragment. | [Modellbaserade strukturerade innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) nu. | 6.5.11.0 |
| Integrering med Creative Cloud | AEM till Mappdelning i Creative Cloud introducerades i AEM 6.2 som ett sätt att ge kreativa användare åtkomst till resurser från AEM, så att de kunde öppna dem i [!DNL Creative Cloud] program och ladda upp nya filer eller spara ändringar i AEM. En ny funktion i Creative Cloud, Adobe Asset Link, ger en mycket bättre användarupplevelse och kraftfullare åtkomst till AEM direkt inifrån Photoshop, InDesign och Illustrator. Adobe planerar inte att göra ytterligare förbättringar av integrationen mellan AEM och Creative Cloud Mappdelning. Funktionen ingår i AEM, men kunderna rekommenderas att använda ersättningslösningar. | Kunder rekommenderas att byta till nya integrationsfunktioner för Creative Cloud, som Adobe Asset Link eller AEM. |  |
| Assets | `AssetDownloadServlet` är inaktiverat som standard för publiceringsinstanserna. Mer information finns i [AEM](/help/sites-administering/security-checklist.md). | Konfigurationen beskrivs i [AEM](/help/sites-administering/security-checklist.md). |  |
| Resurser | Om en användare inte har tillräcklig (läs- och skrivbehörighet) behörighet för `/content/dam/collections`kan användaren inte skapa en samling. | Följ användarens inställningar för åtkomstkontroll och se till att du har rätt behörigheter. |  |
| Adobe Search &amp; Promote | Integreringen med Adobe Search &amp; Promote är föråldrad. Adobe planerar inte att göra ytterligare förbättringar av integrationen av Sök och Befordra. Observera att integrering med Sök och Befordra fortfarande stöds fullt ut när den är inaktuell. |  |  |
| DTM-tagghanteraren | Integrationen med DTM (Dynamic Tag Manager) är föråldrad. | Växla till att använda Adobe Experience Platform Launch som tagghanterare. |  |
| Adobe Target | Genom att lägga till möjligheten för AEM att ansluta till Adobe Target-tjänsten med [!DNL Adobe I/O] API (Rest API) för Adobe Target Standard i AEM 6.5 är XML-sättet (Target Classic API) föråldrat. | Konfigurera om integreringen till [använd det nya API:t](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html). |  |
| Adobe Target | Använda `mbox.js` är inte längre kompatibelt med Adobe Target i AEM. | Växla till att använda `at.js` 1.x |  |
| Handel | [CIF REST](https://github.com/adobe/commerce-cif-api) tillhandahölls 2018 som en uppsättning mikrotjänster för integrering av AEM- och handelsmotorer. Efter att Adobe förvärvat Magento i mitten av 2018 beslutade Adobe att ändra sitt tillvägagångssätt av två skäl. Magento har en egen uppsättning Commerce API:er (REST och GraphQL) och det är inte bra att behålla två uppsättningar API:er. Marknadstrender tyder på att kunderna var på väg mot GraphQL, eftersom det är ett effektivare sätt att fråga data. År 2019 har Adobe släppt det nya Commerce Integration Framework med Magento GraphQL API:er som källa för sanningen. Adobe planerar inte att göra några ytterligare investeringar i CIF REST. Vi rekommenderar starkt att man använder ersättningslösningen. | För AEM-Magento-integreringar växlar du till [AEM CIF-arkityp](https://github.com/adobe/aem-cif-project-archetype) och [AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components). Se AEM och integrering med Adobe Commerce [med Commerce Integration Framework](/help/commerce/cif/integrating/magento.md). Stöd för integreringar med andra tredje part (än Magento) med det nya tillvägagångssättet finns på vår färdplan. |  |
| Komponenter (AEM Sites) | Adobe planerar inte att göra ytterligare förbättringar av de flesta av de grundkomponenter som lagras i `/libs/foundation/components`. Leta efter `cq:deprecated` och `cq:deprecatedReason` -egenskapen i komponentmappen. AEM 6.5 innehåller Foundation Components, och kunder som uppgraderar från tidigare versioner kan fortsätta använda dem som de är. Foundation Components stöds också helt trots att de är inaktuella. | Adobe rekommenderar att du använder kärnkomponenterna för framtida projekt. Befintliga webbplatser kan förbli oförändrade eller använda [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) för att ge webbplatsen en ny funktion för att använda kärnkomponenter. |  |
| Komponenter (AEM Sites) | Komponenter i designimporteraren `/libs/wcm/designimporter/components` har markerats som borttagna från och med 6.5. Adobe planerar inte att göra ytterligare förbättringar av designimportörens implementering. | Adobe planerar att tillhandahålla en alternativ implementering av användningsexemplet i framtida releaser. |  |
| Foundation | Granite Offloading Framework. Adobe planerar inte att göra ytterligare förbättringar av avlastningsramverket som infördes i CQ 5.6.1 för att externalisera materialbearbetningen. | Adobe arbetar med nästa generations molnbaserade ramverk för avlastning. |  |
| Utvecklare | `Hobbes.js`. Adobe planerar inte att göra ytterligare förbättringar av `hobbes.js` testningsramverk för användargränssnitt. | Adobe rekommenderar att man använder Selenium automation. |  |
| Utvecklare | jQuery UI-klientbibliotek. Adobe planerar inte att ytterligare underhålla och uppdatera jQuery UI-klientbiblioteket som levereras som en del av distributionen (QuickStart) | Adobe rekommenderar att kunder som fortfarande behöver jQuery-gränssnittet för sin kod lägger till det i sin projektkodbas. |  |
| Utvecklare | jQuery Animation-klientbibliotek (`granite.jquery.animation`). Adobe planerar inte att ytterligare underhålla och uppdatera jQuery Animation-klientbiblioteket som levereras som en del av distributionen (QuickStart) | Adobe rekommenderar att kunder som fortfarande behöver jQuery Animations för sin kod lägger till den i sin projektkodbas. |  |
| Utvecklare | Klientbibliotek för hanteringsfält. Adobe planerar inte att underhålla och uppdatera Handlebar-klientbiblioteket som levereras som en del av distributionen (Quickstart) ytterligare | Adobe rekommenderar att användare som fortfarande behöver Handlebars för sin kod lägger till den i sin projektkodbas. |  |
| Utvecklare | Advokatklientbiblioteket. Adobe planerar inte att vidare underhålla och uppdatera juristklientbiblioteket som levereras som en del av distributionen (Quickstart) | Adobe rekommenderar att kunder som fortfarande kräver att Lawndog lägger till koden i sin projektkodbas. |  |
| Utvecklare | `Granite.Sling.js` klientbibliotek. Adobe planerar inte att ytterligare förbättra klientbiblioteket Granite.Sling.js som levereras som en del av distributionen (Quickstart) | Adobe rekommenderar att kunder som förlitar sig på att biblioteket kan koda om för att inte längre använda det. |  |
| Utvecklare | Använda YUI för att komprimera/minimera JavaScript-klientbibliotek. Adobe planerar inte att uppdatera YUI-biblioteket ytterligare. Fram till AEM 6.4 var YUI standardinställning för att minimera JavaScript med möjlighet att växla till Google Closure Compiler (GCC). Från och med AEM 6.5 är GCC standard. | Adobe rekommenderar att man uppgraderar till AEM 6.5 för att gå över till GCC för implementering |  |
| Utvecklare | Klassiskt redigeringsprogram för användargränssnittsdialogrutor i CRXDE-listan. Adobe planerar inte att ytterligare förbättra den klassiska dialogruteredigeraren för användargränssnittet som levereras som en del av distributionen (QuickStart) | Det finns ingen ersättning. |  |
| Forms | AEM Forms integrering med AEM Mobile är föråldrad. | Det finns ingen ersättare. |  | Utvecklare | Klassiskt redigeringsprogram för användargränssnittsdialogrutor i CRXDE-listan. Adobe planerar inte att ytterligare förbättra den klassiska dialogruteredigeraren för användargränssnittet som levereras som en del av distributionen (QuickStart) | Det finns ingen ersättning. |  |
| Utvecklare | Klientbibliotek med Lodash/underscore. Adobe planerar inte att ytterligare underhålla och uppdatera Lodash-/understreckklientbiblioteket som levereras som en del av distributionen (QuickStart) | Adobe rekommenderar att kunder som fortfarande behöver Lodash/underscore för sin kod lägger till den i sin projektkodbas. |  |

## Borttagna funktioner {#removed-features}

I det här avsnittet visas funktioner som har tagits bort från AEM 6.5. Tidigare versioner hade dessa funktioner markerats som föråldrade.

| Yta | Funktion | Ersättning | Version (SP) |
|--- |--- |--- |--- |
| Integration med [!DNL Experience Cloud] | Du kan synkronisera dina resurser med [!DNL Experience Cloud] använda en konfigurering via [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] kallades tidigare [!DNL Adobe Marketing Cloud]. | Om du har frågor [kontakta Adobe kundsupport](https://www.adobe.com/account/sign-in.supportportal.html). |  |
| Analytics Activity Map | Den version av Activity Map som ingår i AEM. | På grund av säkerhetsändringar i Adobe Analytics API är det inte längre möjligt att använda den version av Activity Map som ingår i AEM. Använd [ActivityMap-plugin från Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |  |
| Integreringar | ExactTarget-integrering har tagits bort från standarddistributionen (Quickstart) och är inte längre tillgänglig. | Ingen ersättning. |  |
| Integreringar | Integreringen av Salesforce Force API har tagits bort från standarddistributionen (Quickstart) och är nu ett extra paket att installera från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | Funktionen är fortfarande tillgänglig. |
| Forms | Stöd för tjänsten Adobe Central Migration Bridge har tagits bort eftersom Adobe Central inte längre stöds. | Ingen ersättning. |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Ingen ersättning. |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Ingen ersättning |  |
| Forms | Uppgradering från LiveCycle ES4 SP1 till AEM 6.5 Forms på JEE är inte tillgänglig | Se [tillgängliga uppgraderingssökvägar](../forms/using/upgrade.md) i uppgraderingsdokumentationen för AEM Forms. |  |
| Forms | UPD-baserat klusterstöd har tagits bort från AEM Forms på JEE | Du kan bara använda TCP-baserad klustring i AEM Forms på JEE. Om du uppgraderar en UDP-multicast-server från en tidigare version till AEM 5.5 Forms på JEE utförs manuella konfigurationer för att växla till TCP-baserad gemfire-klustring. Detaljerade anvisningar finns i [Uppgradera till AEM 6.5-formulär på JEE](../forms/using/upgrade-forms-jee.md) |  |
| Utvecklare | Firebug Lite har tagits bort från standarddistributionen (Quickstart) | Använd de inbyggda webbläsarkonsolerna för utvecklare |
| Utvecklare | Ta bort `customJavaScriptPath` stöd i HTML Client Library Manager. | Ingen ersättning |  |
| [!DNL Assets] | Funktionen för avlastning av resurser har tagits bort i [!DNL Adobe Experience Manager] 6.5. | Det finns ingen ersättning. |  |
| Cache | `system/console/slingjsp` är inte längre tillgängligt i AEM 6.5. | Klasser och något cacheminne lagras under paketet Apache Sling Commons FileSystem ClassLoader. Du kan kontrollera paketnumret i AEM webbkonsol och ta bort cachemappen direkt från filsystemet (`crx-quickstart/launchpad/felix/bundle<ID>`). |  |

## Förhandsmeddelande för nästa release {#pre-announcement-for-next-release}

Det här avsnittet används för att i förväg meddela kommande ändringar i framtida versioner. De förändringar som annonserats är ännu inte effektiva, men kommer att påverka kunderna. Funktionerna är till exempel inte föråldrade än, men påverkar användarna efter borttagning. Uppdateringarna tillhandahålls för planeringsändamål.

| Yta | Funktion | Meddelande |
|--- |--- |--- |
| Foundation | UI Framework | Adobe planerar att ta bort Coral UI 2-komponenterna under 2019. Coral UI 3 introducerades med AEM 6.2 och AEM 6.5 är helt baserat på Coral 3. Adobe rekommenderar kunder och partners som har byggt anpassade gränssnitt med Coral 2 att ändra dem till Coral 3. Adobe har ett verktyg för att konvertera dialogrutor från Coral 2 till Coral 3 - [Läs mer](/help/sites-developing/modernization-tools.md). |
