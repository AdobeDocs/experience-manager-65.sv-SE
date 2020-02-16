---
title: Använda regeluppsättningar för att omforma URL:er
description: Du kan distribuera regeluppsättningar i Dynamic Media för att omvandla URL:er. Regeluppsättningar är instruktioner skrivna i ett skriptspråk (t.ex. JavaScript) som utvärderar XML-data och utför vissa åtgärder om dessa data uppfyller vissa villkor.
uuid: 9fed0c83-67b7-4483-a9b4-322e6a483449
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: abcff903-204b-4ab6-87d8-6f0ce63d7b41
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Använda regeluppsättningar för att omforma URL:er {#using-rulesets-to-transform-urls}

Du kan distribuera regeluppsättningar i Dynamic Media för att omvandla URL:er. Regeluppsättningar är instruktioner skrivna i ett skriptspråk (t.ex. JavaScript) som utvärderar XML-data och utför vissa åtgärder om dessa data uppfyller vissa villkor. Varje regel består av minst ett villkor och minst en åtgärd. En regel utvärderar XML-data mot villkoren, och om ett villkor är uppfyllt utförs rätt åtgärd. Exempel på regeluppsättningar är följande:

* Lägga till ett MIME-typsuffix. Många tjänster och webbplatser kräver bildsuffix, t.ex. tillägg `.jpg` till en URL.
* Skapa en mappsökväg till URL:en för sökmotoroptimering.

   Se [hur Adobe Scene7 Publishing System stöder SEO](/help/assets/assets/s7_seo.pdf).

* Lägga till metadata i URL:en för sökmotoroptimering.

   Se [hur Adobe Scene7 Publishing System stöder SEO](/help/assets/assets/s7_seo.pdf).

* Ställa in innehållets disposition för att utlösa en hämtning.
* Förenkla bildhanteringen genom att ange URL:er för personalisering. Omvandla `rgb{XX,YY,ZZ}` till RTF-klart `\redXX\greenYY\blueZZ`

* Begär att vissa tecken ska kodas, t.ex. `$`, `{`och `}`vissa tecken som ska avkodas mot ImageServer. Facebook fungerar till exempel inte så bra med URL:er som innehåller specialtecken.

   Se [Ta bort specialtecken från URL-adresser](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

När det gäller Dynamic Media kan webbplatser som använder ett XML-baserat system för att hantera resursinformation överföra XML-filer till Dynamic Media. Du kan ange en av dessa filer som förbearbetningsregeluppsättningsfil för att hantera Dynamic Media-resurser. Den här filen omstrukturerar standardformatet för URL-protokoll så att det uppfyller affärslogiken i system som integreras med Dynamic Media. Du anger en XML-fil som ska fungera som sökväg till definitionsfilen för regeluppsättningen.

>[!CAUTION]
>
>Var försiktig när du använder linjaler. kan de förhindra att dynamiskt medieinnehåll visas på webbplatsen.

Det finns exempellinjaler som kan hjälpa dig att skapa en egen linjaluppsättning.
Se Referens för [regeluppsättning](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/image_catalog/c_rule_set_reference.html).

Precis som när du skapar alla regeluppsättningar måste du se till att XML-filen är giltig innan du överför den med ett XML-valideringsprogram som xmlvalid.
Se även [Felsökningsregeluppsättningar](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Kontrollera också först att du testar regeluppsättningen i en staging-miljö som inte påverkar produktionsmiljön.
Produktionsmiljöer och staging-miljöer kräver normalt olika inloggningar.

* **Inloggningssida för NA-testmiljön** : [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **Inloggningssida för mellanlagringsmiljön** i EMEA: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **Inloggningssida för JAPAC-mellanlagringsmiljö** : [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/)

Se även [Använda&quot;resurs&quot; i stället för&quot;is&quot;-bild i en regeluppsättning](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

**Så här distribuerar du XML-regeluppsättningar:**

1. Logga in på ditt konto för Dynamic Media Classic:

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Dina autentiseringsuppgifter och din inloggning tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kontaktar du teknisk support.

1. Överför regeluppsättningsfilen genom att göra följande:

   * Klicka på **[!UICONTROL Överför]** i fältet Global navigering.
   * Klicka på **[!UICONTROL Bläddra på sidan]** Överför **[!UICONTROL , i det övre vänstra hörnet]**.
   * I dialogrutan **[!UICONTROL Öppna]** bläddrar du till regeluppsättningsfilen (XML).
   * Markera filen och klicka sedan på **[!UICONTROL Öppna]**.
   * Till höger på sidan **[!UICONTROL Överför]** väljer du en målmapp för regeluppsättningsfilen.
   * Kontrollera att **[!UICONTROL Publicera efter överföring]** är markerat längst ned på sidan.
   * Klicka på **[!UICONTROL Skicka överföring]** längst ned till höger på sidan.
   * Klicka på **[!UICONTROL Jobb]** i fältet Global navigering för att kontrollera överföringsjobbets status. När kolumnen **[!UICONTROL Status]** på sidan **[!UICONTROL Jobb]** säger Överför slutförd fortsätter du till nästa steg.

1. Klicka på **[!UICONTROL Inställningar > Programinställningar > Publiceringsinställningar > Bildserver]** i navigeringsfältet uppe på sidan.
1. Gå till gruppen **[!UICONTROL Kataloghantering]** på **[!UICONTROL Image Server Publish]** -sidan och leta reda på sökvägen **[!UICONTROL till]** regeluppsättningsdefinitionsfilen. Klicka sedan på **[!UICONTROL Välj]**.
1. På sidan **[!UICONTROL Välj XML (Rule Set Definition File)]** bläddrar du till regeluppsättningsfilen och klickar sedan på **[!UICONTROL Välj]** i det nedre högra hörnet på sidan.
1. Klicka på **[!UICONTROL Stäng]** i det nedre högra hörnet på sidan Inställningar.
1. Kör ett Image Server-publiceringsjobb.

   Regeluppsättningsvillkoren tillämpas på begäranden till dynamiska mediabildsservrar.

   Om du gör ändringar i regeluppsättningsfilen tillämpas ändringarna omedelbart när du överför och publicerar den uppdaterade regeluppsättningsfilen igen.

