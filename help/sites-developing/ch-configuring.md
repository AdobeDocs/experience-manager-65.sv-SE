---
title: ContextHub konfigureras
seo-title: ContextHub konfigureras
description: Lär dig hur du konfigurerar kontextnavet.
seo-description: Lär dig hur du konfigurerar kontextnavet.
uuid: f2988bb9-6878-42a2-bb51-c3f8683248c5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '1850'
ht-degree: 0%

---


# ContextHub {#configuring-contexthub} konfigureras

ContextHub är ett ramverk för att lagra, ändra och presentera kontextdata. Mer information om ContextHub finns i [utvecklardokumentationen](/help/sites-developing/contexthub.md). ContextHub ersätter [klientkontext](/help/sites-administering/client-context.md) i pekgränssnittet.

Konfigurera verktygsfältet [ContextHub](/help/sites-developing/contexthub.md) för att kontrollera om det visas i förhandsgranskningsläget, för att skapa ContextHub-butiker och lägga till gränssnittsmoduler med det Touch-optimerade användargränssnittet.

## Inaktiverar ContextHub {#disabling-contexthub}

Som standard är ContextHub aktiverat i en AEM installation. ContextHub kan inaktiveras för att förhindra att den läser in js/css och initierar. Det finns två alternativ för att inaktivera ContextHub:

* Redigera ContextHub-konfigurationen och markera alternativet **Inaktivera ContextHub**

   1. Klicka på eller tryck på **Verktyg > Platser > ContextHub**
   1. Klicka eller tryck på standardbehållaren **Configuration Container**
   1. Markera **ContextHub-konfigurationen** och klicka eller tryck på **Redigera markerat element**
   1. Klicka eller tryck på **Inaktivera ContextHub** och klicka eller tryck på **Spara**

eller

* Använd CRXDE Lite för att ställa in egenskapen `disabled` på **true** under `/libs/settings/cloudsettings`

>[!NOTE]
>
>[På grund av omstrukturering av databasen i AEM 6.4 har platsen ](/help/sites-deploying/repository-restructuring.md) för ContextHub-konfigurationer ändrats från  `/etc/cloudsettings` till:
>
> * `/libs/settings/cloudsettings`
> * `/conf/global/settings/cloudsettings`
> * `/conf/<tenant>/settings/cloudsettings`


## Visar och döljer ContextHub-gränssnittet {#showing-and-hiding-the-contexthub-ui}

Konfigurera Adobe Granite ContextHub OSGi-tjänsten för att visa eller dölja användargränssnittet [ContextHub](/help/sites-authoring/ch-previewing.md) på dina sidor. Tjänstens PID är `com.adobe.granite.contexthub.impl.ContextHubImpl.`

Om du vill konfigurera tjänsten kan du antingen använda [webbkonsolen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) eller en [JCR-nod i databasen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository):

* **Webbkonsol:** Om du vill visa användargränssnittet väljer du egenskapen Visa användargränssnitt. Om du vill dölja användargränssnittet avmarkerar du egenskapen Dölj användargränssnitt.
* **JCR-nod:** Om du vill visa användargränssnittet anger du den booleska  `com.adobe.granite.contexthub.show_ui` egenskapen till  `true`. Om du vill dölja användargränssnittet anger du egenskapen till `false`.

När du visar ContextHub-gränssnittet visas det bara på sidor AEM författarinstanser. Gränssnittet visas inte på sidor med publiceringsinstanser.

## Lägger till gränssnittslägen och moduler för ContextHub {#adding-contexthub-ui-modes-and-modules}

Konfigurera de gränssnittslägen och moduler som visas i ContextHub-verktygsfältet i förhandsgranskningsläget:

* Gränssnittslägen: Grupper av relaterade moduler
* Moduler: Widgetar som visar kontextdata från en butik och gör det möjligt för författare att ändra kontexten

Gränssnittslägen visas som en serie ikoner till vänster i verktygsfältet. När du väljer det här alternativet visas modulerna för ett användargränssnittsläge till höger.

![chlimage_1-319](assets/chlimage_1-319.png)

Ikoner är referenser från [ikonbiblioteket för gränssnitt för hörsel](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons).

### Lägga till ett gränssnittsläge {#adding-a-ui-mode}

Lägg till ett gränssnittsläge för att gruppera relaterade ContextHub-moduler. När du skapar gränssnittsläget anger du den titel och ikon som visas i ContextHub-verktygsfältet.

1. Klicka eller tryck på Verktyg > Platser > Kontextnav på Experience Manager-listen.
1. Klicka på eller tryck på standardkonfigurationsbehållaren.
1. Klicka eller tryck på Kontextnavkonfigurationen.
1. Klicka på eller tryck på knappen Skapa och klicka sedan på eller tryck på gränssnittsläget för kontextnav.

   ![chlimage_1-320](assets/chlimage_1-320.png)

1. Ange värden för följande egenskaper:

   * Titel för användargränssnittsläge: Titeln som identifierar användargränssnittsläget
   * Lägesikon: Väljaren för den [korallgränssnittsikon](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) som ska användas, till exempel `coral-Icon--user`
   * Aktiverad: Välj det här alternativet om du vill visa gränssnittsläget i kontextHub-verktygsfältet

1. Klicka på eller tryck på Spara.

### Lägga till en gränssnittsmodul {#adding-a-ui-module}

Lägg till en ContextHub-gränssnittsmodul i ett gränssnittsläge så att den visas i ContextHub-verktygsfältet för förhandsgranskning av sidinnehåll. När du lägger till en UI-modul skapar du en instans av en modultyp som är registrerad med ContextHub. Om du vill lägga till en gränssnittsmodul måste du känna till namnet på den associerade modultypen.

AEM innehåller en grundläggande gränssnittsmodultyp samt flera exempeltyper av gränssnittsmodul som du kan basera en gränssnittsmodul på. Följande tabell innehåller en kort beskrivning av vart och ett av dem. Mer information om hur du utvecklar en anpassad gränssnittsmodul finns i [Skapa gränssnittsmoduler för ContextHub](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Egenskaperna för användargränssnittsmodulen innehåller en detaljkonfiguration där du kan ange värden för modulspecifika egenskaper. Du anger detaljkonfigurationen i JSON-format. Kolumnen Modultyp i tabellen innehåller länkar till information om den JSON-kod som krävs för varje gränssnittsmodultyp.

| Modultyp | Beskrivning | Butik |
|---|---|---|
| [contexthub.base](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) | En allmän gränssnittsmodultyp | Konfigureras i gränssnittsmodulens egenskaper |
| [contexthub.browserinfo](/help/sites-developing/ch-samplemodules.md#contexthub-browserinfo-ui-module-type) | Visar information om webbläsaren | surferinfo |
| [contexthub.datetime](/help/sites-developing/ch-samplemodules.md#contexthub-datetime-ui-module-type) | Visar datum- och tidsinformation | datetime |
| [contexthub.device](/help/sites-developing/ch-samplemodules.md#contexthub-device-ui-module-type) | Visa klientenheten | emulatorer |
| [contexthub.location](/help/sites-developing/ch-samplemodules.md#contexthub-location-ui-module-type) | Visar klientens latitud och longitud samt platsen på en karta. Gör att du kan ändra platsen. | geolokalisering |
| [contexthub.screen-orientation](/help/sites-developing/ch-samplemodules.md#contexthub-screen-orientation-ui-module-type) | Visar enhetens skärmorientering (liggande eller stående) | emulatorer |
| [contexthub.tagcloud](/help/sites-developing/ch-samplemodules.md#contexthub-tagcloud-ui-module-type) | Visar statistik om sidtaggar | tagcloud |
| [granite.profile](/help/sites-developing/ch-samplemodules.md#granite-profile-ui-module-type) | Visar profilinformationen för den aktuella användaren, inklusive authorizedID, displayName och familyName. Du kan ändra värdet för displayName och familyName. | profil |

1. Klicka eller tryck på Verktyg > Platser > ContextHub på Experience Manager-listen.
1. Klicka på eller tryck på den konfigurationsbehållare som du vill lägga till en gränssnittsmodul i.
1. Klicka på eller skriv den ContextHub-konfiguration som du vill lägga till gränssnittsmodulen i.
1. Klicka eller tryck på det användargränssnittsläge som du lägger till användargränssnittsmodulen i.
1. Klicka på eller tryck på knappen Skapa och sedan på eller tryck på ContextHub UI Module (generisk).

   ![chlimage_1-321](assets/chlimage_1-321.png)

1. Ange värden för följande egenskaper:

   * Modultitel för användargränssnitt: En titel som identifierar gränssnittsmodulen
   * Modultyp: Modultypen
   * Aktiverad: Välj det här alternativet om du vill visa gränssnittsmodulen i ContextHub-verktygsfältet

1. (Valfritt) Om du vill åsidosätta standardkonfigurationen för lagring anger du ett JSON-objekt för att konfigurera UI-modulen.
1. Klicka på eller tryck på Spara.

## Skapar ett ContextHub-arkiv {#creating-a-contexthub-store}

Skapa ett kontextnavlager för att behålla användardata och komma åt data efter behov. ContextHub-butikerna baseras på registrerade butikskandidater. När du skapar butiken behöver du värdet för den storeType som butikskandidaten registrerats med. (Se [Skapa anpassade butikskandidater](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).)

### Detaljerad lagringskonfiguration {#detailed-store-configuration}

När du konfigurerar en butik kan du med egenskapen Detaljkonfiguration ange värden för butiksspecifika egenskaper. Värdet baseras på parametern `config` i butikens `init`-funktion. Därför beror det på butiken om du behöver ange det här värdet och värdeformatet.

Värdet för egenskapen Detaljkonfiguration är ett `config`-objekt i JSON-format.

### Exempel på lagringskandidater {#sample-store-candidates}

AEM innehåller följande exempel på butikskandidater som du kan basera en butik på.

| Butikstyp | Beskrivning |
|---|---|
| [aem.segmentation](/help/sites-developing/ch-samplestores.md#aem-segmentation-sample-store-candidate) | Lagra för lösta och olösta ContextHub-segment. Hämtar automatiskt segment från ContextHub SegmentManager |
| [aem.resolvedsegments](/help/sites-developing/ch-samplestores.md#aem-resolvedsegments-sample-store-candidate) | Lagrar de segment som är lösta just nu. Lyssnar på tjänsten ContextHub SegmentManager för att automatiskt uppdatera butiken |
| [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) | Lagrar latitud och longitud för webbläsarplatsen. |
| [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) | Lagrar aktuellt datum, aktuell tid och aktuell säsong för webbläsarplatsen |
| [granite.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) | Definierar egenskaper och funktioner för ett antal enheter och identifierar den aktuella klientenheten |
| [contexthub.generic-jsonp](/help/sites-developing/ch-samplestores.md#contexthub-generic-jsonp-sample-store-candidate) | Hämtar och lagrar data från en JSONP-tjänst |
| [granite.profile](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) | Lagrar profildata för den aktuella användaren |
| [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) | Lagrar information om klienten, t.ex. enhetsinformation, webbläsartyp och fönsterorientering |
| [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) | Lagrar sidtaggar och antal taggar |

1. Klicka eller tryck på Verktyg > Platser > ContextHub på Experience Manager-listen.
1. Klicka eller tryck på standardkonfigurationsbehållaren.
1. Klicka på Kontexthub-konfiguration
1. Om du vill lägga till en butik klickar eller trycker du på ikonen Skapa och sedan på eller trycker du på ContexHub Store Configuration.

   ![chlimage_1-322](assets/chlimage_1-322.png)

1. Ange värden för de grundläggande konfigurationsegenskaperna och klicka eller tryck sedan på Nästa:

   * **Konfigurationstitel:** Titeln som identifierar arkivet
   * **Bastyp:** Värdet för egenskapen storeType för butikskandidaten som butiken ska baseras på
   * **Obligatoriskt:** Välj
   * **Aktiverad:** Markera för att aktivera arkivet

1. (Valfritt) Om du vill åsidosätta standardarkivkonfigurationen anger du ett JSON-objekt i rutan Detaljkonfiguration (JSON).
1. Klicka på eller tryck på Spara.

## Exempel: Använda en JSONP-tjänst {#example-using-a-jsonp-service}

I det här exemplet visas hur du konfigurerar en lagringsplats och visar data i en gränssnittsmodul. I det här exemplet används MD5-tjänsten på jsontest.com-webbplatsen som datakälla för en butik. Tjänsten returnerar MD5-hash-koden för en sträng i JSON-format.

Ett contexthub.generic-jsonp-arkiv har konfigurerats så att det lagrar data för anropet `https://md5.jsontest.com/?text=%22text%20to%20md5%22`. Tjänsten returnerar följande data som visas i en gränssnittsmodul:

```xml
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### Skapar ett kontexthub.generic-jsonp-arkiv {#creating-a-contexthub-generic-jsonp-store}

Med exempelarkivkandidaten contexthub.generic-jsonp kan du hämta data från en JSONP-tjänst eller en webbtjänst som returnerar JSON-data. För den här butikskandidaten använder du butikskonfigurationen för att ange information om den JSONP-tjänst som ska användas.

Funktionen [init](/help/sites-developing/contexthub-api.md#init-name-config) i JavaScript-klassen `ContextHub.Store.JSONPStore` definierar ett `config`-objekt som initierar den här lagringskandidaten. Objektet `config` innehåller ett `service`-objekt som innehåller information om JSONP-tjänsten. Om du vill konfigurera arkivet anger du objektet `service` i JSON-format som värde för egenskapen Detaljkonfiguration.

Om du vill spara data från MD5-tjänsten på jsontest.com-webbplatsen ska du följa proceduren i [Skapa ett ContextHub Store](/help/sites-developing/ch-configuring.md#creating-a-contexthub-store) med följande egenskaper:

* **Konfigurationstitel:** md5
* **Bastyp:** contexthub.generic-jsonp
* **Obligatoriskt:** Välj
* **Aktiverad:** Markera
* **Detaljkonfiguration (JSON):**

   ```xml
   {
    "service": {
    "jsonp": false,
    "timeout": 1000,
    "ttl": 1800000,
    "secure": false,
    "host": "md5.jsontest.com",
    "port": 80,
    "params":{
    "text":"text to md5"
        }
      }
    }
   ```

### Lägga till en gränssnittsmodul för md5-data {#adding-a-ui-module-for-the-md-data}

Lägg till en gränssnittsmodul i ContextHub-verktygsfältet för att visa data som lagras i exempelarkivet md5. I det här exemplet används modulen contexthub.base för att skapa följande gränssnittsmodul:

![chlimage_1-323](assets/chlimage_1-323.png)

Använd proceduren i [Lägga till en UI-modul](#adding-a-ui-module) för att lägga till UI-modulen i ett befintligt UI-läge, t.ex. exemplet UI-läge. Använd följande egenskapsvärden för UI-modulen:

* **UI-modultitel:** MD5
* **Modultyp:** contexthub.base
* **Detaljkonfiguration (JSON):**

   ```xml
   {
    "icon": "coral-Icon--data",
    "title": "MD5 Converstion",
    "storeMapping": { "md5": "md5" },
    "template": "<p> {{md5.original}}</p>;
                 <p>{{md5.md5}}</p>"
   }
   ```

## Felsöka ContextHub {#debugging-contexthub}

Ett felsökningsläge för ContextHub kan aktiveras för att tillåta felsökning. Felsökningsläget kan aktiveras antingen via ContextHub-konfigurationen eller via CRXDE.

### Via konfigurationen {#via-the-configuration}

Redigera ContextHub-konfigurationen och markera alternativet **Felsök**

1. Klicka på eller tryck på **Verktyg > Platser > ContextHub**
1. Klicka eller tryck på standardbehållaren **Configuration Container**
1. Markera **ContextHub-konfigurationen** och klicka eller tryck på **Redigera markerat element**
1. Klicka eller tryck på **Debug** och klicka eller tryck på **Save**

### Via CRXDE {#via-crxde}

Använd CRXDE Lite för att ställa in egenskapen `debug` på **true** under:

* `/conf/global/settings/cloudsettings` eller
* `/conf/<tenant>/settings/cloudsettings`

>[!NOTE]
>
>För ContextHub-konfigurationer som fortfarande finns under de tidigare sökvägarna är platsen som ska anges `debug property` `/libs/settings/cloudsettings/legacy/contexthub` &lt;a1/>.

### Tyst läge {#silent-mode}

I tyst läge inaktiveras all felsökningsinformation. Till skillnad från det normala felsökningsalternativet, som kan anges separat för varje ContextHub-konfiguration, är tyst läge en global inställning som har företräde framför eventuella felsökningsinställningar på ContextHub-konfigurationsnivån.

Detta är användbart för din publiceringsinstans där du inte vill ha någon felsökningsinformation alls. Eftersom det är en global inställning aktiveras den via OSGi.

1. Öppna **Adobe Experience Manager Web Console Configuration** `http://<host>:<port>/system/console/configMgr`
1. Sök efter **Adobe Granite ContextHub**
1. Klicka på konfigurationen **Adobe Granite ContextHub** för att redigera dess egenskaper
1. Markera alternativet **Tyst läge** och klicka på **Spara**

## Återställer ContextHub-konfigurationer efter uppgradering av {#recovering-contexthub-configurations-after-upgrading}

När en [uppgradering till AEM](/help/sites-deploying/upgrade.md) utförs, säkerhetskopieras ContextHub-konfigurationerna och lagras på en säker plats. Under uppgraderingen installeras ContextHub-standardkonfigurationerna, vilket ersätter de befintliga konfigurationerna. Säkerhetskopieringen krävs för att bevara ändringar eller tillägg som du har gjort.

ContextHub-konfigurationer lagras i en mapp med namnet `contexthub` under följande noder:

* `/conf/global/settings/cloudsettings`
* `/conf/<tenant>/settings/cloudsettings`

Efter en uppgradering lagras säkerhetskopian i en mapp med namnet `contexthub` under en nod med namnet:

`/conf/global/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx` eller
`/conf/<tenant>/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx`

Delen `yyyymmdd` i nodnamnet är det datum då uppgraderingen utfördes.

Om du vill återställa dina ContextHub-konfigurationer använder du CRXDE Lite för att kopiera noderna som representerar dina butiker, gränssnittslägen och gränssnittsmoduler från under `default-pre-upgrade_yyyymmdd_xxxxxx`-noden till nedan:

* `/conf/global/settings/cloudsettings` eller
* `/conf/<tenant>/settings/cloudsettings`
