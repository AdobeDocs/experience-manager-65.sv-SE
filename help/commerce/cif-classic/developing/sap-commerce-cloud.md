---
title: Utveckla med SAP Commerce Cloud
description: Integreringsramverket för SAP Commerce Cloud innehåller ett integreringslager med ett API.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: b3de1a4a-f334-44bd-addc-463433204c99
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '2303'
ht-degree: 0%

---

# Utveckla med SAP Commerce Cloud {#developing-with-sap-commerce-cloud}

>[!NOTE]
>
>e-handelsramverket kan användas med alla e-handelslösningar. Vissa detaljer och exempel som behandlas här ser lösningen [hybris](https://www.sap.com/products/crm.html).

Integreringsramverket innehåller ett integreringslager med ett API. På så sätt kan du:

* koppla in ett e-handelssystem och hämta produktdata till Adobe Experience Manager (AEM)

* bygga AEM för handelsfunktioner oberoende av e-handelsmotorn

![chlimage_1-11](/help/sites-developing/assets/chlimage_1-11a.png)

>[!NOTE]
>
>[API-dokumentation](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) är också tillgänglig.

Det finns flera färdiga AEM för att använda integreringslagret. För närvarande är följande:

* en produktvisningskomponent
* en kundvagn
* utcheckning

För sökningar finns en integreringsfunktion som gör att du kan använda AEM, sökningen i e-handelssystemet, en sökning från tredje part eller en kombination av dessa.

## Val av e-handelsmotor {#ecommerce-engine-selection}

eCommerce-ramverket kan användas tillsammans med alla e-handelslösningar, och den motor som används måste kunna identifieras av AEM:

* eCommerce Engines är OSGi-tjänster som stöder gränssnittet `CommerceService`

   * Motorer kan särskiljas av en `commerceProvider`-tjänsteegenskap

* AEM stöder `Resource.adaptTo()` för `CommerceService` och `Product`

   * Implementeringen av `adaptTo` söker efter en `cq:commerceProvider`-egenskap i resursens hierarki:

      * Om det hittas används värdet för att filtrera e-handelstjänstens sökning.

      * Om den inte hittas används den mest rankade e-handelstjänsten.

   * En `cq:Commerce`-blandning används så att `cq:commerceProvider` kan läggas till i starkt typbestämda resurser.

* Egenskapen `cq:commerceProvider` används också för att referera till lämplig definition för handelsfabrik.

   * En `cq:commerceProvider`-egenskap med värdet `hybris` korrelerar till exempel till OSGi-konfigurationen för **Day CQ Commerce Factory för Hybris** (com.adobe.cq.commerce.hybris.impl.HybrisServiceFactory) - där parametern `commerceProvider` också har värdet `hybris`.

   * Här finns ytterligare egenskaper, som **Katalogversion**, som kan konfigureras (när det är lämpligt och tillgängligt).

Se följande exempel nedan:

| `cq:commerceProvider = geometrixx` | i en AEM krävs en specifik implementering. Exempel på Geometrixx, som innehåller minimala tillägg till det allmänna API:t |
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

* Lägg till följande kommandoradsargument till kommandot när du anropar maven

  `-P hybris4`

  Den hämtar den förkonfigurerade Hybris 4-distributionen och bäddar in den i paketet `cq-commerce-hybris-server`.

* I OSGi-konfigurationshanteraren:

   * Inaktivera stöd för Hybris 5 för tjänsten Default Response Parser.

   * Kontrollera att tjänsten Hybris Basic Authentication Handler har en lägre prioritetsordning än tjänsten Hybris OAuth Handler.

### Sessionshantering {#session-handling}

hybris använder en användarsession för att lagra information som kundens kundvagn. Sessions-ID returneras från hybris i en `JSESSIONID`-cookie som måste skickas på efterföljande begäranden till hybris. För att undvika att lagra sessions-ID i databasen kodas det i en annan cookie som lagras i kundens webbläsare. Följande steg utförs:

* På den första begäran anges ingen cookie på köparens begäran, så en begäran skickas till hybris-instansen för att skapa en session.

* Sessionskakorna extraheras från svaret, kodas i en ny cookie (till exempel `hybris-session-rest`) och anges i svaret till användaren. Kodningen i en ny cookie krävs eftersom den ursprungliga cookien bara är giltig för en viss sökväg och annars inte skulle skickas tillbaka från webbläsaren i efterföljande begäranden. Sökvägsinformationen måste läggas till i cookie-filens värde.

* På efterföljande begäranden avkodas cookies från `hybris-session-<*xxx*>`-cookies och anges på HTTP-klienten som används för att begära data från hybris.

>[!NOTE]
>
>En ny anonym session skapas när den ursprungliga sessionen inte längre är giltig.

#### CommerceSession {#commercesession}

* Den här sessionen äger **kundvagnen**

   * utför Lägg till/ta bort/etc

   * utför de olika beräkningarna av vagnen,

     `commerceSession.getProductPrice(Product product)`

* Äger *lagringsplatsen* för **order**-data

  `CommerceSession.getUserContext()`

* Äger bearbetningsanslutningen för **betalningen**

* Äger anslutningen **fulfillment**

### Produktsynkronisering och publicering {#product-synchronization-and-publishing}

Produktdata som finns i hybris måste finnas i AEM. Följande mekanism har implementerats:

* En initial belastning av ID:n tillhandahålls av hybris som foder. Denna feed kan uppdateras.
* hybris levererar uppdateringsinformation via ett foder (som AEM undersökningar).
* När AEM använder produktdata skickas begäranden tillbaka till hybris för aktuella data (villkorlig begäran om hämtning med det senaste ändringsdatumet).
* På hybris är det möjligt att ange foderinnehållet på ett deklarativt sätt.
* Mappning av matningsstrukturen till AEM innehållsmodell sker i matningsadaptern på AEM.

![chlimage_1-12](/help/sites-developing/assets/chlimage_1-12a.png)

* Importören (b) används för den första konfigurationen av sidträdstrukturen i AEM för kataloger.
* Katalogförändringar i hybris anges som AEM via en feed och sedan sprida dessa till AEM b.

   * Produkten har lagts till/tagits bort/ändrats vad gäller katalogversionen.

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

* Katalogkonfigurationen i AEM känner igen katalogversionerna **Mellanlagrade** och **Online**.

* För att synkronisera produkter mellan katalogversioner krävs aktivering eller inaktivering av motsvarande AEM (a, c)

   * Om du vill lägga till en produkt i en **Online** -katalogversion måste du aktivera produktens sida.

   * Borttagning av en produkt kräver inaktivering.

* Aktivering av en sida i AEM c kräver en kontroll (b) och är endast möjlig om

   * Produkten finns i en **Online**-katalogversion för produktsidor.

   * De refererade produkterna är tillgängliga i katalogversionen **Online** för andra sidor (till exempel kampanjsidor).

* Aktiverade produktsidor måste ha åtkomst till produktdatans **Online**-version (d).

* Den AEM Publish-instansen kräver åtkomst till hybris för att hämta produktdata och personaliserade data (d).

### Arkitektur {#architecture}

#### Arkitektur för produkt och varianter {#architecture-of-product-and-variants}

En enskild produkt kan ha flera variationer, t.ex. beroende på färg och/eller storlek. En produkt måste definiera vilka egenskaper som driver variationen. Adobe definierar dessa *variantaxlar*.

Alla egenskaper är dock inte olika axlar. Variationer kan också påverka andra egenskaper. Priset kan till exempel vara beroende av storleken. Dessa egenskaper kan inte väljas av kunden och betraktas därför inte som olika axlar.

Varje produkt och/eller variant representeras av en resurs och mappar därför 1:1 till en databasnod. Det är en extra konsekvens att en specifik produkt och/eller variant kan identifieras unikt genom sin sökväg.

Produkt-/variantresursen innehåller inte alltid den faktiska produktinformationen. Det kan vara en representation av data som finns i ett annat system (t.ex. hybris). Produktbeskrivningar och priser lagras till exempel inte i AEM utan hämtas i realtid från eCommerce-motorn.

Alla produktresurser kan representeras av en `Product API`. De flesta anrop i produkt-API:t är variantspecifika (även om varianter kan ärva delade värden från ett överordnat element), men det finns också anrop som listar variantuppsättningen ( `getVariantAxes()`, `getVariants()` och så vidare).

>[!NOTE]
>
>En variantaxel bestäms av det `Product.getVariantAxes()` returnerar:
>* hybris definierar den för hybris-implementeringen
>
>Produkter (i allmänhet) kan ha många olika axlar, men produktkomponenten som finns i paketet hanterar bara två:
>
>1. `size`
>
>1. plus en till
>
>Den här ytterligare varianten väljs via egenskapen `variationAxis` i produktreferensen (vanligtvis `color` för Geometrixx Outdoors).

#### Produktreferenser och produktdata {#product-references-and-product-data}

Vanligtvis finns produktdata under `/etc` och produktreferenser under `/content`.

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

   * Produktnoderna är `nt:unstructured`.

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

   * `CommerceSession` utför tillägg eller borttagning och så vidare.
   * `CommerceSession` utför även de olika beräkningarna på kundvagnen. &quot;

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

   * I hybris-fallet äger hybris-servern kundvagnen.
   * I det AEM allmänna fallet lagras kundvagnar i [ClientContexten](/help/sites-administering/client-context.md).

**Personalization**

* Kör alltid personalisering via [ClientContexten](/help/sites-administering/client-context.md).
* En ClientContext `/version/` av kundvagnen skapas i samtliga fall:

   * Produkter ska läggas till med metoden `CommerceSession.addCartEntry()`.

* Följande illustrerar ett exempel på kundvagnsinformation i kundvagnen:

![chlimage_1-13](/help/sites-developing/assets/chlimage_1-13a.png)

#### Arkitektur för utcheckning {#architecture-of-checkout}

**Kundvagn- och beställningsdata**

`CommerceSession` äger de tre elementen:

1. Kundvagnsinnehåll
1. Priser
1. Orderinformation

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
   * Kan hämta/uppdatera leveransinformation med `updateOrder(Map<String, Object> delta)`

>[!NOTE]
>
>Du kan implementera en leveransväljare, till exempel:
>
>`yourProject/commerce/components/shippingpicker`:
>
>* Detta kan i princip vara en kopia av `foundation/components/form/radio`, men med återanrop till `CommerceSession` för:
>
>* Kontrollera om metoden är tillgänglig
>* Lägga till prisinformation
>* Om du vill att kunderna ska kunna uppdatera beställningssidan i AEM (inklusive den överordnade texten för leveransmetoder och texten som beskriver dem), samtidigt som de fortfarande har kontrollen att visa relevant `CommerceSession`-information.

**Betalningsbearbetning**

* `CommerceSession` äger även anslutningen för betalningsbearbetning.

* Implementerare bör lägga till specifika anrop (till den valda betalningshanteringstjänsten) i implementeringen av `CommerceSession`.

**Beställningsuppfyllelse**

* `CommerceSession` äger också leveransanslutningen.
* Implementerare måste lägga till specifika anrop (till den valda betalningshanteringstjänsten) i implementeringen av `CommerceSession`.

### Sökdefinition {#search-definition}

I enlighet med standardtjänstens API-modell innehåller e-handelsprojektet en uppsättning sökrelaterade API:er som kan implementeras av enskilda e-handelsmotorer.

>[!NOTE]
>
>För närvarande är det bara hybris-motorn som implementerar söknings-API:t.
>
>Söknings-API:t är dock allmänt och kan implementeras av varje enskild CommerceService.

E-handelsprojektet innehåller en standardsökkomponent i:

`/libs/commerce/components/search`

![chlimage_1-14](/help/sites-developing/assets/chlimage_1-14a.png)

Detta använder söknings-API:t för att fråga den valda e-handelsmotorn (se [Val av eCommerce Engine](#ecommerce-engine-selection)):

#### Söknings-API {#search-api}

Det finns flera allmänna/hjälpklasser i huvudprojektet:

1. `CommerceQuery`

   Beskriver en sökfråga (innehåller information om frågetext, aktuell sida, sidstorlek, sortering och valda aspekter). Alla e-handelstjänster som implementerar söknings-API:t får instanser av den här klassen för att utföra sökningen. En `CommerceQuery` kan instansieras från ett begäranobjekt ( `HttpServletRequest`).

1. `FacetParamHelper`

   Är en verktygsklass som innehåller en statisk metod - `toParams` - som används för att generera `GET` parametersträngar från en lista med facets och ett växlat värde. Detta är användbart på användargränssnittssidan, där du måste visa en hyperlänk för varje värde för varje aspekt, så att respektive värde växlas när användaren klickar på hyperlänken. Det vill säga, om den har markerats tas den bort från frågan, och läggs i annat fall till. Detta tar hand om all logik som används för att hantera flera-/enkelvärdesfaktorer, åsidosätta värden och så vidare.

Startpunkten för söknings-API är metoden `CommerceService#search` som returnerar ett `CommerceResult`-objekt. Mer information om det här ämnet finns i [API-dokumentationen](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation).

### Användarintegrering {#user-integration}

Integrering sker mellan AEM och olika e-handelssystem. Detta kräver en strategi för att synkronisera kunder mellan de olika systemen så att AEM specifik kod bara behöver känna till AEM och omvänt:

* Autentisering

  AEM antas vara webbfront *only* och utför därför *all*-autentisering.

* Konton i Hybris

  AEM skapar ett motsvarande (underordnat) konto i hybris för varje kund. Användarnamnet för det här kontot är samma som AEM användarnamn. Ett kryptografiskt slumpmässigt lösenord genereras automatiskt och lagras (krypteras) i AEM.

#### Befintliga användare {#pre-existing-users}

En AEM framände kan placeras framför en befintlig hybris-implementering. En hybris-motor kan också läggas till i en befintlig AEM. För att göra detta måste systemen kunna hantera befintliga användare på ett effektivt sätt i båda systemen:

* AEM > hybris

   * När du loggar in på hybris, om den AEM användaren inte finns:

      * skapa en hybris-användare med ett kryptografiskt slumpmässigt lösenord
      * lagra hybris-användarnamnet i AEM användarkatalog

   * Se: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`

* hybris > AEM

   * När du loggar in på AEM, om systemet känner igen användaren:

      * försök att logga in på hybris med det angivna användarnamnet/pwd
      * om det lyckas skapar du användaren i AEM med samma lösenord (AEM-specifikt salt-värde ger AEM-specifik hash-kod)

   * Ovanstående algoritm är implementerad i en Sling `AuthenticationInfoPostProcessor`

      * Se: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`

### Anpassa importprocessen {#customizing-the-import-process}

Så här bygger du på befintliga funktioner i din anpassade importhanterare:

* måste implementera gränssnittet `ImportHandler`

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
  * @param parentPath    Path of parent category or base path of import if there is a root category
  * @return Path of created category
  */
  public String createCategory(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;
}
```

För att din anpassade hanterare ska identifieras av importeraren måste den ange egenskapen `service.ranking` med ett värde över 0.

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
