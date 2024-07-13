---
title: JSRP - JCR-lagringsresursprovider
description: JSRP passar bäst för demonstrations- och utvecklingsmiljöer med en Publish-instans och en Author-instans
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# JSRP - JCR-lagringsresursprovider {#jsrp-jcr-storage-resource-provider}

## Om JSRP {#about-jsrp}

När AEM Communities använder JSRP som lagringsalternativ (standard) lagras community-innehåll i JCR, och användargenererat innehåll (UGC) är endast tillgängligt från författaren eller den publiceringsinstans som det publicerades i.

På grund av enkelheten i driftsättningen är JSRP bäst lämpat för demonstrations- eller utvecklingsmiljöer i en Publish-instans och en Author-instans.

Se även [Egenskaper för SRP-alternativ](working-with-srp.md#characteristics-of-srp-options) och [Rekommenderade topologier](topologies.md).

## Konfiguration {#configuration}

### Välj JSRP {#select-jsrp}

Som standard är JSRP lagringsalternativet för UGC.

Konsolen [Lagringskonfiguration](srp-config.md) tillåter val av standardlagringskonfiguration, som identifierar vilken implementering av SRP som ska användas.

För att nå konsolen Lagringskonfiguration i redigeringsmiljön

* Från global navigering: **[!UICONTROL Tools]** > **[!UICONTROL Communities]** > **[!UICONTROL Storage Configuration]**

* Välj **[!UICONTROL JCR Storage Resource Provider (JSRP)]**

* Välj **[!UICONTROL Submit]**

![jsrp-configuration](assets/jsrp-configuration.png)

### Publicera konfigurationen {#publishing-the-configuration}

JSRP är standardkonfigurationen, och du kan se till att den identiska konfigurationen ställs in i publiceringsmiljön:

* Från global navigering: **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**
* Välj **[!UICONTROL Activate Tree]** > **[!UICONTROL Start Path]**:

   * Bläddra till `/conf/global/settings/community/srpc/`

* Välj **[!UICONTROL Activate]**

## Hantera användardata {#managing-user-data}

Mer information om *användare*, *användarprofiler* och *användargrupper* som ofta anges i publiceringsmiljön finns på:

* [Användarsynkronisering](sync.md)
* [Hantera användare och användargrupper](users.md)

## Felsökning {#troubleshooting}

### UGC är inte synlig i JCR {#ugc-not-visible-in-jcr}

Kontrollera att JSRP har konfigurerats som standardprovider genom att kontrollera konfigurationen av lagringsalternativet. Som standard är lagringsresursprovidern JSRP.

På alla Author- och Publish AEM-instanser går du till konsolen Lagringskonfiguration eller kontrollerar AEM:

* I JCR, om [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Den innehåller ingen [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc)-nod, vilket betyder att lagringsprovidern är JSRP.
   * Om srpc-noden finns och innehåller noden [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration), ska standardkonfigurationens egenskaper definiera JSRP som standardprovider.

### UGC är inte synlig på författarinstans {#ugc-not-visible-on-author-instance}

Det här är inte något fel. En egenskap hos JSRP är att communityinnehåll som anges i publiceringsmiljön bara syns i Publish-miljön.

### UGC är inte synlig på Publish-instans {#ugc-not-visible-on-publish-instance}

Om en enskild Publish-instans eller ett publiceringskluster har distribuerats följer du instruktionerna för [UGC är inte synlig i JCR](#ugc-not-visible-in-jcr).

Om en publiceringsgrupp distribueras är egenskapen för JSRP att communityinnehåll bara visas på den Publish-instans som det publicerades på.

För att UGC ska vara synligt från alla Publish-instanser krävs ett publiceringskluster.
