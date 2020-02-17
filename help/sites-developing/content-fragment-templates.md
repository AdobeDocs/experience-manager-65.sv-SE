---
title: Mallar för innehållsfragment
seo-title: Mallar för innehållsfragment
description: Mallar väljs när du skapar ett innehållsfragment och tillhandahåller det nya fragmentet den grundläggande strukturen, elementet och variationen
seo-description: Mallar väljs när du skapar ett innehållsfragment och tillhandahåller det nya fragmentet den grundläggande strukturen, elementet och variationen
uuid: d147bac8-b710-40ed-9664-decb5ffcf8e7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: a975ea2e-5e24-4a96-bd62-63bb98836ff2
docset: aem65
translation-type: tm+mt
source-git-commit: 0dc96f07e45ccbfea4edc87431677ada5b1bfa8c

---


# Mallar för innehållsfragment{#content-fragment-templates}

>[!CAUTION]
>
>[Modeller](/help/assets/content-fragments-models.md) för innehållsfragment rekommenderas nu för att skapa alla dina fragment.
>
>Modeller för innehållsfragment används för alla exempel i We.Retail.

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
>Du ***får*** inte ändra något i `/libs` banan.
>
>Detta beror på att innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan mycket väl skrivas över när du använder en snabbkorrigering eller ett funktionspaket).
>
>Den rekommenderade metoden för konfiguration och andra ändringar är:
>
>1. Återskapa önskat objekt (t.ex. som det finns i `/libs`) under `/apps`
   >
   >
1. Gör ändringar i `/apps`
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
     <td><p><code>String</code></p> <p>required<br /> </p> </td>
     <td>Mallens titel (visas i guiden <strong>Skapa fragment</strong> ).</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>valfritt</p> </td>
     <td>En text som beskriver syftet med mallen (visas i guiden <strong>Skapa fragment</strong> ).</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>valfritt</p> </td>
     <td>En array med sökvägar till samlingar som ska kopplas till ett nyligen skapat innehållsfragment som standard.</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>required</p> </td>
     <td><p><code>true</code>, om de delresurser som representerar elementen (utom huvudelementet) i innehållsfragmentet ska skapas när innehållsfragmentet skapas, <em>false</em> om de ska skapas "i farten".</p> <p><strong>Obs</strong>: för närvarande måste den här parametern anges till <code>true</code>.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>required</p> </td>
     <td><p>Innehållsstrukturens version. stöds för närvarande:</p> <p><strong>Obs</strong>: för närvarande måste den här parametern anges till <code>2</code>.<br /> </p> </td>
    </tr>
   </tbody>
  </table>

* **Element**

   <table>
   <tbody>
    <tr>
     <th>Namn</th>
     <th>Typ</th>
     <th>Värde</th>
    </tr>
    <tr>
     <td><code>elements</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>required</p> </td>
     <td><p>En nod som innehåller definitionen av elementen i innehållsfragmentet. Det är obligatoriskt och måste innehålla minst en underordnad nod för <strong>Main</strong> -elementet, men kan innehålla [1..n] underordnade noder.</p> <p>När mallen används kopieras elementundergrenen till fragmentets modellundergren.</p> <p>Det första elementet (som det visas i CRXDE Lite) anses automatiskt vara <i>huvudelementet</i> . nodnamnet är irrelevant och noden i sig inte har någon särskild betydelse, förutom det faktum att den representeras av huvudtillgången, övriga element hanteras som undertillgångar.</p> </td>
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
     <td><p><code>String</code></p> <p>required</p> </td>
     <td>Elementets rubrik (visas i fragmentredigerarens elementväljare).</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>valfritt</p> <p>default: ""</p> </td>
     <td>Elementets ursprungliga innehåll. används endast om <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>valfritt</p> <p>default: <code>text/html</code></p> </td>
     <td><p>Elementets ursprungliga innehållstyp. används endast om <code>precreateElements</code><i> = </i><code>true</code>; stöds för närvarande:</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>required</p> </td>
     <td>Elementets interna namn. måste vara unik för fragmenttypen.</td>
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
     <td><code>variations</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>valfritt</p> </td>
     <td>Den här valfria noden innehåller definitionen av de ursprungliga variationerna för innehållsfragmentet.</td>
    </tr>
   </tbody>
  </table>

* **Variantnamn**

   <table>
   <tbody>
    <tr>
     <th>Namn</th>
     <th>Typ</th>
     <th>Värde</th>
    </tr>
    <tr>
     <td><code>&lt;<i>variation-name</i>&gt;</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>krävs om det finns en variantnod</p> </td>
     <td><p>Definierar en ursprunglig variation.<br /> Variationen läggs som standard till i alla element i innehållsfragmentet.</p> <p>Variationen kommer att ha samma ursprungliga innehåll som respektive element (se <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>required</p> </td>
     <td>Variantens titel (visas på fliken <strong>Variation</strong> i fragmentredigeraren (vänster)).</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>valfritt</p> <p>default: ""</p> </td>
     <td>En text som innehåller en beskrivning av variationen <span>(visas på fliken <strong>Variation</strong> i fragmentredigeraren (vänster)).</code></td>
    </tr>
   </tbody>
  </table>
