---
title: Konfigurera flera redigerare på plats
seo-title: Konfigurera flera redigerare på plats
description: Det går att konfigurera komponenten så att den har flera redigerare på plats
seo-description: Det går att konfigurera komponenten så att den har flera redigerare på plats
uuid: 4abbfcd5-fe1b-4c02-b115-97db20e60e1e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 0fac1e4a-f08f-4c46-b070-cb1d5a05b6e0
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# Konfigurera flera redigerare på plats{#configuring-multiple-in-place-editors}

Det går att konfigurera komponenten så att den har flera redigerare på plats i det beröringsaktiverade användargränssnittet.

När du har konfigurerat det kan du välja rätt innehåll och öppna rätt redigerare. Exempel:

![chlimage_1-8](assets/chlimage_1-8a.png)

## Konfigurera flera redigerare {#configuring-multiple-editors}

För att kunna aktivera flera redigerare på plats har strukturen för en `cq:InplaceEditingConfig` nodtyp förbättrats med definitionen av `cq:ChildEditorConfig` nodtyp.

Exempel:

```
   /**
       * Configures inplace editing of a component.
       *
       * @prop active true to activate inplace editing for the component
       * @prop editorType ID of inplace editor to use
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional)
       * @node config editor's config (used if no configPath is specified; optional)
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a subcomponent. The name of the this node will
      * be used as DD id.
      *
      * @prop type type of the inline editor. eg: ["image"]
      * @prop title totle od the inline editor
      * @prop icon icon to represent the inline editor
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

Så här konfigurerar du flera redigerare:

1. I noden `cq:inplaceEditing` (av typen `cq:InplaceEditingConfig`) definierar du egenskapen:

   * Namn:`editorType`
   * Typ: `String`
   * Värde: `hybrid`

1. Skapa en ny nod under den här noden:

   * Namn: `cq:ChildEditors`
   * Typ: `nt:unstructured`

1. Skapa en ny nod för varje redigerare på plats under `cq:childEditors` noden:

   * Namn: namnet på varje nod ska vara namnet på den egenskap som den representerar (som med släppmål). Exempel, `image`, `text`.
   * Typ: cq: `ChildEditorConfig`
   >[!NOTE]
   >
   >Det finns en korrelation mellan de definierade släppmålen och de underordnade redigerarna. Namnet på `cq:ChildEditorConfig` noden betraktas som det släppmål-ID som används som parameter till den valda underordnade redigeraren. Om det redigerbara delområdet inte har något släppmål (t.ex. som med en textkomponent) betraktas namnet på den underordnade redigeraren fortfarande som ett ID som identifierar motsvarande redigerbara område.

1. Definiera egenskaperna för var och en av dessa noder ( `cq:ChildEditorConfig`):

   * Namn: `type`
   * Värde: Namnet på den registrerade redigeraren på plats. t.ex. `image`, `text`

   * Namn: `title`
   * Värde: Den rubrik som du vill visa i komponentens urvalslista (för tillgängliga redigerare). t.ex. `Image`, `Text`

### Ytterligare konfiguration för RTF-redigerare {#additional-configuration-for-rich-text-editors}

Konfigurationen för flera textredigerare är något annorlunda eftersom du kan konfigurera varje enskild RTE-instans separat.

>[!NOTE]
>
>Mer information finns i [Konfigurera RTF-redigeraren](/help/sites-administering/rich-text-editor.md).

Om du vill ha flera textredigerare behöver du en konfiguration för varje lokal textram:

* Under `cq:InplaceEditingConfig` Definiera en `config` nod.

   * Under `config` noden definierar du varje enskild RTE-konfiguration.

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    config
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>Rekommenderad bästa metod är att definiera `config` noden under `cq:InplaceEditingConfig` varje enskild textredigerare kan ha olika konfigurationer.
>
>För RTE stöds emellertid egenskapen när det bara finns en instans av textredigeraren (redigerbart delområde) i komponenten. `configPath` Den här användningen av `configPath` har stöd för bakåtkompatibilitet med äldre gränssnittsdialogrutor för komponenten.

## Kodexempel {#code-samples}

**KOD PÅ GITHUB**

Koden för den här sidan finns på GitHub

* [Open aem-authoring-hybrideditors project on GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)

## Lägga till en lokal redigerare {#adding-an-in-place-editor}

Allmän information om hur du lägger till en redigerare på plats finns i dokumentet [Anpassa sidredigering](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).
