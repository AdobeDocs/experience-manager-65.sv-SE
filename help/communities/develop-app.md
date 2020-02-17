---
title: Utveckla sandlådeprogram
seo-title: Utveckla sandlådeprogram
description: Utveckla program med hjälp av grundskript
seo-description: Utveckla program med hjälp av grundskript
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Utveckla sandlådeprogram {#develop-sandbox-application}

I det här avsnittet, nu när mallen har konfigurerats i det [inledande programavsnittet](initial-app.md) , och startsidorna i det [inledande innehållsavsnittet](initial-content.md) , kan programmet utvecklas med grundläggande skript, inklusive möjligheten att aktivera redigering med communitykomponenter. I slutet av det här avsnittet kommer webbplatsen att fungera.

## Använda skript för Foundation Page {#using-foundation-page-scripts}

Standardskriptet, som skapades när komponenten som återger uppspelningssidmallen lades till, ändras så att det innehåller bassidans head.jsp och en local body.jsp.

### Superresurstyp {#super-resource-type}

Det första steget är att lägga till en supertypsegenskap för resursen till `/apps/an-scf-sandbox/components/playpage` noden så att den ärver skripten och egenskaperna för supertypen.

Använda CRXDE Lite:

<!--Resolve steps below-->
    * Namn: `sling:resourceSuperType`
    * Typ: `
    * Värde: &quot;foundation/components/page&quot;

1. Klicka på det gröna **[!UICONTROL [+]Lägg till]**
1. Klicka på **[!UICONTROL Spara alla]**

![chlimage_1-231](assets/chlimage_1-231.png)

### Head- och body-skript {#head-and-body-scripts}

1. I rutan **CRXDE Lite** explorer navigerar du till `/apps/an-scf-sandbox/components/playpage` och dubbelklickar på filen `playpage.jsp` för att öppna den i redigeringsrutan.

#### /apps/an-scf-sandbox/components/playpage/playpage.jsp {#apps-an-scf-sandbox-components-playpage-playpage-jsp}

```xml
<%--

  An SCF Sandbox Play Component component.

  This is the component which renders content for An SCF Sandbox page.

--%><%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" %><%
%><%
 // TODO add your code here
%>
```

1. Ersätt &quot; // TODO ...&quot; eftersom du är medveten om att det finns öppna/stängda skripttaggar. med skript för huvud- och kroppsdelar i &lt;html>.

   Med den överordnade typen `foundation/components/page`kommer alla skript som inte är definierade i samma mapp att matchas till ett skript i `/apps/foundation/components/page` mappen (om det finns), annars till ett skript i `/libs/foundation/components/page` mappen.

#### /apps/an-scf-sandbox/components/playpage/playpage.jsp {#apps-an-scf-sandbox-components-playpage-playpage-jsp-1}

```xml
<%--

    An SCF Sandbox Play Component component: playpage.jsp

  This is the component which renders content for An SCF Sandbox page.

--%><%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" %>
<html>
  <cq:include script="head.jsp"/>
  <cq:include script="body.jsp"/>
</html>
```

1. Grundskriptet `head.jsp` behöver inte överlappas, men grundskriptet `body.jsp` är tomt.

   Om du vill ställa in redigering ska du lägga `body.jsp` över med ett lokalt skript och inkludera ett styckesystem (parsys) i brödtexten:

   1. navigera till `/apps/an-scf-sandbox/components`
   1. markera `playpage`noden
   1. högerklicka och välj `Create > Create File...`

      * Namn: **body.jsp**
   1. Klicka på **[!UICONTROL Spara alla]**
   Öppna `/apps/an-scf-sandbox/components/playpage/body.jsp` och klistra in följande text:

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: body.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <body>
       <h2>Community Play</h2>
       <cq:include path="par" resourceType="foundation/components/parsys" />
   </body>
   ```

1. Klicka på **[!UICONTROL Spara alla]**

**Visa sidan i en webbläsare i redigeringsläge:**

* Standardgränssnitt: [http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html](http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.md)

Du bör inte bara se rubriken **Community Play**, utan även gränssnittet för redigering av sidinnehåll.

Panelen Resurser/Komponenter visas när både sidopanelen är öppen och fönstret är tillräckligt brett för att både sidinnehållet och sidinnehållet ska kunna visas.

![chlimage_1-232](assets/chlimage_1-232.png)

* Klassiskt användargränssnitt: [http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html](http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html)

Så här visas uppspelningssidan i det klassiska användargränssnittet, inklusive med innehållssökaren (cf):

![chlimage_1-233](assets/chlimage_1-233.png)

## Communities-komponenter {#communities-components}

Om du vill aktivera communitykomponenter för redigering börjar du med att följa dessa instruktioner:

* [Åtkomst till webbgruppskomponenter](basics.md#accessing-communities-components)

I den här sandlådan börjar du med följande **webbgruppskomponenter** (aktivera genom att markera rutan):

* Kommentarer
* Forum
* Klassificering
* Recensioner
* Sammanfattning av granskningar (visning)
* Omröstning

Välj dessutom **[!UICONTROL Allmänna]** komponenter, som

* Bild
* Tabell
* Text
* Titel (Foundation)

>[!NOTE]
>
>Komponenterna som är aktiverade för sidans del lagras i databasen som värdet på egenskapen `components` för
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` nod.

## Landningssida {#landing-page}

I en flerspråkig miljö innehåller rotsidan ett skript som tolkar klientens begäran för att avgöra vilket språk som ska användas.

I det här enkla exemplet ställs rotsidan in statiskt för att dirigera om till den engelska sidan, som i framtiden kan komma att bli huvudlandningssida med en länk till uppspelningssidan.

Ändra webbläsarens URL till rotsidan: [http://localhost:4502/editor.html/content/an-scf-sandbox.html](https://locahost:4502/editor.html/content/an-scf-sandbox.html)

* Välj ikonen Sidinformation
* Välj **[!UICONTROL Öppna egenskaper]**
* På fliken AVANCERAT

   * Bläddra till **[!UICONTROL Webbplatser > SCF Sandbox Site > SCF Sandbox]**
   * Click **[!UICONTROL OK]**

* Click **[!UICONTROL OK]**

När webbplatsen har publicerats dirigeras en gång till den engelska sidan om du bläddrar till rotsidan på en publiceringsinstans.

Det sista steget innan du spelar med communitykomponenterna i SCF är att lägga till en klientbiblioteksmapp (clientlibs) ... . **[⇒](add-clientlibs.md)**