---
title: Bygga taggar i ett AEM-program
seo-title: Bygga taggar i ett AEM-program
description: Arbeta programmatiskt med taggar eller utöka taggar i ett anpassat AEM-program
seo-description: Arbeta programmatiskt med taggar eller utöka taggar i ett anpassat AEM-program
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Bygga taggar i ett AEM-program{#building-tagging-into-an-aem-application}

För programmatiskt arbete med taggar eller tillägg av taggar i ett anpassat AEM-program beskriver den här sidan användningen av

* [API för taggning](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

som interagerar med

* [Ramverk för taggning](/help/sites-developing/framework.md)

Mer information om taggning finns i:

* [Administrera taggar](/help/sites-administering/tags.md) om du vill ha information om hur du skapar och hanterar taggar, samt om vilka innehållstaggar som har tillämpats.
* [Använda taggar](/help/sites-authoring/tags.md) för information om att tagga innehåll.

## Översikt över taggnings-API:t {#overview-of-the-tagging-api}

Implementeringen av [taggningsramverket](/help/sites-developing/framework.md) i AEM gör det möjligt att hantera taggar och tagginnehåll med JCR-API:t. TagManager ser till att taggar som anges som värden i strängarrayegenskapen inte dupliceras, det tar bort tagg-ID:n som pekar på taggar som inte finns och uppdaterar tagg-ID:n för flyttade eller sammanfogade taggar. `cq:tags` TagManager använder en JCR-observationslyssnare som återställer felaktiga ändringar. Huvudklasserna finns i [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) -paketet:

* JcrTagManagerFactory - returnerar en JCR-baserad implementering av en `TagManager`. Det är referensimplementeringen av taggnings-API:t.
* `TagManager` - gör att du kan lösa och skapa taggar efter sökvägar och namn.
* `Tag` - definierar taggobjektet.

### Hämta en JCR-baserad TagManager {#getting-a-jcr-based-tagmanager}

Om du vill hämta en TagManager-instans måste du ha en JCR `Session` och anropa `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

I ett typiskt Sling-sammanhang kan du även anpassa dig till en `TagManager` från `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Hämta ett taggobjekt {#retrieving-a-tag-object}

En `Tag` tagg kan hämtas via `TagManager`, antingen genom att en befintlig tagg matchas eller genom att en ny skapas:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

För den JCR-baserade implementeringen, som mappar `Tags` till JCR `Nodes`, kan du använda Slings `adaptTo` -mekanism direkt om du har resursen (t.ex. `/etc/tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Även om en tagg endast kan konverteras *från *en resurs (inte en nod), kan en tagg konverteras *till *både en nod och en resurs:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Det går inte `Node` att direkt anpassa från `Tag` till eftersom `Node` inte implementerar Sling- `Adaptable.adaptTo(Class)` metoden.

### Hämta och ställa in taggar {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### Söker efter taggar {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>Giltig `RangeIterator` att använda:
>
>`com.day.cq.commons.RangeIterator`

### Ta bort taggar {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Replikerar taggar {#replicating-tags}

Det går att använda replikeringstjänsten ( `Replicator`) med taggar eftersom taggar är av typen `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## Tagga på klientsidan {#tagging-on-the-client-side}

`CQ.tagging.TagInputField` är en formulärwidget för att ange taggar. Den har en snabbmeny där du kan välja bland befintliga taggar, som innehåller automatisk komplettering och många andra funktioner. Dess xtype är `tags`.

## Taggskräpinsamlaren {#the-tag-garbage-collector}

Taggskräpinsamlaren är en bakgrundstjänst som rensar de dolda och oanvända taggarna. Dolda och oanvända taggar är taggar under `/etc/tags` som har en `cq:movedTo` egenskap och inte används i en innehållsnod - de har ett antal som är noll. Genom att använda den här lat borttagningsprocessen behöver inte innehållsnoden (dvs. egenskapen `cq:tags` ) uppdateras som en del av flyttningen eller sammanfogningen. Referenserna i `cq:tags` egenskapen uppdateras automatiskt när `cq:tags` egenskapen uppdateras, t.ex. via dialogrutan för sidegenskaper.

Taggskräpinsamlaren körs som standard en gång om dagen. Detta kan konfigureras på:

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Märkordssökning och tagglista {#tag-search-and-tag-listing}

Sökningen efter taggar och tagglistan fungerar enligt följande:

* Sökningen efter TagID söker efter de taggar som har egenskapen `cq:movedTo` inställd på TagID och följer via `cq:movedTo` TagID:n.

* Om du söker efter tagg Titel genomsöks bara de taggar som inte har någon `cq:movedTo` egenskap.

## Taggar på olika språk {#tags-in-different-languages}

Som beskrivs i dokumentationen för att administrera taggar [kan du definiera en tagg på olika språk i avsnittet](/help/sites-administering/tags.md#managing-tags-in-different-languages)Hantera taggar på olika språk `title`. Sedan läggs en språkkänslig egenskap till i taggnoden. Den här egenskapen har formatet `jcr:title.<locale>`, t.ex. `jcr:title.fr` för den franska översättningen. `<locale>` måste vara en ISO-språksträng med gemener och använda &quot;_&quot; i stället för &quot;-&quot;, till exempel: `de_ch`.

När taggen **Djur** läggs till på sidan **Produkter** läggs värdet `stockphotography:animals` till i egenskapen `cq:tags` för noden /content/geometrixx/en/products/jcr:content. Översättningen refereras från taggnoden.

API:t på serversidan har lokaliserade `title`metoder:

* [com.day.cq.tagging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(språkområde)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(Locale locale)
   * getTitlePath(språkområde)

* [com.day.cq.tagging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, Locale locale)
   * createTagByTitle(String tagTitlePath, Locale locale)
   * resolveByTitle(String tagTitlePath, locale)

I AEM kan språket hämtas antingen från sidspråket eller från användarspråket:

* för att hämta sidspråket i en JSP:

   * `currentPage.getLanguage(false)`

* för att hämta användarspråket i en JSP:

   * `slingRequest.getLocale()`

`currentPage` och `slingRequest` är tillgängliga i en JSP via taggen [&lt;cq:definedObjects>](/help/sites-developing/taglib.md) .

För taggning beror lokaliseringen på sammanhanget eftersom taggen `titles`kan visas på sidspråket, på användarspråket eller på något annat språk.

### Lägga till ett nytt språk i dialogrutan Redigera tagg {#adding-a-new-language-to-the-edit-tag-dialog}

I proceduren nedan beskrivs hur du lägger till ett nytt språk (finska) i dialogrutan **Taggredigering** :

1. I **CRXDE** redigerar du egenskapen multi-value `languages` för noden `/etc/tags`.

1. Lägg till `fi_fi` - som representerar den finska språkinställningen - och spara ändringarna.

Det nya språket (finska) är nu tillgängligt i taggdialogrutan för sidegenskaperna och i dialogrutan **Redigera tagg** när du redigerar en tagg i **taggningskonsolen** .

>[!NOTE]
>
>Det nya språket måste vara ett av de språk som AEM känner igen, dvs. det måste vara tillgängligt som en nod nedan `/libs/wcm/core/resources/languages`.

