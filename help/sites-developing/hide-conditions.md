---
title: Använda Dölj villkor
description: Dölj villkor kan användas för att avgöra om en komponentresurs återges eller inte.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
exl-id: 65f5d5e1-ac11-4a3c-8a51-ce06a741c264
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---

# Använda Dölj villkor {#using-hide-conditions}

Dölj villkor kan användas för att avgöra om en komponentresurs återges eller inte. Ett exempel på detta är när en mallskapare konfigurerar kärnkomponenten [listkomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html) i [mallredigerare](/help/sites-authoring/templates.md) och bestämmer sig för att inaktivera alternativen för att skapa listan baserat på underordnade sidor. Om du inaktiverar det här alternativet i designdialogrutan ställs en egenskap in så att det dolda villkoret utvärderas när listkomponenten återges och alternativet att visa underordnade sidor inte visas.

## Ökning {#overview}

Dialogrutor kan bli komplexa med flera alternativ för användaren, som kanske bara använder en del av de alternativ som finns till hands. Detta kan leda till en överväldigande upplevelse av användargränssnittet.

Genom att använda dolda villkor kan administratörer, utvecklare och superanvändare dölja resurser baserat på en uppsättning regler. Med den här funktionen kan de bestämma vilka resurser som ska visas när en författare redigerar innehåll.

>[!NOTE]
>
>ACL-behörigheter ersätts inte när du döljer en resurs baserat på ett uttryck. Innehållet kan redigeras men visas inte.

## Implementerings- och användningsinformation {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` är ansvarig för att filtrera resurserna baserat på förekomsten och värdet av `granite:hide` -egenskap, som finns i det fält som ska filtreras. Genomförandet av `/libs/cq/gui/components/authoring/dialog/dialog.jsp` innehåller en instans av `FilteringResourceWrapper.`

Implementeringen utnyttjar Graniten [ELResolver API](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) och lägger till en `cqDesign` egen variabel via ExpressionCustomizer.

Här är några exempel på hur du döljer villkor i en designnod som finns under `etc/design` eller som en innehållsprincip.

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

Tänk på följande när du definierar ditt dolda uttryck:

* För att vara giltig måste omfånget som egenskapen hittas uttryckas (till exempel `cqDesign.myProperty`).
* Värdena är skrivskyddade.
* Funktioner (om det behövs) bör begränsas till en viss uppsättning som tillhandahålls av tjänsten.

## Exempel {#example}

Exempel på dolda villkor finns i hela AEM och [kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) särskilt. Tänk dig till exempel [listkärnkomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html).

[Använda mallredigeraren](/help/sites-authoring/templates.md)kan mallskaparen i designdialogrutan definiera vilka alternativ för listkomponenten som är tillgängliga för sidförfattaren. Du kan till exempel välja om listan ska vara en statisk lista, en lista med underordnade sidor, en lista med taggade sidor och så vidare, aktivera eller inaktivera.

Om en mallskapare väljer att inaktivera alternativet med underordnade sidor, ställs en designegenskap in och ett dolt villkor utvärderas mot den, vilket gör att alternativet inte återges för sidförfattaren.

1. Som standard kan sidförfattaren använda listkärnkomponenten för att skapa en lista med underordnade sidor genom att välja alternativet **Underordnade sidor**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. I designdialogrutan för listkärnkomponenten kan mallskaparen välja alternativet **Inaktivera underordnade** för att förhindra att alternativet att skapa en lista baserad på underordnade sidor visas för sidförfattaren.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. En principnod skapas under `/conf/we-retail/settings/wcm/policies/weretail/components/content/list` med en egenskap `disableChildren` ange till `true`.
1. Villkoret hide definieras som värdet för en `granite:hide` egenskap på egenskapsnoden dialog `/conf/we-retail/settings/wcm/policies/weretail/components/content/list`

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. Värdet för `disableChildren` hämtas från designkonfigurationen och uttrycket `${cqDesign.disableChildren}` utvärderas till `false`, vilket innebär att alternativet inte återges som en del av komponenten.

   Du kan visa det dolda uttrycket som värdet för `granite:hide` property [i GitHub här](https://github.com/adobe/aem-core-wcm-components/blob/main/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40).

1. Alternativet **Underordnade sidor** återges inte längre för sidförfattaren när listkomponenten används.

   ![chlimage_1-221](assets/chlimage_1-221.png)
