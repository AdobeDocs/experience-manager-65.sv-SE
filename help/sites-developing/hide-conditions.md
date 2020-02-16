---
title: Använda Dölj villkor
seo-title: Använda Dölj villkor
description: Dölj villkor kan användas för att avgöra om en komponentresurs återges eller inte.
seo-description: Dölj villkor kan användas för att avgöra om en komponentresurs återges eller inte.
uuid: 93b4f450-1d94-4222-9199-27b5f295f8e6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 104d1c64-b9b3-40f5-8f9b-fe92d9daaa1f
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Använda Dölj villkor{#using-hide-conditions}

Dölj villkor kan användas för att avgöra om en komponentresurs återges eller inte. Ett exempel på detta är när en mallskapare konfigurerar [listkomponenten](https://helpx.adobe.com/experience-manager/core-components/using/list.html) Core Component i [mallredigeraren](/help/sites-authoring/templates.md) och bestämmer sig för att inaktivera alternativen för att skapa listan baserat på underordnade sidor. Om du inaktiverar det här alternativet i designdialogrutan anges en egenskap så att när listkomponenten återges utvärderas dolda villkor och alternativet att visa underordnade sidor inte visas.

## Översikt {#overview}

Dialogrutor kan bli mycket komplexa med många alternativ för användaren, som kanske bara använder en del av de alternativ som han/hon har till sitt förfogande. Detta kan leda till en överväldigande upplevelse av användargränssnittet.

Genom att använda dolda villkor kan administratörer, utvecklare och superanvändare dölja resurser baserat på en uppsättning regler. Med den här funktionen kan de bestämma vilka resurser som ska visas när en författare redigerar innehåll.

>[!NOTE]
>
>ACL-behörigheter ersätts inte när du döljer en resurs baserat på ett uttryck. Innehållet kan redigeras men visas inte.

## Implementerings- och användningsinformation {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` är ansvarig för att filtrera resurserna baserat på förekomsten och värdet av den `granite:hide` egenskap som finns i det fält som ska filtreras. Implementeringen av `/libs/cq/gui/components/authoring/dialog/dialog.jsp` innehåller en instans av `FilteringResourceWrapper.`

Implementeringen använder Granite [ELResolver API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) och lägger till en `cqDesign` anpassad variabel via ExpressionCustomizer.

Här är några exempel på hur du döljer villkor i en designnod som antingen finns under `etc/design` eller som en innehållsprincip.

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

När du definierar ditt dolda uttryck ska du tänka på:

* För att vara giltig måste det omfång i vilket egenskapen hittas uttryckas (t.ex. `cqDesign.myProperty`).
* Värdena är skrivskyddade.
* Funktioner (om det behövs) bör begränsas till en viss uppsättning som tillhandahålls av tjänsten.

## Exempel {#example}

Exempel på gömda förhållanden finns i hela AEM och i synnerhet i [kärnkomponenterna](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) . Ta till exempel huvudkomponenten [för](https://helpx.adobe.com/experience-manager/core-components/using/list.html)listan.

[Med mallredigeraren](/help/sites-authoring/templates.md)kan mallskaparen i designdialogrutan definiera vilka alternativ för listkomponenten som är tillgängliga för sidförfattaren. Alternativ som om listan ska kunna vara en statisk lista, en lista med underordnade sidor, en lista med taggade sidor osv. kan aktiveras eller inaktiveras.

Om en mallskapare väljer att inaktivera alternativet för underordnade sidor, ställs en designegenskap in och ett dolt villkor utvärderas mot den, vilket gör att alternativet inte återges för sidförfattaren.

1. Som standard kan sidförfattaren använda listkärnkomponenten för att skapa en lista med underordnade sidor genom att välja alternativet **Underordnade sidor**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. I designdialogrutan för listkärnkomponenten kan mallskaparen välja alternativet **Inaktivera underordnade** för att förhindra att alternativet genererar en lista baserad på underordnade sidor som visas för sidförfattaren.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. En principnod skapas under `/conf/we-retail/settings/wcm/policies/weretail/components/content/lis`den med egenskapen `disableChildren` inställd på `true`.
1. Villkoret hide definieras som värdet för en `granite:hid`e-egenskap i egenskapsnoden dialog `/conf/we-retail/settings/wcm/policies/weretail/components/content/list`

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. Värdet för `disableChildren` hämtas från designkonfigurationen och uttrycket `${cdDesign.disableChildren}` utvärderas till `false`, vilket innebär att alternativet inte återges som en del av komponenten.

   Du kan visa uttrycket hide som värdet för `granite:hide` egenskapen [i GitHub här](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40).

1. Alternativet **Underordnade sidor** återges inte längre för sidförfattaren när listkomponenten används.

   ![chlimage_1-221](assets/chlimage_1-221.png)

