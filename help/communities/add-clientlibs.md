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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Lägg till klienter{#add-clientlibs}

## Lägg till en ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Skapa en ClientLibraryFolder med namnet `clientlibs`som innehåller den JS och CSS som används för att återge platsens sidor.

Det `categories`egenskapsvärde som anges för det här klientbiblioteket är den identifierare som används för att ta med klientlibben direkt från en innehållssida eller för att bädda in den i andra klientlibs.

1. med **CRXDE Lite**, expandera `/etc/designs`

1. högerklicka `an-scf-sandbox` och markera `Create Node`

   * Namn : `clientlibs`
   * Typ : `cq:ClientLibraryFolder`

1. click **OK**

![chlimage_1-47](assets/chlimage_1-47.png)

På fliken **Egenskaper** för den nya `clientlibs` noden anger du egenskapen **`categories`**:

* Namn: **kategorier**
* Typ: **String**
* Värde: **apps.an-scf-sandbox**
* click **Add**
* klicka på **Spara alla**

Obs! för att visa kategorivärdet med appar. är en konvention som identifierar att det ägande programmet finns i /apps-mappen, inte /libs.  VIKTIGT! Lägg till platshållare `js.tx`till filer och**`css.tx`**t. (Det är inte officiellt en cq:ClientLibraryFolder utan dem.)

1. högerklicka **`/etc/designs/an-scf-sandbox/clientlibs`**
1. välj **Skapa fil...**
1. **ange** namn: `css.txt`
1. välj **Skapa fil...**
1. **ange** namn: `js.txt`
1. klicka på **Spara alla**

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

Om du bara använder en funktion på en sida kan du inkludera den funktionens fullständiga klientlib direkt på sidan, t.ex. &lt;% ui:includeClientLib categories=cq.social.hbs.forum&quot; %>

I det här fallet är det bäst att inkludera alla och så att de mer grundläggande SCF-klientlibs som är författarens klientlibs:

* Namn : **`embed`**
* Typ : **`String`**
* click **`Multi`**
* Värde: **`cq.social.scf`***&lt;enter> öppnar en dialogruta som klickar på **[+] **efter varje inlägg för att lägga till följande kategorier för klientlib:*

   * **`cq.ckeditor`**
   * **`cq.social.author.hbs.comments`**
   * **`cq.social.author.hbs.forum`**
   * **`cq.social.author.hbs.rating`**
   * **`cq.social.author.hbs.reviews`**
   * **`cq.social.author.hbs.voting`**
   * click **OK**

* klicka på **Spara alla**

![chlimage_1-49](assets/chlimage_1-49.png)

Så här `/etc/designs/an-scf-sandbox/clientlibs` ska nu visas i databasen:

![chlimage_1-50](assets/chlimage_1-50.png)

### Inkludera klienter i PlayPage-mallen {#include-clientlibs-in-playpage-template}

Utan att ta med kategorin `apps.an-scf-sandbox` ClientLibraryFolder på sidan kommer SCF-komponenterna inte att fungera och inte formateras, eftersom de JavaScript och format som behövs inte kommer att vara tillgängliga.

Utan att ta med clientlibs visas SCF-kommentarkomponenten som stylfri:

![chlimage_1-51](assets/chlimage_1-51.png)

När clientlibs för apps.an-scf-sandbox ingår formateras SCF-kommentarskomponenten:

![chlimage_1-52](assets/chlimage_1-52.png)

Programsatsen include tillhör <head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> i <html> script. Standardvärdet **`foundation head.jsp`** innehåller ett skript som kan överlappas: **`headlibs.jsp`**.

**Copy headlibs.jsp and include clientlibs:**

1. med **CRXDE Lite**, välj **`/libs/foundation/components/page/headlibs.jsp`**

1. högerklicka och välj **Kopiera **(eller välj Kopiera från verktygsfältet)
1. select**`/apps/an-scf-sandbox/components/playpage`**
1. högerklicka och välj **Klistra in ** (eller välj Klistra in i verktygsfältet)
1. dubbelklicka **`headlibs.jsp`** för att öppna den
1. lägg till följande rad i slutet av filen
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. klicka på **Spara alla**

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

* från CRXDE Lite klickar du på [paketikonen](https://localhost:4502/crx/packmgr/)
* klicka på **Skapa paket**

   * Paketnamn: an-scf-sandbox-minimum-pkg
   * Version: 0.1
   * Grupp: &lt;lämna som standard>
   * click **OK**

* click **Edit**

   * välj **Filter **tab

      * klicka på **Lägg till filter**
      * Rotsökväg: &lt;browse to** /apps/an-scf-sandbox**>
      * klicka på **Klar**
      * klicka på **Lägg till filter**
      * Rotsökväg: &lt;bläddra till **/etc/designs/an-scf-sandbox**>
      * klicka på **Klar**
      * klicka på **Lägg till filter**
      * Rotsökväg: &lt;browse to **/content/an-scf-sandbox**>
      * klicka på **Klar**
   * click **Save**


* klicka på **Skapa**

Nu kan du välja **Hämta** för att spara den på hårddisken och **Överför paket** någon annanstans. Du kan även välja **Mer > Replikera** för att överföra sandlådan till en lokal värdpubliceringsinstans för att utöka sandlådan.