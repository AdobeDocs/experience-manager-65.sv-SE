---
title: Tålig dag
seo-title: Tålig dag
description: Tough Day-testet simulerar den dagliga belastningen för cirka 1 000 författare i ett värsta scenario där alla åtgärder utförs samtidigt.
seo-description: Tough Day-testet simulerar den dagliga belastningen för cirka 1 000 författare i ett värsta scenario där alla åtgärder utförs samtidigt.
uuid: 1b672182-40f5-4580-b038-2e3c8fbfb8b7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: ea6b40fe-b6e1-495c-b34f-8815a4e2e42e
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Tålig dag{#tough-day}

## Vad är Tom Dag 2? {#what-is-tough-day}

&quot;Tough Day 2&quot; är ett program som gör att du kan testa gränserna för din AEM-instans. Den kan köras direkt med testsviten eller konfigureras för att passa dina testbehov. Du kan titta på [den här inspelningen](https://docs.adobe.com/ddc/en/gems/Toughday2---A-new-and-improved-stress-testing-and-benchmarking-tool.html) för en presentation av programmet.

## Köra tuff dag 2 {#how-to-run-tough-day}

Ladda ned den senaste versionen av Tough Day 2 från [Adobe Repository](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/qe/toughday2/). När du har hämtat programmet kan du köra det direkt genom att ange `host` parametern. I följande exempel körs AEM-instansen lokalt så att `localhost` värdet används:

```xml
java -jar toughday2.jar --host=localhost
```

Standardsviten som körs när du lägger till parametrarna får namnet `toughday`. Det innehåller följande användningsfall:

* Skapa sidor och live-kopior för dem (inklusive rollouts)
* Hämta hemsida
* Köra frågor i Query Builder
* Skapa resurshierarkier
* Ta bort resurser

Programsviten innehåller 15 % skrivåtgärder och 85 % läsåtgärder.

För att köra testerna av sviten installerar Tough Day 2 standardinnehållspaketet. Detta kan undvikas genom att ange `installsamplecontent`parametern som `false`men kom ihåg att du också bör ändra standardsökvägarna för de tester som du tänker köra. Om burken körs utan parametrar visar Tough Day 2 [hjälpinformationen](/help/sites-developing/tough-day.md#getting-help).

Som regel kan du använda programmet genom att följa det här mönstret:

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>Grovdag 2 har inget upprensningssteg. Därför bör du köra Tough Day 2 på en klonad mellanlagringsinstans och inte på huvudproduktionsinstansen. Mellanlagringsinstansen bör tas bort efter testerna.


### Få hjälp {#getting-help}

Dag 2 erbjuder en mängd hjälpalternativ som du kan komma åt från kommandoraden. Exempel:

```xml
java -jar toughday2.jar --help_full
```

I tabellen nedan hittar du relevanta hjälpparametrar.

<table>
 <tbody>
  <tr>
   <td><strong>Parameter</strong></td>
   <td><strong>Beskrivning</strong></td>
   <td><strong>Exempel</strong></td>
  </tr>
  <tr>
   <td>—help</td>
   <td>Skriver ut global information, till exempel: tillgängliga åtgärder, fördefinierade programsviter, körningslägen och globala parametrar.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_publish</td>
   <td>Skriver ut alla tillgängliga utgivare.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_tests</td>
   <td>Skriver ut testklasserna och deras beskrivning.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>Skriver ut allt ovanstående, plus tester, utgivare och Suite-komponenter.</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;Mode&gt;</td>
   <td>Visar information om det angivna körnings- eller publiceringsläget.</td>
   <td><p>java -jar toughday2.jar —help —runmode type=konstantload</p> <p>java -jar toughday2.jar —help —publishmode type=interval</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;SuiteName&gt;</td>
   <td>Listar alla tester av en given svit och deras respektive konfigurerbara egenskaper.</td>
   <td><br /> java -jar toughday2.jar —help —suite=get_tests</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;Tag&gt;</td>
   <td><br /> Visar alla objekt som har den angivna taggen.</td>
   <td>java -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>—help &lt;TestClass/PublisherClass&gt;</td>
   <td><br /> Visar alla konfigurerbara egenskaper för det angivna testet eller utgivaren.</td>
   <td><p>java -jar toughday2.jar —help UploadPDFTest</p> <p>java -jar toughday2.jar —help CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### Globala parametrar {#global-parameters}

Tough Day 2 erbjuder globala parametrar som ställer in eller ändrar miljön för testerna. Bland dessa finns målvärden, portnummer, protokoll, användare och lösenord för instansen och många andra. Exempel:

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

Du hittar de relevanta parametrarna i listan nedan:

| **Parameter** | **Beskrivning** | **Standardvärde** | **Möjliga värden** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | Installerar eller hoppar över standardinnehållspaketet för Tough Day 2. | true |  true eller false |
| `--protocol=<Val>` | Protokollet som används för värden. | http | http eller https |
| `--host=<Val>` | Värdnamnet eller IP-adressen som ska användas som mål. |  |  |
| `--port=<Val>` | Värdens port. | 4502 |  |
| `--user=<Val>` | Användarnamnet för instansen. | admin |  |
| `--password=<Val>` | Lösenord för den angivna användaren. | admin |  |
| `--duration=<Val>` | Provningens varaktighet. Kan anges i (**s**)sekunder, (**m**)minuter, (**h**)timmar och (**d**)dagar. | 1d |  |
| `--timeout=<Val>` | Hur länge ett test ska köras innan det avbryts och markeras som misslyckat. Uttryckt i sekunder. | 180 |  |
| `--suite=<Val>` | Värdet kan vara en eller en lista (avgränsad med kommatecken) med fördefinierade testsviter. | tuffing |  |
| `--configfile=<Val>` | Den målformade dynamiska konfigurationsfilen. |  |  |
| `--contextpath=<Val>` | Instansens kontextsökväg. |  |  |
| `--loglevel=<Val>` | Loggnivån för motorn Tough Day 2. | INFORMATION | ALL, DEBUG, INFO, VARNING, FEL, FATAL, AV |
| `--dryrun=<Val>` | Om true skrivs den resulterande konfigurationen ut och inga tester körs. | false |  true eller false |

## Anpassa {#customizing}

Anpassning kan göras på två sätt: kommandoradsparametrar eller dynamiska konfigurationsfiler. **Konfigurationsfiler används vanligtvis för stora anpassade programsviter och de åsidosätter standardparametrarna för Tough Day 2. Kommandoradsparametrar åsidosätter både konfigurationsfiler och standardparametrar.**

Det enda sättet att spara en testkonfiguration är att kopiera den i yaml-format. Mer information finns i den här konfigurationen av [toughday.yaml](https://repo.adobe.com/nexus/service/local/repositories/releases/content/com/adobe/qe/toughday2/0.2.1/toughday2-0.2.1.yaml) och i exemplen på yaml-konfiguration i avsnitten nedan.

### Lägga till ett nytt test {#adding-a-new-test}

Om du inte vill använda `toughday` standardsviten kan du lägga till ett test med `add` parametern. I exemplen nedan visas hur du lägger till `CreateAssetTreeTest` testet antingen med kommandoradsparametrar eller en gul konfigurationsfil.

Genom att använda kommandoradsparametrar:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

Genom att använda en dynamisk konfigurationsfil:

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### Lägga till flera instanser av samma test {#adding-multiple-instances-of-the-same-test}

Du kan också lägga till och köra flera instanser av samma test, men varje instans måste ha ett unikt namn. I exemplen nedan visas hur du lägger till två instanser av samma test antingen med kommandoradsparametrar eller en gul konfigurationsfil.

Genom att använda kommandoradsparametrar:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

Genom att använda en dynamisk konfigurationsfil:

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
    properties:
      name : FirstAssetTree
  - add : CreateAssetTreeTest
    properties:
      name : SecondAssetTree
```

### Ändra testegenskaper {#changing-the-test-properties}

Om du behöver ändra en eller flera av testegenskaperna kan du lägga till den egenskapen på kommandoraden eller i yaml-konfigurationsfilen. Om du vill visa alla tillgängliga testegenskaper lägger du till parametern på kommandoraden, till exempel: `--help <TestClass/PublisherClass>`

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

Tänk på att standardparametrarna Tough Day 2 skrivs över av standardkonfigurationsfilerna för Yaml och kommandoradsparametrarna åsidosätter både konfigurationsfilerna och standardvärdena.

I exemplen nedan visas hur du ändrar `template` egenskapen för `CreatePageTreeTest` testet antingen med kommandoradsparametrar eller en gul konfigurationsfil.

Genom att använda kommandoradsparametrar:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

Genom att använda en dynamisk konfigurationsfil:

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### Arbeta med fördefinierade testsviter {#working-with-predefined-test-suites}

I exemplen nedan visas hur du lägger till ett test i en fördefinierad svit och hur du konfigurerar om och exkluderar ett befintligt test från en fördefinierad svit.

Du kan lägga till ett nytt test i en fördefinierad svit med parametern `add` och ange den fördefinierade målsviten.

Genom att använda kommandoradsparametrar:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

Genom att använda en dynamisk konfigurationsfil:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

Befintliga tester i en given programsvit kan även konfigureras om med parametern `config`* *. Observera att du också måste ange namnet på sviten och det faktiska namnet på testet (inte testklassens namn). Du hittar testnamnet i egenskapen `name` för testklassen. Mer information om hur du söker efter testegenskaper finns i avsnittet [Ändra testegenskaper](/help/sites-developing/tough-day.md#changing-the-test-properties) .

I exemplet nedan ändras standardresurstiteln för `CreatePageTreeTest` (namngiven `UploadAsset`) till&quot;NewAsset&quot;.

Genom att använda kommandoradsparametrar:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

Genom att använda en dynamisk konfigurationsfil:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

Du kan även ta bort tester från fördefinierade sviter eller utgivare från standardkonfigurationen med hjälp av `exclude` parametern. Observera att du också måste ange namnet på sviten och det faktiska namnet på testet (inte Test C- `lass` namnet). Du hittar testnamnet i egenskapen `name` för klassen test. I exemplet nedan tas `CreatePageTreeTest` (namngivet `UploadAsset`) testet bort från toughday-sviten.

Genom att använda kommandoradsparametrar:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

Genom att använda en dynamisk konfigurationsfil:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### Körningslägen {#run-modes}

Dag 2 kan köras i något av följande lägen: **normal** och **konstant belastning**.

Det **normala** körningsläget har två parametrar:

* `concurrency` - samtidig representerar antalet trådar som Tough Day 2 skapar för testkörning. På dessa trådar kommer tester att utföras tills antingen varaktigheten är slut eller tills det inte finns fler tester att köra.

* `waittime` - väntetiden mellan två på varandra följande testkörningar i samma tråd. Värdet måste anges i millisekunder.

I exemplet nedan visas hur du lägger till parametrar med kommandoraden:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

eller genom att använda en dynamisk konfigurationsfil:

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

Det **konstanta** körningsläget skiljer sig från det normala körningsläget genom att generera ett konstant antal testkörningar, i stället för ett konstant antal trådar. Du kan ställa in inläsningen med parametern för körningsläge med samma namn.

### Testa markering {#test-selection}

Testmarkeringsprocessen är densamma för båda körningslägena och följande fungerar: alla tester har en `weight` egenskap som avgör sannolikheten för körning i en tråd. Om vi till exempel har två tester, ett med en vikt på 5 och det andra med en vikt på 10, är det två gånger mer troligt att det senare utförs än det första.

Dessutom kan tester ha en `count` egenskap som begränsar antalet körningar till ett visst antal. När detta antal har passerats kommer inga fler testkörningar att utföras. Alla testinstanser som redan körs kommer att slutföra körningen enligt konfigurationen. I följande exempel visas hur du lägger till de här parametrarna antingen på kommandoraden eller med hjälp av en dynamisk konfigurationsfil.

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest weight=5 --add CreatePageTreeTest weight=10 count=100 --runmode=normal concurrency=20
```

eller

```xml
- add : CreateAssetTreeTest
    properties :
      name : UploadAsset
      weight : 5
      base : 3
      foldertitle : IAmAFolder
      assettitle : IAmAnAsset
      count : 100
```

>[!NOTE]
>
>På grund av parallella körningar kommer det faktiska antalet testkörningar inte att vara exakt den mängd som konfigurerats i `count` parametern. Förväntade en avvikelse i förhållande till antalet pågående trådar (styrs av `concurrency parameter`).

### Torr körning {#dry-run}

En torr körning tolkar alla angivna indata (kommandoradsparametrar eller konfigurationsfiler), sammanfogar dem med standardvärdena och returnerar sedan resultatet. Den utför inte något av testerna.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## Output {#output}

Dag 2 ger både testvärden och loggar. Mer information finns i följande avsnitt.

### Testmått {#test-metrics}

Tuff dag 2 rapporterar för närvarande 9 testvärden som du kan utvärdera. Mätvärden med ***** -symbolen rapporteras endast efter lyckade körningar:

| **Namn** | **Beskrivning** |
|---|---|
| Tidsstämpel | Tidsstämpel för den senaste slutförda testkörningen. |
| Godkänd | Antal lyckade körningar. |
| Misslyckades | Antal misslyckade körningar. |
| Min* | Testkörningens kortaste varaktighet. |
| Max* | Testkörningens längsta varaktighet. |
| Median* | Beräknad medianduration för alla testkörningar. |
| Medel* | Beräknad genomsnittlig varaktighet för alla testkörningar. |
| StdDev* | Standardavvikelsen. |
| 90p* | 90-percentil. |
| 99p* | 99-percentil. |
| 99,9p* | 99,9 percentil. |
| Verkligt dataflöde* | Antal körningar delat med förfluten körningstid. |

Dessa mätvärden skrivs med hjälp av utgivare som kan läggas till med parametern `add` (på samma sätt som när du lägger till tester). Det finns för närvarande två alternativ:

* **CSVPublisher** - utdata är en CSV-fil.
* **ConsolePublisher** - utdata visas i konsolen.

Som standard är båda utgivare aktiverade.

Det finns dessutom två lägen där mätvärdena rapporteras:

* Det **enkla** publiceringsläget - rapporterar resultatet från körningens början fram till publiceringspunkten.
* Publiceringsläget **för intervaller** - rapporterar resultatet i en given tidsram. Du kan ställa in tidsbildrutan med parametern för **intervallpubliceringsläge** .

I följande exempel visas hur du konfigurerar `intervals` parametern antingen på kommandoraden eller med hjälp av en dynamisk konfigurationsfil.

Genom att använda kommandoradsparametrar:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

Genom att använda en dynamisk konfigurationsfil:

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### Loggning {#logging}

Tough Day 2 skapar en loggmapp i samma katalog som du körde Tough Day 2. Den här mappen innehåller två typer av loggar:

* **toughday.log**: innehåller meddelanden som rör programtillståndet, felsökningsinformation och globala meddelanden.
* **toughday_&lt;testname>.log**: meddelanden relaterade till det angivna testet.

Loggarna skrivs inte över, efterföljande körningar lägger till meddelanden i befintliga loggar. Loggarna har flera nivåer. Mer information finns i ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`.

#### Exempel på användning {#example-usage}

#### Kända fel {#known-issues}

[Hämta fil](assets/toughday-6_1.jar)
