---
title: Uppgradera till AEM 6.5 Forms
seo-title: Uppgradera till AEM 6.5 Forms
description: Du kan uppgradera direkt från AEM 6.1 Forms, AEM 6.2 Forms och LiveCycle ES4 SP1 till AEM 6.3 Forms.
seo-description: Du kan uppgradera direkt från AEM 6.1 Forms, AEM 6.2 Forms och LiveCycle ES4 SP1 till AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 1e39455e-f588-42a2-91f5-daefcfed82a0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# Uppgradera till AEM 6.5 Forms på OSGi {#upgrade-to-aem-forms-osgi}

Du kan uppgradera direkt från AEM 6.3 Forms eller AEM 6.4 Forms till AEM 6.5 Forms.

Direktuppgradering från **AEM 6.0 Forms, AEM 6.1 Forms** och **AEM 6.2 Forms** till AEM 6.5 Forms är inte tillgängligt. Utför en mellanliggande [uppgradering till AEM 6.2 Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html), [uppgradering till AEM 6.3 Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html) eller [uppgradering till AEM 6.4 Forms](/help/forms/using/upgrade.md) och uppgradera sedan från AEM 6.3 Forms eller AEM 6.4 Forms till AEM 6.5.

Gör följande för att uppgradera från AEM 6.3 Forms eller AEM 6.4 Forms till AEM 6.5 Forms:

1. Uppgradera den befintliga AEM till AEM 6.5. Stegen listas nedan:

   1. Installera den senaste Service Pack-uppdateringen och patcharna för AEM 6.3 Forms eller AEM 6.4 Forms. Mer information finns i [AEM uthåb](https://helpx.adobe.com/experience-manager/aem-releases-updates.html).
   1. Förbered källinstansen för uppgraderingen. Mer information finns i [Uppgradera till AEM 6.5](/help/sites-deploying/upgrade.md).
   1. Ladda ned [AEM 6.5 QuickStart](/help/sites-deploying/deploy.md#getting%20the%20software).
   1. **(Endast Unix/Linux-baserade installationer)** Om du använder UNIX eller Linux som underliggande operativsystem öppnar du terminalfönstret, navigerar till mappen som innehåller crx-quickstart och kör följande kommando:

      `chmod -R 755 ../crx-quickstart`

   1. Uppgradera din AEM till AEM 6.3. Stegvisa instruktioner finns i [Uppgradera till AEM 6.5](/help/sites-deploying/upgrade.md).

      Innan du fortsätter med nästa steg väntar du tills meddelandena ServiceEvent REGISTERED och ServiceEvent UNREGISTERED inte visas i filen &lt;crx-database>/error.log.

      >[!NOTE]
      >
      >När servern är igång är några AEM Forms-paket fortfarande i installationstillstånd. Antalet paket kan variera för varje installation. Du kan ignorera läget för dessa paket. Paketen listas på https://&#39;[server]:[port]&#39;/system/console/.

1. Installera AEM Forms tilläggspaket. Stegen listas nedan:

   1. Öppna [Programvarudistribution](https://experience.adobe.com/downloads). Du behöver en Adobe ID för att logga in på Software Distribution.
   1. Tryck på **[!UICONTROL Adobe Experience Manager]** som finns i rubrikmenyn.
   1. I avsnittet **[!UICONTROL Filters]**:
      1. Välj **[!UICONTROL Forms]** i listrutan **[!UICONTROL Solution]**.
      1. Välj version och typ för paketet. Du kan också använda alternativet **[!UICONTROL Search Downloads]** för att filtrera resultaten.
   1. Tryck på det paketnamn som gäller för ditt operativsystem, välj **[!UICONTROL Accept EULA Terms]** och tryck på **[!UICONTROL Download]**.
   1. Öppna [Pakethanteraren](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) och klicka på **[!UICONTROL Upload Package]** för att överföra paketet.
   1. Markera paketet och klicka på **[!UICONTROL Install]**.

      Du kan också hämta paketet via den direktlänk som anges i [AEM Forms-releaser](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)-artikeln.

      >[!NOTE]
      >
      >När paketet har installerats uppmanas du att starta om AEM. **Stoppa inte servern omedelbart.** Innan du stoppar AEM Forms-servern väntar du tills meddelandena ServiceEvent REGISTERED och ServiceEvent UNREGISTERED inte visas i  &lt;crx-repository>/error.log och loggen är stabil. Observera också att ett fåtal paket kan vara i installerat läge. Du kan ignorera dessa paketen.

1. Starta om AEM.

1. Utför efterinstallationsaktiviteter.

   * **Kör migreringsverktyg**

      Migreringsverktyget gör att anpassningsbara formulär och korrespondenshanteringsresurser i tidigare versioner blir kompatibla med AEM 6.5-formulär. Du kan hämta verktyget från AEM Software Distribution. Stegvis information om hur du konfigurerar och använder migreringsverktyget finns i [migreringsverktyg](../../forms/using/migration-utility.md).

      Om du använder [Exempel för att integrera utkast och inskickningskomponent](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) med databasen och uppgradera från en tidigare version kör du följande SQL-frågor när du har utfört uppgraderingen:

      ```sql
      UPDATE metadata m, additionalmetadatatable am
      SET m.dataType = am.value
      WHERE m.id = am.id
      AND am.key = 'dataType'
      ```

      ```sql
      DELETE from additionalmetadatatable
      WHERE `key` = 'dataType'
      ```

   * **(Endast vid uppgradering från AEM 6.2 Forms eller tidigare versioner) Konfigurera om Adobe Sign**

      Om du hade konfigurerat Adobe Sign i den tidigare versionen av AEM Forms konfigurerar du om Adobe Sign från AEM Cloud-tjänsterna. Mer information finns i [Integrera Adobe Sign med AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Stöd för jQuery**

      I AEM 6.5 Forms uppdateras jQuery till 3.2.1 och jQuery UI-versionen uppdateras till 1.12.1. AEM Form använder JQuery i **noConflict**-läge. Om du använder någon annan jQuery-version visas inga problem när du uppgraderar. När du uppgraderar till AEM 6.5 Forms:

      * Kontrollera att eventuella anpassade komponenter är kompatibla med jQuery-versioner som stöds.
      * Ta bort API:er som inte stöds från de anpassade komponenterna. I [uppgraderingsguiden](https://jquery.com/upgrade-guide/3.0/) finns en lista över borttagna API:er. Stöd för API:erna load(), .unload() och .error() har tagits bort. Använd metoden .on() i stället för tidigare nämnda API:er. Ändra till exempel $(&quot;img&quot;).load(fn) till $(&quot;img&quot;).on(&quot;load&quot;, fn).
   * **(Endast vid uppgradering från AEM 6.2 Forms eller tidigare versioner) Konfigurera om analyser och rapporter**

      I AEM 6.4 Forms är inte trafikvariabeln source och success event för intryckt tillgänglig. Så när du uppgraderar från AEM 6.2 Forms eller tidigare, slutar AEM Forms skicka data till Adobe Analytics server och analysrapporter för adaptiva formulär är inte tillgängliga. Dessutom introducerar AEM 6.4 Forms trafikvariabler för den version av formuläranalysen och händelsen success för den tid som läggs på ett fält. Så konfigurera om analyser och rapporter för er AEM Forms-miljö. Detaljerade steg finns i [Konfigurera analyser och rapporter](../../forms/using/configure-analytics-forms-documents.md).


1. Kontrollera att servern har uppgraderats, att alla data har migrerats och att den fungerar som vanligt.

   * **Kontrollera paketens status:** Kontrollera att alla paket är i aktivt läge.
   * **Verifiera replikering och omvänd replikering:** Publicera, fyll i och skicka några migrerade formulär. Verifiera också skickade data.
   * **Verifiera åtkomst till användargränssnitt för administratörer och utvecklare:** Logga in AEM instansen från ett administratörskonto och verifiera att du har åtkomst till följande URL:er:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   I AEM 6.4 Forms har strukturen för crx-database ändrats. Om du uppgraderar från 6.3 Forms till AEM 6.5 Forms kan du använda de nya anpassningsmöjligheterna som du skapar på nytt. En fullständig lista över ändrade sökvägar finns i [Omstrukturering av Forms-databaser i AEM](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).
