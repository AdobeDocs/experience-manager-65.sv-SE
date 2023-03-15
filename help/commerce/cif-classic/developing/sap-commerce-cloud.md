---
title: Utveckla med SAP Commerce Cloud
seo-title: Developing with SAP Commerce Cloud
description: Integreringsramverket för SAP Commerce Cloud innehåller ett integreringslager med ett API
seo-description: The SAP Commerce Cloud integration framework includes an integration layer with an API
uuid: a780dd17-027a-4a61-af8f-3e2f600524c7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: b3de1a4a-f334-44bd-addc-463433204c99
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '2308'
ht-degree: 0%

---

# Utveckla med SAP Commerce Cloud {#developing-with-sap-commerce-cloud}

>[!NOTE]
>
>e-handelsramverket kan användas med alla e-handelslösningar. Vissa detaljer och exempel som behandlas här kommer att avse [hybris](https://www.hybris.com/) lösning.

Integreringsramverket innehåller ett integreringslager med ett API. På så sätt kan du:

* koppla in ett e-handelssystem och hämta in produktdata i AEM

* bygga AEM för handelsfunktioner oberoende av e-handelsmotorn

![chlimage_1-11](/help/sites-developing/assets/chlimage_1-11a.png)

>[!NOTE]
>
>[API-dokumentation](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) finns också.

Det finns ett antal färdiga AEM för att använda integreringslagret. För närvarande är följande:

* en produktvisningskomponent
* en kundvagn
* utcheckning

För sökning tillhandahålls en integreringsfunktion som gör att du kan använda AEM, sökning i e-handelssystemet, en sökning från tredje part eller en kombination av dessa.

## Val av e-handelsmotor {#ecommerce-engine-selection}

eCommerce-ramverket kan användas tillsammans med alla e-handelslösningar, och den motor som används måste kunna identifieras av AEM:

* eCommerce Engines är OSGi-tjänster som stöder `CommerceService` gränssnitt

   * Motorer kan särskiljas av en `commerceProvider` service, egenskap

* AEM `Resource.adaptTo()` for `CommerceService` och `Product`

   * The `adaptTo` implementering söker efter en `cq:commerceProvider` i resursens hierarki:

      * Om det hittas används värdet för att filtrera e-handelstjänstens sökning.

      * Om den inte hittas används den mest rankade e-handelstjänsten.
   * A `cq:Commerce` mixin används så att `cq:commerceProvider` kan läggas till i starkt typbestämda resurser.


* The `cq:commerceProvider` -egenskapen används också för att referera till lämplig definition för handelsfabrik.

   * Till exempel en `cq:commerceProvider` egenskap med värdet `hybris` kommer att korrelera OSGi-konfigurationen för **Day CQ Commerce Factory for Hybris** (com.adobe.cq.commerce.hybris.impl.HybrisServiceFactory) - där parametern `commerceProvider` har även värdet `hybris`.

   * Här finns ytterligare egenskaper, som **Katalogversion** kan konfigureras (när det är lämpligt och tillgängligt).

Se följande exempel nedan:

| `cq:commerceProvider = geometrixx` | Vid en AEM standardinstallation krävs en specifik implementering. till exempel exemplet geometrixx, som innehåller minimala tillägg till det generiska API:t |
|--- |--- |
| `cq:commerceProvider = hybris` | hybriimplementering |

### Exempel {#example}

```shell
/content/store
+ cq:commerceProvider = hybris
  + mens
    + polo-shirt-1
    + polo-shirt-2
    + employee
+ cq:commerceProvider = jcr
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
>Med CRXDE Lite kan du se hur detta hanteras i produktkomponenten för hybris-implementeringen:
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### Utveckling för hybris 4 {#developing-for-hybris}

Utbyggnaden av hybris i eCommerce Integration Framework har uppdaterats för att stödja Hybris 5, samtidigt som bakåtkompatibiliteten med Hybris 4 bibehålls.

Standardinställningarna i koden ställs in för Hybris 5.

För att utveckla för Hybris 4 krävs följande:

* När du anropar maven lägger du till följande kommandoradsargument till kommandot

   `-P hybris4`

   Den laddar ned den förkonfigurerade hybris 4-distributionen och bäddar in den i paketet `cq-commerce-hybris-server`.

* I OSGi-konfigurationshanteraren:

   * Inaktivera stöd för Hybris 5 för tjänsten Default Response Parser.

   * Se till att tjänsten Hybris Basic Authentication Handler har en lägre prioritetsordning än tjänsten Hybris OAuth Handler.

### Sessionshantering {#session-handling}

hybris använder en användarsession för att lagra information som kundens kundvagn. sessions-ID returneras från hybris i en `JSESSIONID` cookie som ska skickas på efterföljande förfrågningar till hybris. För att undvika att lagra sessions-ID i databasen kodas det i en annan cookie som lagras i kundens webbläsare. Följande steg utförs:

* På den första begäran anges ingen cookie på köparens begäran. så att en begäran skickas till hybris-instansen för att skapa en session.

* Sessionscookies extraheras från svaret, kodas i en ny cookie (till exempel `hybris-session-rest`) och anpassa sig till kundresponsen. Kodningen i en ny cookie krävs eftersom den ursprungliga cookien bara är giltig för en viss sökväg och annars inte skulle skickas tillbaka från webbläsaren i efterföljande begäranden. Sökvägsinformationen måste också läggas till i cookie-filens värde.

* På efterföljande begäranden avkodas cookies från `hybris-session-<*xxx*>` cookies och anges på HTTP-klienten som används för att begära data från hybris.

>[!NOTE]
>
>En ny anonym session skapas när den ursprungliga sessionen inte längre är giltig.

#### CommerceSession {#commercesession}

* Den här sessionen&quot;äger&quot; **kundvagn**

   * utför Lägg till/ta bort/etc

   * utför de olika beräkningarna av varukorgen,

      `commerceSession.getProductPrice(Product product)`

* Äger *lagringsplats* för **order** data

   `CommerceSession.getUserContext()`

* Äger även **betalning** bearbetningsanslutning

* Äger även **uppfyllelse** anslutning

### Produktsynkronisering och -publicering {#product-synchronization-and-publishing}

Produktdata som bevaras i hybris måste finnas tillgängliga i AEM. Följande mekanism har implementerats:

* En initial belastning av ID:n tillhandahålls av hybris som foder. Denna feed kan uppdateras.
* hybris kommer att tillhandahålla uppdateringsinformation via ett foder (som AEM undersökningar).
* När AEM använder produktdata skickar den begäranden tillbaka till hybris om aktuella data (villkorlig begäran om hämtning med det senaste ändringsdatumet).
* På hybris är det möjligt att ange foderinnehållet på ett deklarativt sätt.
* Matningsstrukturen mappas till AEM innehållsmodell i matningsadaptern på AEM.

![chlimage_1-12](/help/sites-developing/assets/chlimage_1-12a.png)

* Importören (b) används för den första konfigurationen av sidträdstrukturen i AEM för kataloger.
* Katalogförändringar i hybris anges som AEM via en feed och sedan sprida dessa till AEM b.

   * Produkt som lagts till/tagits bort/ändrats i förhållande till katalogversionen.

   * Produkten är godkänd.

* Tillägget hybris erbjuder en pollingimportör (&quot;hybris&quot;-schema&quot;) som kan konfigureras för att importera ändringar till AEM med ett angivet intervall (t.ex. var 24:e timme där intervallet anges i sekunder):

   ```JavaScript
       http://localhost:4502/content/geometrixx-outdoors/en_US/jcr:content.json
        {
        * "jcr:mixinTypes": ["cq:PollConfig"],
        * "enabled": true,
        * "source": "hybris:outdoors",
        * "jcr:primaryType": "cq:PageContent",
        * "interval": 86400
        }
   ```

* Katalogkonfigurationen i AEM känner igen **Mellanlagrad** och **Online** katalogversioner.

* För att kunna synkronisera produkter mellan katalogversioner krävs en (avaktivering) av motsvarande AEM (a, c)

   * Lägga till en produkt i en **Online** katalogversionen kräver aktivering av produktens sida.

   * Borttagning av en produkt kräver inaktivering.

* Aktivering av en sida i AEM c kräver en kontroll b och är endast möjlig om

   * Produkten finns i **Online** katalogversion för produktsidor.

   * De refererade produkterna är tillgängliga i en **Online** katalogversion för andra sidor (t.ex. kampanjsidor).

* Aktiverade produktsidor behöver åtkomst till produktdata **Online** version (d).

* Den AEM publiceringsinstansen kräver tillgång till hybris för hämtning av produktdata och personaliserade data (d).

### Arkitektur {#architecture}

#### Arkitektur för produkt och varianter {#architecture-of-product-and-variants}

En och samma produkt kan ha flera variationer. den kan till exempel variera beroende på färg och/eller storlek. En produkt måste definiera vilka egenskaper som driver variationen. vi kallar dem *variantaxlar*.

Alla egenskaper är dock inte olika axlar. Variationer kan också påverka andra egenskaper. Priset kan till exempel vara beroende av storleken. Dessa egenskaper kan inte väljas av kunden och betraktas därför inte som olika axlar.

Varje produkt och/eller variant representeras av en resurs och mappar därför 1:1 till en databasnod. Det är en extra konsekvens att en specifik produkt och/eller variant kan identifieras unikt genom sin sökväg.

Produkt-/variantresursen innehåller inte alltid den faktiska produktinformationen. Det kan vara en representation av data som faktiskt finns i ett annat system (t.ex. hybris). Produktbeskrivningar, priser osv. lagras inte i AEM utan hämtas i realtid från eCommerce-motorn.

Alla produktresurser kan representeras av en `Product API`. De flesta anrop i produkt-API:t är variationsspecifika (även om variationer kan ärva delade värden från ett överordnat objekt), men det finns också anrop som listar variantuppsättningen ( `getVariantAxes()`, `getVariants()`, osv.).

>[!NOTE]
>
>I själva verket bestäms en variantaxel av vad som helst `Product.getVariantAxes()` returnerar:
>* hybris definierar den för hybris-implementeringen
>
>Produkter (i allmänhet) kan ha många olika axlar, men produktkomponenten som finns i paketet hanterar bara två:
>
>1. `size`
>
>1. plus ytterligare

>
>Den här extra varianten markeras via `variationAxis` egenskap för produktreferensen (vanligtvis `color` för Geometrixx Outdoors).

#### Produktreferenser och produktdata {#product-references-and-product-data}

I allmänhet:

* produktdata finns under `/etc`

* och produktreferenser under `/content`.

Det måste finnas en 1:1-karta mellan produktvariationer och produktdatanoder.

Produktreferenser måste också ha en nod för varje variant som presenteras - men det finns inget krav på att presentera alla variationer. Om en produkt till exempel har variationer i S, M och L kan produktinformationen vara:

```shell
etc
|──commerce
|  |──products
|     |──shirt
|       |──shirt-s
|       |──shirt-m
|       |──shirt-l
```

En stor och hög katalog kanske bara innehåller:

```shell
content
|──big-and-tall
|  |──shirt
|     |──shirt-l
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

#### com.adobe.cq.commerce.api.VariantFilter  {#com-adobe-cq-commerce-api-variantfilter}

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

   * Produktnoderna är `nt:unstructured`.

   * En produktnod kan vara antingen:

      * En referens med produktdata lagrade någon annanstans:

         * Produktreferenser innehåller en `productData` -egenskap, som pekar på produktdata (vanligtvis under `/etc/commerce/products`).

         * Produktinformationen är hierarkisk. produktattribut ärvs från en produktdatanodens överordnade.

         * Produktreferenser kan också innehålla lokala egenskaper som åsidosätter de som anges i deras produktdata.
      * En produkt i sig:

         * Utan `productData` -egenskap.

         * En produktnod som innehåller alla egenskaper lokalt (och inte innehåller någon productData-egenskap) ärver produktattribut direkt från sina egna överordnade.


* **AEM produktstruktur**

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

   * The `CommerceSession` utför Lägg till/ta bort/etc.
   * The `CommerceSession` utför även de olika beräkningarna på kundvagnen. &quot;

* Även om de inte är direkt kundvagnsrelaterade är `CommerceSession` måste även tillhandahålla information om katalogpriser (eftersom den äger priser)

   * Priset kan innehålla flera modifieringar:

      * Kvantitetsrabatter.
      * Olika valutor.
      * momspliktig och momsfri.
   * Modifierarna är helt öppna med följande gränssnitt:

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**Lagring**

* Lagring

   * I hybris-fallet äger hybris-servern kundvagnen.
   * I det AEM generiska fallet lagras varukorgar i [ClientContext](/help/sites-administering/client-context.md).

**Personanpassning**

* Personalisering bör alltid styras av [ClientContext](/help/sites-administering/client-context.md).
* A ClientContext `/version/` av kundvagnen skapas i samtliga fall:

   * Produkterna ska läggas till med `CommerceSession.addCartEntry()` -metod.

* Följande illustrerar ett exempel på kundvagnsinformation i kundvagnen i ClientContext:

![chlimage_1-13](/help/sites-developing/assets/chlimage_1-13a.png)

#### Arkitektur för utcheckning {#architecture-of-checkout}

**Kundvagn- och orderdata**

The `CommerceSession` äger de tre elementen:

1. Kundvagnsinnehåll
1. Priser
1. Orderinformation

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

   Beställningsinformationen är dock *not* åtgärdat av API:

   ```java
   public void updateOrderDetails(Map<String, String> orderDetails);
   public Map<String, String> getOrderDetails();
   public void submitOrder();
   ```

**Leveransberäkningar**

* Beställningsblanketter måste ofta innehålla flera olika leveransalternativ (och priser).
* Priserna kan baseras på artiklar och detaljer i beställningen, t.ex. vikt och/eller leveransadress.
* The `CommerceSession` har tillgång till alla beroenden, så det kan behandlas på liknande sätt som produktpriser:

   * The `CommerceSession` äger fraktpriser.
   * Kan hämta/uppdatera leveransinformation med `updateOrder(Map<String, Object> delta)`

>[!NOTE]
>
>Du kan implementera en leveransväljare; till exempel:
>
>`yourProject/commerce/components/shippingpicker`:
>
>* Det här kan vara en kopia av `foundation/components/form/radio`, men med återanrop till `CommerceSession` for:
>
>* Kontrollera om metoden är tillgänglig
>* Lägga till prisinformation
>* Att göra det möjligt för kunderna att uppdatera beställningssidan i AEM (inklusive överflödet av leveransmetoder och texten som beskriver dem), samtidigt som de fortfarande har möjlighet att visa de relevanta `CommerceSession` information.


**Betalningshantering**

* The `CommerceSession` äger också anslutningen för betalningshantering.

* Implementerare måste lägga till specifika samtal (till den valda betalningstjänsten) i `CommerceSession` implementering.

**Orderuppfyllelse**

* The `CommerceSession` äger också leveransanslutningen.
* Implementerare måste lägga till specifika samtal (till den valda betalningstjänsten) i `CommerceSession` implementering.

### Sökdefinition {#search-definition}

I enlighet med standardtjänstens API-modell innehåller e-handelsprojektet en uppsättning sökrelaterade API:er som kan implementeras av enskilda e-handelsmotorer.

>[!NOTE]
>
>För närvarande är det bara hybris-motorn som implementerar söknings-API:t.
>
>Söknings-API:t är dock allmänt och kan implementeras av varje enskild CommerceService.

eCommerce-projektet innehåller en standardsökkomponent som finns i:

`/libs/commerce/components/search`

![chlimage_1-14](/help/sites-developing/assets/chlimage_1-14a.png)

Detta använder sökgränssnittet för att fråga den valda e-handelsmotorn (se [Val av e-handelsmotor](#ecommerce-engine-selection)):

#### Söknings-API {#search-api}

Det finns flera allmänna/hjälpklasser i huvudprojektet:

1. `CommerceQuery`

   Används för att beskriva en sökfråga (innehåller information om frågetext, aktuell sida, sidstorlek, sortering och valda aspekter). Alla e-handelstjänster som implementerar söknings-API:t får instanser av den här klassen för att kunna utföra sökningen. A `CommerceQuery` kan instansieras från ett begäranobjekt ( `HttpServletRequest`).

1. `FacetParamHelper`

   Är en verktygsklass som innehåller en statisk metod - `toParams` - som används för att generera `GET` parametersträngar från en lista med facets och ett sammankopplat värde. Detta är användbart på användargränssnittssidan, där du behöver visa en hyperlänk för varje värde i varje aspekt, så att respektive värde växlas när användaren klickar på hyperlänken (d.v.s. om den markerats tas det bort från frågan, annars läggs det till). Detta tar hand om all logik för hantering av flera-/enkelvärdesfaktorer, åsidosättningsvärden osv.

Startpunkten för sökgränssnittet är `CommerceService#search` metod som returnerar en `CommerceResult` -objekt. Se [API-dokumentation](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) om du vill ha mer information om det här avsnittet.

### Användarintegrering {#user-integration}

Integrering sker mellan AEM och olika e-handelssystem. Detta kräver en strategi för att synkronisera kunder mellan de olika systemen så att AEM specifik kod bara behöver känna till AEM och vice versa:

* Autentisering

   AEM antas vara *endast* webbgränssnitt och därför *alla* autentisering.

* Konton i Hybris

   AEM skapar ett motsvarande (underordnat) konto i hybris för varje kund. Användarnamnet för det här kontot är samma som AEM användarnamn. Ett kryptografiskt slumpmässigt lösenord genereras automatiskt och lagras (krypteras) i AEM.

#### Befintliga användare {#pre-existing-users}

En AEM kan placeras framför en befintlig hybris-implementering. En hybris-motor kan också läggas till i en befintlig AEM. För att göra detta måste systemen kunna hantera befintliga användare på ett effektivt sätt i båda systemen:

* AEM -> hybris

   * När du loggar in på hybris, om den AEM användaren inte redan finns:

      * skapa en ny hybris-användare med ett kryptografiskt slumpmässigt lösenord
      * lagra hybris-användarnamnet i AEM användarkatalog
   * Se: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`


* hybris -> AEM

   * När du loggar in på AEM, om systemet känner igen användaren:

      * försök att logga in på hybris med angivet användarnamn/pwd
      * Om det lyckas skapar du den nya användaren i AEM med samma lösenord (AEM-specifikt salt-värde ger AEM-specifik hash-kod)
   * Ovanstående algoritm implementeras i en Sling `AuthenticationInfoPostProcessor`

      * Se: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`


### Anpassa importprocessen {#customizing-the-import-process}

Så här bygger du på befintliga funktioner i din anpassade importhanterare:

* måste implementera `ImportHandler` gränssnitt

* kan utöka `DefaultImportHandler`.

```java
/**
 * Services implementing the <code>ImportHandler</code> interface are
 * called by the {@link HybrisImporter} to create actual commerce entities
 * such as products.
 */
public interface ImportHandler {

  /**
  * Not used.
  */
  public void createTaxonomie(ImporterContext ctx);

  /**
  * Creates a catalog with the given name.
  * @param ctx   The importer context
  * @param name  The catalog's name
  * @return Path of created catalog
  */
  public String createCatalog(ImporterContext ctx, String name) throws Exception;

  /**
  * Creates a product from the given values.
  * @param ctx                The importer context
  * @param values             The product's properties
  * @param parentCategoryPath The containing category's path
  * @return Path of created product
  */
  public String createProduct(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;

  /**
  * Creates a variant product from the given values.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The base product's path
  * @return Path of created product
  */
  public String createVariantProduct(ImporterContext ctx, ValueMap values, String baseProductPath) throws Exception;

  /**
  * Creates an asset for a product. This is usually a product
  * image.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The product's path
  * @return Path of created asset
  */
  public String createAsset(ImporterContext ctx, ValueMap values, String productPath) throws Exception;

  /**
  * Creates a category from the given values.
  * @param ctx           The importer context
  * @param values        The category's properties
  * @param parentPath    Path of parent category or base path of import in case of root category
  * @return Path of created category
  */
  public String createCategory(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;
}
```

För att din anpassade hanterare ska identifieras av importören måste den ange `service.ranking`Egenskaper med ett värde högre än 0. till exempel.

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
