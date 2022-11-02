---
title: Säkerhetschecklista
seo-title: Security Checklist
description: Läs om de olika säkerhetsaspekterna när du konfigurerar och distribuerar AEM.
seo-description: Learn about the various security considerations when configuring and deploying AEM.
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Security
source-git-commit: 58c89e0b96da0f36d233cb8c14e259cc595ddda7
workflow-type: tm+mt
source-wordcount: '2859'
ht-degree: 0%

---

# Säkerhetschecklista {#security-checklist}

I det här avsnittet beskrivs olika åtgärder som du bör vidta för att se till att AEM är säker när du distribuerar. Checklistan ska användas uppifrån och ned.

>[!NOTE]
>
>Ytterligare information finns också tillgänglig om de farligaste säkerhetshot som publicerats av [Open Web Application Security Project (OWASP)](https://owasp.org/www-project-top-ten/).

>[!NOTE]
>
>Det finns ytterligare [säkerhetsaspekter](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) som tillämpas i utvecklingsfasen.

## Viktiga säkerhetsåtgärder {#main-security-measures}

### Kör AEM i produktionsklar läge {#run-aem-in-production-ready-mode}

Mer information finns i [Köra AEM i produktionsklart läge](/help/sites-administering/production-ready.md).

### Aktivera HTTPS för transportlagersäkerhet {#enable-https-for-transport-layer-security}

Det är obligatoriskt att aktivera HTTPS-transportlagret på både författare- och publiceringsinstanser för att en säker instans ska kunna användas.

>[!NOTE]
>
>Se [Aktivera HTTP över SSL](/help/sites-administering/ssl-by-default.md) för mer information.

### Installera snabbkorrigeringar för säkerhet {#install-security-hotfixes}

Kontrollera att du har installerat den senaste [Säkerhetsuppdateringar från Adobe](https://helpx.adobe.com/experience-manager/kb/aem63-available-hotfixes.html).

### Ändra standardlösenord för AEM- och OSGi-konsolens administratörskonton {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe rekommenderar att du efter installationen ändrar lösenordet för de behöriga [**AEM** `admin` konton](#changing-the-aem-admin-password) (i alla instanser).

Dessa konton omfattar:

* AEM `admin` konto

   När du har ändrat lösenordet för AEM administratörskonto måste du använda det nya lösenordet när du använder CRX.

* The `admin` lösenord för OSGi-webbkonsolen

   Den här ändringen kommer även att gälla för det administratörskonto som används för åtkomst till webbkonsolen, så du måste använda samma lösenord när du kommer åt det.

De här två kontona använder separata autentiseringsuppgifter och det är viktigt att ha tydliga, starka lösenord för var och en av dem för att driftsättningen ska vara säker.

#### Ändra AEM administratörslösenord {#changing-the-aem-admin-password}

Lösenordet för AEM administratörskonto kan ändras via [Granitåtgärder - användare](/help/sites-administering/granite-user-group-admin.md) konsol.

Här kan du redigera `admin` konto och [ändra lösenordet](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>Om du ändrar administratörskontot ändras även OSGi-webbkonsolens konto. När du har ändrat administratörskontot bör du ändra OSGi-kontot till något annat.

#### Viktigt att ändra lösenordet för OSGi-webbkonsolen {#importance-of-changing-the-osgi-web-console-password}

Förutom AEM `admin` om du inte ändrar standardlösenordet för OSGi-webbkonsolen kan det leda till:

* Serverns exponering med ett standardlösenord vid start och avstängning (som kan ta minuter för stora servrar).
* Exponering av servern när databasen är avstängd/startad och OSGI körs.

Mer information om hur du ändrar lösenord för webbkonsolen finns i [Ändra administratörslösenordet för OSGi-webbkonsolen](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) nedan.

#### Ändra administratörslösenordet för OSGi-webbkonsolen {#changing-the-osgi-web-console-admin-password}

Du måste också ändra lösenordet som används för att komma åt webbkonsolen. Detta görs genom att konfigurera följande egenskaper för [Apache Felix OSGi Management Console](/help/sites-deploying/osgi-configuration-settings.md):

**Användarnamn** och **Lösenord**, inloggningsuppgifterna för åtkomst till själva Apache Felix Web Management Console.
Lösenordet måste ändras efter den första installationen för att säkerställa instansens säkerhet.

Så här gör du:

1. Navigera till webbkonsolen på `<server>:<port>/system/console/configMgr`.
1. Navigera till **Apache Felix OSGi Management Console** och ändra **användarnamn** och **lösenord**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. Klicka **Spara**.

### Implementera anpassad felhanterare {#implement-custom-error-handler}

Adobe rekommenderar att du definierar anpassade felhanterarsidor, särskilt för 404- och 500 HTTP Response-koder för att förhindra informationsexponering.

>[!NOTE]
>
>Se [Hur skapar jag egna skript eller felhanterare?](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html) kunskapsbasartikel för mer information.

### Slutför checklista för utskickssäkerhet {#complete-dispatcher-security-checklist}

AEM Dispatcher är en viktig del av din infrastruktur. Adobe rekommenderar starkt att du slutför [säkerhetschacklista för avsändare](https://helpx.adobe.com/experience-manager/dispatcher/using/security-checklist.html).

>[!CAUTION]
>
>Med Dispatcher måste du inaktivera &quot;.form&quot;-väljaren.

## Verifieringssteg {#verification-steps}

### Konfigurera replikerings- och transportanvändare {#configure-replication-and-transport-users}

En standardinstallation av AEM anger `admin` som användare för transportreferenser inom standardinställningen [replikeringsagenter](/help/sites-deploying/replication.md). Administratörsanvändaren används också för att hämta replikeringen på författarsystemet.

Av säkerhetsskäl bör båda ändras för att återspegla det aktuella användningsfallet, med följande två aspekter i åtanke:

* The **transportanvändare** ska inte vara administratörsanvändare. I stället anger du en användare i publiceringssystemet som bara har behörighet till de relevanta delarna av publiceringssystemet och använder användarens inloggningsuppgifter för transporten.

   Du kan starta från den paketerade replikeringsmottagaren och konfigurera den här användarens åtkomsträttigheter så att de matchar din situation

* The **replikanvändare** eller **Användar-ID för agent** ska inte heller vara admin-användare, utan en användare som bara kan se innehåll som ska replikeras. Replikeringsanvändaren används för att samla in det innehåll som ska replikeras på författarsystemet innan det skickas till utgivaren.

### Kontrollera säkerhetshälsokontrollerna för instrumentpanelen för åtgärder {#check-the-operations-dashboard-security-health-checks}

I AEM 6 introduceras den nya kontrollpanelen för åtgärder, som är avsedd att hjälpa systemansvariga att felsöka problem och övervaka en instans hälsa.

Kontrollpanelen innehåller också en samling säkerhetskontroller. Vi rekommenderar att du kontrollerar statusen för alla säkerhetshälsokontroller innan du publicerar med produktionsinstansen. Mer information finns i [Dokumentation för instrumentpanelen för åtgärder](/help/sites-administering/operations-dashboard.md).

### Kontrollera om exempelinnehåll finns {#check-if-example-content-is-present}

Allt exempelinnehåll och alla användare (t.ex. Geometrixx och dess komponenter) ska avinstalleras och tas bort helt i ett produktionssystem innan det görs tillgängligt för allmänheten.

>[!NOTE]
>
>Exemplet med webbprogram.Detaljhandelsprogram tas bort om den här instansen körs i [Produktionsklar läge](/help/sites-administering/production-ready.md). Om så inte är fallet kan du avinstallera exempelinnehållet genom att gå till Package Manager och sedan söka efter och avinstallera alla We.Retail-paket. Mer information finns på [Arbeta med paket](package-manager.md).

### Kontrollera om det finns några CRX-utvecklingspaket {#check-if-the-crx-development-bundles-are-present}

Dessa OSGi-utvecklingspaket bör avinstalleras både på författaren och publicera produktionssystem innan de blir tillgängliga.

* Stöd för Adobe CRXDE (com.adobe.granite.crxde-support)
* Adobe Granite CRX Explorer (com.adobe.granite.crx-explorer)
* Adobe Granite CRXDE Lite (com.adobe.granite.crxde-lite)

### Kontrollera om Sling-utvecklingspaketet finns {#check-if-the-sling-development-bundle-is-present}

The [AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md) distribuerar installationsprogrammet för Apache Sling Tooling Support (org.apache.sling.tooling.support.install).

Detta OSGi-paket bör avinstalleras både på författaren och publicera produktionssystem innan de blir tillgängliga.

### Protect mot smidning av förfrågningar mellan webbplatser {#protect-against-cross-site-request-forgery}

#### CSRF Protection Framework {#the-csrf-protection-framework}

AEM 6.1 levereras med en mekanism som hjälper till att skydda mot attacker med attacker med smidda förfrågningar på olika webbplatser, som kallas **Ramverk för CSRF-skydd**. Mer information om hur du använder programmet finns i [dokumentation](/help/sites-developing/csrf-protection.md).

#### Sling Referer-filtret {#the-sling-referrer-filter}

För att åtgärda kända säkerhetsproblem med CSRF (Cross-Site Request Forgery) i CRX WebDAV och Apache Sling måste du lägga till konfigurationer för referensfiltret för att kunna använda det.

Refererarfiltertjänsten är en OSGi-tjänst som gör att du kan konfigurera:

* vilka http-metoder som ska filtreras
* om en tom referensrubrik tillåts
* och en lista över servrar som ska tillåtas utöver servervärden.

   Som standard finns alla varianter av localhost och de värdnamn som servern är bunden till i listan.

Så här konfigurerar du referenspunktsfiltertjänsten:

1. Öppna Apache Felix-konsolen (**Konfigurationer**) på:

   `https://<server>:<port_number>/system/console/configMgr`

1. Logga in som `admin`.
1. I **Konfigurationer** väljer du:

   `Apache Sling Referrer Filter`

1. I `Allow Hosts` anger du alla värdar som tillåts som referent. Varje tävlingsbidrag måste ha blanketten

   &lt;protocol>:/&lt;server>:&lt;port>

   Till exempel:

   * `https://allowed.server:80` tillåter alla begäranden från den här servern med den angivna porten.
   * Om du även vill tillåta https-begäranden måste du ange en andra rad.
   * Om du tillåter alla portar från den servern kan du använda `0` som portnummer.

1. Kontrollera `Allow Empty` om du vill tillåta tomma/saknade hänvisningsrubriker.

   >[!CAUTION]
   >
   >Vi rekommenderar att du skickar en referens när du använder kommandoradsverktyg som `cURL` i stället för att tillåta ett tomt värde eftersom det kan exponera systemet för CSRF-attacker.

1. Redigera de metoder som filtret ska använda för kontroller med `Filter Methods` fält.

1. Klicka **Spara** för att spara ändringarna.

### OSGI-inställningar {#osgi-settings}

Vissa OSGI-inställningar ställs in som standard för att underlätta felsökning av programmet. Dessa måste ändras i era publicerings- och upphovsarbetsinstanser för att undvika att intern information läcker till allmänheten.

>[!NOTE]
>
>Alla inställningar nedan utom **Dagen CQ WCM-felsökningsfilter** täcks automatiskt av [Produktionsklar läge](/help/sites-administering/production-ready.md). Därför rekommenderar vi att du granskar alla inställningar innan du distribuerar instansen i en produktiv miljö.

För var och en av följande tjänster måste de angivna inställningarna ändras:

* [Bibliotekshanteraren Adobe Granite HTML](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * enable **Minify** (för att ta bort CRLF- och blankstegstecken).
   * enable **Gzip** (för att tillåta att filer grupperas och öppnas med en begäran).
   * disable **Felsök**
   * disable **Timing**

* [Dag CQ WCM-felsökningsfilter](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * avmarkera **Aktivera**

* [Dag CQ WCM-filter](/help/sites-deploying/osgi-configuration-settings.md):

   * endast vid publicering, ange **WCM-läge** till &quot;disabled&quot;

* [Apache Sling Java Script Handler](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * disable **Generera felsökningsinformation**

* [Apache Sling JSP Script Handler](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * disable **Generera felsökningsinformation**
   * disable **Mappat innehåll**

Mer information finns i [Konfigurationsinställningar för OSGi](/help/sites-deploying/osgi-configuration-settings.md).

När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. se [Konfigurerar OSGi](/help/sites-deploying/configuring-osgi.md) om du vill ha mer information och rekommenderade rutiner.

## Ytterligare läsningar {#further-readings}

### Minska DoS-attacker (Denial of Service) {#mitigate-denial-of-service-dos-attacks}

En denial of service-attack (DoS) är ett försök att göra en datorresurs otillgänglig för de avsedda användarna. Detta görs ofta genom att överbelasta resursen. till exempel:

* Med en mängd förfrågningar från en extern källa.
* Med en begäran om mer information än vad systemet kan leverera.

   Till exempel en JSON-representation av hela databasen.

* Genom att begära en innehållssida med ett obegränsat antal URL-adresser kan URL-adressen innehålla ett handtag, vissa väljare, ett tillägg och ett suffix, som alla kan ändras.

   Till exempel: `.../en.html` kan också begäras som:

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   Alla giltiga variationer (t.ex. returnera en `200` och är konfigurerade att cachelagras) kommer att cachas av dispatchern, vilket till slut leder till ett fullständigt filsystem och ingen tjänst för ytterligare förfrågningar.

Det finns många konfigurationspunkter för att förhindra sådana attacker, här diskuterar vi bara de som är direkt relaterade till AEM.

**Konfigurera Sling för att förhindra DoS**

Sling är *innehållscentrerad*. Detta innebär att bearbetningen är inriktad på innehållet eftersom varje HTTP-begäran mappas till innehåll i form av en JCR-resurs (en databasnod):

* Det första målet är den resurs (JCR-nod) som innehåller innehållet.
* För det andra finns återgivaren, eller skriptet, från resursegenskaperna i kombination med vissa delar av begäran (t.ex. väljare och/eller tillägg).

>[!NOTE]
>
>Detta beskrivs mer ingående i [Bearbetning av försäljningsbegäran](/help/sites-developing/the-basics.md#sling-request-processing).

Den här metoden gör Sling mycket kraftfull och mycket flexibel, men som alltid är det den flexibilitet som måste hanteras noggrant.

För att förhindra missbruk kan du:

1. Införliva kontroller på applikationsnivå. På grund av antalet möjliga variationer är en standardkonfiguration inte möjlig.

   I ditt program bör du:

   * Styr väljarna i programmet så att du *endast* servar de explicita väljarna som behövs och returnerar `404` för alla andra.
   * Förhindra utdata från ett obegränsat antal innehållsnoder.

1. Kontrollera konfigurationen av standardåtergivningsprogrammen, som kan vara ett problemområde.

   * I synnerhet JSON-renderaren som kan omvända trädstrukturen över flera nivåer.

      Exempelvis begäran:

      `http://localhost:4502/.json`

      kan dumpa hela databasen i en JSON-representation. Detta skulle orsaka allvarliga serverproblem. Därför anger Sling en gräns för antalet maximala resultat. Om du vill begränsa djupet i JSON-återgivningen kan du ange värdet för:

      **JSON Max-resultat** ( `json.maximumresults`)

      i konfigurationen för [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). När den här gränsen överskrids komprimeras återgivningen. Standardvärdet för Sling inom AEM är `1000`.

   * Som en förebyggande åtgärd kan du inaktivera de andra standardåtergivningarna (HTML, oformaterad text, XML). Återigen genom att konfigurera [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >Inaktivera inte JSON-renderaren, vilket krävs för att AEM ska fungera normalt.

1. Använd en brandvägg för att filtrera åtkomsten till instansen.

   * Du måste använda en brandvägg på operativsystemnivå för att filtrera åtkomst till punkter i din instans som kan leda till denial of service-attacker om den lämnas oskyddad.

**Minska mot DoS som orsakas av att formulärväljare används**

>[!NOTE]
>
>Denna begränsning bör endast utföras i AEM som inte använder Forms.

Eftersom AEM inte tillhandahåller index för `FormChooserServlet`, som använder formulärväljare i frågor, utlöser en kostsam databasgenomgång, vilket vanligen leder till att AEM avbryts. Formulärväljare kan identifieras med hjälp av **&amp;ast;.form.&amp;ast;** sträng i frågor.

Följ stegen nedan för att minska detta:

1. Gå till webbkonsolen genom att peka webbläsaren till *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. Sök efter **Day CQ WCM Form Chooser Server**
1. När du har klickat på inlägget inaktiverar du **Avancerad sökning krävs** i följande fönster.

1. Klicka **Spara**.

**Minska mot DoS som orsakas av tjänsten för hämtning av resurser**

Med standardservern för hämtning av resurser kan autentiserade användare skicka godtyckligt stora begäranden om samtidig hämtning för att skapa ZIP-filer med resurser. Om du skapar stora ZIP-arkiv kan servern och nätverket överbelastas. För att minska risken för denial of service-attacker som orsakas av detta beteende `AssetDownloadServlet` OSGi-komponenten är inaktiverad som standard på [!DNL Experience Manager] publiceringsinstans. Den är aktiverad på [!DNL Experience Manager] författarinstans som standard.

Om du inte behöver nedladdningsfunktionen kan du inaktivera servleten för att skapa och publicera distributioner. Om din installation kräver att hämtningsfunktionen är aktiverad, se [den här artikeln](/help/assets/download-assets-from-aem.md) för mer information. Du kan också ange en maximal hämtningsgräns som din distribution kan stödja.

### Inaktivera WebDAV {#disable-webdav}

WebDAV ska vara inaktiverat i både författar- och publiceringsmiljön. Detta kan göras genom att stoppa de aktuella OSGi-paketen.

1. Anslut till **Felix Management Console** som körs:

   `https://<*host*>:<*port*>/system/console`

   Till exempel `http://localhost:4503/system/console/bundles`.

1. I listan med paket hittar du paketet:

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Klicka på stoppknappen (i åtgärdskolumnen) för att stoppa paketet.

1. I listan med paket hittar du det paket som heter:

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Klicka på stoppknappen för att stoppa det här paketet.

   >[!NOTE]
   >
   >Du behöver inte starta om AEM.

### Verifiera att du inte avslöjar personligt identifierbar information i användarens hemsökväg {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

Det är viktigt att du skyddar dina användare genom att se till att du inte visar någon personligt identifierbar information i databasanvändarens hemsökväg.

Sedan AEM 6.1 har sättet som användar-ID-nodnamn (kallas även auktoriseringsbara) lagras på ändrats med en ny implementering av `AuthorizableNodeName` gränssnitt. Det nya gränssnittet visar inte längre användar-ID:t i nodnamnet, utan genererar i stället ett slumpmässigt namn.

Ingen konfiguration behöver göras för att aktivera den, eftersom detta nu är standardsättet att generera auktoriserbara ID:n i AEM.

Även om det inte rekommenderas kan du inaktivera det om du behöver den gamla implementeringen för bakåtkompatibilitet med dina befintliga program. För att göra detta måste du:

1. Gå till webbkonsolen och ta bort posten** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** från egenskapen **requiredServicePids** in **Apache Jackrabbit Oak SecurityProvider**.

   Du kan också hitta Oak Security Provider genom att leta efter **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID i OSGi-konfigurationer.

1. Ta bort **Apache Jackrabbit Oak Random Authorizable Node Name** OSGi-konfiguration från webbkonsolen.

   Observera att PID för den här konfigurationen är **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>Mer information finns i Oak-dokumentationen på [Generering av auktoriseringsbart nodnamn](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### Förhindra clickjacking {#prevent-clickjacking}

För att förhindra clickjacking rekommenderar vi att du konfigurerar webbservern så att den `X-FRAME-OPTIONS` HTTP-huvudet är inställt på `SAMEORIGIN`.

Mer [information om clickjacking finns på OWASP-webbplatsen](https://www.owasp.org/index.php/Clickjacking).

### Se till att du replikerar krypteringsnycklar korrekt vid behov {#make-sure-you-properly-replicate-encryption-keys-when-needed}

Vissa AEM funktioner och autentiseringsscheman kräver att du replikerar dina krypteringsnycklar i alla AEM instanser.

Innan du gör detta bör du tänka på att nyckelreplikering sker på olika sätt mellan versionerna eftersom det sätt som nycklarna lagras på skiljer sig åt mellan 6.3 och äldre versioner.

Mer information finns nedan.

#### Replikeringsnycklar för AEM 6.3 {#replicating-keys-for-aem}

I äldre versioner lagrades replikeringsnycklarna i databasen, med början AEM 6.3 lagras de i filsystemet.

För att replikera dina nycklar mellan instanser måste du därför kopiera dem från källinstansen till målinstansens plats i filsystemet.

Mer specifikt:

1. få åtkomst till AEM, vanligtvis en författarinstans, som innehåller det nyckelmaterial som ska kopieras,
1. Leta reda på paketet com.adobe.granite.crypto.file i det lokala filsystemet. Under den här sökvägen:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25`

   The `bundle.info` filen i varje mapp identifierar paketnamnet.

1. Navigera till datamappen. Till exempel:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. Kopiera HMAC-filer och överordnad filer.
1. Gå sedan till den målinstans som du vill duplicera HMAC-nyckeln till och navigera till datamappen. Till exempel:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. Klistra in de två filer som du kopierade tidigare.
1. [Uppdatera krypteringspaketet](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) om målinstansen redan körs.
1. Upprepa stegen ovan för alla förekomster som du vill replikera nyckeln till.

>[!NOTE]
>
>Du kan återgå till metoden för att lagra nycklar före 6.3 genom att lägga till parametern nedan när du först installerar AEM:
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### Replikeringsnycklar för AEM 6.2 och äldre versioner {#replicating-keys-for-aem-and-older-versions}

I AEM 6.2 och tidigare lagras nycklarna i databasen under `/etc/key` nod.

Det rekommenderade sättet att på ett säkert sätt replikera nycklarna mellan dina instanser är att bara replikera den här noden. Du kan selektivt replikera noder via CRXDE Lite:

1. Öppna CRXDE Lite genom att gå till *https://&lt;serveraddress>:4502/crx/de/index.jsp*
1. Välj `/etc/key` nod.
1. Gå till **Replikering** -fliken.
1. Tryck på **Replikering** -knappen.

### Utför ett penetrationstest {#perform-a-penetration-test}

Adobe rekommenderar starkt att du utför ett penetrationstest av din AEM infrastruktur innan du börjar producera.

### Bästa praxis för utveckling {#development-best-practices}

Det är viktigt att ny utveckling följer [Bästa praxis för säkerhet](/help/sites-developing/security.md) för att säkerställa att AEM är säker.
