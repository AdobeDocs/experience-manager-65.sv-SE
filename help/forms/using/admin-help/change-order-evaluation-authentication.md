---
title: Ändra utvärderingsordningen för autentisering
description: Du kan ändra ordningen i vilken AEM utvärderas av flera autentiseringsleverantörer.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Ändra utvärderingsordningen för autentisering {#change-the-order-of-evaluation-for-authentication}

>[!NOTE]
> 
> Kontrollera att användaren har administratörsbehörighet för att komma åt administratörskonsolen.

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

   I `<entry key="order" value="3" />` redigerar du värdet för varje nod för att ange ordningen för autentiseringsutvärderingen.

1. Om du vill importera den uppdaterade filen går du till Användarhantering och klickar på Konfiguration > Importera och exportera konfigurationsfiler.
1. Klicka på Bläddra för att hitta filen, klicka på Importera och sedan på OK.
