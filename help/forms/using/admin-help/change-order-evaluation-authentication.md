---
title: Ändra utvärderingsordningen för autentisering
seo-title: Ändra utvärderingsordningen för autentisering
description: Du kan ändra ordningen i vilken AEM-formulär utvärderar flera autentiseringsleverantörer.
seo-description: Du kan ändra ordningen i vilken AEM-formulär utvärderar flera autentiseringsleverantörer.
uuid: c2693e5b-cf09-4bb8-815a-2b20ebf6eea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5434df9c-ecf6-450a-aa7e-d9ab69b66fe6
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ändra utvärderingsordningen för autentisering {#change-the-order-of-evaluation-for-authentication}

Om du har konfigurerat flera autentiseringsleverantörer kan du ändra ordningen i vilken AEM-formulär utvärderar dem för autentisering. Ordningen på de autentiseringsproviders som visas i filen config.xml avgör ordningen på utvärderingen av autentiseringen.

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Konfiguration > Importera och exportera konfigurationsfiler.
1. Om du vill exportera den aktuella konfigurationsinställningen till en fil klickar du på Exportera och sparar konfigurationsfilen på en annan plats.
1. Sök efter följande nod i filen:

   ```as3
    <node name="AuthSchemes">
        <map />
            <node name="CertificateAuth">
                <map>
                    <entry key="order" value="3" />
                    <entry key="name" value="edc.server.auth.scheme.certificate" />
                </map>
        </node>
        <node name="Kerberos">
            <map>
                <entry key="kerberosSPN" value="defaultSPN" />
                <entry key="order" value="1" />
                <entry key="name" value="edc.server.auth.scheme.kerberos" />
            </map>
    </node>
   ```

   I `<entry key="order" value="3" />`redigerar du värdet för varje nod för att ange ordningen för autentiseringsutvärderingen.

1. Om du vill importera den uppdaterade filen klickar du i Användarhantering på Konfiguration > Importera och exportera konfigurationsfiler.
1. Klicka på Bläddra för att hitta filen, klicka på Importera och sedan på OK.

