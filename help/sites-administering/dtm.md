---
title: Integrera med Adobe Dynamic Tag Management
seo-title: Integrating with Adobe Dynamic Tag Management
description: Läs om integrationen med Adobe Dynamic Tag Management.
seo-description: Learn about integration with Adobe Dynamic Tag Management.
uuid: cbb9f942-44e3-4cd5-b07d-4298a7a08376
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b8c7a20a-7694-4a49-b66a-060720f17dad
exl-id: 1e0821f5-627f-4262-ba76-62303890e112
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '2205'
ht-degree: 0%

---

# Integrera med Adobe Dynamic Tag Management {#integrating-with-adobe-dynamic-tag-management}

Integrera [Adobe Dynamic Tag Management](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) med AEM så att du kan använda dina dynamiska Tag Management-webbegenskaper för att spåra AEM webbplatser. Med Dynamic Tag Management kan marknadsförarna hantera taggar för datainsamling och distribuera data i olika digitala marknadsföringssystem. Använd till exempel Dynamic Tag Management för att samla in användningsdata för din AEM webbplats och distribuera data för analys i Adobe Analytics eller Adobe Target.

Innan du kan integrera måste du skapa den dynamiska Tag Management [web, egenskap](https://microsite.omniture.com/t2/help/en_US/dtm/#Web_Properties) som spårar domänen för din AEM. The [värdalternativ](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) av webbegenskapen måste konfigureras så att du kan konfigurera AEM för åtkomst till dynamiska Tag Management-bibliotek.

När du har konfigurerat integreringen behöver du inte ändra den dynamiska Tag Management-konfigurationen i AEM för att ändra distributionsverktygen och reglerna för Dynamic Tag Management. Ändringarna är automatiskt tillgängliga för AEM.

>[!NOTE]
>
>Om du använder DTM med en anpassad proxykonfiguration måste du konfigurera både HTTP-klientproxykonfigurationer eftersom vissa funktioner i AEM använder 3.x-API:erna och andra 4.x-API:er:
>
>* 3.x har konfigurerats med [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x har konfigurerats med [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

## Distributionsalternativ {#deployment-options}

Följande distributionsalternativ påverkar konfigurationen av integreringen med Dynamic Tag Management.

### Dynamic Tag Management Hosting {#dynamic-tag-management-hosting}

AEM har stöd för Dynamic Tag Management som ligger i molnet eller AEM.

* Molnbaserade: De dynamiska javascript-biblioteken i Tag Management lagras i molnet och dina AEM sidor refererar direkt till dem.
* AEM: Dynamic Tag Management genererar javascript-bibliotek. AEM använder en arbetsflödesmodell för att hämta och installera biblioteken.

Vilken typ av värdtjänst implementeringen använder avgör vilka konfigurations- och implementeringsuppgifter du utför. Mer information om värdalternativ finns i [Hosting - fliken Embed](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) i Dynamic Tag Management Help.

### Mellanlagrings- och produktionsbibliotek {#staging-and-production-library}

Bestäm om AEM författarinstans använder den dynamiska Tag Management-koden för staging eller produktion.

Vanligtvis använder din författarinstans de dynamiska Tag Management-mellanlagringsbiblioteken, och produktionsinstansen använder produktionsbiblioteken. Med det här scenariot kan du använda författarinstansen för att testa ogodkända dynamiska Tag Management-konfigurationer.

Om du vill kan du använda produktionsbiblioteken i din författarinstans. Webbläsarplugin-program är tillgängliga som gör att du kan växla mellan att använda mellanlagringsbibliotek i testsyfte när biblioteken är molnbaserade.

### Använda Dynamic Tag Management Deployment Hook {#using-the-dynamic-tag-management-deployment-hook}

När AEM är värd för de dynamiska Tag Management-biblioteken kan du använda Dynamic Tag Management-tjänsten för att automatiskt överföra biblioteksuppdateringar till AEM. Biblioteksuppdateringar överförs när ändringar görs i biblioteken, till exempel när egenskaperna för den dynamiska Tag Management-webbegenskapen redigeras.

Dynamic Tag Management måste kunna ansluta till den AEM instansen som är värd för biblioteken för att kunna använda distributionspaken. Du måste [aktivera åtkomst till AEM](/help/sites-administering/dtm.md#enabling-access-for-the-deployment-hook-service) för dynamiska Tag Management-servrar.

I vissa fall kan AEM vara oåtkomliga, till exempel när AEM ligger bakom en brandvägg. I dessa fall kan du använda alternativet AEM avsökningsimporteraren för att regelbundet hämta biblioteken. Ett cron-jobbuttryck bestämmer schemat för bibliotekshämtning.

## Aktivera åtkomst för distributionsnätverkstjänsten {#enabling-access-for-the-deployment-hook-service}

Aktivera Dynamic Tag Management-tjänsten för distributionskoppling så att AEM kan uppdatera AEM bibliotek. Ange IP-adressen för dynamiska Tag Management-servrar som uppdaterar mellanlagrings- och produktionsbiblioteken efter behov:

* Mellanlagring: `107.21.99.31`
* Produktion: `23.23.225.112` och `204.236.240.48`

Utför konfigurationen med hjälp av [Webbkonsol](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) eller en [`sling:OsgiConfig`](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) nod:

* I webbkonsolen använder du Adobe DTM Deploy Hook Configuration-objektet på konfigurationssidan.
* Tjänstens-PID är för en OSGi-konfiguration `com.adobe.cq.dtm.impl.servlets.DTMDeployHookServlet`.

I följande tabell beskrivs de egenskaper som ska konfigureras.

| Egenskapen Web Console | OSGi, egenskap | Beskrivning |
|---|---|---|
| Mellanlagring DTM IP - vit lista | `dtm.staging.ip.whitelist` | IP-adressen till den Dynamic Tag Management-server som uppdaterar mellanlagringsbiblioteken. |
| Vit lista för produktionsDTM IP | `dtm.production.ip.whitelist` | IP-adressen till den dynamiska Tag Management-servern som uppdaterar produktionsbiblioteken. |

## Skapa en dynamisk Tag Management-konfiguration {#creating-the-dynamic-tag-management-configuration}

Skapa en molnkonfiguration så att den AEM instansen kan autentisera med Dynamic Tag Management och interagera med din webbegenskap.

>[!NOTE]
>
>Undvik att använda två spårningskoder från Adobe Analytics på dina sidor när din DTM-webbegenskap innehåller Adobe Analytics-verktyget och du också använder [Content Insight](/help/sites-authoring/content-insights.md). I [Adobe Analytics molnkonfiguration](/help/sites-administering/adobeanalytics-connect.md#configuring-the-connection-to-adobe-analytics)markerar du alternativet Inkludera inte spårningskod.

### Allmänna inställningar {#general-settings}

<table>
 <tbody>
  <tr>
   <th>Egenskap</th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td>API-token</td>
   <td>Värdet på API-tokenegenskapen för ditt Dynamic Tag Management-användarkonto. AEM använder den här egenskapen för autentisering med Dynamic Tag Management.</td>
  </tr>
  <tr>
   <td>Företag</td>
   <td>Det företag som ditt inloggnings-ID är kopplat till.</td>
  </tr>
  <tr>
   <td>Egenskap</td>
   <td>Namnet på webbegenskapen som du skapade för att hantera taggarna för AEM.</td>
  </tr>
  <tr>
   <td>Inkludera produktionskod på författare</td>
   <td><p>Välj det här alternativet om du vill att AEM författare och publiceringsinstanser ska använda produktionsversionen av de dynamiska Tag Management-biblioteken. </p> <p>När det här alternativet inte är markerat används mellanlagringsinställningarna för författarinstansen och produktionsinställningarna gäller för publiceringsinstansen.</p> </td>
  </tr>
 </tbody>
</table>

### Egenskaper för värdtjänster - förproduktion och produktion {#self-hosting-properties-staging-and-production}

Följande egenskaper i den dynamiska Tag Management-konfigurationen gör att AEM kan vara värd för de dynamiska Tag Management-biblioteken. Med egenskaperna kan AEM hämta och installera biblioteken. Om du vill kan du automatiskt uppdatera biblioteken så att de återspeglar ändringar som gjorts i hanteringsprogrammet för Dynamic Tag Management.

I vissa egenskaper används värden som du får från avsnittet Bibliotekshämtning på fliken Bädda in för din dynamiska Tag Management-webbegenskap. Mer information finns i [Bibliotekshämtning](https://microsite.omniture.com/t2/help/en_US/dtm/#Library_Download) i Dynamic Tag Management Help.

>[!NOTE]
>
>När du är värd för det dynamiska Tag Management-paketet AEM måste bibliotekshämtning vara aktiverat i Dynamic Tag Management innan du skapar konfigurationen. Akamai måste också vara aktiverat eftersom Akamai innehåller bibliotek för hämtning.

När du har de dynamiska Tag Management-biblioteken AEM konfigurerar AEM automatiskt vissa egenskaper för webbegenskapen enligt din konfiguration. Se beskrivningarna i följande tabell.

<table>
 <tbody>
  <tr>
   <th>Egenskap</th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td>Använd värdtjänst</td>
   <td>Välj när du har den dynamiska Tag Management-biblioteksfilen AEM. Om du väljer det här alternativet visas de andra egenskaperna i tabellen.</td>
  </tr>
  <tr>
   <td>DTM-paket-URL</td>
   <td>Den URL som ska användas för att hämta det dynamiska Tag Management-biblioteket. Hämta det här värdet från delen Hämta URL:er på sidan Bibliotekshämtning i Dynamic Tag Management. Av säkerhetsskäl måste det här värdet konfigureras manuellt.</td>
  </tr>
  <tr>
   <td>Hämta arbetsflöde</td>
   <td><p>Arbetsflödesmodellen som ska användas för att hämta och installera det dynamiska Tag Management-biblioteket. Standardmodellen är DTM Bundle Download. Använd den här modellen om du inte har skapat en anpassad modell.</p> <p>Standardarbetsflödet för hämtning aktiverar automatiskt biblioteken när de hämtas.</p> </td>
  </tr>
  <tr>
   <td>Domäntips</td>
   <td><p>(Valfritt) Domänen för den AEM servern som är värd för det dynamiska Tag Management-biblioteket. Ange ett värde för att åsidosätta standarddomänen som konfigurerats för <a href="/help/sites-developing/externalizer.md">Day CQ Link Externalizer-tjänst</a>.</p> <p>Vid anslutning till Dynamic Tag Management använder AEM det här värdet för att konfigurera mellanlagrings-HTTP-sökvägen eller Production HTTP-sökvägen för bibliotekets hämtningsegenskaper för den dynamiska Tag Management-webbegenskapen.</p> </td>
  </tr>
  <tr>
   <td>Tips för säker domän</td>
   <td><p>(Valfritt) Domänen för den AEM servern som är värd för det dynamiska Tag Management-biblioteket via HTTPS. Ange ett värde för att åsidosätta standarddomänen som konfigurerats för <a href="/help/sites-developing/externalizer.md">Day CQ Link Externalizer-tjänst</a>.</p> <p>När AEM är ansluten till Dynamic Tag Management används det här värdet för att konfigurera HTTPS-sökvägen för mellanlagring eller HTTPS-sökvägen för bibliotekets hämtningsegenskaper för den dynamiska Tag Management-webbegenskapen.</p> </td>
  </tr>
  <tr>
   <td>Delad hemlighet</td>
   <td><p>(Valfritt) Den delade hemlighet som ska användas för dekryptering av nedladdningen. Hämta det här värdet från fältet Delad hemlighet på sidan Bibliotekshämtning i Dynamic Tag Management.</p> <p><strong>Obs!</strong> Du måste ha <a href="https://www.openssl.org/docs/apps/openssl.html">OpenSSL</a> bibliotek som är installerade på den dator där AEM är installerat så att AEM kan dekryptera de hämtade biblioteken.</p> </td>
  </tr>
  <tr>
   <td>Aktivera avsökningsimporteraren</td>
   <td><p>(Valfritt) Välj att regelbundet hämta och installera det dynamiska Tag Management-biblioteket för att vara säker på att du använder en uppdaterad version. När detta är markerat skickar inte Dynamic Tag Management HTTP-POST-begäranden till Distribuera hook-URL:en.</p> <p>AEM konfigurerar automatiskt egenskapen Distribuera URL för hook i bibliotekets hämtningsegenskaper för den dynamiska Tag Management-webbegenskapen. När du väljer det här alternativet konfigureras egenskapen utan värde. Om du inte väljer det här alternativet konfigureras egenskapen med URL:en för din dynamiska Tag Management-konfiguration.</p> <p>Aktivera avsökningsimporteraren när Dynamic Tag Management-distributionkroken inte kan ansluta till AEM, till exempel när AEM ligger bakom en brandvägg.</p> </td>
  </tr>
  <tr>
   <td>Schemalägg uttryck</td>
   <td>(Visas och krävs när Aktivera avsökningsimporterare är markerat.) Ett cron-uttryck som styr när de dynamiska tagghanteringsbiblioteken hämtas.</td>
  </tr>
 </tbody>
</table>

![chlimage_1-352](assets/chlimage_1-352.png)

### Egenskaper för molntjänster - förproduktion och produktion {#cloud-hosting-properties-staging-and-production}

Du konfigurerar följande egenskaper för din dynamiska Tag Management-konfiguration när Dynamic Tag Configuration är molnbaserad.

<table>
 <tbody>
  <tr>
   <th>Egenskap</th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td>Använd värdtjänst</td>
   <td>Avmarkera det här alternativet när den dynamiska Tag Management-biblioteksfilen finns i molnet.</td>
  </tr>
  <tr>
   <td>Huvudkod</td>
   <td><p>Huvudkoden för mellanlagring som hämtas från Dynamic Tag Management för värden. Värdet fylls i automatiskt när du ansluter till Dynamic Tag Management.</p> <p> Om du vill visa koden i Dynamic Tag Management klickar du på fliken Bädda in och sedan på värdnamnet. Expandera sektionen Huvudkod och klicka på Kopiera inbäddningskod för mellanlagringsinbäddningskod eller området Produktionsinbäddningskod efter behov.</p> </td>
  </tr>
  <tr>
   <td>Sidfotskod</td>
   <td><p>Sidfotskoden för mellanlagring som hämtas från Dynamic Tag Management för värden. Värdet fylls i automatiskt när du ansluter till Dynamic Tag Management.</p> <p>Om du vill visa koden i Dynamic Tag Management klickar du på fliken Bädda in och sedan på värdnamnet. Expandera sidfotskoden och klicka på Kopiera inbäddningskod för mellanlagringsinbäddningskod eller området Produktionsinbäddningskod efter behov.</p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-353](assets/chlimage_1-353.png)

I följande procedur används det pekoptimerade användargränssnittet för att konfigurera integreringen med Dynamic Tag Management.

1. Klicka på Verktyg > Åtgärder > Moln > Cloud Service på listen.
1. I området Dynamic Tag Management visas en av följande länkar för att lägga till en konfiguration:

   * Klicka på Konfigurera nu om det här är den första konfigurationen som du lägger till.
   * Klicka på Visa konfigurationer och klicka sedan på länken + bredvid Tillgängliga konfigurationer om en eller flera konfigurationer har skapats.

   ![chlimage_1-354](assets/chlimage_1-354.png)

1. Ange en rubrik för konfigurationen och klicka sedan på Skapa.
1. I fältet API-token anger du värdet för API-tokenegenskapen för ditt Dynamic Tag Management-användarkonto.

   Kontakta DTM Client Care för att få API-tokenvärdet.

   >[!NOTE]
   >
   >API-token upphör inte att gälla förrän Dynamic Tag Management-användaren uttryckligen begär det.

   ![chlimage_1-355](assets/chlimage_1-355.png)

1. Klicka på Anslut till DTM. AEM autentiserar med Dynamic Tag Management och hämtar listan över företag som ditt konto är kopplat till.
1. Markera företaget och välj sedan den egenskap som du använder för att spåra din AEM webbplats.
1. Om du använder mellanlagringskod på författarinstansen avmarkerar du Inkludera produktionskod på författare.
1. Ange värden för egenskaperna på fliken Mellanlagringsinställningar och på fliken Produktionsinställningar om det behövs. Klicka sedan på OK.

## Hämta det dynamiska Tag Management-biblioteket manuellt {#manually-downloading-the-dynamic-tag-management-library}

Hämta de dynamiska Tag Management-biblioteken manuellt för att uppdatera dem direkt AEM. Du kan till exempel hämta manuellt när du vill testa ett uppdaterat bibliotek innan avsökningsimporteraren är schemalagd att hämta biblioteket automatiskt.

1. Klicka på Verktyg > Åtgärder > Moln > Cloud Service på listen.
1. Klicka på Visa konfigurationer i området Dynamiska Tag Management och klicka sedan på din konfiguration.
1. Klicka på knappen Trigger Download Workflow (Utlös hämtning av arbetsflöde) i området för mellanlagringsinställningar eller i området för produktionsinställningar för att hämta och distribuera bibliotekspaketet.

   ![chlimage_1-356](assets/chlimage_1-356.png)

>[!NOTE]
>
>De hämtade filerna lagras under `/etc/clientlibs/dtm/my config/companyID/propertyID/servertype`.
>
>Följande tas direkt från [DTM-konfiguration](#creating-the-dynamic-tag-management-configuration).
>
>* `myconfig`
>* `companyID`
>* `propertyID`
>* `servertype`
>

## Koppla en dynamisk Tag Management-konfiguration till din plats {#associating-a-dynamic-tag-management-configuration-with-your-site}

Koppla din dynamiska Tag Management-konfiguration till webbplatsens sidor så att AEM lägger till det nödvändiga skriptet på sidorna. Associera platsens rotsida med konfigurationen. Alla underordnade till den sidan ärver kopplingen. Om det behövs kan du åsidosätta associationen på en underordnad sida.

Använd följande procedur för att associera en sida och de underordnade med en dynamisk Tag Management-konfiguration.

1. Öppna webbplatsens rotsida i det klassiska användargränssnittet.
1. Använd Sidekick för att öppna sidegenskaperna.
1. På fliken Cloud Service klickar du på Lägg till tjänst, väljer Dynamisk Tag Management och sedan på OK.

   ![chlimage_1-357](assets/chlimage_1-357.png)

1. Använd listrutan Dynamisk Tag Management för att välja konfiguration och klicka sedan på OK.

Använd följande procedur för att åsidosätta den ärvda konfigurationsassociationen för en sida. Åsidosättningen påverkar sidan och alla underordnade sidor.

1. Öppna sidan i det klassiska användargränssnittet.
1. Använd Sidekick för att öppna sidegenskaperna.
1. På fliken Cloud Service klickar du på hänglåsikonen bredvid egenskapen Ärvd från och sedan på Ja i bekräftelsedialogrutan.

   ![chlimage_1-358](assets/chlimage_1-358.png)

1. Ta bort eller välj en annan dynamisk Tag Management-konfiguration och klicka sedan på OK.
