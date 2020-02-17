---
title: Kodningstips
seo-title: Kodningstips
description: Tips för kodning för AEM
seo-description: Tips för kodning för AEM
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Kodningstips{#coding-tips}

## Använd taglibs eller HTL så mycket som möjligt {#use-taglibs-or-htl-as-much-as-possible}

Om du inkluderar skript i JSP:er blir det svårt att felsöka problem i koden. Dessutom är det svårt att separera affärslogiken från visningslagret genom att inkludera skriptlets i JSP:er, vilket är ett brott mot principen om ett enda ansvar och designmönstret för MVC.

### Skriv läsbar kod {#write-readable-code}

Koden skrivs en gång, men läses många gånger. Om vi lägger lite tid på att städa koden vi skriver kommer vi att betala ut utdelningar längs vägen när vi och andra utvecklare behöver läsa den senare.

### Välj namn som ska avslöjas {#choose-intention-revealing-names}

Helst behöver inte en annan programmerare öppna en modul för att förstå vad den gör. De bör också kunna avgöra vad en metod gör utan att läsa den. Ju bättre vi kan prenumerera på dessa idéer, desto enklare blir det att läsa vår kod och desto snabbare kan vi skriva och ändra vår kod.

I AEM-kodbasen används följande konventioner:


* En enskild implementering av ett gränssnitt namnges `<Interface>Impl`, dvs. `ReaderImpl`.
* Flera implementeringar av ett gränssnitt namnges `<Variant><Interface>`, dvs. `JcrReader` och `FileSystemReader`.
* Abstrakta basklasser namnges `Abstract<Interface>` eller `Abstract<Variant><Interface>`.
* Paket namnges `com.adobe.product.module`.  Varje Maven-artefakt eller OSGi-paket måste ha ett eget paket.
* Java-implementeringar placeras i ett impl-paket under deras API.


Observera att dessa konventioner inte nödvändigtvis behöver gälla för kundimplementeringar, men det är viktigt att konventionerna definieras och följs så att koden kan bevaras.

Helst borde namn visa sin avsikt. Ett vanligt kodtest för när namn inte är så tydliga som de ska vara är att det finns kommentarer som förklarar vad variabeln eller metoden är till för:

<table>
 <tbody>
  <tr>
   <td><p><strong>Otydlig</strong></p> </td>
   <td><p><strong>Radera</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d, //förfluten tid i dagar</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//get tagged images<br /> public List getItems() {}</p> </td>
   <td><p>public List getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### Upprepa inte dig själv {#don-t-repeat-yourself}

DRY anger att samma uppsättning kod aldrig ska dupliceras. Detta gäller även för exempelvis stränglitteraler. Kodduplicering öppnar dörren för defekter när något måste ändras och bör sökas ut och elimineras.

### Undvik nakna CSS-regler {#avoid-naked-css-rules}

CSS-reglerna ska vara specifika för målelementet i programmets sammanhang. En CSS-regel som tillämpas på *.content.center* skulle till exempel vara alltför bred och skulle kunna påverka mycket innehåll i hela systemet, vilket kräver att andra åsidosätter formatet i framtiden. *.myapp-centertext* är en mer specifik regel eftersom centrerad *text* anges i programmets sammanhang.

### Eliminera användning av inaktuella API:er {#eliminate-usage-of-deprecated-apis}

När ett API är inaktuellt är det alltid bättre att hitta det nya rekommenderade sättet i stället för att förlita sig på det inaktuella API:t. Detta ger smidigare uppgraderingar i framtiden.

### Skriv lokaliserbar kod {#write-localizable-code}

Alla strängar som inte tillhandahålls av en författare ska kapslas in i ett anrop till AEM:s i18n-ordlista via *I18n.get()* i JSP/Java och *CQ.I18n.get()* i JavaScript. Den här implementeringen returnerar strängen som skickades till den om ingen implementering hittas, vilket ger flexibiliteten att implementera lokalisering efter implementering av funktionerna på det primära språket.

### Escape-resurssökvägar för säkerhet {#escape-resource-paths-for-safety}

Även om sökvägar i JCR inte får innehålla blanksteg, bör koden inte brytas om de finns. Jackrabbit tillhandahåller en Text-verktygsklass med metoderna *escape()* och *escapePath()* . För JSP:er visar Granite-gränssnittet en *granite:encodeURIPath() EL* -funktion.

### Använd XSS API och/eller HTML för att skydda mot serveröverskridande skriptattacker (cross-site scripting) {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM har ett XSS-API för att enkelt rensa parametrar och skydda sig mot serveröverskridande skriptattacker (cross-site scripting). Dessutom har HTML dessa skydd inbyggda direkt i mallspråket. Ett API-kalkylblad finns att ladda ned på [Development - Guidelines and Best Practices](/help/sites-developing/dev-guidelines-bestpractices.md).

### Implementera lämplig loggning {#implement-appropriate-logging}

För Java-kod har AEM stöd för slf4j som standard-API för loggningsmeddelanden och bör användas tillsammans med de konfigurationer som görs tillgängliga via OSGi-konsolen för att ge en konsekvent administration. Slf4j visar fem olika loggningsnivåer. Vi rekommenderar att du använder följande riktlinjer när du väljer vilken nivå du vill logga ett meddelande på:

* FEL: När något har brutits i koden kan bearbetningen inte fortsätta. Detta beror ofta på ett oväntat undantag. Det är vanligtvis praktiskt att ta med stackspår i dessa scenarier.
* VARNING: När något inte har fungerat som det ska, men bearbetningen kan fortsätta. Detta beror ofta på ett undantag som vi förväntade oss, till exempel ett *PathNotFoundException*.
* INFORMATION: Information som kan vara användbar vid övervakning av ett system. Tänk på att detta är standardinställningen och att de flesta kunder låter detta vara på plats i sina miljöer. Använd den därför inte för mycket.
* FELSÖKNING: Lägre information om bearbetning. Användbart vid felsökning av supportproblem.
* SPÅR: Information på den lägsta nivån, till exempel genom att ange/avsluta metoder. Detta används vanligtvis bara av utvecklare.

I JavaScript bör *console.log* endast användas under utvecklingen och alla loggsatser bör tas bort före lanseringen.

### Undvik lasthanteringsprogrammering {#avoid-cargo-cult-programming}

Undvik att kopiera kod utan att förstå vad den gör. Om du är osäker är det alltid bäst att fråga någon som har mer erfarenhet av modulen eller API:t som du inte är säker på.
