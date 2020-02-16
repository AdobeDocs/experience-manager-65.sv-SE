---
title: Innehållsarkitektur
seo-title: Innehållsarkitektur
description: Tips för att skapa ditt innehåll (tips - allt är innehåll)
seo-description: Tips för att skapa ditt innehåll i Adobe Experience Manager (AEM). (tips - allt är innehåll)
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Innehållsarkitektur{#content-architecture}

## Följ David modell {#follow-david-s-model}

David’s Model skrevs av David Nuescheler för flera år sedan, men dagens idéer är sanna. David’s Model har följande huvudinnehåll:

* Data kommer först, strukturen senare. Kanske.
* Driv fram innehållshierarkin, låt den inte ske.
* Arbetsytor är för `clone()`, `merge()`och `update()`.
* Se upp för samma namn som syskon.
* Referenser anses vara skadliga.
* Filer är filer.
* ID:n är onda.

David’s Model finns på Jackrabbit wiki på [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### Allt är innehåll {#everything-is-content}

Allt ska lagras i databasen i stället för att förlita sig på separata datakällor från tredje part, som databaser. Detta gäller redigerat innehåll, binära data som bilder, kod, konfigurationer osv. Detta gör att vi kan använda en uppsättning API:er för att hantera allt innehåll och för att hantera kampanjen av det här innehållet genom replikering. Vi får också en enda källa för säkerhetskopiering, loggning osv.

### Använd designprincipen&quot;innehållsmodell först&quot; {#use-the-content-model-first-design-principle}

När du skapar en ny funktion börjar du alltid med att designa JCR-innehållsstrukturen först och tittar sedan på hur du läser och skriver ditt innehåll med standardservletarna för Sling. På så sätt kan du vara säker på att implementeringen fungerar bra med åtkomstkontrollsmekanismer som är klara att användas och du kan undvika att generera onödiga CRUD-servrar.

### Var RESTful {#be-restful}

Servlets bör definieras baserat på resourceTypes i stället för sökvägar. Detta gör det möjligt att använda JCR-åtkomstkontroller, följa REST-principer och använda den resurs- och resurslösare som vi får i begäran. Detta gör även att vi kan ändra skript som återger URL:er på serversidan utan att behöva ändra några URL:er från klientsidan, samtidigt som implementeringsinformation på serversidan döljs från klienten för ökad säkerhet.

### Undvik att definiera nya nodtyper {#avoid-defining-new-node-types}

Nodtyper fungerar på en låg nivå i infrastrukturlagret och de flesta krav kan uppfyllas med hjälp av en sling:resourceType som tilldelats nodtypen int:unStructed, oak:Unstructed, sling:Folder eller cq:Page. Nodtyper motsvarar schemat i databasen och det kan vara väldigt dyrt att ändra nodtyperna längs vägen.

### Anta namnkonventioner i den gemensamma CR-rapporten {#adhere-to-naming-conventions-in-the-jcr}

Om du följer namngivningskonventioner blir kodbasen mer konsekvent, vilket minskar förekomsten av defekter och ökar hastigheten för utvecklare som arbetar i systemet. Följande konventioner används av Adobe vid utveckling av AEM:

* Nodnamn

   * Alla gemener
   * Ordseparation med bindestreck

* Egenskapsnamn

   * Kamerafodral, med början med en gemen bokstav

* Komponenter (JSP/HTML)

   * Alla gemener
   * Ordseparation med bindestreck

