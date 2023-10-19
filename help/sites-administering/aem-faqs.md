---
title: AEM frågor och svar
description: Använd de här vanliga frågorna för att förstå, konfigurera och felsöka vanliga arbetsflöden och problem i AEM.
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
source-git-commit: f7bfbfab9fb9ec00304f2889735c70be924cc217
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 0%

---

# AEM frågor och svar {#aem-faqs}

Lär känna svaren på några AEM problem med felsökning och konfiguration.

## Sites {#sites}

### Hur konfigurerar jag binär distribution? {#how-do-i-configure-binary-less-distribution}

Binär distribution stöds för distributioner via ett delat datalager och innefattar agenter som utnyttjar exporteraren för det vaultbaserade distributionspaketet (standard-PID: `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`) package builder.

När det binära läget är aktiverat innehåller de distribuerade innehållspaketen referenser till binära filer i stället för till de faktiska binära filerna.

#### Hur aktiverar jag binär distribution? {#how-do-i-enable-binary-less-distribution}

Om du vill aktivera binär distribution distribuerar du med ett delat blobarkiv.
Kontrollera `useBinaryReferences` i OSGI-konfigurationen med fabriks-PID ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)* som din agent använder.

#### Hur kan jag anpassa felmeddelandena när jag navigerar i sidhierarkin AEM webbplatskonsolen? {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

Kontrollera nätverkspanelen (i Chrome-webbläsaren) där en personlig konfiguration (JS inte har miniatyrbildats).

Visa `Initiator` för att avgöra vilken initierare som en begäran initierades i. Den innehåller filerna och radnumren som AJAX anropar från. Senare kan du spåra felhanteringsfunktionen och ändra felmeddelandet efter dina behov.

#### Hur aktiverar jag behörigheter när du skapar en språkkopia för innehållsförfattare i AEM? {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

Innehållsförfattare måste ha behörighet att skapa funktionen för språkkopiering på `/content/projects` plats.

Om du även behöver hantera projekt av författare kan du lösa problemet genom att lägga till författaren i `projects-administrators` grupp.

#### Hur ändrar du format när du skapar en språkkopia för ett projekt? {#how-to-change-the-format-while-creating-language-copy-for-a-project}

Skapa en språkrot och en språkkopia i roten innan du skapar ett översättningsprojekt.

Skapa till exempel en språkrot på `/content/geometrixx` med namn som `fr_LU` (och titeln franska (Luxemburg)). Skapa sedan en språkkopia av sidan från referenspanelen och navigera till `Create structure only` alternativ i `Create & Translate`. Skapa slutligen ett översättningsprojekt och lägg sedan till språkkopian i översättningsjobbet.

Mer information finns i de andra resurserna nedan:

* [Förbereda innehåll för översättning](/help/sites-administering/tc-prep.md)
* [Hantera översättningsprojekt](/help/sites-administering/tc-manage.md)

#### Hur granskar AEM som inloggningsförsök och ACL eller behörighetsändringar? {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM har introducerat möjligheten att logga administrativa ändringar för bättre felsökning och granskning. Som standard är informationen loggad i `error.log` -fil. För att underlätta övervakningen rekommenderar vi att de dirigeras om till en separat loggfil.
Information om hur du omdirigerar utdata till en separat loggfil finns i [Hur man granskar användarhanteringsåtgärder i AEM](/help/sites-administering/audit-user-management-operations.md).

#### Hur aktiverar jag SSL som standard? {#how-to-enable-ssl-by-default}

Adobe Experience Manager (AEM) 6.4 levereras med SSL-guiden och har ett användargränssnitt för att konfigurera Jetty och Granite Jetty SSL-stöd.

Information om hur du aktiverar SSL som standard finns i [SSL som standard](/help/sites-administering/ssl-by-default.md).

#### Vilken är den rekommenderade arkitekturen när AEM Content Services från en mobilapp, ideally React Native, används? {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

Content Services baseras på Sling Models och AEM utvecklare måste tillhandahålla en Sling Model pojo för varje komponent som exporteras.

Mer information om hur du använder AEM innehållstjänster från ett React-program finns i [Kom igång med AEM Content Services](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html) självstudie.

Om utvecklarna vill exportera ett träd med komponenter kan de också implementera `ComponentExporter` och `ContainerExporter` och använder `ModelFactory` för att iterera över de underordnade komponenterna och returnera deras modellbeteckning. Se resurserna nedan:

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling: Sling Models](https://sling.apache.org/documentation/bundles/models.html)

#### Hur stänger jag av AEM 6.4-enkätsvar? {#how-to-disable-aem-survey-pop-up}

Du kan välja att samla in användningsstatistik med hjälp av Touch-gränssnittet eller webbkonsolen. Detaljerade anvisningar finns i [Insamling av sammanställd användningsstatistik](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### Finns det någon bra resurs som sätter fokus på de viktigaste funktionerna för uppgradering till AEM 6.4? {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

Se [Förstå skäl att uppgradera AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) som beskriver en högnivåuppdelning av de viktigaste funktionerna för kunder som funderar på att uppgradera till den senaste versionen av Adobe Experience Manager.

## Assets {#assets}

### Varför upprepas arbetsflödet Resurser när MP4-filer överförs (till exempel med metoden dra och släpp)? {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

Om användaren inte har borttagningsbehörighet under objektnoden när de överför filmfilerna misslyckas borttagningssegmentnoderna och överföringen startas om.

#### Vilka är standardinställningarna för OTB-konfigurationer när du skapar en språkkopia? {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

När du skapar en språkkopia via Touch-gränssnittet (**Referenser** -> **Uppdatera språkkopia**) skapas en ny DAM-mapp under det nya språket och resurserna refereras därifrån.

Det här är standardinställningen för OTB-konfigurationer. Du kan ange **Översätt sidresurser** = **Översätt inte** i översättningskonfigurationer.
AEM 6.4 **verktyg** > **Cloud Service** > **Översättningsmolntjänster**.

#### Hur inaktiverar man en AEM som orsakar exponentiell tillväxt för AEM SegmentStore (AEM 6.3.1.1)? {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

Du kan inaktivera OSGi Component Disabler. Information om hur du använder den här tjänsten finns i [OSGi Component Disabler](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

Som en tillfällig lösning kan du även inaktivera komponenten manuellt antingen via användargränssnittet eller via en `curl` efter varje AEM omstart (exempel nedan).

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### Hur anpassar man administrationskonsoler? {#how-to-customize-admin-consoles}

AEM innehåller olika mekanismer som gör att du kan anpassa konsolerna och sidredigeringsfunktionerna i din redigeringsinstans. Mer information om hur du skapar en anpassad konsol och anpassar en standardvy för en konsol finns i [Anpassa konsolerna](/help/sites-developing/customizing-consoles-touch.md).

#### Vad är skillnaden mellan CoralUI 2- och CoralUI 3-baserade komponenter? {#what-is-the-difference-between-coralui-and-coralui-based-components}

En ny uppsättning Sling-komponenter för Granite UI Foundation har skapats för Coral3 och finns under [/libs/granite/ui/components/coral/Foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) Det finns en uppsättning för CoralUI 2-baserade komponenter och en uppsättning för CoralUI 3-baserade komponenter. Den nya uppsättningen kommer inte bara att vara en kopiera-klistra in av den gamla uppsättningen, utan kommer att rensas (till exempel strömlinjeformning, borttagning av borttagen funktion). Därför rekommenderar vi att en sida bara använder CoralUI 3-baserad eller CoralUI 2-baserad uppsättning.

Mer information finns i [Migreringshandbok till CoralUI 3-baserad](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html).

#### Hur anpassar man sökkomponenten i AEM Assets? {#how-to-customize-the-search-component-in-aem-assets}

Mer information om sökökning/rankning och ytterligare implementeringsinformation finns i [Implementeringshandbok för enkel sökning](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html).

Den enkla sökimplementeringen är material från 2017 Summit lab AEM Search Demystified.

#### Går det att bygga plugin-program för WordPress som ger en kund möjlighet att välja bilder i Adobe Resursväljaren? {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

Ja, en kund som använder WordPress kan använda Adobe Resursväljare för att välja bilder från sin AEM Assets-server och lägga till i inlägg på sin WordPress-webbplats.

Se [Resursväljare](../assets/search-assets.md#assetpicker) för mer information.
