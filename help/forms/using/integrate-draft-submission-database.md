---
title: Exempel för att integrera komponent för utkast och inlämning med databas
seo-title: Sample for integrating drafts & submissions component with database
description: Referera till implementering av anpassade data- och metadatatjänster för att integrera komponenter för utkast och inlämning i en databas.
seo-description: Reference implementation of customized data and metadata services to integrate drafts and submissions component with a database.
uuid: ccdb900e-2c2e-4ed3-8a88-5c97aa0092a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: da96d3d8-a338-470a-8d20-55ea39bd15bf
exl-id: 2e4f8f51-df02-4bbb-99bb-30181facd1e0
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# Exempel för att integrera komponent för utkast och inlämning med databas {#sample-for-integrating-drafts-submissions-component-with-database}

## Exempelöversikt {#sample-overview}

Med AEM Forms portalutkast och skicka-komponenter kan användarna spara sina formulär som utkast och skicka dem senare från vilken enhet som helst. Användarna kan även se de inskickade formulären på portalen. För att aktivera den här funktionen tillhandahåller AEM Forms data- och metadatatjänster för att lagra data som fyllts i av en användare i formuläret och de formulärmetadata som är kopplade till utkast och skickade formulär. Dessa data lagras som standard i CRX-databasen. När användarna interagerar med blanketterna via AEM publiceringsinstans, som vanligtvis ligger utanför företagets brandvägg, kan det vara bra att anpassa datalagringen så att den blir säkrare och tillförlitligare.

Exemplet, som behandlas i det här dokumentet, är en referensimplementering av anpassade data- och metadatatjänster för att integrera komponenter för utkast och inskickning med en databas. Databasen som används i exempelimplementeringen är **MySQL 5.6.24**. Du kan emellertid integrera komponenterna för utkast och inskickning med valfri databas.

>[!NOTE]
>
>* De exempel och konfigurationer som beskrivs i det här dokumentet är enligt MySQL 5.6.24 och du måste ersätta dem på lämpligt sätt för ditt databassystem.
>* Kontrollera att du har installerat den senaste versionen av AEM Forms tilläggspaket. En lista över tillgängliga paket finns i [AEM Forms](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) artikel.
>* Exempelpaketet fungerar bara med adaptiva Forms-sändningsåtgärder.


## Konfigurera och konfigurera exemplet {#set-up-and-configure-the-sample}

Utför följande steg på alla författare- och publiceringsinstanser för att installera och konfigurera exemplet:

1. Hämta följande **aem-fp-db-integration-sample-pkg-6.1.2.zip** till filsystemet.

   Exempelpaket för databasintegrering

[Hämta fil](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Gå till AEM på https://[*värd*]:[*port*]/crx/packmgr/.
1. Klicka på **[!UICONTROL Upload Package]**.

1. Bläddra för att välja **aem-fp-db-integration-sample-pkg-6.1.2.zip** paketera och klicka på **[!UICONTROL OK]**.
1. Klicka **[!UICONTROL Install]** till bredvid paketet för att installera paketet.
1. Gå till **[!UICONTROL AEM Web Console Configuration]**
på https://[*värd*]:[*port*]/system/console/configMgr.
1. Klicka för att öppna **[!UICONTROL Forms Portal Draft and Submission Configuration]** i redigeringsläge.

1. Ange värdena för egenskaperna enligt följande tabell:

   | **Egenskap** | **Beskrivning** | **Värde** |
   |---|---|---|
   | Forms Portal Draft Data Service | Identifierare för datatjänsten för utkast | formsportal.sampledataservice |
   | Forms Portal Draft Metadata Service | Identifierare för metadatatjänsten för utkast | formsportal.samplemetadataservice |
   | Forms Portal Submit Data Service | Identifierare för Skicka datatjänst | formsportal.sampledataservice |
   | Forms Portal Submit Metadata Service | Identifierare för tjänsten Skicka metadata | formsportal.samplemetadataservice |
   | Datatjänst för Forms Portal som väntar på signering | Identifierare för datatjänsten för väntande signering | formsportal.sampledataservice |
   | Metadatatjänst för Forms Portal som väntar på signering | Identifierare för metadatatjänsten för väntande signering | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >Tjänsterna löses av deras namn som anges som värde för `aem.formsportal.impl.prop` enligt följande:

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   Du kan ändra namn på data- och metadatatabellerna.

   Så här anger du ett annat namn för metadatatabellen:

   * I Web Console Configuration söker du efter och klickar på Exempel på implementering av Forms Portal Metadata Service. Du kan ändra värdena för datakälla, metadata eller ytterligare metadatatabellnamn.

   Så här anger du ett annat namn för datatabellen:

   * I Web Console Configuration söker du efter och klickar på Exempel på implementering av Forms Portal Data Service. Du kan ändra värdena för datakällan och datatabellnamnet.
   >[!NOTE]
   >
   >Om du ändrar tabellnamnen anger du dem i formulärportalskonfigurationen.

1. Låt andra konfigurationer vara som de är och klicka på **[!UICONTROL Save]**.

1. Databasanslutningen kan göras via den poolade datakällan för Apache Sling-anslutningen.
1. För Apache Sling-anslutningen söker du efter och klickar för att öppna **[!UICONTROL Apache Sling Connection Pooled DataSource]** i redigeringsläge i webbkonsolkonfigurationen. Ange värdena för egenskaperna enligt följande tabell:

<table>
 <tbody>
  <tr>
   <td><strong>Egenskap</strong></td>
   <td><strong>Värde</strong></td>
  </tr>
  <tr>
   <td>Datakällans namn</td>
   <td><p>Ett datakällnamn för filtrering av drivrutiner från datakällpoolen</p> <p><strong>Obs! </strong><em>I exempelimplementeringen används FormsPortal som datakällnamn.</em></p> </td>
  </tr>
  <tr>
   <td>JDBC-drivrutinsklass</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>URI för JDBC-anslutning<br /> </td>
   <td>jdbc:mysql://[<em>värd</em>]:[<em>port</em>]/[<em>schema_name</em>]</td>
  </tr>
  <tr>
   <td>Användarnamn</td>
   <td>Ett användarnamn för att autentisera och utföra åtgärder på databastabeller</td>
  </tr>
  <tr>
   <td>Lösenord</td>
   <td>Lösenord som är kopplat till användarnamnet</td>
  </tr>
  <tr>
   <td>Transaktionsisolering</td>
   <td>READ_COMMTED</td>
  </tr>
  <tr>
   <td>Maximalt antal aktiva anslutningar</td>
   <td>1000</td>
  </tr>
  <tr>
   <td>Maximalt antal inaktiva anslutningar</td>
   <td>100</td>
  </tr>
  <tr>
   <td>Minsta antal inaktiva anslutningar</td>
   <td>10</td>
  </tr>
  <tr>
   <td>Inledande storlek</td>
   <td>10</td>
  </tr>
  <tr>
   <td>Max. väntan</td>
   <td>100000</td>
  </tr>
  <tr>
   <td>Testa om Born</td>
   <td>Markerad</td>
  </tr>
  <tr>
   <td>Testa vid inaktivitet</td>
   <td>Markerad</td>
  </tr>
  <tr>
   <td>Valideringsfråga</td>
   <td>Exempelvärden är SELECT 1(mysql), välj 1 från dual(oracle), SELECT 1(MS Sql Server) (validationQuery)</td>
  </tr>
  <tr>
   <td>Timeout för verifieringsfråga</td>
   <td>10000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* JDBC-drivrutinen för MySQL ingår inte i exemplet. Se till att du har etablerat dig för den och ange den information som krävs för att konfigurera JDBC-anslutningspoolen.
>* Peka författaren och publicera instanser för att använda samma databas. Värdet för URI-fältet för JDBC-anslutningen måste vara samma för alla författare- och publiceringsinstanser.


1. Låt andra konfigurationer vara som de är och klicka på **[!UICONTROL Save]**.

1. Om du redan har en tabell i databasschemat går du vidare till nästa steg.

   Om du inte redan har en tabell i databasschemat kör du följande SQL-satser för att skapa separata tabeller för data, metadata och ytterligare metadata i databasschemat:

   >[!NOTE]
   >
   >Du behöver inte olika databaser för författare och publiceringsinstanser. Använd samma databas på alla författare- och publiceringsinstanser.

   **SQL-sats för datatabell**

   ```sql
   CREATE TABLE `data` (
   `owner` varchar(255) DEFAULT NULL,
   `data` longblob,
   `metadataId` varchar(45) DEFAULT NULL,
   `id` varchar(45) NOT NULL,
   PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **SQL-sats för metadatatabell**

   ```sql
   CREATE TABLE `metadata` (
   `formPath` varchar(1000) DEFAULT NULL,
   `formType` varchar(100) DEFAULT NULL,
   `description` text,
   `formName` varchar(255) DEFAULT NULL,
   `owner` varchar(255) DEFAULT NULL,
   `enableAnonymousSave` varchar(45) DEFAULT NULL,
   `renderPath` varchar(1000) DEFAULT NULL,
   `nodeType` varchar(45) DEFAULT NULL,
   `charset` varchar(45) DEFAULT NULL,
   `userdataID` varchar(45) DEFAULT NULL,
   `status` varchar(45) DEFAULT NULL,
   `formmodel` varchar(45) DEFAULT NULL,
   `markedForDeletion` varchar(45) DEFAULT NULL,
   `showDorClass` varchar(255) DEFAULT NULL,
   `sling:resourceType` varchar(1000) DEFAULT NULL,
   `attachmentList` longtext,
   `draftID` varchar(45) DEFAULT NULL,
   `submitID` varchar(45) DEFAULT NULL,
   `id` varchar(60) NOT NULL,
   `profile` varchar(255) DEFAULT NULL,
   `submitUrl` varchar(1000) DEFAULT NULL,
   `xdpRef` varchar(1000) DEFAULT NULL,
   `agreementId` varchar(255) DEFAULT NULL,
   `nextSigners` varchar(255) DEFAULT NULL,
   `eSignStatus` varchar(45) DEFAULT NULL,
   `pendingSignID` varchar(45) DEFAULT NULL,
   `agreementDataId` varchar(255) DEFAULT NULL,
   `enablePortalSubmit` varchar(45) DEFAULT NULL,
   `submitType` varchar(45) DEFAULT NULL,
   `dataType` varchar(45) DEFAULT NULL,
   `jcr:lastModified` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`id`),
   UNIQUE KEY `ID_UNIQUE` (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **SQL-sats för ytterligare metadata**

   ```sql
   CREATE TABLE `additionalmetadatatable` (
   `value` text,
   `key` varchar(255) NOT NULL,
   `id` varchar(60) NOT NULL,
   PRIMARY KEY (`id`,`key`),
   CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **SQL-sats för kommentartabell**

   ```sql
   CREATE TABLE `commenttable` (
   `commentId` varchar(255) DEFAULT NULL,
   `comment` text DEFAULT NULL,
   `ID` varchar(255) DEFAULT NULL,
   `commentowner` varchar(255) DEFAULT NULL,
   `time` varchar(255) DEFAULT NULL);
   ```

1. Om du redan har tabellerna (data, metadata och ytterligare metadata) i databasschemat kör du följande ändringsfrågor:

   **SQL-sats för att ändra datatabellen**

   ```sql
   ALTER TABLE `data` CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **SQL-sats för att ändra metadatatabellen**

   ```sql
   ALTER TABLE metadata add markedForDeletion varchar(45) DEFAULT NULL
   ```

   >[!NOTE]
   >
   >ALTER TABLE-metadatatilläggsfrågan misslyckas om du redan har kört den och kolumnen markedforDeletion finns i tabellen.

   ```sql
   ALTER TABLE metadata add agreementId varchar(255) DEFAULT NULL,
   add nextSigners varchar(255) DEFAULT NULL,
   add eSignStatus varchar(45) DEFAULT NULL,
   add pendingSignID varchar(45) DEFAULT NULL,
   add agreementDataId varchar(255) DEFAULT NULL,
   add enablePortalSubmit varchar(45) DEFAULT NULL,
   add submitType varchar(45) DEFAULT NULL,
   add dataType varchar(45) DEFAULT NULL;
   ```

   ```sql
   ALTER TABLE `metadata` CHANGE `formPath` `formPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formType` `formType` VARCHAR(100) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `description` `description` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formName` `formName` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `renderPath` `renderPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `showDorClass` `showDorClass` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `sling:resourceType` `sling:resourceType` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `profile` `profile` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `submitUrl` `submitUrl` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `xdpRef` `xdpRef` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **SQL-sats för att ändra tabellen med ytterligare metadata**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

Exempelimplementeringen är nu konfigurerad, som du kan använda för att lista dina utkast och överföringar medan du lagrar alla data och metadata i en databas. Nu ska vi se hur data och metadatatjänster är konfigurerade i exemplet.

## Installera filen mysql-connector-java-5.1.39-bin.jar {#install-mysql-connector-java-bin-jar-file}

Utför följande steg på alla författare- och publiceringsinstanser för att installera filen mysql-connector-java-5.1.39-bin.jar:

1. Navigera till `https://'[server]:[port]'/system/console/depfinder` och söka efter paketet com.mysql.jdbc.
1. I kolumnen Exporterad av kontrollerar du om paketet exporteras av något paket.

   Fortsätt om paketet inte exporteras av något paket.

1. Navigera till `https://'[server]:[port]'/system/console/bundles` och klicka **[!UICONTROL Install/Update]**.
1. Klicka **[!UICONTROL Choose File]** och bläddra till filen mysql-connector-java-5.1.39-bin.jar. Välj även **[!UICONTROL Start Bundle]** och **[!UICONTROL Refresh Packages]** kryssrutor.
1. Klicka på **[!UICONTROL Install or Update]**. Starta om servern när du är klar.
1. (*Endast Windows*) Stäng av operativsystemets brandvägg.

## Exempelkod för formulärportaldata och metadatatjänst {#sample-code-for-forms-portal-data-and-metadata-service}

Följande ZIP innehåller `FormsPortalSampleDataServiceImpl` och `FormsPortalSampleMetadataServiceImpl` (implementeringsklasser) för gränssnitt för data- och metadatatjänster. Dessutom innehåller den alla klasser som krävs för kompilering av ovannämnda implementeringsklasser.

[Hämta fil](assets/sample_package.zip)

## Verifiera längden på filnamnet  {#verify-length-of-the-file-name}

Databasimplementeringen av Forms Portal använder ytterligare metadatatabell. Tabellen har en sammansatt primärnyckel baserad på kolumnerna Key och id i tabellen. MySQL tillåter primärnycklar upp till 255 tecken. Du kan använda följande valideringsskript på klientsidan för att kontrollera längden på filnamnet som är kopplat till filwidgeten. Valideringen körs när en fil bifogas. Skriptet som ges i följande procedur visar ett meddelande när filnamnet är större än 150 (inklusive filtillägg). Du kan ändra skriptet för att kontrollera om det innehåller ett annat antal tecken.

Utför följande steg för att skapa [ett klientbibliotek](/help/sites-developing/clientlibs.md) och använd skriptet:

1. Logga in på CRXDE och navigera till /etc/clientlibs/
1. Skapa en nod av typen **cq:ClientLibraryFolder** och ange nodens namn. Till exempel, `validation`.

   Klicka på **[!UICONTROL Save All]**.

1. Högerklicka på noden och klicka på **[!UICONTROL create new file]** och skapa en fil med tillägget .txt. Till exempel: `js.txt`Lägg till följande kod i den nyligen skapade TXT-filen och klicka på **[!UICONTROL Save All]**.

   ```javascript
   #base=util
    util.js
   ```

   I ovanstående kod `util` är namnet på mappen och `util.js` filens namn i `util` mapp. The `util` mapp och `util.js` filen skapas i följande steg.

1. Högerklicka på `cq:ClientLibraryFolder` som skapades i steg 2 väljer du Skapa > Skapa mapp. Skapa en mapp med namnet `util`. Klicka på **[!UICONTROL Save All]**. Högerklicka på `util` väljer du Skapa > Skapa fil. Skapa en fil med namnet `util.js`. Klicka på **[!UICONTROL Save All]**.

1. Lägg till följande kod i filen util.js och klicka på **[!UICONTROL Save All]**. Koden verifierar längden på filnamnet.

   ```javascript
   /*
    * ADOBE CONFIDENTIAL
    * ___________________
    *
    * Copyright 2016 Adobe Systems Incorporated
    * All Rights Reserved.
    *
    * NOTICE:  All information contained herein is, and remains
    * the property of Adobe Systems Incorporated and its suppliers,
    * if any.  The intellectual and technical concepts contained
    * herein are proprietary to Adobe Systems Incorporated and its
    * suppliers and may be covered by U.S. and Foreign Patents,
    * patents in process, and are protected by trade secret or copyright law.
    * Dissemination of this information or reproduction of this material
    * is strictly forbidden unless prior written permission is obtained
    * from Adobe Systems Incorporated.
    *
    */
   (function () {
       var connectWithGuideBridge = function (gb) {
           gb.connect(function () {
               //For first time load
               window.guideBridge.on("elementValueChanged" , function(event, payload) {
           var component = payload.target; // Field whose value has changed
                   if(component.name == 'fileAttachment' && component.parent) {
                       var fileItems = $('#'+payload.target.parent.id).find(".guide-fu-fileItem");
                       for (i = 0;i<fileItems.length;i++) {
                           var filename = $(fileItems[i]).find(".guide-fu-fileName").text();
                           //check whether it is previously attached file or a newly  attached one
                           if(filename.length > 150 && filename.indexOf("fp.attach.jsp") < 0) {
                               window.alert("filename is larger than 150 : "+filename);
                                $(fileItems[i]).find(".guide-fu-fileClose.close").click();
                           }
                       }
                   }
   
      });
           });
       };
   
       if (window.guideBridge) {
           connectWithGuideBridge(window.guideBridge);
       } else {
           window.addEventListener("bridgeInitializeStart", function (event) {
               connectWithGuideBridge(event.detail.guideBridge);
           });
       }
   })();
   ```

   >[!NOTE]
   >
   >Skriptet är avsett för widgetkomponenten för bifogad OTB-fil. Om du har anpassat widgeten för bifogade OTB-filer ändrar du skriptet ovan så att respektive ändringar införs.

1. Lägg till följande egenskap i mappen som skapades i steg 2 och klicka på **[!UICONTROL Save All]**.

   * **[!UICONTROL Name:]** kategorier

   * **[!UICONTROL Type:]** Sträng

   * **[!UICONTROL Value:]** fp.validation

   * **[!UICONTROL multi option:]** Aktiverad

1. Navigera till `/libs/fd/af/runtime/clientlibs/guideRuntime`och lägg till `fp.validation` värdet till egenskapen embed.

1. Navigera till /libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA och lägg till `fp.validation` värde för att bädda in egenskap.

   >[!NOTE]
   >
   >Om du använder anpassade klientbibliotek i stället för klientbiblioteken guideRuntime och guideRuntimeWithXfa använder du kategorinamnet för att bädda in klientbiblioteket som skapas i den här proceduren i dina anpassade bibliotek som läses in vid körning.

1. Klicka **[!UICONTROL Save All.]** När filnamnet är större än 150 tecken (inklusive filtillägg) visas nu ett meddelande.
