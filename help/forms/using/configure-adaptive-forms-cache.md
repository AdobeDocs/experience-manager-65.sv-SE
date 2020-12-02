---
title: Konfigurera cacheminne för adaptiva formulär
seo-title: Konfigurera cacheminne för adaptiva formulär
description: 'Cacheminnet för anpassningsbara formulär är särskilt utformat för anpassningsbara formulär och dokument. Den cache-lagrar adaptiva formulär och adaptiva dokument i syfte att minska den tid som krävs för att återge ett adaptivt formulär eller dokument på klienten. '
seo-description: 'Cacheminnet för anpassningsbara formulär är särskilt utformat för anpassningsbara formulär och dokument. Den cache-lagrar adaptiva formulär och adaptiva dokument i syfte att minska den tid som krävs för att återge ett adaptivt formulär eller dokument på klienten. '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
translation-type: tm+mt
source-git-commit: ade3747ba608164a792a62097b82c55626245891
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%

---


# Konfigurera cache för adaptiva formulär {#configure-adaptive-forms-cache}

Ett cacheminne är en mekanism som förkortar dataåtkomsttider, minskar latensen och förbättrar I/O-hastigheter (input/output). Cacheminnet för adaptiva formulär lagrar endast HTML-innehåll och JSON-strukturen i ett adaptivt formulär utan att några förfyllda data sparas. Det minskar tiden som krävs för att återge ett anpassat formulär på klienten. Det är särskilt utformat för anpassningsbara formulär.

## Konfigurera cacheminne för anpassade formulär vid författare och publiceringsinstanser {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Gå till konfigurationshanteraren AEM webbkonsolen på `https://[server]:[port]/system/console/configMgr`.
1. Klicka på **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** om du vill redigera dess konfigurationsvärden.
1. I dialogrutan [!UICONTROL edit configuration values] anger du det maximala antalet formulär eller dokument som en instans av AEM [!DNL Forms]-servern kan cachelagra i fältet **[!UICONTROL Number of Adaptive Forms]**. Standardvärdet är 100.

   >[!NOTE]
   >
   >Om du vill inaktivera cachen anger du värdet **0** i fältet Antal adaptiva Forms. Cacheminnet återställs och alla formulär och dokument tas bort från cacheminnet när du inaktiverar eller ändrar cachekonfigurationen.

   ![Konfigurationsdialogruta för HTML-cache för adaptiva formulär](assets/cache-configuration-edit.png)

1. Klicka på **[!UICONTROL Save]** för att spara konfigurationen.

Miljön är konfigurerad att använda cacheadaptiva formulär och relaterade resurser.


## (Valfritt) Konfigurera cacheminne för anpassat formulär vid dispatcher {#configure-the-cache}

Du kan också konfigurera adaptiv formulärcache-lagring vid dispatcher för ytterligare prestandaförbättringar.

### Krav {#pre-requisites}

* Aktivera alternativet [sammanfogning eller förifyllning av data på klienten](prepopulate-adaptive-form-fields.md#prefill-at-client). Det hjälper till att sammanfoga unika data för varje instans av ett förfyllt formulär.
* [Aktivera tömningsagenten för varje publiceringsinstans](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance). Det ger bättre cachningsprestanda för adaptiva formulär. Standardwebbadressen för rensningsagenter är `http://[server]:[port]]/etc/replication/agents.publish/flush.html`.

### Att tänka på vid cachelagring av adaptiva formulär på en dispatcher {#considerations}

* När du använder cacheminnet för adaptiva formulär använder du AEM [!DNL Dispatcher] för att cachelagra klientbibliotek (CSS och JavaScript) för ett adaptivt formulär.
* När du utvecklar anpassade komponenter på servern som används för utveckling ska du inaktivera cachen för anpassade formulär.
* URL:er utan tillägg cachelagras inte. URL:er med mönstret `/content/forms/[folder-structure]/[form-name].html` cachelagras till exempel, och cachelagring ignorerar URL:er med mönstret `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Använd URL:er med tillägg för att utnyttja fördelarna med cachning.
* Att tänka på när det gäller lokaliserade adaptiva formulär:
   * Använd URL-formatet `http://host:port/content/forms/af/<afName>.<locale>.html` för att begära en lokaliserad version av ett adaptivt formulär i stället för `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [Inaktivera användning av webbläsarens ](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) språkområde för URL:er med format  `http://host:port/content/forms/af/<adaptivefName>.html`.
   * När du använder URL-formatet `http://host:port/content/forms/af/<adaptivefName>.html`, och **[!UICONTROL Use Browser Locale]** i konfigurationshanteraren är inaktiverat, används den icke-lokaliserade versionen av det adaptiva formuläret. Det icke-lokaliserade språket är det språk som används vid utvecklingen av det adaptiva formuläret. Språkinställningen som är konfigurerad för webbläsaren (webbläsarens språkområde) beaktas inte och en icke-lokaliserad version av det anpassade formuläret används.
   * När du använder URL-formatet `http://host:port/content/forms/af/<adaptivefName>.html`, och **[!UICONTROL Use Browser Locale]** i konfigurationshanteraren är aktiverat, visas en lokaliserad version av det adaptiva formuläret, om en sådan finns. Språket i det lokaliserade adaptiva formuläret baseras på det språk som är konfigurerat för webbläsaren (webbläsarens språkområde). Det kan leda till [cachelagring av endast den första instansen av ett adaptivt formulär]. Information om hur du förhindrar att problemet uppstår på din instans finns i [felsökning](#only-first-insatnce-of-adptive-forms-is-cached).

### Aktivera cachelagring vid dispatcher

Utför stegen nedan för att aktivera och konfigurera cachelagring av adaptiva formulär vid dispatcher:

1. Öppna följande URL för varje publiceringsinstans i miljön och konfigurera replikeringsagenten:
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Lägg till följande i din dispatcher.any-fil](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files):

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   När du lägger till ovanstående:

   * Ett anpassat formulär finns kvar i cachen tills en uppdaterad version av formuläret inte publiceras.

   * När en nyare version av en resurs som refereras i ett adaptivt formulär publiceras blir de adaptiva formulären automatiskt ogiltiga. Det finns några undantag för automatisk ogiltigförklaring av refererade resurser. Du hittar mer information om undantag i avsnittet [felsökning](#troubleshooting).
1. [Lägg till regeldispatchern nedan.vilken eller vilken anpassad regelfil](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache) som helst. URL:er som inte stöder cachelagring utesluts. Exempel: Interaktiv kommunikation.

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [Lägg till följande parametrar i listan](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters) med ignorerade URL-parametrar:

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

Din AEM är konfigurerad att cachelagra adaptiva formulär. Den cache-lagrar alla typer av anpassningsbara formulär. Om du måste kontrollera användaråtkomstbehörighet för en sida innan du kan leverera den cachelagrade sidan läser du [cachelagra skyddat innehåll](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/permissions-cache.html).

## Felsökning {#troubleshooting}

### Vissa adaptiva formulär som innehåller bilder eller videoklipp ogiltigförklaras inte automatiskt från dispatcherns cache {#videos-or-images-not-auto-invalidated}

#### Utgåva {#issue1}

När du markerar och lägger till bilder eller videoklipp via en filläsare i ett anpassat formulär och dessa bilder och videoklipp redigeras i Assets Editor blir adaptiva formulär som innehåller sådana bilder inte automatiskt ogiltiga från dispatchercachen.

#### Lösning {#Solution1}

När du har publicerat bilder och video avpublicerar och publicerar du de adaptiva formulären som refererar till dessa resurser.

### Vissa adaptiva formulär som innehåller innehållsfragment eller upplevelsefragment ogiltigförklaras inte automatiskt från dispatchercachen {#content-or-experience-fragment-not-auto-invalidated}

#### Utgåva {#issue2}

När du lägger till ett innehålls- eller upplevelsefragment i ett anpassat formulär och dessa resurser redigeras och publiceras oberoende av varandra, blir adaptiva formulär som innehåller sådana resurser inte automatiskt ogiltiga från dispatchercachen.

#### Lösning {#Solution2}

När du har publicerat uppdaterat innehållsfragment eller upplevelsefragment kan du uttryckligen avpublicera och publicera de adaptiva formulär som använder dessa resurser.

### Endast den första instansen av ett adaptivt formulär cachelagras{#only-first-insatnce-of-adptive-forms-is-cached}

#### Utgåva {#issue3}

När URL:en för det adaptiva formuläret inte har någon lokaliseringsinformation och **[!UICONTROL Use Browser Locale]** i konfigurationshanteraren är aktiverad, hanteras en lokaliserad version av det adaptiva formuläret och endast den första instansen av det adaptiva formuläret cachelagras och levereras till varje efterföljande användare.

#### Lösning {#Solution3}

Utför följande steg för att lösa problemet:

1. Öppna conf.d/httpd-dispatcher.conf eller någon annan konfigurationsfil som är konfigurerad att läsas in under körning.

1. Lägg till följande kod i filen och spara den. Det är en exempelkod som ändrar den så att den passar din miljö.

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two character which most likely will be the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
