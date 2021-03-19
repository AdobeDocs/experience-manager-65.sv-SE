---
title: Referens för arbetsflödessteg
seo-title: Referens för arbetsflödessteg
description: Referens för arbetsflödessteg
seo-description: 'null'
uuid: 88bf6997-73a1-4639-82aa-5dff08d3ef86
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e3afffd0-d90c-4bd0-b814-f7aeac6ceb6d
docset: aem65
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3288'
ht-degree: 0%

---


# Referens för arbetsflödessteg {#workflow-step-reference}

Arbetsflödesmodeller består av en serie steg av olika typer. Beroende på typ kan dessa steg konfigureras och utökas med parametrar och skript för att ge den funktionalitet och kontroll som du behöver.

>[!NOTE]
>
>I det här avsnittet beskrivs de vanliga arbetsflödesstegen.
>
>För modulspecifika steg, se även:
>
>* [AEM Forms Workflow Step Reference](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [Bearbeta resurser med mediehanterare och arbetsflöden](/help/assets/media-handlers.md)

>



## Stegegenskaper {#step-properties}

Varje stegkomponent har en **Stegegenskaper**-dialogruta där du kan definiera och redigera nödvändiga egenskaper.

### Stegegenskaper - fliken Allmänt {#step-properties-common-tab}

En kombination av följande egenskaper är tillgängliga för de flesta arbetsflödesstegkomponenter på fliken **Allmänt** i dialogrutan Egenskaper:

* ****
TitelStegets titel.

* **Beskrivning**
En beskrivning av steget.

* **Arbetsflödesfas**

   En nedrullningsbar väljare som använder en [scen](/help/sites-developing/workflows.md#workflow-stages) på steget.

* **Timeout**

   Den period efter vilken steget&quot;har gått ut&quot;.
Du kan välja mellan: **Av**, **Omedelbar**, **1h**, **6h**, **12h**, **24h**.

* **Timeout-hanterare**

   Den hanterare som ska styra arbetsflödet när steget går ut; till exempel:
   `Auto Advancer`

* **Avancerad hanterare**

   Välj det här alternativet om du vill att arbetsflödet automatiskt ska gå vidare till nästa steg efter körningen. Om du inte väljer det här alternativet måste implementeringsskriptet hantera arbetsflödets utveckling.

### Stegegenskaper - fliken Användare/grupp {#step-properties-user-group-tab}

Följande egenskaper är tillgängliga för många arbetsflödesstegkomponenter på fliken **Användare/grupp** i dialogrutan Egenskaper:

* **Meddela användare via e-post**

   * Du kan meddela deltagare genom att skicka ett e-postmeddelande när arbetsflödet når steget.
   * Om det här alternativet är aktiverat skickas ett e-postmeddelande till den användare som definieras av egenskapen **Användare/grupp** eller till varje medlem i gruppen om en grupp har definierats.

* **Användare/grupp**

   * I en listruta kan du navigera och välja en användare eller grupp.
   * Om du tilldelar ett steg till en viss användare kan bara den här användaren utföra en åtgärd på steget.
   * Om du tilldelar steget till en hel grupp kommer alla användare i gruppen att få åtgärden i sin **Inkorg för arbetsflöde** när arbetsflödet når det här steget.
   * Mer information finns i [Delta i arbetsflöden](/help/sites-authoring/workflows-participating.md).

## OCH dela {#and-split}

Med **AND Split** skapas en delning i arbetsflödet, varefter båda grenarna blir aktiva. Du kan lägga till arbetsflödessteg i varje gren efter behov. I det här steget kan du införa flera bearbetningssökvägar i arbetsflödet. Du kan t.ex. tillåta att vissa granskningssteg utförs parallellt, vilket sparar tid.

![wf-26](assets/wf-26.png)

### AND Split - Configuration {#and-split-configuration}

Så här konfigurerar du delningen:

* Redigera **OCH Dela egenskaper**:

   * **Delningsnamn**: tilldela ett namn i förklarande syfte
   * Ange antalet filialer som krävs. 2, 3, 4 eller 5.

* Lägg till arbetsflödessteg i grenarna efter behov.

   ![wf-27](assets/wf-27.png)

## Behållarsteg {#container-step}

Ett behållarsteg startar en annan arbetsflödesmodell som körs som ett underordnat arbetsflöde.

Med den här behållaren kan du återanvända arbetsflödesmodeller för att implementera vanliga stegsekvenser. En arbetsflödesmodell för översättning kan till exempel användas i flera redigeringsarbetsflöden.

![wf-28](assets/wf-28.png)

### Behållarsteg - konfiguration {#container-step-configuration}

Om du vill konfigurera steget redigerar du och använder följande flikar:

* [Vanliga](#step-properties-common-tab)
* **Behållare**

   * **Delarbetsflöde**: Välj arbetsflödet som ska startas.

## Gå till steg {#goto-step}

Med **Gå till steg** kan du ange nästa steg som ska köras i arbetsflödesmodellen. Du kan ange en regeldefinition, ett externt skript eller ett ECMA-skript som routningsuttryck för att utvärdera nästa steg för arbetsflödesmodellen.

* Om villkoret som du anger är true slutförs **Gå till steg** och arbetsflödesmotorn kör det angivna steget.
* Om villkoret som du anger inte innehåller true slutförs **Gå till steg** och den normala routningslogiken bestämmer nästa steg som ska köras.

Med **Gå till steg** kan du implementera avancerade routningsstrukturer i dina arbetsflödesmodeller. Om du till exempel vill implementera en slinga kan du definiera **Gå till steg** för att köra ett föregående steg i arbetsflödet, där routningsuttrycket utvärderar ett slingvillkor.

### Gå till steg - konfiguration {#goto-step-configuration}

Om du vill konfigurera steget redigerar du och använder följande flikar:

* [Vanliga](#step-properties-common-tab)
* **Process**

   * **Målsteg**: Välj det steg som ska köras när villkoret för routningsuttrycket har utvärderats.
   * **Routningsuttryck**: Välj Regeldefinition, Externt skript eller ett ECMA-skript som avgör om  **målsteget** ska köras.

      * **Regeldefinition:** Använd  [uttrycksredigeraren ](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) för att definiera regeln.
      * **Externt skript:** Det externa skriptets sökväg.
      * **ECMA-skript**: Skriptet som avgör om  **Gå till steg** ska köras.

#### Simulera en for-slinga {#simulating-a-for-loop}

När du simulerar en for-slinga måste du behålla antalet upprepningar av slingor som har inträffat:

* Antalet representerar vanligtvis ett index med objekt som hanteras i arbetsflödet.
* Antalet utvärderas som avslutningskriterier för slingan.

Om du till exempel vill implementera ett arbetsflöde som utför en åtgärd på flera JCR-noder kan du använda en loopräknare som index för noderna. Om du vill behålla antalet lagrar du ett `integer`-värde i datamappningen för arbetsflödesinstansen. Använd skriptet för **Gå till steg** för att öka antalet samt jämföra antalet med avslutningskriterierna.

```
function check(){
   var count=0;
   var keyname="loopcount"
   try{
      if (workflowData.getMetaDataMap().containsKey(keyname)){
        log.info("goto script: found loopcount key");
        count= parseInt(workflowData.getMetaDataMap().get(keyname))+1;
      }

     workflowData.getMetaDataMap().put(keyname,count);

     }catch(err) {
         log.info(err.message);
         return false;
    }
   if (parseInt(count) <7){
       return true;
   } else {
      return false;
   }
}
```

### Simulera en for-slinga med regeldefinitionen {#simulateforloop}

Du kan också simulera en for-slinga med hjälp av Regeldefinition som routningsuttryck. [Skapa en  **** ](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) talvariabel av datatypen Long. Använd **Uttryck** som mappningsläge i steget **[Ange variabel](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)** för att ange värdet för variabeln **count** till **count + 1** för varje körning av steget **Ange variabel**.

![Simulera en for-slinga](assets/variable_use_case_count_new.png)

I **Gå till steg** använder du **Ange variabel** som **målsteg** och **antal &lt; 5** som routningsuttryck.

![Villkor för simulering av en for-slinga](assets/variable_use_case_count1_new.png)

Steget **Ange variabel** körs upprepade gånger och värdet **count** variabel ökas med 1 för varje körning tills värdet når 5.

## ELLER Dela {#or-split}

Med **OR Split** skapas en delning i arbetsflödet, varefter endast en gren är aktiv. I det här steget kan du lägga in sökvägar för villkorlig bearbetning i arbetsflödet. Du kan lägga till arbetsflödessteg i varje gren efter behov.

>[!NOTE]
>
>Mer information om hur du skapar en OR-delning finns i: [https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html](https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html)

![Förgreningar med ELLER Dela](assets/variables_orsplit_new.png)

### ELLER Dela - konfiguration {#or-split-configuration}

Så här konfigurerar du delningen:

* Redigera **ELLER Dela egenskaper**:

   * **Vanliga**

      * Ange delningsnamnet.
   * **Förgreningar (*x)***

      * **Lägg till grenar:** Lägg till fler grenar i steget.
      * **Välj routningsuttryck**: Välj det routningsuttryck som ska utvärdera den aktiva grenen. Möjliga värden är: Regeldefinition, Externt skript och ECMA-skript.
      * **Klicka för att lägga till uttryck**: Lägg till uttryck för att utvärdera den aktiva grenen om du väljer  **Regeldefinitioner** som routningsuttryck.
      * **Skriptsökväg**: Sökvägen till en fil som innehåller skriptet som ska utvärdera den aktiva grenen om du väljer  **Externa** skript som routningsuttryck.
      * **Skript**: Lägg till skriptet i rutan för att utvärdera den aktiva grenen om du väljer  **ECMA** Scriptas som routningsuttryck.
      * **Standardflöde**: Standardförgreningen följs om det finns flera förgreningar. Du kan bara ange en gren som standard.

   >[!NOTE]
   >
   >    * En gren utvärderas i taget baserat på routningsuttrycket.
   >    * Förgreningarna utvärderas uppifrån och ned.
   >    * Det första skriptet som utvärderas till true körs.
   >    * Om ingen gren utvärderas till true, går arbetsflödet inte framåt.


   >[!NOTE]
   >
   >Se [Definiera en regel för en OR-delning](/help/sites-developing/workflows-models.md#defineruleecmascript).

* Lägg till arbetsflödessteg i grenarna efter behov.

## Deltagarsteg och väljare {#participant-steps-and-choosers}

### Deltagarsteg {#participant-step}

Med ett **deltagarsteg** kan du tilldela ägarskap för en viss åtgärd. Arbetsflödet fortsätter bara när användaren har bekräftat steget manuellt. Detta används när du vill att någon ska vidta en åtgärd i arbetsflödet; till exempel ett granskningssteg.

Även om det inte är direkt relaterat måste användarauktorisering beaktas när en åtgärd tilldelas. användaren måste ha åtkomst till sidan som är arbetsflödets nyttolast.

#### Deltagarsteg - konfiguration {#participant-step-configuration}

Om du vill konfigurera steget redigerar du och använder följande flikar:

* [Vanliga](#step-properties-common-tab)
* [Användare/grupp](#step-properties-user-group-tab)

>[!NOTE]
>
>Arbetsflödesinitieraren meddelas alltid när:
>
>* Arbetsflödet är slutfört (färdigt).
>* Arbetsflödet avbryts (avslutas).

>



>[!NOTE]
>
>Vissa egenskaper måste konfigureras för att e-postmeddelanden ska kunna aktiveras. Du kan också anpassa e-postmallen eller lägga till en e-postmall för ett nytt språk. Se [Konfigurera e-postmeddelanden](/help/sites-administering/notification.md#configuringemailnotification) för att konfigurera e-postmeddelanden i AEM.

### Steg {#dialog-participant-step} för dialogdeltagare

Använd ett **dialogdeltagarsteg** för att samla in information från användaren som är tilldelad arbetsposten. Det här steget är användbart när du vill samla in små mängder data som används senare i arbetsflödet.

När du är klar med steget innehåller dialogrutan **Fullständigt arbetsobjekt** de fält som du definierar i dialogrutan. De data som samlas in i fälten lagras i noder i arbetsflödets nyttolast. Efterföljande arbetsflödessteg kan sedan läsa värdet från databasen.

Om du vill konfigurera steget anger du vilken grupp eller användare som arbetsposten ska tilldelas till och sökvägen till dialogrutan.

#### Steg för dialogdeltagare - konfiguration {#dialog-participant-step-configuration}

Om du vill konfigurera steget redigerar du och använder följande flikar:

* [Vanliga](#step-properties-common-tab)
* [Användare/grupp](#step-properties-user-group-tab)
* **Dialog**

   * **Dialogrutans sökväg**: Sökvägen till dialognoden i den  [dialogruta som du skapar](#dialog-participant-step-creating-a-dialog).

#### Steg för dialogdeltagare - Skapa en dialogruta {#dialog-participant-step-creating-a-dialog}

Om du vill skapa en dialogruta måste du skapa den:

* Bestäm var de resulterande data ska sparas i nyttolasten](#dialog-participant-step-storing-data-in-the-payload).[
* [Definiera dialogrutan. Detta innefattar att definiera de fält som används för att samla in (och spara) data](#dialog-participant-step-dialog-definition).

#### Steg för dialogdeltagare - lagra data i nyttolasten {#dialog-participant-step-storing-data-in-the-payload}

Du kan lagra widgetdata i arbetsflödets nyttolast eller i arbetsobjektets metadata. Formatet på egenskapen `name` för widgetnoden avgör var data lagras.

* **Lagra data med nyttolasten**

   * Om du vill lagra widgetdata som en egenskap för arbetsflödets nyttolast använder du följande format för värdet för namnegenskapen för widgetnoden:
      `./jcr:content/nodename`

   * Data lagras i egenskapen `nodename` för nyttolastnoden. Om noden inte innehåller den egenskapen skapas egenskapen.
   * När den lagras med nyttolasten skriver efterföljande användning av dialogrutan med samma nyttolast över egenskapens värde.

* **Lagra data med arbetsobjektet**

   * Om du vill lagra widgetdata som en egenskap för arbetsobjektets metadata använder du följande format för värdet för egenskapen name:
      `nodename`

   * Data lagras i egenskapen `nodename` för arbetsobjektet `metadata`. Data bevaras om dialogrutan sedan används med samma nyttolast.

#### Steg för dialogdeltagare - Dialogrutedefinition {#dialog-participant-step-dialog-definition}

1. **Dialogrutans struktur**

   Dialogrutorna för Dialog Deltagare-steg liknar dialogrutor som du skapar för redigeringskomponenter. De lagras under:

   `/apps/myapp/workflow/dialogs`

   Dialogrutor för det pekaktiverade standardgränssnittet har följande nodstruktur:

   ```xml
   newComponent (cq:Component)
     |- cq:dialog (nt:unstructured)
       |- content
         |- layout
           |- items
             |- column
               |- items
                 |- component0
                 |- component1
                 |- ...
   ```

   >[!NOTE]
   >
   >Mer information finns i [Skapa och konfigurera en dialogruta](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog).

1. **Dialogrutans sökvägsegenskap**

   **Dialogdeltagarsteget** har egenskapen **Dialogsökväg** (tillsammans med egenskaperna för ett [deltagarsteg](#participant-step)). Värdet för egenskapen **Dialogsökväg** är sökvägen till noden `dialog` i dialogrutan.

   Dialogrutan finns till exempel i en komponent med namnet `EmailWatch` som lagras i noden:

   `/apps/myapp/workflows/dialogs`

   För det beröringsaktiverade användargränssnittet används följande värde för egenskapen **Dialog Path**:

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **Exempeldialogrutedefinition**

   Följande XML-kodfragment representerar en dialogruta som lagrar ett `String`-värde i `watchEmail`-noden för nyttolastinnehållet. Titelnoden representerar komponenten [TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html):

   ```xml
   jcr:primaryType="nt:unstructured"
       jcr:title="Watcher Email Address Dialog"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/foundation/container">
           <layout jcr:primaryType="nt:unstructured"
               margin="false"
               sling:resourceType="granite/ui/components/foundation/layouts/fixedcolumns"
           />
           <items jcr:primaryType="nt:unstructured">
               <column jcr:primaryType="nt:unstructured"
                   sling:resourceType="granite/ui/components/foundation/container">
                   <items jcr:primaryType="nt:unstructured">
                       <title jcr:primaryType="nt:unstructured"
                           fieldLabel="Notification Email Address"
                           name="./jcr:content/watchEmails"
                           sling:resourceType="granite/ui/components/foundation/form/textfield"
                       />
                   </items>
               </column>
           </items>
       </content>
   </cq:dialog>
   ```

   Det här exemplet kommer, när det gäller det beröringskänsliga användargränssnittet, att resultera i en dialogruta som:

   ![chlimage_1-70](assets/chlimage_1-70.png)

### Steg för dynamisk deltagare {#dynamic-participant-step}

Komponenten **Dynamiskt deltagarsteg** liknar **[Deltagarsteg](#participant-step)** med skillnaden att deltagaren väljs automatiskt vid körning.

Om du vill konfigurera steget väljer du en **deltagarväljare** som identifierar deltagaren som arbetsposten ska tilldelas till, tillsammans med en dialogruta.

#### Dynamiskt deltagarsteg - konfiguration {#dynamic-participant-step-configuration}

Om du vill konfigurera steget redigerar du och använder följande flikar:

* [Vanliga](#step-properties-common-tab)
* **Väljare för deltagare**

   * **Väljare**: Namnet på den  [deltagarväljare som du skapar](#developingtheparticipantchooser).
   * **Argument**: Alla obligatoriska argument.
   * **E-post**: Anger om ett e-postmeddelande ska skickas till användaren.

* **Dialog**

   * **Dialogrutans sökväg**: Sökvägen till dialognoden i den  [dialogruta som du skapar (som med steget **för** dialogdeltagare)](#dialog-participant-step-creating-a-dialog).

#### Steg för dynamisk deltagare - Utveckla deltagarväljaren {#dynamic-participant-step-developing-the-participant-chooser}

Du skapar deltagarväljaren. Därför kan du använda valfri urvalslogik eller valfria villkor. Din deltagarväljare kan t.ex. välja den användare (i en grupp) som har minst arbetsobjekt. Du kan skapa valfritt antal deltagare som du kan använda med olika instanser av komponenten **Dynamic Participant Step** i arbetsflödesmodellerna.

Skapa en OSGi-tjänst eller ett ECMAScript-skript som väljer en användare att tilldela arbetsposten till.

* **ECMAscript**

   Skript måste innehålla en funktion med namnet getParticipant som returnerar ett användar-ID som `String`-värde. Lagra dina egna skript i till exempel mappen `/apps/myapp/workflow/scripts` eller en undermapp.

   Ett exempelskript ingår i en AEM standardinstans:

   `/libs/workflow/scripts/initiator-participant-chooser.ecma`

   >[!CAUTION]
   >
   >Du ***får*** inte ändra något i `/libs`-sökvägen.
   >
   >
   >Detta beror på att innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan skrivas över när du använder en snabbkorrigering eller ett funktionspaket).

   Det här skriptet väljer arbetsflödesinitieraren som deltagare:

   ```
   function getParticipant() {
       return workItem.getWorkflow().getInitiator();
   }
   ```

   >[!NOTE]
   >
   >**Deltagarväljaren för arbetsflödesinitieraren** utökar **steget för den dynamiska deltagaren** och använder det här skriptet som stegimplementering.

* **OSGi-tjänst**

   Tjänsterna måste implementera gränssnittet [com.day.cq.workflow.exec.ParticipantStepChooser](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html). Gränssnittet definierar följande medlemmar:

   * `SERVICE_PROPERTY_LABEL` fält: Använd det här fältet för att ange namnet på deltagarväljaren. Namnet visas i en lista över tillgängliga deltagarval i egenskaperna **Dynamiskt deltagarsteg**.

   * `getParticipant` metod: Returnerar det dynamiskt lösta huvud-ID:t som ett  `String` värde.
   >[!CAUTION]
   >
   >Metoden `getParticipant` returnerar det dynamiskt matchade huvud-ID:t. Detta kan vara ett grupp-ID eller användar-ID.
   >
   >
   >Ett grupp-ID kan dock bara användas för ett **deltagarsteg** när en lista över deltagare returneras. För ett **dynamiskt deltagarsteg** returneras en tom lista som inte kan användas för delegering.

   Om du vill göra implementeringen tillgänglig för **komponenter för dynamisk deltagare, steg**, lägger du till din Java-klass i ett OSGi-paket som exporterar tjänsten och distribuerar paketet till AEM.

   >[!NOTE]
   >
   >**Random Participant** Chooserär en exempeltjänst som väljer en slumpmässig användare (  `com.day.cq.workflow.impl.process.RandomParticipantChooser`). **Stickprovet Välj slumpmässig deltagare** r för stegkomponenten utökar **steget för den dynamiska deltagaren** och använder den här tjänsten som stegimplementering.

#### Dynamiskt deltagarsteg - Exempel på deltagarväljartjänst {#dynamic-participant-step-example-participant-chooser-service}

Följande Java-klass implementerar gränssnittet `ParticipantStepChooser`. Klassen returnerar namnet på deltagaren som initierade arbetsflödet. Koden använder samma logik som exempelskriptet (`initiator-participant-chooser.ecma`) använder.

`@Property`-anteckningen ställer in värdet för fältet `SERVICE_PROPERTY_LABEL` till `Workflow Initiator Participant Chooser`.

```java
package com.adobe.example;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.osgi.framework.Constants;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.ParticipantStepChooser;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;

@Component
@Service
@Properties({
        @Property(name = Constants.SERVICE_DESCRIPTION, value = "An example implementation of a dynamic participant chooser."),
        @Property(name = ParticipantStepChooser.SERVICE_PROPERTY_LABEL, value = "Workflow Initiator Participant Chooser (service)") })
public class InitiatorParticipantChooser implements ParticipantStepChooser {

 private Logger logger = LoggerFactory.getLogger(this.getClass());

 public String getParticipant(WorkItem arg0, WorkflowSession arg1,
   MetaDataMap arg2) throws WorkflowException {

  String initiator = arg0.getWorkflow().getInitiator();
  logger.info("Assigning Dynamic Participant Step work item to {}",initiator);

  return initiator;
 }
}
```

I dialogrutan **Dynamiskt deltagarsteg**-egenskaper innehåller listan **Deltagarväljare** objektet `Workflow Initiator Participant Chooser (script)`, som representerar den här tjänsten.

När arbetsflödesmodellen startas anger loggen ID:t för användaren som initierade arbetsflödet och vem som tilldelats arbetsposten. I det här exemplet startade `admin`-användaren arbetsflödet.

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### Formulärdeltagarsteg {#form-participant-step}

**Formulärdeltagarsteget** visar ett formulär när arbetsobjektet öppnas. När användaren fyller i och skickar formuläret lagras fältdata i noderna i arbetsflödets nyttolast.

Om du vill konfigurera steget anger du vilken grupp eller användare som arbetsposten ska tilldelas till och sökvägen till formuläret.

>[!CAUTION]
>
>I det här avsnittet behandlas [Forms-delen av Foundation Components för sidredigering](/help/sites-authoring/default-components-foundation.md#form).

#### Steg för formulärdeltagare - konfiguration {#form-participant-step-configuration}

Om du vill konfigurera steget redigerar du och använder följande flikar:

* [Vanliga](#step-properties-common-tab)
* [Användare/grupp](#step-properties-user-group-tab)
* **Formulär**

   * **Formulärsökväg**: Sökvägen till det  [formulär du skapar](#form-participant-step-creating-the-form).

#### Steg för formulärdeltagare - Skapa formuläret {#form-participant-step-creating-the-form}

Skapa ett formulär som ska användas med ett **steg för formulärdeltagare** som vanligt. Formulär för ett steg för formulärdeltagare måste dock ha följande konfigurationer:

* **Start av formulär**-komponenten måste ha egenskapen **Åtgärdstyp** inställd på `Edit Workflow Controlled Resource(s)`.
* Komponenten **Start av formulär** måste ha ett värde för egenskapen `Form Identifier`.
* Formulärkomponenterna måste ha egenskapen **Elementnamn** inställd på sökvägen till noden där fältdata lagras. Sökvägen måste hitta en nod i arbetsflödets nyttolastinnehåll. Värdet har följande format:

   `./jcr:content/path_to_node`

* Formuläret måste innehålla en **Skicka-knapp(ar) för arbetsflöde**-komponent. Du konfigurerar inga egenskaper för komponenten.

Arbetsflödets krav avgör var fältdata ska lagras. Fältdata kan till exempel användas för att konfigurera egenskaper för sidinnehåll. Följande värde för egenskapen **Elementnamn** lagrar fältdata som värdet för egenskapen `redirectTarget` för noden `jcr:content`:

`./jcr:content/redirectTarget`

I följande exempel används fältdata som innehåll i en **Text**-komponent på nyttolastsidan:

`./jcr:content/par/text_3/text`

Det första exemplet kan användas för alla sidor som återges av komponenten `cq:Page`. Det andra exemplet kan bara användas när nyttolastsidan innehåller en **Text**-komponent som har ID `text_3`.

Formuläret kan finnas var som helst i databasen, men arbetsflödesanvändare måste ha behörighet att läsa formuläret.

### Slumpmässig deltagarväljare {#random-participant-chooser}

Steget **Slumpmässig deltagarväljare** är en deltagarväljare som tilldelar det genererade arbetsobjektet till en användare som väljs slumpmässigt från en lista.

![wf-31](assets/wf-31.png)

#### Slumpmässig deltagarväljare - konfiguration {#random-participant-chooser-configuration}

Om du vill konfigurera steget redigerar du och använder följande flikar:

* [Vanliga](#step-properties-common-tab)
* **Argument**

   * **Deltagare**: Anger listan med användare som är tillgängliga för markering. Om du vill lägga till en användare i listan klickar du på **Lägg till objekt** och skriver hemsökvägen för användarnoden eller användar-ID:t. Användarnas ordning påverkar inte sannolikheten att tilldelas en arbetsuppgift.

### Väljare för deltagare i arbetsflödesinitieraren {#workflow-initiator-participant-chooser}

**Väljaren för deltagare i arbetsflödesinitieraren** är en deltagarväljare som tilldelar det genererade arbetsobjektet till användaren som startade arbetsflödet. Det finns inga andra egenskaper att konfigurera än egenskaperna **Common**.

#### Väljare för deltagare i arbetsflödesinitiering - konfiguration {#workflow-initiator-participant-chooser-configuration}

Om du vill konfigurera steget redigerar du på följande flikar:

* [Vanliga](#step-properties-common-tab)

## Processsteg {#process-step}

Ett **processteg** kör ett ECMAScript eller anropar en OSGi-tjänst för att utföra automatisk bearbetning.

![wf-32](assets/wf-32.png)

### Processsteg - konfiguration {#process-step-configuration}

Om du vill konfigurera steget redigerar du och använder följande flikar:

* [Vanliga](#step-properties-common-tab)
* **Process**

   * **Process**: Processimplementeringen som ska köras. Använd listrutan för att välja ECMAScript- eller OSGi-tjänsten. Mer information om:

      * Standardtjänsterna ECMAScripts och OSGi, se [Inbyggda processer för processteg](/help/sites-developing/workflows-process-ref.md).
      * Information om hur du skapar ECMAScript för ett processsteg finns i [Implementera ett processsteg med ett ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).
      * Information om hur du skapar OSGi-tjänster för ett processsteg finns i [Implementera ett processsteg med en Java-klass](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class).
   * **Handler Advance**: Välj det här alternativet om du vill att arbetsflödet automatiskt ska gå vidare till nästa steg efter körningen. Om du inte väljer det här alternativet måste implementeringsskriptet hantera arbetsflödets utveckling.
   * **Argument**: Argument som ska skickas till processen.


## Ange variabel {#set-variable}

Med steget Ange variabel kan du ange ett värde för en variabel och definiera i vilken ordning värdena ska anges. Variabeln ställs in i den ordning som variabelmappningarna visas i steget Ange variabel.

![Lägg till mappning för att ange en variabel](assets/set_variable_addmappingnew.png)

### Ange variabel - konfiguration {#setvariable}

Om du vill konfigurera steget redigerar du och använder följande flikar:

* [Vanliga](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **Mappning**

   * **Välj Variabel:** Använd det här alternativet om du vill välja en variabel för att ange dess värde.
   * **Välj Mappningsläge:** Välj ett mappningsläge för att ange värdet för variabeln. Beroende på variabelns datatyp kan du använda följande alternativ för att ange värdet för en variabel:

      * **Literal:** Använd alternativet när du vet exakt vilket värde du vill ange.
      * **Uttryck:** Använd alternativet när värdet som ska användas beräknas baserat på ett uttryck. Uttrycket skapas i den angivna uttrycksredigeraren.
      * **JSON-punktnotation:** Använd alternativet för att hämta ett värde från en JSON- eller FDM-typvariabel.
      * **XPATH:** Använd alternativet för att hämta ett värde från en XML-typvariabel.
      * **Relativt till nyttolast:** Använd alternativet när värdet som ska sparas till variabeln är tillgängligt på en sökväg som är relativ till nyttolasten.
      * **Absolut sökväg:** Använd alternativet när värdet som ska sparas i variabeln är tillgängligt med en absolut sökväg.
   * **Ange värde:** Ange ett värde som ska kopplas till variabeln. Vilket värde du anger i det här fältet beror på mappningsläget.
   * **Lägg till mappning:** Använd det här alternativet om du vill lägga till fler mappningar för att ange ett värde för variabeln.
