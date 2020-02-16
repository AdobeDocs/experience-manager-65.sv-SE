---
title: Bästa praxis för arbetsflöden
seo-title: Bästa praxis för arbetsflöden
description: 'null'
seo-description: 'null'
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Bästa praxis för arbetsflöden{#workflow-best-practices}

Med arbetsflöden kan ni automatisera Adobe Experience Manager-aktiviteter (AEM).

De representerar ofta en stor del av den bearbetning som sker i en AEM-miljö, så när anpassade arbetsflödessteg inte skrivs enligt bästa praxis, eller när färdiga arbetsflöden inte är konfigurerade att köras så effektivt som möjligt, kan systemet drabbas av detta.

Vi rekommenderar därför att du noga planerar implementeringarna av arbetsflödena.

## Konfiguration {#configuration}

När du konfigurerar arbetsflödesprocesser (anpassade och/eller färdiga) finns det några saker som du bör tänka på.

### Övergående arbetsflöden {#transient-workflows}

För att optimera stora mängder insatsmaterial kan du definiera ett [arbetsflöde som övergående](/help/sites-developing/workflows.md#transient-workflows).

När ett arbetsflöde är övergående bevaras inte körningsdata som relaterar till de mellanliggande arbetsstegen i JCR när de körs (utdatarenderingarna behålls förstås).

Fördelarna kan vara:

* En minskning av arbetsflödets bearbetningstid. upp till 10 %.
* Minska databastillväxten avsevärt.
* Inga fler CRUD-arbetsflöden behövs för att rensa bort.
* Dessutom minskar det antalet TAR-filer som ska komprimeras.

>[!CAUTION]
>
>Aktivera inte den här funktionen om ditt företag kräver att du ska spara/arkivera arbetsflödets körningsdata för granskning.

### Justera arbetsflöden för DAM {#tuning-dam-workflows}

Riktlinjer för prestandajustering för DAM-arbetsflöden finns i prestandajusteringsguiden för [AEM Resurser](/help/assets/performance-tuning-guidelines.md).

### Konfigurera maximalt antal samtidiga arbetsflöden {#configure-the-maximum-number-of-concurrent-workflows}

AEM kan tillåta flera arbetsflödestrådar att köras samtidigt. Som standard är antalet trådar konfigurerat till halva antalet processorkärnor i systemet.

I de fall där arbetsflödena som körs kräver systemresurser, kan detta innebära att det inte finns mycket kvar för AEM att använda för andra åtgärder, som att återge redigeringsgränssnittet. Det kan leda till att systemet blir trögt under aktiviteter som massöverföring av bilder.

Adobe rekommenderar att du konfigurerar antalet **maximala parallella jobb** till mellan hälften och tre fjärdedelar av antalet processorkärnor i systemet för att åtgärda problemet. Detta bör ge tillräcklig kapacitet för att systemet ska kunna vara responsivt när dessa arbetsflöden bearbetas.

Om du vill konfigurera **maximalt antal parallella jobb** kan du antingen:

* Konfigurera **[OSGi-konfigurationen](/help/sites-deploying/configuring-osgi.md)**från AEM Web Console; för **kö: Begränsa arbetsflödeskö**(en **konfiguration**för Apache Sling-jobbkö).

* Konfigurera kön med alternativet **Sling Jobs** i AEM Web Console. för **jobbkökonfiguration: Begränsa arbetsflödeskö**, på `http://localhost:4502/system/console/slingevent`.

Dessutom finns det en separat konfiguration för **jobbkön** för den externa processen Bevilja arbetsflöde. Detta används för arbetsflödesprocesser som startar externa binärfiler, till exempel **InDesign Server** eller **Image Magick**.

### Konfigurera enskilda jobbköer {#configure-individual-job-queues}

I vissa fall kan det vara användbart att konfigurera enskilda jobbköer för att styra samtidiga trådar eller andra köalternativ, utifrån enskilda jobb. Du kan lägga till och konfigurera en enskild kö från webbkonsolen via **konfigurationsfabriken** för Apache Sling Job Queue. Om du vill hitta rätt ämne att lista kör du arbetsflödets modell och letar efter den i **Sling Jobs** -konsolen. till exempel på `http://localhost:4502/system/console/slingevent`.

Enskilda jobbköer kan även läggas till för tillfälliga arbetsflöden.

### Konfigurera rensning av arbetsflöde {#configure-workflow-purging}

I en standardinstallation tillhandahåller AEM en underhållskonsol där dagliga och veckovisa underhållsaktiviteter kan schemaläggas och konfigureras. till exempel:

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

Som standard har **veckounderhållsfönstret** en **tömningsåtgärd** för arbetsflöde, men detta måste konfigureras innan det kan köras. Om du vill konfigurera rensning av arbetsflöden måste en ny **Adobe Granite Workflow Renge Configuration** läggas till i webbkonsolen.

Mer information om underhållsåtgärder i AEM finns i [Operations Dashboard](/help/sites-administering/operations-dashboard.md).

## Anpassning {#customization}

När du skriver anpassade arbetsflödesprocesser finns det vissa saker som du bör tänka på.

### Platser {#locations}

Definitioner av arbetsflödesmodeller, startverktyg, skript och meddelanden lagras i databasen efter typ. dvs. färdiga, anpassade, bland annat.

>[!NOTE]
>
>Se även [Repository-omstrukturering i AEM 6.5](/help/sites-deploying/repository-restructuring.md).

#### Platser - arbetsflödesmodeller {#locations-workflow-models}

Arbetsflödesmodeller lagras i databasen enligt typ:

* Färdiga arbetsflöden finns under följande sökväg:

   `/libs/settings/workflow/models/`

   >[!CAUTION]
   >
   >Gör inte:
   >
   >* placera någon av dina anpassade arbetsflödesmodeller i den här mappen
   >* redigera vad som helst i `/libs`
   >
   >Alla ändringar kan skrivas över vid uppgradering eller vid installation av snabbkorrigeringar, kumulativa korrigeringspaket eller servicepaket.

* Anpassade arbetsflödesdesigner finns under:

   ```
   /conf/global/settings/workflow/models/...
   ```

* Arbetsflödesdesign vid körning (både färdiga och anpassade) finns på följande sökväg:

   `/var/workflow/models/`

* Äldre arbetsflödesdesign (både designtid och körningsmiljö) finns under följande sökväg:

   `/etc/workflow/models/`

   >[!NOTE]
   >
   >Om dessa designer redigeras *med AEM UI* kopieras informationen till de nya platserna.

#### Platser - Starta arbetsflöden {#locations-workflow-launchers}

Definitioner av arbetsflödets startprogram lagras också i databasen enligt typ:

* Körklara startprogram för arbetsflöden finns under följande sökväg:

   `/libs/settings/workflow/launcher/`

   >[!CAUTION]
   >
   >Gör inte:
   >
   >* placera någon av dina anpassade startsidor för arbetsflöden i den här mappen
   >* redigera vad som helst i `/libs`
   >
   >Alla ändringar kan skrivas över vid uppgradering eller vid installation av snabbkorrigeringar, kumulativa korrigeringspaket eller servicepaket.

* Skräddarsydda arbetsflödesstarter finns under:

   ```
   /conf/global/settings/workflow/launcher/...
   ```

* Inledande arbetsflöden finns på följande sökväg:

   `/etc/workflow/launcher/`

   >[!NOTE]
   >
   >Om dessa definitioner redigeras *med AEM-gränssnittet* kopieras informationen till de nya platserna.

#### Platser - arbetsflödesskript {#locations-workflow-scripts}

Arbetsflödesskript lagras också i databasen enligt typ:

* Skript för färdiga arbetsflöden finns under följande sökväg:

   `/libs/workflow/scripts/`

   >[!CAUTION]
   >
   >Gör inte:
   >
   >* placera något av dina anpassade arbetsflödesskript i den här mappen
   >* redigera vad som helst i `/libs`
   >
   >Alla ändringar kan skrivas över vid uppgradering eller vid installation av snabbkorrigeringar, kumulativa korrigeringspaket eller servicepaket.

* Skript för anpassade arbetsflöden finns under:

   ```
   /apps/workflow/scripts/...
   ```

* Äldre arbetsflödesskript sparas under följande sökväg:

   `/etc/workflow/scripts/`

#### Platser - arbetsflödesmeddelanden {#locations-workflow-notifications}

Arbetsflödesmeddelanden lagras också i databasen enligt typ:

* Meddelandedefinitioner för färdiga arbetsflöden finns under följande sökväg:

   `/libs/settings/workflow/notification/`

   >[!CAUTION]
   >
   >Gör inte:
   >
   >* placera någon av de anpassade definitionerna för arbetsflödesmeddelanden i den här mappen
   >* redigera vad som helst i `/libs`
   >
   >Alla ändringar kan skrivas över vid uppgradering eller vid installation av snabbkorrigeringar, kumulativa korrigeringspaket eller servicepaket.

* Definitioner för anpassade arbetsflödesmeddelanden finns under:

   ```
   /conf/global/settings/workflow/notification/...
   ```

   >[!NOTE]
   >
   >Om du vill åsidosätta en meddelandetext i arbetsflödet skapar du en åsidosatt sökväg under:
   >
   >
   >`/conf/global/settings/workflow/notification/<path-under-libs>`

* De äldre definitionerna för arbetsflödesmeddelanden finns under följande sökväg:

   `/etc/workflow/notification/`

### Bearbeta sessioner {#process-sessions}

Som vid all anpassad utveckling bör du alltid använda en användarsession när det är möjligt:

* för att följa riktlinjerna för säkerhet på bästa sätt
* så att systemet kan hantera öppning och stängning av sessionen

När en arbetsflödesprocess implementeras:

* En arbetsflödessession tillhandahålls och bör användas om det inte finns någon tvingande anledning att inte göra det.
* Nya sessioner ska inte skapas från arbetsflödessteg eftersom detta orsakar inkonsekvenser i tillståndet/tillstånden tillsammans med eventuella samtidiga problem i arbetsflödesmotorn.
* Du bör inte hämta en ny JCR-session från ett processsteg i ett arbetsflöde. du bör anpassa arbetsflödessessionen som tillhandahålls av API:t för processsteg till en jcr-session. Exempel:

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

Spara en session:

* Om arbetsflödet används för att ändra databasen och sessionen inte sparas explicit i arbetsflödet, kommer arbetsflödet att spara sessionen när den är klar. `WorkflowSession`
* `Session.Save` ska inte anropas inifrån ett arbetsflödessteg:

   * Vi rekommenderar att arbetsflödets jcr-session anpassas. är då inte `save` nödvändigt eftersom arbetsflödesmotorn sparar sessionen automatiskt när arbetsflödet har slutförts.
   * rekommenderas inte för ett processsteg för att skapa en egen jcr-session.

* Genom att eliminera onödiga besparingar kan du minska omkostnaderna och på så sätt effektivisera arbetsflödena.

>[!CAUTION]
>
>Om du skapar en egen jcr-session, trots rekommendationerna här, måste den sparas.

### Minimera antal/omfattning för startare {#minimize-the-number-scope-of-launchers}

Det finns en avlyssnare som ansvarar för alla registrerade [arbetsflödeskörare](/help/sites-administering/workflows-starting.md#workflows-launchers) :

* Den lyssnar efter ändringar på alla sökvägar som anges i de andra startarnas globbing-egenskaper.
* När en händelse skickas utvärderas varje startprogram av arbetsflödesmotorn för att avgöra om den ska köras.

Om du skapar för många startprogram kommer utvärderingsprocessen att gå långsammare.

Om du skapar en globbningssökväg i roten av databasen för en enskild startfunktion kan arbetsflödesmotorn avlyssna och utvärdera händelserna create/modify för alla noder i databasen. Därför rekommenderar vi att du bara skapar startprogram som behövs och att du gör ordlistan så specifik som möjligt.

På grund av hur de här startverktygen påverkar arbetsflödets beteende kan det även vara bra att inaktivera användningsklara startprogram som inte används.

### Konfigurationsförbättringar för startare {#configuration-enhancements-for-launchers}

Den anpassade [startkonfigurationen](/help/sites-administering/workflows-starting.md#workflows-launchers) har förbättrats så att den har stöd för följande:

* Ha flera villkor&quot;OCH&quot; tillsammans.
* Har ELLER-villkor i ett enda villkor.
* Inaktivera/aktivera startprogram baserat på om en funktionsflagga är aktiverad eller inaktiverad.
* Support regex under startförhållanden.

### Starta inte arbetsflöden från andra arbetsflöden {#do-not-start-workflows-from-other-workflows}

Arbetsflöden kan medföra en avsevärd mängd overheadkostnader, både när det gäller objekt som skapas i minnet och noder som spåras i databasen. Därför är det bättre att ha ett arbetsflöde som hanterar själva arbetsflödet i stället för att starta ytterligare arbetsflöden.

Ett exempel på detta är ett arbetsflöde som implementerar en affärsprocess för en uppsättning innehåll och sedan aktiverar innehållet. Det är bättre att skapa en anpassad arbetsflödesprocess som aktiverar var och en av dessa noder, i stället för att starta en **aktiveringsmodell** för varje innehållsnod som behöver publiceras. Det här arbetssättet kräver ytterligare utvecklingsarbete, men är mer effektivt när det körs än att starta en separat arbetsflödesinstans för varje aktivering.

Ett annat exempel är ett arbetsflöde som bearbetar ett antal noder, skapar ett arbetsflödespaket och sedan aktiverar det paketet. I stället för att skapa paketet och sedan starta ett separat arbetsflöde med paketet som nyttolast, kan du ändra arbetsflödets nyttolast i det steg som skapar paketet och sedan anropa steget för att aktivera paketet i samma arbetsflödesmodell.

### Avancerad hanterare {#handler-advance}

När du utformar en arbetsflödesmodell kan du aktivera hanterare i dina arbetsflödessteg. Du kan också lägga till kod i arbetsflödessteget för att avgöra vilket steg som ska köras härnäst och sedan köra det.

Vi rekommenderar att du använder hanterarframsteg eftersom de ger bättre prestanda.

### Arbetsflödessteg {#workflow-stages}

Du kan definiera [arbetsflödesfaser](/help/sites-developing/workflows.md#workflow-stages)och sedan tilldela uppgifter/steg till en viss arbetsflödesfas.

Den här informationen används för att visa förloppet för ett arbetsflöde när du klickar på fliken [**Arbetsflödesinformation **i ett arbetsobjekt från** Inkorgen **](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). Befintliga arbetsflödesmodeller kan redigeras för att lägga till faser.

### Aktivera steg för sidprocess {#activate-page-process-step}

Steget **Aktivera sidprocess** aktiverar sidor åt dig, men inga refererade DAM-resurser hittas automatiskt och de aktiveras också.

Detta är något att tänka på om du tänker använda det här steget som en del av en arbetsflödesmodell.

### Överväganden vid uppgradering {#upgrade-considerations}

När du uppgraderar din instans:

* Kontrollera att alla anpassade arbetsflödesmodeller säkerhetskopieras innan en instans uppgraderas.
* bekräfta att inga av dina anpassade arbetsflöden lagras under [platsen](#locations):

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>Se även [Repository-omstrukturering i AEM 6.5](/help/sites-deploying/repository-restructuring.md).

## Systemverktyg {#system-tools}

Det finns många systemverktyg som du kan använda för att övervaka, underhålla och felsöka arbetsflöden. Alla exempel-URL:er nedan använder `localhost:4502`men bör vara tillgängliga för alla författarinstanser ( `<hostname>:<port>`).

### Sling Job Handling Console {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

Sling Job Handling-konsolen visar:

* Statistik över status för jobb i systemet sedan den senaste omstarten.
* Den visar också konfigurationerna för alla jobbköer och ger en genväg till redigering i konfigurationshanteraren.

### Verktyg för arbetsflödesrapport {#workflow-report-tool}

Arbetsflödesrapportverktyget tas bort i 6.3 för att förhindra prestandaförsämring.

### MBean för underhållsåtgärder för arbetsflöde {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

MBean för arbetsflödesunderhåll visar flera praktiska underhållsrutiner, som att tömma slutförda arbetsflöden och hämta arbetsflödesstatistik.

## Ytterligare information {#further-information}

Mer information finns i:

* [Arbeta med arbetsflöden](/help/sites-authoring/workflows.md)
* [Administrera arbetsflöden](/help/sites-administering/workflows.md)
* [Utveckla och utöka arbetsflöden](/help/sites-developing/workflows.md)
* [Prestandaoptimering](/help/sites-deploying/configuring-performance.md)