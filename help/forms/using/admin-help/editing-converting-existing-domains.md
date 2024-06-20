---
title: Redigera och konvertera befintliga domäner
description: Lär dig hur du ändrar inställningarna för befintliga domäner på sidan Domänhantering. Konvertera en befintlig företagsdomän till en hybriddomän eller omvänt.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 34ac5f8b-f209-4f99-ad71-4df6f2c88c1e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Redigera och konvertera befintliga domäner{#editing-and-converting-existing-domains}

Du kan ändra inställningarna för befintliga domäner på sidan Domänhantering. Du kan också konvertera en befintlig företagsdomän till en hybriddomän.

## Redigera en befintlig domän {#edit-an-existing-domain}

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Domänhantering.
1. Klicka på namnet på den domän som ska redigeras.
1. Om du vill ändra domännamnet ändrar du texten i rutan Namn.
1. Om du vill ändra autentiseringsinformationen för ett företag eller en hybriddomän klickar du på motsvarande autentiseringsnamn längst ned på sidan. Ändra inställningarna på sidan Redigera autentisering. (Se [Autentiseringsinställningar](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Om du vill ändra kataloginformationen för en företagsdomän klickar du på lämpligt katalognamn längst ned på sidan. Ändra inställningarna på sidan Redigera katalog efter behov. (Se [Lägga till kataloger eller anpassade SPI-filer](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Klicka på OK när du är klar med ändringarna.

## Konvertera en företagsdomän till en hybriddomän {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Domänhantering.
1. Klicka på namnet på den företagsdomän som ska konverteras.
1. Klicka på Konvertera till hybrid-domän.
1. Granska informationen om användar- och gruppdata och autentisering av användare och klicka på OK.
1. Redigera inställningarna för den hybriddomänen och klicka på OK.

>[!NOTE]
>
>Om den företagsdomän som du konverterar inte innehåller kataloginställningar går alla LDAP-autentiseringsinställningar förlorade.

## Konvertera en hybriddomän till en företagsdomän {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Domänhantering.
1. Klicka på namnet på den hybriddomän som ska konverteras.
1. Klicka på Konvertera till företagsdomän.
1. Granska informationen om användar- och gruppdata och autentisering av användare och klicka på OK.
1. Klicka på Lägg till katalog och konfigurera nödvändig kataloginformation. (Se [Lägga till kataloger eller anpassade SPI-filer](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
