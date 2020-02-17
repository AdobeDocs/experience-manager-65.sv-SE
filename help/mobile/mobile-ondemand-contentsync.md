---
title: Mobil med innehållssynkronisering
seo-title: Mobil med innehållssynkronisering
description: Följ den här sidan om du vill veta mer om Innehållssynkronisering. Sidor som har skapats i AEM kan användas som appinnehåll, även när enheten är offline. Eftersom AEM-sidor dessutom bygger på webbstandarder fungerar de på olika plattformar så att du kan bädda in dem i alla inbyggda wrapper. Den här strategin minskar utvecklingsinsatserna och gör att du enkelt kan uppdatera appinnehåll.
seo-description: Följ den här sidan om du vill veta mer om Innehållssynkronisering. Sidor som har skapats i AEM kan användas som appinnehåll, även när enheten är offline. Eftersom AEM-sidor dessutom bygger på webbstandarder fungerar de på olika plattformar så att du kan bädda in dem i alla inbyggda wrapper. Den här strategin minskar utvecklingsinsatserna och gör att du enkelt kan uppdatera appinnehåll.
uuid: 11f74cc5-99a5-4186-9b60-b19351305432
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 8fb70ca4-86fc-477d-9773-35b84d5e85a8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Mobil med innehållssynkronisering{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Använd Innehållssynkronisering för att paketera innehåll så att det kan användas i inbyggda mobilprogram. Sidor som har skapats i AEM kan användas som appinnehåll, även när enheten är offline. Eftersom AEM-sidor dessutom bygger på webbstandarder fungerar de på olika plattformar så att du kan bädda in dem i alla inbyggda wrapper. Den här strategin minskar utvecklingsinsatserna och gör att du enkelt kan uppdatera appinnehåll.

I ramverket för innehållssynkronisering skapas en arkivfil som innehåller webbinnehållet. Innehållet kan vara allt från enkla sidor, bilder, PDF-filer eller hela webbprogram. API:t för innehållssynkronisering ger åtkomst till arkivfilen från mobilappar eller byggprocesser så att innehållet kan hämtas och inkluderas i appen.

Följande stegsekvens visar ett typiskt användningsfall för Innehållssynkronisering:

1. AEM-utvecklaren skapar en konfiguration för innehållssynkronisering som anger vilket innehåll som ska inkluderas.
1. Innehållssynkroniseringsramverket samlar in och cachelagrar innehållet.
1. På en mobil enhet startas mobilprogrammet och begär innehåll från servern, som levereras i en ZIP-fil.
1. Klienten packar upp ZIP-innehållet i det lokala filsystemet. Mappstrukturen i ZIP-filen simulerar de sökvägar som en klient (t.ex. en webbläsare) normalt skulle begära från servern.
1. Klienten öppnar innehållet i en inbäddad webbläsare eller använder det på något annat sätt.
1. Senare begär klienten uppdaterat innehåll från servern. Innehållssynkroniseringsramverket innehåller inkrementella uppdateringar som minskar hämtningsstorleken och hämtningstiden, vilket kan vara viktigt för mobila enheter på grund av begränsad bandbredd eller begränsade datavolymer.

## Utveckla hanterare för innehållssynkronisering {#developing-the-content-sync-handlers}

Några av riktlinjerna för utveckling av Hanterare för innehållssynkronisering är följande:

* Hanterare måste implementera *com.day.cq.contentsync.handler.ContentUpdateHandler* (antingen direkt eller genom att utöka en klass som gör det)
* Hanterare kan utöka *com.adobe.cq.moile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Hanteraren får bara rapportera true om den uppdaterar ContentSync-cachen. Felaktig rapportering av true innebär att AEM skapar en uppdatering när en uppdatering inte faktiskt gjordes.
* Hanteraren bör bara uppdatera cacheminnet om innehållet faktiskt ändras. Skriv inte till cacheminnet om en vit inte behövs. Detta resulterar i att en onödig uppdatering skapas.

>[!NOTE]
>
>Aktivera *ContentSync-felsökningsloggning* via OSGI-loggkonfigurationer på paketet *com.day.cq.contentsync*. Detta gör att du kan spåra vad hanterarna har kört och om de har uppdaterat cachen och rapporterat att cachen har uppdaterats.

## Konfigurera innehåll för innehållssynkronisering {#configuring-the-content-sync-content}

Skapa en konfiguration för innehållssynkronisering för att ange innehållet i ZIP-filen som skickas till klienten. Du kan skapa valfritt antal konfigurationer för innehållssynkronisering. Varje konfiguration har ett namn för identifieringsändamål.

Om du vill skapa en konfiguration för innehållssynkronisering lägger du till en `cq:ContentSyncConfig` nod i databasen med `sling:resourceType` egenskapen inställd på `contentsync/config`. Noden kan finnas var som helst i databasen, men noden måste vara tillgänglig för användare på AEM-publiceringsinstansen. `cq:ContentSyncConfig` Därför bör du lägga till noden nedan `/content`.

Om du vill ange innehållet i ZIP-filen för innehållssynkronisering lägger du till underordnade noder i cq:ContentSyncConfig-noden. Följande egenskaper för varje underordnad nod identifierar ett innehållsobjekt som ska inkluderas och hur det bearbetas när det läggs till:

* `path`: Innehållets plats.
* `type`: Namnet på den konfigurationstyp som ska användas för bearbetning av innehållet. Flera typer finns tillgängliga och beskrivs i avsnittet *Konfigurationstyper*.

Mer information finns i *Exempel på konfiguration* av innehållssynkronisering.

När du har skapat konfigurationen för innehållssynkronisering visas den i konsolen för innehållssynkronisering.

>[!NOTE]
>
>Innehållssynkroniseringsramverket kontrollerar inte att beroenden av resurser och designrelaterade filer ingår i innehålls-Synkroniseringspaket. Se till att du inkluderar alla nödvändiga filer i ZIP-filen.

### Konfigurera åtkomst till hämtningar för innehållssynkronisering {#configuring-access-to-content-sync-downloads}

Ange en användare eller grupp som kan hämtas från Innehållssynkronisering. Du kan konfigurera standardanvändaren eller standardgruppen som kan hämtas från alla cacheminnen för innehållssynkronisering, och du kan åsidosätta standardinställningen och konfigurera åtkomst för en viss konfiguration för innehållssynkronisering.

När AEM är installerat kan medlemmar i administratörsgruppen hämta från innehållssynkronisering som standard.

#### Ange standardåtkomst för hämtning av innehållssynkronisering {#setting-the-default-access-for-content-sync-downloads}

Tjänsten Day CQ Content Sync Manager styr åtkomsten till Content Sync. Konfigurera den här tjänsten för att ange den användare eller grupp som kan hämtas från innehållssynkronisering som standard.

Om du [konfigurerar tjänsten med webbkonsolen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)anger du namnet på användaren eller gruppen som värdet för egenskapen Authorizable för reservcache.

Om du [konfigurerar i databasen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)använder du följande information om tjänsten:

* PID: com.day.cq.contentsync.impl.ContentSyncManagerImpl
* Egenskapsnamn: contentsync.fallback.authzable

#### Åsidosätta hämtningsåtkomst för en cache för innehållssynkronisering {#overriding-download-access-for-a-content-sync-cache}

Om du vill konfigurera hämtningsåtkomst för en viss konfiguration för innehållssynkronisering lägger du till följande egenskap i `cq:ContentSyncConfig` noden:

* Namn: auktoriseringsbar
* Typ:Sträng
* Värde: Namnet på den användare eller grupp som kan hämtas.

Med din app kan användare till exempel installera uppdateringar direkt från innehållssynkronisering. Om du vill att alla användare ska kunna hämta uppdateringen anger du värdet för egenskapen authorized till `everyone`.

Om `cq:ContentSyncConfig` noden inte har någon auktoriseringsbar egenskap avgör standardanvändaren eller gruppen som är konfigurerad för auktoriseringsbar reservcache-egenskap för tjänsten Day CQ Content Sync Manager vem som kan hämta.

### Konfigurera användaren för uppdatering av en cache för innehållssynkronisering {#configuring-the-user-for-updating-a-content-sync-cache}

När en användare uppdaterar cachen för innehållssynkronisering utför ett specifikt användarkonto åtgärden åt användaren. Den anonyma användaren uppdaterar alla cacheminnen för innehållssynkronisering som standard.

Du kan åsidosätta standardanvändaren och ange en användare eller grupp som uppdaterar en viss cache för innehållssynkronisering.

Om du vill åsidosätta standardanvändaren anger du en användare eller grupp som utför uppdateringar för en specifik konfiguration för innehållssynkronisering genom att lägga till följande egenskap i cq:ContentSyncConfig-noden:

* Namn: `updateuser`
* Typ: `String`
* Värde: Namnet på den användare eller grupp som kan utföra uppdateringarna.

Om `cq:ContentSyncConfig` noden inte har någon `updateuser` egenskap uppdaterar `anonymous` standardanvändaren cachen.

### Konfigurationstyper {#configuration-types}

Bearbetningen kan omfatta allt från rendering av enkel JSON till fullständig rendering av sidor, inklusive deras refererade resurser. I det här avsnittet visas tillgängliga konfigurationstyper och deras specifika parametrar:

**kopiera** Kopiera bara filer och mappar.

* **path** - Om sökvägen pekar på en enda fil kopieras bara filen. Om den pekar på en mapp (inklusive sidnoder) kopieras alla filer och mappar nedan.

**innehåll** Återge innehåll med standardbearbetning av [Sling-begäran](/help/sites-developing/the-basics.md#sling-request-processing).

* **path** - Sökväg till resurs som ska vara utdata.
* **extension** - Extension that should be used in the request. Vanliga exempel är *html* och *json*, men alla andra tillägg är möjliga.

* **väljare** - valfria väljare avgränsade med punkt. Vanliga exempel är *touch* för återgivning av mobilversioner av en sida eller *oändlighet* för JSON-utdata.

**clientlib** Paketera ett JavaScript- eller CSS-klientbibliotek.

* **path** - Sökväg till klientbibliotekets rot.
* **extension** - Type of client library. Detta bör anges till *js* eller *css* för tillfället.

**resurser**

Samla in ursprungliga återgivningar av resurser.

* **path** - Sökväg till en resursmapp under /content/dam.

**image** Samla in en bild.

* **path** - Sökväg till en bildresurs.

Bildtypen används för att inkludera logotypen We Retail i zip-filen.

**sidor** Återge AEM-sidor och samla in refererade resurser.

* **path** - Path to a page.
* **extension** - Extension that should be used in the request. För sidor är detta nästan alltid *html*, men andra är fortfarande möjliga.

* **väljare** - valfria väljare avgränsade med punkt. Vanliga exempel är *touch* för återgivning av mobilversioner av en sida.

* **deep** - Valfri boolesk egenskap som avgör om underordnade sidor också ska inkluderas. The default value is *true.*

* **includeImages** - Valfri boolesk egenskap som avgör om bilder ska inkluderas. The default value is *true*.

   Som standard beaktas endast bildkomponenter med en resurstyp för grund/komponenter/bild. Du kan lägga till fler resurstyper genom att konfigurera uppdateringshanteraren **för CQ WCM Pages för** Dag i webbkonsolen.

**rewrite** The rewrite node define how the links are rewritten in the exported page. De omskrivna länkarna kan antingen peka på filerna som finns i ZIP-filen eller på resurserna på servern.

Noden måste `rewrite` finnas under `page` noden.

Noden kan ha en eller flera av följande egenskaper: `rewrite`

* `clientlibs`: skriver om klientlibs-banor.

* `images`: skriver om bildbanor.
* `links`: skriver om länksökvägar.

Varje egenskap kan ha något av följande värden:

* `REWRITE_RELATIVE`: skriver om sökvägen med en relativ position till HTML-filen på sidan i filsystemet.

* `REWRITE_EXTERNAL`: skriver om sökvägen genom att peka på resursen på servern med hjälp av tjänsten [AEM](/help/sites-developing/externalizer.md)Externalizer.

Med AEM-tjänsten **PathRewriterTransformerFactory** kan du konfigurera de specifika html-attribut som ska skrivas om. Tjänsten kan konfigureras i webbkonsolen och har en konfiguration för varje egenskap i `rewrite` noden: `clientlibs`, `images` och `links`.

Den här funktionen lades till i AEM 5.5.

### Exempel på konfiguration för innehållssynkronisering {#example-content-sync-configuration}

I listan nedan visas ett exempel på en konfiguration för innehållssynkronisering.

```xml
+ weretail_go [cq:ContentSyncConfig]
  - sling:resourceType = "contentsync/config"

  + etc.designs.default [nt:unstructured]
    - path = "/etc/designs/default"
    - type = "copy"

  + etc.designs.mobile [nt:unstructured]
    - path = "/etc/designs/mobile"
    - type = "copy"

  + events.plist [nt:unstructured]
    - path = "/content/weretail_mobile/en/events/jcr:content/par/events"
    - type = "content"
    - extension = "plist"

  + events.touch.html [nt:unstructured]
    - path = "/content/weretail_mobile/en/events"
    - type = "pages"
    - extension = "html"
    - selector = "touch"

  + logo [nt:unstructured]
    - path = "/etc/designs/mobile/jcr:content/mobilecontentpage/logo"
    - type = "logo"

  + manifest [nt:unstructured]
    - indexPage = "/content/weretail_mobile/en/events.touch.html"
    - metadataPlist = "/content/weretail_mobile/en/events/_jcr_content/par/events.plist"

  + ...
```

**etc.designs.default och osv.designs.mobile** De två första posterna i konfigurationen bör vara ganska tydliga. Eftersom vi ska ta med ett antal mobilsidor behöver vi de relaterade designfilerna nedan /etc/designs. Och eftersom ingen extra bearbetning behövs räcker det med en kopia.

**events.plist** Den här posten är lite speciell. Som nämndes i inledningen bör programmet tillhandahålla en kartvy med markörer för händelsernas platser. Vi kommer att tillhandahålla nödvändig platsinformation som en separat fil i PLIST-format. För att detta ska fungera har händelselistkomponenten som används på indexsidan ett skript som heter plist.jsp. Skriptet körs när komponentens resurs begärs med tillägget .plist. Som vanligt anges komponentsökvägen i egenskapen path och typen ställs in på content eftersom vi vill utnyttja bearbetningen [av](/help/sites-developing/the-basics.md#sling-request-processing)Sling-begäran.

**events.touch.html** Nästa visar de faktiska sidorna som visas i appen. Egenskapen path ställs in på händelsens rotsida. Alla händelsesidor under den sidan inkluderas också eftersom egenskapen deep har standardvärdet true. Vi använder sidor som konfigurationstyp, så att alla bilder eller andra filer som kan refereras från en bild eller en nedladdningskomponent på en sida inkluderas. Om du dessutom ställer in pekväljaren får vi en mobilversion av sidorna. Konfigurationen i funktionspaketet innehåller fler poster av den här typen, men utelämnas för enkelhetens skull här.

**logo** Logotypkonfigurationen har inte nämnts hittills och är ingen av de inbyggda typerna. Ramverket för innehållssynkronisering är dock delvis utökningsbart och det är ett exempel på det, som kommer att behandlas i nästa avsnitt.

**manifest** Det är ofta önskvärt att ta med någon typ av metadata i zip-filen, till exempel startsidan för innehållet. Om du däremot hårdkodar sådan information kan du inte ändra den senare. Innehållssynkroniseringsramverket stöder det här användningsexemplet genom att söka efter en manifestnod i konfigurationen, som bara identifieras med namn och som inte kräver någon konfigurationstyp. Alla egenskaper som definieras på den aktuella noden läggs till i en fil, som också kallas manifest och finns i zip-filens rot.

I exemplet ska händelselistsidan vara den inledande sidan. Den här informationen finns i egenskapen **indexPage** och kan därför enkelt ändras när som helst. En andra egenskap definierar sökvägen till filen *events.plist* . Som vi kommer att se senare kan klientprogrammet nu läsa manifestet och agera utifrån det.

När konfigurationen är klar kan innehållet laddas ned med en webbläsare eller en annan HTTP-klient, eller om du utvecklar för iOS kan du använda det dedikerade WAppKitSync-klientbiblioteket. Hämtningsplatsen består av konfigurationens sökväg och tillägget *.zip* , t.ex. när du arbetar med en lokal AEM-instans: *http://localhost:4502/content/weretail_go.zip*

### Konsolen Innehållssynkronisering {#the-content-sync-console}

I konsolen Innehållssynkronisering visas alla konfigurationer för innehållssynkronisering i databasen (alla noder av typen `cq:ContentSyncConfig`) och för varje konfiguration kan du göra följande:

* Uppdatera cachen.
* Rensa cachen.
* Ladda ned en komplett zip.
* Ladda ned en diff-zip mellan idag och ett specifikt datum och en viss tid.

Det kan vara användbart för utveckling och felsökning.

Konsolen finns på:

`http://localhost:4502/libs/cq/contentsync/content/console.html`

Den ser ut så här:

![chlimage_1-50](assets/chlimage_1-50.png)

### Utöka ramverket för innehållssynkronisering {#extending-the-content-sync-framework}

Även om antalet konfigurationsalternativ redan är ganska många kanske det inte täcker alla krav som gäller ditt specifika användningsfall. I det här avsnittet beskrivs tilläggen för ramverket för innehållssynkronisering och hur du skapar anpassade konfigurationstyper.

För varje konfigurationstyp finns det en *Content Update Handler*, som är en OSGi-komponentfabrik som är registrerad för den specifika typen. Hanterarna samlar in, bearbetar och lägger till innehåll i ett cacheminne som underhålls av ramverket för innehållssynkronisering. Implementera följande gränssnitt eller abstrakt basklass:

* `com.day.cq.contentsync.handler.ContentUpdateHandler` - Gränssnitt som alla uppdateringshanterare måste implementera
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - en abstrakt klass som förenklar återgivningen av resurser med Sling

Registrera klassen som OSGi-komponentfabrik och distribuera den i OSGi-behållaren i ett paket. Detta kan du göra med plugin-programmet [för](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html) Maven SCR med hjälp av JavaDoc-taggar eller anteckningar. I följande exempel visas JavaDoc-versionen:

```java
/*
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/customtype"
 */
public class CustomTypeUpdateHandler implements ContentUpdateHandler {
    // add your code here
}

/*
 * @scr.component metatype="no" inherit="true"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/othertype"
 */
public class OtherTypeUpdateHandler extends AbstractSlingResourceUpdateHandler {
    // add your code here
}
```

Observera att *fabriksdefinitionen* innehåller det gemensamma gränssnittet och den anpassade typen separerad med snedstreck. Den här strategin gör att innehållssynkroniseringsramverket kan hitta och skapa en instans av din anpassade klass som känner igen den anpassade typen i en konfigurationspost. I nästa avsnitt finns ett konkret exempel på en anpassad uppdateringshanterare.

>[!CAUTION]
>
>När du bygger vidare på basklassen AbstractSlingResourceUpdateHandler måste du lägga till den *ärvda* definitionen. Annars kommer OSGi-behållaren inte att ange de nödvändiga referenserna som deklareras i basklassen.

### Implementera en anpassad uppdateringshanterare {#implementing-a-custom-update-handler}

På varje sida för e-butiksmobilen finns en logotyp i det övre vänstra hörnet som vi förstås vill inkludera i zip-filen. För cacheoptimering refererar inte AEM till bildfilens verkliga plats i databasen, vilket förhindrar oss från att bara använda konfigurationstypen för **kopian** . Vi måste istället tillhandahålla en egen **logotypkonfigurationstyp** som gör bilden tillgänglig på den plats som AEM begär. I följande kodexempel visas den fullständiga implementeringen av hanteraren för uppdatering av logotyp:

#### LogoUpdateHandler.java {#logoupdatehandler-java}

```java
package com.day.cq.wcm.apps.weretail.impl;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.day.cq.commons.jcr.JcrUtil;
import com.day.cq.contentsync.config.ConfigEntry;
import com.day.cq.contentsync.handler.ContentUpdateHandler;
import com.day.cq.wcm.foundation.Image;
import com.day.text.Text;

/**
 * The <code>LogoUpdateHandler</code> is used to update the content sync cache
 * with a page logo added using a logo component.
 *
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/logo"
 */
public class LogoUpdateHandler implements ContentUpdateHandler {

    private static final Logger log = LoggerFactory.getLogger(LogoUpdateHandler.class);

    /** @scr.reference policy="static" */
    protected JcrResourceResolverFactory resolverFactory;

    public boolean updateCacheEntry(ConfigEntry configEntry, Long lastUpdated, String configCacheRoot, Session admin, Session session) {
        ResourceResolver resolver = resolverFactory.getResourceResolver(admin);
        Resource resource = resolver.getResource(configEntry.getContentPath());

        Image img = new Image(resource);
        img.setItemName(Image.NN_FILE, "image");
        img.setItemName(Image.PN_REFERENCE, "imageReference");
        img.setSelector("img");

        try {
            if(img.getLastModified() == null || lastUpdated < img.getLastModified().getTime().getTime()) {
                String src = img.getSrc();
                String parentPath = configCacheRoot + Text.getRelativeParent(src, 1);

                Node parent = JcrUtil.createPath(parentPath, "sling:Folder", admin);
                Node image = resolver.getResource(resource.getPath() + "/image").adaptTo(Node.class);
                JcrUtil.copy(image, parent, Text.getName(src));

                admin.save();

                return true;
            }
        } catch (RepositoryException e) {
            log.error("Unexpected error while updating logo: ", e);
        }

        return false;
    }
}
```

Klassen implementerar `LogoUpdateHandler` gränssnittets `ContentUpdateHandler` `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` metod, som tar ett antal argument:

* En `ConfigEntry` instans som ger åtkomst till konfigurationsposten, som hanteraren anropas för, och dess egenskaper.
* En `lastUpdated` tidsstämpel som anger när Content Sync senast uppdaterade sin cache. Innehåll som inte har ändrats efter den tidsstämpeln ska inte uppdateras av hanteraren.
* Ett `configCacheRoot` argument som anger cachens rotsökväg. Alla uppdaterade filer måste lagras under den här sökvägen för att kunna läggas till i zip-filen.
* En administrativ session som ska användas för alla cacherelaterade databasåtgärder.
* En användarsession som kan användas för att uppdatera innehåll för en viss användare och därmed tillhandahålla en sorts personaliserat innehåll.

Om du vill implementera den anpassade hanteraren skapar du först en instans av klassen Image baserat på resursen som anges i konfigurationsposten. Detta är i princip samma procedur som den faktiska logotypkomponenten på våra sidor gör. Det ser till att målsökvägen för bilden är densamma som den som en sida refererar till.

Kontrollera sedan om resursen har ändrats sedan den senaste uppdateringen. Anpassade implementeringar bör undvika onödiga uppdateringar av cachen och returnera false om inget ändras. Om resursen har ändrats kopierar du bilden till den förväntade målplatsen i förhållande till cacheroten. Slutligen `true` returneras för att ange för ramverket att cachen uppdaterades.

## Använda innehållet på klienten {#using-the-content-on-the-client}

För att kunna använda innehåll i en mobilapp som tillhandahålls av Content Sync måste du begära innehåll via en HTTP- eller HTTPS-anslutning. Det innebär att hämtat innehåll (packat i en ZIP-fil) kan extraheras och lagras lokalt på den mobila enheten. Observera att innehåll inte bara avser data utan även logik, dvs. fullständiga webbapplikationer. vilket gör det möjligt för mobilanvändaren att köra hämtade webbprogram och motsvarande data även utan nätverksanslutning.

Innehållssynkronisering levererar innehåll på ett intelligent sätt: Endast dataändringar sedan den senaste lyckade datasynkroniseringen levereras, vilket minskar tiden för dataöverföring. Vid den första körningen av en programdataändring begärs ändringar sedan den 1 januari 1970, medan endast data som ändrats sedan den senaste lyckade synkroniseringen efterfrågas. AEM använder ett ramverk för klientkommunikation för iOS för att förenkla datakommunikation och dataöverföring så att en minimal mängd systemspecifik kod krävs för att aktivera ett iOS-baserat webbprogram.

Alla överförda data kan extraheras till samma katalogstruktur, det finns inga ytterligare steg (t.ex. beroendekontroller) som krävs när data extraheras. I iOS lagras alla data i en undermapp i mappen Documents i iOS-appen.

Vanlig körningssökväg för en iOS-baserad AEM-mobilapp:

* Användaren startar programmet på en iOS-enhet.
* Appen försöker ansluta till AEM-serverdelen och begär dataändringar sedan den senaste körningen.
* Servern hämtar data i fråga och packar in dem i en fil.
* Data returneras till klientenheten där de extraheras till dokumentmappen.
* UIWebView-komponenten startar/uppdaterar.

Om det inte går att upprätta en anslutning visas tidigare hämtade data.

### Additional Resources {#additional-resources}

Mer information om roller och ansvar för en administratör och en författare finns i resurserna nedan:

* [Skapa AEM-innehåll för AEM Mobile On Demand Services](/help/mobile/mobile-apps-ondemand.md)
* [Administrera innehåll för att använda AEM Mobile On Demand Services](/help/mobile/aem-mobile.md)

