---
title: Konfigurera inställningar för låsning av konto
seo-title: Konfigurera inställningar för låsning av konto
description: Använd alternativet Aktivera låsning av konto om du vill låsa användarkonton efter ett angivet antal på varandra följande autentiseringsfel.
seo-description: Använd alternativet Aktivera låsning av konto om du vill låsa användarkonton efter ett angivet antal på varandra följande autentiseringsfel.
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera inställningar för låsning av konto {#configure-account-locking-settings}

När du lägger till en domän anger du om kontolåsning ska aktiveras. När alternativet Aktivera låsning av konto är markerat låses användarkonton efter ett angivet antal på varandra följande autentiseringsfel. Efter en viss tid kan användaren försöka autentisera igen. Den här funktionen förhindrar användare från att testa olika autentiseringskombinationer för att få åtkomst till systemet.

Använd inställningarna på sidan Domänhantering för att ange maximalt antal autentiseringsfel och hur länge kontona är låsta. De här inställningarna gäller för alla domäner där kontolåsning är aktiverat.

1. I administrationskonsolen klickar du på **[!UICONTROL Inställningar > Användarhantering > Domänhantering]**.
1. I rutan Maximalt antal misslyckade autentiseringar i följd anger du antalet gånger i följd som en användare inte kan försöka logga in innan kontot är låst. Standardvärdet är 20.
1. I rutan Lås upp kontot efter (minuter) anger du antalet minuter som användarkontot är låst. Efter det angivna antalet minuter kan användaren försöka logga in igen. Standardvärdet är 30.
1. Click **[!UICONTROL Save]**.

