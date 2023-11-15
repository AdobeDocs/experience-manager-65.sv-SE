---
title: Användargränssnitt Recommendations för kunder
seo-title: User Interface Recommendations for Customers
description: En lista med rekommendationer relaterade till de klassiska och pekoptimerade användargränssnitten.
seo-description: A list of recommendations related to the classic and touch-optimized user interfaces.
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# Användargränssnitt Recommendations för kunder{#user-interface-recommendations-for-customers}

Adobe Experience Manager har två användargränssnitt - det enhetliga användargränssnittet för Experience Cloud (kallas även användargränssnittet med pekfunktion) och det klassiska användargränssnittet.

Det här dokumentet är avsett att vägleda kunderna att välja vilket användargränssnitt som ska användas beroende på deras situation.

Intressevillkor:

* **Användargränssnitt (eller standardgränssnitt)**
Modernt användargränssnitt som introducerades i 5.6.0 som en förhandstitt på teknik och utökades i efterföljande versioner. Det bygger på den enhetliga användarupplevelsen för Adobe Experience Cloud, som tidigare kallades användargränssnitt med pekfunktion eller användargränssnitt.

* **Klassiskt användargränssnitt**
Användargränssnitt som bygger på ExtJS-teknik som introducerades med CQ 5.1 2008.

* **Webbplatsadministratör**
Möjlighet att hantera platshierarkin (flytta, aktivera, hantera referenser) och skapa nya sidor.

* **Sidredigering**
Möjlighet att lägga till/redigera innehållet på en sida.

* **DAM-/resursadministratör**
Möjlighet att hantera digitalt material (inklusive bilder, video, dokument, nedladdningar).

* **ContextHub**
Möjlighet att samla information om besökaren och använda den för olika syften. Tillhandahåller ett användargränssnitt för att simulera personer som besöker webbplatsen. Med början AEM 6.2 ersatte ContextHub den tidigare tekniken, Client Context.

## Allmänt {#general}

Under de senaste åren har Adobe uppdaterat alla Adobe Experience Cloud-lösningar med ett enhetligt användargränssnitt. De olika Experience Cloud-lösningarna har en enhetlig upplevelse av de vanligaste mönstren för hur programmen används och används. I varje release har Adobe förfinat sitt användargränssnitt baserat på feedback från kunder som arbetar med de olika lösningarna.

Det ursprungliga användargränssnittet för Adobe Experience Manager (tidigare CQ5), som introducerades 2008 och används av kunder som kör version 5.0-5.6.1, finns i AEM 6.5. Detta garanterar att kunderna kan uppdatera till 6.5 och dra nytta av en uppdaterad plattform med nya funktioner samtidigt som de använder samma användargränssnitt.

Adobe rekommenderar att man planerar att gå över till det nya användargränssnittet under 2018/2019. Detta kan antingen göras under uppdateringen till 6.5, eller i ett separat projekt efter uppdateringen som innehåller nödvändiga justeringar av anpassningarna och komponentdialogrutorna.

Det klassiska användargränssnittet har tagits bort i AEM 6.4 och Adobe planerar inte att göra ytterligare förbättringar av det klassiska användargränssnittet. Observera att Classic-användargränssnittet fortfarande stöds fullt ut när det är inaktuellt.

### Regler och Recommendations {#rules-and-recommendations}

Nedan följer en lista över rekommendationer från Product Management för Adobe Experience Manager 6.5:

<table>
 <tbody>
  <tr>
   <th>Mitt projekt...</th>
   <th>Recommendations</th>
  </tr>
  <tr>
   <td>Börjar bara använda Adobe Experience Manager.</td>
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
     <li>Uppdatera komponentdialogrutorna så att de använder Dialogrutan Coral 3. Adobe rekommenderar att du använder <a href="/help/sites-developing/modernization-tools.md">Verktyg för AEM</a> för att uppdatera komponenterna.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Har skapat en webbplats som använder ClientContexten med integreringar.<br /> </td>
   <td>
    <ol>
     <li>Uppdatera till 6.5</li>
     <li>Använd standardgränssnittet för platsadministration, resurser, ... osv.</li>
     <li>Konfigurera åtgärden Redigera sida för att öppna den klassiska sidredigeraren i användargränssnittet. Se <a href="#selecting-your-ui">Välja användargränssnitt</a>.</li>
    </ol> <p>I en andra fas:</p>
    <ol>
     <li>Uppdatera komponentdialogrutorna så att de använder Dialogrutan Coral 3. Adobe rekommenderar att du använder <a href="/help/sites-developing/modernization-tools.md">Verktyg för AEM</a> för att uppdatera komponenterna.</li>
     <li>Konfigurera ContextHub (ersättning för ClientContexten) och uppdatera sidmallarna så att ContextHub används. ContextHub har ett kompatibilitetsläge som tillåter inläsning av anpassade ClientContexter.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>Har använt CQ/AEM i många år.</p> <p>Har utökat produktgränssnittet (till exempel Webbplatsadministratör) och byggt komponenter med omfattande redigeringsdialogrutor.</p> </td>
   <td><p>Uppdatera till 6.5 och konfigurera det klassiska användargränssnittet som standard för sidredigering för alla användare. Se <a href="#selecting-your-ui">Välja användargränssnitt</a>.</p> <p>Starta sedan ett projekt för att anpassa och optimera komponentdialogrutorna i Coral 3-format. Se <a href="#resources-to-help">Resurser att hjälpa</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Vanliga frågor {#faq}

Läs artikeln i kunskapsbasen [Vanliga frågor om redigering av Touch UI](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html), om du vill ha mer information, inklusive information om tidsplanen för borttagning av dubbletter för det klassiska användargränssnittet.

### Välja användargränssnitt {#selecting-your-ui}

Se [Välja användargränssnitt](/help/sites-authoring/select-ui.md) om du vill ha information om hur du konfigurerar systemet.

### Pekaktiverad gränssnittsstatus {#touch-enabled-ui-status}

Mer information om förbättringarna av det beröringsaktiverade användargränssnittet i AEM 6.5 finns i [Nyheter](/help/release-notes/release-notes.md#what-s-new) i versionsinformationen.

En fullständig översikt finns i [Funktionsstatus för Touch UI](/help/release-notes/touch-ui-features-status.md) page

### Resurser att hjälpa {#resources-to-help}

För bakgrundsinformation om grundläggande hantering:

* [Redigeringssidor](/help/sites-authoring/page-authoring.md).

Detaljerad utvecklingsinformation:

* [UI-arkitektur med pekskärmsfunktioner](/help/sites-developing/touch-ui-concepts.md).
* Använd [Verktyg för AEM](/help/sites-developing/modernization-tools.md) om du vill konvertera komponentredigeringsdialogrutor från det klassiska användargränssnittet till det beröringsaktiverade användargränssnittet.

* [Struktur för användargränssnittet med pekskärm](/help/sites-developing/touch-ui-structure.md).

* [Anpassa konsolerna i det pekaktiverade användargränssnittet](/help/sites-developing/customizing-consoles-touch.md) (innehåller exempelkod).

* [Anpassa sidredigering i det beröringsaktiverade användargränssnittet](/help/sites-developing/customizing-page-authoring-touch.md) (innehåller exempelkod).

* [Granite UI-dokumentation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).
