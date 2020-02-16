---
title: Konfigurera din sida för gruppredigering av sidegenskaper
seo-title: Konfigurera din sida för gruppredigering av sidegenskaper
description: Med gruppredigering av sidegenskaper kan du redigera egenskaperna för flera sidor samtidigt
seo-description: Med gruppredigering av sidegenskaper kan du redigera egenskaperna för flera sidor samtidigt
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera din sida för gruppredigering av sidegenskaper {#configuring-your-page-for-bulk-editing-of-page-properties}

[Med gruppredigering av sidegenskaper](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) kan du redigera egenskaperna för flera sidor samtidigt.

På grund av möjligheten att det finns olika värden är sidegenskaperna inte aktiverade för massredigering som standard. De måste vara uttryckligt vitlistade (aktiverade). När du definierar vilka sidegenskaper som ska vara tillgängliga för massredigering måste du ta hänsyn till vissa konsekvenser, till exempel:

* Vissa fält är vanligtvis unika. till exempel en sidrubrik. Du måste bestämma om det är meningsfullt att aktivera sådana fält för massredigering, när ett värde ska användas.
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
>Massredigering är också tillgängligt för Assets. Den är mycket lik, men skiljer sig på några punkter. Mer information finns i [Redigera egenskaper för flera resurser](/help/assets/managing-multiple-assets.md) . Du kan anpassa fälten i redigeraren för massmetadata för resurser med [schemaredigeraren](/help/assets/metadata-schemas.md).

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



Fält är aktiverade i sidkomponenten (*inte* i mallen):

1. Om du använder CRXDE Lite (eller en motsvarande metod) öppnar du sidkomponenten.

   Exempel: `/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >I det här exemplet antas att kärnkomponenterna har installerats på instansen, vilket är fallet om instansen körs med exempelinnehållet We.Retail. Mer information finns i dokumentationen [för](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) kärnkomponenter.

1. Navigera till det obligatoriska fältet i `cq:dialog` definitionen.
1. Definiera följande egenskap på fältnoden:

   * **Namn**: `allowBulkEdit`
   * **Typ**: `Boolean`
   * **Värde**: `true`
   Exempel: för standardkomponenten [för](/help/sites-authoring/default-components-foundation.md)sidans grund:

   `/libs/foundation/components/page`

   Egenskapen skulle definieras för:

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >Du ***får*** inte ändra något i `/libs` banan.
   >
   >Detta beror på att innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan mycket väl skrivas över när du använder en snabbkorrigering eller ett funktionspaket).
   >
   >Den rekommenderade metoden för konfiguration och andra ändringar är:
   >
   >    1. Återskapa önskat objekt (t.ex. som det finns i `/libs`) under `/apps`
   >    1. Gör ändringar i `/apps`


1. Välj **Spara alla** om du vill behålla uppdateringarna.

