---
title: Utveckla för riktat innehåll
seo-title: Utveckla för riktat innehåll
description: Ämnen om utveckling av komponenter för användning med målinriktning mot innehåll
seo-description: Ämnen om utveckling av komponenter för användning med målinriktning mot innehåll
uuid: 2449347e-7e1c-427b-a5b0-561055186934
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bff078cd-c390-4870-ad1d-192807c67ca4
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Utveckla för riktat innehåll{#developing-for-targeted-content}

I det här avsnittet beskrivs ämnen om utveckling av komponenter för användning med målinriktning mot innehåll.

* Mer information om hur du ansluter till Adobe Target finns i [Integrera med Adobe Target](/help/sites-administering/target.md).
* Mer information om att skapa riktat innehåll finns i [Skapa riktat innehåll med målläge](/help/sites-authoring/content-targeting-touch.md).

>[!NOTE]
>
>När du riktar in dig på en komponent i AEM-författaren gör komponenten ett antal serveranrop till Adobe Target för att registrera kampanjen, konfigurera erbjudanden och hämta Adobe Target-segment (om de är konfigurerade). Inga serversamtal görs från AEM-publicering till Adobe Target.

## Aktivera målgruppsanpassning med Adobe Target på dina sidor {#enabling-targeting-with-adobe-target-on-your-pages}

Om du vill använda målkomponenter på dina sidor som interagerar med Adobe Target, ska du inkludera specifik klientkod i &lt;head>-elementet.

### Huvudsektionen {#the-head-section}

Lägg till båda följande kodblock i &lt;head>-avsnittet på sidan:

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

Den här koden lägger till de nödvändiga JavaScript-analysobjekten och läser in molntjänstbiblioteken som är kopplade till webbplatsen. För måltjänsten läses biblioteken in via `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

Den inlästa biblioteksuppsättningen beror på vilken typ av målklientbibliotek (mbox.js eller at.js) som används i målkonfigurationen:

**Som standard mbox.js**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/mbox.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**För anpassad mbox.js**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/mbox.js"></script>
        <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**For at.js**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs.js"></script>
```

>[!NOTE]
>
>Det går endast att använda den version av produkten som `at.js` levereras tillsammans. Den version av produkten som `at.js` levererades kan hämtas genom att man tittar på `at.js` filen på platsen:
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**.

**För anpassad at.js**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

Target-funktionen på klientsidan hanteras av `CQ_Analytics.TestTarget` objektet. Därför kommer sidan att innehålla init-kod som i följande exempel:

```
<script type="text/javascript">
            if ( !window.CQ_Analytics ) {
                window.CQ_Analytics = {};
            }
            if ( !CQ_Analytics.TestTarget ) {
                CQ_Analytics.TestTarget = {};
            }
            CQ_Analytics.TestTarget.clientCode = 'my_client_code';
        </script>
      ...

    <div class="cloudservice testandtarget">
  <script type="text/javascript">
  CQ_Analytics.TestTarget.maxProfileParams = 11;

  if (CQ_Analytics.CCM) {
   if (CQ_Analytics.CCM.areStoresInitialized) {
    CQ_Analytics.TestTarget.registerMboxUpdateCalls();
   } else {
    CQ_Analytics.CCM.addListener("storesinitialize", function (e) {
     CQ_Analytics.TestTarget.registerMboxUpdateCalls();
    });
   }
  } else {
   // client context not there, still register calls
   CQ_Analytics.TestTarget.registerMboxUpdateCalls();
  }
  </script>
 </div>
```

JSP lägger till de nödvändiga JavaScript-analysobjekten och referenserna i javascript-bibliotek på klientsidan. Filen testandtarget.js innehåller funktionerna mbox.js. HTML-koden som skriptet genererar liknar följande exempel:

```xml
<script type="text/javascript">
        if ( !window.CQ_Analytics ) {
            window.CQ_Analytics = {};
        }
        if ( !CQ_Analytics.TestTarget ) {
            CQ_Analytics.TestTarget = {};
        }
        CQ_Analytics.TestTarget.clientCode = 'MyClientCode';
</script>
<link rel="stylesheet" href="/etc/clientlibs/foundation/testandtarget/testandtarget.css" type="text/css">
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/testandtarget.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/init.js"></script>
```

#### The body Section (start) {#the-body-section-start}

Lägg till följande kod omedelbart efter &lt;body>-taggen för att lägga till klientkontextfunktionerna på sidan:

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### The body Section (end) {#the-body-section-end}

Lägg till följande kod omedelbart före &lt;/body>-sluttaggen:

```xml
<cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
```

JSP-skriptet för den här komponenten genererar anrop till Target javascript API och implementerar andra nödvändiga konfigurationer. HTML-koden som skriptet genererar liknar följande exempel:

```xml
<div class="servicecomponents cloudservices">
  <div class="cloudservice testandtarget">
    <script type="text/javascript">
      CQ_Analytics.TestTarget.maxProfileParams = 11;
      CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
        CQ_Analytics.TestTarget.registerMboxUpdateCalls();
      });
    </script>
    <div id="cq-analytics-texthint" style="background:white; padding:0 10px; display:none;">
      <h3 class="cq-texthint-placeholder">Component clientcontext is missing or misplaced.</h3>
    </div>
    <script type="text/javascript">
      $CQ(function(){
      if( CQ_Analytics &&
          CQ_Analytics.ClientContextMgr &&
          !CQ_Analytics.ClientContextMgr.isConfigLoaded )
        {
          $CQ("#cq-analytics-texthint").show();
        }
      });
    </script>
  </div>
</div>
```

### Använda en anpassad målbiblioteksfil {#using-a-custom-target-library-file}

>[!NOTE]
>
>Om du inte använder DTM eller något annat målmarknadsföringssystem kan du använda anpassade målbiblioteksfiler.

>[!NOTE]
>
>Som standard är rutor dolda - klassen mboxDefault bestämmer detta beteende. Genom att dölja kryssrutor kan besökarna inte se standardinnehållet innan det byts ut. Men om du döljer lådor påverkas upplevda prestanda.

Standardfilen mbox.js som används för att skapa mbox finns på /etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js. Om du vill använda filen mbox.js för en kund lägger du till filen i molnkonfigurationen för Target. Om du vill lägga till filen måste filen mbox.js vara tillgänglig i filsystemet.

Om du till exempel vill använda [Marketing Cloud ID-tjänsten](https://marketing.adobe.com/resources/help/en_US/mcvid/) måste du hämta mbox.js så att den innehåller rätt värde för `imsOrgID` variabeln, som baseras på din klientorganisation. Den här variabeln krävs för integrering med Marketing Cloud ID-tjänsten. Mer information finns i [Adobe Analytics som rapportkälla för Adobe Target](https://marketing.adobe.com/resources/help/en_US/target/a4t/a4t.html) och [Innan du implementerar](https://marketing.adobe.com/resources/help/en_US/target/a4t/c_before_implement.html).

>[!NOTE]
>
>Om en anpassad mbox definieras i en Target-konfiguration måste alla ha läsåtkomst till **/etc/molntjänster** på publiceringsservrar. Utan den här åtkomsten uppstår ett 404-fel när mbox.js-filer läses in på publiceringswebbplatsen.

1. Gå till CQ- **verktygssidan** och välj **Cloud Services**. ([https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
1. Välj Adobe Target i trädet och dubbelklicka på målkonfigurationen i listan över konfigurationer.
1. Klicka på Redigera på konfigurationssidan.
1. För egenskapen Custom mbox.js klickar du på Browse och väljer filen.
1. Om du vill använda ändringarna anger du lösenordet för ditt Adobe Target-konto, klickar på Anslut till mål igen och klickar på OK när anslutningen lyckas. Klicka sedan på OK i dialogrutan Redigera komponent.

Målkonfigurationen innehåller en anpassad mbox.js-fil. Koden [som krävs i huvudsektionen](/help/sites-developing/target.md#p-the-head-section-p) på sidan lägger till filen i klientbibliotekets ramverk i stället för en referens till biblioteket testandtarget.js.

## Inaktivera målkommandot för komponenter {#disabling-the-target-command-for-components}

De flesta komponenter kan konverteras till målkomponenter med hjälp av kommandot Mål på snabbmenyn.

![chlimage_1-21](assets/chlimage_1-21.png)

Om du vill ta bort kommandot Target från snabbmenyn lägger du till följande egenskap i cq:editConfig-noden för komponenten:

* Namn: cq:disableTargeting
* Typ:Boolean
* Värde:True

Om du till exempel vill inaktivera mål för titelkomponenterna på sidorna Geometrixx Demo Site lägger du till egenskapen i noden /apps/geometrixx/components/title/cq:editConfig.

![chlimage_1-22](assets/chlimage_1-22.png)

## Skicka orderbekräftelseinformation till Adobe Target {#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>Om du inte använder DTM skickar du en orderbekräftelse till Adobe Target.

Om du vill följa upp hur webbplatsen fungerar skickar du inköpsinformation från orderbekräftelsesidan till Adobe Target. (Se [Skapa en orderConfirmPage Mbox](https://marketing.adobe.com/resources/help/en_US/dtm/target/order-confirmation-mbox.html) i dokumentationen för Adobe Target.) Adobe Target identifierar mbox-data som orderbekräftelsedata när ditt MBox-namn är `orderConfirmPage` och använder följande specifika parameternamn:

* productPurchasedId: En lista med ID:n som identifierar de köpta produkterna.
* orderId: Orderns ID.
* orderTotal: Det totala beloppet för köpet.

Koden på den återgivna HTML-sidan som skapar mbox liknar följande exempel:

```xml
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=product1 product2 product3',
     'orderId=order1234',
     'orderTotal=24.54');
</script>
```

Värdena för varje parameter är olika för varje ordning. Därför behöver du en komponent som genererar koden baserat på inköpets egenskaper. CQ [eCommerce Integration Framework](/help/sites-administering/ecommerce.md) gör att du kan integrera med din produktkatalog och implementera en kundvagn- och kassasida.

Exemplet Geometrixx Outdoor visar följande bekräftelsesida när en besökare köper produkter:

![chlimage_1-23](assets/chlimage_1-23.png)

Följande kod för JSP-skriptet för en komponent öppnar egenskaperna för kundvagnen och skriver sedan ut koden för att skapa mbox.

```java
<%--

  confirmationmbox component.

--%><%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"
          import="com.adobe.cq.commerce.api.CommerceService,
                  com.adobe.cq.commerce.api.CommerceSession,
                  com.adobe.cq.commerce.common.PriceFilter,
                  com.adobe.cq.commerce.api.Product,
                  java.util.List, java.util.Iterator"%><%

/* obtain the CommerceSession object */
CommerceService commerceservice = resource.adaptTo(CommerceService.class);
CommerceSession session = commerceservice.login(slingRequest, slingResponse);

/* obtain the cart items */
List<CommerceSession.CartEntry> entries = session.getCartEntries();
Iterator<CommerceSession.CartEntry> cartiterator = entries.iterator();

/* iterate the items and get the product IDs */
String productIDs = new String();
while(cartiterator.hasNext()){
 CommerceSession.CartEntry entry = cartiterator.next();
 productIDs = productIDs + entry.getProduct().getSKU();
    if (cartiterator.hasNext()) productIDs = productIDs + ", ";
}

/* get the cart price and orderID */
String total = session.getCartPrice(new PriceFilter("CART", "PRE_TAX"));
String orderID = session.getOrderId();

%><div class="mboxDefault"></div>
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=<%= productIDs %>',
     'orderId=<%= orderID %>',
     'orderTotal=<%= total %>');
</script>
```

När komponenten inkluderas på utcheckningssidan i föregående exempel innehåller sidkällan följande skript som skapar mbox:

```
<div class="mboxDefault"></div>
<script type="text/javascript">

     mboxCreate('orderConfirmPage',
     'productPurchasedId=47638-S, 46587',
     'orderId=d03cb015-c30f-4bae-ab12-1d62b4d105ca',
     'orderTotal=US$677.00');

</script>
```

## Förstå målkomponenten {#understanding-the-target-component}

Med Target-komponenten kan författare skapa dynamiska rutor från CQ-innehållskomponenter. (Se [Målanpassning](/help/sites-authoring/content-targeting-touch.md)av innehåll.) Målkomponenten finns på /libs/cq/personalization/components/target.

Skriptet target.jsp får åtkomst till sidegenskaperna för att avgöra vilken målmotor som ska användas för komponenten och kör sedan rätt skript:

* Adobe Target: /libs/cq/personalization/components/target/engine_tnt.jsp
* [Adobe Target med AT.JS](/help/sites-administering/target.md): /libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md): /libs/cq/personalization/components/target/engine_cq_campaign.jsp
* Regler/ContextHub på klientsidan: /libs/cq/personalization/components/target/engine_cq.jsp

### Skapa Mboxes {#the-creation-of-mboxes}

>[!NOTE]
>
>Som standard är rutor dolda - klassen mboxDefault bestämmer detta beteende. Genom att dölja kryssrutor kan besökarna inte se standardinnehållet innan det byts ut. Men om du döljer lådor påverkas upplevda prestanda.

När Adobe Target driver innehållet mot målgruppsanpassning skapar skriptet engine_tnt.jsp mbox som innehåller innehållet i målupplevelsen:

* Lägger till ett `div` element med klassen för `mboxDefault`, vilket krävs av API:t för Adobe Target.

* Lägger till innehållet i mbox (innehållet i målupplevelsen) inuti `div` elementet.

Efter `mboxDefault` div-elementet infogas det javascript som skapar mbox:

* Rutans namn, ID och plats baseras på komponentens databassökväg.
* Skriptet hämtar parameternamn och värden för klientkontextparametrar.
* Anrop görs till de funktioner som mbox.js och andra klientbibliotek definierar för att skapa mbox-filer.

#### Klientbibliotek för målanpassning av innehåll {#client-libraries-for-content-targeting}

Följande är tillgängliga clientlib-kategorier:

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
