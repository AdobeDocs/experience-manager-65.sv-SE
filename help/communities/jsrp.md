---
title: JSRP - JCR-lagringsresursprovider
seo-title: JSRP - JCR-lagringsresursprovider
description: JSRP passar oftast bäst för demonstrations- och utvecklingsmiljöer med en publiceringsinstans och en författarinstans
seo-description: JSRP passar oftast bäst för demonstrations- och utvecklingsmiljöer med en publiceringsinstans och en författarinstans
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
translation-type: tm+mt
source-git-commit: aa2c75e061e00ba74d54843a5f35bb7d82d12a92

---


# JSRP - JCR-lagringsresursprovider {#jsrp-jcr-storage-resource-provider}

## Om JSRP {#about-jsrp}

När AEM Communities använder JSRP som lagringsalternativ (standard) lagras community-innehåll i JCR och användargenererat innehåll (UGC) är endast tillgängligt från författaren eller den publiceringsinstans som det publicerades i.

På grund av enkelheten i distributionen passar JSRP oftast bäst för demonstrations- eller utvecklingsmiljöer med en publiceringsinstans och en författarinstans.

Se även [egenskaper för SRP-alternativ](working-with-srp.md#characteristics-of-srp-options) och [rekommenderade topologier](topologies.md).

## Konfiguration {#configuration}

### Välj JSRP {#select-jsrp}

Som standard är JSRP lagringsalternativet för UGC.

Med konsolen [för](srp-config.md) lagringskonfiguration kan du välja standardlagringskonfiguration, som identifierar vilken implementering av SRP som ska användas.

För att nå konsolen Lagringskonfiguration i redigeringsmiljön

* Från global navigering: **[!UICONTROL Verktyg > Communities > Storage Configuration]**

![chlimage_1-234](assets/chlimage_1-234.png)

* Välj **[!UICONTROL JSRP (JCR Storage Resource Provider)]**
* Välj **[!UICONTROL Skicka]**

### Publicera konfigurationen {#publishing-the-configuration}

När JSRP är standardkonfigurationen, kontrollerar du att den identiska konfigurationen är inställd i publiceringsmiljön:

* On author:

   * Från global navigering: **[!UICONTROL Verktyg > Distribution > Replikering]**
   * Välj **[!UICONTROL Aktivera träd]**
   * **[!UICONTROL Startsökväg]**:

      * Bläddra till `/conf/global/settings/community/srpc/`
   * Välj **[!UICONTROL Aktivera]**


## Hantera användardata {#managing-user-data}

Information om *användare*, *användarprofiler* och *användargrupper* som ofta används i publiceringsmiljön finns på

* [Användarsynkronisering](sync.md)
* [Hantera användare och användargrupper](users.md)

## Felsökning {#troubleshooting}

### UGC är inte synlig i JCR {#ugc-not-visible-in-jcr}

Kontrollera att JSRP har konfigurerats som standardprovider genom att kontrollera konfigurationen av lagringsalternativet. Som standard är lagringsresursprovidern JSRP.

Gå till konsolen för lagringskonfiguration eller kontrollera AEM-databasen på alla författare och publicera AEM-instanser:

* i JCR, if [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Innehåller ingen [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) -nod, vilket betyder att lagringsprovidern är JSRP
   * Om srpc-noden finns och innehåller [standardkonfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)för nod, ska standardkonfigurationens egenskaper definiera JSRP som standardprovider

### UGC är inte synlig på författarinstans {#ugc-not-visible-on-author-instance}

Det här är inte något fel. En egenskap hos JSRP är att communityinnehåll som anges i publiceringsmiljön endast visas i publiceringsmiljön.

### UGC är inte synlig vid publiceringsinstans {#ugc-not-visible-on-publish-instance}

Om en enskild publiceringsinstans eller ett publiceringskluster distribueras följer du instruktionerna för [UGC som inte är synlig i JCR](#ugc-not-visible-in-jcr).

Om en publiceringsgrupp distribueras är egenskapen för JSRP att communityinnehåll bara visas på den publiceringsinstans som det publicerades i.

För att UGC ska vara synligt från alla publiceringsinstanser krävs ett publiceringskluster.
