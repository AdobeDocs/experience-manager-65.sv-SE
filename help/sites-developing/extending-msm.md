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
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Utöka Multi Site Manager{#extending-the-multi-site-manager}

På den här sidan kan du utöka funktionerna i Multi Site Manager:

* Läs mer om huvudmedlemmarna i MSM Java API.
* Skapa en ny synkroniseringsåtgärd som kan användas i en utrullningskonfiguration.
* Ta bort steget &quot;Kapitel&quot; i guiden Skapa plats.
* Ändra standardspråk och landskoder.

>[!NOTE]
>
>Den här sidan ska läsas tillsammans med [Återanvända innehåll: Multi Site Manager](/help/sites-administering/msm.md).

>[!CAUTION]
>
>Multi Site Manager och dess API används vid utvecklingen av en webbplats, så de är bara avsedda att användas i en författarmiljö.

## Översikt över Java API {#overview-of-the-java-api}

Hantering av flera platser består av följande paket:

* [com.day.cq.wcm.msm.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.Commons](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

De huvudsakliga MSM API-objekten interagerar på följande sätt (se även [Använda](/help/sites-administering/msm.md#terms-used)termer):

![chlimage_1-73](assets/chlimage_1-73.png)

* **`Blueprint`**

   A `Blueprint` (som i [designkonfigurationen](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations)) anger de sidor från vilka en live-kopia kan ärva innehåll.

   ![chlimage_1-74](assets/chlimage_1-74.png)

   * Det är valfritt att använda en ritningskonfiguration ( `Blueprint`), men:

      * Tillåter författaren att använda alternativet **Rollout** på källan (för att (explicit) överföra ändringar till live-kopior som ärver från den här källan).
      * Låter författaren använda **Skapa plats**, på så sätt kan användaren enkelt välja språk och konfigurera strukturen för live-kopian.
      * Definierar standardkonfigurationen för utrullning för alla resulterande live-kopior.

* **`LiveRelationship`** Anger `LiveRelationship` anslutningen (relationen) mellan en resurs i livekopiegrenen och dess motsvarande källa/ritresurs.

   * Relationerna används vid arv och utrullning.
   * `LiveRelationship` -objekt ger åtkomst (referenser) till rollout-konfigurationer ( `RolloutConfig`), `LiveCopy`och `LiveStatus` objekt som är relaterade till relationen.

   * En live-kopia skapas t.ex. i `/content/copy/us` från källan/ritningen `/content/we-retail/language-masters`. Resurserna `/content/we.retail/language-masters/en/jcr:content` och `/content/copy/us/en/jcr:content` utgör en relation.

* **`LiveCopy`** `LiveCopy` innehåller konfigurationsinformation för relationerna ( `LiveRelationship`) mellan live-kopieringsresurserna och deras käll-/ritningsresurser.

   * Använd `LiveCopy` klassen för att komma åt sidans sökväg, sökvägen till käll-/ritningssidan, rollout-konfigurationerna och om underordnade sidor också ska inkluderas i `LiveCopy`.

   * En `LiveCopy` nod skapas varje gång **Skapa plats** eller **Skapa Live-kopia** används.

* **`LiveStatus`**

   `LiveStatus` -objekt ger åtkomst till körningsstatus för en `LiveRelationship`. Används för att fråga synkroniseringsstatusen för en live-kopia.

* **`LiveAction`**

   A `LiveAction` är en åtgärd som utförs på varje resurs som ingår i utrullningen.

   * LiveActions genereras endast av RolloutConfigs.

* **`LiveActionFactory`**

   Skapar `LiveAction` objekt utifrån en `LiveAction` konfiguration. Konfigurationer lagras som resurser i databasen.

* **`RolloutConfig`** Den `RolloutConfig` innehåller en lista med `LiveActions`som ska användas när den aktiveras. Det `LiveCopy` ärver `RolloutConfig` och resultatet finns i `LiveRelationship`.

   * När du konfigurerar en live-kopia för första gången används också en RolloutConfig (som utlöser LiveActions).

### Skapa en ny synkroniseringsåtgärd {#creating-a-new-synchronization-action}

Skapa anpassade synkroniseringsåtgärder som du kan använda med dina utrullningskonfigurationer. Skapa en synkroniseringsåtgärd när de [installerade åtgärderna](/help/sites-administering/msm-sync.md#installed-synchronization-actions) inte uppfyller dina specifika programkrav. Skapa då två klasser:

* En implementering av det [`com.day.cq.wcm.msm.api.LiveAction`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) gränssnitt som utför åtgärden.
* En OSGI-komponent som implementerar [ gränssnittet och skapar instanser av din `com.day.cq.wcm.msm.api.LiveActionFactory`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) `LiveAction` klass.

I `LiveActionFactory` skapas instanser av `LiveAction` klassen för en viss konfiguration:

* `LiveAction` -klasser innehåller följande metoder:

   * `getName`: Returnerar namnet på åtgärden Namnet används för att referera till åtgärden, till exempel i utrullningskonfigurationer.
   * `execute`: Utför åtgärderna.

* `LiveActionFactory` -klasserna innehåller följande medlemmar:

   * `LIVE_ACTION_NAME`: Ett fält som innehåller namnet på det associerade fältet `LiveAction`. Namnet måste sammanfalla med värdet som returneras av `getName` metoden för `LiveAction` klassen.

   * `createAction`: Skapar en instans av `LiveAction`. Den valfria `Resource` parametern kan användas för att tillhandahålla konfigurationsinformation.

   * `createsAction`: Returnerar namnet på associerat `LiveAction`objekt.

### Åtkomst till konfigurationsnoden för LiveAction {#accessing-the-liveaction-configuration-node}

Använd konfigurationsnoden i databasen för att lagra information som påverkar `LiveAction` `LiveAction` instansens körningsbeteende. Noden i databasen som lagrar `LiveAction` konfigurationen är tillgänglig för `LiveActionFactory` objektet vid körning. Därför kan du lägga till egenskaper i konfigurationsnoden och använda dem i din `LiveActionFactory` implementering efter behov.

Ett exempel: en användare `LiveAction` måste lagra namnet på den som har skapat ritningen. En egenskap för konfigurationsnoden innehåller egenskapsnamnet för den planeringssida som lagrar informationen. Vid körning hämtar egenskapsnamnet från konfigurationen och hämtar sedan egenskapsvärdet. `LiveAction`

Parametern för ` [LiveActionFactory](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html).createAction` metoden är ett `Resource` objekt. Detta `Resource` objekt representerar `cq:LiveSyncAction` noden för den här live-åtgärden i rollout-konfigurationen. se [Skapa en utrullningskonfiguration](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration). När du använder en konfigurationsnod bör du som vanligt anpassa den till ett `ValueMap` objekt:

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

Följande objekt anges som parametrar för `execute` metoden för `LiveAction` objektet:

* Ett [ objekt `Resource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) som representerar källan till Live Copy.
* Ett `Resource` objekt som representerar målet för Live Copy.
* Objektet [ för `LiveRelationship`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) live-kopian.
* Värdet anger `autoSave` om dina ändringar `LiveAction` ska sparas i databasen.

* Återställningsvärdet anger återställningsläget för utrullning.

Från de här objekten kan du hämta all information om `LiveCopy`. Du kan också använda `Resource` objekten för att hämta `ResourceResolver`, `Session`och `Node` objekt. De här objekten är användbara för att hantera databasinnehåll:

I den första raden i följande kod är källan källsidans `Resource` objekt:

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>Argumenten kan vara `Resource` eller `null` objekt som inte anpassar sig till `Resources` objekt, t.ex. `Node`[ `NonExistingResource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/NonExistingResource.html) objekt.

### Skapa en ny utrullningskonfiguration {#creating-a-new-rollout-configuration}

Skapa en utrullningskonfiguration när de installerade utrullningskonfigurationerna inte uppfyller dina programkrav:

* [Skapa utrullningskonfigurationen](#create-the-rollout-configuration).
* [Lägg till synkroniseringsåtgärder i utrullningskonfigurationen](#add-synchronization-actions-to-the-rollout-configuration).

Den nya utrullningskonfigurationen är sedan tillgänglig för dig när du ställer in utrullningskonfigurationer på en ritnings- eller Live copy-sida.

>[!NOTE]
>
>Se även de [bästa sätten att anpassa rollouts](/help/sites-administering/msm-best-practices.md#customizing-rollouts).

#### Skapa utrullningskonfiguration {#create-the-rollout-configuration}

1. Öppna **verktygskonsolen** i det klassiska användargränssnittet. till exempel [https://localhost:4502/miscadmin#/etc](https://localhost:4502/miscadmin#/etc)

   >[!NOTE]
   >
   >I det pekaktiverade standardgränssnittet kan du navigera till den klassiska UI-verktygskonsolen med hjälp av **verktygen**, **åtgärderna** och sedan **Konfiguration**.

1. I mappträdet väljer du mappen **Verktyg**, **MSM** och **utrullningskonfigurationer** .
1. Klicka på **Ny** och sedan på **Ny sida** för att definiera egenskaperna för utrullningskonfiguration:

   * **Titel**: Titeln på utrullningskonfigurationen, till exempel Min utrullningskonfiguration
   * **Namn**: Namnet på noden som lagrar egenskapsvärden, till exempel myrolloutconfig
   * Välj **RolloutConfig-mall**.

1. Klicka på **Skapa**.
1. Dubbelklicka på den utrullningskonfiguration som du skapade för att öppna den för ytterligare konfiguration.
1. Click **Edit**.
1. I dialogrutan **Utbyteskonfiguration** väljer du **[Synkroniseringsutlösare](/help/sites-administering/msm-sync.md#rollout-triggers)**för att definiera åtgärden som orsakar utrullningen.
1. Spara ändringarna genom att klicka på **OK** .

#### Lägg till synkroniseringsåtgärder i utrullningskonfigurationen {#add-synchronization-actions-to-the-rollout-configuration}

Utrullningskonfigurationer lagras under `/etc/msm/rolloutconfigs` noden. Lägg till underordnade noder av typen `cq:LiveSyncAction` för att lägga till synkroniseringsåtgärder i rollout-konfigurationen. Ordningen på synkroniseringsåtgärdsnoderna avgör i vilken ordning åtgärderna utförs.

1. Open CRXDE Lite; till exempel [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. Markera `jcr:content` noden under din rollout-konfigurationsnod.

   För utrullningskonfigurationen med egenskapen **Namn** i `myrolloutconfig`väljer du noden:

   `/etc/msm/rolloutconfigs/myrolloutconfig/jcr:content`

1. Klicka på **Skapa** och sedan **Skapa nod**. Konfigurera sedan följande nodegenskaper och klicka på **OK**:

   * **Namn**: Synkroniseringsåtgärdens nodnamn. Namnet måste vara detsamma som **åtgärdsnamnet** i tabellen under [Synkroniseringsåtgärder](/help/sites-administering/msm-sync.md#installed-synchronization-actions), till exempel `contentCopy` eller `workflow`.

   * **Typ**: `cq:LiveSyncAction`

1. Markera åtgärdsnoden som nyss skapades och lägg till följande egenskap i noden:

   * **Namn**: Åtgärdens egenskapsnamn. Namnet måste vara detsamma som **egenskapsnamnet** i tabellen under [Synkroniseringsåtgärder](/help/sites-administering/msm-sync.md#installed-synchronization-actions), till exempel `enabled`.

   * **Typ**:Sträng

   * **Värde**: åtgärdens egenskapsvärde. Giltiga värden finns i kolumnen **Egenskaper** i [Synkroniseringsåtgärder](/help/sites-administering/msm-sync.md#installed-synchronization-actions), till exempel `true`.

1. Lägg till och konfigurera så många noder för synkroniseringsåtgärder som du behöver. Ordna om åtgärdsnoderna så att ordningen matchar den ordning i vilken du vill att de ska visas. Den översta åtgärdsnoden inträffar först.
1. Klicka på **Spara alla**.

### Skapa och använda en enkel LiveActionFactory-klass {#creating-and-using-a-simple-liveactionfactory-class}

Följ anvisningarna i det här avsnittet för att utveckla ett `LiveActionFactory` program och använda det i en utrullningskonfiguration. Processerna använder Maven och Eclipse för att utveckla och driftsätta `LiveActionFactory`:

1. [Skapa maven-projektet](#create-the-maven-project) och importera det till Eclipse.
1. [Lägg till beroenden](#add-dependencies-to-the-pom-file) i POM-filen.
1. [Implementera `LiveActionFactory` gränssnittet](#implement-liveactionfactory) och driftsätt OSGi-paketet.
1. [Skapa utrullningskonfigurationen](#create-the-example-rollout-configuration).
1. [Skapa en live-kopia](#create-the-live-copy).

Maven-projektet och Java-klassens källkod är tillgängliga i det offentliga Git-arkivet.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Open ExperienceManager-java-msmrollout-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

#### Skapa projektet Maven {#create-the-maven-project}

Följande procedur kräver att du har lagt till adobe-public-profilen i Maven-inställningsfilen.

* Mer information om adobe-public-profilen finns i [Hämta innehållspaketet Maven Plugin](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* Mer information om inställningsfilen för Maven finns i Maven [Settings Reference](https://maven.apache.org/settings.html).

1. Öppna en terminal- eller kommandoradssession och ändra katalogen så att den pekar på den plats där projektet ska skapas.
1. Ange följande kommando:

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. Ange följande värden vid en interaktiv fråga:

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`: `MyLiveActionFactory`
   * `version`: `1.0-SNAPSHOT`
   * `package`: `MyPackage`
   * `appsFolderName`: `myapp`
   * `artifactName`: `MyLiveActionFactory package`
   * `packageGroup`: `myPackages`

1. Starta Eclipse och [importera projektet](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse)Maven.

#### Lägg till beroenden till POM-filen {#add-dependencies-to-the-pom-file}

Lägg till beroenden så att Eclipse-kompilatorn kan referera till de klasser som används i `LiveActionFactory` koden.

1. Öppna filen i Eclipse Project Explorer:

   `MyLiveActionFactory/pom.xml`

1. Klicka på `pom.xml` fliken i redigeraren och leta reda på `project/dependencyManagement/dependencies` avsnittet.
1. Lägg till följande XML i `dependencyManagement` elementet och spara sedan filen.

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

1. Öppna POM-filen för paketet från **Project Explorer** på `MyLiveActionFactory-bundle/pom.xml`.
1. I redigeraren klickar du på `pom.xml` fliken och letar upp avsnittet Projekt/beroenden. Lägg till följande XML i beroendeelementet och spara sedan filen:

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

#### Implementera LiveActionFactory {#implement-liveactionfactory}

Följande `LiveActionFactory` klass implementerar en `LiveAction` som loggar meddelanden om käll- och målsidorna och kopierar `cq:lastModifiedBy` egenskapen från källnoden till målnoden. Den aktiva åtgärdens namn är `exampleLiveAction`.

1. Högerklicka på paketet i Eclipse Project Explorer och klicka på `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` Nytt **>** Klass ****. Ange **namnet**`ExampleLiveActionFactory` och klicka sedan på **Slutför**.
1. Öppna `ExampleLiveActionFactory.java` filen, ersätt innehållet med följande kod och spara filen.

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
        lastMod = sourcevm.get(com.day.cq.wcm.api.NameConstants.PN_PAGE_LAST_MOD_BY, String.class);
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

1. Använd terminalen eller kommandosessionen för att ändra katalogen till `MyLiveActionFactory` katalogen (Maven-projektkatalogen). Ange sedan följande kommando:

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   AEM- `error.log` filen ska ange att paketet har startats.

   Till exempel [https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs).

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

#### Skapa exempelkonfigurationen {#create-the-example-rollout-configuration}

Skapa den MSM-introduktionskonfiguration som använder `LiveActionFactory` den som du skapade:

1. Skapa och konfigurera en [utrullningskonfiguration med standardproceduren](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) - och använd egenskaperna:

   1. Skapa:

      1. **Titel**: Exempelkonfiguration
      1. **Namn**: examplerolloutconfig
      1. Använda mallen **** RolloutConfig.
   1. Redigera:

      1. **Synkroniseringsutlösare**: Vid aktivering


#### Lägg till Live-åtgärden i exempelkonfigurationen för utrullning {#add-the-live-action-to-the-example-rollout-configuration}

Konfigurera den utrullningskonfiguration som du skapade i föregående procedur så att den använder `ExampleLiveActionFactory` klassen.

1. Open CRXDE Lite; till exempel [https://localhost:4502/crx/de](https://localhost:4502/crx/de).
1. Skapa följande nod under `/etc/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **Namn**: `exampleLiveAction`
   * **Typ**: `cq:LiveSyncAction`
   ![chlimage_1-75](assets/chlimage_1-75.png)

1. Klicka på **Spara alla**.
1. Markera `exampleLiveAction` noden och lägg till följande egenskap:

   * **Namn**: `repLastModBy`
   * **Typ**: `Boolean`
   * **Värde**: `true`
   Den här egenskapen anger för `ExampleLiveAction` klassen att `cq:LastModifiedBy` egenskapen ska replikeras från källan till målnoden.

1. Klicka på **Spara alla**.

#### Skapa Live Copy {#create-the-live-copy}

[Skapa en live-kopia](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) av engelska/produkter-grenen av referenswebbplatsen för Vi.Retail med din rollout-konfiguration:

* **Källa**: `/content/we-retail/language-masters/en/products`

* **Konfiguration**: Exempelkonfiguration

Aktivera sidan **Produkter** (engelska) i källgrenen och observera de loggmeddelanden som `LiveAction` klassen genererar:

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

### Ta bort kapitelsteget i guiden Skapa plats {#removing-the-chapters-step-in-the-create-site-wizard}

I vissa fall krävs inte valet av **kapitel** i guiden Skapa plats (endast valet **Språk** krävs). Så här tar du bort det här steget i standardversionen av Web.Retail English:

1. Ta bort noden i CRX Explorer:
   `/etc/blueprints/weretail-english/jcr:content/dialog/items/tabs/items/tab_chap`.

1. Navigera till `/libs/wcm/msm/templates/blueprint/defaults/livecopy_tab/items` och skapa en ny nod:

   1. **Namn** = `chapters`; **Typ** = `cq:Widget`.

1. Lägg till följande egenskaper i den nya noden:

   1. **Namn** = `name`; **Typ** = `String`; **Värde** = `msm:chapterPages`

   1. **Namn** = `value`; **Typ** = `String`; **Värde** = `all`

   1. **Namn** = `xtype`; **Typ** = `String`; **Värde** = `hidden`

### Ändra språknamn och standardländer {#changing-language-names-and-default-countries}

AEM använder en standarduppsättning med språk- och landskoder.

* Standardspråkkoden är den gemena, tvåbokstavskod som definieras av ISO-639-1.
* Standardlandskoden är den gemena eller versala tvåbokstavskoden enligt ISO 3166.

MSM använder en lagrad lista med språk- och landskoder för att fastställa namnet på landet som är associerat med namnet på språkversionen av sidan. Du kan ändra följande aspekter av listan om det behövs:

* Språktitlar
* Landsnamn
* Standardländer för språk (för koder som `en`t. `de`ex.

Språklistan lagras under `/libs/wcm/core/resources/languages` noden. Varje underordnad nod representerar ett språk eller ett språkområde:

* Nodnamnet är språkkoden (till exempel `en` eller `de`) eller språkkoden (till exempel `en_us` eller `de_ch`).

* Egenskapen `language` för noden lagrar det fullständiga namnet på språket för koden.
* Egenskapen `country` för noden lagrar det fullständiga namnet på landet för koden.
* När nodnamnet bara består av en språkkod (till exempel `en`), är egenskapen country `*`och ytterligare en `defaultCountry` egenskap lagrar koden för det språklandet för att ange vilket land som ska användas.

![chlimage_1-76](assets/chlimage_1-76.png)

Så här ändrar du språk:

1. Öppna CRXDE Lite i webbläsaren; till exempel [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. Markera `/apps` mappen, klicka på **Skapa** och sedan på **Skapa mapp.**

   Ge den nya mappen ett namn `wcm`.

1. Upprepa föregående steg för att skapa `/apps/wcm/core` mappträdet. Skapa en nod av typen `sling:Folder` i `core` anropad `resources`.

   ![chlimage_1-77](assets/chlimage_1-77.png)

1. Högerklicka på `/libs/wcm/core/resources/languages` noden och klicka på **Kopiera**.
1. Högerklicka på `/apps/wcm/core/resources` mappen och klicka på **Klistra in**. Ändra de underordnade noderna efter behov.
1. Klicka på **Spara alla**.
1. Klicka på **Verktyg**, **Åtgärder** och sedan **Webbkonsol**. Från den här konsolen klickar du på **OSGi** och sedan på **Konfiguration**.
1. Leta upp och klicka på **Day CQ WCM Language Manager**, ändra värdet för **Språklista** till `/apps/wcm/core/resources/languages`och klicka sedan på **Spara**.

   ![chlimage_1-78](assets/chlimage_1-78.png)

### Konfigurera MSM-lås på sidegenskaper (pekaktiverat gränssnitt) {#configuring-msm-locks-on-page-properties-touch-enabled-ui}

När du skapar en anpassad sidegenskap kan du behöva fundera på om den nya egenskapen ska kunna rullas ut till alla live-kopior.

Om till exempel två nya sidegenskaper läggs till:

* E-postadress:

   * Den här egendomen behöver inte rullas ut eftersom den kommer att vara olika i varje land (eller varumärke osv.).

* Visuell huvudstil:

   * Projektkravet är att denna egenskap ska rullas ut eftersom den (vanligtvis) är gemensam för alla länder (eller varumärken, osv.).

Då måste du se till att:

* E-postadress:

   * är utesluten från de utrullade egenskaperna, Se [Exkludera egenskaper och nodtyper från synkronisering](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization).

* Visuell huvudstil:

   * Se till att du inte får redigera den här egenskapen i det beröringsaktiverade användargränssnittet om inte arvet avbryts, och att du sedan kan återinstallera arvet; Detta styrs genom att klicka på kedjelänkarna/brutna kedjor som växlar för att ange anslutningsstatus.

Anger om en sidegenskap ska rullas ut och därför styrs arvet av egenskapen dialog, under förutsättning att arvet avbryts/återställs vid redigering:

* `cq-msm-lockable`

   * kan användas för objekt i en dialogruta med pekfunktioner
   * skapar kedjelänkssymbolen i dialogrutan
   * tillåter bara redigering om arv avbryts (kedjelänken bryts)
   * gäller endast den första underordnade nivån för resursen
   * **Typ**: `String`

   * **Värde**: har namnet på den aktuella egendomen (och är jämförbart med värdet på egendomen `name`; se
      `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

När kedjan bryts/stängs kommer den att interagera med MSM på följande sätt: `cq-msm-lockable`

* if the value of `cq-msm-lockable` is:

   * **Relativ** (t.ex. `myProperty` eller `./myProperty`)

      * den lägger till och tar bort egenskapen från `cq:propertyInheritanceCancelled`.
   * **Absolut** (t.ex. `/image`)

      * om du bryter kedjan avbryts arvet genom att du lägger till den `cq:LiveSyncCancelled` mixin i `./image` och anger `cq:isCancelledForChildren` till `true`.

      * Om du stänger kedjan återställs arvet.


>[!NOTE]
>
>`cq-msm-lockable` används på den första underordnade nivån för resursen som ska redigeras och den fungerar inte på något djupare nivåöverordnat objekt, oavsett om värdet är definierat som absolut eller relativ.

>[!NOTE]
>
>När du återaktiverar arv synkroniseras inte egenskapen för live-kopieringssidan automatiskt med egenskapen source. Du kan begära en synkronisering manuellt om det behövs.
