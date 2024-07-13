---
title: Utveckla (allmän)
description: Integreringsramverket innehåller ett integreringslager med ett API som gör att du kan skapa AEM komponenter för e-handelsfunktioner.
contentOwner: Guillaume Carlino
exl-id: 1138a548-d112-4446-b0e1-b7a9ea7c7604
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 0%

---

# Utveckla (allmän){#developing-generic}

>[!NOTE]
>
>[API-dokumentation](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) är också tillgänglig.

Integreringsramverket innehåller ett integreringslager med ett API. Detta gör att du kan bygga AEM komponenter för e-handelsfunktioner (oberoende av din specifika e-handelsmotor). Man kan också använda CRX interna databas eller koppla in ett e-handelssystem och hämta in produktdata i AEM.

Det finns flera färdiga AEM för att använda integreringslagret. För närvarande är följande:

* En produktvisningskomponent
* En kundvagn
* Kampanjer och kuponger
* Katalog- och avsnittsritningar
* Checka ut
* Sök

Vid sökning finns en integreringsfunktion som gör att du kan använda sökningen i Adobe Experience Manager (AEM), en sökning från tredje part eller en kombination av dessa.

## Val av e-handelsmotor {#ecommerce-engine-selection}

eCommerce-ramverket kan användas tillsammans med alla e-handelslösningar, och den motor som används måste identifieras av AEM - även när den AEM generiska motorn används:

* eCommerce Engines är OSGi-tjänster som stöder gränssnittet `CommerceService`

   * Motorer kan särskiljas av en `commerceProvider`-tjänsteegenskap

* AEM stöder `Resource.adaptTo()` för `CommerceService` och `Product`

   * Implementeringen av `adaptTo` söker efter en `cq:commerceProvider`-egenskap i resursens hierarki:

      * Om det hittas används värdet för att filtrera e-handelstjänstens sökning.
      * Om den inte hittas används den mest rankade e-handelstjänsten.

   * En `cq:Commerce`-blandning används så att `cq:commerceProvider` kan läggas till i starkt typbestämda resurser.

* Egenskapen `cq:commerceProvider` används också för att referera till lämplig definition för handelsfabrik.

   * En `cq:commerceProvider`-egenskap med Geometrixx value korrelerar till exempel till OSGi-konfigurationen för **Day CQ Commerce Factory för Geometrixx-Outdoor** (`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`), där parametern `commerceProvider` också har värdet `geometrixx`.
   * Här kan ytterligare egenskaper konfigureras (när det är lämpligt och tillgängligt).

I en AEM krävs en specifik implementering, till exempel:

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | geometrixx-exempel; detta inkluderar minimala tillägg till det generiska API:t |

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
>Med CRXDE Lite kan du se hur detta hanteras i produktkomponenten för den AEM allmänna implementeringen:
>
>`/apps/geometrixx-outdoors/components/product`

### Sessionshantering {#session-handling}

En session där information om kundens kundvagn lagras.

**CommerceSession**:

* Äger **kundvagnen**

   * utför Lägg till/ta bort/etc
   * utför de olika beräkningarna av vagnen,

     `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* Äger beständighet för **order**-data:

  `CommerceSession.getUserContext()`

* Kan hämta/uppdatera leveransinformation med `updateOrder(Map<String, Object> delta)`
* Äger bearbetningsanslutningen för **betalningen**
* Äger anslutningen **fulfillment**

### Arkitektur {#architecture}

#### Arkitektur för produkt och varianter {#architecture-of-product-and-variants}

En enskild produkt kan ha flera variationer, t.ex. beroende på färg och/eller storlek. En produkt måste definiera vilka egenskaper som driver variationen. Adobe definierar dessa *variantaxlar*.

Alla egenskaper är dock inte olika axlar. Variationer kan också påverka andra egenskaper. Priset kan till exempel vara beroende av storleken. Dessa egenskaper kan inte väljas av kunden och betraktas därför inte som olika axlar.

Varje produkt och/eller variant representeras av en resurs och mappar därför 1:1 till en databasnod. Det är en extra konsekvens att en specifik produkt och/eller variant kan identifieras unikt genom sin sökväg.

Alla produktresurser kan representeras av en `Product API`. De flesta anrop i produkt-API:t är variantspecifika (även om varianter kan ärva delade värden från ett överordnat element), men det finns också anrop som listar variantuppsättningen ( `getVariantAxes()`, `getVariants()` och så vidare).

>[!NOTE]
>
>En variantaxel bestäms av det `Product.getVariantAxes()` returnerar:
>
>* för den generiska implementeringen, läser AEM den från en egenskap i produktdata ( `cq:productVariantAxes`)
>
>Produkter (i allmänhet) kan ha många olika axlar, men produktkomponenten som finns i paketet hanterar bara två:
>
>1. `size`
>1. plus en till
>
>   Den här ytterligare varianten väljs via egenskapen `variationAxis` i produktreferensen (vanligtvis `color` för Geometrixx Outdoors).

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

Slutligen finns det inget krav på att använda produktdata. Du kan placera alla produktdata under referenserna i katalogen, men du kan inte ha flera kataloger utan att duplicera alla produktdata.

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

#### com.adobe.cq.commerce.api.VariantFilter  {#com-adobe-cq-commerce-api-variantfilter}

```java
/**
 * Interface for filtering variants and AxisFilter provided as common implementation
 *
 * The <code>VariantFilter</code> is used to filter variants,
 * for example, when using {@link Product#getVariants(VariantFilter filter)}.
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

         * Produktreferenser innehåller en `productData`-egenskap som pekar på produktdata (vanligtvis under `/etc/commerce/products`).
         * Produktinformationen är hierarkisk. Produktattribut ärvs från en produktdatanodens överordnade.
         * Produktreferenser kan också innehålla lokala egenskaper som åsidosätter de som anges i deras produktdata.

      * En produkt i sig:

         * Utan egenskapen `productData`.
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

   * `CommerceSession` utför tillägg, borttagning och så vidare.
   * `CommerceSession` utför även de olika beräkningarna på kundvagnen.
   * `CommerceSession` tillämpar även verifikationer och kampanjer som har utlösts till kundvagnen.

* Även om den inte är direkt kundvagnsrelaterad måste `CommerceSession` även tillhandahålla katalogprisinformation (eftersom den äger priser)

   * Priset kan innehålla flera modifieringar:

      * Kvantitetsrabatter.
      * Olika valutor.
      * momspliktig och momsfri.

   * Modifierarna är öppna med följande gränssnitt:

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`

**Lagring**

* Lagring

   * I det AEM allmänna fallet lagras kundvagnarna i [ClientContexten](/help/sites-administering/client-context.md)

**Personalization**

* Kör alltid personalisering via [ClientContexten](/help/sites-administering/client-context.md).
* En ClientContext `/version/` av kundvagnen skapas i samtliga fall:

   * Produkter ska läggas till med metoden `CommerceSession.addCartEntry()`.

* Följande illustrerar ett exempel på kundvagnsinformation i kundvagnen:

![chlimage_1-33](/help/sites-developing/assets/chlimage_1-33a.png)

#### Arkitektur för utcheckning {#architecture-of-checkout}

**Kundvagn- och beställningsdata**

`CommerceSession` äger de tre elementen:

1. **Kundinnehåll**

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

   Orderinformationen är *inte* fast av API:t:

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**Leveransberäkningar**

* Beställningsblanketterna måste ofta innehålla flera leveransalternativ (och priser).
* Priserna kan baseras på artiklar och detaljer i beställningen, t.ex. vikt och/eller leveransadress.
* `CommerceSession` har åtkomst till alla beroenden, så den kan behandlas på liknande sätt som produktpriser:

   * `CommerceSession` äger fraktpriser.
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

E-handelsprojektet innehåller en standardsökkomponent i:

`/libs/commerce/components/search`

![chlimage_1-34](/help/sites-developing/assets/chlimage_1-34a.png)

Det här använder söknings-API:t för att fråga den valda e-handelsmotorn (se [Val av eCommerce Engine](#ecommerce-engine-selection)):

#### Söknings-API {#search-api}

Det finns flera allmänna/hjälpklasser i huvudprojektet:

1. `CommerceQuery`

   Används för att beskriva en sökfråga (innehåller information om frågetext, aktuell sida, sidstorlek, sortering och valda aspekter). Alla e-handelstjänster som implementerar söknings-API:t får instanser av den här klassen för att utföra sökningen. En `CommerceQuery` kan instansieras från ett begäranobjekt ( `HttpServletRequest`).

1. `FacetParamHelper`

   Är en verktygsklass som innehåller en statisk metod - `toParams` - som används för att generera `GET` parametersträngar från en lista med facets och ett växlat värde. Detta är användbart på användargränssnittets sida, där du behöver visa en hyperlänk för varje värde för varje aspekt, så att respektive värde växlas när användaren klickar på hyperlänken. Det vill säga, om den är markerad tas den bort från frågan, i annat fall läggs den till. Detta tar hand om all logik som används för att hantera flera-/enkelvärdesfaktorer, åsidosätta värden och så vidare.

Startpunkten för söknings-API är metoden `CommerceService#search` som returnerar ett `CommerceResult`-objekt. Mer information om det här avsnittet finns i API-dokumentationen.

### Utveckla kampanjer och Vouchers {#developing-promotions-and-vouchers}

* Vouchers:

   * En Voucher är en sidbaserad komponent som skapas/redigeras med webbplatskonsolen och lagras under:

     `/content/campaigns`

   * Kuponger:

      * En kupongkod (som anges i kundvagnen av kunden).
      * En verifikationsetikett (visas när kunden har skrivit in den i kundvagnen).
      * En kampanjsökväg (som definierar den åtgärd som vouchern tillämpar).

   * Vouchers har inte sina egna datum- och datumtider, utan använder dem från sina överordnade kampanjer.
   * Externa handelsmotorer kan också tillhandahålla vouchers, som kräver minst

      * En verifikationskod
      * En `isValid()`-metod

   * Komponenten **Voucher** ( `/libs/commerce/components/voucher`) innehåller:

      * En renderare för verifikationsadministration. Detta visar eventuella verifikationer som finns i kundvagnen.
      * Redigeringsdialogrutorna (formuläret) för att administrera (lägga till/ta bort) vouchers.
      * De åtgärder som krävs för att lägga till/ta bort verifikationer i/från kundvagnen.

* Kampanjer:

   * En kampanj är en sidbaserad komponent som skapas/redigeras med webbplatskonsolen och lagras under:

     `/content/campaigns`

   * Erbjudanden:

      * En prioritet
      * En sökväg till en erbjudandehanterare

   * Du kan koppla kampanjer till en kampanj för att definiera datum/tid för på/av-kampanjer.
   * Du kan koppla kampanjer till en upplevelse för att definiera deras segment.
   * Kampanjer som inte är kopplade till en upplevelse utlöses inte separat, men de kan fortfarande utlösas av en Voucher.
   * Kampanjkomponenten ( `/libs/commerce/components/promotion`) innehåller:

      * renderare och dialogrutor för kampanjadministration
      * underkomponenter för återgivning och redigering av konfigurationsparametrar som är specifika för kampanjhanterarna

   * Två marknadsföringshanterare medföljer:

      * `DiscountPromotionHandler`, som tillämpar en absolut eller procentuell rabatt som gäller för hela kundvagnen
      * `PerfectPartnerPromotionHandler`, som tillämpar en absolut eller procentuell rabatt på produkten om partnerprodukten också finns i kundvagnen

   * ClientContexten `SegmentMgr` löser segment och ClientContexten `CartMgr` löser kampanjer. Varje kampanj som är föremål för minst ett löst segment utlöses.

      * Utlösta kampanjer skickas tillbaka till servern via ett AJAX anrop för att beräkna kundvagnen på nytt.
      * Utlösta kampanjer (och tillagda Vouchers) visas också på panelen ClientContext.

Du kan lägga till/ta bort en verifikation från en kundvagn med API:t `CommerceSession`:

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

På så sätt ansvarar `CommerceSession` för att kontrollera om det finns en verifikation och om den kan användas eller inte. Detta kan vara för verifikationer som bara kan tillämpas om ett visst villkor är uppfyllt. Om till exempel det totala kundvagnspriset är större än $100. Om en voucher inte kan användas av någon anledning genereras ett undantag av metoden `addVoucher`. Dessutom ansvarar `CommerceSession` för att uppdatera kundvagnens priser efter att en verifikation har lagts till eller tagits bort.

`Voucher` är en böldliknande klass som innehåller fält för:

* Verifikationskod
* En kort beskrivning
* Referera till den relaterade kampanjen som anger rabattypen och värdet

Angiven `AbstractJcrCommerceSession` kan använda verifikationer. Verifikationerna som returneras av klassen `getVouchers()` är instanser av `cq:Page` som innehåller en jcr:content-nod med följande egenskaper (bland annat):

* `sling:resourceType` (String) - det här måste vara `commerce/components/voucher`

* `jcr:title` (sträng) - för voucherns beskrivning
* `code` (sträng) - den kod som användaren måste ange för att kunna använda vouchern
* `promotion` (String) - den befordran som ska användas, till exempel `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

Kampanjhanterare är OSGi-tjänster som ändrar kundvagnen. Kundvagnen stöder flera krokar som definieras i gränssnittet `PromotionHandler`.

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

* `DiscountPromotionHandler` tillämpar en absolut eller procentuell rabatt som gäller för hela varukorgen
* `PerfectPartnerPromotionHandler` tillämpar en absolut eller procentuell rabatt på produkten om produktpartnern också finns i kundvagnen
* `FreeShippingPromotionHandler` bjuder på fri frakt
