---
title: Vanliga frågor om AEM
seo-title: Vanliga frågor om AEM 6.4
description: Använd de här vanliga frågorna för att förstå, konfigurera och felsöka vanliga arbetsflöden och problem i AEM.
seo-description: Använd de här vanliga frågorna för att förstå, konfigurera och felsöka vanliga arbetsflöden och problem i AEM.
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
translation-type: tm+mt
source-git-commit: bc042696506bf1691c2eeffc6ab941be85fa274c

---


# Vanliga frågor om AEM {#aem-faqs}

Lär känna svaren på vissa problem med AEM-felsökning och konfiguration.

## Webbplatser {#sites}

### Hur konfigurerar jag binär distribution? {#how-do-i-configure-binary-less-distribution}

Binär distribution stöds för distributioner via ett delat datalager och innefattar agenter som utnyttjar exporteraren för det vaultbaserade distributionspaketet (standard-PID: `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`) package builder.

När det binära läget är aktiverat innehåller de distribuerade innehållspaketen referenser till binära filer i stället för till de faktiska binära filerna.

#### Hur aktiverar jag binär distribution? {#how-do-i-enable-binary-less-distribution}

Om du vill aktivera binär distribution distribuerar du med ett delat blobarkiv.
Kontrollera `useBinaryReferences` egenskapen i OSGI-konfigurationen med det fabriks-PID ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)*som din agent använder.

#### Hur kan jag anpassa felmeddelandena när jag navigerar i sidhierarkin i AEM-webbplatskonsolen? {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

Kontrollera nätverkspanelen (i Chrome-webbläsaren) där en personlig konfiguration (JS inte har miniatyrbildats).

Visa kolumnen för att ta reda på vilken som initierade en begäran `Initiator` . Den innehåller filerna och radnumren som AJAX-anropen görs från. Senare kan du spåra felhanteringsfunktionen och ändra felmeddelandet efter dina behov.

#### Hur aktiverar man behörigheter när man skapar en språkkopia för innehållsförfattare i AEM? {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

Innehållsförfattare måste ha behörighet på `/content/projects` plats för att kunna skapa en språkkopieringsfunktion.

Om man också behöver hantera projekt av författare är lösningen att lägga till författaren i `project-administrators` gruppen.

#### Hur ändrar du format när du skapar en språkkopia för ett projekt? {#how-to-change-the-format-while-creating-language-copy-for-a-project}

Skapa en språkrot och en språkkopia i roten innan du skapar ett översättningsprojekt.

Du kan till exempel skapa en språkrot i `/content/geometrixx` med namnet som `fr_LU` (och titeln som franska (Luxemburg)). Skapa sedan en språkkopia av sidan på referenspanelen och navigera till `Create structure only` alternativet i `Create & Translate`. Skapa slutligen ett översättningsprojekt och lägg sedan till språkkopian i översättningsjobbet.

Mer information finns i de andra resurserna nedan:

* [Förbereda innehåll för översättning](/help/sites-administering/tc-prep.md)
* [Hantera översättningsprojekt](/help/sites-administering/tc-manage.md)

#### Hur granskar man AEM-funktioner som inloggningsförsök och ACL eller behörighetsändringar? {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM har introducerat möjligheten att logga administrativa ändringar för bättre felsökning och granskning. Som standard loggas informationen i `error.log` filen. För att underlätta övervakningen rekommenderar vi att de dirigeras om till en separat loggfil.
Mer information om hur du omdirigerar utdata till en separat loggfil finns i [Granska användarhanteringsåtgärder i AEM](/help/sites-administering/audit-user-management-operations.md).

#### Hur aktiverar jag SSL som standard? {#how-to-enable-ssl-by-default}

Adobe Experience Manager (AEM) 6.4 levereras med SSL-guiden och har ett användargränssnitt för att konfigurera Jetty och Granite Jetty SSL-stöd.

Information om hur du aktiverar SSL finns i [SSL som standard](/help/sites-administering/ssl-by-default.md).

#### Vilken är den rekommenderade arkitekturen när man använder AEM:s Content Services från en mobilapp, ideally React Native? {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

Content Services är baserat på Sling Models och AEM-utvecklarna måste tillhandahålla en Sling Model pojo för varje komponent som exporteras.

Mer information om hur du använder AEM-innehållstjänster från ett React-program finns i [Självstudiekursen Kom igång med AEM Content Services](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html) .

Om utvecklarna vill exportera ett träd med komponenter kan de också implementera `ComponentExporter` - och `ContainerExporter` gränssnitten samt använda `ModelFactory` för att iterera över de underordnade komponenterna och returnera sin modellbeteckning. Se resurserna nedan:

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling:Sling Models](https://sling.apache.org/documentation/bundles/models.html)

#### Hur inaktiverar man popup-fönstret för AEM 6.4-undersökningen? {#how-to-disable-aem-survey-pop-up}

Du kan välja att samla in användningsstatistik med hjälp av Touch-gränssnittet eller webbkonsolen. Mer information finns i [Välja in i aggregerad användningsstatistik](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### Finns det någon bra resurs som sätter fokus på de viktigaste funktionerna för uppgradering till AEM 6.4? {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

Se [Förstå orsaker till att uppgradera AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) som beskriver en högnivåuppdelning av nyckelfunktioner för kunder som överväger att uppgradera till den senaste versionen av Adobe Experience Manager.

## Resurser {#assets}

### Varför upprepas arbetsflödet Resurser när MP4-filer överförs (till exempel med metoden dra och släpp)? {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

Om användaren inte har borttagningsbehörighet under objektnoden när de överför filmfilerna misslyckas borttagningssegmentnoderna och överföringen startas om.

#### Hur många digitala resurser kan användas med AEM 6.4 i taget? {#what-is-the-maximum-number-of-digital-assets-that-can-be-operated-with-aem-at-a-time}

Med Adobe Experience Manager (AEM) 6.5 kan du överföra upp till 2 GB resurser i taget.

Mer information om maximalt antal resurser som kan användas med AEM 6.5 finns i [Handbok](/help/assets/assets-sizing-guide.md)för resursstorlek.

#### Vilka är standardinställningarna för OTB-konfigurationer när du skapar en språkkopia? {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

När du skapar språkkopior med hjälp av det klassiska användargränssnittet flyttas resurser inte under den nya språkhierarkin utan används från språkinställningen.

När du skapar en språkkopia med Touch-gränssnittet (**Referenser** -> **Uppdatera språkkopia**) skapas en ny DAM-mapp under det nya språket och resurser refereras därifrån.

Det här är standardinställningen för OTB-konfigurationer. Du kan ställa in **Översätt sidresurser** = **Översätt** inte i översättningskonfigurationer.
För AEM 6.4, **Verktyg** > **Molntjänster** > **Översättningsmolntjänster**.

#### Hur inaktiverar man en AEM-komponent som ger exponentiell tillväxt för AEM SegmentStore (AEM 6.3.1.1)? {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

Du kan inaktivera OSGi Component Disabler. Information om hur du använder den här tjänsten finns i [OSGi Component Disabler](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

Som en tillfällig lösning kan du även inaktivera komponenten manuellt antingen via gränssnittet eller via ett `curl` kommando (exempel nedan) efter varje AEM-omstart.

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### Hur konfigurerar man tillgångsinsikter med AEM 6.5-instansen? {#how-to-configure-asset-insights-with-aem-instance}

Information om hur du konfigurerar och konfigurerar tillgångsinsikter för Experience Manager som distribueras via Adobe Activation (DTM) finns i [Konfigurera tillgångsinsikter med AEM Assets](https://helpx.adobe.com/experience-manager/kt/assets/using/asset-insights-tutorial-setup.html).

#### Hur anpassar man administrationskonsoler? {#how-to-customize-admin-consoles}

AEM innehåller olika mekanismer som gör att du kan anpassa konsolerna och sidredigeringsfunktionerna i din redigeringsinstans. Mer information om hur du skapar en anpassad konsol och anpassar en standardvy för en konsol finns i [Anpassa konsoler](/help/sites-developing/customizing-consoles-touch.md).

#### Vad är skillnaden mellan CoralUI 2- och CoralUI 3-baserade komponenter? {#what-is-the-difference-between-coralui-and-coralui-based-components}

En ny uppsättning Sling-komponenter för Granite UI Foundation har skapats för Coral3 och finns under [/libs/granite/ui/components/coral/Foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) Det finns en uppsättning för CoralUI 2-baserade komponenter och en uppsättning för CoralUI 3-baserade komponenter. Den nya uppsättningen kommer inte bara att vara en kopiera-klistra in av den gamla uppsättningen, utan kommer att rensas (till exempel strömlinjeformning, borttagning av borttagen funktion). Därför rekommenderar vi att en sida endast använder CoralUI 3-baserad eller CoralUI 2-baserad uppsättning.

Mer information finns i [Migreringshandboken till CoralUI 3-baserad](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html).

#### Hur anpassar man sökkomponenten i AEM Assets? {#how-to-customize-the-search-component-in-aem-assets}

Mer information om sökökning/rankning och ytterligare implementeringsinformation finns i [Enkel sökimplementeringshandbok](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html).

Den enkla sökimplementeringen är material från 2017 Summit lab AEM Search Demystified.

#### Vad är skillnaden mellan AEM Assets och AEM MediaLibrary? {#what-is-the-difference-between-aem-assets-and-aem-medialibrary}

AEM Assets är en applikation på AEM Platform som gör det möjligt för våra kunder att hantera sina digitala resurser (bilder, videor, dokument och ljudklipp) i en webbaserad databas medan AEM Media Library är en utsedd del av AEM WCM-innehållsarkivet där bilder och andra delade resurser lagras.

Mer information finns i [AEM Assets vs. AEM MediaLibrary](/help/assets/medialibrary.md) .

#### Går det att bygga plugin-program för WordPress som ger en kund tillgång till Adobe Asset Picker för att välja bilder? {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

Ja, en kund som använder WordPress kan använda Adobe Resursväljaren för att välja bilder från sin AEM Resurser-server för att lägga till i inlägg på sin WordPress-webbplats.

Mer information finns i [Resursväljaren](../assets/search-assets.md#assetselector) .

#### Går det att utöka sökfunktionerna i AEM Resurser för att lägga till fler predikat? {#is-it-possible-to-extend-the-search-facets-in-aem-assets-to-add-additional-predicates}

En företagsövergripande driftsättning av Adobe Experience Manager Assets (AEM) kan lagra många resurser. Du kan lägga till predikat i standardformuläret eller använda ett anpassat formulär som innehåller valfria aspekter.

Mer information finns i [Sök efter ansikten](/help/assets/search-facets.md) .
