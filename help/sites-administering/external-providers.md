---
title: Analyser med externa leverantörer
seo-title: Analyser med externa leverantörer
description: Lär dig mer om Analytics med externa leverantörer.
seo-description: Lär dig mer om Analytics med externa leverantörer.
uuid: 31a773ca-901e-45f2-be8f-951c26f9dbc5
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bab465bc-1ff4-4f21-9885-e4a875c73a8d
docset: aem65
translation-type: tm+mt
source-git-commit: 0eda6ee61acf737abc91d1e5df731e719663b3f2

---


# Analyser med externa leverantörer {#analytics-with-external-providers}

Analyser kan ge dig viktig och intressant information om hur webbplatsen används.

Det finns olika färdiga konfigurationer för integrering med rätt tjänst, till exempel:

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

Du kan också konfigurera en egen instans av **Generic Analytics-kodfragment** för att definiera en ny tjänstkonfiguration.

Informationen samlas sedan in med små kodfragment som läggs till på webbsidorna. Exempel:

>[!CAUTION]
>
>Skript får inte omslutas av `script` taggar.

```
var _gaq = _gaq || [];
_gaq.push(['_setAccount', 'UA-XXXXX-X']);
_gaq.push(['_trackPageview']);

(function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
})();
```

Sådana fragment gör det möjligt att samla in data och generera rapporter. De faktiska data som samlas in beror på providern och vilket kodfragment som används. Exempel på statistik är:

* hur många besökare som helst
* hur många sidor som besöktes
* söktermer som används
* landningssidor

>[!CAUTION]
>
>Demosplatsen Geometrixx-Outdoor är konfigurerad så att attributen som finns i Sidegenskaper läggs till i HTML-källkoden (precis ovanför `</html>` sluttaggen) i motsvarande `js` skript.

>Om dina egna `/apps` inte ärver från standardsidkomponenten ( `/libs/foundation/components/page`) måste du (eller dina utvecklare) se till att motsvarande `js` skript inkluderas, t.ex. genom att inkludera `cq/cloudserviceconfigs/components/servicescomponents`eller använda en liknande mekanism.
>
>Utan detta kommer ingen av tjänsterna (Generic, Analytics, Target, etc.) att fungera.

## Skapa en ny tjänst med ett allmänt kodfragment {#creating-a-new-service-with-a-generic-snippet}

För den grundläggande konfigurationen:

1. Öppna **verktygskonsolen** .
1. Expandera **Cloud Services Configurations** i den vänstra rutan.
1. Dubbelklicka på **Generic Analytics-kodfragment** för att öppna sidan:

   ![](assets/analytics_genericoverview.png)

1. Klicka på + för att lägga till en ny konfiguration med dialogrutan. åtminstone tilldela ett namn, till exempel Google Analytics:

   ![](assets/analytics_addconfig.png)

1. Klicka på **Skapa**, så öppnas fragmentdialogrutan omedelbart - klistra in lämpligt javascript-fragment i fältet:

   ![](assets/analytics_snippet.png)

1. Spara genom att klicka på **OK** .

## Använda din nya tjänst på sidor {#using-your-new-service-on-pages}

När du har skapat tjänstkonfigurationen behöver du nu konfigurera de sidor som krävs för att använda den:

1. Navigera till sidan.
1. Öppna **Sidegenskaperna** från sidosparken och sedan fliken **Cloud-tjänster** .
1. Klicka på **Lägg till tjänst** och välj sedan önskad tjänst; till exempel **kodavsnittet** för allmän analys:

   ![](assets/analytics_selectservice.png)

1. Spara genom att klicka på **OK** .
1. Du kommer nu tillbaka till fliken **Cloud-tjänster** . Utdraget för **allmän analys** visas nu med meddelandet `Configuration reference missing`. Använd listrutan för att välja en specifik tjänstinstans; till exempel google-analys:

   ![](assets/analytics_selectspecificservice.png)

1. Spara genom att klicka på **OK** .

   Utdraget visas nu om du visar sidans sidkälla.

   Efter en lämplig tidsperiod kan du visa den statistik som har samlats in.

   >[!NOTE]
   Om konfigurationen är kopplad till en sida som har underordnade sidor, ärvs tjänsten även av dessa sidor.
