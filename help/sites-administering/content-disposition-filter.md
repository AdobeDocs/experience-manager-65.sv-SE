---
title: Innehållsdispositionsfilter
description: Lär dig hur du använder filtret för innehållsdisposition för att förhindra XSS-attacker.
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Innehållsdispositionsfilter {#content-disposition-filter}

Dispositionsfiltret är en säkerhetsfunktion mot XSS-attacker mot SVG-filer.

När filtret har installerats blockeras åtkomsten till alla resurser. Du kan till exempel inte visa PDF online. I det här avsnittet beskrivs hur du konfigurerar filtret efter dina behov.

## Konfigurera filtret för innehållsdisposition {#configure-content-disposition-filter}

Du kan visa [Dispositionsfiltret för Apache Sling-innehåll i GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Alternativen för Innehållsdispositionsfilter innehåller följande funktioner:

* **Sökvägar för innehållsdisposition:** En lista med sökvägar där filtret används följt av en lista med MIME-typer som ska uteslutas på den sökvägen. Sökvägen måste vara en absolut sökväg och kan innehålla ett jokertecken (`*`) i slutet, för att matcha alla resurssökvägar med det angivna sökvägsprefixet. `/content/*:image/jpeg,image/svg+xml` använder till exempel filtret på alla noder i `/content?` förutom bilder i JPG och SVG.

* **Uteslutna resurssökvägar:** En lista över exkluderade resurser. Varje resurssökväg måste anges som en absolut och fullständig sökväg. Prefixmatchning/jokertecken stöds inte.

* **Aktivera för alla resurssökvägar:** Den här flaggan kontrollerar om det här filtret ska aktiveras för alla sökvägar, utom för de uteslutna sökvägarna som definieras av Undantagna resurssökvägar. Om du anger flaggan som true ignoreras innehållets dispositionssökvägar. Oberoende av konfigurationen täcks bara resurssökvägar som innehåller egenskapen `jcr:data` eller `jcr:content/jcr:data`.
