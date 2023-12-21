---
title: Hur aktiverar man adaptiva Forms Core-komponenter i AEM 6.5 Forms?
description: Steg för steg-guide som hjälper dig att aktivera adaptiva Forms Core-komponenter i en AEM 6.5 Forms-miljö.
keywords: Aktivera kärnkomponenter, kärnkomponenter adaptiva Forms, kärnkomponenter i 6.5, adaptiva Forms Core-komponenter i AEM 6.5, AF Core-komponenter i AEM 6.5, AEM 6.5 Forms Core-komponenter
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms, Core Components
exl-id: 6585ea71-6242-47d3-bc59-6f603cf507b6
source-git-commit: 4ecdcb2659b26043f95ba1dc3e907c33f65b8834
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 0%

---

# Aktivera adaptiva Forms Core-komponenter i AEM 6.5 Forms {#enable-adaptive-forms-core-components}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html) |
| AEM 6.5 | Denna artikel |

**Gäller för:** ✅ adaptiva Form Core-komponenter ❎ adaptiva Form Foundation-komponenter.

Genom att aktivera adaptiva Forms Core-komponenter kan du börja skapa, publicera och leverera [Core Components based Adaptive Forms](create-an-adaptive-form-core-components.md) och [Headless Adaptive Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) från din AEM 6.5 Forms-miljö.

Om du vill aktivera adaptiva Forms Core-komponenter i din Forms-miljö med AEM 6.5 installerar och driftsätter du en [AEM Archetype 41 eller senare](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) baserat projekt (med formuläralternativ aktiverade) på alla dina författarinstanser och publiceringsinstanser.

I den här artikeln finns detaljerade anvisningar om hur du konfigurerar och distribuerar AEM Archetype 41 eller senare baserat på ditt projekt i Forms-miljön AEM 6.5 för att aktivera adaptiva Forms Core-komponenter. Du kan läsa listan nedan för **AEM 6.5** kompatibla versioner för aktivering av Forms Core Components:

## Förutsättningar {#prerequisites}

Innan du aktiverar adaptiva Forms Core-komponenter i en AEM 6.5 Forms-miljö:

* [Uppgradera till AEM 6.5 Forms Service Pack 16 (6.5.16.0) eller senare](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html).

* Installera den senaste versionen av [Apache Maven](https://maven.apache.org/download.cgi).

* Installera en vanlig textredigerare. Exempel: Microsoft Visual Studio Code.

## Skapa och distribuera det senaste AEM Archetype-baserade projektet

Så här skapar du en AEM Archetype 41 eller [senare](https://github.com/adobe/aem-project-archetype) -baserat projekt och distribuera det till alla dina författare- och publiceringsinstanser:

1. Logga in på datorn som värd och kör AEM 6.5 Forms-instansen som administratör.
1. Öppna kommandotolken eller avsluta och kör följande kommando för att skapa AEM Archetype-projekt (med formuläralternativ aktiverade):

   * Microsoft Windows

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate ^
      -D archetypeGroupId=com.adobe.aem ^
      -D archetypeArtifactId=aem-project-archetype ^
      -D archetypeVersion=41 ^
      -D appTitle="My Form" ^
      -D appId="myform" ^
      -D groupId="com.myform" ^
      -D includeFormsenrollment="y" ^
      -D aemVersion="6.5.15" 
   ```

   * Linux eller Apple macOS

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
      -D archetypeGroupId=com.adobe.aem \
      -D archetypeArtifactId=aem-project-archetype \
      -D archetypeVersion=41 \
      -D appTitle="My Form" \
      -D appId="myform" \
      -D groupId="com.myform" \
      -D includeFormsenrollment="y" \
      -D aemVersion="6.5.15" 
   ```

   Tänk på följande när du kör kommandot ovan:

   * Ändra inte värdet för `aemVersion` egenskap från `6.5.15.0` till något annat.

   * Ange `archetypeVersion` egenskap till `41` eller senare. Den senaste versionen finns i avsnittet om systemkrav i [AEM Project Archettype](https://github.com/adobe/aem-project-archetype) dokumentation.

   * Uppdatera kommandot så att det återspeglar de specifika värdena för miljön, inklusive `appTitle`, `appId`och `groupId`. Ange även värdet för  `includeFormsenrollment` egenskap till `y`. Om du använder Forms Portal anger du `includeExamples=y` om du vill inkludera Forms Portal Core Components i ditt projekt.


1. (Endast för Arketype version 41-baserade projekt) När AEM Archetype-projektet har skapats kan du aktivera teman för Core Components-baserade Adaptive Forms. Så här aktiverar du teman:

   1. Öppna [AEM Archetype-projektmapp]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html för redigering:

   1. Lägg till följande kod på rad 21:

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![Lägg till ovanstående kod på rad 21](/help/forms/using/assets/code-to-enable-themes.png)

   1. Spara och stäng filen.

1. Uppdatera projektet så att det innehåller den senaste versionen av Forms Core Components:

   1. Öppna [AEM Archetype-projektmapp]/pom.xml för redigering.
   1. Ange version av `core.forms.components.version` och `core.forms.components.af.version` till [senaste Forms Core Components](https://github.com/adobe/aem-core-forms-components/tree/release/650#system-requirements) och se till att båda har samma version som **Forms Core Components** som anges i tabellen och ange version av `core.wcm.components.version` som anges i **WCM-kärnkomponenter**.

      >[!WARNING]
      >
      >* När du skapar ett Arketype-projekt med `version 45`, [AEM Archetype-projektmapp]/pom.xml ställer först in versionen av formulärets kärnkomponenter till `1.1.28`. Innan du bygger eller driftsätter Archetype-projektet ska du uppdatera komponentversionen för formulär till `1.1.26`.


      >[!NOTE]
      >
      >* Om du konfigurerar någon annan topologi måste du lägga till överförings-, förifyllnings- och andra URL-adresser till tillåtelselista i Dispatcher-lagret.

   1. Spara och stäng filen.


1. När det AEM Archetype-projektet har skapats ska du skapa distributionspaketet för din miljö. Så här skapar du paketet:

   1. Navigera till rotkatalogen för ditt AEM Archetype-projekt.

   1. Kör följande kommando för att skapa AEM Archetype-projekt för din miljö:

      ```Shell
      mvn clean install
      ```

      ![arkietypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   När det AEM Archetype-projektet har skapats skapas ett AEM. Paketet finns på [AEM Archetype-projektmapp]\all\target\[appid].all-[version].zip

1. Använd [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en) för att distribuera [AEM Archetype-projektmapp]\all\target\[appid].all-[version]ZIP-paket för alla författare- och publiceringsinstanser.

>[!NOTE]
>
>
>
> * Om du får problem med att komma åt inloggningsdialogrutan på en publiceringsinstans kan du försöka med att använda URL-adressen för att installera paketet via pakethanteraren: `http://[Publish Server URL]:[PORT]/system/console` för inloggning. På så sätt kan du komma åt inloggningssidan i en Publish-instans och fortsätta med installationsprocessen.
> * Ta inte bort eller ignorera Arketype-projektet efter att du distribuerat det till din miljö. Arketype-projektet krävs för att du ska kunna lägga till anpassade och nya adaptiva Forms Core Components-teman i din miljö.

Kärnkomponenterna är aktiverade för din miljö. En tom Core Components-baserad Adaptive Form-mall och Canvas 3.0-temat distribueras till din miljö, vilket gör att du kan [skapa baskomponentbaserade adaptiva Forms](create-an-adaptive-form-core-components.md).

## Vanliga frågor

### Vad är kärnkomponenter?

The [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) är en uppsättning standardiserade WCM-komponenter (Web Content Management) för AEM som snabbar upp utvecklingstiden och minskar underhållskostnaderna för dina webbplatser.

### Vad finns det för funktioner för att aktivera kärnkomponenter?


När de adaptiva Forms Core-komponenterna är aktiverade för din miljö läggs en tom Core Components-baserad Adaptive Form-mall och Canvas 3.0-tema till i din miljö. När du har aktiverat adaptiva Forms Core-komponenter för din miljö kan du:

* Skapa grundkomponentbaserade adaptiva Forms.
* Skapa grundkomponentbaserade adaptiva formulärmallar.
* Skapa egna teman för grundkomponentbaserade adaptiva formulärmallar.
* Servera Core Component-baserade Adaptive Form JSON-representationer för kanaler som mobiler, webben, inbyggda appar och tjänster som kräver att ett formulär visas utan rubrik.

## What&#39;s Next

* [Skapa en grundkomponentbaserad adaptiv form](/help/forms/using/create-an-adaptive-form-core-components.md)
* [Skapa eller lägga till ett anpassat formulär på en AEM Sites-sida eller ett Experience Fragment](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Skapa teman för grundkomponentbaserade adaptiva Forms](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [Skapa en mall för Core Components-baserade Adaptive Forms](template-editor.md)
