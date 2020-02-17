---
title: AEM Commerce - beredskap för GDPR
seo-title: AEM Commerce - beredskap för GDPR
description: 'null'
seo-description: 'null'
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# AEM Commerce - beredskap för GDPR{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR används som exempel i avsnitten nedan, men de ingående detaljerna är tillämpliga på alla dataskydds- och sekretessbestämmelser. såsom GDPR, CCPA osv.

Europeiska unionens allmänna dataskyddsförordning om integritetsskydd får verkan från och med maj 2018. Mer information finns på [GDPR-sidan på Adobe Privacy Center](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Mer information finns i [AEM GDPR-beredskap](/help/managing/data-protection-and-privacy.md) .

![screen_shot_2018-03-22at11606](assets/screen_shot_2018-03-22at111606.jpg)

I våra färdiga Commerce-integreringar är AEM upplevelselagret, konsumerar tjänster och skickar tillbaka data till kundens handelsplattform som körs i headlessläge.

För vissa e-handelsplattformar lagrar vi profilinformation ( `/home/users`) och e-handelstoken (för inloggning på e-handelsplattformen) i AEM. I dessa fall ska du läsa [Hantera GDPR-förfrågningar för AEM-plattformen](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at11621](assets/screen_shot_2018-03-22at111621.jpg)

## Hantera GDPR-begäranden för AEM Commerce {#handling-gdpr-requests-for-aem-commerce}

För Salesforce Commerce Cloud-integreringen lagrar inte AEM Commerce någon GDPR-relevant information. Du bör vidarebefordra begäran till [Salesforce Cloud](https://documentation.demandware.com/).

För hybris- och IBM WebSphere-integreringarna finns det vissa data i AEM. Du bör använda [AEM Platform GDPR-instruktionerna](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) och överväga följande frågor:

1. **Var lagras/används mina data?** Cachelagrad användarprofilinformation som namn, användaridentifierare för e-handel, token, lösenord, adressdata osv. visas från AEM.
1. **Med vem delar jag de täckta GDPR-uppgifterna?** Alla uppdateringar av GDPR-relevanta data i AEM Commerce lagras inte (utom relevant profilinformation, som nämns ovan) utan läggs tillbaka i e-handelsplattformen.
1. **Hur tar jag bort mina användardata**? Ta bort användarprofilen i AEM och anropa användarborttagningen på handelsplattformen.

>[!NOTE]
>
>Ta en titt på [hybris wiki](https://wiki.hybris.com/) eller [Websphere Commerce-dokumentationen](https://www-01.ibm.com/support/docview.wss?uid=swg27036450) om det behövs.

