---
title: Integrera AEM 6.5 med Adobe Campaign Classic
description: Lär dig integrera AEM 6.5 med Adobe Campaign Classic
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: a7281ca0-461f-4762-a631-6bb539596200
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 6fb844ea428c15adab71503dde6138e46eabf0a3
workflow-type: tm+mt
source-wordcount: '1564'
ht-degree: 0%

---


# Integrera AEM 6.5 med Adobe Campaign Classic {#integrating-campaign-classic}

Genom att integrera AEM med Adobe Campaign Classic (ACC) kan ni hantera e-postleveranser, innehåll och formulär direkt i AEM. Konfigurationssteg i både Adobe Campaign Classic och AEM behövs för att möjliggöra dubbelriktad kommunikation mellan lösningar.

Tack vare den här integreringen kan AEM och Adobe Campaign Classic användas oberoende av varandra. Marknadsförare kan skapa kampanjer och använda målinriktning i Adobe Campaign, medan innehållsskapare kan arbeta parallellt med innehållsdesign i AEM. Tack vare integreringen kan innehållet i och utformningen av kampanjen som skapats i AEM målinrikta och levereras av Adobe Campaign.

>[!INFO]
>
>I det här dokumentet beskrivs hur du integrerar Adobe Campaign Classic med AEM 6.5. Andra Campaign-integreringar finns i dokumentet [Integrera AEM 6.5 med Adobe Campaign.](campaign.md)

## Integreringssteg {#integration-steps}

Integrationen mellan AEM och Campaign kräver flera steg i båda lösningarna.

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
   * Om du behöver mer information om hur du konfigurerar och konfigurerar Adobe Campaign Classic kan du läsa [Adobe Campaign Classic-dokumentationen](https://experienceleague.adobe.com/docs/campaign-classic/using/campaign-classic-home.html?lang=sv-SE), särskilt installations- och konfigurationsguiden.
* Administratörsåtkomst till AEM

## Installera AEM integreringspaket i Campaign {#install-package}

Paketet **AEM Integration** i Adobe Campaign innehåller flera standardkonfigurationer som krävs för att ansluta till AEM.

1. Som administratör loggar du in på Adobe Campaign-instansen med klientkonsolen.

1. Välj **Verktyg** > **Avancerat** > **Importera paket...**.

   ![Importera paket](assets/import-package.png)

1. Klicka på **Installera ett standardpaket** och sedan på **Nästa**.

1. Kontrollera paketet **AEM Integration**.

   ![Installera ett standardpaket](assets/select-package.png)

1. Klicka på **Nästa** och sedan på **Start** för att påbörja installationen.

   ![Installationsförlopp](assets/installation.png)

1. Klicka på **Stäng** när installationen är klar.

Integrationspaketet är nu installerat.

## Skapa operatorn för AEM i Campaign {#create-operator}

Integrationspaketet skapar automatiskt operatorn `aemserver` som AEM använder för att ansluta till Adobe Campaign. Definiera en säkerhetszon för den här operatorn och ange dess lösenord.

1. Logga in på Adobe Campaign som administratör med klientkonsolen.

1. Välj **Verktyg** > **Utforskaren** på menyraden.

1. Gå till noden **Administration** > **Åtkomsthantering** > **Operatorer** i Utforskaren.

1. Välj operatorn `aemserver`.

1. På fliken **Redigera** för operatorn markerar du underfliken **Åtkomstbehörighet** och klickar sedan på länken **Redigera åtkomstparametrar..** .

   ![Ange säkerhetszon](assets/access-rights.png)

1. Välj lämplig säkerhetszon och definiera den betrodda IP-masken efter behov.

   >[!CAUTION]
   >
   >Säkerhetszonen som ska konfigureras är **Privat företagsnätverk (VPN+LAN)**.

1. Klicka på **Spara**.

1. Logga ut från Adobe Campaign klient.

1. På Adobe Campaign-serverns filsystem går du till installationsplatsen för Campaign och redigerar filen `serverConf.xml` som administratör. Den här filen finns vanligtvis under:
   * `C:\Program Files\Adobe\Adobe Campaign Classic v7\conf` i Windows.
   * `/usr/local/neolane/nl6/conf/eng` i Linux.

1. Sök efter `securityZone` och kontrollera att följande parametrar har angetts för säkerhetszonen för AEM.

   * `allowHTTP="true"`
   * `sessionTokenOnly="true"`
   * `allowUserPassword="true"`.

1. Spara filen.

1. Kontrollera att säkerhetszonen inte skrivs över av respektive inställning i filen `config-<server name>.xml`.

   * Om konfigurationsfilen innehåller en separat säkerhetsinställning ändrar du attributet `allowUserPassword` till `true`.

1. Om du vill ändra Adobe Campaign Classic-serverporten ersätter du `8080` med den önskade porten.

   >[!CAUTION]
   >
   >Som standard finns ingen säkerhetszon konfigurerad för operatorn. För att AEM ska kunna ansluta till Adobe Campaign måste du välja en zon enligt beskrivningen i föregående steg.
   >
   >Adobe rekommenderar starkt att du skapar en säkerhetszon som ska AEM för att undvika säkerhetsproblem. Mer information om det här avsnittet finns i [Adobe Campaign Classic-dokumentationen.](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/security-zones.html?lang=sv-SE)

1. Gå tillbaka till operatorn `aemserver` i Campaign-klienten och välj fliken **Allmänt**.

1. Klicka på länken **Återställ lösenord..**.

1. Ange ett lösenord och lagra det på en säker plats för framtida bruk.

1. Klicka på **OK** för att spara lösenordet för operatorn `aemserver`.

## Konfigurera Campaign-integrering i AEM {#campaign-integration}

AEM använder [operatorn som du redan har konfigurerat i Campaign](#create-operator) för att kommunicera med Campaign

1. Logga in som administratör i AEM redigeringsinstans.

1. På den globala navigeringssidan väljer du **Verktyg** > **Cloud Service** > **Äldre Cloud Service** > **Adobe Campaign** och klickar sedan på **Konfigurera nu**.

   ![Konfigurera Adobe Campaign](assets/configure-campaign-service.png)

1. I dialogrutan skapar du en konfiguration för Campaign-tjänsten genom att ange en **titel** och klicka på **Skapa**.

   ![Konfigurera kampanjdialogrutan](assets/configure-campaign-dialog.png)

1. Ett nytt fönster och en ny dialogruta öppnas där du kan redigera konfigurationen. Tillhandahåll nödvändig information.

   * **Användarnamn** - Detta är [den Adobe Campaign AEM Integration-paketoperator som skapades i föregående steg.](#create-operator) Som standard är det `aemserver`.
   * **Lösenord** - Det här är lösenordet för [den Adobe Campaign AEM Integration-paketoperator som skapades i föregående steg.](#create-operator)
   * **API-slutpunkt** - Detta är Adobe Campaign-instans-URL:en.

   ![Konfigurera Adobe Campaign i AEM](assets/configure-campaign.png)

1. Välj **Anslut till Adobe Campaign** för att verifiera anslutningen och klicka sedan på **OK**.

AEM kan nu kommunicera med Adobe Campaign.

>[!NOTE]
>
>Se till att din Adobe Campaign-server är tillgänglig via Internet. AEM har inte åtkomst till privata nätverk.

## Konfigurera replikering till AEM Publish-instans {#replication}

Kampanjinnehåll skapas av innehållsförfattare i AEM. Den här instansen är vanligtvis endast tillgänglig internt i din organisation. För att innehåll som bilder och resurser ska vara tillgängliga för mottagarna av kampanjen måste ni publicera det innehållet.

Replikeringsagenten ansvarar för att publicera ditt innehåll från AEM författarinstans till publiceringsinstansen och måste konfigureras för att integreringen ska fungera korrekt. Det här steget är också nödvändigt för att replikera vissa redigeringsinstanskonfigurationer till publiceringsinstansen.

Så här konfigurerar du replikering från AEM författarinstans till publiceringsinstansen:

1. Logga in som administratör i AEM redigeringsinstans.

1. På den globala navigeringssidan väljer du **Verktyg** > **Distribution** > **Replikering** > **Agenter på författare** och klickar sedan på **Standardagent (publicering)**.

   ![Konfigurera replikeringsagenten](assets/acc-replication-config.png)

1. Klicka på **Redigera** och välj sedan fliken **Transport**.

1. Konfigurera fältet **URI** genom att ersätta standardvärdet `localhost` med IP-adressen för den AEM publiceringsinstansen.

   ![Fliken Transport](assets/acc-transport-tab.png)

1. Klicka på **OK** om du vill spara ändringarna i agentinställningarna.

Du har konfigurerat replikering till AEM publiceringsinstans så att kampanjmottagarna kan komma åt ditt innehåll.

>[!NOTE]
>
>Om du inte vill använda replikerings-URL:en utan i stället använder den offentliga URL:en kan du ange den offentliga URL:en i följande konfigurationsinställning via OSGi
>
>På den globala navigeringssidan väljer du **Verktyg** > **Åtgärder** > **Webbkonsol** > **OSGi-konfiguration** och söker efter **AEM Campaign Integration - Configuration**. Redigera konfigurationen och ändra fältet **Offentlig URL** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`).

## Konfigurera AEM {#externalizer}

[Externalizer](/help/sites-developing/externalizer.md) är en OSGi-tjänst i AEM som omvandlar en resurssökväg till en extern och absolut URL, vilket är nödvändigt för att AEM ska kunna hantera innehåll som Campaign kan använda. Konfigurera så att Campaign-integreringen fungerar.

1. Logga in som administratör i AEM.
1. Välj **Verktyg** > **Åtgärder** > **Webbkonsol** > **OSGi-konfiguration** i den globala navigeringssidlisten och sök efter **Day CQ-länkens externaliserare**.
1. Som standard är den sista posten i fältet **Domäner** avsedd för publiceringsinstansen. Ändra URL:en från standardvärdet `http://localhost:4503` till den offentliga publiceringsinstansen.

   ![Konfigurerar externaliseraren](assets/acc-externalizer-config.png)

1. Klicka på **Spara**.

Du har konfigurerat Externalizer och Adobe Campaign kan nu komma åt ditt innehåll.

>[!NOTE]
>
>Publiceringsinstansen måste kunna nås från Adobe Campaign-servern. Om den pekar på `localhost:4503` eller en annan server som Adobe Campaign inte kan nå visas inte bilder från AEM i Adobe Campaign-konsolen.

## Konfigurera användaren på AEM {#configure-user}

För att Campaign ska kunna kommunicera med AEM måste du ange ett lösenord för användaren `campaign-remote` i AEM.

1. Logga in AEM som administratör.
1. På huvudnavigeringskonsolen klickar du på **Verktyg** i den vänstra listen.
1. Klicka sedan på **Säkerhet** > **Användare** för att öppna användaradministrationskonsolen.
1. Leta reda på användaren `campaign-remote`.
1. Markera användaren `campaign-remote` och klicka på **Egenskaper** för att redigera användaren.
1. Klicka på **Ändra lösenord** i fönstret **Redigera användarinställningar**.
1. Ange ett nytt lösenord för användaren och notera lösenordet på en säker plats för framtida bruk.
1. Klicka på **Spara** för att spara lösenordsändringen.
1. Klicka på **Spara och stäng** för att spara ändringarna för användaren `campaign-remote`.

## Konfigurera det AEM externa kontot i kampanj {#acc-setup}

När [installerar paketet **AEM Integration** i Campaign &#x200B;](#install-package) skapas ett externt konto för AEM. Genom att konfigurera det här externa kontot kan Adobe Campaign ansluta till AEM, vilket möjliggör tvåvägskommunikation mellan lösningarna.

1. Logga in på Adobe Campaign som administratör med klientkonsolen.

1. Välj **Verktyg** > **Utforskaren** på menyraden.

1. Gå till noden **Administration** > **Plattform** > **Externa konton** i Utforskaren.

   ![Externa konton](assets/external-accounts.png)

1. Leta reda på det externa AEM-kontot. Som standard har den värdena:

   * **Typ** - `AEM`
   * **Etikett** - `AEM Instance`
   * **Internt namn** - `aemInstance`

1. På fliken **Allmänt** för det här kontot anger du användarinformationen som du definierade i steget [Ange användarlösenord för fjärrkampanj](#set-campaign-remote-password).

   * **Server** - AEM författarserveradress
      * AEM författarserver måste kunna nås från Adobe Campaign Classic serverinstans.
      * Kontrollera att serveradressen **inte** avslutas med ett avslutande snedstreck.
   * **Konto** - Som standard är detta den `campaign-remote` användare som du anger i AEM i steget [Ange användarlösenord för fjärrkampanj](#set-campaign-remote-password).
   * **Lösenord** - Det här lösenordet är samma som den `campaign-remote`-användare som du angav i AEM i [Ange lösenord för kampanjfjärranvändare](#set-campaign-remote-password).

1. Markera kryssrutan **Aktiverad**.

1. Klicka på **Spara**.

Adobe Campaign kan nu kommunicera med AEM.

## Nästa steg {#next-steps}

När både Adobe Campaign Classic och AEM är konfigurerade är integreringen nu klar.

Nu kan du lära dig hur du skapar ett nyhetsbrev i Adobe Experience Manager genom att fortsätta med [det här dokumentet.](/help/sites-authoring/campaign.md)
