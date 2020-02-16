---
title: Ingå i Adobe Analytics och Adobe Target
seo-title: Ingå i Adobe Analytics och Adobe Target
description: Lär dig hur du väljer Adobe Analytics och Adobe Target.
seo-description: Lär dig hur du väljer Adobe Analytics och Adobe Target.
uuid: 9090a0f3-d373-4826-aa68-6aa82c0fbfbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: de466511-d82f-4ddb-8f6a-7ca9240fdeab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ingå i Adobe Analytics och Adobe Target{#opting-into-adobe-analytics-and-adobe-target}

AEM har en anmälningsprocedur som hjälper er att integrera med Adobe Analytics och Adobe Target. Detta är tillgängligt när du vill, som en förinläst uppgift som tilldelats administratörsanvändargruppen.

När du loggar in som administratör är den här uppgiften (**Konfigurera analys och anpassning**) tillgänglig i [Inkorgen](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks). Baserat på de autentiseringsuppgifter du anger hjälper det dig att konfigurera och integrera dessa tjänster.

Du har följande alternativ för att konfigurera integreringen:

* Konfigurera integreringen via uppgiften.

   Detta kan göras antingen direkt eller senare, och aktiviteten finns kvar i Inkorgen tills någon åtgärd har utförts. I båda fallen kan konfigurationen göras direkt i användargränssnittet eller med en fördefinierad `.properties` fil.

* Avanmäl dig från integreringen.

   Välj det här alternativet om du föredrar att [konfigurera integreringen](/help/sites-administering/marketing-cloud.md)manuellt. Se även [Integrera AEM med Adobe Target och Adobe Analytics med DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

* Konfigurera konfiguration och etablering med hjälp av ett skript.

## Konfigurera integreringen {#configuring-the-integration}

Anmäl dig till integrationen med:

* Analyser som gör det möjligt att använda deras funktioner för sidspårning och sidanalys.
* Rikta in er för att utnyttja deras personaliseringsfunktioner.

För båda alternativen måste du ange användarkontoinformationen och ange vilka sidor som ska spåras.

>[!NOTE]
>
>Du kan också ange Analytics- och Target-kontoinformation med hjälp av en egenskapsfil som läses när servern startas. Se [Ange kontoinformation med hjälp av en egenskapsfil](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file).

När du väljer att integrera utför AEM följande uppgifter:

* Skapar molnkonfigurationer som aktiverar anslutningen till Analytics och Target.
* Skapar ramverk som bestämmer vilka data som spåras.
* Konfigurerar webbsidorna så att de använder dessa tjänster.

>[!NOTE]
>
>AT.js är standardklientbiblioteket. Detta konfigureras under [målkonfigurationen](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration)för molntjänster.
>
>Adobe rekommenderar att du använder AT.js som klientbibliotek.

Så här avanmäler du dig från den förinlästa uppgiften:

1. I [Inkorgen väljer du och **öppnar** aktiviteten Konfigurera analys och anpassning](/help/sites-authoring/inbox.md#taking-action-on-an-item) .

   ![optin-01](assets/optin-01.png)

1. För analys:

   1. Ange användarkontoinformationen för Analytics och klicka sedan på motsvarande **Lägg till** -knapp.
   1. Autentiseringsuppgifterna är autentiserade.
   1. När Analytics-kontot autentiseras väljer du den Analytics-rapportsserie som ska användas. AEM hämtar dessa analysrapportsviter. Statusen uppdateras till **Tillagd**.

1. För mål:

   1. Ange användarkontoinformationen för Target och klicka sedan på motsvarande **Lägg till** -knapp.
   1. Autentiseringsuppgifterna är autentiserade. Statusen uppdateras till **Tillagd**.

1. Välj **Nästa**.
1. Välj de webbplatser som Analytics och/eller Target ska användas för.

1. Välj **Klar** för att slutföra.

   >[!CAUTION]
   >
   >När du har valt att konfigurera måste du publicera den eller de berörda platserna för att replikera dessa ändringar till publiceringsinstansen.

## Avanmäl dig från integreringen {#opting-out-of-the-integration}

Avanmäl dig från integreringen med Analytics och Target när du antingen:

* Vill inte integreras med dessa produkter.
* Använd det här alternativet om du vill konfigurera integreringarna manuellt.

   Mer information om hur du konfigurerar integreringarna manuellt finns i [Integrera med Adobe Analytics](/help/sites-administering/adobeanalytics.md) och [Integrera med Adobe Target](/help/sites-administering/target.md).

Om du vill avanmäla dig måste du slutföra den förinlästa uppgiften:

* I [Inkorgen väljer du och **slutför** uppgiften Konfigurera analys och anpassning](/help/sites-authoring/inbox.md#taking-action-on-an-item) .

## Ange kontoinformation med hjälp av en egenskapsfil {#providing-account-information-using-a-properties-file}

Installera en egenskapsfil som AEM läser när servern startas för att konfigurera kontoegenskaperna för integreringen med Analytics och Target. När du använder egenskapsfilen använder anmälningsguiden automatiskt egenskaperna från filen och molnkonfigurationen skapas därefter.

Egenskapsfilen är en textfil med namnet marketingcloud.properties som du sparar i arbetskatalogen som AEM-processen använder (vanligtvis samma katalog som JAR-filen). Filen innehåller följande egenskaper:

* analytics.server: URL:en till det Analytics-datacenter som du använder.
* analytics.company: Det företag som är associerat med ditt Analytics-användarkonto.
* analytics.username: Ditt användarnamn för Analytics.
* analytics.secrets: Den hemlighet som är kopplad till ditt användarnamn i Analytics.
* analytics.reportsuite: Namnet på analysrapportsviten som ska användas.
* target.clientcode: Klientkoden som är associerad med ditt Target-konto.
* target.email: E-postadressen som du använder för att autentisera ditt Target-konto.
* target.password: Lösenordet som är kopplat till din e-postadress.

Egenskaper och värden avgränsas med likhetstecken (=). Analysegenskaperna har prefixet `analytics`och Target-egenskaperna har prefixet `target`. Om du vill konfigurera en tjänst anger du värden för alla egenskaper för den tjänsten. Om du inte vill konfigurera en tjänst anger du inga värden för den tjänsten.

Följande exempelfil innehåller `.properties` egenskapsvärdena för att skapa en molnkonfiguration för Analytics:

```xml
analytics.server=https://test.omniture.com/login/
analytics.company=MyCompany
analytics.username=sbroders
analytics.secret=12345678
analytics.reportsuite=myreportsuite
target.clientcode=
target.email=
target.password=
```

I proceduren nedan beskrivs hur du väljer att gå med i integreringen med hjälp av egenskapsfilen.

1. Skapa `marketingcloud.properties` filen i arbetskatalogen som AEM-processen använder (författarinstans).

   >[!NOTE]
   >
   >Arbetskatalogen är vanligtvis den katalog som innehåller burken eller `license.properties` filen.
   >
   >Men den kan också definieras som en absolut sökväg av egenskapen system:
   >
   >`mac.provisioning.file.container`

1. Lägg till egenskapsvärden enligt dina Analytics- och/eller Target-konton.
1. Starta eller starta om servern och logga sedan in med ett administratörskonto.
1. Öppna aktiviteten Konfigurera analys och målanpassning så som beskrivs i [Konfigurera integreringen](/help/sites-administering/opt-in.md#configuring-the-integration). I stället för att begära din kontoinformation använder guiden värdena från `.properties` filen.

   Välj **Lägg till** för rätt tjänst och fortsätt sedan med guiden.

   ![optin-02](assets/optin-02.png)

## Om molnkonfigurationer {#about-the-cloud-configurations}

När du konfigurerar integreringen med Analytics och Target skapar AEM automatiskt de molnkonfigurationer och ramverk som krävs. Molnkonfigurationen för Analytics kallas till exempel för Provisioned Analytics-konto.

Du behöver inte ändra molnkonfigurationerna. Du kan dock konfigurera ramverken efter behov. (Se [Mappa komponentdata med Adobe Analytics-egenskaper](/help/sites-administering/adobeanalytics-mapping.md) och [Lägg till ett Target Framework](/help/sites-administering/target.md).)

>[!NOTE]
>
>Som standard aktiveras korrekt målanpassning när du väljer att gå med i konfigurationsguiden för Adobe Target.
>
>Korrekt målinriktning innebär att molntjänstkonfigurationen väntar på att kontexten ska läsas in innan innehållet läses in. Därför kan en korrekt målinriktning i fråga om prestanda skapa en fördröjning på några millisekunder innan innehållet läses in.
>
>Korrekt målinriktning är alltid aktiverat på författarinstansen. På publiceringsinstansen kan du dock välja att inaktivera korrekt målinriktning globalt genom att avmarkera kryssrutan bredvid Exakt målanpassning i molntjänstkonfigurationen (**http://localhost:4502/etc/cloudservices.html**). Du kan även aktivera och inaktivera exakt målinriktning för enskilda komponenter, oavsett vilken inställning du har i molntjänstkonfigurationen.
>
>Om du ***redan*** har skapat målkomponenter och ändrar den här inställningen påverkar ändringarna inte dessa komponenter. Du måste göra ändringar i den komponenten direkt.

>[!CAUTION]
>
>När du väljer att använda Analytics-konfigurationen och ett specifikt `reportsuite` väljs, begränsas ramverket till publiceringskörningsläget. Det innebär att spårning bara fungerar på publiceringsinstansen.
>
>Om det behövs spårning för en redigeringsinstans bör även värdet ändras till `all`.

## Konfigurera inställningar och etablering via skript {#configuring-the-setup-and-provisioning-via-script}

Som administratör kanske du vill aktivera konfiguration och etablering med ett skript i stället för att stega igenom guiden manuellt. Du kan göra det genom att:

* Skicka en POST-begäran till **/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json** med de parametrar som krävs.

Vilka parametrar du skickar beror på följande:

* Om du vill använda filen **marketingcloud.properties** ifylld med alla nödvändiga autentiseringsuppgifter måste du skicka följande parametrar:

   * `automaticProvisioning`= `true`
   * `servicename`= `analytics|target`
   * `path`=sökväg till en AEM-sida för att bifoga de molntjänster som skapas
   En curl-begäran som skapar både Analytics- och Target-konfigurationer och bifogar dem till sidan we.retail skulle till exempel vara:

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

* Om du inte vill använda filen **marketingcloud.properties** måste du skicka inloggningsuppgifterna samt parametrarna; till exempel:

   * automaticProvisioning= `true`
   * servicename= `analytics|target`
   * path=path to an AEM page to attach the created cloud services configs; flera banor kan definieras
   * analytics.server= `https://servername`
   * analytics.company= `Name of company`
   * analytics.username= `me`
   * analytics.secrets= `secret`
   * analytics.reportsuite= `we-retail`
   * target.clientcode= `mycompany`
   * target.email= `me@adobe.com`
   * target.password= `password`
   I det här fallet skulle den begäran som skapar både Analytics- och Target-konfigurationer och bifogar dem till webbsidan vara:

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

