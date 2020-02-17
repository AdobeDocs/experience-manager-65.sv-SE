---
title: Datamodellering - David Nueschelers modell
seo-title: Datamodellering - David Nueschelers modell
description: David Nueschelers rekommendationer för innehållsmodellering
seo-description: David Nueschelers rekommendationer för innehållsmodellering
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Datamodellering - David Nueschelers modell{#data-modeling-david-nuescheler-s-model}

## Source {#source}

Följande detaljer är idéer och kommentarer från David Nuescheler.

David var en av grundarna och CTO på Day Software AG, en ledande leverantör av programvara för global innehållshantering och innehållsinfrastruktur, som Adobe förvärvade 2010. Han är nu medlem i och VP för Enterprise Technology hos Adobe och leder också utvecklingen av JSR-170, Java Content Repository (JCR), applikationsgränssnitt (API), teknikstandarden för innehållshantering.

Ytterligare uppdateringar finns också på [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

## Introduktion från David {#introduction-from-david}

I olika diskussioner fann jag att utvecklarna är lite osäkra på de funktioner som JCR presenterade när det gäller innehållsmodellering. Det finns ännu ingen guide och mycket liten erfarenhet av att modellera innehåll i en databas och varför en innehållsmodell är bättre än den andra.

I den relationella världen har programvarubranschen en hel del erfarenhet av att modellera data, men vi är fortfarande i ett tidigt skede när det gäller innehållslagerutrymmet.

Jag skulle vilja börja fylla denna tomrumpa genom att uttrycka mina personliga åsikter om hur innehåll bör modelleras, och hoppas att detta en dag kan utexamineras i något mer meningsfullt för utvecklarcommunityn, som inte bara är &quot;min åsikt&quot; utan något som är mer allmänt tillämpligt. Så tänk på det här som min snabbaste början på det.

>[!NOTE]
>
>Ansvarsfriskrivning: Dessa riktlinjer uttrycker mina personliga, ibland kontroversiella åsikter. Jag ser fram emot att debattera dessa riktlinjer och förfina dem.

## Sju enkla regler {#seven-simple-rules}

### Regel 1: Data först, struktur senare. Kanske. {#rule-data-first-structure-later-maybe}

#### Förklaring {#explanation-1}

Jag rekommenderar att man inte behöver bekymra sig om en deklarerad datastruktur i ett ERD-avseende. Inledningsvis.

Lär dig att älska inte:ostrukturerade (&amp; vänner) under utvecklingen.

Jag tror att Stefano summerar det här.

Mitt resultat: Strukturen är dyr och i många fall är det helt onödigt att uttryckligen deklarera strukturen till den underliggande lagringen.

Det finns ett implicit kontrakt om strukturen som ditt program använder. Jag lagrar ändringsdatumet för ett blogginlägg i en lastModified-egenskap. Min app kan automatiskt läsa ändringsdatumet från samma egenskap igen, det finns ingen anledning att deklarera det uttryckligen.

Ytterligare databegränsningar som obligatoriska eller typ- och värdebegränsningar bör endast tillämpas där det är nödvändigt av dataintegritetsskäl.

#### Exempel {#example-1}

Ovanstående exempel på hur du använder en `lastModified` Date-egenskap på till exempel en blogginläggsnod innebär inte att det behövs en särskild nodtyp. Jag använder definitivt `nt:unstructured` blogginläggsnoderna åtminstone från början. Eftersom jag i mitt bloggprogram bara kommer att visa datumet lastModified i alla fall (eventuellt &quot;order by&quot;) bryr jag mig knappt om det är ett datum alls. Eftersom jag ändå litar på att mitt blogginläggsprogram ska placera ett &quot;datum&quot; behöver jag inte deklarera ett `lastModified` datum i formatet en nodetype.

### Regel 2: Låt inte innehållshierarkin hända. {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### Förklaring {#explanation-2}

Innehållshierarkin är en mycket värdefull resurs. Så låt det inte bara hända, designa det. Om du inte har ett &quot;bra&quot;, läsbart namn för en nod är det antagligen något du bör tänka om. Godtyckliga siffror är så gott som aldrig ett &quot;bra namn&quot;.

Även om det kan vara extremt enkelt att snabbt lägga in en befintlig relationsmodell i en hierarkisk modell, bör man tänka lite i den processen.

Enligt min erfarenhet är det oftast bra drivrutiner för innehållshierarkin om man tänker på åtkomstkontroll och inneslutning. Tänk på det som om det vore ditt filsystem. Du kan till och med använda filer och mappar för att modellera dem på den lokala hårddisken.

Personligen föredrar jag hierarkiska konventioner framför nodetypsystemet i många fall först och sedan introducerar jag typningen senare.

>[!CAUTION]
>
>Det sätt på vilket en innehållsdatabas är strukturerad kan även påverka prestanda. För bästa prestanda bör antalet underordnade noder som är kopplade till enskilda noder i en innehållsdatabas i allmänhet inte överstiga 1 000.
>
>Se [hur mycket data CRX kan hantera?](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) för mer information.

#### Exempel {#example-2}

Jag skulle modellera ett enkelt bloggsystem enligt följande. Observera att jag från början inte ens bryr mig om vilka nodtyper jag använder just nu.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

Jag tror att en av de saker som blir uppenbara är att vi alla förstår innehållets struktur baserat på exemplet utan några ytterligare förklaringar.

Det som till en början kan vara oväntat är varför jag inte skulle lagra &quot;kommentarerna&quot; med &quot;posten&quot;, som beror på åtkomstkontroll som jag skulle vilja ha på ett rimligt hierarkiskt sätt.

Med innehållsmodellen ovan kan jag enkelt låta den anonyma användaren&quot;skapa&quot; kommentarer, men behålla den anonyma användaren skrivskyddad för resten av arbetsytan.

### Regel 3: Arbetsytorna är för clone(), merge() och update(). {#rule-workspaces-are-for-clone-merge-and-update}

#### Förklaring {#explanation-3}

Om du inte använder `clone()`det är förmodligen en enda arbetsyta `merge()` eller `update()` metoder i programmet som är rätt väg.

&quot;Motsvarande noder&quot; är ett koncept som definieras i JCR-specifikationen. Det handlar i princip om noder som representerar samma innehåll, i olika så kallade arbetsytor.

JCR introducerar det mycket abstrakta begreppet Workspaces, vilket gör att många utvecklare inte vet vad de ska göra med dem. Jag vill föreslå att du använder arbetsytorna för att testa följande.

Om du har en avsevärd överlappning av&quot;motsvarande&quot; noder (i huvudsak noder med samma UUID) i flera arbetsytor kan du förmodligen använda arbetsytorna på ett bra sätt.

Om det inte finns någon överlappning av noder med samma UUID använder du antagligen arbetsytor.

Arbetsytor bör inte användas för åtkomstkontroll. Synlighet för innehåll för en viss användargrupp är inget bra argument för att dela upp saker i olika arbetsytor. JCR har &quot;Åtkomstkontroll&quot; i innehållsdatabasen för att tillhandahålla den.

Arbetsytor är gränsen för referenser och frågor.

#### Exempel {#example-3}

Använd arbetsytor för exempelvis:

* v1.2 av ditt projekt jämfört med v1.3 av ditt projekt
* ett&quot;utvecklingstillstånd&quot;,&quot;QA&quot; och ett&quot;publicerat&quot; innehållstillstånd

Använd inte arbetsytor för exempelvis:

* användarens hemkataloger
* distinkt innehåll för olika målgrupper som public, private, local, ...
* e-postinkorgar för olika användare

### Regel 4: Se upp för likasinnade namn. {#rule-beware-of-same-name-siblings}

#### Förklaring {#explanation-4}

Även om SNS (Same Name Siblings) har införts i specifikationen för att möjliggöra kompatibilitet med datastrukturer som är utformade för och uttryckta genom XML och därför är mycket värdefulla för JCR, har SNS en avsevärd belastning och komplexitet för databasen.

Alla sökvägar till innehållsdatabasen som innehåller en SNS i ett av dess sökvägssegment blir mycket mindre stabila, om en SNS tas bort eller sorteras om, påverkar det sökvägarna för alla andra SNS och deras underordnade.

För import av XML eller interaktion med befintlig XML SNS kan det vara nödvändigt och användbart, men jag har aldrig använt SNS och kommer aldrig att göra det i mina&quot;gröna fältsdatamodeller&quot;.

#### Exempel {#example-4}

Användning

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

i stället för

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### Regel 5: Referenser som betraktas som skadliga. {#rule-references-considered-harmful}

#### Förklaring {#explanation-5}

Referenser innebär referensintegritet. Jag tycker att det är viktigt att förstå att referenser inte bara medför extra kostnader för databasen som hanterar referensintegriteten, utan även är kostsamma ur ett flexibelt perspektiv.

Personligen ser jag till att jag bara använder referenser när jag inte kan hantera en farlig referens och i annat fall använda en sökväg, ett namn eller en sträng-UID för att referera till en annan nod.

#### Exempel {#example-5}

Låt oss anta att jag tillåter &quot;referenser&quot; från ett dokument (a) till ett annat dokument (b). Om jag modellerar den här relationen med hjälp av referensegenskaper innebär det att de två dokumenten är länkade på en databasnivå. Jag kan inte exportera/importera dokument (a) separat, eftersom referensegenskapens mål kanske inte finns. Även andra åtgärder som sammanfogning, uppdatering, återställning och kloning påverkas.

Därför skulle jag antingen modellera dessa referenser som &quot;svag referens&quot; (i JCR v1.0 så här böjer det sig i princip ned till strängegenskaper som innehåller målnodens uuid) eller bara använda en sökväg. Ibland är banan mer meningsfull att börja med.

Jag tror att det finns situationer där ett system verkligen inte fungerar om en referens är farlig, men jag kan inte komma på ett bra &quot;verkligt&quot; men ändå enkelt exempel från min direkta erfarenhet.

### Regel 6: Filer är filer. {#rule-files-are-files}

#### Förklaring {#explanation-6}

Om en innehållsmodell visar något som till och med *känner* av lukt på fjärrbasis, som en fil eller en mapp som jag försöker använda (eller utöka från) `nt:file`och `nt:folder` `nt:resource`.

Enligt min erfarenhet tillåter många generiska program interaktion med nt:folder och nt:files implicit och vet hur de ska hantera och visa dessa händelser om de har berikats med ytterligare metainformation. En direkt interaktion med filserverimplementeringar som CIFS eller WebDAV som sitter ovanpå JCR blir till exempel implicit.

Jag tror att en bra tumregel kan behöva följande: Om du behöver lagra filnamnet och mime-typen så är `nt:file`/ `nt:resource` en bra matchning. Om du kan ha flera &quot;filer&quot; kan det vara bra att spara dem i mappen nt:folder.

Om du behöver lägga till metainformation för resursen kan vi säga &quot;författare&quot; eller &quot;beskrivning&quot;, men utöka `nt:resource` inte `nt:file`. Jag utökar sällan inte:fil och utökar ofta `nt:resource`.

#### Exempel {#example-6}

Låt oss anta att någon vill ladda upp en bild till ett blogginlägg på:

```xml
/content/myblog/posts/iphone_shipping
```

och kanske den initiala uttarningsreaktionen är att lägga till en binär egenskap som innehåller bilden.

Även om det finns bra användningsexempel för att bara använda en binär egenskap (vi ska säga att namnet är irrelevant och att mime-typen är implicit) i det här fallet rekommenderar jag följande struktur för bloggexemplet.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### Regel 7:ID:n är onda. {#rule-ids-are-evil}

#### Förklaring {#explanation-7}

I relationsdatabaser är id:n ett nödvändigt sätt att uttrycka relationer, så folk tenderar att använda dem även i innehållsmodeller. Mestadels av fel skäl.

Om innehållsmodellen är full av egenskaper som slutar på&quot;ID&quot; använder du förmodligen inte hierarkin korrekt.

Det är sant att vissa noder behöver en stabil identifiering under hela sin livscykel. Mycket färre än du tror. mix:referenceable innehåller en sådan mekanism som är inbyggd i databasen, så det finns inget behov av att hitta ytterligare sätt att identifiera en nod på ett stabilt sätt.

Tänk också på att objekt kan identifieras med sökväg, och så mycket som &quot;symlinks&quot; är mer användbart för de flesta användare än maskinlänkar i ett enhetligt filsystem, är en sökväg ett bra sätt för de flesta program att referera till en målnod.

Dessutom är det **mix**:referenable, vilket betyder att det kan användas på en nod vid den tidpunkt då du faktiskt behöver referera till den.

Låt oss säga bara för att du vill kunna referera till en nod av typen&quot;Dokument&quot; innebär det inte att din&quot;Dokument&quot;-nodtyp måste byggas ut från mix:referenable på ett statiskt sätt eftersom den kan läggas till dynamiskt i alla instanser av&quot;Dokument&quot;.

#### Exempel {#example-7}

Användning:

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

i stället för:

```xml
[Blog]
-- blogId
-- author
[Post]
-- postId
-- blogId
-- title
-- text
-- date
[Attachment]
-- attachmentId
-- postId
-- filename
+ resource (nt:resource)
```

