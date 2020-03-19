---
title: Lägg till klienter
seo-title: Lägg till klienter
description: Lägg till en ClientLibraryFolder
seo-description: Lägg till en ClientLibraryFolder
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# Lägg till klienter {#add-clientlibs}

## Lägg till en ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Skapa en ClientLibraryFolder med namnet `clientlibs`som innehåller den JS och CSS som används för att återge platsens sidor.

Det `categories`egenskapsvärde som anges för det här klientbiblioteket är den identifierare som används för att ta med klientlibben direkt från en innehållssida eller för att bädda in den i andra klientlibs.

1. Expandera med **CRXDE Lite**`/etc/designs`

1. Högerklicka `an-scf-sandbox` och välj `Create Node`

   * Namn : `clientlibs`
   * Typ : `cq:ClientLibraryFolder`

1. Click **OK**

![chlimage_1-47](assets/chlimage_1-47.png)

På fliken **Egenskaper** för den nya `clientlibs` noden anger du egenskapen **categories** :

* Namn: **kategorier**
* Typ: **String**
* Värde: **apps.an-scf-sandbox**
* Click **Add**
* Klicka på **Spara alla**

Obs! för att visa kategorivärdet med appar. är en konvention som identifierar att det ägande programmet finns i /apps-mappen, inte /libs.  VIKTIGT! Lägg till platshållare `js.tx`för **`css.txt`** filer. (Det är inte officiellt en cq:ClientLibraryFolder utan dem.)

1. Högerklicka **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Välj **Skapa fil..**
1. Ange **namn:** `css.txt`
1. Välj **Skapa fil..**
1. Ange **namn:** `js.txt`
1. Klicka på **Spara alla**

![chlimage_1-48](assets/chlimage_1-48.png)

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

På fliken **Egenskaper** för `clientlibs` noden anger du strängegenskapen **embed** med flera värden. Detta bäddar in nödvändiga [klientbibliotek (klientlibs) för SCF-komponenter](/help/communities/client-customize.md#clientlibs-for-scf). I den här självstudiekursen har många av de klientlibs som behövs för webbkomponenterna lagts till.

**Observera** att detta kan vara det önskade tillvägagångssättet för en produktionsplats, eftersom det kan vara en god idé jämfört med storleken/hastigheten på de klienter som laddas ned för varje sida.

Om du bara använder en funktion på en sida kan du inkludera den funktionens fullständiga klientlib direkt på sidan, t.ex.

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

I det här fallet är det bäst att inkludera alla och så att de mer grundläggande SCF-klientlibs som är författarens klientlibs:

* Namn : **`embed`**
* Typ : **`String`**
* Klicka på **`Multi`**
* Värde: **`cq.social.scf`**

   * Den öppnar en dialogruta och klickar **`+`** efter varje post för att lägga till följande clientlib-kategorier:

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * click **OK**

* Klicka på **Spara alla**

![chlimage_1-49](assets/chlimage_1-49.png)

Så här `/etc/designs/an-scf-sandbox/clientlibs` ska nu visas i databasen:

![chlimage_1-50](assets/chlimage_1-50.png)

### Inkludera klienter i PlayPage-mallen {#include-clientlibs-in-playpage-template}

Utan att ta med kategorin `apps.an-scf-sandbox` ClientLibraryFolder på sidan kommer SCF-komponenterna inte att fungera och inte formateras, eftersom de JavaScript och format som behövs inte kommer att vara tillgängliga.

Utan att ta med clientlibs visas SCF-kommentarkomponenten som stylfri:

![chlimage_1-51](assets/chlimage_1-51.png)

När clientlibs för apps.an-scf-sandbox ingår formateras SCF-kommentarskomponenten:

![chlimage_1-52](assets/chlimage_1-52.png)

Programsatsen include tillhör i `head` avsnittet i `html` skriptet. Standardvärdet **`foundation head.jsp`** innehåller ett skript som kan överlappas: **`headlibs.jsp`**.

**Copy headlibs.jsp and include clientlibs:**

1. Med **CRXDE Lite** väljer du **`/libs/foundation/components/page/headlibs.jsp`**

1. Högerklicka och välj **Kopiera** (eller välj Kopiera i verktygsfältet)
1. Välj **`/apps/an-scf-sandbox/components/playpage`**
1. Högerklicka och välj **Klistra in** (eller välj Klistra in i verktygsfältet)
1. Dubbelklicka **`headlibs.jsp`** för att öppna den
1. Lägg till följande rad i slutet av filen
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. Klicka på **Spara alla**

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

![chlimage_1-53](assets/chlimage_1-53.png)

### Spara ditt arbete hittills {#saving-your-work-so-far}

I det här läget finns det en minimalistisk sandlåda och det kan vara värt att spara som ett paket så att du, när du spelar upp, kan aktivera servern om databasen blir skadad och du vill börja om, stänga av servern, byta namn på eller ta bort mappen crx-quickstart/, aktivera servern, ladda upp och installera det här sparade paketet och inte behöver upprepa dessa mest grundläggande steg.

Paketet finns i självstudiekursen [Skapa en exempelsida](/help/communities/create-sample-page.md) för dem som inte vill vänta på att bara hoppa in och börja spela upp!..

Så här skapar du ett paket:

* Från CRXDE Lite klickar du på [paketikonen](https://localhost:4502/crx/packmgr/)
* Klicka på **Skapa paket**

   * Paketnamn: an-scf-sandbox-minimum-pkg
   * Version: 0.1
   * Grupp: `leave as default`
   * Click **OK**

* Click **Edit**

   * Välj **fliken Filter**

      * Klicka på **Lägg till filter**
      * Rotsökväg: bläddra till `/apps/an-scf-sandbox`
      * Klicka på **Klar**
      * Klicka på **Lägg till filter**
      * Rotsökväg: bläddra till `/etc/designs/an-scf-sandbox`
      * Klicka på **Klar**
      * Klicka på **Lägg till filter**
      * Rotsökväg: bläddra till `/content/an-scf-sandbox**`
      * Klicka på **Klar**
   * Click **Save**


* Klicka på **Skapa**

Nu kan du välja **Hämta** för att spara den på hårddisken och **Överför paket** någon annanstans. Du kan även välja **Mer > Replikera** för att överföra sandlådan till en lokal värdpubliceringsinstans för att utöka sandlådan.