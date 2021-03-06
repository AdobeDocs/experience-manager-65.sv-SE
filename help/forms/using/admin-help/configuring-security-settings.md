---
title: Konfigurera säkerhetsinställningar
seo-title: Konfigurera säkerhetsinställningar
description: Lär dig hur du konfigurerar säkerhetsinställningar.
seo-description: Lär dig hur du konfigurerar säkerhetsinställningar.
uuid: 9747f268-3551-4064-8dba-e1de4a577843
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a89ab508-173f-4b1c-88d9-ef944af4d9ae
feature: PDF Generator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---


# Konfigurera säkerhetsinställningar{#configuring-security-settings}

Du kan begränsa åtkomsten till PDF-dokument genom att ange lösenord och begränsa vissa funktioner, som utskrift och redigering. När ett PDF-dokument har begränsade funktioner är verktyg och menyalternativ som är relaterade till dessa funktioner nedtonade. Du kan också använda andra metoder för att skapa säkra dokument, till exempel kryptera eller certifiera ett dokument. En säkerhetsinställning innehåller lösenordet och specifika alternativ för vissa PDF-konverteringar.

På sidan Säkerhetsinställningar kan du göra följande:

## Skapa eller redigera en säkerhetsinställning {#create-or-edit-a-security-setting}

En *säkerhetsinställning* styr säkerhet och behörigheter för filer som konverteras med den säkerhetsinställningen.

1. I administrationskonsolen klickar du på Tjänster > PDF Generator > Skyddsinställningar.
1. Klicka på Ny eller klicka på namnet på en säkerhetsinställning.
1. Fyll i den information som krävs för säkerhetsinställningen på sidan Ny/Redigera säkerhetsinställning. (Se [Konfigurera filtypsinställningar](/help/forms/using/admin-help/configuring-file-type-settings.md#configuring-file-type-settings).)
1. Klicka på Spara och skriv ett namn för inställningen i dialogrutan som visas och klicka sedan på OK.

### Säkerhetsinställningar {#security-settings}

De här inställningarna konfigurerar kompatibilitet och kryptering. Instruktioner om hur du får åtkomst till teckensnittsinställningarna finns i [Skapa eller redigera en säkerhetsinställning](configuring-security-settings.md#create-or-edit-a-security-setting).

**Kompatibilitet:** Anger krypteringstypen för att öppna ett lösenordsskyddat dokument. För alternativet Acrobat 3.0 och senare används en låg krypteringsnivå, men för de andra alternativen används en hög krypteringsnivå:

**Acrobat 3.0 och senare:** Använder låg krypteringsnivå (40-bitars RC4).

**Acrobat 5.0 och senare:** Använder hög kryptering (128-bitars RC4).

**Acrobat 6.0 och senare:** Använder hög kryptering (128-bitars RC4). Med det här alternativet kan du aktivera metadata för sökning.

**Acrobat 7.0 och senare:** Använder hög kryptering (128-bitars AES). Med det här alternativet kan du aktivera metadata för sökning och kryptering av endast bifogade filer.

**Acrobat 9.0 och senare:** Använder hög kryptering (256-bitars AES). Med det här alternativet kan du aktivera metadata för sökning och kryptering av endast bifogade filer.

En tidigare version av Acrobat kan inte öppna ett PDF-dokument med en högre kompatibilitetsinställning. Om du t.ex. väljer alternativet Acrobat 7.0 och senare kan du inte öppna dokumentet i Acrobat 6.0 eller tidigare.

Kontrollera att kompatibilitetsnivån är konsekvent med PDF-kompatibilitetsnivån för samma källa. Om du till exempel har en bevakad mapp som är konfigurerad att använda standardinställningen för PDF, som är kompatibel med Acrobat 5.0 eller senare, får din kompatibilitetsnivå inte vara högre än Acrobat 5.0.

**Dokumentbegränsning:** Vilka dokumentbegränsningar som är tillgängliga beror på vilket kompatibilitetsalternativ du har valt.

**Ingen kryptering:** Krypterar inte någon del av dokumentet.

**Kryptera allt dokumentinnehåll:** Krypterar dokumentet och dokumentets metadata. När det här alternativet är markerat kan sökmotorer inte komma åt dokumentets metadata.

**Kryptera allt innehåll i dokumentet utom metadata (Acrobat 6 och senare):** Krypterar innehållet i ett dokument men tillåter ändå sökmotorer att få åtkomst till dokumentets metadata. Det här alternativet är bara tillgängligt när du har valt Acrobat 6.0 eller senare, Acrobat 7.0 eller senare eller Acrobat 9.0 eller senare.

**Kryptera endast bifogade filer (Acrobat 7 och senare):** Användare kan öppna dokumentet utan lösenord men måste ange ett lösenord för att kunna öppna bifogade filer. Det här alternativet är bara tillgängligt när du har angett Kompatibilitet till Acrobat 7.0 eller senare eller till Acrobat 9.0 eller senare.

De här inställningarna konfigurerar lösenordsskyddet:

>[!NOTE]
>
>Om du glömmer bort lösenordet kan det inte återställas från dokumentet. Vi rekommenderar att du lagrar lösenord på en annan säker plats ifall du skulle glömma dem. Spara också en säkerhetskopia av dokumentet som inte är lösenordsskyddat.

**Kräv ett lösenord för att öppna dokumentet:** Aktiverar lösenordsalternativen.

**Lösenord för att öppna dokument:** Förhindrar att användare öppnar dokumentet om de inte skriver det lösenord som du anger. Lösenord är skiftlägeskänsliga. Acrobat använder RC4-säkerhetsmetoden från RSA Security Inc. för att lösenordsskydda PDF-dokument. Om du begränsar utskrift och redigering rekommenderar vi att du lägger till ett lösenord för dokumentöppning för att öka säkerheten.

**Skriv lösenordet för dokumentöppning igen:** Ser till att lösenordet för dokumentöppning är korrekt.

**Kräv ett lösenord för att öppna bifogade filer:** Aktiverar lösenordsalternativen. Det här alternativet är endast tillgängligt när alternativet Kompatibilitet är inställt på Acrobat 7.0 eller senare eller på Acrobat 9.0 eller senare och alternativet Dokumentbegränsning är inställt på Kryptera endast bifogade filer.

**Lösenord för att öppna bifogad fil:** Ser till att ett lösenord krävs för att öppna en bifogad fil. Användarna kan öppna dokumentet utan lösenord. Det här alternativet är endast tillgängligt när alternativet Kompatibilitet är inställt på Acrobat 7.0 eller senare eller på Acrobat 9.0 eller senare och alternativet Dokumentbegränsning är inställt på Kryptera endast bifogade filer.

**Skriv in bifogad fil igen:** Ser till att lösenordet är korrekt. Det här alternativet är endast tillgängligt när alternativet Kompatibilitet är inställt på Acrobat 7.0 eller senare eller på Acrobat 9.0 eller senare och alternativet Dokumentbegränsning är inställt på Kryptera endast bifogade filer.

De här alternativen konfigurerar behörigheter:

**Använd ett lösenord för att begränsa utskrift och redigering av dokumentet och dess skyddsinställningar:** Aktiverar behörighetsbegränsningar.

**Lösenord för behörighet:** hindrar användare från att skriva ut och redigera. Användarna kan inte ändra de här säkerhetsinställningarna såvida de inte skriver det lösenord som du anger. Du kan inte använda samma lösenord som används för lösenord för att öppna dokument. När du anger ett behörighetslösenord kan bara de personer som skriver lösenordet ändra säkerhetsinställningarna. Om PDF-dokumentet har båda typerna av lösenord öppnas det i båda lösenorden. En användare kan dock bara ange eller ändra de begränsade funktionerna med behörighetslösenordet. Om PDF-dokumentet bara har behörighetslösenordet eller om en användare öppnar dokumentet med hjälp av lösenordet för dokumentöppning, visas lösenordsmeddelandet när användaren försöker ändra säkerhetsinställningarna.

**Skriv lösenordet för behörighet igen:** ser till att lösenordet för behörighet är korrekt.

**Tillåtna utskrifter:** Anger utskriftskvaliteten för PDF-dokumentet:

**Inget:** Förhindrar att användare skriver ut dokumentet.

**Låg upplösning (150 dpi):** Tillåter användare att skriva ut dokumentet med en upplösning som inte överstiger 150 dpi. Utskriften kan ta längre tid eftersom varje sida skrivs ut som en bitmappsbild. Det här alternativet är bara tillgängligt om du har valt en hög krypteringsnivå (Acrobat 5.0, 6.0, 7.0 eller 9.0).

**Hög upplösning:** Användare kan skriva ut med valfri upplösning och dirigera högkvalitativa vektorutdata till PostScript-skrivare och andra skrivare som stöder avancerade högkvalitativa utskriftsfunktioner.

**Tillåtna ändringar:** Definierar vilka redigeringsåtgärder som tillåts i PDF-dokumentet:

**Inget:** Hindrar användare från att ändra dokumentet, inklusive fylla i signatur- och formulärfält.

**Infoga, ta bort och rotera sidor:** Låter användarna infoga, ta bort och rotera sidor samt skapa bokmärken och miniatyrsidor. Det här alternativet är bara tillgängligt om du har valt en hög krypteringsnivå (Acrobat 5.0, 6.0, 7.0 eller 9.0).

**Fylla i formulärfält och signera befintliga signaturfält:** Låter användarna fylla i formulär och lägga till digitala signaturer. Användarna kan dock inte lägga till kommentarer eller skapa formulärfält. Det här alternativet är bara tillgängligt om du har valt en hög krypteringsnivå (Acrobat 5.0, 6.0, 7.0 eller 9.0).

**Kommentera, fylla i formulärfält och signera befintliga signaturfält:** Låter användarna fylla i formulär och lägga till digitala signaturer och kommentarer.

**Sidlayout, slutredigering, ifyllning av formulärfält och signering av befintliga signaturfält:** Låter användarna infoga, rotera eller ta bort sidor och skapa bokmärken eller miniatyrbilder, fylla i formulär och lägga till digitala signaturer. Det här alternativet tillåter inte användare att skapa formulärfält. Det här alternativet är bara tillgängligt om du har valt en låg krypteringsnivå (Acrobat 3.0).

**Valfritt utom att extrahera sidor:** Låter användare ändra dokumentet med någon metod i Tillåtelselista Ändringar, förutom att ta bort sidor.

**Aktivera kopiering av text, bilder och annat innehåll:** Låter användarna markera och kopiera innehållet i PDF-dokumentet. Det ger även verktyg som behöver ha tillgång till innehållet i en PDF-fil, t.ex. Acrobat Catalog, tillgång till innehållet. Det här alternativet är bara tillgängligt om du har valt en hög krypteringsnivå.

**Aktivera textåtkomst för skärmläsarenheter med nedsatt syn:** Gör att användare med nedsatt syn kan läsa dokumentet med skärmläsare. Användarna kan dock inte kopiera eller extrahera dokumentinnehållet. Det här alternativet är bara tillgängligt om du har valt en hög krypteringsnivå.

## Ta bort en säkerhetsinställning {#delete-a-security-setting}

Du kan ta bort en säkerhetsinställning om den inte längre behövs. Förkonfigurerade säkerhetsinställningar kan dock inte tas bort.

1. Klicka på **[!UICONTROL Services > PDF Generator > Security Settings]** i administrationskonsolen.
1. Markera kryssrutan bredvid inställningen som ska tas bort. Du kan välja flera inställningar.
1. Klicka på **[!UICONTROL Delete]** och klicka på **[!UICONTROL Delete]** igen på sidan **[!UICONTROL Delete Confirmation]**.

