---
title: Förhindra CSRF-attacker
seo-title: Förhindra CSRF-attacker
description: Lär dig hur du förhindrar att CSRF-attacker (Cross-site Request ForVerification) angriper webbplatser och skyddar användardata från att äventyras.
seo-description: Lär dig hur du förhindrar att CSRF-attacker (Cross-site Request ForVerification) angriper webbplatser och skyddar användardata från att äventyras.
uuid: f3553826-f5eb-40ea-aeb7-90e4ad30598c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a3cbffb7-c1d1-47c2-bcfd-70f1e2d81ac9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Förhindra CSRF-attacker {#preventing-csrf-attacks}

## Hur CSRF-attacker fungerar {#how-csrf-attacks-work}

CSRF (Cross-site request formunoration) är en sårbarhet på en webbplats där en giltig användares webbläsare används för att skicka en skadlig begäran, eventuellt via en iFrame. Eftersom webbläsaren skickar cookies på domänbasis kan användarens data bli komprometterade om användaren är inloggad i ett program.

Tänk dig till exempel ett scenario där du är inloggad på administrationskonsolen i en webbläsare. Du får ett e-postmeddelande som innehåller en länk. Du klickar på länken, vilket öppnar en ny flik i webbläsaren. Sidan som du öppnade innehåller en dold iFrame som gör en skadlig begäran till formulärservern med hjälp av cookien från din autentiserade AEM-formulärsession. Eftersom användarhantering tar emot en giltig cookie, godkänns begäran.

## CSRF-relaterade termer {#csrf-related-terms}

**** Referens: Adressen till källsidan som en begäran kommer från. En webbsida på webbplats1.com innehåller till exempel en länk till webbplats2.com. När du klickar på länken skickas en begäran till site2.com. Referenten till denna begäran är site1.com eftersom begäran görs från en sida vars källa är site1.com.

**** Godkända URI:er: URI:er identifierar resurser på formulärservern som begärs, till exempel /adminui eller /contentspace. Vissa resurser kan tillåta att en begäran skickas till programmet från externa platser. Dessa resurser betraktas som godkända URI:er. Formulärservern utför aldrig någon referenskontroll från godkända URI:er.

**** Null-referens: När du öppnar ett nytt webbläsarfönster eller en ny flik, skriver en adress och trycker på Retur är referenten null. Begäran är helt ny och kommer inte från en överordnad webbsida. Det finns därför ingen hänvisning till begäran. Formulärservern kan ta emot en null-referens från:

* begäranden som gjorts på SOAP- eller REST-slutpunkter från Acrobat
* alla skrivbordsklienter som gör en HTTP-begäran på en AEM-formulärs SOAP- eller REST-slutpunkt
* när ett nytt webbläsarfönster öppnas och URL:en för inloggningssidan för ett AEM-formulär anges

Tillåt en null-referens för SOAP- och REST-slutpunkter. Tillåt även en null-referens på alla URI-inloggningssidor som /adminui och /contentspace och deras motsvarande mappade resurser. Den mappade serverleten för /contentspace är till exempel /contentspace/faces/jsp/login.jsp, som bör vara ett null-referensundantag. Det här undantaget är bara nödvändigt om du aktiverar GET-filtrering för webbprogrammet. Programmen kan ange om null-referenser ska tillåtas. Se&quot;Skydda från attacker med smidning av förfrågningar mellan webbplatser&quot; i [Förbättring och säkerhet för AEM-formulär](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**** Undantag för tillåten referens: Tillåtet referensundantag är en underlista till listan över tillåtna referenser, från vilka begäranden blockeras. Tillåtna referensundantag gäller endast för webbprogram. Om en delmängd av Tillåtna referenter inte ska kunna anropa ett visst webbprogram kan du svartlista hänvisarna via Tillåtna referensundantag. Tillåtna referensundantag anges i filen web.xml för ditt program. (Se&quot;Skydda mot attacker med förfalskade korswebbplatser&quot; på sidan Hjälp och självstudiekurser för AEM-formulär.)

## Hur tillåtna referenser fungerar {#how-allowed-referers-work}

AEM-formulär har referensfiltrering som kan förhindra CSRF-attacker. Så här fungerar referensfiltrering:

1. Formulärservern kontrollerar HTTP-metoden som används för anrop:

   * Om det är POST utför formulärservern kontrollen av referensrubriken.
   * Om det är GET åsidosätter formulärservern referenskontrollen, såvida inte CSRF_CHECK_GETS är inställt på true, vilket innebär att referenthuvudet kontrolleras. CSRF_CHECK_GETS anges i filen web.xml för ditt program. (Se&quot;Skydda mot attacker med förfalskning av förfrågningar mellan webbplatser&quot; i [Försvårande och säkerhetsanvisning](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).)

1. Formulärservern kontrollerar om den begärda URI:n är vitlistad:

   * Om URI:n vitlistas, skickas begäran av servern.
   * Om den begärda URI:n inte är vitlistad hämtar servern referensen för begäran.

1. Om det finns en referens i begäran kontrollerar servern om det är en tillåten referens. Om det är tillåtet söker servern efter ett referensundantag:

   * Om det är ett undantag blockeras begäran.
   * Om det inte är ett undantag skickas begäran.

1. Om det inte finns någon referens i begäran kontrollerar servern om en null-referens är tillåten.

   * Om en null-referens tillåts, skickas begäran.
   * Om en null-referens inte tillåts, kontrollerar servern om den begärda URI:n är ett undantag för null-referenten och hanterar begäran därefter.

## Konfigurera tillåtna referenser {#configure-allowed-referers}

När du kör Configuration Manager läggs standardvärden och IP-adressen eller formulärservern till i listan Tillåten referens. Du kan redigera den här listan i administrationskonsolen.

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Konfiguration > Konfigurera tillåtna referens-URL:er. Listan Tillåten referens visas längst ned på sidan.
1. Så här lägger du till en tillåten referens:

   * Skriv ett värdnamn eller en IP-adress i rutan Tillåtna referenser. Om du vill lägga till mer än en tillåten referens åt gången skriver du varje värdnamn eller IP-adress på en ny rad.
   * I rutorna HTTP-port och HTTPS-portar anger du vilka portar som ska tillåtas för HTTP, HTTPS eller båda. Om du lämnar rutorna tomma används standardportarna (port 80 för HTTP och port 443 för HTTPS). Om du anger `0` (noll) i rutorna aktiveras alla portar på den servern. Du kan också ange ett specifikt portnummer för att bara aktivera den porten.
   * Klicka på Lägg till

1. Om du vill ta bort en post från listan Tillåtna referenser markerar du objektet i listan och klickar på Ta bort.

   Om listan över tillåtna referenser är tom slutar CSRF-funktionen att fungera och systemet blir osäkert.

1. När du har ändrat listan över tillåtna referenser startar du om AEM-formulärservern.

