---
title: Grundläggande om Rich Text Editor
seo-title: Grundläggande om Rich Text Editor
description: Översikt över textredigeringsfunktionen
seo-description: Översikt över textredigeringsfunktionen
uuid: f96015cc-114b-431a-a5ba-dc195c2a0b83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0225a543-0fad-488b-8b0b-8b3512d44fbe
translation-type: tm+mt
source-git-commit: 4b6311cbfe11a61b74f68bf5a25ad1f5faef5358
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---


# Grundläggande om Rich Text Editor {#rich-text-editor-essentials}

## Översikt {#overview}

Med en textredigerare kan du skriva text med markeringar.

För webbgruppskomponenter, som liknar [textredigeraren i författarmiljön](../../help/sites-authoring/rich-text-editor.md), påverkar det text som anges i publiceringsmiljön.

![textredigerare](assets/rich-text-editor.png)

## Aktivera RTF-redigeraren {#enabling-rich-text-editor}

Communities-komponenter som tillåter användargenererat innehåll (UGC) kan aktiveras för att tillåta RTE. Beroende på om komponenten har lagts till på en sida eller inkluderats i en [funktion](functions.md), kan RTE vara aktiverat som standard.

Om den inte är aktiverad anger du bara [redigeringsläget för författare](sites-console.md#authoring-site-content), markerar komponenten för redigering och markerar kryssrutan `Rich Text Editor`.

RTE är tillgängligt för följande Communities-komponenter:

* [Blogg](blog-feature.md)
* [Kalender](calendar.md)
* [Kommentarer](comments.md)
* [Filbibliotek](file-library.md)
* [Forum](forum.md)
* [Meddelanden](configure-messaging.md)
* [QnA](working-with-qna.md)
* [Recensioner](reviews.md)

## Anpassning {#customization}

Det går att anpassa RTF-redigeraren eftersom implementeringen baseras på [CKEditor](https://www.ckeditor.com/).

Den aktuella konfigurationen för Communities-komponenter finns i `cq.social.  scf   clientlib`, som finns i databasen på

`/libs/clientlibs/social/commons/scf/ckrte.js`

Du bör inte ändra klientlib cq.social.scf eftersom framtida uppgraderingar kan åsidosätta redigeringar.

### Exempelanpassning: Textbundna länkar {#example-customization-inline-links}

På grund av säkerhetsproblem inkluderas inte hyperlänksalternativen i den uppsättning med textikoner som visas för medlemmar som standard. Förmågan till skada är stor när hrefs tillåts i UGC.

Så här lägger du till hyperlänksalternativen i verktygsfältet:

* Lägg till ett verktygsfält med namnet &quot; `links`&quot;
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

