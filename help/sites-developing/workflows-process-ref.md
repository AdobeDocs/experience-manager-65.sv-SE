---
title: Referens för arbetsflödesprocess
seo-title: Referens för arbetsflödesprocess
description: 'null'
seo-description: 'null'
uuid: de367aa8-4580-4810-b665-2a7b521e36ca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: dbdf981f-791b-4ff7-8ca8-039d0bdc9c92
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 0%

---


# Referens för arbetsflödesprocess{#workflow-process-reference}

AEM innehåller flera processsteg som kan användas för att skapa arbetsflödesmodeller. Anpassade processsteg kan också läggas till för uppgifter som inte omfattas av de inbyggda stegen (se [Skapa arbetsflödesmodeller](/help/sites-developing/workflows-models.md)).

## Processegenskaper {#process-characteristics}

Följande egenskaper beskrivs för varje steg i processen.

### Java-klass eller ECMA-sökväg {#java-class-or-ecma-path}

Processstegen definieras antingen av en Java-klass eller av ett ECMAScript.

* För Java-klassprocesserna anges det fullständiga, kvalificerade klassnamnet.
* För ECMAScript-processerna anges sökvägen till skriptet.

### Nyttolast {#payload}

Nyttolasten är den enhet som en arbetsflödesinstans agerar på. Nyttolasten väljs implicit av den kontext i vilken en arbetsflödesinstans startas.

Om till exempel ett arbetsflöde används på en AEM sida *P*, skickas *P* från steg till steg när arbetsflödet går vidare, där varje steg kan agera på *P* på något sätt.

I det vanligaste fallet är nyttolasten en JCR-nod i databasen (till exempel en AEM eller resurs). En JCR-nodnyttolast skickas som en sträng som antingen är en JCR-sökväg eller en JCR-identifierare (UUID). I vissa fall kan nyttolasten vara en JCR-egenskap (skickas som en JCR-sökväg), en URL, ett binärt objekt eller ett generiskt Java-objekt. Enskilda processsteg som fungerar på nyttolasten förväntar sig vanligtvis en nyttolast av en viss typ, eller fungerar på olika sätt beroende på nyttolasttypen. För varje process som beskrivs nedan beskrivs den förväntade nyttolasttypen, om sådan finns,.

### Argument {#arguments}

Vissa arbetsflödesprocesser accepterar argument som administratören anger när arbetsflödessteget ställs in.

Argument anges som en enskild sträng i egenskapen **Processargument** i rutan **Egenskaper** i arbetsflödesredigeraren. För varje process som beskrivs nedan beskrivs argumentsträngens format i en enkel EBNF-grammatik. Följande indikerar till exempel att argumentsträngen består av ett eller flera kommaavgränsade par, där varje par består av ett namn (som är en sträng) och ett värde, avgränsade med ett dubbelkolon:

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### Timeout {#timeout}

Efter den här tidsgränsen är arbetsflödessteget inte längre i drift. Vissa arbetsflödesprocesser respekterar tidsgränsen, medan andra inte gäller och ignoreras.

### Behörigheter {#permissions}

Sessionen som skickas till `WorkflowProcess` backas upp av tjänstanvändaren för arbetsflödets processtjänst, som har följande behörigheter i arkivets rot:

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

Om den behörighetsuppsättningen inte är tillräcklig för din `WorkflowProcess`-implementering måste den använda en session med de behörigheter som krävs.

Det rekommenderade sättet att göra detta är att använda en tjänstanvändare som har skapats med den nödvändiga, men minimala, underuppsättningen behörigheter som krävs.

>[!CAUTION]
>
>Om du uppgraderar från en tidigare version än AEM 6.2 kan du behöva uppdatera implementeringen.
>
>I tidigare versioner skickades administratörssessionen till `WorkflowProcess`-implementeringarna och kunde sedan ha fullständig åtkomst till databasen utan att behöva definiera specifika åtkomstkontrollistor.
>
>Behörigheterna definieras nu enligt ovan ([Behörigheter](#permissions)). Detta är den rekommenderade metoden för att uppdatera implementeringen.
>
>En kortsiktig lösning finns också tillgänglig för bakåtkompatibla syften när kodändringar inte är möjliga:
>
>* Använd webbkonsolen ( `/system/console/configMgr`) för att hitta konfigurationstjänsten för arbetsflödet **Adobe Granite**
   >
   >
* aktivera **äldre arbetsflödesprocessläge**
>
>
Detta återgår till det gamla beteendet att tillhandahålla en administratörssession till `WorkflowProcess`-implementeringen och ger obegränsad åtkomst till hela databasen igen.

## Arbetsflödeskontrollprocesser {#workflow-control-processes}

Följande processer utför inga åtgärder på innehåll. De styr själva arbetsflödet.

### AbsoluteTimeAutoAdvanced (autoförskott för absolut tid) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

Processen `AbsoluteTimeAutoAdvancer` (autoavancerat för absolut tid) fungerar på samma sätt som **autoförskott**, förutom att den inträffar vid en viss tidpunkt och ett visst datum i stället för efter en viss tidslängd.

* **Java-klass**:  `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **Nyttolast**: Ingen.
* **Argument**: Ingen.
* **Timeout**: Bearbetningstiderna är slut när den angivna tiden och datumet nås.

### AutoAdvantage (autoavancerat) {#autoadvancer-auto-advancer}

Processen `AutoAdvancer` flyttar automatiskt arbetsflödet till nästa steg. Om det finns mer än ett möjligt nästa steg (till exempel om det finns en OR-delning) kommer den här processen att flytta arbetsflödet längs *standardvägen*, om en sådan har angetts, annars kommer arbetsflödet inte att avanceras.

* **Java-klass**:  `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **Nyttolast**: Ingen.
* **Argument**: Ingen.
* **Timeout**: Bearbetningstiderna är slut efter angiven tidslängd.

### ProcessAssembler (Process Assembler) {#processassembler-process-assembler}

`ProcessAssembler`-processen kör flera underprocesser sekventiellt i ett enda arbetsflödessteg. Om du vill använda `ProcessAssembler` skapar du ett enda steg av den här typen i arbetsflödet och anger dess argument för att ange namn och argument för de underprocesser som du vill köra.

* **Java-klass**:  `com.day.cq.workflow.impl.process.ProcessAssembler`

* **Nyttolast**: En DAM-resurs, AEM sida eller ingen nyttolast (beror på underprocessernas krav).
* **Argument**:

```
        args := arg [',' arg]
        arg := processname ['::' processargs]
        processname := /* A fully qualified Java Class or absolute
        repository path to an ECMAScript */
        processargs := processarg [';' processarg]*
        processarg := '[' nobracketprocessarg ']' | nobracketprocessarg
        nobracketprocessarg := listitem [':' listitem]*
        listitem := /* A string */
```

* **Timeout**: Respekt.

Till exempel:

* Extrahera metadata från resursen.
* Skapa tre miniatyrbilder av de tre angivna storlekarna.
* Skapa en JPEG-bild från resursen, förutsatt att resursen ursprungligen varken är en GIF eller en PNG (i vilket fall ingen JPEG skapas).
* Ange det senast ändrade datumet för tillgången.

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## Grundläggande processer {#basic-processes}

Följande processer utför enkla uppgifter eller fungerar som exempel.

>[!CAUTION]
>
>Du ***får*** inte ändra något i `/libs`-sökvägen.
>
>Detta beror på att innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan skrivas över när du använder en snabbkorrigering eller ett funktionspaket).

### delete {#delete}

Objektet vid den angivna sökvägen tas bort.

* **ECMAScript-sökväg**:  `/libs/workflow/scripts/delete.ecma`

* **Nyttolast**: JCR-sökväg
* **Argument**: Ingen
* **Timeout**: Ignorerad

### noop {#noop}

Detta är null-processen. Ingen åtgärd utförs, men ett felsökningsmeddelande loggas.

* **ECMAScript-sökväg**:  `/libs/workflow/scripts/noop.ecma`

* **Nyttolast**: Ingen
* **Argument**: Ingen
* **Timeout**: Ignorerad

### rule-false {#rule-false}

Detta är en null-process som returnerar `false` för metoden `check()`.

* **ECMAScript-sökväg**:  `/libs/workflow/scripts/rule-false.ecma`

* **Nyttolast**: Ingen
* **Argument**: Ingen
* **Timeout**: Ignorerad

### exempel {#sample}

Detta är ett exempel på ECMAScript-process.

* **ECMAScript-sökväg**:  `/libs/workflow/scripts/sample.ecma`

* **Nyttolast**: Ingen
* **Argument**: Ingen
* **Timeout**: Ignorerad

### urlcaller {#urlcaller}

Det här är en enkel arbetsflödesprocess som anropar den angivna URL:en. Vanligtvis är URL:en en referens till en JSP (eller annan servermotsvarighet) som utför en enkel åtgärd. Denna process bör endast användas under utveckling och demonstrationer och inte i en produktionsmiljö. Argumenten anger URL, inloggning och lösenord.

* **ECMAScript-sökväg**:  `/libs/workflow/scripts/urlcaller.ecma`

* **Nyttolast**: Ingen
* **Argument**:

```
        args := url [',' login ',' password]
        url := /* The URL to be called */
        login := /* The login to access the URL */
        password := /* The password to access the URL */
```

Till exempel: `http://localhost:4502/my.jsp, mylogin, mypassword`

* **Timeout**: Ignorerad

### LockProcess {#lockprocess}

Låser arbetsflödets nyttolast.

* **Java-klass:** `com.day.cq.workflow.impl.process.LockProcess`

* **Nyttolast:** JCR_PATH och JCR_UID
* **argument:** ingen
* **timeout:** Ignorerad

Stegen har ingen effekt under följande omständigheter:

* Nyttolasten är redan låst
* Noden nyttload innehåller inte en underordnad jcr:content-nod

### UnlockProcess {#unlockprocess}

Låser upp arbetsflödets nyttolast.

* **Java-klass:** `com.day.cq.workflow.impl.process.UnlockProcess`

* **Nyttolast:** JCR_PATH och JCR_UID
* **argument:** ingen
* **timeout:** Ignorerad

Stegen har ingen effekt under följande omständigheter:

* Nyttolasten är redan upplåst
* Noden nyttload innehåller inte en underordnad jcr:content-nod

## Versionshantering {#versioning-processes}

Följande process utför en versionsrelaterad uppgift.

### CreateVersionProcess {#createversionprocess}

Skapar en ny version av arbetsflödets nyttolast (AEM eller DAM-resurs).

* **Java-klass**:  `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **Nyttolast**: En JCR-sökväg eller UUID som refererar till en sida eller en DAM-resurs
* **Argument**: Ingen
* **Timeout**: Respekt

