---
title: AEM Forms JEE Patch Installer
description: 'null'
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
translation-type: tm+mt
source-git-commit: c1af919d4c0fd984249e1a7009274c63b8ce9adb
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# AEM Forms JEE Patch Installer {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html) om du vill ha mer information eller om du vill ha en patch.

## Om installationsprogrammet för korrigeringsfilen {#about-the-patch-installer}

Installationsprogrammet för AEM 6.5 Forms JEE patch innehåller alla åtgärdade fel för alla komponenter i AEM 6.5 Forms JEE som är tillgängliga till dess att den här korrigeringen släppts. En fullständig lista över åtgärdade problem finns i den senaste [Service Pack-versionsinformationen](sp-release-notes.md) .

## Krav för att installera korrigeringen {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Installera och konfigurera korrigeringen {#installing-and-configuring-the-patch}

1. Säkerhetskopiera mappen &lt;*AEM_forms_root*>/deploy. Det krävs om du bestämmer dig för att avinstallera snabbkorrigeringen.
1. Stoppa programservern.
1. Extrahera arkivfilen för patch-installationsprogrammet till hårddisken.
1. I katalogen som namnges enligt det operativsystem som du använder:

   * **Windows** Navigera till rätt katalog på installationsmediet eller mappen på hårddisken där du kopierade installationsprogrammet och dubbelklicka på filen aemforms65_cfp_install.exe.

      * (32-bitars Windows) `Windows\Disk1\InstData\VM`
      * (64-bitars Windows) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux** Navigera till rätt katalog och skriv från en kommandotolk 
`./aem65_cfp_install.bin`.

      * (Linux) `Linux/Disk1/InstData/NoVM`

   Då startas en installationsguide som vägleder dig genom installationen.

1. Klicka på panelen Introduktion **[!UICONTROL Next]**.
1. På skärmen Välj installationsmapp kontrollerar du att den standardplats som visas är korrekt för den befintliga installationen. Du kan också klicka på den alternativa mapp där AEM formulär installeras och sedan klicka på **[!UICONTROL Browse]** **[!UICONTROL Next]**.
1. Läs Quick Fix Patch Summary-informationen och klicka på **[!UICONTROL Next]**.
1. Läs mer i Sammanfattning av förinstallation och klicka på **[!UICONTROL Install]**.
1. När installationen är klar klickar du på **[!UICONTROL Next]** för att tillämpa snabbkorrigeringsuppdateringarna på de installerade filerna.

1. Avmarkera alternativet Starta Configuration Manager innan du klickar på Klar. Innan du kör konfigurationshanteraren med **ConfigurationManager.exe** eller **ConfigurationManager_IPv6.exe** går du till *&lt;AEMForms_Install_Dir>\configurationManager\bin* och uppdaterar **axis.jar** till **axis-1.4.1.1.jar** i följande filer:

   * ConfigurationManager.lax
   * ConfigurationManager_IPv6.lax

1. Kryssrutan Starta Configuration Manager är markerad som standard. Klicka **[!UICONTROL Done]** för att köra Configuration Manager.

1. Om du vill köra Configuration Manager senare avmarkerar du alternativet Starta Configuration Manager innan du klickar på Klar. Du kan starta Configuration Manager senare med rätt skript i `[AEM_forms_root]/configurationManager/bin` katalogen.

1. Beroende på vilken programserver du använder väljer du något av följande dokument och följer instruktionerna i avsnittet *Konfigurera och distribuera AEM formulär* .

   * [Installera och distribuera AEM formulär för JBoss](http://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Installera och distribuera AEM formulär för WebSphere](http://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (Endast JBoss) När du har installerat korrigeringen och konfigurerat servern tar du bort tmp och arbetskataloger för JBoss-programservern.

## Konfigurationer efter distributionen {#post-deployment-configurations}

### SAML-konfigurationer {#saml-configurations}

Om du har konfigurerat SAML-autentisering och har problem med stora IDP-metadata gör du följande när du har installerat korrigeringen:

1. Ange följande systemegenskap på programservern:\
   `um.saml.enable.large.xml=true`
1. Starta om servern.
1. Ta bort befintliga SAML-autentiseringsproviders och lägg till dem igen för befintliga domäner enligt beskrivningen i SAML-inställningarna.

## Påverkade moduler {#impacted-modules}

* Dokumenttjänster
* Dokumentsäkerhet
* Foundation JEE

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
