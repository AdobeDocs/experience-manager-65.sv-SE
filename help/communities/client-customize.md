---
title: Anpassning på klientsidan
seo-title: Anpassning på klientsidan
description: Anpassa beteende eller utseende på klientsidan i AEM Communities
seo-description: Anpassa beteende eller utseende på klientsidan i AEM Communities
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Anpassning på klientsidan {#client-side-customization}

| **[⇐ - funktioner](essentials.md)** | **[Anpassning på serversidan](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers](handlebars-helpers.md)** |

Det finns flera sätt att anpassa utseendet och/eller beteendet för en AEM Communities-komponent på klientsidan.

Två större metoder är att täcka över eller utöka en komponent.

[Om du ersätter](#overlays) en komponent ändras standardkomponenten och alla referenser till komponenten påverkas.

[Om du utökar](#extensions) en komponent, som får ett unikt namn, begränsas ändringsomfånget. Termen&quot;utöka&quot; används omväxlande med&quot;åsidosätt&quot;.

## Övertäckningar {#overlays}

Att ersätta en komponent är ett sätt att göra ändringar i en standardkomponent och påverka alla förekomster som använder standardkomponenten.

Övertäckningen uppnås genom att en kopia av standardkomponenten i katalogen /**apps** ändras, i stället för att originalkomponenten i katalogen /**libs** ändras. Komponenten är konstruerad med en identisk relativ sökväg, förutom att &#39;libs&#39; ersätts med &#39;apps&#39;.

Katalogen /apps är den första plats som genomsöks för att lösa begäranden, och om den inte hittas används standardversionen i katalogen /libs.

Standardkomponenten i katalogen /libs får aldrig ändras eftersom framtida korrigeringar och uppgraderingar är fria att ändra katalogen /libs på det sätt som behövs, samtidigt som de allmänna gränssnitten bibehålls.

Detta skiljer sig från [att utöka](#extensions) en standardkomponent där du vill göra ändringar för en viss användning, skapa en unik sökväg till komponenten och förlita dig på att referera den ursprungliga standardkomponenten i katalogen /libs som den överordnade resurstypen.

Om du snabbt vill se ett exempel på hur du lägger över kommentarkomponenten kan du testa självstudiekursen [Komponenten för överläggskommentarer](overlay-comments.md).

## Tillägg {#extensions}

Att utöka (åsidosätta) en komponent är ett sätt att göra ändringar för en viss användning utan att påverka alla instanser som använder standardvärdet. Den utökade komponenten har ett unikt namn i mappen /apps och refererar till standardkomponenten i mappen /libs, vilket innebär att en komponents standarddesign och beteende inte ändras.

Detta skiljer sig från [att täcka över](#overlays) standardkomponenten där Sling-typen löser relativa referenser till programmen/mappen innan sökning görs i libs/folder, vilket innebär att en komponents design eller beteende ändras globalt.

Ett snabbt exempel på hur du utökar kommentarkomponenten finns i självstudiekursen [Utöka kommentarkomponent](extend-comments.md).

## Javascript-bindning {#javascript-binding}

HBS-skriptet för komponenten måste vara bundet till JavaScript-objekt, modeller och vyer som implementerar den här funktionen.

Värdet för `data-scf-component` attributet kan vara standardvärdet, till exempel **`social/tally/components/hbs/rating`** eller en utökad (anpassad) komponent för anpassade funktioner, till exempel **werdetail/components/hbs/rating**.

Om du vill binda en komponent måste hela komponentskriptet inneslutas i ett &lt;div>-element med följande attribut:

* `data-component-id`=&quot;{{id}}&quot;

   matchar egenskapen id från kontexten

* `data-scf-component`=&quot;*&lt;resourceType>*

Från `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## Egna egenskaper {#custom-properties}

När du utökar eller döljer en komponent kan du lägga till egenskaper i en ändrad dialogruta.

Du kommer åt alla egenskaper som har angetts för en komponent/resurs genom att referera till egenskapstangenterna i mallen för verktygsfält:

`{{properties.<property_name>}}`

## CSS-skal {#skinning-css}

Du kan anpassa komponenterna så att de matchar det övergripande temat på webbplatsen genom att&quot;skala&quot; - ändra färger, teckensnitt, bilder, knappar, länkar, mellanrum och till och med placering i viss utsträckning.

Du kan skapa skal genom att åsidosätta ramverksformaten selektivt eller genom att skriva helt nya formatmallar. SCF-komponenterna definierar namnutrymmen, modulära och semantiska CSS-klasser som påverkar de olika elementen som en komponent består av.

Så här skalförändrar du en komponent:

1. Identifiera de element som du vill ändra (t.ex. dispositionsområde, knappar i verktygsfält, meddelandeteckensnitt).
1. Identifiera CSS-klassen/reglerna som påverkar dessa element.
1. Skapa en formatmallsfil (.css).
1. Inkludera formatmallen i en klientbiblioteksmapp ([clientlibs](#clientlibs-for-scf)) för platsen och se till att den tas med från dina mallar och sidor med [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. Definiera om CSS-klasserna och reglerna som du har identifierat (#2) i formatmallen och lägg till format.

De anpassade formaten åsidosätter nu standardramverksformaten och komponenten återges med det nya skalet.

>[!CAUTION]
>
>Alla CSS-klassnamn som har prefixet** scf-js-&amp;ast;**används specifikt i javascript-kod. Dessa klasser påverkar en komponents tillstånd (till exempel växla från dold till synlig) och bör varken åsidosättas eller tas bort.
>
>Medan scf-js-&amp;ast; klasser påverkar inte format. Klassnamnen kan användas i formatmallar med det intrycket att det kan finnas biverkningar när de styr elementens lägen.

## Utöka JavaScript {#extending-javascript}

Om du vill utöka en Javascript-implementering av komponenter behöver du bara

1. Skapa en komponent för ditt program med jcr:resourceSuperType inställd på värdet för den utökade komponentens jcr:resourceType, t.ex. social/forum/components/hbs/forum
1. Granska JavaScript-komponentens standardkomponent för att ta reda på vilka metoder som behöver registreras med SCF.registerComponent()
1. Kopiera den utökade komponentens JavaScript eller börja från början
1. Utöka metoden
1. Använd SCF.registerComponent() för att registrera alla metoder med antingen standardvärdena eller anpassade objekt och vyer.

### forum.js: Exempeltillägg för forum - HBS {#forum-js-sample-extension-of-forum-hbs}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";
    var GMForumView = SCF.ForumView.extend({
        viewName: "GMForum",
        showComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        },
        hideComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        }
    });

    SCF.registerComponent('social/forum/components/hbs/post', SCF.Post, SCF.PostView);
    SCF.registerComponent('social/forum/components/hbs/topic', SCF.Topic, SCF.TopicView);
    SCF.registerComponent('social/forum/components/hbs/forum', SCF.Forum, GMForumView );
})($CQ, _, Backbone, SCF);
```

## Skripttaggar {#script-tags}

Skripttaggar är en del av klientsidans ramverk. Det är limmet som kan binda den kod som genereras på serversidan till modellerna och vyerna på klientsidan.

Skripttaggar i SCF-skript bör inte tas bort när komponenter åsidosätts eller åsidosätts. SCF-skripttaggar som skapas automatiskt för att injicera JSON i HTML identifieras med attributet `data-scf-json=`true.

## Clientlibs for SCF {#clientlibs-for-scf}

Med hjälp av bibliotek [på](../../help/sites-developing/clientlibs.md) klientsidan (clientlibs) kan du ordna och optimera JavaScript och CSS som används för att återge innehåll på klienten.

Klientlibs for SCF följer ett mycket specifikt namngivningsmönster för två varianter, som endast varierar beroende på om det finns &#39;author&#39; i kategorinamnet:

| Clientlib-variant | Mönster för kategoriegenskap |
|--- |--- |
| complete clientlib | cq.social.hbs.&lt;komponentnamn> |
| författare clientlib | cq.social.author.hbs.&lt;komponentnamn> |

### Fullständiga klienter {#complete-clientlibs}

De fullständiga (icke-författare) klientlibs innehåller beroenden och är praktiska att använda med ui:includeClientLib.

Dessa versioner finns i:

* /etc/clientlibs/social/hbs/&lt;komponentnamn>

Exempel:

* Klientmappsnod: /etc/clientlibs/social/hbs/forum
* Egenskapen Kategorier: cq.social.hbs.forum

I guiden [för](components-guide.md) communitykomponenter visas de fullständiga klientlibs som krävs för varje SCF-komponent.

[Clientlibs for Communities Components](clientlibs.md) beskriver hur du lägger till clientlibs på en sida.

### Författarklipp {#author-clientlibs}

Klientlibs för författarversionen tas bort från det minsta JavaScript-skript som behövs för att implementera komponenten.

Dessa clientlibs ska aldrig tas med direkt, utan kan bäddas in i andra clientlibs, som har skapats för en webbplats för hand.

Dessa versioner finns i mappen SCF libs:

* /libs/social/&lt;feature>/components/hbs/&lt;component name>/clientlibs

Exempel:

* Klientmappsnod: /libs/social/forum/hbs/forum/clientlibs
* Egenskapen Kategorier: cq.social.author.hbs.forum

Obs! Även om författarklienter aldrig bäddar in andra bibliotek listar de sina beroenden. När beroendena är inbäddade i andra bibliotek hämtas de inte automatiskt in och måste även bäddas in.

Du kan identifiera de nödvändiga författarklientlibs genom att infoga&quot;författare&quot; i de klientlibs som visas för varje SCF-komponent i [Community Components Guide](components-guide.md).

### Användning {#usage-considerations}

Alla webbplatser är olika när det gäller hantering av klientbibliotek. Olika faktorer kan vara:

* Total hastighet: Kanske vill man att sajten ska vara responsiv, men den första sidan ska vara lite långsam att ladda. Om många av sidorna använder samma Javascript kan de olika JavaScript-skripten bäddas in i ett clientlib och refereras från den första sidan som ska läsas in. Javascript-filen i den här hämtningen förblir cachelagrad, vilket minimerar mängden data som ska hämtas för efterföljande sidor.
* Kort tid till första sidan: Kanske vill man att första sidan ska läsas in snabbt. I det här fallet finns Javascript i flera små filer som bara ska refereras där det behövs.
* Balans mellan första sidinläsning och efterföljande nedladdningar.

| **[⇐ - funktioner](essentials.md)** | **[Anpassning på serversidan](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers](handlebars-helpers.md)** |

