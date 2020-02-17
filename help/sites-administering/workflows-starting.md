---
title: Starta arbetsflöden
seo-title: Starta arbetsflöden
description: Lär dig hur du startar arbetsflöden i AEM.
seo-description: Lär dig hur du startar arbetsflöden i AEM.
uuid: 0648d335-ecce-459d-95fd-3d4d76181b32
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: e9ab4796-a050-40de-b073-af7d33cff009
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Starta arbetsflöden{#starting-workflows}

När du administrerar arbetsflöden kan du starta dem på flera olika sätt:

* Manuellt:

   * Från en [arbetsflödesmodell](#workflow-models).
   * Använda ett arbetsflödespaket för [gruppbearbetning](#workflow-packages-for-batch-processing).

* Automatiskt:

   * Som svar på nodändringar, [med Launcher](#workflows-launchers).

>[!NOTE]
>
>Andra metoder är också tillgängliga för författare. Mer information finns i:
>
>* [Använda arbetsflöden på sidor](/help/sites-authoring/workflows-applying.md)
>* [Tillämpa arbetsflöden på DAM-resurser](/help/assets/assets-workflow.md)
>* [AEM-formulär](https://helpx.adobe.com/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [Översättningsprojekt](/help/sites-administering/tc-manage.md)
>



## Arbetsflödesmodeller {#workflow-models}

Du kan starta ett arbetsflöde [baserat på någon av modellerna](/help/sites-administering/workflows.md#workflow-models-and-instances) som visas i konsolen Arbetsflödesmodeller. Den enda obligatoriska informationen är nyttolasten, men du kan även lägga till en titel och/eller kommentar.

## Starta arbetsflöden {#workflows-launchers}

Workflow Launcher övervakar ändringar i innehållsdatabasen för att starta arbetsflöden beroende på platsen och resurstypen för den ändrade noden.

Med **Launcher** kan du:

* Se de arbetsflöden som redan har startats för specifika noder.
* Välj ett arbetsflöde som ska startas när en viss nod/nodtyp har skapats/ändrats/tagits bort.
* Ta bort en befintlig relation mellan arbetsflöde och nod.

En startfil kan skapas för alla noder. Ändringar av vissa noder startar dock inte arbetsflöden. Ändringar av noder under följande sökvägar leder inte till att arbetsflöden startar:

* `/var/workflow/instances`
* Alla arbetsflödesinkorgsnoder som finns var som helst i `/home/users` grenen
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * Undantag: Ändringar av noder nedan `/var/statistics/tracking`*leder* till att arbetsflöden startas.

Olika definitioner ingår i standardinstallationen. Dessa används för hantering av digitala resurser och samarbete i sociala medier:

![wf-100](assets/wf-100.png)

## Arbetsflödespaket för gruppbearbetning {#workflow-packages-for-batch-processing}

Arbetsflödespaket är paket som kan skickas till ett arbetsflöde som nyttolast för bearbetning, vilket gör att flera resurser kan bearbetas.

Ett arbetsflödespaket:

* innehåller länkar till en uppsättning resurser (till exempel sidor, resurser).
* innehåller paketinformation, t.ex. datum då paketet skapades, den användare som skapade paketet och en kort beskrivning.
* definieras med hjälp av en särskild sidmall, På sådana sidor kan användaren ange resurser i paketet.
* kan användas flera gånger.
* kan ändras av användaren (lägg till eller ta bort resurser) medan arbetsflödesinstansen körs.

## Starta ett arbetsflöde från Models Console {#starting-a-workflow-from-the-models-console}

1. Gå till **Models** Console med **Tools**, **Workflow** och sedan **Models**.
1. Välj arbetsflöde (enligt konsolvyn); Du kan också använda Sök (längst upp till vänster) om det behövs:

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >Indikatorn **[Övergående](/help/sites-developing/workflows.md#transient-workflows)**visar arbetsflöden där arbetsflödeshistoriken inte kommer att sparas.

1. Välj **Starta arbetsflöde** i verktygsfältet.
1. Dialogrutan Kör arbetsflöde öppnas och du kan ange:

   * **Nyttolast**

      Detta kan vara en sida, nod, resurs, paket, bland annat.

   * **Titel**

      En valfri titel som hjälper dig att identifiera den här instansen.

   * **Kommentar**

      En valfri kommentar som hjälper till att ange detaljer för den här instansen.
   ![wf-104](assets/wf-104.png)

## Skapa en startkonfiguration {#creating-a-launcher-configuration}

1. Gå till **Workflow Launchers** -konsolen med **Tools**, **Workflow** och sedan **Launcher**.
1. Välj **Skapa** och sedan **Lägg till startprogram** för att öppna dialogrutan:

   ![wf-105](assets/wf-105.png)

   * **Händelsetyp**

      Händelsetypen som startar arbetsflödet:

      * Skapad
      * Ändrad
      * Borttagen
   * **Notetype**

      Den typ av nod som arbetsflödets startprogram gäller för.

   * **Bana**

      Sökvägen som arbetsflödets startprogram gäller för.

   * **Körningsläge(n)**

      Den typ av server som arbetsflödets startprogram gäller för. Välj **Författare**, **Publicera** eller **Författare och publicera**.

   * **Villkor**

      En lista med villkor för nodvärden som, när de utvärderas, avgör om arbetsflödet startas. Följande villkor gör att arbetsflödet startar när noden har ett egenskapsnamn med värdet User:

      name==User

   * **Funktioner**

      En lista över funktioner som ska aktiveras. Välj önskad(a) funktion(er) i listrutan.

   * **Inaktiverade funktioner**
   En lista över funktioner som ska inaktiveras. Välj önskad(a) funktion(er) i listrutan.

   * **Arbetsflödesmodell**

      Det arbetsflöde som ska startas när händelsetypen inträffar på noden och/eller sökvägen under det definierade villkoret.

   * **Beskrivning**

      Din egen text som beskriver och identifierar startkonfigurationen.

   * **Aktivera**

      Anger om arbetsflödets startprogram är aktiverat:

      * Välj **Aktivera** för att starta arbetsflöden när konfigurationsegenskaperna är uppfyllda.
      * Välj **Inaktivera** när arbetsflödet inte ska köras (inte ens när konfigurationsegenskaperna är uppfyllda).
   * **Uteslut lista**

      Detta anger alla JCR-händelser som ska exkluderas (d.v.s. ignoreras) när du avgör om ett arbetsflöde ska utlösas.

      Den här startegenskapen är en kommaavgränsad lista med objekt: &quot;

      * `property-name` ignorera alla `jcr` händelser som utlöses för det angivna egenskapsnamnet. &quot;
      * `event-user-data:<*someValue*>` ignorerar alla händelser som innehåller `*<someValue*`> `user-data` -uppsättningen via [ API `ObservationManager`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String).
      Exempel:

      `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

      Den här funktionen kan användas för att ignorera ändringar som utlöses av en annan arbetsflödesprocess genom att lägga till exkluderingsobjektet:

      `event-user-data:changedByWorkflowProcess`





1. Välj **Skapa** för att skapa startprogrammet och återgå till konsolen.

   När en lämplig händelse inträffar aktiveras startprogrammet och arbetsflödet startas.

## Hantera en startkonfiguration {#managing-a-launcher-configuration}

När du har skapat startkonfigurationen kan du använda samma konsol för att markera instansen och sedan **Visa egenskaper** (och redigera dem) eller **Ta bort**.
