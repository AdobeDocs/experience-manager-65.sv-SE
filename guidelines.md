---
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---
# Riktlinjer för att bidra till Adobe Experience Manager-dokumentation

## Dokumentationsfilosofi

Adobe vet att Adobe Experience Manager användare arbetar i mycket konkurrensutsatta miljöer och strävar efter att skapa digitala upplevelser som skiljer dem från deras konkurrenter. Därför är det viktigt att Adobe när de tillhandahåller avancerade nya verktyg i AEM kompletteras med korrekt och tydlig dokumentation som gör det möjligt för kunden att omedelbart använda sin AEM och maximera avkastningen på investeringen.

Målet med den AEM dokumentationen är att ge AEM tillgång till dokumentation så snart som möjligt. Därför prioriterar Adobe korrekt, användbar dokumentation och strävar efter att kontinuerligt uppdatera och förbättra den.

## Dokumentationsbidrag

För att ständigt förbättra AEM dokumentation är AEM välkommen att bidra till dokumentationen. Vare sig det gäller förfrågningar eller frågor kan förbättringar av dokumentationen vara korrigeringar, förtydliganden, tillägg och ytterligare exempel.

## Dokumentationsstandarder

Adobe välkomnar bidrag till vår dokumentation, men alla bidrag till AEM, antingen i form av en ansökan om att få lämna in en ansökan eller i form av ett problem, bör överensstämma med våra standarder för bidrag och dokumentation.

Bidrag som inte uppfyller dessa standarder kan avvisas.

### Dokumentets standardanvändningsexempel.

AEM dokumentation täcker standardanvändningsfall. Användningsfall som inte omfattas av standardinstallationer och standardanvändning av produkten ingår inte i AEM.

### Dokumentationen dokumenterar vanligtvis inte fel eller tillfälliga lösningar.

AEM dokumentation täcker standardanvändningsfall. Av den anledningen är buggar, effekter orsakade av buggar och tillfälliga lösningar för buggar vanligtvis inte dokumenterade.

Undantag från den här regeln gäller versionsinformationen där kända problem kan listas med möjliga lösningar som har godkänts av AEM produkthantering.

### Dokumentationsbidragen är inte till för att besvara tekniska frågor.

Alla idéer du kan behöva förbättra AEM dokumentation är välkomna som bidrag. Kommentarer, problem och förfrågningar är dock avsedda för *avgifter* endast. De är inte avsedda att användas för att besvara frågor om hur du använder AEM, implementerar ditt AEM eller löser tekniska problem.

Om du har frågor om hur AEM eller tekniska fel har använts ska du rapportera via den normala supportprocessen via [Experience Manager supportportal](https://experienceleague.adobe.com/sv?support-solution=Experience+Manager#support) eller diskuteras i [Experience Manager community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community).

***AEM ska inte ersätta Adobe kundsupport*** och eventuella bidrag som söker svar på frågor som rör stöd kommer att refuseras.

### Bidragen ska tydligt hänvisa till berörda dokumentationssidor.

Om du skapar ett problem som kan föreslå förbättringar av dokumentationen måste du inkludera länkar till de sidor som påverkas. Om du skapar ett problem med hjälp av **Redigera den här sidan** på en dokumentationssida skapas problemet automatiskt med en länk till sidan.

Detta gäller inte för pull-begäranden eftersom pull-begäranden till sin natur refererar till de berörda sidorna.

## Riktlinjer för dokumentation

Vi ber att eventuella bidrag till vår dokumentation följer vissa riktlinjer för format.

Genom att följa dessa riktlinjer blir det enklare att granska ditt bidrag och det går därför snabbare att integrera det i vår dokumentation.

### Språk och format

#### Språk

* AEM dokumentation skrivs och underhålls på amerikansk engelska.
* Håll meningar så enkla som möjligt.
* Se till att språket är klart och koncist.

Kom ihåg att läsarna av AEM är från hela världen och inte kan förväntas vara inbyggda eller flytande engelska. Undvik kollokvialism och håll språket så tydligt och enkelt som möjligt.

#### Följ Microsoft® Manual of Style

[The Microsoft® Manual of Style](https://learn.microsoft.com/en-us/style-guide/welcome/) är en kostnadsfri handbok för dokumentationsformat som fokuserar på programvarudokumentation och AEM dokumentation följer den här handboken när det är möjligt.

### Formatering

| Objekt | Stil |
|---|---|
| Element eller alternativ i användargränssnittet | **fet** |
| Filnamn, sökväg, användarindata, parametervärden | `monospaced` |
| Kod, kommandorad | ```Code Block``` |

### Skärmbilder

Skärmbilder ska användas med omdöme och endast när en textbeskrivning är otillräcklig.

Använd inte markörer eller andra anteckningar i skärmbilder (som röda ramar, pilar eller text). På så sätt är skärmbilderna enklare att återanvända eller replikera i lokaliserade versioner av dokumentationen.

### Versionsspecifika referenser

Undvik om möjligt direkta referenser till en viss version i dokumentationsinnehållet. Detta gör dokumentationen mer flexibel och utbyggbar för framtida versioner.

### Användning av dag, AEM, CQ, CRX

Produktens fullständiga namn ska alltid anges **Adobe Experience Manager** för första gången i en artikel och kan därefter kallas **AEM**.

Använd inte Dag, Dag Software, CQ och CRX utom när det är oundvikligt, t.ex. i klassnamn eller med hänvisning till AEM.