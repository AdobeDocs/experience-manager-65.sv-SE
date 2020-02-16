---
title: Adaptiv mallåtergivning
seo-title: Adaptiv mallåtergivning
description: 'null'
seo-description: 'null'
uuid: 97226ae1-e42a-40ae-a5e0-886cd77559d8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f5cb0e98-0d6e-4f14-9b94-df1a9d8cbe5b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Adaptiv mallåtergivning{#adaptive-template-rendering}

Med den adaptiva mallåtergivningen kan du hantera en sida med variationer. Den här funktionen är ursprungligen användbar för att leverera olika HTML-utdata för mobila enheter (t.ex. funktionstelefon eller smarttelefon), men den är användbar när upplevelser måste levereras till olika enheter som behöver olika märkningar eller HTML-utdata.

## Översikt {#overview}

Mallar byggs vanligtvis runt ett responsivt rutnät, och sidor som skapas baserat på dessa mallar är helt responsiva och justeras automatiskt till visningsrutan på klientenheten. Med hjälp av verktygsfältet Emulator i sidredigeraren kan författare rikta layouten till specifika enheter.

Det går också att skapa mallar som stöder adaptiv återgivning. När enhetsgrupper är korrekt konfigurerade återges sidan med en annan väljare i URL:en när en enhet väljs i emulatorläge. Om du använder en väljare kan en viss sidåtergivning anropas direkt via webbadressen.

Kom ihåg när du konfigurerar enhetsgrupper:

* Alla enheter måste finnas i minst en enhetsgrupp.
* En enhet kan finnas i flera enhetsgrupper.
* Eftersom enheter kan finnas i flera enhetsgrupper kan väljarna kombineras.
* Kombinationen av väljare utvärderas uppifrån och ned när de sparas i databasen.

>[!NOTE]
>
>Enhetsgruppen **Responsiva enheter** kommer aldrig att ha någon väljare eftersom enheter som identifieras som kompatibla med responsiv design antas inte behöva någon adaptiv layout

## Konfiguration {#configuration}

Anpassningsbara återgivningsväljare kan konfigureras för befintliga enhetsgrupper eller för [grupper som du själv har skapat.](/help/sites-developing/mobile.md#device-groups)

I det här exemplet ska vi konfigurera den befintliga enhetsgruppen **Smarta telefoner** så att den har en adaptiv återgivningsväljare som en del av **Experience Page** -mallen i We.Retail.

1. Redigera enhetsgruppen som kräver en adaptiv väljare i `http://localhost:4502/miscadmin#/etc/mobile/groups`

   Ange alternativet **Inaktivera emulator** och spara.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Väljaren är tillgänglig för **Blackberry** och **iPhone 4** förutsatt att enhetsgruppen **Smart Phone** läggs till i mall- och sidstrukturen i följande steg.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. Med CRX DE Lite kan du tillåta att enhetsgruppen används i mallen genom att lägga till den i egenskapen för flervärdessträngen `cq:deviceGroups` i mallstrukturen.

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   Om vi till exempel vill lägga till enhetsgruppen Smart Phone:

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. Med CRX DE Lite kan du tillåta att enhetsgruppen används på din webbplats genom att lägga till den i egenskapen för flervärdessträngen `cq:deviceGroups` i webbplatsens struktur.

   `/content/<your-site>/jcr:content`

   Om vi till exempel vill tillåta enhetsgruppen **Smart Phone** :

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

När du nu använder [emulatorn](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) i sidredigeraren (till exempel när du [ändrar layouten](/help/sites-authoring/responsive-layout.md)) och väljer en enhet i den konfigurerade enhetsgruppen, återges sidan med en väljare som en del av URL-adressen.

När du redigerar en sida som är baserad på mallen **Experience Page** och väljer iPhone 4 i emulatorn återges sidan med väljaren som `arctic-surfing-in-lofoten.smart.html``arctic-surfing-in-lofoten.html`

Du kan även anropa sidan direkt med den här väljaren.

![chlimage_1-161](assets/chlimage_1-161.png)

