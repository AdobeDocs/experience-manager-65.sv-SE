---
title: Användargränssnitt Recommendations för kunder
description: En lista med rekommendationer relaterade till de klassiska och pekoptimerade användargränssnitten.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Användargränssnitt Recommendations för kunder{#user-interface-recommendations-for-customers}

Adobe Experience Manager har två användargränssnitt - det enhetliga användargränssnittet för Experience Cloud (kallas även användargränssnittet med pekfunktion) och det klassiska användargränssnittet.

Det här dokumentet är avsett att vägleda kunderna att välja vilket användargränssnitt som ska användas beroende på deras situation.

Intressevillkor:

* **Gränssnitt (eller standardgränssnitt)**
Modernt användargränssnitt som introducerades i 5.6.0 som en förhandstitt på teknik och utökades i efterföljande versioner. Det bygger på den enhetliga användarupplevelsen för Adobe Experience Cloud, som tidigare kallades användargränssnitt med pekfunktion eller användargränssnitt.

* **Klassiskt användargränssnitt**
Användargränssnitt som bygger på ExtJS-teknik som introducerades med CQ 5.1 2008.

* **Webbplatsadministratör**
Möjlighet att hantera platshierarkin (flytta, aktivera, hantera referenser) och skapa nya sidor.

* **Sidredigering**
Möjlighet att lägga till/redigera innehållet på en sida.

* **DAM/Assets Admin**
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
   <td><p>Har använt AEM ett tag.</p> <p>Har använt produktgränssnittet som det är färdigt och utvecklat anpassade komponenter för webbplatserna.<br /> </p> </td>
   <td>
    <ol>
     <li>Uppdatera till 6.5</li>
     <li>Använd standardgränssnittet för platsadministration, resurser, ... etc.<br /> </li>
     <li>Konfigurera åtgärden Redigera sida för att öppna den klassiska sidredigeraren i användargränssnittet. Se <a href="#selecting-your-ui">Välja användargränssnitt</a>.</li>
    </ol> <p>I en andra fas:</p>
    <ol>
     <li>Uppdatera komponentdialogrutorna så att de använder Dialogrutan Coral 3. Adobe rekommenderar att du använder <a href="/help/sites-developing/modernization-tools.md">AEM modereringsverktygen</a> för att uppdatera komponenterna.</li>
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
     <li>Uppdatera komponentdialogrutorna så att de använder Dialogrutan Coral 3. Adobe rekommenderar att du använder <a href="/help/sites-developing/modernization-tools.md">AEM modereringsverktygen</a> för att uppdatera komponenterna.</li>
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

Mer information finns i kunskapsbasartikeln [Vanliga frågor om redigering av användargränssnitt](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html), inklusive information om borttagningsschemat för det klassiska användargränssnittet.

### Välja användargränssnitt {#selecting-your-ui}

Se [Välja användargränssnitt](/help/sites-authoring/select-ui.md) för information om hur du konfigurerar systemet efter behov.

### Pekaktiverad gränssnittsstatus {#touch-enabled-ui-status}

Mer information om förbättringarna av det beröringsaktiverade användargränssnittet i AEM 6.5 finns i [Nyheter](/help/release-notes/release-notes.md#what-s-new) i versionsinformationen.

En fullständig översikt finns på sidan [Funktionsstatus för användargränssnittet](/help/release-notes/touch-ui-features-status.md)

### Resurser att hjälpa {#resources-to-help}

För bakgrundsinformation om grundläggande hantering:

* [Redigerar sidor](/help/sites-authoring/page-authoring.md).

Detaljerad utvecklingsinformation:

* [Användargränssnittsarkitektur aktiverad för pekfunktioner](/help/sites-developing/touch-ui-concepts.md).
* Använd [AEM moderniseringsverktyg](/help/sites-developing/modernization-tools.md) för att konvertera komponentredigeringsdialogrutor från det klassiska användargränssnittet till det beröringsaktiverade användargränssnittet.

* [Struktur för det beröringsaktiverade användargränssnittet](/help/sites-developing/touch-ui-structure.md).

* [Anpassa konsolerna i det beröringsaktiverade användargränssnittet](/help/sites-developing/customizing-consoles-touch.md) (inkluderar exempelkod).

* [Anpassa sidredigering i det beröringsaktiverade användargränssnittet](/help/sites-developing/customizing-page-authoring-touch.md) (inkluderar exempelkod).

* [Bevilja gränssnittsdokumentation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).
