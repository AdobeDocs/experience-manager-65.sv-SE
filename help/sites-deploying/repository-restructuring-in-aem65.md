---
title: Omstrukturering av lager i AEM 6.5
seo-title: Omstrukturering av lager i AEM 6.5
description: Läs om omstruktureringen av databasen i AEM 6.5
seo-description: Läs om omstruktureringen av databasen i AEM 6.5
uuid: bc577c82-3279-4ddd-898c-607864868db0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 274a7f5a-d509-4ca9-9ae5-30e48f34f171
docset: aem65
redirecttarget: /content/help/en/experience-manager/6-5/help/sites-deploying/repository-restructuring.html
translation-type: tm+mt
source-git-commit: bd0dc09ea230416ad3544d14440b7b74b80ec406

---


# Omstrukturering av lager i AEM 6.5 {#repository-restructuring-in-aem}

## Introduktion {#introduction}

Före AEM 6.5 driftsattes kundkoden i oförutsägbara områden av JCR som kunde ändras vid uppgraderingar. Därför var det vanligt att formella AEM-versioner (huvudversioner, funktionspaket, Service Pack eller programfixar) skriver över anpassad kod, konfiguration eller innehåll. Dessutom skriver kundens ändringar ibland över AEM-produktkoden eller -innehållet, vilket bryter mot produktfunktionaliteten.

Konflikterna kunde inte alltid lösas automatiskt, vilket krävde lång bearbetningstid att flagga och att mänsklig intervention krävdes för att lösa dem, och lösningen var inte alltid tydlig. Genom att tydligt definiera hierarkier för AEM-produktkod och kundkod kan dessa konflikter undvikas.

Med början i AEM 6.5 och som kommer att fortsätta i framtida versioner struktureras innehållet därför ut ur `/etc` till andra mappar i databasen, tillsammans med riktlinjer om vilket innehåll som ska placeras, enligt följande högnivåregler:

* AEM-produktkoden placeras alltid i `/libs`, som inte får skrivas över av anpassad kod
* Anpassad kod ska placeras i `/apps`, `/content`och `/conf`

Den här artikeln är uppdelad i tre avsnitt, som representerar den typ av innehåll som har flyttats bort från `/etc`:

1. Konfiguration
1. Klientbibliotek
1. Övrigt

Varje avsnitt innehåller:

* en tabell med omstrukturerade platser och extra sammanhang. Inom den närmaste framtiden förväntas tabellerna formateras till en smidigare struktur för förbättrad läsbarhet.
* en utökningsstrategi som tillåter anpassad kod att utöka AEM-programkod som finns under `/libs`.

## Bakåtkompatibilitet {#backwards-compatibility}

I de flesta fall bibehålls bakåtkompatibilitet till de gamla platserna efter uppgradering till AEM 6.5. Detta uppnås genom att de gamla platserna bevaras och respekteras av produktkoden, utöver de nya platserna som läggs till. I de flesta fall används villkorsstyrd logik för att kontrollera om den äldre mappen finns och för att läsa innehåll därifrån i stället för den nya platsen.

Efter uppgraderingen till version 6.5 uppmuntras kunderna att ta bort de gamla platserna så att innehållet på de nya platserna används. Tabellerna nedan innehåller anvisningar om hur du följer den nya innehållsstrukturen per plats.

>[!NOTE]
>
>En uppgraderad instans på plats kommer att innehålla gamla innehållsplatser förutom de nya platserna. En ny utvecklarinstallation innehåller endast de nya platserna.

## Läs tabellerna {#how-to-read-the-tables}

Tabellen i varje avsnitt innehåller följande:

* den AEM-lösning (Sites, Assets, Forms, etc.) för vilken det här innehållet är relevant
* den gamla platsen (6.4 och tidigare)
* den nya platsen 6.5
* Instruktioner för anpassning till den nya innehållsstrukturen. Det kan till exempel vara nödvändigt att köra ett skript eller flytta filer manuellt under veckorna eller månaderna efter en uppgradering av version 6.5
* Den metod som AEM har använt för att underhålla bakåtkompatibilitet för gamla innehållsplatser för kunder som uppgraderar till AEM 6.5 från en tidigare version

## Konfiguration {#configuration}

Innehållsplatserna i det här avsnittet avser vanligtvis innehåll som finns under en `/settings` mapp under `/libs`, `/apps`eller `/conf`.

### Utbyggbarhetsstrategi {#extensibility-strategy}

I allmänhet, men med några få undantag, kan innehållet i det här avsnittet utökas med hjälp av funktionen Kontextmedveten konfiguration [ i Apache Sling](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) .

Med Kontextmedveten konfiguration kan innehåll i en del av databasen överlappas flera gånger av innehåll i andra delar av databasen. Innehåll i `/libs` kan till exempel överlappas av innehåll i `/apps`, som sedan kan överlappas av innehåll i `/conf`. Innehåll i en global mapp under `/conf` kan dessutom överlappas av en specifik&quot;klient&quot; eller&quot;plats&quot; (t.ex. `/conf/we-retail/settings`).

Vanligtvis används Kontextmedveten konfiguration som en strategi för att utöka funktionskonfigurationer, men det finns fall där den används av andra innehållstyper.

Tabellen nedan innehåller en extra kolumn med namnet&quot;Konfigurationstyp&quot; som förklarar i vilken utsträckning en konfiguration kan överlappas. Här finns mer information om dessa konfigurationstyper:

**inte kontextmedveten**

* Resurser råkar befinna sig i kontextmedvetna mappstrukturer (som `/libs/settings`), men refereras alltid via absolut sökväg så att kontextmedvetenhet inte används.
* Resurserna kan vara var som helst. Resurser-DRM-licenser kan till exempel vara `/content/my-customer/licenses/creative-commons.html`
* Exempel:

   * Arbetsflödesskript -> `/apps/settings/workflow/scripts/noop.ecma`
   * Resurser - DRM-licenser -> `/apps/settings/dam/drm/my-license`

**endast global**

* Funktion med endast global konfiguration
* Som referenspunkt bör du ange inställningarna i det här exemplet: `/libs/settings` &lt; `/apps/settings` &lt; `/conf/global`

* AEM har endast stöd för global konfiguration och inte för konfigurationer som är anpassade för innehavare
* AEM börjar alltid söka efter konfigurationer på /conf/global nivå först

* Exempel:

   * Starta arbetsflöden -> `/libs/settings/workflow/launcher`
   * Arbetsflödesmodeller -> `/conf/global/settings/workflow/models`

**innehavarmedveten**

* Information om konfigurationer som är kompatibla med innehavare finns i det här exemplet om prioriteten för konfigurationssökvägar: `/libs/settings` &lt; `/apps/settings` &lt; `/conf/global` &lt; `/conf/we-retail`, där vi-retail är innehavarens namn. Innehavarmedvetna konfigurationer har även stöd för underinnehavare.

* AEM stöder tenantiserade konfigurationer. Egenskapen för hierarkin respekteras `cq:conf`
* Exempel:

   * Redigerbara mallar -> `/conf/we-retail/settings/wcm/templates`
   * Molnkonfigurationer -> `/conf/we-retail/settings/cloudsettings`

<table>
 <tbody>
  <tr>
   <td><strong>Lösning</strong></td>
   <td><strong>Föregående plats</strong><br /> </td>
   <td><strong>Ny plats</strong></td>
   <td><strong>Kontextmedveten konfigurationstyp</strong><br /> </td>
   <td><strong>Bakåtkompatibilitetsmetod</strong></td>
   <td><strong>Krav för anpassning till den senaste modellen</strong></td>
  </tr>
  <tr>
   <td>AEM Sites/AEM Forms</td>
   <td><p><code>/etc/cloudservices/typekit</code></p> <p><code>/etc/cloudservices/recaptcha</code></p> <p><code>/etc/cloudservices/echosign</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/typekit</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/recaptcha</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/echosign</code></p> </td>
   <td>innehavarmedveten</td>
   <td><p>Gamla molntjänster.</p> <p>Uppgradera på plats. Kod för att lista och läsa dem finns fortfarande i AEM som reserv.</p> </td>
   <td>Verktyget för Lazy-innehållsmigrering kan aktiveras av användargränssnittet för formulärmigrering för automatisk konvertering till den nya sökvägen.<br /> </td>
  </tr>
  <tr>
   <td>AEM-formulär</td>
   <td><code>/etc/cloudservices/fdm</code></td>
   <td><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/fdm</code></td>
   <td>innehavarmedveten</td>
   <td><p>Gamla molntjänster.</p> <p>Upprätthålls på en uppgraderad installation på plats. Kod för att lista och läsa dem finns fortfarande i AEM som reserv.</p> </td>
   <td>Verktyget för Lazy-innehållsmigrering kan aktiveras av användargränssnittet för formulärmigrering för automatisk konvertering till den nya sökvägen.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/adhocassetshare</code></td>
   <td><code>/libs/settings/dam/adhocassetshare</code></td>
   <td>innehavarmedveten</td>
   <td>Äldre innehållsstrukturer får högre prioritet än nya, OTB.</td>
   <td>Anpassningar på projektnivå måste klippas ut och klistras in i motsvarande <code>/apps</code> eller <code>/conf</code> tillämpliga sökvägar.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
   <td><code>/libs/settings/dam/workflow</code></td>
   <td>innehavarmedveten</td>
   <td>Äldre innehållsstrukturer får högre prioritet än nya, OTB.</td>
   <td>Anpassningar på projektnivå måste klippas ut och klistras in i motsvarande <code>/apps</code> eller <code>/conf</code> tillämpliga sökvägar.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/drm/licenses/</code></td>
   <td><code>/libs/settings/dam/drm</code></td>
   <td>inte kontextmedveten</td>
   <td>Äldre innehållsstrukturer får högre prioritet än nya, OTB.</td>
   <td>Anpassningar på projektnivå måste klippas ut och klistras in i motsvarande <code>/apps</code> eller <code>/conf</code> tillämpliga sökvägar.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/indesign/scripts</code></td>
   <td><code>/libs/settings/dam/indesign</code></td>
   <td>innehavarmedveten</td>
   <td>Äldre innehållsstrukturer får högre prioritet än nya, OTB.</td>
   <td><p>Anpassningar på projektnivå måste klippas ut och klistras in under motsvarande <code>/apps</code> eller <code>/conf</code> tillämpliga sökvägar.</p> <p>När du kör ett anpassat arbetsflöde för tillgångsinmatning finns referenser till den gamla platsen i /etc fortfarande i processkonfigurationen för medieextrahering. Förutom att flytta skripten från /etc till motsvarande /apps- och /conf-sökvägar, måste anpassade argument för medieextraheringsprocessen ändras från absoluta till relativa sökvägar för att kunna hantera ändringarna.</p> <p>Mer information finns på <a href="https://helpx.adobe.com/experience-manager/6-2/help/assets/indesign.html">den här sidan</a>.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video</code></td>
   <td><code>/libs/settings/dam/video</code></td>
   <td>innehavarmedveten</td>
   <td>Äldre innehållsstrukturer får högre prioritet än nya, bland annat nya.</td>
   <td>Anpassningar på projektnivå måste klippas ut och klistras in i motsvarande <code>/apps</code> eller <code>/conf</code> tillämpliga sökvägar.</td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/notification/email/default</code></td>
   <td><code>/libs/settings/dam/notification</code></td>
   <td>innehavarmedveten</td>
   <td>Äldre innehållsstrukturer får högre prioritet än nya, bland annat nya.</td>
   <td>Anpassningar på projektnivå måste klippas ut och klistras in i motsvarande <code>/apps</code> eller <code>/conf</code> tillämpliga sökvägar.</td>
  </tr>
  <tr>
   <td>AEM Sites/AEM Assets</td>
   <td><code>/etc/designs</code> </td>
   <td><code>/libs/settings/wcm/designs</code></td>
   <td>inte kontextmedveten</td>
   <td><p>Konsumtionstjänster är medvetna om den gamla platsen.</p> <p>Konfigurationer från den gamla platsen beaktas</p> </td>
   <td><br /> Flytta anpassat innehåll från <code>/etc/design</code> till <code>/apps/settings/wcm/design</code> för justering med den nya databasstrukturen. I framtiden kan du överväga att uppgradera dina webbplatser till redigerbara mallfunktioner, som ersätter behovet av designläge och därmed även det här innehållet.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/scaffolding</code></td>
   <td><p><code>/libs/settings/wcm/template-types/scaffolding/scaffolding</code></p> <p><code>/apps/settings/wcm/template-types/scaffolding/scaffolding</code></p> </td>
   <td>inte kontextmedveten</td>
   <td>Komponenterna på den gamla platsen under <code>/etc/scaffolding</code> fortsätter att fungera, men har tagits bort.</td>
   <td>Adobe rekommenderar att du använder de nya skalkomponenterna under den nya platsen.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/blueprints</code></td>
   <td><p>/libs/msm för out-box-skärmar och Commerce-ritningar</p> <p> </p> </td>
   <td>inte kontextmedveten</td>
   <td><p>Förbrukningstjänster är medvetna om den gamla platsen.</p> <p>Konfigurationer från den gamla platsen beaktas.</p> </td>
   <td>Konfigurationerna måste kopieras till de nya platserna.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/mobile</code></td>
   <td><code>/libs/settings/mobile</code></td>
   <td>innehavarmedveten</td>
   <td>Funktionen utnyttjar Configuration Manager och stöder fortfarande den gamla platsen som reserv.</td>
   <td>
    <ol>
     <li>Flytta konfigurationerna från <code>/etc</code> till <code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li>Uppdatera sedan referensen i innehållet enligt följande:</li>
    </ol> <p><code>/content/&lt;tenant&gt;/jcr:content/cq:deviceGroups{String[]}=mobile/groups/responsive</code></p> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/msm/rolloutConfigs</code></td>
   <td><code>/libs/msm/wcm/rolloutconfigs</code></td>
   <td>Ej tillämpligt</td>
   <td><p>Konsumenttjänsterna är medvetna om den gamla platsen.</p> <p>Om konfigurationer identifieras på den gamla platsen används de.</p> </td>
   <td>Om du vill anpassa den till den nya modellen måste konfigurationer skapas på de nya platserna, och de gamla under <code>/etc</code> måste tas bort.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/segmentation/contexthub</code></td>
   <td><code>/conf/we-retail/settings/wcm/segments</code></td>
   <td>innehavarmedveten</td>
   <td><p>Segment från den gamla platsen:</p>
    <ul>
     <li>Behåll i skrivskyddat läge i målgruppskonsolen.</li>
     <li>Läses fortfarande in på sidan (om den angivna sökvägen är markerad i <strong>Sidegenskaper &gt; Personalisering &gt; Segmentsökväg</strong>).</li>
     <li>Kan användas för målinriktning av innehåll.</li>
    </ul> </td>
   <td>Du kan använda <a href="/help/sites-deploying/upgrading-code-and-customizations.md#migrateconfigurations">segmentmigreringsverktyget</a> för att migrera till den nya platsen.</td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/social/config/languageOpts</code></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
   <td>Ej tillämpligt</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/templates</code></td>
   <td><code>/libs/settings/community/templates</code></td>
   <td> </td>
   <td><p>Koden känner till platsen för den gamla mallen. Befintliga mallar fortsätter att refereras och läsas/skrivas från <code>/etc</code>.</p> <p><br /> Om kunden för e-postmallar redan har sina egna mallar på en annan sökväg genom att konfigurera <strong>mallens rotsökväg</strong> i <strong>AEM Communities-konfigurationen</strong> för e-postsvar, stannar den som den är.</p> </td>
   <td><p>Ett <a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration" target="_blank">migreringsverktyg</a> kan anpassas till den senaste AEM Communities-mallmodellen.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/badging</code></td>
   <td><p><strong>Badge Rules:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Badge Images:</strong></p> <p>Bilderna utanför rutan på den gamla platsen vid <code>/etc/community/badging/images</code> flyttas till <code>/libs/community/badging/images </code> </p> <p> </p> <p>Anpassade bilder flyttas till <code>/content/community/badging/images</code>.</p> <p> </p> </td>
   <td>innehavarmedveten</td>
   <td><p>Koden känner till de gamla badging-sökvägarna.</p> <p><br /> Den kontrollerar först om det finns äldre sökvägar<br /> . Om de inte finns kommer de nya banorna att användas.</p> </td>
   <td><p>Manuell migrering krävs för att anpassa sig till den senaste modellen. Följ stegen nedan för att uppnå detta:</p>
    <ol>
     <li>Skapa en platskontextbucket med hjälp av konfigurationsläsaren under <strong>Verktyg</strong></li>
     <li>Gå till platsroten</li>
     <li>Ange <code>cq:conf</code> egenskapen till den bucketsökväg där du vill lagra alla konfigurationer. Samma sak kan ställas in via <strong>Site Edit Wizard - Set Cloud Config Input</strong>, och sedan spara ändringarna</li>
     <li>Flytta relevanta regler för märkning och poängsättning från <code>etc/community/*</code> webbplatsens kontextbucket som skapades i föregående steg</li>
     <li>Justera egenskaperna <code>badgingRules</code> och <code>scoringRules</code> i platsroten så att den har relativa referenser till de nya regelplatserna. Om <code>cq:conf</code> till exempel är inställt på <code>/conf/we-retail</code>, kommer värdet för <code>badgingRules</code> att vara <code>community/badging/rules</code> om reglerna nu flyttas till den nya bucket</li>
     <li>På samma sätt kan du justera referenserna för poängregler i en nod med en badging-regel så att de har en relativ sökväg.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/cloudservices/facebookconnect</code></p> <p><code>/etc/cloudservices/twitterconnect</code></p> <p><code>/etc/cloudservices/pinterestconnect</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> </td>
   <td>innehavarmedveten</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/scoring</code></td>
   <td><code>/libs/settings/community/scoring</code></td>
   <td> </td>
   <td><p>Koden känner till de gamla badging-sökvägarna.</p> <p><br /> Den kontrollerar först om det finns äldre sökvägar<br /> . Om de inte finns kommer de nya banorna att användas.</p> </td>
   <td><p>Manuella migreringssteg krävs för att anpassa sig till den senaste modellen.</p> <p>Stegen är desamma i märkningsreglerna ovan.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/notifications</code></td>
   <td><code>/libs/settings/community/notifications</code></td>
   <td>inte kontextmedveten</td>
   <td><p>Dessa konfigurationer är inte bakåtkompatibla. I kolumnen Krav för att justeras mot den senaste modellen finns anvisningar om hur du migrerar till de nya platserna.<br /> </p> <br /> </td>
   <td><p>Manuell migrering krävs för att anpassa sig till den senaste modellen. Du kan använda konfigurationshanteraren för Begränsa för att flytta konfigurationerna till den nya sökvägen under <code>/apps/settings</code>.</p> <p>Därför måste du ange egenskapen <code>mergeList</code> till true på <code>/libs/settings/community/subscriptions</code> noden och sedan lägga till en <code>nt:unstructured</code> underordnad nod.<br /> </p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/subscriptions</code></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
   <td>inte kontextmedveten</td>
   <td>Dessa konfigurationer är inte bakåtkompatibla. I kolumnen Krav för att justeras mot den senaste modellen finns anvisningar om hur du migrerar till de nya platserna.</td>
   <td><p>Manuell migrering krävs för att anpassa sig till den senaste modellen. Du kan använda konfigurationshanteraren för Begränsa för att flytta konfigurationerna till den nya sökvägen under <code>/apps/settings</code>.</p> <p>Därför måste du ange egenskapen <code>mergeList</code> till true på <code>/libs/settings/community/subscriptions</code> noden och sedan lägga till en <code>nt:unstructured</code> underordnad nod.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/socialconfig/srpc/defaultconfiguration</code></td>
   <td><code>/conf/global/settings/community/srpc/defaultconfiguration</code></td>
   <td>globalt</td>
   <td>Dessa konfigurationer är bakåtkompatibla. Om de gamla sökvägarna identifieras kommer de att användas. Annars får de nya sökvägarna företräde.</td>
   <td><p>Aktiviteten Lazy Content Migration är tillgänglig i form av <code>CQ64CommunitiesConfigsCleanupTask</code>.</p> <p>Mer information finns i dokumentationen för <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">Lazy-migrering</a>.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/watchwords</code></td>
   <td><code>/libs/community/watchwords</code></td>
   <td>Ej tillämpligt</td>
   <td>Dessa konfigurationer är bakåtkompatibla. Om de gamla sökvägarna identifieras kommer de att användas. Annars får de nya sökvägarna företräde.</td>
   <td><p>Aktiviteten Lazy Content Migration är tillgänglig i form av <code>CQ64CommunitiesConfigsCleanupTask</code>.</p> <p>Bevakningsord måste flyttas manuellt från <code>/etc/watchwords</code> till <code>/conf/global/settings/community/watchwords</code>.</p> </td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code> </p> <p><code>/var/workflow/models</code></p> </td>
   <td>globalt</td>
   <td><p>Äldre plats används om den finns och ingen konfiguration finns i <code>/libs</code> eller <code>/conf</code>.</p> <p>När du redigerar OOTB-arbetsflödesmodeller måste du skapa kontextmedvetna övertäckningar under <code>/conf</code> för att de ska kunna ändras.</p> <p>Paketexporten måste inkludera modellen i <code>/libs</code> eller <code>/conf</code> och körningsmodellen i <code>/var/workflow/models.</code></p> </td>
   <td><p>Nya modeller skapas på <code>/conf/global/settings</code> platsen.</p> <p>Alla redigeringar i <code>/etc</code> eller <code>/libs</code> kräver att du uttryckligen skapar en åsidosättning i <code>/conf/global/settings</code> innan redigering kan göras. Knappen Redigera måste vara markerad och det gör att åsidosättningen i <code>/conf</code> skapas och redigering tillåts.</p> </td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/workflow/launcher</code></td>
   <td><p><code>/libs/settings/workflow/launcher</code></p> <p><code>/conf/global/settings/workflow/launcher</code></p> </td>
   <td>globalt</td>
   <td>Äldre plats används om den finns och det inte finns någon konfiguration<br /> i <code>/libs</code> eller <code>/conf</code> . På det här sättet bevaras anpassade startprogram.</td>
   <td><p>Nyligen skapade eller redigerade startkonfigurationer finns på <code>/conf</code> platsen.</p> <p>Alla startprogram ska flyttas från den gamla <code>/etc</code> platsen till<code> /conf/global/settings/workflow/launcher.</code></p> </td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> </td>
   <td>globalt</td>
   <td>Äldre plats används om den finns och det inte finns någon konfiguration<br /> i <code>/libs</code> eller <code>/conf</code> . På så sätt bevaras anpassade arbetsflödesmodeller.</td>
   <td><p>Alla arbetsflödesmodeller ska flyttas från den äldre <code>/etc</code> platsen till <code>/conf/global/settings/workflow/models</code>.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/workflow/notification</code></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
   <td>inte kontextmedveten</td>
   <td><p>För bakåtkompatibilitet används den äldre platsen om sådan finns.</p> <p>Tidigare var man tvungen att åsidosätta mallar som redigerades i <code>/etc</code>. Nu ska åsidosättning lagras i <code>/conf/global</code>.</p> </td>
   <td>Mer information finns i arbetsflödets dokumentation.<br /> </td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/cloudservices/translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> <p> </p> </td>
   <td>innehavarmedveten</td>
   <td>Gamla molntjänster. Bevaras på en uppgraderad installation på plats. Kod som listar dem och läser dem finns fortfarande i produkten som reserv.</td>
   <td><p>Om du vill flytta molnkonfigurationer till <code>/conf</code>kan du antingen:</p>
    <ul>
     <li>Skapa konfigurationer med det nya Touch-gränssnittet<br /> eller<br /> </li>
     <li>Kopiera konfigurationerna från <code>/etc/cloudservices/translation</code> till deras respektive nya plats(er)</li>
    </ul> <p>När detta är klart måste konfigurationerna kopplas till platser via <strong>Platser &gt; Egenskaper</strong> i användargränssnittet.</p> <p><em>Obs! Översättningsanslutningar måste vara kompatibla med AEM 6.5 för att detta ska fungera.</em></p> </td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/cloudservices/msft-translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/msft-translation</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/msft-translation</code></p> </td>
   <td>innehavarmedveten</td>
   <td>Gamla molntjänster. Bevaras på en uppgraderad installation på plats. Kod som listar dem och läser dem finns fortfarande i produkten som reserv.</td>
   <td><p>Om du vill flytta molnkonfigurationer till <code>/conf</code>kan du antingen:</p>
    <ul>
     <li>Skapa konfigurationer med det nya Touch-gränssnittet eller<br /> </li>
     <li>Kopiera äldre konfigurationer från <code>/etc/cloudservices/translation</code> till deras respektive nya platser</li>
    </ul> <p>När detta är klart måste konfigurationerna kopplas till platser via <strong>Platser &gt; Egenskaper</strong> i användargränssnittet.</p> </td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/cloudsettings</code></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
   <td>innehavarmedveten</td>
   <td><p>Befintliga poster under <code>/etc</code> finns kvar när instansen uppgraderas.</p> <p>Om du får åtkomst till användargränssnittet för molninställningarna efter uppgraderingen kopieras de befintliga molninställningarna till den nya databasstrukturen samtidigt som befintligt innehåll bevaras för bakåtkompatibilitet.</p> </td>
   <td><p>Innehållsmodellerna är desamma, bara platsen har ändrats för att passa in kontextmedvetna konfigurationer.</p> <p>Aktiviteten <a href="/help/sites-deploying/lazy-content-migration.md"></a> Lazy Migration som täcker dessa molninställningar utför följande åtgärder:</p>
    <ul>
     <li>Kopiera befintliga molninställningar i <code>/etc/cloudsettings</code> till <code>/conf/global/settings/cloudsettings</code></li>
     <li>Ta bort alla underordnade <code>/etc/cloudsettings</code></li>
    </ul> <p>Det finns dock manuella steg som krävs efter uppgraderingen och innan migreringen körs:</p>
    <ul>
     <li>Alla referenser som pekar på <code>/etc/cloudsettings/*</code> behöver uppdateras till att peka på <code>/conf/global</code></li>
    </ul> <p>Caveat:</p>
    <ul>
     <li>Behållaren <code>/etc/cloudsettings</code> måste bevaras</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
   <td>endast global</td>
   <td><p>Molnkonfiguration för Dynamic Media - Scene7 (<code>dynamicmedia_scene7</code> runmode) installeras på samma plats. Processen fungerar som den är. Om du behöver justera molnkonfigurationsvärdet finns det två alternativ:</p>
    <ol>
     <li>Uppdatera en befintlig konfiguration via det gamla molnkonfigurationsgränssnittet.</li>
     <li>Skapa en ny molnkonfiguration via det nya Touch-gränssnittet. Detta har högre prioritet än den gamla.</li>
    </ol> </td>
   <td><p>Om du vill justera till den senaste modellen måste du köra skriptet som finns på:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/viewer</code></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
   <td>endast global</td>
   <td><p>OTB-visningsförinställningarna är bara tillgängliga på den nya platsen, medan förinställningen för det anpassade visningsprogrammet fortfarande är under <code>/etc</code> tills en ändring har gjorts.</p> <p>När den har ändrats sparas den på den nya platsen via Lazy Migration. Servern för inbäddning av bilder kommer att granska både den äldre sökvägen och den nya sökvägen när en begäran tas emot. Därför behöver du inte ändra deras inbäddningskod eller URL-adress.</p> </td>
   <td><p>Visningsförinställningen som visas utanför rutan är bara tillgänglig på den nya platsen. För den anpassade visningsförinställningen måste du köra migreringsskriptet på den här platsen:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p>På samma sätt som bakåtkompatibilitetsfallet behöver du inte justera copyURL/embed-koden så att den pekar på <code>/conf</code>. Befintlig begäran om <code>/etc</code> omdirigeras under huven till rätt innehåll från <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/imageserver/macros</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
   <td>endast global</td>
   <td>Makrot under <code>/etc</code> är fortfarande giltigt. Om du ändrar den flyttas den ändrade noden till den nya platsen under <code>/conf</code> via en Lazy-migreringsaktivitet.</td>
   <td><p>Du måste köra migreringsskriptet på följande plats:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia/Adaptive Video Encoding</code></td>
   <td><code>/libs/settings/dam/dm/presets/video/jcr:content/Adaptive Video Encoding</code></td>
   <td>Ej tillämpligt</td>
   <td><p>Videoprofilen tas bort ur kartongen utan att resursmappsegenskapen uppdateras för att länka till profilen.</p> <p>Kodningsprocessen har inbyggd översättning mellan den gamla och den nya platsen. Den gamla banan konverteras så att den ser ut som den nya profilsökvägen.</p> </td>
   <td>Inga ändringar krävs.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
   <td>endast global</td>
   <td><p>Den anpassade videoprofilen bevaras tills du ändrar den.</p> <p>Sedan flyttas den till den nya platsen via en Lazy Migration-uppgift. Det liknar den färdiga videoförinställningen för kodningssökning. Kodningsprocessen har en inbyggd sökvägsöversättare som först söker efter den gamla platsen och sedan den nya platsen för videoprofilen.</p> </td>
   <td><p>Om du vill justera till den senaste modellen kan du köra migreringsskriptet under:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
   <td>endast global</td>
   <td><p>Denna molnkonfiguration för Dynamic Media-hybridinstallation (<code>dynamicmedia</code> runmode) finns kvar på samma plats. Processen fungerar som den ska. Om du behöver justera konfigurationsvärdet kan du göra det på två sätt.</p>
    <ol>
     <li>Uppdatera en befintlig konfiguration via det gamla molnkonfigurationsgränssnittet.</li>
     <li>Skapa en ny molnkonfiguration via det nya pekgränssnittet. Detta har högre prioritet än den gamla.</li>
    </ol> </td>
   <td><p>Du måste köra migreringsskriptet för att kunna anpassa dig till den senaste modellen. Du kan hitta skriptet på den här platsen:<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/youtube</code></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
   <td>endast global</td>
   <td><p>Molnkonfigurationen för DM-Youtube-installationen finns kvar på samma plats. Processen fungerar som den ska. Om du behöver justera värdet för molnkonfigurationen kan du göra det på två sätt:</p>
    <ol>
     <li>Uppdatera en befintlig konfiguration via det gamla molnkonfigurationsgränssnittet.</li>
     <li>Skapa en ny molnkonfiguration via det nya pekgränssnittet. Detta har högre prioritet än den gamla.</li>
    </ol> </td>
   <td><p>Du kan köra ett migreringsskript som justeras mot den senaste modellen. Skriptet finns på följande plats:<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/analytics</code></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
   <td>endast global</td>
   <td>Ingen åtgärd krävs.</td>
   <td><p>Du kan köra ett migreringsskript för att anpassa det till det senaste läget. Skriptet finns på följande plats:<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><p><code>/etc/notification/email/default/com.day.cq.replication</code></p> <p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
   <td><code>/libs/settings/notification-templates</code></td>
   <td>endast global</td>
   <td>Mallarna i <code>/etc/notification/email/default/</code> ges företräde framför mallarna i <code>/libs/settings/notification-templates</code>.</td>
   <td>Om du vill justera till den senaste modellen kan du skapa nya mallar under <code>/apps/settings/notification-templates</code> och göra nya ändringar där.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/msm/rolloutconfigs/launch</code></p> <p><code>/etc/msm/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td><p><code>/libs/msm/launches/rolloutconfigs/launch</code></p> <p><code>/libs/msm/launches/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td>Ej tillämpligt</td>
   <td><p>Förbrukningstjänster är medvetna om den gamla platsen.</p> <p>Om konfigurationer identifieras på den gamla platsen används de.</p> </td>
   <td>Om du vill anpassa den till den nya modellen måste konfigurationer skapas på de nya platserna, och de gamla under <code>/etc</code> måste tas bort.</td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/translation/supportedLanguages</code></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
   <td>inte kontextmedveten</td>
   <td>En grovlek är att anpassade språk måste läggas till i listan.<br /> </td>
   <td>Täck över och uppdatera den nya listan med ytterligare språk (om sådana finns). Det går också att kopiera den gamla listan till <code>/apps</code> en plats.</td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
   <td>endast global</td>
   <td>Bevaras på en uppgraderad installation. Kod som listar dem och läser dem fortfarande i produkten.</td>
   <td>Om du vill behålla ändringarna kopierar du XML-filen från <code>/etc</code> till <code>/libs</code> eller <code>/conf</code>. Du kan också<strong> </strong>ta bort filen från <code>/etc</code>.</td>
  </tr>
 </tbody>
</table>

## Klientbibliotek {#client-side-libraries}

[Klientbibliotek](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/clientlibs.html) är javascript och CSS-kod som bearbetas i webbläsaren.

### Utbyggbarhetsstrategi {#extensibility-strategy-1}

AEM tillhandahåller ett utbyggbart ramverk för att lägga till flera JavaScript-filer. Alla filer med samma kategoriegenskap läggs till så att den anpassade koden kan utöka den AEM-kod som finns under `/libs`.

<table>
 <tbody>
  <tr>
   <td><strong>Lösning</strong></td>
   <td><strong>Föregående plats</strong><br /> </td>
   <td><strong>Ny plats</strong></td>
   <td><strong>Bakåtkompatibilitetsmetod</strong></td>
   <td><strong>Krav för anpassning till den senaste modellen</strong></td>
  </tr>
  <tr>
   <td>AEM-formulär</td>
   <td><code>/etc/clientlibs/fd/fp</code></td>
   <td><code>/libs/fd/fp/components</code></td>
   <td><p>Äldre klientlib som kommer att finnas kvar i en instans som har uppgraderats via en uppgradering på plats.</p> <p>Nya clientlibs har samma kategorinamn tillsammans med egenskapen "<strong><code>replaces</code></strong>" för att undvika sammanfogning av gamla och nya clientlibs.</p> </td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>AEM-formulär</td>
   <td><code>/etc/clientlibs/fd/rte</code></td>
   <td><code>/libs/fd/rte</code></td>
   <td><p>Äldre klienter som sparas på en instans som har uppgraderats via en uppgradering på plats.</p> <p>Nya clientlibs har samma kategorinamn tillsammans med egenskapen "<strong><code>replaces</code></strong>" för att undvika sammanfogning av gamla och nya clientlibs.</p> </td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>AEM-formulär</td>
   <td><code>/etc/clientlibs/fd/af</code></td>
   <td><code>/libs/fd/af/authoring/clientlibs</code></td>
   <td>Gamla klienter. Bevaras för en instans som har uppgraderats via en uppgradering på plats. Nya clientlibs har samma kategorinamn tillsammans med egenskapen "<strong><code>replaces</code></strong>" för att undvika sammanfogning av gamla och nya clientlibs.</td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>AEM-formulär</td>
   <td><code>/etc/clientlibs/fd/themes/themeLibrary</code></td>
   <td>Detta ingår inte längre i paketet AEM 6.5.</td>
   <td><p>Slut på teman i adaptiva formulär.</p> <p>Bevaras på en uppgraderad installation.</p> </td>
   <td>Detta är delvis användargenererat innehåll. Detta levereras som ett referenspaket med <code>aem-forms-reference-themes</code> namnet.</td>
  </tr>
  <tr>
   <td>AEM-formulär</td>
   <td><code>/etc/clientlibs/fd/expeditor</code></td>
   <td><code>/libs/fd/expeditor/clientlibs</code></td>
   <td>Gamla klienter. Bevaras för en instans som har uppgraderats via en uppgradering på plats. Nya clientlibs har samma kategorinamn tillsammans med egenskapen "<strong><code>replaces</code></strong>" för att undvika sammanfogning av gamla och nya clientlibs.</td>
   <td>Ingen åtgärd krävs.<p> </p> </td>
  </tr>
  <tr>
   <td>AEM-formulär</td>
   <td><code>/etc/clientlibs/fd/fmaddon</code></td>
   <td><code>/libs/fd/fmaddon</code></td>
   <td>Äldre analyser och Target-klienter som inte ska användas direkt. </td>
   <td>Rensade efteruppgraderingen med ett rensningsfilter.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
   <td><code>/libs/dam/clientlibs</code></td>
   <td>Äldre klienter har olika kundkategorinamn.</td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td> </td>
   <td><code>/etc/clientlibs/ckeditor</code></td>
   <td><code>/libs/clientlibs/ckeditor</code></td>
   <td>Det här är äldre klienter. De kommer att finnas kvar på en uppgraderad installation. Nya klientlibs har samma kategorinamn tillsammans med egenskapen "<code>replaces</code>" för att undvika att gamla och nya klientlibs sammanfogas.</td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/sitecatalyst</code></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
   <td><p>Det här är äldre klienter. Bevaras på en uppgraderad installation.</p> <p>Nya klienter har samma kategorinamn.</p> </td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/personalization</code></td>
   <td><code>/libs/cq/personalization/clientlibs/personalization</code></td>
   <td><p>Det här är äldre klienter. Bevaras på en uppgraderad installation.</p> <p>Nya klienter har samma kategorinamn.</p> </td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/searchpromote</code></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
   <td><p>Det här är äldre klienter. Bevaras på en uppgraderad installation.</p> <p>Nya klienter har samma kategorinamn</p> </td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/target</code></td>
   <td><code>/libs/cq/target/clientlibs/target</code></td>
   <td><p>Det här är äldre klienter. Bevaras på en uppgraderad installation.</p> <p>Nya klienter har samma kategorinamn.</p> </td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/address</code></td>
   <td><code>/libs/cq/address/clientlibs</code></td>
   <td>Nya klienter har samma kategorinamn.</td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation</code></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
   <td>Gamla klienter. Bevaras på en uppgraderad installation. Nya klipp har samma kategorinamn tillsammans med egenskapen "<strong>replaces</strong>" för att undvika att gamla och nya klipp slås samman.</td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
   <td><p><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></p> </td>
   <td><p>Vid en uppgradering på en plats kommer den äldre filen (/etc/clientlibs/wcm/..._) att finnas kvar och inte tas bort automatiskt. Därför kommer referenser till den gamla /etc/clientlibs/wcm/foundation/grid/grid_base.less att fortsätta att vara stelnade.</p> <p><em>Observera att filen är ett avvikande fall där den här LESS-filen refereras av den absoluta sökvägen via LESS @import-satser och INTE av clientlib-kategorin.</em></p> <p>Om kunden LESS refererar till "grid_base.less" pekar på en fil som inte finns, kommer läget Redigerbar malllayout att avbrytas och eventuella justeringar som görs med den kommer inte att finnas (dvs. alla komponenter blir hela sidbredden).</p> </td>
   <td>Uppdatera alla referenser i anpassad kod (t.ex. i LESS-filer som refererar till den flyttade filen grid_base.less) så att de pekar på den nya platsen och tar bort den gamla platsen.</td>
  </tr>
 </tbody>
</table>

Det här är andra omstruktureringar som inte faller under de föregående avsnitten.

### Utbyggbarhetsstrategi {#extensibility-strategy-2}

Se varje tabellrad för en utökningsmodell som stöds. Innehållet i det här avsnittet utökas vanligtvis inte.

## Övrigt {#miscellaneous}

<table>
 <tbody>
  <tr>
   <td><strong>Lösning</strong></td>
   <td><strong>Föregående plats</strong><br /> </td>
   <td><strong>Ny plats</strong></td>
   <td><strong>Bakåtkompatibilitetsmetod</strong></td>
   <td><strong>Krav för anpassning till den senaste modellen</strong></td>
  </tr>
  <tr>
   <td>AEM-formulär</td>
   <td><code>/etc/designs/fd/fp</code></td>
   <td><code>/libs/fd/fp</code></td>
   <td><p>Äldre OOTB-mallar för AEM Forms-portalen. Mallarna finns kvar i /etc efter en uppgraderad installation på plats.</p> <p>I malllistan läggs ordet<em> "ersatt</em>" till i malltiteln för att skilja dem från de nyare mallarna.</p> </td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>AEM-formulär</td>
   <td><code>/etc/aep</code></td>
   <td><code>/var/fd/content/annotations</code></td>
   <td>Äldre Correspondence Management-anteckningsfiler. Inte avsedd att konsumeras direkt. Rensas efter uppgraderingen med ett rensningsfilter.</td>
   <td>Tidigare plats rensad efter uppgradering med ett rensningsfilter.</td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/tags</code></td>
   <td><code>/content/cq:tags</code></td>
   <td>Tagghanterarens API har stöd för både den gamla och den nya platsen. När JCR Tag Manager Factory OSGi Component startas, identifieras om den körs på en uppgraderad eller äldre instans och använder rätt plats.<br /> </td>
   <td><p>För att den nya modellen ska kunna justeras korrekt:</p>
    <ol>
     <li>Ersätt referenserna till den gamla modellen (<code>/etc/tags</code>) med den nya (<code>/content/cq:tags</code>) med <code>tagID.</code></li>
     <li>Logga in på CRXDE Lite</li>
     <li>Flytta taggarna från <code>/etc/tags</code> till <code>/content/cq:tags</code></li>
     <li>Starta om OSGi-komponenten <code class="code">com.day.cq.tagging.impl.JcrTagManagerFactoryImpl.
        </code></li>
    </ol> <p> </p> </td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>Äldre plats som används vid bearbetning av arbetsflöden under<br /> flygning. Nya arbetsflöden använder den nya platsen i <code>/var.</code></td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/workflow/scripts</code></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
   <td><p>Befintliga arbetsflödesmodellsteg som refererar till arbetsflödesskript på den äldre platsen på <code>/etc/workflow/scripts</code> fortsätter att peka på dessa skript efter uppgraderingen och utförs korrekt.</p> <p>Anteckna AEM-gränssnittet för redigering av arbetsflödesstegen (Process, Delningar osv.) inte längre med skript i listrutan <code>/etc/workflow/scripts</code> som används för att välja arbetsflödesskript.</p> </td>
   <td><p>Arbetsflöden som utnyttjar dessa skript fortsätter att fungera som förväntat om det associerade arbetsflödessteget inte redigeras i AEM.</p> <p>För fullständig bakåtkompatibilitet, inklusive när stegen redigeras, krävs dock manuell åtgärd från kundens sida efter uppgraderingen:</p>
    <ul>
     <li>Skripten måste flyttas från <code>/etc/workflow/scripts</code> till <code>/apps/workflow/scripts.</code></li>
     <li>Alla<strong> </strong>referenser till <code>/etc/workflow/scripts</code> i arbetsflödesmodellsteg måste uppdateras för att referera till den nya <code>/apps/workflow/scripts</code> platsen.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/replication/treeactivation</code></td>
   <td><code>/libs/replication/treeactivation</code></td>
   <td>Verktygssidan ClassicUI finns kvar vid uppgraderingen.</td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/jobs</code></td>
   <td><code>/var/dam/jobs</code></td>
   <td><p>Tillfällig plats för ZIP-filer som har genererats för att AEM Assets-hämtningsåtgärden ska anropas.</p> <p>Det finns ingen anledning att uppdatera eftersom när klienten begär att få ladda ned resursen genereras filen på den nya platsen.</p> </td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/products</code></td>
   <td><code>/var/commerce/products</code></td>
   <td><p>Det gamla innehållet finns kvar på plats och kan användas efter uppgraderingen.</p> <p>En Lazy Migration-uppgift tillhandahålls för migrering till den nya platsen.</p> </td>
   <td><p>Migreringen utförs via en Lazy Migration-uppgift: <code>CQ64CommerceMigrationTask.</code></p> <p>Följande steg utförs:</p>
    <ul>
     <li>Justerar referenser från den gamla platsen så att de pekar på den nya platsen</li>
     <li>Flyttar innehåll från den gamla platsen till den nya</li>
     <li><p>Tar bort den gamla platsen för att till slut aktivera användningen av den nya platsen i hela systemet</p> </li>
    </ul> <p>Platserna som ska täckas av uppgiften är:</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>För större kataloger rekommenderar vi att du kör migreringsaktiviteten för e-handel separat genom att skicka följande Java-systemegenskap till AEM:</p>
    <ul>
     <li>egenskapsnamn: <code>com.adobe.upgrade.forcemigration</code></li>
     <li>egenskapsvärde: <code>com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></li>
    </ul> <p>Efter migreringen måste AEM startas om.</p> </td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/orders</code></td>
   <td><code>/var/commerce/orders</code></td>
   <td><p>Det gamla innehållet finns kvar på plats och kan användas efter uppgraderingen.</p> <p>En Lazy Migration-uppgift tillhandahålls för migrering till den nya platsen.</p> </td>
   <td>Se beskrivningen ovan för <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/collections</code></td>
   <td><code>/var/commerce/collections</code></td>
   <td><p>Det gamla innehållet finns kvar på plats och kan användas efter uppgraderingen.</p> <p>En Lazy Migration-uppgift tillhandahålls för migrering till den nya platsen.</p> </td>
   <td>Se beskrivningen ovan för <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/classifications</code></td>
   <td><code>/var/commerce/classifications</code></td>
   <td>Ingen åtgärd krävs.</td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/shipping-methods</code></td>
   <td><code>/var/commerce/shipping-methods</code></td>
   <td><p>Det gamla innehållet finns kvar på plats och kan användas efter uppgraderingen.</p> <p>En Lazy Migration-uppgift tillhandahålls för migrering till den nya platsen.</p> </td>
   <td>Se beskrivningen ovan för <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/payment-methods</code></td>
   <td><code>/var/commerce/payment-methods</code></td>
   <td><p>Det gamla innehållet finns kvar på plats och kan användas efter uppgraderingen.</p> <p>En Lazy Migration-uppgift tillhandahålls för migrering till den nya platsen.</p> </td>
   <td>Se beskrivningen ovan för <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/taskmanagement</code></td>
   <td><code>/var/taskmanagement</code></td>
   <td><p>Nya uppgifter skapas under <code>/var/taskmanagement</code></p> <p>Befintliga uppgifter på den gamla platsen visas fortfarande i AEM-inkorgen.</p> </td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/workflow/packages</code></td>
   <td><code>/var/workflow/packages</code></td>
   <td><p>AEM-paket som skapats med AEM Package Manager lagras fortfarande i <code>/etc/workflow/packages.</code></p> <p>Andra paket som skapats via AEM Sites och Workflows lagras även i<code>/var/workflow/packages.</code></p> <p>Paket som hittas i både <code>/etc/workflow/packages</code> och <code>/var/workflow/packages</code> kan fortfarande redigeras via AEM:s Package Manager. </p> </td>
   <td><p>Ingen åtgärd krävs.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>Nya arbetsflödesinstanser skapas under <code>/var</code> automatiskt.</td>
   <td>Ingen åtgärd krävs.</td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/commerce/searchpromote</code></td>
   <td><code>/var/cq/searchpromote</code></td>
   <td><p>Ny plats för Sök och Befordra feed-innehåll.</p> <p>Den gamla URL:en fortsätter att fungera och begäran vidarebefordras av ett ServletFilter till den nya platsen.</p> </td>
   <td><br /> Ingen åtgärd krävs. <br /> </td>
  </tr>
  <tr>
   <td>Alla</td>
   <td><code>/etc/dtm-hook</code></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
   <td><p>Ny plats för DTM Web-Hooks.</p> <p>Den gamla URL:en fortsätter att fungera och begäran vidarebefordras av ett ServletFilter till den nya platsen.</p> </td>
   <td><br /> Ingen åtgärd krävs. <br /> </td>
  </tr>
 </tbody>
</table>

