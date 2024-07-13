---
title: Tagga användargenererat innehåll
description: Taggning av användargenererat innehåll (UGC) är hur communitymedlemmar kan hjälpa andra medlemmar att söka efter innehåll
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Tagga användargenererat innehåll {#tagging-user-generated-content}

## Ökning {#overview}

Taggning av användargenererat innehåll (UGC) är det sätt på vilket communitymedlemmar kan hjälpa andra medlemmar att söka efter innehåll.

Taggar används oftast av författare och administratörer i författarmiljön. Taggning av UGC är unik eftersom UGC-taggar används av communitymedlemmar i publiceringsmiljön.

Taggnamnutrymmen och taxonomier är samma för båda programmen.

## Funktioner i Communities {#communities-features}

AEM Communities-funktionerna som kan konfigureras för att tillåta taggning är:

* [Blogg](blog-feature.md)
* [Kalender](calendar.md)
* [Filbibliotek](file-library.md)
* [Forum](forum.md#configuretheaddedforum)
* [Frågor och svar](working-with-qna.md)

## Administrera taggar {#administering-tags}

Se [Administrera taggar](../../help/sites-administering/tags.md#tagging-console) för att skapa och hantera taggnamnutrymmen och taxonomier.

Mer utvecklarinformation finns i [Tagga viktiga](tag.md).

Se [Använda molnet för sociala taggar](tagcloud.md) för att lägga till en komponent i molnet för sociala taggar på en sida för att underlätta sökning efter publicerad UGC med de använda taggarna.

### Taggbehörigheter {#tag-permissions}

Standardbehörigheterna är inställda på att inte tillåta att taggnamnutrymmen kan läsas av alla i publiceringsmiljön.

Eftersom taggar används i UGC i publiceringsmiljön måste läsbehörighet aktiveras för communitymedlemmar för att de ska kunna markera taggar som ska användas.

Se [Ange taggbehörigheter](../../help/sites-administering/tags.md#setting-tag-permissions).

Så här visas det i CRXDE när en administratör tillämpar läsbehörigheter på `/etc/tag/discussions` för gruppen `Community Engage Members`.

![tagg-permissions](assets/tag-permissions.png)
