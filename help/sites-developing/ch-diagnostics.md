---
title: ContextHub Diagnostics
seo-title: ContextHub Diagnostics
description: ContextHub tillhandahåller en diagnostiksida där du kan se en översikt över ContextHub-ramverket
seo-description: ContextHub tillhandahåller en diagnostiksida där du kan se en översikt över ContextHub-ramverket
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: e37ff1c9e657c580c607f2656adca01a2b39f81f

---


# ContextHub Diagnostics {#contexthub-diagnostics}

ContextHub tillhandahåller en diagnostiksida där du kan se en översikt över ContextHub-ramverket. Öppna sidan genom att gå till `contexthub.diagnostics.html` sidan med AEM-författarinstansen, till exempel:

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

På sidan ContextHub Diagnostics (ContextHub-diagnostik) finns information om de butiker och gränssnittsmoduler som har skapats, vilka mappar i klientbiblioteket som har lästs in samt länkar till användbara sidor.

>[!NOTE]
>
>Felsökningsläget måste vara aktiverat för att diagnostikinformation ska kunna returneras, annars är diagnostiksidan tom. I [det här dokumentet](/help/sites-administering/contexthub-config.md#debugging-contexthub) finns mer information om hur du aktiverar felsökningsläget.

>[!NOTE]
>
>För ContextHub-konfigurationer som fortfarande finns under sina tidigare sökvägar är platsen för diagnostiksidan `http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`.

## Lager {#stores}

I avsnittet Lager visas alla ContextHub-butiker som har konfigurerats. Varje post i listan består av följande information:

* **** Titel: Den [butikstyp](/help/sites-developing/ch-samplestores.md) som butiken baseras på.
* **** sökväg: Sökvägen till databasnoden som innehåller konfigurationen.
* **** resourceType: Sökvägen till databasnoden där lagringstypen har definierats.
* **** clientlibs: Kategorierna för de klientbibliotek som läses in och som implementerar lagringstypen.

## Moduler {#modules}

I avsnittet Moduler visas alla ContextHub-gränssnittsmoduler som har konfigurerats. Varje post i listan består av följande information:

* **** Titel: Den [UI-modultyp](/help/sites-developing/ch-samplemodules.md) som UI-modulen baseras på.
* **** sökväg: Sökvägen till databasnoden som innehåller konfigurationen.
* **** resourceType: Sökvägen till databasnoden där gränssnittsmodultypen definieras.
* **** clientlibs: De kategorier av klientbiblioteken som är inlästa och som implementerar UI-modultypen.

## Clientlibs {#clientlibs}

I Clientlibs-avsnittet visas alla klientbiblioteksmappar som ContextHub har läst in. Klientbiblioteken är kategoriserade:

* **** kernel.js: Klientbibliotek som implementerar ContextHub-ramverket, segmentmotorn och lagringstyperna.
* **** ui.js: Klientbibliotek som implementerar gränssnittstyperna ContextHub och UI.
* **** style.css: CSS-filer som läses in från klientbibliotek.

## URL:er {#urls}

Avsnittet URL:er innehåller länkar till ContextHub-funktioner:

* **** Konfigurationsredigerare: Öppnar [ContextHub Configuration-sidan](/help/sites-administering/contexthub-config.md) där du kan konfigurera butiker, gränssnittslägen och gränssnittsmoduler.

* **** Konfiguration av ContextHub-moduler: Öppnar filen /etc/cloudsettings/default/contexthub.config.kernel.js, som innehåller Javascript-objektrepresentationen av ContextHub-lagringskonfigurationerna.
* **** Konfiguration av ContextHub-gränssnitt: Öppnar filen /etc/cloudsettings/default/contexthub.config.ui.js, som innehåller Javascript-objektrepresentationen av ContextHub-gränssnittets lägeskonfigurationer.
* **** kernel.js: Öppnar filen /etc/cloudsettings/default/contexthub.kernel.js, som innehåller källkoden för klientbiblioteken som implementerar ContextHub-ramverket, segmentmotorn och lagringstyperna.
* **** ui.js: Öppnar filen /etc/cloudsettings/default/contexthub.ui.js, som innehåller källkoden för de klientbibliotek som implementerar gränssnittstyperna för ContextHub och UI.
* **** style.css: Öppnar filen /etc/cloudsettings/default/contexthub.styles.css, som innehåller CSS-formaten för ContextHub-gränssnittsmodulerna och UI.