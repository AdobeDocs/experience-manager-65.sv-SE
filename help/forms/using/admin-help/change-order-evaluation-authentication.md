---
title: Ändra utvärderingsordningen för autentisering
seo-title: Change the order of evaluation for authentication
description: Du kan ändra ordningen i vilken AEM utvärderas av flera autentiseringsleverantörer.
seo-description: You can change the order in which AEM forms evaluates multiple authentication providers.
uuid: c2693e5b-cf09-4bb8-815a-2b20ebf6eea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5434df9c-ecf6-450a-aa7e-d9ab69b66fe6
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Ändra utvärderingsordningen för autentisering {#change-the-order-of-evaluation-for-authentication}

Om du har konfigurerat flera autentiseringsleverantörer kan du ändra i vilken ordning AEM utvärderas för autentisering. Ordningen på de autentiseringsproviders som visas i filen config.xml avgör ordningen på utvärderingen av autentiseringen.

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Konfiguration > Importera och exportera konfigurationsfiler.
1. Om du vill exportera den aktuella konfigurationsinställningen till en fil klickar du på Exportera och sparar konfigurationsfilen på en annan plats.
1. Sök efter följande nod i filen:

   ```xml
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

   I `<entry key="order" value="3" />`, redigera värdet för varje nod för att ange ordningen för autentiseringsutvärderingen.

1. Om du vill importera den uppdaterade filen klickar du i Användarhantering på Konfiguration > Importera och exportera konfigurationsfiler.
1. Klicka på Bläddra för att hitta filen, klicka på Importera och sedan på OK.
