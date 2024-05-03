---
title: Känna igen giltiga och utgångna certifikat i PDF-dokument
description: Lär dig hur du känner igen giltiga och utgångna certifikat i PDF-dokument.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Känna igen giltiga och utgångna certifikat i PDF-dokument {#recognizing-valid-and-expired-certificates-in-pdf-documents}

När ett PDF-dokument som har användningsrättigheter som används av Reader Extensions öppnas i Adobe Reader visas ett statusfält som beskriver de specifika användningsrättigheter som är aktiverade i PDF-dokumentet.

När det digitala certifikatet som anger användningsrättigheterna för ett PDF-dokument upphör att gälla och PDF-dokumentet öppnas i Adobe Reader visas en dialogruta som informerar användaren om att PDF-dokumentet har användningsbehörighet, men dessa rättigheter är inaktiverade. Även om meddelandet anger att dokumentet i PDF har ändrats eller manipulerats behöver detta inte nödvändigtvis vara fallet. Det här meddelandet visas i Adobe Reader när ett certifikat upphör att gälla eller när ett dokument ändras. I Adobe Reader 7.0.x och senare kan du inte avgöra vilket fall som är det aktuella problemet.

När du har stängt dialogrutan öppnas dokumentet PDF. Användningsrättigheterna som tillämpades med Acrobat Reader DC-tillägg är inte tillgängliga som förväntat. Om PDF-dokumentet är ett interaktivt formulär låses formulärfälten och användaren kan inte ändra formulärdata.
