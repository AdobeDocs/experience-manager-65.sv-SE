---
title: Allmänna inställningar för AEM-formulär
seo-title: Allmänna inställningar för AEM-formulär
description: Lär dig att konfigurera inställningarna på sidan Core Configurations i administrationskonsolen som kan förbättra systemets prestanda.
seo-description: Lär dig att konfigurera inställningarna på sidan Core Configurations i administrationskonsolen som kan förbättra systemets prestanda.
uuid: 940680fd-b7ab-4376-aa5b-e139223522ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bd648c38-731b-420e-973d-a4728b69868e
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Allmänna inställningar för AEM-formulär {#general-aem-forms-settings}

Sidan Core Configurations i administrationskonsolen innehåller inställningar som kan förbättra systemets prestanda. När du har konfigurerat eller uppdaterat inställningarna startar du om programservern.

Mer information om hur du aktiverar läget för säker säkerhetskopiering finns i [Aktivera och inaktivera läget](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode)för säker säkerhetskopiering.


>[!NOTE]
>
>Filerna i den tillfälliga katalogen och de långlivade dokumenten i GDS-rotkatalogen (Global Document Storage) kan innehålla känslig användarinformation, t.ex. information som kräver särskilda autentiseringsuppgifter när de används med API:er eller användargränssnitt. Därför är det viktigt att den här katalogen skyddas på rätt sätt genom att använda de metoder som är tillgängliga för operativsystemet. Vi rekommenderar att endast det operativsystemskonto som används för att köra programservern har läs- och skrivåtkomst till den här katalogen.


1. I administrationskonsolen klickar du på **[!UICONTROL Inställningar > Core System Settings > Configurations]**.
1. Ändra alternativen på sidan Core Configurations (Grundkonfiguration) efter behov och klicka på **[!UICONTROL OK]**. Mer information om alternativen finns i Alternativ för [kärnkonfigurationer](configure-general-aem-forms-settings.md#core-configurations-options).


## Alternativ för kärnkonfigurationer {#core-configurations-options}

**Plats för tillfällig katalog** Katalogsökvägen där AEM-formulär skapar tillfälliga produktfiler. Om värdet för den här inställningen är tomt används systemets tillfälliga katalog som standard. Kontrollera att den tillfälliga katalogen är en skrivbar mapp.

***Obs **! Kontrollera att den tillfälliga katalogen finns i det lokala filsystemet. AEM-formulär stöder inte en tillfällig katalog på en fjärrplats.*

**Rotkatalog** för global dokumentlagring Rotkatalogen för global dokumentlagring (GDS) används i följande syften:

* Lagra långlivade dokument. Långa dokument har ingen förfallotid och finns kvar tills de tas bort (t.ex. PDF-filerna som används i en arbetsflödesprocess). De långvariga dokumenten utgör en kritisk del av det övergripande systemtillståndet. Om några eller alla dessa dokument förloras eller skadas kan formulärservern bli instabil. Därför är det viktigt att den här katalogen lagras på en RAID-enhet.
* Lagra tillfälliga dokument som behövs under bearbetningen.

   ***Obs **: Du kan även aktivera dokumentlagring i AEM-formulärdatabasen. Systemprestanda är dock bättre när du använder GDS.*

* Överför dokument mellan noder i ett kluster. Om du kör AEM-formulär i en klustrad miljö måste katalogen vara tillgänglig från alla noder i klustret.
* Tar emot inkommande parametrar från fjärr-API-anrop.

Om du inte anger någon GDS-rotkatalog används en programserverkatalog som standard:

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

***Obs **: Om du ändrar värdet för GDS-rotkataloginställningen bör du vara särskilt försiktig. GDS-katalogen används för att lagra både långlivade filer som används i en process och viktiga produktkomponenter för AEM-formulär. Att ändra platsen för GDS-katalogen är en stor systemändring. Om GDS-katalogen konfigureras på ett felaktigt sätt kommer AEM-formulären att fungera och en fullständig ominstallation av AEM-formulären kan krävas. Om du anger en ny plats för GDS-katalogen måste programservern stängas av och data migreras innan servern kan startas om. Systemadministratören måste flytta alla filer från den gamla platsen till den nya, men behålla den interna katalogstrukturen.*

***Obs **: Ange inte samma katalog för den tillfälliga katalogen och GDS-katalogen.*

Mer information om GDS-katalogen finns i [Förbereda för att installera AEM-formulär (Single Server)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Sökväg till Adobe Server Fonts-katalogen** Ange sökvägen till den katalog som innehåller Adobe-serverteckensnitten. Dessa teckensnitt installeras med AEM-formulär. Standardplatsen för teckensnitten är [aem-forms root]/fonts-katalogen. Om den här katalogen inte är tillgänglig kan du kopiera teckensnitten någon annanstans och använda den här inställningen för att ange den nya platsen.

**Sökväg till kundteckensnittskatalogen** Ange sökvägen till en katalog som innehåller ytterligare teckensnitt som du vill använda.

***Obs **! Teckensnitt hämtas från Windows-systemets teckensnittscache och en systemomstart krävs för att uppdatera cachen. När du har angett kundens teckensnittskatalog måste du starta om datorn där AEM-formulär är installerade.*

**Sökväg till katalogen** System Fonts Ange sökvägen till teckensnittskatalogen som finns i operativsystemet. Flera kataloger kan läggas till, avgränsade med semikolon **;**.

**Platsen för Data Services-konfigurationsfilen** Anger platsen för services-config.xml-filen. Som standard är den här filen inbäddad i filen adobe-core-appserver.ear och är inte användartillgänglig. En kopia av standardfilen services-config.xml finns i [aem-forms root]\sdk\misc\DataServices\Server-Configuration. Om du har ändrat den här filen och flyttat den anger du den nya platsen i det här fältet.

Konfigurationsfilen för Data Services gör det möjligt att anpassa datatjänster, till exempel autentiseringstyp och felsökningsutdata.

Den här inställningen är tom som standard.

**Maximal textbunden dokumentstorlek (byte)** Det maximala antalet byte som finns i minnet när dokument skickas mellan olika AEM-formulärkomponenter. Använd den här inställningen för prestandajustering. Dokument som är mindre än det här antalet lagras i minnet och sparas i databasen. Dokument som överskrider det högsta tillåtna antalet lagras på hårddisken.

Den här inställningen är obligatorisk. Standardvärdet är 65 536 byte.

**Standardtidsgräns för borttagning av dokument (sekunder)** Den maximala tiden, i sekunder, under vilken ett dokument som skickas mellan olika AEM-formulärkomponenter anses vara aktiv. När den här tiden har gått kan filer som används för att lagra det här dokumentet tas bort. Använd den här inställningen för att kontrollera hur mycket diskutrymme som används.

Den här inställningen är obligatorisk. Standardvärdet är 600 sekunder.

**Intervall för dokumentsvepning (sekunder)** Den tid, i sekunder, mellan försök att ta bort filer som inte längre behövs och som användes för att skicka dokumentdata mellan tjänster.

Den här inställningen är obligatorisk. Standardvärdet är 30 sekunder.

**Aktivera FIPS** Välj det här alternativet om du vill aktivera FIPS-läget. Federal Information Processing Standard (FIPS) 140-2 är en kryptologistandard som definierats av USA:s regering. När AEM-formulär körs i FIPS-läge begränsar de dataskyddet till godkända FIPS 140-2-algoritmer genom att använda krypteringsmodulen RSA BSAFE Crypto-C 2.1.

FIPS-läget stöder inte krypteringsalgoritmer som används i tidigare versioner av Adobe Acrobat® än 7.0. Om FIPS-läget är aktiverat och du använder krypteringstjänsten för att kryptera PDF-filen med ett lösenord med kompatibilitetsnivån inställd på Acrobat 5, misslyckas krypteringsförsöket med ett fel.

När FIPS är aktiverat används vanligtvis inte lösenordskryptering för något dokument. Om du försöker göra det genereras ett FIPSModeException-undantag som anger att lösenordskryptering inte tillåts i FIPS-läge. Dessutom stöds inte elementet PDFsFromBookmarks (DX) i dokumentbeskrivningens XML-element i FIPS-läge när basdokumentet är lösenordskrypterat.

***Obs **: AEM-formulärprogram validerar inte kod för att säkerställa FIPS-kompatibilitet. Den tillhandahåller ett FIPS-driftläge så att FIPS-godkända algoritmer används för kryptografiska tjänster från FIPS-godkända bibliotek (RSA).*

**Aktivera WSDL** Välj det här alternativet om du vill aktivera generering av WSDL (Web Service Definition Language) för alla tjänster som ingår i AEM-formulär.

Aktivera det här alternativet i utvecklingsmiljöer, där utvecklare använder WSDL-generering för att skapa sina klientprogram. Du kan välja att inaktivera WSDL-generering i en produktionsmiljö för att undvika att visa tjänstens interna information.

**Aktivera dokumentlagring i databasen** Välj det här alternativet om du vill lagra långlivade dokument i AEM-formulärdatabasen. Om du aktiverar det här alternativet tas inte behovet av en GDS-katalog bort. Om du väljer det här alternativet förenklas dock säkerhetskopieringen av AEM-formulär. Om du bara använder GDS-systemet innebär en säkerhetskopiering att AEM-formulärsystemet försätts i säkerhetskopieringsläge och att säkerhetskopieringen av databasen och GDS slutförs. Om du väljer databasalternativet innebär säkerhetskopieringen att du slutför databassäkerhetskopieringen för en ny installation eller slutför databassäkerhetskopieringen och engångskopieringen av GDS för en uppgradering. Ytterligare hantering av databasen kan behövas för att rensa jobb och data jämfört med en GDS-konfiguration. (Se Alternativ för säkerhetskopiering när databasen används för dokumentlagring.)

**Aktivera DSC-anropsstatistik** När det här alternativet är markerat spårar AEM-formulär startstatistik, t.ex. antalet anrop, hur lång tid det tar att anropa och antalet fel i anrop. Denna information lagras i en JMX-böna så att du kan använda Java™ JConsole eller tredjepartsprogram för att ta en titt på statistiken. Om du inte vill se den här statistiken avmarkerar du det här alternativet för att förbättra prestanda för AEM-formulär.

**Aktivera RDS** Om du väljer det här alternativet aktiveras fjärrutvecklingstjänstens (RDS) tjänstplats i AEM-formulär. När det här alternativet är aktiverat kan verktyg på klientsidan interagera med datatjänster för att göra saker som att driftsätta eller avdistribuera modeller för att skapa destinationer och slutpunkter, eller för att ta reda på vilka modeller som har distribuerats till slutpunkter. Som standard är det här alternativet inte markerat.

**Tillåt icke-skyddade RDS-begäranden** När det här alternativet är markerat behöver RDS-begäranden inte använda https. Som standard är det här alternativet inte markerat och all kommunikation till datatjänster måste vara https-begäranden.

**Tillåt osäker dokumentöverföring från Flex-program:** Filöverföringsservern som används för att överföra dokument från Adobe Flex®-program till AEM-formulär kräver att användarna är autentiserade och behöriga innan de kan överföra dokument. Användaren måste tilldelas rollen som användare av Document Upload Application eller en annan roll som innefattar behörigheten Dokumentöverföring. Detta förhindrar obehöriga användare från att överföra dokument till AEM-formulärservern. Välj det här alternativet om du vill inaktivera den här säkerhetsfunktionen i en utvecklingsmiljö eller för bakåtkompatibilitet med tidigare versioner av AEM-formulär. Som standard är det här alternativet inte markerat. Mer information finns i&quot;Anropa AEM-formulär med AEM Forms Remoting&quot; i Programmering med AEM-formulär.

**Tillåt oskyddad dokumentöverföring från Java SDK-program:** Överföringar med HTTP DocumentManager måste vara skyddade. Som standard kräver HTTP-överföringar att användare autentiseras och auktoriseras innan de kan överföra dokument. Användaren måste tilldelas rollen Tjänstanvändare eller en annan roll som innehåller behörigheten Tjänstanrop. Detta förhindrar obehöriga användare från att överföra dokument till formulärservern. Välj det här alternativet om du vill inaktivera den här säkerhetsfunktionen i en utvecklingsmiljö, för bakåtkompatibilitet med tidigare versioner av AEM-formulär eller baserat på din brandvägg. Som standard är det här alternativet inte markerat. Mer information finns i&quot;Anropa AEM-formulär med Java API&quot; i Programmering med AEM-formulär.
