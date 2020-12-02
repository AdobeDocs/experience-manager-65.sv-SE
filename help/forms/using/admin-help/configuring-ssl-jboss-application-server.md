---
title: Konfigurera SSL för JBoss Application Server
seo-title: Konfigurera SSL för JBoss Application Server
description: Lär dig hur du konfigurerar SSL för JBoss Application Server.
seo-description: Lär dig hur du konfigurerar SSL för JBoss Application Server.
uuid: 7c13cf00-ea89-4894-a4fc-aaeec7ae9f66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c187daa4-41b7-47dc-9669-d7120850cafd
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---


# Konfigurerar SSL för JBoss-programservern {#configuring-ssl-for-jboss-application-server}

Om du vill konfigurera SSL på JBoss-programservern behöver du en SSL-autentiseringsuppgift för autentisering. Du kan använda Java-nyckelverktyget för att skapa en referens eller begära och importera en autentiseringsuppgift från en certifikatutfärdare (CA). Du måste sedan aktivera SSL på JBoss.

Du kan köra nyckelverktyget med ett enda kommando som innehåller all information som behövs för att skapa nyckelbehållaren.

I denna procedur:

* `[appserver root]` är arbetskatalogen för den programserver som kör AEM formulär.
* `[type]` är ett mappnamn som varierar beroende på vilken typ av installation du har utfört.

## Skapa en SSL-autentiseringsuppgift {#create-an-ssl-credential}

1. I en kommandotolk går du till *[JAVA HOME]*/bin och skriver följande kommando för att skapa autentiseringsuppgifter och nyckelbehållare:

   `keytool -genkey -dname "CN=`*Värdnamn* `, OU=`*Grupp* `, O=`*NamnFöretag* `,L=`*NamnOrt* `, S=`** `, C=`NamnDelstatLandskod  `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*nyckel_* `-keystore`*lösenordNyckelnyckelnamn* `.keystore`

   >[!NOTE]
   >
   >Ersätt `[JAVA_HOME]` med katalogen där JDK är installerat och ersätt texten i kursiv stil med värden som motsvarar din miljö. Värdnamnet är det fullständiga domännamnet för programservern.

1. Ange `keystore_password` när du uppmanas att ange ett lösenord. Lösenordet för nyckelbehållaren och nyckeln måste vara identiska.

   >[!NOTE]
   >
   >Det `keystore_password` *som anges i det här steget kan vara samma lösenord (key_password) som du angav i steg 1, eller så kan det vara ett annat lösenord.*

1. Kopiera *nyckelordsnamnet*.keystore till katalogen `[appserver root]/server/[type]/conf` genom att skriva något av följande kommandon:

   * (Windows Single Server) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * (Windows Server Cluster) copy `keystorename.keystore[appserver root]\domain\configuration`
   * (Linux Single Server) `cp keystorename.keystore [appserver root]/standalone/configuration`
   * (Linux Server Cluster) `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. Exportera certifikatfilen genom att skriva följande kommando:

   * (En server) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * (Serverkluster) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. Ange *keystore_password* när du uppmanas att ange ett lösenord.
1. Kopiera filen AEMForms_cert.cer till katalogen *[appserver root] \conf* genom att skriva följande kommando:

   * (Windows Single Server) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * (Windows Server Cluster) `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * (Linux Single Server) `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * (Linux Server Cluster) `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. Visa innehållet i certifikatet genom att skriva följande kommando:

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. Utför följande uppgift om du vill ge kontofilen skrivåtkomst i `[JAVA_HOME]\jre\lib\security`, om det behövs:

   * (Windows) Högerklicka på kontofilen och välj Egenskaper. Avmarkera sedan det skrivskyddade attributet.
   * (Linux) Typ `chmod 777 cacerts`

1. Importera certifikatet genom att skriva följande kommando:

   `keytool -import -alias “AEMForms Cert” -file`*AEMForms_* `.cer -keystore`*certJAVA_HOME* `\jre\lib\security\cacerts`

1. Ange `changeit` som lösenord. Det här lösenordet är standardlösenordet för en Java-installation och kan ha ändrats av systemadministratören.
1. När du uppmanas till `Trust this certificate? [no]`: skriver du `yes`. Bekräftelsen &quot;Certificate was added to keystore&quot; visas.
1. Om du ansluter via SSL från Workbench installerar du certifikatet på Workbench-datorn.
1. Öppna följande filer för redigering i en textredigerare:

   * En server - `[appserver root]`/standalone/configuration/lc_&lt;dbname/totalkey>.xml

   * Serverkluster - `[appserver root]`/domain/configuration/host.xml

   * Serverkluster - `[appserver root]`/domän/konfiguration/domän_&lt;dbname>.xml

1. 
   * **För en enda server lägger du** till följande efter &lt;dbaname>avsnittet i filen lc_ &lt;security-realms> .xml:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   Leta reda på `<server>`-avsnittet som finns efter följande kod:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Lägg till följande i &lt;server>-avsnittet som finns efter ovanstående kod:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **För serverkluster ska du lägga till följande efter-** avsnitt  [i ]appserverroten &lt;security-realms> \domain\configuration\host.xml på alla noder:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   På den primära noden i serverklustret går du till [appserver root]\domain\configuration\domain_&lt;dbname>.xml och letar reda på &lt;server>-avsnittet som finns efter följande kod:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Lägg till följande i &lt;server>-avsnittet som finns efter ovanstående kod:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. Ändra värdet för attributet `keystoreFile` och attributet `keystorePass` till nyckelbehållarlösenordet som du angav när du skapade nyckelbehållaren.
1. Starta om programservern:

   * För körklara installationer:

      * Klicka på Administrationsverktyg på Kontrollpanelen i Windows och sedan på Tjänster.
      * Välj JBoss för Adobe Experience Manager-formulär.
      * Välj Åtgärd > Stoppa.
      * Vänta tills tjänstens status visas som stoppad.
      * Välj Åtgärd > Start.
   * För förkonfigurerade eller manuellt konfigurerade JBoss-installationer i Adobe:

      * Navigera från en kommandotolk till *`[appserver root]`*/bin.
      * Stoppa servern genom att ange följande kommando:

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * Vänta tills JBoss-processen har stängts av helt (när JBoss-processen återgår till terminalen startades den i).
      * Starta servern genom att ange följande kommando:

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. Om du vill få åtkomst till administrationskonsolen med SSL skriver du `https://[host name]:'port'/adminui` i en webbläsare:

   Standardporten för SSL för JBoss är 8443. Ange den här porten när du öppnar AEM formulär.

## Begär en autentiseringsuppgift från en certifikatutfärdare {#request-a-credential-from-a-ca}

1. I en kommandotolk går du till *[JAVA HOME]*/bin och skriver följande kommando för att skapa nyckelbehållaren och nyckeln:

   `keytool -genkey -dname "CN=`*Värdnamn* `, OU=`*Grupp* `, O=`*Namn Företag* `, L=`*NamnOrt* `, S=`** `, C=`*NamnDelstatLandskod*&quot;  `-alias "AEMForms Cert"` `-keyalg RSA -keypass`-*key_* `-keystore`*passwordkeystorename* `.keystore`

   >[!NOTE]
   >
   >Ersätt *`[JAVA_HOME]`* med katalogen där JDK är installerat och ersätt texten i kursiv stil med värden som motsvarar din miljö.

1. Skriv följande kommando för att skapa en certifikatbegäran som ska skickas till certifikatutfärdaren:

   `keytool -certreq -alias` &quot;AEMForms Cert&quot;  `-keystore`** `.keystore -file`*keystorenameAEMFormscertRequest.csr*

1. När din begäran om en certifikatfil är klar slutför du nästa procedur.

## Använd en autentiseringsuppgift som hämtats från en certifikatutfärdare för att aktivera SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. I en kommandotolk går du till *`[JAVA HOME]`*/bin och skriver följande kommando för att importera rotcertifikatet för den certifikatutfärdare som CSR har signerats med:

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   Om rotcertifikatet inte finns i webbläsaren importerar du det också där.

   >[!NOTE]
   >
   >Ersätt *`[JAVA_HOME]`med katalogen där JDK är installerad och ersätt texten i kursiv stil med värden som motsvarar din miljö.*

1. I en kommandotolk går du till *`[JAVA HOME]`*/bin och anger följande kommando för att importera autentiseringsuppgifterna till nyckelbehållaren:

   `keytool -import -trustcacerts -file`** `.crt -keystore`*CACertificateNamekeystorename* `.keystore`

   >[!NOTE]
   >
   >* Ersätt `[JAVA_HOME]` med katalogen där JDK är installerat och ersätt texten i kursiv stil med värden som motsvarar din miljö.
   >* Det importerade CA-signerade certifikatet ersätter ett självsignerat offentligt certifikat om det finns.


1. Slutför steg 13-18 i Skapa en SSL-autentiseringsuppgift.
