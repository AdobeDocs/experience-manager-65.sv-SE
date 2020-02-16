---
title: Hantera paket med Maven
seo-title: Hantera paket med Maven
description: Använd pluginen Content Package Maven för att integrera pakethanteringsuppgifter i dina Maven-projekt
seo-description: Använd pluginen Content Package Maven för att integrera pakethanteringsuppgifter i dina Maven-projekt
uuid: fa73f0d6-8848-4911-9b96-311c875b45be
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 943de371-0149-4307-be3a-b11c590b3451
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Hantera paket med Maven{#managing-packages-using-maven}

Använd pluginen Content Package Maven för att integrera pakethanteringsuppgifter i dina Maven-projekt. Mål och parametrar för plugin-programmet gör att du kan automatisera många av de uppgifter som du normalt skulle utföra med hjälp av pakethanteringssidan eller kommandoraden för FileVault:

* Skapa nya paket från filer i filsystemet.
* Installera och avinstallera paket på CRX- eller CQ-servern.
* Skapa paket som redan har definierats på servern.
* Hämta en lista med paket som är installerade på servern.
* Ta bort ett paket från servern.

## Lägga till plugin-programmet Content Package Maven i POM-filen {#adding-the-content-package-maven-plugin-to-the-pom-file}

Om du vill använda plugin-programmet Content Package Maven lägger du till följande plugin-element i build-elementet i din POM-fil:

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>0.0.24</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Om du vill att Maven ska kunna hämta plugin-programmet använder du profilen som finns i [avsnittet Hämta plugin-programmet](#obtaining-the-content-package-maven-plugin) för innehållspaket Maven på den här sidan.

## Mål för Innehållspaketet Maven Plugin {#goals-of-the-content-package-maven-plugin}

Mål- och målparametrarna som finns i innehållspaketets plugin-program beskrivs i följande avsnitt. Parametrar som beskrivs i avsnittet Vanliga parametrar kan användas för de flesta målen. Parametrar som gäller för ett mål beskrivs i avsnittet för det målet.

**Plugin-prefix**

Plugin-prefixet är content-package. Använd det här prefixet för att köra ett mål från kommandoraden, som i följande exempel:

```shell
mvn content-package:build
```

**Parameterprefix**

Om inget annat anges använder målen och parametrarna för plugin-programmet valvprefixet, som i följande exempel:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

**Proxies**

Mål som använder proxy för CRX- eller CQ-servern använder den första giltiga proxykonfigurationen som finns i inställningarna för Maven. Om ingen proxykonfiguration hittas används ingen proxy. Se parametern useProxy i avsnittet Common Settings.

### Gemensamma parametrar {#common-parameters}

Parametrarna i följande tabell är gemensamma för alla mål utom när de anges i målkolumnen.

<table>
 <tbody>
  <tr>
   <th>Namn</th>
   <th>Typ</th>
   <th>Krävs</th>
   <th>Standardvärde</th>
   <th>Beskrivning</th>
   <th>Mål</th>
  </tr>
  <tr>
   <td>failsOnError</td>
   <td>boolean</td>
   <td>Nej</td>
   <td>false</td>
   <td>Värdet <code>true</code> gör att bygget misslyckas när ett fel inträffar. Värdet på <code>false</code> gör att felet ignoreras.</td>
   <td>Alla mål utom paket.</td>
  </tr>
  <tr>
   <td>name</td>
   <td>Sträng</td>
   <td>bygg: Ja<br /> installation: Ingen<br /> rm:Ja</td>
   <td>Bygg: Ingen standard.<br /> installera: Värdet på egenskapen artifactId för Maven-projektet.</td>
   <td>Namnet på det paket som ska användas.</td>
   <td>Alla mål utom mål.</td>
  </tr>
  <tr>
   <td>password</td>
   <td>Sträng</td>
   <td>Ja</td>
   <td>admin</td>
   <td>Lösenordet som används för autentisering med CRX-servern.</td>
   <td>Alla mål utom paket.</td>
  </tr>
  <tr>
   <td>serverId</td>
   <td>Sträng</td>
   <td>Nej</td>
   <td></td>
   <td>Det server-ID som användarnamn och lösenord för autentisering ska hämtas från.</td>
   <td>Alla mål utom paket.</td>
  </tr>
  <tr>
   <td>targetURL</td>
   <td>Sträng</td>
   <td>Ja</td>
   <td>http://localhost:4502/<br /> crx/packmgr/<br /> service.jsp</td>
   <td>URL:en för HTTP-tjänstens API för CRX-pakethanteraren.</td>
   <td>Alla mål utom paket.</td>
  </tr>
  <tr>
   <td>timeout</td>
   <td>int</td>
   <td>Nej</td>
   <td>5</td>
   <td>Anslutningens timeout för kommunikation med pakethanterartjänsten, i sekunder.</td>
   <td>Alla mål utom paket.</td>
  </tr>
  <tr>
   <td>useProxy</td>
   <td>boolean</td>
   <td>Nej</td>
   <td>true</td>
   <td>Avgör om proxykonfigurationer från inställningsfilen för Maven ska användas. Ett värde på <code>true</code> används för att använda den första aktiva proxykonfigurationen som hittas för proxybegäranden till pakethanteraren. Värdet false medför att ingen proxy används.</td>
   <td>Alla mål utom paket.</td>
  </tr>
  <tr>
   <td>userId</td>
   <td>Sträng</td>
   <td>Ja</td>
   <td>admin</td>
   <td>Användarnamnet som ska autentiseras med CRX-servern.</td>
   <td>Alla mål utom paket.</td>
  </tr>
  <tr>
   <td>utförlig</td>
   <td>boolean</td>
   <td>Nej</td>
   <td>false</td>
   <td>Aktiverar eller inaktiverar utförlig loggning. Värdet <code>true</code> möjliggör utförlig loggning.</td>
   <td>Alla mål utom paket.</td>
  </tr>
 </tbody>
</table>

### bygga {#build}

Skapar ett innehållspaket som redan har definierats på en AEM-instans.

>[!NOTE]
>
>Detta mål behöver inte genomföras inom ett Maven-projekt.

#### Parametrar {#parameters}

Alla parametrar för build-målet beskrivs i avsnittet [Common Parameters](#common-parameters) .

#### Exempel {#example}

I följande exempel skapas det arbetsflödespaket som är installerat på AEM-instansen med IP-adressen 10.36.79.223. Målet körs med följande kommando:

```shell
mvn content-package:build
```

Följande POM-fil finns i den aktuella katalogen för kommandoradsverktyget. POM anger paketnamnet och URL:en för pakettjänsten.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### installera {#install}

Installerar ett paket i databasen. För att detta mål ska kunna uppnås krävs inget Maven-projekt. Målet är bundet till installationsfasen av bygglivscykeln för Maven.

#### Parametrar {#parameters-1}

Förutom följande parametrar finns beskrivningarna i avsnittet [Vanliga parametrar](#common-parameters) .

<table>
 <tbody>
  <tr>
   <th>Namn</th>
   <th>Typ</th>
   <th>Krävs</th>
   <th>Standardvärde</th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td>artefakt</td>
   <td>Sträng</td>
   <td>Nej</td>
   <td> Värdet på egenskapen artifactId för Maven-projektet.</td>
   <td>En sträng med formulärgruppen groupId:artifactId:version[:packaging].</td>
  </tr>
  <tr>
   <td>artifactId</td>
   <td>Sträng</td>
   <td>Nej</td>
   <td></td>
   <td>ID för den artefakt som ska installeras</td>
  </tr>
  <tr>
   <td>groupId</td>
   <td>Sträng</td>
   <td>Nej</td>
   <td></td>
   <td>GroupId för den artefakt som ska installeras</td>
  </tr>
  <tr>
   <td>installera</td>
   <td>boolean</td>
   <td>Nej</td>
   <td>true</td>
   <td>Avgör om paketet ska packas upp automatiskt när det överförs. Värdet true packar upp paketet och false packar inte upp paketet.</td>
  </tr>
  <tr>
   <td>localRepository</td>
   <td>org.apache.maven.<br /> artefakt. databas.<br /> ArtifactRepository</td>
   <td>Nej</td>
   <td>Värdet på variabeln localRepository-system.</td>
   <td>Den lokala databasen Maven. Du kan inte konfigurera den här parametern med plugin-konfigurationen. Systemegenskapen används alltid.</td>
  </tr>
  <tr>
   <td>packageFile</td>
   <td>java.io.File</td>
   <td>Nej</td>
   <td>Den primära artefakten som definieras för Maven-projektet.</td>
   <td>Namnet på den paketfil som ska installeras.</td>
  </tr>
  <tr>
   <td>packning</td>
   <td>Sträng</td>
   <td>Nej</td>
   <td>zip</td>
   <td>Den typ av förpackning av artefakten som ska installeras</td>
  </tr>
  <tr>
   <td>pomRemoteRepositories</td>
   <td>java.util.List</td>
   <td>Ja</td>
   <td>Värdet för egenskapen remoteAtifactRepositories som är definierad för Maven-projektet.</td>
   <td>Det här värdet kan inte konfigureras med plugin-konfigurationen. Värdet måste anges i projektet. </td>
  </tr>
  <tr>
   <td>projekt</td>
   <td>org.apache.maven.<br /> project.MavenProject</td>
   <td>Ja</td>
   <td>Det projekt som plugin-programmet är konfigurerat för.</td>
   <td>Maven-projektet. Projektet är implicit eftersom projektet innehåller plugin-konfigurationen.</td>
  </tr>
  <tr>
   <td>databaseId <i>(POM)</i><br /> repoID <i>(kommandorad)</i></td>
   <td>Sträng</td>
   <td>Nej</td>
   <td>temp</td>
   <td>ID för databasen som artefakten hämtas från. Använd databaseID i en POM. Använd repoID på en kommandorad.</td>
  </tr>
  <tr>
   <td>databaseUrl <i>(POM)</i><br /> repoURL <i>(kommandorad)</i></td>
   <td>Sträng</td>
   <td>Nej</td>
   <td></td>
   <td>URL:en för databasen som artefakten hämtas från. Använd databaseURL i en POM. Använd repoURL på en kommandorad.</td>
  </tr>
  <tr>
   <td>version</td>
   <td>Sträng</td>
   <td>Nej</td>
   <td></td>
   <td>Den version av artefakten som ska installeras.</td>
  </tr>
 </tbody>
</table>

#### Exempel {#example-1}

I följande exempel skapas ett paket som innehåller det arbetsflödesbaserade OSGi-paketet (se exemplet för [byggmålet](#build) ) och sedan installeras paketet. Eftersom installationsmålet är bundet till paketinstallationsfasen kör följande kommando installationsmålet:

```shell
mvn install
```

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

### ls {#ls}

Visar de paket som distribueras till Package Manager.

#### Parametrar {#parameters-2}

Alla parametrar för ls-målet beskrivs i avsnittet [Vanliga parametrar](#common-parameters) .

#### Exempel {#example-2}

I följande exempel visas de paket som är installerade på AEM-instansen med IP-adressen 10.36.79.223. Målet körs med följande kommando:

```shell
mvn content-package:ls
```

Följande POM-fil finns i den aktuella katalogen för kommandoradsverktyget. POM anger pakettjänstens URL.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### rm {#rm}

Tar bort ett paket från Package Manager.

#### Parametrar {#parameters-3}

Alla parametrar för RM-målet beskrivs i avsnittet [Vanliga parametrar](#common-parameters) .

#### Exempel {#example-3}

Följande exempel tar bort det arbetsflödespaket som är installerat på AEM-instansen med IP-adressen 10.36.79.223. Målet körs med följande kommando:

```shell
mvn content-package:rm
```

Följande POM-fil finns i den aktuella katalogen för kommandoradsverktyget. POM anger pakettjänstens URL och paketets namn.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
                    <name>workflow-mbean</name>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### avinstallera {#uninstall}

Avinstallerar ett paket. Paketet finns kvar på servern i avinstallerat läge.

#### Parametrar {#parameters-4}

Alla parametrar för avinstallationsmålet beskrivs i avsnittet [Vanliga parametrar](#common-parameters) .

#### Exempel {#example-4}

I följande exempel avinstalleras det arbetsflödespaket som är installerat på AEM-instansen med IP-adressen 10.36.79.223. Målet körs med följande kommando:

```shell
mvn content-package:uninstall
```

Följande POM-fil finns i den aktuella katalogen för kommandoradsverktyget. POM anger paketnamnet och URL:en för pakettjänsten.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### package {#package}

Skapar ett innehållspaket. Standardkonfigurationen för paketmålet omfattar innehållet i katalogen där kompilerade filer sparas. Körningen av paketmålet kräver att kompileringsfasen har slutförts. Paketmålet är bundet till paketfasen av bygglivscykeln för Maven.

#### Parametrar {#parameters-5}

Förutom följande parametrar kan du läsa beskrivningen av `name` parametern i avsnittet [Vanliga parametrar](#common-parameters) .

<table>
 <tbody>
  <tr>
   <th>Namn</th>
   <th>Typ</th>
   <th>Krävs</th>
   <th>Standardvärde</th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td>archive</td>
   <td>org.apache.maven.<br /> arkivering.<br /> MavenArchiveConfiguration</td>
   <td>Nej</td>
   <td></td>
   <td>Den arkivkonfiguration som ska användas. Se <a href="https://maven.apache.org/shared/maven-archiver/index.html">dokumentationen för Maven Archiver</a>.</td>
  </tr>
  <tr>
   <td>builtContentDirectory</td>
   <td>java.io.File</td>
   <td>Ja</td>
   <td>Värdet på utdatakatalogen för Maven-bygget.</td>
   <td>Katalogen som innehåller innehållet som ska inkluderas i paketet.</td>
  </tr>
  <tr>
   <td>beroenden</td>
   <td>java.util.List</td>
   <td>Nej</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>embeddedTarget</td>
   <td>java.lang.String</td>
   <td>Nej</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>inbäddade</td>
   <td>java.util.List</td>
   <td>Nej</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>failsOnMissingEmbed</td>
   <td>boolean</td>
   <td>Ja</td>
   <td>false</td>
   <td>Värdet true gör att bygget misslyckas när en inbäddad artefakt inte hittas i projektberoendena. Ett offalvärde gör att felet ignoreras.</td>
  </tr>
  <tr>
   <td>filterSource</td>
   <td>java.io.File</td>
   <td>Nej</td>
   <td></td>
   <td>En fil som anger källan för arbetsytefiltret. Filtren som anges i konfigurationen och injiceras via inbäddade eller underpaket sammanfogas med filinnehållet.</td>
  </tr>
  <tr>
   <td>filter</td>
   <td>com.day.jcr.<br /> vault.maven.pack.impl.<br /> DefaultWorkspaceFilter</td>
   <td>Nej</td>
   <td></td>
   <td>Innehåller filterelement som definierar paketinnehållet. När de körs inkluderas filtren i filen filter.xml. Se avsnittet Använda filter nedan.</td>
  </tr>
  <tr>
   <td>finalName</td>
   <td>java.lang.String</td>
   <td>Ja</td>
   <td>finalName definieras i Maven-projektet (byggfasen).</td>
   <td>Namnet på den genererade paketets ZIP-fil, utan filtillägget ZIP.</td>
  </tr>
  <tr>
   <td> grupp</td>
   <td>java.lang.String</td>
   <td>Ja</td>
   <td>Det groupID som definieras i Maven-projektet.</td>
   <td>GroupId för det genererade innehållspaketet. Detta värde är en del av målinstallationssökvägen för innehållspaketet.</td>
  </tr>
  <tr>
   <td>outputDirectory</td>
   <td>java.io.File</td>
   <td>Ja</td>
   <td>Byggkatalogen som definieras i Maven-projektet.</td>
   <td>Den lokala katalog där innehållspaketet sparas.</td>
  </tr>
  <tr>
   <td>prefix</td>
   <td>java.lang.String</td>
   <td>Nej</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>projekt</td>
   <td>org.apache.maven.<br /> project.MavenProject</td>
   <td>Ja</td>
   <td></td>
   <td>Maven-projektet.</td>
  </tr>
  <tr>
   <td>egenskaper</td>
   <td>java.util.Map</td>
   <td>Nej</td>
   <td></td>
   <td>Ytterligare egenskaper som du kan ange i filen properties.xml. Dessa egenskaper kan inte skriva över följande fördefinierade egenskaper:
    <ul>
     <li>grupp: Använd gruppparameter för att ange</li>
     <li>namn: Använd namnparameter för att ange</li>
     <li>version: Använd versionsparameter för att ange</li>
     <li>beskrivning: Ange från projektbeskrivningen</li>
     <li>groupId: groupId för projektbeskrivningen för Maven</li>
     <li>artifactId: artifactId för Maven-projektbeskrivningen</li>
     <li>beroenden: Använd parametern för beroenden för att ange</li>
     <li>createdBy: Värdet för systemegenskapen user.name</li>
     <li>skapad: Den aktuella systemtiden</li>
     <li>requiresRoot: Använd parametern requiresRoot som ska anges</li>
     <li>packagePath: Genereras automatiskt från grupp- och paketnamnet</li>
    </ul> </td>
  </tr>
  <tr>
   <td>requiresRoot</td>
   <td>boolean</td>
   <td>Ja</td>
   <td>false</td>
   <td>Definierar om paketet kräver en rot. Detta blir egenskapen &lt;code&gt;requiresRoot&lt;/code&gt; för filen properties.xml.</td>
  </tr>
  <tr>
   <td>subPackages</td>
   <td>java.util.List</td>
   <td>Nej</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>version</td>
   <td>java.lang.String</td>
   <td>Ja</td>
   <td>Versionen som definierats i Maven-projektet</td>
   <td>Innehållspaketets version.</td>
  </tr>
  <tr>
   <td>workDirectory</td>
   <td>java.io.File</td>
   <td>Ja</td>
   <td>Den katalog som definieras i Maven-projektet (byggfasen).</td>
   <td>Katalogen som innehåller innehållet som ska inkluderas i paketet.</td>
  </tr>
 </tbody>
</table>

#### Använda filter {#using-filters}

Använd elementet filters för att definiera paketinnehållet. Filtren läggs till i elementet workspaceFilter i paketets `META-INF/vault/filter.xml` fil.

I följande filterexempel visas XML-strukturen som ska användas:

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

**Importläge**

Elementet `mode` definierar hur innehållet i databasen påverkas när paketet importeras. Följande värden kan användas:

* **** Sammanfoga: Innehåll i paketet som inte redan finns i databasen läggs till. Innehåll som finns både i paketet och i databasen ändras inte. Inget innehåll tas bort från databasen.
* **** Ersätt: Innehåll i paketet som inte finns i databasen läggs till i databasen. Innehåll i databasen ersätts med matchande innehåll i paketet. Innehåll tas bort från databasen när den inte finns i paketet.
* **** Uppdatering: Innehåll i paketet som inte finns i databasen läggs till i databasen. Innehåll i databasen ersätts med matchande innehåll i paketet. Befintligt innehåll tas bort från databasen.

När filtret inte innehåller något `mode` element används standardvärdet för `replace` .

#### Exempel {#example-5}

I följande exempel skapas ett paket som innehåller det arbetsflödesbaserade OSGi-paketet. POM-filen identifierar jcr_root-katalogen som värdet för egenskapen builtContentDirectory. Katalogen jcr_root innehåller JAR-paketfilen i katalogstrukturen som speglar databasen:

`jcr_root/apps/myapp/install/workflow-mbean-0.03-SNAPSHOT.jar`

Eftersom målet är bundet till paketbyggfasen kör följande kommando paketets mål:

`mvn package`

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

I stället för att uttrycka `package` målet i plugin- `executions` avsnittet kan du använda `content-package` som värde för `packaging` projektelementet:

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
  <packaging>content-package</packaging>
  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

### help {#help}

#### Parametrar {#parameters-6}

| Namn | Typ | Krävs | Standardvärde | Beskrivning |
|---|---|---|---|---|
| detalj | boolean | Nej | false | Avgör om alla inställningsbara egenskaper för varje mål ska visas. Värdet true visar alla inställningsbara egenskaper. |
| mål | Sträng | Nej |  | Namnet på målet som hjälpen ska visas för. Om inget värde anges visas hjälpen för alla mål. |
| indentSize | int | Nej | 2 | Antalet blanksteg som ska användas för indrag på varje nivå. Om du anger ett värde bör värdet vara positivt. |
| lineLength | int | Nej | 80 | Den maximala längden för en visningslinje. Om du anger ett värde bör värdet vara positivt. |

## Hämta innehållspaketet Maven Plugin {#obtaining-the-content-package-maven-plugin}

Plugin-programmet är tillgängligt från Adobes offentliga arkiv. Om du vill hämta plugin-programmet lägger du till följande Maven-profil i Maven-inställningsfilen och aktiverar den. När du använder kommandot Maven hämtas plugin-programmet till din lokala databas om det behövs.

>[!NOTE]
>
>Det går inte att bläddra i Adobe Public Releases-databasen, så om du navigerar till databas-URL:en med webbläsaren uppstår ett ej hittat fel. Maven har dock åtkomst till databaskatalogerna.

```xml
<profile>
    <id>adobe-public</id>
    <activation>
         <activeByDefault>false</activeByDefault>
    </activation>
    <properties>
         <releaseRepository-Id>adobe-public-releases</releaseRepository-Id>
         <releaseRepository-Name>Adobe Public Releases</releaseRepository-Name>
         <releaseRepository-URL>https://repo.adobe.com/nexus/content/groups/public</releaseRepository-URL>
    </properties>
    <repositories>
         <repository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </repository>
     </repositories>
     <pluginRepositories>
         <pluginRepository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </pluginRepository>
     </pluginRepositories>
</profile>
```

## Bädda in OSGi Bundles i ett innehållspaket {#embedding-osgi-bundles-in-a-content-package}

Använd innehållspaketet Maven Plugin för att bädda in OSGi-paket i innehållspaketet. Implementera följande konfigurationer för att bädda in paketet:

* Paketet måste deklareras som ett beroende av projektet Maven.
* Instickskonfigurationen refererar till paketet med den önskade sökvägen för paketet i paketet.

I följande exempel skapas ett paket som innehåller paketet Apache Sling JCR UserManager. I paketet finns den paketerade JAR-filen i `jcr_root/apps/myapp/install` mappen:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
             https://maven.apache.org/maven-v4_0_0.xsd">
 <modelVersion>4.0.0</modelVersion>
   <groupId>com.adobe.example.myapp</groupId>
 <artifactId>embedded-example</artifactId>
 <packaging>content-package</packaging>
 <version>1.0.0-SNAPSHOT</version>

   <build>
 <plugins>
     <plugin>
        <groupId>com.day.jcr.vault</groupId>
      <artifactId>content-package-maven-plugin</artifactId>
      <version>0.0.24</version>
      <extensions>true</extensions>
      <configuration>
   <filters>
       <filter>
    <root>/apps/myapp</root>
       </filter>
    </filters>
    <embeddeds>
       <embedded>
    <groupId>org.apache.sling</groupId>
    <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
    <target>/apps/myproject/install</target>
        </embedded>
    </embeddeds>
       </configuration>
  </plugin>
    </plugins>
    </build>
    <dependencies>
 <dependency>
      <groupId>org.apache.sling</groupId>
      <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
      <version>2.2.0</version>
 </dependency>
    </dependencies>
</project>
```

## Inkludera en miniatyrbild eller egenskapsfil i paketet {#including-a-thumbnail-image-or-properties-file-in-the-package}

Ersätt standardpaketkonfigurationsfilerna för att anpassa paketegenskaperna. Ta till exempel med en miniatyrbild för att skilja på paketet i Pakethanteraren och Paketresurs.

I paketet finns FileVault-specifika filer i mappen /META-INF/vault. Källfilerna kan finnas var som helst i filsystemet. I POM-filen definierar du byggresurser som kopierar källfilerna till target/vault-work/META-INF för inkludering i paketet.

Följande POM-kod lägger till filerna i META-INF-mappen för projektkällan i paketet:

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

Följande POM-kod lägger bara till en miniatyrbild i paketet. Miniatyrbilden måste ha namnet thumbnail.png och finnas i mappen META-INF/vault/definition i paketet. I det här exemplet finns källfilen i mappen /src/main/content/META-INF/vault/definition för projektet:

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## Använda arkitekturer för att generera AEM-projekt {#using-archetypes-to-generate-aem-projects}

Flera Maven-arkitekter finns tillgängliga för att generera AEM-projekt. Använd den arkityp som motsvarar dina utvecklingsmål:

* Ett innehållspaket som installerar resurser för ett AEM-program: [simple-content-package-archietype](#simple-content-package-archetype)
* Ett innehållspaket som innehåller artefakter från tredje part: [simple-content-package-with-embedded-architype](#simple-content-package-with-embedded-archetype).
* Ett program med flera moduler som kan användas för utveckling av Java-klasser och enhetstester: [multimodule-content-package-architype](#multimodule-content-package-archetype).

>[!NOTE]
>
>Apache Sling-projektet erbjuder också arketyper som är användbara i AEM-utveckling. Dessa finns dokumenterade på [https://sling.apache.org/site/maven-archetypes.html](https://sling.apache.org/documentation/development/maven-archetypes.html).

Varje arkityp genererar följande objekt:

* Projektmappstrukturen.
* POM-filer.
* Konfigurationsfiler för FileVault.

Arketype-artefakter finns i Adobe Public Maven-arkivet. Om du vill ladda ned och köra en arkityp, identifierar du typen av arkiv och Adobe-databasen med parametrarna för arkivtypen Maven:generate:

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId={id_of_archetype} -DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

Plugin-programmet Maven Archetype använder interaktivt läge i skalet eller kommandotolken för att samla in information om projektet. Den information du anger används för att konfigurera olika projektegenskaper, till exempel mappnamn och artefakt-ID:n.

**POM-filer**

De genererade POM-filerna innehåller kommandon för att kompilera kod, skapa paket och distribuera dem till AEM i paket. Egenskaperna `groupID`, `artifactId`, `version`och `name` för Maven-projektet fylls i automatiskt med de värden som du anger för Maven- `archetype:generate` interaktiva prompten.

Du kan ändra följande standardvärden i den genererade pom.xml-filen:

* CQ-serverns namn eller IP-adress: Standardvärdet är `localhost`. Elementet `crx.host` nedan `project/properties` innehåller det här värdet.

* Portnumret för CQ-servern: Standardvärdet är `4502`. Elementet `crx.port` nedan `project/properties` innehåller det här värdet.

* The version of Content Package Maven Plugin: Använd den senaste versionen som innehåll för elementet `version` för plugin-programmet med `artifactId` i `content-package-maven-plugin`. Standardvärdet är `0.0.24`.

**Använda arkityperna**

1. I ett kommandofönster eller en kommandotolk anger du `archetype:generate` kommandot Maven. Ange värden för de återstående parametrarna när du uppmanas till detta.

   Mer information om de olika parametrarna finns i avsnittet om den arkityp som du använder.

1. Använd en textredigerare för att öppna filen pom.xml och redigera standardvärden enligt dina önskemål.
1. Fyll de genererade mapparna med resurser.
1. Ange `mvn clean install` kommandot.

### simple-content-package-architype {#simple-content-package-archetype}

Skapar ett maven-projekt som är lämpligt för att installera resurser för ett enkelt AEM-program. Mappstrukturen är den som används under `/apps` mappen i AEM-databasen. POM definierar kommandon för att paketera resurser som du placerar i mapparna och installera paketen på AEM-instansen.

**Artefaktegenskaper för arkityp:**

* Grupp-ID: `com.day.jcr.vault`
* Artefakt-ID: `simple-content-package-archetype`
* Version: `1.0.2`
* Databas: `adobe-public-releases`

**Maven command:**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**Arketype-parametrar:**

* groupId: groupId för det innehållspaket som Maven genererar. Värdet används automatiskt i POM-filen.
* artifactId: Innehållspaketets namn. Värdet används också som namn på projektmappen.
* version:Innehållspaketets version.
* paket: Det här värdet används inte för enkel-content-package-architype.
* appsFolderName: Namnet på mappen under /apps.
* artifactName: Beskrivning av innehållspaketet.
* packageGroup: Namnet på innehållspaketgruppen. Det här värdet konfigurerar parametern group för målet Package i plugin-programmet Content Package Maven.

**Mappstruktur:**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                               |- .content.xml
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
                        |- .content.xml
```

### simple-content-package-with-embedded-architype {#simple-content-package-with-embedded-archetype}

Utför samma uppgifter som enkel-content-package-archietype, och hämtar och inkluderar även en artefakt från en offentlig Maven-databas.

**Egenskaper för arkitekturpaket:**

* Grupp-ID: `com.day.jcr.vault`
* Artefakt-ID: `simple-content-package-with-embedded-archetype`
* Version: `1.0.2`
* Databas: `adobe-public-releases`

**Maven command:**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-with-embedded-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**Arketype-parametrar:**

* groupId: groupId för det innehållspaket som Maven genererar. Värdet används automatiskt i POM-filen.
* artifactId: Innehållspaketets namn. Värdet används också som namn på projektmappen.
* version:Innehållspaketets version.
* paket: Den här parametern används inte.
* appsFolderName: Namnet på mappen under /apps.
* artifactName: Beskrivning av innehållspaketet.
* embeddedArtifactId: ID för den artefakt som ska bäddas in i innehållspaketet.
* embeddedGroupId: Grupp-ID för den artefakt som ska bäddas in.
* embeddedVersion: Den version av artefakten som ska bäddas in.
* packageGroup: Namnet på innehållspaketgruppen. Det här värdet konfigurerar parametern group för målet Package i plugin-programmet Content Package Maven.

**Mappstruktur:**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
```

### multimodule-content-package-architype {#multimodule-content-package-archetype}

Skapar ett maven-projekt som innehåller mappstrukturen för utveckling av ett AEM-program och installation av resurser på servern.

Mappen innehåller `bundle` mappstrukturen som lagrar Java- och JUnit-källfilerna som du utvecklar. Filen pom.xml i den här mappen skapar OSGi-paketet. Följande värden i POM identifierar artefakten och paketet:

* artifactID: `${artifactID}-bundle`.
* Bundle-SymbolicName: `${groupId}.${artifactId}-bundle`.

`${artifactID}` och `${groupId}` är de värden som du anger för de här parametrarna när du kör arkityperna.

Mappen innehåller `content` resurserna som är installerade på AEM-instansen. Värdet för artifactID är `${artifactID}multimodule-bundle`.

Den överordnade mappen innehåller den överordnade POM som hanterar plugin-program för Maven och beroenden.

**Egenskaper för arkitekturpaket:**

* Grupp-ID: `com.day.jcr.vault`
* Artefakt-ID: `multimodule-content-package-archetype`
* Version: `1.0.2`
* Databas: `adobe-public-releases`

**Maven command:**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=multimodule-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**Arketype-parametrar:**

* groupId: groupId för det innehållspaket som Maven genererar. Värdet används automatiskt i POM-filen.
* artifactId: Innehållspaketets namn. Värdet används också som namn på projektmappen.
* version:Innehållspaketets version.
* paket: Det här värdet används inte för arkivtypen multimodule-content-package.
* appsFolderName: Namnet på mappen under /apps.
* artifactName: Beskrivning av innehållspaketet.
* packageGroup: Namnet på innehållspaketgruppen. Det här värdet konfigurerar parametern group för målet Package i plugin-programmet Content Package Maven.

**Mappstruktur:**

```xml
${artifactId}
   |- pom.xml
   |- bundle
      |- pom.xml
      |- src
         |- main
            |- java
               |- ${groupId}
                  |- SimpleDSComponent.java
         |- test
            |- java
               |- ${groupId}
                  |- SimpleUnitTest.java
   |- content
      |- pom.xml
      |- src
         |- main
            |- content
               |- jcr_root
                  |- apps
                     |- ${appsFolderName}
                            |- config
                            |- install
                  |- META-INF
                      |- vault
                         |- config.xml
                         |- filter.xml
                         |- nodetypes.cnd
                         |- properties.xml
                         |- definition
                            |- .content.xml
```

