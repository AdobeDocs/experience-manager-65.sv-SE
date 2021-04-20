---
title: API:er för åtkomst till bokstavsinstanser
seo-title: API:er för åtkomst till bokstavsinstanser
description: Lär dig hur du använder API:er för att komma åt bokstavsinstanser.
seo-description: Lär dig hur du använder API:er för att komma åt bokstavsinstanser.
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---


# API:er för åtkomst till bokstavsinstanser {#apis-to-access-letter-instances}

## Översikt {#overview}

Med hjälp av användargränssnittet Skapa korrespondens för korrespondenshantering kan du spara utkast av pågående bokstavsinstanser och det finns skickade brevinstanser.

Med Correspondence Management kan du skapa API:er som du kan använda för att skapa listgränssnittet och arbeta med skickade brev eller utkast. API:erna listar och öppnar instanser av en agent som skickats och utkastbrev, så att agenten kan fortsätta arbeta med utkast eller skickade brev.

## Hämtar bokstavsinstanser {#fetching-letter-instances}

Correspondence Management exponerar API:er för att hämta bokstavsinstanser via tjänsten LetterInstanceService.

| Metod | Beskrivning |
|--- |--- |
| getAllLetterInstances | Hämtar bokstavsinstanser baserat på frågeindataparametern. Om du vill hämta alla bokstavsinstanser skickar du frågeparametern som null. |
| getLetterInstance | Hämtar den angivna bokstavsinstansen baserat på bokstavsinstansens ID. |
| letterInstanceExists | Kontrollerar om det finns en LetterInstance med det angivna namnet. |

>[!NOTE]
>
>LetterInstanceService är en OSGI-tjänst och dess instans kan hämtas med @Reference i Java
>Class eller sling.getService(LetterInstanceService). klass) i JSP.

### Använda getAllLetterInstances {#using-nbsp-getallletterinstances}

Följande API hittar bokstavsinstanserna baserat på frågeobjektet (både Skickat och Utkast). Om frågeobjektet är null returneras alla bokstavsinstanser. Detta API returnerar en lista med [LetterInstanceVO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html)-objekt, som kan användas för att extrahera ytterligare information om bokstavsinstansen

**Syntax**:  `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>Parameter</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>query</td>
   <td>Frågeparametern används för att hitta/filtrera instansen av Letter. Här har frågan bara stöd för objektets attribut/egenskaper på den översta nivån. Frågan består av satser och "attributeName" som används i Statement-objektet ska vara namnet på egenskapen i Letter-instansobjektet.<br /> </td>
  </tr>
 </tbody>
</table>

#### Exempel 1: Hämta alla bokstavsinstanser av typen SKICKAD {#example-fetch-all-the-letter-instances-of-type-submitted}

Följande kod returnerar listan med skickade bokstavsinstanser. Om du bara vill hämta utkast ändrar du `LetterInstanceType.COMPLETE.name()` till `LetterInstanceType.DRAFT.name().`

```java
@Reference
LetterInstanceService letterInstanceService;
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

#### Exempel 2: Hämta alla bokstavsinstanser som skickats av en användare och teckeninstanstypen är DRAFT {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

Följande kod har flera satser i samma fråga för att få resultaten filtrerade baserat på olika villkor, t.ex. bokstavsinstans som skickats (attribut som skickats av en användare) och typen av letterInstanceType är DRAFT.

```java
@Reference
LetterInstanceService letterInstanceService;

String submittedBy = "tglodman";
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);

Statement statementForSubmittedBy = new Statement();
statementForSubmittedBy .setAttributeName("submittedby");
statementForSubmittedBy .setOperator(Operator.EQUALS);
statementForSubmittedBy .setAttributeValue(submittedBy);
query.addStatement(statementForSubmittedBy );
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

### Använda getLetterInstance {#using-nbsp-getletterinstance}

Hämta den bokstavsinstans som identifieras av det angivna bokstavsinstansens ID. Det returnerar &quot;null om instans-ID inte matchas.

**Syntax:** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### Verifierar om det finns en LetterInstance {#verifying-if-letterinstance-exist}

Kontrollera om det finns en bokstavsinstans med det angivna namnet

**Syntax**:  `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **Parameter** | **Beskrivning** |
|---|---|
| letterInstanceName | Namnet på den bokstavsinstans som du vill kontrollera om den finns. |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## Inledande bokstavsinstanser {#opening-letter-instances}

Bokstavsinstans kan vara av typen Skickat eller Utkast. Om du öppnar båda bokstavsinstansstyperna visas olika beteenden:

* Om det är en instans av skickad bokstav öppnas en PDF som representerar bokstavsinstansen. Instansen Letter som finns kvar på servern innehåller även dataXML och bearbetad XDP, som kan användas för att åstadkomma och ytterligare anpassad användning av exempelvis PDF/A.
* Om det gäller en instans av ett utkast, läses gränssnittet för att skapa korrespondens in på nytt till exakt föregående läge som det var när utkastet skapades

### Instans för inledande av utkast  {#opening-draft-letter-instance-nbsp}

CCR-gränssnittet stöder parametern cmLetterInstanceId som kan användas för att läsa in bokstaven igen.

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>Du behöver inte ange cmLetterId eller cmLetterName/State/Version när du läser in korrespondensen igen, eftersom skickade data redan innehåller all information om korrespondensen som läses in igen. RandomNo används för att undvika problem med webbläsarcache, du kan använda tidsstämpel som ett slumpmässigt tal.

### Öppnar den skickade bokstavsinstansen {#opening-submitted-letter-instance}

Skickad PDF kan öppnas direkt med ID för bokstavsinstans:

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
