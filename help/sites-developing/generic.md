---
title: Utveckla (allmän)
seo-title: Utveckla (allmän)
description: Integreringsramverket innehåller ett integreringslager med ett API som gör att du kan skapa AEM-komponenter för e-handelsfunktioner
seo-description: Integreringsramverket innehåller ett integreringslager med ett API som gör att du kan skapa AEM-komponenter för e-handelsfunktioner
uuid: 393bb28a-9744-44f4-9796-09228fcd466f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: d8ee3b57-633a-425e-bf36-646f0e0bad52
translation-type: tm+mt
source-git-commit: 06f1f753b9bb7f7336454f166e03f753e3735a16

---


# Utveckla (allmän){#developing-generic}

>[!NOTE]
>
>[API-dokumentation](/help/sites-developing/ecommerce.md#api-documentation) finns också tillgänglig.

Integreringsramverket innehåller ett integreringslager med ett API. På så sätt kan du skapa AEM-komponenter för e-handelsfunktioner (oberoende av din specifika e-handelsmotor). Man kan också använda den interna CRX-databasen eller koppla in ett e-handelssystem och hämta produktdata till AEM.

Ett antal färdiga AEM-komponenter finns för att använda integreringslagret. För närvarande är följande:

* En produktvisningskomponent
* En kundvagn
* Kampanjer och kuponger
* Katalog- och avsnittsritningar
* Checka ut
* Sök

För sökning finns en integreringsfunktion som gör att du kan använda AEM-sökningen, en tredjepartssökning (som Search&amp;Promote) eller en kombination av dessa.

## Val av e-handelsmotor {#ecommerce-engine-selection}

eCommerce-ramverket kan användas tillsammans med alla e-handelslösningar, och den motor som används måste identifieras av AEM - även när den allmänna AEM-motorn används:

* eCommerce Engines är OSGi-tjänster som stöder `CommerceService` gränssnittet

   * Motorer kan särskiljas av en `commerceProvider` tjänsteegenskap

* AEM har stöd `Resource.adaptTo()` för `CommerceService` och `Product`

   * Implementeringen `adaptTo` söker efter en `cq:commerceProvider` egenskap i resursens hierarki:

      * Om det hittas används värdet för att filtrera e-handelstjänstens sökning.
      * Om den inte hittas används den mest rankade e-handelstjänsten.
   * En `cq:Commerce` mixin används så att `cq:commerceProvider` det kan läggas till i starkt typbestämda resurser.


* Egenskapen `cq:commerceProvider` används också för att referera till lämplig definition av handelsfabrik.

   * En `cq:commerceProvider` egenskap med värdet geometrixx korrelerar till exempel till OSGi-konfigurationen för **Day CQ Commerce Factory för Geometrixx-Outdoor** (`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`), där parametern `commerceProvider` också har värdet `geometrixx`.
   * Här kan ytterligare egenskaper konfigureras (när det är lämpligt och tillgängligt).

I en standard-AEM-installation krävs en specifik implementering, till exempel:

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | Geometrixx-exempel; detta inkluderar minimala tillägg till det generiska API:t |

### Exempel {#example}

```shell
/etc/commerce/products/geometrixx-outdoors
+ cq:commerceProvider = geometrixx
  + adobe-logo-shirt
    + cq:commerceType = product
    + price = 12.50
  + adobe-logo-shirt_S
    + cq:commerceType = variant
    + size = S
  + adobe-logo-shirt_XL
    + cq:commerceType = variant
    + size = XL
    + price = 14.50
```

>[!NOTE]
>
>Med CRXDE Lite kan du se hur detta hanteras i produktkomponenten för den allmänna implementeringen av AEM:
>
>`/apps/geometrixx-outdoors/components/product`

### Sessionshantering {#session-handling}

En session där information om kundens kundvagn lagras.

The **CommerceSession**:

* Äger **kundvagnen**

   * utför Lägg till/ta bort/etc
   * utför de olika beräkningarna av varukorgen,

      `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* Äger beständighet för **orderdata** :

   `CommerceSession.getUserContext()`

* Kan hämta/uppdatera leveransinformation med `updateOrder(Map<String, Object> delta)`
* Äger även **betalningshanteringsanslutningen**
* Äger även **leveransanslutningen**

### Arkitektur {#architecture}

#### Arkitektur för produkt och varianter {#architecture-of-product-and-variants}

En och samma produkt kan ha flera variationer. den kan till exempel variera beroende på färg och/eller storlek. En produkt måste definiera vilka egenskaper som driver variationen. vi kallar dessa *variantaxlar*.

Alla egenskaper är dock inte olika axlar. Variationer kan också påverka andra egenskaper. Priset kan till exempel vara beroende av storleken. Dessa egenskaper kan inte väljas av kunden och betraktas därför inte som olika axlar.

Varje produkt och/eller variant representeras av en resurs och mappar därför 1:1 till en databasnod. Det är en extra konsekvens att en specifik produkt och/eller variant kan identifieras unikt genom sin sökväg.

Alla produktresurser kan representeras av en `Product API`. De flesta anrop i produkt-API:t är variationsspecifika (även om variationer kan ärva delade värden från ett överordnat element), men det finns också anrop som listar variantuppsättningen ( `getVariantAxes()`, `getVariants()`osv.).

>[!NOTE]
>
>I själva verket bestäms en variantaxel av vad som än `Product.getVariantAxes()` returnerar:
>
>* för den allmänna implementeringen läser AEM den från en egenskap i produktdata ( `cq:productVariantAxes`)
>
>
Produkter (i allmänhet) kan ha många olika axlar, men produktkomponenten som finns i paketet hanterar bara två:
>
>1. `size`
   >
   >
1. plus ytterligare
   >   Den här ytterligare varianten väljs via egenskapen `variationAxis` för produktreferensen (vanligtvis `color` för Geometrixx Outdoor).
>



#### Produktreferenser och PIM-data {#product-references-and-pim-data}

I allmänhet:

* PIM-data finns under `/etc`

* Produktreferenser under `/content`.

Det måste finnas en 1:1-karta mellan produktvariationer och produktdatanoder.

Produktreferenser måste också ha en nod för varje variant som presenteras - men det finns inget krav på att presentera alla variationer. Om en produkt till exempel har variationer i S, M och L kan produktinformationen vara:

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

En stor och hög katalog kanske bara innehåller:

```shell
content
  big-and-tall
    shirt
      shirt-l
```

Slutligen finns det inget krav på att använda produktdata. Du kan placera alla produktdata under referenserna i katalogen; men du kan inte ha flera kataloger utan att duplicera alla produktdata.

**API**

#### com.adobe.cq.commerce.api.Product interface {#com-adobe-cq-commerce-api-product-interface}

```java
public interface Product extends Adaptable {

    public String getPath();            // path to specific variation
    public String getPagePath();        // path to presentation page for all variations
    public String getSKU();             // unique ID of specific variation

    public String getTitle();           // shortcut to getProperty(TITLE)
    public String getDescription();     // shortcut to getProperty(DESCRIPTION)
    public String getImageUrl();        // shortcut to getProperty(IMAGE_URL)
    public String getThumbnailUrl();    // shortcut to getProperty(THUMBNAIL_URL)

    public <T> T getProperty(String name, Class<T> type);

    public Iterator<String> getVariantAxes();
    public boolean axisIsVariant(String axis);
    public Iterator<Product> getVariants(VariantFilter filter) throws CommerceException;
}
```

#### com.adobe.cq.commerce.api.VariantFilter {#com-adobe-cq-commerce-api-variantfilter}

```java
/**
 * Interface for filtering variants and AxisFilter provided as common implementation
 *
 * The <code>VariantFilter</code> is used to filter variants,
 * e.g. when using {@link Product#getVariants(VariantFilter filter)}.
 */
public interface VariantFilter {
    public boolean includes(Product product);
}

/**
 * A {@link VariantFilter} for filtering variants by the given
 * axis and value. The following example returns a list of
 * variant products that have a value of <i>blue</i> on the
 * <i>color</i> axis.
 *
 * <p>
 * <code>product.getVariants(new AxisFilter("color", "blue"));</code>
 */
public class AxisFilter implements VariantFilter {

    private String axis;
    private String value;

    public AxisFilter(String axis, String value) {
        this.axis = axis;
        this.value = value;
    }

    /**
     * {@inheritDoc}
     */
    public boolean includes(Product product) {
        ValueMap values = product.adaptTo(ValueMap.class);

        if(values != null) {
            String v = values.get(axis, String.class);

            return v != null && v == value;
        }

        return false;
    }
}
```

* **Allmän lagringsmekanism**

   * Produktnoder är inte:ostrukturerade.
   * En produktnod kan vara antingen:

      * En referens med produktdata lagrade någon annanstans:

         * Produktreferenser innehåller en `productData` egenskap som pekar på produktdata (vanligtvis under `/etc/commerce/products`).
         * Produktinformationen är hierarkisk. produktattribut ärvs från en produktdatanodens överordnade.
         * Produktreferenser kan också innehålla lokala egenskaper som åsidosätter de som anges i deras produktdata.
      * En produkt i sig:

         * Utan en `productData` egenskap.
         * En produktnod som innehåller alla egenskaper lokalt (och inte innehåller någon productData-egenskap) ärver produktattribut direkt från sina egna överordnade.


* **AEM-generisk produktstruktur**

   * Varje variant måste ha en egen lövnod.
   * Produktgränssnittet representerar både produkter och varianter, men den relaterade databasnoden är specifik för vilken den är.
   * Produktnoden beskriver produktattribut och variantaxlar.

#### Exempel {#example-1}

```shell
+ banyan_shirt
    - cq:commerceType = product
    - cq:productAttributes = [jcr:title, jcr:description, size, price, color]
    - cq:productVariantAxes = [color, size]
    - jcr:title = Banyan Shirt
    - jcr:description = Flowery, all-cotton shirt.
    - price = 14.00
    + banyan_shirt_s
        - cq:commerceType = variant
        - size = S
        + banyan_shirt_s_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_s_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_m
        - cq:commerceType = variant
        - size = M
        + banyan_shirt_m_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_m_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_l
        - cq:commerceType = variant
        - size = L
        + banyan_shirt_l_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_l_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_xl
        - cq:commerceType = variant
        - size = XL
        - price = 18.00
```

#### Arkitektur för kundvagnen {#architecture-of-the-shopping-cart}

**Komponenter**

* Kundvagnen ägs av `CommerceSession:`

   * Utför `CommerceSession` att lägga till, ta bort osv.
   * De olika beräkningarna av vagnen utförs också `CommerceSession` .
   * Den gäller också `CommerceSession` kuponger och kampanjer som har sparats i kundvagnen.

* Även om den inte är direkt kundvagnsrelaterad måste `CommerceSession` den även tillhandahålla katalogprisinformation (eftersom den äger prissättningen)

   * Priset kan innehålla flera modifieringar:

      * Kvantitetsrabatter.
      * Olika valutor.
      * momspliktig och momsfri.
   * Modifierarna är helt öppna med följande gränssnitt:

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**Lagring**

* Lagring

   * I de allmänna AEM-kundvagnarna sparas kundvagnarna i [ClientContext](/help/sites-administering/client-context.md)

**Personalisering**

* Personalisering bör alltid drivas via [ClientContext](/help/sites-administering/client-context.md).
* En ClientContext `/version/` i kundvagnen skapas i samtliga fall:

   * Produkterna ska läggas till med hjälp av `CommerceSession.addCartEntry()` metoden.

* Följande illustrerar ett exempel på kundvagnsinformation i ClientContext cart:

![chlimage_1-33](assets/chlimage_1-33a.png)

#### Arkitektur för utcheckning {#architecture-of-checkout}

**Kundvagn- och orderdata**

De tre elementen `CommerceSession` äger:

1. **Kundvagnsinnehåll**

   Schemat för kundvagnens innehåll har korrigerats av API:

   ```java
       public void addCartEntry(Product product, int quantity);
       public void modifyCartEntry(int entryNumber, int quantity);
       public void deleteCartEntry(int entryNumber);
   ```

1. **Priser**

   Prisschemat är också fast av API:

   ```java
       public String getCartPreTaxPrice();
       public String getCartTax();
       public String getCartTotalPrice();
       public String getOrderShipping();
       public String getOrderTotalTax();
       public String getOrderTotalPrice();
   ```

1. **Beställningsinformation**

   Beställningsinformationen har dock *inte* åtgärdats av API:t:

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**Leveransberäkningar**

* Beställningsblanketter måste ofta innehålla flera olika leveransalternativ (och priser).
* Priserna kan baseras på artiklar och detaljer i beställningen, t.ex. vikt och/eller leveransadress.
* De `CommerceSession` har tillgång till alla beroenden, så de kan behandlas på liknande sätt som produktpriser:

   * Det `CommerceSession` egna fraktpriset.
   * Använd `updateOrder(Map<String, Object> delta)` för att hämta/uppdatera leveransinformation.

### Sökdefinition {#search-definition}

I enlighet med standardtjänstens API-modell innehåller e-handelsprojektet en uppsättning sökrelaterade API:er som kan implementeras av enskilda e-handelsmotorer.

>[!NOTE]
>
>För närvarande är det bara hybris-motorn som implementerar söknings-API:t.
>
>Söknings-API:t är dock allmänt och kan implementeras av varje enskild CommerceService.
>
>Även om den generiska implementeringen inte implementerar det här API:t kan du utöka det och lägga till sökfunktionen.

eCommerce-projektet innehåller en standardsökkomponent som finns i:

`/libs/commerce/components/search`

![chlimage_1-34](assets/chlimage_1-34a.png)

Detta använder söknings-API:t för att fråga den valda e-handelsmotorn (se [eCommerce Engine Selection](#ecommerce-engine-selection)):

#### Söknings-API {#search-api}

Det finns flera allmänna/hjälpklasser i huvudprojektet:

1. `CommerceQuery`

   
Används för att beskriva en sökfråga (innehåller information om frågetext, aktuell sida, sidstorlek, sortering och valda aspekter). Alla e-handelstjänster som implementerar söknings-API:t får instanser av den här klassen för att kunna utföra sökningen. En `CommerceQuery` instans kan skapas från ett begäranobjekt ( `HttpServletRequest`).

1. `FacetParamHelper`

   
Är en verktygsklass som innehåller en statisk metod - `toParams` - som används för att generera `GET` parametersträngar från en lista med facets och ett växlat värde. Detta är användbart på användargränssnittssidan, där du behöver visa en hyperlänk för varje värde i varje aspekt, så att respektive värde växlas när användaren klickar på hyperlänken (d.v.s. om den markerats tas det bort från frågan, annars läggs det till). Detta tar hand om all logik för hantering av flera-/enkelvärdesfaktorer, åsidosättningsvärden osv.

Startpunkten för söknings-API är den `CommerceService#search` metod som returnerar ett `CommerceResult` objekt. Mer information om det här avsnittet finns i API-dokumentationen.

### Utveckla kampanjer och Vouchers {#developing-promotions-and-vouchers}

* Vouchers:

   * En Voucher är en sidbaserad komponent som skapas/redigeras med webbplatskonsolen och lagras under:

      `/content/campaigns`

   * Kuponger:

      * En kupongkod (som anges i kundvagnen av kunden).
      * En verifikationsetikett (visas när kunden har skrivit in den i kundvagnen).
      * En kampanjsökväg (som definierar den åtgärd som vouchern tillämpar).
   * Vouchers har inte sina egna datum- och datumtider, utan använder dem från sina överordnade kampanjer.
   * Externa handelsmotorer kan också tillhandahålla vouchers, kräver minst

      * En verifikationskod
      * En `isValid()` metod
   * Komponenten **Voucher** ( `/libs/commerce/components/voucher`) ger:

      * En renderare för kupongadministration. visar eventuella verifikationer som finns i kundvagnen.
      * Redigeringsdialogrutorna (formuläret) för att administrera (lägga till/ta bort) verifikationerna.
      * De åtgärder som krävs för att lägga till/ta bort verifikationer i/från kundvagnen.



* Kampanjer:

   * En kampanj är en sidbaserad komponent som skapas/redigeras med webbplatskonsolen och lagras under:

      `/content/campaigns`

   * Erbjudanden:

      * En prioritet
      * En sökväg till en erbjudandehanterare
   * Du kan koppla kampanjer till en kampanj för att definiera datum/tid för på/av-kampanjer.
   * Du kan koppla kampanjer till en upplevelse för att definiera deras segment.
   * Kampanjer som inte är kopplade till en upplevelse kommer inte att utlösas fristående, men de kan fortfarande utlösas av en Voucher.
   * Kampanjkomponenten ( `/libs/commerce/components/promotion`) innehåller:

      * renderare och dialogrutor för kampanjadministration
      * underkomponenter för återgivning och redigering av konfigurationsparametrar som är specifika för kampanjhanterarna
   * Två marknadsföringshanterare medföljer:

      * `DiscountPromotionHandler`som ger en absolut rabatt eller en procentuell rabatt som gäller för hela varukorgen
      * `PerfectPartnerPromotionHandler`, som ger en produkt i absolut eller procentuell rabatt om partnerprodukten också finns i kundvagnen
   * ClientContext `SegmentMgr` löser segment och ClientContext `CartMgr` löser kampanjer. Varje kampanj som gäller minst ett löst segment kommer att utlösas.

      * Utlösta kampanjer skickas tillbaka till servern via ett AJAX-anrop för att beräkna kundvagnen på nytt.
      * Utlösta kampanjer (och tillagda Vouchers) visas också på panelen ClientContext.




Du kan lägga till/ta bort en voucher från en kundvagn via `CommerceSession` API:t:

```java
/**
 * Apply a voucher to this session's cart.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void addVoucher(String code) throws CommerceException;

/**
 * Remove a voucher that was previously added with {@link #addVoucher(String)}.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void removeVoucher(String code) throws CommerceException;

/**
 * Get a list of vouchers that were added to this cart via {@link #addVoucher(String)}.
 *
 * @throws CommerceException
 */
public List<Voucher> getVouchers() throws CommerceException;
```

På så sätt ansvarar användaren för `CommerceSession` att kontrollera om en voucher finns och om den kan användas eller inte. Detta kan vara för kuponger som bara kan tillämpas om ett visst villkor är uppfyllt. till exempel om det totala kundvagnspriset är större än $100). Om en verifikation inte kan användas av någon anledning genereras ett undantag av metoden `addVoucher` . Dessutom ansvarar `CommerceSession` användaren för att uppdatera kundvagnens priser efter att en verifikation har lagts till eller tagits bort.

Klassen `Voucher` är en böldliknande klass som innehåller fält för:

* Verifikationskod
* En kort beskrivning
* Referera till den relaterade kampanjen som anger rabattypen och värdet

Angiven `AbstractJcrCommerceSession` kan använda verifikationer. De vouchers som returneras av klassen `getVouchers()` är instanser av `cq:Page` som innehåller en jcr:content-nod med följande egenskaper (bland annat):

* `sling:resourceType` (String) - det här måste vara `commerce/components/voucher`

* `jcr:title` (String) - för voucherns beskrivning
* `code` (String) - den kod som användaren måste ange för att kunna använda vouchern
* `promotion` (String) - den befordran som ska genomföras.t.ex. `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

Kampanjhanterare är OSGi-tjänster som ändrar kundvagnen. Kundvagnen har stöd för flera krokar som definieras i `PromotionHandler` gränssnittet.

```java
/**
 * Apply promotion to a cart line item. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @param cartEntry The cart line item
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyCartEntryPromotion(CommerceSession commerceSession,
                                         Promotion promotion, CartEntry cartEntry)
    throws CommerceException;

/**
 * Apply promotion to an order. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyOrderPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

public PriceInfo applyShippingPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

/**
 * Allows a promotion handler to define a custom, author-oriented message for a promotion.
 * The {@link com.adobe.cq.commerce.common.promotion.PerfectPartnerPromotionHandler}, for instance,
 * uses this to list the qualifying pairs of products in the current cart.
 * @param commerceSession
 * @param promotion
 * @return A message to display
 * @throws CommerceException
 */
public String getMessage(SlingHttpServletRequest request, CommerceSession commerceSession, Promotion promotion) throws CommerceException;

/**
 * Informs the promotion handler that something under the promotions root has been edited, and the handler
 * should invalidate any caches it might be keeping.
 */
public void invalidateCaches();
```

Tre marknadsföringshanterare ingår:

* `DiscountPromotionHandler` använder en absolut rabatt eller en procentuell rabatt för hela varukorgen
* `PerfectPartnerPromotionHandler` tillämpar en absolut eller procentuell rabatt på produkten om produktpartnern också finns i kundvagnen
* `FreeShippingPromotionHandler` kostnadsfri frakt

