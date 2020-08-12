---
title: '"Självstudiekurs: Skapa formulärdatamodell "'
seo-title: Skapa formulärdatamodell, genomgång
description: Skapa formulärdatamodell
seo-description: Skapa formulärdatamodell
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
translation-type: tm+mt
source-git-commit: 78768e6eab65f452421d8809384500c6eab6b97f
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 1%

---


# Självstudiekurs: Skapa formulärdatamodell {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Den här självstudiekursen är ett steg i serien [Create Your First Adaptive Form](../../forms/using/create-your-first-adaptive-form.md) . Vi rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga exemplet på självstudiekurser.

## Om självstudiekursen {#about-the-tutorial}

Med AEM [!DNL Forms] dataintegreringsmodul kan du skapa en formulärdatamodell från olika backend-datakällor som AEM användarprofil, RESTful web services, SOAP-baserade webbtjänster, OData services och relationsdatabaser. Du kan konfigurera datamodellsobjekt och datatjänster i en formulärdatamodell och koppla den till ett anpassat formulär. Anpassningsbara formulärfält är bundna till objektegenskaper för datamodell. Med tjänsterna kan du förifylla det adaptiva formuläret och skriva skickade formulärdata tillbaka till datamodellobjektet.

Mer information om integrering av formulärdata och formulärdatamodell finns i [AEM Forms-dataintegrering](../../forms/using/data-integration.md).

I den här självstudiekursen får du hjälp med att förbereda, skapa, konfigurera och associera en formulärdatamodell med ett adaptivt formulär. I slutet av den här självstudiekursen kan du:

* [Konfigurera MySQL-databasen som datakälla](#config-database)
* [Skapa formulärdatamodell med MySQL-databas](#create-fdm)
* [Konfigurera formulärdatamodell](#config-fdm)
* [Testa formulärdatamodell](#test-fdm)

Formulärdatamodellen ser ut ungefär så här:

![form-data-model_l](assets/form-data-model_l.png)

**S.** Konfigurerade datakällor **B.** Datakällscheman **C.** Tillgängliga tjänster **D.** Datamodellsobjekt **E.** Konfigurerade tjänster

## Förutsättningar {#prerequisites}

Kontrollera att du har följande innan du börjar:

* [!DNL MySQL] databas med exempeldata enligt avsnittet Krav i [Skapa ditt första adaptiva formulär](../../forms/using/create-your-first-adaptive-form.md)
* OSGi-paket för [!DNL MySQL] JDBC-drivrutin enligt beskrivningen i [Paketera JDBC-databasdrivrutinen](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Adaptiv form enligt den första självstudiekursen [Skapa ett adaptivt formulär](/help/forms/using/create-adaptive-form.md)

## Steg 1: Konfigurera MySQL-databasen som datakälla {#config-database}

Du kan konfigurera olika typer av datakällor för att skapa en formulärdatamodell. I den här självstudiekursen konfigurerar vi MySQL-databasen som du har konfigurerat och fyllt i med exempeldata. Information om andra datakällor som stöds och hur du konfigurerar dem finns i [AEM Forms-dataintegrering](../../forms/using/data-integration.md).

Gör följande för att konfigurera din [!DNL MySQL] databas:

1. Installera JDBC-drivrutin för [!DNL MySQL] databasen som ett OSGi-paket:

   1. Logga in på AEM [!DNL Forms] Author Instance som administratör och gå till AEM webbkonsolpaket. Standardwebbadressen är [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Tryck på **[!UICONTROL Install/Update]**. En [!UICONTROL Upload / Install Bundles] dialogruta visas.

   1. Tryck för **[!UICONTROL Choose File]** att bläddra och välja OSGi-paketet för [!DNL MySQL] JDBC-drivrutinen. Markera **[!UICONTROL Start Bundle]** och **[!UICONTROL Refresh Packages]** tryck **[!UICONTROL Install or Update]**. Kontrollera att [!DNL Oracle Corporation's] JDBC-drivrutinen för [!DNL MySQL] är aktiv. Drivrutinen är installerad.

1. Konfigurera [!DNL MySQL] databasen som en datakälla:

   1. Gå till AEM webbkonsol på [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Leta reda på konfigurationen **för poolad DataSource** för Apache Sling-anslutningen. Tryck för att öppna konfigurationen i redigeringsläge.
   1. Ange följande information i konfigurationsdialogrutan:

      * **Datakällans namn:** Du kan ange vilket namn som helst. Ange till exempel **WeRetailMySQL**.
      * **Egenskapsnamn** för DataSource-tjänst: Ange namnet på den tjänsteegenskap som innehåller DataSource-namnet. Den anges när datakällinstansen registreras som OSGi-tjänst. Exempel: **datasource.name**.
      * **JDBC-drivrutinsklass**: Ange Java-klassnamnet för JDBC-drivrutinen. För [!DNL MySQL] databas anger du **com.mysql.jdbc.Driver**.
      * **JDBC-anslutnings-URI**: Ange anslutnings-URL för databasen. För [!DNL MySQL] databaser som körs på port 3306 och schema är URL:en: `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **Användarnamn:** Användarnamn för databasen. Det krävs för att JDBC-drivrutinen ska kunna upprätta en anslutning till databasen.
      * **Lösenord:** Lösenord för databasen. Det krävs för att JDBC-drivrutinen ska kunna upprätta en anslutning till databasen.
      * **Test on Borgo:** Aktivera **[!UICONTROL Test on Borrow]** alternativet.
      * **Test vid retur:** Aktivera **[!UICONTROL Test on Return]** alternativet.
      * **Valideringsfråga:** Ange en SELECT-fråga (SQL) för att validera anslutningar från poolen. Frågan måste returnera minst en rad. Du kan till exempel **välja * från kundinformation**.
      * **Transaktionsisolering**: Ange värdet **READ_COMMTED**.

         Lämna övriga egenskaper med standardvärden [](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) och tryck **[!UICONTROL Save]**.

         En konfiguration som liknar följande skapas.

         ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## Steg 2: Skapa formulärdatamodell {#create-fdm}

AEM [!DNL Forms] har ett intuitivt användargränssnitt för att [skapa en formulärdatamodell](data-integration.md) från konfigurerade datakällor. Du kan använda flera datakällor i en formulärdatamodell. Vi kommer att använda den konfigurerade [!DNL MySQL] datakällan.

Gör följande för att skapa formulärdatamodell:

1. I AEM författarinstans går du till **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**.
1. Tryck på **[!UICONTROL Create]** > **[!UICONTROL Form Data Model]**.
1. I dialogrutan Skapa formulärdatamodell anger du ett **namn** för formulärdatamodellen. Exempel: **kundleveransfaktureringsuppgifter**. Tryck på **[!UICONTROL Next]**.
1. På skärmen Välj datakälla visas alla konfigurerade datakällor. Välj **Datakällan WeRetailMySQL** och tryck **[!UICONTROL Create]**.

   ![datakälla-markering](assets/data-source-selection.png)

Formulärdatamodellen för **kundleveransfaktureringsinformation** skapas.

## Steg 3: Konfigurera formulärdatamodell {#config-fdm}

I konfigurationen av formulärdatamodellen ingår:

* lägga till datamodellobjekt och datatjänster
* konfigurera läs- och skrivtjänster för datamodellobjekt

Gör följande för att konfigurera formulärdatamodellen:

1. Navigera AEM författarinstansen till **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**. Standardwebbadressen är [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. Den **formulärdatamodell som du skapade för kundleveransfakturering** listas här. Öppna den i redigeringsläge.

   Den valda datakällan **WeRetailMySQL** har konfigurerats i formulärdatamodellen.

   ![default-fdm](assets/default-fdm.png)

1. Expandera trädet för datakällan WeRailMySQL. Välj följande datamodellsobjekt och datatjänster från **Nere** > schema med **kundinformation** till formulärdatamodell:

   * **Datamodellsobjekt**:

      * id
      * name
      * shippingAddress
      * stad
      * läge
      * zipcode
   * **Tjänster:**

      * get
      * update

   Tryck på **Lägg till markerade** för att lägga till markerade datamodellsobjekt och tjänster i formulärdatamodellen.

   ![WeRetail Schema](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >Standardtjänsterna för hämtning, uppdatering och infogning av JDBC-datakällor levereras med formulärdatamodell direkt.

1. Konfigurera läs- och skrivtjänster för datamodellobjektet.

   1. Markera datamodellobjektet **kundinformation** och tryck på **[!UICONTROL Edit Properties]**.
   1. Välj **[!UICONTROL get]** i listrutan Lästjänst. Argumentet **id** , som är primärnyckeln i datamodellobjektet för kundinformation, läggs till automatiskt. Tryck på ![aem_6_3_edit](assets/aem_6_3_edit.png) och konfigurera argumentet enligt följande.

      ![read-default](assets/read-default.png)

   1. Välj på liknande sätt **[!UICONTROL update]** som skrivtjänst. Objektet **kundinformation** läggs automatiskt till som argument. Argumentet är konfigurerat enligt följande.

      ![write-default](assets/write-default.png)

      Lägg till och konfigurera argumentet **id** enligt följande.

      ![id-arg](assets/id-arg.png)

   1. Tryck **[!UICONTROL Done]** för att spara datamodellens objektegenskaper. Tryck sedan på **[!UICONTROL Save]** för att spara formulärdatamodellen.

      Tjänsterna **[!UICONTROL get]** och **[!UICONTROL update]** läggs till som standardtjänster för datamodellobjektet.

      ![data-model-object](assets/data-model-object.png)

1. Gå till **[!UICONTROL Services]** fliken och konfigurera **[!UICONTROL get]** och **[!UICONTROL update]** tjänster.

   1. Markera **[!UICONTROL get]** tjänsten och tryck på **[!UICONTROL Edit Properties]**. Dialogrutan Egenskaper öppnas.
   1. Ange följande i dialogrutan Redigera egenskaper:

      * **Titel**: Ange tjänstens titel. Till exempel: Hämta leveransadress.
      * **Beskrivning**: Ange en beskrivning som innehåller detaljerad funktionalitet för tjänsten. Till exempel:

         Den här tjänsten hämtar leveransadress och annan kundinformation från [!DNL MySQL] databasen

      * **Objekt** för utdatamodell: Välj schema som innehåller kunddata. Till exempel:

         kundinformationsschema

      * **Returmatris**: Inaktivera alternativet **Retur-array** .
      * **Argument**: Välj argument med namnet **ID**.

      Tryck på **[!UICONTROL Done]**. Tjänsten för att hämta kundinformation från MySQL-databasen har konfigurerats.

      ![shiiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. Markera **[!UICONTROL update]** tjänsten och tryck på **[!UICONTROL Edit Properties]**. Dialogrutan Egenskaper öppnas.

   1. Ange följande i [!UICONTROL Edit Properties] dialogrutan:

      * **Titel**: Ange tjänstens titel. Exempel: Uppdatera leveransadress.
      * **Beskrivning**: Ange en beskrivning som innehåller detaljerad funktionalitet för tjänsten. Till exempel:

         Den här tjänsten uppdaterar leveransadress och relaterade fält i MySQL-databasen

      * **Indatamodellsobjekt**: Välj schema som innehåller kunddata. Till exempel:

         kundinformationsschema

      * **Utdatatyp**: Välj **BOOLEAN**.

      * **Argument**: Välj argument med namnet **ID** och **kundinformation**.
      Tryck på **[!UICONTROL Done]**. Tjänsten **[!UICONTROL update]** för att uppdatera kundinformation i [!DNL MySQL] databasen har konfigurerats.

      ![leveransadress-uppdatering](assets/shiiping-address-update.png)



Datamodellsobjektet och -tjänsterna i formulärdatamodellen har konfigurerats. Nu kan du testa formulärdatamodellen.

## Steg 4: Testa formulärdatamodell {#test-fdm}

Du kan testa datamodellsobjektet och datatjänsterna för att verifiera att formulärdatamodellen är korrekt konfigurerad.

Gör följande för att köra testet:

1. Gå till **[!UICONTROL Model]** fliken, markera datamodellobjektet **kundinformation** och tryck på **[!UICONTROL Test Model Object]**.
1. I [!UICONTROL Test Model/Service] fönstret väljer du **[!UICONTROL Read model object]** i **[!UICONTROL Select Model/Service]** listrutan.
1. I avsnittet **kundinformation** anger du ett värde för **id** -argumentet som finns i den konfigurerade [!DNL MySQL] databasen och trycker på **[!UICONTROL Test]**.

   Kundinformationen som är kopplad till det angivna ID:t hämtas och visas i **[!UICONTROL Output]** avsnittet enligt nedan.

   ![test-read-model](assets/test-read-model.png)

1. På samma sätt kan du testa Write-modellobjektet och tjänsterna.

   I följande exempel uppdaterar uppdateringstjänsten adressinformationen för ID 7102715 i databasen.

   ![test-write-model](assets/test-write-model.png)

   Om du testar läsmodelltjänsten igen för ID 7107215 hämtas och visas den uppdaterade kundinformationen enligt nedan.

   ![läsuppdaterad](assets/read-updated.png)
