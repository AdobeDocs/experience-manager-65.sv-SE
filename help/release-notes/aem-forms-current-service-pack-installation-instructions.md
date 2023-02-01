---
title: Installationsanvisningar för AEM Forms Patch för AEM Forms
description: Installationsanvisningar för AEM Forms Service Pack för OSGi- och JEE-miljö
source-git-commit: a470627eb87735dd55edda93c3e2dac4a2c36752
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 0%

---


# Installationsanvisningar för AEM 6.5 Forms Service Pack {#aem-form-patch-installation-instructions}

## Versionsinformation

| Produkt | Adobe Experience Manager 6.5 Forms |
|---|---|
| Version | 6.5.15.0 |
| Typ | Service Pack-version |
| Date | 1 december 2022 |
| Hämta URL | [Senaste AEM Forms Releases](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) |

>[!NOTE]
>
>Se de senaste [AEM Service Pack versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html#forms-6515) för en fullständig lista över åtgärdade problem.

## Vad ingår i Experience Manager Forms 6.5

Adobe Experience Manager (AEM) Forms Service Pack innehåller nya och uppgraderade funktioner, t.ex. viktiga kundefterfrågade förbättringar, prestanda, stabilitet och säkerhetsförbättringar. AEM Forms lanserar Service Pack med regelbundna intervall för att ge tillgång till de senaste funktionerna och förbättringarna. Beroende på din stack väljer du en av följande sökvägar för att hämta och installera Service Pack på din miljö:

* [Hämta och installera Service Pack på ett AEM formulär i JEE-miljö](#download-and-install-for-jee-service-pack)
* [Hämta och installera Service Pack på en AEM i OSGi-miljö](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> Adobe släpper ett fullständigt installationsprogram efter varje sjätte Service Pack. AEM 6.5 Forms Service Pack 12 (6.5.12.0) i JEE är det sista fullständiga installationsprogrammet. Det fullständiga installationsprogrammet har stöd för nya plattformar, medan det vanliga installationsprogrammet för Service Pack endast innehåller felkorrigeringar och allmänna förbättringar. Om du gör en ny installation eller planerar att använda den senaste programvaran för din AEM 6.5 Forms i JEE-miljö rekommenderar Adobe att du använder AEM 6.5.12.0 Forms i JEE-fullversionen som släpptes den 3 mars 2022 i stället för det AEM 6.5 Forms-installationsprogrammet som släpptes den 8 april 2019. Installera det senaste Service Pack-paketet när du har använt det fullständiga installationsprogrammet.

## Hämta och installera Service Pack på ett AEM formulär i JEE-miljö {#download-and-install-for-jee-service-pack}

![JEE-installation](/help/forms/using/assets/jeeinstallation.png)

+++1. Säkerhetskopiera din befintliga miljö:

1. Säkerhetskopiera [CRX-databas, databasschema och GDS (global dokumentlagring)](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).
1. Säkerhetskopiera &lt;*AEM_forms_root*>/distribuera mapp. Det krävs om du bestämmer dig för att avinstallera Service Pack.

>[!NOTE]
>
> Innan du kör installationsprogrammet för AEM Service Pack bör du kontrollera att du har skrivbehörighet AEM installationskatalogen.

+++

+++2.Ladda ned nödvändig programvara:

* [AEM Forms on JEE 6.5.15.0 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/jee-patch-installer-65.html)
* [AEM 6.5.15.0 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fservicepack%2Faem-service-pkg-6.5.15.0.zip)
* [Forms tilläggspaket](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-forms-addon-2022.12.20.00-220900.zip)
* [Fragmentservervlet](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

+++

+++3. Installera AEM Forms på JEE-Service Pack:

1. Stoppa programservern.
1. Extrahera **AEM Forms på installationsarkiv för JEE 6.5.15.0 Service Pack** till hårddisken:

   * **Windows**
Navigera till rätt katalog på installationsmediet eller mappen på hårddisken där du kopierade installationsprogrammet och dubbelklicka på 
`aemforms65_cfp_install.exe` -fil.

      * (32-bitars Windows) `Windows\Disk1\InstData\VM`
      * (64-bitars Windows) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux®**
Navigera till rätt katalog och från ett skal och en typ 
`./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Då startas en installationsguide som vägleder dig genom installationen.

1. På introduktionspanelen klickar du på **[!UICONTROL Next]**.
1. På **Välj installationsmapp** kontrollerar du att den standardplats som visas är korrekt för din befintliga installation eller klickar på **[!UICONTROL Browse]** för att välja en alternativ mapp där AEM är installerad och klicka på **[!UICONTROL Next]**.
1. Läs sammanfattningsinformationen för Service Pack och klicka på **[!UICONTROL Next]**.
1. Läs mer i Sammanfattning av förinstallation och klicka på **[!UICONTROL Install]**.
1. När installationen är klar klickar du på **[!UICONTROL Next]** för att använda snabbkorrigeringsuppdateringar på dina installerade filer.
1. **[Endast för Windows]:** Utför något av följande steg:

   * Avmarkera **Starta Configuration Manager** innan du klickar **[!UICONTROL Done]**. Kör **Konfigurationshanteraren** genom att använda **ConfigurationManager.bat** filen finns i `[aem-forms root]\configurationManager\bin`.

   * Eller avmarkera **Starta Configuration Manager** innan du klickar **[!UICONTROL Done]**. Före körning **Konfigurationshanteraren** använda **ConfigurationManager.exe** eller **ConfigurationManager_IPv6.exe**, navigera till *`<AEMForms_Install_Dir>\configurationManager\bin`* katalog och ersätt [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) och [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) filer.

      >[!NOTE]
      >
      > Använda **ConfigurationManager.bat** kan du undvika att uppdatera namnet på .lax-filer manuellt.

1. **[Endast för Unix-baserade]:** The **Starta Configuration Manager** är markerad som standard. Klicka **[!UICONTROL Done]** för att köra Configuration Manager direkt eller för att köra **Konfigurationshanteraren** avmarkera **Starta Configuration Manager** innan du klickar **[!UICONTROL Done]**. Du kan börja **Konfigurationshanteraren** senare använda lämpligt skript i `[AEM_forms_root]/configurationManager/bin` katalog.

   Du måste utföra de angivna åtgärderna när du kör **Konfigurationshanteraren**:
   * Konfigurera CRX
   * Driftsätt Adobe Experience Manager Forms EAR
   * Initiera Adobe Experience Manager Forms-databas
   * Distribuera Adobe Experience Manager Forms-komponenter
   * Driftsätt och validera DSC-burkarna.

1. Beroende på programservern väljer du ett av följande dokument och följer instruktionerna i *Konfigurera och distribuera AEM formulär* -avsnitt.

   * [Installera och distribuera AEM formulär för JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Installera och distribuera AEM för WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)
   * [Installera och distribuera AEM Forms för WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65)

>[!NOTE]
>
> När du har installerat AEM Forms på JEE-Service Pack måste du ta bort Forms-tilläggspaketet från `crx-repository\install` innan appservern startas om. Hämta det senaste Forms-tilläggspaketet från [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

+++

+++4. Installera serverletsfragmentet

Det är obligatoriskt att installera **serletfragment** för alla programservrar utom de som körs på JBoss® EAP 7.4.0. Så här hämtar och installerar du serverletsfragmentet:

1. Om du inte har hämtat fragmentet hämtar du det från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

1. Starta programservern, vänta på att loggarna ska stabiliseras och kontrollera paketläget.

1. Öppna Web Console Bundles. Standardwebbadressen är `http://[Server]:[Port]/system/console/bundles`.

1. Klicka på Installera/Uppdatera. Välj det hämtade fragmentet, `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. Klicka **Installera** eller **Uppdatera**. Vänta tills programservern har stabiliserats

1. Stoppa programservern.

+++

+++5. Installera AEM Service Pack

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.
1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager] -instans.
1. Hämta Service Pack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Öppna Pakethanteraren och välj **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns på [Pakethanteraren](/help/sites-administering/package-manager.md).
1. Markera paketet och välj **[!UICONTROL Install]**.
1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3 - datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

**Automatisk installation**

Det finns två olika metoder som du kan använda för att installera automatiskt [!DNL ExperienceManager] 6.5.15.0<!--       UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i `../crx-quickstart/install` när servern är tillgänglig online.
Paketet installeras automatiskt.

* Använd [HTTP-API från Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html). Använd  `cmd=install&recursive=true` så att de kapslade paketen installeras.

   >[!NOTE]
   >
   >Experience Manager 6.5.15.0 stöder inte installation av Bootstrap. <!-- UPDATE FOR EACHNEW RELEASE -->

**Validera installationen**

Om du vill veta vilka plattformar som är certifierade för att fungera med den här versionen kan du läsa [tekniska krav](/help/sites-deploying/technical-requirements.md).

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience      Manager (6.5.15.0)` under [!UICONTROL Installed Products].<!-- UPDATE FOR EACH NEW RELEASE -->
1. Alla OSGi-paket är antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Använd webbkonsol: `/system/console/bundles`).
1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.2.13 eller senare (Använd WebConsole: `/system/console/     bundles`).

+++

+++6. Installera AEM Experience Manager Forms tilläggspaket

1. Kontrollera att du har installerat [!DNL Experience Manager] Service Pack.
1. Ladda ned motsvarande tilläggspaket från Forms på [AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#forms-updates) för ditt operativsystem.
1. Installera Forms tilläggspaket enligt beskrivningen i [Installera AEM Forms tilläggspaket](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi.html?lang=en#install-aem-forms-add-on-package).
1. Om du använder bokstäver i Experience Manager 6.5 Forms installerar du [senaste AEMFD-kompatibilitetspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++


<!-- 1. (JBoss only) After installing the patch and configuring the server, delete  tmp  and work directories of JBoss application server.

>[!IMPORTANT]
>
>Before installing [AEM 6.5.15.0 service pack](#install-the-aem-service-pack-install-aem-service-pack), for all the AEM Forms on JEE environments using any application servers other than JBoss EAP 7.4.0: 
> * Install  the [org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) servlet fragment and wait for the application server to stabilize.
>* If you install the latest [AEM service pack (6.5.15.0)](#install-the-aem-service-pack-install-aem-service-pack), prior to the fragment servlet `org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar` on JEE environment, the CRX/bundle and the start page show service unavailable errors, [click here](/help/forms/using/aem-service-pack-installation-solution.md) to know the troubleshooting steps. 

### !-->


## Hämta och installera Service Pack på en AEM i OSGi-miljö {#download-and-install-for-osgi-service-pack}

![Installationssteg för OSGi](/help/forms/using/assets/osgiinstallation.png)


+++1. Säkerhetskopiera din befintliga miljö:

1. Säkerhetskopiera [CRX-databas och databasschema](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).

>[!NOTE]
>
> Om du installerar AEM Forms Service Pack för relationsdatabas måste du säkerhetskopiera DB_schema.

+++

+++2.Ladda ned nödvändig programvara:

* [AEM 6.5.15.0 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fservicepack%2Faem-service-pkg-6.5.15.0.zip)
* [Forms tilläggspaket](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-forms-addon-2022.12.20.00-220900.zip)

+++

+++3. Installera AEM Service Pack

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.
1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager] -instans.
1. Hämta Service Pack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Öppna Pakethanteraren och välj **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns på [Pakethanteraren](/help/sites-administering/package-manager.md).
1. Markera paketet och välj **[!UICONTROL Install]**.
1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3 - datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

**Automatisk installation**

Det finns två olika metoder som du kan använda för att installera automatiskt [!DNL Experience Manager] 6.5.15.0<!--       UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.
* Använd [HTTP-API från Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html). Använd `cmd=install&recursive=true` så att de kapslade paketen installeras.

   >[!NOTE]
   >
   >Experience Manager 6.5.15.0 stöder inte installation av Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validera installationen**

Om du vill veta vilka plattformar som är certifierade för att fungera med den här versionen kan du läsa [tekniska krav](/help/sites-deploying/technical-requirements.md).

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience      Manager (6.5.15.0)` under [!UICONTROL Installed Products]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Alla OSGi-paket är antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Use Web Console: `/system/console/bundles`).

   1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.2.13 eller senare (Använd webbkonsol: `/system/console/bundles`).

+++

+++4. Installera AEM Experience Manager Forms tilläggspaket

1. Kontrollera att du har installerat [!DNL Experience Manager] Service Pack.
1. Ladda ned motsvarande tilläggspaket från Forms på [AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#forms-updates) för ditt operativsystem.
1. Installera Forms tilläggspaket enligt beskrivningen i [Installera AEM Forms tilläggspaket](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi.html?lang=en#install-aem-forms-add-on-package).
1. Om du använder bokstäver i Experience Manager 6.5 Forms installerar du [senaste AEMFD-kompatibilitetspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## Felsökning

* Installera om AEM Forms Service Pack om ett fel inträffar under installationen. Kontakta produktteamet om problemet kvarstår.

* If **Dialogruta för pakethanterarens användargränssnitt** avslutar under installationen av Service Pack, vänta tills felloggarna har stabiliserats innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar det här problemet i webbläsaren Safari, men det kan inträffa i alla webbläsare.

* Kontrollera övervakningsloggarna (error.log) när installationen är klar för att se om det finns några aktiviteter. Vänta i några minuter tills loggarna inte har någon aktivitet. Starta om AEM.

* Om du får en **service-otillgängligt fel** efter installation av senaste AEM Forms 6.5.15.0 Service Pack, [installera serverns fragment och paket](/help/forms/using/aem-service-pack-installation-solution.md) för att åtgärda felet.


