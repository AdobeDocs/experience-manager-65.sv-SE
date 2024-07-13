---
title: AEM Commerce - GDPR-beredskap
description: Lär dig mer om hur du hanterar GDPR-förfrågningar i AEM Commerce och hur du använder dem.
contentOwner: carlino
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
solution: Experience Manager, Experience Manager Sites
feature: Compliance
role: Admin, Architect, Developer, Leader, User, Data Architect, Data Engineer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# AEM Commerce - GDPR-beredskap{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR används som exempel i avsnitten nedan, men de ingående detaljerna gäller alla dataskydds- och sekretessbestämmelser, såsom GDPR och CCPA.

Europeiska unionens allmänna dataskyddsförordning om integritetsskydd får verkan från och med maj 2018. Se sidan [GDPR på Adobe Privacy Center](https://business.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Mer information finns i [AEM GDPR-beredskap](/help/managing/data-protection-and-privacy.md).

![screen_shot_2018-03-22at11606](assets/screen_shot_2018-03-22at111606.jpg)

Med Adobe körklara Commerce-integreringar är AEM upplevelselagret, konsumerar tjänster och skickar tillbaka data till kundens e-handelsplattform som körs i headlessläge.

För vissa e-handelsplattformar lagrar Adobe profilinformation ( `/home/users`) och e-handelstoken (för inloggning på e-handelsplattformen) i AEM. Läs [Hantera GDPR-begäranden för AEM ](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) om du vill använda dessa exempel.

![screen_shot_2018-03-22at11621](assets/screen_shot_2018-03-22at111621.jpg)

## Hantera GDPR-begäranden för AEM Commerce {#handling-gdpr-requests-for-aem-commerce}

För Salesforce-integreringen med Commerce Cloud lagrar AEM Commerce ingen GDPR-relevant information. Vidarebefordra begäran till [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

För hybris- och HCL WebSphere® Commerce-integreringar finns det vissa data i AEM. Använd [AEM-plattformens GDPR-instruktioner](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) och överväg följande frågor:

1. **Var lagras/används mina data?** cachelagrad användarprofilinformation som namn, användaridentifierare för e-handel, token, lösenord och adressdata som visas AEM.
1. **Med vem delar jag GDPR-data som omfattas?** Alla uppdateringar av GDPR-relevanta data i AEM Commerce lagras inte (förutom relevant profilinformation, som nämns ovan), utan proxyskickas tillbaka till handelsplattformen.
1. **Hur tar jag bort mina användardata**? Ta bort användarprofilen i AEM och anropa användarborttagningen på handelsplattformen.

>[!NOTE]
>
>Ta en titt på [hybris wiki](https://wiki.hybris.com/) eller [HCL WebSphere® Commerce-dokumentationen](https://help.hcltechsw.com/commerce/index.html) om det behövs.
