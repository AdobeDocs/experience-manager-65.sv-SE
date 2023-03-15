---
title: Hantera certifikatåterkallningslistor
seo-title: Managing certificate revocationlists
description: Lär dig hur du hanterar listor över återkallade certifikat.
seo-description: Learn how to manage certificate revocation lists.
uuid: d8c4b64c-a273-4f5d-8b71-f6ea455c0f0a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9744cc2d-5e6b-4341-9270-43d479bdca04
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 1%

---

# Hantera certifikatåterkallningslistor{#managing-certificate-revocationlists}

Med pålitlighetslagerhantering kan du importera, redigera och ta bort listor över återkallade certifikat (CRL). Bas64 och DER-kodade listor över återkallade certifikat stöds.

## Importera en CRL {#import-a-crl}

1. I administrationskonsolen klickar du på Inställningar > Lita på arkivhantering > Lista över återkallade certifikat och sedan på Importera.
1. Ange en identifierare för CRL i rutan Alias.
1. Klicka på Bläddra för att leta upp listan över återkallade certifikat och klicka sedan på OK.

## Exportera en CRL {#export-a-crl}

1. I administrationskonsolen klickar du på Inställningar > Lita på arkivhantering > Lista över återkallade certifikat.
1. Klicka på aliasnamnet för den lista över återkallade certifikat som ska exporteras och klicka sedan på Exportera.
1. Följ instruktionerna för att exportera CRL:en. CRL-listor exporteras i Base64-kodning.
1. Klicka på OK.

## Ta bort en CRL {#delete-a-crl}

1. I administrationskonsolen klickar du på Inställningar > Lita på arkivhantering > Lista över återkallade certifikat.
1. Markera kryssrutorna för de listor över återkallade certifikat som ska tas bort, klicka på Ta bort och sedan på OK.
