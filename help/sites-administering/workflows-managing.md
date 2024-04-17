---
title: Hantera åtkomst till arbetsflöden
description: Lär dig hur du konfigurerar åtkomstkontrollistor utifrån användarkonton så att du kan starta (eller inaktivera) och delta i arbetsflöden.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: cc54d637-d66c-49d2-99ee-00d96f1a74e0
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Hantera åtkomst till arbetsflöden{#managing-access-to-workflows}

Konfigurera åtkomstkontrollistor enligt användarkonton för att tillåta (eller inaktivera) start och deltagande i arbetsflöden.

## Nödvändiga användarbehörigheter för arbetsflöden {#required-user-permissions-for-workflows}

Åtgärder för arbetsflöden kan vidtas om

* du arbetar med `admin` konto
* kontot har tilldelats standardgruppen `workflow-users`:

   * den här gruppen innehåller alla behörigheter som krävs för att dina användare ska kunna utföra arbetsflödesåtgärder.
   * när kontot finns i den här gruppen har det bara tillgång till arbetsflöden som det har initierat.

* kontot har tilldelats standardgruppen `workflow-administrators`:

   * den här gruppen innehåller alla behörigheter som krävs för att dina behöriga användare ska kunna övervaka och administrera arbetsflöden.
   * när kontot finns i den här gruppen har det åtkomst till alla arbetsflöden.

>[!NOTE]
>
>Detta är minimikraven. Ditt konto måste också vara antingen tilldelad deltagare eller medlem i den tilldelade gruppen för att kunna vidta särskilda åtgärder.

## Konfigurera åtkomst till arbetsflöden {#configuring-access-to-workflows}

Arbetsflödesmodeller ärver en standardåtkomstkontrollista (ACL) som styr hur användare kan interagera med arbetsflöden. Om du vill anpassa användaråtkomst för ett arbetsflöde ändrar du åtkomstkontrollistan (ACL) i databasen för den mapp som innehåller arbetsflödesmodellnoden:

* [Använd en ACL för den specifika arbetsflödesmodellen på /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [Skapa en undermapp i /var/workflow/models och tillämpa ACL på den](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>Mer information om hur du konfigurerar åtkomstkontrollistor i CRXDE Lite finns i [Behörighetshantering](/help/sites-administering/user-group-ac-admin.md#access-right-management).

### Använd en ACL för den specifika arbetsflödesmodellen på /var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

Om arbetsflödesmodellen lagras i `/var/workflow/models`kan du tilldela en specifik åtkomstkontrollista som är relevant endast för det arbetsflödet till mappen:

1. Öppna CRXDE Lite i webbläsaren (till exempel [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. I nodträdet väljer du noden för mappen för arbetsflödesmodeller:

   `/var/workflow/models`

1. Klicka på **Åtkomstkontroll** -fliken.
1. I **Principer för lokal åtkomstkontroll** (**Åtkomstkontrollista**) klickar du på plusikonen för att **Lägg till post**.
1. I **Lägg till nytt inlägg** lägger du till en ACE med följande egenskaper:

   * **kapitalbelopp**: `content-authors`
   * **Typ**: `Deny`
   * **Behörighet**: `jcr:read`
   * **rep:glob**: referens till arbetsflödet

   ![wf-108](assets/wf-108.png)

   The **Åtkomstkontrollista** tabellen innehåller nu en begränsning för `content-authors` på `prototype-wfm-01` arbetsflödesmodell.

   ![wf-109](assets/wf-109.png)

1. Klicka **Spara alla**.

   The `prototype-wfm-01` arbetsflödet är inte längre tillgängligt för medlemmar i `content-authors` grupp.

### Skapa en undermapp i /var/workflow/models och tillämpa ACL på den {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

Dina [utvecklarteamet kan skapa arbetsflöden i en undermapp](/help/sites-developing/workflows-models.md#creating-a-new-workflow) av

`/var/workflow/models`

Jämfört med arbetsflödena för DAM som lagras under

`/var/workflow/models/dam/`

Du kan sedan lägga till en ACL i själva mappen.

1. Öppna CRXDE Lite i webbläsaren (till exempel [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. I nodträdet väljer du noden för den enskilda mappen i mappen för arbetsflödesmodeller, till exempel:

   `/var/workflow/models/prototypes`

1. Klicka på **Åtkomstkontroll** -fliken.
1. I **Tillämplig åtkomstkontrollprincip** tabell klickar du på plusikonen för att **Lägg till** ett bidrag.
1. I **Principer för lokal åtkomstkontroll** (**Åtkomstkontrollista**) klickar du på plusikonen för att **Lägg till post**.
1. I **Lägg till nytt inlägg** lägger du till en ACE med följande egenskaper:

   * **kapitalbelopp**: `content-authors`
   * **Typ**: `Deny`
   * **Behörighet**: `jcr:read`

   >[!NOTE]
   >
   >Som med [Använd en ACL för den specifika arbetsflödesmodellen på /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models) du kan ta med en rep:glob för att begränsa åtkomsten till ett visst arbetsflöde.

   ![wf-110](assets/wf-110.png)

   The **Åtkomstkontrollista** tabellen innehåller nu en begränsning för `content-authors` på `prototypes` mapp.

   ![wf-111](assets/wf-111.png)

1. Klicka **Spara alla**.

   Modellerna i `prototypes` mappen inte längre är tillgänglig för medlemmar i `content-authors` grupp.
