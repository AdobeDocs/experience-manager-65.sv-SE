---
title: Anpassa layout och placering av felmeddelanden i ett anpassat formulär
seo-title: Anpassa layout och placering av felmeddelanden i ett anpassat formulär
description: 'Du kan anpassa layout och placering av felmeddelanden för en adaptiv for. '
seo-description: 'Du kan anpassa layout och placering av felmeddelanden för en adaptiv for. '
uuid: 6d3490f6-c867-44c9-a527-55f6d7221f99
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 136ac7e3-9d1f-4d58-bd4f-9dbe09eeafee
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Anpassa layout och placering av felmeddelanden i ett anpassat formulär{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

Du kan anpassa layout och placering av felmeddelanden i ett anpassat formulär. Du kan utföra följande anpassningar:

* Anpassa plats och layout för bildtexten i ett fält utan att ändra motsvarande CSS-egenskaper
* Anpassa positionen för textbundna felmeddelanden
* Anpassa innehållet i indikatorn för dynamisk hjälp
* Anpassa placeringen av fältkomponenterna (bildtext, widget, kort beskrivning, lång beskrivning och hjälpindikatorkomponenter) utan att göra några ändringar i motsvarande CSS-egenskaper

## Anpassa fältlayout {#customize-layout-of-fields}

Du kan anpassa layouten för ett enskilt fält eller för alla fält för att ändra positionen för bildtexter och felmeddelanden. Utför följande steg för att tillämpa en anpassad layout på ett fält:

### Anpassa layouten för ett enskilt fält {#customize-layout-of-a-single-field}

Utför följande steg för att tillämpa en anpassad layout på ett enskilt fält:

1. Öppna formuläret i **stilläge** . Om du vill öppna formuläret i formatläge trycker du på ![arbetsytelistrutan](assets/canvas-drop-down.png) > **Format** i sidverktygsfältet.
1. Markera fältet under **Formulärobjekt** i sidofältet och tryck på redigeringsknappen ![Redigera-knapp](assets/edit-button.png).
1. Markera läget för det fält som du vill anpassa och ange format för det läget.

   ![Ange infogad formatering för ett fält](assets/edit-error-state.png)

### Anpassa layouten för alla fält i ett formulär {#customize-layout-of-all-the-fields-of-a-form}

Med AEM Forms kan du nu skapa ett tema och använda det i ditt formulär. Med temaredigeraren kan du ange format för formulärkomponenter på ett och samma ställe. När du skapar ett tema anger du en stil på komponentnivå. Mer information om teman finns i [Teman i AEM-formulär](../../forms/using/themes.md).

Skapa ett tema med hjälp av temaredigeraren för att anpassa layouten för alla fält i formuläret. När du har skapat ett tema utför du följande steg för att tillämpa det på ett formulär:

1. Öppna formuläret i redigeringsläge.
1. Markera en komponent i redigeringsläget, tryck sedan på ![fältnivå](assets/field-level.png) > **Adaptiv formulärbehållare** och tryck sedan på ![cmpr](assets/cmppr.png).
1. I sidlisten, under Adaptivt formulärtema, väljer du det tema du har skapat med hjälp av Theme Editor.

## Skapa en anpassad fältlayout {#create-a-custom-field-layout}

1. Öppna CRXDE lite. Standardwebbadressen är https://&#39;[server]:[port]&#39;/crx/de.
1. Kopiera en fältlayout från noden /libs/fd/af/layouts/field (till exempel defaultFieldLayout) till noden /apps (till exempel /apps/af-field-layout).
1. Byt namn på den kopierade noden och filen defaultFieldLayout.jsp. Till exempel errorOnRight.jsp.

1. Ändra värdet för egenskaperna qtip och jcr:description för den kopierade noden. Ändra till exempel värdet för egenskaperna till Fel till höger

1. Om du vill lägga till nya format och beteenden skapar du ett klientbibliotek i noden /etc.

   Skapa till exempel nodens klientbibliotek på platsen /etc/af-field-layout-clientlib. Lägg till egenskapen categories med värdet af.field.errorOnRight och style.less med följande kod:

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
1. Öppna redigeringsdialogrutan för fältet och välj fliken **Format** . I listrutan **Konfigurera fältlayout** markerar du den nya layouten och klickar på **OK**.

Paketet ErrorOnRight.zip innehåller kod som visar felmeddelanden till höger om fält.

[Hämta fil](assets/erroronright.zip)
