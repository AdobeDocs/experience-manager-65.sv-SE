---
title: Uppgradera till AEM 6.5-formulär
seo-title: Uppgradera till AEM 6.5-formulär
description: Du kan uppgradera direkt från AEM 6.1-formulär, AEM 6.2-formulär och LiveCycle ES4 SP1 till AEM 6.3-formulär.
seo-description: Du kan uppgradera direkt från AEM 6.1-formulär, AEM 6.2-formulär och LiveCycle ES4 SP1 till AEM 6.3-formulär.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Uppgradera till AEM 6.5 Forms on OSGi {#upgrade-to-aem-forms-osgi}

Du kan uppgradera direkt från AEM 6.3-formulär eller AEM 6.4-formulär till AEM 6.5-formulär.

Direktuppgradering från **AEM 6.0 Forms, AEM 6.1 Forms** och **AEM 6.2 Forms** till AEM 6.5 Forms är inte tillgängligt. Utför en mellanliggande [uppgradering till AEM 6.2 Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html), [uppgradera till AEM 6.3 Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html)eller [uppgradera till AEM 6.4 Forms](/help/forms/using/upgrade.md) och uppgradera sedan från AEM 6.3 Forms eller AEM 6.4 Forms till AEM 6.5 Forms.

Gör följande för att uppgradera från AEM 6.3-formulär eller AEM 6.4-formulär till AEM 6.5-formulär:

1. Uppgradera den befintliga AEM-instansen till AEM 6.5. Stegen listas nedan:

   1. Installera de senaste Service Pack-uppdateringarna och patcharna för AEM 6.3-formulär eller AEM 6.4-formulär. Mer information finns i [AEM Sustenance Hub](https://helpx.adobe.com/experience-manager/aem-releases-updates.html).
   1. Förbered källinstansen för uppgraderingen. Mer information finns i [Uppgradera till AEM 6.5](/help/sites-deploying/upgrade.md).
   1. Ladda ned [AEM 6.5 QuickStart](/help/sites-deploying/deploy.md#getting%20the%20software).
   1. **(Endast Unix/Linux-baserade installationer)** Om du använder UNIX eller Linux som underliggande operativsystem öppnar du terminalfönstret, navigerar till mappen som innehåller crx-quickstart och kör följande kommando:

      `chmod -R 755 ../crx-quickstart`

   1. Uppgradera din AEM-instans till AEM 6.3. Stegvisa instruktioner finns i [Uppgradera till AEM 6.5](/help/sites-deploying/upgrade.md).

      Innan du fortsätter med nästa steg väntar du tills meddelandena ServiceEvent REGISTERED och ServiceEvent UNREGISTERED inte visas i filen &lt;crx-database>/error.log.

      >[!NOTE]
      >
      >När servern har startats och körts är några av AEM Forms-paketen fortfarande i installationstillstånd. Antalet paket kan variera för varje installation. Du kan ignorera läget för dessa paket. Paketen listas på https://&#39;[server]:[port]&#39;/system/console/.

1. Installera tilläggspaketet AEM Forms. Stegen listas nedan:

   1. Logga in på AEM-servern som administratör och öppna paketresursen. Standardwebbadressen för paketresursen är `https://'[server]:[port]'/crx/packageshare`.
   1. I paketresursen söker du efter **AEM 6.5-formulärtilläggspaket**, klickar på det paket som gäller för ditt operativsystem och klickar på **Hämta**. Läs och godkänn licensavtalet och klicka på **OK**. Nedladdningen startar. När du har hämtat **visas ordet Hämtad** bredvid paketet.

      Du kan också använda de hyperlänkar som visas i [AEM Forms-versioner](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) för att hämta ett paket manuellt.

   1. När nedladdningen är klar klickar du på **Nedladdad**. Du omdirigeras till pakethanteraren. I pakethanteraren söker du efter det hämtade paketet och klickar på **Installera**.

      Om du hämtar paketet manuellt med hjälp av den direktlänk som visas i [AEM Forms-releaser](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)öppnar du AEM Package Manager, klickar på **Överför paket**, markerar det hämtade paketet och klickar på Överför. När paketet har överförts klickar du på paketnamnet och sedan på **Installera.**

      >[!NOTE]
      >
      >När paketet har installerats uppmanas du att starta om AEM-instansen. **Stoppa inte servern omedelbart.** Innan du stoppar AEM Forms-servern väntar du tills ServiceEvent REGISTERED- och ServiceEvent UNREGISTERED-meddelandena inte längre visas i &lt;crx-database>/error.log och loggen är stabil. Observera också att ett fåtal paket kan vara i installerat läge. Du kan ignorera dessa paketen.

   1. Starta om AEM-instansen.

1. Utför efterinstallationsaktiviteter.

   * **Kör migreringsverktyg**

      Migreringsverktyget gör att anpassningsbara formulär och korrespondenshanteringsresurser i tidigare versioner blir kompatibla med AEM 6.5-formulär. Du kan hämta verktyget från AEM-paketresursen. Stegvis information om hur du konfigurerar och använder migreringsverktyget finns i [Migreringsverktyget](../../forms/using/migration-utility.md).

      Om du använder [Sample för att integrera utkast och inskickskomponenter](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) i databasen och uppgradera från en tidigare version kör du följande SQL-frågor när du har utfört uppgraderingen:

      ```
      UPDATE metadata m, additionalmetadatatable am
      SET m.dataType = am.value
      WHERE m.id = am.id
      AND am.key = 'dataType'
      ```

      ```
      DELETE from additionalmetadatatable
      WHERE `key` = 'dataType'
      ```

   * **(Om du uppgraderar från AEM 6.2-formulär eller tidigare versioner) Konfigurera om Adobe Sign**

      Om du hade konfigurerat Adobe Sign i den tidigare versionen av AEM Forms konfigurerar du om Adobe Sign från AEM Cloud-tjänster. Mer information finns i [Integrera Adobe Sign med AEM-formulär](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Stöd för jQuery**

      I AEM 6.5 Forms uppdateras versionen av jQuery till 3.2.1 och användargränssnittsversionen för jQuery uppdateras till 1.12.1. AEM Form använder JQuery i **noConflict** -läge. Om du använder någon annan jQuery-version visas inga problem när du uppgraderar. När du uppgraderar till AEM 6.5 Forms:

      * Kontrollera att eventuella anpassade komponenter är kompatibla med jQuery-versioner som stöds.
      * Ta bort API:er som inte stöds från de anpassade komponenterna. En lista över borttagna API:er finns i [uppgraderingsguiden](https://jquery.com/upgrade-guide/3.0/) . Stöd för API:erna load(), .unload() och .error() har tagits bort. Använd metoden .on() i stället för tidigare nämnda API:er. Ändra till exempel $(&quot;img&quot;).load(fn) till $(&quot;img&quot;).on(&quot;load&quot;, fn).
   * **(Om du uppgraderar från AEM 6.2 Forms eller tidigare versioner) Konfigurera om analyser och rapporter**

      I AEM 6.4 Forms är inte trafikvariabeln source och success event för intryckt tillgänglig. När du uppgraderar från AEM 6.2 Forms eller tidigare versioner slutar AEM Forms skicka data till Adobe Analytics-servern och analysrapporter för adaptiva formulär är inte tillgängliga. Dessutom introducerar AEM 6.4 Forms trafikvariabler för den version av formuläranalysen och händelsen success för den tid som läggs på ett fält. Konfigurera om analyser och rapporter för AEM Forms-miljön. Detaljerade steg finns i [Konfigurera analyser och rapporter](../../forms/using/configure-analytics-forms-documents.md).


1. Kontrollera att servern har uppgraderats, att alla data har migrerats och att den fungerar som vanligt.

   * **Verifiera paketens status:** Kontrollera att alla paket är i aktivt läge.
   * **Verifiera replikering och omvänd replikering:** Publicera, fyll i och skicka några migrerade formulär. Verifiera också skickade data.
   * **Verifiera åtkomst till användargränssnitt för administratörer och utvecklare:** Logga in på AEM-instansen från ett administratörskonto och verifiera att du har tillgång till följande URL:er:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`
   >[!NOTE]
   I AEM 6.4 Forms har strukturen för crx-databasen ändrats. Om du uppgraderar från 6.3-formulär till AEM 6.5-formulär kan du använda de ändrade sökvägarna för anpassning som du skapar på nytt. En fullständig lista över ändrade sökvägar finns i [Omstrukturering av formulärdatabaser i AEM](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).

