---
title: Migrera AEM Forms-resurser och -dokument
description: Med migreringsverktyget kan du migrera Adobe Experience Manager (AEM) Forms-resurser och -dokument från AEM 6.3 Forms eller tidigare versioner till AEM 6.4 Forms.
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
docset: aem65
role: Admin
exl-id: 0f9aab7d-8e41-449a-804b-7e1bfa90befd
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1736'
ht-degree: 0%

---

# Migrera AEM Forms-resurser och -dokument{#migrate-aem-forms-assets-and-documents}

Migreringsverktyget konverterar [Adaptivt Forms-material](../../forms/using/introduction-forms-authoring.md), [molnkonfigurationer](/help/sites-developing/extending-cloud-config.md)och [Korrespondenshanteringsresurser](/help/forms/using/cm-overview.md) från det format som användes i de tidigare versionerna till det format som användes i Adobe Experience Manager (AEM) 6.5 Forms. När du kör migreringsverktyget migreras följande:

* Anpassade komponenter för adaptiva formulär
* Anpassningsbara mallar för blanketter och korrespondenshantering
* Molnkonfigurationer
* Korrespondenshantering och adaptiva formulärresurser

>[!NOTE]
>
>Om det finns en uppgradering som inte är på plats för Correspondence Management-resurser kan du köra migreringen varje gång du importerar resurserna. För migrering av Correspondence Management måste Forms-kompatibilitetspaketet vara installerat.

## Migreringsmetod {#approach-to-migration}

Du kan [uppgradera](../../forms/using/upgrade.md) till den senaste versionen av AEM Forms 6.5 från AEM Forms 6.4, 6.3 eller 6.2, eller en ny installation. Beroende på om du har uppgraderat din tidigare installation eller utfört en ny installation måste du göra något av följande:

**Om det finns en uppgradering på plats**

Om du har utfört en uppgradering på plats har den uppgraderade instansen redan resurserna och dokumenten. Innan du kan använda resurserna och dokumenten måste du installera [AEMFD-kompatibilitetspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en) (inkluderar kompatibilitetspaket för hantering av korrespondenshantering)

Sedan måste du uppdatera resurserna och dokumenten efter [köra migreringsverktyget](#runningmigrationutility).

**Om det finns en installation på annan plats**

Om installationen är på fel plats (ny) måste du installera programmet innan du kan använda resurserna och dokumenten [AEMFD-kompatibilitetspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en) (inkluderar paketet Correspondence Management Compatibility).

Sedan måste du importera resurspaketet (zip eller cmp) till den nya konfigurationen och sedan uppdatera resurserna och dokumenten med [köra migreringsverktyget](#runningmigrationutility). Adobe rekommenderar att du bara skapar resurser på den nya konfigurationen efter att du har kört migreringsverktyget.

Förfaller [bakåtkompatibilitetsrelaterad](/help/sites-deploying/backward-compatibility.md) ändras platserna för några mappar i crx-databasen. Exportera och importera beroenden manuellt (anpassade bibliotek och resurser) från tidigare inställningar till en ny miljö.

## Innan du fortsätter med migreringen {#prerequisites}

För Correspondence Management-resurser:

* För resurser som importeras från den tidigare plattformen läggs en egenskap till: **fd:version=1.0**.
* Eftersom AEM 6.1 Forms inte kan kommentera direkt i dokumentet. Kommentarerna som lades till tidigare är tillgängliga i resurserna, men visas inte automatiskt i gränssnittet. Anpassa egenskapen extendedProperties i AEM Forms användargränssnitt för att göra kommentarerna synliga.
* I vissa av de tidigare versionerna, till exempel LiveCycle ES4, redigerades text med Flex RichTextEditor, men sedan AEM 6.1 Forms används HTML Editor. På grund av den här återgivningen och utseendet på teckensnitten kan teckenstorlekar och marginaler skilja sig från de tidigare versionerna i användargränssnittet för Författare. Bokstäverna ser dock likadana ut när de återges.
* Listor i textmoduler har förbättrats och återges nu annorlunda. Det kan finnas skillnader i synen. Adobe rekommenderar att du återger och ser bokstäverna där du använder listor i textmoduler.
* Eftersom bildinnehållsmoduler konverteras till DAM-resurser och layouter och fragment läggs till i formulär under migreringen ändras egenskapen Uppdaterat av för dessa moduler till admin.
* Resursernas versionshistorik migreras inte och är inte tillgänglig efter migreringen. Den efterföljande versionshistoriken efter migreringen bevaras.
* Läget Klar att publicera är föråldrat sedan AEM 6.1 Forms, så alla resurser i läget Klar att publicera ändras till läget Ändrat.
* Eftersom användargränssnittet uppdateras i AEM Forms 6.3 skiljer sig även stegen för att utföra anpassningarna. Gör om anpassningen om du migrerar från en version före 6.3.
* Layoutfragment flyttas från `/content/apps/cm/layouts/fragmentlayouts/1001` till `/content/apps/cm/modules/fragmentlayouts`. Referens till datamordlista i resurser visar sökvägen till datamappningen i stället för dess namn.
* Alla tabbavstånd som används för justering i textmoduler måste justeras om. Mer information finns i [Korrespondenshantering - Använda tabbavstånd för att ordna text](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).
* Resurshanterarkonfigurationer ändras till Correspondence Management-konfigurationer.
* Resurser flyttas under mappar med namn som Befintlig text och Befintlig lista.

## Använda migreringsverktyget {#using-the-migration-utility}

### Kör migreringsverktyget {#runningmigrationutility}

Kör migreringsverktyget innan du ändrar i resurserna eller skapar resurser. Adobe rekommenderar att du inte kör verktyget efter att du har gjort några ändringar eller skapat resurser. Kontrollera att användargränssnittet Correspondence Management eller Adaptive Forms Assets inte är öppet när migreringsprocessen körs.

När du kör migreringsverktyget för första gången skapas en logg med följande sökväg och namn: `\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log`. Loggen uppdateras kontinuerligt med information om Correspondence Management och adaptive Forms-migrering, som att flytta resurser.

>[!NOTE]
>
>Innan du kör migreringsverktyget måste du se till att du har säkerhetskopierat din crx-databas.

1. I en webbläsarsession loggar du in på AEM Author-instansen som administratör.

1. Öppna följande URL i webbläsaren:

   https://[*värdnamn*]:[*port*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   Webbläsaren visar fyra alternativ:

   * Migrering av AEM Forms Assets
   * Adaptiv migrering av anpassade Forms-komponenter
   * Migrering av adaptiva Forms-mallar
   * Migrering av konfigurationer i AEM Forms Cloud

1. Gör följande för att utföra migreringen:

   * Migrera **resurser**, väljer AEM Forms Assets Migration (migrering av-resurser) och väljer **Starta migrering**. Följande migreras:

      * Anpassningsbara formulär
      * Dokumentfragment
      * Teman
      * Bokstäver
      * Dataordlistor

   >[!NOTE]
   >
   >Vid resursmigrering kan du hitta varningsmeddelanden som &quot;Konflikt hittad för...&quot;. Sådana meddelanden visar att reglerna för vissa komponenter i anpassade formulär inte kan migreras. Om komponenten till exempel har en händelse som har både regler och skript, kommer inga regler för komponenten att migreras om regler inträffar efter skript. Du kan [migrera sådana regler genom att öppna regelredigeraren](#migrate-rules) i anpassningsbara formulär.

   * Om du vill migrera anpassade formulärkomponenter väljer du **Adaptiv migrering av anpassade Forms-komponenter** och på sidan för migrering av anpassade komponenter väljer du **Starta migrering**. Följande migreras:

      * Anpassade komponenter skrivna för Adaptive Forms
      * Komponentövertäckningar, om sådana finns.

   * Om du vill migrera adaptiva formulärmallar väljer du **Adaptiv migrering av Forms-mallar** och på sidan för migrering av anpassade komponenter väljer du **Starta migrering**. Följande migreras:

      * Anpassningsbara blankettmallar som skapats i `/apps` eller `/conf` med AEM mallredigerare.

   * Migrera konfigurationstjänsterna i AEM Forms Cloud till att använda det nya kontextmedvetna molntjänstparadigmet, som innehåller det beröringsaktiverade användargränssnittet (under `/conf`). När du migrerar AEM Forms Cloud Configuration Services är molntjänsterna i `/etc` flyttas till `/conf`. Om du inte har några anpassningar av molntjänster som är beroende av de äldre sökvägarna (`/etc`) rekommenderar Adobe att du kör migreringsverktyget efter att du uppgraderat till 6.5. Använd molnkonfigurationen Touch UI för ytterligare arbete. Om du har befintliga anpassningar av molntjänster kan du fortsätta använda det klassiska användargränssnittet i uppgraderad konfiguration tills anpassningarna har uppdaterats för att passa de migrerade sökvägarna (`/conf`) och kör sedan migreringsverktyget.

   Migrera **AEM Forms molntjänster**, som innehåller följande, väljer du migrering av AEM Forms Cloud-konfiguration (migreringen av molnkonfigurationen är oberoende av AEMFD-kompatibilitetspaketet). Välj migrering av AEM Forms Cloud-konfigurationer och välj sedan på sidan Konfigurationsmigrering **Starta migrering**:

   * Molntjänster för formulärdatamodell

      * Källsökväg: `/etc/cloudservices/fdm`
      * Målsökväg: `/conf/global/settings/cloudconfigs/fdm`

   * Recaptcha

      * Källsökväg: `/etc/cloudservices/recaptcha`
      * Målsökväg: `/conf/global/settings/cloudconfigs/recaptcha`

   * Adobe Sign

      * Källsökväg: `/etc/cloudservices/echosign`
      * Målsökväg: `/conf/global/settings/cloudconfigs/echosign`

   * Typekit cloud services

      * Källsökväg: `/etc/cloudservices/typekit`
      * Målsökväg: `/conf/global/settings/cloudconfigs/typekit`

   I webbläsarfönstret visas följande när migreringsprocessen utförs:

   * När resurserna uppdateras uppdateras: Resurserna har uppdaterats.
   * När migreringen är klar: Slutförd migrering av resurser.

   När migreringsverktyget körs gör det följande:

   * **Lägger till taggar i resurserna**: Lägger till taggen &quot;Correspondence Management : Migrated Assets&quot; / &quot;Adaptive Forms : Migrated Assets&quot;. till de migrerade resurserna, så att användarna kan identifiera migrerade resurser. När du kör migreringsverktyget markeras alla befintliga resurser i systemet som migrerade.
   * **Skapar taggar**: Kategorier och underkategorier i det föregående systemet skapas som taggar, och sedan kopplas dessa taggar till de relevanta Correspondence Management-resurserna i AEM. Exempelvis genereras en kategori (anspråk) och en underkategori (anspråk) för en bokstavsmall som taggar.

1. När migreringsverktyget är klart går du till [hushållsarbete](#housekeepingtasks).

#### Migrera regler med regelredigeraren {#migrate-rules}

Dessa komponenter kan migreras genom att de öppnas i regelredigeraren i den adaptiva Forms-redigeraren.

* Om du vill migrera regler och skript (krävs inte om du uppgraderar från 6.3) i anpassade komponenter väljer du Anpassad migrering för Forms och väljer Starta migrering på nästa skärm. Följande migreras:

   * Regler och skript skapade med regelredigeraren (6.1 FP1 och senare)

   * Skript som skapats med fliken Skript i användargränssnittet i 6.1 och tidigare versioner

* Om du vill migrera mallar (krävs inte om du uppgraderar från 6.3 och 6.4) väljer du Adaptiv migrering av Forms-mallar och väljer Starta migrering på nästa skärm. Följande migreras:

   * Gamla mallar - de adaptiva formulärmallarna som skapats under /apps med AEM 6.1 Forms eller tidigare. Detta inkluderar de skript som definierades i mallkomponenterna.

   * Nya mallar - adaptiva formulärmallar som skapats med malleditorn under `/conf`. Detta inkluderar migrering av regler och skript som skapats med regelredigeraren.

### Hushållsuppgifter efter att migreringsverktyget har körts {#housekeepingtasks}

När du har kört migreringsverktyget ska du sköta följande uppgifter:

1. Kontrollera att XFA-versionen av layouter och fragmentlayouter är 3.3 eller senare. Om du använder layouter och fragmentlayouter av en äldre version kan det uppstå problem när bokstaven återges. Så här uppdaterar du en version av en äldre XFA till den senaste versionen:

   1. [Hämta XFA som en zip-fil](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) från Forms användargränssnitt.
   1. Hämta filen.
   1. Öppna XFA-filen i den senaste Designer-filen och spara den. Versionen av XFA uppdateras till den senaste.
   1. Överför XFA i Forms användargränssnitt.

1. Publicera alla resurser som publicerades i det tidigare systemet före migreringen. Flyttningsverktyget uppdaterar bara resurserna på Author-instansen och för att uppdatera resurserna på Publish-instanserna måste du publicera resurserna.

1. I AEM Forms 6.4 och 6.5 ändras vissa rättigheter för användargrupperna. Om du vill att någon av dina användare ska kunna överföra XDP-filer och adaptiva Forms-skript eller använda en kodredigerare måste du lägga till dem i gruppen för användare med avancerade formulär. Mallförfattare kan inte heller längre använda kodredigeraren i regelredigeraren. För att användare ska kunna använda en kodredigerare lägger du till dem i gruppen af-template-script-writers. Instruktioner om hur du lägger till användare i grupper finns i [Hantera användare och användargrupper](/help/communities/users.md).
