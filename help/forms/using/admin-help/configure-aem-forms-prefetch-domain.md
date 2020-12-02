---
title: Konfigurera AEM formulär för förhämtning av domäninformation
seo-title: Konfigurera AEM formulär för förhämtning av domäninformation
description: Konfigurera AEM för att hämta domäninformation i förväg om du får en långsammare svarstid på grund av djupt inkapslade grupper eller om du är medlem i många grupper.
seo-description: Konfigurera AEM för att hämta domäninformation i förväg om du får en långsammare svarstid på grund av djupt inkapslade grupper eller om du är medlem i många grupper.
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Konfigurera AEM formulär till förhämtningsdomäninformation {#configure-aem-forms-to-prefetchdomain-information}

Användare kan få en långsammare svarstid om de tillhör många grupper (till exempel 500 eller fler) eller om grupperna är djupt inkapslade (till exempel 30 nivåer). Om du får problem kan du konfigurera AEM formulär så att information från vissa domäner hämtas i förväg.

1. Klicka på **[!UICONTROL Settings > User Management > Configuration > Import And Export Configuration Files]** i administrationskonsolen.
1. Om du vill exportera den aktuella konfigurationsinställningen till en fil klickar du på **[!UICONTROL Export]** och sparar konfigurationsfilen på en annan plats.
1. Lägg till följande nod (markerad med fet stil):

   ```xml
    <node name="UM">
    <map/>
    <node name="PrincipalCache">
        <map>
            <entry key="principalCacheSize" value="1000"/>
            <entry key="principalCacheBatchFetchSize" value="10"/>
            <entry key="rebuildCacheAfterSync" value="true />
            <entry key="enableFullPrefetch" value="false"/>
            <entry key="principalCacheDomains" value="Domain_Name1/Domain_Name2/Domain_Name3"/>
        <map>
    </node>
    <node name="APSAuditService">
   ```

   I det här exemplet har flera domäner konfigurerats för förhämtning. Domännamnen avgränsas med &quot;/&quot;. Detta visas i exemplet ovan med *Domännamn1*, *Domännamn2* och *Domännamn3*.

1. Om du vill importera den uppdaterade filen klickar du på **[!UICONTROL Configuration > Import And Export Configuration Files]** i Användarhantering.
1. Klicka på **[!UICONTROL Browse]** för att hitta filen, klicka på Importera och sedan på **[!UICONTROL OK]**.

