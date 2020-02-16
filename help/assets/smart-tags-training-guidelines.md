---
title: Utbildningsriktlinjer för smarta innehållstjänster
description: Utbilda Adobe Senseis AI-tjänst för att använda smarta taggar på resurser
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Utbildningsriktlinjer för smarta innehållstjänster {#smart-content-service-training-guidelines}

För att effektivt märka upp varumärkesbilderna kräver Smart Content Service att utbildningsbilderna följer vissa riktlinjer.

## Riktlinjer för utbildning {#guidelines-for-training}

För bästa resultat bör bilderna i din utbildningsserie följa följande riktlinjer:

**** Kvantitet och storlek: Minst 30 bilder per tagg. Minst 500 pixlar på den längre sidan.

**Samstämmighet**: Bilderna för en tagg bör vara visuellt lika.

Det är till exempel ingen bra idé att tagga alla dessa bilder som `my-party` (för utbildning) eftersom de inte är visuellt lika.

![Illustrativa bilder som exempel på riktlinjer för utbildning](/help/assets/assets/do-not-localize/coherence.png)

**Täckning**: Det ska finnas tillräckligt med variation i bilderna i utbildningen. Tanken är att ge några exempel som är ganska olika, men som ändå är ganska olika, så att AEM lär sig att fokusera på rätt saker. Om du använder samma tagg på bilder som ser olika ut bör du ta med minst fem exempel av varje typ.

För taggen *model-down* kan du t.ex. inkludera fler utbildningsbilder som liknar den markerade bilden nedan för tjänsten för att identifiera liknande bilder mer exakt under taggningen.

![Illustrativa bilder som exempel på riktlinjer för utbildning](/help/assets/assets/do-not-localize/coverage_1.png)

**Distraktion/obstruktion**: Tjänsten tränar bättre på bilder som inte är så distraherande (framträdande bakgrunder, icke-relaterade komponenter, t.ex. objekt/personer med huvudmotivet).

För taggen *casual-shoe*&#x200B;är den andra bilden till exempel inte en bra träningskandidat.

![Illustrativa bilder som exempel på riktlinjer för utbildning](/help/assets/assets/do-not-localize/distraction.png)

**** Fullständighet: Om en bild kvalificerar för mer än en tagg lägger du till alla tillämpliga taggar innan du inkluderar bilden för utbildning. För taggar, till exempel `raincoat` och `model-side-view`lägger du till båda taggarna i den kvalificerade mediefilen innan du inkluderar den för utbildning.

![Illustrativa bilder som exempel på riktlinjer för utbildning](/help/assets/assets/do-not-localize/completeness.png)

## Begränsningar {#limitations}

Förbättrade smarta taggar bygger på inlärningsmodeller för bilder och taggar. Dessa modeller är inte alltid perfekta när det gäller att identifiera taggar. Den aktuella versionen av Smart Content Service har följande begränsningar:

* Oförmåga att identifiera små skillnader i bilder. Till exempel tunna eller jämna skjortor.
* Oförmåga att identifiera taggar baserat på små mönster/delar av en bild. Till exempel logotyper på T-shirts.
* Taggning stöds i de språkområden som AEM stöds i. En lista med språk finns i Versionsinformation för [Smart Content Services](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/smart-content-service-release-notes.html).

Om du vill söka efter resurser med smarta taggar (vanliga eller förbättrade) använder du Resursmomenten (fulltextsökning). Det finns inget separat sökpredikat för smarta taggar.

>[!NOTE]
>
>Möjligheten för Smart Content Service att lära sig taggar och använda dem på andra bilder beror på kvaliteten på de bilder du använder i utbildningen. För bästa resultat rekommenderar Adobe att du använder visuellt liknande bilder för att utbilda tjänsten för varje tagg.
