---
title: Utvecklingsverktyg
seo-title: Utvecklingsverktyg
description: För att utveckla dina JCR-, Apache Sling- eller AEM-program finns ett antal verktygsuppsättningar
seo-description: För att utveckla dina JCR-, Apache Sling- eller AEM-program finns ett antal verktygsuppsättningar
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# Utvecklingsverktyg{#development-tools}

Följande verktygsuppsättningar är tillgängliga för att utveckla dina JCR-, Apache Sling- eller AEM-program:

* en uppsättning bestående av [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) och WebDAV. CRXDE Lite är inbäddat i CRX/AEM och gör att du kan utföra standardutvecklingsuppgifter i webbläsaren. Med CRXDE Lite kan du skapa och redigera filer (som .jsp och .java), mappar, mallar, komponenter, dialogrutor, noder, egenskaper och paket när du loggar och integrerar med SVN.

   CRXDE Lite rekommenderas när du inte har direktåtkomst till CRX-/AEM-servern, när du utvecklar ett program genom att utöka eller ändra de körklara komponenterna och Java-paketen eller när du inte behöver en dedikerad felsökare, kodkomplettering och syntaxmarkering.

* en uppsättning bestående av en integrerad utvecklingsmiljö (t.ex. [Eclipse](/help/sites-developing/howto-projects-eclipse.md) eller [IntelliJ](/help/sites-developing/ht-intellij.md)), ett byggverktyg (till exempel: [Apache Maven](/help/sites-developing/ht-projects-maven.md)), FileVault som har utvecklats av Adobe för att mappa en databas till ett filsystem, ett versionskontrollsystem (till exempel: Subversion), ett felsökningssystem (till exempel: Jira), ett centralt beroendehanteringssystem (till exempel: Apache Archiva) och ett system för automatisering av byggen (till exempel: Apache Continuum).

   Med den här konfigurationen kan du helt integrera ditt program (innehåll, kod, konfiguration) i alla utvecklingsmiljöer och processer. Länken mellan de olika elementen är filsystemrepresentationen av databasen via FileVault, eftersom alla tidigare nämnda utvecklingsverktyg kan fungera med filer.

## Tillägg för integrerade utvecklingsmiljöer {#extensions-for-integrated-development-environments}

Adobe har släppt följande tillägg:

* [AEM Eclipse-tillägg](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets Extension](/help/sites-developing/aem-brackets.md)
* [AEM IntelliJ-tillägg](https://github.com/headwirecom/aem-ide-tooling-4-intellij/blob/master/documenation/AEM%20Tooling%20Plugin%20for%20IntelliJ%20IDEA.pdf) (från huvudtråden)

### Andra verktyg {#other-tools}

AEM levereras med andra verktyg som underlättar utvecklingen:

* [Dialogruteredigeraren](/help/sites-developing/dialog-editor.md)
* [Använda översättare för att hantera ordlistor](/help/sites-developing/i18n-translator.md)
* [Hantera paket med Maven](/help/sites-developing/vlt-mavenplugin.md)
* [Utveckla AEM-projekt med Eclipse](/help/sites-developing/howto-projects-eclipse.md)
* [Så här skapar du AEM-projekt med Apache Maven](/help/sites-developing/ht-projects-maven.md)
* [Utveckla AEM-projekt med IntelliJ IDEA](/help/sites-developing/ht-intellij.md)
* [Så här använder du VLT-verktyget](/help/sites-developing/ht-vlttool.md)
* [Så här använder du proxyserververktyget](/help/sites-developing/ht-proxy-server.md)
* [Verktyget Dialogkonvertering](/help/sites-developing/dialog-conversion.md)
* [AEM Repo Tool](/help/sites-developing/aem-repo-tool.md)

Verktyg som underlättar skapandet av nya projekt:

* [AEM Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [AEM Lazybone-mallar](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>Följande självstudiekurser kan vara intressanta när du startar ett nytt AEM-projekt:
>[Komma igång med AEM Sites del 1 - Projektinställningar](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)

