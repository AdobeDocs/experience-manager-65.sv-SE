---
title: Bästa praxis
seo-title: Bästa praxis
description: Adobes tekniker och konsultteam har utvecklat en omfattande uppsättning metodtips för AEM-utvecklare
seo-description: Adobes tekniker och konsultteam har utvecklat en omfattande uppsättning metodtips för AEM-utvecklare
uuid: f962c31f-8140-482f-b189-16376e23bfed
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 99678c1a-81f3-4fb3-bf73-98f0691c3fb6
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# Bästa praxis{#best-practices}

## Best Practices for Developers - Getting Started {#best-practices-for-developers-getting-started}

Adobe Engineering and Consulting-teamet har utvecklat en omfattande uppsättning metodtips för AEM-utvecklare. Adobes utvecklare följer dessa standarder när de utvecklar viktiga AEM-produktuppdateringar och kundkod för kundimplementeringar.

Innan du börjar ditt AEM-utvecklingsprojekt bör du först granska följande metodtips:

* [Utvecklingspraxis](/help/sites-developing/development-practices.md)
* [Innehållsarkitektur](/help/sites-developing/content-architecture.md)
* [Programvaruarkitektur](/help/sites-developing/software-architecture.md)
* [Kodningstips](/help/sites-developing/coding-tips.md)
* [Code Pitfalls](/help/sites-developing/code-pitfalls.md)
* [JCR-interaktion](/help/sites-developing/jcr-integration.md)
* [OSGi Bundles](/help/sites-developing/osgi-bundles.md)

### Ytterligare metodinformation {#additional-best-practices-information}

Följande områden har dokumentation som är specifik för att utveckla metodtips:

* [Webbplatser](#sites)
* [Communities](/help/sites-developing/best-practices.md#communities)
* [Verktyg/HTML](/help/sites-developing/best-practices.md#tooling-htl)

Specifika dokument beskrivs och länkas till i de tabeller som följer.

De bästa sätten att administrera, distribuera och underhålla, eller att skapa, finns i något av följande:

* [Administrera metodtips](/help/sites-administering/administer-best-practices.md)
* [Bästa tillvägagångssätt](/help/sites-authoring/best-practices.md)
* [Effektiva rutiner](/help/sites-deploying/best-practices.md)

## Webbplatser {#sites}

Hantering och redigering av webbplatsinnehåll har några beprövade metoder:

<table>
 <tbody>
  <tr>
   <td>En del av teorin bakom standardgränssnittet med pekfunktioner.</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">Pekaktiverat användargränssnitt: Concepts</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">Pekaktiverat användargränssnitt:Struktur</a></p> </td>
   <td>Dessa dokument ger en översikt över begreppen, och strukturen, för det beröringskänsliga användargränssnittet.</td>
  </tr>
  <tr>
   <td>Pekaktiverat användargränssnitt: Anpassa konsoler </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">Anpassa användargränssnittskonsoler med pekskärm</a></td>
   <td>I det här dokumentet beskrivs det bästa sättet att utöka konsolerna för det beröringsaktiverade användargränssnittet.</td>
  </tr>
  <tr>
   <td>Pekaktiverat användargränssnitt: Anpassa sidredigering</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">Anpassa redigering av pekaktiverade gränssnittssidor</a></td>
   <td>Beskriver hur du utökar sidredigering för det beröringsaktiverade användargränssnittet.</td>
  </tr>
  <tr>
   <td>Arbetsflöden</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">Utveckla och utöka arbetsflöden</a></td>
   <td><p>Med arbetsflöden kan du automatisera Adobe Experience Manager-aktiviteter (AEM) och representera en stor del av den bearbetning som sker i en AEM-miljö, så vi rekommenderar att du noggrant planerar implementeringarna av arbetsflöden.</p> </td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

[AEM Communities](/help/communities/overview.md) förenklar framtagning och hantering av lokala communityn.

Här beskrivs några tips för Communities:

|  |  |  |
|---|---|---|
| Bästa tillvägagångssätt för att arbeta med användargenererat innehåll (UGC) | [Riktlinjer för kodning](/help/communities/code-guide.md) | Riktlinjer för utveckling av flexibel, portabel kod för ramverket [för](/help/communities/scf.md) sociala komponenter (SCF). |
| Exempel på användning av webbgruppskomponenter | [Community Components Guide](/help/communities/components-guide.md) | Ett interaktivt utvecklingsverktyg. |

## Verktyg/HTML {#tooling-htl}

HTML-mallspråk (HTL) är ett nytt HTML-mallsystem som introducerades med AEM 6.0. Den ersätter JSP och ESP som det föredragna mallsystemet i AEM.

|  |  |  |
|---|---|---|
| HTML - översikt | [HTML-översikt och -syntax](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) | Det här dokumentet beskriver vad HTML är, hur du går till HTML, ett exempelprojekt, syntax, uttryck och programsatser |
| Använda API i java | [HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | Med HTL Java Use-API:t kan en HTML-fil få åtkomst till hjälpmetoder i en anpassad Java-klass. |

>[!NOTE]
>
>Följande självstudiekurs i flera delar kan vara av intresse för den bästa metoden för att skapa ett nytt AEM-projekt, med information om kärnkomponenter, redigerbara mallar, klientbibliotek och komponentutveckling:
>[Komma igång med AEM Sites - självstudiekurs om WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)

