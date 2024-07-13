---
title: Adaptiv mallåtergivning
description: Lär dig mer om adaptiv mallrendering i Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 2%

---

# Adaptiv mallåtergivning{#adaptive-template-rendering}

Med den adaptiva mallåtergivningen kan du hantera en sida med variationer. Den här funktionen är ursprungligen användbar när du vill leverera olika utdataformat för mobila enheter (till exempel från telefoner till smarttelefoner), men den är användbar när du vill leverera HTML till olika enheter som behöver olika märkningar eller HTML.

## Ökning {#overview}

Mallar byggs runt ett responsivt rutnät, och sidor som skapas baserat på dessa mallar är helt responsiva och justeras automatiskt till visningsrutan på klientenheten. Med verktygsfältet Emulator i sidredigeraren kan man rikta layouten till specifika enheter.

Det går också att skapa mallar som har stöd för adaptiv återgivning. När enhetsgrupper är korrekt konfigurerade återges sidan med en annan väljare i URL:en när en enhet väljs i emulatorläge. Om du använder en väljare kan en viss sidåtergivning anropas direkt via webbadressen.

Kom ihåg när du konfigurerar enhetsgrupper:

* Alla enheter måste finnas i minst en enhetsgrupp.
* En enhet kan finnas i flera enhetsgrupper.
* Eftersom enheter kan finnas i flera enhetsgrupper kan väljarna kombineras.
* Kombinationen av väljare utvärderas uppifrån och ned när de sparas i databasen.

>[!NOTE]
>
>Enhetsgruppen **Responsiva enheter har aldrig någon väljare eftersom enheter som identifieras som kompatibla med responsiv design antas inte behöva någon anpassad layout

## Konfiguration {#configuration}

Anpassningsbara återgivningsväljare kan konfigureras för befintliga enhetsgrupper eller för [grupper som du själv har skapat.](/help/sites-developing/mobile.md#device-groups)

I det här exemplet ska du konfigurera den befintliga enhetsgruppen **Smarta telefoner** så att den har en adaptiv återgivningsväljare som en del av mallen **Experience Page** i We.Retail.

1. Redigera enhetsgruppen som kräver en adaptiv väljare i `http://localhost:4502/miscadmin#/etc/mobile/groups`

   Ange alternativet **Inaktivera emulatorn** och spara.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Väljaren är tillgänglig för **BlackBerry®** och **iPhone 4** förutsatt att enhetsgruppen **Smart Phone** läggs till i mall- och sidstrukturerna i följande steg.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. Använd CRXDE Lite för att tillåta att enhetsgruppen används i mallen genom att lägga till den i strängegenskapen `cq:deviceGroups` med flera värden i mallstrukturen.

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   Om du till exempel vill lägga till enhetsgruppen Smart Phone:

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. Använd CRXDE Lite för att tillåta att enhetsgruppen används på din plats genom att lägga till den i strängegenskapen `cq:deviceGroups` med flera värden i platsens struktur.

   `/content/<your-site>/jcr:content`

   Om du till exempel vill tillåta enhetsgruppen **Smart Phone**:

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

När du nu använder [emulatorn](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) i sidredigeraren (till exempel när du [ändrar layouten](/help/sites-authoring/responsive-layout.md)) och väljer en enhet i den konfigurerade enhetsgruppen, återges sidan med en väljare som en del av URL:en.

I det här exemplet återges sidan med väljaren som `arctic-surfing-in-lofoten.smart.html` i stället för `arctic-surfing-in-lofoten.html` när du redigerar en sida baserat på mallen **Experience Page** och väljer iPhone 4 i emulatorn

Du kan även anropa sidan direkt med den här väljaren.

![chlimage_1-161](assets/chlimage_1-161.png)
