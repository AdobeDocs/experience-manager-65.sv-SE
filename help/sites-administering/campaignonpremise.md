---
title: Integrera med Adobe Campaign Classic
seo-title: Integrating with Adobe Campaign Classic
description: Lär dig integrera AEM med Adobe Campaign Classic
seo-description: Learn how to integrate AEM with Adobe Campaign Classic
uuid: 3c998b0e-a885-4aa9-b2a4-81b86f9327d3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: df94dd1b-1b65-478b-a28d-81807a8084b1
exl-id: a7281ca0-461f-4762-a631-6bb539596200
source-git-commit: 7fed5ce55f6ee7638d2578ee7ef2d84deb24277f
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 0%

---


# Integrera med Adobe Campaign Classic {#integrating-campaign-classic}

Genom att integrera AEM med Adobe Campaign kan ni hantera e-postleveranser, innehåll och formulär direkt i AEM. Konfigurationssteg i både Adobe Campaign Classic och AEM behövs för att möjliggöra dubbelriktad kommunikation mellan lösningar.

Tack vare den här integreringen kan AEM och Adobe Campaign Classic användas oberoende av varandra. Marknadsförare kan skapa kampanjer och använda målinriktning i Adobe Campaign, medan innehållsskapare kan arbeta parallellt med innehållsdesign i AEM. Tack vare integreringen kan innehåll och utformning av kampanjen i AEM riktas mot och levereras av Adobe Campaign.

## Integreringssteg {#integration-steps}

Integrationen mellan AEM och Campaign kräver ett antal steg i båda lösningarna.

1. [Installera AEM integreringspaket i Campaign.](#install-package)
1. [Skapa en operator för AEM i Campaign](#create-operator)
1. [Konfigurera Campaign-integrering i AEM](#campaign-integration)
1. [Konfigurera AEM](#externalizer)
1. [Konfigurera kampanjfjärranvändaren i AEM](#configure-user)
1. [Konfigurera det AEM externa kontot i Campaign](#acc-setup)

Det här dokumentet leder dig igenom dessa steg i detalj.

## Förutsättningar {#prerequisites}

* Administratörsåtkomst till Adobe Campaign Classic
   * För att kunna utföra integreringen behöver du en fungerande Adobe Campaign Classic-instans, inklusive en konfigurerad databas.
   * Om du vill ha mer information om hur du konfigurerar och konfigurerar Adobe Campaign Classic kan du läsa [Adobe Campaign Classic dokumentation,](https://experienceleague.adobe.com/docs/campaign-classic/using/campaign-classic-home.html) särskilt i installations- och konfigureringshandboken.
* Administratörsåtkomst till AEM

## Installera AEM integreringspaket i Campaign {#install-package}

The **AEM** i Adobe Campaign innehåller ett antal standardkonfigurationer som krävs för att ansluta till AEM.

1. Som administratör loggar du in på Adobe Campaign-instansen med klientkonsolen.

1. Välj **verktyg** > **Avancerat** > **Importera paket...**.

   ![Importera paket](assets/import-package.png)

1. Klicka **Installera ett standardpaket** och sedan klicka **Nästa**.

1. Kontrollera **AEM** paket.

   ![Installera ett standardpaket](assets/select-package.png)

1. Klicka **Nästa** och sedan **Starta** för att starta installationen.

   ![Installationsförlopp](assets/installation.png)

1. Klicka **Stäng** när installationen är klar.

Integrationspaketet är nu installerat.

## Skapa en operator för AEM i Campaign {#create-operator}

Integrationspaketet skapar automatiskt `aemserver` som AEM använder för att ansluta till Adobe Campaign. Du måste definiera en säkerhetszon för den här operatorn och ange dess lösenord.

1. Logga in på Adobe Campaign som administratör med klientkonsolen.

1. Välj **verktyg** -> **Utforskaren** på menyraden.

1. I Utforskaren går du till **Administration** > **Åtkomsthantering** > **Operatorer** nod.

1. Välj `aemserver` -operator.

1. På **Redigera** -operatorfliken väljer du **Åtkomsträttigheter** underfliken och klicka sedan på **Redigera åtkomstparametrar...** länk.

   ![Ange säkerhetszon](assets/access-rights.png)

1. Välj lämplig säkerhetszon och definiera den betrodda IP-masken efter behov.

1. Klicka **Spara**.

1. Logga ut från Adobe Campaign-klienten.

1. På Adobe Campaign-serverns filsystem går du till installationsplatsen för Campaign och redigerar `serverConf.xml` som administratör. Den här filen finns vanligtvis under:
   * `C:\Program Files\Adobe\Adobe Campaign Classic v7\conf` i Windows.
   * `/usr/local/neolane/nl6/conf/eng` i Linux.

1. Sök efter `securityZone` och se till att följande parametrar ställs in för AEM säkerhetszon.

   * `allowHTTP="true"`
   * `sessionTokenOnly="true"`
   * `allowUserPassword="true"`.

1. Spara filen.

1. Se till att säkerhetszonen inte skrivs över av respektive inställning i dialogrutan `config-<server name>.xml` -fil.

   * Om konfigurationsfilen innehåller en separat inställning för säkerhetszon ändrar du `allowUserPassword` attribut till `true`.

1. Om du vill ändra serverporten för Adobe Campaign Classic ersätter du `8080` med önskad port.

   >[!CAUTION]
   >
   >Som standard finns ingen säkerhetszon konfigurerad för operatorn. För att AEM ska kunna ansluta till Adobe Campaign måste du välja en zon enligt beskrivningen i föregående steg.
   >
   >Adobe rekommenderar starkt att du skapar en säkerhetszon som ska AEM för att undvika säkerhetsproblem. Mer information om detta finns i [Adobe Campaign Classic dokumentation.](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/security-zones.html)

1. Gå tillbaka till Campaign-klienten `aemserver` och väljer **Allmänt** -fliken.

1. Klicka på **Återställ lösenord...** länk.

1. Ange ett lösenord och lagra det på en säker plats för framtida bruk.

1. Klicka **OK** för att spara lösenordet för `aemserver` -operator.

## Konfigurera kampanjintegrering i AEM {#campaign-integration}

AEM [operatorn som du redan har ställt in i Campaign](#create-operator) för att kommunicera med Campaign

1. Logga in som administratör i din AEM.

1. Välj **verktyg** > **Cloud Services** > **Äldre Cloud Services** > **Adobe Campaign** och sedan klicka **Konfigurera nu**.

   ![Konfigurera Adobe Campaign](assets/configure-campaign-service.png)

1. I dialogrutan skapar du en konfiguration för Campaign-tjänsten genom att ange en **Titel** och klicka **Skapa**.

   ![Konfigurera Campaign-dialogrutan](assets/configure-campaign-dialog.png)

1. Ett nytt fönster och en ny dialogruta öppnas där du kan redigera konfigurationen. Tillhandahåll nödvändig information.

   * **Användarnamn** - Det här är [paketoperatorn Adobe Campaign AEM Integration som skapades i föregående steg.](#create-operator) Som standard är det `aemserver`.
   * **Lösenord** - Det här är lösenordet för [paketoperatorn Adobe Campaign AEM Integration som skapades i föregående steg.](#create-operator)
   * **API-slutpunkt** - Detta är Adobe Campaign instans-URL:en.

   ![Konfigurera Adobe Campaign i AEM](assets/configure-campaign.png)

1. Välj **Anslut till Adobe Campaign** för att bekräfta anslutningen och sedan klicka på **OK**.

AEM kan nu kommunicera med Adobe Campaign.

>[!NOTE]
>
>Se till att din Adobe Campaign-server är tillgänglig via Internet. AEM har inte åtkomst till privata nätverk.

## Konfigurerar replikering till AEM Publish Instance {#replication}

Kampanjinnehåll skapas av innehållsförfattare i AEM. Den här instansen är vanligtvis endast tillgänglig internt i din organisation. För att innehåll som bilder och resurser ska vara tillgängliga för mottagarna av kampanjen måste ni publicera det innehållet.

Replikeringsagenten ansvarar för att publicera ditt innehåll från AEM författarinstans till publiceringsinstansen och måste konfigureras för att integreringen ska fungera korrekt. Det här steget är också nödvändigt för att replikera vissa redigeringsinstanskonfigurationer till publiceringsinstansen.

Så här konfigurerar du replikering från AEM författarinstans till publiceringsinstansen:

1. Logga in som administratör i din AEM.

1. Välj **verktyg** > **Distribution** > **Replikering** > **Agenter på författare** och sedan trycka eller klicka **Standardagent (publicera)**.

   ![Konfigurera replikeringsagent](assets/acc-replication-config.png)

1. Tryck eller klicka **Redigera** väljer du **Transport** -fliken.

1. Konfigurera **URI** fält genom att ersätta standardvärdet `localhost` värde med IP-adressen för den AEM publiceringsinstansen.

   ![Fliken Transport](assets/acc-transport-tab.png)

1. Tryck eller klicka **OK** för att spara ändringarna i agentinställningarna.

Du har konfigurerat replikering till AEM publiceringsinstans så att kampanjmottagarna kan komma åt ditt innehåll.

>[!NOTE]
>
>Om du inte vill använda replikerings-URL:en utan i stället använder den offentliga URL:en kan du ange den offentliga URL:en i följande konfigurationsinställning via OSGi
>
>Välj **verktyg** > **Operationer** > **Webbkonsol** > **OSGi-konfiguration** och söka efter **AEM Campaign Integration - Configuration**. Redigera konfigurationen och ändra fältet **Offentlig URL** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`).

## Konfigurera AEM Externalizer {#externalizer}

[Externalizer](/help/sites-developing/externalizer.md) är en OSGi-tjänst i AEM som omvandlar en resurssökväg till en extern och absolut URL-adress, vilket krävs för att AEM ska kunna hantera innehåll som Campaign kan använda. Du måste konfigurera det för att Campaign-integreringen ska fungera.

1. Logga in som administratör i AEM.
1. Välj **verktyg** > **Operationer** > **Webbkonsol** > **OSGi-konfiguration** och söka efter **Day CQ link Externalizer**.
1. Som standard är den sista posten i **Domäner** -fältet är avsett för publiceringsinstansen. Ändra URL:en från standardvärdet `http://localhost:4503` till den offentliga publiceringsinstansen.

   ![Konfigurera Externalizer](assets/acc-externalizer-config.png)

1. Tryck eller klicka **Spara**.

Du har konfigurerat Externalizer och Adobe Campaign kan inte komma åt ditt innehåll.

>[!NOTE]
Publiceringsinstansen måste kunna nås från Adobe Campaign-servern. Om den pekar på `localhost:4503` eller en annan server som Adobe Campaign inte kan nå visas inte bilder från AEM i Adobe Campaign-konsolen.

## Konfigurera användaren på AEM {#configure-user}

För att Campaign ska kunna kommunicera med AEM måste du ange ett lösenord för `campaign-remote` användare i AEM.

1. Logga in AEM som administratör.
1. På huvudnavigeringskonsolen klickar du på **verktyg** till vänster.
1. Klicka sedan på **Säkerhet** -> **Användare** för att öppna användaradministrationskonsolen.
1. Leta reda på `campaign-remote` användare.
1. Välj `campaign-remote` användare och klicka **Egenskaper** för att redigera användaren.
1. I **Redigera användarinställningar** fönster, klicka **Ändra lösenord**.
1. Ange ett nytt lösenord för användaren och notera lösenordet på en säker plats för framtida bruk.
1. Klicka **Spara** för att spara lösenordsändringen.
1. Klicka **Spara och stäng** för att spara ändringarna i `campaign-remote` användare.

## Konfigurera det AEM externa kontot i Campaign {#acc-setup}

När [installera **AEM** paket i Campaign,](#install-package) ett externt konto skapas för AEM. Genom att konfigurera det här externa kontot kan Adobe Campaign ansluta till AEM, vilket möjliggör tvåvägskommunikation mellan lösningarna.

1. Logga in på Adobe Campaign som administratör med klientkonsolen.

1. Välj **verktyg** -> **Utforskaren** på menyraden.

1. I Utforskaren går du till **Administration** > **Plattform** > **Externa konton** nod.

   ![Externa konton](assets/external-accounts.png)

1. Leta reda på det externa AEM. Som standard har den värdena:

   * **Typ** - `AEM`
   * **Etikett** - `AEM Instance`
   * **Internt namn** - `aemInstance`

1. På **Allmänt** fliken för det här kontot anger du användarinformationen som du har definierat i [Ange användarlösenord för fjärrkampanj](#set-campaign-remote-password) steg.

   * **Server** - AEM författarserveradress
      * AEM författarserver måste kunna nås från Adobe Campaign Classic serverinstans.
      * Kontrollera att serveradressen **not** i ett avslutande snedstreck.
   * **Konto** - Som standard är detta `campaign-remote` användare som du anger i AEM [Ange användarlösenord för fjärrkampanj](#set-campaign-remote-password) steg.
   * **Lösenord** - Det här lösenordet är samma som `campaign-remote` användare som du anger i AEM [Ange användarlösenord för fjärrkampanj](#set-campaign-remote-password) steg.

1. Välj **Aktiverad** kryssrutan.

1. Klicka **Spara**.

Adobe Campaign kan nu kommunicera med AEM.

## Nästa steg {#next-steps}

När både Adobe Campaign Classic och AEM är konfigurerade är integreringen klar.

Nu kan du lära dig skapa nyhetsbrev i Adobe Experience Manager genom att fortsätta med [det här dokumentet.](/help/sites-authoring/campaign.md)
