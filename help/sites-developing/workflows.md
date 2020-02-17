---
title: Utveckla och utöka arbetsflöden
seo-title: Utveckla och utöka arbetsflöden
description: AEM innehåller flera verktyg och resurser för att skapa arbetsflödesmodeller, utveckla arbetsflödessteg och för programmeringsinkoppling med arbetsflöden
seo-description: AEM innehåller flera verktyg och resurser för att skapa arbetsflödesmodeller, utveckla arbetsflödessteg och för programmeringsinkoppling med arbetsflöden
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# Utveckla och utöka arbetsflöden{#developing-and-extending-workflows}

AEM innehåller flera verktyg och resurser för att skapa arbetsflödesmodeller, utveckla arbetsflödessteg och för programmässig interaktion med arbetsflöden.

Med arbetsflöden kan ni automatisera processer för hantering av resurser och publicering av innehåll i AEM-miljön. Arbetsflödena består av en serie steg där varje steg utför en viss uppgift. Du kan använda logik- och körtidsdata för att avgöra när en process kan fortsätta och välja nästa steg i ett av flera möjliga steg.

Affärsprocesserna för att skapa och publicera webbsidor innefattar till exempel att godkänna och godkänna av olika deltagare. Dessa processer kan utformas med hjälp av AEM-arbetsflöden och tillämpas på specifikt innehåll.

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
>* En communityartikel från början till slut finns i [Ändra digitala resurser med hjälp av Adobe Experience Manager-arbetsflöden.](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)
>* Se [Ask the AEM Experts Webinar om arbetsflöden](https://bit.ly/ATACE218).
>* En communityartikel från början till slut finns i [Skapa ett anpassat steg](https://helpx.adobe.com/experience-manager/using/dynamic-steps-aem63.html)för dynamiska Adobe Experience Manager 6.3.
>* Ändringar av informationsplatserna finns i [Databasomstrukturering i AEM 6.5](/help/sites-deploying/repository-restructuring.md) och Bästa [arbetsflöden - platser](/help/sites-developing/workflows-best-practices.md#locations).
>



## Modell {#model}

En `WorkflowModel` representerar en definition (modell) av ett arbetsflöde. Den är gjord av `WorkflowNodes` och `WorkflowTransitions`. Övergångarna ansluter noderna och definierar *flödet*. Modellen har alltid en startnod och en slutnod.

### Körningsmodell {#runtime-model}

Arbetsflödesmodeller är versionshanterade. När du kör en arbetsflödesinstans används (och behålls) arbetsflödets körningsmodell (så som den är tillgänglig när arbetsflödet startades).

En körningsmodell [genereras när **Synkronisering** aktiveras i arbetsflödesmodellredigeraren](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

Redigeringar av arbetsflödesmodellen som inträffar och/eller körningsmodeller som genereras *efter* att den specifika instansen startades kommer inte att tillämpas på den instansen.

>[!CAUTION]
>
>Stegen som utförs är de som definieras av [körningsmodellen](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model). detta genereras när **synkroniseringsåtgärden** aktiveras i arbetsflödesmodellredigeraren.
>
>Om arbetsflödesmodellen ändras efter den här tidpunkten (utan att **Synkronisering** aktiveras) kommer körningsinstansen inte att återspegla dessa ändringar. Det är bara körningsmodeller som genereras efter uppdateringen som återspeglar ändringarna. Undantagen är de underliggande ECMA-skripten, som sparas endast en gång så att ändringar görs.

### Step {#step}

Varje steg ger en diskret uppgift. Det finns olika typer av arbetsflödessteg:

* Deltagare (användare/grupp): Dessa steg genererar ett arbetsobjekt och tilldelar det till en användare eller grupp. En användare måste slutföra arbetsuppgiften för att kunna gå vidare i arbetsflödet.
* Process (skript, Java-metodanrop): Dessa steg utförs automatiskt av systemet. Ett ECMA-skript eller en Java-klass implementerar steget. Tjänsterna kan utvecklas för att avlyssna särskilda arbetsflödeshändelser och utföra uppgifter enligt affärslogiken.
* Behållare (delarbetsflöde): Den här typen av steg startar en annan arbetsflödesmodell.
* ELLER Dela/förena: Använd logik för att bestämma vilket steg som ska köras härnäst i arbetsflödet.
* OCH Dela/förena: Tillåter att flera steg körs samtidigt.

Alla steg har följande gemensamma egenskaper: `Autoadvance` och `Timeout` varningar (skriptbara).

### Övergång {#transition}

En `WorkflowTransition` representerar en övergång mellan två `WorkflowNodes` av en `WorkflowModel`.

* Den definierar länken mellan två på varandra följande steg.
* Det är möjligt att tillämpa regler.

### WorkItem {#workitem}

A `WorkItem` är den enhet som skickas genom en `Workflow` instans av en `WorkflowModel`. Den innehåller `WorkflowData` det som instansen agerar på och en referens till det `WorkflowNode` som beskriver det underliggande arbetsflödessteget.

* Den används för att identifiera uppgiften och placeras i respektive inkorg.
* En arbetsflödesinstans kan ha en eller flera `WorkItems` samtidigt (beroende på arbetsflödesmodellen).
* Referensen `WorkItem` till arbetsflödesinstansen.
* I databasen `WorkItem` lagras arbetsflödesinstansen nedanför.

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

Varje användarkonto har en egen arbetsflödesinkorg där det tilldelade `WorkItems` är tillgängligt.

De `WorkItems` tilldelas antingen användarkontot direkt eller till gruppen som de tillhör.

### Arbetsflödestyper {#workflow-types}

Det finns olika typer av arbetsflöden som anges i konsolen Arbetsflödesmodeller:

![wf-upgrade-03](assets/wf-upgraded-03.png)

* **Standard**

   Det här är färdiga arbetsflöden som ingår i en standard-AEM-instans.

* Anpassade arbetsflöden (ingen indikator i konsolen)

   Det här är arbetsflöden som har skapats som nya eller från körklara arbetsflöden som har överlagrats med anpassningar.

* **Äldre**

   Arbetsflöden som skapats i en tidigare version av AEM. Dessa kan behållas under en uppgradering eller exporteras som ett arbetsflödespaket från den tidigare versionen och sedan importeras till den nya versionen.

### Övergående arbetsflöden {#transient-workflows}

Standardarbetsflöden sparar körningsinformation (historik) under körningen. Du kan också definiera en arbetsflödesmodell som **Transient** för att undvika att sådan historik sparas. Detta används för prestandajustering eftersom det sparar/undviker den tid/de resurser som används för att lagra informationen.

Övergående arbetsflöden kan användas för alla arbetsflöden som:

* körs ofta.
* behöver inte arbetsflödeshistoriken.

Övergående arbetsflöden introducerades för inläsning av ett stort antal resurser, där resursinformationen är viktig, men inte arbetsflödets körningshistorik.

>[!NOTE]
>
>Mer information finns i [Skapa ett tillfälligt arbetsflöde](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) .

>[!CAUTION]
>
>När en arbetsflödesmodell har flaggats som Transient finns det några scenarier när körningsinformationen fortfarande bevaras:
>
>* Nyttolasttypen (till exempel video) kräver externa steg för bearbetning. I sådana fall krävs körtidshistoriken för statusbekräftelse.
>* Arbetsflödet går in i en **AND-delning**. I sådana fall krävs körtidshistoriken för statusbekräftelse.
>* När det tillfälliga arbetsflödet går in i ett deltagarsteg ändras läget (vid körning) till icke-tillfälligt. när aktiviteten skickas till en person måste historiken bevaras
>



>[!CAUTION]
>
>Inom ett tillfälligt arbetsflöde bör du inte använda ett **Gå till-steg**.
>
>Detta är som **Gå till steg** skapar ett sling-jobb för att fortsätta arbetsflödet vid `goto` punkten. Detta motverkar syftet att göra arbetsflödet övergående och genererar ett fel i loggfilen.
>
>Om du vill fatta beslut i ett tillfälligt arbetsflöde kan du använda **ELLER Dela**.

>[!NOTE]
>
>Se [Bästa metoder för resurser](/help/assets/performance-tuning-guidelines.md#transient-workflows) för mer information om hur Transient Workflows påverkar tillgångarnas prestanda.

### Stöd för flera resurser {#multi-resource-support}

Att aktivera **Multi Resource Support** för arbetsflödesmodellen innebär att en enda arbetsflödesinstans kommer att startas även när du väljer flera resurser. dessa bifogas som ett paket.

Om **Multi Resource Support** inte är aktiverat för arbetsflödesmodellen och flera resurser har valts, kommer en enskild arbetsflödesinstans att startas för varje resurs.

>[!NOTE]
>
>Mer information finns i [Konfigurera ett arbetsflöde för stöd](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) för flera resurser.

### Arbetsflödessteg {#workflow-stages}

Med arbetsflödesfaser kan du visualisera förloppet för ett arbetsflöde när du hanterar uppgifter. De kan användas för att ge en översikt över hur långt arbetsflödet är genom bearbetningen, som när arbetsflödet körs, så att användaren kan visa förloppet som beskrivs av **scenen** (till skillnad från enskilda steg).

Eftersom namnen på de enskilda stegen kan vara specifika och tekniska, kan du definiera dem för att få en konceptuell vy över arbetsflödesförloppet.

För ett arbetsflöde med sex steg och fyra steg:

1. Du kan [konfigurera arbetsflödessteg (som visar arbetsflödets förlopp) och sedan tilldela rätt steg till varje steg i arbetsflödet](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

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

1. När arbetsflödet körs kan användaren visa förloppet enligt scennamnen (i stället för stegnamnen). Arbetsflödets förlopp visas på fliken [ARBETSFLÖDESINFO i fönstret med uppgiftsinformation för arbetsposten](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) som visas i [Inkorgen](/help/sites-authoring/inbox.md).

### Arbetsflöden och formulär {#workflows-and-forms}

Vanligtvis används arbetsflöden för att bearbeta formulärinskickade formulär i AEM. Detta kan vara fallet med [kärnkomponenterna](https://helpx.adobe.com/experience-manager/core-components/using/form-container.html) som finns i en AEM-standardinstans eller med [AEM Forms-lösningen](/help/forms/using/aem-forms-workflow.md).

När du skapar ett nytt formulär är det enkelt att koppla formulärinlämningen till en arbetsflödesmodell. t.ex. för att lagra innehållet på en viss plats i databasen eller för att meddela en användare om att formuläret har skickats in och dess innehåll.

### Arbetsflöden och översättning {#workflows-and-translation}

Arbetsflöden är också en viktig del av [översättningsprocessen](/help/sites-administering/translation.md) .
