---
title: Utveckla AEM projekt med IntelliJ IDEA
description: Lär dig använda IntelliJ IDEA för att utveckla Adobe Experience Manager-projekt.
uuid: 382b5008-2aed-4e08-95be-03c48f2b549e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: df6410a2-794e-4fa2-ae8d-37271274d537
exl-id: 5a79c79b-df65-4cb2-b9d4-eda994c992ec
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 1%

---

# Utveckla AEM projekt med IntelliJ IDEA{#how-to-develop-aem-projects-using-intellij-idea}

## Ökning {#overview}

För att komma igång med utvecklingen AEM IntelliJ krävs följande steg.

Varje steg förklaras mer ingående i resten av detta avsnitt.

* Installera IntelliJ
* Konfigurera ditt AEM baserat på Maven
* Förbered JSP-stöd för IntelliJ i Maven POM
* Importera Maven Project till IntelliJ

>[!NOTE]
>
>Den här guiden bygger på IntelliJ IDEA Ultimate Edition 12.1.4 och AEM 5.6.1.

### Installera IntelliJ IDEA {#install-intellij-idea}

Hämta IntelliJ IDEA från [nedladdningssidan på JetBrains](https://www.jetbrains.com/idea/download/).

Följ sedan installationsanvisningarna på den sidan.

### Konfigurera ditt AEM baserat på Maven {#set-up-your-aem-project-based-on-maven}

Konfigurera sedan projektet med Maven enligt beskrivningen i [Skapa AEM projekt med Apache Maven](/help/sites-developing/ht-projects-maven.md).

För att börja arbeta med AEM projekt i IntelliJ IDEA är grundinställningarna i [Komma igång om 5 minuter](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) är tillräckligt.

### Förbered JSP-stöd för IntelliJ IDEA {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA kan även ge stöd vid arbete med JSP, till exempel:

* automatisk komplettering av taggbibliotek
* medvetenhet om objekt som definieras av `<cq:defineObjects />` och `<sling:defineObjects />`

För att det ska fungera, följ instruktionerna på [Så här arbetar du med JSP:er](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [Skapa AEM projekt med Apache Maven](/help/sites-developing/ht-projects-maven.md).

### Importera projektet Maven {#import-the-maven-project}

1. Öppna **Importera** i IntelliJ IDEA genom att

   * markera **Importera projekt** på välkomstskärmen om du inte har något projekt öppet än
   * markera **Arkiv > Importera projekt** på huvudmenyn

1. Välj POM-filen för projektet i dialogrutan Importera.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Fortsätt med standardinställningarna enligt dialogrutan nedan.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Fortsätt genom följande dialogrutor genom att klicka på **Nästa** och **Slutför**.
1. Du är nu konfigurerad för AEM Development med IntelliJ IDEA

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### Felsöka JSP:er med IntelliJ IDEA {#debugging-jsps-with-intellij-idea}

Följande steg är nödvändiga för att felsöka JSP:er med IntelliJ IDEA

* Konfigurera en webbaspekt i projektet
* Installera JSR45 support-plugin
* Konfigurera en felsökningsprofil
* Konfigurera AEM för felsökningsläge

#### Konfigurera en webbaspekt i projektet {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA måste förstå var JSP:er för felsökning ska hittas. Eftersom IDEA inte kan tolka `content-package-maven-plugin` -inställningar måste den konfigureras manuellt.

1. Gå till **Arkiv > Projektstruktur**
1. Välj **Innehåll** modul
1. Klicka **+** ovanför listan med moduler och välj **Webb**
1. Som webbresurskatalog väljer du `content/src/main/content/jcr_root subdirectory` av ditt projekt enligt skärmbilden nedan.

![chlimage_1-48](assets/chlimage_1-48a.png)

#### Installera JSR45 support-plugin {#install-the-jsr-support-plugin}

1. Gå till **Plugins** i IntelliJ IDEA-inställningarna
1. Navigera till **JSR45-integrering** Plugin-program och markera kryssrutan bredvid det
1. Klicka **Använd**
1. Starta om IntelliJ IDEA när du ombeds att

![chlimage_1-49](assets/chlimage_1-49a.png)

#### Konfigurera en felsökningsprofil {#configure-a-debug-profile}

1. Gå till **Kör > Redigera konfigurationer**
1. Träffa **+** och markera **JSR45-fjärr**
1. Välj **Konfigurera** nästa **Programserver** och konfigurera en allmän server
1. Ange en lämplig URL för startsidan om du vill öppna en webbläsare när du startar felsökningen
1. Ta bort alla **Före start** uppgifter om du använder vlt autosync eller konfigurerar lämpliga Maven-uppgifter om du inte gör det
1. På **Start/anslutning** ruta, justera porten om det behövs
1. Kopiera de kommandoradsargument som IntelliJ IDEA föreslår

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### Konfigurera AEM för felsökningsläge {#configure-aem-for-debug-mode}

Det sista steget är att börja AEM med de JVM-alternativ som IntelliJ IDEA föreslår.

Starta AEM jar-filen direkt och lägg till dessa alternativ med följande kommandorad:

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -jar cq-quickstart-6.5.0.jar`

Du kan också lägga till dessa alternativ i startskriptet i `crx-quickstart/bin/start` enligt nedan.

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### Starta felsökning {#start-debugging}

Du är nu redo att felsöka JSP:er i AEM.

1. Välj **Kör > Felsök > Din felsökningsprofil**
1. Ange brytpunkter i komponentkoden
1. Öppna en sida i webbläsaren

![chlimage_1-52](assets/chlimage_1-52a.png)

### Felsökningspaket med IntelliJ IDEA {#debugging-bundles-with-intellij-idea}

Kod i paket kan felsökas med en allmän fjärrfelsökningsanslutning som standard. Du kan följa [Jetbrain-dokumentation om fjärrfelsökning](https://www.jetbrains.com/help/idea/remote-debugging-with-product.html#remote-interpreter).
