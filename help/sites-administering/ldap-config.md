---
title: Konfigurera LDAP med AEM 6
seo-title: Configuring LDAP with AEM 6
description: Lär dig hur du konfigurerar LDAP med AEM.
seo-description: Learn how to configure LDAP with AEM.
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
exl-id: 2ebca4fb-20f7-499c-96a0-4018eaeddc1a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 0%

---

# Konfigurera LDAP med AEM 6 {#configuring-ldap-with-aem}

LDAP **L** ightweight **D** katalog **A**&#x200B;åtkomst **P** Protokoll) används för åtkomst till centraliserade katalogtjänster. Detta minskar den arbetsinsats som krävs för att hantera användarkonton eftersom de kan nås av flera program. En sådan LDAP-server är Active Directory. LDAP används ofta för att uppnå enkel inloggning, vilket gör att en användare kan få åtkomst till flera program efter inloggning en gång.

Användarkonton kan synkroniseras mellan LDAP-servern och databasen med LDAP-kontoinformation som sparas i databasen. Detta gör att konton kan tilldelas till databasgrupper för att tilldela de behörigheter och behörigheter som krävs.

Databasen använder LDAP-autentisering för att autentisera sådana användare, där inloggningsuppgifterna skickas till LDAP-servern för validering, vilket krävs innan åtkomst till databasen tillåts. För att förbättra prestandan kan validerade inloggningsuppgifter cachas av databasen med en tidsgräns för förfallodatum så att omvalidering sker efter en lämplig period.

När ett konto tas bort från LDAP-serververifieringen inte längre beviljas åtkomst till databasen. Information om LDAP-konton som sparas i databasen kan också rensas.

Användningen av sådana konton är transparent för användarna, de ser ingen skillnad mellan användar- och gruppkonton som skapats från LDAP och konton som skapats enbart i databasen.

I AEM 6 har LDAP-stödet en ny implementering som kräver en annan typ av konfiguration än i tidigare versioner.

Alla LDAP-konfigurationer är nu tillgängliga som OSGi-konfigurationer. De kan konfigureras via webbhanteringskonsolen på:
`https://serveraddress:4502/system/console/configMgr`

För att LDAP ska fungera med AEM måste du skapa tre OSGi-konfigurationer:

1. En LDAP-identitetsleverantör (IDP).
1. En synkroniseringshanterare.
1. En extern inloggningsmodul.

>[!NOTE]
>
>Titta [Oak&#39;s External Login Module - Authenticating with LDAP and Beyond](https://docs.adobe.com/content/ddc/en/gems/oak-s-external-login-module---authenticating-with-ldap-and-beyon.html#) för att göra externa inloggningsmoduler djupdykare.
>
>Ett exempel på hur du konfigurerar Experience Manager med Apache DS finns i [Konfigurerar Adobe Experience Manager 6.5 för att använda Apache Directory Service.](https://helpx.adobe.com/experience-manager/using/configuring-aem64-apache-directory-service.html)

## Konfigurera LDAP-identitetsleverantören {#configuring-the-ldap-identity-provider}

LDAP-identitetsprovidern används för att definiera hur användare hämtas från LDAP-servern.

Den finns i hanteringskonsolen under **Apache Jackrabbit Oak LDAP Identity Provider** namn.

Följande konfigurationsalternativ är tillgängliga för LDAP-identitetsleverantören:

<table>
 <tbody>
  <tr>
   <td><strong>LDAP-providernamn</strong></td>
   <td>Namnet på den här LDAP-providerkonfigurationen.</td>
  </tr>
  <tr>
   <td><strong>Värdnamn för LDAP-server</strong><br /> </td>
   <td>Värdnamn för LDAP-servern</td>
  </tr>
  <tr>
   <td><strong>LDAP-serverport</strong></td>
   <td>Port för LDAP-servern</td>
  </tr>
  <tr>
   <td><strong>Använd SSL</strong></td>
   <td>Anger om en SSL-anslutning (LDAP) ska användas.</td>
  </tr>
  <tr>
   <td><strong>Använd TLS</strong></td>
   <td>Anger om TLS ska startas på anslutningar.</td>
  </tr>
  <tr>
   <td><strong>Inaktivera certifikatkontroll</strong></td>
   <td>Anger om servercertifikatvalidering ska inaktiveras.</td>
  </tr>
  <tr>
   <td><strong>Bind DN</strong></td>
   <td>Unikt namn för användaren för autentisering. Om detta lämnas tomt utförs en anonym bindning.</td>
  </tr>
  <tr>
   <td><strong>Bind lösenord</strong></td>
   <td>Användarens lösenord för autentisering</td>
  </tr>
  <tr>
   <td><strong>Timeout för sökning</strong></td>
   <td>Tid tills sökningen tar slut</td>
  </tr>
  <tr>
   <td><strong>Admin pool max aktiv</strong></td>
   <td>Maximal aktiv storlek för administratörsanslutningspoolen.</td>
  </tr>
  <tr>
   <td><strong>Användarpoolen är max aktiv</strong></td>
   <td>Den maximala aktiva storleken för användaranslutningspoolen.</td>
  </tr>
  <tr>
   <td><strong>Användar-bas-DN</strong></td>
   <td>Unikt namn för användarsökningar</td>
  </tr>
  <tr>
   <td><strong>Användarobjektklasser</strong></td>
   <td>Listan över objektklasser som en användarpost måste innehålla.</td>
  </tr>
  <tr>
   <td><strong>Användar-id-attribut</strong></td>
   <td>Namnet på det attribut som innehåller användar-ID:t.</td>
  </tr>
  <tr>
   <td><strong>Extra filter för användare</strong></td>
   <td>Extra LDAP-filter som används vid sökning efter användare. Det sista filtret formateras så här: '(&amp;(&lt;idattr&gt;=&lt;userid&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)' (user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>Användarens DN-sökvägar</strong></td>
   <td>Anger om det unika namnet ska användas för att beräkna en del av den mellanliggande sökvägen.</td>
  </tr>
  <tr>
   <td><strong>Gruppbasens unika namn</strong></td>
   <td>Basens unika namn för gruppsökningar.</td>
  </tr>
  <tr>
   <td><strong>Gruppobjektklasser</strong></td>
   <td>Listan med objektklasser som en grupppost måste innehålla.</td>
  </tr>
  <tr>
   <td><strong>Gruppnamnsattribut</strong></td>
   <td>Namnet på det attribut som innehåller gruppnamnet.</td>
  </tr>
  <tr>
   <td><strong>Gruppera extra filter</strong></td>
   <td>Extra LDAP-filter som används vid sökning efter grupper. Det sista filtret formateras så här: '(&amp;(&lt;nameattr&gt;=&lt;groupname&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>Gruppera DN-sökvägar</strong></td>
   <td>Anger om det unika namnet ska användas för att beräkna en del av den mellanliggande sökvägen.</td>
  </tr>
  <tr>
   <td><strong>Gruppmedlemsattribut</strong></td>
   <td>Gruppattribut som innehåller medlemmarna i en grupp.</td>
  </tr>
 </tbody>
</table>

## Konfigurera synkroniseringshanteraren {#configuring-the-synchronization-handler}

Synkroniseringshanteraren definierar hur Indentity Provider-användare och -grupper ska synkroniseras med databasen.

Den finns under **Standardsynkhanterare för Apache Jackrabbit** i hanteringskonsolen.

Följande konfigurationsalternativ är tillgängliga för Synkroniseringshanteraren:

<table>
 <tbody>
  <tr>
   <td><strong>Namn på synkroniseringshanterare</strong></td>
   <td>Namn på synkroniseringskonfigurationen.</td>
  </tr>
  <tr>
   <td><strong>Förfallotid för användare</strong></td>
   <td>Varaktighet tills en synkroniserad användare går ut.</td>
  </tr>
  <tr>
   <td><strong>Automatiskt medlemskap för användare</strong></td>
   <td>Lista över grupper som en synkroniserad användare läggs till i automatiskt.</td>
  </tr>
  <tr>
   <td><strong>Mappning av användaregenskaper</strong></td>
   <td>Lista mappningsdefinition för lokala egenskaper från externa egenskaper.</td>
  </tr>
  <tr>
   <td><strong>Användarsökvägsprefix</strong></td>
   <td>Det sökvägsprefix som används när nya användare skapas.</td>
  </tr>
  <tr>
   <td><strong>Förfallotid för användarmedlemskap</strong></td>
   <td>Tid efter vilken medlemskapet upphör.<br /> </td>
  </tr>
  <tr>
   <td><strong>Inkapslingsdjup för användarmedlemskap</strong></td>
   <td>Returnerar det maximala djupet för gruppkapsling när medlemsrelationer synkroniseras. Värdet 0 inaktiverar sökning efter gruppmedlemskap. Värdet 1 lägger bara till en användares direktgrupper. Det här värdet har ingen effekt vid synkronisering av enskilda grupper endast när en användares medlemskapshistorik synkroniseras.</td>
  </tr>
  <tr>
   <td><strong>Förfallotid för grupp</strong></td>
   <td>Varaktighet tills en synkroniserad grupp förfaller.</td>
  </tr>
  <tr>
   <td><strong>Automatiskt gruppmedlemskap</strong></td>
   <td>Lista över grupper som en synkroniserad grupp läggs till i automatiskt.</td>
  </tr>
  <tr>
   <td><strong>Mappning av gruppegenskaper</strong></td>
   <td>Lista mappningsdefinition för lokala egenskaper från externa egenskaper.</td>
  </tr>
  <tr>
   <td><strong>Prefix för gruppsökväg</strong></td>
   <td>Det sökvägsprefix som används när nya grupper skapas.</td>
  </tr>
 </tbody>
</table>

## Den externa inloggningsmodulen {#the-external-login-module}

Den externa inloggningsmodulen finns under **Apache Jackrabbit Oak External Login Module** under hanteringskonsolen.

>[!NOTE]
>
>Apache Jackrabbit Oak External Login Module implementerar Java Authentication and Authorization Servi (JAAS)-specifikationerna. Se [Java Security Reference Guide för Oracle](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) för mer information.

Dess uppdrag är att definiera vilken identitetsleverantör och synkroniseringshanterare som ska användas, vilket effektivt binder de två modulerna.

Följande konfigurationsalternativ är tillgängliga:

| **JAAS-rankning** | Ange rangordningen (dvs. sorteringsordningen) för den här inloggningsmodulposten. Posterna sorteras i fallande ordning (dvs. högre rangordnade konfigurationer kommer först). |
|---|---|
| **JAAS-kontrollflagga** | Egenskap som anger om en LoginModule är OBLIGATORISK, REQUISITE, SUFFICIENT eller OPTIONAL.Mer information om vad dessa flaggor betyder finns i JAAS-konfigurationsdokumentationen. |
| **JAAS Realm** | Sfärnamnet (eller programnamnet) som LoginModule registreras mot. Om inget sfärnamn anges registreras LoginModule med en standardsfärk som konfigurerats i Felix JAAS-konfigurationen. |
| **Namn på identitetsleverantör** | Identitetsleverantörens namn. |
| **Namn på synkroniseringshanterare** | Synkroniseringshanterarens namn. |

>[!NOTE]
>
>Om du planerar att ha mer än en LDAP-konfiguration med din AEM-instans måste separata identitetsleverantörer och synkroniseringshanterare skapas för varje konfiguration.

## Konfigurera LDAP över SSL {#configure-ldap-over-ssl}

AEM 6 kan konfigureras för autentisering med LDAP över SSL genom att följa nedanstående procedur:

1. Kontrollera **Använd SSL** eller **Använd TLS** kryssrutor när du konfigurerar [LDAP-identitetsleverantör](#configuring-the-ldap-identity-provider).
1. Konfigurera Synkroniseringshanteraren och modulen för extern inloggning enligt inställningarna.
1. Installera SSL-certifikaten i Java VM om det behövs. Detta kan du göra med nyckelverktyget:

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. Testa anslutningen till LDAP-servern.

### Skapa SSL-certifikat {#creating-ssl-certificates}

Självsignerade certifikat kan användas när AEM konfigureras för autentisering med LDAP via SSL. Nedan visas ett exempel på ett arbetssätt för att generera certifikat som ska användas med AEM.

1. Kontrollera att du har ett SSL-bibliotek installerat och att det fungerar. I den här proceduren används OpenSSL som exempel.

1. Skapa en anpassad OpenSSL-konfigurationsfil (cnf). Detta kan du göra genom att kopiera standardkonfigurationsfilen **openssl.cnf **och anpassa den. På UNIX-system finns den vanligtvis på `/usr/lib/ssl/openssl.cnf`

1. Fortsätt till att skapa certifikatutfärdarens rotnyckel genom att köra följande kommando i en terminal:

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. Skapa sedan ett nytt självsignerat certifikat:

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. Inspect det nya certifikatet för att säkerställa att allt är i rätt ordning:

   `openssl x509 -noout -text -in root-ca.crt`

1. Kontrollera att alla mappar som anges i certifikatkonfigurationsfilen (.cnf) finns. Om inte, skapar du dem.
1. Skapa ett slumpmässigt startvärde genom att köra:

   `openssl rand -out private/.rand 8192`

1. Flytta de skapade .pem-filerna till de platser som är konfigurerade i .cnf-filen.

1. Lägg slutligen till certifikatet i Java-nyckelbehållaren.

## Aktivera felsökningsloggning {#enabling-debug-logging}

Felsökningsloggning kan aktiveras för både LDAP-identitetsleverantören och modulen för extern inloggning för att felsöka anslutningsproblem.

Om du vill aktivera felsökningsloggning måste du:

1. Gå till webbhanteringskonsolen.
1. Sök efter&quot;Konfiguration av loggningsloggare för Apache Sling&quot; och skapa två loggare med följande alternativ:

* Loggnivå: Felsök
* Loggfil logs/ldap.log
* Meddelandemönster: {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Logger: org.apache.jackrabbit.oak.security.authentication.ldap

* Loggnivå: Felsök
* Loggfil: logs/external.log
* Meddelandemönster: {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Logger: org.apache.jackrabbit.oak.spi.security.authentication.external

## Ett ord om gruppanknytning {#a-word-on-group-affiliation}

Användare som synkroniseras via LDAP kan ingå i olika grupper i AEM. Dessa grupper kan vara externa LDAP-grupper som läggs till AEM som en del av synkroniseringsprocessen, men de kan också vara grupper som läggs till separat och inte ingår i det ursprungliga LDAP-grupptillhörighetsschemat.

I de flesta fall kan dessa grupper läggas till av en lokal AEM eller av någon annan identitetsleverantör.

Om en användare tas bort från en grupp på LDAP-servern återspeglas ändringen även på AEM sida vid synkroniseringen. Alla andra grupptillhörigheter för användaren som inte lades till av LDAP finns dock kvar.

AEM upptäcker och hanterar rensning av användare från externa grupper genom att använda `rep:externalId` -egenskap. Den här egenskapen läggs till automatiskt för alla användare eller grupper som synkroniseras med Synchronization Handler och den innehåller information om den ursprungliga identitetsleverantören.

Mer information finns i dokumentationen för Apache Oak på [Användar- och gruppsynkronisering](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## Kända fel {#known-issues}

Om du tänker använda LDAP över SSL måste du kontrollera att de certifikat du använder skapas utan alternativet Netscape-kommentar. Om det här alternativet är aktiverat misslyckas autentiseringen med ett SSL-handskakningsfel.
