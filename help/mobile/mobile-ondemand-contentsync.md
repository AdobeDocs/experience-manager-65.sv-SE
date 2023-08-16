---
title: Mobil med innehållssynkronisering
description: Följ den här sidan om du vill veta mer om Innehållssynkronisering. Sidor som har skapats i Adobe Experience Manager (AEM) kan användas som appinnehåll, även när enheten är offline. Eftersom AEM bygger på webbstandarder fungerar de på olika plattformar så att du kan bädda in dem i alla inbyggda wrapper. Den här strategin minskar utvecklingsinsatserna och gör att du enkelt kan uppdatera appinnehåll.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: a6e59334-09e2-4bb8-b445-1868035da556
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2974'
ht-degree: 0%

---

# Mobil med innehållssynkronisering{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Använd Innehållssynkronisering för att paketera innehåll så att det kan användas i inbyggda mobilprogram. Sidor som har skapats i Adobe Experience Manager (AEM) kan användas som appinnehåll, även när enheten är offline. Eftersom AEM bygger på webbstandarder fungerar de på olika plattformar så att du kan bädda in dem i alla inbyggda wrapper. Den här strategin minskar utvecklingsinsatserna och gör att du enkelt kan uppdatera appinnehåll.

I ramverket för innehållssynkronisering skapas en arkivfil som innehåller webbinnehållet. Innehållet kan vara allt från enkla sidor, bilder och PDF eller hela webbprogram. API:t för innehållssynkronisering ger åtkomst till arkivfilen från mobilappar eller byggprocesser så att innehållet kan hämtas och inkluderas i appen.

Följande stegsekvens visar ett typiskt användningsfall för Innehållssynkronisering:

1. Den AEM utvecklaren skapar en konfiguration för innehållssynkronisering som anger vilket innehåll som ska inkluderas.
1. Innehållssynkroniseringsramverket samlar in och cachelagrar innehållet.
1. På en mobil enhet startas mobilprogrammet och begär innehåll från servern, som levereras i en ZIP-fil.
1. Klienten packar upp ZIP-innehållet i det lokala filsystemet. Mappstrukturen i ZIP-filen simulerar de sökvägar som en klient (till exempel en webbläsare) normalt skulle begära från servern.
1. Klienten öppnar innehållet i en inbäddad webbläsare eller använder det på något annat sätt.
1. Senare begär klienten uppdaterat innehåll från servern. Innehållssynkroniseringsramverket innehåller inkrementella uppdateringar som minskar hämtningsstorleken och hämtningstiden, vilket kan vara viktigt för mobila enheter på grund av begränsad bandbredd eller begränsade datavolymer.

## Utveckla hanterare för innehållssynkronisering {#developing-the-content-sync-handlers}

Några av riktlinjerna för utveckling av Hanterare för innehållssynkronisering är följande:

* Hanterare måste implementera *com.day.cq.contentsync.handler.ContentUpdateHandler* (antingen direkt eller genom att utöka en klass som gör det)
* Hanterare kan utöka *com.adobe.cq.momobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Hanteraren får bara rapportera true om den uppdaterar ContentSync-cachen. Felaktig rapportering av true AEM skapa en uppdatering när en uppdatering inte faktiskt gjordes.
* Hanteraren bör bara uppdatera cacheminnet om innehållet ändras. Skriv inte till cacheminnet om en vit inte behövs. Detta resulterar i att en onödig uppdatering skapas.

>[!NOTE]
>
>Aktivera *Felsökningsloggning för ContentSync* via OSGI-loggkonfigurationer på paket *com.day.cq.contentsync*. Detta gör att du kan spåra vad hanterarna har kört och om de har uppdaterat cachen och rapporterat att cachen har uppdaterats.

## Konfigurera innehåll för innehållssynkronisering {#configuring-the-content-sync-content}

Skapa en konfiguration för innehållssynkronisering för att ange innehållet i ZIP-filen som levereras till klienten. Du kan skapa valfritt antal konfigurationer för innehållssynkronisering. Varje konfiguration har ett namn för identifieringsändamål.

Skapa en konfiguration för innehållssynkronisering genom att lägga till en `cq:ContentSyncConfig` till databasen med `sling:resourceType` egenskap inställd på `contentsync/config`. The `cq:ContentSyncConfig` noden kan finnas var som helst i databasen, men noden måste vara tillgänglig för användare på AEM publiceringsinstans. Därför bör du lägga till noden nedan `/content`.

Om du vill ange innehållet i ZIP-filen för innehållssynkronisering lägger du till underordnade noder i cq:ContentSyncConfig-noden. Följande egenskaper för varje underordnad nod identifierar ett innehållsobjekt som ska inkluderas och hur det bearbetas när det läggs till:

* `path`: Innehållets plats.
* `type`: Namnet på den konfigurationstyp som ska användas för bearbetning av innehållet. Flera typer finns tillgängliga och beskrivs i avsnittet *Konfigurationstyper*.

Se *Exempel på konfiguration för innehållssynkronisering* för mer information.

När du har skapat konfigurationen för innehållssynkronisering visas den i konsolen för innehållssynkronisering.

>[!NOTE]
>
>Innehållssynkroniseringsramverket kontrollerar inte att beroenden av resurser och designrelaterade filer ingår i innehålls-Synkroniseringspaket. Se till att du inkluderar alla nödvändiga filer i ZIP-filen.

### Konfigurera åtkomst till hämtningar för innehållssynkronisering {#configuring-access-to-content-sync-downloads}

Ange en användare eller grupp som kan hämtas från Innehållssynkronisering. Du kan konfigurera standardanvändaren eller standardgruppen som kan hämtas från alla cacheminnen för innehållssynkronisering, och du kan åsidosätta standardinställningen och konfigurera åtkomst för en viss konfiguration för innehållssynkronisering.

När AEM är installerat kan medlemmar i administratörsgruppen hämta från innehållssynkronisering som standard.

#### Ange standardåtkomst för hämtning av innehållssynkronisering {#setting-the-default-access-for-content-sync-downloads}

Tjänsten Day CQ Content Sync Manager styr åtkomsten till Content Sync. Konfigurera den här tjänsten för att ange den användare eller grupp som kan hämtas från innehållssynkronisering som standard.

Om du [konfigurera tjänsten med webbkonsolen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)skriver du namnet på användaren eller gruppen som värdet på egenskapen Authorizable för återställningscache.

Om du [konfigurera i databasen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)använder du följande information om tjänsten:

* PID: com.day.cq.contentsync.impl.ContentSyncManagerImpl
* Egenskapsnamn: contentsync.fallback.authzable

#### Åsidosätta hämtningsåtkomst för en cache för innehållssynkronisering {#overriding-download-access-for-a-content-sync-cache}

Om du vill konfigurera hämtningsåtkomst för en viss konfiguration för innehållssynkronisering lägger du till följande egenskap i `cq:ContentSyncConfig` nod:

* Namn: auktoriseringsbar
* Typ: String
* Värde: Namnet på den användare eller grupp som kan hämtas.

Med din app kan användare till exempel installera uppdateringar direkt från innehållssynkronisering. Om du vill att alla användare ska kunna hämta uppdateringen anger du värdet för egenskapen authable till `everyone`.

Om `cq:ContentSyncConfig` noden har ingen auktoriseringsbar egenskap, standardanvändaren eller standardgruppen som är konfigurerad för egenskapen Autentiserbar för reservcache i tjänsten för dagen CQ Content Sync Manager avgör vem som kan hämta.

### Konfigurera användaren för uppdatering av en cache för innehållssynkronisering {#configuring-the-user-for-updating-a-content-sync-cache}

När en användare uppdaterar cachen för innehållssynkronisering utför ett specifikt användarkonto åtgärden åt användaren. Den anonyma användaren uppdaterar alla cacheminnen för innehållssynkronisering som standard.

Du kan åsidosätta standardanvändaren och ange en användare eller grupp som uppdaterar en viss cache för innehållssynkronisering.

Om du vill åsidosätta standardanvändaren anger du en användare eller grupp som utför uppdateringar för en specifik konfiguration för innehållssynkronisering genom att lägga till följande egenskap i cq:ContentSyncConfig-noden:

* Namn: `updateuser`
* Typ: `String`
* Värde: Namnet på den användare eller grupp som kan utföra uppdateringarna.

Om `cq:ContentSyncConfig` noden har ingen `updateuser` egenskap, standard `anonymous` användaren uppdaterar cachen.

### Konfigurationstyper {#configuration-types}

Bearbetningen kan omfatta allt från rendering av enkel JSON till fullständig rendering av sidor, inklusive deras refererade resurser. I det här avsnittet visas tillgängliga konfigurationstyper och deras specifika parametrar:

**copy** - Kopiera filer och mappar.

* **bana** - Om sökvägen pekar på en enda fil kopieras bara filen. Om den pekar på en mapp (inklusive sidnoder) kopieras alla filer och mappar nedan.

**innehåll** Återge innehåll med hjälp av standard [Bearbetning av försäljningsbegäran](/help/sites-developing/the-basics.md#sling-request-processing).

* **bana** - Sökväg till en resurs som ska vara utdata.
* **extension** - Tillägg som ska användas i begäran. Vanliga exempel är *html* och *json*, men alla andra tillägg är möjliga.

* **väljare** - Valfria väljare avgränsade med punkt. Vanliga exempel är *touch* för återgivning av mobilversioner av en sida eller *oändlighet* för JSON-utdata.

**clientlib** - Paketera ett JavaScript- eller CSS-klientbibliotek.

* **bana** - Sökväg till klientbibliotekets rot.
* **extension** - Typ av klientbibliotek. Detta bör anges till antingen *js* eller *css* för tillfället.

**resurser**

Samla in ursprungliga återgivningar av resurser.

* **bana** - Sökväg till en resursmapp nedanför /content/dam.

**image** - Samla in en bild.

* **bana** - Sökväg till en bildresurs.

Bildtypen används för att inkludera logotypen We Retail i zip-filen.

**sidor** - Återge AEM sidor och samla in refererade resurser.

* **bana** - Sökväg till en sida.
* **extension** - Tillägg som ska användas i begäran. För sidor är det här nästan alltid *html* men andra är fortfarande möjliga.

* **väljare** - Valfria väljare avgränsade med punkt. Vanliga exempel är *touch* för återgivning av mobilversioner av en sida.

* **djup** - Valfri boolesk egenskap som avgör om underordnade sidor också ska inkluderas. Standardvärdet är *true.*

* **includeImages** - Valfri boolesk egenskap som avgör om bilder ska inkluderas. Standardvärdet är *true*.

  Som standard beaktas endast bildkomponenter med en resurstyp för grund/komponenter/bild. Du kan lägga till fler resurstyper genom att konfigurera **CQ WCM-siduppdateringshanterare för dag** i webbkonsolen.

**rewrite** - Noden rewrite definierar hur länkarna skrivs om på den exporterade sidan. De omskrivna länkarna kan antingen peka på filerna som finns i ZIP-filen eller på resurserna på servern.

The `rewrite` noden måste finnas under `page` nod.

The `rewrite` noden kan ha en eller flera av följande egenskaper:

* `clientlibs`: skriver om klientlibs-banor.

* `images`: skriver om bildbanor.
* `links`: skriver om länksökvägar.

Varje egenskap kan ha något av följande värden:

* `REWRITE_RELATIVE`: skriver om sökvägen med en relativ position till HTML-filen på sidan i filsystemet.

* `REWRITE_EXTERNAL`: skriver om sökvägen genom att peka på resursen på servern med AEM [Externalizer-tjänst](/help/sites-developing/externalizer.md).

AEM anropade **PathRewriterTransformerFactory** I kan du konfigurera de specifika HTML-attribut som ska skrivas om. Tjänsten kan konfigureras i webbkonsolen och har en konfiguration för varje egenskap i `rewrite` nod: `clientlibs`, `images`och `links`.

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

**etc.designs.default och etc.designs.mobile** - De två första posterna i konfigurationen är uppenbara. När du ska ta med flera mobilsidor behöver du de relaterade designfilerna nedan /etc/designs. Och eftersom ingen extra bearbetning behövs räcker det med en kopia.

**events.plist** - Den här posten är lite speciell. Som nämndes i inledningen bör programmet tillhandahålla en kartvy med markörer för händelsernas platser. Den nödvändiga platsinformationen tillhandahålls som en separat fil i PLIST-format. För att detta ska fungera har händelselistkomponenten som används på indexsidan ett skript som heter plist.jsp. Skriptet körs när komponentens resurs begärs med `.plist` tillägg. Som vanligt anges komponentsökvägen i egenskapen path och typen ställs in på content eftersom du vill använda [Bearbetning av försäljningsbegäran](/help/sites-developing/the-basics.md#sling-request-processing).

**events.touch.html** - Därefter kommer de sidor som visas i appen. Egenskapen path ställs in på händelsens rotsida. Alla händelsesidor under den sidan inkluderas också eftersom egenskapen deep har standardvärdet true. Du använder sidor som konfigurationstyp så att alla bilder eller andra filer som kan refereras från en bild eller hämtas från en komponent på en sida inkluderas. Om du dessutom ställer in pekväljaren får vi en mobilversion av sidorna. Konfigurationen i funktionspaketet innehåller fler poster av den här typen, men utelämnas för enkelhetens skull här.

**logo** - Logotypens konfigurationstyp har inte nämnts hittills och den är ingen av de inbyggda typerna. Ramverket för innehållssynkronisering är dock delvis utökningsbart och det är ett exempel på det, som kommer att behandlas i nästa avsnitt.

**manifest** - Det är ofta önskvärt att ZIP-filen innehåller någon typ av metadata, till exempel startsidan för ditt innehåll. Om du däremot hårdkodar sådan information kan du inte ändra den senare. Innehållssynkroniseringsramverket stöder det här användningsexemplet genom att söka efter en manifestnod i konfigurationen, som identifieras med namn och som inte kräver någon konfigurationstyp. Alla egenskaper som definieras på den aktuella noden läggs till i en fil, som också kallas manifest och finns i zip-filens rot.

I exemplet ska händelselistsidan vara den första sidan. Denna information finns i **indexPage** och kan därför ändras när som helst. En andra egenskap definierar sökvägen till *events.plist* -fil. Som du ser senare kan klientprogrammet nu läsa manifestet och agera enligt det.

När konfigurationen är konfigurerad kan innehållet hämtas med en webbläsare eller en annan HTTP-klient, eller om du utvecklar för iOS kan du använda det dedikerade WAppKitSync-klientbiblioteket. Hämtningsplatsen består av konfigurationens sökväg och *.zip* tillägg, till exempel när du arbetar med en lokal AEM: *http://localhost:4502/content/weretail_go.zip*

### Konsolen Innehållssynkronisering {#the-content-sync-console}

I konsolen Innehållssynkronisering visas alla konfigurationer för innehållssynkronisering i databasen (alla noder av typen `cq:ContentSyncConfig`) och för varje konfiguration kan du göra följande:

* Uppdatera cachen.
* Rensa cachen.
* Ladda ned en komplett zip.
* Ladda ned en diff-zip mellan idag och ett specifikt datum och en viss tid.

Den kan vara användbar för utveckling och felsökning.

Konsolen finns på:

`http://localhost:4502/libs/cq/contentsync/content/console.html`

Den ser ut så här:

![chlimage_1-50](assets/chlimage_1-50.png)

### Utöka ramverket för innehållssynkronisering {#extending-the-content-sync-framework}

Även om antalet konfigurationsalternativ redan är stort kanske det inte täcker alla krav för ditt specifika användningsfall. I det här avsnittet beskrivs tilläggen för ramverket för innehållssynkronisering och hur du skapar anpassade konfigurationstyper.

För varje konfigurationstyp finns en *Hanterare för innehållsuppdatering*, som är en OSGi-komponentfabrik som är registrerad för just den typen. Hanterarna samlar in, bearbetar och lägger till innehåll i ett cacheminne som underhålls av ramverket för innehållssynkronisering. Implementera följande gränssnitt eller abstrakt basklass:

* `com.day.cq.contentsync.handler.ContentUpdateHandler` - Gränssnitt som alla uppdateringshanterare måste implementera
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - en abstrakt klass som förenklar återgivningen av resurser med Sling

Registrera klassen som OSGi-komponentfabrik och distribuera den i OSGi-behållaren i ett paket. Detta kan du göra med [Maven SCR plugin](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/apache-felix-maven-scr-plugin-use.html) antingen med JavaDoc-taggar eller anteckningar. I följande exempel visas JavaDoc-versionen:

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

Observera att *fabrik* definitionen innehåller det gemensamma gränssnittet och den anpassade typen separerad med snedstreck. Den här strategin gör att innehållssynkroniseringsramverket kan hitta och skapa en instans av din anpassade klass som känner igen den anpassade typen i en konfigurationspost. I nästa avsnitt finns ett konkret exempel på en anpassad uppdateringshanterare.

>[!CAUTION]
>
>När du bygger vidare på basklassen AbstractSlingResourceUpdateHandler måste du lägga till *ärva* definition. Annars kommer OSGi-behållaren inte att ange de nödvändiga referenserna som deklareras i basklassen.

### Implementera en anpassad uppdateringshanterare {#implementing-a-custom-update-handler}

Varje sida för e-butiksmobilen innehåller en logotyp i det övre vänstra hörnet som ska inkluderas i zip-filen. För cacheoptimering refererar AEM inte till bildfilens verkliga plats i databasen, vilket förhindrar oss från att använda **copy** konfigurationstyp. Vad du måste göra istället är att erbjuda våra **logo** konfigurationstyp som gör bilden tillgänglig på den plats som AEM begär. I följande kodexempel visas den fullständiga implementeringen av hanteraren för uppdatering av logotyp:

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

The `LogoUpdateHandler` klassen implementerar `ContentUpdateHandler` gränssnitt `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` -metod, som tar flera argument:

* A `ConfigEntry` -instans som ger åtkomst till konfigurationsposten, som hanteraren anropas för, och dess egenskaper.
* A `lastUpdated` tidsstämpel som anger när Content Sync senast uppdaterade sin cache. Innehåll som inte har ändrats efter den tidsstämpeln ska inte uppdateras av hanteraren.
* A `configCacheRoot` -argument som anger cachens rotsökväg. Alla uppdaterade filer måste lagras under den här sökvägen för att kunna läggas till i zip-filen.
* En administrativ session som ska användas för alla cacherelaterade databasåtgärder.
* En användarsession som kan användas för att uppdatera innehåll för en viss användare och därmed tillhandahålla en sorts personaliserat innehåll.

Om du vill implementera den anpassade hanteraren skapar du först en instans av klassen Image baserat på resursen som anges i konfigurationsposten. Detta är samma procedur som den faktiska logotypkomponenten på våra sidor gör. Det ser till att målsökvägen för bilden är densamma som den som en sida refererar till.

Kontrollera sedan om resursen har ändrats sedan den senaste uppdateringen. Anpassade implementeringar bör undvika onödiga uppdateringar av cacheminnet och returnera false om inget ändras. Om resursen har ändrats kopierar du bilden till den förväntade målplatsen i förhållande till cacheroten. Äntligen `true` returneras för att ange för ramverket att cachen har uppdaterats.

## Använda innehållet på klienten {#using-the-content-on-the-client}

Om du vill använda innehåll i en mobilapp som tillhandahålls av Innehållssynkronisering måste du begära innehåll via en HTTP- eller HTTPS-anslutning. Det innebär att hämtat innehåll (packat i en ZIP-fil) kan extraheras och lagras lokalt på den mobila enheten. Innehållet avser inte bara data utan också logik, det vill säga kompletta webbprogram, vilket gör att mobilanvändaren kan köra hämtade webbprogram och motsvarande data även utan nätverksanslutning.

Innehållssynkronisering levererar innehåll på ett intelligent sätt: Endast dataändringar sedan den senaste lyckade datasynkroniseringen har utförts, vilket minskar tiden för dataöverföring. När ett program körs första gången begärs dataändringar sedan den 1 januari 1970, medan endast data som ändrats sedan den senaste lyckade synkroniseringen begärs senare. AEM använder ett ramverk för klientkommunikation för iOS för att förenkla datakommunikation och dataöverföring så att en minimal mängd systemspecifik kod krävs för att aktivera ett iOS-baserat webbprogram.

Alla överförda data kan extraheras till samma katalogstruktur, det finns inga ytterligare steg (till exempel beroendekontroller) som krävs när data extraheras. Om det finns iOS lagras alla data i en undermapp i mappen Documents i iOS App.

Vanlig körningssökväg för en iOS-baserad AEM Mobile-app:

* Användaren startar appen på iOS-enheten.
* Appen försöker ansluta till AEM och begär dataändringar sedan den senaste körningen.
* Servern hämtar data i fråga och packar in dem i en fil.
* Data returneras till klientenheten där de extraheras till dokumentmappen.
* UIWebView-komponenten startar/uppdaterar.

Om det inte gick att upprätta en anslutning tidigare visas hämtade data.

### Ytterligare resurser {#additional-resources}

Mer information om roller och ansvar för en administratör och en författare finns i resurserna nedan:

* [AEM innehåll för AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
* [Administrera innehåll för användning av AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
