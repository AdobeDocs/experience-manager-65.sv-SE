---
title: Konfigurera cacheminne för adaptiva formulär
description: Cacheminnet för anpassningsbara formulär är särskilt utformat för anpassningsbara formulär och dokument. Den cache-lagrar adaptiva formulär och adaptiva dokument i syfte att minska den tid som krävs för att återge ett adaptivt formulär eller dokument på klienten.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: 153986f0-b6ff-4278-8bb6-70c320a4e539
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Foundation Components
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# Konfigurera cacheminne för adaptiva formulär {#configure-adaptive-forms-cache}

Ett cacheminne är en mekanism som förkortar dataåtkomsttider, minskar latensen och förbättrar I/O-hastigheter (input/output). Cacheminnet för adaptiva formulär lagrar endast HTML-innehåll och JSON-struktur i ett adaptivt formulär utan att några förfyllda data sparas. Det minskar tiden som krävs för att återge ett anpassat formulär på klienten. Det är särskilt utformat för anpassningsbara formulär.

## Konfigurera cacheminne för anpassade formulär vid författare och publiceringsinstanser {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Gå till konfigurationshanteraren AEM webbkonsolen på `https://[server]:[port]/system/console/configMgr`.
1. Klicka **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** om du vill redigera dess konfigurationsvärden.
1. I [!UICONTROL edit configuration values] kan du ange maximalt antal formulär, eller dokument, en instans av AEM [!DNL Forms] servern kan cachelagra i **[!UICONTROL Number of Adaptive Forms]** fält. Standardvärdet är 100.

   >[!NOTE]
   >
   >Om du vill inaktivera cachen anger du värdet i fältet Antal adaptiva Forms till **0**. Cacheminnet återställs och alla formulär och dokument tas bort från cacheminnet när du inaktiverar eller ändrar cachekonfigurationen.

   ![Konfigurationsdialogruta för HTML cache för adaptiva formulär](assets/cache-configuration-edit.png)

1. Klicka **[!UICONTROL Save]** för att spara konfigurationen.

Miljön är konfigurerad att använda cacheadaptiva formulär och relaterade resurser.


## (Valfritt) Konfigurera cacheminne för anpassningsbara formulär vid Dispatcher {#configure-the-cache}

Du kan även konfigurera adaptiv formulärcache-lagring på Dispatcher för att få ytterligare prestandaförbättringar.

### Krav {#pre-requisites}

* Aktivera [sammanfoga eller förifylla data hos klienten](prepopulate-adaptive-form-fields.md#prefill-at-client) alternativ. Det hjälper till att sammanfoga unika data för varje instans av ett förfyllt formulär.

### Att tänka på vid cachelagring av adaptiva formulär på en Dispatcher {#considerations}

* När du använder cacheminnet för anpassade formulär ska du använda AEM [!DNL Dispatcher] för att cachelagra klientbibliotek (CSS och JavaScript) för ett adaptivt formulär.
* När du utvecklar anpassade komponenter på servern som används för utveckling ska du inaktivera cachen för anpassade formulär.
* URL:er utan tillägg cachelagras inte. Exempel: URL med mönster `/content/forms/[folder-structure]/[form-name].html` cachelagras och URL:er med mönster ignoreras vid cachelagring `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Använd URL:er med tillägg för att utnyttja fördelarna med cachning.
* Att tänka på när det gäller lokaliserade adaptiva formulär:
   * Använd URL-format `http://host:port/content/forms/af/<afName>.<locale>.html` begära en lokaliserad version av ett adaptivt formulär istället för `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [Inaktivera med webbläsarens språkområde](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) för URL:er med format `http://host:port/content/forms/af/<adaptivefName>.html`.
   * När du använder URL-format `http://host:port/content/forms/af/<adaptivefName>.html`och **[!UICONTROL Use Browser Locale]** i konfigurationshanteraren är inaktiverad, hanteras den icke-lokaliserade versionen av det adaptiva formuläret. Det icke-lokaliserade språket är det språk som används vid utvecklingen av det adaptiva formuläret. Det språk som är konfigurerat för webbläsaren (webbläsarens språkområde) beaktas inte och en icke-lokaliserad version av det anpassade formuläret används.
   * När du använder URL-format `http://host:port/content/forms/af/<adaptivefName>.html`och **[!UICONTROL Use Browser Locale]** när konfigurationshanteraren är aktiverad, tillhandahålls en lokaliserad version av det adaptiva formuläret, om en sådan finns. Språket i det lokaliserade adaptiva formuläret baseras på det språk som är konfigurerat för webbläsaren (webbläsarens språkområde). Det kan leda till [cachelagra endast den första instansen av ett adaptivt formulär]. Om du vill förhindra att ett problem inträffar på din instans kan du läsa [felsökning](#only-first-insatnce-of-adptive-forms-is-cached).

### Aktivera cachelagring vid Dispatcher

Så här aktiverar och konfigurerar du cachelagring av adaptiva formulär på Dispatcher:

1. Öppna följande URL för varje publiceringsinstans i miljön och [aktivera rensningsagent för publicering av instanser av din miljö](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance):
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Lägg till följande i din dispatcher.alla filer](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files):

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

   * Ett anpassat formulär finns kvar i cacheminnet tills en uppdaterad version av formuläret inte publiceras.

   * När en nyare version av en resurs som refereras till i ett adaptivt formulär publiceras blir de adaptiva formulären automatiskt ogiltiga. Det finns några undantag för automatisk ogiltigförklaring av refererade resurser. Information om hur du använder undantag finns i [felsökning](#troubleshooting) -avsnitt.
1. [Lägg till nedanstående regeldispatcher.vilken eller vilken anpassad regelfil som helst](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache). URL:er som inte stöder cachelagring utesluts. Interaktiv kommunikation.

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Do not cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Do not cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Do not cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [Lägg till följande parametrar i listan över ignorerade URL-parametrar](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

Din AEM är konfigurerad att cachelagra adaptiva formulär. Den cache-lagrar alla typer av anpassningsbara formulär. Om du behöver kontrollera användaråtkomstbehörigheterna för en sida innan du levererar den cachelagrade sidan, se [cachelagra skyddat innehåll](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html).

## Felsökning {#troubleshooting}

### Vissa anpassningsbara formulär som innehåller bilder eller videor ogiltigförklaras inte automatiskt från Dispatcher-cachen {#videos-or-images-not-auto-invalidated}

#### Problem {#issue1}

När du markerar och lägger till bilder eller videoklipp via en filläsare i ett anpassat formulär och dessa bilder och videoklipp redigeras i Resursredigeraren blir adaptiva formulär som innehåller sådana bilder inte automatiskt ogiltiga från Dispatcher-cachen.

#### Lösning {#Solution1}

När du har publicerat bilder och video avpublicerar och publicerar du de adaptiva formulären som refererar till dessa resurser.

### Endast den första instansen av ett adaptivt formulär cachelagras {#only-first-instance-of-adaptive-forms-is-cached}

#### Problem {#issue3}

När den anpassningsbara formulärets URL inte har någon lokaliseringsinformation, och **[!UICONTROL Use Browser Locale]** när konfigurationshanteraren är aktiverad, används en lokaliserad version av det adaptiva formuläret. Endast den första instansen av det adaptiva formuläret cachelagras och skickas till alla efterföljande användare.

#### Lösning {#Solution3}

Lös problemet genom att utföra följande steg:

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
