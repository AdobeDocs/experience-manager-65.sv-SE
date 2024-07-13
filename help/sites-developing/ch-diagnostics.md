---
title: ContextHub Diagnostics
description: ContextHub tillhandahåller en diagnostiksida där du kan se en översikt över ContextHub-ramverket
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: b833c28b-76c6-42a2-b690-3e81ddf91bc2
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# ContextHub Diagnostics {#contexthub-diagnostics}

ContextHub tillhandahåller en diagnostiksida där du kan se en översikt över ContextHub-ramverket. Öppna sidan genom att gå till sidan `contexthub.diagnostics.html` i AEM författarinstans, till exempel:

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

På sidan ContextHub Diagnostics (ContextHub-diagnostik) finns information om de butiker och gränssnittsmoduler som har skapats, vilka mappar i klientbiblioteket som har lästs in samt länkar till användbara sidor.

>[!NOTE]
>
>Felsökningsläget måste vara aktiverat för att diagnostikinformation ska kunna returneras, annars är diagnostiksidan tom. Mer information om hur du aktiverar felsökningsläget finns i [det här dokumentet](ch-configuring.md#debugging-contexthub).

>[!NOTE]
>
>För ContextHub-konfigurationer som fortfarande finns under de tidigare sökvägarna är platsen för diagnostiksidan `http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`.

## Lager {#stores}

I avsnittet Lager visas alla ContextHub-butiker som har konfigurerats. Varje post i listan består av följande information:

* **Titel:** [Butikstypen](/help/sites-developing/ch-samplestores.md) som butiken baseras på.
* **sökväg:** Sökvägen till databasnoden som innehåller konfigurationen.
* **resourceType:** Sökvägen till databasnoden där lagringstypen definieras.
* **clientlibs:** De kategorier i klientbiblioteken som är inlästa och som implementerar lagringstypen.

## Moduler {#modules}

I avsnittet Moduler visas alla ContextHub-gränssnittsmoduler som har konfigurerats. Varje post i listan består av följande information:

* **Titel:** Den [UI-modultyp](/help/sites-developing/ch-samplemodules.md) som UI-modulen baseras på.
* **sökväg:** Sökvägen till databasnoden som innehåller konfigurationen.
* **resourceType:** Sökvägen till databasnoden där gränssnittsmodultypen definieras.
* **clientlibs:** Kategorierna för klientbiblioteken som är inlästa och som implementerar UI-modultypen.

## Clientlibs {#clientlibs}

I Clientlibs-avsnittet visas alla klientbiblioteksmappar som ContextHub har läst in. Klientbiblioteken är kategoriserade:

* **kernel.js:** Klientbibliotek som implementerar ContextHub-ramverket, segmentmotorn och lagringstyperna.
* **ui.js:** Klientbibliotek som implementerar gränssnittstyperna ContextHub och UI.
* **style.css:** CSS-filer som läses in från klientbibliotek.

## URL:er {#urls}

Avsnittet URL:er innehåller länkar till ContextHub-funktioner:

* **Konfigurationsredigeraren:** Öppnar [konfigurationssidan för ContextHub](ch-configuring.md) där du kan konfigurera arkiv, gränssnittslägen och gränssnittsmoduler.

* **Konfiguration av ContextHub-moduler:** Öppnar filen /etc/cloudsettings/default/contexthub.config.kernel.js, som innehåller JavaScript-objektrepresentationen av ContextHub-lagringskonfigurationerna.
* **Konfiguration av ContextHub-gränssnitt:** Öppnar filen /etc/cloudsettings/default/contexthub.config.ui.js, som innehåller JavaScript-objektrepresentationen av ContextHub-gränssnittskonfigurationerna.
* **kernel.js:** Öppnar filen /etc/cloudsettings/default/contexthub.kernel.js, som innehåller källkoden för klientbiblioteken som implementerar ContextHub-ramverket, segmentmotorn och lagertyperna.
* **ui.js:** Öppnar filen /etc/cloudsettings/default/contexthub.ui.js, som innehåller källkoden för de klientbibliotek som implementerar gränssnittstyperna ContextHub och UI.
* **style.css:** Öppnar filen /etc/cloudsettings/default/contexthub.styles.css, som innehåller CSS-formaten för ContextHub-gränssnittsmodulerna.
