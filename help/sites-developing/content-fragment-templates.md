---
title: Mallar för innehållsfragment
description: Mallar väljs när du skapar ett innehållsfragment och tillhandahåller det nya fragmentet den grundläggande strukturen, elementet och variationen
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 1b75721c-b223-41f0-88d9-bd855b529f31
solution: Experience Manager, Experience Manager Sites
feature: Developing,Content Fragments
role: Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 0%

---

# Mallar för innehållsfragment{#content-fragment-templates}

>[!CAUTION]
>
>[Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) rekommenderas för att skapa alla nya innehållsfragment.
>
>Innehållsfragmentmodeller används för alla exempel i WKND.

>[!NOTE]
>
>Före AEM 6.3 skapades innehållsfragment baserade på mallar i stället för modeller.
>
>Mallar för innehållsfragment är nu föråldrade. De kan fortfarande användas för att skapa fragment, men du bör använda Content Fragment Models i stället. Inga nya funktioner kommer att läggas till i fragmentmallar och de kommer att tas bort i en framtida version.

Mallar väljs när ett innehållsfragment skapas. De ger det nya fragmentet grundläggande struktur, element och variation. Mallarna som används för innehållsfragment omfattas av Granite Configuration Manager.

De färdiga mallarna finns i

* `/libs/settings/dam/cfm/templates`

Du kan skapa webbplatsspecifika mallar för innehållsfragment under:

* `/apps/settings/dam/cfm/templates`
Plats för att täcka över färdiga mallar eller tillhandahålla kundspecifika, programövergripande mallar som inte är avsedda att utökas/ändras under körning.

* `/conf/global/settings/dam/cfm/templates`
Platsen för användarspecifika mallar för hela instansen som behöver ändras vid körning.

Prioritetsordningen är (i fallande ordning) `/conf`, `/apps`, `/libs`.

>[!CAUTION]
>
>Du ***får*** inte ändra något i sökvägen `/libs`.
>
>Detta beror på att innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan mycket väl skrivas över när du använder en snabbkorrigering eller ett funktionspaket).
>
>Den rekommenderade metoden för konfiguration och andra ändringar är:
>
>1. Återskapa det obligatoriska objektet (det vill säga som det finns i `/libs`) under `/apps`
>
>1. Gör ändringar i `/apps`
>

En malls grundläggande struktur hålls under

```xml
conf
  global
    settings
      dam
        cfm
          templates
            <template-name>
              ...
```

Med den specifika strukturen:

```xml
+ <template-name>
    - jcr:primaryType
    - jcr:title
    - jcr:description
    - initialAssociatedContent
    - precreateElements
    - version
    + elements
        - jcr:primaryType
        + <element-name>
            - jcr:primaryType
            - jcr:title
            - defaultContent
            - initialContentType
            - name
        ... + other element definitions
    + variations
        - jcr:primaryType
        + <variation-name>
            - jcr:primaryType
            - jcr:title
            - jcr:description
            - name
        ... + other variation definitions
```

Mer information om noderna och deras egenskaper är:

* **Mall**

  <table>
   <tbody>
    <tr>
     <th>Namn</th>
     <th>Typ</th>
     <th>Värde</th>
    </tr>
    <tr>
     <td><code>&lt;<em>template-name</em>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>Den här noden är roten för varje mall. Det är obligatoriskt och ska ha ett unikt namn.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>krävs<br /> </p> </td>
     <td>Mallens titel (visas i guiden <strong>Skapa fragment</strong>).</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>valfri</p> </td>
     <td>En text som beskriver syftet med mallen (visas i guiden <strong>Skapa fragment</strong> ).</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>valfri</p> </td>
     <td>En array med sökvägar till samlingar som ska kopplas till ett nyligen skapat innehållsfragment som standard.</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>obligatoriskt</p> </td>
     <td><p><code>true</code>, om de delresurser som representerar elementen (utom huvudelementet) i innehållsfragmentet ska skapas när innehållsfragmentet skapas: <em>false</em> om de ska skapas direkt.</p> <p><strong>Obs!</strong>: för närvarande måste den här parametern anges till <code>true</code>.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>obligatoriskt</p> </td>
     <td><p>Version av innehållsstrukturen som stöds för närvarande:</p> <p><strong>Obs!</strong>: den här parametern måste vara inställd på <code>2</code>.<br /> </p> </td>
    </tr>
   </tbody>
  </table>

* **Elements**

  <table>
   <tbody>
    <tr>
     <th>Namn</th>
     <th>Typ</th>
     <th>Värde</th>
    </tr>
    <tr>
     <td><code>elements</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>obligatoriskt</p> </td>
     <td><p>En nod som innehåller definitionen av elementen i innehållsfragmentet. Det är obligatoriskt och måste innehålla minst en underordnad nod för elementet <strong>Main</strong>, men kan innehålla [1..n] underordnade noder.</p> <p>När mallen används kopieras elementundergrenen till fragmentets modellundergren.</p> <p>Det första elementet (som det visas i CRXDE Lite) anses automatiskt vara <i>main</i> -elementet. Nodnamnet är irrelevant och själva noden har ingen speciell betydelse, förutom att det representeras av huvudresursen. De andra elementen hanteras som underresurser.</p> </td>
    </tr>
   </tbody>
  </table>

* **Elementnamn**

  <table>
   <tbody>
    <tr>
     <th>Namn</th>
     <th>Typ</th>
     <th>Värde</th>
    </tr>
    <tr>
     <td><code>&lt;<i>element-name</i>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>Den här noden definierar ett element. Det är obligatoriskt och ska ha ett unikt namn.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>obligatoriskt</p> </td>
     <td>Elementets rubrik (visas i fragmentredigerarens elementväljare).</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>valfri</p> <p>standard: ""</p> </td>
     <td>Elementets ursprungliga innehåll. Används bara om <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>valfri</p> <p>standard: <code>text/html</code></p> </td>
     <td><p>Elementets ursprungliga innehållstyp. Används bara om <code>precreateElements</code><i> = </i><code>true</code>; stöds för närvarande:</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>obligatoriskt</p> </td>
     <td>Elementets interna namn; måste vara unikt för fragmenttypen.</td>
    </tr>
   </tbody>
  </table>

* **Variationer**

  <table>
   <tbody>
    <tr>
     <th>Namn</th>
     <th>Typ</th>
     <th>Värde</th>
    </tr>
    <tr>
     <td><code>variations</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>valfri</p> </td>
     <td>Den här valfria noden innehåller definitionen av de ursprungliga variationerna för innehållsfragmentet.</td>
    </tr>
   </tbody>
  </table>

* **Variationsnamn**

  <table>
   <tbody>
    <tr>
     <th>Namn</th>
     <th>Typ</th>
     <th>Värde</th>
    </tr>
    <tr>
     <td><code>&lt;<i>variation-name</i>&gt;</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>krävs om det finns en variantnod</p> </td>
     <td><p>Definierar en ursprunglig variation.<br /> Variationen läggs som standard till i alla element i innehållsfragmentet.</p> <p>Variationen kommer att ha samma ursprungliga innehåll som respektive element (se <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>obligatoriskt</p> </td>
     <td>Variantens titel (visas på fliken <strong>Variation</strong> i fragmentredigeraren (vänster)).</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>valfri</p> <p>standard: ""</p> </td>
     <td>En text som innehåller en beskrivning av variationen <span> (som visas på fliken <strong>Variation</strong> i fragmentredigeraren (vänster)).</code></td>
    </tr>
   </tbody>
  </table>
