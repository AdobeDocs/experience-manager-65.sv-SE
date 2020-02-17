---
title: Använda delningsadaptrar
seo-title: Använda delningsadaptrar
description: Sling erbjuder ett adaptermönster för att enkelt översätta objekt som implementerar gränssnittet Adaptable
seo-description: Sling erbjuder ett adaptermönster för att enkelt översätta objekt som implementerar gränssnittet Adaptable
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Använda delningsadaptrar{#using-sling-adapters}

[Sling](https://sling.apache.org) erbjuder ett [adaptermönster](https://sling.apache.org/site/adapters.html) för att enkelt översätta objekt som implementerar det [adapterbara](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) gränssnittet. Det här gränssnittet innehåller en generisk [customiTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) -metod som översätter objektet till den klasstyp som skickas som argument.

Om du till exempel vill översätta ett Resource-objekt till motsvarande Node-objekt kan du bara göra följande:

```java
Node node = resource.adaptTo(Node.class);
```

## Användningsexempel {#use-cases}

Det finns följande användningsområden:

* Få implementeringsspecifika objekt.

   En JCR-baserad implementering av det generiska [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) gränssnittet ger till exempel tillgång till den underliggande JCR-referensen [`Node`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).&quot;

* Skapa genvägar för objekt som kräver att interna kontextobjekt skickas.

   Den JCR-baserade referensen [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) innehåller till exempel en referens till begäran [`JCR Session`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html)som i sin tur behövs för många objekt som ska fungera baserat på den begärandesessionen, till exempel [`PageManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) eller [`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html).

* Genväg till tjänster.

   Ett sällsynt fall - `sling.getService()` är också enkelt.

### Null-returvärde {#null-return-value}

`adaptTo()` kan returnera null.

Det finns olika orsaker till detta, bland annat:

* implementeringen saknar stöd för måltypen
* en adapterfabrik som hanterar det här ärendet är inte aktivt (t.ex. på grund av saknad tjänstreferens)
* internt villkor misslyckades
* tjänsten är inte tillgänglig

Det är viktigt att du hanterar skiftläget null på ett smidigt sätt. Vid jsp-återgivning kan det vara acceptabelt att jsp misslyckas om det resulterar i en tom del av innehållet.

### Cachelagring {#caching}

För att förbättra prestanda kan implementeringar cachelagra objektet som returneras från ett `obj.adaptTo()` anrop. Om det `obj` är samma returnerade objekt är det samma.

Denna cachelagring utförs för alla `AdapterFactory` baserade fall.

Det finns dock ingen allmän regel - objektet kan vara antingen en ny eller en befintlig instans. Det innebär att du inte kan förlita dig på något av beteendena. Därför är det viktigt, särskilt internt `AdapterFactory`, att objekt kan återanvändas i det här scenariot.

### Så här fungerar det {#how-it-works}

Det finns olika sätt att `Adaptable.adaptTo()` implementera:

* själva objektet, implementera själva metoden och mappa till vissa objekt.
* Med [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)` kan godtyckliga objekt mappas.

   Objekten måste fortfarande implementera `Adaptable` gränssnittet och måste utöka [`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (som skickar `adaptTo` anropet till en central adapterhanterare).

   Detta gör att det går att ansluta till `adaptTo` mekanismen för befintliga klasser, till exempel `Resource`.

* En kombination av båda.

I det första fallet kan javadocs visa vad som `adaptTo-targets` är möjligt. Detta är dock ofta inte möjligt för vissa underklasser, t.ex. JCR-baserade resurser. I det senare fallet är implementeringar av `AdapterFactory` vanligtvis en del av de privata klasserna i ett paket och exponeras därför inte i ett klient-API, och inte heller listas i javadocs. Teoretiskt sett skulle det vara möjligt att få tillgång till alla `AdapterFactory` implementeringar från [OSGi](/help/sites-deploying/configuring-osgi.md) -tjänstmiljön och titta på deras&quot;adaptable&quot; (sources and target)-konfigurationer, men inte mappa dem till varandra. I slutändan beror detta på den interna logiken, som måste dokumenteras. Denna referens.

## Referens {#reference}

### Sling {#sling}

[**Resursen **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html)anpassas till:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nod</a></td>
   <td>Om detta är en JCR-nodbaserad resurs eller en JCR-egenskap som refererar till en nod.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Egenskap</a></td>
   <td>Om detta är en JCR-egenskapsbaserad resurs.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Objekt</a></td>
   <td>Om detta är en JCR-baserad resurs (nod eller egenskap).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">Karta</a></td>
   <td>Returnerar en karta över egenskaperna, om detta är en JCR-nodbaserad resurs (eller annan resurs som stöder värdekartor).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>Returnerar en användbar karta över egenskaperna, om detta är en JCR-nodbaserad resurs (eller annan resurs som stöder värdekartor). Kan också uppnås (enklare) med<br /> hjälp av <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> (hanterar null-skiftläge etc.).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">ArvValueMap</a></td>
   <td>Tillägg för <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> som gör det möjligt att ta hänsyn till resurshierarkin vid sökning efter egenskaper.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/PersistableValueMap.html">PersistableValueMap</a></td>
   <td>Om detta är en JCR-nodbaserad resurs och användaren har behörighet att ändra egenskaper på den noden.<br /> Obs! flera beständiga kartor delar inte sina värden.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>Returnerar det binära innehållet i en "fil"<code>nt:resource</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>AuthorizableResourceProvider</code><code>org.apache.sling.jackrabbit.usermanager</code><code>/system/userManager</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>cq:Page</code><code>cq:PseudoPage</code></td></tr><tr><td></td><td><code>cq:Component</code></td></tr><tr><td></td><td><code>cq:Page</code></td></tr><tr><td></td><td><code>cq:Template</code></td></tr><tr><td></td><td><code>cq:Page</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>cq:Tag</code></td></tr><tr><td></td><td><code>cq:Preferences</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>cq:ContentSyncConfig</code></td></tr><tr><td></td><td><code>cq:ContentSyncConfig</code></td></tr></tbody></table>

[**ResourceResolver **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html)anpassas till:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Session</a></td>
   <td>JCR-sessionen för begäran, om det här är en JCR-baserad resurslösare (standard).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>Baserat på JCR-sessionen, om detta är en JCR-baserad resurslösare.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>Baserat på JCR-sessionen, om detta är en JCR-baserad resurslösare.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>Baserat på JCR-sessionen, om detta är en JCR-baserad resurslösare och om användaren har behörighet att komma åt UserManager.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Auktoriserbar</a> </td>
   <td>Den aktuella användaren.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">Användare</a><br /> </td>
   <td>Den aktuella användaren.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/privileges/PrivilegeManager.html">PrivilegeManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/preferences/Preferences.html">Inställningar</a></td>
   <td>Inställningar för den aktuella användaren (baserat på JCR-session om detta är en JCR-baserad resurslösare).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/preferences/PreferencesService.html">PreferencesService</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/auth/pin/PinManager.html">PinManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td>
   <td>För att göra absoluta URL:er externaliserade, även med objektet request.<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html)anpassas till:

Inga mål ännu, men implementerar Adaptable och kan användas som källa i en anpassad AdapterFactory.

[**SlingHttpServletResponse **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html)anpassas till:

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>Om det här är ett svarsalternativ.</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

[**Sidan **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)anpassas till:

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resurs</a><br /> </td>
   <td>Sidans resurs.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">EtiketteradResurs</a></td>
   <td>Etiketterad resurs (== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nod</a></td>
   <td>Sidans nod.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Allt som sidans resurs kan anpassas till.</td>
  </tr>
 </tbody>
</table>

[**Komponenten **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html)anpassas till:

| [Resurs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Komponentens resurs. |
|---|---|
| [EtiketteradResurs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | Etiketterad resurs (== this). |
| [Nod](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Komponentens nod. |
| ... | Allt som komponentens resurs kan anpassas till. |

[**Mallen **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html)anpassas till:

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resurs</a><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /></a></td>
   <td>Mallens resurs.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">EtiketteradResurs</a></td>
   <td>Etiketterad resurs (== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nod</a></td>
   <td>Nod för den här mallen.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Allt som mallens resurs kan anpassas till.</td>
  </tr>
 </tbody>
</table>

#### Dokumentskydd {#security}

[**Authorizable **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/Authorizable.html),[**User**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/User.html) and [**Group **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/Group.html)customize to:

| [Nod](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Returnerar hemnoden för användaren/gruppen. |
|---|---|
| [ReplicationStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | Returnerar replikeringsstatusen för användarens/gruppens hemnod. |

#### DAM {#dam}

[**Tillgången **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html)anpassas till:

| [Resurs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Resurs för tillgången. |
|---|---|
| [Nod](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nod för resursen. |
| ... | Allt som resursen kan anpassas till. |

#### Taggning {#tagging}

[**Taggen **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html)anpassas till:

| [Resurs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Resurs för taggen. |
|---|---|
| [Nod](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Taggens nod. |
| ... | Allt som taggens resurs kan anpassas till. |

#### Annan {#other}

Dessutom innehåller Sling/JCR/OCM också ett ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` alternativ för anpassade OCM-objekt ([Object Content Mapping](https://jackrabbit.apache.org/object-content-mapping.html)).
