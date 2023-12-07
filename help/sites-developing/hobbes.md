---
title: Testa användargränssnittet
description: AEM tillhandahåller ett ramverk för automatisering av tester för ditt AEM användargränssnitt
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
docset: aem65
exl-id: 2d28cee6-31b0-4288-bad3-4d2ecad7b626
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 2%

---

# Testa användargränssnittet{#testing-your-ui}

>[!NOTE]
>
>Från och med AEM 6.5 är testningsramverket hobbes.js UI föråldrat. Adobe planerar inte att göra ytterligare förbättringar av det och rekommenderar sina kunder att använda Selenium Automation.
>
>Se [Föråldrade och borttagna funktioner](/help/release-notes/deprecated-removed-features.md).

AEM tillhandahåller ett ramverk för automatisering av tester för ditt AEM användargränssnitt. Med hjälp av ramverket kan du skriva och köra gränssnittstester direkt i en webbläsare. Ramverket innehåller ett JavaScript-API för att skapa tester.

I AEM testramverk används Hobbes.js, ett testbibliotek som är skrivet i JavaScript. Hobbes.js-ramverket utvecklades för testning av AEM som en del av utvecklingsprocessen. Ramverket är nu tillgängligt för allmän användning för testning av dina AEM program.

>[!NOTE]
>
>Se Hobbes.js [dokumentation](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html) om du vill ha fullständig information om API:t.

## Testernas struktur {#structure-of-tests}

När du använder automatiska tester i AEM är följande termer viktiga att förstå:

| Åtgärd | An **Åtgärd** är en specifik aktivitet på en webbsida, till exempel genom att klicka på en länk eller en knapp. |
|---|---|
| Testfall | A **Testfall** är en specifik situation som kan bestå av en eller flera **Åtgärder**. |
| Test Suite | A **Test Suite** är en grupp av relaterade **Testfall** som tillsammans testar ett visst användningsfall. |

## Kör tester {#executing-tests}

### Visa testsviter {#viewing-test-suites}

Öppna testkonsolen för att se de registrerade testsviterna. Testpanelen innehåller en lista med testsviter och deras testfall.

Navigera till verktygskonsolen via **Global Navigation > Tools > Operations > Testing**.

![chlimage_1-63](assets/chlimage_1-63.png)

När du öppnar konsolen visas testsviterna till vänster tillsammans med ett alternativ för att köra alla sekventiellt. Utrymmet till höger som visas med en schackmönstrad bakgrund är en platshållare för hur sidinnehållet visas när testerna körs.

![chlimage_1-64](assets/chlimage_1-64.png)

### Köra en testsvit {#running-a-single-test-suite}

Testsviter kan köras individuellt. När du kör en testsvit ändras sidan allt eftersom testärenden och deras åtgärder körs och resultaten visas när testet har slutförts. Ikoner anger resultatet.

En bockmarkeringsikon anger att testet har slutförts:

![Kryssmarkeringsikon.](do-not-localize/chlimage_1-2.png)

En X-ikon anger att testet misslyckades:

![Ikonen för testet misslyckades, vilket indikeras av ett X inuti en cirkel.](do-not-localize/chlimage_1-3.png)

Så här kör du en testsvit:

1. Klicka på namnet på det testfall som du vill köra på panelen Testa för att visa information om åtgärderna.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Klicka **Kör test**.

   ![En bild av knappen Kör test, som indikeras av en högerriktad pekare inuti en cirkel.](do-not-localize/chlimage_1-4.png)

1. Platshållaren ersätts med sidinnehåll när testet utförs.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Granska resultatet av testfallet genom att trycka på eller klicka på beskrivningen för att öppna **Resultat** -panelen. Tryck eller klicka på namnet på testfallet i dialogrutan **Resultat** på panelen visas all information.

   ![chlimage_1-67](assets/chlimage_1-67.png)

### Köra flera tester {#running-multiple-tests}

Testsviter körs sekventiellt i den ordning som de visas i konsolen. Du kan fördjupa dig i ett test för att se de detaljerade resultaten.

![chlimage_1-68](assets/chlimage_1-68.png)

1. På testpanelen klickar du på **Kör alla tester** eller **Kör tester** under namnet på testsviten som du vill köra.

   ![En bild av knappen Kör alla tester och knappen Kör test, som indikeras av en högerriktad pekare inuti en cirkel.](do-not-localize/chlimage_1-5.png)

1. Om du vill visa resultatet av varje testfall klickar du på titeln på testfallet. Klicka på namnet på testet i **Resultat** på panelen visas all information.

   ![chlimage_1-69](assets/chlimage_1-69.png)

## Skapa och använda en enkel testprogramsvit {#creating-and-using-a-simple-test-suite}

I proceduren nedan beskrivs hur du skapar och kör en Test Suite med [Innehåll för webb.butik](/help/sites-developing/we-retail.md), men du kan enkelt ändra testet så att det använder en annan webbsida.

Mer information om hur du skapar egna testsviter finns i [Hobbes.js API-dokumentation](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html).

1. Öppna CRXDE Lite. ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. Högerklicka på `/etc/clientlibs` mapp och klicka på **Skapa > Skapa mapp**. Typ `myTests` för namnet och klicka på **OK**.
1. Högerklicka på `/etc/clientlibs/myTests` mapp och klicka på **Skapa > Skapa nod**. Använd följande egenskapsvärden och klicka sedan på **OK**:

   * Namn: `myFirstTest`
   * Typ: `cq:ClientLibraryFolder`

1. Lägg till följande egenskaper i noden myFirstTest:

   | Namn | Typ | Värde |
   |---|---|---|
   | `categories` | Sträng[] | `granite.testing.hobbes.tests` |
   | `dependencies` | Sträng[] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**Endast AEM Forms**
   >
   >
   >Om du vill testa adaptiva formulär lägger du till följande värden i kategorierna och beroenden. Till exempel:
   >
   >
   >**kategorier**: `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**beroenden**: `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. Klicka **Spara alla**.
1. Högerklicka på `myFirstTest` och klicka på **Skapa > Skapa fil**. Namnge filen `js.txt` och klicka **OK**.
1. I `js.txt` anger du följande text:

   ```
   #base=.
   myTestSuite.js
   ```

1. Klicka **Spara alla** och stäng sedan `js.txt` -fil.
1. Högerklicka på `myFirstTest` och klicka på **Skapa > Skapa fil**. Namnge filen `myTestSuite.js` och klicka **OK**.
1. Kopiera följande kod till `myTestSuite.js` och sedan spara filen:

   ```
   new hobs.TestSuite("Experience Content Test Suite", {path:"/etc/clientlibs/myTests/myFirstTest/myTestSuite.js"})
      .addTestCase(new hobs.TestCase("Navigate to Experience Content")
         .navigateTo("/content/we-retail/us/en/experience/arctic-surfing-in-lofoten.html")
      )
      .addTestCase(new hobs.TestCase("Hover Over Topnav")
         .mouseover("li.visible-xs")
      )
      .addTestCase(new hobs.TestCase("Click Topnav Link")
         .click("li.active a")
   );
   ```

1. Navigera till **Testning** för att testa testsviten.
