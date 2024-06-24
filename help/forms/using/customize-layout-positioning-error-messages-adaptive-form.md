---
title: Anpassa layout och placering av felmeddelanden i ett anpassat formulär
description: Du kan anpassa layouten och placeringen av felmeddelanden för en adaptiv for.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 5cb3ee55-f411-4692-84f7-89bf6ade729d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Anpassa layout och placering av felmeddelanden i ett anpassat formulär{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

Du kan anpassa layout och placering av felmeddelanden i ett anpassat formulär. Du kan utföra följande anpassningar:

* Anpassa plats och layout för bildtexten i ett fält utan att ändra motsvarande CSS-egenskaper
* Anpassa positionen för infogade felmeddelanden
* Anpassa innehållet i indikatorn för dynamisk hjälp
* Anpassa placeringen av fältkomponenterna (bildtext, widget, kort beskrivning, lång beskrivning och hjälpindikatorkomponenter) utan att ändra motsvarande CSS-egenskaper

## Anpassa fältlayout {#customize-layout-of-fields}

Du kan anpassa layouten för ett enskilt fält eller för alla fält för att ändra positionen för bildtexter och felmeddelanden.

Så här använder du en anpassad layout för ett fält:

### Anpassa layouten för ett enskilt fält {#customize-layout-of-a-single-field}

1. Öppna formuläret i **Stil** läge. Om du vill öppna formuläret i formatläge väljer du ![canvas-drop-down](assets/canvas-drop-down.png) > **Stil**.
1. I sidlisten, under **Formulärobjekt** markerar du fältet och väljer redigeringsknappen ![edit-button](assets/edit-button.png).
1. Markera läget för det fält som du vill anpassa och ange formatet för det läget.

   ![Ange infogad formatering för ett fält](assets/edit-error-state.png)

### Anpassa layout för alla fält i ett formulär {#customize-layout-of-all-the-fields-of-a-form}

Med AEM Forms kan du nu skapa ett tema och använda det i ditt formulär. Med temaredigeraren kan du ange formaten för formulärkomponenterna på ett och samma ställe. När du skapar ett tema anger du en stil på komponentnivå. Mer information om teman finns i [Teman i AEM Forms](../../forms/using/themes.md).

Skapa ett tema med hjälp av temaredigeraren för att anpassa layouten för alla fält i formuläret. När du har skapat ett tema utför du följande steg för att tillämpa det på ett formulär:

1. Öppna formuläret i redigeringsläge.
1. Markera en komponent i redigeringsläget och välj sedan ![fältnivå](assets/field-level.png) > **Adaptiv formulärbehållare** och sedan markera ![cmppr](assets/cmppr.png).
1. I sidlisten, under Adaptivt formulärtema, väljer du det tema du har skapat med hjälp av Theme Editor.

## Skapa en anpassad fältlayout {#create-a-custom-field-layout}

1. Öppna CRXDE Lite. Standardwebbadressen är https://&#39;[server]:[port]&#39;/crx/de.
1. Kopiera en fältlayout från noden /libs/fd/af/layouts/field (till exempel defaultFieldLayout) till noden /apps (till exempel /apps/af-field-layout).
1. Byt namn på den kopierade noden och filen defaultFieldLayout.jsp. Till exempel errorOnRight.jsp.

1. Ändra värdet för egenskaperna qtip och jcr:description för den kopierade noden. Ändra till exempel värdet för egenskaperna till Fel till höger

1. Om du vill lägga till nya format och beteenden skapar du ett klientbibliotek i noden /etc.

   Skapa till exempel nodens klientbibliotek på platsen /etc/af-field-layout-clientlib. Lägg till egenskapen categories med värdet af.field.errorOnRight och style.less i följande kod:

   ```css
   .widgetErrorWrapper {
   
    height: 38px;
    margin: 5px;
   
    .guideFieldWidget{
    width: 60%;
    float: left; 
    }
   
    .guideFieldError{
    overflow:hidden;
    width:40%; 
    }
   
   }
   ```

1. Om du vill förbättra utseendet och beteendet inkluderar du klientbiblioteket som skapades i layoutfilen (errorOnRight.jsp).
1. Öppna redigeringsdialogrutan för fältet och välj **Stilar** -fliken. I **Konfigurera fältlayout** väljer du den nya layouten och klickar på **OK**.

Paketet ErrorOnRight.zip innehåller kod som visar felmeddelanden till höger om fält.

[Hämta fil](assets/erroronright.zip)
