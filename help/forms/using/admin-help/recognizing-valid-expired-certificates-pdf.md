---
title: Känna igen giltiga och utgångna certifikat i PDF-dokument
seo-title: Recognizing valid and expired certificates in PDF documents
description: Lär dig hur du känner igen giltiga och utgångna certifikat i PDF-dokument.
seo-description: Learn how to recognize valid and expired certificates in PDF documents.
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Känna igen giltiga och utgångna certifikat i PDF-dokument {#recognizing-valid-and-expired-certificates-in-pdf-documents}

När ett PDF-dokument som har användningsrättigheter som används av Reader Extensions öppnas i Adobe Reader visas ett statusfält som beskriver de specifika användningsrättigheter som är aktiverade i PDF-dokumentet.

När det digitala certifikatet som anger användningsrättigheterna för ett PDF-dokument upphör att gälla och PDF-dokumentet öppnas i Adobe Reader visas en dialogruta som informerar användaren om att PDF-dokumentet har användningsbehörighet, men dessa rättigheter är inaktiverade. Även om meddelandet anger att dokumentet i PDF har ändrats eller manipulerats behöver detta inte nödvändigtvis vara fallet. Det här meddelandet visas i Adobe Reader när ett certifikat upphör att gälla eller när ett dokument ändras. I Adobe Reader 7.0.x eller senare kan du inte avgöra vilket fall som är det aktuella problemet.

När du har stängt dialogrutan öppnas dokumentet PDF. Användningsrättigheterna som tillämpades med Acrobat Reader DC-tillägg är inte tillgängliga som förväntat. Om PDF-dokumentet är ett interaktivt formulär låses formulärfälten och användaren kan inte ändra formulärdata.
