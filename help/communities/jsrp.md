---
title: JSRP - JCR-lagringsresursprovider
seo-title: JSRP - JCR Storage Resource Provider
description: JSRP passar oftast bäst för demonstrations- och utvecklingsmiljöer med en publiceringsinstans och en författarinstans
seo-description: JSRP is generally best suited for demonstration or development environments of one publish instance and one author instance
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 1%

---

# JSRP - JCR-lagringsresursprovider {#jsrp-jcr-storage-resource-provider}

## Om JSRP {#about-jsrp}

När AEM Communities använder JSRP som lagringsalternativ (standard) lagras community-innehåll i JCR och användargenererat innehåll (UGC) är endast tillgängligt från författaren eller den publiceringsinstans som det publicerades i.

På grund av enkelheten i distributionen passar JSRP oftast bäst för demonstrations- eller utvecklingsmiljöer med en publiceringsinstans och en författarinstans.

Se även [Egenskaper för SRP-alternativ](working-with-srp.md#characteristics-of-srp-options) och [Rekommenderade topologier](topologies.md).

## Konfiguration {#configuration}

### Välj JSRP {#select-jsrp}

Som standard är JSRP lagringsalternativet för UGC.

The [Konsol för lagringskonfiguration](srp-config.md) gör det möjligt att välja standardlagringskonfiguration, som identifierar vilken implementering av SRP som ska användas.

För att nå konsolen Lagringskonfiguration i redigeringsmiljön

* Från global navigering: **[!UICONTROL Tools]** > **[!UICONTROL Communities]** > **[!UICONTROL Storage Configuration]**

* Välj **[!UICONTROL JCR Storage Resource Provider (JSRP)]**

* Välj **[!UICONTROL Submit]**

![jsrp-configuration](assets/jsrp-configuration.png)

### Publicera konfigurationen {#publishing-the-configuration}

JSRP är standardkonfigurationen, och för att säkerställa att den identiska konfigurationen ställs in i publiceringsmiljön:

* Från global navigering: **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**
* Välj **[!UICONTROL Activate Tree]** > **[!UICONTROL Start Path]**:

   * Bläddra till `/conf/global/settings/community/srpc/`

* Välj **[!UICONTROL Activate]**

## Hantera användardata {#managing-user-data}

För information om *användare*, *användarprofiler* och *användargrupper*, som ofta används i publiceringsmiljön, går till:

* [Användarsynkronisering](sync.md)
* [Hantera användare och användargrupper](users.md)

## Felsökning {#troubleshooting}

### UGC är inte synlig i JCR {#ugc-not-visible-in-jcr}

Kontrollera att JSRP har konfigurerats som standardprovider genom att kontrollera konfigurationen av lagringsalternativet. Som standard är lagringsresursprovidern JSRP.

Gå till konsolen för lagringskonfiguration eller kontrollera den AEM databasen för alla författare och publiceringsinstanser:

* I JCR, om [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Innehåller inte [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) -nod betyder det att lagringsprovidern är JSRP.
   * Om srpc-noden finns och innehåller nod [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)ska standardkonfigurationens egenskaper definiera JSRP som standardprovider.

### UGC är inte synlig på författarinstans {#ugc-not-visible-on-author-instance}

Det här är inte något fel. En egenskap hos JSRP är att communityinnehåll som anges i publiceringsmiljön endast visas i publiceringsmiljön.

### UGC är inte synlig vid publiceringsinstans {#ugc-not-visible-on-publish-instance}

Om en publiceringsinstans eller ett publiceringskluster distribueras följer du instruktionerna för [UGC är inte synlig i JCR](#ugc-not-visible-in-jcr).

Om en publiceringsgrupp distribueras är egenskapen för JSRP att communityinnehåll bara visas på den publiceringsinstans som det publicerades i.

För att UGC ska vara synligt från alla publiceringsinstanser krävs ett publiceringskluster.
