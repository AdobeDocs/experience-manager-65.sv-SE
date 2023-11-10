---
title: Installationsanvisningar för AEM Forms Patch för AEM Forms
description: Installationsanvisningar för AEM Forms Service Pack för OSGi- och JEE-miljö
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: 6f45b0f8dad44e66570f6436a560060cbed56161
workflow-type: tm+mt
source-wordcount: '1746'
ht-degree: 0%

---

# Installationsanvisningar för AEM 6.5 Forms Service Pack {#aem-form-patch-installation-instructions}

## Versionsinformation

| Produkt | Adobe Experience Manager 6.5 Forms |
|---|---|
| Version | 6.5.18.0 |
| Typ | Service Pack-version |
| Datum | 31 augusti 2023 |
| Hämta URL | [Senaste AEM Forms Releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) |

>[!NOTE]
>
>Se de senaste [AEM Service Pack versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html) för en fullständig lista över åtgärdade problem.

## Vad ingår i Experience Manager Forms 6.5

Adobe Experience Manager (AEM) Forms Service Pack innehåller nya och uppgraderade funktioner, t.ex. viktiga kundefterfrågade förbättringar, prestanda, stabilitet och säkerhetsförbättringar. AEM Forms lanserar Service Pack med regelbundna intervall för att ge tillgång till de senaste funktionerna och förbättringarna. Beroende på din stack väljer du en av följande sökvägar för att hämta och installera Service Pack på din miljö:

* [Hämta och installera Service Pack på ett AEM formulär i JEE-miljö](#download-and-install-for-jee-service-pack)
* [Hämta och installera Service Pack på en AEM i OSGi-miljö](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> * Adobe släpper ett fullständigt installationsprogram var sjätte service pack. AEM 6.5 Forms Service Pack 18 (6.5.18.0) är det senaste fullständiga JEE-installationsprogrammet. Det fullständiga installationsprogrammet har stöd för nya plattformar medan det vanliga installationsprogrammet för Service Pack innehåller nya funktioner, felkorrigerade och allmänna förbättringar. Om du gör en ny installation eller planerar att använda den senaste programvaran för din AEM 6.5 Forms i JEE-miljö rekommenderar Adobe att du använder AEM 6.5.18.0 Forms i JEE-fullversionen som släpptes den 31 augusti 2023 i stället för det AEM 6.5 Forms-installationsprogrammet som släpptes den 8 april 2019 eller AEM 6.5.12 Forms Installationsprogrammet som släpptes den 3 Mars 2022. Installera det senaste Service Pack-paketet när du har använt det fullständiga installationsprogrammet.
> 
> * AEM Forms-funktionen, som Adaptive Forms, finns i [AEM 6.5 QuickStart](https://experienceleague.corp.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html), endast för prospektering och utvärdering. För produktion krävs en giltig licens för AEM Forms.



## Hämta och installera Service Pack på ett AEM formulär i JEE-miljö {#download-and-install-for-jee-service-pack}

![JEE-installation](/help/forms/using/assets/jeeinstallation.png)

+++1. Säkerhetskopiera din befintliga miljö:

1. Säkerhetskopiera [CRX-databas, databasschema och GDS (global dokumentlagring)](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).
1. Säkerhetskopiera &lt;*AEM_forms_root*>/distribuera mapp.

>[!NOTE]
>
> Innan du kör installationsprogrammet för AEM Service Pack bör du kontrollera att du har skrivbehörighet AEM installationskatalogen.

+++

+++2.Ladda ned nödvändig programvara:

* [AEM Forms på JEE Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
* [Forms tilläggspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [Fragmentserver](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

+++

+++3. Installera AEM Forms på JEE-Service Pack:

1. Stoppa programservern.
1. Extrahera **Installationsarkiv för AEM Forms på JEE Service Pack** till hårddisken:

   * **Windows**
Navigera till rätt katalog på installationsmediet eller mappen på hårddisken där du kopierade installationsprogrammet och dubbelklicka på `aemforms65_cfp_install.exe` -fil.

      * (32-bitars Windows) `Windows\Disk1\InstData\VM`
      * (64-bitars Windows) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
Navigera till rätt katalog och från ett skal och en typ `./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Då startas en installationsguide som vägleder dig genom installationen.

1. Klicka på panelen Introduktion **[!UICONTROL Next]**.
1. På **Välj installationsmapp** kontrollerar du att den standardplats som visas är korrekt för din befintliga installation eller klickar på **[!UICONTROL Browse]** för att välja en alternativ mapp där AEM är installerad och klicka på **[!UICONTROL Next]**.
1. Läs sammanfattningsinformationen för Service Pack och klicka på **[!UICONTROL Next]**.
1. Läs mer i Förinstallationssammanfattning och klicka på **[!UICONTROL Install]**.
1. När installationen är klar klickar du **[!UICONTROL Next]** för att använda snabbkorrigeringsuppdateringar på dina installerade filer.
1. **[Endast för Windows]:** Gör något av följande:

   * Avmarkera **Starta Configuration Manager** innan du klickar **[!UICONTROL Done]**. Kör **Konfigurationshanteraren** genom att använda **ConfigurationManager.bat** fil i `[aem-forms root]\configurationManager\bin`.

   * Eller avmarkera **Starta Configuration Manager** innan du klickar **[!UICONTROL Done]**. Före körning **Konfigurationshanteraren** använda **ConfigurationManager.exe** eller **ConfigurationManager_IPv6.exe**, navigera till *`<AEMForms_Install_Dir>\configurationManager\bin`* katalog och ersätta [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) och [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) filer.

     >[!NOTE]
     >
     >* Uppdatera eller ersätta **ConfigurationManager.bat** kan du undvika att uppdatera .lax-filerna manuellt.

1. **[Endast för Unix-baserade]:** The **Starta Configuration Manager** är markerad som standard. Klicka **[!UICONTROL Done]** för att köra Configuration Manager direkt eller köra **Konfigurationshanteraren** avmarkera **Starta Configuration Manager** innan du klickar **[!UICONTROL Done]**. Du kan börja **Konfigurationshanteraren** senare använda lämpligt skript i `[AEM_forms_root]/configurationManager/bin` katalog.

1. Beroende på programservern väljer du ett av följande dokument och följer instruktionerna i *Konfigurera och distribuera AEM* -avsnitt.

   * [Installera och distribuera AEM formulär för JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Installera och distribuera AEM för WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)
   * [Installera och distribuera AEM Forms för WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65)
   * [Installera och distribuera AEM formulär för JBoss® Cluster](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [Installera och distribuera AEM för WebSphere® Cluster](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [Installera och distribuera AEM Forms för WebLogic-kluster](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
> När du har installerat AEM Forms på JEE-Service Pack måste du ta bort Forms-tilläggspaketet från `crx-repository\install` innan appservern startas om. Hämta det senaste Forms-tilläggspaketet från [Programdistributionsportal](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

+++4. Installera serverdelen (AEM Service Pack 6.5.14.0 eller tidigare)

>[!NOTE]
>
> * Om du uppgraderar från **AEM Service Pack 6.5.15.0**, installation av **serletfragment** är inte obligatoriskt. För versioner **AEM Service Pack 6.5.14.0** eller tidigare är det obligatoriskt att installera servletsfragmentet.
> * Du måste installera **serletfragment** för alla programservrar utom de som körs på **JBoss® EAP 7.4.0**.


Så här hämtar och installerar du serverletsfragmentet:

1. Om du inte har hämtat fragmentet hämtar du det från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

1. Starta programservern, vänta på att loggarna ska stabiliseras och kontrollera paketläget.

1. Öppna Web Console Bundles. Standardwebbadressen är `http://[Server]:[Port]/system/console/bundles`.

1. Klicka på Installera/Uppdatera. Välj det hämtade fragmentet, `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. Klicka **Installera** eller **Uppdatera**. Vänta tills programservern har stabiliserats

1. Stoppa programservern.

+++

+++5. Installera AEM Service Pack

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.
1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager] -instans.
1. Hämta Service Pack från [Programvarudistribution](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Öppna Pakethanteraren och välj **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns på [Pakethanteraren](/help/sites-administering/package-manager.md).
1. Markera paketet och välj **[!UICONTROL Install]**.

**Automatisk installation**

Det finns två olika metoder som du kan använda för att installera automatiskt [!DNL ExperienceManager] Service Pack.<!--       UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i `../crx-quickstart/install` när servern är tillgänglig online.
Paketet installeras automatiskt.

* Använd [HTTP-API från Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html). Använd  `cmd=install&recursive=true` så att de kapslade paketen installeras.

  >[!NOTE]
  >
  Service Pack för Experience Manager stöder inte installation av Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

  **Validera installationen**

  Om du vill veta vilka plattformar som är certifierade för att fungera med den här versionen kan du läsa [tekniska krav](/help/sites-deploying/technical-requirements.md).

   1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (spversion)` under [!UICONTROL Installed Products].<!-- UPDATE FOR EACH NEW RELEASE -->
   1. Alla OSGi-paket är **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Använd webbkonsol: `/system/console/bundles`).
   1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.2.14 eller senare (Använd WebConsole: `/system/console/     bundles`).

+++

+++6. Installera AEM Experience Manager Forms tilläggspaket

1. Kontrollera att du har installerat [!DNL Experience Manager] Service Pack.
1. Ladda ned motsvarande tilläggspaket från Forms på [AEM Forms-versioner](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) för ditt operativsystem.
1. Installera Forms tilläggspaket enligt beskrivningen i [Installera AEM Forms tilläggspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. Om du använder brev i Experience Manager 6.5 Forms installerar du [senaste AEMFD-kompatibilitetspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## Hämta och installera Service Pack på en AEM i OSGi-miljö {#download-and-install-for-osgi-service-pack}

![Installationssteg för OSGi](/help/forms/using/assets/osgiinstallation.png)


+++1. Säkerhetskopiera din befintliga miljö:

1. Säkerhetskopiera [CRX-databas och databasschema](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).

>[!NOTE]
>
Om du installerar AEM Forms Service Pack för relationsdatabas måste du säkerhetskopiera DB_schema.

+++

+++2.Ladda ned nödvändig programvara:

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
* [Forms tilläggspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)

+++

+++3. Installera AEM Service Pack

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.
1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager] -instans.
1. Hämta Service Pack från [Programvarudistribution](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Öppna Pakethanteraren och välj **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns på [Pakethanteraren](/help/sites-administering/package-manager.md).
1. Markera paketet och välj **[!UICONTROL Install]**.

**Automatisk installation**

Det finns två olika metoder som du kan använda för att installera automatiskt [!DNL Experience Manager] Service Pack.<!--  UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.
* Använd [HTTP-API från Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html). Använd `cmd=install&recursive=true` så att de kapslade paketen installeras.

  >[!NOTE]
  >
  Service Pack för Experience Manager stöder inte installation av Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

  **Validera installationen**

  Om du vill veta vilka plattformar som är certifierade för att fungera med den här versionen kan du läsa [tekniska krav](/help/sites-deploying/technical-requirements.md).

   1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (spversion)` under [!UICONTROL Installed Products]. <!-- UPDATE FOR EACH NEW RELEASE -->

   1. Alla OSGi-paket är **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Use Web Console: `/system/console/bundles`).

      1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.2.14 eller senare (Använd webbkonsol: `/system/console/bundles`).

+++

+++4. Installera AEM Experience Manager Forms tilläggspaket

1. Kontrollera att du har installerat [!DNL Experience Manager] Service Pack.
1. Ladda ned motsvarande tilläggspaket från Forms på [AEM Forms-versioner](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) för ditt operativsystem.
1. Installera Forms tilläggspaket enligt beskrivningen i [Installera AEM Forms tilläggspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. Om du använder brev i Experience Manager 6.5 Forms installerar du [senaste AEMFD-kompatibilitetspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## Felsökning

* If **Dialogruta för pakethanterarens användargränssnitt** avslutar under installationen av Service Pack, vänta tills felloggarna har stabiliserats innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar det här problemet i webbläsaren Safari, men det kan inträffa i alla webbläsare.

* Kontrollera övervakningsloggarna (error.log) när installationen är klar för att se om det finns några aktiviteter. Vänta i några minuter tills loggarna inte har någon aktivitet. Starta om AEM.

* Om du får en **service-otillgängligt fel** efter installation av AEM Forms 6.5.15.0 eller senare, [installera serverns fragment och paket](/help/forms/using/aem-service-pack-installation-solution.md) för att åtgärda felet.
