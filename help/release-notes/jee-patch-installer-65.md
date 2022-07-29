---
title: AEM Forms JEE Patch Installer
description: AEM Forms JEE Patch Installer
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: d28d78e426f1e89caa8bd28b067765d40b95cb8a
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# AEM Forms JEE Patch Installer {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html) för mer information eller för att få plåstret.

## Om installationsprogrammet för korrigeringsfilen {#about-the-patch-installer}

Installationsprogrammet för AEM 6.5 Forms JEE patch innehåller alla åtgärdade fel för alla komponenter i AEM 6.5 Forms JEE som är tillgängliga till dess att den här korrigeringen släppts. Se de senaste  [Versionsinformation för Service Pack](release-notes.md) för en fullständig lista över åtgärdade problem.

## Krav för att installera korrigeringen {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Installera och konfigurera korrigeringen {#installing-and-configuring-the-patch}

1. Säkerhetskopiera &lt;*AEM_forms_root*>/distribuera mapp. Det krävs om du bestämmer dig för att avinstallera snabbkorrigeringen.
1. Stoppa programservern.
1. Extrahera arkivfilen för patch-installationsprogrammet till hårddisken.
1. I katalogen som namnges enligt det operativsystem som du använder:

   * **Windows**
Navigera till rätt katalog på installationsmediet eller mappen på hårddisken där du kopierade installationsprogrammet och dubbelklicka på filen aemforms65_cfp_install.exe.

      * (32-bitars Windows) `Windows\Disk1\InstData\VM`
      * (64-bitars Windows) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux**
Navigera till rätt katalog och skriv i en kommandotolk 
`./aem65_cfp_install.bin`.

      * (Linux) `Linux/Disk1/InstData/NoVM`

   Då startas en installationsguide som vägleder dig genom installationen.

1. På introduktionspanelen klickar du på **[!UICONTROL Next]**.
1. Kontrollera att den standardplats som visas är korrekt för din befintliga installation på skärmen Välj installationsmapp, eller klicka på **[!UICONTROL Browse]** för att välja en alternativ mapp där AEM är installerad och klicka på **[!UICONTROL Next]**.
1. Läs Quick Fix Patch Summary-informationen och klicka på **[!UICONTROL Next]**.
1. Läs mer i Sammanfattning av förinstallation och klicka på **[!UICONTROL Install]**.
1. När installationen är klar klickar du på **[!UICONTROL Next]** för att använda snabbkorrigeringsuppdateringar på dina installerade filer.

1. Avmarkera alternativet Starta Configuration Manager innan du klickar på Klar. Innan du kör konfigurationshanteraren med **ConfigurationManager.exe** eller **ConfigurationManager_IPv6.exe**, navigera till *&lt;aemforms_install_dir>\configurationManager\bin* katalog och uppdatering `ConfigurationManager.lax` och `ConfigurationManager_IPv6.lax` filer med följande namnbytesåtgärder:

   * `axis.jar` till `axis-1.4.1.1.jar`
   * `serializer-2.7.1.jar` till `serializer-2.7.2.jar`
   * `xalan-2.7.1.jar` till `xalan-2.7.2.jar`
   * `xercesImpl-2.9.1.jar` till `xercesImpl-2.12.0.jar`
   * `xml-apis-2.7.1.jar` till `xml-apis-2.7.2.jar`

1. Kryssrutan Starta Configuration Manager är markerad som standard. Klicka **[!UICONTROL Done]** för att köra Configuration Manager.

1. Om du vill köra Configuration Manager senare avmarkerar du alternativet Starta Configuration Manager innan du klickar på Klar. Du kan starta Configuration Manager senare med rätt skript i `[AEM_forms_root]/configurationManager/bin` katalog.

1. Beroende på programservern väljer du ett av följande dokument och följer instruktionerna i *Konfigurera och distribuera AEM formulär* -avsnitt.

   * [Installera och distribuera AEM formulär för JBoss](http://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Installera och distribuera AEM formulär för WebSphere](http://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (Endast JBoss) När du har installerat korrigeringen och konfigurerat servern tar du bort tmp och arbetskataloger för JBoss-programservern.

>**Obs!** Innan du startar **Konfigurationshanteraren**, hämta och ersätta [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) -fil.

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
