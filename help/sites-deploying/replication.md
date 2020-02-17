---
title: Replikering
seo-title: Replikering
description: Lär dig hur du konfigurerar och övervakar replikeringsagenter i AEM.
seo-description: Lär dig hur du konfigurerar och övervakar replikeringsagenter i AEM.
uuid: 6c0bc2fe-523a-401f-8d93-e5795f2e88b9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 3cae081e-93e3-4317-b307-1316283c307a
docset: aem65
translation-type: tm+mt
source-git-commit: d281ea4a5e7711aafa906bc0c43009c3c2cc8947

---


# Replikering{#replication}

Replikeringsagenter är centrala för Adobe Experience Manager (AEM) eftersom den mekanism som används för att:

* [Publicera (aktivera)](/help/sites-authoring/publishing-pages.md#activatingcontent) innehåll från en författare till en publiceringsmiljö.
* Rensa innehåll explicit från Dispatcher-cachen.
* Returnera användarindata (till exempel formulärindata) från publiceringsmiljön till författarmiljön (under kontroll av författarmiljön).

Begäranden [köas](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) till lämplig agent för behandling.

>[!NOTE]
>
>Användardata (användare, användargrupper och användarprofiler) replikeras inte mellan författare- och publiceringsinstanser.
>
>För flera publiceringsinstanser distribueras användardata när [användarsynkronisering](/help/sites-administering/sync.md) är aktiverat.

## Replikerar från författare till publicering {#replicating-from-author-to-publish}

Replikering till en publiceringsinstans eller dispatcher sker i flera steg:

* författaren begär att visst innehåll ska publiceras (aktiveras), detta kan initieras av en manuell begäran eller av automatiska utlösare som har förkonfigurerats.
* begäran skickas till lämplig standardredigeringsagent, en miljö kan ha flera standardagenter som alltid väljs för sådana åtgärder.
* replikeringsagenten&quot;paketerar&quot; innehållet och placerar det i replikeringskön.
* på fliken Webbplatser är den [färgade statusindikatorn](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) inställd för de enskilda sidorna.
* innehållet tas bort från kön och transporteras till publiceringsmiljön med det konfigurerade protokollet, vanligtvis är detta HTTP.
* en server i publiceringsmiljön tar emot begäran och publicerar det mottagna innehållet, standardservleten är `https://localhost:4503/bin/receive`.

* flera skribent- och publiceringsmiljöer kan konfigureras.

![chlimage_1-21](assets/chlimage_1-21.png)

### Replikerar från publicera till författare {#replicating-from-publish-to-author}

Vissa funktioner tillåter användare att ange data i en publiceringsinstans.

I vissa fall behövs en typ av replikering som kallas omvänd replikering för att returnera dessa data till den redigeringsmiljö varifrån de distribueras till andra publiceringsmiljöer. Av säkerhetsskäl måste all trafik från publicering till redigeringsmiljön vara strikt kontrollerad.

Omvänd replikering använder en agent i publiceringsmiljön som refererar till redigeringsmiljön. Den här agenten placerar data i en utkorg. Utkorgen matchas med replikeringslyssnare i redigeringsmiljön. Avlyssnarna avsöker utkorgarna för att samla in alla data som anges och sedan distribuera dem efter behov. Detta garanterar att redigeringsmiljön styr all trafik.

I andra fall, t.ex. för communityfunktioner (t.ex. forum, bloggar, kommentarer och granskningar), är mängden användargenererat innehåll (UGC) som anges i publiceringsmiljön svår att effektivt synkronisera mellan AEM-instanser med hjälp av replikering.

AEM [Communities](/help/communities/overview.md) använder aldrig replikering för UGC. Distributionen för Communities kräver i stället en gemensam butik för UGC (se [Community Content Storage](/help/communities/working-with-srp.md)).

### Replikering - utanför lådan {#replication-out-of-the-box}

Webbplatsen för webbutiker som ingår i en standardinstallation av AEM kan användas för att illustrera replikering.

Om du vill följa det här exemplet och använda standardreplikeringsagenterna måste du [installera AEM](/help/sites-deploying/deploy.md) med:

* författarmiljön på porten `4502`
* publiceringsmiljön på porten `4503`

>[!NOTE]
>
>Aktiverad som standard:
>
>* Agenter på författare:Standardagent (publicera)
>
>
Inaktiverat som standard (från och med AEM 6.1):
>
>* Agenter på författare: Agenten för omvänd replikering (publish_reverse)
>* Agenter vid publicering: Omvänd replikering (utkorg)
>
>
Om du vill kontrollera status för agenten eller kön använder du **verktygskonsolen** .
>Se [Övervaka dina replikeringsagenter](#monitoring-your-replication-agents).

#### Replikering (författare att publicera) {#replication-author-to-publish}

1. Navigera till supportsidan i författarmiljön.
   **https://localhost:4502/content/we-retail/us/en/experience.html**`<pi>`
1. Redigera sidan för att lägga till ny text.
1. **Aktivera sidan** om du vill publicera ändringarna.
1. Öppna supportsidan i publiceringsmiljön:
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. Du kan nu se ändringarna som du har angett för författaren.

Den här replikeringen utförs från redigeringsmiljön av:

* **Standardagent (publicera)**Den här agenten replikerar innehåll till standardpubliceringsinstansen.
Information om detta (konfiguration och loggar) finns på verktygskonsolen i författarmiljön. eller:
   `https://localhost:4502/etc/replication/agents.author/publish.html`.

#### Replikeringsagenter - utanför lådan {#replication-agents-out-of-the-box}

Följande agenter är tillgängliga i en AEM-standardinstallation:

* [Standardagent](#replication-author-to-publish)används för replikering från författare till publicering.

* Dispatcher FlushDetta används för att hantera Dispatcher-cachen. Mer information finns i [Invalidera Dispatcher Cache från redigeringsmiljön](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment) och [Invalidera Dispatcher Cache från en Publishing-instans](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance) .

* [Omvänd replikering](#reverse-replication-publish-to-author)används för replikering från publicering till författare. Omvänd replikering används inte för communityfunktioner som forum, bloggar och kommentarer. Den är inaktiverad eftersom utkorgen inte är aktiverad. Användning av omvänd replikering kräver anpassad konfiguration.

* Statisk agentDetta är en&quot;agent som lagrar en statisk representation av en nod i filsystemet&quot;.
Med standardinställningarna lagras t.ex. innehållssidor och dammresurser under `/tmp`, antingen som HTML eller i lämpligt resursformat. Mer information finns på flikarna `Settings` och `Rules` i konfigurationen.
Detta begärdes så att innehållet kan ses när sidan begärs direkt från programservern. Detta är en specialiserad agent och (troligen) krävs inte för de flesta instanser.

## Replikeringsagenter - konfigurationsparametrar {#replication-agents-configuration-parameters}

När du konfigurerar en replikeringsagent från verktygskonsolen är fyra flikar tillgängliga i dialogrutan:

###  Inställningar {#settings}

* **Namn**

   Ett unikt namn för replikeringsagenten.

* **Beskrivning**

   En beskrivning av syftet med den här replikeringsagenten.

* **Aktiverad**

   Anger om replikeringsagenten är aktiverad.

   När agenten är **aktiverad** visas kön som:

   * **Aktiv** när artiklar bearbetas.
   * **Inaktiv** när kön är tom.
   * **Blockeras** när objekten finns i kön men inte kan bearbetas; till exempel när mottagande kö är inaktiverad.

* **Serialiseringstyp**

   Typ av serialisering:

   * **Standard**: Ange om agenten ska väljas automatiskt.
   * **Dispatcher Flush**: Välj det här alternativet om agenten ska användas för att tömma dispatchercachen.

* **Återförsöksfördröjning**

   Fördröjningen (i millisekunder) mellan två försök om ett problem skulle uppstå.

   Default: `60000`

* **Användar-ID för agent**

   Beroende på miljön kommer agenten att använda det här användarkontot för att:

   * samla in och paketera innehåll från författarmiljön
   * skapa och skriva innehåll i publiceringsmiljön
   Lämna det här fältet tomt om du vill använda systemanvändarkontot (det konto som definierats i sling som administratörsanvändare). som standard är detta `admin`).

   >[!CAUTION]
   >
   >För en agent i författarmiljön *måste* det här kontot ha läsåtkomst till alla sökvägar som du vill ha replikerade.

   >[!CAUTION]
   >
   >För en agent i publiceringsmiljön *måste* det här kontot ha den behörighet att skapa/skriva som krävs för att replikera innehållet.

   >[!NOTE]
   >
   >Detta kan användas som en mekanism för att välja specifikt innehåll för replikering.

* **Loggnivå**

   Anger den detaljnivå som ska användas för loggmeddelanden.

   * `Error`: endast fel loggas
   * `Info`: fel, varningar och andra informationsmeddelanden loggas
   * `Debug`: en hög detaljnivå kommer att användas i meddelandena, främst i felsökningssyfte
   Default: `Info`

* **Använd för omvänd replikering**

   Anger om agenten ska användas för omvänd replikering. returnerar användarindata från publicerings- till författarmiljön.

* **Aliasuppdatering**

   Om du väljer det här alternativet aktiveras ogiltiga aliassökvägar eller ogiltiga sökvägar för Dispatcher. Se även [Konfigurera en Dispatcher Flush Agent](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent).

#### Transport {#transport}

* **URI**

   Detta anger den mottagande servern på målplatsen. Du kan särskilt ange värdnamnet (eller aliaset) och kontextsökvägen till målinstansen här.

   Exempel:

   * En standardagent kan replikeras till `https://localhost:4503/bin/receive`
   * En agent för utskickstömning kan replikeras till `https://localhost:8000/dispatcher/invalidate.cache`
   Det protokoll som anges här (HTTP eller HTTPS) avgör transportmetoden.

   För Dispatcher Flush-agenter används URI-egenskapen endast om du använder sökvägsbaserade virtualhost-poster för att skilja mellan grupper, använder du det här fältet för att göra gruppen ogiltig. Servergrupp nr 1 har till exempel en virtuell värd av `www.mysite.com/path1/*` och servergrupp nr 2 har en virtuell värd av `www.mysite.com/path2/*`. Du kan använda en URL av `/path1/invalidate.cache` för att ange den första servergruppen som mål och `/path2/invalidate.cache` för den andra servergruppen.

* **Användare**

   Användarnamn för kontot som ska användas för att komma åt målet.

* **Lösenord**

   Lösenord för kontot som ska användas för att komma åt målet.

* **NTLM-domän**

   Domän för NTML-autentisering.

* **NTLM-värd**

   Värd för NTML-autentisering.

* **Aktivera relaxerad SSL**

   Aktivera om du vill att självcertifierade SSL-certifikat ska godkännas.

* **Tillåt utgångna certifikat**

   Aktivera om du vill att utgångna SSL-certifikat ska godkännas.

#### Proxy {#proxy}

Följande inställningar behövs bara om en proxy behövs:

* **Proxyvärd**

   Värdnamn för proxyn som används för transport.

* **Proxyport**

   Proxyns port.

* **Proxyanvändare**

   Användarnamn för kontot som ska användas.

* **Proxylösenord**

   Lösenord för kontot som ska användas.

* **Proxy NTLM-domän**

   NTLM-proxydomänen.

* **Proxy NTLM-värd**

   NTLM-proxydomänen.

#### Utökad {#extended}

* **Gränssnitt**

   Här kan du definiera socketgränssnittet som du vill binda till.

   Detta anger den lokala adress som ska användas när anslutningar skapas. Om detta inte anges används standardadressen. Detta är användbart när du vill ange vilket gränssnitt som ska användas på system med flera hem eller kluster.

* **HTTP-metod**

   HTTP-metoden som ska användas.

   För en Dispatcher Flush-agent är detta nästan alltid GET och ska inte ändras (POST är ett annat möjligt värde).

* **HTTP-huvuden**

   Dessa används för Dispatcher Flush-agenter och anger element som måste tömmas.

   För en Dispatcher Flush-agent behöver de tre standardposterna inte ändras:

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`
   Dessa används, beroende på vad som är lämpligt, för att ange vilken åtgärd som ska användas när handtaget eller banan töms. Underparametrarna är dynamiska:

   * `{action}` anger en replikeringsåtgärd

   * `{path}` anger en bana
   De ersätts av den sökväg/åtgärd som är relevant för begäran och behöver därför inte&quot;hårdkodas&quot;:

   >[!NOTE]
   >
   >Om du har installerat AEM i en annan kontext än den rekommenderade måste du registrera kontexten i HTTP-rubrikerna. Exempel:
   >`CQ-Handle:/<*yourContext*>{path}`

* **Stäng anslutning**

   Aktivera för att stänga anslutningen efter varje begäran.

* **Tidsgräns för anslutning**

   Timeout (i millisekunder) som ska användas vid försök att upprätta en anslutning.

* **Tidsgräns för socket**

   Timeout (i millisekunder) som ska användas vid väntan på trafik efter att en anslutning har upprättats.

* **Protokollversion**

   Protokollets version. till exempel `1.0` för HTTP/1.0.

#### Utlösare {#triggers}

De här inställningarna används för att definiera utlösare för automatiserad replikering:

* **Ignorera standard**

   Om du markerar detta utesluts agenten från standardreplikering. Detta innebär att det inte kommer att användas om en innehållsförfattare utfärdar en replikeringsåtgärd.

* **Vid ändring**

   Här aktiveras en replikering från den här agenten automatiskt när en sida ändras. Detta används främst för Dispatcher Flush-agenter, men även för omvänd replikering.

* **Vid distribution**

   Om det här alternativet är markerat kopieras automatiskt allt innehåll som är markerat för distribution när det ändras.

* **On-/Offtime uppnådd**

   Detta startar automatisk replikering (för att aktivera eller inaktivera en sida efter behov) när de tider eller offtider som har definierats för en sida inträffar. Detta används främst för Dispatcher Flush-agenter.

* **Vid mottagning**

   Om det här alternativet är markerat kommer agenten att kedja replikeringen när den tar emot replikeringshändelser.

* **Ingen statusuppdatering**

   När det här alternativet är markerat framtvingar agenten ingen uppdatering av replikeringsstatusen.

* **Ingen versionshantering**

   När det här alternativet är markerat framtvingar agenten inte versionshantering av aktiverade sidor.

## Konfigurera replikeringsagenter {#configuring-your-replication-agents}

Mer information om hur du ansluter replikeringsagenter till publiceringsinstansen med MSSL finns i [Replikera med ömsesidig SSL](/help/sites-deploying/mssl-replication.md).

### Konfigurera dina replikeringsagenter från författarmiljön {#configuring-your-replication-agents-from-the-author-environment}

På fliken Verktyg i författarmiljön kan du konfigurera replikeringsagenter som finns i antingen författarmiljön (**agenter på författare**) eller publiceringsmiljön (**agenter på publicering**). Följande procedurer illustrerar konfigurationen av en agent för författarmiljön, men kan användas för båda.

>[!NOTE]
>
>När en dispatcher hanterar HTTP-begäranden för författare- eller publiceringsinstanser måste HTTP-begäran från replikeringsagenten innehålla PATH-huvudet. Utöver följande procedur måste du lägga till PATH-huvudet i avsändarlistan med klientrubriker. (Se [/clientheaders (Klientrubriker)](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders). [](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders)


1. Gå till fliken **Verktyg** i AEM.
1. Klicka på **Replikering** (vänster ruta för att öppna mappen).
1. Dubbelklicka på **Agenter på författaren** (antingen vänster eller höger ruta).
1. Klicka på lämpligt agentnamn (som är en länk) för att visa detaljerad information om agenten.
1. Klicka på **Redigera** för att öppna konfigurationsdialogrutan:

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. De angivna värdena ska vara tillräckliga för en standardinstallation. Om du gör ändringar klickar du på **OK** för att spara dem (mer information om de enskilda parametrarna finns i [Replikeringsagenter - Konfigurationsparametrar](#replication-agents-configuration-parameters) ).

>[!NOTE]
>
>En standardinstallation av AEM anger `admin` som användare för transportreferenser inom standardreplikeringsagenterna.
>
>Detta bör ändras till ett platsspecifikt replikeringsanvändarkonto med behörighet att replikera de nödvändiga sökvägarna.

### Konfigurerar omvänd replikering {#configuring-reverse-replication}

Omvänd replikering används för att hämta användarinnehåll som genererats på en publiceringsinstans tillbaka till en författarinstans. Detta används ofta för funktioner som undersökningar och registreringsformulär.

Av säkerhetsskäl tillåter de flesta nätverkstopologier inte anslutningar *från* den &quot;Demilitarized Zone&quot; (ett undernätverk som exponerar de externa tjänsterna för ett ej betrott nätverk som Internet).

Eftersom publiceringsmiljön vanligtvis finns i DMZ måste anslutningen initieras från författarinstansen för att innehållet ska kunna skickas tillbaka till redigeringsmiljön. Detta görs med:

* en *utkorg* i publiceringsmiljön där innehållet placeras.
* en agent (publicera) i författarmiljön som regelbundet frågar efter nytt innehåll i utkorgen.

>[!NOTE]
>
>För AEM [Communities](/help/communities/overview.md)används inte replikering för användargenererat innehåll på en publiceringsinstans. Se [Community Content Storage](/help/communities/working-with-srp.md).

För att göra detta behöver du:

**En agent för omvänd replikering i författarmiljön** Detta fungerar som den aktiva komponenten för att samla in information från utkorgen i publiceringsmiljön:

Om du vill använda omvänd replikering kontrollerar du att agenten är aktiverad.

![chlimage_1-23](assets/chlimage_1-23.png)

**A reverse replication agent in the publish environment (an outbox)** This is the passive element as it actions as an &quot;outbox&quot;. Användarindata placeras här, där de samlas in av agenten i författarmiljön.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### Konfigurera replikering för flera publiceringsinstanser {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>Endast innehåll replikeras - användardata är inte det (användare, användargrupper och användarprofiler).
>
>Om du vill synkronisera användardata över flera publiceringsinstanser aktiverar du [Användarsynkronisering](/help/sites-administering/sync.md).

Vid installationen är en standardagent redan konfigurerad för replikering av innehåll till en publiceringsinstans som körs på port 4503 på den lokala värden.

Så här konfigurerar du replikering av innehåll för ytterligare en publiceringsinstans som du måste skapa och konfigurera en ny replikeringsagent:

1. Öppna fliken **Verktyg** i AEM.
1. Välj **Replikering** och sedan **Agenter på författaren** i den vänstra panelen.
1. **Välj** ny... .
1. Ange **titel** och **namn** och välj sedan **Replikeringsagent**.
1. Klicka på **Skapa** för att skapa den nya agenten.
1. Dubbelklicka på det nya agentobjektet för att öppna konfigurationspanelen.
1. Klicka på **Redigera** - dialogrutan **Agentinställningar** öppnas - **Serialiseringstypen** är redan definierad som Standard. Detta måste vara så.

   * På fliken **Inställningar** :

      * Aktivera **aktiverat**.
      * Ange en **beskrivning**.
      * Ange **fördröjning** för återförsök till `60000`.

      * Låt **serialiseringstypen** vara `Default`.
   * På fliken **Transport** :

      * Ange den URI som krävs för den nya publiceringsinstansen. till exempel
         `https://localhost:4504/bin/receive`.

      * Ange det platsspecifika användarkonto som används för replikering.
      * Du kan konfigurera andra parametrar efter behov.


1. Klicka på **OK** för att spara inställningarna.

Du kan sedan testa åtgärden genom att uppdatera och sedan publicera en sida i författarmiljön.

Uppdateringarna visas på alla publiceringsinstanser som har konfigurerats enligt ovan.

Om du får problem kan du kontrollera loggarna på författarinstansen. Beroende på den detaljnivå som krävs kan du även ange **loggnivån** till `Debug` med dialogrutan **Agentinställningar** enligt ovan.

>[!NOTE]
>
>Detta kan kombineras med användning av [agentens användar-ID](#agentuserid) för att välja ett annat innehåll som ska replikeras till de enskilda publiceringsmiljöerna. För varje publiceringsmiljö:
>
>1. Konfigurera en replikeringsagent för replikering till den publiceringsmiljön.
>1. Konfigurera ett användarkonto; med de åtkomsträttigheter som krävs för att läsa det innehåll som ska replikeras till den specifika publiceringsmiljön.
>1. Tilldela användarkontot som **agentens användar-ID** för replikeringsagenten.
>



### Konfigurera en agent för utskickstömning {#configuring-a-dispatcher-flush-agent}

Standardagenter ingår i installationen. Men en viss konfiguration behövs fortfarande, och det samma gäller om du definierar en ny agent:

1. Öppna fliken **Verktyg** i AEM.
1. Klicka på **Distribution**.
1. Välj **Replikering** och sedan **Agenter vid publicering**.
1. Dubbelklicka på **Dispatcher Flush** -objektet för att öppna översikten.
1. Klicka på **Redigera** - dialogrutan **Agentinställningar** öppnas:

   * På fliken **Inställningar** :

      * Aktivera **aktiverat**.
      * Ange en **beskrivning**.
      * Låt **serialiseringstypen** vara `Dispatcher Flush`eller ange den som sådan om du skapar en ny agent.

      * (valfritt) Markera **Aliasuppdatering** om du vill aktivera aliasbegäran eller ogiltighetsbegäran för ogiltighetssökvägen till Dispatcher.
   * På fliken **Transport** :

      * Ange den URI som krävs för den nya publiceringsinstansen. till exempel
         `https://localhost:80/dispatcher/invalidate.cache`.

      * Ange det platsspecifika användarkonto som används för replikering.
      * Du kan konfigurera andra parametrar efter behov.
   För Dispatcher Flush-agenter används URI-egenskapen endast om du använder sökvägsbaserade virtualhost-poster för att skilja mellan grupper, använder du det här fältet för att göra gruppen ogiltig. Servergrupp nr 1 har till exempel en virtuell värd av `www.mysite.com/path1/*` och servergrupp nr 2 har en virtuell värd av `www.mysite.com/path2/*`. Du kan använda en URL av `/path1/invalidate.cache` för att ange den första servergruppen som mål och `/path2/invalidate.cache` för den andra servergruppen.

   >[!NOTE]
   >
   >Om du har installerat AEM i en annan kontext än den rekommenderade måste du konfigurera [HTTP-rubrikerna](#extended) på fliken **Extended** .

1. Spara ändringarna genom att klicka på **OK** .
1. Gå tillbaka till fliken **Verktyg** och **aktivera** agenten för **utskickstömning** (**agenter vid publicering**).

Replikeringsagenten **för bortträngning** av utskickspass är inte aktiv på författaren. Du kan komma åt samma sida i publiceringsmiljön med motsvarande URI; till exempel `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### Kontrollera åtkomst till replikeringsagenter {#controlling-access-to-replication-agents}

Åtkomst till de sidor som används för att konfigurera replikeringsagenterna kan styras med användar- och/eller gruppsidbehörigheter på `etc/replication` noden.

>[!NOTE]
>
>Om du anger sådana behörigheter påverkas inte användare som replikerar innehåll (t.ex. från webbplatskonsolen eller sidosparsalternativet). Replikeringsramverket använder inte den aktuella användarens användarsession för att komma åt replikeringsagenter när sidor replikeras.

### Konfigurera replikeringsagenter från CRXDE Lite {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>Det går bara att skapa replikeringsagenter på `/etc/replication` databasplatsen. Detta krävs för att de tillhörande åtkomstkontrollistorna ska hanteras på rätt sätt. Om du skapar en replikeringsagent på en annan plats i trädet kan det leda till obehörig åtkomst.

Olika parametrar för dina replikeringsagenter kan konfigureras med CRXDE Lite.

Om du navigerar till `/etc/replication` följande tre noder:

* `agents.author`
* `agents.publish`
* `treeactivation`

De två `agents` innehåller konfigurationsinformation om lämplig miljö och är bara aktiva när den miljön körs. Till exempel används `agents.publish` bara i publiceringsmiljön. På följande skärmbild visas publiceringsagenten i författarmiljön, som ingår i AEM WCM:

![chlimage_1-24](assets/chlimage_1-24.png)

## Övervaka replikeringsagenter {#monitoring-your-replication-agents}

Så här övervakar du en replikeringsagent:

1. Gå till fliken **Verktyg** i AEM.
1. Klicka på **Replikering**.
1. Dubbelklicka på länken till agenterna för lämplig miljö (antingen vänster eller höger ruta). till exempel **Agenter på författare**.

   I det resulterande fönstret visas en översikt över alla dina replikeringsagenter för redigeringsmiljön, inklusive mål och status.

1. Klicka på lämpligt agentnamn (som är en länk) för att visa detaljerad information om agenten:

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   Här kan du:

   * Se om agenten är aktiverad.
   * Se målet för alla replikeringar.
   * Kontrollera om replikeringskön är aktiv (aktiverad).
   * Se om det finns några objekt i kön.
   * **Uppdatera** eller **Rensa** för att uppdatera visningen av köposter. så att du lättare kan se objekt komma in i och lämna kön.

   * **Visa logg** för att komma åt loggen för eventuella åtgärder som utförs av replikeringsagenten.
   * **Testa Connection** till målinstansen.
   * **Tvinga Försök igen** för alla köobjekt om det behövs.
   >[!CAUTION]
   >
   >Använd inte länken Testa anslutning för den omvända replikeringsutkorgen på en publiceringsinstans.
   >
   >
   >Om ett replikeringstest utförs för en Utkorgskö kommer alla objekt som är äldre än testreplikeringen att bearbetas på nytt med varje omvänd replikering.

   >Om sådana objekt redan finns i en kö kan de hittas med följande XPath JCR-fråga och bör tas bort.
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## Batchreplikering {#batch-replication}

Gruppreplikeringen replikerar inte enskilda sidor eller resurser, men väntar på att det första tröskelvärdet för de två sidorna, baserat på tid eller storlek, ska aktiveras.

Därefter paketeras alla replikeringsobjekt i ett paket som sedan replikeras som en enda fil till utgivaren.

Utgivaren packar upp alla artiklar, sparar dem och rapporterar tillbaka till författaren.

### Konfigurerar batchreplikering {#configuring-batch-replication}

1. Gå till `http://serveraddress:serverport/siteadmin`
1. Tryck på **[!UICONTROL verktygsikonen]** på skärmens övre sida
1. I den vänstra navigeringslisten går du till **[!UICONTROL Replikering - Agenter på författare]** och dubbelklickar på **[!UICONTROL Standardagent]**.
   * Du kan även nå standardagenten för publiceringsreplikering genom att gå direkt till `http://serveraddress:serverport/etc/replication/agents.author/publish.html`
1. Tryck på knappen **[!UICONTROL Redigera]** ovanför replikeringskön.
1. I följande fönster går du till fliken **[!UICONTROL Gruppera]** :
   ![batchreplikering](assets/batchreplication.png)
1. Konfigurera agenten.

### Parametrar {#parameters}

* `[!UICONTROL Enable Batch Mode]` - aktiverar eller inaktiverar batchreplikeringsläge
* `[!UICONTROL Max Wait Time]` - Maximal väntetid i sekunder tills en gruppbegäran startas. Standardvärdet är 2 sekunder.
* `[!UICONTROL Trigger Size]` - Startar batchreplikering när den här storleksgränsen överskrids

## Additional Resources {#additional-resources}

Mer information om felsökning finns på sidan [Felsökning av replikering](/help/sites-deploying/troubleshoot-rep.md) .

För ytterligare information har Adobe en serie Knowledge Base-artiklar om replikering:

[https://helpx.adobe.com/experience-manager/kb/ReplicationSiblingReordering.html](https://helpx.adobe.com/experience-manager/kb/ReplicationSiblingReordering.html)[https://helpx.adobe.com/experience-manager/kb/ReplicationFailureAfterNewIP.html](https://helpx.adobe.com/experience-manager/kb/ReplicationFailureAfterNewIP.html)[https://helpx.adobe.com/experience-manager/kb/LimitAccessToReplicationAgents.html](https://helpx.adobe.com/experience-manager/kb/LimitAccessToReplicationAgents.html)[https://helpx.adobe.com/experience-manager/kb/PagePermissionsNotReplicatedWithUser.html](https://helpx.adobe.com/experience-manager/kb/PagePermissionsNotReplicatedWithUser.html)[https://helpx.adobe.com/experience-manager/kb/HowToUseReverseReplication.html](https://helpx.adobe.com/experience-manager/kb/HowToUseReverseReplication.html)[](https://helpx.adobe.com/experience-manager/kb/CQ5ReplicateToSpecificAgents.html)[](https://helpx.adobe.com/experience-manager/kb/ReplicationListener.html)[](https://helpx.adobe.com/experience-manager/kb/replication-stuck.html)[](https://helpx.adobe.com/experience-manager/kb/replication-privileges-missing-after-upgrade-to-cq-5-5.html)[](https://helpx.adobe.com/experience-manager/kb/CQ53UnableToCreateJobQueueDueToMaxQueues.html)[](https://helpx.adobe.com/experience-manager/kb/ACLReplication.html)[](https://helpx.adobe.com/experience-manager/kb/content-grow-due-reverse-replication.html)[](https://helpx.adobe.com/experience-manager/kb/ReplicationAgentUsingAnonUser.html)https://helpx.adobe.com/experience-manager/kb/CQ5ReplicateToSpecificAgents.htmlhttps://helpx.adobe.com/experience-manager/kb/ReplicationListener.htmlhttps://helpx.adobe.com/experience-manager/kb/ACLReplication.htmlhttps://helpx.adobe.com/experience-manager/kb/content-grow-due-reverse-replication.htmlhttps://helpx.adobe.com/experience-manager/kb/replication-stuck.htmlhttps://helpx.adobe.com/experience-manager/kb/CQ53UnableToCreateJobQueueDueToMaxQueues.htmlhttps://helpx.adobe.com/experience-manager/kb/replication-privileges-missing-after-upgrade-to-cq-5-5.htmlhttps://helpx.adobe.com/experience-manager/kb/ReplicationAgentUsingAnonUser.htmlhttps://helpx.adobe.com/experience-manager/kb/ReplicationSiblingReordering.htmlhttps://helpx.adobe.com/experience-manager/kb/ReplicationFailureAfterNewIP.htmlhttps://helpx.adobe.com/experience-manager/kb/LimitAccessToReplicationAgents.htmlredigeringredigeringsårUnderredigeringsårredigeringsårredigeringsprogramredigeringsårredigeringsårredigeringsdatumdelegeringsdatumförStörande bjudande