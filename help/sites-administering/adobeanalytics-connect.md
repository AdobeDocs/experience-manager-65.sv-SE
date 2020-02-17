---
title: Ansluta till Adobe Analytics och skapa ramverk
seo-title: Ansluta till Adobe Analytics och skapa ramverk
description: Lär dig hur du ansluter AEM till SiteCatalyst och skapar ramverk.
seo-description: Lär dig hur du ansluter AEM till SiteCatalyst och skapar ramverk.
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# Ansluta till Adobe Analytics och skapa ramverk {#connecting-to-adobe-analytics-and-creating-frameworks}

Om du vill spåra webbdata från dina AEM-sidor i Adobe Analytics skapar du en konfiguration för Adobe Analytics Cloud Services och ett ramverk för Adobe Analytics:

* **** Adobe Analytics-konfiguration: Informationen om ditt Adobe Analytics-konto. Med Adobe Analytics-konfigurationen kan AEM ansluta till Adobe Analytics. Skapa en Adobe Analytics-konfiguration för varje konto du använder.
* **** Adobe Analytics Framework: En uppsättning mappningar mellan egenskaper för Adobe Analytics-rapportsviten och CQ-variabler. Använd ett ramverk för att konfigurera hur webbplatsdata fyller i era Adobe Analytics-rapporter. Ramverk är kopplade till en Adobe Analytics-konfiguration. Du kan skapa flera ramverk för varje konfiguration.

När du associerar en webbsida med ett ramverk utför ramverket spårning för den sidan och de underordnade sidorna för den sidan. Sidvyer kan sedan hämtas från Adobe Analytics och visas i webbplatskonsolen.

## Förutsättningar {#prerequisites}

### Adobe Analytics-konto {#adobe-analytics-account}

Om du vill spåra AEM-data i Adobe Analytics måste du ha ett giltigt Adobe Marketing Cloud Adobe Analytics-konto.

Adobe Analytics-kontot behöver:

* Har **administratörsbehörighet**
* Anges till användargruppen **Webbtjänståtkomst** .

>[!CAUTION]
>
>Att ge **administratörsbehörighet** (i Adobe Analytics) räcker inte för att en användare ska kunna ansluta från AEM till Adobe Analytics. Kontot måste även ha **behörighet för webbtjänståtkomst** .

![chlimage_1-67](assets/chlimage_1-67.png)

Innan du fortsätter bör du kontrollera att dina autentiseringsuppgifter tillåter dig att logga in på Adobe Analytics. Via antingen:

* [https://marketing.adobe.com](https://marketing.adobe.com)

* [https://sc.omniture.com/login/](https://sc.omniture.com/login/)

### Konfigurera AEM för att använda dina Adobe Analytics-datacenter {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics- [datacenter](https://developer.omniture.com/en_US/content_page/concepts-terminology/c-how-is-data-stored) samlar in, bearbetar och lagrar data som är kopplade till din Adobe Analytics-rapportserie. Du måste konfigurera AEM så att det datacenter som är värd för din Adobe Analytics-rapportserie används. I följande tabell visas tillgängliga datacenter och deras URL.

| Datacenter | Webbadress |
|---|---|
| San Jose | https://api.omniture.com/admin/1.4/rest/ |
| Dallas | https://api2.omniture.com/admin/1.4/rest/ |
| London | https://api3.omniture.com/admin/1.4/rest/ |
| Singapore | https://api4.omniture.com/admin/1.4/rest/ |
| Oregon | https://api5.omniture.com/admin/1.4/rest/ |

AEM använder datacentret i San Jose (https://api.omniture.com/admin/1.4/rest/) som standard.

Använd [webbkonsolen för att konfigurera OSGi-paketet](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) med **Adobe AEM Analytics HTTP Client**. Lägg till **datacenter-URL** för det datacenter som är värd för en rapportsvit som dina AEM-sidor samlar in data för.

![aa-07](assets/aa-07.png)

1. Öppna webbkonsolen i webbläsaren. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Ange dina inloggningsuppgifter för att komma åt konsolen.

   >[!NOTE]
   >
   >Kontakta webbplatsadministratören för att ta reda på om du har tillgång till den här konsolen.

1. Markera konfigurationsobjektet **Adobe AEM Analytics HTTP Client**.
1. Om du vill lägga till URL:en för ett datacenter trycker du på plusknappen (+) bredvid listan med URL:er **för** datacenter och skriver URL:en i rutan.

1. Om du vill ta bort en URL-adress från listan klickar du på knappen - bredvid URL-adressen.
1. Klicka på Spara.

## Konfigurera anslutningen till Adobe Analytics {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>På grund av säkerhetsändringar i Adobe Analytics-API:t är det inte längre möjligt att använda den version av Activity Map som ingår i AEM.
>
>Det [ActivityMap-plugin som tillhandahålls av Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) bör nu användas.

## Konfigurera för aktivitetskartan {#configuring-for-the-activity-map}

>[!CAUTION]
>
>På grund av säkerhetsändringar i Adobe Analytics-API:t är det inte längre möjligt att använda den version av Activity Map som ingår i AEM.
>
>Det [ActivityMap-plugin som tillhandahålls av Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) bör nu användas.

## Skapa ett Adobe Analytics Framework {#creating-a-adobe-analytics-framework}

För det Report Suite-ID (RSID) som du använder kan du styra vilka serverinstanser (författare, publicera eller båda) som ska bidra med data till Report Suite:

* **Alla**: Information från både författaren och publiceringsinstansen fyller i Report Suite.
* **Författare**: Rapportsviten fylls bara i med information från författarinstansen.
* **Publicera**: Rapportsviten fylls bara i med information från publiceringsinstansen.

>[!NOTE]
>
>När du väljer typ av serverinstans begränsas inte anrop till Adobe Analytics, utan bara vilka anrop som innehåller RSID.
>
>Ett ramverk är till exempel konfigurerat för att använda *rapportsviten* diwernetail och författaren är den valda serverinstansen. När sidor publiceras tillsammans med ramverket anropas fortfarande Adobe Analytics, men dessa anrop innehåller inte RSID. Endast anrop från författarinstansen innehåller RSID.

1. Välj **Navigering**, **Verktyg**, **Molntjänster** och sedan **Äldre molntjänster**.
1. Bläddra till **Adobe Analytics** och klicka på **[+]** bredvid **Tillgängliga konfigurationer**.
1. Klicka på länken **[+]** bredvid din Adobe Analytics-konfiguration.

1. I dialogrutan **Skapa ramverk** :

   * Ange en **titel**.
   * Du kan också ange **Namn** för noden som lagrar ramverkets information i databasen.
   * Välj **Adobe Analytics Framework**
   Klicka på **Skapa**.

   Ramverket öppnas för redigering.

1. Klicka på **Lägg till objekt** i delen **Rapportsviter på sidopanelen (höger sida av huvudpanelen)**. Använd sedan listrutan för att välja det Report Suite-ID (till exempel `geometrixxauth`) som ramverket ska interagera med.

   >[!NOTE]
   >
   >Innehållssökaren till vänster fylls i med Adobe Analytics-variabler (SiteCatalyst-variabler) när du väljer ett Report Suite-ID.

1. Använd sedan listrutan **Körningsläge** (bredvid rapportsvitens ID) för att välja de serverinstanser som du vill skicka information till rapportsviten.

   ![aa-framework-01](assets/aa-framework-01.png)

1. Om du vill göra ramverket tillgängligt på publiceringsinstansen av webbplatsen klickar du på **Aktivera ramverk på fliken** Sida **i sidokicka.**

### Konfigurera serverinställningar för Adobe Analytics {#configuring-server-settings-for-adobe-analytics}

Med ramverkssystemet kan du ändra serverinställningarna i varje Adobe Analytics-ramverk.

>[!CAUTION]
>
>Dessa inställningar avgör var data skickas och hur, så det är viktigt att du *inte ändrar inställningarna* och låter Adobe Analytics-representanten konfigurera dem i stället.

Börja med att öppna panelen. Tryck på nedåtpilen bredvid **Servrar**:

![server_001](assets/server_001.png)

* **Spårningsserver**

   * innehåller den URL som används för att skicka Adobe Analytics-anrop

      * cname - används som standard för Adobe Analytics-kontots *företagsnamn*
      * d1 - motsvarar det datacenter som informationen skickas till (kan vara antingen d1, d2 eller d3)
      * sc.omtrdc.net - domännamn

* **Secure Tracking Server**

   * Har samma segment som spårningsservern
   * Detta används för att skicka data från säkra sidor (https://)

* **Namnutrymme för besökare**

   * Namnutrymmet bestämmer den första delen av spårnings-URL:en.
   * Om du t.ex. ändrar namnutrymmet till **CNAME** kommer de anrop som görs till Adobe Analytics att se ut som **CNAME.d1.omtrdc.net** i stället för som standard.

## Associera en sida med ett Adobe Analytics Framework {#associating-a-page-with-a-adobe-analytics-framework}

När en sida är kopplad till ett Adobe Analytics-ramverk skickar sidan data till Adobe Analytics när sidan läses in. Variabler som sidan fyller mappas och hämtas från Adobe Analytics-variabler i ramverket. Sidvyer hämtas till exempel från Adobe Analytics.

Underordnade till sidan ärver kopplingen till ramverket. Om du till exempel associerar platsens rotsida med ett ramverk, kopplas alla sidor på webbplatsen till ramverket.

1. På **webbplatskonsolen** väljer du den sida som du vill konfigurera med spårning.
1. Öppna **[Sidegenskaperna](/help/sites-authoring/editing-page-properties.md)**, antingen direkt från konsolen eller sidredigeraren.
1. Öppna fliken** Cloud Services**.

1. Använd listrutan **Lägg till konfiguration** för att välja **Adobe Analytics** bland de tillgängliga alternativen. Om arv är plats måste du inaktivera det innan väljaren blir tillgänglig.

1. Listrutan för **Adobe Analytics** läggs till i de tillgängliga alternativen. Använd detta för att välja den nödvändiga ramverkskonfigurationen.

1. Välj **Spara och stäng**.
1. **[Publicera](/help/sites-authoring/publishing-pages.md)**sidan för att aktivera sidan och eventuella anslutna konfigurationer/filer.
1. Det sista steget är att besöka sidan i publiceringsinstansen och söka efter ett nyckelord (t.ex. äggplank) med komponenten **Sök** .
1. Sedan kan du kolla samtalen till Adobe Analytics med ett lämpligt verktyg: till exempel [Adobe Marketing Cloud Debugger](https://marketing.adobe.com/resources/help/en_US/sc/implement/debugger_install.html).
1. I exemplet som anges ska anropet innehålla det värde som anges (dvs. eggplant) i eVar7 och händelselistan ska innehålla event3.

### Sidvyer {#page-views}

När en sida är kopplad till ett Adobe Analytics-ramverk kan antalet sidvisningar visas i listvyn i Sites-konsolen.

Mer information finns i [Se data](/help/sites-authoring/page-analytics-using.md) för sidanalys.

### Konfigurera importintervallet {#configuring-the-import-interval}

Konfigurera rätt instans av tjänsten **Adobe AEM Managed Polling Configuration** :

* **Avsökningsintervall**:
Intervallet, i sekunder, där tjänsten hämtar sidvisningsdata från Adobe Analytics.
Standardintervallet är 43200000 ms (12 timmar).

* **Aktivera**:
Aktivera eller inaktivera tjänsten. Som standard är tjänsten aktiverad.

Om du vill konfigurera den här OSGi-tjänsten kan du antingen använda [webbkonsolen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) eller en [osgiConfig-nod i databasen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (tjänstens PID är `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`).

## Redigera Adobe Analytics-konfigurationer och/eller -ramverk {#editing-adobe-analytics-configurations-and-or-frameworks}

Precis som när du skapar en konfiguration eller ett ramverk för Adobe Analytics går du till (äldre) **molntjänster** . Välj **Visa konfigurationer** och klicka sedan på länken till den specifika konfiguration som du vill uppdatera.

När du redigerar en Adobe Analytics-konfiguration måste du också trycka på knappen **Redigera** på konfigurationssidan för att kunna öppna dialogrutan **Redigera komponent** .

## Ta bort Adobe Analytics-ramverk {#deleting-adobe-analytics-frameworks}

Om du vill ta bort ett Adobe Analytics-ramverk [öppnar du det först för redigering](#editing-adobe-analytics-configurations-and-or-frameworks).

Välj sedan **Ta bort ramverk** på fliken **Sida** i sidosparken.

