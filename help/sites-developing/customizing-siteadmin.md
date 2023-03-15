---
title: Anpassa webbplatskonsolen (Classic UI)
seo-title: Customizing the Websites Console (Classic UI)
description: Konsolen Administrera webbplatser kan utökas till att visa anpassade kolumner
seo-description: The Websites Administration console can be extended to display custom columns
uuid: 9163fdff-5351-477d-b91c-8a74f8b41d34
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: aeb37103-541d-4235-8a78-980b78c8de66
docset: aem65
exl-id: 2b9b4857-821c-4f2f-9ed9-78a1c9f5ac67
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# Anpassa webbplatskonsolen (Classic UI){#customizing-the-websites-console-classic-ui}

## Lägga till en anpassad kolumn i webbplatskonsolen (siteadmin) {#adding-a-custom-column-to-the-websites-siteadmin-console}

Konsolen Administrera webbplatser kan utökas till att visa anpassade kolumner. Konsolen byggs baserat på ett JSON-objekt som kan utökas genom att skapa en OSGI-tjänst som implementerar `ListInfoProvider` gränssnitt. En sådan tjänst ändrar JSON-objektet som skickas till klienten för att bygga konsolen.

I den här stegvisa självstudiekursen beskrivs hur du visar en ny kolumn i administrationskonsolen för webbplatser genom att implementera `ListInfoProvider` gränssnitt. Det består av följande steg:

1. [Skapa OSGI-tjänsten](#creating-the-osgi-service) och distribuera paketet som innehåller det till AEM.
1. (valfritt) [Testa den nya tjänsten](#testing-the-new-service) genom att utfärda ett JSON-anrop för att begära JSON-objektet som används för att skapa konsolen.
1. [Visa den nya kolumnen](#displaying-the-new-column) genom att utöka nodstrukturen för konsolen i databasen.

>[!NOTE]
>
>Den här självstudiekursen kan även användas för att utöka följande administrationskonsoler:
>
>* Digital Assets-konsolen
>* Community-konsolen
>


### Skapa OSGI-tjänsten {#creating-the-osgi-service}

The `ListInfoProvider` gränssnittet definierar två metoder:

* `updateListGlobalInfo`, för att uppdatera globala egenskaper för listan,
* `updateListItemInfo`, för att uppdatera ett listobjekt.

Argumenten för båda metoderna är:

* `request`, det associerade Sling HTTP-begäranobjektet,
* `info`, det JSON-objekt som ska uppdateras, som är den globala listan eller det aktuella listobjektet.
* `resource`, en Sling-resurs.

Exempelimplementeringen nedan:

* Lägger till en *stjärnad* egenskapen för varje objekt, som `true` om sidnamnet börjar med *e* och `false` i annat fall.

* Lägger till en *starredCount* som är global för listan och innehåller antalet stjärnlistobjekt.

Så här skapar du OSGI-tjänsten:

1. I CRXDE Lite [skapa ett paket](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle).
1. Lägg till exempelkoden nedan.
1. Bygg paketet.

Den nya tjänsten körs.

```java
package com.test;

import com.day.cq.commons.ListInfoProvider;
import com.day.cq.i18n.I18n;
import com.day.cq.wcm.api.Page;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;

@Component(metatype = false)
@Service(value = ListInfoProvider.class)
public class StarredListInfoProvider implements ListInfoProvider {

    private int count = 0;

    public void updateListGlobalInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        info.put("starredCount", count);
        count = 0; // reset for next execution
    }

    public void updateListItemInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        Page page = resource.adaptTo(Page.class);
        if (page != null) {
            // Consider starred if page name starts with 'e'
            boolean starred = page.getName().startsWith("e");
            if (starred) {
                count++;
            }
            I18n i18n = new I18n(request);
            info.put("starred", starred ? i18n.get("Yes") : i18n.get("No"));
        }
    }

}
```

>[!CAUTION]
>
>* Implementeringen bör, baserat på den angivna begäran och/eller resursen, avgöra om den ska lägga till informationen till JSON-objektet eller inte.
>* Om `ListInfoProvider` implementeringen definierar en egenskap som redan finns i svarsobjektet. Dess värde skrivs över av den som du anger.
>
>  Du kan använda [rangordning av tjänster](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) för att hantera körningsordningen för flera `ListInfoProvider` implementeringar.

### Testa den nya tjänsten {#testing-the-new-service}

När du öppnar administrationskonsolen för webbplatser och bläddrar igenom webbplatsen skickar webbläsaren ett ajax-anrop för att hämta JSON-objektet som används för att skapa konsolen. Om du till exempel bläddrar till `/content/geometrixx` mapp skickas följande begäran till AEM server för att bygga konsolen:

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

Så här kontrollerar du att den nya tjänsten körs efter att du har distribuerat paketet som innehåller den:

1. Peka webbläsaren på följande URL:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. Svaret ska visa de nya egenskaperna enligt följande:

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### Visa den nya kolumnen {#displaying-the-new-column}

Det sista steget består i att anpassa nodstrukturen i administrationskonsolen för webbplatser så att den nya egenskapen för alla Geometrixx visas genom att täcka över `/libs/wcm/core/content/siteadmin`. Gör så här:

1. Skapa nodstrukturen i CRXDE Lite `/apps/wcm/core/content` med noder av typen `sling:Folder` återspegla strukturen `/libs/wcm/core/content`.

1. Kopiera noden `/libs/wcm/core/content/siteadmin` och klistra in den nedan `/apps/wcm/core/content`.

1. Kopiera noden `/apps/wcm/core/content/siteadmin/grid/assets` till `/apps/wcm/core/content/siteadmin/grid/geometrixx` och ändrar dess egenskaper:

   * Ta bort **pageText**

   * Ange **pathRegex** till `/content/geometrixx(/.*)?`
Detta gör att stödrasterkonfigurationen blir aktiv för alla geometrixx-webbplatser.

   * Ange **storeProxySuffix** till `.pages.json`

   * Redigera **storeReaderFields** flervärdesegenskap och lägg till `starred` värde.

   * Om du vill aktivera MSM-funktioner lägger du till följande MSM-parametrar i egenskapen multi-String **storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. Lägg till en `starred` nod (av typ **nt:ostrukturerad**) nedan `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` med följande egenskaper:

   * **dataIndex**: `starred` av typen String

   * **header**: `Starred` av typen String

   * **xtype**: `gridcolumn` av typen String

1. (valfritt) Släpp de kolumner som du inte vill visa vid `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` är en mållös bana som som standard pekar på `/libs/wcm/core/content/siteadmin`.
Om du vill dirigera om den här till din version av siteadmin på `/apps/wcm/core/content/siteadmin` definiera egenskapen `sling:vanityOrder` att ha ett värde som är högre än det som definierats på `/libs/wcm/core/content/siteadmin`. Standardvärdet är 300, så allt högre är lämpligt.

1. Gå till administrationskonsolen för webbplatser och navigera till Geometrixx:
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. Den nya kolumnen anropades **Started** är tillgängligt och visar anpassad information enligt följande:

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>Om flera rutnätskonfigurationer matchar den begärda sökvägen som definieras av **pathRegex** egenskapen kommer den första att användas, och inte den mest specifika, vilket betyder att ordningen för konfigurationerna är viktig.

### Exempelpaket {#sample-package}

Resultatet av den här självstudiekursen finns i [Anpassa administrationskonsolen för webbplatser](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) paket på paketresurs.
