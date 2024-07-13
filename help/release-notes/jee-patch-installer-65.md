---
title: AEM Forms JEE Patch Installer
description: Lär dig hur du använder AEM Forms JEE Patch Installer för att åtgärda problem i AEM 6.5 Forms-komponenter.
content-type: reference
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
hide: true
hidefromtoc: true
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# AEM Forms JEE Patch Installer {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Kontakta support](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support) om du vill ha mer information eller vill hämta korrigeringen.

## Om patch-installationsprogrammet {#about-the-patch-installer}

Installationsprogrammet för AEM 6.5 Forms JEE patch innehåller alla åtgärdade fel för alla komponenter i AEM 6.5 Forms JEE som är tillgängliga till dess att den här korrigeringen släppts. I den senaste [Service Pack-versionsinformationen](release-notes.md) finns en fullständig lista över åtgärdade problem.

## Krav för att installera korrigeringen {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Installera och konfigurera korrigeringen {#installing-and-configuring-the-patch}

1. Säkerhetskopiera mappen &lt;*AEM_forms_root*>/deploy. Det krävs om du bestämmer dig för att avinstallera snabbkorrigeringen.
1. Stoppa programservern.
1. Extrahera arkivfilen för patch-installationsprogrammet till hårddisken.
1. I katalogen som namnges enligt det operativsystem som du använder:

   * **Windows**
Navigera till rätt katalog på installationsmediet eller mappen på hårddisken där du kopierade installationsprogrammet och dubbelklicka på filen aemforms65_cfp_install.exe.

      * (32-bitars Windows) `Windows\Disk1\InstData\VM`
      * (64-bitars Windows) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
Navigera till rätt katalog och skriv `./aem65_cfp_install.bin` från en kommandotolk.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Då startas en installationsguide som vägleder dig genom installationen.

1. Klicka på **[!UICONTROL Next]** på introduktionspanelen.
1. På skärmen **Välj installationsmapp** kontrollerar du att den standardplats som visas är korrekt för den befintliga installationen. Du kan också klicka på **[!UICONTROL Browse]** och välja en alternativ mapp där AEM har installerats. Klicka sedan på **[!UICONTROL Next]**.
1. Läs Quick Fix Patch Summary-informationen och klicka på **[!UICONTROL Next]**.
1. Läs informationen om sammanfattning av förinstallation och klicka på **[!UICONTROL Install]**.
1. När installationen är klar klickar du på **[!UICONTROL Next]** för att tillämpa snabbkorrigeringsuppdateringarna på de installerade filerna.

1. **[För endast Windows]:** Gör följande:
   * Avmarkera alternativet **Starta Configuration Manager** innan du klickar på **[!UICONTROL Done]**. Kör **Configuration Manager** med filen **ConfigurationManager.bat** i `[aem-forms root]\configurationManager\bin`.

   * Du kan också avmarkera alternativet **Starta Configuration Manager** innan du klickar på **[!UICONTROL Done]**. Innan du kör **Configuration Manager** med **ConfigurationManager.exe** eller **ConfigurationManager_IPv6.exe** navigerar du till katalogen *`<AEMForms_Install_Dir>\configurationManager\bin`* och ersätter katalogen **ConfigurationManager.lax** och **ConfigurationManager_IPV6.lax** med den senaste [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) och [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) -filer söker du efter och ersätter **axis-1.4.1.1.jar** med **axis-1.4.1.2.jar** i dessa två filer.

   >[!NOTE]
   >
   >Om du använder filen **ConfigurationManager.bat** kan du undvika att uppdatera namnet på .lax-filer manuellt.
   >

1. **[Endast för Unix-baserade]:**

   * Kryssrutan **Starta Configuration Manager** är markerad som standard. Klicka på **[!UICONTROL Done]** om du vill köra Configuration Manager direkt eller **Configuration Manager** senare, avmarkera alternativet **Starta Configuration Manager** innan du klickar på **[!UICONTROL Done]**. Du kan starta **Configuration Manager** senare med lämpligt skript i katalogen `[AEM_forms_root]/configurationManager/bin`.

1. Beroende på vilken programserver du använder väljer du något av följande dokument och följer instruktionerna i avsnittet *Konfigurera och distribuera AEM formulär*.

   * [Installera och distribuera AEM formulär för JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Installera och distribuera AEM formulär för WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (Endast JBoss®) När du har installerat korrigeringen och konfigurerat servern tar du bort tmp och arbetskataloger för JBoss®-programservern.

## Konfigurationer för Post-driftsättning {#post-deployment-configurations}

### SAML-konfigurationer {#saml-configurations}

Om du har konfigurerat SAML-autentisering och har problem med stora IDP-metadata gör du följande efter att du har installerat korrigeringen:

1. Ange följande systemegenskap på programservern:\
   `um.saml.enable.large.xml=true`
1. Starta om servern.
1. Ta bort befintliga SAML-autentiseringsproviders och lägg till dem igen för befintliga domäner enligt beskrivningen i SAML-inställningarna.

>[!NOTE]
>
> Du bör använda kommandot Ctrl + C för att starta om SDK:n. Om du startar om AEM SDK med alternativa metoder, till exempel genom att stoppa Java-processer, kan det leda till inkonsekvenser i den AEM utvecklingsmiljön.

## Påverkade moduler {#impacted-modules}

* Dokumenttjänster
* Dokumentsäkerhet
* Foundation JEE

[Kontakta support](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support)
