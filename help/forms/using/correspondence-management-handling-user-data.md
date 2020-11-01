---
title: Korrespondenshantering | Hantera användardata
seo-title: Korrespondenshantering | Hantera användardata
description: Korrespondenshantering | Hantera användardata
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---


# Korrespondenshantering | Hantera användardata {#correspondence-management-handling-user-data}

Med AEM Forms Correspondence Management kan ni skapa, hantera och effektivisera säkra och personaliserade kundkorrespondenser. Det ger ett intuitivt användargränssnitt där företagsanvändare kan skapa korrespondens med hjälp av godkända innehållsblock och mediaelement. Mer information om hur du skapar korrespondenser finns i [Skapa korrespondens](/help/forms/using/create-correspondence.md).

När en affärsanvändare eller en agent sparar en korrespondens som utkast eller skickar den, sparas en bokstavsinstans i AEM. Bokstaven innehåller korrespondensdata och metadata.

>[!NOTE]
>
>I AEM 6.5 Forms är korrespondenshantering inte tillgänglig i paketet. Om du uppgraderar från en tidigare version av AEM Forms ska du installera kompatibilitetspaketet och migrera dina resurser för korrespondenshantering för att fortsätta använda dem i AEM 6.5 Forms. Mer information finns i [Kompatibilitetspaket](/help/forms/using/compatibility-package.md).

## Användardata och datalager {#data}

Korrespondenshantering lagrar data för utkast och skickade brev AEM databasen endast om publiceringsinstansen är konfigurerad för att hantera bokstavsinstanser. Mer information om konfigurationen finns i Konfigurationsegenskaper för [korrespondenshantering](/help/forms/using/cm-configuration-properties.md).

Beroende på den datalagringsbeständighet som har konfigurerats för din AEM-distribution lagras utkast och skickade korrespondensdata på följande platser.

<table>
 <tbody>
  <tr>
   <td><p><strong>Typ av beständighet</strong></p> </td>
   <td><p><strong>Datalager</strong></p> </td>
   <td><p><strong>Plats</strong></p> </td>
  </tr>
  <tr>
   <td><p>Standard</p> </td>
   <td><p>AEM för publiceringsinstans och författarinstanser som anges i konfigurationen för omvänd replikering</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td>
  </tr>
  <tr>
   <td><p>Fjärr</p> </td>
   <td><p>AEM databas för den fjärrbehandlande författarinstansen</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

I ovanstående AEM:

* `[yyyy]/[mm]/[dd]` är nodstrukturen baserad på det datum då bokstavsinstansen skapades
* `[node-id]` är det ID som tilldelats mappen som innehåller bokstaven
* `[letter-instance-name]` är namnet som anges när du sparar eller skickar ett brev

Under noden [letter-instance-name] skapas följande nodstruktur och data för varje bokstavsinstans lagras i AEM.

| Nod | Beskrivning |
|---|---|
| `extendedProperties` | Lagrar metadataegenskaper för bokstavsinstansen. |
| `dataXML` | Lagrar en nedladdningsbar dataXML-fil som innehåller korrespondensdata i binärt format. |
| `processedXDP` | Innehåller information om XDP-mallen som används för att skapa det skickade brevet. Den här noden skapas endast för skickade korrespondenser. |
| `submittedLetter` | Lagrar skickade bokstavsdata i hämtningsbart binärt format. Den här noden skapas endast för skickade korrespondenser. |

## Få åtkomst till och ta bort användardata {#access-and-delete-user-data}

Du kan få åtkomst till utkast och skickade korrespondensdata i de konfigurerade datalagret, och ta bort dem om det behövs.

### Åtkomst till användardata {#access-user-data}

Korrespondenshanteringen innehåller API:er som du kan använda för att hitta och komma åt utkast och skickade brev. Med API:erna kan du söka efter och öppna bokstavsinstanser med hjälp av bokstavsinstans-ID:t eller den användare som sparade eller skickade korrespondensen. Mer information finns i API: [er för att komma åt bokstavsinstanser](/help/forms/using/cm-apis-to-access-letter-instances.md).

Du kan också navigera till bokstavsinstansen i AEM med CRX DELite. Se [Användardata och datalager](/help/forms/using/correspondence-management-handling-user-data.md#data) för information om lagrade data och databasplats.

### Ta bort användardata {#delete-user-data}

Om du vill hitta en bokstavsinstans som innehåller data för en viss användare kan du:

* Använd API:er för korrespondenshantering om namnet på bokstavsinstansen eller användaren som sparade utkastet eller skickade korrespondensen är känt
* Använd AEM databassökning med personligt identifierbar information som e-post-ID eller namn för att hitta noden där informationen lagras

Om du vill ta bort användardata från utkast och skickade korrespondenser helt från AEM system måste du manuellt ta bort noden letter instance från alla tillämpliga AEM.
