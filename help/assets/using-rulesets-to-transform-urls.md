---
title: Använd regeluppsättningar för att omforma URL:er
description: Du kan distribuera regeluppsättningar i Dynamic Media för att omvandla URL:er. Regeluppsättningar är instruktioner skrivna i ett skriptspråk (t.ex. JavaScript) som utvärderar XML-data och utför vissa åtgärder om dessa data uppfyller vissa villkor.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin,Developer
exl-id: b0ac587b-8592-4d37-9ce0-98a0859c367f
feature: Configuration,Rulesets
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 0%

---

# Använd regeluppsättningar för att omforma URL:er {#using-rulesets-to-transform-urls}

Du kan distribuera regeluppsättningar i Dynamic Media för att omvandla URL:er. Regeluppsättningar är instruktioner skrivna i ett skriptspråk (t.ex. JavaScript) som utvärderar XML-data och utför vissa åtgärder om dessa data uppfyller vissa villkor. Varje regel består av minst ett villkor och minst en åtgärd. En regel utvärderar XML-data mot villkoren, och om ett villkor är uppfyllt utförs rätt åtgärd. Exempel på regeluppsättningar är följande:

* Lägga till ett MIME-typsuffix. Många tjänster och webbplatser kräver bildsuffix, som att lägga till `.jpg` till en URL.
* Skapa en mappsökväg till URL:en för sökmotoroptimering.

   Se [Hur Adobe Dynamic Media Classic stöder SEO](/help/assets/assets/s7_seo.pdf).

* Lägga till metadata i URL:en för sökmotoroptimering.

   Se [Hur Adobe Dynamic Media Classic stöder SEO](/help/assets/assets/s7_seo.pdf).

* Ställa in innehållets disposition för att utlösa en hämtning.
* Förenkla bildhanteringen genom att ange URL:er för personalisering. Till exempel: `rgb{XX,YY,ZZ}` i RTF-klart `\redXX\greenYY\blueZZ`

* Begär att vissa tecken ska kodas, till exempel `$`, `{`och `}`och vissa tecken som ska avkodas mot ImageServer. Facebook fungerar till exempel inte så bra med URL:er som innehåller specialtecken.

   Se [Ta bort specialtecken från URL-adresser](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

I Dynamic Media-sammanhang kan webbplatser som använder ett XML-baserat system för att hantera resursinformation överföra XML-filer till Dynamic Media. Du kan ange en av dessa filer som förbearbetningsregeluppsättningsfil för Dynamic Media-resurser. Den här filen omstrukturerar URL-protokollets standardformat så att det uppfyller affärslogiken i system som integreras med Dynamic Media. Du anger en XML-fil som ska fungera som sökväg till definitionsfilen för regeluppsättningen.

>[!CAUTION]
>
>Var försiktig när du använder linjaler. kan de förhindra att Dynamic Media-innehåll visas på din webbplats.

Det finns exempellinjaler som kan hjälpa dig att skapa en egen linjaluppsättning.
Se [Referens för regeluppsättning](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Precis som när du skapar alla regeluppsättningar måste du se till att XML-filen är giltig innan du överför den med ett XML-valideringsprogram som xmlvalid.
Se även [Felsöka regeluppsättningar](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Kontrollera också först att du testar regeluppsättningen i en staging-miljö som inte påverkar produktionsmiljön.
Produktionsmiljöer och staging-miljöer kräver normalt olika inloggningar.

Se [Adobe Dynamic Media Classic-datorprogram för inloggningsinformation](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE INFORMATION * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

Se även [Använd&quot;resurs&quot; i stället för&quot;is&quot;-bild i en regeluppsättning](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

**Så här distribuerar du XML-regeluppsättningar:**

1. Logga in på [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

   Dina autentiseringsuppgifter och inloggningsuppgifter tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kan du kontakta Adobe kundsupport.

1. Överför regeluppsättningsfilen genom att göra följande:

   * Välj **[!UICONTROL Upload]**.
   * På **[!UICONTROL Upload]** sida, nära det övre vänstra hörnet, markera **[!UICONTROL Browse]**.
   * I **[!UICONTROL Open]** bläddra till regeluppsättningsfilen (XML).
   * Markera filen och välj **[!UICONTROL Open]**.
   * Till höger på sidan **[!UICONTROL Upload]** väljer du en målmapp för regeluppsättningsfilen.
   * Långt ned på sidan ser du till att **[!UICONTROL Publish After Uploading]** är markerad.
   * Välj **[!UICONTROL Submit Upload]**.
   * Välj **[!UICONTROL Jobs]** för att kontrollera överföringsjobbets status. När **[!UICONTROL Status]** kolumn på **[!UICONTROL Job]** fortsätter sidan till nästa steg.

1. Välj **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.
1. På **[!UICONTROL Image Server Publish]** sida, under **[!UICONTROL Catalog Management]** grupp, leta upp **[!UICONTROL Rule Set Definition File Path]** väljer **[!UICONTROL Select]**.
1. På **[!UICONTROL Select Rule Set Definition File (XML)]** bläddrar du till regeluppsättningsfilen och väljer sedan i det nedre högra hörnet av sidan **[!UICONTROL Select]**.
1. Välj **[!UICONTROL Close]**.
1. Kör ett Image Server-publiceringsjobb.

   Regeluppsättningsvillkoren tillämpas på begäranden till Dynamic Media Image-servrar.

   Om du ändrar regeluppsättningsfilen tillämpas ändringarna omedelbart när du överför och publicerar den uppdaterade regeluppsättningsfilen igen.
