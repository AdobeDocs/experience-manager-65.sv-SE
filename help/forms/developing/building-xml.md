---
title: Hur använder man den körda skripttjänsten i AEM Forms på JEE Workbench för att skapa XML-data?
description: Använda den körda skripttjänsten i AEM Forms på JEE Workbench för att skapa XML-data
source-git-commit: 730ae7cd6cd04eb6377b37eafe29db597e93cce3
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---

# Använda den körda skripttjänsten i AEM Forms på JEE Workbench för att skapa XML-data {#using-execute-script-service-forms-jee-workbench}

Det finns mycket XML i AEM Forms om arbetsflöden för JEE-processhantering, till exempel: XML-information kan byggas in i en process och skickas till ett Flex-program i AEM Forms på JEE Workspace, användas för systeminställningar eller för att skicka information till och från formulär. Det finns många tillfällen då en AEM Forms on JEE-utvecklare behöver hantera XML, och många gånger kräver detta att XML hanteras via en AEM Forms on JEE-process.

När du hanterar enkla XML-inställningar kan du använda tjänsten `Set Value`, som är AEM Forms standardtjänst för JEE. Den här tjänsten anger värdet för ett eller flera dataobjekt i processdatamodellen. För mycket enkla villkorsbaserade logikscenarier,&quot;om det är så&quot;, kan den här tjänsten passa ändamålet.

I mer komplexa situationer är dock tjänsten Ange värde inte lika effektiv. I sådana fall måste du förlita dig på en mer robust uppsättning programmeringskommandon, till exempel de som finns i ett programmeringsspråk som Java. Det kan vara mycket enklare och tydligare att använda Java för att skapa komplex XML än att skapa ett XML-dokument av enkel text i tjänsten Ange värde. Dessutom är det enklare att inkludera villkorsstyrd programmering i Java än i en Set Value-tjänst.

## Använda Execute Script Service i en process {#using-execute-script-service-in-process}

Inom ramen för AEM Forms standardtjänster för JEE-tjänster som är tillgängliga i AEM Forms på JEE Workbench finns tjänsten `Execute Script`. Med den här tjänsten kan du köra skript i processer och utföra `executeScript`-åtgärden.

### Skapa ett program och en process med tjänsten &quot;Execute Script&quot; definierad som en aktivitet {#create-an-application}

Den här självstudiekursen täcker inte längre alla applikationer och processer, men för instruktionens skull har vi skapat ett program med namnet&quot;DemoApplication02&quot;. Om ett program redan har skapats måste vi skapa en process i det här programmet för att anropa executeScript-tjänsten. Så här lägger du till en process i programmet som innehåller tjänsten `Execute Script`:

1. Högerklicka på programmet och välj [!UICONTROL New]. Välj [!UICONTROL Process] i listrutan [!UICONTROL New]. Namnge processen därefter, lägg till en beskrivning om det behövs och välj den ikon som du vill ska representera processen. I den här självstudiekursen har vi skapat en process och gett den namnet `executeScriptDemoProcess`.
1. Definiera startpunkterna eller välj att lägga till startpunkterna senare.
1. Processen skapas nu och ska öppnas automatiskt i fönstret [!UICONTROL Process Design]. I det här fönstret klickar du på ikonen Aktivitetsväljaren högst upp i fönstret Processdesign och drar den nya aktiviteten till simbanan. Nu ska [!UICONTROL Define Activity Window] visas (se figur nedan).
   ![Definiera aktivitet](assets/define-activity.jpg)
1. Tjänsten executeScript finns under `Foundation`-uppsättningen med tjänster. Tjänstnamnet listar objektet som `Execute Script – 1.0` med åtgärdsnamnet `executeScript`. Klicka för att markera det här objektet.
1. Processen bör nu skapas och som standard ska fönstret [!UICONTROL Process Properties] visas i rutan till vänster.

#### Lägg till ett skript i processen med tjänsten&quot;Execute Script&quot; {#add-script-to-process-with-execute-script}

När processen har skapats med aktiviteten Execute Script Service definierad kan du lägga till ett skript i processen. Så här lägger du till ett skript i den här processen:

1. Navigera till paletten [!UICONTROL Process Properties]. Utöka [!UICONTROL Input]-avsnittet på paletten och klicka på ikonen &quot;..&quot;.

1. Skriv skriptet i textrutan som visas. När skriptet har skrivits trycker du på OK (se figur nedan).
   ![Kör skript](assets/execute-script.jpg)

## Skapa XML med tjänsten Execute Script {#create-xml-execute-script-service}

När en process har skapats med skripttjänsten Execute, kan man sedan använda det här skriptet för att skapa XML. Man skriver de skript som beskrivs nedan i textrutan som beskrivs i avsnittet Lägg till ett skript i processen med `Execute Script`-tjänstavsnittet ovan.

**Om Execute Script Service-tekniken**

För att veta vilka funktioner och begränsningar som finns i Execute Script-tjänsten måste man känna till tjänstens tekniska grunder. I AEM Forms på JEE används parsern Apache Xerces Document Object Model (DOM) för att skapa och lagra XML-variabler i processer. Xerces är en Java-implementering av W3C:s Document Object Model-specifikation. definierade [här](https://dom.spec.whatwg.org/). DOM-specifikationen är ett standardsätt att hantera XML som har funnits sedan 1998. Java-implementeringen av Xerces, Xerces-J, stöder DOM Level 2 version 1.0.

Java-klasserna som används för att lagra XML-variabler är:

* org.apache.xerces.dom.NodeImpl och

* org.apache.xerces.dom.DocumentImpl

DocumentImpl är en underklass till NodeImpl, så det kan antas att alla XML-processvariabler är en NodeImpl-härledning. Dokumentationen för NodeImpl [finns här](http://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html).

**Ett exempel på hur du skapar XML med tjänsten Execute Script**

Här är exemplet på hur du skapar XML i en Execute Script-tjänst. Processen har en variabel, node, som är av typen XML. Slutresultatet av den här aktiviteten blir ett XML-dokument. Vad det dokumentet gör, eller hur det gäller den övergripande processen, är utanför omfånget för den här självstudiekursen, Slutligen handlar det om vad XML-koden måste göra i det övergripande programmet. Som nämndes i inledningen kan XML användas för många syften i AEM Forms för JEE-formulär och -processer. Det här är bara en förklaring av hur du kodar Execute Script-aktiviteten för att skapa ett enkelt XML-dokument.

Ett enkelt Java-skript för XML skulle se ut ungefär så här:

```xml
import org.apache.xerces.dom.DocumentImpl;

import org.w3c.dom.Document;

import org.w3c.dom.Element;



Document document = new DocumentImpl();

Element topLevelResources = document.createElement("resources");

Element resource = document.createElement("resource");

resource.setAttribute("id", "first item id");

resource.setAttribute("value", "first item value");

topLevelResources.appendChild(resource);

document.appendChild(topLevelResources);

patExecContext.setProcessDataValue("/process_data/node", document);
```

>[!NOTE]
>
>att de tidigare nämnda DOM-objekten måste importeras till skriptet.

Resultatet av det här enkla skriptet är ett nytt XML-dokument med en variabelnod som är inställd på:

```xml
<resources>

<resource id="first item id" value="first item value"/>

</resources>
```

**Använda en iterativ slinga för att lägga till noder i XML**

Noder kan också läggas till i en befintlig XML-variabel i processen. Variabeln, node, innehåller XML-objektet som vi nyss skapade.

```xml
Document document = patExecContext.getProcessDataValue("/process_data/node");

NodeList childNodes = document.getChildNodes();

int numChildren = childNodes.getLength();

for (int i = 0; i < numChildren; i++)

{

Node currentChild = childNodes.item(i);

if (currentChild.getNodeType() == Node.ELEMENT_NODE)

{

// found the top level node

Element newResource = document.createElement("resource");

newResource.setAttribute("id", "second item id");

newResource.setAttribute("value", "second item value");

currentChild.appendChild(newResource);

break;

}

}

patExecContext.setProcessDataValue("/process_data/node", document);
The variable node in the XML is now set to:

<resources> 

<resource id="first item id" value="first item value"/> 

<resource id="second item id" value="second item value"/> 

</resources>
```



