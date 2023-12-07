---
title: Konfigurera inställningar för låsning av konto
description: Använd alternativet Aktivera låsning av konto om du vill låsa användarkonton efter ett angivet antal på varandra följande autentiseringsfel.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Konfigurera inställningar för låsning av konto {#configure-account-locking-settings}

När du lägger till en domän anger du om kontolåsning ska aktiveras. När alternativet Aktivera låsning av konto är markerat låses användarkonton efter ett angivet antal på varandra följande autentiseringsfel. Efter en viss tid kan användaren försöka autentisera igen. Den här funktionen förhindrar användare från att testa olika autentiseringskombinationer för att få åtkomst till systemet.

Använd inställningarna på sidan Domänhantering för att ange maximalt antal autentiseringsfel och hur länge kontona är låsta. De här inställningarna gäller för alla domäner där kontolåsning är aktiverat.

1. I administrationskonsolen klickar du på **[!UICONTROL Settings > User Management > Domain Management]**.
1. I rutan Maximalt antal misslyckade autentiseringar i följd anger du antalet gånger i följd som en användare inte kan försöka logga in innan kontot är låst. Standardvärdet är 20.
1. I rutan Lås upp kontot efter (minuter) anger du antalet minuter som användarkontot är låst. Efter det angivna antalet minuter kan användaren försöka logga in igen. Standardvärdet är 30.
1. Klicka på **[!UICONTROL Save]**.
