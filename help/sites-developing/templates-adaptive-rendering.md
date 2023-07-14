---
title: Adaptiv mallåtergivning
description: Adaptiv mallåtergivning
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Adaptiv mallåtergivning{#adaptive-template-rendering}

Med den adaptiva mallåtergivningen kan du hantera en sida med variationer. Den här funktionen är ursprungligen användbar när du vill leverera olika utdataformat för mobila enheter (till exempel från telefoner till smarttelefoner), men den är användbar när du vill leverera HTML till olika enheter som behöver olika märkningar eller HTML.

## Översikt {#overview}

Mallar byggs runt ett responsivt rutnät, och sidor som skapas baserat på dessa mallar är helt responsiva och justeras automatiskt till visningsrutan på klientenheten. Med verktygsfältet Emulator i sidredigeraren kan man rikta layouten till specifika enheter.

Det går också att skapa mallar som stöder adaptiv återgivning. När enhetsgrupper är korrekt konfigurerade återges sidan med en annan väljare i URL:en när en enhet väljs i emulatorläge. Om du använder en väljare kan en viss sidåtergivning anropas direkt via webbadressen.

Kom ihåg när du konfigurerar enhetsgrupper:

* Alla enheter måste finnas i minst en enhetsgrupp.
* En enhet kan finnas i flera enhetsgrupper.
* Eftersom enheter kan finnas i flera enhetsgrupper kan väljarna kombineras.
* Kombinationen av väljare utvärderas uppifrån och ned när de sparas i databasen.

>[!NOTE]
>
>Enhetsgruppen **Responsiva enheter har aldrig någon väljare eftersom enheter som identifieras som kompatibla med responsiv design antas inte behöva någon adaptiv layout

## Konfiguration {#configuration}

Anpassningsbara återgivningsväljare kan konfigureras för befintliga enhetsgrupper eller till [grupper som du själv har skapat.](/help/sites-developing/mobile.md#device-groups)

I det här exemplet ska du konfigurera den befintliga enhetsgruppen **Smarta telefoner** att ha en adaptiv återgivningsväljare som en del av **Experience Page** i We.Retail.

1. Redigera enhetsgruppen som kräver en adaptiv väljare i `http://localhost:4502/miscadmin#/etc/mobile/groups`

   Ange alternativ **Inaktivera emulatorn** och spara.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Väljaren är tillgänglig för **BlackBerry®** och **iPhone 4** tillhandahöll enhetsgruppen **Smart Phone** läggs till i mall- och sidstrukturerna i följande steg.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. Tillåt att enhetsgruppen används i mallen med CRXDE Lite genom att lägga till den i egenskapen för flervärdessträngen `cq:deviceGroups` på mallens struktur.

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   Om du till exempel vill lägga till enhetsgruppen Smart Phone:

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. Tillåt att enhetsgruppen används på din plats med CRXDE Lite genom att lägga till den i egenskapen för flervärdessträngen `cq:deviceGroups` på webbplatsens struktur.

   `/content/<your-site>/jcr:content`

   Om du till exempel vill tillåta **Smart Phone** enhetsgrupp:

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

Nu när du använder [emulator](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) i sidredigeraren (till exempel när [ändra layouten](/help/sites-authoring/responsive-layout.md)) och du väljer en enhet i den konfigurerade enhetsgruppen återges sidan med en väljare som en del av URL:en.

I det här exemplet, när du redigerar en sida baserat på **Experience Page** och väljer iPhone 4 i emulatorn återges sidan med väljaren som `arctic-surfing-in-lofoten.smart.html` i stället för `arctic-surfing-in-lofoten.html`

Du kan även anropa sidan direkt med den här väljaren.

![chlimage_1-161](assets/chlimage_1-161.png)
