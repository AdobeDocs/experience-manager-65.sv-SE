---
title: Rekommendationer för användargränssnitt för kunder
seo-title: Rekommendationer för användargränssnitt för kunder
description: En lista med rekommendationer relaterade till de klassiska och pekoptimerade användargränssnitten.
seo-description: En lista med rekommendationer relaterade till de klassiska och pekoptimerade användargränssnitten.
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# Rekommendationer för användargränssnitt för kunder{#user-interface-recommendations-for-customers}

Adobe Experience Manager har två användargränssnitt - det enhetliga användargränssnittet i Experience Cloud (även kallat det pekaktiverade användargränssnittet) och det klassiska användargränssnittet.

Det här dokumentet är avsett att vägleda kunderna att välja vilket användargränssnitt som ska användas beroende på deras situation.

Intressevillkor:

* **Användargränssnitt (eller standardgränssnitt)** Modernt användargränssnitt som introducerades i 5.6.0 som en förhandstitt på teknik och utökades i efterföljande versioner. Det baseras på den enhetliga användarupplevelsen för Adobe Experience Cloud, som tidigare kallades användargränssnitt med pekfunktion eller användargränssnitt.

* **Klassiskt användargränssnitt** baserat på ExtJS-teknik som introducerades med CQ 5.1 2008.

* **Webbplatsadministratörer** kan hantera platshierarkin (flytta, aktivera, hantera referenser) och skapa nya sidor.

* **Sidredigering** för att lägga till/redigera innehållet på en sida.

* **DAM/Assets Admin** Capabilities to manage digital assets (including images, video, documents, downloads).

* **ContextHub** Capabilities för att samla information om besökaren och använda den för olika syften. Tillhandahåller ett användargränssnitt för att simulera personer som besöker webbplatsen. Med början från AEM 6.2 ersatte ContextHub den tidigare tekniken, Client Context.

## Allmänt {#general}

Under de senaste åren har Adobe uppdaterat alla Adobe Experience Cloud-lösningar med ett enhetligt användargränssnitt. Användare i hela Experience Cloud-lösningar får en enhetlig upplevelse av vanliga mönster för hur de använder och använder programmen. I varje release har Adobe förfinat användargränssnittet baserat på feedback från kunder som arbetar med de olika lösningarna.

Det ursprungliga användargränssnittet för Adobe Experience Manager (tidigare kallat CQ5), som introducerades 2008 och används av kunder som kör version 5.0-5.6.1, finns i AEM 6.5. Detta garanterar att kunderna kan uppdatera till 6.5 och dra nytta av en uppdaterad plattform med nya funktioner samtidigt som de använder samma användargränssnitt.

Adobe rekommenderar kunder att gå över till det nya användargränssnittet under 2018/2019. Detta kan antingen göras under uppdateringen till 6.5, eller i ett separat projekt efter uppdateringen som innehåller nödvändiga justeringar av anpassningarna och komponentdialogrutorna.

Det klassiska användargränssnittet har tagits bort i AEM 6.4 och Adobe planerar inte att göra ytterligare förbättringar av det klassiska användargränssnittet. Observera att Classic-användargränssnittet fortfarande stöds fullt ut när det är inaktuellt.

### Regler och rekommendationer {#rules-and-recommendations}

Nedan följer en lista med rekommendationer från Product Management för Adobe Experience Manager 6.5:

<table>
 <tbody>
  <tr>
   <th>Mitt projekt...</th>
   <th>Rekommendationer</th>
  </tr>
  <tr>
   <td>Vi börjar precis använda Adobe Experience Manager.</td>
   <td>Använd standardgränssnittet.</td>
  </tr>
  <tr>
   <td><p>Har använt AEM ett tag.</p> <p>Har använt produktgränssnittet som det är tänkt och utvecklat anpassade komponenter för webbplatserna.<br /> </p> </td>
   <td>
    <ol>
     <li>Uppdatera till 6.5</li>
     <li>Använd standardgränssnittet för platsadministration, resurser, ... osv.<br /> </li>
     <li>Konfigurera åtgärden Redigera sida för att öppna den klassiska sidredigeraren i användargränssnittet. Se <a href="#selecting-your-ui">Välja användargränssnitt</a>.</li>
    </ol> <p>I en andra fas:</p>
    <ol>
     <li>Uppdatera komponentdialogrutorna så att de använder Dialogrutan Coral 3. Adobe rekommenderar att du uppdaterar komponenterna med <a href="/help/sites-developing/dialog-conversion.md">Dialog Conversion Tool</a> .</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Har skapat en webbplats som använder ClientContext med integreringar.<br /> </td>
   <td>
    <ol>
     <li>Uppdatera till 6.5</li>
     <li>Använd standardgränssnittet för platsadministration, resurser, ... osv.</li>
     <li>Konfigurera åtgärden Redigera sida för att öppna den klassiska sidredigeraren i användargränssnittet. Se <a href="#selecting-your-ui">Välja användargränssnitt</a>.</li>
    </ol> <p>I en andra fas:</p>
    <ol>
     <li>Uppdatera komponentdialogrutorna så att de använder Dialogrutan Coral 3. Adobe rekommenderar att du uppdaterar komponenterna med <a href="/help/sites-developing/dialog-conversion.md">Dialog Conversion Tool</a> .</li>
     <li>Konfigurera ContextHub (ersättning för ClientContext) och uppdatera sidmallarna så att ContextHub används. Observera att ContextHub har ett kompatibilitetsläge som tillåter inläsning av anpassade ClientContext-lager.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>Har använt CQ/AEM i många år.</p> <p>Har utökat produktgränssnittet (t.ex. platsadministratör) och byggt komponenter med omfattande redigeringsdialogrutor.</p> </td>
   <td><p>Uppdatera till 6.5 och konfigurera det klassiska användargränssnittet som standard för sidredigering för alla användare. Se <a href="#selecting-your-ui">Välja användargränssnitt</a>.</p> <p>Starta sedan ett projekt för att anpassa och optimera komponentdialogrutorna i Coral 3-format. Se <a href="#resources-to-help">Resurser att hjälpa</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Vanliga frågor {#faq}

Mer information finns i kunskapsbasartikeln [Touch UI Authoring FAQ](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html). inklusive information om det klassiska användargränssnittets borttagningsschema.

### Välja användargränssnitt {#selecting-your-ui}

Se [Välja användargränssnitt](/help/sites-authoring/select-ui.md) för information om hur du konfigurerar systemet efter behov.

### Pekaktiverad gränssnittsstatus {#touch-enabled-ui-status}

Mer information om förbättringarna av det beröringsaktiverade användargränssnittet i AEM 6.5 finns i [Nyheter](/help/release-notes/release-notes.md#what-s-new) i versionsinformationen.

En fullständig översikt finns på sidan [Funktionsstatus](/help/release-notes/touch-ui-features-status.md) för Touch UI

### Resurser att hjälpa {#resources-to-help}

För bakgrundsinformation om grundläggande hantering:

* [Redigeringssidor](/help/sites-authoring/page-authoring.md).

Detaljerad utvecklingsinformation:

* [Pekaktiverad gränssnittsarkitektur](/help/sites-developing/touch-ui-concepts.md).
* Använd verktyget [för](/help/sites-developing/dialog-conversion.md) dialogkonvertering för att konvertera komponentredigeringsdialogrutor från det klassiska användargränssnittet till det beröringsaktiverade användargränssnittet.

* [Struktur för det beröringskänsliga användargränssnittet](/help/sites-developing/touch-ui-structure.md).

* [Anpassa konsolerna i det beröringsaktiverade användargränssnittet](/help/sites-developing/customizing-consoles-touch.md) (inklusive exempelkod).

* [Anpassa sidredigering i det beröringsaktiverade användargränssnittet](/help/sites-developing/customizing-page-authoring-touch.md) (inkluderar exempelkod).

* [AEM Gem Session vid beröringsaktiverad anpassning](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html).
* [Bevilja gränssnittsdokumentation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

