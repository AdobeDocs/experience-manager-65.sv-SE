---
title: Föråldrade och borttagna funktioner
description: Versionsinformation om borttagna och borttagna funktioner i Adobe Experience Manager 6.5.
uuid: 81d9a064-e712-4eff-bd3b-6e15513a5435
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: e8e2e01b-0117-48c3-86d8-609d29a147be
docset: aem65
translation-type: tm+mt
source-git-commit: 471b57a52efc849eb57201e6397221fa4f88c746

---


# Föråldrade och borttagna funktioner {#deprecated-and-removed-features}

Adobe utvärderar ständigt produktfunktioner för att så småningom förnya eller ersätta äldre funktioner med modernare alternativ för att förbättra det totala kundvärdet, alltid med noggrant övervägande av bakåtkompatibilitet.

Följande regler gäller för att informera om kommande borttagning/ersättning av AEM-funktioner:

1. Föråldringsanmälan kommer först. Funktioner är fortfarande tillgängliga, men de kommer inte att förbättras ytterligare.
1. Borttagning av föråldrade funktioner kommer att ske tidigast i följande större version. Faktiskt måldatum för borttagning tillkännages.

Den här processen ger kunderna minst en releasecykel för att anpassa implementeringen till en ny version eller en efterföljare till en borttagningsfunktion, innan den faktiska borttagningen.

## Föråldrade funktioner {#deprecated-features}

I det här avsnittet listas funktioner som har markerats som borttagna i AEM 6.5. I allmänhet är funktioner som ska tas bort i en framtida version först inaktuella, med ett alternativ.

Kunderna rekommenderas att granska om de använder funktionen/funktionen i den aktuella distributionen och planera för att ändra implementeringen så att den använder det alternativ som finns.

<table>
 <tbody>
  <tr>
   <td><b>Yta</b></td>
   <td><b>Funktion</b></td>
   <td><b>Ersättning</b></td>
  </tr>
  <tr>
   <td>Integrering med Creative Cloud</td>
   <td><p><a href="/help/assets/aem-cc-folder-sharing-best-practices.md">AEM till Creative Cloud Mappdelning</a> introducerades i AEM 6.2 som ett sätt för kreativa användare att få tillgång till resurser från AEM, så att de kan öppna dem i CC-program och överföra nya filer eller spara ändringar i AEM. En ny funktion i Creative Cloud-programmet, Adobe Asset Link, ger en mycket bättre användarupplevelse och kraftfullare åtkomst till resurser från AEM direkt inifrån Photoshop, InDesign och Illustrator.</p> <p>Adobe planerar inte att göra ytterligare förbättringar av AEM i integreringen av mappdelning i Creative Cloud. Funktionen ingår i AEM, men kunderna rekommenderas att använda ersättningslösningar.</p> </td>
   <td>Kunder rekommenderas att gå över till nya integreringsfunktioner i Creative Cloud, som Adobe Asset Link eller AEM-datorprogrammet. Mer information finns i Bästa praxis <a href="/help/assets/aem-cc-integration-best-practices.md">för integrering av</a> AEM och Creative Cloud.</td>
  </tr>
  <tr>
   <td>Resurser</td>
   <td>
    <ol>
     <li>AssetDownloadServlet är inaktiverat som standard för publiceringsinstanserna. Mer information finns i <a href="/help/sites-administering/security-checklist.md">checklista</a>för AEM-säkerhet.</li>
     <li>Om en användare inte har tillräcklig (läs- och skrivbehörighet) behörighet för /content/dam/collections kan användaren inte skapa en samling.</li>
    </ol> </td>
   <td>
    <ol>
     <li>Konfiguration som beskrivs i checklistan <a href="/help/sites-administering/security-checklist.md">för</a>AEM-säkerhet.</li>
     <li>Följ användarens inställningar för åtkomstkontroll och se till att du har rätt behörigheter.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Adobe Search &amp; Promote</td>
   <td><p>Integrationen med Adobe Search &amp; Promote är föråldrad.</p> <p>Adobe planerar inte att göra fler förbättringar av integrationen mellan Sök och Befordra. Observera att integrering med Sök och Befordra fortfarande stöds fullt ut när den är inaktuell.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>DTM-tagghanteraren</td>
   <td>Integrationen med DTM (Dynamic Tag Manager) är föråldrad.</td>
   <td>Växla till Adobe Experience Platform Launch som tagghanterare</td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>Med möjligheten för AEM att ansluta till Adobe Target-tjänsten med hjälp av Adobe I/O-baserat Adobe Target Standard API (Rest API) i AEM 6.5 är metoden för Target Classic API (XML) föråldrad.</td>
   <td><a href="https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html">Konfigurera om integreringen så att den använder det nya API:t</a></td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>Användningen av den mbox.js-baserade integrationen med Adobe Target i AEM är föråldrad.</td>
   <td>Växla till att använda at.js 1.x</td>
  </tr>
  <tr>
   <td>Handel</td>
   <td><p><a href="https://github.com/adobe/commerce-cif-api" target="_blank">CIF REST</a> tillhandahölls 2018 som en uppsättning mikrotjänster för att möjliggöra integrering mellan AEM- och handelsmotorer.</p> <p>Efter att Adobe förvärvat Magento i mitten av 2018 beslutade Adobe att ändra sitt tillvägagångssätt av två skäl: </p> <p><strong>1.</strong> Magento har en egen uppsättning Commerce API:er (REST och GraphQL) och det är inte bra att underhålla två uppsättningar API:er </p> <p><strong>2.</strong> Marknadstrender tyder på att kunderna var på väg mot GraphQL, eftersom det är ett effektivare sätt att fråga data. 2019 har Adobe släppt nya Commerce Integration Framework med Magento GraphQL API:er som källa för sanningen.</p> <p>Adobe planerar inte att göra några ytterligare investeringar i CIF REST. Vi rekommenderar starkt att man använder ersättningslösningen.</p> </td>
   <td><p>För AEM-Magento-integrationer växlar du till <a href="https://github.com/adobe/aem-cif-project-archetype" target="_blank">AEM CIF-arkitekturen</a>och <a href="https://github.com/adobe/aem-core-cif-components" target="_blank">AEM CIF Core-komponenterna</a></p> <p>Mer information finns i <a href="https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md" target="_blank">AEM och Magento Integration med Commerce Integration Framework</a> .</p> <p>Stöd för integreringar med andra tredjepartsleverantörer (än Magento) med det nya tillvägagångssättet finns på vår färdplan.</p> </td>
  </tr>
  <tr>
   <td>Komponenter (AEM Sites)</td>
   <td><p>Adobe planerar inte att göra ytterligare förbättringar av de flesta grundkomponenterna som lagras i /libs/foundation/components.</p> <p>Leta efter egenskapen <strong>cq:deprecated</strong> och <strong>cq:deprecatedReason</strong> i komponentmappen.</p> <p>AEM 6.5 innehåller Foundation Components, och kunder som uppgraderar från tidigare versioner kan fortsätta använda dem som de är. Foundation Components stöds även fortsättningsvis fullt ut medan de är inaktuella. </p> </td>
   <td>Kunderna rekommenderas att använda kärnkomponenterna för framtida projekt. Befintliga webbplatser kan vara som de är eller använda <a href="https://github.com/adobe/aem-modernize-tools">AEM Modernize Tools Suite</a> för att omforma webbplatsen till att använda kärnkomponenter.</td>
  </tr>
  <tr>
   <td>Komponenter (AEM Sites)</td>
   <td>Komponenter för designimporteraren /libs/wcm/designimportör/komponenter har markerats som borttagna från och med 6.5. Adobe planerar inte att ytterligare förbättra implementeringen av designimportören.</td>
   <td>Adobe planerar att tillhandahålla en alternativ implementering av användningsexemplet i framtida versioner.</td>
  </tr>
  <tr>
   <td>Komponenter (AEM Forms)</td>
   <td><p>Med signatursteget kan användare verifiera och signera ett anpassat formulär. I tidigare versioner kunde signatursteget använda både Adobe Sign- och Klottsigneringskomponenter som signaturfält. I AEM 6.5-formulär används inte längre skriptsignaturbaserad signering i Signature Step.</p> </td>
   <td>
    <ul>
     <li>Om du har gjort en ny installation:
      <ul>
       <li>Använd Adobe Sign-baserad signeringsupplevelse i ett signeringssteg i ett anpassat formulär.</li>
       <li>Använd en fristående komponent för klottersignaturer i ett adaptivt formulär, interaktiv kommunikation och HTML5-formulär.</li>
      </ul> </li>
     <li>Om du har uppgraderat från en tidigare version till AEM 6.5-formulär:<br />
      <ul>
       <li>Fortsätt att använda funktionen för signering med klottersignering i Signature Step med formulär som redan använder funktionen.<br /> </li>
       <li>Använd en fristående komponent för Klottsignering eller en Adobe Sign-baserad signeringsupplevelse i ett signeringssteg när du skapar ett nytt formulär. </li>
      </ul> </li>
    </ul> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>Foundation</td>
   <td><p>Granite Offloading Framework</p> <p>Adobe planerar inte att göra ytterligare förbättringar av avlastningsramverket som introducerades i 5.6.1 för att externalisera materialbearbetningen. </p> </td>
   <td>Adobe arbetar på en ny generationens molnbaserade ramverk för avlastning.</td>
  </tr>
  <tr>
   <td>Utvecklare</td>
   <td><p>Hobbes.js</p> <p>Adobe planerar inte att göra ytterligare förbättringar av testmiljön för användargränssnittet hobbes.js.</p> </td>
   <td>Adobe rekommenderar att kunderna använder Selenium automation.</td>
  </tr>
  <tr>
   <td>Utvecklare</td>
   <td><p>jQuery UI-klientbibliotek</p> <p>Adobe planerar inte att ytterligare underhålla och uppdatera jQuery UI-klientbiblioteket som levereras som en del av distributionen (QuickStart)</p> </td>
   <td>Adobe rekommenderar att kunder som fortfarande behöver jQuery-gränssnittet för sin kod lägger till det i sin projektkodbas.</td>
  </tr>
  <tr>
   <td>Utvecklare</td>
   <td><p>jQuery Animation-klientbibliotek (granite.jquery.animation)</p> <p>Adobe planerar inte att ytterligare underhålla och uppdatera jQuery Animation-klientbiblioteket som levereras som en del av distributionen (QuickStart)</p> </td>
   <td>Adobe rekommenderar att kunder som fortfarande behöver jQuery Animations för sin kod lägger till den i sin projektkodbas.</td>
  </tr>
  <tr>
   <td>Utvecklare</td>
   <td><p>Klientbibliotek för hanteringsfält</p> <p>Adobe planerar inte att underhålla och uppdatera Handlebar-klientbiblioteket som levereras som en del av distributionen (Quickstart) ytterligare</p> </td>
   <td>Adobe rekommenderar att kunder som fortfarande behöver Handlebars för sin kod lägger till den i sin projektkodbas.</td>
  </tr>
  <tr>
   <td>Utvecklare</td>
   <td><p>Advokatklientbibliotek</p> <p>Adobe planerar inte att vidare underhålla och uppdatera juristklientbiblioteket som levereras som en del av distributionen (Quickstart)</p> </td>
   <td>Adobe rekommenderar att kunder som fortfarande behöver Lawndog lägger till koden i sina projektkodbaser.</td>
  </tr>
  <tr>
   <td>Utvecklare</td>
   <td><p>Bibliotek för Granite.Sling.js</p> <p>Adobe planerar inte att ytterligare förbättra klientbiblioteket Granite.Sling.js som levereras som en del av distributionen (Quickstart)</p> </td>
   <td>Adobe rekommenderar att kunder som förlitar sig på bibliotekets kapacitet att koda om för att inte längre använda det.</td>
  </tr>
  <tr>
   <td>Utvecklare</td>
   <td>Använda YUI för att komprimera/minimera JavaScript-klientbibliotek. Adobe planerar inte att uppdatera YUI-biblioteket ytterligare. Fram till AEM 6.4 var YUI standardinställning att minifiera JavaScript med alternativet att byta till Google Closure Compiler (GCC). Från och med AEM 6.5 är GCC standard.</td>
   <td>Adobe rekommenderar kunder som uppgraderar till AEM 6.5 att gå över till GCC för implementering</td>
  </tr>
  <tr>
   <td>Utvecklare</td>
   <td><p>Klassiskt redigeringsprogram för användargränssnittet i CRXDE-listan</p> <p>Adobe planerar inte att ytterligare förbättra den klassiska dialogruteredigeraren för användargränssnittet som levereras som en del av distributionen (QuickStart)</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Borttagna funktioner {#removed-features}

I det här avsnittet listas funktioner som har tagits bort från AEM 6.5. Tidigare versioner hade dessa funktioner markerats som föråldrade.

| Yta | Funktion | Ersättning |
|--- |--- |--- |
| Aktivitetskarta för analyser | Den version av aktivitetskartan som ingår i AEM. | På grund av säkerhetsändringar i Adobe Analytics-API:t är det inte längre möjligt att använda den version av Activity Map som ingår i AEM. Använd plugin-programmet [ActivityMap från Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |
| Integreringar | ExactTarget-integrering har tagits bort från standarddistributionen (Quickstart) och är inte längre tillgänglig. | Ingen ersättning |
| Integreringar | Integreringen av Salesforce Force API har tagits bort från standarddistributionen (Quickstart) och är nu ett extra paket att installera från PackageShare. | Funktionen är fortfarande tillgänglig. |
| Formulär | Stöd för tjänsten Adobe Central Migration Bridge har tagits bort eftersom Adobe Central-produkten inte längre stöds. | Ingen ersättning |
| Formulär | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Ingen ersättning |
| Formulär | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Ingen ersättning |
| Utvecklare | Firebug Lite har tagits bort från standarddistributionen (Quickstart) | Använd de inbyggda webbläsarkonsolerna för utvecklare |
| Utvecklare | Ta bort `customJavaScriptPath` stöd i HTML Client Library Manager. | Ingen ersättning |
| Resurser | Funktionen för att avlasta resurser har tagits bort i AEM 6.5 | Ingen ersättning |
| Cache | `system/console/slingjsp` är inte längre tillgängligt i AEM 6.5. | Klasser och något cacheminne lagras under paketet Apache Sling Commons FileSystem ClassLoader. Du kan kontrollera paketnumret i AEM Web Console och ta bort cachemappen direkt från filsystemet (`crx-quickstart/launchpad/felix/bundle<ID>`). |

## Förhandsmeddelande för nästa release {#pre-announcement-for-next-release}

Det här avsnittet används för att i förväg meddela om ändringar i framtida versioner som inte är inaktuella, men som kommer att påverka kunderna. Dessa tillhandahålls för planeringsändamål.

| Yta | Funktion | Meddelande |
|--- |--- |--- |
| Foundation | UI Framework | Adobe planerar att ta bort komponenterna i gränssnittet för Coral 2 under 2019. Coral UI 3 introducerades med AEM 6.2, och AEM 6.5 är helt baserat på Coral 3. Adobe rekommenderar kunder och partners som har byggt anpassade användargränssnitt med Coral 2 att ändra dem till Coral 3. Adobe tillhandahåller ett verktyg för att konvertera dialogrutor från Coral 2 till Coral 3 - [Läs mer](/help/sites-developing/dialog-conversion.md). |
