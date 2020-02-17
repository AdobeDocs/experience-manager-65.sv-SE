---
title: Referens för metadatamappningar
description: 'Lär dig mer om standardkonventioner för att beskriva metadata för resurser, inklusive Dublin Core, IPTC och andra metadatamatchningar. '
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Referens för metadatamappningar {#metadata-schemata-reference}

Följande referens innehåller information om en viss metadataram (i alfabetisk ordning) samt en lista över egenskaper och deras definitioner.

## Dublin Core {#dublin-core}

Dublin Core-metadata innehåller en standardiserad uppsättning konventioner för att beskriva resurser så att de blir lättare att hitta. I AEM Assets beskriver Dublin Core digitala resurser som video, ljud, bilder och dokument.

Den enkla DCMES-uppsättningen (Dublin Core Metadata Element Set) innehåller 15 metadataelement som listas i följande tabell. Varje Dublin Core-element är valfritt och kan upprepas. Du kan lägga till eller ta bort metadata för Dublin Core på samma sätt som du gör för medietypsspecifika metadata.

Förutom DCMES finns det andra metadataelement som skapats av Dublin Core Initiative. Mer information finns i [Dublin Core Initiative](https://dublincore.org/) .

| Egenskap | Beskrivning |
|---|---|
| medverkande | Den person eller det företag som är ansvarigt för att bidra till innehållet. |
| täckning | Den geografiska plats eller tidsperiod som tillgången täcker. |
| skapare | Den person eller det företag som ansvarar för att skapa innehållet. |
| date | Datum eller tidsperiod som är associerad med tillgången. |
| description | Mer information om resursen. |
| format | Filformat, fysiskt medium eller dimensioner för resursen. AEM använder dc:format för att ange resursens mime-typ. |
| identifierare | En unik referens till tillgången. |
| language | Språket för resursen (t.ex. en för engelska). |
| utgivare | Den person eller det företag som ansvarar för att göra tillgången tillgänglig. |
| relation | En relaterad tillgång. |
| rättigheter | Information om vem som har behörighet till den här resursen. |
| source | En relaterad tillgång som tillgången härrör från. |
| ämne | Tillgångens ämne. |
| title | Ett namn för resursen. |
| type | Tillgångens art eller genre. |

## IPTC {#iptc}

IPTC (International Press Telecommunications Council) är ett konsortium av nyhetsbyråer över hela världen - ett av målen är att utveckla och underhålla tekniska standarder. IPTC definierade en uppsättning metadatastandarder för foton som är nästan allmänt accepterade bland fotografer. Dessa metadatastandarder ingick i den bredare standarden IPTC Information Interchange Model (IIM) som skapades på 1990-talet.

Även om IPTC-huvudinformationen till största delen har ersatts av XMP finns det ett IPTC-kärnschema och ett tilläggsschema för XMP. I bildprogram synkroniseras både XMP- och IPTC-egenskaper.
