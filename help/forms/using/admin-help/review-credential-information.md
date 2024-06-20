---
title: Granska användarinformation för autentiseringsuppgifter
description: Lär dig hur du granskar informationen om autentiseringsuppgifter. Information om hur de används i inloggningsuppgifterna finns i Acrobat Reader-tillägget.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8e16cf8-f3c8-48ce-87da-2f0de0b10a6e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# Granska användarinformation för autentiseringsuppgifter {#review-credential-use-information}

Autentiseringsuppgiften innehåller information som beskriver dess avsedda användning och som är tillgänglig via Acrobat Reader DC-tilläggens slutanvändarwebbprogram. Du kan använda den här informationen för att avgöra vilken typ av autentiseringsuppgifter som är installerad (utvärdering eller produktion) och dess giltighetsdatum.

1. Öppna en webbläsare och ange följande URL:

   http://localhost:port/ReaderExtensions (där *port* är programserverns portnummer)

1. Logga in med standardanvändarnamnet och standardlösenordet:

   Användarnamn: administratör

   Lösenord: lösenord

   >[!NOTE]
   >
   >Du måste ha behörighet som administratör eller superanvändare för att kunna logga in med standardanvändarnamnet och standardlösenordet. Om du vill ge andra användare åtkomst till Acrobat Reader DC-tillägg skapar du användarkontona i Användarhantering och ger användarna rollen Acrobat Reader DC-tillägg för webbprogram.

1. Välj autentiseringsalias i listan Välj autentiseringsuppgifter och granska informationen som finns i Förfallodatum och Meddelande om avsedd användning.

>[!NOTE]
>
>Giltighetstiden för autentiseringsuppgifterna finns också på sidan Inställningar > Hantering av förtroendearkiv > Lokala autentiseringsuppgifter i administrationskonsolen, under Förfallodatum.
