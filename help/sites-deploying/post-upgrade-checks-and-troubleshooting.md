---
title: Kontrollera och felsök efter uppgradering
seo-title: Kontrollera och felsök efter uppgradering
description: Lär dig hur du felsöker problem som kan uppstå efter en uppgradering.
seo-description: Lär dig hur du felsöker problem som kan uppstå efter en uppgradering.
uuid: 3f525f2c-8d25-4bb8-a57e-3adf667edde8
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 5a67aa9f-e5eb-4d7e-89da-2ee1a45eb8ce
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Kontrollera och felsök efter uppgradering{#post-upgrade-checks-and-troubleshooting}

## Bokför uppgraderingskontroller {#post-upgrade-checks}

Efter den [lokala uppgraderingen](/help/sites-deploying/in-place-upgrade.md) ska följande aktiviteter utföras för att slutföra uppgraderingen. Det antas att AEM har startats med 6.5-behållaren och att den uppgraderade kodbasen har distribuerats.

* [Verifiera loggar för uppgraderingen](#main-pars-header-290365562)

* [Verifiera OSGi Bundles](#main-pars-header-1637350649)

* [Verifiera Oak-version](#main-pars-header-1293049773)

* [Granska mappen PreUpgradeBackup](#main-pars-header-988995987)

* [Inledande validering av sidor](#main-pars-header-20827371)
* [Använd AEM-servicepaket](#main-pars-header-215142387)

* [Migrera AEM-funktioner](#main-pars-header-1434457709)

* [Verifiera schemalagda underhållskonfigurationer](#main-pars-header-1552730183)

* [Aktivera replikeringsagenter](#main-pars-header-823243751)

* [Aktivera anpassade schemalagda jobb](#main-pars-header-244535083)

* [Kör testplan](#main-pars-header-1167972233)

### Verifiera loggar för lyckad uppgradering {#verify-logs-for-upgrade-success}

**upgrade.log**

Tidigare krävdes noggrann kontroll av olika loggfiler, delar av databasen och startplattan för att kontrollera status efter uppgraderingen av instansen. Genom att generera en rapport efter uppgraderingen kan du upptäcka defekta uppgraderingar innan du publicerar den.

Huvudsyftet med den här funktionen är att minska behovet av manuell tolkning eller komplex parsningslogik för flera slutpunkter som krävs för att en uppgradering ska lyckas. Lösningen syftar till att tillhandahålla entydig information för externa automatiseringssystem som kan reagera på om en uppdatering lyckas eller inte.

Mer specifikt säkerställer det att

* Uppgraderingsfel som upptäcks av uppgraderingsramverket kan centraliseras i en enda uppgraderingsrapport.
* Uppgraderingsrapporten innehåller indikatorer om nödvändigt manuellt ingripande.

För att detta ska fungera har ändringar gjorts i hur loggarna genereras i `upgrade.log` filen.

Här följer ett exempel på en rapport som inte visar några fel under uppgraderingen:

![1487887443006](assets/1487887443006.png)

Här följer ett exempel på en rapport som visar ett paket som inte installerades under uppgraderingsprocessen:

![1487887532730](assets/1487887532730.png)

**error.log**

error.log bör granskas noggrant under och efter starten av AEM med målversionen jar. Alla varningar och fel bör granskas. I allmänhet är det bäst att söka efter problem i början av loggen. Fel som inträffar senare i loggen kan i själva verket vara biverkningar av en rotorsak som anropas tidigt i filen. Om upprepade fel och varningar inträffar, se nedan för [analys av problem med uppgraderingen](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade).

### Verifiera OSGi Bundles {#verify-osgi-bundles}

Navigera till OSGi-konsolen `/system/console/bundles` och kontrollera om några paket inte har startats. Om något paket är installerat kan du ta reda på vad som är `error.log` orsaken.

### Verifiera Oak-version {#verify-oak-version}

Efter uppgraderingen ser du att Oak-versionen har uppdaterats till **1.10.2**. Verifiera Oak-versionen genom att navigera till OSGi-konsolen och titta på den version som är associerad med Oak bundles: Oak Core, Oak Commons, Oak Segment tar.

### Inspektera mappen PreUpgradeBackup {#inspect-preupgradebackup-folder}

Under uppgraderingen försöker AEM säkerhetskopiera anpassningar och lagra dem under `/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>`. Om du vill visa den här mappen i CRXDE Lite måste du kanske [tillfälligt aktivera CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

Mappen med tidsstämpeln ska ha en egenskap med namnet `mergeStatus` med värdet `COMPLETED`. Mappen **som ska bearbetas** ska vara tom och den **överskrivna** noden anger vilka noder som skrevs över under uppgraderingen. Innehåll under **vänsternoden** visar innehåll som inte gick att sammanfoga säkert under uppgraderingen. Om implementeringen är beroende av någon av de underordnade noderna (och inte redan har installerats av det uppgraderade kodpaketet) måste de sammanfogas manuellt.

Inaktivera CRXDE Lite efter den här övningen om den finns på en scen- eller produktionsmiljö.

### Inledande validering av sidor {#initial-validation-of-pages}

Utför en inledande validering mot flera sidor i AEM. Om du uppgraderar en redigeringsmiljö öppnar du Start-sidan och välkomstsidan ( `/aem/start.html`, `/libs/cq/core/content/welcome.html`). I både redigerings- och publiceringsmiljöer öppnas några programsidor och röktester som återges korrekt. Om det uppstår några problem kan du läsa `error.log` för att felsöka.

### Använd AEM-servicepaket {#apply-aem-service-packs}

Använd alla relevanta AEM 6.5-servicepaket om de har släppts.

### Migrera AEM-funktioner {#migrate-aem-features}

Flera funktioner i AEM kräver ytterligare steg efter uppgraderingen. En fullständig lista över de här funktionerna och stegen för att migrera dem i AEM 6.5 finns på sidan [Uppgraderingskod och anpassningar](/help/sites-deploying/upgrading-code-and-customizations.md) .

### Verifiera schemalagda underhållskonfigurationer {#verify-scheduled-maintenance-configurations}

#### Aktivera skräpinsamling för datalager {#enable-data-store-garbage-collection}

Om du använder ett fildatalager måste du se till att skräpinsamlingsaktiviteten för datalagret är aktiverad och läggs till i listan Veckounderhåll. Instruktioner beskrivs [här](/help/sites-administering/data-store-garbage-collection.md).

>[!NOTE]
>
>Detta rekommenderas inte för anpassade datalagerinstallationer i S3 eller när ett delat datalager används.

#### Aktivera rensning av onlineändringar {#enable-online-revision-cleanup}

Om du använder MongoMK eller det nya StjärmMK-segmentformatet ser du till att aktiviteten Revision Clean Up (Revision Clean Up) är aktiverad och läggs till i listan Daily Maintenance (Dagligt underhåll). Instruktioner som beskrivs [här](/help/sites-deploying/revision-cleanup.md).

### Kör testplan {#execute-test-plan}

Kör detaljerad testplan mot den definierade [uppgraderingskoden och anpassningarna](/help/sites-deploying/upgrading-code-and-customizations.md) under avsnittet **Testprocedur** .

### Aktivera replikeringsagenter {#enable-replication-agents}

När publiceringsmiljön har uppgraderats och validerats aktiverar du replikeringsagenter i redigeringsmiljön. Kontrollera att agenter kan ansluta till respektive publiceringsinstanser. Se [Uppgraderingsprocedur](/help/sites-deploying/upgrade-procedure.md) för mer information om händelseordningen.

### Aktivera anpassade schemalagda jobb {#enable-custom-scheduled-jobs}

Alla schemalagda jobb som en del av kodbasen kan nu aktiveras.

## Analysera problem med uppgraderingen {#analyzing-issues-with-upgrade}

Det här avsnittet innehåller några problemscenarier som man kan ställas inför under uppgraderingsprocessen till AEM 6.3.

Dessa scenarier bör hjälpa till att hitta orsaken till uppgraderingsrelaterade problem och bör hjälpa till att identifiera projekt- eller produktspecifika problem.

### Databasmigreringen misslyckades {#repository-migration-failing-}

Datamigrering från CRX2 till Oak bör vara möjlig för alla scenarier som börjar med källinstanser baserade på CQ 5.4. Se till att du följer uppgraderingsinstruktionerna i det här dokumentet, som innehåller förberedelsen av `repository.xml`dokumentet, och se till att ingen anpassad autentiserare startas via JAAS och att instansen har kontrollerats för inkonsekvenser innan migreringen startar.

Om migreringen fortfarande misslyckas kan du ta reda på vad som är grundorsaken genom att undersöka `upgrade.log`. Om problemet inte är känt ännu, rapportera det till kundsupport.

### Uppgraderingen kördes inte {#the-upgrade-did-not-run}

Innan du startar förberedelsestegen måste du först köra **källinstansen** genom att köra den med kommandot java -jar aem-quickstart.jar. Detta krävs för att filen quickstart.properties ska kunna genereras korrekt. Om den saknas fungerar inte uppgraderingen. Du kan också kontrollera om filen finns genom att söka under `crx-quickstart/conf` installationsmappen för källinstansen. När du startar AEM för att starta uppgraderingen måste den dessutom köras med kommandot java -jar aem-quickstart.jar. Att starta från ett startskript startar inte AEM i uppgraderingsläge.

### Paket och paket kunde inte uppdateras {#packages-and-bundles-fail-to-update-}

Om paketen inte installeras under uppgraderingen kommer de paket de innehåller inte heller att uppdateras. Den här kategorin av problem orsakas vanligtvis av felkonfigurering av datalagret. De visas också som **ERROR** - och **WARN** -meddelanden i error.log. Eftersom standardinloggningen i de flesta fall kanske inte fungerar kan du använda CRXDE direkt för att undersöka och hitta konfigurationsproblemen.

### Vissa AEM Bundles växlar inte till det aktiva läget {#some-aem-bundles-are-not-switching-to-the-active-state}

Om paketen inte startar bör du kontrollera om du inte är nöjd med beroendet.

Om det här problemet uppstår men baseras på en misslyckad paketinstallation som ledde till att paket inte uppgraderas, kommer de att anses vara inkompatibla för den nya versionen. Mer information om hur du felsöker detta finns i **Paket och paket som inte kan uppdateras** ovan.

Vi rekommenderar också att du jämför paketlistan för en ny AEM 6.5-instans med den uppgraderade instansen för att identifiera de paket som inte uppgraderats. Detta ger en närmare beskrivning av vad du ska söka efter i `error.log`.

### Anpassade paket växlar inte till aktivt läge {#custom-bundles-not-switching-to-the-active-state}

Om dina anpassade paket inte växlar till det aktiva läget är det mest troligt att det finns kod som inte importerar ändrings-API. Detta leder ofta till missnöjda beroenden.

API som har tagits bort ska markeras som borttaget i en av de tidigare versionerna. Instruktioner om direktmigrering av koden finns i det här meddelandet om borttagning. Adobe planerar semantisk versionshantering där det är möjligt så att versionerna kan visa på förändringar som går förlorade.

Det är också bäst att kontrollera om den ändring som har orsakat problemet var absolut nödvändig och återställa den om den inte är det. Kontrollera också om versionsökningen av paketexporten ökade mer än nödvändigt efter strikt semantisk versionshantering.

### Felaktigt gränssnitt för plattformen {#malfunctioning-platform-ui}

Om det finns vissa gränssnittsfunktioner som inte fungerar som de ska efter uppgraderingen bör du först kontrollera om gränssnittet är anpassat. Vissa strukturer kan ha ändrats och övertäckningen kan behöva uppdateras eller vara föråldrad.

Kontrollera sedan om det finns JavaScript-fel som kan spåras till anpassade tillagda tillägg som är kopplade till klientbibliotek. Samma sak kan gälla för anpassad CSS som kan orsaka problem i AEM-layouten.

Slutligen kontrollerar du om Javascript inte kan hantera en felkonfiguration. Detta är vanligtvis fallet med felaktigt inaktiverade tillägg.

### Felfungerande anpassade komponenter, mallar eller gränssnittstillägg {#malfunctioning-custom-components-templates-or-ui-extensions}

I de flesta fall är orsaken till de här problemen densamma som för paket som inte har startats eller paket som inte installeras med den enda skillnaden att problemen börjar inträffa när komponenterna används för första gången.

Ett sätt att hantera felaktig egen kod är att först utföra röktester för att identifiera orsaken. När du har hittat den kan du titta i rekommendationerna i den här [länksektionen] i artikeln för att hitta sätt att åtgärda dem.

### Anpassningar saknas under /etc {#missing-customizations-under-etc}

`/apps` och `/libs` hanteras väl av uppgraderingen, men ändringar under `/etc` kan behöva återställas manuellt från `/var/upgrade/PreUpgradeBackup` uppgraderingen. Kontrollera den här platsen för allt innehåll som behöver sammanfogas manuellt.

### Analyserar error.log och upgrade.log {#analyzing-the-error.log-and-upgrade.log}

I de flesta fall måste loggarna sökas efter fel för att hitta orsaken till ett problem. Vid uppgraderingar är det dock också nödvändigt att övervaka beroendeproblem eftersom gamla paket kanske inte uppgraderas korrekt.

Det bästa sättet att göra detta är att ta bort error.log genom att ta bort alla meddelanden som inte har med problemet att göra. Du kan göra detta med ett verktyg som grep genom att använda:

```shell
grep -v UnrelatedErrorString
```

Vissa felmeddelanden kanske inte är omedelbart förklarande. I det här fallet kan det vara lättare att förstå var felet uppstod om man tittar i sammanhanget. Du kan avgränsa felet med:

* `grep -B` för att lägga till rader före felet,

eller

* `grep -A` för att lägga till rader efter.

I ett fåtal fall kan fel också hittas i WARN-meddelanden eftersom det kan finnas giltiga fall som leder till det här läget och programmet inte alltid kan avgöra om det här är ett faktiskt fel. Se till att du också läser dessa meddelanden.

### Kontakta Adobe Support {#contacting-adobe-support}

Om du har gått igenom råden på den här sidan och fortfarande ser problem kan du kontakta Adobes support. Om du vill ge så mycket information som möjligt till den supporttekniker som arbetar med ditt ärende måste du inkludera filen upgrade.log från uppgraderingen.
