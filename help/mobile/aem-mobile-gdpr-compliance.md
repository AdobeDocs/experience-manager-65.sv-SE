---
title: AEM Mobile - GDPR-beredskap
seo-title: AEM Mobile - GDPR-beredskap
description: 'null'
seo-description: 'null'
uuid: 817c434f-4b78-40f7-99d6-6efafdedb77e
contentOwner: trushton
discoiquuid: 9399dd3d-a485-4f53-a6f2-7b190da4235b
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# AEM Mobile - GDPR-beredskap {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR används som exempel i avsnitten nedan, men de ingående detaljerna är tillämpliga på alla dataskydds- och sekretessbestämmelser. såsom GDPR, CCPA osv.

## Stöd för AEM Mobile GDPR {#aem-mobile-gdpr-support}

AEM Mobile är redo att hjälpa kunderna med deras GDPR-efterlevnadsskyldigheter. Inga personuppgifter lagras i AEM Mobile. Om du är etablerad kan du logga in på Adobe Experience Mobile med ditt Adobe ID.

[https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html)

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

Adobes digitala publiceringsprodukt (som föregår AEM Mobile) stöder Adobes beredskapsinitiativ i GDPR. Se [https://www.adobe.com/privacy/general-data-protection-regulation.html](https://www.adobe.com/privacy/general-data-protection-regulation.html). Nedan finns information om stöd för GDPR-relevanta funktioner i Digital Publishing Suite-produkten, inklusive hur du arbetar med Adobe för att initiera GDPR-förfrågningar.

För att vara säker på att du inte blandar ihop AEM Mobile med den äldre Digital Publishing Suite-produkten kan du logga in på Digital Publishing Suite här:

[https://digitalpublishing.acrobat.com/welcome.html](https://digitalpublishing.acrobat.com/welcome.html)

### Initiera en GDPR-begäran {#initiating-a-gdpr-request}

Kontakta Adobes kundtjänst för att få en GDPR-förfrågan om Digital Publishing Suite.

Följande ID krävs för att hitta kunddata. Alla delmängder som tas emot innebär att andra ID:n inte är tillämpliga för den här användaren.

Obligatorisk:

* Kundens kontrakt-ID: *dpsc-contractId*

Ange minst 1 av följande:

* Slutanvändarens kund tillhandahöll OAuth ID (det ID som används i kundens system för direkttillstånd): *dpsc-directEntitlementId*
* För Windows-appanvändare, slutanvändarens App Store-ID: *dpsc-windowsAppStoreId*
* E-postadressen som slutanvändaren använde för att interagera med DPS-appen: *e-post*

### Vanliga frågor och svar (FAQ) {#frequently-asked-questions-faq}

**Kommer Adobe att ta bort mina App Store-köp när jag initierar en DELETE-begäran?**

Adobe raderar information om App Store-köp (prenumerationer osv.) men inköp registreras fortfarande i appbutikerna. Om appen (slutanvändaren) är inloggad i App Store hämtas dessa kvitton igen och skickas till Adobe, och därefter betraktas de som nya inköp och återställs av appen för att få åtkomst igen.

**Kommer Adobe att ta bort kundens angivna rättigheter när en DELETE-begäran initieras?**

Adobe kommer att ta bort information om kundens ytterligare rättigheter. Om appen (slutanvändaren) loggar in på den OAuth-mekanism som kunden har använt, skickar den information till Adobe och tjänsterna hämtar de extra berättigandena igen.

**Vad förväntas av slutanvändaren?**

Eftersom nyckeln för att tilldela behörigheter till appen finns på enheten som en del av visningsprogramprogramvaran bör slutanvändaren avinstallera appen. Slutanvändaren bör inse att om de installerar om appen kommer befintliga inköp (som är kopplade till App Store-användaren) och direkta berättigandetillägg (som är kopplade till OAuth-användaren av kunden) fortfarande att återställas.

**Vad händer när en app delas mellan personer på en enhet?**

Adobe har mycket lite information som associeras direkt med en viss användare. Den associerar data med ett slumpmässigt skapat UUID som finns i appens data och skickas i varje begäran som appen initierar. Det innebär att slutanvändare som delar appen på samma enhet kommer att använda samma UUID och att alla data kommer att anses ägda av den person som gör GDPR-begäran. För både Access- och Delete-begäranden kommer DPSC att betrakta personer som delar en app som en person.

**Vilka personuppgifter spåras med Analytics?**

Inget. Data spåras, men på appnivå (inte personlig). Detta inkluderar händelser som starter, krascher, stängningar, aktiviteter, köp eller folioövertäckningar. Geografiska platser, namn, enhets-ID:n eller IP-adresser spåras inte.

**Slutanvändaren tillhandahöll sin information men inget hittades. Varför inte?**

I takt med att Digital Publishing Suite-produkten utvecklades ändrades implementeringarna av tjänsterna och mer data försvårades. Om inga data hittades med användarens angivna data betyder det att användarens data inte kan spåras tillbaka till den personen.

### Exempel {#example}

Kontakta Adobes kundtjänst för att få en GDPR-förfrågan.

Här följer ett exempel på indata och resultat från en Digital Publishing Suite GDPR-förfrågan:

#### Indata: {#inputs}

```
dpsc-contractId = “12345-1234-12416234” 
directEntitlementId = “1234-1234-1234” 
windowsAppStoreId = “testWinAppStoreId” 
email = “test@what.com”
```

#### Utdata {#outputs}

```
{

    "jobId": "test-1524750204384",

    "product": "DPSC",

    "action": "access",

    "userIDS": [

        {

        "namespace": "email",

        "value": "test@what.com"

        },

        {

        "namespace": "windowsAppStoreId",

        "value": "testWinAppStoreId"

        },

        {

        "namespace": "directEntitlementId",

        "value": "1234-1234-1234"

        }

    ],

    "receiptData": {

    "recordsFound": 6,

    "recordsAffected": 0,

    "tablesModified": 0,

    "subscriptionsFound": 24,

    "entitlementsFound": 24

    },

    "records": {

        "DPS_Stage_EntitlementUserDevices": [

        {

            "user_id": "testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "device_id": "appleStore:test1b16-f032-4d9c-9200-0d19999405c4",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test967d-5179-4dc6-958c-facd9d94da38",

            "device_id": "appleStore:test3f07-d5aa-4b32-8fac-b2b690b7ccd7",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test1838-6494-4e74-912c-1edf61581d0e",

            "device_id": "appleStore:test3813-f8cc-49ce-b021-50eb0814a3bb",

            "account_id": "1234-1234-1234"

        },

        {

            "user_id": "test5468-1a11-4e4c-be43-274181a9ef81",

            "device_id": "appleStore:testf082-2783-498d-ab62-b1b2e3eb67ae",

            "account_id": "1234-1234-1234"

        }

        ],

            "DPS_Stage_EntitlementUsers": [

        {

            "id": "store:test04a7-33a3-4b90-863d-79981ead0f19:appleStore",

            "part_id": "0",

            "alias_user_id": "testWinAppStoreId"

        },

        {

            "id": "internal:testd2da-0606-4444-87ef-0d5a1d4a121d:adobe",

            "part_id": "0",

            "user_id": "test@what.com"

        }

        ],

            "DPS_Stage_Subscriptions": [

        {

            "id": "appleStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test3531-a209-4391-beb9-951c7822244e",

            "overflow": "test4e59-86a8-4b75-b699-77e980c287ab",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "test491b-379e-4d24-96ef-e481bf8d3062",

            "overflow": "test931b-7422-485d-85a5-134828187b6c",

            "entitlement_count": "12"

        }

        ],

            "DPS_Stage_Entitlements": [

        {

            "id": "samsungStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test7332-60a0-42b8-a508-474668d83d2e",

            "overflow": "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "testf766-102a-460d-8f5a-42f7bb9d68b7",

            "overflow": "test4d96-2197-45a8-9caf-2aa2846b770c",

            "entitlement_count": "12"

        }

        ],

            "s3Buckets": {

            "name": "DPS-Entitlements-Overflow",

            "folder": "stage/",

            "overflows": {

            "subscriptions": [

            "test4e59-86a8-4b75-b699-77e980c287ab",

            "test931b-7422-485d-85a5-134828187b6c"

        ],

            "entitlements": [

            "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "test4d96-2197-45a8-9caf-2aa2846b770c"

                ]

            }

        }

    }

}
```

