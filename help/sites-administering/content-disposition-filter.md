---
title: Innehållsdispositionsfilter
seo-title: Innehållsdispositionsfilter
description: Lär dig hur du använder filtret för innehållsdisposition för att förhindra XSS-attacker.
seo-description: Lär dig hur du använder filtret för innehållsdisposition för att förhindra XSS-attacker.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Innehållsdispositionsfilter{#content-disposition-filter}

Dispositionsfiltret är en säkerhetsfunktion mot XSS-attacker på SVG-filer.

När filtret har installerats blockeras åtkomsten till alla resurser. Du kan till exempel inte visa en PDF online. I det här avsnittet beskrivs hur du konfigurerar filtret efter dina behov.

## Konfigurera filtret för innehållsdisposition {#configure-content-disposition-filter}

Du kan visa filtret för disposition av [Apache Sling-innehåll i GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Alternativen för Innehållsdispositionsfilter innehåller följande funktioner:

* Sökvägar för innehållsdisposition: en lista med sökvägar där filtret ska användas följt av en lista med MIME-typer som ska uteslutas på den sökvägen. Sökvägen måste vara en absolut sökväg och kan innehålla ett jokertecken (&#39;&amp;ast;&#39;) i slutet, för att matcha alla resurssökvägar med det angivna sökvägsprefixet. Till exempel: /content/&amp;ast;:image/jpeg,image/svg+xml &quot; tillämpar filtret på alla noder i /content, utom jpg- och svg-bilder

* Uteslutna resurssökvägar: En lista över uteslutna resurser. Varje resurssökväg måste anges som en absolut och fullständig sökväg. Prefixmatchning/jokertecken stöds inte.

* Aktivera för alla resurssökvägar: Den här flaggan anger om det här filtret ska aktiveras för alla sökvägar, förutom för de uteslutna sökvägarna som definieras av Uteslutna resurssökvägar. Om du anger värdet true ignoreras innehållets dispositionsbanor. Oberoende av konfigurationen täcks bara resurssökvägar som innehåller en egenskap med namnet jcr:data eller jcr:content jcr:data.

