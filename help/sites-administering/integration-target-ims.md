---
title: Integrering med Adobe Target med IMS
description: Läs om hur du integrerar AEM med Adobe Target med IMS
exl-id: 8ddd86d5-a5a9-4907-b07b-b6552d7afdc8
source-git-commit: 2f5f6a94a20feb2813b6da1b71e22f8675529ea5
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 0%

---


# Integrering med Adobe Target med IMS{#integration-with-adobe-target-using-ims}

Integreringen av AEM med Adobe Target via Target Standard API kräver att Adobe IMS (Identity Management System) konfigureras med Adobe Developer Console.

>[!NOTE]
>
>Stöd för Adobe Target Standard API är nytt i AEM 6.5. Målstandard-API:t använder IMS-autentisering.
>
>Det finns fortfarande stöd för att använda Adobe Target Classic API i AEM för bakåtkompatibilitet. The [Target Classic API använder inloggningsuppgifter](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).
>
>API-valet styrs av den autentiseringsmetod som används för AEM/Target-integrering.
>Se även [Klient-ID och klientkod](#tenant-client) -avsnitt.

## Förutsättningar {#prerequisites}

Innan du börjar med den här proceduren:

* [Stöd för Adobe](https://helpx.adobe.com/se/contact/enterprise-support.ec.html) måste tillhandahålla ditt konto för:

   * Adobe Console
   * Adobe Developer Console
   * Adobe Target och
   * Adobe IMS (Identity Management System)

* Din organisations systemadministratör bör använda Admin Console för att lägga till de utvecklare som behövs i organisationen till de relevanta produktprofilerna.

   * Detta ger specifika utvecklare behörighet att aktivera integreringar i Adobe Developer Console.
   * Mer information finns i [Hantera utvecklare](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Konfigurera en IMS-konfiguration - Generera en offentlig nyckel {#configuring-an-ims-configuration-generating-a-public-key}

Det första steget i konfigurationen är att skapa en IMS-konfiguration i AEM och generera den offentliga nyckeln.

1. Öppna AEM **verktyg** -menyn.
1. I **Säkerhet** avsnittsmarkera **Adobe IMS-konfigurationer**.
1. Välj **Skapa** för att öppna **Adobe IMS Technical Account Configuration**.
1. Använda listrutan under **Molnkonfiguration**, markera **Adobe Target**.
1. Aktivera **Skapa nytt certifikat** och ange ett nytt alias.
1. Bekräfta med **Skapa certifikat**.

   ![Guiden Konfigurera Adobe IMS Technical Account](assets/integrate-target-io-01.png)

1. Välj **Hämta** (eller **Hämta offentlig nyckel**) för att hämta filen till den lokala hårddisken, så att den är klar att användas när [konfigurera IMS för Adobe Target-integrering med AEM](#configuring-ims-for-adobe-target-integration-with-aem).

   >[!CAUTION]
   >
   >Låt konfigurationen vara öppen, den behövs igen när [Slutför IMS-konfigurationen i AEM](#completing-the-ims-configuration-in-aem).

   ![Informationsmeddelande om att lägga till certifikat på Adobe I/O](assets/integrate-target-io-02.png)

## Konfigurera IMS för Adobe Target-integrering med AEM {#configuring-ims-for-adobe-target-integration-with-aem}

Med Adobe Developer Console måste du skapa ett projekt (integration) med Adobe Target som AEM ska använda och sedan tilldela de behörigheter som krävs.

### Skapa projektet {#creating-the-project}

Öppna Adobe Developer Console och skapa ett projekt med Adobe Target som AEM ska använda:

1. Öppna Adobe Developer Console for Projects:

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. Alla projekt du har visas. Välj **Skapa nytt projekt** - platsen och användningen beror på:

   * Om du inte har något projekt än **Skapa nytt projekt** kommer att vara i mitten, nederst.
     ![Skapa nytt projekt - första projektet](assets/integration-target-io-02.png)
   * Om du redan har befintliga projekt listas dessa och **Skapa nytt projekt** kommer att vara överst till höger.
     ![Skapa nytt projekt - flera projekt](assets/integration-target-io-03.png)


1. Välj **Lägg till i projekt** följt av **API**:

   ![Adobe Developer Console](assets/integration-target-io-10.png)

1. Välj **Adobe Target** sedan **Nästa**:

   >[!NOTE]
   >
   >Om du prenumererar på Adobe Target, men inte ser det i listan, bör du kontrollera [Förutsättningar](#prerequisites).

   ![Klicka på nästa](assets/integration-target-io-12.png)

1. **Överför din offentliga nyckel** och när det är klart fortsätter du med **Nästa**:

   ![Lägga till integreringar med Developer Console](assets/integration-target-io-13.png)

1. Granska inloggningsuppgifterna och fortsätt med **Nästa**:

   ![Skapa ett nytt projekt](assets/integration-target-io-15.png)

1. Välj önskade produktprofiler och fortsätt med **Spara konfigurerat API**:

   >[!NOTE]
   >
   >Vilka produktprofiler som visas beror på om du har:
   >
   >* Adobe Target Standard - endast **Standardarbetsyta** är tillgänglig
   >* Adobe Target Premium - alla tillgängliga arbetsytor visas i listan enligt nedan

   ![Välja ett API att lägga till](assets/integration-target-io-16.png)

1. Skapandet bekräftas.

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### Tilldela behörigheter till integreringen {#assigning-privileges-to-the-integration}

Du måste nu tilldela nödvändig behörighet till integreringen:

1. Öppna Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Navigera till **Produkter** (övre verktygsfältet) och sedan välja **Adobe Target - &lt;*din-tenant-id*>** (från den vänstra panelen).
1. Välj **Produktprofiler** och sedan den arbetsyta du behöver i den lista som visas. Exempel: Standardarbetsyta.
1. Välj **API-autentiseringsuppgifter** och sedan den integreringskonfiguration som krävs.
1. Välj **Redigerare** som **Produktroll**; i stället för **Observer**.

## Information lagrad för Adobe Developer Console Integration Project {#details-stored-for-the-ims-integration-project}

I Adobe Developer Console - Projekt kan du se en lista över alla dina integreringsprojekt:

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

Välj **Visa** (till höger om en viss projektpost) om du vill visa mer information om konfigurationen. Bland dessa finns:

* Projektöversikt
* Insikter
* Autentiseringsuppgifter
   * Tjänstkonto (JWT)
      * Information om autentiseringsuppgifter
      * Generera JWT
* APIS
   * Exempel: Adobe Target

Vissa av dessa behöver du för att slutföra integreringen av Adobe Target i AEM baserat på IMS.

## Slutför IMS-konfigurationen i AEM {#completing-the-ims-configuration-in-aem}

Om du går tillbaka till AEM kan du slutföra IMS-konfigurationen genom att lägga till obligatoriska värden från Adobe Developer Console-integreringen för Target:

1. Återgå till [IMS-konfiguration öppnas i AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Välj **Nästa**.

1. Här kan du använda [information från projektkonfigurationen i Adobe Developer Console](#details-stored-for-the-ims-integration-project):

   * **Titel**: Din text.
   * **Auktoriseringsserver**: Kopiera/klistra in detta från `aud` rad i **Nyttolast** avsnitt nedan, t.ex. `https://ims-na1.adobelogin.com` i exemplet nedan
   * **API-nyckel**: Kopiera detta från [Översikt](#details-stored-for-the-ims-integration-project) section
   * **Klienthemlighet**: Generera detta i [Översikt](#details-stored-for-the-ims-integration-project) och kopiera
   * **Nyttolast**: Kopiera detta från [Generera JWT](#details-stored-for-the-ims-integration-project) section

   ![Konfiguration av tekniskt konto](assets/integrate-target-io-10.png)

1. Bekräfta med **Skapa**.

1. Din Adobe Target-konfiguration visas i AEM.

   ![Adobe IMS Technical Account Configuration](assets/integrate-target-io-11.png)

## Bekräfta IMS-konfigurationen {#confirming-the-ims-configuration}

Så här bekräftar du att konfigurationen fungerar som förväntat:

1. Öppna:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Till exempel:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`

1. Välj din konfiguration.
1. Välj **Kontrollera hälsa** i verktygsfältet, följt av **Kontrollera**.

   ![Adobe IMS-konfigurationer](assets/integrate-target-io-12.png)

1. Om det lyckas visas meddelandet:

   ![Kontrollera en konfiguration](assets/integrate-target-io-13.png)

## Konfigurera Adobe Target-Cloud Servicen {#configuring-the-adobe-target-cloud-service}

Det går nu att referera till konfigurationen för en Cloud Service som använder Target Standard API:

1. Öppna **verktyg** -menyn. Sedan, i **Cloud Services** avsnitt, markera **Äldre Cloud Services**.
1. Bläddra nedåt till **Adobe Target** och markera **Konfigurera nu**.

   The **Skapa konfiguration** öppnas.

1. Ange **Titel** och, om du vill, en **Namn** (Om inget anges genereras detta från titeln).

   Du kan också välja önskad mall (om fler än en är tillgänglig).

1. Bekräfta med **Skapa**.

   The **Redigera komponent** öppnas.

1. Ange informationen i dialogrutan **Adobe Target-inställningar** tab:

   * **Autentisering**: IMS

   * **Klient-ID**: Adobe IMS-klientens ID. Se även [Klient-ID och klientkod](#tenant-client) -avsnitt.

     >[!NOTE]
     >
     >För IMS måste det här värdet hämtas från Target. Du kan logga in på Target och extrahera klient-ID:t från URL:en.
     >
     >Om URL:en till exempel är:
     >
     >`https://experience.adobe.com/#/@yourtenantid/target/activities`
     >
     >Då använder du `yourtenantid`.

   * **Klientkod**: Se [Klient-ID och klientkod](#tenant-client) -avsnitt.

   * **IMS-konfiguration**: välj namnet på IMS-konfigurationen

   * **API-typ**: REST

   * **A4T Analytics Cloud-konfiguration**: Välj den Analytics-molnkonfiguration som används för målaktivitetsmål och -mått. Du behöver detta om du använder Adobe Analytics som rapportkälla när du skapar innehåll för målgruppsanpassning. Om du inte ser din molnkonfiguration kan du läsa mer i [Konfigurera A4T Analytics Cloud-konfiguration](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).

   * **Använd exakt målinriktning**: Som standard är den här kryssrutan markerad. Om du väljer det här alternativet väntar molntjänstkonfigurationen på att kontexten ska läsas in innan innehållet läses in. Se följande.

   * **Synkronisera segment från Adobe Target**: Välj det här alternativet om du vill hämta segment som har definierats i Target för att använda dem i AEM. Du måste välja det här alternativet när API-typegenskapen är REST, eftersom infogade segment inte stöds och du alltid måste använda segment från Target. (Observera att den AEM termen segment motsvarar målgruppen.)

   * **Klientbibliotek**: Välj om du vill ha klientbiblioteket AT.js eller mbox.js (utgått).

   * **Använd Tag Management System för att leverera klientbibliotek**: Använd DTM (utgått), Adobe Launch eller något annat tagghanteringssystem.

   * **Anpassad AT.js**: Lämna tomt om du har markerat rutan Tag Management eller om du vill använda AT.js som standard. Du kan även överföra dina anpassade AT.js. Visas bara om du har valt AT.js.

   >[!NOTE]
   >
   >[Konfiguration av en Cloud Service som ska använda API:t för klassiska mål](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) har tagits bort (använder fliken Adobe Recommendations-inställningar).

1. Klicka **Anslut till mål** för att initiera anslutningen till Adobe Target.

   Om anslutningen lyckas visas meddelandet **Anslutningen lyckades** visas.

1. Välj **OK** i meddelandet, följt av **OK** i dialogrutan för att bekräfta konfigurationen.

1. Du kan nu fortsätta till [Lägga till ett målramverk](/help/sites-administering/target-configuring.md#adding-a-target-framework) för att konfigurera ContextHub- eller ClientContext-parametrar som ska skickas till Target. Observera att detta kanske inte behövs för att exportera AEM Experience Fragments till Target.

### Klient-ID och klientkod {#tenant-client}

Med [Adobe Experience Manager 6.5.8.0](/help/release-notes/release-notes.md), hade fältet Klientkod lagts till i fönstret för målkonfigurationen.

Tänk på följande när du konfigurerar fälten för klient-ID och klientkod:

1. För de flesta kunder är innehavar-ID och klientkod samma. Det innebär att båda fälten innehåller samma information och är identiska. Se till att du anger klient-ID i båda fälten.
2. För äldre syften kan du även ange olika värden i fälten Klient-ID och Klientkod.

I båda fallen ska du tänka på följande:

* Som standard kopieras även klientkoden (om den läggs till först) automatiskt till fältet Klient-ID.
* Du kan ändra standardinställningen för klient-ID.
* Därför kommer serverdelsanropen till Target att baseras på klientens ID och klientsidans anrop till Target kommer att baseras på klientkoden.

Som tidigare nämnts är det första fallet det vanligaste för AEM 6.5. Oavsett hur du väljer **båda** fälten innehåller rätt information beroende på dina behov.

>[!NOTE]
>
>Om du vill ändra en befintlig målkonfiguration:
>
>1. Ange klientorganisations-ID:t igen.
>2. Återanslut till mål.
>3. Spara konfigurationen.
