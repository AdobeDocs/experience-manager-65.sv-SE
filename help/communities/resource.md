---
title: Skapa och tilldela aktiveringsresurser
seo-title: Skapa och tilldela aktiveringsresurser
description: Lägg till aktiveringsresurser
seo-description: Lägg till aktiveringsresurser
uuid: da940242-0c9b-4ad8-8880-61fd41461c3b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8fe97181-600e-42ac-af25-d5d4db248740
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 2%

---


# Skapa och tilldela aktiveringsresurser {#create-and-assign-enablement-resources}

## Lägg till en aktiveringsresurs {#add-an-enablement-resource}

Så här lägger du till en aktiveringsresurs på den nya communitywebbplatsen:

* Logga in som systemadministratör på författarinstansen:
   * Till exempel [http://localhost:4502/](http://localhost:4503/)
* Välj **[!UICONTROL Communities]** > **[!UICONTROL Resources]** från global navigering

   ![resurser](assets/resources.png)

   ![enablement-resource](assets/enablement-resource.png)
* Välj den community där aktiveringsresurser läggs till:
   * Välj **[!UICONTROL Enablement Tutorial]**.
* Välj **[!UICONTROL Create]** i menyn.
* Välj **[!UICONTROL Resource]**.

![create-resource](assets/create-enablement-resource.png)

### Grundläggande information {#basic-info}

Fyll i grundläggande information för resursen:

* **[!UICONTROL Site Name]**

   Ange namnet på den valda communitywebbplatsen: Självstudiekurs om aktivering

* **[!UICONTROL Resource Name&ast;]**

   Ski Lesson 1

* **[!UICONTROL Tags]**

   Självstudiekurs: Idrott/skidåkning

* **[!UICONTROL Show in Catalog]**

   Ställ in den på **På**.

* **[!UICONTROL Description]**

   Snön snurrar för nybörjare.

* **[!UICONTROL Add Image]**

   Lägg till en bild som representerar resursen för medlemmen i uppdragsvyn.

   ![basic-info](assets/basic-info.png)

* Välj **[!UICONTROL Next]**

### Lägg till innehåll {#add-content}

Det ser ut som om flera resurser kan väljas, men bara en är tillåten.

Välj `'+' icon` i det övre högra hörnet för att börja välja resursen genom att identifiera källan.

![add-content](assets/add-content.png)

![upload-resource](assets/upload-resource.png)

Överför en resurs. Om det är en videoresurs kan du antingen överföra en anpassad bild som ska visas innan videon börjar spelas upp eller tillåta att en miniatyrbild genereras från videon (kan ta några minuter - det är inte nödvändigt att vänta).

![upload-video](assets/upload-video.png)

* Välj **[!UICONTROL Next]**.

### Inställningar {#settings}

* **[!UICONTROL Social Settings]**

   Lämna standardinställningarna så att eleverna kan kommentera och betygsätta aktiveringsresurser.

* **[!UICONTROL Due Date]**

   *(Valfritt)*  Ett datum då uppdraget ska vara slutfört kan väljas.

* **[!UICONTROL Resource Author]**

   *(Valfritt)* Lämna tomt.

* **[!UICONTROL Resource Contact&ast;]**

   *(Obligatoriskt)* Använd listrutan för att välja medlem  `Quinn Harper`.

* **[!UICONTROL Resource Expert]**

   *(Valfritt)* Lämna tomt.

   **Obs**: Om användare eller grupper inte visas kontrollerar du att de har lagts till i  `Community Enable Members` gruppen och  ** sparats i publiceringsinstansen.

   ![enablement-settings](assets/enablement-settings.png)

* Välj **[!UICONTROL Next]**

### Uppdrag {#assignments}

* **[!UICONTROL Add Assignees]**

   Låt vara unset eftersom den här aktiveringsresursen läggs till i en utbildningsväg. Om en elev tilldelas till den enskilda aktiveringsresursen samt en learningsökväg som innehåller aktiveringsresursen, tilldelas eleven till aktiveringsresursen två gånger.

   ![tillägg](assets/add-assignments.png)

* Välj **[!UICONTROL Create]**

   ![create-resource](assets/create-resource.png)

Resursen har skapats och återgår till resurskonsolen med den nyligen skapade resursen markerad. Från den här konsolen går det att publicera, lägga till deltagare och ändra andra inställningar.

Om du vill överföra en ny version av aktiveringsresursen rekommenderar vi att du skapar en ny resurs och sedan avregistrerar medlemmar från den gamla versionen och registrerar dem i den nya versionen.

### Publicera resursen {#publish-the-resource}

Innan registrerare kan se den tilldelade kursen måste den publiceras:

* Välj ikonen `Publish` för världen

Aktiveringen har bekräftats med ett meddelande:

![publish-resource](assets/publish-resource.png)

## Lägg till en andra aktiveringsresurs {#add-a-second-enablement-resource}

Upprepa stegen ovan för att skapa och publicera en andra relaterad aktiveringsresurs som en inlärningsväg skapas från.

![add-resource](assets/add-resource.png)

**Publicera** den andra resursen.

Gå tillbaka till självstudiekursen om aktivering av dess resurser.

*Tips: Uppdatera sidan om båda resurserna inte visas.*

![refresh-resource](assets/refresh-resource.png)

## Lägg till en utbildningssökväg {#add-a-learning-path}

En inlärningsväg är en logisk gruppering av aktiveringsresurser som utgör en kurs.

* Välj `+ Create` från resurskonsolen
* Välj **[!UICONTROL Learning Path]**

![add-learning-path](assets/add-learning-path.png)

Lägg till **[!UICONTROL Basic Info]**:

* **[!UICONTROL Learning Path Name]**

   Ski-lektioner

* **[!UICONTROL Tags]**

   Självstudiekurs: Skickar

* **[!UICONTROL Show in Catalog]**

   Lämna omarkerad

* **[!UICONTROL Upload an image]**

   För att visa utbildningssökvägen i resurskonsolen.

   ![learningpath-basic](assets/learningpath-basic.png)

* Välj **[!UICONTROL Next]**.

Hoppa över nästa panel eftersom det inte finns några nödvändiga inlärningsvägar att lägga till.

* Välj **[!UICONTROL Next]**

På panelen Lägg till resurser:

* Välj `+ Add Resources` om du vill välja de två skidsessionerna som ska läggas till i inlärningsvägen.

   Obs! Endast **publicerade** resurser kan markeras.

>[!NOTE]
>
>Du kan bara välja resurser på samma nivå som utbildningsvägen. För en inlärningsväg som skapats i en grupp är t.ex. endast resurserna på gruppnivå tillgängliga. för en inlärningsväg som skapats på en community-webbplats finns resurserna på den webbplatsen tillgängliga för tillägg till inlärningsvägen.

* Välj **[!UICONTROL Submit]**.

   ![learningpath](assets/learningpath-add.png)

   ![create-learningpath](assets/create-learningpath.png)

* Välj **[!UICONTROL Next]**

   ![learningpath-settings](assets/learningpath-settings.png)

* **[!UICONTROL Add Assignees]**

   Använd listrutan för att välja gruppen `Community Ski Class` som ska innehålla medlemmarna `Riley Taylor` och `Sidney Croft.`

* **[!UICONTROL Learning Path Contact&ast;]**

   *(Obligatoriskt)* Använd listrutan för att välja medlem  `Quinn Harper`.

* Välj **[!UICONTROL Create]**.

   ![learningpath-info](assets/learningpath-info.png)

Utbildningssökvägen har skapats och återgår till resurskonsolen med den nya utbildningssökvägen markerad. Från den här konsolen går det att publicera, lägga till deltagare och ändra andra inställningar.

**Publicera** utbildningsvägen.

