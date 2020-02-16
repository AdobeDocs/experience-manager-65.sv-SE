---
title: Administrera arbetsflödesinstanser
seo-title: Administrera arbetsflödesinstanser
description: Lär dig hur du administrerar arbetsflödesinstanser.
seo-description: Lär dig hur du administrerar arbetsflödesinstanser.
uuid: 81e53ef5-fe62-4ed4-b2d4-132aa986d5aa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d9c96e7f-9416-48e1-a6af-47384f7bee92
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Administrera arbetsflödesinstanser{#administering-workflow-instances}

Arbetsflödeskonsolen innehåller flera verktyg för att administrera arbetsflödesinstanser för att säkerställa att de körs som förväntat.

>[!NOTE]
>
>JMX- [konsolen](/help/sites-administering/jmx-console.md#workflow-maintenance) innehåller ytterligare underhållsåtgärder för arbetsflöden.

Det finns en rad konsoler som du kan använda för att administrera dina arbetsflöden. Använd den [globala navigeringen](/help/sites-authoring/basic-handling.md#global-navigation) för att öppna rutan **Verktyg** och välj sedan **Arbetsflöde**:

* **Modeller**: Hantera arbetsflödesdefinitioner
* **Instanser**: Visa och hantera pågående arbetsflödesinstanser
* **Startprogram**: Hantera hur arbetsflöden ska startas
* **Arkiv**: Visa historik över arbetsflöden som har slutförts
* **Fel**: Visa historik över arbetsflöden som slutförts med fel

## Övervaka status för arbetsflödesinstanser {#monitoring-the-status-of-workflow-instances}

1. Välj Navigering, välj **Verktyg** och sedan **Arbetsflöde**.
1. Markera **instanser** om du vill visa en lista över pågående arbetsflödesinstanser.

   ![wf-96](assets/wf-96.png)

1. Markera ett specifikt objekt och **öppna historik** för att se mer information:

   ![wf-97](assets/wf-97.png)

## Göra uppehåll, återuppta och avsluta en arbetsflödesinstans {#suspending-resuming-and-terminating-a-workflow-instance}

1. Välj Navigering, välj **Verktyg** och sedan **Arbetsflöde**.
1. Markera **instanser** om du vill visa en lista över pågående arbetsflödesinstanser.

   ![wf-96-1](assets/wf-96-1.png)

1. Välj ett specifikt objekt och använd sedan **Avsluta**, **Gör uppehåll** eller **Återuppta**, beroende på vad som är tillämpligt. bekräftelse och/eller ytterligare uppgifter krävs:

   ![wf-97-1](assets/wf-97-1.png)

## Visa arkiverade arbetsflöden {#viewing-archived-workflows}

1. Välj Navigering, välj **Verktyg** och sedan **Arbetsflöde**.
1. Välj **Arkiv** om du vill visa en lista över de arbetsflödesinstanser som har slutförts.

   ![wf-98](assets/wf-98.png)

   >[!NOTE]
   >
   >Avbruten status betraktas som en avslutad åtgärd eftersom den inträffar till följd av en användaråtgärd. till exempel:
   >
   >* användning av **åtgärden Avsluta** .
   >* när en sida, som är underställd ett arbetsflöde, tas bort (framtvingar), avslutas arbetsflödet


1. Markera ett specifikt objekt och **öppna historik** för att se mer information:

   ![wf-99](assets/wf-99.png)

## Åtgärdar fel i arbetsflödesinstansen {#fixing-workflow-instance-failures}

När ett arbetsflöde misslyckas tillhandahåller AEM konsolen **Fel** så att du kan undersöka och vidta lämpliga åtgärder när den ursprungliga orsaken har hanterats:

* **Felinformation**&#x200B;Öppnar ett fönster där **felmeddelandet**, **steget** och **felstacken** visas.

* **Öppna historik** Visar information om arbetsflödeshistoriken.

* **Försök stega** igen Kör komponentinstansen för skriptsteget igen. Använd kommandot Försök igen när du har åtgärdat orsaken till det ursprungliga felet. Du kan till exempel försöka utföra steget igen när du har åtgärdat ett fel i skriptet som utförs av processteget.
* **Avsluta** Avsluta arbetsflödet om felet har orsakat en oåterkallelig situation för arbetsflödet. Arbetsflödet kan t.ex. vara beroende av miljöförhållanden, t.ex. information i databasen som inte längre är giltig för arbetsflödesinstansen.
* **Avsluta och försök igen** Liknar **Avsluta** förutom att en ny arbetsflödesinstans startas med den ursprungliga nyttolasten, titeln och beskrivningen.

Så här undersöker du fel och sedan återupptar eller avslutar du arbetsflödet:

1. Välj Navigering, välj **Verktyg** och sedan **Arbetsflöde**.
1. Markera **Fel** om du vill visa en lista över arbetsflödesinstanser som inte slutfördes korrekt.
1. Välj ett specifikt objekt och sedan lämplig åtgärd:

   ![wf-47](assets/wf-47.png)

## Vanlig tömning av arbetsflödesinstanser {#regular-purging-of-workflow-instances}

Om du minimerar antalet arbetsflödesinstanser ökas arbetsflödesmotorns prestanda, så att du regelbundet kan rensa avslutade eller pågående arbetsflödesinstanser från databasen.

Konfigurera **Adobe Granite Workflow Renge Configuration** för att rensa arbetsflödesinstanser efter ålder och status. Du kan också rensa arbetsflödesinstanser av alla modeller eller av en viss modell.

Du kan också skapa flera konfigurationer av tjänsten för att rensa arbetsflödesinstanser som uppfyller olika villkor. Skapa till exempel en konfiguration som tömmer instanser av en viss arbetsflödesmodell när de körs mycket längre än förväntat. Skapa en annan konfiguration som tömmer alla slutförda arbetsflöden efter ett visst antal dagar för att minimera databasens storlek.

Om du vill konfigurera tjänsten kan du använda [webbkonsolen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) eller [lägga till en OSGi-konfiguration i databasen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). I följande tabell beskrivs de egenskaper som du behöver för någon av metoderna.

>[!NOTE]
>
>För att lägga till konfigurationen i databasen är tjänst-PID:
>
>`com.adobe.granite.workflow.purge.Scheduler`
>
>Eftersom tjänsten är en fabrikstjänst kräver nodens namn ett identifierarsuffix, till exempel: `sling:OsgiConfig`
>
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>Egenskapsnamn (webbkonsol)</th>
   <th>OSGi-egenskapsnamn</th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td>Jobbnamn</td>
   <td>schemalagd tömning.namn</td>
   <td>Ett beskrivande namn för den schemalagda rensningen.</td>
  </tr>
  <tr>
   <td>Arbetsflödesstatus</td>
   <td>schemalagd tömning.workflowStatus</td>
   <td><p>Status för de arbetsflödesinstanser som ska rensas. Följande värden är giltiga:</p>
    <ul>
     <li>SLUTFÖRT: Slutförda arbetsflödesinstanser rensas.</li>
     <li>KÖRS: Körande arbetsflödesinstanser rensas.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modeller att tömma</td>
   <td>schemalagd tömning.modelIds</td>
   <td><p>ID:t för arbetsflödesmodellerna som ska rensas. <br /> ID är sökvägen till modellnoden, till exempel: /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> Ange inget värde för att rensa instanser av alla arbetsflödesmodeller.</p> <p>Om du vill ange flera modeller klickar du på plusknappen (+) i webbkonsolen. </p> </td>
  </tr>
  <tr>
   <td>Arbetsflödesålder</td>
   <td>schemalagd tömning.dag såld</td>
   <td> Åldern på arbetsflödesinstanserna som ska rensas, i dagar.</td>
  </tr>
 </tbody>
</table>

## Ange maximal storlek för inkorgen {#setting-the-maximum-size-of-the-inbox}

Du kan ange den maximala storleken på inkorgen genom att konfigurera **Adobe Granite Workflow Service**, använda [webbkonsolen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) eller [lägga till en OSGi-konfiguration i databasen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). I följande tabell beskrivs egenskapen som du konfigurerar för båda metoderna.

>[!NOTE]
>
>För att lägga till konfigurationen i databasen är tjänst-PID:
>
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Egenskapsnamn (webbkonsol) | OSGi-egenskapsnamn |
|---|---|
| Max Inbox Query Size | granite.workflow.inboxQuerySize |

