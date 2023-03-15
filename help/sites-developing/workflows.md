---
title: Utveckla och utöka arbetsflöden
seo-title: Developing and Extending Workflows
description: AEM innehåller flera verktyg och resurser för att skapa arbetsflödesmodeller, utveckla arbetsflödessteg och för att interagera programmatiskt med arbetsflöden
seo-description: AEM provides several tools and resources for creating workflow models, developing workflow steps, and for programmatically interacting with workflows
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
source-git-commit: 82b9b852fa3134f140f8de0bad229282979c8a30
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 0%

---


# Utveckla och utöka arbetsflöden{#developing-and-extending-workflows}

AEM innehåller flera verktyg och resurser för att skapa arbetsflödesmodeller, utveckla arbetsflödessteg och för programmässig interaktion med arbetsflöden.

Med arbetsflöden kan ni automatisera processer för hantering av resurser och publicering av innehåll i AEM. Arbetsflödena består av en serie steg där varje steg utför en viss uppgift. Du kan använda logik- och körtidsdata för att avgöra när en process kan fortsätta och välja nästa steg i ett av flera möjliga steg.

Affärsprocesserna för att skapa och publicera webbsidor innefattar till exempel att godkänna och godkänna av olika deltagare. Dessa processer kan utformas med hjälp AEM arbetsflöden och tillämpas på specifikt innehåll.

Nedan beskrivs de viktigaste aspekterna, medan följande sidor innehåller mer information:

* [Skapa arbetsflödesmodeller](/help/sites-developing/workflows-models.md)
* [Utöka arbetsflödesfunktioner](/help/sites-developing/workflows-customizing-extending.md)
* [Interagera med arbetsflöden programmatiskt](/help/sites-developing/workflows-program-interaction.md)
* [Referens för arbetsflödessteg](/help/sites-developing/workflows-step-ref.md)
* [Referens för arbetsflödesprocess](/help/sites-developing/workflows-process-ref.md)
* [Bästa praxis för arbetsflöden](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>Mer information om:
>
>* Delta i arbetsflöden, se [Använda arbetsflöden](/help/sites-authoring/workflows.md).
>* Administrera arbetsflöden och arbetsflödesinstanser, se [Administrera arbetsflöden](/help/sites-administering/workflows.md).
>* En artikel från början till slut finns på [Ändra digitala resurser med Adobe Experience Manager Workflows.](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)
>* Se [Fråga webbinariet AEM experter om arbetsflöden](https://bit.ly/ATACE218).
>* En artikel från början till slut finns på [Skapa ett anpassat steg för en dynamisk deltagare i Adobe Experience Manager 6.3](https://helpx.adobe.com/experience-manager/using/dynamic-steps-aem63.html).
>* Ändringar av informationsplatserna finns i [Omstrukturering av lager i AEM 6.5](/help/sites-deploying/repository-restructuring.md) och [Bästa praxis för arbetsflöden - platser](/help/sites-developing/workflows-best-practices.md#locations).
>


## Modell {#model}

A `WorkflowModel` representerar en definition (modell) av ett arbetsflöde. Den är gjord av `WorkflowNodes` och `WorkflowTransitions`. Övergångarna ansluter noderna och definierar *flöde*. Modellen har alltid en startnod och en slutnod.

### Körningsmodell {#runtime-model}

Arbetsflödesmodeller är versionshanterade. När du kör en arbetsflödesinstans används (och behålls) arbetsflödets körningsmodell (så som den är tillgänglig när arbetsflödet startades).

En körningsmodell är [genereras när **Synkronisera** aktiveras i arbetsflödesmodellredigeraren](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

Redigeringar av arbetsflödesmodellen som inträffar och/eller körningsmodeller som genereras, *efter* den specifika instansen som startades kommer inte att tillämpas på den instansen.

>[!CAUTION]
>
>Stegen som utförs är de som definieras av [körningsmodell](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model); detta genereras när **Synkronisera** åtgärden aktiveras i arbetsflödesmodellredigeraren.
>
>Om arbetsflödesmodellen ändras efter den här tidpunkten (utan **Synkronisera** aktiveras) kommer körningsinstansen inte att återspegla dessa ändringar. Det är bara körningsmodeller som genereras efter uppdateringen som återspeglar ändringarna. Undantagen är de underliggande ECMA-skripten, som sparas endast en gång så att ändringar görs.

### Steg {#step}

Varje steg ger en diskret uppgift. Det finns olika typer av arbetsflödessteg:

* Deltagare (användare/grupp): Dessa steg genererar ett arbetsobjekt och tilldelar det till en användare eller grupp. En användare måste slutföra arbetsuppgiften för att kunna gå vidare i arbetsflödet.
* Process (skript, Java-metodanrop): Dessa steg utförs automatiskt av systemet. Ett ECMA-skript eller en Java-klass implementerar steget. Tjänsterna kan utvecklas för att avlyssna särskilda arbetsflödeshändelser och utföra uppgifter enligt affärslogiken.
* Behållare (delarbetsflöde): Den här typen av steg startar en annan arbetsflödesmodell.
* ELLER Dela/förena: Använd logik för att bestämma vilket steg som ska köras härnäst i arbetsflödet.
* OCH Dela/förena: Tillåter att flera steg körs samtidigt.

Alla steg har följande gemensamma egenskaper: `Autoadvance` och `Timeout` varningar (skriptbara).

### Övergång {#transition}

A `WorkflowTransition` representerar en övergång mellan två `WorkflowNodes` av `WorkflowModel`.

* Den definierar länken mellan två på varandra följande steg.
* Det är möjligt att tillämpa regler.

### WorkItem {#workitem}

A `WorkItem` är den enhet som passeras genom en `Workflow` instans av en `WorkflowModel`. Den innehåller `WorkflowData` som instansen agerar på och en referens till `WorkflowNode` som beskriver det underliggande arbetsflödessteget.

* Den används för att identifiera uppgiften och placeras i respektive inkorg.
* En arbetsflödesinstans kan ha en eller flera `WorkItems` samtidigt (beroende på arbetsflödesmodell).
* The `WorkItem` refererar till arbetsflödesinstansen.
* I databasen är `WorkItem` lagras under arbetsflödesinstansen.

### Nyttolast {#payload}

Refererar till resursen som måste avanceras via ett arbetsflöde.

Nyttolastimplementeringen refererar till en resurs i databasen (via sökväg, UUID eller URL) eller av ett serialiserat java-objekt. Att referera till en resurs i databasen är mycket flexibelt och i kombination med en sling som är mycket produktiv. Den refererade noden kan till exempel återges som ett formulär.

### Livscykel {#lifecycle}

Skapas när ett nytt arbetsflöde startas (genom att respektive arbetsflödesmodell väljs och nyttolasten definieras) och avslutas när slutnoden bearbetas.

Följande åtgärder är möjliga för en arbetsflödesinstans:

* Avsluta
* Gör uppehåll
* Återuppta
* Starta om

Slutförda och avslutade instanser arkiveras.

### Inkorg {#inbox}

Varje användarkonto har en egen arbetsflödesinkorg där `WorkItems` är tillgängliga.

The `WorkItems` tilldelas antingen användarkontot direkt eller till den grupp som de tillhör.

### Arbetsflödestyper {#workflow-types}

Det finns olika typer av arbetsflöden som anges i konsolen Arbetsflödesmodeller:

![wf-upgrade-03](assets/wf-upgraded-03.png)

* **Standard**

   Det här är färdiga arbetsflöden som ingår i en AEM.

* Anpassade arbetsflöden (ingen indikator i konsolen)

   Det här är arbetsflöden som har skapats som nya eller från körklara arbetsflöden som har överlagrats med anpassningar.

* **Äldre**

   Arbetsflöden som skapats i en tidigare version av AEM. Dessa kan behållas under en uppgradering eller exporteras som ett arbetsflödespaket från den tidigare versionen och sedan importeras till den nya versionen.

### Övergående arbetsflöden {#transient-workflows}

Standardarbetsflöden sparar körningsinformation (historik) under körningen. Du kan också definiera en arbetsflödesmodell som **Övergående** för att undvika att sådan historik sparas. Detta används för prestandajustering eftersom det sparar/undviker den tid/de resurser som används för att lagra informationen.

Övergående arbetsflöden kan användas för alla arbetsflöden som:

* körs ofta.
* behöver inte arbetsflödeshistoriken.

Övergående arbetsflöden introducerades för inläsning av ett stort antal resurser, där resursinformationen är viktig, men inte arbetsflödets körningshistorik.

>[!NOTE]
>
>Se [Skapa ett tillfälligt arbetsflöde](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) för mer information.

>[!CAUTION]
>
>När en arbetsflödesmodell har flaggats som Transient finns det några scenarier när körningsinformationen fortfarande bevaras:
>
>* Nyttolasttypen (till exempel video) kräver externa steg för bearbetning. I sådana fall krävs körtidshistoriken för statusbekräftelse.
>* Arbetsflödet anger en **OCH dela**; I sådana fall krävs körtidshistoriken för statusbekräftelse.
>* När det tillfälliga arbetsflödet går in i ett deltagarsteg ändras läget (vid körning) till icke-tillfälligt. när aktiviteten skickas till en person måste historiken bevaras
>


>[!CAUTION]
>
>Inom ett tillfälligt arbetsflöde bör du inte använda en **Gå till steg**.
>
>Det här är **Gå till steg** skapar ett sling-jobb för att fortsätta arbetsflödet på `goto` punkt. Detta motverkar syftet att göra arbetsflödet övergående och genererar ett fel i loggfilen.
>
>Om du vill fatta beslut i ett tillfälligt arbetsflöde kan du använda **ELLER Dela**.

>[!NOTE]
>
>Se [Metodtips för Assets](/help/assets/performance-tuning-guidelines.md#transient-workflows) för mer information om hur Transient Workflows påverkar tillgångarnas prestanda.

### Stöd för flera resurser {#multi-resource-support}

Aktiverar **Stöd för flera resurser** för arbetsflödesmodellen innebär att en arbetsflödesinstans startas även när du väljer flera resurser, dessa bifogas som ett paket.

If **Stöd för flera resurser** är inte aktiverat för arbetsflödesmodellen och flera resurser har valts, kommer en enskild arbetsflödesinstans att startas för varje resurs.

>[!NOTE]
>
>Se [Konfigurera ett arbetsflöde för stöd för flera resurser](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) för mer information.

### Arbetsflödessteg {#workflow-stages}

Med arbetsflödesfaser kan du visualisera förloppet för ett arbetsflöde när du hanterar uppgifter. De kan användas för att ge en översikt över hur långt arbetsflödet är genom bearbetningen, som när arbetsflödet körs kan användaren visa förloppet som beskrivs i **Scen** (till skillnad från enskilda steg).

Eftersom namnen på de enskilda stegen kan vara specifika och tekniska, kan du definiera dem för att få en konceptuell vy över arbetsflödesförloppet.

För ett arbetsflöde med sex steg och fyra steg:

1. Du kan [konfigurera arbetsflödessteg (som visar arbetsflödets förlopp) och sedan tilldela rätt fas till varje steg i arbetsflödet](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * Du kan skapa flera scennamn.
   * Sedan tilldelas varje steg ett enskilt scennamn (ett scennamn kan tilldelas ett eller flera steg).

   | **Stegnamn** | **Scen (tilldelad till steget)** |
   |---|---|
   | Steg 1 | Skapa |
   | Steg 2 | Skapa |
   | Steg 3 | Granska |
   | Steg 4 | Godkänn |
   | Steg 5 | Slutförd |
   | Steg 6 | Slutförd |

1. När arbetsflödet körs kan användaren visa förloppet enligt scennamnen (i stället för stegnamnen). Arbetsflödets förlopp visas i [Fliken INFO FÖR ARBETSFLÖDE i aktivitetsinformationsfönstret för arbetsposten](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) som anges i [Inkorg](/help/sites-authoring/inbox.md).

### Arbetsflöden och Forms {#workflows-and-forms}

Vanligtvis används arbetsflöden för att bearbeta formulärinskickade formulär i AEM. Det här kan du göra med [grundkomponenterna](https://helpx.adobe.com/experience-manager/core-components/using/form-container.html) finns i en AEM eller med [AEM Forms](/help/forms/using/aem-forms-workflow.md).

När du skapar ett nytt formulär är det enkelt att koppla formulärinlämningen till en arbetsflödesmodell. t.ex. för att lagra innehållet på en viss plats i databasen eller för att meddela en användare om att formuläret har skickats in och dess innehåll.

### Arbetsflöden och översättning {#workflows-and-translation}

Arbetsflöden är också en viktig del av [Översättning](/help/sites-administering/translation.md) -processen.
