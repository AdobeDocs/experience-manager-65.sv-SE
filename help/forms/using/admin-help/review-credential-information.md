---
title: Granska användarinformation för autentiseringsuppgifter
seo-title: Review credential use information
description: Lär dig hur du granskar användarinformation för autentiseringsuppgifter.
seo-description: Learn how to review credential use information.
uuid: 02af75f9-c235-470d-a98b-a2102aa31381
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cdf61cff-768b-49f7-9926-400bc96b0708
exl-id: a8e16cf8-f3c8-48ce-87da-2f0de0b10a6e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
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
