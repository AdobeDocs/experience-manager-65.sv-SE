---
title: Konfigurera AEM-formulär för förhämtningsdomäninformation
seo-title: Konfigurera AEM-formulär för förhämtningsdomäninformation
description: Konfigurera AEM-formulär för att förhämta domäninformation om du får en långsammare svarstid på grund av djupt inkapslade grupper eller om du är medlem i många grupper.
seo-description: Konfigurera AEM-formulär för att förhämta domäninformation om du får en långsammare svarstid på grund av djupt inkapslade grupper eller om du är medlem i många grupper.
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera AEM-formulär för förhämtningsdomäninformation {#configure-aem-forms-to-prefetchdomain-information}

Användare kan få en långsammare svarstid om de tillhör många grupper (till exempel 500 eller fler) eller om grupperna är djupt inkapslade (till exempel 30 nivåer). Om du får det här problemet kan du konfigurera AEM-formulär så att information från vissa domäner hämtas i förväg.

1. I administrationskonsolen klickar du på **[!UICONTROL Inställningar > Användarhantering > Konfiguration > Importera och exportera konfigurationsfiler]**.
1. Om du vill exportera den aktuella konfigurationsinställningen till en fil klickar du på **[!UICONTROL Exportera]** och sparar konfigurationsfilen på en annan plats.
1. Lägg till följande nod (markerad med fet stil):

   ```as3
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

   I det här exemplet har flera domäner konfigurerats för förhämtning. Domännamnen avgränsas med &quot;/&quot;. Detta visas i exemplet ovan med *Domain_Name1*, *Domain_Name2* och *Domain_Name3*.

1. Om du vill importera den uppdaterade filen går du till Användarhantering och klickar på **[!UICONTROL Konfiguration > Importera och exportera konfigurationsfiler]**.
1. Klicka på **[!UICONTROL Bläddra]** för att hitta filen, klicka på Importera och sedan på **[!UICONTROL OK]**.

