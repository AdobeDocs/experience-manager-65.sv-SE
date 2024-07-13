---
title: Emulatorer
description: AEM gör det möjligt för författare att visa en sida i en emulator som simulerar den miljö i vilken slutanvändaren ska visa sidan
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Emulatorer{#emulators}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Med Adobe Experience Manager (AEM) kan författare visa en sida i en emulator som simulerar den miljö i vilken slutanvändaren ska visa sidan, till exempel på en mobilenhet eller i en e-postklient.

AEM emulatorramverk:

* Innehållsutveckling i ett simulerat användargränssnitt, t.ex. en mobilenhet eller en e-postklient (används för att skapa nyhetsbrev).
* Anpassar sidinnehållet enligt det simulerade användargränssnittet.
* Gör att du kan skapa egna emulatorer.

>[!CAUTION]
>
>Den här funktionen stöds bara i Classic UI.

## Emulatoregenskaper {#emulators-characteristics}

En emulator:

* Baseras på ExtJS.
* Fungerar på sidan DOM.
* Dess utseende regleras via CSS.
* Stöder plugin-program (till exempel plugin-programmet för mobilenhetsrotation).
* Är bara aktivt på författare.
* Dess baskomponent är vid `/libs/wcm/emulator/components/base`.

### Hur emulatorn omformar innehållet {#how-the-emulator-transforms-the-content}

Emulatorn fungerar genom att kapsla in HTML innehåll i emulatorns DIV:er. Följande html-kod:

```xml
<body>
<div id="wrapper" class="page mobilecontentpage ">
    <div class="topnav mobiletopnav">
    ...
    </div>
    ...
</div>
</body>
```

omvandlas till följande html-kod efter emulatorns start:

```xml
<body>
 <div id="cq-emulator-toolbar">
 ...
 </div>
 <div id="cq-emulator-wrapper">
  <div id="cq-emulator-device">
   <div class=" android vertical" id="cq-emulator">
    ...
    <div class=" android vertical" id="cq-emulator-content">
     ...
     <div id="wrapper" class="page mobilecontentpage">
     ...
     </div>
     ...
    </div>
   </div>
  </div>
 </div>
 ...
</body>
```

Två div-taggar har lagts till:

* diven med ID `cq-emulator` som innehåller emulatorn som helhet och

* div med ID `cq-emulator-content` som representerar den visningsruta/skärm/innehållsområde på enheten där sidinnehållet finns.

Nya CSS-klasser tilldelas också till den nya emulatorns divar: de representerar namnet på den aktuella emulatorn.

Plugin-program för en emulator kan utöka listan med tilldelade CSS-klasser ytterligare, som i exemplet med plugin-programmet för rotation, genom att infoga en&quot;vertikal&quot; eller&quot;horisontell&quot; klass beroende på den aktuella enhetsrotationen.

På så sätt kan emulatorns fullständiga utseende styras genom att CSS-klasserna motsvarar emulatorns ID:n och CSS-klasser.

>[!NOTE]
>
>Vi rekommenderar att projektet HTML kapslar in brödtextinnehållet i en enda div, precis som i exemplet ovan. Om brödtextinnehållet innehåller flera taggar kan det ge oförutsägbara resultat.

### Mobila emulatorer {#mobile-emulators}

Befintliga mobilemulatorer:

* Finns under /libs/wcm/mobile/components/emulators.
* Finns via JSON-servleten på:

  http://localhost:4502/bin/wcm/mobile/emulators.json

När sidkomponenten är beroende av den mobila sidkomponenten ( `/libs/wcm/mobile/components/page`), integreras emulatorfunktionen automatiskt på sidan med följande mekanism:

* Den mobila sidkomponenten `head.jsp` innehåller enhetsgruppens associerade init-komponent för emulering (endast i redigeringsläge) och enhetsgruppens återgivnings-CSS via:

  `deviceGroup.drawHead(pageContext);`

* Metoden `DeviceGroup.drawHead(pageContext)` innehåller emulatorns init-komponent, d.v.s. anropar emulatorkomponentens `init.html.jsp`. Om emulatorkomponenten inte har sin egen `init.html.jsp` och är beroende av mobilbasemulatorn ( `wcm/mobile/components/emulators/base)`) anropas initieringsskriptet för mobilbasemulatorn ( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* Initieringsskriptet för mobilbasemulatorn definierar via JavaScript:

   * Konfigurationen för alla emulatorer som är definierade för sidan (emulatorConfigs)
   * Emulatorhanteraren som integrerar emulatorns funktioner på sidan genom:

     `emulatorMgr.launch(config)`;

     Emulatorhanteraren definieras av:

     `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### Skapa en anpassad emulator för mobiler {#creating-a-custom-mobile-emulator}

Så här skapar du en anpassad mobilemulator:

1. Under `/apps/myapp/components/emulators` skapar du komponenten `myemulator` (nodtyp: `cq:Component`).

1. Ange egenskapen `sling:resourceSuperType` till `/libs/wcm/mobile/components/emulators/base`

1. Definiera ett CSS-klientbibliotek med kategorin `cq.wcm.mobile.emulator` för emulatorns utseende: name = `css`, nodtyp = `cq:ClientLibrary`

   Du kan till exempel referera till noden `/libs/wcm/mobile/components/emulators/iPhone/css`

1. Om det behövs definierar du till exempel ett JS-klientbibliotek för att definiera ett specifikt plugin-program: name = js, nodtyp = cq:ClientLibrary

   Du kan till exempel referera till noden `/libs/wcm/mobile/components/emulators/base/js`

1. Om emulatorn har stöd för specifika funktioner som definieras av plugin-program (som pekrullning) skapar du en konfigurationsnod under emulatorn: name = `cq:emulatorConfig`, nodtyp = `nt:unstructured` och lägger till egenskapen som definierar plugin-programmet:

   * Namn = `canRotate`, typ = `Boolean`, värde = `true`: om du vill inkludera rotationsfunktionen.

   * Namn = `touchScrolling`, typ = `Boolean`, värde = `true`: om du vill inkludera pekrullningsfunktionen.

   Du kan lägga till fler funktioner genom att definiera egna plugin-program.
