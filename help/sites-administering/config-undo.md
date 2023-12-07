---
title: Konfigurera Ångra för sidredigering
description: Lär dig hur du konfigurerar Ångra-stöd för sidredigering i AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 2cf3ac3f-ee17-480d-a32a-c57631502693
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---

# Konfigurera Ångra för sidredigering{#configuring-undo-for-page-editing}

The [OSGi-tjänst](/help/sites-deploying/configuring-osgi.md)  **Konfiguration av Ångra för CQ WCM dag** ( `com.day.cq.wcm.undo.UndoConfigService`) visar flera egenskaper som styr beteendet för kommandona ångra och gör om för att redigera sidor.

## Standardkonfiguration {#default-configuration}

I en standardinstallation definieras standardinställningarna som egenskaper i `sling:OsgiConfig`nod:

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

Den här noden innehåller `cq.wcm.undo.whitelist` och `cq.wcm.undo.blacklist` -egenskaper, för de andra egenskaperna används standardvärdena.

>[!CAUTION]
>
>Du ***måste*** ändrar ingenting i dialogrutan `/libs` bana.
>
>Detta beror på innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan mycket väl skrivas över när du installerar en snabbkorrigering eller ett funktionspaket).

## Konfigurera Ångra och Gör om {#configuring-undo-and-redo}

Du kan konfigurera dessa OSGi-tjänstegenskaper för din egen instans.

>[!NOTE]
>
>När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. Se [Konfigurerar OSGi](/help/sites-deploying/configuring-osgi.md) om du vill ha mer information och rekommenderade rutiner.

I följande lista visas egenskaperna så som de visas i webbkonsolen, följt av namnet på motsvarande OSGi-parameter, tillsammans med en beskrivning och standardvärdet (där det är lämpligt):

* **Aktivera**
( `cq.wcm.undo.enabled`)

   * **Beskrivning**: Avgör om sidförfattare kan ångra och göra om ändringar.
   * **Standard**: `Selected`
   * **Typ**: `Boolean`

* **Bana**
( `cq.wcm.undo.path`)

   * **Beskrivning**: Databassökvägen för beständiga binära ångra-data. När författare ändrar binära data, t.ex. bilder, behålls den ursprungliga versionen av dessa data här. När ändringar av binära data ångras återställs dessa binära ångra-data till sidan.
   * **Standard**: `/var/undo`
   * **Typ**: `String`

  >[!NOTE]
  >
  >Som standard har bara administratörer åtkomst till `/var/undo` nod. Författare kan bara ångra och göra om åtgärder för binärt innehåll efter att de har fått behörighet att komma åt binära ångra-data.

* **Min. giltighet**
( `cq.wcm.undo.validity`)

   * **Beskrivning**: Den kortaste tiden som binära ångra-data lagras i timmar. Efter den här tidsperioden är binära data tillgängliga för borttagning för att spara diskutrymme.
   * **Standard**: `10`
   * **Typ**: `Integer`

* **Steg**
( `cq.wcm.undo.steps`)

   * **Beskrivning**: Det maximala antalet sidåtgärder som lagras i ångra-historiken.
   * **Standard**: `20`
   * **Typ**: `Integer`

* **Persistence**
( `cq.wcm.undo.persistence`)

   * **Beskrivning**: Den klass som innehåller ångringshistorik. Två beständiga klasser finns:

      * `CQ.undo.persistence.WindowNamePersistence`: Bevarar historik med egenskapen window.name.
      * `CQ.undo.persistence.CookiePersistance`: Bevarar historik med cookies.

   * **Standard**: `CQ.undo.persistence.WindowNamePersistence`
   * **Typ**: `String`

* **Beständighetsläge**
( `cq.wcm.undo.persistence.mode`)

   * **Beskrivning**: Avgör när ångra-historiken sparas. Välj det här alternativet om du vill behålla ångra-historiken efter varje sidredigering. Avmarkera det här alternativet om du bara vill behålla när en sidinläsning sker (till exempel navigerar användaren till en annan sida).

     Om du vill ångra-historiken används webbläsarresurserna. Om användarens webbläsare svarar långsamt på sidredigeringar kan du försöka med att behålla ångra-historiken när sidan läses in igen.

   * **Standard**: `Selected`
   * **Typ**: `Boolean`

* **Markörläge**
( `cq.wcm.undo.markermode`)

   * **Beskrivning**: Anger den visuella referenspunkt som ska användas för att ange vilka stycken som ska påverkas när en ångra eller gör om inträffar. Följande värden är giltiga:

      * flash: Markeringsindikatorn för styckena blinkar tillfälligt.
      * markera: Stycket är markerat.

   * **Standard**: `flash`
   * **Typ**: `String`

* **Bra komponenter**
( `cq.wcm.undo.whitelist`)

   * **Beskrivning**: En lista över komponenter som du vill ska påverkas av kommandona Ångra och Gör om. Lägg till komponentsökvägar i den här listan när de fungerar korrekt med ångra/gör om. Lägg till en asterisk (&amp;ast;) för att ange en grupp komponenter:

      * Följande värde anger den grundläggande textkomponenten:

        `foundation/components/text`

      * Följande värde anger alla grundkomponenter:

        `foundation/components/*`

   * När Ångra eller Gör om utfärdas till en komponent som inte finns i den här listan visas ett meddelande om att kommandot kan vara otillförlitligt.

   * **Standard**: Egenskapen är ifylld med många komponenter som AEM tillhandahåller.
   * **Typ**: `String[]`

* **Felaktiga komponenter**
( `cq.wcm.undo.blacklist`)

   * **Beskrivning**: En lista med komponenter och/eller komponentåtgärder som du inte vill ska påverkas av kommandot Ångra. Lägg till komponenter och komponentåtgärder som inte fungerar som de ska med kommandot Ångra:

      * Lägg till en komponentsökväg när du inte vill ha någon av komponentens åtgärder i ångra-historiken, till exempel `collab/forum/components/post`
      * Lägg till ett kolon (:) och en åtgärd i sökvägen när du vill att den specifika åtgärden ska utelämnas från ångra-historiken (andra åtgärder fungerar korrekt), till exempel `collab/forum/components/post:insertParagraph.`

  >[!NOTE]
  >
  >När en åtgärd finns i listan läggs den fortfarande till i ångra-historiken. Användare kan inte ångra åtgärder som finns tidigare än en **Felaktig komponent** i ångra-historiken.

   * Vanliga åtgärdsnamn är:

      * `insertParagraph`: Komponenten läggs till på sidan.
      * `removeParagraph`: Komponenten tas bort.
      * `moveParagraph`: Stycket flyttas till en annan plats.
      * `updateParagraph`: Styckeegenskaperna ändras.

   * **Standard**: Egenskapen fylls i med flera komponentåtgärder.
   * **Typ**: `String[]`
