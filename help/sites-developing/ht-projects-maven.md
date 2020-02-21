---
title: Så här skapar du AEM-projekt med Apache Maven
seo-title: Så här skapar du AEM-projekt med Apache Maven
description: I det här dokumentet beskrivs hur du konfigurerar ett AEM-projekt baserat på Apache Maven
seo-description: I det här dokumentet beskrivs hur du konfigurerar ett AEM-projekt baserat på Apache Maven
uuid: 5db68639-7393-48b7-9d81-5b19b596ff21
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 3ebc1d22-a7a2-4375-9aa5-a18a7ceb446a
docset: aem65
translation-type: tm+mt
source-git-commit: 9d42526ff4c7b7d8a31690ebfb8b45d0e951ebac

---


# Så här skapar du AEM-projekt med Apache Maven{#how-to-build-aem-projects-using-apache-maven}

## Översikt {#overview}

I det här dokumentet beskrivs hur du konfigurerar ett AEM-projekt baserat på [Apache Maven](https://maven.apache.org/).

Apache Maven är ett verktyg med öppen källkod för att hantera programvaruprojekt genom att automatisera byggen och tillhandahålla projektinformation av hög kvalitet. Det är det rekommenderade bygghanteringsverktyget för AEM-projekt.

Att bygga ett AEM-projekt baserat på Maven ger dig flera fördelar:

* En IDE-agnostisk utvecklingsmiljö
* Användning av Maven Archetypes och Artifacts från Adobe
* Användning av verktygsuppsättningarna Apache Sling och Apache Felix för Maven-baserade utvecklingsmiljöer
* Enkel import till en integrerad utvecklingsmiljö. till exempel Eclipse och/eller IntelliJ
* Enkel integrering med system för kontinuerlig integrering

### Maven Project Archetypes {#maven-project-archetypes}

Adobe tillhandahåller två Maven-arkitekter som kan fungera som baslinje för dina AEM-projekt. Mer information finns på länkarna nedan:

* [AEM-projekttyp](https://github.com/adobe/aem-project-archetype)
* [Maven Archetype for Single Page Applications Starter Kit](https://github.com/adobe/aem-spa-project-archetype)

## Experience Manager API-beroenden {#experience-manager-api-dependencies}

### Vad är UberJar? {#what-is-the-uberjar}

&quot;UberJar&quot; är det informella namn som ges till en särskild Java Archives-fil (JAR) från Adobe. Dessa JAR-filer innehåller alla publika Java-API:er som exponeras av Adobe Experience Manager. De innehåller även begränsade externa bibliotek, särskilt alla publika API:er i AEM som kommer från Apache Sling, Apache Jackrabbit, Apache Lucene, Google Guava och två bibliotek som används för bildbearbetning (Werner Randelshofer&#39;s CYMK JPEG ImageIO-bibliotek och TwelveMonkeys bildbibliotek). UberJars innehåller bara API-gränssnitt och klasser, vilket innebär att de bara innehåller gränssnitt och klasser som exporteras av ett OSGi-paket i AEM. De innehåller också en *MANIFEST.MF* -fil som innehåller rätt paketexportversioner för alla dessa exporterade paket, vilket säkerställer att projekt som skapats mot UberJar har rätt paketimportintervall.

### Varför skapade Adobe UberJars? {#why-did-adobe-create-the-uberjars}

Tidigare var utvecklarna tvungna att hantera ett relativt stort antal enskilda beroenden till olika AEM-bibliotek, och när varje nytt API användes var det nödvändigt att lägga till ett eller flera individuella beroenden i projektet. I ett projekt ledde införandet av UberJar till att 30 olika beroenden togs bort från projektet.

Från och med AEM 6.5 tillhandahåller Adobe två UberJars: ett som innehåller borttagna gränssnitt och ett som tar bort dessa borttagna gränssnitt. Genom att referera till en explicit vid byggtillfället, är kunderna noga med att förstå om de är beroende av inaktuell kod.

Den andra Uber Jar rensar bort alla inaktuella klasser, metoder och egenskaper så att kunderna kan kompilera mot dem och förstå om den anpassade koden är ett framtida bevis.

### Vilken UberJar ska användas? {#which-uberjar-to-use}

AEM 6.5 finns i två versioner av Uber Jar:

1. Uber Jar - Inkluderar endast de publika gränssnitt som inte är markerade för borttagning. Det här är den **rekommenderade** UberJar-metoden som används för att framtidssäkra kodbasen från att förlita sig på inaktuella API:er.
1. Uber Jar med inaktuella API:er - Innehåller alla publika gränssnitt, inklusive de som markerats för borttagning i en framtida version av AEM.

### Hur använder jag UberJars? {#how-to-i-use-the-uberjars}

Om du använder Apache Maven som ett byggsystem (vilket är fallet för de flesta AEM Java-projekt) måste du lägga till ett eller två element i *filen pom.xml* . Det första är ett *beroendeelement* som lägger till det faktiska beroendet i ditt projekt:

**Uber Jar-beroende *(utan inaktuella API:er)***

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

**Uber JAR-beroende med inaktuella API:er**

>[!CAUTION]
>
>Adobe rekommenderar att du distribuerar mot Uber Jar så att ***inte* **innehåller de föråldrade API:erna så att du kan vara säker på att dina program kommer att köras korrekt i framtida versioner av AEM.
>
>Använd bara Uber Jar med inaktuellt API-stöd om koden som är beroende av de inaktuella API:erna inte kan ändras för att passa ändringarna.

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis-with-deprecations</classifier>
    <scope>provided</scope>
</dependency>
```

Om ditt företag redan använder en Maven Repository Manager, t.ex. Sonatype Nexus, Apache Archiva eller JFrog Artifactory, lägger du till rätt konfiguration i ditt projekt som referens till den här databashanteraren och lägger till Adobes Maven-databas ([https://repo.adobe.com/nexus/content/groups/public/](https://repo.adobe.com/nexus/content/groups/public/)) i din databashanterare.

Om du inte använder en databashanterare måste du lägga till ett *databaselement* i din *pom.xml* -fil:

```xml
<repositories>
    <repository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.adobe.com/nexus/content/groups/public/</url>
        <layout>default</layout>
    </repository>
</repositories>
<pluginRepositories>
    <pluginRepository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.adobe.com/nexus/content/groups/public/</url>
        <layout>default</layout>
    </pluginRepository>
</pluginRepositories>
```

### Vad kan jag göra med UberJar? {#what-can-i-do-with-the-uberjar}

Med UberJar kan du kompilera projektkod som är beroende av AEM API:er (och de API:er som används i de projekt som nämns ovan). Du kan också generera information om OSGi Service Component Runtime (SCR) och OSGi Metatype. Med vissa begränsningar kan du även skriva och köra enhetstester.

### Vad kan jag inte göra med UberJar? {#what-can-t-i-do-with-the-uberjar}

Eftersom UberJar **bara** innehåller API:er är den inte körbar och kan inte användas för att **köra** Adobe Experience Manager. För att köra AEM behöver du formuläret AEM QuickStart, antingen fristående eller WAR (Web Application Archive).

### Du nämnde begränsningar för enhetstester. Vänligen förklara vidare. {#you-mentioned-limitations-on-unit-tests-please-explain-further}

Enhetstester interagerar vanligtvis med produkt-API:er på tre olika sätt, som alla påverkas något olika av UberJar.

#### Använd fall 1 - Anpassad kod som anropar ett API-gränssnitt {#use-case-custom-code-which-calls-a-api-interface}

I det här fallet, som är det vanligaste, ingår anpassad kod som kör metoder i ett Java-gränssnitt som definieras av AEM API. Implementeringen av detta gränssnitt kan antingen tillhandahållas direkt eller injiceras med hjälp av Dependency Injection-mönstret. **Det här användningsfallet kan hanteras med UberJar.**

Ett exempel på det första är:

```java
public class ClassWhichHasAEMInterfacePassedIn {
    /**
     * Get the first length characters of the page title.
     */
    public String getTrimmedTitle(Page page, int length) {
         String title = page.getTitle();
         return StringUtils.left(title, length);
    }
}
```

Ett exempel på det senare är:

```java
@Component
@Service
public class ComponentWhichHasAEMInterfaceInjected implements TitleTrimmer {
    @Reference
    private PageManagerFactory pageManagerFactory;

    /**
     * Get the first length characters of the title of the page containing the provided Resource.
     */
    public String getTrimmedTitle(Resource resource, int length) {
        PageManager pageManager = pageManagerFactory.getPageManager(resource.getResourceResolver());
        Page page = pageManager.getContainingPage(resource);
        if (page == null) {
           return null;
        }
        String title = page.getTitle();
        return StringUtils.left(title, length);
    }
}
```

För enhetstestning av någon av dessa metoder använder en utvecklare ett modellramverk som [JMockit](http://jmockit.github.io), [Mockito](https://mockito.org/), [JMock](https://www.jmock.org/)eller [Easymock](https://easymock.org/) för att skapa ett modellobjekt för det AEM API som refereras. De här exemplen använder JMockit, men i det här specifika fallet är skillnaden mellan dessa ramverk i stort sett syntativ.

```java
@RunWith(JMockit.class)
public class ClassWhichHasAEMInterfacePassedInTest {

    @Tested
    private ClassWhichHasAEMInterfacePassedIn instance;

    @Mocked
    private Page page;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(page, 8));
    }
}
```

```java
@RunWith(JMockit.class)
public class ComponentWhichHasAEMInterfaceInjectedTest {

    @Tested
    private ComponentWhichHasAEMInterfaceInjected instance;

    @Mocked
    private Page page;

    @Mocked
    private PageManager pageManager;

    @Injectable
    private PageManagerFactory pageManagerFactory;

    @Mocked
    private Resource resource;

    @Mocked
    private ResourceResolver resourceResolver;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            resource.getResourceResolver();
            result = resourceResolver;
            pageManagerFactory.getPageManager(resourceResolver);
            result = pageManager;
            pageManager.getContainingPage(resource);
            result = page;
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(resource, 8));
    }
}
```

#### Använd fall nr 2 - Anpassad kod som anropar en API-implementeringsklass {#use-case-custom-code-which-calls-an-api-implementation-class}

Det här användningsfallet innebär anrop till en statisk metod eller instansmetod för en klass i AEM API där du refererar till en konkret klass, till skillnad från ett gränssnitt som i Use Case #1.

```java
public class ClassWhichUsesAStaticMethodFromAPI {

    /**
     * Get a map of asset titles to asset objects.
     *
     * @param resource either an asset resource or a folder containing assets.
     * @return an map of titles to assets. if an asset doesn't have a title, the name is used instead.
     */
    public Map<String, Asset> getAssetTitles(Resource resource) {
        Iterator<Asset> assets = DamUtil.getAssets(resource);
        Map<String, Asset> result = new HashMap<String, Asset>();
        while (assets.hasNext()) {
            Asset asset = assets.next();
            String title = asset.getMetadataValue(DamConstants.DC_TITLE);
            if (title == null) {
                title = asset.getName();
            }
            result.put(title, asset);
        }
        return result;
    }
}
```

```java
public class ClassWhichUsesAnInstanceMethodFromAPI {

    /**
     * Count the number of paragraphs in a parsys.
     *
     * @param resource the parsys resource
     * @return the count
     */
    public int countParagraphs(Resource resource) {
        return new ParagraphSystem(resource).paragraphs().size();
    }
}
```

**Det här användningsexemplet kan hanteras med UberJar**. Du bör emellertid fortfarande göra en dummy av API:t när det är möjligt för prestandatester.

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAStaticMethodFromAPITest {

    @Tested
    private ClassWhichUsesAStaticMethodFromAPI instance;

    @Mocked(stubOutClassInitialization = true)
    private DamUtil unusedDamUtil = null;

    @Mocked
    private Resource resource;

    @Test
    public void test_that_empty_iterator_produces_empty_map() {
        new Expectations() {
            {
                DamUtil.getAssets(resource);
                result = Collections.<Asset> emptySet().iterator();
            }
        };
        Map<String, Asset> result = new ClassWhichUsesAStaticMethodFromAPI().getAssetTitles(resource);
        assertNotNull(result);
        assertEquals(0, result.size());
    }
    @Test
    public void test_with_reference_search() {
        assertTrue(true);
    }
}
```

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAnInstanceMethodFromAPITest {

    @Tested
    private ClassWhichUsesAnInstanceMethodFromAPI instance;

    @Mocked
    private Resource parsys;

    @Mocked
    private Paragraph firstPar;

    @Mocked
    private Paragraph secondPar;

    @Test
    public void test_empty_parsys_returns_zero() {
        new MockUp<ParagraphSystem>() {
            @Mock
            public void $init(Resource resource) {
                assertEquals(parsys, resource);
            }
            @Mock
            public List<Paragraph> paragraphs() {
                return Collections.<Paragraph> emptyList();
            }
        };
        assertEquals(0, instance.countParagraphs(parsys));
    }
}
```

#### Använd fall nr 3 - Anpassad kod som utökar en basklass från API:t {#use-case-custom-code-which-extends-a-base-class-from-the-api}

Precis som för SCR Generation, **måste** du använda UberJar för att testa om koden utökar en basklass (abstrakt eller betong) från AEM API:t.

## Vanliga utvecklingsuppgifter med Maven {#common-development-tasks-with-maven}

### Så här lägger du till banor i innehållsmodulen {#how-to-add-paths-to-the-content-module}

Innehållsmodulen innehåller en fil src/main/content/META-INF/vault/filter.xml som definierar filtren för AEM-paketet som skapas av Maven. Filen som skapas av Maven-arkivtypen ser ut så här:

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

Den här filen används på flera olika sätt:

* genom `content-package-maven-plugin` att bestämma vilket innehåll som ska inkluderas i paketet
* av VLT-verktyget för att avgöra vilka banor som ska övervägas
* om paketet är ombyggt i AEM Package Manager, definierar detta även vilka sökvägar som ska inkluderas

Beroende på programmets krav kan det vara bra att lägga till mer innehåll i sökvägarna, till exempel:

* Konfigurationer för utrullning
* Blueprints
* Arbetsflödesmodeller
* Designsidor
* Exempelinnehåll

Lägg till fler `<filter>` element i banorna:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
    <filter root="/etc/msm/rolloutconfigs/myrolloutconfig"/>
    <filter root="/etc/blueprints/mysite/globalsite"/>
    <filter root="/etc/workflow/models/myproject"/>
    <filter root="/etc/designs/myproject"/>
    <filter root="/content/myproject/sample-content"/>
</workspaceFilter>
```

#### Lägga till sökvägar i paketet utan att synkronisera dem {#adding-paths-to-the-package-without-syncing-them}

Om du har filer som ska läggas till i paketet som skapas av content-package-mask-plugin-programmet, men som inte ska synkroniseras mellan filsystemet och databasen, kan du använda `.vltignore` filer. Dessa filer har samma syntax som [.gitignore](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html) -filer.

Arketypen använder till exempel en `.vltignore` fil för att förhindra att den JAR-fil som är installerad som en del av paketet synkroniseras tillbaka till filsystemet:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore}

```xml
*.jar
```

#### Synkronisera banor utan att lägga till dem i paketet {#syncing-paths-without-adding-them-to-the-package}

I vissa fall kanske du vill synkronisera vissa sökvägar mellan filsystemet och databasen, men inte låta dem ingå i det paket som ska installeras i AEM.

Ett typiskt fall är `/libs/foundation` banan. I utvecklingssyfte kanske du vill att innehållet i den här sökvägen ska vara tillgängligt i filsystemet, så att t.ex. din IDE kan matcha JSP-inkluderingar som inkluderar JSP:er i `/libs`. Du vill dock inte inkludera den delen i paketet som du skapar, eftersom delen innehåller produktkod som inte får ändras av anpassade implementeringar `/libs` .

För att uppnå detta kan du ange en fil `src/main/content/META-INF/vault/filter-vlt.xml`. Om den här filen finns kommer den att användas av VLT-verktyget, t.ex. när du utför `vlt up` och `vlt ci`, eller när du har konfigurerat `vlt sync` . content-package-maven-plugin-programmet fortsätter att använda filen `src/main/content/META-INF/vault/filter.xml` när paketet skapas.

Om du till exempel vill göra `/libs/foundation` tillgängligt lokalt för utveckling, men bara inkludera `/apps/myproject` i paketet, använder du följande två filer.

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml-1}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

#### src/main/content/META-INF/vault/filter-vlt.xml {#src-main-content-meta-inf-vault-filter-vlt-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/libs/foundation"/>
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

Du måste också konfigurera om plugin-programmet maven-resources-plugin för att inte inkludera dessa filer i paketet: filen filter.xml tillämpas inte när paketet installeras, men bara när paketet byggs igen med hjälp av pakethanteraren.

Ändra `<resources>` avsnittet i innehållshandboken enligt följande:

#### src/main/content/pom.xml {#src-main-content-pom-xml}

```xml
<!-- ... -->
<resources>
 <resource>
  <directory>src/main/content/jcr_root</directory>
  <filtering>false</filtering>
  <excludes>
   <exclude>**/.vlt</exclude>
   <exclude>**/.vltignore</exclude>
   <exclude>libs/</exclude>
  </excludes>
 </resource>
</resources>
<!-- ... -->
```

### Så här arbetar du med JSP:er {#how-to-work-with-jsps}

I Maven-konfigurationen som beskrivits hittills skapas ett innehållspaket som även kan innehålla komponenter och motsvarande JSP:er. Men Maven behandlar dem som andra filer som är en del av innehållspaketet och känner inte ens igen dem som JSP:er.

De resulterande komponenterna fungerar på samma sätt i AEM, men det finns två stora fördelar med att göra Maven medveten om JSP:erna

* Maven kan misslyckas om JSP:er innehåller fel, så att dessa uppstår vid byggtillfället och inte när de kompileras första gången i AEM
* För IDE-miljöer som kan importera Maven-projekt möjliggör detta även kodkomplettering och stöd för taggbibliotek i JSP-programmen

Det krävs två saker för att aktivera den här konfigurationen:

1. lägg till taggbiblioteksberoenden
1. kompilera JSP:er som en del av Maven-kompileringsprocessen

#### Lägga till taggbiblioteksberoenden {#adding-tag-library-dependencies}

Nedanstående beroenden måste läggas till i modulens POM `content` .

>[!NOTE]
>
>Om du inte importerar produktberoenden enligt beskrivningen i [Importera AEM-produktberoenden](#importingaemproductdependencies) ovan, måste de också läggas till i den överordnade produktstrukturen tillsammans med den version som matchar din AEM-konfiguration enligt beskrivningen i [Lägga till beroenden](#addingdependencies) ovan. Kommentarerna i varje post nedan visar det paket som du vill söka efter i Beroendesökaren.

>[!NOTE]
>
>Artefakten ingår inte i `com.adobe.granite.xssprotection` POM för cq-quickstart-product-skindencies och kräver fullständiga Maven-koordinater enligt Dependency Finder.

#### Kompilera JSP som en del av Maven Compile Phase {#compiling-jsps-as-part-of-the-maven-compile-phase}

För att kompilera JSP:er i Maven `compile` fas använder vi Apache Slings [Maven JspC-plugin](https://sling.apache.org/documentation/development/jspc.html) enligt nedan:

* vi ställer in en körning för `jspc` målet (vilket som standard binder till `compile` fasen, så vi behöver inte ange fasen explicit)

* vi anger att den ska kompilera JSP:er i `${project.build.directory}/jsps-to-compile`
* och returnerar resultatet till `${project.build.directory}/ignoredjspc` (vilket innebär `myproject/content/target/ignoredjspc`)

* Vi har konfigurerat maven-resources-plugin för att kopiera JSP:er till `${project.build.directory}/jsps-to-compile` i genereringskällefasen och konfigurera den så att den inte kopierar `libs/` mappen (eftersom det är AEM-produktkod och vi varken vill använda beroenden för kompilering för projektet eller verifiera att den kompileras.

Vårt främsta mål, enligt vad som anges ovan, är att validera JSP:erna och se till att byggprocessen misslyckas om de innehåller fel. Det är därför vi kompilerar dem till en separat katalog som ignoreras (och i själva verket raderas omedelbart därefter, som du kommer att se om en minut).

Resultatet av Maven JspC-pluginen kan också paketeras och driftsättas som en del av OSGi Bundle, men detta har andra konsekvenser och biverkningar och går utöver målet att validera de JSP:er.

För att de klasser som kompileras från JSP:n ska kunna tas bort konfigurerar vi plugin-programmet Maven Clean enligt nedan. Om du vill undersöka resultatet av pluginmodulen Maven JspC kan du köra `mvn compile` in `myproject/content` - sedan hittar du resultatet i `myproject/content/target/ignoredjspc`).

#### myproject/content/pom.xml {#myproject-content-pom-xml}

```xml
<build>
  <!-- ... -->
  <plugins>
    <!-- ... -->
    <plugin>
      <artifactId>maven-resources-plugin</artifactId>
      <executions>
        <execution>
          <id>copy-resources</id>
          <phase>generate-sources</phase>
          <goals>
            <goal>copy-resources</goal>
          </goals>
          <configuration>
            <outputDirectory>${project.build.directory}/jsps-to-compile</outputDirectory>
            <resources>
              <resource>
                <directory>src/main/content/jcr_root</directory>
                <excludes>
                  <exclude>libs/**</exclude>
                </excludes>
              </resource>
            </resources>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <groupId>org.apache.sling</groupId>
      <artifactId>maven-jspc-plugin</artifactId>
      <version>2.0.6</version>
      <executions>
        <execution>
          <id>compile-jsp</id>
          <goals>
            <goal>jspc</goal>
          </goals>
          <configuration>
            <jasperClassDebugInfo>false</jasperClassDebugInfo>
            <sourceDirectory>${project.build.directory}/jsps-to-compile</sourceDirectory>
            <outputDirectory>${project.build.directory}/ignoredjspc</outputDirectory>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <artifactId>maven-clean-plugin</artifactId>
      <executions>
        <execution>
          <id>remove-compiled-jsps</id>
          <goals>
            <goal>clean</goal>
          </goals>
          <phase>process-classes</phase>
          <configuration>
            <excludeDefaultDirectories>true</excludeDefaultDirectories>
            <filesets>
              <fileset>
                <directory>${project.build.directory}/jsps-to-compile</directory>
                <directory>${project.build.directory}/ignoredjspc</directory>
              </fileset>
            </filesets>
          </configuration>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

>[!NOTE]
>
>Beroende på om du faktiskt använder JSP-kod i `/libs` (d.v.s. inkluderar JSP:er därifrån) måste du förfina vilka JSP:er som kopieras för kompilering.
>
>Om du till exempel inkluderar `/libs/foundation/global.jsp`kan du använda följande konfiguration för `maven-resources-plugin` i stället för den konfiguration över som helt hoppar över `/libs`.
>
>
```
> <resource>  
>           <directory>src/main/content/jcr_root</directory>  
>           <includes>  
>                   <include>apps/**</include>  
>                   <include>libs/foundation/global.jsp</include>
>       </includes>  
>   </resource>  
>```

### Så här arbetar du med SCM-system {#how-to-work-with-scm-systems}

När du arbetar med hantering av källkonfiguration (SCM) bör du kontrollera att

* VCS ignorerar icke-källartefakter i filsystemet
* VLT ignorerar artefakter i VCS och checkar inte in dem i databasen

>[!NOTE]
>
>Beskrivningen handlar inte om hur du konfigurerar Maven så att den fungerar med din SCM, som beskrivs utförligt i [Maven POM-referensen](https://maven.apache.org/pom.html#SCM) och [Maven SCM Plugin-programmets dokumentation](https://maven.apache.org/scm/).

#### Mönster som ska uteslutas från SCM {#patterns-to-exclude-from-scm}

Nedan följer en typisk lista över mönster som ska inkluderas från SCM. Om du t.ex. använder Git kan du lägga till dessa i projektets `.gitignore` fil.

#### sample.gitignore {#sample-gitignore}

```shell
# Ignore VLT files
.vlt
.vlt-sync.log
.vlt-sync-config.properties

# Ignore Quickstart launches in the source tree
license.properties
crx-quickstart

# Ignore compilation results
target

# Ignore IDE and Operating System artifacts
.idea
.classpath
.metadata
.project
.settings
maven-eclipse.xml
*.iml
*.ipr
*.iws
.DS_Store
```

#### Ignorerar SCM-kontrollfiler i VLT {#ignoring-scm-control-files-in-vlt}

I vissa fall kan du ha SCM-kontrollfiler i innehållskällträdet som du inte vill checka in i databasen.

Tänk på följande situation:

Arketypen har redan skapat en .vltignore-fil för att förhindra att den installerade källfilen synkroniseras tillbaka till filsystemet:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-1}

```shell
*.jar
```

Du vill naturligtvis inte heller ha den här filen i SCM, så om du t.ex. använder Git lägger du till en motsvarande fil. `gitignore` fil:

#### src/main/content/jcr_root/apps/myproject/install/.gitignore {#src-main-content-jcr-root-apps-myproject-install-gitignore}

```shell
*.jar
```

Som . `gitignore` -filen får inte heller gå in i databasen. `vltignore` filen måste utökas för att inkludera . `gitignore` fil:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-2}

```shell
*.jar
.gitignore
```

### Arbeta med distributionsprofiler {#how-to-work-with-deployment-profiles}

Om byggprocessen ingår i en större konfiguration av livscykelhantering, till exempel en kontinuerlig integreringsprocess, behöver du ofta distribuera till andra datorer än bara utvecklarens lokala instans.

I sådana fall kan du enkelt lägga till nya [Maven Build-profiler](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) i projektets POM.

I exemplet nedan läggs en profil till `integrationServer`som definierar värdnamnen och portarna för författaren och publiceringsinstanserna. Du kan distribuera till dessa servrar genom att köra maven från projektets rot enligt nedan.

```shell
# install on integration test author
$ mvn -PautoInstallPackage -PintegrationServer install

# install on integration test publisher
$ mvn -PautoInstallPackagePublish -PintegrationServer install
```

#### myproject/pom.xml {#myproject-pom-xml}

```xml
<profiles>

    <!-- ... -->

    <profile>
        <id>integrationServer</id>
        <properties>
            <crx.host>dev-author.intranet</crx.host>
            <crx.port>5502</crx.port>
            <publish.crx.host>dev-publish.intranet</publish.crx.host>
            <publish.crx.port>5503</publish.crx.port>
        </properties>
    </profile>
</profiles>
```

### Hur man arbetar med AEM Communities {#how-to-work-with-aem-communities}

Om du har licens för AEM Communities-funktionen krävs ytterligare en API-behållare.

Mer information finns i [Använda Maven för grupper](/help/communities/maven.md)
