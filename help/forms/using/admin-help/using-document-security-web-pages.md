---
title: Använda webbsidor för dokumentsäkerhet
seo-title: Använda webbsidor för dokumentsäkerhet
description: Lär dig hur du kan logga in, navigera och använda webbsidorna för dokumentsäkerhet.
seo-description: Lär dig hur du kan logga in, navigera och använda webbsidorna för dokumentsäkerhet.
uuid: b4863343-cda5-474a-a101-a20e39b1f8c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2878b145-e6c0-48d3-810c-3540de13c826
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Använda webbsidor för dokumentsäkerhet {#using-the-document-security-webpages}

Användare och administratörer använder dokumentsäkerhetswebbsidorna för att skapa och hantera profiler, hantera profilskyddade dokument och övervaka händelser som är kopplade till profilskyddade dokument. Administratörer använder också webbsidorna för att skapa uppsättningar av profiler och utse samordnare för principuppsättningar, konfigurera standardinställningar för dokumentsäkerhet, hantera inbjudna användarregistreringar och konton samt övervaka och hantera server-, princip-, användar- och dokumentrelaterade händelser.

>[!NOTE]
>
>Du kan också logga in på dokumentsäkerhet via Acrobat och andra klientprogram med ditt användarkonto. (Se [Konfigurera åtkomst till dokumentsäkerhet från klientprogram](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications).)

Om du vill öppna webbsidorna måste du ha en webbläsare och en URL och inloggningsinformation för dokumentsäkerhet. URL:en för användare skiljer sig från URL:en för administratörer.

Eftersom dokumentsäkerheten hänvisar till organisationens befintliga kataloger för användarinformation, kan inloggningsinformationen för dokumentsäkerhet vara samma information som du använder för att logga in i ditt nätverk och andra program. Kontakta systemadministratören eller administratören om du vill ha kontoinformation.

Om du vill logga in som administratör måste du ha administratörsrollen tilldelad dig. Du kan använda det superadministratörskonto som skapas som standard under installationen.

## Logga in på webbsidorna {#log-in-to-the-web-pages}

Om du vill logga in på webbsidorna med en webbläsare behöver du dokumentets säkerhets-URL och ett konto. URL:en för användare skiljer sig från URL:en för administratörer. Administratörer kan även logga in på användarsidorna för att skapa profiler.

Om du har tillgång till mer än en installation av dokumentsäkerhet behöver du URL:en för den instans av dokumentsäkerhet som du vill komma åt. Kontakta administratören om du inte har den här informationen. Standardwebbadressen för användarsidorna är `https://[host]:[port]/edc`. Portnumret kanske inte krävs i vissa fall. Be administratören om mer information.

Standardwebbadressen för administratörer är `https://[host]:[port]/adminui`.

För administratörer skapas ett superadministratörskonto som standard under installationen. Du kan använda det här kontot för att logga in när dokumentsäkerhet först installeras.

>[!NOTE]
>
>Du kan även komma åt webbsidorna från Acrobat och andra klientprogram. Mer information finns i hjälpen för Acrobat eller i hjälpen för Acrobat Reader DC-tillägg.

1. Skriv URL-adressen i webbläsaren:

   Dokumentets säkerhets-URL: `https://[host]:[port]/edc`

   eller URL för administrationskonsolen: `https://[host]:[port]/adminui`

1. Skriv ditt användarnamn och lösenord i inloggningsfönstret och klicka på OK.
1. I administrationskonsolen klickar du på Tjänster > Dokumentsäkerhet.

>[!NOTE]
>
>När du arbetar med webbsidor bör du undvika att använda webbläsarknapparna, t.ex. bakåtknappen, uppdateringsknappen och bakåt- och framåtpilarna eftersom den här åtgärden kan orsaka oönskad datainhämtning och problem med visningen av data.

## Navigera på webbsidorna {#navigating-the-web-pages}

När du loggar in på användarens webbsidor visas länkar till användarsidorna för profiler, dokument och händelser.

När du loggar in på administrationskonsolen och navigerar till huvudsidan för dokumentsäkerhet kan du även se en eller två ytterligare länkar, en för konfigurationssidan och en för sidan Inbjudna och Lokala användare. Sidan Inbjudna och lokala användare visas bara om den inbjudna användarregistreringen är aktiverad.

Använd de här länkarna för att komma åt de olika sidorna, där du skapar och hanterar profiler och policyskyddade dokument.

**Visa en sida**

1. Klicka på sidans namn; till exempel klicka på Profiler.

**Gå tillbaka till föregående sida**

1. Klicka på navigeringslänken högst upp på sidan för den sida som du vill gå tillbaka till.

**Uppdatera datalistan på en sida**

1. På huvudsidan klickar du på länken till sidan som du vill uppdatera.

>[!NOTE]
>
>När du arbetar med webbsidor bör du undvika att använda webbläsarknapparna, som bakåtknappen, uppdateringsknappen samt bakåt- och framåtpilarna, eftersom den här åtgärden kan orsaka oönskade problem med datainhämtning och datavisning.

## Konfigurera åtkomst till dokumentsäkerhet från klientprogram {#setting-up-access-to-document-security-from-client-applications}

Klientprogram måste vara konfigurerade för att kunna ansluta till dokumentsäkerhet för att skydda dokument, öppna principskyddade dokument och ansluta till dokumentets säkerhetswebbsidor. Mer information om hur du konfigurerar anslutningen i klientprogrammet finns i *Acrobat-hjälpen* eller i lämplig *Rights ManagementExtension-hjälp* .

Dokumentsäkerhet nås via SSL (Secure Sockets Layer). Du måste installera webbplatsens certifikat i certifikatarkivet så att du kan komma åt dokumentsäkerhet via klientprogrammen.

<!-- Fix broken link See Configuring SSL for information on SSL.-->

De här instruktionerna är specifika för Internet Explorer, men du kan installera certifikatet med en webbläsare som stöds. Mer information finns i hjälpen till webbläsaren.

**Installera servercertifikatet med Internet Explorer**

1. Öppna webbläsaren och skriv bas-URL:en för dokumentsäkerhet i rutan Adress. For example, type `https://[host]:[port]`. Dialogrutan Säkerhetsvarning visas.
1. Klicka på Visa certifikat och sedan på Installera certifikat och välj standardinställningar för installationen. Certifikatet måste installeras i de betrodda rotcertifikatutfärdarna.
1. Stäng webbläsarsessionen.
1. Öppna ett annat webbläsarfönster och skriv samma URL i rutan Adress. En dialogruta för säkerhetsvarning ska inte visas. Det här testet bekräftar att certifikatet är korrekt installerat.

## Logga ut från webbsidorna {#log-out-of-the-web-pages}

Logga ut när du är klar med webbsidorna så att du kan använda webbläsaren i andra syften. Beroende på hur dokumentsäkerheten är konfigurerad kan du behöva stänga webbläsaren för att logga ut helt.

1. Klicka på Logga ut i det övre högra hörnet på sidan.
1. Om ett meddelande visas på utloggningssidan stänger du webbläsarfönstret för att logga ut helt. I annat fall kan du fortsätta att använda webbläsaren för andra syften.

