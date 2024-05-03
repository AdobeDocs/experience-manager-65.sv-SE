---
title: "Självstudie: Skapa formulärdatamodell i AEM Forms"
description: Skapa formulärdatamodell för interaktiv kommunikation
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: c8a6037c-46bd-4058-8314-61cb925ba5a8
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2684'
ht-degree: 0%

---

# Självstudie: Skapa formulärdatamodell i AEM Forms{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Den här självstudiekursen är ett steg i [Skapa din första interaktiva kommunikation](/help/forms/using/create-your-first-interactive-communication.md) serie. Vi rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga självstudiekurserna.

## Om självstudiekursen {#about-the-tutorial}

Med dataintegreringsmodulen i AEM Forms kan du skapa en formulärdatamodell från olika backend-datakällor som AEM användarprofil, RESTful web services, SOAP-baserade webbtjänster, OData services och relationsdatabaser. Du kan konfigurera datamodellsobjekt och datatjänster i en formulärdatamodell och koppla den till ett anpassat formulär. Anpassningsbara formulärfält är bundna till objektegenskaper för datamodell. Med tjänsterna kan du förifylla det adaptiva formuläret och skriva skickade formulärdata tillbaka till datamodellobjektet.

Mer information om integration av formulärdata och formulärdatamodell finns i [AEM Forms dataintegrering](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

I den här självstudiekursen får du hjälp med att förbereda, skapa, konfigurera och koppla en formulärdatamodell till en interaktiv kommunikation. I slutet av den här självstudiekursen kan du:

* [Konfigurera databasen](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [Konfigurera MySQL-databasen som datakälla](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [Skapa formulärdatamodell](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [Konfigurera formulärdatamodell](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [Testa formulärdatamodell](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

Formulärdatamodellen ser ut ungefär så här:

![Formulärdatamodell](assets/form_data_model_callouts_new.png)

**S.** Konfigurerade datakällor **B.** Datakällscheman **C.** Tillgängliga tjänster **D.** Datamodellsobjekt **E.** Konfigurerade tjänster

## Förutsättningar {#prerequisites}

Kontrollera att du har följande innan du börjar:

* MySQL-databas med exempeldata som anges i [Konfigurera databasen](../../forms/using/create-form-data-model0.md#step-set-up-the-database) -avsnitt.
* OSGi-paket för MySQL JDBC-drivrutin enligt beskrivningen i [Paketera JDBC-databasdrivrutinen](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)

## Steg 1: Konfigurera databasen {#step-set-up-the-database}

En databas är nödvändig för att skapa en interaktiv kommunikation. I den här självstudiekursen används en databas för att visa formulärdatamodellens och beständighetsfunktionerna i interaktiv kommunikation. Konfigurera en databas som innehåller kundregister, räkningar och samtalstabeller.
Följande bild visar exempeldata för kundtabellen:

![sample_data_cust](assets/sample_data_cust.png)

Använd följande DDL-sats för att skapa **kund** tabellen i databasen.

```sql
CREATE TABLE `customer` (
   `mobilenum` int(11) NOT NULL,
   `name` varchar(45) NOT NULL,
   `address` varchar(45) NOT NULL,
   `alternatemobilenumber` int(11) DEFAULT NULL,
   `relationshipnumber` int(11) DEFAULT NULL,
   `customerplan` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`mobilenum`),
   UNIQUE KEY `mobilenum_UNIQUE` (`mobilenum`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

Använd följande DDL-sats för att skapa **växlar** tabellen i databasen.

```sql
CREATE TABLE `bills` (
   `billplan` varchar(45) NOT NULL,
   `latepayment` decimal(4,2) NOT NULL,
   `monthlycharges` decimal(4,2) NOT NULL,
   `billdate` date NOT NULL,
   `billperiod` varchar(45) NOT NULL,
   `prevbal` decimal(4,2) NOT NULL,
   `callcharges` decimal(4,2) NOT NULL,
   `confcallcharges` decimal(4,2) NOT NULL,
   `smscharges` decimal(4,2) NOT NULL,
   `internetcharges` decimal(4,2) NOT NULL,
   `roamingnational` decimal(4,2) NOT NULL,
   `roamingintnl` decimal(4,2) NOT NULL,
   `vas` decimal(4,2) NOT NULL,
   `discounts` decimal(4,2) NOT NULL,
   `tax` decimal(4,2) NOT NULL,
   PRIMARY KEY (`billplan`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

Använd följande DDL-sats för att skapa **samtal** tabellen i databasen.

```sql
CREATE TABLE `calls` (
   `mobilenum` int(11) DEFAULT NULL,
   `calldate` date DEFAULT NULL,
   `calltime` varchar(45) DEFAULT NULL,
   `callnumber` int(11) DEFAULT NULL,
   `callduration` varchar(45) DEFAULT NULL,
   `callcharges` decimal(4,2) DEFAULT NULL,
   `calltype` varchar(45) DEFAULT NULL
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

The **samtal** tabellen innehåller samtalsinformation som samtalsdatum, samtalstid, samtalsnummer, samtalslängd och samtalsavgifter. The **kund** tabellen är länkad till anropstabellen med hjälp av fältet Mobilnummer (mobiltelefonnummer). För varje mobilnummer som visas i **kund** tabellen, det finns flera poster i **samtal** tabell. Du kan till exempel hämta samtalsinformationen för **1457892541** mobilnummer genom att referera till **samtal** tabell.

The **växlar** tabellen innehåller fakturainformation som faktureringsdatum, faktureringsperiod, månadsavgifter och samtalsavgifter. The **kund** tabellen är länkad till **växlar** tabellen med hjälp av faktureringsplanfältet. Det finns en plan för varje kund i **kund** tabell. The **växlar** tabellen innehåller prisuppgifter för alla befintliga planer. Du kan till exempel hämta avtalsinformation för **Sarah** från **kund** tabellen och använd dessa detaljer för att hämta prisinformation från **växlar** tabell.

## Steg 2: Konfigurera MySQL-databasen som datakälla {#step-configure-mysql-database-as-data-source}

Du kan konfigurera olika typer av datakällor för att skapa en formulärdatamodell. I den här självstudiekursen konfigurerar du MySQL-databasen som är konfigurerad och ifylld med exempeldata. Mer information om andra datakällor som stöds och hur du konfigurerar dem finns i [AEM Forms dataintegrering](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

Gör följande för att konfigurera MySQL-databasen:

1. Installera JDBC-drivrutin för MySQL-databas som ett OSGi-paket:

   1. Logga in på AEM Forms Author Instance som administratör och gå till AEM webbkonsolpaket. Standardwebbadressen är [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).
   1. Välj **Installera/uppdatera**. An **Ladda upp/installera programpaket** visas.

   1. Välj **Välj fil** för att bläddra och välja paketet MySQL JDBC driver OSGi. Välj **Startpaket** och **Uppdatera paket** och markera **Installera** eller **Uppdatera**. Kontrollera att Oraclets JDBC-drivrutin för MySQL är aktiv. Drivrutinen är installerad.

1. Konfigurera MySQL-databasen som en datakälla:

   1. Gå till AEM webbkonsol på [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Sök **Poolad datakälla för Apache Sling-anslutning** konfiguration. Välj det här alternativet om du vill öppna konfigurationen i redigeringsläge.
   1. Ange följande information i konfigurationsdialogrutan:

      * **Datakällans namn:** Du kan ange vilket namn som helst. Ange till exempel **MySQL**.

      * **Egenskapsnamn för DataSource-tjänst**: Ange namnet på den tjänsteegenskap som innehåller namnet på datakällan. Den anges när datakällinstansen registreras som OSGi-tjänst. Till exempel: **datakälla.namn**.

      * **JDBC-drivrutinsklass**: Ange Java-klassnamnet för JDBC-drivrutinen. För MySQL-databas anger du **com.mysql.jdbc.Driver**.

      * **URI för JDBC-anslutning**: Ange anslutnings-URL för databasen. För MySQL-databaser som körs på port 3306 och schematabell är URL:en: `jdbc:mysql://'server':3306/teleca?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **Användarnamn:** Användarnamn för databasen. Det krävs för att JDBC-drivrutinen ska kunna upprätta en anslutning till databasen.
      * **Lösenord:** Lösenord för databasen. Det krävs för att JDBC-drivrutinen ska kunna upprätta en anslutning till databasen.
      * **Test on Borgo:** Aktivera **Testa om Borgen** alternativ.

      * **Test vid retur:** Aktivera **Test vid retur** alternativ.

      * **Valideringsfråga:** Ange en SELECT-fråga (SQL) för att validera anslutningar från poolen. Frågan måste returnera minst en rad. Till exempel: **välj &#42; från kund**.

      * **Transaktionsisolering**: Ange värdet till **READ_COMMTED**.

   Lämna övriga egenskaper som standard [values](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) och markera **Spara**.

   En konfiguration som liknar följande skapas.

   ![Apache-konfiguration](assets/apache_configuration_new.png)

## Steg 3: Skapa formulärdatamodell {#step-create-form-data-model}

AEM Forms har ett intuitivt användargränssnitt för [skapa ett formulärdataläge](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)l från konfigurerade datakällor. Du kan använda flera datakällor i en formulärdatamodell. I den här självstudiekursen använder du MySQL som datakälla.

Gör följande för att skapa formulärdatamodell:

1. I AEM författarinstans går du till **Forms** > **Dataintegrering**.
1. Välj **Skapa** > **Formulärdatamodell**.
1. I guiden Skapa formulärdatamodell anger du **name** för formulärdatamodellen. Till exempel: **FDM_Create_First_IC**. Välj **Nästa**.
1. På skärmen Välj datakälla visas alla konfigurerade datakällor. Välj **MySQL** datakälla och markera **Skapa**.

   ![MYSQL-datakälla](assets/fdm_mysql_data_source_new.png)

1. Klicka **Klar**. The **FDM_Create_First_IC** formulärdatamodellen skapas.

## Steg 4: Konfigurera formulärdatamodell {#step-configure-form-data-model}

I konfigurationen av formulärdatamodellen ingår:

* [lägga till datamodellsobjekt och -tjänster](#add-data-model-objects-and-services)
* [skapa beräknade underordnade egenskaper för datamodellobjekt](#create-computed-child-properties-for-data-model-object)
* [lägga till associationer mellan datamodellobjekt](#add-associations-between-data-model-objects)
* [redigera objektegenskaper för datamodell](#edit-data-model-object-properties)
* [konfigurera tjänster för datamodellobjekt](#configure-services)

### Lägga till datamodellsobjekt och -tjänster {#add-data-model-objects-and-services}

1. Navigera AEM författarinstansen till **Forms** > **Dataintegrering**. Standardwebbadressen är [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. The **FDM_Create_First_IC** formulärdatamodellen som du skapade tidigare visas här. Markera den och markera **Redigera**.

   Den valda datakällan **MySQL** visas i **Datakällor** fönster.

   ![MYSQL-datakälla för FDM](assets/mysql_fdm_new.png)

1. Expandera **MySQL** datakällträd. Välj följande datamodellsobjekt och -tjänster från **teleca** schema:

   * **Datamodellsobjekt**:

      * växlar
      * samtal
      * kund

   * **Tjänster:**

      * get
      * uppdatera

   Välj **Lägg till markerade** om du vill lägga till markerade datamodellsobjekt och tjänster i formulärdatamodellen.

   ![Markera datamodellsobjektstjänster](assets/select_data_model_object_services_new.png)

   Modellobjekt för räkningar, samtal och kunddata visas i den högra rutan i **Modell** -fliken. Tjänsterna get och update visas i **Tjänster** -fliken.

   ![Datamodellsobjekt](assets/data_model_objects_new.png)

### Skapa beräknade underordnade egenskaper för datamodellobjekt {#create-computed-child-properties-for-data-model-object}

En beräknad egenskap är den vars värde beräknas baserat på en regel eller ett uttryck. Med hjälp av en regel kan du ange värdet för en beräknad egenskap till en litteral sträng, ett tal, resultatet av ett matematiskt uttryck eller värdet för en annan egenskap i formulärdatamodellen.

Baserat på användningsfallet skapar du **usagecharges** underordnad beräknad egenskap i **växlar** datamodellsobjekt med följande matematiska uttryck:

* Användningsavgifter = samtalsavgifter + konferenssamtalsavgifter + SMS-avgifter + mobilinternetavgifter + roaming nationellt + roaming internationellt + VAS (alla dessa egenskaper finns i räkningens datamodell) Mer information om **usagecharges** underordnad beräknad egenskap, se [Planera interaktiv kommunikation](/help/forms/using/planning-interactive-communications.md).

Utför följande steg för att skapa beräknade underordnade egenskaper för datamodellobjektet för räkningar:

1. Markera kryssrutan högst upp i **växlar** datamodellsobjekt för att markera det och markera **Skapa underordnad egenskap**.
1. I **Skapa underordnad egenskap** ruta:

   1. Retur **usagecharges** som namnet på den underordnade egenskapen.
   1. Aktivera **Beräknad**.
   1. Välj **Float** som typ och välj **Klar** för att lägga till den underordnade egenskapen i **växlar** datamodellsobjekt.

   ![Skapa underordnad egenskap](assets/create_child_property_new.png)

1. Välj **Redigera regel** för att öppna regelredigeraren.
1. Välj **Skapa**. The **Ange värde** regelfönstret öppnas.
1. Välj i listrutan Välj alternativ **Matematiskt uttryck**.

   ![Regelredigerare för användningsavgifter](assets/usage_charges_rule_editor_new.png)

1. I det matematiska uttrycket väljer du **callCharts** och **sammandragande** som första respektive andra objekt. Välj **plus** som -operatorn. Markera i det matematiska uttrycket och välj **Utöka uttryck** att lägga till **smscharges**, **internetavgifter**, **roamingnationell**, **roamingInl** och **arbetsyta** -objekt till uttrycket.

   Följande bild visar det matematiska uttrycket i regelredigeraren:

   ![Användningsavgiftsregel](assets/usage_charges_rule_all_new.png)

1. Välj **Klar**. Regeln skapas i regelredigeraren.
1. Välj **Stäng** för att stänga fönstret Regelredigerare.

### Lägga till associationer mellan datamodellsobjekt {#add-associations-between-data-model-objects}

När datamodellsobjekten har definierats kan du skapa associationer mellan dem. Associationen kan vara en-till-en eller en-till-många. Det kan till exempel finnas flera beroenden som är kopplade till en medarbetare. Den kallas en-till-många-association och avbildas med 1:n på linjen som förbinder associerade datamodellsobjekt. Om en association returnerar ett unikt medarbetarnamn för ett givet medarbetar-ID kallas den en-till-en-association.

När du lägger till associerade datamodellobjekt i en datakälla i en formulärdatamodell behålls deras associationer och visas som kopplade med pilrader.

Baserat på användningsfallet skapar du följande associationer mellan datamodellsobjekten:

| Association | Datamodellsobjekt |
|---|---|
| 1:n | kund:samtal (flera samtal kan kopplas till en kund i en månadsfaktura) |
| 1:1 | kund:växlar (en faktura är kopplad till en kund för en viss månad) |

Utför följande steg för att skapa associationer mellan datamodellsobjekt:

1. Markera kryssrutan högst upp i **kund** datamodellsobjekt för att markera det och markera **Lägg till association**. The **Lägg till association** egenskapspanelen öppnas.
1. I **Lägg till association** ruta:

   * Ange en titel för associationen. Det är ett valfritt fält.
   * Välj **En till många** från **Typ** listruta.

   * Välj **samtal** från **Modellobjekt** listruta.

   * Välj **get** från **Tjänst** listruta.

   * Välj **Lägg till** för att länka **kund** datamodellobjekt till **samtal** datamodellsobjekt som använder en egenskap. Baserat på användningsfallet måste anropsdatamodellsobjektet länkas till mobilnummeregenskapen i kunddatamodellsobjektet. The **Lägg till argument** öppnas.

   ![Lägg till association](assets/add_association_new.png)

1. I **Lägg till argument** dialogruta:

   * Välj **mobilenum** från **Namn** listruta. Egenskapen för mobilnummer är en vanlig egenskap som är tillgänglig i kunden och anropar datamodellsobjekt. Det innebär att det används för att skapa en association mellan kund- och anropsdatamodellsobjekt.
För varje mobilnummer som är tillgängligt i kunddatamodellobjektet finns det flera samtalsposter tillgängliga i samtalstabellen.

   * Ange en valfri titel och beskrivning för argumentet.
   * Välj **kund** från **Bindning till** listruta.

   * Välj **mobilenum** från **Bindningsvärde** listruta.

   * Välj **Lägg till**.

   ![Lägg till association för ett argument](assets/add_association_argument_new.png)

   Mobenum-egenskapen visas i **Argument** -avsnitt.

   ![Lägg till argumentassociation](assets/add_argument_association_new.png)

1. Välj **Klar** för att skapa en 1:n-association mellan kund och anropar datamodellsobjekt.

   När du har skapat en association mellan kund- och anropsdatamodellsobjekt skapar du en 1:1-association mellan kunden och faktureringsdatamodellsobjekten.

1. Markera kryssrutan högst upp i **kund** datamodellsobjekt för att markera det och markera **Lägg till association**. The **Lägg till association** egenskapspanelen öppnas.
1. I **Lägg till association** ruta:

   * Ange en titel för associationen. Det är ett valfritt fält.
   * Välj **En till en** från **Typ** listruta.

   * Välj **växlar** från **Modellobjekt** listruta.

   * Välj **get** från **Tjänst** listruta. The **faktureringsplan** egenskapen, som är primärnyckeln för räkningstabellen, är redan tillgänglig i **Argument** -avsnitt.
Fakturorna och modellobjekten för kunddata länkas med egenskaperna för faktureringsplanen (räkningarna) respektive kundplanen (kunden). Skapa en bindning mellan de här egenskaperna för att hämta avtalsinformationen för alla kunder som är tillgängliga i MySQL-databasen.

   * Välj **kund** från **Bindning till** listruta.

   * Välj **kundplan** från **Bindningsvärde** listruta.

   * Välj **Klar** för att skapa en bindning mellan egenskaperna för faktureringsplanen och kundplanen.

   ![Lägg till association för kundfaktura](assets/add_association_customer_bills_new.png)

   I följande bild visas associationerna mellan datamodellsobjekten och egenskaperna som används för att skapa associationer mellan dem:

   ![fdm_association](assets/fdm_associations.gif)

### Redigera objektegenskaper för datamodell {#edit-data-model-object-properties}

När du har skapat associationer mellan kunden och andra datamodellsobjekt kan du redigera kundegenskaperna för att definiera den egenskap som data hämtas från datamodellsobjektet. Baserat på användningsfallet används mobilnummer som egenskap för att hämta data från kunddatamodellsobjektet.

1. Markera kryssrutan högst upp i **kund** datamodellsobjekt för att markera det och markera **Redigera egenskaper**. The **Redigera egenskaper** öppnas.
1. Ange **kund** som **Modellobjekt på översta nivån**.
1. Välj **get** från **Läs tjänsten** listruta.
1. I **Argument** avsnitt:

   * Välj **Begär attribut** från **Bindning till** listruta.

   * Ange **mobilenum** som bindningsvärde.

1. Välj **uppdatera** från **Skriv** Listruta för tjänst.
1. I **Argument** avsnitt:

   * För **mobilenum** egenskap, välj **kund** från **Bindning till** listruta.

   * Välj **mobilenum** från **Bindningsvärde** listruta.

1. Välj **Klar** för att spara egenskaperna.

   ![Konfigurera tjänster](assets/configure_services_customer_new.png)

1. Markera kryssrutan högst upp i **samtal** datamodellsobjekt för att markera det och markera **Redigera egenskaper**. The **Redigera egenskaper** öppnas.
1. Inaktivera **Modellobjekt på översta nivån** for **samtal** datamodellsobjekt.
1. Välj **Klar**.

   Upprepa steg 8-10 för att konfigurera egenskaperna för **växlar** datamodellsobjekt.

### Konfigurera tjänster {#configure-services}

1. Gå till **Tjänster** -fliken.
1. Välj **get** service och välj **Redigera egenskaper**. The **Redigera egenskaper** öppnas.
1. I **Redigera egenskaper** ruta:

   * Ange en valfri titel och beskrivning.
   * Välj **kund** från **Objekt för utdatamodell** listruta.

   * Välj **Klar** för att spara egenskaperna.

   ![Redigera egenskaper](assets/edit_properties_get_details_new.png)

1. Välj **uppdatera** service och välj **Redigera egenskaper**. The **Redigera egenskaper** öppnas.
1. I **Redigera egenskaper** ruta:

   * Ange en valfri titel och beskrivning.
   * Välj **kund** från **Indatamodellsobjekt** listruta.

   * Välj **Klar**.
   * Välj **Spara** för att spara formulärdatamodellen.

   ![Uppdatera tjänstegenskaper](assets/update_service_properties_new.png)

## Steg 5: Testa formulärdatamodell och -tjänster {#step-test-form-data-model-and-services}

Du kan testa datamodellsobjektet och datatjänsterna för att verifiera att formulärdatamodellen är korrekt konfigurerad.

Gör följande för att köra testet:

1. Gå till **Modell** väljer du **kund** datamodellsobjekt, och markera **Testmodellobjekt**.
1. I **Testa formulärdatamodell** fönster, markera **Läs modellobjekt** från **Välj modell/tjänst** listruta.
1. I **Indata** anger du ett värde för **mobilenum** som finns i den konfigurerade MySQL-databasen och väljer **Testa**.

   Kundinformationen som är associerad med den angivna mobilegenskapen hämtas och visas i utdataavsnittet enligt nedan. Stäng dialogrutan.

   ![Testa datamodell](assets/test_data_model_new.png)

1. Gå till **Tjänster** -fliken.
1. Välj **get** service och välj **Testtjänst.**
1. I **Indata** anger du ett värde för **mobilenum** som finns i den konfigurerade MySQL-databasen och väljer **Testa**.

   Kundinformationen som är associerad med den angivna mobilegenskapen hämtas och visas i utdataavsnittet enligt nedan. Stäng dialogrutan.

   ![Testtjänst](assets/test_service_new.png)

### Redigera och spara exempeldata {#edit-and-save-sample-data}

Med formulärdatamodellredigeraren kan du generera exempeldata för alla datamodellsobjektsegenskaper, inklusive beräknade egenskaper, i en formulärdatamodell. Det är en uppsättning slumpmässiga värden som överensstämmer med den datatyp som konfigurerats för varje egenskap. Du kan också redigera och spara data, som behålls även om du genererar om exempeldata.

Gör följande för att generera, redigera och spara exempeldata:

1. På formulärdatamodellsidan väljer du **Redigera exempeldata**. Den genererar och visar exempeldata i fönstret Redigera exempeldata.

   ![Redigera exempeldata](assets/edit_sample_data_new.png)

1. I **Redigera exempeldata** fönster, redigera data efter behov och markera **Spara**. Stäng fönstret.
