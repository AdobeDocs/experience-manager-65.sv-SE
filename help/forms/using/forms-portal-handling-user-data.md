---
title: Forms Portal | Hantera användardata
description: Forms Portal | Hantera användardata
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin
exl-id: 791524a4-a8bb-4632-a68d-e96864e139a9
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---

# Forms Portal | Hantera användardata {#forms-portal-handling-user-data}

[!DNL AEM Forms] -portalen innehåller komponenter som du kan använda för att lista adaptiva formulär, HTML5-formulär och andra Forms-resurser på [!DNL AEM Sites] sida. Dessutom kan du konfigurera den så att den visar utkast och skickade adaptiva formulär och HTML5-formulär för en inloggad användare. Mer information om formulärportalen finns i [Introduktion till att publicera formulär på en portal](/help/forms/using/introduction-publishing-forms.md).

När en inloggad användare sparar ett adaptivt formulär som ett utkast eller skickar det, visas de på flikarna Utkast och Skicka på formulärportalen. Data för ifyllda eller inskickade formulär lagras i datalagret som är konfigurerat för AEM. Utkast och inskickade data för anonyma användare visas inte på formulärportalsidan, men data lagras i det konfigurerade datalagret. Se [Konfigurera lagringstjänster för utkast och överföringar](/help/forms/using/configuring-draft-submission-storage.md).

## Användardata och datalager {#user-data-and-data-stores}

Forms portal lagrar data för utkast och inskickade formulär i följande scenarier:

* Skicka-åtgärden som konfigurerats i det adaptiva formuläret är **Forms Portal Submit Action**.
* För andra skicka-åtgärder än **Forms Portal Submit Action**, **[!UICONTROL Store data in forms portal]** är aktiverat i **[!UICONTROL Submission]** egenskaper för den adaptiva formulärbehållaren.

För varje utkast och skickat formulär för inloggade och anonyma användare lagras följande data i formulärportalen:

* Formulärmetadata som formulärnamn, formulärsökväg, utkast- eller överförings-ID, sökväg till bilagor och användar-ID
* Bifogade formulär som databyte
* Formulärdata som databyte

Beroende på den konfigurerade datalagringens beständighet lagras utkast och skickade formulärdata på följande platser.

<table>
 <tbody>
  <tr>
   <td><p><strong>Typ av beständighet</strong></p> </td>
   <td><p><strong>Datalager</strong></p> </td>
   <td><p><strong>Plats</strong></p> </td>
  </tr>
  <tr>
   <td><p>Standard</p> </td>
   <td><p>AEM databas med författare och publiceringsinstanser</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Fjärr</p> </td>
   <td><p>AEM databas med författare och AEM</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Databas</p> </td>
   <td><p>AEM databas för författarinstans och databastabeller</p> </td>
   <td>Databastabeller <code>data</code>, <code>metadata</code>och <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## Få åtkomst till och ta bort användardata {#access-and-delete-user-data}

Du kan komma åt formulärdata för inloggade och anonyma användare i konfigurerade datalager och vid behov ta bort dem.

### AEM instanser {#aem-instances}

Alla utkast och skickade formulärdata för AEM (författare, publicering eller fjärranvändare) för inloggade och anonyma användare lagras i `/content/forms/fp/` nod för tillämplig AEM. Varje gång en inloggad eller anonym användare sparar ett utkast eller skickar ett formulär är `draft ID` eller `submission ID`, a `user data ID`och en slumpmässig `ID` för varje bifogad fil (om tillämpligt) genereras. Det är kopplat till respektive utkast eller inlämning.

#### Åtkomst till användardata {#access-user-data}

När en inloggad användare sparar ett utkast eller skickar ett formulär skapas en underordnad nod med användar-ID:t. Till exempel utkast och data skickas för Sarah Rose vars användar-ID är `srose` lagras i `/content/forms/fp/srose/` nod i AEM. I användar-ID-noden ordnas data i en hierarkisk struktur.

I följande tabell förklaras hur data för alla utkast har `srose` lagras i AEM.

>[!NOTE]
>
>En exakt struktur som `drafts` replikeras för skickade formulär för `srose` under `/content/forms/fp/srose/submit/` nod.
>
>Alla utkast och inskickat material av `anonymous` -användare lagras under `/content/forms/fp/anonymous/` som organiserar utkast och inskickade data för alla anonyma användare under `draft` och `submit` noder.

| Nod | Beskrivning |
|---|---|
| `/content/forms/fp/srose/drafts` | Behållarnoddata för alla utkast av användaren |
| `/content/forms/fp/srose/drafts/attachments/` | Ordnar alla bilagor för användaren baserat på utkast-ID |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | Innehåller en bifogad fil för det valda ID:t i binärt format |
| `/content/forms/fp/srose/drafts/metadata/` | Ordnar formulärmetadata för användaren baserat på utkast-ID |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | Innehåller formulärmetadata för det valda utkast-ID:t |
| `/content/forms/fp/srose/drafts/data/` | Organiserar formulärdata för användaren baserat på användarens data-ID |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | Innehåller formulärdata för det valda användar-ID:t i binärt format |

#### Ta bort användardata {#delete-user-data}

Om du vill ta bort användardata från utkast och inskickade data för en inloggad användare från AEM system helt måste du ta bort `user ID` nod för en viss användare från författarnoden. Ta bort data manuellt från alla tillämpliga AEM.

Utkast och inlämningsdata för alla anonyma användare lagras i den gemensamma `drafts` och `submit` noder under `/content/forms/fp/anonymous`. Det finns ingen metod för att hitta data för en viss anonym användare om inte viss identifierbar information är känd. I det här fallet kan du söka efter information som identifierar den anonyma användaren i AEM och manuellt ta bort noden som innehåller den från alla tillämpliga AEM för att ta bort data från AEM. Om du vill ta bort data för alla anonyma användare kan du ta bort `anonymous` nod för att ta bort utkast och skicka data för alla anonyma användare.

### Databas {#database}

När AEM har konfigurerats för att lagra data i en databas lagras formulärportalutkast och överföringsdata i följande databastabeller för både inloggade och anonyma användare:

* data
* metadata
* extra metadata

#### Åtkomst till användardata {#access-user-data-1}

Kör följande databaskommando om du vill komma åt utkast och skicka data för en inloggad och anonym användare i databastabellerna. Ersätt `logged-in user` med det användar-ID vars data du vill komma åt eller med `anonymous` för anonyma användare.

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### Ta bort användardata {#delete-user-data-1}

Om du vill ta bort utkast och skicka data för en inloggad användare från databastabellerna kör du följande databaskommando. Ersätt `logged-in user` med det användar-ID vars data du vill ta bort eller med `anonymous` för anonyma användare. Om du vill ta bort data för en viss anonym användare från databasen måste du hitta dem med identifierbar information och ta bort dem från databastabeller som innehåller informationen.

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
