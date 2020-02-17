---
title: Anropa AEM-formulär med API:er
seo-title: Anropa AEM-formulär med API:er
description: 'null'
seo-description: 'null'
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Anropa AEM-formulär med API:er {#invoking-aem-forms-using-apis}

Adobe Experience Manager Forms är J2EE-baserad företagsprogramvara som består av tjänster som fungerar i en delad infrastruktur. Serviceåtgärder brukar förbruka eller producera dokument. Genom att använda AEM Forms kan du kombinera formulärarbetsflöden med elektroniska formulär, dokumentsäkerhet och dokumentgenerering i en integrerad och sammanhängande uppsättning tjänster. Dessa tjänster kan nås inifrån och utanför brandväggen.

Klientprogram kan programmatiskt anropa AEM Forms-tjänster med Java API, webbtjänster, Remoting och REST. Med administrationskonsolen kan du konfigurera en tjänst så att en slutpunkt visas som gör att AEM Forms-tjänster kan anropas via programmering. Som standard är de flesta tjänster förkonfigurerade för att visa slutpunkter för Remoting, Java och webbtjänster.

Dina affärskrav avgör vilken anropsmetod som ska användas. Med Java API kan du till exempel integrera AEM Forms-funktionalitet i Java Enterprise-program som Java Entity och Message Beans. På samma sätt kan du integrera AEM Forms-funktionalitet i .NET-projekt (eller andra projekt som utvecklats med utvecklingsmiljöer som stöder webbtjänststandarder) med hjälp av webbtjänster.

Tjänsterna kräver en tjänstbehållare för att köras, ungefär som Enterprise JavaBeans™ (EJB) kräver en J2EE-behållare. AEM Forms innehåller endast en implementering av en tjänstbehållare. Tjänstbehållaren ansvarar för att hantera tjänstens livstid, inklusive distribuering, och ser till att alla begäranden skickas till rätt tjänst. Den hanterar också dokument som en tjänst förbrukar eller producerar.

>[!NOTE]
>
>Programmering med AEM-formulär innehåller ingen information om hur AEM-formulär anropas med Bevakade mappar eller e-post.

