---
title: AEM Developer Tools for Eclipse
seo-title: AEM Developer Tools for Eclipse
description: AEM Developer Tools for Eclipse
seo-description: null
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
exl-id: 00473769-c447-4966-a71e-117c669e0151
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 1%

---

# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## Översikt {#overview}

&quot;AEM Developer Tools&quot; är en Eclipse-plugin som bygger på [Eclipse-plugin för Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) som släpps under Apache License 2.

Den har flera funktioner som gör AEM enklare:

* Smidig integrering med AEM instanser via Eclipse Server Connector.
* Synkronisering för både innehåll och OSGI-paket.
* Felsökningsstöd med möjlighet att byta kod under drift.
* Enkelt Bootstrap i AEM projekt med hjälp av en särskild projektguide.
* Enkel redigering av JCR-egenskaper.

## Krav {#requirements}

Innan du använder AEM Developer Tools ska du göra följande:

* Hämta och installera [Eclipse IDE for Java™ EE Developers](https://www.eclipse.org/downloads/packages/release/luna/r/eclipse-ide-java-ee-developers). AEM Developer Tools har för närvarande stöd för Eclipse Kepler eller senare

* Kan användas med AEM version 5.6.1 eller senare
* Konfigurera förmörkelseinstallationen för att säkerställa att du har minst 1 GB stackminne genom att redigera `eclipse.ini` konfigurationsfilen enligt beskrivningen i [Vanliga frågor om Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>I macOS högerklickar du **Eclipse.app** och sedan markera **Visa paketinnehåll** för att hitta `eclipse.ini`.

## Installera AEM Developer Tools for Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

När du har uppfyllt [krav](#requirements) ovan kan du installera plugin-programmet på följande sätt:

1. Bläddra i **AEM Developer Tools** webbplats på `https://eclipse.adobe.com/aem/dev-tools/`.

1. Kopiera **Installationslänk**.

   Du kan även hämta ett arkiv i stället för att använda installationslänken. Om du gör det kan du installera offline, men du saknar meddelanden om automatiska uppdateringar.

1. Öppna **Hjälp** -menyn.
1. Klicka **Installera ny programvara**.
1. Klicka **Lägg till...**.
1. I **Namn** AEM Developer Tools.
1. I **Plats** kopiera installations-URL:en.
1. Klicka **OK**.
1. Markera båda **AEM** och **Sling** plugin-program.
1. Klicka på **Nästa**.
1. Klicka på **Nästa**.
1. Godkänn de linjära avtalen och klicka på **Slutför**.
1. Klicka **Ja** för att starta om Eclipse.

## Importera befintliga projekt {#how-to-import-existing-projects}

>[!NOTE]
>
>Se [Så här arbetar du med ett paket i Eclipse när det hämtades från AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## AEM {#the-aem-perspective}

AEM utvecklingsverktyg för Eclipse levereras med ett perspektiv som ger dig full kontroll över dina AEM projekt och instanser.

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## Exempel på flermodulsprojekt {#sample-multi-module-project}

&quot;AEM utvecklingsverktyg&quot; innehåller ett exempel på ett flermodulsprojekt som hjälper dig att snabbt komma igång med projektkonfigurationen i Eclipse. Det är också en praktisk guide till flera AEM funktioner. [Läs mer om Project Archetype](https://github.com/adobe/aem-project-archetype).

Så här skapar du exempelprojektet:

1. I **Fil** > **Nytt** > **Projekt** -menyn, bläddra till **AEM** avsnitt och markera **Exempel på AEM projekt med flera moduler**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Klicka på **Nästa**.

   >[!NOTE]
   >
   >Det här steget kan ta en stund eftersom m2eclipse måste skanna arkivtypskatalogerna.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. Välj **com.adobe.granite.archietypes : sample-project-architype : (högsta antal)** från menyn och sedan klicka på **Nästa**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. Fyll i en **Namn**, **Grupp-ID** och **Artefakt-ID** för exempelprojektet. Du kan också välja att ange vissa avancerade egenskaper.

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. Konfigurera nu en AEM som Eclipse kan ansluta till.

   Om du vill använda felsökningsfunktionen måste du ha startat AEM i felsökningsläge, vilket du kan göra genom att lägga till följande på kommandoraden:

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. Klicka **Slutför**. Projektstrukturen skapas.

   >[!NOTE]
   >
   >I en ny anläggning (närmare bestämt: när större beroenden aldrig har laddats ned) kan det uppstå fel i projektet. I så fall följer du det förfarande som beskrivs i [Löser ogiltig projektdefinition](#resolving-invalid-project-definition).

## Felsökning {#troubleshooting}

### Löser ogiltig projektdefinition {#resolving-invalid-project-definition}

Så här löser du ogiltiga beroenden och projektdefinitioner:

1. Markera alla skapade projekt.
1. Högerklicka. På menyn **Maven**, markera **Uppdatera projekt**.
1. Kontrollera **Tvinga uppdateringar av ögonblicksbild/releaser**.
1. Klicka **OK**. Eclipse försöker hämta nödvändiga beroenden.

### Aktivera automatisk komplettering av taggbibliotek i JSP-filer {#enabling-tag-library-autocompletion-in-jsp-files}

Automatisk komplettering av taggbibliotek går inte att utföra eftersom rätt beroenden läggs till i projektet. Det finns ett känt fel i AEM Uber Jar, som inte innehåller de tld- och TagExtraInfo-filer som behövs.

Se till att artefakten org.apache.sling.scripting.jsp.taglib finns i klassökvägen före AEM Uber Jar. För Maven-projekt placerar du följande beroende i pom.xml före Uber Jar.

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

Se till att du lägger till rätt version för din distribution av AEM.

## Mer information {#more-information}

Den officiella versionen av Apache Sling IDE-verktygen för Eclipse-webbplatsen innehåller användbar information:

* The [**Apache Sling IDE-verktyg för Eclipse** Användarhandbok](https://sling.apache.org/documentation/development/ide-tooling.html)I den här dokumentationen får du hjälp med de övergripande begreppen, serverintegreringen och distributionsfunktionerna som stöds av AEM utvecklingsverktyg.
* The [Felsökningsavsnitt](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* The [Lista över kända fel](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

Följande tjänsteman [Eclipse](https://www.eclipse.org/) dokumentation kan hjälpa dig att konfigurera miljön:

* [Komma igång med Eclipse](https://www.eclipse.org/getting-started/)
* [Hjälpsystemet Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Maven Integration (m2eclipse)](https://www.eclipse.org/m2e/)
