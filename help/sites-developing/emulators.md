---
title: Emulatorer
seo-title: Emulatorer
description: Med AEM kan författare visa en sida i en emulator som simulerar miljön där slutanvändaren visar sidan
seo-description: Med AEM kan författare visa en sida i en emulator som simulerar miljön där slutanvändaren visar sidan
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Emulatorer{#emulators}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Med Adobe Experience Manager (AEM) kan författare visa en sida i en emulator som simulerar i vilken miljö slutanvändaren ska visa sidan, till exempel på en mobil enhet eller i en e-postklient.

AEM-emulatorramverket:

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
* Stöder plugin-program (t.ex. plugin-programmet för mobilenhetsrotation).
* Är bara aktivt på författare.
* Dess baskomponent är på `/libs/wcm/emulator/components/base`.

### Hur emulatorn omformar innehållet {#how-the-emulator-transforms-the-content}

Emulatorn fungerar genom att kapsla HTML-brödinnehållet i emulatorns DIV:er. Följande HTML-kod:

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

* diven med id `cq-emulator` som innehåller emulatorn som helhet och

* div-taggen med ett id `cq-emulator-content` som representerar den visningsruta/skärm/innehållsområde där sidinnehållet finns.

Nya CSS-klasser tilldelas också till de nya emulatordiven: de representerar namnet på den aktuella emulatorn.

Plugin-program för en emulator kan utöka listan med tilldelade CSS-klasser ytterligare, som i exemplet med plugin-programmet för rotation, genom att infoga en&quot;vertikal&quot; eller&quot;horisontell&quot; klass beroende på den aktuella enhetsrotationen.

På så sätt kan emulatorns fullständiga utseende styras genom att CSS-klasserna motsvarar emulatorns ID:n och CSS-klasser.

>[!NOTE]
>
>Vi rekommenderar att projekt-HTML kapslar in brödtextinnehållet i en enda div, precis som i exemplet ovan. Om brödtextinnehållet innehåller flera taggar kan det ge oförutsägbara resultat.

### Mobila emulatorer {#mobile-emulators}

Befintliga mobilemulatorer:

* Finns under /libs/wcm/mobile/components/emulators.
* Finns via JSON-servleten på:

   http://localhost:4502/bin/wcm/mobile/emulators.json

När sidkomponenten är beroende av den mobila sidkomponenten ( `/libs/wcm/mobile/components/page`), integreras emulatorfunktionen automatiskt på sidan med följande mekanism:

* Komponenten för mobilsidan `head.jsp` innehåller enhetsgruppens associerade init-komponent för emulatorn (endast i redigeringsläge) och enhetsgruppens återgivnings-CSS via:

   `deviceGroup.drawHead(pageContext);`

* Metoden `DeviceGroup.drawHead(pageContext)` innehåller emulatorns init-komponent, d.v.s. anropar emulatorkomponentens `init.html.jsp` init-komponent. Om emulatorkomponenten inte har en egen `init.html.jsp` och är beroende av mobilbasemulatorn ( `wcm/mobile/components/emulators/base)`anropas initieringsskriptet för mobilbasemulatorn ( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* Initieringsskriptet för mobilbasemulatorn definierar via Javascript:

   * Konfigurationen för alla emulatorer som är definierade för sidan (emulatorConfigs)
   * Emulatorhanteraren som integrerar emulatorns funktioner på sidan genom:

      `emulatorMgr.launch(config)`;

      Emulatorhanteraren definieras av:

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### Skapa en anpassad mobilemulator {#creating-a-custom-mobile-emulator}

Så här skapar du en anpassad mobilemulator:

1. Nedan `/apps/myapp/components/emulators` skapar du komponenten `myemulator` (nodtyp: `cq:Component`).

1. Ange `sling:resourceSuperType` egenskapen till `/libs/wcm/mobile/components/emulators/base`

1. Definiera ett CSS-klientbibliotek med en kategori `cq.wcm.mobile.emulator` för emulatorns utseende: name = `css`, nodtyp = `cq:ClientLibrary`

   Du kan till exempel referera till noden `/libs/wcm/mobile/components/emulators/iPhone/css`

1. Definiera vid behov ett JS-klientbibliotek, t.ex. för att definiera ett specifikt plugin-program: name = js, nodtyp = cq:ClientLibrary

   Du kan till exempel referera till noden `/libs/wcm/mobile/components/emulators/base/js`

1. Om emulatorn har stöd för vissa funktioner som definieras av plugin-program (som pekrullning) skapar du en konfigurationsnod under emulatorn: name = `cq:emulatorConfig`, node type = `nt:unstructured` och add the property that define the plugin:

   * Namn = `canRotate`, Typ = `Boolean`, Värde = `true`: för att inkludera rotationsfunktionen.

   * Namn = `touchScrolling`, Typ = `Boolean`, Värde = `true`: för att inkludera pekskärmsfunktionen.
   Du kan lägga till fler funktioner genom att definiera egna plugin-program.

