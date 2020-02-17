---
title: Migrera AEM Forms-resurser och dokument
seo-title: Migrera AEM Forms-resurser och dokument
description: Med migreringsverktyget kan du migrera AEM Forms-resurser och -dokument från AEM 6.3-formulär eller tidigare versioner till AEM 6.4-formulär.
seo-description: Med migreringsverktyget kan du migrera AEM Forms-resurser och -dokument från AEM 6.3-formulär eller tidigare versioner till AEM 6.4-formulär.
uuid: a3fdf940-7fc2-441c-91c8-ad66ba47e5f2
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
discoiquuid: 39dfef85-d047-4b6d-a0f5-92bd77df103b
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# Migrera AEM Forms-resurser och dokument{#migrate-aem-forms-assets-and-documents}

Migreringsverktyget konverterar resurserna [för](../../forms/using/introduction-forms-authoring.md)adaptiva formulär, [molnkonfigurationer](/help/sites-developing/extending-cloud-config.md)och [Correspondence Management-resurser](/help/forms/using/cm-overview.md) från det format som användes i de tidigare versionerna till det format som används i AEM 6.5-formulär. När du kör migreringsverktyget migreras följande:

* Anpassade komponenter för adaptiva formulär
* Anpassningsbara mallar för blanketter och korrespondenshantering
* Molnkonfigurationer
* Korrespondenshantering och adaptiva formulärresurser

>[!NOTE]
>
>Om du har en uppgradering som inte är på plats, för Correspondence Management-resurser, kan du köra migreringen varje gång du importerar resurserna. För migrering av Correspondence Management måste du ha installerat Forms Compatibility Package.

## Migreringsmetod {#approach-to-migration}

Du kan [uppgradera](../../forms/using/upgrade.md) till den senaste versionen av AEM Forms 6.5 från AEM Forms 6.4, 6.3 eller 6.2 eller göra en ny installation. Beroende på om du har uppgraderat din tidigare installation eller utfört en ny installation måste du göra något av följande:

**Vid uppgradering på plats**

Om du har utfört en uppgradering på plats har den uppgraderade instansen redan resurserna och dokumenten. Innan du kan använda resurserna och dokumenten måste du dock installera [AEMFD-kompatibilitetspaketet](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) (inkluderar kompatibilitetspaketet för hantering av korrespondence Management)

Därefter måste du uppdatera resurserna och dokumenten genom att [köra migreringsverktyget](#runningmigrationutility).

**Om installationen inte är på plats**

Om det är en installation på fel plats (ny) måste du installera [AEMFD-kompatibilitetspaketet](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) innan du kan använda resurserna och dokumenten (innehåller Correspondence Management Compatibility-paketet).

Därefter måste du importera resurspaketet (zip eller cmp) till den nya konfigurationen och sedan uppdatera resurserna och dokumenten genom att [köra migreringsverktyget](#runningmigrationutility). Adobe rekommenderar att du bara skapar nya resurser i den nya konfigurationen efter att du har kört migreringsverktyget.

På grund av [bakåtkompatibilitetsrelaterade](/help/sites-deploying/backward-compatibility.md) ändringar ändras platserna för några mappar i crx-databasen. Exportera och importera beroenden manuellt (anpassade bibliotek och resurser) från tidigare inställningar till en ny miljö.

## Läs innan du fortsätter med migreringen {#prerequisites}

För Correspondence Management-resurser:

* För resurser som importeras från den tidigare plattformen läggs en egenskap till: **fd:version=1.0**.
* Eftersom AEM 6.1-formulär inte kan användas med kommentarer. Kommentarerna som lades till tidigare är tillgängliga i resurserna men visas inte automatiskt i gränssnittet. Du måste anpassa egenskapen extendedProperties i användargränssnittet för AEM Forms för att göra kommentarerna synliga.
* I vissa av de tidigare versionerna, till exempel LiveCycle ES4, redigerades text med Flex RichTextEditor, men sedan AEM 6.1-formulär används HTML-redigeraren. På grund av den här återgivningen och utseendet på teckensnitten kan teckenstorlekar och marginaler skilja sig från de tidigare versionerna i användargränssnittet för författare. Bokstäverna ser dock likadana ut när de återges.
* Listor i textmoduler har förbättrats och återges nu annorlunda. Det kan finnas skillnader i synen. Vi rekommenderar att du återger och ser bokstäverna där du använder listor i textmoduler.
* Eftersom bildinnehållsmoduler konverteras till DAM-resurser och layouter och fragment läggs till i formulär under migreringen ändras egenskapen Uppdaterat av för dessa moduler till admin.
* Resursernas versionshistorik migreras inte och är inte tillgänglig efter migreringen. Den efterföljande versionshistoriken efter migreringen bevaras.
* Läget Klar att publicera är föråldrat sedan AEM 6.1-formulär, så alla resurser i läget Klar att publicera ändras till läget Ändrat.
* Eftersom användargränssnittet uppdateras i AEM Forms 6.3 skiljer sig även stegen för att utföra anpassningarna åt. Du måste göra om anpassningen om du migrerar från en version som är äldre än 6.3.
* Layoutfragment går från /content/apps/cm/layouts/fragmentlayouts/1001 till /content/apps/cm/modules/fragmentlayouts. Referens för datamordlista i resurser visar sökvägen till datamappningslistan i stället för dess namn.
* Alla tabbavstånd som används för justering i textmoduler måste justeras om. Mer information finns i [Korrespondenshantering - Använda tabbavstånd för att ordna text](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).
* Resurshanterarkonfigurationer ändras till Correspondence Management-konfigurationer.
* Resurser flyttas under mappar med namn som Befintlig text och Befintlig lista.

## Använda migreringsverktyget {#using-the-migration-utility}

### Kör migreringsverktyget {#runningmigrationutility}

Kör migreringsverktyget innan du gör några ändringar i resurserna eller skapar resurserna. Vi rekommenderar att du inte kör verktyget efter att du har gjort några ändringar eller skapat resurser. Kontrollera att användargränssnittet Correspondence Management eller Adaptive Forms Assets inte är öppet när migreringsprocessen körs.

När du kör migreringsverktyget för första gången skapas en logg med följande sökväg och namn: \[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log. Den här loggen uppdateras kontinuerligt med information om Correspondence Management och Adaptive Forms-migrering, som att flytta resurser.

>[!NOTE]
>
>Innan du kör migreringsverktyget måste du se till att du har säkerhetskopierat din crx-databas.

1. I en webbläsarsession loggar du in på AEM-författarinstansen som administratör.

1. Öppna följande URL i webbläsaren:

   https://[*värdnamn*]:[*port*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   Webbläsaren visar fyra alternativ:

   * Migrering av AEM Forms-resurser
   * Migrering av anpassade komponenter för adaptiva formulär
   * Migrering av adaptiva formulärmallar
   * Migrering av konfigurationer för AEM Forms Cloud

1. Gör följande för att utföra migreringen:

   * Om du vill migrera **resurser** trycker du på AEM Forms Assets Migration (AEM Forms-resursmigrering) och på **startskärmen**. Följande migreras:

      * Anpassningsbara formulär
      * Dokumentfragment
      * Teman
      * Bokstäver
      * Dataordlistor
   >[!NOTE]
   >
   >Vid resursmigrering kan du hitta varningsmeddelanden som &quot;Konflikt hittad för...&quot;. Sådana meddelanden visar att reglerna för vissa komponenter i anpassade formulär inte kan migreras. Om komponenten till exempel har en händelse som har både regler och skript, kommer inga regler för komponenten att migreras om regler inträffar efter skript. Sådana regler kan dock migreras genom att regelredigeraren öppnas i redigeringsprogram för anpassningsbara formulär.
   >
   >
   >Dessa komponenter kan migreras genom att de öppnas i regelredigeraren i redigeraren för anpassade formulär.
   >
   >
   >
   >    * Om du vill migrera regler och skript (krävs inte om du uppgraderar från 6.3) i anpassade komponenter trycker du på migrering av anpassade formulär och trycker på Starta migrering på nästa skärm. Följande migreras: >
      >
      >
      >        

      * Regler och skript skapade med regelredigeraren (6.1 FP1 och senare)
      >        * Skript som skapats med fliken Skript i användargränssnittet i 6.1 och tidigare versioner
   >
   >
   >    * Om du vill migrera mallar (krävs inte om du uppgraderar från 6.3 och 6.4) trycker du på migrering av adaptiva formulärmallar och trycker på Starta migrering på nästa skärm. Följande migreras:
      >
      >
      >
      >        


      * Gamla mallar - adaptiva formulärmallar som skapats under /appar med AEM 6.1 Forms eller tidigare. Detta inkluderar de skript som definierades i mallkomponenterna.
      >        * Nya mallar - Anpassningsbara formulärmallar som skapats med mallredigerare under /conf. Detta inkluderar migrering av regler och skript som skapats med regelredigeraren.


   * Om du vill migrera anpassade formulärkomponenter trycker du på **Adaptive Forms Custom Components Migration** (migrering av anpassade komponenter) och på sidan Custom Components (migrering av anpassade komponenter) trycker du på **Start Migration (Starta migrering**). Följande migreras:

      * Anpassade komponenter skrivna för adaptiva formulär
      * Komponentövertäckningar, om sådana finns.
   * Om du vill migrera adaptiva formulärmallar trycker du på **migrering** av adaptiva formulärmallar och på sidan migrering av anpassade komponenter trycker du på **Starta migrering**. Följande migreras:

      * Anpassningsbara formulärmallar som skapats under /apps eller /conf med hjälp av AEM Template Editor.
   * Migrera konfigurationstjänsterna för AEM Forms Cloud för att utnyttja det nya sammanhangsberoende molntjänstparadigmet, som inkluderar det beröringsaktiverade användargränssnittet (under /conf). När du migrerar tjänsterna för konfiguration av AEM Forms Cloud flyttas molntjänsterna i /etc till /conf. Om du inte har några anpassningar av molntjänster som är beroende av de äldre sökvägarna (/etc) rekommenderar vi att du kör migreringsverktyget direkt efter uppgraderingen till 6.5 och använder molnkonfigurationsgränssnittet för ytterligare arbete. Om du har befintliga anpassningar av molntjänster kan du fortsätta använda det klassiska användargränssnittet vid uppgraderad installation tills anpassningarna har uppdaterats för att anpassas till de migrerade sökvägarna (/conf) och sedan köra migreringsverktyget.
   Om du vill migrera **AEM Forms-molntjänster**, som innehåller följande, trycker du på AEM Forms Cloud Configuration Migration (migrering av molnkonfiguration är oberoende av AEMFD-kompatibilitetspaketet), trycker på AEM Forms Cloud Configurations Migration och sedan på sidan Configuration Migration (konfigurationsmigrering) trycker du på **Start Migration**:

   * Molntjänster för formulärdatamodell

      * Källsökväg: /etc/cloudservices/fdm
      * Målsökväg: /conf/global/settings/cloudconfigs/fdm
   * Recaptcha

      * Källsökväg: /etc/cloudservices/recaptcha
      * Målsökväg: /conf/global/settings/cloudconfigs/recaptcha
   * Adobe Sign

      * Källsökväg: /etc/cloudServices/echosign
      * Målsökväg: /conf/global/settings/cloudconfigs/echosign
   * Typekit-molntjänster

      * Källsökväg: /etc/cloudServices/typekit
      * Målsökväg: /conf/global/settings/cloudconfigs/typekit
   I webbläsarfönstret visas följande när migreringsprocessen utförs:

   * När resurserna uppdateras: Resurserna har uppdaterats.
   * När migreringen är klar: Slutförde migrering av resurser.
   När migreringsverktyget körs gör det följande:

   * **Lägger till taggarna i resurserna**: Lägger till taggen &quot;Correspondence Management: Migrerade resurser/Adaptiva former: Migrerade resurser&quot;. till de migrerade resurserna, så att användarna kan identifiera migrerade resurser. När du kör migreringsverktyget markeras alla befintliga resurser i systemet som migrerade.
   * **Genererar taggar**: Kategorier och underkategorier som finns i det tidigare systemet skapas som taggar, och sedan kopplas dessa taggar till relevanta Correspondence Management-resurser i AEM. Exempelvis genereras en kategori (anspråk) och en underkategori (anspråk) för en bokstavsmall som taggar.

















1. När migreringsverktyget är klart går du vidare till [hushållssysslorna](#housekeepingtasks).

### Hushållsuppgifter efter att migreringsverktyget har körts {#housekeepingtasks}

När du har kört migreringsverktyget ska du sköta följande uppgifter: [](../../forms/using/import-export-forms-templates.md)

1. Kontrollera att XFA-versionen av layouter och fragmentlayouter är 3.3 eller senare. Om du använder layouter och fragmentlayouter av en äldre version kan det uppstå problem när bokstaven återges. Så här uppdaterar du en äldre XFA-version till den senaste versionen:

   1. [Hämta XFA som en zip-fil](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) från användargränssnittet i Forms.
   1. Extrahera filen.
   1. Öppna XFA-filen i den senaste Designer-filen och spara den. Versionen av XFA uppdateras till den senaste.
   1. Överför XFA i användargränssnittet för Forms.

1. Publicera alla resurser som publicerades i det tidigare systemet före migreringen. Flyttningsverktyget uppdaterar bara resurserna på författarinstansen och uppdaterar resurserna på den eller de publiceringsinstanser du behöver för att publicera resurserna.
1. I AEM Forms 6.4 och 6.5 har vissa av rättigheterna för användargrupperna ändrats. Om du vill att någon av dina användare ska kunna överföra XDP-filer och adaptiva formulär som innehåller skript eller använda kodredigeraren måste du lägga till dem i en grupp för användare som har avancerade formulär. På samma sätt kan mallskapare inte längre använda kodredigeraren i regelredigeraren. För att användare ska kunna använda kodredigeraren lägger du till dem i gruppen af-template-script-writers. Instruktioner om hur du lägger till användare i grupper finns i [Hantera användare och användargrupper](/help/communities/users.md).

