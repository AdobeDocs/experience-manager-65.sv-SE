---
title: Konfigurera din sida för gruppredigering av sidegenskaper
description: Med gruppredigering av sidegenskaper kan du redigera egenskaperna för flera sidor samtidigt
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 1787e643-fc8e-40e0-8e14-97b222a7c320
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Konfigurera din sida för gruppredigering av sidegenskaper {#configuring-your-page-for-bulk-editing-of-page-properties}

[Massredigering av sidegenskaper](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) Med kan du redigera egenskaper för flera sidor samtidigt.

På grund av möjligheten att det finns olika värden är sidegenskaperna inte aktiverade för massredigering som standard. De måste vara uttryckligen tillåtna (aktiverade). När du definierar vilka sidegenskaper som ska vara tillgängliga för massredigering måste du ta hänsyn till vissa konsekvenser, till exempel:

* Vissa fält är vanligtvis unika, till exempel en sidtitel. Bestäm om det är meningsfullt att aktivera sådana fält för massredigering, när ett värde ska användas.
* Vissa fält kan ha flera värden - detta kräver en meningsfull representation vid återgivningen.

  Till exempel en kryssruta som anger&quot;Klart för publikation&quot;. Detta kan ha flera värden före gruppredigering (t.ex. ready, in-review, in-progress).

>[!CAUTION]
>
>Massredigering av sidegenskaper är:
>
>* Inte tillgängligt i det klassiska användargränssnittet.
>* Inte tillgängligt för sidor i en live-kopia.
>* Endast tillgängligt för sidor med samma resurstyp.
>

>[!NOTE]
>
>Massredigering är också tillgängligt för Assets. Den är mycket lik, men skiljer sig på några punkter. Se [Redigera egenskaper för flera resurser](/help/assets/metadata.md) för fullständig information. Du kan anpassa fälten i redigeraren för massmetadata för resurser med hjälp av [Schemaredigerare](/help/assets/metadata-schemas.md).

## Aktivera ett fält {#enabling-a-field}

>[!NOTE]
>
>Vissa fält kan ha flera värden - detta kräver en meningsfull representation vid återgivningen. Därför bör du bara aktivera följande fälttyper:
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>

Fält är aktiverade i sidkomponenten (*not* på mallen):

1. Öppna sidkomponenten med CRXDE Lite (eller en motsvarande metod).

   Till exempel: `/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >I det här exemplet antas att kärnkomponenterna har installerats på instansen, vilket är fallet om instansen körs med exempelinnehållet We.Retail. Se [Dokumentation för kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) för mer information.

1. Navigera till det obligatoriska fältet i `cq:dialog` definition.
1. Definiera följande egenskap på fältnoden:

   * **Namn**: `allowBulkEdit`
   * **Typ**: `Boolean`
   * **Värde**: `true`

   Till exempel för standardsidan [Foundation-komponent](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   Egenskapen skulle definieras för:

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >Du ***måste*** ändrar ingenting i dialogrutan `/libs` bana.
   >
   >Detta beror på innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan mycket väl skrivas över när du installerar en snabbkorrigering eller ett funktionspaket).
   >
   >Den rekommenderade metoden för konfiguration och andra ändringar är:
   >
   >    1. Återskapa önskat objekt (d.v.s. som det finns i `/libs`) under `/apps`
   >    1. Gör ändringar i `/apps`

1. Välj **Spara alla** för att behålla uppdateringarna.
