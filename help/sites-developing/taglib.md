---
title: Taggbibliotek
description: Taggbiblioteken Granite, CQ och Sling ger dig tillgång till specifika funktioner som du kan använda i JSP-skriptet för dina mallar och komponenter
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 50e608d5-951f-4a3f-bed4-9e92ff5d7bd4
solution: Experience Manager, Experience Manager Sites
feature: Developing,Tagging
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2452'
ht-degree: 0%

---

# Taggbibliotek{#tag-libraries}

Taggbiblioteken Granite, CQ och Sling ger dig tillgång till specifika funktioner som du kan använda i JSP-skriptet för dina mallar och komponenter.

## Bibliotek för Granite-taggar {#granite-tag-library}

Biblioteket med Granite-taggar innehåller användbara funktioner.

När du utvecklar jsp-skriptet för en GRA-gränssnittskomponent bör du ta med följande kod högst upp i skriptet:

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

Den globala filen deklarerar också [Sling Library](/help/sites-developing/taglib.md#sling-tag-library).

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### &lt;ui:includeClientLib> {#ui-includeclientlib}

The `<ui:includeClientLib>` tagg Innehåller ett AEM HTML-klientbibliotek, som kan vara ett js, en css eller ett temabibliotek. För flera inkluderingar av olika typer, till exempel js och css, måste den här taggen användas flera gånger i jsp. Den här taggen är ett bekvämt omslag runt ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)` tjänstgränssnitt.

Den har följande attribut:

**kategorier** - En lista med kommaavgränsade klientlibkategorier. Detta inkluderar alla JavaScript- och CSS-bibliotek för de angivna kategorierna. Temanamnet extraheras från begäran.

Motsvarar: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**tema** - En lista med kommaavgränsade klientlibkategorier. Detta inkluderar alla temarelaterade bibliotek (både CSS och JS) för de angivna kategorierna. Temanamnet extraheras från begäran.

Motsvarar: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js** - En lista med kommaavgränsade klientlibkategorier. Detta inkluderar alla JavaScript-bibliotek för de angivna kategorierna.

Motsvarar: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css** - En lista med kommaavgränsade klientlibkategorier. Detta inkluderar alla CSS-bibliotek för de angivna kategorierna.

Motsvarar: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**tema** - En flagga som endast anger teman eller icke-teman för bibliotek ska inkluderas. Om det utelämnas inkluderas båda uppsättningarna. Gäller endast rena JS- eller CSS-inkluderingar (inte för kategorier eller teman).

The `<ui:includeClientLib>` -taggen kan användas så här i en jsp:

```xml
<%-- all: js + theme (theme-js + css) --%>
<ui:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<ui:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<ui:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<ui:includeClientLib css="cq.collab.calendar, cq.security" />
```

## CQ-taggbibliotek {#cq-tag-library}

CQ-taggbiblioteket innehåller användbara funktioner.

Om du vill använda CQ-taggbiblioteket i skriptet måste skriptet börja med följande kod:

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>När `/libs/foundation/global.jsp` -filen inkluderas i skriptet, taglib deklareras automatiskt.

När du utvecklar jsp-skriptet för en AEM bör du ta med följande kod högst upp i skriptet:

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

Den deklarerar sling-, CQ- och jstl-taggarna och visar de skriptobjekt som används ofta och definieras av [`<cq:defineObjects />`](#amp-lt-cq-defineobjects) -tagg. Detta förkortar och förenklar jsp-koden för komponenten.

### &lt;cq:text> {#cq-text}

The `<cq:text>` -taggen är en praktisk tagg som visar komponenttext i en JSP.

Den har följande valfria attribut:

**property** - Namnet på den egenskap som ska användas. Namnet är relativt till den aktuella resursen.

**value** - Värde som ska användas för utdata. Om det här attributet finns skrivs användningen av egenskapsattributet över.

**oldValue** - Värde som ska användas för differensutdata. Om det här attributet finns skrivs användningen av egenskapsattributet över.

**escapeXml** - Definierar om tecknen &lt;, >, &amp;, &#39; och &quot; i den resulterande strängen ska konverteras till motsvarande teckenentitetskoder. Standardvärdet är false. Den nya inställningen används efter den valfria formateringen.

**format** - Valfritt java.text.Format som ska användas för att formatera texten.

**noDiff** - Utelämnar beräkningen av ett diff-resultat, även om det finns en diff-information.

**tagClass** - CSS-klassnamn för ett element som omger utdata som inte är tomma. Om det är tomt läggs inget element till.

**tagName** - Namnet på det element som omger ett utdata som inte är tomt. Som standard är det DIV.

**platshållare** - Standardvärde som används för null eller tom text i redigeringsläge, det vill säga platshållaren. Standardkontrollen utförs efter den valfria formateringen och escape-konverteringen, d.v.s. efter att utdata har skrivits som de är. Standardvärdet är:

`<div><span class="cq-text-placeholder">&para;</span></div>`

**standard** - Standardvärde som ska användas för null eller tom text. Standardkontrollen utförs efter den valfria formateringen och escape-konverteringen, d.v.s. efter att utdata har skrivits som de är.

Några exempel på hur `<cq:text>` -taggen kan användas i en JSP:

```xml
<cq:text property="jcr:title" tagName="h2"/>
<cq:text property="jcr:description" tagName="p"/>

<cq:text value="<%= listItem.getTitle() %>" tagName="h4" placeholder="" />
<cq:text value="<%= listItem.getDescription() %>" tagName="p" placeholder=""/>

<cq:text property="jcr:title" value="<%= title %>" tagName="h3"/><%
    } else if (type.equals("link")) {
        %><cq:text property="jcr:title" value="<%= "\u00bb " + title %>" tagName="p" tagClass="link"/><%
    } else if (type.equals("extralarge")) {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h1"/><%
    } else {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h2"/><%

<cq:text property="jcr:description" placeholder="" tagName="small"/>

<cq:text property="tableData"
               escapeXml="false"
               placeholder="<img src=\"/libs/cq/ui/resources/0.gif\" class=\"cq-table-placeholder\" alt=\"\">"
    />

<cq:text property="text"/>

<cq:text property="image/jcr:description" placeholder="" tagName="small"/>
<cq:text property="text" tagClass="text"/>
```

### &lt;cq:setContentBundle> {#cq-setcontentbundle}

The `<cq:setContentBundle>` -taggen skapar en i18n-lokaliseringskontext och lagrar den i `javax.servlet.jsp.jstl.fmt.localizationContext` konfigurationsvariabel.

Den har följande attribut:

**språk** - Språket för det språkområde som resurspaketet ska hämtas för.

**källa** - Källan varifrån språkinställningen ska hämtas. Den kan ställas in på ett av följande värden:

* **static** - språkinställningen hämtas från `language` om det är tillgängligt, annars från serverns standardspråkområde.

* **page** - språkinställningen hämtas från den aktuella sidans eller resursens språk, om tillgängligt, annars från `language` om det är tillgängligt, annars från serverns standardspråkområde.

* **förfrågan** - språkinställningen hämtas från den begärda språkinställningen ( `request.getLocale()`).

* **auto** - språkinställningen hämtas från `language` om tillgängligt, annars från den aktuella sidans eller resursens språk, om tillgängligt, i annat fall från begäran.

Om `source` inget attribut har angetts:

* Om `language` -attribut anges, `source` som standard är &quot; `static`.

* Om `language` inget attribut har angetts, `source` som standard för attribut till `auto`.

Innehållspaketet kan användas av standard-JSTL `<fmt:message>` -taggar. Nyckelsökningen efter meddelanden är två gånger:

1. Först genomsöks JCR-egenskaperna för den underliggande resurs som återges efter översättningar. På så sätt kan du definiera en enkel komponentdialogruta för att redigera dessa värden.
1. Om noden inte innehåller någon egenskap med namnet exakt som nyckeln, är reservdelen att läsa in ett resurspaket från försäljningsbegäran ( `SlingHttpServletRequest.getResourceBundle(Locale)`). Språket eller språkområdet för det här paketet definieras av språk- och källattributen för `<cq:setContentBundle>` -tagg.

The `<cq:setContentBundle>` -taggen kan användas på följande sätt i ett jsp.

För sidor som definierar språk:

```xml
... %><cq:setContentBundle source="page"/><%  %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

För användaranpassade sidor:

```xml
... %><cq:setContentBundle scope="request"/><% %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

### &lt;cq:include> {#cq-include}

The `<cq:include>` -taggen innehåller en resurs på den aktuella sidan.

Den har följande attribut:

**flush**

* Ett booleskt värde som anger om utdata ska rensas innan målet tas med.

**bana**

* Sökvägen till det resursobjekt som ska inkluderas i den aktuella bearbetningen av begäran. Om den här sökvägen är relativ läggs den till i sökvägen till den aktuella resursen vars skript innehåller den angivna resursen. Sökväg och resourceType, eller skript måste anges.

**resourceType**

* Resurstypen för resursen som ska inkluderas. Om resurstypen anges måste sökvägen vara den exakta sökvägen till ett resursobjekt: i det här fallet stöds inte tillägg av parametrar, väljare och tillägg till sökvägen.
* Om resursen som ska inkluderas anges med sökvägsattributet som inte kan matchas för en resurs, kan taggen skapa ett syntetiskt resursobjekt från sökvägen och den här resurstypen.
* Sökväg och resourceType, eller skript måste anges.

**script**

* Det jsp-skript som ska inkluderas. Sökväg och resourceType, eller skript måste anges.

**ignoreComponentHierarchy**

* Ett booleskt värde som styr om komponenthierarkin ska ignoreras för skriptupplösning. Om true respekteras bara sökvägarna.

**Exempel:**

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><div class="center">
    <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
    <cq:include path="title" resourceType="foundation/components/title" />
    <cq:include script="redirect.jsp"/>
    <cq:include path="par" resourceType="foundation/components/parsys" />
</div>
```

Ska du använda `<%@ include file="myScript.jsp" %>` eller `<cq:include script="myScript.jsp" %>` om du vill inkludera ett skript?

* The `<%@ include file="myScript.jsp" %>` -direktivet informerar JSP-kompilatorn om att inkludera en fullständig fil i den aktuella filen. Det är som om innehållet i den inkluderade filen klistrades in direkt i originalfilen.
* Med `<cq:include script="myScript.jsp">` -taggen inkluderas filen vid körning.

Ska du använda `<cq:include>` eller `<sling:include>`?

* När du utvecklar AEM bör du använda `<cq:include>`.
* `<cq:include>` I kan du direkt inkludera skriptfiler efter deras namn när du använder skriptattributet. Detta tar hänsyn till arv av komponent- och resurstyp och är ofta enklare än att följa Sling:s skriptupplösning med väljare och tillägg.

### &lt;cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` Borttagen sedan AEM 5.6. [`<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) ska användas istället.

The `<cq:includeClientLib>` tagg Innehåller ett AEM HTML-klientbibliotek, som kan vara ett js, en css eller ett temabibliotek. För flera inkluderingar av olika typer, till exempel js och css, måste den här taggen användas flera gånger i jsp. Den här taggen är ett bekvämt omslag runt `com.day.cq.widget.HtmlLibraryManager` tjänstgränssnitt.

Den har följande attribut:

**kategorier** - En lista med kommaavgränsade klientlibkategorier. Detta inkluderar alla JavaScript- och CSS-bibliotek för de angivna kategorierna. Temanamnet extraheras från begäran.

Motsvarar: `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**tema** - En lista med kommaavgränsade klientlibkategorier. Detta inkluderar alla temarelaterade bibliotek (både CSS och JS) för de angivna kategorierna. Temanamnet extraheras från begäran.

Motsvarar: `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js** - En lista med kommaavgränsade klientlibkategorier. Detta inkluderar alla JavaScript-bibliotek för de angivna kategorierna.

Motsvarar: `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css** - En lista med kommaavgränsade klientlibkategorier. Detta inkluderar alla CSS-bibliotek för de angivna kategorierna.

Motsvarar: `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**tema** - En flagga som endast anger teman eller icke-teman för bibliotek ska inkluderas. Om det utelämnas inkluderas båda uppsättningarna. Gäller endast rena JS- eller CSS-inkluderingar (inte för kategorier eller teman).

The `<cq:includeClientLib>` -taggen kan användas så här i en jsp:

```xml
<%-- all: js + theme (theme-js + css) --%>
<cq:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<cq:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<cq:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<cq:includeClientLib css="cq.collab.calendar, cq.security" />
```

### &lt;cq:defineObjects> {#cq-defineobjects}

The `<cq:defineObjects>` -taggen visar följande, ofta använda, skriptobjekt som utvecklaren kan referera till. Objekten som definieras av [`<sling:defineObjects>`](#amp-lt-sling-defineobjects) -tagg.

**componentContext**

* det aktuella komponentkontextobjektet för begäran (com.day.cq.wcm.api.components.ComponentContext interface).

**komponent**

* det aktuella AEM-komponentobjektet för den aktuella resursen (com.day.cq.wcm.api.components.Component interface).

**currentDesign**

* den aktuella sidans designobjekt (com.day.cq.wcm.api.designer.Design-gränssnitt).

**currentPage**

* det aktuella AEM WCM-sidobjektet (com.day.cq.wcm.api.Page interface).

**currentStyle**

* det aktuella formatobjektet för den aktuella cellen (com.day.cq.wcm.api.designer.Style-gränssnitt).

**designer**

* det designer-objekt som används för att komma åt designinformation (com.day.cq.wcm.api.designer.Designer-gränssnitt).

**editContext**

* Redigera context-objektet för AEM (com.day.cq.wcm.api.components.EditContext interface).

**pageManager**

* sidhanterarobjektet för åtgärder på sidnivå (com.day.cq.wcm.api.PageManager-gränssnittet).

**pageProperties**

* sidegenskapsobjektet för den aktuella sidan (org.apache.sling.api.resource.ValueMap).

**egenskaper**

* egenskapsobjektet för den aktuella resursen (org.apache.sling.api.resource.ValueMap).

**resourceDesign**

* Resurssidans design-objekt (com.day.cq.wcm.api.designer.Design-gränssnitt).

**resourcePage**

* resurssidans objekt (com.day.cq.wcm.api.Page interface).
* Den har följande attribut:

**requestName**

* ärvd från sling

**responseName**

* ärvd från sling

**resourceName**

* ärvd från sling

**nodeName**

* ärvd från sling

**logName**

* ärvd från sling

**resourceResolverName**

* ärvd från sling

**slingName**

* ärvd från sling

**componentContextName**

* specifikt för wcm

**editContextName**

* specifikt för wcm

**propertiesName**

* specifikt för wcm

**pageManagerName**

* specifikt för wcm

**currentPageName**

* specifikt för wcm

**resourcePageName**

* specifikt för wcm

**pagePropertiesName**

* specifikt för wcm

**componentName**

* specifikt för wcm

**designerName**

* specifikt för wcm

**currentDesignName**

* specifikt för wcm

**resourceDesignName**

* specifikt för wcm

**currentStyleName**

* specifikt för wcm

**Exempel**

```xml
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%@ page import="com.day.cq.wcm.api.WCMMode" %><%
%><%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><cq:defineObjects/>
```

>[!NOTE]
>
>När `/libs/foundation/global.jsp` filen ingår i skriptet, `<cq:defineObjects />` -taggen inkluderas automatiskt.

### &lt;cq:requestURL> {#cq-requesturl}

The `<cq:requestURL>` -taggen skriver den aktuella begärande-URL:en till JspWriter. De två taggarna [`<cq:addParam>`](#amp-lt-cq-addparam) och [`<cq:removeParam>`](#amp-lt-cq-removeparam) och kan användas inuti den här taggens brödtext för att ändra den aktuella begärande-URL:en innan den skrivs.

Du kan skapa länkar till den aktuella sidan med olika parametrar. Du kan till exempel omvandla din begäran:

`mypage.html?mode=view&query=something` till `mypage.html?query=something`.

Användning av `addParam` eller `removeParam` ändrar bara förekomsten av den angivna parametern, övriga parametrar påverkas inte.

`<cq:requestURL>` saknar attribut.

Exempel:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:addParam> {#cq-addparam}

The `<cq:addParam>` lägger till en request-parameter med det angivna namnet och värdet i det omslutande [`<cq:requestURL>`](#amp-lt-cq-requesturl) -tagg.

Den har följande attribut:

**name**

* namnet på den parameter som ska läggas till

**value**

* värdet på parametern som ska läggas till

**Exempel:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:removeParam> {#cq-removeparam}

The `<cq:removeParam>` taggen tar bort en request-parameter med det angivna namnet och värdet från den omslutande [`<cq:requestURL>`](#amp-lt-cq-requesturl) -tagg. Om inget värde anges tas alla parametrar med det angivna namnet bort.

Den har följande attribut:

**name**

* namnet på den parameter som ska tas bort

Exempel:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Sling Tag Library {#sling-tag-library}

Sling-taggbiblioteket innehåller användbara Sling-funktioner.

När du använder Sling Tag Library i skriptet måste skriptet börja med följande kod:

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>När `/libs/foundation/global.jsp` -filen inkluderas i skriptet, så deklareras sling-taglib automatiskt.

### &lt;sling:include> {#sling-include}

The `<sling:include>` -taggen innehåller en resurs på den aktuella sidan.

Den har följande attribut:

**flush**

* Ett booleskt värde som anger om utdata ska rensas innan målet tas med.

**resurs**

* Resursobjektet som ska inkluderas i den aktuella begärandebearbetningen. Resurs eller sökväg måste anges. Om båda anges prioriteras resursen.

**bana**

* Sökvägen till det resursobjekt som ska inkluderas i den aktuella bearbetningen av begäran. Om den här sökvägen är relativ läggs den till i sökvägen till den aktuella resursen vars skript innehåller den angivna resursen. Resurs eller sökväg måste anges. Om båda anges prioriteras resursen.

**resourceType**

* Resurstypen för resursen som ska inkluderas. Om resurstypen anges måste sökvägen vara den exakta sökvägen till ett resursobjekt: i det här fallet stöds inte tillägg av parametrar, väljare och tillägg till sökvägen.
* Om resursen som ska inkluderas anges med sökvägsattributet som inte kan matchas för en resurs, kan taggen skapa ett syntetiskt resursobjekt från sökvägen och den här resurstypen.

**replaceSelectors**

* När väljarna skickas ersätts de med värdet för det här attributet.

**addSelectors**

* När du skickar läggs värdet för det här attributet till i väljarna.

**replaceSuffix**

* När suffixet skickas ersätts det av attributets värde.

>[!NOTE]
>
>Resursens och skriptets upplösning som ingår i `<sling:include>` -taggen är densamma som för en vanlig sling-URL-upplösning. Som standard används väljarna, tillägget och så vidare från den aktuella begäran även för det inkluderade skriptet. De kan ändras med taggattributen: `replaceSelectors="foo.bar"` gör att du kan skriva över väljarna.

Exempel:

```xml
<div class="item"><sling:include path="<%= pathtoinclude %>"/></div>
```

```xml
<sling:include resource="<%= par %>"/>
```

```xml
<sling:include addSelectors="spool"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include replaceSelectors="content" />
```

### &lt;sling:defineObjects> {#sling-defineobjects}

The `<sling:defineObjects>` -taggen visar följande, ofta använda, skriptobjekt som utvecklaren kan referera till:

**slingRequest**

* SlingHttpServletRequest-objekt som ger åtkomst till rubrikinformationen för HTTP-begäran - utökar HttpServletRequest-standarden och ger åtkomst till Sling-specifika saker som resurs, sökvägsinformation och väljare.

**slingResponse**

* SlingHttpServletResponse-objekt som ger åtkomst till HTTP-svaret som skapas av servern. Detta är samma som det HttpServletResponse som det utökas från.**förfrågan**
* Standardobjektet för JSP-begäran, som är en ren HttpServletRequest.**svar**
* Standardsvarsobjektet för JSP som är ett rent HttpServletResponse.

**resourceResolver**

* Det aktuella ResourceResolver-objektet. Det är samma som slingRequest.getResourceResolver()

.**sling**

* Ett SlingScriptHelper-objekt som innehåller praktiska metoder för skript, huvudsakligen sling.include(&#39;/some/other/resource&#39;) för att inkludera svar från andra resurser i det här svaret (till exempel inbäddning av HTML-rubrikfragment) och sling.getService(foo.bar.Service.class) för att hämta OSGi-tjänster som är tillgängliga i Sling (klassnotation beroende på skriptspråk).

**resurs**

* det aktuella resursobjekt som ska hanteras, beroende på URL:en för begäran. Det är samma som slingRequest.getResource().

**currentNode**

* Om den aktuella resursen pekar på en JCR-nod (vilket vanligtvis är fallet i Sling) ger detta direktåtkomst till nodobjektet. I annat fall är det här objektet inte definierat.

**logg**

* Innehåller en SLF4J-loggare för loggning till Sling-loggsystemet från skript, till exempel log.info(&quot;Kör mitt skript&quot;).

* Den har följande attribut:

**requestName**

**responseName**

**nodeName**

l **ogName resourceResolverName**

**slingName**

**Exempel:**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## JSTL-taggbibliotek {#jstl-tag-library}

The [JavaServer Pages Standard Tag Library](https://www.oracle.com/java/technologies/java-server-tag-library.html) innehåller många användbara och standardtaggar. Märkorden core, formatting och functions definieras av `/libs/foundation/global.jsp` som i följande kodutdrag.

### Extract of /libs/foundation/global.jsp {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

Efter import av `/libs/foundation/global.jsp` så som beskrivs ovan kan du använda `c`, `fmt` och `fn` -prefix för att komma åt dessa taglibs. JSTL:s officiella dokumentation finns på [Självstudiekursen Java™ EE 5 - JavaServer Pages Standard Tag Library](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html).
