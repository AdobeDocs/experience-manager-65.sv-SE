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
source-git-commit: c798eb79dc9f8e58cef86cf90af02622c3a2ed78
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 1%

---


# JSRP - JCR-lagringsresursprovider {#jsrp-jcr-storage-resource-provider}

## Om JSRP {#about-jsrp}

När AEM Communities använder JSRP som lagringsalternativ (standard) lagras communityinnehåll i JCR och användargenererat innehåll (UGC) är endast tillgängligt från författaren eller den publiceringsinstans som det publicerades i.

På grund av enkelheten i distributionen passar JSRP oftast bäst för demonstrations- eller utvecklingsmiljöer med en publiceringsinstans och en författarinstans.

Se även [egenskaper för SRP-alternativ](working-with-srp.md#characteristics-of-srp-options) och [rekommenderade topologier](topologies.md).

## Konfiguration {#configuration}

### Välj JSRP {#select-jsrp}

Som standard är JSRP lagringsalternativet för UGC.

Med konsolen [för](srp-config.md) lagringskonfiguration kan du välja standardlagringskonfiguration, som identifierar vilken implementering av SRP som ska användas.

För att nå konsolen Lagringskonfiguration i redigeringsmiljön

* Från global navigering: **[!UICONTROL Tools]** > **[!UICONTROL Communities]** > **[!UICONTROL Storage Configuration]**

* Välj **[!UICONTROL JCR Storage Resource Provider (JSRP)]**

* Välj **[!UICONTROL Submit]**

![chlimage_1-234](assets/chlimage_1-234.png)

### Publicera konfigurationen {#publishing-the-configuration}

JSRP är standardkonfigurationen, och för att säkerställa att den identiska konfigurationen ställs in i publiceringsmiljön:

* On author:

   * Från global navigering: **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**
   * Välj **[!UICONTROL Activate Tree]** > **[!UICONTROL Start Path]**:

      * Bläddra till `/conf/global/settings/community/srpc/`
   * Välj **[!UICONTROL Activate]**


## Hantera användardata {#managing-user-data}

Information om *användare*, *användarprofiler* och *användargrupper* som ofta används i publiceringsmiljön finns på:

* [Användarsynkronisering](sync.md)
* [Hantera användare och användargrupper](users.md)

## Felsökning {#troubleshooting}

### UGC är inte synlig i JCR {#ugc-not-visible-in-jcr}

Kontrollera att JSRP har konfigurerats som standardprovider genom att kontrollera konfigurationen av lagringsalternativet. Som standard är lagringsresursprovidern JSRP.

Gå till konsolen för lagringskonfiguration eller kontrollera AEM-databasen på alla författare och publicera AEM-instanser:

* I JCR, if [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Innehåller ingen [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) -nod, vilket betyder att lagringsprovidern är JSRP.
   * Om srpc-noden finns och innehåller [standardkonfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)för nod, ska standardkonfigurationens egenskaper definiera JSRP som standardprovider.

### UGC är inte synlig på författarinstans {#ugc-not-visible-on-author-instance}

Det här är inte något fel. En egenskap hos JSRP är att communityinnehåll som anges i publiceringsmiljön endast visas i publiceringsmiljön.

### UGC är inte synlig vid publiceringsinstans {#ugc-not-visible-on-publish-instance}

Om en enskild publiceringsinstans eller ett publiceringskluster distribueras följer du instruktionerna för [UGC som inte är synlig i JCR](#ugc-not-visible-in-jcr).

Om en publiceringsgrupp distribueras är egenskapen för JSRP att communityinnehåll bara visas på den publiceringsinstans som det publicerades i.

För att UGC ska vara synligt från alla publiceringsinstanser krävs ett publiceringskluster.
