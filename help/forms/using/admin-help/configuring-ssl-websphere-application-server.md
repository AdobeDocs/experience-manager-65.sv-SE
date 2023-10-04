---
title: Konfigurera SSL för WebSphere Application Server
description: Lär dig hur du konfigurerar SSL för WebSphere Application Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b0786b52-879e-4a24-9cc9-bd9dcb2473cc
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 0%

---

# Konfigurera SSL för WebSphere Application Server {#configuring-ssl-for-websphere-application-server}

I det här avsnittet beskrivs följande steg för att konfigurera SSL med IBM WebSphere Application Server.

## Skapa ett lokalt användarkonto i WebSphere {#creating-a-local-user-account-on-websphere}

För att aktivera SSL behöver WebSphere åtkomst till ett användarkonto i det lokala operativsystemets användarregister som har behörighet att administrera systemet:

* (Windows) Skapa en ny Windows-användare som är en del av gruppen Administratörer och har behörighet att fungera som en del av operativsystemet. (Se [Skapa en Windows-användare för WebSphere](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere).)
* (Linux, UNIX) Användaren kan vara en rotanvändare eller en annan användare som har rotbehörighet. När du aktiverar SSL på WebSphere använder du den här användarens server-ID och lösenord.

### Skapa en Linux- eller UNIX-användare för WebSphere {#create-a-linux-or-unix-user-for-websphere}

1. Logga in som root-användare.
1. Skapa en användare genom att ange följande kommando i en kommandotolk:

   * (Linux och Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. Ställ in lösenordet för den nya användaren genom att ange `passwd` kommandotolken.
1. (Linux och Solaris) Skapa en skugglösenordsfil genom att ange `pwconv` (utan parametrar) i kommandotolken.

   >[!NOTE]
   >
   >(Linux och Solaris) För att WebSphere Application Server Local OS-säkerhetsregistret ska fungera måste det finnas en skugglösenordsfil. Skugglösenordsfilen heter **vanligtvis /etc/shadow** och baseras på filen /etc/passwd. Om skugglösenordsfilen inte finns uppstår ett fel efter aktivering av global säkerhet och konfiguration av användarregistret som lokalt operativsystem.

1. Öppna gruppfilen från katalogen /etc i en textredigerare.
1. Lägg till användaren som du skapade i steg 2 i `root` gruppen.
1. Spara och stäng filen.
1. (UNIX med SSL aktiverat) Starta och stoppa WebSphere som rotanvändare.

### Skapa en Windows-användare för WebSphere {#create-a-windows-user-for-websphere}

1. Logga in i Windows med ett administratörsanvändarkonto.
1. Välj **Start > Control Panel > Administrative Tools > Computer Management > Local Users and Groups**.
1. Högerklicka på Användare och välj **Ny användare**.
1. Skriv ett användarnamn och lösenord i rutorna och ange eventuell annan information som du vill ha i de övriga rutorna.
1. Avmarkera **Användaren måste ändra lösenordet vid nästa inloggning**, klicka **Skapa** och klicka sedan på **Stäng**.
1. Klicka **Användare**, högerklicka på den användare du just skapade och välj **Egenskaper**.
1. Klicka på **medlem i** och sedan klicka på **Lägg till**.
1. Skriv i rutan Ange de objektnamn du vill markera `Administrators`klickar du på Kontrollera namn för att se till att gruppnamnet är korrekt.
1. Klicka **OK** och sedan klicka **OK** igen.
1. Välj **Start > Kontrollpanelen > Administrationsverktyg > Lokal säkerhetsprincip > Lokala profiler**.
1. Klicka på Tilldelning av användarrättigheter, högerklicka sedan på Agera som en del av operativsystemet och välj Egenskaper.
1. Klicka **Lägg till användare eller grupp**.
1. Skriv namnet på den användare som du skapade i steg 4 i rutan Ange de objektnamn som ska väljas. Klicka sedan på **Kontrollera namn** för att säkerställa att namnet är korrekt, och klicka sedan på **OK**.
1. Klicka **OK** för att stänga funktionsmakrot som en del av dialogrutan för operativsystemsegenskaper.

### Konfigurera WebSphere för att använda den nyskapade användaren som administratör {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. Kontrollera att WebSphere körs.
1. I administrationskonsolen för WebSphere väljer du **Säkerhet > Global säkerhet**.
1. Under Administrativ säkerhet väljer du **Administrativa användarroller**.
1. Klicka på Lägg till och gör följande:

   1. Typ **&amp;ast;** i sökrutan och klicka på Sök.
   1. Klicka **Administratör** under roller.
   1. Lägg till den nyskapade användaren i Mappad till roll och mappa den till Administratör.

1. Klicka **OK** och spara ändringarna.
1. Starta om WebSphere-profilen.

## Aktivera administrativ säkerhet {#enable-administrative-security}

1. I administrationskonsolen för WebSphere väljer du **Säkerhet > Global säkerhet**.
1. Klicka **Guiden Konfigurera säkerhet**.
1. Säkerställ **Aktivera programsäkerhet** kryssrutan är aktiverad. Klicka på **Nästa**.
1. Välj **Federerade databaser** och klicka **Nästa**.
1. Ange de autentiseringsuppgifter som du vill ange och klicka på **Nästa**.
1. Klicka **Slutför**.
1. Starta om WebSphere-profilen.

   WebSphere börjar använda standardnyckelbehållaren och förtrostore.

## Aktivera SSL (anpassad nyckel och förvaltararkiv) {#enable-ssl-custom-key-and-truststore}

Du kan skapa förtroendelager och nyckelbehållare med hjälp av nyckelverktyget eller Admin Console. Se till att installationssökvägen för WebSphere inte innehåller parenteser så att nyckelmannen fungerar som den ska.

1. I administrationskonsolen för WebSphere väljer du **Säkerhet > SSL-certifikat och nyckelhantering**.
1. Klicka **Nyckelbehållare och certifikat** under Relaterade artiklar.
1. I **Användning av nyckelbehållare** listruta, kontrollera att **SSL-nyckelbehållare** är markerat. Klicka **Nytt**.
1. Ange ett logiskt namn och en beskrivning.
1. Ange sökvägen där du vill att nyckelbehållaren ska skapas. Om du redan har skapat en nyckelbehållare via ikeyman anger du sökvägen till nyckellagerfilen.
1. Ange och bekräfta lösenordet.
1. Välj typ av nyckelbehållare och klicka på **Använd**.
1. Spara huvudkonfigurationen.
1. Klicka **Personligt certifikat**.
1. Om du redan har skapat en nyckelbehållare med nyckelhanteraren visas ditt certifikat. Annars måste du lägga till ett nytt självsignerat certifikat genom att utföra följande steg:

   1. Välj **Skapa > själv signerat certifikat**.
   1. Ange lämpliga värden i certifikatformuläret. Se till att du behåller Alias och eget namn som fullständigt kvalificerat domännamn för datorn.
   1. Klicka på **Använd.**

1. Upprepa steg 2 till 10 för att skapa en truststore.

## Tillämpa anpassad nyckellagring och truststore på servern {#apply-custom-keystore-and-truststore-to-the-server}

1. I WebSphere Administrative Console väljer du **Säkerhets- > SSL-certifikat och nyckelhantering**.
1. Klicka på **Hantera konfiguration** av slutpunktssäkerhet. Den lokala topologikartan öppnas.
1. Under Inkommande väljer du direkt underordnad noder.
1. Under Relaterade objekt väljer du **SSL-konfigurationer**.
1. Välj **NodeDeafultSSLSetting**.
1. I listrutorna för förvaltararkivnamn och nyckelbehållarnamn väljer du det anpassade förvaltararkivet och nyckelbehållaren som du skapade.
1. Klicka **Använd**.
1. Spara huvudkonfigurationen.
1. Starta om WebSphere-profilen.

   Din profil kan nu köras med anpassade SSL-inställningar och ditt certifikat.

## Aktivera stöd för AEM {#enabling-support-for-aem-forms-natives}

1. I administrationskonsolen för WebSphere väljer du **Säkerhet > Global säkerhet**.
1. Expandera i avsnittet Autentisering **RMI/IP-säkerhet** och klicka **CSIv2 inkommande kommunikation**.
1. Se till att **SSL-stöd** väljs i listrutan Transport.
1. Starta om WebSphere-profilen.

## Konfigurera WebSphere för att konvertera URL:er som börjar med https {#configuring-websphere-to-convert-urls-that-begins-with-https}

Om du vill konvertera en URL som börjar med https lägger du till ett signerarcertifikat för den URL:en på WebSphere-servern.

**Skapa ett signerarcertifikat för en https-aktiverad webbplats**

1. Kontrollera att WebSphere körs.
1. I administrationskonsolen för WebSphere navigerar du till signerarcertifikat och klickar sedan på Säkerhet > SSL-certifikat och nyckelhantering > Nyckelarkiv och certifikat > NodeDefaultTrustStore > Signerarcertifikat.
1. Klicka på Hämta från port och utför följande åtgärder:

   * Skriv URL-adressen i rutan Värd. Skriv till exempel `www.paypal.com`.
   * I rutan Port skriver du `443`. Den här porten är standardport för SSL.
   * Skriv ett alias i rutan Alias.

1. Klicka på Hämta signerarinformation och kontrollera sedan att informationen har hämtats.
1. Klicka på Använd och sedan på Spara.

Konvertering från HTML till PDF från den webbplats vars certifikat läggs till fungerar nu från tjänsten Generate PDF.

>[!NOTE]
>
>Ett signerarcertifikat krävs för att ett program ska kunna ansluta till SSL-webbplatser inifrån WebSphere. Den används av Java Secure Socket Extensions (JSSE) för att validera certifikat som fjärrsidan av anslutningen skickar under en SSL-handskakning.

## Konfigurera dynamiska portar {#configuring-dynamic-ports}

IBM WebSphere tillåter inte flera anrop till ORB.init() när Global Security är aktiverat. Du kan läsa om permanent begränsning på https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704.

Utför följande steg för att ange att porten ska vara dynamisk och för att lösa problemet:

1. I administrationskonsolen för WebSphere väljer du **Servrar** > **Servertyper** > **WebSphere-programserver**.
1. Välj servern i avsnittet Inställningar.
1. I **Konfiguration** flik, under **Kommunikation** sektion, expandera **Portar** och klicka **Information**.
1. Klicka på följande portnamn och ändra **portnummer** till 0 och klicka på **OK**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## Konfigurera filen sling.properties {#configure-the-sling-properties-file}

1. Öppna `[aem-forms_root]`\crx-repository\launchpad\sling.properties fil för redigering.
1. Leta reda på `sling.bootdelegation.ibm` egenskap och lägg till `com.ibm.websphere.ssl.*`till värdefältet. Det uppdaterade fältet ser ut så här:

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. Spara filen och starta om servern.
