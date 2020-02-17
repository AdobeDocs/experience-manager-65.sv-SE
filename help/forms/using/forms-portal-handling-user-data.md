---
title: Formulärportal| Hantera användardata
seo-title: Formulärportal| Hantera användardata
description: 'null'
seo-description: 'null'
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Formulärportal| Hantera användardata {#forms-portal-handling-user-data}

AEM Forms-portalen innehåller komponenter som du kan använda för att lista adaptiva formulär, HTML5-formulär och andra formulärresurser på sidan AEM Sites. Dessutom kan du konfigurera den så att den visar utkast och skickade adaptiva formulär och HTML5-formulär för en inloggad användare. Mer information om formulärportalen finns i [Introduktion till att publicera formulär på en portal](/help/forms/using/introduction-publishing-forms.md).

När en inloggad användare sparar ett adaptivt formulär som utkast eller skickar det, visas de på flikarna Utkast och Skicka på formulärportalen. Data för utkast eller skickade formulär lagras i datalagret som konfigurerats för AEM-distribution. Utkasten och inskickade förslag från anonyma användare visas inte på portalsidan för formulär. data lagras dock i det konfigurerade datalagret. Mer information finns i [Konfigurera lagringstjänster för utkast och överföringar](/help/forms/using/configuring-draft-submission-storage.md).

## Användardata och datalager {#user-data-and-data-stores}

Formulärportalen lagrar data för utkast och skickade formulär i följande scenarier:

* Den skicka-åtgärd som har konfigurerats i det adaptiva formuläret är **Forms Portal Submit Action**.
* För andra skicka-åtgärder än **Forms Portal Submit Action**, aktiveras alternativet **[!UICONTROL Lagra data i formulärportalen]** i **överföringsegenskaperna** för den adaptiva formulärbehållaren.

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
   <td><p>AEM-databas med författare och publiceringsinstanser</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Fjärr</p> </td>
   <td><p>AEM-databas med författare och fjärr-AEM-instanser</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Databas</p> </td>
   <td><p>AEM-databas med författarinstanser och databastabeller</p> </td>
   <td>Databastabeller <code>data</code>, <code>metadata</code>och <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## Få åtkomst till och ta bort användardata {#access-and-delete-user-data}

Du kan komma åt formulärdata för inloggade och anonyma användare i konfigurerade datalager och ta bort dem om det behövs.

### AEM-instanser {#aem-instances}

Alla utkast och skickade formulärdata i AEM-instanser (författare, publicering eller fjärranvändare) för inloggade och anonyma användare lagras i noden `/content/forms/fp/` i den tillämpliga AEM-databasen. Varje gång en inloggad eller anonym användare sparar ett utkast eller skickar ett formulär, ett formulär `draft ID` eller `submission ID`, ett `user data ID`och ett slumpmässigt `ID` för varje bifogad fil (om tillämpligt) genereras, vilket är associerat med respektive utkast eller inskickat material.

#### Åtkomst till användardata {#access-user-data}

När en inloggad användare sparar ett utkast eller skickar ett formulär skapas en underordnad nod med användar-ID:t. Till exempel gör utkast och skickar data för Sarah Rose vars användar-ID `srose` lagras i `/content/forms/fp/srose/` noden i AEM-databasen. I användar-ID-noden ordnas data i en hierarkisk struktur.

Tabellen nedan förklarar hur data för alla utkast som `srose` lagras i AEM-databasen.

>[!NOTE]
>
>En exakt struktur som `drafts` replikeras för skickade formulär `srose` under `/content/forms/fp/srose/submit/` noden.
>
>Alla utkast och inskickade förslag från `anonymous` användare lagras under `/content/forms/fp/anonymous/` noden, som organiserar utkast och inskickade data för alla anonyma användare under `draft` - och `submit` -noderna.

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

Om du vill ta bort användardata från utkast och inskickade data för en inloggad användare från AEM-system helt och hållet, måste du ta bort noden för en viss användare från författarnoden `user ID` . Du måste ta bort data manuellt från alla tillämpliga AEM-instanser.

Utkast och inlämningsdata för alla anonyma användare lagras i de gemensamma `drafts` noderna och `submit` noderna under `/content/forms/fp/anonymous`. Det finns ingen metod för att hitta data för en viss anonym användare såvida inte viss identifierbar information är känd.I det här fallet kan du söka efter information som identifierar den anonyma användaren i AEM-databasen och manuellt ta bort noden som innehåller den från alla tillämpliga AEM-instanser för att ta bort data från AEM-systemet. Om du vill ta bort data för alla anonyma användare kan du ta bort noden för att ta bort utkast och skicka data för alla anonyma användare. `anonymous`

### Databas {#database}

När AEM är konfigurerat för att lagra data i en databas lagras formulärportalutkast och överföringsdata i följande databastabeller för både inloggade och anonyma användare:

* data
* metadata
* extra metadata

#### Åtkomst till användardata {#access-user-data-1}

Kör följande databaskommando om du vill komma åt utkast och skicka data för inloggade och anonyma användare i databastabellerna. Ersätt i frågan `logged-in user` med det användar-ID vars data du vill få åtkomst till eller med `anonymous` för anonyma användare.

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### Ta bort användardata {#delete-user-data-1}

Om du vill ta bort utkast och skicka data för en inloggad användare från databastabellerna kör du följande databaskommando. Ersätt i frågan `logged-in user` med det användar-ID vars data du vill ta bort eller med `anonymous` för anonyma användare. Observera att om du vill ta bort data för en viss anonym användare från databasen måste du söka efter dem med hjälp av identifierbar information och ta bort dem från databastabeller som innehåller informationen.

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```

