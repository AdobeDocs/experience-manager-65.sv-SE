---
title: AEM Commerce - GDPR-beredskap
description: Lär dig mer om hur man hanterar GDPR-förfrågningar i AEM Commerce och hur man använder dem.
contentOwner: carlino
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# AEM Commerce - GDPR-beredskap{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR används som exempel i avsnitten nedan, men de ingående detaljerna gäller alla dataskydds- och sekretessbestämmelser, såsom GDPR och CCPA.

Europeiska unionens allmänna dataskyddsförordning om integritetsskydd får verkan från och med maj 2018. Se [GDPR-sidan på Adobe Privacy Center](https://business.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Se [AEM GDPR-beredskap](/help/managing/data-protection-and-privacy.md) för mer information.

![screen_shot_2018-03-22at11606](assets/screen_shot_2018-03-22at111606.jpg)

Med Adobe körklara Commerce-integreringar är AEM upplevelselagret, konsumerar tjänster och skickar tillbaka data till kundens handelsplattform som körs i headlessläge.

För vissa e-handelsplattformar lagrar Adobe profilinformation ( `/home/users`) och e-handelstoken (för inloggning på e-handelsplattformen) i AEM. Läs [Hantera GDPR-begäranden för AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at11621](assets/screen_shot_2018-03-22at111621.jpg)

## Hantera GDPR-förfrågningar för AEM {#handling-gdpr-requests-for-aem-commerce}

För Salesforce-integreringen med Commerce Cloud lagrar AEM inte någon GDPR-relevant information. Vidarebefordra begäran till [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

För hybris- och HCL WebSphere® Commerce-integreringar finns det vissa data i AEM. Använd [AEM GDPR-instruktioner](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) och fundera över följande frågor:

1. **Var lagras/används mina data?** Cachelagrad användarprofilinformation som namn, användaridentifierare för e-handel, token, lösenord och adressdata som visas AEM.
1. **Med vem delar jag de täckta GDPR-uppgifterna?** Alla uppdateringar av GDPR-relevanta data i AEM Commerce lagras inte (utom relevant profilinformation, som nämns ovan) utan läggs tillbaka till handelsplattformen.
1. **Ta bort mina användardata**? Ta bort användarprofilen i AEM och anropa användarborttagningen på handelsplattformen.

>[!NOTE]
>
>Ta en titt på [hybris wiki](https://wiki.hybris.com/) eller [HCL WebSphere® Commerce-dokumentation](https://help.hcltechsw.com/commerce/index.html), om det behövs.
