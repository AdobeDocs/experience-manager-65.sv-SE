---
title: CRX/bundle och Start page service unavailable errors once latest 6.5.15.0 service pack is installed
description: CRX/bundle och Start page service unavailable errors once latest 6.5.15.0 service pack is installed
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Tjänsten är inte tillgänglig efter installation av AEM (6.5.15.0) Service Pack {#steps-to-resolve-error-after-installing-service-pack}

## Problem {#issue}

När du har installerat [AEM 6.5.15.0 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), inträffar felet som:
* FEL [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException: Det går inte att lösa org.apache.sling.scripting.console

När du har installerat AEM 6.5.15.0 Service Pack visar CRX/bundle och startsidan fel som inte är tillgängliga för tjänsten.

## Gäller för {#applies-to}

Denna lösning gäller
* AEM Forms på alla JEE-servrar utom de som körs på JBoss EAP 7.4.0

## Lösning {#solution}

>[!NOTE]
>
>Felsökningsstegen gäller alla programservrar utom JBoss EAP 7.4.

Efter installation [AEM 6.5.15.0 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)Om det uppstår fel i CRX/bundle och startsidan, ska du utföra följande steg:

1. Stoppa programservern.
1. Navigera till `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. Leta reda på `bundle.info` -fil.
1. Öppna `bundle.info` i redigeraren för ant-text och sök efter paketnamnet som `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >Om `bundle.info` under `bundle52` innehåller inte `org.apache.felix.http.bridge` paket, kontrollera paketnumret inom hakparentes bredvid `org.apache.felix.http.bridge`. Navigera sedan till [aem-forms root]\crx-repository\launchpad\felix\bundle[x] och utför nästa steg på den här platsen.

1. Navigera till URL: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. Sök efter `bundle.jar` och ändra namn på `bundle.jar` till `bundle.jar.bak`.
1. Kopiera `Bundle for AEM 6.5 Forms on JEE Service Pack 15` på den här platsen från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. Starta programservern, vänta på att loggarna ska stabiliseras och kontrollera paketläget.
1. När alla paket är aktiva installerar du [Fragment för AEM 6.5 Forms för JEE Service Pack 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) från `system/console/bundles` och vänta på att programservern ska stabiliseras.
1. Stoppa programservern.
1. Navigera till `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` och ta bort `bundle.jar`.
1. Byt namn på `bundle.jar.bak` till `bundle.jar`.
1. Starta programservern.
