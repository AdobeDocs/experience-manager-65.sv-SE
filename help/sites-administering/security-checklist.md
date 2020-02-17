---
title: Säkerhetschecklista
seo-title: Säkerhetschecklista
description: Läs om de olika säkerhetsaspekterna när du konfigurerar och distribuerar AEM.
seo-description: Läs om de olika säkerhetsaspekterna när du konfigurerar och distribuerar AEM.
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Säkerhetschecklista {#security-checklist}

I det här avsnittet beskrivs olika åtgärder som du bör vidta för att se till att din AEM-installation är säker när den distribueras. Checklistan ska användas uppifrån och ned.

>[!NOTE]
>
>Ytterligare information [finns också om de farligaste säkerhetshot som publicerats av Open Web Application Security Project (OWASP)](https://www.owasp.org/index.php/OWASP_Top_Ten_Project).

>[!NOTE]
>
>Det finns ytterligare [säkerhetsaspekter](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) att tänka på under utvecklingsfasen.

## Viktiga säkerhetsåtgärder {#main-security-measures}

### Kör AEM i produktionsklar läge {#run-aem-in-production-ready-mode}

Mer information finns i [Köra AEM i produktionsklart läge](/help/sites-administering/production-ready.md).

### Aktivera HTTPS för transportlagersäkerhet {#enable-https-for-transport-layer-security}

Det är obligatoriskt att aktivera HTTPS-transportlagret på både författare- och publiceringsinstanser för att en säker instans ska kunna användas.

>[!NOTE]
>
>Mer information finns i avsnittet [Aktivera HTTP över SSL](/help/sites-administering/ssl-by-default.md) .

### Installera snabbkorrigeringar för säkerhet {#install-security-hotfixes}

Kontrollera att du har installerat de senaste [säkerhetsuppdateringarna från Adobe](https://helpx.adobe.com/experience-manager/kb/aem63-available-hotfixes.html).

### Ändra standardlösenord för administratörskonton för AEM- och OSGi-konsolen {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe rekommenderar att du efter installationen ändrar lösenordet för de behöriga [**AEM **-`admin`kontona](#changing-the-aem-admin-password)(i alla instanser).

Dessa konton omfattar:

* AEM- `admin` kontot

   När du har ändrat lösenordet för AEM-administratörskontot måste du använda det nya lösenordet när du använder CRX.

* Lösenordet `admin` för OSGi-webbkonsolen

   Den här ändringen kommer även att gälla för det administratörskonto som används för åtkomst till webbkonsolen, så du måste använda samma lösenord när du kommer åt det.

De här två kontona använder separata autentiseringsuppgifter och det är viktigt att ha tydliga, starka lösenord för var och en av dem för att driftsättningen ska vara säker.

#### Ändra AEM-administratörslösenordet {#changing-the-aem-admin-password}

Lösenordet för AEM-administratörskontot kan ändras via [Granite Operations - Users](/help/sites-administering/granite-user-group-admin.md) console.

Här kan du redigera `admin` kontot och [ändra lösenordet](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>Om du ändrar administratörskontot ändras även OSGi-webbkonsolens konto. När du har ändrat administratörskontot bör du ändra OSGi-kontot till något annat.

#### Viktigt att ändra lösenordet för OSGi-webbkonsolen {#importance-of-changing-the-osgi-web-console-password}

Förutom från AEM- `admin` kontot kan följande hända om du inte ändrar standardlösenordet för OSGi-webbkonsolen:

* Serverns exponering med ett standardlösenord vid start och avstängning (som kan ta minuter för stora servrar).
* Exponering av servern när databasen är avstängd/startad och OSGI körs.

Mer information om hur du ändrar lösenord för webbkonsolen finns i [Ändra administratörslösenordet](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) för OSGi-webbkonsolen nedan.

#### Ändra administratörslösenordet för OSGi-webbkonsolen {#changing-the-osgi-web-console-admin-password}

Du måste också ändra lösenordet som används för att komma åt webbkonsolen. Detta görs genom att konfigurera följande egenskaper för [Apache Felix OSGi Management Console](/help/sites-deploying/osgi-configuration-settings.md):

**Användarnamn** och **lösenord**, autentiseringsuppgifter för åtkomst till själva Apache Felix Web Management Console.
Lösenordet måste ändras efter den första installationen för att säkerställa instansens säkerhet.

Så här gör du:

1. Navigera till webbkonsolen på `<server>:<port>/system/console/configMgr`.
1. Gå till **Apache Felix OSGi Management Console** och ändra **användarnamn** och **lösenord**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. Click **Save**.

### Implementera anpassad felhanterare {#implement-custom-error-handler}

Adobe rekommenderar att du definierar anpassade felhanterarsidor, särskilt för 404- och 500 HTTP Response-koder, för att förhindra informationsexponering.

>[!NOTE]
>
>Mer information finns i [Så här skapar jag anpassade skript eller felhanterare](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html) i kunskapsbasartikeln.

### Slutför checklista för utskickssäkerhet {#complete-dispatcher-security-checklist}

AEM Dispatcher är en viktig del av din infrastruktur. Adobe rekommenderar att du slutför [säkerhetskontrolllistan](https://helpx.adobe.com/experience-manager/dispatcher/using/security-checklist.html)för dispatcher.

>[!CAUTION]
>
>Med Dispatcher måste du inaktivera &quot;.form&quot;-väljaren.

## Verifieringssteg {#verification-steps}

### Konfigurera replikerings- och transportanvändare {#configure-replication-and-transport-users}

En standardinstallation av AEM anger `admin` som användare för transportreferenser inom [standardreplikeringsagenterna](/help/sites-deploying/replication.md). Administratörsanvändaren används också för att hämta replikeringen på författarsystemet.

Av säkerhetsskäl bör båda ändras för att återspegla det aktuella användningsfallet, med följande två aspekter i åtanke:

* Administratörsanvändaren **ska inte vara** transportanvändaren. I stället anger du en användare i publiceringssystemet som bara har behörighet till de relevanta delarna av publiceringssystemet och använder användarens inloggningsuppgifter för transporten.

   Du kan starta från den paketerade replikeringsmottagaren och konfigurera den här användarens åtkomsträttigheter så att de matchar din situation

* Användaren **eller användar-ID:t** för **** replikering ska inte heller vara adminanvändare, utan en användare som bara kan se innehåll som ska replikeras. Replikeringsanvändaren används för att samla in det innehåll som ska replikeras på författarsystemet innan det skickas till utgivaren.

### Kontrollera säkerhetshälsokontrollerna för instrumentpanelen för åtgärder {#check-the-operations-dashboard-security-health-checks}

I AEM 6 introduceras den nya kontrollpanelen för åtgärder, som är avsedd att hjälpa systemansvariga att felsöka problem och övervaka hälsan för en instans.

Kontrollpanelen innehåller också en samling säkerhetskontroller. Vi rekommenderar att du kontrollerar statusen för alla säkerhetshälsokontroller innan du publicerar med produktionsinstansen. Mer information finns i dokumentationen [till](/help/sites-administering/operations-dashboard.md)kontrollpanelen för åtgärder.

### Kontrollera om exempelinnehåll finns {#check-if-example-content-is-present}

Allt exempelinnehåll och alla användare (t.ex. Geometrixx-projektet och dess komponenter) ska avinstalleras och tas bort helt i ett produktionssystem innan det görs tillgängligt för allmänheten.

>[!NOTE]
>
>Exemplet med webbprogram.Detaljhandelsprogram tas bort om den här instansen körs i [produktionsklart läge](/help/sites-administering/production-ready.md). Om så inte är fallet kan du avinstallera exempelinnehållet genom att gå till Package Manager och sedan söka efter och avinstallera alla We.Retail-paket. Mer information finns i [Arbeta med paket](package-manager.md).

### Kontrollera om det finns några CRX-utvecklingspaket {#check-if-the-crx-development-bundles-are-present}

Dessa OSGi-utvecklingspaket bör avinstalleras både på författaren och publicera produktionssystem innan de blir tillgängliga.

* Stöd för Adobe CRXDE (com.adobe.granite.crxde-support)
* Adobe Granite CRX Explorer (com.adobe.granite.crx-explorer)
* Adobe Granite CRXDE Lite (com.adobe.granite.crxde-lite)

### Kontrollera om Sling-utvecklingspaketet finns {#check-if-the-sling-development-bundle-is-present}

I [AEM Developer Tools för Eclipse](/help/sites-developing/aem-eclipse.md) distribueras installationsprogrammet för Apache Sling Tooling (org.apache.sling.tooling.support.install).

Detta OSGi-paket bör avinstalleras både på författaren och publicera produktionssystem innan de blir tillgängliga.

### Skydda mot smidning av förfrågningar på olika webbplatser {#protect-against-cross-site-request-forgery}

#### CSRF Protection Framework {#the-csrf-protection-framework}

AEM 6.1 levereras med en mekanism som hjälper till att skydda mot attacker med attacker med smidda förfrågningar mellan webbplatser, som kallas **CSRF Protection Framework**. Mer information om hur du använder programmet finns i [dokumentationen](/help/sites-developing/csrf-protection.md).

#### Sling Referer-filtret {#the-sling-referrer-filter}

För att åtgärda kända säkerhetsproblem med CSRF (Cross-Site Request Forgery) i CRX WebDAV och Apache Sling måste du lägga till konfigurationer för referensfiltret för att kunna använda det.

Refererarfiltertjänsten är en OSGi-tjänst som gör att du kan konfigurera:

* vilka http-metoder som ska filtreras
* om en tom referensrubrik tillåts
* och en vit lista över servrar som ska tillåtas utöver servervärden.

Som standard finns alla varianter av localhost och de värdnamn som servern är bunden till i den vita listan.

Så här konfigurerar du referenspunktsfiltertjänsten:

1. Öppna Apache Felix-konsolen (**konfigurationer**) på:

   `https://<server>:<port_number>/system/console/configMgr`

1. Logga in som `admin`.
1. Välj: ****

   `Apache Sling Referrer Filter`

1. I `Allow Hosts` fältet anger du alla värdar som tillåts som referent. Varje tävlingsbidrag måste ha blanketten

   &lt;protocol>://&lt;server>:&lt;port>

   Exempel:

   * `https://allowed.server:80` tillåter alla begäranden från den här servern med den angivna porten.
   * Om du även vill tillåta https-begäranden måste du ange en andra rad.
   * Om du tillåter alla portar från den servern kan du använda `0` som portnummer.

1. Markera `Allow Empty` fältet om du vill tillåta tomma eller saknade hänvisningsrubriker.

   >[!CAUTION]
   >
   >Vi rekommenderar att du skickar en referens när du använder kommandoradsverktyg som `cURL` i stället för att tillåta ett tomt värde eftersom det kan exponera systemet för CSRF-attacker.

1. Redigera de metoder som filtret ska använda för kontroller med `Filter Methods` fältet.

1. Klicka på **Spara** för att spara ändringarna.

### OSGI-inställningar {#osgi-settings}

Vissa OSGI-inställningar ställs in som standard för att underlätta felsökning av programmet. Dessa måste ändras i era publicerings- och upphovsarbetsinstanser för att undvika att intern information läcker till allmänheten.

>[!NOTE]
>
>Alla inställningar nedan förutom Dag CQ WCM-felsökningsfiltret **** för CQ omfattas automatiskt av [produktionsklart läge](/help/sites-administering/production-ready.md). Därför rekommenderar vi att du granskar alla inställningar innan du distribuerar instansen i en produktiv miljö.

För var och en av följande tjänster måste de angivna inställningarna ändras:

* [Adobe Granite HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * aktivera **Minify** (för att ta bort CRLF- och whitespace-tecken).
   * aktivera **Gzip** (för att tillåta att filer grupperas och öppnas med en begäran).
   * inaktivera **felsökning**
   * inaktivera **timing**

* [Dag CQ WCM-felsökningsfilter](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * avmarkera **Aktivera**

* [Dag CQ WCM-filter](/help/sites-deploying/osgi-configuration-settings.md):

   * endast vid publicering, ange **WCM-läge** som &quot;inaktiverat&quot;

* [Apache Sling Java Script Handler](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * inaktivera **Generera felsökningsinformation**

* [Apache Sling JSP Script Handler](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * inaktivera **Generera felsökningsinformation**
   * inaktivera **mappat innehåll**

Mer information finns i [OSGi-konfigurationsinställningar](/help/sites-deploying/osgi-configuration-settings.md).

När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. Mer information och rekommendationer finns i [Konfigurera OSGi](/help/sites-deploying/configuring-osgi.md) .

## Ytterligare läsningar {#further-readings}

### Minska DoS-attacker (Denial of Service) {#mitigate-denial-of-service-dos-attacks}

En denial of service-attack (DoS) är ett försök att göra en datorresurs otillgänglig för de avsedda användarna. Detta görs ofta genom att överbelasta resursen. till exempel:

* Med en mängd förfrågningar från en extern källa.
* Med en begäran om mer information än vad systemet kan leverera.

   Till exempel en JSON-representation av hela databasen.

* Genom att begära en innehållssida med ett obegränsat antal URL-adresser kan URL-adressen innehålla ett handtag, vissa väljare, ett tillägg och ett suffix, som alla kan ändras.

   Du kan till exempel också `.../en.html` begära följande:

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`
   Alla giltiga variationer (t.ex. returnera ett `200` svar och konfigureras att cachelagras) cachas av dispatchern, vilket till slut leder till ett fullständigt filsystem och ingen tjänst för ytterligare begäranden.

Det finns många konfigurationspunkter för att förhindra sådana attacker, här diskuterar vi bara de som är direkt relaterade till AEM.

**Konfigurera Sling för att förhindra DoS**

Sling är *innehållscentrerat*. Detta innebär att bearbetningen är inriktad på innehållet eftersom varje HTTP-begäran mappas till innehåll i form av en JCR-resurs (en databasnod):

* Det första målet är den resurs (JCR-nod) som innehåller innehållet.
* För det andra finns återgivaren, eller skriptet, från resursegenskaperna i kombination med vissa delar av begäran (t.ex. väljare och/eller tillägg).

>[!NOTE]
>
>Detta beskrivs mer ingående under [Behandling](/help/sites-developing/the-basics.md#sling-request-processing)av försäljningsbegäran.

Den här metoden gör Sling mycket kraftfull och mycket flexibel, men som alltid är det den flexibilitet som måste hanteras noggrant.

För att förhindra missbruk kan du:

1. Införliva kontroller på applikationsnivå. På grund av antalet möjliga variationer är en standardkonfiguration inte möjlig.

   I ditt program bör du:

   * Styr väljarna i programmet så att du *bara* betjänar de explicita väljarna som behövs och returnerar `404` för alla andra.
   * Förhindra utdata från ett obegränsat antal innehållsnoder.

1. Kontrollera konfigurationen av standardåtergivningsprogrammen, som kan vara ett problemområde.

   * I synnerhet JSON-renderaren som kan omvända trädstrukturen över flera nivåer.

      Exempelvis begäran:

      `http://localhost:4502/.json`

      kan dumpa hela databasen i en JSON-representation. Detta skulle orsaka allvarliga serverproblem. Därför anger Sling en gräns för antalet maximala resultat. Om du vill begränsa djupet i JSON-återgivningen kan du ange värdet för:

      **JSON Max-resultat** ( `json.maximumresults`)

      i konfigurationen för [Apache Sling GET-servern](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). När den här gränsen överskrids komprimeras återgivningen. Standardvärdet för Sling i AEM är `200`.

   * Som en förebyggande åtgärd inaktiverar du de andra standardåtergivningarna (HTML, oformaterad text, XML). Återigen genom att konfigurera [Apache Sling GET-servern](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >Inaktivera inte JSON-renderaren, vilket krävs för AEM:s normala drift.

1. Använd en brandvägg för att filtrera åtkomsten till instansen.

   * Du måste använda en brandvägg på operativsystemnivå för att filtrera åtkomst till punkter i din instans som kan leda till denial of service-attacker om den lämnas oskyddad.

**Minska mot DoS som orsakas av att formulärväljare används**

>[!NOTE]
>
>Denna begränsning bör endast utföras i AEM-miljöer som inte använder Forms.

Eftersom AEM inte tillhandahåller indexvärden för `FormChooserServlet`formuläret kommer formulärväljare i frågor att utlösa en kostsam databasövergång, vilket vanligen gör att AEM-instansen avbryts. Formulärväljare kan identifieras med **&amp;stämpeln;ast;.form.** &amp;ast; sträng i frågor.

Följ stegen nedan för att minska detta:

1. Gå till webbkonsolen genom att peka på *https://&lt;serveradress>:&lt;serverport>/system/console/configMgr*

1. Sök efter **Dag CQ WCM Form Chooser Servlet**
1. När du har klickat på posten inaktiverar du **Advanced Search Require** i följande fönster.

1. Click **Save**.

**Minska mot DoS som orsakas av hämtningstjänsten**

Med standardtjänsten för hämtning av resurser i AEM kan autentiserade användare skicka godtyckligt stora, samtidiga hämtningsbegäranden för att skapa ZIP-filer med resurser som är synliga för dem och som kan överbelasta servern och/eller nätverket.

För att minska de potentiella DoS-riskerna som orsakas av den här funktionen är `AssetDownloadServlet` OSGi-komponenten inaktiverad som standard för publiceringsinstanser i de senaste AEM-versionerna.

Om installationen kräver att hämtningsservern för resurser är aktiverad kan du läsa [den här artikeln](/help/assets/download-assets-from-aem.md) för mer information.

### Inaktivera WebDAV {#disable-webdav}

WebDAV ska vara inaktiverat i både författar- och publiceringsmiljön. Detta kan göras genom att stoppa de aktuella OSGi-paketen.

1. Anslut till **Felix Management Console** som körs på:

   `https://<*host*>:<*port*>/system/console`

   Exempel `http://localhost:4503/system/console/bundles`.

1. I listan med paket hittar du paketet:

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Klicka på stoppknappen (i åtgärdskolumnen) för att stoppa paketet.

1. I listan med paket hittar du det paket som heter:

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Klicka på stoppknappen för att stoppa det här paketet.

   >[!NOTE]
   >
   >AEM behöver inte startas om.

### Verifiera att du inte avslöjar personligt identifierbar information i användarens hemsökväg {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

Det är viktigt att du skyddar dina användare genom att se till att du inte visar någon personligt identifierbar information i databasanvändarens hemsökväg.

Sedan AEM 6.1 har sättet som användar-ID-nodnamn (kallas även auktoriseringsbara) lagras på ändrats med en ny implementering av `AuthorizableNodeName` gränssnittet. Det nya gränssnittet visar inte längre användar-ID:t i nodnamnet, utan genererar i stället ett slumpmässigt namn.

Ingen konfiguration behöver göras för att aktivera den, eftersom detta nu är standardsättet att generera auktoriserbara ID:n i AEM.

Även om det inte rekommenderas kan du inaktivera det om du behöver den gamla implementeringen för bakåtkompatibilitet med dina befintliga program. För att göra detta måste du:

1. Gå till webbkonsolen och ta bort posten** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** från egenskapen **requiredServicePids** i **Apache Jackrabbit Oak SecurityProvider**.

   Du kan också hitta Oak Security Provider genom att leta efter **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID i OSGi-konfigurationerna.

1. Ta bort konfigurationen **Apache Jackrabbit Oak Random Authorizable Node Name** OSGi från webbkonsolen.

   Observera att PID:t för den här konfigurationen är **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** för enklare sökning.

>[!NOTE]
>
>Mer information finns i dokumentationen om [autentisering av nodnamn](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### Förhindra clickjacking {#prevent-clickjacking}

För att förhindra clickjacking rekommenderar vi att du konfigurerar webbservern så att den tillhandahåller en HTTP-rubrik som är inställd på `X-FRAME-OPTIONS` `SAMEORIGIN`.

Mer [information om clickjacking finns på OWASP-webbplatsen](https://www.owasp.org/index.php/Clickjacking).

### Se till att du replikerar krypteringsnycklar korrekt vid behov {#make-sure-you-properly-replicate-encryption-keys-when-needed}

Vissa AEM-funktioner och autentiseringsscheman kräver att du replikerar dina krypteringsnycklar i alla AEM-instanser.

Innan du gör detta bör du tänka på att nyckelreplikering sker på olika sätt mellan versionerna eftersom det sätt som nycklarna lagras på skiljer sig åt mellan 6.3 och äldre versioner.

Mer information finns nedan.

#### Replikeringsnycklar för AEM 6.3 {#replicating-keys-for-aem}

I äldre versioner lagrades replikeringsnycklarna i databasen, med början från AEM 6.3, men de lagras i filsystemet.

För att replikera dina nycklar mellan instanser måste du därför kopiera dem från källinstansen till målinstansens plats i filsystemet.

Mer specifikt:

1. Få tillgång till AEM-instansen, vanligtvis en författarinstans, som innehåller det nyckelmaterial som ska kopieras.
1. Leta reda på paketet com.adobe.granite.crypto.file i det lokala filsystemet. Under den här sökvägen:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
   Den `bundle.info` fil som finns i varje mapp identifierar paketnamnet.

1. Navigera till datamappen. Exempel:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Kopiera HMAC- och mallfilerna.
1. Gå sedan till den målinstans som du vill duplicera HMAC-nyckeln till och navigera till datamappen. Exempel:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Klistra in de två filer som du kopierade tidigare.
1. [Uppdatera Crypto Bundle](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) om målinstansen redan körs.
1. Upprepa stegen ovan för alla förekomster som du vill replikera nyckeln till.

>[!NOTE]
>
>Du kan återgå till att lagra nycklar före 6.3 genom att lägga till parametern nedan när du installerar AEM första gången:
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### Replikeringsnycklar för AEM 6.2 och äldre versioner {#replicating-keys-for-aem-and-older-versions}

I AEM 6.2 och tidigare versioner lagras nycklarna i databasen under `/etc/key` noden.

Det rekommenderade sättet att på ett säkert sätt replikera nycklarna mellan dina instanser är att bara replikera den här noden. Du kan selektivt replikera noder via CRXDE Lite:

1. Öppna CRXDE Lite genom att gå till *https://&lt;serveradress>:4502/crx/de/index.jsp*
1. Select the `/etc/key` node.
1. Gå till fliken **Replikering** .
1. Tryck på knappen **Replikering** .

### Utför ett penetrationstest {#perform-a-penetration-test}

Adobe rekommenderar starkt att du testar din AEM-infrastruktur innan du börjar producera.

### Bästa praxis för utveckling {#development-best-practices}

Det är viktigt att ny utveckling följer [bästa säkerhetspraxis](/help/sites-developing/security.md) för att säkerställa att din AEM-miljö är säker.
