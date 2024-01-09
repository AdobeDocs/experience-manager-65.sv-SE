---
title: Hur skapar man ett adaptivt formulär?
description: Lär dig hur du skapar ett adaptivt formulär med [!DNL Experience Manager Forms]. Adaptiva Forms är responsiva HTML5-formulär som effektiviserar informationsinsamling och -bearbetning. Mer information om hur du skapar ett adaptivt formulär baserat på en formulärdatamodell och ett XML- eller JSON-schema.
Keywords: create adaptive form core component, create core component based adaptive form, creare adaptive form
products: SG_EXPERIENCEMANAGER/6.5/FORMS
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms, Core Components
exl-id: ee596672-b0b5-42e9-a139-72f90287bf3b
source-git-commit: 4a8155f754d1f71354717f5eb22511baab110916
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 0%

---

# Skapa grundkomponenter baserade på adaptiva Forms {#creating-an-adaptive-form-core-components}


<span class="preview"> Adobe rekommenderar att du använder kärnkomponenter för att [lägga till adaptiv Forms på en AEM Sites-sida](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) eller till [skapa fristående Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md). </span>

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html) |
| AEM 6.5 | Denna artikel |

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

Med anpassningsbara Forms kan du skapa engagerande, responsiva, dynamiska och anpassningsbara formulär. AEM Forms har ett användarvänligt gränssnitt för att snabbt skapa adaptiva Forms. Användargränssnittet erbjuder snabb tabbnavigering så att du enkelt kan välja förkonfigurerade mallar, format, fält och alternativ för att skicka formulär för att skapa ett anpassat formulär.

Innan du börjar får du lära dig mer om vilken typ av Forms-komponenter du kan använda:

* [Adaptiva Forms Core-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en): Dessa är standardiserade komponenter för datainhämtning. Dessa komponenter har anpassningsmöjligheter, kortare utvecklingstid och lägre underhållskostnader för era digitala registreringsupplevelser. En utvecklare kan enkelt anpassa och utforma dessa komponenter. Adobe rekommenderar att du använder dessa moderna och utbyggbara komponenter för att utveckla Adaptiv Forms.

* [Adaptiva Forms Foundation-komponenter](creating-adaptive-form.md): Dessa är klassiska (gamla) komponenter för datainhämtning. Du kan fortsätta att använda dessa för att redigera dina befintliga grundläggande komponentbaserade adaptiva formulär. Om du skapar formulär rekommenderar Adobe att du använder  [Adaptiva Forms Core-komponenter](/help/forms/using/create-adaptive-form.md) för att skapa en adaptiv Forms.

## Krav

Du behöver följande för att skapa ett adaptivt formulär:

* **Aktivera adaptiva Forms Core-komponenter för din miljö**: AEM Archetype project version 41 or later is required to [aktivera kärnkomponenter för din miljö](/help/forms/using/enable-adaptive-forms-core-components.md). När du aktiverar kärnkomponenterna för din miljö, **Adaptiv Forms (kärnkomponent)** -mallar och Canvas-teman läggs till i din miljö.

* **En adaptiv formulärmall**: En mall innehåller en grundläggande struktur och definierar utseendet (layouter och format) för ett adaptivt formulär. Den har förformaterade komponenter som innehåller vissa egenskaper och innehållsstruktur. Här finns också alternativ för att definiera ett tema och en skicka-åtgärd. Temat definierar utseendet, känslan och skickaåtgärden definierar vilken åtgärd som ska vidtas när ett adaptivt formulär skickas in. Du kan också distribuera [exempelmallar](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) i din miljö. Med dessa kan du snabbt börja skapa formulär.

  >[!NOTE]
  >
  > Om du inte har det, **Adaptiv Forms (kärnkomponent)** mallar i din miljö, [Aktivera adaptiva Forms Core-komponenter för din miljö](/help/forms/using/enable-adaptive-forms-core-components.md). När du aktiverar kärnkomponenterna för din miljö, **Adaptiv Forms (kärnkomponent)** -mallen läggs till i din miljö.

* **Ett adaptivt formulärtema**: Ett tema innehåller formatinformation för komponenterna och panelerna. Format innehåller egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet, justering och storlek. När du använder ett tema återspeglas det angivna formatet i motsvarande komponenter.  The `Canvas` -temat läggs till som standard när du aktiverar kärnkomponenter för din miljö. Du kan  [ladda ned och anpassa standardteman](create-or-customize-themes-for-adaptive-forms-core-components.md). För **ur lådan** teman som du kan distribuera [exempelteman](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) i din miljö. Dessa hjälper dig att börja utforma formulären och skapa en grundstruktur för att skapa eller anpassa ett tema efter företagets behov.

* **Behörigheter**: Lägg till dina användare i [!DNL forms-users] grupp. Medlemmarna i [!DNL forms-users] gruppen har behörighet att skapa ett adaptivt formulär. En detaljerad lista över formulärspecifika användargrupper finns i [Grupper och behörigheter](forms-groups-privileges-tasks.md).

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## Skapa ett adaptivt formulär {#create-an-adaptive-form}

1. Logga in lokalt [AEM författarinstans](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=en#author-and-publish-installs).

1. Ange dina uppgifter på inloggningssidan för Experience Manager. När du är inloggad väljer du **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.

1. Välj **[!UICONTROL Create]**  > **[!UICONTROL Create Adaptive Forms]**.

1. Välj en adaptiv Forms Core Components-mall och klicka på **[!UICONTROL Next]**.

1. The **[!UICONTROL Add Properties]** visas. Ange värdena för följande egenskapsfält. Fälten Titel och Namn är obligatoriska:

   * **[!UICONTROL Title:]** Anger formulärets visningsnamn. Titeln hjälper dig att identifiera formuläret i [!DNL Experience Manager Forms] användargränssnitt.
   * **[!UICONTROL Name:]** Anger formulärets namn. En nod med det angivna namnet skapas i databasen. När du börjar skriva en titel genereras värdet för namnfältet automatiskt. Du kan ändra det föreslagna värdet. Namnfältet får endast innehålla alfanumeriska tecken, bindestreck och understreck.
   * **[!UICONTROL Description:]** Anger detaljerad information om formuläret.
   * **[!UICONTROL Theme Client Library]:** Anger temat för ett adaptivt formulär. Som standard är `adaptiveform.theme.canvas3` -temat är valt. Du kan också välja ett annat tema från **[!UICONTROL Theme Client Library]** listruta.
   * **[!UICONTROL Configuration Container:]**  Definierar en plats där konfigurationsfiler för Adaptive Forms lagras. Dessa konfigurationsfiler innehåller inställningar och egenskaper som är relaterade till beteendet och utseendet för Adaptive Forms.
   * **[!UICONTROL Tags:]** Anger taggar som unikt identifierar den adaptiva formen. Taggar hjälper dig att söka i formuläret. Om du vill skapa taggar skriver du nya taggnamn i **[!UICONTROL Tags]** box.
1. Välj **[!UICONTROL Create]**. Ett anpassat formulär skapas och en dialogruta öppnas där du kan öppna formuläret för redigering.


1. Välj **[!UICONTROL Edit]** om du vill öppna det nya formuläret på en ny flik. Formuläret öppnas för redigering och visar det innehåll som är tillgängligt i mallen. Här visas också sidofältet för att anpassa det nya formuläret.


## Använd adaptiva Forms Core-komponenter för att skapa ditt formulär

När du har öppnat formuläret för redigering kan du använda tillgängliga adaptiva Forms Core-komponenter för att lägga till formulärfält i formuläret. Du kan dra och släppa eller använda + [infoga komponent] för att lägga till dessa komponenter i ett formulär. Läs AEM Core Components-dokumentationen om du vill veta mer om tillgängliga komponenter [Adaptiva Forms Core-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en#components). Du kan också besöka [https://aemcomponents.dev/](https://aemcomponents.dev/) för att se hur de tillgängliga kärnkomponenterna fungerar i praktiken.

## Konfigurera åtgärden Skicka för ett anpassat formulär {#configure-submit-action-for-form}

Med en Skicka-åtgärd kan du välja målet för data som har hämtats via ett anpassat formulär. Den aktiveras när en användare klickar på knappen Skicka på ett anpassat formulär. Anpassade formulär innehåller några av de åtgärder som har vidtagits för att skicka in. Du kan också utöka en standardåtgärd för att skicka för att skapa en egen anpassad åtgärd. Så här konfigurerar du en Skicka-åtgärd för formuläret:

1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** som ingår i det adaptiva formuläret.
1. Klicka på egenskaperna för stödlinjebehållaren ![Stödlinjeegenskaper](/help/forms/using/assets/configure-icon.svg) -ikon. Dialogrutan Adaptiv formulärbehållare öppnas.

1. Klicka på  **[!UICONTROL Submission]** -fliken.

   ![Klicka på skiftningsikonen för att öppna dialogrutan Adaptiv formulärbehållare och konfigurera en sändningsåtgärd](/help/forms/using/assets/adaptive-forms-submit-message.png)

1. Välj och konfigurera en **[!UICONTROL Submit action]**, baserat på era behov. Mer information om Skicka åtgärder finns i [Inlämningsåtgärd för anpassat formulär](/help/forms/using/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## Dirigera om användaren till en sida eller visa ett tackmeddelande när formuläret skickas

När du skickar ett formulär kan du dirigera om användaren till en annan webbsida eller ett meddelande. Så här omdirigerar du användaren eller konfigurerar tackmeddelandet:

1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** som ingår i det adaptiva formuläret.
1. Klicka på egenskaperna för stödlinjebehållaren ![Stödlinjeegenskaper](/help/forms/using/assets/configure-icon.svg) -ikon. Dialogrutan Adaptiv formulärbehållare öppnas.
1. Öppna **[!UICONTROL Submission]** -fliken.

   ![Klicka på ikonen för skiftnyckel för att öppna dialogrutan Adaptiv formulärbehållare för att konfigurera en omdirigeringssida eller ett tack för ditt meddelande](/help/forms/using/assets/adaptive-forms-submit-message.png)

   * Om du vill konfigurera en omdirigerings-URL för alternativet Skicka väljer du **[!UICONTROL Redirect to URL]** och bläddra och markera en AEM Sites-sida, eller ange en URL-adress för en extern sida.

   * Om du vill konfigurera ett anpassat meddelande eller ett tackmeddelande väljer du alternativet Skicka i **[!UICONTROL Show Message]** och skriv ett meddelande i **[!UICONTROL Message content]** box. Det är en RTF-ruta som du kan använda helskärmsalternativet för att visa alla tillgängliga RTF-objekt.

## Konfigurera ett schema eller en formulärdatamodell för ett anpassat formulär {#configure-schema-or-data-model-for-form}

Du kan använda formulärdatamodellen för att ansluta ett formulär till en datakälla för att skicka och ta emot data baserat på användaråtgärder. Du kan också ansluta ett formulär till ett JSON-schema för att ta emot skickade data i ett fördefinierat format. Beroende på vad som krävs kan du ansluta formuläret till ett JSON-schema eller en formulärdatamodell:

* [Skapa ett JSON-schema och överför det till din miljö](/help/forms/using/adaptive-form-json-schema-form-model.md)
* [Skapa en formulärdatamodell](/help/forms/using/create-form-data-models.md)

### Konfigurera ett JSON-schema eller en formulärdatamodell för formuläret

Så här konfigurerar du ett JSON-schema eller en formulärdatamodell för formuläret:

1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** som ingår i det adaptiva formuläret.
1. Klicka på egenskaperna för stödlinjebehållaren ![Stödlinjeegenskaper](/help/forms/using/assets/configure-icon.svg) -ikon. Dialogrutan Adaptiv formulärbehållare öppnas.
1. Öppna **[!UICONTROL Data Model]** -fliken.

   ![Klicka på ikonen för skiftnyckel för att öppna dialogrutan Adaptiv formulärbehållare för att konfigurera ett JSON-schema eller en formulärdatamodell](/help/forms/using/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. Välj och konfigurera ett JSON-schema eller en formulärdatamodell utifrån dina krav:

   * När du väljer **[!UICONTROL Form Model]** -alternativ, använd **[!UICONTROL Select Form Data Model]** för att välja en förkonfigurerad formulärdatamodell.
   * När du väljer **[!UICONTROL Schema]** -alternativ, använd **[!UICONTROL Schema]** för att välja ett JSON-schema för formuläret.

1. Klicka på **[!UICONTROL Done]**.

>[!NOTE]
>
> Du kan redigera JSON-schemat eller formulärdatamodellen för ett adaptivt formulär med hjälp av egenskaperna för Guide Container.

## Konfigurera en förifyllningstjänst  {#configure-prefill-service-for-form}

Du kan använda förifyllningstjänsten för att autofylla fält i ett adaptivt formulär med befintliga data. När en användare öppnar ett formulär är värdena för dessa fält förifyllda. Du kan:

* [Skapa en anpassad förifyllningstjänst](/help/forms/using/prepopulate-adaptive-form-fields.md)
* [Använd förifyllningstjänsten för formulärdatamodell](#fdm-prefill-service)

### Använd förifyllningstjänsten för formulärdatamodell för att fylla i fält i ett adaptivt formulär i förväg {#fdm-prefill-service}

Du kan använda förifyllningstjänsten för formulärdatamodell för att fylla i fält i ett adaptivt formulär i förväg med hjälp av en formulärdatamodell eller en anpassad förifyllningstjänst. Tjänsten för förifyllnad av formulärdatamodell använder [Hämta tjänst för konfigurerad formulärdatamodell](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) för att hämta data. Så här använder du förifyllningstjänsten för formulärdatamodell för ett adaptivt formulär:

1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** som ingår i det adaptiva formuläret.
1. Klicka på egenskaperna för stödlinjebehållaren ![Stödlinjeegenskaper](/help/forms/using/assets/configure-icon.svg) -ikon. Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på egenskaperna för den adaptiva formulärbehållaren ![Egenskaper för adaptiv formulärbehållare](/help/forms/using/assets/configure-icon.svg) -ikon. Dialogrutan Adaptiv formulärbehållare öppnas för att konfigurera datamodeller.
   ![Klicka på ikonen för skiftnyckel för att öppna dialogrutan Adaptiv formulärbehållare för att konfigurera en omdirigeringssida eller ett tack för ditt meddelande](/help/forms/using/assets/adaptive-forms-container-prefill-service.png)
1. Välj en formulärdatamodell. Öppna **[!UICONTROL Basic]** -fliken. I förifyllningstjänsten väljer du **[!UICONTROL Form Data Model Prefill Service]**.
1. Klicka på **[!UICONTROL Done]**. Ditt adaptiva formulär har nu konfigurerats för att använda förifyllning av formulärdatamodell. Nu kan du använda [regelredigerare](rule-editor.md) om du vill skapa regler för förifyllning av formulärfält.

<!--
## Edit Form Model properties of an Adaptive Form {#edit-form-model}

1. Select the Adaptive Form and select ![Page information](/help/forms/using/assets/configure-icon.svg) > **[!UICONTROL Open Properties]**. The Form Properties page opens. 

1. Go to the **[!UICONTROL Form Model]** tab and choose a form model. If the Adaptive Form is without a form model, you have the freedom to choose either a JSON schema or a form data model. On the other hand, if the Adaptive Form is already based on a form model, you have the option to switch to another form model of the same type. For instance, if the form is using a JSON schema, you can easily switch to another JSON schema, and similarly if the form is using a Form Data Model, you can switch to another Form Data Model. 

1. Select **[!UICONTROL Save]** to save the properties.
-->

## What&#39;s Next

* [Använd regelredigeraren för att lägga till dynamiskt beteende i formulär](rule-editor.md)
* [Skapa eller anpassa teman för grundkomponentbaserade adaptiva Forms](create-or-customize-themes-for-adaptive-forms-core-components.md)


## Se även

* [Skapa en grundkomponentbaserad adaptiv form](create-an-adaptive-form-core-components.md)
* [Skapa eller lägga till ett anpassat formulär på en AEM Sites-sida eller ett Experience Fragment](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Exempelmallar för teman och formulärdatamodeller](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)
