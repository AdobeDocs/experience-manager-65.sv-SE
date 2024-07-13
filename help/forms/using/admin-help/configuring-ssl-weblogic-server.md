---
title: Konfigurera SSL för WebLogic Server
description: Lär dig hur du skapar en SSL-autentiseringsuppgift som ska användas på WebLogic-servern och hur du konfigurerar SSL för WebLogic Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---


# Konfigurera SSL för WebLogic Server {#configuring-ssl-for-weblogic-server}

Om du vill konfigurera SSL på WebLogic-servern behöver du en SSL-autentiseringsuppgift för autentisering. Du kan använda Java-nyckelverktyget för att utföra följande åtgärder för att skapa en autentiseringsuppgift:

* Skapa ett par med offentlig/privat nyckel, slå ihop den offentliga nyckeln i ett självsignerat X.509 v1-certifikat som lagras som en certifikatkedja med ett element och lagra sedan certifikatkedjan och den privata nyckeln i en ny nyckelbehållare. Den här nyckelbehållaren är programserverns nyckelbehållare för anpassad identitet.
* Extrahera certifikatet och infoga det i en ny nyckelbehållare. Den här nyckelbehållaren är programserverns nyckelbehållare för anpassat förtroende.

Konfigurera sedan WebLogic så att den använder nyckelbehållaren Custom Identity och Custom Trust som du skapade. Inaktivera även funktionen för verifiering av WebLogic-värdnamn eftersom det unika namn som användes för att skapa nyckelbehållarfilerna inte innehöll namnet på den dator som är värd för WebLogic.

## Skapa en SSL-autentiseringsuppgift som ska användas på WebLogic-servern {#creating-an-ssl-credential-for-use-on-weblogic-server}

Nyckelverktygskommandot finns vanligtvis i Java-katalogen jre/bin och måste innehålla flera alternativ och alternativvärden, som visas i följande tabell.

<table>
 <thead>
  <tr>
   <th><p>Alternativet Nyckelverktyg</p></th>
   <th><p>Beskrivning</p></th>
   <th><p>Alternativvärde</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>-alias</p></td>
   <td><p>Nyckelbehållarens alias.</p></td>
   <td>
    <ul>
     <li><p>Nyckelbehållare för anpassad identitet: <code>ads-credentials</code></p></li>
     <li><p>Nyckelbehållare för anpassat förtroende: <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>Den algoritm som ska användas för att generera nyckelparet.</p></td>
   <td><p>RSA</p><p>Du kan använda en annan algoritm beroende på företagets policy.</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>Sökvägsfilens plats och namn.</p><p>Platsen kan innehålla den absoluta sökvägen för filen. Den kan också vara relativ till den aktuella katalogen i kommandotolken där kommandot för nyckelverktyget anges.</p></td>
   <td>
    <ul>
     <li><p>Nyckelbehållare för anpassad identitet: <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[servernamn]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>Nyckelbehållare för anpassat förtroende: <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[servernamn]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-file</p></td>
   <td><p>Certifikatfilens plats och namn.</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-validity</p></td>
   <td><p>Antalet dagar som certifikatet anses vara giltigt.</p></td>
   <td><p>3650</p><p>Du kan använda ett annat värde beroende på företagets policy.</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>Lösenordet som skyddar innehållet i nyckelbehållaren. </p></td>
   <td>
    <ul>
     <li><p>Nyckelbehållare för anpassad identitet: Lösenordet för nyckelbehållaren måste motsvara lösenordet för SSL-autentiseringsuppgifter som har angetts för komponenten Trust Store i administrationskonsolen.</p></li>
     <li><p>Nyckelbehållare för anpassat förtroende: Använd samma lösenord som du använde för nyckelbehållaren för anpassad identitet.</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>Lösenordet som skyddar nyckelparets privata nyckel.</p></td>
   <td><p>Använd samma lösenord som för alternativet <code>-storepass</code>. Nyckellösenordet måste innehålla minst sex tecken.</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>Det unika namn som identifierar den person som äger nyckelbehållaren.</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> är identifieringen av den användare som äger nyckelbehållaren.</p></li>
     <li><p><code><i>[Group Name]</i></code> är identifieringen av den företagsgrupp som nyckelbehållarägaren tillhör.</p></li>
     <li><p><code><i>[Company Name]</i></code> är organisationens namn.</p></li>
     <li><p><code><i>[City Name]</i></code> är den ort där organisationen finns.</p></li>
     <li><p><code><i>[State or province]</i></code> är den region där din organisation finns.</p></li>
     <li><p><code><i>[Country Code]</i></code> är koden med två bokstäver för det land där organisationen finns.</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

Mer information om hur du använder kommandot keytool finns i filen keytool.html som är en del av JDK-dokumentationen.

## Skapa nyckelbehållare för anpassad identitet och pålitlighet {#create-the-custom-identity-and-trust-keystores}

1. Navigera från en kommandotolk till *[appserverdomain]*/adobe/*[servernamn]*.
1. Ange följande kommando:

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >Ersätt `[JAVA_HOME]`*med katalogen där JDK är installerat och ersätt texten i kursiv stil med värden som motsvarar din miljö.*

   Till exempel:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   Nyckelfilen för den anpassade identiteten med namnet&quot;ads-credentials.jks&quot; skapas i katalogen [appserverdomain]/adobe/[servernamn].

1. Extrahera certifikatet från nyckelbehållaren med annonsuppgifter genom att ange följande kommando:

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**password**

   >[!NOTE]
   >
   >Ersätt `[JAVA_HOME]` med katalogen där JDK är installerat och ersätt `store`*_* `password`* med lösenordet för nyckelbehållaren för anpassad identitet.*

   Till exempel:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   Certifikatfilen med namnet &quot;ads-ca.cer&quot; skapas i katalogen [appserverdomain]/adobe/[*servernamn*].

1. Kopiera filen ads-ca.cer till alla värddatorer som behöver säker kommunikation med programservern.
1. Infoga certifikatet i en ny nyckelfil (nyckelbehållaren Anpassat förtroende) genom att ange följande kommando:

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >Ersätt `[JAVA_HOME]` med den katalog där JDK är installerat och ersätt `store`*_* `password` och `key`*_* `password` *med dina egna lösenord.*

   Till exempel:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

Nyckelfilen för anpassat förtroende med namnet &quot;ads-ca.jks&quot; skapas i katalogen [appserverdomain]/adobe/&#39;server.

Konfigurera WebLogic så att den använder nyckelbehållaren Custom Identity och Custom Trust som du skapade. Inaktivera även funktionen för verifiering av WebLogic-värdnamn eftersom det unika namn som användes för att skapa nyckelbehållarfilerna inte innehöll namnet på den dator som är värd för WebLogic-servern.

## Konfigurera WebLogic att använda SSL {#configure-weblogic-to-use-ssl}

1. Starta administrationskonsolen för WebLogic-servern genom att skriva `https://`*[värdnamnet ]*`:7001/console` på URL-raden i en webbläsare.
1. Under Miljö, i Domänkonfigurationer, väljer du **Servrar > &#39;server&#39; > Konfiguration > Allmänt**.
1. Under Allmänt, i Konfiguration, kontrollerar du att **lyssningsporten är aktiverad** och **SSL-lyssningsporten aktiverad** är markerade. Om det inte är aktiverat gör du följande:

   1. Klicka på **Lås och redigera** under ändringscentret om du vill ändra markeringar och värden.
   1. Markera kryssrutorna för **lyssningsporten aktiverad** och **SSL-lyssningsporten aktiverad**.

1. Om den här servern är en hanterad server ändrar du lyssningsporten till ett oanvänt portvärde (till exempel 8001) och SSL-lyssningsporten till ett oanvänt portvärde (till exempel 8002). På en fristående server är SSL-standardporten 7002.
1. Klicka på **Versionskonfiguration**.
1. Under Miljö, i Domänkonfigurationer, klickar du på **Servrar > [*Hanterad server*] > Konfiguration > Allmänt**.
1. Under Allmänt, i Konfiguration, väljer du **Nyckelbehållare**.
1. Klicka på **Lås och redigera** under ändringscentret om du vill ändra markeringar och värden.
1. Klicka på **Ändra** för att hämta nyckelbehållarlistan som nedrullningsbar lista och välj **Anpassad identitet och anpassat förtroende**.
1. Ange följande värden under Identitet:

   **Anpassad identitetsnyckelbehållare**: *[appserverdomain]*/adobe/*[servernamn]*/ads-credentials.jks, där *[appserverdomain] *är den faktiska sökvägen och *[servernamn]* är programserverns namn.

   **Nyckellagringstyp för anpassad identitet**: JKS

   **Lösenfras för anpassad identitetsnyckelbehållare**: *mypassword* (lösenord för anpassad identitetsnyckelbehållare)

1. Ange följande värden under Lita på:

   **Namn på nyckelfil för anpassat förtroende**: `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`, där `*[appserverdomain]*` är den faktiska sökvägen

   **Nyckellagringstyp för anpassat förtroende**: JKS

   **Nyckelarkivlösenfras för anpassat förtroende**: *mypassword* (lösenord för anpassad förtroendenyckel)

1. Välj **SSL** under Allmänt i Konfiguration.
1. Som standard är Keystore valt för Identity and Trust Locations. Om inte, ändra den till nyckelbehållaren.
1. Ange följande värden under Identitet:

   **Alias för privat nyckel**: annonser-autentiseringsuppgifter

   **Lösenfras**: *mypassword*

1. Klicka på **Versionskonfiguration**.

## Inaktivera funktionen för värdnamnsverifiering {#disable-the-hostname-verification-feature}

1. Klicka på SSL på fliken Konfiguration.
1. Välj Ingen i listan Verifiering av värdnamn under Avancerat.

   Om värdnamnsverifiering inte är inaktiverat måste servervärdnamnet (CN) innehålla serverns värdnamn.

1. Klicka på Lås och redigera under Ändringscenter om du vill ändra markeringar och värden.
1. Starta om programservern.

