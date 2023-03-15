---
title: Grundläggande konfigurationskoncept
seo-title: Basic Configuration Concepts
description: Lär dig konfigurera AEM.
seo-description: Learn how to configure AEM.
uuid: edcdd4bd-5917-417e-8913-40d488383ea9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 2673ea92-1651-4b1b-9aac-f4ba8b36782e
feature: Configuring
exl-id: 3777a1ba-cc4e-41b9-9098-236f8141925f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 0%

---

# Grundläggande konfigurationskoncept{#basic-configuration-concepts}

Adobe Experience Manager (AEM) installeras med standardinställningar för alla parametrar så att det kan köras &quot;utanför lådan&quot;. Du kan dock konfigurera AEM efter dina egna specifika krav.

Det finns många aspekter av AEM som kan konfigureras:

* Vissa är [konfigureras vanligtvis för varje projektinstallation](#primary-configuration-considerations) och måste granskas för att bekräfta om de är tillämpliga på ditt projekt eller inte.
* [Ytterligare konfigurationer](#further-configuration-considerations) kan vara vanlig men inte tvingande, relaterade till funktioner, eller systemprestanda och stabilitet.
* Andra är bara obligatoriska för vissa valfria funktioner i AEM (dessa dokumenteras tillsammans med lämplig funktion).

Beroende på den specifika konfigurationen kan dessa ändringar göras antingen med:

* **Adobe CQ Web Console**

   Det här är en standardplats för att konfigurera OSGi-paket och -tjänster.

   Se [Konfigurerar OSGi](/help/sites-deploying/configuring-osgi.md) för mer information och rekommenderade metoder.

* **Databas**

   En deluppsättning OSGi-konfigurationer är tillgängliga i databasen. Detta garanterar att identiska konfigurationer återskapas när databasinnehåll kopieras eller replikeras. Du kan också lägga till egna konfigurationer, beroende på körningsläge, i databasen.

   Se [OSGi-konfiguration i databasen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) särskilt [Lägga till en ny konfiguration i databasen](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) för mer information.

* **Filsystem**

   Några konfigurationsfiler finns i filsystemet.

* **AEM WCM**

   Olika aspekter kan konfigureras i AEM WCM, många med [verktyg](/help/sites-administering/tools-consoles.md) konsol, till exempel replikeringsagenter.

>[!NOTE]
>
>När du arbetar med Adobe Experience Manager finns det flera metoder för att hantera konfigurationsinställningarna för OSGi-tjänster (konsol- eller databasnoder).
>
>Se [Konfigurerar OSGi](/help/sites-deploying/configuring-osgi.md) för fullständig information.

>[!NOTE]
>
>Det är enkelt att konfigurera AEM, men du måste vara medveten om att:
>
>Vissa ändringar kan ha stor effekt på programmet/programmen. Se därför till att du har den erfarenhet och kunskap som krävs innan du börjar konfigurera AEM, och gör bara de ändringar som du vet är nödvändiga. Alla ändringar som görs via OSGi-konsolen är **omedelbart** används på det system som körs (ingen omstart krävs).

## Överväganden om primär konfiguration {#primary-configuration-considerations}

Den här listan innehåller information om de primära områden som vanligtvis konfigureras för varje nytt projekt. Alla behövs inte, men listan måste läsas och granskas för att se vad som gäller för ditt projekt.

Listan innehåller en kort översikt över varje konfigurationsaspekt, tillsammans med länkar till sidorna med fullständig information.

### Säkerhetschecklista {#security-checklist}

Flera viktiga konfigurationsproblem visas i [Säkerhetschecklista](/help/sites-administering/security-checklist.md). Kontrollera att du läser detta och gör de åtgärder som krävs för installationen.

### Konfigurera standardgränssnittet - Touchoptimerat eller Classic {#configuring-the-default-ui-touch-optimized-or-classic}

Det finns två gränssnitt som kan användas i AEM:

* Det pekoptimerade användargränssnittet
* Det klassiska användargränssnittet

Du kan konfigurera användargränssnittet som du behöver med [Rotmappning](/help/sites-deploying/osgi-configuration-settings.md).

>[!NOTE]
>
>Mer information om hur du väljer användargränssnittet finns i [Välja användargränssnitt](/help/sites-authoring/select-ui.md).

### IPv4 och IPv6 {#ipv-and-ipv}

Alla element i AEM (t.ex. databasen, Dispatcher osv.) kan installeras i både IPv4- och IPv6-nätverk.

Åtgärden är smidig eftersom ingen speciell konfiguration krävs. När det behövs kan du bara ange en IP-adress med det format som passar din nätverkstyp.

Det innebär att när en IP-adress måste anges kan du välja (efter behov) bland:

* en IPv6-adress

   till exempel `https://[ab12::34c5:6d7:8e90:1234]:4502`

* en IPv4-adress

   till exempel `https://123.1.1.4:4502`

* ett servernamn

   till exempel `https://www.yourserver.com:4502`

* standardfallet för `localhost` tolkas för både IPv4- och IPv6-nätverksinstallationer

   till exempel `http://localhost:4502`

### Rensning av version {#version-purging}

I en standardinstallation AEM en ny version av en sida eller nod när du aktiverar en sida (efter att innehållet har uppdaterats). Du kan också skapa ytterligare versioner på begäran med **Versionshantering** sidosparkens flik. Alla dessa versioner lagras i databasen och kan återställas om det behövs.

Dessa versioner rensas aldrig, så databasstorleken kommer att öka med tiden och måste därför hanteras.

Se [Rensning av version](/help/sites-deploying/version-purging.md) för fullständig information, särskilt [Versionshanteraren](/help/sites-deploying/version-purging.md#version-manager) om du vill ha information om hur du konfigurerar AEM att rensa äldre versioner när en ny version skapas.

### Loggning {#logging}

AEM ger dig möjlighet att konfigurera:

* globala parametrar för den centrala loggningstjänsten
* begära dataloggning, en särskild loggningskonfiguration för begärandeinformation
* särskilda inställningar för de enskilda tjänsterna, t.ex. en enskild loggfil och ett format för loggmeddelandena

Se [Loggning](/help/sites-deploying/configure-logging.md) för fullständig information.

### Körningslägen {#run-modes}

Med körningslägena kan du justera AEM för ett specifikt ändamål; till exempel författare eller publicera, testa, utveckla eller intranät.

Detta görs genom att definiera samlingar av konfigurationsparametrar för varje körningsläge. En grundläggande uppsättning konfigurationsparametrar används för alla körningslägen, och du kan sedan justera ytterligare uppsättningar efter syftet med den specifika miljön. Dessa används sedan efter behov.

Alla konfigurationsinställningar lagras i en databas och aktiveras genom att du anger **Körningsläge**.

Se [Körningslägen](/help/sites-deploying/configure-runmodes.md) för fullständig information.

### Enkel inloggning {#single-sign-on}

Med enkel inloggning (SSO) kan en användare få åtkomst till flera system efter att ha angett inloggningsuppgifter (till exempel användarnamn och lösenord) en gång. Ett separat system (som kallas betrodd autentiserare) utför autentiseringen och ger Experience Manager inloggningsuppgifterna. Experience Manager kontrollerar och verkställer användarens åtkomstbehörigheter (d.v.s. avgör vilka resurser användaren har åtkomst till).

Se [Enkel inloggning](/help/sites-deploying/single-sign-on.md) för mer information.

### Resursmappning {#resource-mapping}

Resursmappning används för att definiera omdirigeringar, tillfälliga URL:er och virtuella värdar för AEM.

Du kan till exempel använda dessa mappningar för:

* Prefix för alla begäranden med `/content` så att den interna strukturen döljs för besökarna på webbplatsen.
* Definiera en omdirigering så att alla förfrågningar till `/content/en/gateway` webbplatsen omdirigeras till `https://gbiv.com/`.

Se [Resursmappning](/help/sites-deploying/resource-mapping.md) för mer information.

### Replikerings-, omvänd replikering- och replikeringsagenter {#replication-reverse-replication-and-replication-agents}

Replikeringsagenter AEM som den mekanism som används för att:

* [Publicera (aktivera)](/help/sites-authoring/publishing-pages.md) innehåll från en författare till en publiceringsmiljö.
* Rensa innehåll explicit från Dispatcher-cachen.
* Returnera användarindata (till exempel formulärindata) från publiceringsmiljön till författarmiljön (under kontroll av författarmiljön).

Mer information finns i [Replikering](/help/sites-deploying/replication.md).

### Konfigurationsinställningar för OSGi {#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) är en grundläggande del i AEM. Det används för att styra de sammansatta AEM och deras konfiguration.

Se [Konfigurationsinställningar för OSGi](/help/sites-deploying/osgi-configuration-settings.md) för en lista över de olika programpaket som är relevanta för projektimplementeringen (listade efter paket). Alla inställningar som visas behöver inte justeras, vissa anges för att du ska förstå hur AEM fungerar.

När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. se [Konfigurerar OSGi](/help/sites-deploying/configuring-osgi.md) om du vill ha mer information och rekommenderade rutiner.

### Konfigurerar LDAP {#configuring-ldap}

LDAP-autentisering krävs för att autentisera användare som lagras i en (central) LDAP-katalog som Active Directory. Detta minskar den arbetsinsats som krävs för att hantera användarkonton.

LDAP-autentisering sker på databasnivå, så den hanteras direkt av databasen. Mer information finns i [Konfigurera LDAP med AEM](/help/sites-administering/ldap-config.md).

Användarhantering inom AEM (inklusive tilldelning av åtkomsträttigheter) finns på [Användaradministration och -säkerhet](/help/sites-administering/security.md).

### Konfigurera Dispatcher {#configuring-the-dispatcher}

Dispatcher är ett Adobe Experience Manager verktyg för cachelagring och/eller belastningsutjämning som kan användas tillsammans med en webbserver i företagsklass.

Se [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) för fullständig information, särskilt [Konfigurera Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) för mer konfigurationsinformation.

### Konfigurerar AEM LiveCycle Connector {#configuring-aem-livecycle-connector}

I och med releasen av AEM dokumenttjänster och AEM dokumentsäkerhet har vi nu möjlighet att anropa LiveCycle doc-tjänsterna för att återge ett XFA-formulär, konvertera ett dokument till PDF och skydda ett dokument med hjälp av policyfunktioner. Läs [AEM LiveCycle Connector](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html) för mer information.

### Jobbavlastning och topologiadministration {#job-offloading-and-topology-administration}

[Avlastning](/help/sites-deploying/offloading.md) distribuerar bearbetningsuppgifter som är Experience Manager instanser i en topologi. Med avlastning kan du använda särskilda Experience Manager-instanser för att utföra vissa typer av bearbetning. Specialiserad bearbetning gör att du kan maximera användningen av tillgängliga serverresurser.

Topologier är löst kopplade Experience Manager-kluster som deltar i avlastning. Ett kluster består av en eller flera Experience Manager-serverinstanser (en enda instans betraktas som ett kluster).

Mer information om hur du visar eller ändrar topologimedlemskap finns i [Administrera topologier](/help/sites-deploying/offloading.md#administering-topologies) -avsnitt.

### Konfigurera välkomstkonsolen {#configuring-the-welcome-console}

Välkomstkonsolen för det klassiska användargränssnittet innehåller en lista med länkar till de olika konsolerna och funktionerna i AEM.

Det går att konfigurera synliga länkar, se [Konfigurera välkomstkonsolen](/help/sites-developing/customizing-the-welcome-console.md) för mer information.

### Konfigurera för prestanda {#configuring-for-performance}

[Prestanda](/help/sites-deploying/configuring-performance.md) är nyckeln till ditt projekt. Vissa aspekter av AEM (och/eller den underliggande databasen) kan konfigureras för att optimera prestanda.

Se [Konfigurera för prestanda](/help/sites-deploying/configuring-performance.md#configuring-for-performance) för mer information.

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### Delat datalager {#shared-data-store}

Databasens datalager används för att avlasta lagringen av stora binärfiler från databasen till ett separat område, så att flera instanser av samma binära (till exempel en bild) i databasträdet bara lagras en gång.

Den här funktionen&quot;store-once, reference-many-times&quot; kan utökas så att den inte bara innehåller ett enda databasträd utan helt separata databaser, genom att konfigurera datalagret för varje databas så att den refererar till samma delade filsystemplats.

Ett sådant datalager kan delas mellan olika noder i samma kluster, olika publicerings- och/eller författarinstanser i samma installation eller till och med helt separata instanser i olika installationer.

Mer information finns i [Konfigurera datalager och nodlager](/help/sites-deploying/data-store-config.md).

## Ytterligare konfigurationsöverväganden {#further-configuration-considerations}

### Aktivera HTTP över SSL {#enabling-http-over-ssl}

Du kan aktivera HTTP över SSL för att använda säkrare anslutningar till dina servrar.

Se [Aktivera HTTP över SSL](/help/sites-administering/ssl-by-default.md) för mer information.

### AEM portaler och portlets {#aem-portals-and-portlets}

En portal är ett webbprogram som innehåller personalisering, samlad inloggning, innehållsintegrering från olika källor och som är värd för informationssystemens presentationsskikt. Med portletkomponenten kan du även bädda in en portlet på sidan. För att få tillgång till innehåll som tillhandahålls av CQ5 WCM kan portalservern utrustas med CQ5 Portal Director Portlet. Du kan göra detta genom att installera, konfigurera och lägga till portleten på portalsidan.

Se [Portal och Portlets](/help/sites-administering/aem-as-portal.md) för mer information.

### Förfallotid för statiska objekt {#expiration-of-static-objects}

Statiska objekt (till exempel ikoner) ändras inte. Därför bör systemet konfigureras så att det inte upphör att gälla (under en rimlig tidsperiod) och på så sätt minskar onödig trafik.

Se [Förfallotid för statiska objekt](/help/sites-deploying/expiration-static-objects.md) för mer information.

### Öppna filer i Java-processen {#open-files-in-the-java-process}

Varje java-process kan komma åt filer - detta kräver systemresurser. Av den anledningen definieras en övre gräns för hur många filer varje process har åtkomst till samtidigt. Om detta överskrids kan ett undantagsfel uppstå.

Om AEM överstiger det högsta tillåtna antalet får meddelandet `too many open files`&quot; kommer att visas i `error.log`.

För att undvika sådana undantag måste du:

1. Kontrollera hur många öppna filer som AEM använder.

   Hur du gör den här kontrollen beror på vilken plattform instansen körs på. Verktyg som LSOF (Unix) eller Process Explorer (Windows) kan användas.

   Detta värde bör övervakas under utveckling och testning för att

   * bekräfta att filer stängs efter behov
   * fastställa det högsta värde som behövs (under olika omständigheter)

1. Ange högsta tillåtna värde.

   Det nya värdet bör ta hänsyn till både aktuella behov och framtida toppar, så det är tillrådligt att fördubbla nuvarande behov.

   Som standard `serverctl` configures `CQ_MAX_OPEN_FILES` till `8192`; detta bör räcka för de flesta scenarier.

### Konfigurera RTF-redigeraren {#configuring-the-rich-text-editor}

The **RTF-redigerare** (**RTE**) har ett stort antal [funktionalitet](/help/sites-authoring/rich-text-editor.md) för redigering av textinnehåll, som ger dem ikoner, valrutor och menyer för en WYSIWYG-upplevelse.

Se [Konfigurera RTF-redigeraren](/help/sites-administering/rich-text-editor.md) för mer information.

### Konfigurera Ångra för sidredigering {#configuring-undo-for-page-editing}

Det finns flera egenskaper som styr hur kommandona Ångra och Gör om fungerar när du redigerar sidor. Dessa kan konfigureras, se [Konfigurera Ångra för sidredigering](/help/sites-administering/config-undo.md) för mer information.

### Konfigurera videokomponenten {#configuring-the-video-component}

The [Videokomponent](/help/sites-authoring/default-components-foundation.md#video) Med kan du placera ett fördefinierat videoelement direkt på sidan.

Administratören måste [Installera FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg) separat. De kan också [Konfigurera videoprofiler](/help/sites-administering/config-video.md#configure-video-profiles) för användning med html5-element.

### Konfigurera och anpassa rapporter {#configuring-and-customizing-reports}

CQ ger dig möjlighet att övervaka och analysera instansens status och innehåller ett urval standardrapporter som kan konfigureras för dina individuella behov:

Se [Grunderna i anpassning av rapporter](/help/sites-administering/reporting.md#the-basics-of-report-customization) för mer information.

### Konfigurerar e-postmeddelande {#configuring-email-notification}

CQ skickar e-postmeddelanden till användare som:

* Prenumerera på sidhändelser, t.ex. ändring eller replikering.
* Prenumerera på forumevent.
* Måste utföra ett steg i ett arbetsflöde.

Se [Konfigurerar e-postmeddelande](/help/sites-administering/notification.md) för mer information.

### Aktivera sidavbildningar {#enabling-page-impressions}

Sidavbildningar visas i **Impressions** -kolumnen i den klassiska användargränssnittets platadminkonsol. Om du vill kunna hämta sidvisningar måste du konfigurera:

* I publiceringsinstansen:

   * [Dagens CQ WCM-sidstatistik](/help/sites-deploying/osgi-configuration-settings.md)

* På författarinstansen:

   * [Spårning för Adobe-sidestryck](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>Konfigurationen av spårningsfunktionen för Adobe-siduppläsningar i författarmiljön tillåter anonyma begäranden till spårningstjänsten.
