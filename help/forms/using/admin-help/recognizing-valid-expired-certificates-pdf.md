---
title: Känna igen giltiga och utgångna certifikat i PDF-dokument
seo-title: Känna igen giltiga och utgångna certifikat i PDF-dokument
description: Lär dig hur du känner igen giltiga och utgångna certifikat i PDF-dokument.
seo-description: Lär dig hur du känner igen giltiga och utgångna certifikat i PDF-dokument.
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Känna igen giltiga och utgångna certifikat i PDF-dokument {#recognizing-valid-and-expired-certificates-in-pdf-documents}

När ett PDF-dokument som har användningsrättigheter som tillämpas av Reader Extensions öppnas i Adobe Reader visas ett statusfält som beskriver de specifika användningsrättigheter som är aktiverade i PDF-dokumentet.

När det digitala certifikatet som anger användningsrättigheterna för ett PDF-dokument upphör att gälla och PDF-dokumentet öppnas i Adobe Reader, visas en dialogruta som informerar användaren om att PDF-dokumentet har användningsbehörighet, men dessa rättigheter är inaktiverade. Även om meddelandet anger att PDF-dokumentet har ändrats eller manipulerats är detta inte nödvändigtvis fallet. Det här meddelandet visas i Adobe Reader när ett certifikat upphör att gälla eller när ett dokument ändras. I Adobe Reader 7.0.x eller senare kan du inte avgöra vilket fall som är problemet.

När du har stängt dialogrutan öppnas PDF-dokumentet i Adobe Reader. De användningsrättigheter som tillämpades med Acrobat Reader DC-tillägg är inte tillgängliga som förväntat. Om PDF-dokumentet är ett interaktivt formulär är formulärfälten låsta och användaren kan inte ändra formulärdata.
