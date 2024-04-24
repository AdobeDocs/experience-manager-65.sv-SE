---
title: Lägg till klienter
description: Lär dig hur du lägger till en ClientLibraryFolder (clientlibs) som används för att innehålla de JavaScript- och Cascading Style Sheets som används för att återge platsens sidor.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# Lägg till klienter {#add-clientlibs}

## Lägg till en ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Skapa en ClientLibraryFolder med namnet `clientlibs` som innehåller JavaScript (JS) och CSS (Cascading Styles Sheets) som används för att återge sidorna på platsen.

The `categories` egenskapsvärdet som anges för det här klientbiblioteket är den identifierare som används för att direkt ta med klienten från en innehållssida eller för att bädda in den i andra klienter.

1. Använda **CRXDE Lite**, expandera `/etc/designs`

1. Högerklicka `an-scf-sandbox` och markera `Create Node`

   * Namn: `clientlibs`
   * Typ: `cq:ClientLibraryFolder`

1. Klicka **OK**

![add-client-library](assets/add-client-library.png)

I **Egenskaper** för den nya `clientlibs` nod, ange **kategorier** egenskap:

* Namn: **kategorier**
* Typ: **Sträng**
* Värde: **apps.an-scf-sandbox**
* Klicka **Lägg till**
* Klicka **Spara alla**

Obs! Kategorivärdet förskjuts med &#39;appar&#39;. är en konvention som identifierar att &quot;ägande program&quot; finns i /apps-mappen, inte /libs. VIKTIGT: Lägg till platshållare `js.tx`t och **`css.txt`** filer. (Det är inte officiellt en cq:ClientLibraryFolder utan dem.)

1. Högerklicka **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Välj **Skapa fil...**
1. Retur **Namn:** `css.txt`
1. Välj **Skapa fil...**
1. Retur **Namn:** `js.txt`
1. Klicka **Spara alla**

![clientlibs-css](assets/clientlibs-css.png)

Den första raden i css.txt och js.txt identifierar den basplats från vilken följande fillistor ska hittas.

Försök att ställa in innehållet i css.txt på

```
#base=.
 style.css
```

Skapa sedan en fil under clientlibs med namnet style.css och ställ in innehållet på

`body {`

`background-color: #b0c4de;`

`}`

### Bädda in SCF-klienter {#embed-scf-clientlibs}

I **Egenskaper** -fliken för `clientlibs` node, enter the multi-value String property **embed**. Detta bäddar in nödvändiga [klientbibliotek (klientlibs) för SCF-komponenter](/help/communities/client-customize.md#clientlibs-for-scf). I den här självstudiekursen läggs många av de klientlibs som behövs för komponenterna i Communities till.

Detta kan vara det önskade tillvägagångssättet för en produktionsplats, eftersom det finns praktiska överväganden jämfört med storleken/hastigheten för de klienter som laddas ned för varje sida.

Om du bara använder en funktion på en sida kan du inkludera den funktionens fullständiga klientlib direkt på sidan, till exempel

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

I det här fallet är det bäst att ta med alla och så att de mer grundläggande SCF-klientlibs som författarklienten tillhör:

* Namn: **`embed`**
* Typ: **`String`**
* Klicka **`Multi`**
* Värde: **`cq.social.scf`**

   * En dialogruta öppnas. Klicka **`+`** efter varje post för att lägga till följande clientlib-kategorier:

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * Klicka **OK**

* Klicka **Spara alla**

![scf-clientlibs](assets/scf-clientlibs.png)

Så här är det `/etc/designs/an-scf-sandbox/clientlibs` ska nu visas i databasen:

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### Inkludera klientlibs i PlayPage-mallen {#include-clientlibs-in-playpage-template}

Utan att inkludera `apps.an-scf-sandbox` Kategorin ClientLibraryFolder på sidan. SCF-komponenterna fungerar inte och är inte formaterade eftersom nödvändiga JavaScript- och CSS-format inte är tillgängliga.

Utan att ta med clientlibs visas SCF-kommentarkomponenten som stylfri:

![clientlibs-comment](assets/clientlibs-comment.png)

När clientlibs för apps.an-scf-sandbox ingår formateras SCF-kommentarskomponenten:

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

Programsatsen include tillhör `head` i `html` skript. Standardvärdet **`foundation head.jsp`** innehåller ett skript som kan överlappas: **`headlibs.jsp`**.

**Copy headlibs.jsp and include clientlibs:**

1. Använda **CRXDE Lite**, markera **`/libs/foundation/components/page/headlibs.jsp`**

1. Högerklicka och välj **Kopiera** (eller välj Kopiera från verktygsfältet)
1. Välj **`/apps/an-scf-sandbox/components/playpage`**
1. Högerklicka och välj **Klistra in** (eller välj Klistra in i verktygsfältet)
1. Dubbelklicka **`headlibs.jsp`** så att du kan öppna den
1. Lägg till följande rad i slutet av filen
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. Klicka **Spara alla**

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

Läs in webbplatsen i webbläsaren och se om bakgrunden inte är en blå nyans.

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![community-play](assets/community-play.png)

### Spara ditt arbete hittills {#saving-your-work-so-far}

För närvarande finns det en minimalistisk sandlåda. Det kan vara värt att spara som ett paket så att du kan inaktivera servern när du spelar upp, om databasen blir skadad och du vill börja om. Byt namn på eller ta bort mappen crx-quickstart/, aktivera servern, ladda upp och installera det här sparade paketet och behöver inte upprepa dessa grundläggande steg.

Det här paketet finns på [Skapa en exempelsida](/help/communities/create-sample-page.md) självstudiekurs för dem som inte vill vänta och börja spela.

Så här skapar du ett paket:

* Klicka på CRXDE Lite [Paketikon](https://localhost:4502/crx/packmgr/)
* Klicka **Skapa paket**

   * Paketnamn: an-scf-sandbox-minimum-pkg
   * Version: 0.1
   * Grupp: `leave as default`
   * Klicka **OK**

* Klicka **Redigera**

   * Välj **Filter** tab

      * Klicka **Lägg till filter**
      * Rotsökväg: bläddra till `/apps/an-scf-sandbox`
      * Klicka **Klar**
      * Klicka **Lägg till filter**
      * Rotsökväg: bläddra till `/etc/designs/an-scf-sandbox`
      * Klicka **Klar**
      * Klicka **Lägg till filter**
      * Rotsökväg: bläddra till `/content/an-scf-sandbox**`
      * Klicka **Klar**

   * Klicka **Spara**

* Klicka **Bygge**

Nu kan du välja **Ladda ned** för att spara den på disk och **Överför paket** någon annanstans, och markera **Mer > Replikera** om du vill överföra sandlådan till en lokal publiceringsinstans för att utöka sandlådans sfär.
