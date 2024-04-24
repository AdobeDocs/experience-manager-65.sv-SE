---
title: Utveckla sandlådeprogram
description: Lär dig hur du utvecklar ett sandlådeprogram som använder grundskript och som har funktioner för att skapa med komponenter i Communities.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Utveckla sandlådeprogram  {#develop-sandbox-application}

I det här avsnittet, nu när mallen är konfigurerad i [ursprungligt program](initial-app.md) och startsidorna i [ursprungligt innehåll](initial-content.md) kan du utveckla programmet. Det gör du genom att använda grundläggande skript som inkluderar möjligheten att aktivera redigering med komponenter i Communities. I slutet av det här avsnittet har du en webbplats som är helt funktionell.

## Använda skript för Foundation Page {#using-foundation-page-scripts}

Standardskriptet, som skapades när komponenten som återger uppspelningssidmallen lades till, ändras så att det innehåller bassidans head.jsp och en local body.jsp.

### Superresurstyp {#super-resource-type}

Det första steget är att lägga till en supertypsegenskap för resursen i `/apps/an-scf-sandbox/components/playpage` så att den ärver skripten och egenskaperna för supertypen.

Använda CRXDE Lite:

1. Välj nod `/apps/an-scf-sandbox/components/playpage`.
1. Ange en ny egenskap med följande värden på fliken Egenskaper:

   Namn: `sling:resourceSuperType`

   Typ: `String`

   Värde: `foundation/components/page`

1. Klicka på den gröna **[!UICONTROL +Add]** -knappen.
1. Klicka på **[!UICONTROL Save All]**.

   ![page-script](assets/page-script.png)

### Head- och body-skript {#head-and-body-scripts}

1. I **CRXDE Lite** utforskarfönster, navigera till `/apps/an-scf-sandbox/components/playpage` och dubbelklicka på filen `playpage.jsp` för att öppna den i redigeringsrutan.

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

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

1. Ersätt &quot; // TODO ...&quot; med `includes` skript för huvud- och kroppsdelar i &lt;html>.

   Med en överordnad typ av `foundation/components/page`, tolkas alla skript som inte är definierade i samma mapp som ett skript i `/apps/foundation/components/page` mapp (om den finns), eller till ett skript i `/libs/foundation/components/page` mapp.

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

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

1. Täcka över basskriptet `head.jsp` är inte nödvändigt, men det grundläggande skriptet `body.jsp` är tom.

   Om du vill konfigurera för redigering, övertäckning `body.jsp` med ett lokalt skript och innehåller ett styckesystem (parsys) i brödtexten:

   1. Navigera till `/apps/an-scf-sandbox/components`.
   1. Välj `playpage` nod.
   1. Högerklicka och välj `Create > Create File...`

      * Namn: **body.jsp**

   1. Klicka på **[!UICONTROL Save All]**.

   Öppna `/apps/an-scf-sandbox/components/playpage/body.jsp` och klistra in i följande text:

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

1. Klicka på **[!UICONTROL Save All]**.

**Visa sidan i en webbläsare i redigeringsläge:**

* Standardgränssnitt: `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

Du bör inte bara se rubriken **Community Play**, men även gränssnittet för redigering av sidinnehåll.

Panelen Resurser/Komponenter visas när både sidopanelen är öppen och fönstret är tillräckligt brett för att både sidinnehållet och sidinnehållet ska kunna visas.

![view-page](assets/view-page.png)

* Klassiskt användargränssnitt: `http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

Här beskrivs hur uppspelningssidan visas i det klassiska användargränssnittet, inklusive med innehållssökaren (cf):

![play-page-view](assets/play-page-view.png)

## Communities-komponenter {#communities-components}

Om du vill aktivera communitykomponenter för redigering börjar du med att följa dessa instruktioner:

* [Åtkomst till webbgruppskomponenter](basics.md#accessing-communities-components)

I den här sandlådan börjar du med dessa **Communities** komponenter (aktivera genom att markera rutan):

* Kommentar
* Forum
* Klassificering
* Recensioner
* Sammanfattning av granskningar (visning)
* Omröstning

Välj dessutom **[!UICONTROL General]** komponenter, som

* Bild
* Tabell
* Text
* Titel (Foundation)

>[!NOTE]
>
>Komponenterna som är aktiverade för sidans del lagras i databasen som värdet för `components` egenskapen för
>
>Nod `/etc/designs/an-scf-sandbox/jcr:content/playpage/par`.

## Landningssida {#landing-page}

I en flerspråkig miljö innehåller rotsidan ett skript som tolkar klientens begäran för att fastställa vilket språk som ska användas.

I det här exemplet ställs rotsidan in statiskt för att dirigera om till den engelska sidan, som kan komma att utvecklas i framtiden som huvudlandningssida med en länk till uppspelningssidan.

Ändra webbläsarens URL till rotsidan: `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* Välj ikonen Sidinformation
* Välj **[!UICONTROL Open Properties]**
* På fliken AVANCERAT

   * Bläddra till posten Omdirigering: **[!UICONTROL Websites]** > **[!UICONTROL SCF Sandbox Site]** > **[!UICONTROL SCF Sandbox]**
   * Klicka **[!UICONTROL OK]**

* Klicka **[!UICONTROL OK]**

När webbplatsen har publicerats dirigeras surfning till den engelska sidan om när du bläddrar till rotsidan för en publiceringsinstans.

Det sista steget innan du börjar spela upp med komponenterna i Community SCF är att lägga till en klientbiblioteksmapp (clientlibs) ... [Lägg till klienter](add-clientlibs.md)
