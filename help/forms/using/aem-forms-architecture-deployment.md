---
title: Arkitektur och driftsättningstopologier för AEM Forms
seo-title: Arkitektur och driftsättningstopologier för AEM Forms
description: Arkitekturinformation för AEM Forms och rekommenderade topologier för nya och befintliga AEM kunder och kunder som uppgraderar från LiveCycle ES4 till AEM Forms.
seo-description: Arkitekturinformation för AEM Forms och rekommenderade topologier för nya och befintliga AEM kunder och kunder som uppgraderar från LiveCycle ES4 till AEM Forms.
uuid: 90baa57a-4785-4b49-844c-a44717d3c12d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 0156b5c3-3bef-4213-9ada-c7b6ae96ada4
role: Administratör
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2491'
ht-degree: 0%

---


# Arkitektur och driftsättningstopologier för AEM Forms {#architecture-and-deployment-topologies-for-aem-forms}

## Arkitektur {#architecture}

AEM Forms är ett program som distribueras till AEM som ett AEM. Paketet kallas för AEM Forms tilläggspaket. AEM Forms-tilläggspaketet innehåller båda tjänsterna (API-providers), som distribueras i AEM OSGi-behållaren, och servlets eller JSP (som tillhandahåller både front-end- och REST API-funktioner) som hanteras av AEM Sling-ramverket. I följande diagram visas den här konfigurationen:

![arkitektur](assets/architecture.png)

Arkitekturen för AEM Forms innehåller följande komponenter:

* **AEM:** Grundläggande tjänster som AEM till ett distribuerat program. Dessa tjänster omfattar en JCR-kompatibel innehållsdatabas, en OSGI-tjänstbehållare, en arbetsflödesmotor, ett förtroendearkiv, en nyckelbehållare osv. Dessa tjänster är tillgängliga för AEM Forms-program, men tillhandahålls inte av AEM Forms-paket. Dessa tjänster är en integrerad del av den övergripande AEM och olika AEM Forms-komponenter använder dessa tjänster.
* **Forms-tjänster:** Tillhandahåll formulärrelaterade funktioner som att skapa, sammanställa, distribuera och arkivera PDF-dokument, lägga till digitala signaturer för att begränsa tillgången till dokument och avkoda streckkodsformulär. Dessa tjänster är allmänt tillgängliga för användning av anpassad kod som distribueras tillsammans i AEM.
* **webblager:** JSP eller serverlets, som bygger på vanliga tjänster och formulärtjänster, och som har följande funktioner:

   * **Författare**: Ett användargränssnitt för att skapa och hantera formulär.
   * **Formuläråtergivning och inskickning**: Ett användarvänligt gränssnitt som kan användas av AEM Forms-användare (t.ex. medborgare som besöker en myndighets webbplats). Detta ger formuläråtergivning (visa formulär i en webbläsare) och funktioner för att skicka in formulär.
   * **REST API**: JSP:er och serverlets exporterar en delmängd av formulärtjänster för fjärranvändning av HTTP-baserade klienter, t.ex. formulärets mobila SDK.

**AEM Forms på OSGi:** En AEM Forms på OSGi-miljö är standard-AEM Author eller AEM Publish med AEM Forms-paket driftsatt på den. Du kan köra AEM Forms på OSGi i en [servermiljö, servergrupp och grupperade inställningar](/help/sites-deploying/recommended-deploys.md). Klusterinställningar är bara tillgängliga för AEM Author-instanser.

**AEM Forms på JEE:** AEM Forms på JEE är en AEM Forms-server som körs på JEE-stacken. Den har AEM Author med AEM Forms tilläggspaket och ytterligare AEM Forms JEE-funktioner som kan användas tillsammans på en enda JEE-stack som körs på en programserver. Du kan köra AEM Forms på JEE i enserver- och gruppkonfigurationer. AEM Forms on JEE krävs endast för dokumentsäkerhet, processhantering och för LiveCycle som uppgraderar till AEM Forms. Här är några ytterligare scenarier för användning av AEM Forms i JEE:

* **Stöd för HTML-arbetsyta (för kunder som använder HTML-arbetsytan):** AEM Forms på JEE möjliggör enkel inloggning med bearbetningsinstanser, visar vissa resurser som återges i bearbetningsinstanser och hanterar inlämning av formulär som återges i HTML-arbetsytan.
* **Avancerad bearbetning** av ytterligare blanketter/interaktiva kommunikationsdata: AEM Forms on JEE kan användas för att ytterligare bearbeta formulär-/interaktiva kommunikationsdata (och spara resultaten i ett lämpligt datalager) i komplexa fall där avancerade processhanteringsfunktioner krävs.

AEM Forms on JEE innehåller även följande stödtjänster till AEM:

* **Integrerad användarhantering:** Gör att användare av AEM Forms på JEE kan identifieras som AEM formulär för OSGi-användare och möjliggör enkel inloggning för både OSGi- och JEE-användare. Detta krävs för scenarier där enkel inloggning mellan AEM på OSGi och AEM Forms på JEE krävs (till exempel HTML-arbetsyta).
* **Värdtjänster för resurser:** AEM Forms på JEE kan hantera resurser (till exempel HTML5-formulär) som återges på AEM Forms på OSGi.

AEM Forms redigeringsgränssnitt stöder inte skapande av DOR (Document of Record), PDF forms och HTML5 Forms. Sådana resurser är utformade med det fristående Forms Designer-programmet och överförs individuellt till AEM Forms Manager. För AEM Forms på JEE kan formulär även utformas som programresurser (i AEM Forms Workbench) och distribueras till AEM Forms på JEE-server.

AEM Forms på OSGi och AEM Forms på JEE har båda arbetsflödesfunktioner. Du kan snabbt skapa och distribuera grundläggande arbetsflöden för olika uppgifter i AEM formulär på OSGi, utan att behöva installera AEM Forms fullständiga processhanteringsfunktion på JEE. Det finns en viss skillnad i [funktionerna i det formulärbaserade arbetsflödet på AEM Forms i OSGi och Process Management-funktionen i AEM Forms i JEE](capabilities-osgi-jee-workflows.md). Utvecklandet och hanteringen av formulärcentrerade arbetsflöden i AEM Forms på OSGi använder de välbekanta AEM arbetsflödes- och AEM Inbox-funktionerna.

## Terminologier {#terminologies}

I följande bild visas olika AEM formulärserverkonfigurationer och deras komponenter som används i en typisk AEM Forms-distribution:

![aem_forms_-_recommendedtopology](assets/aem_forms_-_recommendedtopology.png)

**Författare:** En författarinstans är en AEM Forms-server som körs i standardkörningsläget Författare. Det kan vara AEM Forms på JEE eller AEM Forms i OSGi-miljö. Det är avsett för interna användare, formulärutvecklare och designers av interaktiv kommunikation. Det aktiverar följande funktioner:

* **Skapa och hantera formulär och interaktiv kommunikation:** Designers och utvecklare kan skapa och redigera adaptiva formulär och interaktiv kommunikation, överföra andra typer av formulär som skapats externt, till exempel formulär som skapats i Adobe Forms Designer, och hantera dessa resurser med Forms Manager-konsolen.
* **Publicering av formulär och interaktiv kommunikation:** resurser som lagras på en författarinstans kan publiceras till en publiceringsinstans för att utföra körningsåtgärder. Resurspublicering använder AEM replikeringsfunktioner. Adobe rekommenderar att en replikeringsagent är konfigurerad för alla författarinstanser för att manuellt skicka publicerade formulär till bearbetningsinstanser, och att en annan replikeringsagent är konfigurerad för att bearbeta instanser med utlösaren *On Receive* aktiverad för att automatiskt replikera mottagna formulär till publiceringsinstanser.

**Publicera:** En publiceringsinstans är en AEM Forms-server som körs i standardläget Publicera. Publiceringsinstanser är avsedda för slutanvändare av formulärbaserade program, t.ex. användare som öppnar en offentlig webbplats och som skickar formulär. Det aktiverar följande funktioner:

* Återge och skicka Forms för slutanvändare.
* Transport av obearbetade inlämnade formulärdata till bearbetningsinstanser för vidare bearbetning och lagring i det slutliga databassystemet. Standardimplementeringen i AEM Forms uppnår detta med AEM bakåtreplikeringsfunktioner. Det finns också en alternativ implementering för att skicka formulärdata direkt till bearbetningsservrar i stället för att spara dem lokalt först (det senare är en förutsättning för att omvänd replikering ska aktiveras). Kunder som oroar sig för lagring av potentiellt känsliga data på publiceringsinstanser kan gå in för denna [alternativa implementering](/help/forms/using/configuring-draft-submission-storage.md), eftersom bearbetningsinstanser vanligtvis ligger i en säkrare zon.
* Återge och skicka interaktiv kommunikation och interaktiva brev: En interaktiv kommunikation och ett interaktivt brev återges på publiceringsinstanser och motsvarande data skickas till bearbetningsinstanser för lagring och efterbearbetning. Data kan antingen sparas lokalt på en publiceringsinstans och återreplikeras till en bearbetningsinstans (standardalternativet) senare, eller skickas direkt till bearbetningsinstansen utan att sparas i publiceringsinstansen. Den senare implementeringen är användbar för säkerhetsmedvetna kunder.

**Bearbetning:** En instans av AEM Forms som körs i redigeringsläge utan användare tilldelade till formulärhanteringsgruppen. Du kan distribuera AEM Forms på JEE eller AEM Forms på OSGi som en bearbetningsinstans. Användarna är inte tilldelade att säkerställa att formulärredigerings- och hanteringsaktiviteter inte utförs på Bearbetning-instansen och bara inträffar på Author-instansen. En bearbetningsinstans aktiverar följande funktioner:

* **Bearbetning av råformulärsdata som kommer från en Publish-instans:** Detta uppnås huvudsakligen med en Processing-instans via AEM arbetsflöden som utlöser när data kommer. I arbetsflödena kan du använda steget Formulärdatamodell som du får när du vill arkivera data eller dokument i ett lämpligt datalager.
* **Säker lagring av formulärdata**: Bearbetningen är en databas bakom brandväggen för rådata som är isolerade från användarna. Varken formulärdesigners på författarinstansen eller slutanvändare på publiceringsinstansen har åtkomst till den här databasen.

   >[!NOTE]
   >
   > Adobe rekommenderar att du använder ett datalager från tredje part för att spara slutliga bearbetade data i stället för att använda AEM.

* **Lagring och efterbearbetning av korrespondensdata som kommer från en Publish-instans:** AEM arbetsflöden utför den valfria efterbearbetningen av motsvarande bokstavsdefinitioner. Dessa arbetsflöden kan spara de slutliga bearbetade data i lämpliga externa datalager.

* **Värdtjänst** för HTML-arbetsyta: En bearbetningsinstans är värd för frontend för HTML Workspace. HTML-arbetsytan innehåller användargränssnittet för associerade uppgifter/grupptilldelningar för gransknings- och godkännandeprocesser.

En bearbetningsinstans har konfigurerats att köras i redigeringskörningsläget på grund av:

* Det möjliggör omvänd replikering av rådata från en Publish-instans. Standardhanteraren för datalagring kräver funktionen för omvänd replikering.
* AEM arbetsflöden, som är det primära sättet att bearbeta råformulärsdata som kommer från en publiceringsinstans, rekommenderas för körning i ett system av utvecklartyp.

## Exempel på fysiska topologier för AEM Forms på JEE {#sample-physical-topologies-for-aem-forms-on-jee}

De AEM Forms on JEE-topologier som rekommenderas nedan gäller främst kunder som uppgraderar från LiveCycle eller en tidigare version av AEM Forms på JEE. Adobe rekommenderar att AEM Forms används på OSGi för nya installationer. En ny installation av AEM Forms på JEE rekommenderas endast för dokumentsäkerhet och processhantering.

### Topologi för att använda dokumenttjänster eller dokumentsäkerhetsfunktioner {#topology-for-using-document-services-or-document-security-capabilities}

AEM Forms-kunder som bara planerar att använda dokumenttjänster eller dokumentsäkerhetsfunktioner kan ha en topologi som liknar den som visas nedan. Den här topologin rekommenderar att du använder en enda instans av AEM Forms. Du kan också skapa ett kluster eller en grupp med AEM Forms-servrar om det behövs. Den här topologin rekommenderas när de flesta användare programmässigt får tillgång till funktioner på AEM Forms-servern och det krävs minsta möjliga ingrepp via användargränssnittet. Topologin är användbar vid gruppbearbetning av dokumenttjänster. Du kan till exempel använda utdatatjänsten för att skapa hundratals icke-redigerbara PDF-dokument dagligen.

Även om AEM Forms låter dig konfigurera och köra alla funktioner från en enda server bör du ändå göra kapacitetsplanering, lastbalansering och konfigurera dedikerade servrar för specifika funktioner i en produktionsmiljö. I en miljö som använder tjänsten PDF Generator för att konvertera tusentals sidor om dagen och lägga till digitala signaturer för att begränsa åtkomsten till dokumenten, kan du skapa separata AEM Forms-servrar för tjänsten PDF Generator och funktioner för digitala signaturer. Det ger optimala prestanda och skalar servrarna oberoende av varandra.

![grundläggande funktioner](assets/basic-features.png)

### Topologi för AEM Forms processhantering {#topology-for-using-aem-forms-process-management}

AEM Forms-kunder som planerar att använda AEM Forms processhanteringsfunktioner kan till exempel ha en topologi som liknar den som visas nedan. AEM Forms på JEE-servern kan vara i en enda server- eller klusterkonfiguration.

Om du uppgraderar från LiveCycle ES4 speglar denna topologi noga det du redan har i LiveCycle, förutom att AEM Author är inbyggt i AEM Forms på JEE. Dessutom ändras inte kraven på klustring för kunder som utför en uppgradering. Om du använder AEM Forms i en klustermiljö kan du fortsätta med samma sak i AEM 6.5 Forms. För en ny installation av AEM Forms av JEE för HTML-arbetsytan är det ytterligare ett krav att köra AEM författarinstans inbyggd i JEE-miljön.

Formulärdatalagret är ett datalager från tredje part som används för att lagra slutliga bearbetade data av formulär och interaktiv kommunikation. Detta är ett valfritt element i topologin. Du kan också välja att konfigurera en bearbetningsinstans och använda dess databas som det slutliga systemet för post, om det behövs.

![topology_for_usinghtmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

Topologin rekommenderas för kunder som planerar att använda AEM Forms på en JEE-server för processhanteringsfunktioner (HTML Workspace) utan att behöva använda någon efterbearbetning, adaptiva formulär, HTML5-formulär eller interaktiv kommunikationskapacitet.

### Topologi för användning av adaptiva formulär, HTML5-formulär, interaktiva kommunikationsfunktioner {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

AEM Forms-kunder som planerar att använda AEM Forms funktioner för datainhämtning, till exempel adaptiva formulär, HTML5 Forms, PDF forms, kan ha en topologi som liknar den som visas nedan. Denna topologi rekommenderas också för interaktiv kommunikation i AEM Forms.

![topology-for-using-forms-osgi-modules](assets/topology-for-using-forms-osgi-modules.png)

Du kan göra följande ändringar/anpassningar av ovanstående föreslagna topologi:

* Om du vill använda HTML Workspace och AEM Forms-appen måste du ha en AEM författare eller bearbetningsinstans. Du kan använda den AEM författarinstansen som är inbyggd i AEM Forms på JEE-servern i stället för att konfigurera ytterligare en extern AEM författarserver.
* En AEM Author- eller Processing-instans krävs endast för Forms-centrerade arbetsflöden i OSGi, adaptiva formulär, formulärportalen och interaktiv kommunikation.
* gränssnitt för interaktiv kommunikationsagent körs vanligtvis inom organisationen. Du kan därför behålla en publiceringsserver för agentanvändargränssnittet i det privata nätverket.
* AEM formulär på OSGi-instansen inbyggda i AEM Forms på JEE-servern kan även köra Forms-centrerade arbetsflöden på OSGi och Bevakade mappar.

## Exempel på fysiska topologier för användning av AEM Forms på OSGi {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### Topology for data capture, interactive communication, Form-Centric Workflow on OSGi capabilities {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

AEM Forms-kunder som planerar att använda AEM Forms funktioner för datainhämtning, till exempel adaptiva formulär, HTML5 Forms, PDF forms, kan ha en topologi som liknar den som visas nedan. Den här topologin rekommenderas också för interaktiv kommunikation och Forms-centrerade arbetsflöden för OSGi-funktioner, till exempel för användning av AEM Inbox och AEM Forms App för arbetsflöden med affärsprocesser.

![interactive-use-cases-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### Topologi för att använda bevakade mappfunktioner för batchbearbetning offline {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

AEM Forms-kunder som planerar att använda bevakade mappar för batchbearbetning kan ha en topologi som liknar den som visas nedan. Topologin visar en klustrad miljö, men du bestämmer dig för att använda en enda instans eller en grupp AEM Forms-servrar beroende på inläsningen. Tredjepartsdatakällan är ditt eget postsystem. Den fungerar som indatakälla för bevakade mappar. Topologin visar också utdata i form av en utskriven fil. Du kan också lagra utdatainnehållet i ett filsystem, skicka via e-post och använda andra anpassade metoder för att förbruka utdata.

![offline-batch-processing-via-watch-folders](assets/offline-batch-processing-via-watched-folders.png)

### Topologi för att använda dokumenttjänster för offline-API-baserad bearbetning {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

AEM Forms-kunder som bara planerar att använda dokumenttjänster kan ha en topologi som liknar den som visas nedan. Den här topologin rekommenderar att du använder ett kluster av AEM Forms på OSGi-servrar. Den här topologin rekommenderas när de flesta användare använder API:er via programmering för att få åtkomst till AEM Forms-servrar och ett ingripande via användargränssnittet är minimum. Topologin är mycket användbar i olika kundscenarier. Till exempel kan flera klienter använda PDF Generator-tjänsten för att skapa PDF-dokument på begäran.

Även om du kan använda AEM Forms för att konfigurera och köra alla funktioner från en enda server, bör du göra kapacitetsplanering, lastbalansering och konfigurera dedikerade servrar för specifika funktioner i en produktionsmiljö. Om du till exempel använder tjänsten PDF Generator för att konvertera tusentals sidor om dagen och flera adaptiva formulär för att hämta in data, kan du skapa separata AEM Forms-servrar för tjänsten PDF Generator och funktioner för adaptiva formulär. Det ger optimala prestanda och skalar servrarna oberoende av varandra.

![offline-api-baserad-bearbetning](assets/offline-api-based-processing.png)

