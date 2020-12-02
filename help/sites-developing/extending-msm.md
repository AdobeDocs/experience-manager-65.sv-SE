---
title: Utöka Multi Site Manager
seo-title: Utöka Multi Site Manager
description: Den här sidan hjälper dig att utöka funktionerna i Multi Site Manager
seo-description: Den här sidan hjälper dig att utöka funktionerna i Multi Site Manager
uuid: dfa7d050-29fc-4401-8d4d-d6ace6b49bea
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6128c91a-4173-42b4-926f-bbbb2b54ba5b
docset: aem65
translation-type: tm+mt
source-git-commit: 3a1d02fc1bc561b54e57cf91abc8f4406ba8c365
workflow-type: tm+mt
source-wordcount: '2601'
ht-degree: 0%

---


# Utöka Multi Site Manager{#extending-the-multi-site-manager}

På den här sidan kan du utöka funktionerna i Multi Site Manager:

* Läs mer om huvudmedlemmarna i MSM Java API.
* Skapa en ny synkroniseringsåtgärd som kan användas i en utrullningskonfiguration.
* Ändra standardspråk och landskoder.

<!-- * Remove the "Chapters" step in the Create Site wizard. -->

>[!NOTE]
>
>Den här sidan ska läsas tillsammans med [Återanvända innehåll: Multi Site Manager](/help/sites-administering/msm.md).
>
>Följande avsnitt av Omstrukturering av Sites Repository i AEM 6.4 kan också vara av intresse:
>* [Designkonfigurationer för hantering av flera webbplatser](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-blueprint-configurations)
>* [Körningskonfigurationer för flera platshanterare](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-rollout-configurations)


>[!CAUTION]
>
>Multi Site Manager och dess API används vid utvecklingen av en webbplats, så de är bara avsedda att användas i en författarmiljö.

## Översikt över Java API {#overview-of-the-java-api}

Hantering av flera platser består av följande paket:

* [com.day.cq.wcm.msm.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.Commons](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

De huvudsakliga MSM API-objekten interagerar på följande sätt (se även [Använda termer](/help/sites-administering/msm.md#terms-used)):

![chlimage_1-73](assets/chlimage_1-73.png)

* **`Blueprint`**

   En `Blueprint` (som i [blå konfiguration](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations)) anger de sidor från vilka en live-kopia kan ärva innehåll.

   ![chlimage_1-74](assets/chlimage_1-74.png)

   * Det är valfritt att använda en ritningskonfiguration ( `Blueprint`), men:

      * Tillåter författaren att använda alternativet **Rollout** i källan (att (explicit) skicka ändringar till live-kopior som ärver från den här källan).
      * Låter författaren använda **Skapa plats**; på så sätt kan användaren enkelt välja språk och konfigurera strukturen för live-kopian.
      * Definierar standardkonfigurationen för utrullning för alla resulterande live-kopior.

* **`LiveRelationship`** Anger  `LiveRelationship` anslutningen (relationen) mellan en resurs i livekopiegrenen och dess motsvarande källa/rityta.

   * Relationerna används vid arv och utrullning.
   * `LiveRelationship` -objekt ger åtkomst (referenser) till rollout-konfigurationer (  `RolloutConfig`),  `LiveCopy`och  `LiveStatus` objekt som är relaterade till relationen.

   * En live-kopia skapas t.ex. i `/content/copy/us` från källan/utkast på `/content/we-retail/language-masters`. Resurserna `/content/we.retail/language-masters/en/jcr:content` och `/content/copy/us/en/jcr:content` utgör en relation.

* **`LiveCopy`** `LiveCopy` innehåller konfigurationsinformation för relationerna (  `LiveRelationship`) mellan live-kopieringsresurserna och deras käll-/ritningsresurser.

   * Använd klassen `LiveCopy` för att komma åt sidans sökväg, sökvägen till käll-/ritningssidan, rollout-konfigurationerna och om underordnade sidor också ska inkluderas i `LiveCopy`.

   * En `LiveCopy`-nod skapas varje gång **Create Site** eller **Create Live Copy** används.

* **`LiveStatus`**

   `LiveStatus` -objekt ger åtkomst till körningsstatus för en  `LiveRelationship`. Används för att fråga synkroniseringsstatusen för en live-kopia.

* **`LiveAction`**

   En `LiveAction` är en åtgärd som körs för varje resurs som ingår i utrullningen.

   * LiveActions genereras endast av RolloutConfigs.

* **`LiveActionFactory`**

   Skapar `LiveAction`-objekt som tilldelats en `LiveAction`-konfiguration. Konfigurationer lagras som resurser i databasen.

* **`RolloutConfig`** Den  `RolloutConfig` innehåller en lista med  `LiveActions`som ska användas när den aktiveras. `LiveCopy` ärver `RolloutConfig` och resultatet finns i `LiveRelationship`.

   * När du konfigurerar en live-kopia för första gången används också en RolloutConfig (som utlöser LiveActions).

## Skapar en ny synkroniseringsåtgärd {#creating-a-new-synchronization-action}

Skapa anpassade synkroniseringsåtgärder som du kan använda med dina utrullningskonfigurationer. Skapa en synkroniseringsåtgärd när de [installerade åtgärderna](/help/sites-administering/msm-sync.md#installed-synchronization-actions) inte uppfyller dina specifika programkrav. Skapa då två klasser:

* En implementering av [ `com.day.cq.wcm.msm.api.LiveAction`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveAction.html)-gränssnittet som utför åtgärden.
* En OSGI-komponent som implementerar [ `com.day.cq.wcm.msm.api.LiveActionFactory`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html)-gränssnittet och skapar instanser av din `LiveAction`-klass.

`LiveActionFactory` skapar instanser av klassen `LiveAction` för en given konfiguration:

* `LiveAction` -klasser innehåller följande metoder:

   * `getName`: Returnerar namnet på åtgärden Namnet används för att referera till åtgärden, till exempel i utrullningskonfigurationer.
   * `execute`: Utför åtgärderna.

* `LiveActionFactory` -klasserna innehåller följande medlemmar:

   * `LIVE_ACTION_NAME`: Ett fält som innehåller namnet på det associerade fältet  `LiveAction`. Det här namnet måste sammanfalla med det värde som returneras av metoden `getName` i klassen `LiveAction`.

   * `createAction`: Skapar en instans av  `LiveAction`. Den valfria parametern `Resource` kan användas för att tillhandahålla konfigurationsinformation.

   * `createsAction`: Returnerar namnet på associerat  `LiveAction`objekt.

### Åtkomst till LiveAction-konfigurationsnoden {#accessing-the-liveaction-configuration-node}

Använd konfigurationsnoden `LiveAction` i databasen för att lagra information som påverkar körningsbeteendet för `LiveAction`-instansen. Noden i databasen som lagrar konfigurationen `LiveAction` är tillgänglig för objektet `LiveActionFactory` vid körning. Därför kan du lägga till egenskaper i konfigurationsnoden och använda dem i `LiveActionFactory`-implementeringen efter behov.

Ett `LiveAction`-objekt måste till exempel lagra namnet på den som skapat ritningen. En egenskap för konfigurationsnoden innehåller egenskapsnamnet för den planeringssida som lagrar informationen. Vid körning hämtar `LiveAction` egenskapsnamnet från konfigurationen och hämtar sedan egenskapsvärdet.

Parametern för metoden ` [LiveActionFactory](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html).createAction` är ett `Resource`-objekt. Detta `Resource`-objekt representerar `cq:LiveSyncAction`-noden för den här live-åtgärden i rollout-konfigurationen; se [Skapa en utrullningskonfiguration](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration). När du använder en konfigurationsnod bör du som vanligt anpassa den till ett `ValueMap`-objekt:

```java
public LiveAction createAction(Resource resource) throws WCMException {
        ValueMap config;
        if (resource == null || resource.adaptTo(ValueMap.class) == null) {
            config = new ValueMapDecorator(Collections.<String, Object>emptyMap());
        } else {
            config = resource.adaptTo(ValueMap.class);
        }
        return new MyLiveAction(config, this);
}
```

### Åtkomst till målnoder, källnoder och LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

Följande objekt anges som parametrar för metoden `execute` för objektet `LiveAction`:

* Ett [ `Resource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html)-objekt som representerar källan för Live-kopian.
* Ett `Resource`-objekt som representerar målet för Live-kopian.
* Objektet [ `LiveRelationship`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) för live-kopian.
* Värdet `autoSave` anger om `LiveAction` ska spara ändringar som görs i databasen.

* Återställningsvärdet anger återställningsläget för utrullning.

Från de här objekten kan du hämta all information om `LiveCopy`. Du kan också använda objekten `Resource` för att hämta objekten `ResourceResolver`, `Session` och `Node`. De här objekten är användbara för att hantera databasinnehåll:

I den första raden i följande kod är källan `Resource`-objektet för källsidan:

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>Argumenten `Resource` kan vara `null` eller `Resources` objekt som inte anpassar sig till `Node`-objekt, till exempel [ `NonExistingResource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/NonExistingResource.html)-objekt.

## Skapar en ny utrullningskonfiguration {#creating-a-new-rollout-configuration}

Skapa en utrullningskonfiguration när de installerade utrullningskonfigurationerna inte uppfyller dina programkrav:

* [Skapa utrullningskonfigurationen](#create-the-rollout-configuration).
* [Lägg till synkroniseringsåtgärder i utrullningskonfigurationen](#add-synchronization-actions-to-the-rollout-configuration).

Den nya utrullningskonfigurationen är sedan tillgänglig för dig när du ställer in utrullningskonfigurationer på en ritnings- eller Live copy-sida.

>[!NOTE]
>
>Se även de [bästa sätten att anpassa rollouts](/help/sites-administering/msm-best-practices.md#customizing-rollouts).

### Skapa utrullningskonfigurationen {#create-the-rollout-configuration}

Så här skapar du en ny utrullningskonfiguration:

1. Öppna CRXDE Lite, till exempel:
   [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Navigera till :
   `/apps/msm/<your-project>/rolloutconfigs`

   >[!NOTE]
   >Det här är projektets anpassade version av:
   >`/libs/msm/wcm/rolloutconfigs`
   >Måste skapas om detta är din första konfiguration.

   >[!NOTE]
   >
   >Du får inte ändra något i sökvägen /libs.
   >Detta beror på att innehållet i /libs skrivs över nästa gång du uppgraderar din instans (och kan mycket väl skrivas över när du använder en snabbkorrigering eller ett funktionspaket).
   >Den rekommenderade metoden för konfiguration och andra ändringar är:
   >* Återskapa önskat objekt (t.ex. som det finns i /libs) under /apps
   >* Gör ändringar i /apps


1. Under denna **Skapa** en nod med följande egenskaper:

   * **Namn**: Nodnamnet för utrullningskonfigurationen. md#installed-synchronization-actions), till exempel `contentCopy` eller `workflow`.
   * **Typ**:  `cq:RolloutConfig`

1. Lägg till följande egenskaper i den här noden:
   * **Namn**:  `jcr:title`

      **Typ**:  `String`
      **Värde**: En identifierande titel som visas i användargränssnittet.
   * **Namn**:  `jcr:description`

      **Typ**:  `String`
      **Värde**: En valfri beskrivning.
   * **Namn**:  `cq:trigger`

      **Typ**:  `String`
      **Värde**: Den  [utrullningsutlösare ](/help/sites-administering/msm-sync.md#rollout-triggers) som ska användas. Välj  från:
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. Klicka på **Spara alla**.

### Lägg till synkroniseringsåtgärder i utrullningskonfigurationen {#add-synchronization-actions-to-the-rollout-configuration}

Konfigurationer för utrullning lagras under [rollout configuration node](#create-the-rollout-configuration) som du har skapat under `/apps/msm/<your-project>/rolloutconfigs`-noden.

Lägg till underordnade noder av typen `cq:LiveSyncAction` för att lägga till synkroniseringsåtgärder i rollout-konfigurationen. Ordningen på synkroniseringsåtgärdsnoderna avgör i vilken ordning åtgärderna utförs.

1. I CRXDE Lite väljer du fortfarande noden [Rollout Configuration](#create-the-rollout-configuration).

   Till exempel:
   `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`

1. **Skapa en** nod med följande nodegenskaper:

   * **Namn**: Synkroniseringsåtgärdens nodnamn.
Namnet måste vara detsamma som **Åtgärdsnamnet** i tabellen under [Synkroniseringsåtgärder](/help/sites-administering/msm-sync.md#installed-synchronization-actions), till exempel `contentCopy` eller `workflow`.
   * **Typ**:  `cq:LiveSyncAction`

1. Lägg till och konfigurera så många noder för synkroniseringsåtgärder som du behöver. Ordna om åtgärdsnoderna så att ordningen matchar den ordning i vilken du vill att de ska visas. Den översta åtgärdsnoden inträffar först.

## Skapa och använda en enkel LiveActionFactory-klass {#creating-and-using-a-simple-liveactionfactory-class}

Följ anvisningarna i det här avsnittet för att utveckla en `LiveActionFactory` och använda den i en utrullningskonfiguration. I procedurerna används Maven och Eclipse för att utveckla och distribuera `LiveActionFactory`:

1. [Skapa maven-](#create-the-maven-project) projektet och importera det till Eclipse.
1. [Lägg till ](#add-dependencies-to-the-pom-file) beroenden i POM-filen.
1. [Implementera  `LiveActionFactory` ](#implement-liveactionfactory) gränssnittet och distribuera OSGi-paketet.
1. [Skapa utrullningskonfigurationen](#create-the-example-rollout-configuration).
1. [Skapa en live-kopia](#create-the-live-copy).

Maven-projektet och Java-klassens källkod är tillgängliga i det offentliga Git-arkivet.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Open ExperienceManager-java-msmrollout-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

### Skapa Maven Project {#create-the-maven-project}

Följande procedur kräver att du har lagt till adobe-public-profilen i Maven-inställningsfilen.

* Mer information om profilen adobe-public finns i [Hämta innehållspaketet Maven Plugin](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* Mer information om inställningsfilen för Maven finns i [Inställningsreferens](https://maven.apache.org/settings.html).

1. Öppna en terminal- eller kommandoradssession och ändra katalogen så att den pekar på den plats där projektet ska skapas.
1. Ange följande kommando:

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. Ange följande värden vid en interaktiv fråga:

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`:  `MyLiveActionFactory`
   * `version`:  `1.0-SNAPSHOT`
   * `package`:  `MyPackage`
   * `appsFolderName`:  `myapp`
   * `artifactName`:  `MyLiveActionFactory package`
   * `packageGroup`:  `myPackages`

1. Starta Eclipse och [importera Maven-projektet](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse).

### Lägg till beroenden i POM-filen {#add-dependencies-to-the-pom-file}

Lägg till beroenden så att Eclipse-kompilatorn kan referera till klasserna som används i `LiveActionFactory`-koden.

1. Öppna filen i Eclipse Project Explorer:

   `MyLiveActionFactory/pom.xml`

1. Klicka på fliken `pom.xml` i redigeraren och leta reda på avsnittet `project/dependencyManagement/dependencies`.
1. Lägg till följande XML i `dependencyManagement`-elementet och spara sedan filen.

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
     <version>5.6.2</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
     <version>2.4.3-R1488084</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
     <version>5.6.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
     <version>2.0.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
     <version>2.0.0</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
   ```

1. Öppna POM-filen för paketet från **Project Explorer** `MyLiveActionFactory-bundle/pom.xml`.
1. Klicka på fliken `pom.xml` i redigeraren och leta upp avsnittet Projekt/beroenden. Lägg till följande XML i beroendeelementet och spara sedan filen:

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
   ```

### Implementera LiveActionFactory {#implement-liveactionfactory}

Följande `LiveActionFactory`-klass implementerar en `LiveAction` som loggar meddelanden om käll- och målsidorna och kopierar egenskapen `cq:lastModifiedBy` från källnoden till målnoden. Den aktiva åtgärdens namn är `exampleLiveAction`.

1. Högerklicka på `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm`-paketet i Eclipse Project Explorer och klicka på **New** > **Class**. För **Namn** anger du `ExampleLiveActionFactory` och klickar sedan på **Slutför**.
1. Öppna filen `ExampleLiveActionFactory.java`, ersätt innehållet med följande kod och spara filen.

   ```java
   package com.adobe.example.msm;
   
   import java.util.Collections;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.resource.ResourceResolver;
   import org.apache.sling.api.resource.ValueMap;
   import org.apache.sling.api.wrappers.ValueMapDecorator;
   import org.apache.sling.commons.json.io.JSONWriter;
   import org.apache.sling.commons.json.JSONException;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   
   import com.day.cq.wcm.msm.api.ActionConfig;
   import com.day.cq.wcm.msm.api.LiveAction;
   import com.day.cq.wcm.msm.api.LiveActionFactory;
   import com.day.cq.wcm.msm.api.LiveRelationship;
   import com.day.cq.wcm.api.WCMException;
   
   @Component(metatype = false)
   @Service
   public class ExampleLiveActionFactory implements LiveActionFactory<LiveAction> {
    @Property(value="exampleLiveAction")
    static final String actionname = LiveActionFactory.LIVE_ACTION_NAME;
   
    public LiveAction createAction(Resource config) {
     ValueMap configs;
     /* Adapt the config resource to a ValueMap */
           if (config == null || config.adaptTo(ValueMap.class) == null) {
               configs = new ValueMapDecorator(Collections.<String, Object>emptyMap());
           } else {
               configs = config.adaptTo(ValueMap.class);
           }
   
     return new ExampleLiveAction(actionname, configs);
    }
    public String createsAction() {
     return actionname;
    }
    /************* LiveAction ****************/
    private static class ExampleLiveAction implements LiveAction {
     private String name;
     private ValueMap configs;
     private static final Logger log = LoggerFactory.getLogger(ExampleLiveAction.class);
   
     public ExampleLiveAction(String nm, ValueMap config){
      name = nm;
      configs = config;
     }
   
     public void execute(Resource source, Resource target,
       LiveRelationship liverel, boolean autoSave, boolean isResetRollout)
         throws WCMException {
   
      String lastMod = null;
   
      log.info(" *** Executing ExampleLiveAction *** ");
   
      /* Determine if the LiveAction is configured to copy the cq:lastModifiedBy property */
      if ((Boolean) configs.get("repLastModBy")){
   
       /* get the source's cq:lastModifiedBy property */
       if (source != null && source.adaptTo(Node.class) !=  null){
        ValueMap sourcevm = source.adaptTo(ValueMap.class);
        lastMod = sourcevm.get(com.day.cq.wcm.msm.api.MSMNameConstants.PN_PAGE_LAST_MOD_BY, String.class);
       }
   
       /* set the target node's la-lastModifiedBy property */
       Session session = null;
       if (target != null && target.adaptTo(Node.class) !=  null){
        ResourceResolver resolver = target.getResourceResolver();
        session = resolver.adaptTo(javax.jcr.Session.class);
        Node targetNode;
        try{
         targetNode=target.adaptTo(javax.jcr.Node.class);
         targetNode.setProperty("la-lastModifiedBy", lastMod);
         log.info(" *** Target node lastModifiedBy property updated: {} ***",lastMod);
        }catch(Exception e){
         log.error(e.getMessage());
        }
       }
       if(autoSave){
        try {
         session.save();
        } catch (Exception e) {
         try {
          session.refresh(true);
         } catch (RepositoryException e1) {
          e1.printStackTrace();
         }
         e.printStackTrace();
        }
       }
      }
     }
     public String getName() {
      return name;
     }
   
     /************* Deprecated *************/
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3) throws WCMException {
     }
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3, boolean arg4)
         throws WCMException {
     }
     @Deprecated
     public String getParameterName() {
      return null;
     }
     @Deprecated
     public String[] getPropertiesNames() {
      return null;
     }
     @Deprecated
     public int getRank() {
      return 0;
     }
     @Deprecated
     public String getTitle() {
      return null;
     }
     @Deprecated
     public void write(JSONWriter arg0) throws JSONException {
     }
    }
   }
   ```

1. Använd terminalen eller kommandosessionen för att ändra katalogen till katalogen `MyLiveActionFactory` (Maven project directory). Ange sedan följande kommando:

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   AEM `error.log`-filen ska ange att paketet har startats.

   Exempel: [https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs).

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### Skapa exempelkonfigurationen {#create-the-example-rollout-configuration}

Skapa den MSM-utrullningskonfiguration som använder `LiveActionFactory` som du skapade:

1. Skapa och konfigurera en [utrullningskonfiguration med standardproceduren](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) och med egenskaperna:

   * **Titel**: Exempelkonfiguration
   * **Namn**: examplerolloutconfig
   * **cq:trigger**:  `publish`

### Lägg till Live-åtgärden i exempelkonfigurationen {#add-the-live-action-to-the-example-rollout-configuration}

Konfigurera den utrullningskonfiguration som du skapade i föregående procedur så att den använder klassen `ExampleLiveActionFactory`.

1. Öppna CRXDE Lite, till exempel [https://localhost:4502/crx/de](https://localhost:4502/crx/de).
1. Skapa följande nod under `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **Namn**:  `exampleLiveAction`
   * **Typ**:  `cq:LiveSyncAction`

1. Klicka på **Spara alla**.
1. Markera noden `exampleLiveAction` och lägg till följande egenskap:

   * **Namn**:  `repLastModBy`
   * **Typ**:  `Boolean`
   * **Värde**:  `true`

   Den här egenskapen anger för klassen `ExampleLiveAction` att egenskapen `cq:LastModifiedBy` ska replikeras från källan till målnoden.

1. Klicka på **Spara alla**.

### Skapa Live-kopian {#create-the-live-copy}

[Skapa en live-](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) kopia av engelska/produkter-grenen i referenswebbplatsen för Vi.Retail med din rollout-konfiguration:

* **Källa**:  `/content/we-retail/language-masters/en/products`

* **Konfiguration**: Exempelkonfiguration

Aktivera sidan **Produkter** (engelska) i källgrenen och observera de loggmeddelanden som genereras av klassen `LiveAction`:

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

<!--
## Removing the Chapters Step in the Create Site Wizard {#removing-the-chapters-step-in-the-create-site-wizard}

In some cases, the **Chapters** selection is not required in the create site wizard (only the **Languages** selection is required). To remove this step in the default We.Retail English blueprint:

1. In CRX Explorer, remove the node:
   `/etc/blueprints/weretail-english/jcr:content/dialog/items/tabs/items/tab_chap`.

1. Navigate to `/libs/wcm/msm/templates/blueprint/defaults/livecopy_tab/items` and create a new node:

    1. **Name** = `chapters`; **Type** = `cq:Widget`.

1. Add following properties to the new node:

    1. **Name** = `name`; **Type** = `String`; **Value** = `msm:chapterPages`

    1. **Name** = `value`; **Type** = `String`; **Value** = `all`

    1. **Name** = `xtype`; **Type** = `String`; **Value** = `hidden`
-->

## Ändra språknamn och standardländer {#changing-language-names-and-default-countries}

AEM använder en standarduppsättning med språk- och landskoder.

* Standardspråkkoden är den gemena, tvåbokstavskod som definieras av ISO-639-1.
* Standardlandskoden är den gemena eller versala tvåbokstavskoden enligt ISO 3166.

MSM använder en lagrad lista med språk- och landskoder för att fastställa namnet på landet som är associerat med namnet på språkversionen av sidan. Du kan ändra följande aspekter av listan om det behövs:

* Språktitlar
* Landsnamn
* Standardländer för språk (för koder som t.ex. `en`, `de`)

Språklistan lagras under noden `/libs/wcm/core/resources/languages`. Varje underordnad nod representerar ett språk eller ett språkområde:

* Nodnamnet är språkkoden (till exempel `en` eller `de`) eller språkkoden (till exempel `en_us` eller `de_ch`).

* Egenskapen `language` för noden lagrar det fullständiga namnet på språket för koden.
* Egenskapen `country` för noden lagrar det fullständiga namnet på landet för koden.
* När nodnamnet bara består av en språkkod (till exempel `en`) är egenskapen country `*` och ytterligare `defaultCountry`-egenskap lagrar koden för det språkområde som anger vilket land som ska användas.

![chlimage_1-76](assets/chlimage_1-76.png)

Så här ändrar du språk:

1. Öppna CRXDE Lite i webbläsaren; till exempel [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. Markera mappen `/apps` och klicka på **Skapa** och **Skapa mapp.**

   Ge den nya mappen namnet `wcm`.

1. Upprepa föregående steg för att skapa mappträdet `/apps/wcm/core`. Skapa en nod av typen `sling:Folder` i `core` med namnet `resources`. <!-- ![chlimage_1-77](assets/chlimage_1-77.png) -->

1. Högerklicka på noden `/libs/wcm/core/resources/languages` och klicka på **Kopiera**.
1. Högerklicka på mappen `/apps/wcm/core/resources` och klicka på **Klistra in**. Ändra de underordnade noderna efter behov.
1. Klicka på **Spara alla**.
1. Klicka på **Verktyg**, **Åtgärder** och **Webbkonsol**. Från den här konsolen klickar du på **OSGi** och sedan på **Konfiguration**.
1. Leta reda på och klicka på **Day CQ WCM Language Manager** och ändra värdet för **Språklista** till `/apps/wcm/core/resources/languages`. Klicka sedan på **Spara**.

   ![chlimage_1-78](assets/chlimage_1-78.png)

## Konfigurera MSM-lås på sidegenskaper (Touch-aktiverat gränssnitt) {#configuring-msm-locks-on-page-properties-touch-enabled-ui}

När du skapar en anpassad sidegenskap kan du behöva fundera på om den nya egenskapen ska kunna rullas ut till alla live-kopior.

Om till exempel två nya sidegenskaper läggs till:

* E-postadress:

   * Den här egendomen behöver inte rullas ut eftersom den kommer att vara olika i varje land (eller varumärke osv.).

* Visuell huvudstil:

   * Projektkravet är att denna egenskap ska rullas ut eftersom den (vanligtvis) är gemensam för alla länder (eller varumärken, osv.).

Då måste du se till att:

* E-postadress:

   * är utesluten från de utrullade egenskaperna, se [Exkludera egenskaper och nodtyper från synkronisering](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization).

* Visuell huvudstil:

   * Se till att du inte får redigera den här egenskapen i det beröringsaktiverade användargränssnittet om inte arvet avbryts, och att du sedan kan återinstallera arvet; Detta styrs genom att klicka på kedjelänkarna/brutna kedjor som växlar för att ange anslutningsstatus.

Anger om en sidegenskap ska rullas ut och därför styrs arvet av egenskapen dialog, under förutsättning att arvet avbryts/återställs vid redigering:

* `cq-msm-lockable`

   * kan användas för objekt i en dialogruta med pekfunktioner
   * skapar kedjelänkssymbolen i dialogrutan
   * tillåter bara redigering om arv avbryts (kedjelänken bryts)
   * gäller endast den första underordnade nivån för resursen
   * **Typ**:  `String`

   * **Värde**: har namnet på den aktuella egendomen (och är jämförbart med värdet på egendomen  `name`; se
      `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

När `cq-msm-lockable` har definierats interagerar en brytning/stängning av kedjan med MSM på följande sätt:

* om värdet för `cq-msm-lockable` är:

   * **Relativ**  (t.ex.  `myProperty` eller  `./myProperty`)

      * den lägger till och tar bort egenskapen från `cq:propertyInheritanceCancelled`.
   * **Absolut** (t.ex.  `/image`)

      * Om du bryter kedjan avbryts arvet genom att blanda `cq:LiveSyncCancelled` till `./image` och ställa in `cq:isCancelledForChildren` till `true`.

      * Om du stänger kedjan återställs arvet.


>[!NOTE]
>
>`cq-msm-lockable` används på den första underordnade nivån för resursen som ska redigeras och den fungerar inte på något djupare nivåöverordnat objekt, oavsett om värdet är definierat som absolut eller relativ.

>[!NOTE]
>
>När du återaktiverar arv synkroniseras inte egenskapen för live-kopieringssidan automatiskt med egenskapen source. Du kan begära en synkronisering manuellt om det behövs.
