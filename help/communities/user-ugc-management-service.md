---
title: Tjänsten för hantering av användare och användargenererat innehåll i AEM Communities
seo-title: Tjänsten för hantering av användare och användargenererat innehåll i AEM Communities
description: Använd API:er för att massexportera användargenererat innehåll och inaktivera användarkontot.
seo-description: Använd API:er för att massexportera användargenererat innehåll och inaktivera användarkontot.
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---


# Tjänsten för hantering av användare och användargenererat innehåll i AEM Communities {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>GDPR används som exempel i avsnitten nedan, men de ingående detaljerna är tillämpliga på alla dataskydds- och sekretessbestämmelser. såsom GDPR, CCPA osv.

AEM Communities visar användningsklara API:er för hantering av användarprofiler och grupphantering av användargenererat innehåll (UGC). När tjänsten **UserUgcManagement** har aktiverats kan behöriga användare (community-administratörer och moderatorer) inaktivera användarprofiler och massborttagning eller massexport av UGC för specifika användare. Dessa API:er gör det även möjligt för personuppgiftsansvariga och personuppgiftsbiträden att följa EU:s allmänna dataskyddsförordningar (GDPR) och andra GDPR-inspirerade sekretessbestämmelser.

Mer information finns på sidan [GDPR på Adobe Privacy Center](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Om du konfigurerade [Adobe Analytics på AEM Communities](/help/communities/analytics.md)-platsen skickas den hämtade användarinformationen till Adobe Analytics-servern. Adobe Analytics tillhandahåller API:er som gör att du kan komma åt, exportera och ta bort användardata och följa GDPR. Mer information finns i [Skicka in åtkomst- och borttagningsbegäranden](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html).

Om du vill använda dessa API:er måste du aktivera slutpunkten `/services/social/ugcmanagement` genom att aktivera tjänsten UserUgcManagement. Om du vill aktivera den här tjänsten installerar du [exempelservleten](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) som finns på [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). Tryck sedan på slutpunkten på publiceringsinstansen av communitywebbplatsen med lämpliga parametrar med en http-begäran, som:

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. Du kan även skapa ett användargränssnitt (användargränssnitt) för att hantera användarprofiler och användargenererat innehåll i systemet.

Dessa API:er gör det möjligt att utföra följande funktioner.

## Hämta användargränssnittskontrollen för en användare {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)** hjälper till att exportera all UGC för en användare från systemet.

* **användare**: Auktoriserbart ID för en användare.
* **outputStream**: Resultatet returneras som utdataström, vilket är en zip-fil som innehåller det användargenererade innehållet (som json-fil) och bilagor (som innehåller bilder eller videor som överförts av användaren).

Om du till exempel vill exportera användargenererat innehåll för en användare med namnet Weston McCall, som använder weston.mccall@dodgit.com som auktoriseringsbart ID för att logga in på communitysajten, kan du skicka en http GET-begäran som ser ut så här:

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## Ta bort användargränssnittskontrollen för en användare {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)** hjälper till att ta bort all UGC för en användare från systemet.

* **användare**: Användarens autentiserbara ID.

Om du till exempel vill ta bort användargränssnittskontrollen för en användare med ett auktoriserbart ID weston.mccall@dodgit.com genom en http-POST-begäran använder du följande parametrar:

* user = `weston.mccall@dodgit.com`
* operation = `deleteUgc`

### Ta bort UGC från Adobe Analytics {#delete-ugc-from-adobe-analytics}

Om du vill ta bort användardata från Adobe Analytics följer du arbetsflödet [GDPR Analytics](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html); eftersom API inte tar bort användardata från Adobe Analytics.

För Adobe Analytics-variabelmappningar som används av AEM Communities, se följande bild:

![AEM communityvariabelmappning för Adobe Analytics](assets/analytics-communities-mapping.png)

## Inaktivera ett användarkonto {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user)** hjälper till att inaktivera ett användarkonto.

* **användare**: Användarens autentiserbara ID.

>[!NOTE]
>
>Om du inaktiverar en användare tas allt användargenererat innehåll som användaren har på servern bort.

Om du till exempel vill ta bort profilen för en användare som har ett autentiserbart ID `weston.mccall@dodgit.com` via http-POST-begäran använder du följande parametrar:

* användare = `weston.mccall@dodgit.com`
* operation = `deleteUser`

>[!NOTE]
>
>deleteUserAccount() API inaktiverar bara en användarprofil i systemet och tar bort UGC. Om du vill ta bort en användarprofil från systemet går du till **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de), leta reda på användarnoden och ta bort den.
