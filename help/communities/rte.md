---
title: Grundläggande om Rich Text Editor
description: Läs om grunderna och funktionerna i en textredigerare där du kan skriva text med markeringar.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 821e32f4-da8d-4bbb-936a-0844b8a24cdd
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Grundläggande om Rich Text Editor {#rich-text-editor-essentials}

## Ökning {#overview}

Med en textredigerare kan du skriva text med markeringar.

För webbgruppskomponenter, som liknar [RTF-redigeraren i författarmiljön](../../help/sites-authoring/rich-text-editor.md), påverkar det text som anges i publiceringsmiljön.

![RTF-redigerare](assets/rich-text-editor.png)

## Aktivera RTF-redigeraren {#enabling-rich-text-editor}

Communities-komponenter som tillåter användargenererat innehåll (UGC) kan aktiveras för att tillåta RTE. Om komponenten har lagts till på en sida eller inkluderats i en [funktion](functions.md) kan RTE vara aktiverat som standard.

Om den inte är aktiverad anger du bara [redigeringsläget för författare](sites-console.md#authoring-site-content), markerar komponenten för redigering och markerar kryssrutan `Rich Text Editor` .

RTE är tillgängligt för följande Communities-komponenter:

* [Blogg](blog-feature.md)
* [Kalender](calendar.md)
* [Kommentar](comments.md)
* [Filbibliotek](file-library.md)
* [Forum](forum.md)
* [Meddelanden](configure-messaging.md)
* [QnA](working-with-qna.md)
* [Recensioner](reviews.md)

## Anpassning {#customization}

Det går att anpassa RTF-redigeraren eftersom implementeringen baseras på [CKEditor](https://ckeditor.com/).

Den aktuella konfigurationen för Communities-komponenter finns i `cq.social.  scf   clientlib`, i databasen på

`/libs/clientlibs/social/commons/scf/ckrte.js`

Du bör inte ändra klientlib cq.social.scf eftersom framtida uppgraderingar kan åsidosätta redigeringar.

### Exempelanpassning: Textbundna länkar {#example-customization-inline-links}

På grund av säkerhetsproblem inkluderas inte hyperlänksalternativen i den uppsättning med textikoner som visas för medlemmar som standard. Förmågan till skada är stor när hrefs tillåts i UGC.

Så här lägger du till hyperlänksalternativen i verktygsfältet:

* Lägg till ett verktygsfält med namnet `links`
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* Välj **[!UICONTROL Save All]**

#### /libs/clientlibs/social/commons/scf/ckrte.js {#libs-clientlibs-social-commons-scf-ckrte-js}

```
CKRte.prototype.config = {
    toolbar: [
        { name: "basicstyles",
           items: ["Bold", "Italic", "Underline", "NumberedList", "BulletedList", "Outdent", "Indent", "JustifyLeft", "JustifyCenter", "JustifyRight", "JustifyBlock", "TextColor"]
        },
        { name: 'links',
           items: [ 'Link','Unlink','Anchor' ]
        }
    ],
    autoParagraph: false,
    autoUpdateElement: false,
    removePlugins: "elementspath",
    resize_enabled: false
};
```
