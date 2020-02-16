---
title: Dataskydd och dataintegritet - Adobe Experience Manager-beredskap
seo-title: Adobe Experience Manager Readiness for Data Protection and Data Privacy Regulations; såsom GDPR, CCPA osv.
description: 'Läs om stödet för Adobe Experience Manager för de olika dataskydds- och datasekretessreglerna. inklusive EU:s allmänna dataskyddsförordning (GDPR), Kaliforniens konsumentintegritetslag och hur man ska följa detta när man genomför ett nytt AEM-projekt. '
seo-description: 'Läs om stödet för Adobe Experience Manager för de olika dataskydds- och datasekretessreglerna. inklusive EU:s allmänna dataskyddsförordning (GDPR), Kaliforniens konsumentintegritetslag och hur man ska följa detta när man genomför ett nytt AEM-projekt. '
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: aheimoz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: grdp
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
translation-type: tm+mt
source-git-commit: 9b16c8ae2ee28c60f35f9e0f990d79173463c33b

---


# Adobe Experience Manager Readiness for Data Protection and Data Privacy Regulations {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Innehållet i detta dokument utgör inte juridisk rådgivning och är inte avsett som ersättning för juridisk rådgivning.
>
>Kontakta företagets juridiska avdelning för råd angående dataskydd och dataintegritet.

>[!NOTE]
>
>Mer information om Adobes svar på sekretessfrågor och vad detta innebär för dig som Adobe-kund finns i [Adobes Sekretesscenter](https://www.adobe.com/privacy.html).

Adobe tillhandahåller dokumentation och procedurer (med API:er när sådana finns) för kundsekretessadministratören eller AEM-administratören för att hantera förfrågningar om dataskydd och datasekretess och hjälpa våra kunder att följa dessa regler. De dokumenterade procedurerna gör det möjligt för kunderna att utföra förfrågningar manuellt eller genom att anropa API:er, om sådana finns, från en extern portal eller tjänst.

>[!CAUTION]
>
>Informationen som beskrivs här är begränsad till Adobe Experience Manager.
>
>Data från en annan Adobe On-demand-tjänst, tillsammans med eventuella relaterade sekretessförfrågningar, kräver åtgärder för den tjänsten.
>
>Mer information finns i [Adobes Sekretesscenter](https://www.adobe.com/privacy.html).

## Introduktion {#introduction}

Instanser av Adobe Experience Manager och de program som körs på dem ägs och hanteras av våra kunder.

Följaktligen är dataskyddsbestämmelser, som GDPR, CCPA med flera, i huvudsak kundernas ansvar.

Som en mycket kort introduktion innehåller reglerna för datasekretess och skydd nya regler som ska följas av rollerna för:

* Affärsenheter (CCPA) och/eller datakontroller (GDPR)

* Tjänsteleverantörer (CCPA) och/eller dataprocessorer (GDPR)

De viktigaste bestämmelserna i sådana förordningar är

1. Utökad definition av personuppgifter som ska omfatta alla unika ID:n. som direkt och indirekt identifierbara data.

2. Förbättrade krav på samtycke.

3. Ökat fokus på raderingsrättigheter (dataradering).

4. Avanmäl dig från försäljning av data.

För Adobe Experience Manager:

* Förekomsterna och tillämpningarna som körs på dem ägs och hanteras av kunden.

   * Detta innebär att kunden i praktiken hanterar de reglerande rollerna, bland annat affärsenheter och tjänsteleverantör, datakontroller och dataprocessor.

   * Integritetstjänsten för Adobe Experience Platform kommer inte att ingå i arbetsflödet för AEM, vilket visas i bilden nedan.

* AEM innehåller dokumentation och förfaranden för kundens integritetsadministratör och/eller AEM-administratör för att verkställa förfrågningar om sekretessbestämmelser. antingen manuellt eller via API:er, om sådana finns.

* Ingen ny tjänst eller gränssnitt har lagts till.

   * Istället dokumenteras procedurer och API:er för användning av kundgränssnitt/portaler som hanterar förfrågningar om sekretessbestämmelser.

* AEM kommer inte att innehålla några färdiga verktyg som stöder arbetsflödet för sekretessförfrågningar.

   * Adobe kommer att tillhandahålla dokumentation och procedurer för kundens sekretessadministratör och/eller AEM-administratör, vilket gör att de manuellt kan utföra förfrågningar relaterade till sekretessreglerna.

Adobe tillhandahåller rutiner för hantering av sekretessförfrågningar relaterade till åtkomst, borttagning och avanmälan för Adobe Experience Manager. I vissa fall finns det API:er som kan anropas från en kundutvecklad portal eller skript som kan hjälpa till med automatisering.

Följande diagram visar hur ett arbetsflöde för sekretesspolicy kan se ut (illustreras med Adobe Experience Manager 6.5):

![Dataskydd och integritet](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager och beredskap för regelefterlevnad {#aem-and-regulatory-readiness}

Se avsnitten nedan för information om gällande regelverk för AEM-produkter.

## AEM Foundation {#aem-foundation}

Se [Hantera dataskydd och sekretessförfrågningar för AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM avanmäler sig till Samling med användningsstatistik {#aem-opting-into-aggregate-usage-statistics-collection}

Se Samling med statistik om [aggregerad användning](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

Se [AEM Sites - Data Protection and Privacy Readiness.](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

Se [AEM Commerce - dataskydd och sekretesberedskap](/help/sites-administering/gdpr-compliance-commerce.md).

## AEM Mobile {#aem-mobile}

Se [AEM Mobile - Dataskydd och integritet](/help/mobile/aem-mobile-gdpr-compliance.md).

## AEM-integrering med Adobe Target och Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Dessa Adobe Experience Manager-integreringar är anpassade för dataskydd och sekretess (till exempel GDPR eller CCPA). Inga personuppgifter från Adobe Target eller Adobe Analytics lagras i AEM i relation till integreringarna.
Mer information finns i:

* [Adobe Target - Integritetsöversikt](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Arbetsflöde för dataintegritet i Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities utnyttjar de registrerade rätt till dataportabilitet, rätt till åtkomst och rätt att bli bortglömda med hjälp av API:er [som är färdiga att](/help/communities/user-ugc-management-service.md)användas. Dessa API:er möjliggör massborttagning och bulkexport av användargenererat innehåll och inaktiverar användarkonton som identifieras med deras auktoriserbara ID:n. Det går dock att permanent ta bort användarkontot genom att ta bort användarnoden i CRXDE Lite, som åtgärdar behovet av enkel avanmälan från systemet.

Dessutom erbjuder AEM Communities sekretess genom design tack vare sin konsol för massmoderering, som tillåter behöriga medlemmar att hitta och ta bort bidrag och information om användarna. Hanteringskonsolen för medlemmar gör det möjligt att begränsa till att förbjuda en medverkande. Dessutom ger det de registrerade rätt att ta bort de bidrag som de har skapat.

## AEM Forms {#aem-forms}

AEM Forms innehåller komponenter och arbetsflöden som samlar in, bearbetar och lagrar data för att samordna affärsprocesser och slutföra digitala transaktioner. Olika komponenter använder olika datalager och tillåter även integrering med anpassade datalager. I följande dokumentation förklaras procedurer och riktlinjer för att komma åt och hantera användardata för att stödja arbetsflöden för dataskydd och sekretess (till exempel GDPR eller CCPA) för en komponent.

* [Formulärportal](/help/forms/using/forms-portal-handling-user-data.md)
* [Korrespondenshantering](/help/forms/using/correspondence-management-handling-user-data.md)
* [Integrering med Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Formulärbaserade arbetsflöden i OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Formulär-JEE-arbetsflöden](/help/forms/using/forms-workflow-jee-handling-user-data.md) (endast AEM Forms JEE)
* [Dokumentsäkerhet](/help/forms/using/document-security-handling-user-data.md) (endast AEM Forms JEE)
* [Användarhantering](/help/forms/using/user-management-handling-user-data.md) (endast AEM Forms JEE)
