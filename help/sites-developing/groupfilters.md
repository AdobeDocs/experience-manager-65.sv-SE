---
title: Skapa enhetsgruppsfilter
description: Skapa ett enhetsgruppsfilter för att definiera en uppsättning krav för enhetsfunktioner
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/groupfilters
exl-id: 419d2e19-1198-4ab5-9aa0-02ad18fe171d
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 0%

---

# Skapa enhetsgruppsfilter{#creating-device-group-filters}

{{ue-over-mobile}}

Skapa ett enhetsgruppsfilter för att definiera en uppsättning krav för enhetsfunktioner. Skapa så många filter du behöver för att rikta in dig på de grupper av enhetsfunktioner som behövs.

Utforma dina filter så att du kan använda kombinationer av dem för att definiera grupper av funktioner. Vanligtvis finns det överlappande funktioner för olika enhetsgrupper. Därför kan du använda vissa filter med flera enhetsgruppsdefinitioner.

När du har skapat ett filter kan du använda det i [gruppkonfigurationen.](/help/sites-developing/mobile.md#creating-a-device-group)

## Klassen Filter Java™ {#the-filter-java-class}

Ett enhetsgruppsfilter är en OSGi-komponent som implementerar gränssnittet [com.day.cq.wcm.mobile.api.device.DeviceGroupFilter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html). När implementeringsklassen distribueras tillhandahåller den en filtertjänst som är tillgänglig för enhetsgruppskonfigurationer.

Den lösning som beskrivs i denna artikel använder Apache Felix Maven SCR Plugin för att underlätta utvecklingen av komponenten och tjänsten. Därför används anteckningarna `@Component` och `@Service` i Java™-klassen i exemplet. Klassen har följande struktur:

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service
public class myDeviceGroupFilter implements DeviceGroupFilter {

       public String getDescription() {
  return null;
 }

 public String getTitle() {
  return null;
 }

 public boolean matches(DeviceGroup arg0, String arg1, Map arg2) {
  return false;
 }

}
```

Ange kod för följande metoder:

* `getDescription`: Returnerar filterbeskrivningen. Beskrivningen visas i dialogrutan Konfiguration av enhetsgrupp.
* `getTitle`: Returnerar namnet på filtret. Namnet visas när du väljer filter för enhetsgruppen.
* `matches`: Avgör om enheten har de nödvändiga funktionerna.

### Ange filternamn och beskrivning {#providing-the-filter-name-and-description}

Metoderna `getTitle` och `getDescription` returnerar filternamnet och beskrivningen. Följande kod visar den enklaste implementeringen:

```java
public String getDescription() {
    return "An example device group filter";
}

public String getTitle() {
 return "myFilter";
}
```

Det räcker att hårdkoda namn- och beskrivningstexten för en enspråkig redigeringsmiljö. Överväg att externalisera strängarna för flerspråkig användning, eller för att möjliggöra ändring av strängar utan att behöva kompilera om källkoden.

### Utvärdera mot filtervillkor {#evaluating-against-filter-criteria}

Funktionen `matches` returnerar `true` om enhetsfunktionerna uppfyller alla filtervillkor. Utvärdera informationen i metodargumenten för att avgöra om enheten tillhör gruppen. Följande värden anges som argument:

* Ett DeviceGroup-objekt
* Namnet på användaragenten
* Ett Map-objekt som innehåller enhetsfunktionerna. Kartnycklarna är WURFL™-funktionsnamnen och värdena är motsvarande värden från WURFL™-databasen.

Gränssnittet [com.day.cq.wcm.mobile.api.devicespecs.DeviceSpecsConstants](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) innehåller en delmängd av WURFL™-funktionsnamnen i statiska fält. Använd dessa fältkonstanter som nycklar när du hämtar värden från kartan över enhetsfunktioner.

Följande kodexempel avgör till exempel om enheten stöder CSS:

```xml
boolean cssSupport = true;
cssSupport = NumberUtils.toInt(capabilities.get(DeviceSpecsConstants.DSPEC_XHTML_SUPPORT_LEVEL)) > 1;
```

Paketet `org.apache.commons.lang.math` innehåller klassen `NumberUtils`.

>[!NOTE]
>
>Kontrollera att den WURFL™-databas som distribueras till AEM innehåller de funktioner som du använder som filtervillkor. (Se [Enhetsidentifiering](/help/sites-developing/mobile.md#server-side-device-detection).)

### Exempelfilter för skärmstorlek {#example-filter-for-screen-size}

Den exempel på implementering av DeviceGroupFilter som följer avgör om enhetens fysiska storlek uppfyller minimikraven. Det här filtret är avsett att ge gruppen med pekenheter granularitet. Storleken på knapparna i programgränssnittet bör vara densamma oavsett den fysiska skärmstorleken. Storleken på andra objekt, till exempel text, kan variera. Filtret aktiverar det dynamiska urvalet av en viss CSS som styr storleken på gränssnittselementen.

Det här filtret tillämpar storlekskriterier på egenskapsnamnen `physical_screen_height` och `physical_screen_width` WURFL™.

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.commons.lang.math.NumberUtils;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service
@SuppressWarnings("unused")
public class ScreenSizeLarge implements DeviceGroupFilter {
    private int len=400;
    private int wid=200;
    public String getDescription() {

        return "Requires the physical size of the screen to have minimum dimensions " + len + "x" + wid+".";
    }

    public String getTitle() {
        return "Screen Size Large ("+len + "x" + wid+")";
    }

    public boolean matches(DeviceGroup deviceGroup, String userAgent,
            Map<String, String> deviceCapabilities) {

        boolean longEnough=true;
        boolean wideEnough=false;
        int dimension1=NumberUtils.toInt(deviceCapabilities.get("physical_screen_height"));
        int dimension2=NumberUtils.toInt(deviceCapabilities.get("physical_screen_width"));
        if(dimension1>dimension2){
            longEnough=dimension1>=len;
            wideEnough=dimension2>=wid;
        }else{
            longEnough=dimension2>=len;
            wideEnough=dimension1>=wid;
        }

        return longEnough && wideEnough;
    }
}
```

Strängvärdet som returneras av metoden getTitle visas i listrutan för enhetsgruppsegenskaperna.

![filteraddToGroup](assets/filteraddtogroup.png)

De strängvärden som returneras av metoderna getTitle och getDescription finns längst ned på sammanfattningssidan för enhetsgruppen.

![filterdescription](assets/filterdescription.png)

### The Maven POM File {#the-maven-pom-file}

Följande POM-kod är användbar om du använder Maven för att skapa program. POM refererar till flera nödvändiga plugin-program och beroenden.

**Plugin-program:**

* Apache Maven Compiler Plugin: Kompilerar Java™-klasser från källkod.
* Apache Felix Maven Bundle Plugin: Skapar paketet och manifestet
* Apache Felix Maven SCR Plugin: Skapar komponentbeskrivningsfilen och konfigurerar tjänstkomponentens manifesthuvud.

**Beroenden:**

* `cq-wcm-mobile-api-5.5.2.jar`: Tillhandahåller gränssnitten DeviceGroup och DeviceGroupFilter.

* `org.apache.felix.scr.annotations.jar`: Tillhandahåller komponentanteckningar och tjänstanteckningar.

Gränssnitten DeviceGroup och DeviceGroupFilter ingår i Day Communique 5 WCM Mobile API bundle. Felix-anteckningarna ingår i paketet Apache Felix Declarative Services. Du kan hämta den här JAR-filen från den offentliga Adobe-databasen.

Vid redigeringen är 5.5.2 den version av WCM Mobile API-paketet som finns i den senaste versionen av AEM. Använd Adobe Web Console ([https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)) för att kontrollera att det här är den paketversion som distribueras i din miljö.

**POM:** (Din POM använder ett annat groupId och en annan version.)

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
        xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.adobe.example.myapp</groupId>
      <artifactId>devicefilter</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <name>my app device filter</name>
      <url>https://dev.day.com/docs/en/cq/current.html</url>
  <packaging>bundle</packaging>
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>1.5</source>
                <target>1.5</target>
            </configuration>
        </plugin>
        <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-scr-plugin</artifactId>
            <executions>
                  <execution>
                    <id>generate-scr-scrdescriptor</id>
                    <goals>
                          <goal>scr</goal>
                    </goals>
                  </execution>
            </executions>
          </plugin>
        <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-bundle-plugin</artifactId>
            <version>1.4.3</version>
            <extensions>true</extensions>
            <configuration>
                <instructions>
                    <Export-Package>com.adobe.example.myapp.*;version=${project.version}</Export-Package>
                </instructions>
            </configuration>
        </plugin>
    </plugins>
</build>
<dependencies>
     <dependency>
         <groupId>com.day.cq.wcm</groupId>
         <artifactId>cq-wcm-mobile-api</artifactId>
         <version>5.5.2</version>
         <scope>provided</scope>
     </dependency>
     <dependency>
        <groupId>org.apache.felix</groupId>
        <artifactId>org.apache.felix.scr.annotations</artifactId>
        <version>1.6.0</version>
        <scope>compile</scope>
    </dependency>
</dependencies>
</project>
```

Lägg till den profil som finns i avsnittet [Hämtning av innehållspaketet från Plugin-programmet ](/help/sites-developing/vlt-mavenplugin.md) för din maven-inställningsfil för användning i den publika Adobe-databasen.
