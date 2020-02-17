---
title: Konfigurera Ångra för sidredigering
seo-title: Konfigurera Ångra för sidredigering
description: Lär dig hur du konfigurerar Ångra-stöd för sidredigering i AEM.
seo-description: Lär dig hur du konfigurerar Ångra-stöd för sidredigering i AEM.
uuid: e5a49587-a2a6-41d5-b449-f7a8f7e4cee6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3cc7efc5-bcb2-41c9-b78b-308f6b7a298e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera Ångra för sidredigering{#configuring-undo-for-page-editing}

I [OSGi-tjänsten](/help/sites-deploying/configuring-osgi.md) CQ WCM Undo Configuration **(** `com.day.cq.wcm.undo.UndoConfigService`) finns flera egenskaper som styr beteendet för kommandona Ångra och Gör om för redigering av sidor.

## Standardkonfiguration {#default-configuration}

I en standardinstallation definieras standardinställningarna som egenskaper på `sling:OsgiConfig`noden:

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

Den här noden innehåller `cq.wcm.undo.whitelist` och `cq.wcm.undo.blacklist` egenskaper. För de andra egenskaperna används standardvärdena.

>[!CAUTION]
>
>Du ***får*** inte ändra något i `/libs` banan.
>
>Detta beror på att innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan mycket väl skrivas över när du använder en snabbkorrigering eller ett funktionspaket).

## Konfigurera Ångra och Gör om {#configuring-undo-and-redo}

Du kan konfigurera dessa OSGi-tjänstegenskaper för din egen instans.

>[!NOTE]
>
>När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. Mer information och rekommendationer finns i [Konfigurera OSGi](/help/sites-deploying/configuring-osgi.md) .

I följande lista visas egenskaperna så som de visas i webbkonsolen, följt av namnet på motsvarande OSGi-parameter, tillsammans med en beskrivning och standardvärdet (där det är lämpligt):

* **Enable**( `cq.wcm.undo.enabled`)

   * **Beskrivning**: Avgör om sidförfattare kan ångra och göra om ändringar.
   * **Standard**: `Selected`
   * **Typ**: `Boolean`

* **Path**( `cq.wcm.undo.path`)

   * **Beskrivning**: Databassökvägen för beständiga binära ångra-data. När författare ändrar binära data, t.ex. bilder, behålls den ursprungliga versionen av dessa data här. När ändringar av binära data ångras återställs dessa binära ångra-data till sidan.
   * **Standard**: `/var/undo`
   * **Typ**: `String`
   >[!NOTE]
   >
   >Som standard har bara administratörer åtkomst till `/var/undo` noden. Författare kan bara ångra och göra om åtgärder för binärt innehåll efter att de har fått behörighet att komma åt binära ångra-data.

* **Min. validity**( `cq.wcm.undo.validity`)

   * **Beskrivning**: Den kortaste tiden som binära ångra-data lagras, i timmar. Efter den här tidsperioden är binära data tillgängliga för borttagning för att spara diskutrymme.
   * **Standard**: `10`
   * **Typ**: `Integer`

* **Steg**( `cq.wcm.undo.steps`)

   * **Beskrivning**: Det maximala antalet sidåtgärder som lagras i ångra-historiken.
   * **Standard**: `20`
   * **Typ**: `Integer`

* **Persistence**( `cq.wcm.undo.persistence`)

   * **Beskrivning**: Klassen som innehåller ångra-historiken. Två beständiga klasser finns:

      * `CQ.undo.persistence.WindowNamePersistence`: Bevarar historik med egenskapen window.name.
      * `CQ.undo.persistence.CookiePersistance`: Bevarar historik med hjälp av cookies.
   * **Standard**: `CQ.undo.persistence.WindowNamePersistence`
   * **Typ**: `String`


* **Beständiga lägen**( `cq.wcm.undo.persistence.mode`)

   * **Beskrivning**: Avgör när ångra-historiken sparas. Välj det här alternativet om du vill behålla ångra-historiken efter varje sidredigering. Avmarkera det här alternativet om du bara vill behålla när en sidinläsning sker (användaren t.ex. navigerar till en annan sida).

      Om du vill ångra-historiken används webbläsarresurserna. Om användarens webbläsare svarar långsamt på sidredigeringar kan du försöka med att behålla ångra-historiken när sidan läses in igen.

   * **Standard**: `Selected`
   * **Typ**: `Boolean`

* **Markörläge**( `cq.wcm.undo.markermode`)

   * **Beskrivning**: Anger den visuella referens som ska användas för att ange vilka stycken som påverkas när en ångra eller gör om inträffar. Följande värden är giltiga:

      * flash: Markeringsindikatorn för styckena blinkar tillfälligt.
      *  välj: Stycket är markerat.
   * **Standard**: `flash`
   * **Typ**: `String`


* **Bra komponenter**( `cq.wcm.undo.whitelist`)

   * **Beskrivning**: En lista över komponenter som du vill ska påverkas av kommandona Ångra och Gör om. Lägg till komponentsökvägar i den här listan när de fungerar korrekt med ångra/gör om. Lägg till en asterisk (&amp;ast;) för att ange en grupp komponenter:

      * Följande värde anger den grundläggande textkomponenten:

         `foundation/components/text`

      * Följande värde anger alla grundkomponenter:

         `foundation/components/*`
   * När Ångra eller Gör om utfärdas till en komponent som inte finns i den här listan visas ett meddelande om att kommandot kan vara otillförlitligt.

   * **Standard**: Egenskapen är ifylld med många komponenter som AEM tillhandahåller.
   * **Typ**: `String[]`


* **Felaktiga komponenter**( `cq.wcm.undo.blacklist`)

   * **Beskrivning**: En lista med komponenter och/eller komponentåtgärder som du inte vill ska påverkas av kommandot Ångra. Lägg till komponenter och komponentåtgärder som inte fungerar som de ska med kommandot Ångra:

      * Lägg till en komponentsökväg när du inte vill ha någon av komponentens åtgärder i ångra-historiken, till exempel `collab/forum/components/post`
      * Lägg till ett kolon (:) och en åtgärd i sökvägen när du vill att den specifika åtgärden ska utelämnas från ångra-historiken (andra åtgärder fungerar korrekt), till exempel `collab/forum/components/post:insertParagraph.`
   >[!NOTE]
   >
   >När en åtgärd finns i listan läggs den fortfarande till i ångra-historiken. Användare kan inte ångra åtgärder som finns tidigare än en **Dålig komponent** -åtgärd i ångra-historiken.

   * Vanliga åtgärdsnamn är:

      * `insertParagraph`: Komponenten läggs till på sidan.
      * `removeParagraph`: Komponenten tas bort.
      * `moveParagraph`: Stycket flyttas till en annan plats.
      * `updateParagraph`: Styckeegenskaperna ändras.
   * **Standard**: Egenskapen fylls i med flera komponentåtgärder.
   * **Typ**: `String[]`




