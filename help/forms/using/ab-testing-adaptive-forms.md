---
title: Skapa och hantera A/B-tester för adaptiva formulär
seo-title: Skapa och hantera A/B-tester för adaptiva formulär
description: AEM Forms kan integreras med Adobe Target för att köra A/B-tester för adaptiva formulär för att förbättra kundupplevelsen och konverteringsgraden.
seo-description: AEM Forms kan integreras med Adobe Target för att köra A/B-tester för adaptiva formulär för att förbättra kundupplevelsen och konverteringsgraden.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
translation-type: tm+mt
source-git-commit: 3eaace94bc0499aaebfcd389d4dc97b97c7d9160

---


# Skapa och hantera A/B-tester för adaptiva formulär{#create-and-manage-a-b-test-for-adaptive-forms}

## Översikt {#overview-br}

Kunderna överger troligtvis ett formulär om upplevelsen inte är engagerande. Även om det är frustrerande för kunderna kan det också öka supportvolymen och kostnaderna för organisationen. Det är både viktigt och utmanande att identifiera och tillhandahålla rätt kundupplevelse som ökar konverteringsgraden. Adobe Experience Manager Forms innehåller nyckeln till det här problemet.

AEM Forms kan integreras med Adobe Target, en Adobe Marketing Cloud-lösning, för att leverera personaliserade och engagerande kundupplevelser i flera digitala kanaler. En av de viktigaste funktionerna i Target är A/B-testning som gör att ni snabbt kan ställa in samtidiga A/B-tester, presentera relevant innehåll för målanvändare och identifiera upplevelsen som ökar konverteringsgraden.

Med AEM Forms kan du konfigurera och köra A/B-tester på adaptiva formulär i realtid. Den har också färdiga och anpassningsbara rapportfunktioner som visualiserar formulärupplevelserna i realtid och identifierar den som maximerar användarengagemanget och konverteringsgraden.

## Konfigurera och integrera Target i AEM-formulär {#set-up-and-integrate-target-in-aem-forms}

Innan du börjar skapa och analysera A/B-tester för adaptiva formulär måste du konfigurera målservern och integrera den i AEM Forms.

### Konfigurera mål {#set-up-target}

Om du vill integrera AEM med Target måste du ha ett giltigt Adobe Target-konto. När du registrerar dig hos Adobe Target får du en klientkod. Du behöver klientkoden, e-postadressen som är kopplad till Target-kontot och lösenordet för att kunna ansluta AEM till Target.

Klientkoden identifierar Adobe Target-kundkontot och används som en underdomän i URL:en när Adobe Target-servern anropas. Innan du fortsätter bör du kontrollera att du har behörighet att logga in på [https://testandtarget.omniture.com/](https://testandtarget.omniture.com/).

### Integrera mål i AEM-formulär {#integrate-target-in-aem-forms}

Utför följande steg för att integrera en målserver som körs med AEM Forms:

1. På AEM-servern går du till https://&lt;*värdnamn*>:&lt;*port*>/libs/cq/core/content/tools/cloudservices.html.

1. Klicka på **Visa konfigurationer** i delen **Adobe Target** och sedan på ikonen **+** för att lägga till en ny konfiguration.
Om du konfigurerar målet för första gången klickar du på **Konfigurera nu.**

1. Ange en **titel** och eventuellt ett **namn** för konfigurationen i dialogrutan Skapa konfiguration.

1. Klicka på **Skapa**. Dialogrutan Redigera komponent öppnas.
1. Ange information om ditt Target-konto, till exempel klientkod, e-post och lösenord.
1. Välj **Återställ** i listrutan API-typ.

1. Klicka på **Anslut till Adobe Target** för att initiera anslutningen till Target. Om anslutningen lyckas visas meddelandet Anslutningen lyckades. Klicka på **OK** i meddelandet och **OK** i dialogrutan. Målkontot är konfigurerat.

1. Skapa ett målramverk enligt beskrivningen i [Lägg till ett ramverk](/help/sites-administering/target.md).

1. Gå till https://&lt;*värdnamn*>:&lt;*port*>/system/console/configMgr.

1. Klicka på **AEM Forms Target Configuration**.
1. Välj ett **målramverk**.
1. I fältet **Mål-URL** anger du alla URL:er där A/B-tester ska köras. Exempel: https://&lt;*värdnamn*>:&lt;*port*>/ för AEM Forms-server på OSGi eller https://&lt;*värdnamn*>:&lt;*port*>/lc/ för AEM Forms-server på JEE.
Tänk på att du vill konfigurera en mål-URL för en publiceringsinstans och att dina kunder kan komma åt den via värdnamnet eller IP-adressen, så måste du konfigurera båda som mål-URL:er - med värdnamnet och IP-adressen. Om du bara konfigurerar en av URL:erna kommer ditt A/B-test inte att köras för kunder som kommer från den andra URL:en. Klicka **+** om du vill ange flera URL:er.

1. Click **Save**.

Målservern är integrerad med AEM Forms. Du kan nu aktivera A/B-testning om du har en fullständig licens för att använda Adobe Target.

Om du har en fullständig licens för att använda Adobe Target ska du starta servern med följande parametrar när du har integrerat Target med AEM Forms:

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

Om AEM-instansen körs på JBoss, startades som en tjänst från körningsnyckeln, i `jboss\bin\standalone.conf.bat` filen, lägger du till parametern -Dabtesting.enabled=true i följande post:

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

Förutom jboss-servern kan du lägga till argumentet -Dabtesting.enabled=true jvm i serverns startskript för alla programservrar. Nu kan du skapa och köra A/B-tester för adaptiva formulär.

>[!NOTE]
>
>Om du uppdaterar de konfigurerade mål-URL:erna senare måste du uppdatera alla A/B-tester som körs så att de pekar på de aktuella URL:erna. Mer information om hur du uppdaterar A/B-tester finns i [Uppdatera A/B-test](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).


## Skapa målgrupper i AEM {#create-audiences-within-aem}

Med AEM kan du skapa en målgrupp och använda den för ett A/B-test. Den målgrupp du skapar i AEM finns i AEM Forms. Utför följande steg för att skapa målgrupper i AEM:

1. I redigeringsinstansen trycker du på **Adobe Experience Manager** > **Personalisering** > **Publiker**.

1. På sidan Publiker trycker du på **Create Audience > Create Target Audience**.
1. I dialogrutan Adobe Target Configuration väljer du en målkonfiguration och klickar på **OK**.
1. Skapa regler på sidan Skapa ny publik. Med regler kan ni kategorisera målgruppen. Du vill till exempel kategorisera målgrupper baserat på operativsystem. Din målgrupp A kommer från Windows, och målgrupp B kommer från Linux.

   1. Om du vill kategorisera målgruppen baserat på Windows väljer du **OS** -attributtyp i regel 1. Välj **Windows i listrutan När.**

   1. Om du vill kategorisera målgruppen baserat på Linux väljer du **OS** -attributtyp i regel 2. I listrutan **När** väljer du **Linux** och klickar på **Nästa**.

1. Ange ett namn för målgruppen och klicka på **Spara**.

Du kan välja målgrupp när du konfigurerar A/B-testning för ett formulär, vilket visas nedan.

## Skapa A/B-test {#create-a-b-test}

Utför följande steg för att skapa ett A/B-test för ett anpassat formulär.

1. Gå till **Formulär och dokument** på https://&lt;*värdnamn*>:&lt;*port*>/aem/forms.html/content/dam/formSanddocuments.

1. Navigera till mappen som innehåller det adaptiva formuläret.
1. Klicka på **markeringsverktyget** i verktygsfältet och välj det anpassade formuläret.
1. Klicka på **Mer** i verktygsfältet och välj **Konfigurera A/B-testning**. Sidan Konfigurera A/B-testning öppnas.

[ Konfigurationssida ![för A/B-tester för adaptiva formulär](assets/ab-test-configure.png)](assets/ab-test-configure-1.png)

1. Ange ett **aktivitetsnamn** för A/B-testet.

1. I listrutan Målgrupp väljer du en målgrupp till vilken du vill leverera olika upplevelser av formuläret. Exempel: **Besökare som använder Chrome**. Målgruppslistan fylls i från den konfigurerade målservern.

1. I fälten **Experience Distribution** för upplevelserna A och B anger du fördelningen, uttryckt i procent, för att avgöra hur upplevelserna ska fördelas mellan den totala publiken. Om du till exempel anger 40, 60 för upplevelserna A respektive B kommer upplevelsen A att visas för 40 % av publiken och de återstående 60 % kommer att se upplevelsen B.
1. Klicka på **Konfigurera**. En dialogruta visas som bekräftar att A/B-testet har skapats.
1. Klicka på **Redigera upplevelse B** för att öppna det adaptiva formuläret i redigeringsläget. Ändra formuläret för att skapa en annan upplevelse än standardupplevelsen A. Möjliga variationer som tillåts i Experience B är förändringar i:

   * CSS eller format
   * Ordning på fält i olika paneler eller på samma panel
   * Panellayout
   * Panelrubriker
   * Beskrivning, etikett och hjälptext för ett fält
   * Skript som inte påverkar eller bryter skicka-flödet
   * Valideringar (både klient- och serversidor)
   * Tema för upplevelse B. (Du kan välja ett alternativt tema för upplevelse B)

1. Gå till gränssnittet för formulär och dokument, markera det adaptiva formuläret, klicka på **Mer** och välj **Starta A/B-testning**.

A/B-testet körs nu och den angivna målgruppen kommer att få slumpvis betjänade upplevelser baserat på den angivna fördelningen.

## Uppdatera A/B-test {#update-a-b-test}

Du kan uppdatera målgruppen och upplevelsedistributionen för ett A/B-test som körs. Så här gör du:

1. Navigera till mappen som innehåller det adaptiva formuläret som A/B-testet körs på i gränssnittet för Formulär och dokument.
1. Markera det adaptiva formuläret.
1. Klicka på **Mer** och välj sedan **Redigera A/B-testning**. Sidan Uppdatera A/B-testning öppnas.

1. Uppdatera målgrupps- och upplevelsedistributionen efter behov.
1. Klicka på **Uppdatera**.

## Visa och analysera A/B-testrapport {#view-and-analyze-a-b-test-report}

När du har tillåtit A/B-testet att köras under den önskade perioden kan du generera en rapport och kontrollera vilken upplevelse som har resulterat i bättre konvertering. Du kan deklarera en vinnares bättre prestation eller välja att köra ett annat A/B-test. Gör så här:

1. Markera det adaptiva formuläret, klicka på **Mer** och sedan på **A/B-testrapport**. Rapporten visas.

[ Provningsrapport ![A/B](assets/ab-test-report-2.png)](assets/ab-test-report-3.png)

1. Analysera rapporten och se om ni har tillräckligt många datapunkter för att kunna deklarera en av de mest framgångsrika upplevelserna som en vinnare. Du kan välja att fortsätta med samma A/B-test längre eller deklarera en vinnare och avsluta A/B-testet.
1. Om du vill deklarera en vinnare och avsluta A/B-testet klickar du på knappen **End A/B test** på kontrollpanelen för rapporter. En dialogruta uppmanar er att förklara en av de två upplevelserna som vinnare. Välj en vinnare och bekräfta att du vill avsluta A/B-testet.
Du kan också först deklarera en vinnare genom att klicka på knappen **Deklarera vinnare** för respektive upplevelse. Du uppmanas att bekräfta vinnaren. Klicka på **Ja** för att avsluta A/B-testet.

Om ni valde upplevelsen A som vinnare kommer A/B-testet att få ett slut, och om ni fortsätter kommer bara Experience A att erbjudas alla målgrupper.
