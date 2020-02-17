---
title: SRP och UGC Essentials
seo-title: SRP och UGC Essentials
description: Lagringsresursleverantör och användargenererat innehåll - översikt
seo-description: Lagringsresursleverantör och användargenererat innehåll - översikt
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# SRP och UGC Essentials {#srp-and-ugc-essentials}

## Introduktion {#introduction}

Om du inte känner till lagringsresursens leverantör (SRP) och dess relation till användargenererat innehåll (UGC) kan du besöka [Community Content Storage](working-with-srp.md) and [Storage Resource Provider Overview](srp.md).

I det här avsnittet av dokumentationen finns viktig information om SRP och UGC.

## StorageResourceProvider API {#storageresourceprovider-api}

SocialResourceProvider API (SRP API) är ett tillägg till olika Sling Resource Provider API:er. Den har stöd för sidnumrering och atomisk ökning (användbart för tally och scoring).

Frågor är nödvändiga för SCF-komponenter eftersom det behövs sortering efter datum, hjälpmedel, antal röster och så vidare. Alla SRP-alternativ har flexibla frågemekanismer som inte är beroende av bucketing.

SRP-lagringsplatsen innehåller komponentsökvägen. SRP-API:t ska alltid användas för att komma åt UGC eftersom rotsökvägen beror på vilket SRP-alternativ som har valts, till exempel ASRP, MSRP eller JSRP.

SRP API är inte en abstrakt klass, utan ett gränssnitt. En anpassad implementering bör inte utföras lätt, eftersom fördelarna med framtida förbättringar av interna implementeringar skulle missas vid uppgradering till en ny version.

Sättet att använda SRP API är via tillhandahållna verktyg, t.ex. de som finns i paketet SocialResourceUtilities.

När du uppgraderar från AEM 6.0 eller tidigare måste du migrera UGC för alla SRP som har ett verktyg för öppen källkod. Se [Uppgradera till AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>Tidigare hittades verktyg för att komma åt UGC i paketet SocialUtils, som inte längre finns.
>
>Information om ersättningsverktyg finns i [Omfaktorisering](socialutils.md)för SocialUtils.

## Verktygsmetod för åtkomst till UGC {#utility-method-to-access-ugc}

Om du vill få åtkomst till UGC använder du en metod från paketet SocialResourceUtilities som returnerar en sökväg som är lämplig för åtkomst till UGC från SRP och ersätter den borttagna metoden som finns i paketet SocialUtils.

Följande är ett minimalt exempel på hur du använder metoden resourceToUGCStoragePath() i en serverlet:

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String ugcPath = socialResourceUtilities.resourceToUGCStoragePath(request.getResource());
  // rest of servlet
}
```

Andra ersättningar för SocialUtils finns i [Omfaktorisering](socialutils.md)för SocialUtils.

Riktlinjer för kodning finns på [Accessing UGC with SRP](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>Sökvägen resourceToUGCStoragePath() returnerar *Passar inte *för [ACL-kontroll](srp.md#for-access-control-acls).

## Verktygsmetod för åtkomst till åtkomstkontrollistor {#utility-method-to-access-acls}

Vissa SRP-implementeringar, som ASRP och MSRP, lagrar communityinnehåll i databaser som inte ger någon ACL-verifiering. Skuggnoder är en plats i den lokala databasen som ACL-listor kan användas på.

Med SRP API utför alla SRP-alternativ samma kontroll av skuggplatsen före alla CRUD-åtgärder.

Om du vill kontrollera åtkomstkontrollistor använder du en metod som returnerar en sökväg som är lämplig för att kontrollera behörigheterna som används i resursens UGC.

Nedan följer ett enkelt exempel på hur du använder metoden resourceToACLPath() i en serverlet:

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String aclPath = socialResourceUtilities.resourceToACLPath(request.getResource());
  // rest of servlet
}
```

>[!CAUTION]
>
>Sökvägen som returneras av resourceToACLPath() är *inte *lämplig för [åtkomst till själva UGC](#utility-method-to-access-acls) .

## UGC-relaterade lagringsplatser {#ugc-related-storage-locations}

Följande beskrivningar av lagringsplats kan vara till hjälp när du utvecklar med JSRP eller kanske MSRP. Det finns för närvarande inget användargränssnitt som kan komma åt UGC som lagras i ASRP, vilket finns för verktygen JSRP ([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)) och MSRP (MongoDB).

**komponentplacering**

När en medlem går in i UGC i publiceringsmiljön interagerar de med en komponent som en del av en AEM-webbplats.

Ett exempel på en sådan komponent är [kommentarkomponenten](http://localhost:4502/content/community-components/en/comments.html) som finns på webbplatsen för [Community Components Guide](components-guide.md) . Sökvägen till kommentarnoden i den lokala databasen är:

* Komponentsökväg = */content/community-components/en/comments/jcr:content/content/includable/comments*

**skuggnodplats**

När du skapar UGC skapas även en [skuggnod](srp.md#about-shadow-nodes-in-jcr) som de nödvändiga åtkomstkontrollistorna tillämpas på. Sökvägen till motsvarande skuggnod i den lokala databasen är resultatet av att skuggnodens rotsökväg har försatts i komponentsökvägen:

* Rotsökväg = /content/usergenerated
* Kommentarskuggnod = /content/usergenerated/content/community-components/en/comments/jcr:content/indesign/comments

**UGC-plats**

UGC skapas på båda dessa platser och ska bara nås med en [verktygsmetod](#utility-method-to-access-ugc) som anropar SRP API.

* Rotsökväg = /content/usergenerated/asi/srp-choice
* UGC-nod för JSRP = /content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/includable/comments/srzd-let_it_be_

*Observera* att UGC-noden för JSRP *endast* finns i AEM-instansen (antingen författaren eller publiceringen) som den angavs för. Om det anges i en publiceringsinstans går det inte att moderera från modereringskonsolen på författaren.

## Relaterad information {#related-information}

* [Översikt över](srp.md) lagringsresursleverantör - introduktion och databasanvändning - översikt
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - riktlinjer för kodning
* [Omfaktorisering för SocialUtils](socialutils.md) - Mappar borttagna verktygsmetoder till aktuella SRP-verktygsmetoder

