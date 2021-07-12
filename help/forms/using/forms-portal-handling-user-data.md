---
title: Forms Portal | Hantera användardata
seo-title: Forms Portal | Hantera användardata
description: Forms Portal | Hantera användardata
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
role: Admin
exl-id: 791524a4-a8bb-4632-a68d-e96864e139a9
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# Forms Portal | Hantera användardata {#forms-portal-handling-user-data}

[!DNL AEM Forms] portal innehåller komponenter som du kan använda för att lista adaptiva formulär, HTML5-formulär och andra Forms-resurser på  [!DNL AEM Sites] sidan. Dessutom kan du konfigurera den så att den visar utkast och skickade adaptiva formulär och HTML5-formulär för en inloggad användare. Mer information om formulärportalen finns i [Introduktion till att publicera formulär på en portal](/help/forms/using/introduction-publishing-forms.md).

När en inloggad användare sparar ett adaptivt formulär som utkast eller skickar det, visas de på flikarna Utkast och Skicka på formulärportalen. Data för utkast eller skickade formulär lagras i datalagret som konfigurerats för AEM distribution. Utkasten och inskickade förslag från anonyma användare visas inte på portalsidan för formulär. data lagras dock i det konfigurerade datalagret. Mer information finns i [Konfigurera lagringstjänster för utkast och överföringar](/help/forms/using/configuring-draft-submission-storage.md).

## Användardata och datalager {#user-data-and-data-stores}

Forms portal lagrar data för utkast och inskickade formulär i följande scenarier:

* Skicka-åtgärden som konfigurerats i det adaptiva formuläret är **Forms Portal Submit Action**.
* För andra skicka-åtgärder än **Forms Portal Submit Action** aktiveras alternativet **[!UICONTROL Store data in forms portal]** i **[!UICONTROL Submission]**-egenskaperna för den adaptiva formulärbehållaren.

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
   <td>Databastabeller <code>data</code>, <code>metadata</code> och <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## Få åtkomst till och ta bort användardata {#access-and-delete-user-data}

Du kan komma åt formulärdata för inloggade och anonyma användare i konfigurerade datalager och ta bort dem om det behövs.

### AEM {#aem-instances}

Alla utkast och skickade formulärdata i AEM instanser (författare, publicering eller fjärranvändare) för inloggade och anonyma användare lagras i noden `/content/forms/fp/` i den tillämpliga AEM. Varje gång en inloggad eller anonym användare sparar ett utkast eller skickar ett formulär, genereras ett `draft ID` eller `submission ID`, ett `user data ID` och ett slumpmässigt `ID` för varje bifogad fil (om tillämpligt), som associeras med respektive utkast eller sändning.

#### Åtkomst till användardata {#access-user-data}

När en inloggad användare sparar ett utkast eller skickar ett formulär skapas en underordnad nod med användar-ID:t. Till exempel lagras utkast och data för Sarah Rose vars användar-ID är `srose` i noden `/content/forms/fp/srose/` i AEM. I användar-ID-noden ordnas data i en hierarkisk struktur.

I följande tabell förklaras hur data för alla utkast av `srose` lagras i AEM.

>[!NOTE]
>
>En exakt struktur som `drafts` replikeras för skickade formulär för `srose` under noden `/content/forms/fp/srose/submit/`.
>
>Alla utkast och inskickade data från `anonymous`-användare lagras under noden `/content/forms/fp/anonymous/`, som organiserar utkast och inskickade data för alla anonyma användare under noderna `draft` och `submit`.

| Nod | Beskrivning |
|---|---|
| `/content/forms/fp/srose/drafts` | Behållarnoddata för alla utkast av användaren |
| `/content/forms/fp/srose/drafts/attachments/` | Ordnar alla bilagor för användaren baserat på utkast-ID |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | Innehåller bilaga för det valda ID:t i binärt format |
| `/content/forms/fp/srose/drafts/metadata/` | Ordnar formulärmetadata för användaren baserat på utkast-ID |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | Innehåller formulärmetadata för det valda utkast-ID:t |
| `/content/forms/fp/srose/drafts/data/` | Organiserar formulärdata för användaren baserat på användarens data-ID |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | Innehåller formulärdata för det valda användar-ID:t i binärt format |

#### Ta bort användardata {#delete-user-data}

Om du vill ta bort användardata från utkast och överföringar för en inloggad användare från AEM system helt måste du ta bort noden `user ID` för en viss användare från författarnoden. Du måste ta bort data manuellt från alla tillämpliga AEM.

Utkast och inskickningsdata för alla anonyma användare lagras i de gemensamma `drafts`- och `submit`-noderna under `/content/forms/fp/anonymous`. Det finns ingen metod för att hitta data för en viss anonym användare om inte viss identifierbar information är känd. I det här fallet kan du söka efter information som identifierar den anonyma användaren i AEM och manuellt ta bort noden som innehåller den från alla tillämpliga AEM för att ta bort data från AEM. Om du vill ta bort data för alla anonyma användare kan du ta bort noden `anonymous` och ta bort utkast och skickade data för alla anonyma användare.

### Databas {#database}

När AEM har konfigurerats för att lagra data i en databas lagras formulärportalutkast och överföringsdata i följande databastabeller för både inloggade och anonyma användare:

* data
* metadata
* extra metadata

#### Åtkomst till användardata {#access-user-data-1}

Kör följande databaskommando om du vill komma åt utkast och skicka data för inloggade och anonyma användare i databastabellerna. I frågan ersätter du `logged-in user` med det användar-ID vars data du vill komma åt eller med `anonymous` för anonyma användare.

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### Ta bort användardata {#delete-user-data-1}

Om du vill ta bort utkast och skicka data för en inloggad användare från databastabellerna kör du följande databaskommando. I frågan ersätter du `logged-in user` med det användar-ID vars data du vill ta bort eller med `anonymous` för anonyma användare. Observera att om du vill ta bort data för en viss anonym användare från databasen måste du söka efter dem med hjälp av identifierbar information och ta bort dem från databastabeller som innehåller informationen.

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
