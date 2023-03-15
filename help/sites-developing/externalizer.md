---
title: Extern URL
seo-title: Externalizing URLs
description: Externalizer är en tjänst av typen OSGI som gör att du kan omvandla en resurssökväg programmatiskt till en extern och absolut URL
seo-description: The Externalizer is an OSGI service that allows you to programmatically transform a resource path into an external and absolute URL
uuid: 65bcc352-fc8c-4aa0-82fb-1321a035602d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 938469ad-f466-42f4-8b6f-bfc060ae2785
docset: aem65
exl-id: 971d6c25-1fbe-4c07-944e-be6b97a59922
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Extern URL{#externalizing-urls}

AEM **Externalizer** är en OSGI-tjänst som gör att du kan omforma en resurssökväg programmatiskt (t.ex. `/path/to/my/page`) till en extern och absolut URL (till exempel `https://www.mycompany.com/path/to/my/page`) genom att ange sökvägen som prefix med en förkonfigurerad DNS.

Eftersom en instans inte känner till sin externt synliga URL-adress om den körs bakom ett webblager, och eftersom en länk ibland måste skapas utanför det begärda omfånget, utgör den här tjänsten en central plats för att konfigurera de externa URL-adresserna och skapa dem.

På den här sidan beskrivs hur du konfigurerar **Externalizer** och hur du använder den. Mer information finns i [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).

## Konfigurera tjänsten Externalizer {#configuring-the-externalizer-service}

The **Externalizer** kan du centralt definiera flera domäner som kan användas för att programmässigt prefix för resurssökvägar. Varje domän identifieras med ett unikt namn som används för att programmässigt referera till domänen.

Definiera en domänmappning för **Externalizer** tjänst:

1. Navigera till konfigurationshanteraren via **verktyg** sedan **Webbkonsol** eller ange:

   `https://<host>:<port>/system/console/configMgr`

1. Klicka **Day CQ Link Externalizer** för att öppna konfigurationsdialogrutan.

   >[!NOTE]
   >
   >Den direkta länken till konfigurationen är `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. Definiera en **Domäner** mappning: en mappning består av ett unikt namn som kan användas i koden för att referera till domänen, ett blanksteg och domänen:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Var:

   * **system** är vanligtvis http eller https, men kan också vara ftp osv.

      * använd https för att framtvinga https-länkar vid behov
      * den kommer att användas om klientkoden inte åsidosätter schemat när en URL-adress begärs externt.
   * **server** är värdnamnet (kan vara ett domännamn eller en IP-adress).
   * **port** (valfritt) är portnumret.
   * **kontextbana** (valfritt) anges bara om AEM har installerats som ett webbprogram under en annan kontextsökväg.

   Till exempel: `production https://my.production.instance`

   Följande mappningsnamn är fördefinierade och måste alltid anges som AEM är beroende av dem:

   * `local` - den lokala instansen
   * `author` - redigeringssystemets DNS
   * `publish` - den offentliga webbplatsens DNS

   >[!NOTE]
   >
   >Med en anpassad konfiguration kan du lägga till en ny kategori, till exempel `production`, `staging` eller till och med externa icke-AEM system som `my-internal-webservice`. Det är praktiskt att undvika hårdkodning av sådana URL:er på olika platser i ett projekts kodbas.

1. Klicka **Spara** för att spara ändringarna.

>[!NOTE]
>
>Adobe rekommenderar att du [lägg till konfigurationen i databasen](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository).

### Använda tjänsten Externalizer {#using-the-externalizer-service}

I det här avsnittet visas några exempel på hur **Externalizer** kan användas:

1. **Så här hämtar du tjänsten Externalizer i en JSP:**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **Så här gör du en extern sökväg med domänen &#39;publish&#39;:**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   Anta domänmappningen:

   * `publish https://www.website.com`

   `myExternalizedUrl` slutar med värdet:

   * `https://www.website.com/contextpath/my/page.html`


1. **Så här gör du en extern sökväg med domänen &#39;författare&#39;:**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   Anta domänmappningen:

   * `author https://author.website.com`

   `myExternalizedUrl` slutar med värdet:

   * `https://author.website.com/contextpath/my/page.html`


1. **Så här externaliserar du en sökväg med domänen&quot;local&quot;:**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   Anta domänmappningen:

   * `local https://publish-3.internal`

   `myExternalizedUrl` slutar med värdet:

   * `https://publish-3.internal/contextpath/my/page.html`


1. Du hittar fler exempel i [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).
