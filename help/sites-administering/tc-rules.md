---
title: Identifiera innehåll som ska översättas
description: Lär dig hur du identifierar innehåll som behöver översättas i Adobe Experience Manager.
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 8ca7bbcc-413a-49a8-a836-7083a9cadda1
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 1%

---

# Identifiera innehåll som ska översättas{#identifying-content-to-translate}

Översättningsregler identifierar innehållet som ska översättas för sidor, komponenter och resurser som ingår i, eller utesluts från, översättningsprojekt. När en sida eller resurs översätts extraherar AEM innehållet så att det kan skickas till översättningstjänsten.

Sidor och resurser representeras som noder i JCR-databasen. Innehållet som extraheras är ett eller flera egenskapsvärden för noderna. Översättningsreglerna identifierar de egenskaper som innehåller innehållet som ska extraheras.

Översättningsreglerna uttrycks i XML-format och lagras på följande platser:

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

Filen gäller för alla översättningsprojekt.

>[!NOTE]
>
>Efter en uppgradering till 6.4 bör du flytta filen från /etc. Se [Omstrukturering av de gemensamma tillgångarna i AEM 6.5](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules) för mer information.

Reglerna innehåller följande information:

* Sökvägen till noden som regeln gäller för. Regeln gäller även för nodens underordnade noder.
* Namnen på nodegenskaperna som innehåller innehållet som ska översättas. Egenskapen kan vara specifik för en viss resurstyp eller för alla resurstyper.

Du kan till exempel skapa en regel som översätter innehållet som författare lägger till i alla AEM grundläggande textkomponenter på dina sidor. Regeln kan identifiera `/content` noden och `text` -egenskapen för `foundation/components/text` -komponenten.

Det finns en [konsol](#translation-rules-ui) som har lagts till för att konfigurera översättningsregler. Definitionerna i användargränssnittet fyller i filen åt dig.

En översikt över funktionerna för innehållsöversättning i AEM finns på [Översätta innehåll för flerspråkiga webbplatser](/help/sites-administering/translation.md).

>[!NOTE]
>
>AEM har stöd för 1:1-mappning mellan resurstyper och referensattribut för översättning av refererat innehåll på en sida.

## Regelsyntax för sidor, komponenter och resurser {#rule-syntax-for-pages-components-and-assets}

En regel är en `node` element med ett eller flera underordnade `property` element och noll eller fler underordnade `node` element:

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

Alla dessa `node` elementen har följande egenskaper:

* The `path` -attributet innehåller sökvägen till rotnoden för grenen som reglerna gäller för.
* Underordnad `property` element identifierar de nodegenskaper som ska översättas för alla resurstyper:

   * The `name` -attributet innehåller egenskapsnamnet.
   * Valfritt `translate` attribute equals `false` om egenskapen inte är översatt. Som standard är värdet `true`. Det här attributet är användbart när du åsidosätter tidigare regler.

* Underordnad `node` element identifierar de nodegenskaper som ska översättas för specifika resurstyper:

   * The `resourceType` -attributet innehåller sökvägen som matchar komponenten som implementerar resurstypen.
   * Underordnad `property` element identifierar den nodegenskap som ska översättas. Använd den här noden på samma sätt som den underordnade noden `property` -element för nodregler.

Följande exempelregel orsakar innehållet i alla `text` egenskaper som ska översättas för alla sidor under `/content` nod. Regeln gäller för alla komponenter som lagrar innehåll i en `text` -egenskapen, till exempel komponenten Foundation Text och bildkomponenten.

```xml
<node path="/content">
          <property name="text"/>
</node>
```

I följande exempel översätts innehållet i alla `text` och översätter även andra egenskaper för Image-komponenten som utgör grunden. Om andra komponenter har egenskaper med samma namn gäller regeln inte för dem.

```xml
<node path="/content">
      <property name="text"/>
      <node resourceType="foundation/components/textimage">
         <property name="image/alt"/>
         <property name="image/jcr:description"/>
         <property name="image/jcr:title"/>
      </node>
</node>
```

## Regelsyntax för att extrahera resurser från sidor  {#rule-syntax-for-extracting-assets-from-pages}

Använd följande regelsyntax för att inkludera resurser som är inbäddade i eller refererade från komponenter:

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

Varje `assetNode` -elementet har följande egenskaper:

* Ett `resourceType` -attribut som är lika med sökvägen som matchar komponenten.
* Ett `assetReferenceAttribute` som är lika med namnet på den egenskap som lagrar resursens binära (för inbäddade resurser) eller sökvägen till den refererade resursen.

I följande exempel extraheras bilder från Image-komponenten som grund:

```xml
<assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
```

## Åsidosätta regler {#overriding-rules}

Filen translation_rules.xml består av en `nodelist` element med flera underordnade `node` -element. AEM läser nodlistan uppifrån och ned. När flera regler har samma nod som mål används den regel som är lägre i filen. Följande regler skapar till exempel allt innehåll i `text` egenskaper som ska översättas förutom för `/content/mysite/en` sidförgrening:

```xml
<nodelist>
     <node path="/content">
           <property name="text" />
     </node>
     <node path="/content/mysite/en">
          <property name="text" translate="false" />
     </node>
<nodelist>
```

## Filteregenskaper {#filtering-properties}

Du kan filtrera noder som har en viss egenskap med en `filter` -element.

Följande regler skapar till exempel allt innehåll i `text` egenskaper som ska översättas, förutom de noder som har egenskapen `draft` ange till `true`.

```xml
<nodelist>
    <node path="/content">
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## Gränssnitt för översättningsregler {#translation-rules-ui}

Det finns även en konsol för att konfigurera översättningsregler.

Så här kommer du åt den:

1. Navigera till **verktyg** och sedan **Allmänt**.

   ![chlimage_1-55](assets/chlimage_1-55.jpeg)

1. Välj **Översättningskonfiguration**.

   ![chlimage_1-56](assets/chlimage_1-56.jpeg)

Härifrån kan du **Lägg till kontext**. På så sätt kan du lägga till en bana.

![chlimage_1-57](assets/chlimage_1-57.jpeg)

Sedan måste du markera kontexten och sedan klicka **Redigera**. Då öppnas redigeraren för översättningsregler.

![chlimage_1-58](assets/chlimage_1-58.jpeg)

Det finns fyra attribut som du kan ändra via gränssnittet: `isDeep`, `inherit`, `translate` och `updateDestinationLanguage`.

**isDeep** Det här attributet gäller för nodfilter och är som standard true. Den kontrollerar om noden (eller dess överordnade noder) innehåller den egenskapen med det angivna egenskapsvärdet i filtret. Om värdet är false kontrolleras endast den aktuella noden.

Underordnade noder läggs till i ett översättningsjobb även om den överordnade noden har en egenskap `draftOnly` inställd på true för att flagga utkastinnehåll. Här `isDeep` spelas upp och kontrollerar om de överordnade noderna har en egenskap `draftOnly` som true och exkluderar dessa underordnade noder.

I redigeraren kan du markera/avmarkera **Är djup** i **Filter** -fliken.

![chlimage_1-59](assets/chlimage_1-59.jpeg)

Här är ett exempel på den resulterande XML-filen när **Är djup** är avmarkerad i användargränssnittet:

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

**ärva** Detta gäller för egenskaper. Som standard ärvs alla egenskaper, men om du vill att vissa egenskaper inte ska ärvas på den underordnade, kan du markera den egenskapen som false så att den bara tillämpas på den specifika noden.

I användargränssnittet kan du checka in/avmarkera **Inherit** i **Egenskaper** -fliken.

![chlimage_1-60](assets/chlimage_1-60.jpeg)

**translate** Attributet translate används bara för att ange om en egenskap ska översättas eller inte.

I användargränssnittet kan du checka in/avmarkera **Översätt** i **Egenskaper** -fliken.

**updateDestinationLanguage** Det här attributet används för egenskaper som inte har text men språkkoder, till exempel jcr:language. Användaren översätter inte text utan språkinställningen från källan till målet. Sådana egenskaper skickas inte för översättning.

I användargränssnittet kan du checka in/avmarkera **Översätt** i **Egenskaper** -tabb, men för de specifika egenskaper som har språkkoder som värde.

Förtydliga skillnaden mellan `updateDestinationLanguage` och `translate`Här följer ett enkelt exempel på ett sammanhang med bara två regler:

![chlimage_1-61](assets/chlimage_1-61.jpeg)

Resultatet i xml kommer att se ut så här:

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## Redigera regelfilen manuellt {#editing-the-rules-file-manually}

Filen translation_rules.xml som installeras med AEM innehåller en standarduppsättning med översättningsregler. Du kan redigera filen så att den uppfyller översättningsprojektens krav. Du kan till exempel lägga till regler så att innehållet i dina anpassade komponenter översätts.

Om du redigerar filen translation_rules.xml sparar du en säkerhetskopia i ett innehållspaket. Om du installerar AEM Service Pack eller installerar om vissa AEM kan den aktuella filen translation_rules.xml ersättas med originalfilen. Om du vill återställa reglerna i den här situationen kan du installera det paket som innehåller säkerhetskopian.

>[!NOTE]
>
>När du har skapat innehållspaketet återskapar du paketet varje gång du redigerar filen.

## Exempel på översättningsregelfil {#example-translation-rules-file}

```xml
<nodelist>
    <!-- translation rules for Geometrixx Demo site (example) -->
    <node path="/content/geometrixx">
        <!-- list all node properties that should be translated -->
        <property name="jcr:title" /> <!-- translation workflows running on content saved in /content/geometrixx, will extract jcr:title values independent of the component. -->
        <property name="jcr:description" />
        <node resourceType ="foundation/components/image"> <!-- translation workflows running on content saved in /content/geometrixx, will extract alternateText values only for Image component. -->
            <property name="alternateText"/>
        </node>
        <node resourceType ="geometrixx/components/title">
            <property name="richText"/>
            <property name="jcr:title" translate="false"/> <!-- translation workflows running on content saved in /content/geometrixx, will not extract jcr:title for Title component, but instead use richText. -->
        </node>
        <node pathContains="/cq:annotations">
            <property name="text" translate="false"/> <!-- translation workflows running on content saved in /content/geometrixx, will not extract text if part of cq:annotations node. -->
        </node>
    </node>
    <!-- translation rules for Geometrixx Outdoors site (example) -->
    <node path="/content/geometrixx-outdoors">
        <node resourceType ="foundation/components/image">
            <property name="alternateText"/>
            <property name="jcr:title" />
        </node>
        <node resourceType ="geometrixx-outdoors/components/title">
            <property name="richText"/>
        </node>
    </node>
    <!-- translation rules for ASSETS (example) -->
    <node path="/content/dam">
        <!-- configure list of metadata properties here -->
        <property name="dc:title" />
        <property name="dc:description" />
    </node>
    <!-- translation rules for extracting ASSETS from SITES content, configure all components that embed or reference assets -->
    <assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="foundation/components/video" assetReferenceAttribute="asset"/>
    <assetNode resourceType="foundation/components/download" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="foundation/components/mobileimage" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="wcm/foundation/components/image" assetReferenceAttribute="fileReference"/>
</nodelist>
```
