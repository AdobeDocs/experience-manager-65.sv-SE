---
title: Skapa ett anpassat formulär med hjälp av en uppsättning anpassningsbara formulär
description: Med AEM Forms kan du sammanföra adaptiva formulär och ta fram ett enda stort anpassat formulär och förstå dess funktioner.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 4254c2cb-66cc-4a46-b447-bc5e32def7a0
source-git-commit: d85fc98d9a31bc4014aef4311ba0f838c7ef619a
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Skapa ett anpassat formulär med hjälp av en uppsättning anpassningsbara formulär{#create-an-adaptive-form-using-a-set-of-adaptive-forms}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>

## Ökning {#overview}

I ett arbetsflöde, till exempel ett program för att öppna ett bankkonto, fyller dina användare i flera formulär. I stället för att be dem fylla i en uppsättning formulär kan du stapla formulären tillsammans och skapa ett stort formulär (överordnat formulär). När du lägger till ett anpassat formulär i det större formuläret läggs det till som en panel (underordnat formulär). Du lägger till en uppsättning med underordnade formulär för att skapa ett överordnat formulär. Du kan visa eller dölja paneler baserat på användarindata. Knappar i det överordnade formuläret, till exempel skicka och återställ, skriver över knapparna i det underordnade formuläret. Om du vill lägga till ett anpassat formulär i det överordnade formuläret kan du dra och släppa det anpassningsbara formuläret från resursläsaren (som adaptiva formulärfragment).

Tillgängliga funktioner är:

* Oberoende redigering
* Visa/dölj lämpliga formulär
* Lazy loading

Funktioner som oberoende redigering och lat inläsning ger prestandaförbättringar jämfört med att använda enskilda komponenter för att skapa det överordnade formuläret.

>[!NOTE]
>
>Du kan inte använda XFA-baserade adaptiva formulär/fragment som underordnade eller överordnade formulär.

## Bakom scenen {#behind-the-scenes}

Du kan lägga till XSD-baserade adaptiva formulär och fragment i det överordnade formuläret. Det överordnade formulärets struktur är densamma som [alla anpassningsbara formulär](../../forms/using/prepopulate-adaptive-form-fields.md). När du lägger till ett anpassat formulär som ett underordnat formulär läggs det till som en panel i det överordnade formuläret. Data i ett bundet underordnat formulär lagras under `data`roten i `afBoundData` i det överordnade formulärets XML-schema.

Kunderna fyller t.ex. i en ansökningsblankett. De två första fälten i formuläret är namn och identitet. XML:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
        </data>
    </afBoundData>
</afData>
```

Du lägger till ett annat formulär i programmet som gör att dina kunder kan fylla i sin kontorsadress. Det underordnade formulärets schemarot är `officeAddress`. Använd `bindref` `/application/officeAddress` eller `/officeAddress`. If `bindref`har inte angetts, läggs det underordnade formuläret till som `officeAddress` underträd. Se XML för formuläret nedan:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
        </data>
    </afBoundData>
</afData>
```

Om du infogar ett annat formulär där kunderna kan ange sin hemadress, ska du använda `bindref` `/application/houseAddress or /houseAddress.`XML ser ut så här:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
            <houseAddress>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </houseAddress>
        </data>
    </afBoundData>
</afData>
```

Om du vill behålla samma underrotnamn som schemaroten ( `Address`i det här exemplet) använder du indexerade bindrefs.

Använd t.ex. bindrefs `/application/address[1]` eller `/address[1]` och `/application/address[2]` eller `/address[2]`. Formulärets XML är:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <address>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
            <address>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
        </data>
    </afBoundData>
</afData>
```

Du kan ändra standardunderträdet för det adaptiva formuläret/fragmentet med `bindRef` -egenskap. The `bindRef` Med -egenskapen kan du ange sökvägen som pekar på en plats i XML-schemats trädstruktur.

Om det underordnade formuläret är obundet lagras dess data under `data`roten i `afUnboundData` i det överordnade formulärets XML-schema.

Du kan lägga till ett anpassat formulär som ett underordnat formulär flera gånger. Se till att `bindRef` ändras på rätt sätt så att varje instans av det adaptiva formuläret pekar på en annan underrot under dataroten.

>[!NOTE]
>
>Om olika formulär/fragment mappas till samma underrot skrivs data över.

## Lägga till ett adaptivt formulär som ett underordnat formulär med hjälp av resursläsaren {#adding-an-adaptive-form-as-a-child-form-using-asset-browser}

Utför följande steg för att lägga till ett anpassat formulär som ett underordnat formulär med hjälp av resursläsaren.

1. Öppna det överordnade formuläret i redigeringsläge.
1. Klicka på **Resurser** ![assets-browser](assets/assets-browser.png). Under Resurser väljer du **Adaptiv form** i listrutan.
   [![Välja anpassat formulär under Resurser](assets/asset.png)](assets/asset-1.png)

1. Dra och släpp det adaptiva formulär som du vill lägga till som ett underordnat formulär.
   [![Dra-och-släpp det anpassningsbara formuläret på webbplatsen](assets/drag-drop.png)](assets/drag-drop-1.png)Det anpassningsbara formuläret som du släpper läggs till som ett underordnat formulär.
