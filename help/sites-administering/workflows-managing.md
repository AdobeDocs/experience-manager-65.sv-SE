---
title: Hantera åtkomst till arbetsflöden
seo-title: Hantera åtkomst till arbetsflöden
description: Lär dig hur du hanterar åtkomst till arbetsflöden.
seo-description: Lär dig hur du hanterar åtkomst till arbetsflöden.
uuid: 58f79b89-fe56-4565-a869-8179c1ac68de
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5150867a-02a9-45c9-b2fd-e536b60ffa8c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Hantera åtkomst till arbetsflöden{#managing-access-to-workflows}

Konfigurera åtkomstkontrollistor enligt användarkonton för att tillåta (eller inaktivera) start och deltagande i arbetsflöden.

## Nödvändiga användarbehörigheter för arbetsflöden {#required-user-permissions-for-workflows}

Åtgärder för arbetsflöden kan vidtas om

* du arbetar med `admin` kontot
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
>Mer information om hur du använder CRXDE Lite för att konfigurera åtkomstkontrollistor finns i [Åtkomsträttshantering](/help/sites-administering/user-group-ac-admin.md#access-right-management).

### Använd en ACL för den specifika arbetsflödesmodellen på /var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

Om arbetsflödesmodellen lagras i `/var/workflow/models` kan du tilldela en specifik åtkomstkontrollista som är relevant endast för det arbetsflödet till mappen:

1. Öppna CRXDE Lite i webbläsaren (till exempel [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. I nodträdet väljer du noden för mappen för arbetsflödesmodeller:

   `/var/workflow/models`

1. Klicka på fliken **Åtkomstkontroll** .
1. I tabellen **Local Access Control Policies** (**Access Control List**) klickar du på plusikonen för att **lägga till post**.
1. I dialogrutan **Lägg till nytt inlägg** lägger du till en ny ACE med följande egenskaper:

   * **Huvudkonto**: `content-authors`
   * **Typ**: `Deny`
   * **Behörigheter**: `jcr:read`
   * **rep:glob**: referens till det specifika arbetsflödet
   ![wf-108](assets/wf-108.png)

   Registret **Åtkomstkontrollista** innehåller nu begränsningen för `content-authors` i `prototype-wfm-01` arbetsflödesmodellen.

   ![wf-109](assets/wf-109.png)

1. Klicka på **Spara alla**.

   Arbetsflödet är inte längre `prototype-wfm-01` tillgängligt för medlemmar i `content-authors` gruppen.

### Skapa en undermapp i /var/workflow/models och tillämpa ACL på den {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

Utvecklingsteamet kan [skapa arbetsflödena i en undermapp](/help/sites-developing/workflows-models.md#creating-a-new-workflow) i

`/var/workflow/models`

Jämfört med arbetsflödena för DAM som lagras under

`/var/workflow/models/dam/`

Du kan sedan lägga till en ACL i själva mappen.

1. Öppna CRXDE Lite i webbläsaren (till exempel [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. I nodträdet väljer du noden för den enskilda mappen i mappen för arbetsflödesmodeller. till exempel:

   `/var/workflow/models/prototypes`

1. Klicka på fliken **Åtkomstkontroll** .
1. Klicka på plusikonen i tabellen **Tillämplig åtkomstkontrollprincip** för att **lägga till** en post.
1. I tabellen **Local Access Control Policies** (**Access Control List**) klickar du på plusikonen för att **lägga till post**.
1. I dialogrutan **Lägg till nytt inlägg** lägger du till en ny ACE med följande egenskaper:

   * **Huvudkonto**: `content-authors`
   * **Typ**: `Deny`
   * **Behörigheter**: `jcr:read`
   >[!NOTE]
   >
   >Precis som med [Tillämpa en åtkomstkontrollista för den specifika arbetsflödesmodellen på /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models) kan du inkludera en rep:glob för att begränsa åtkomsten till ett visst arbetsflöde.

   ![wf-110](assets/wf-110.png)

   Registret **Åtkomstkontrollista** innehåller nu begränsningen för `content-authors` mappen `prototypes` .

   ![wf-111](assets/wf-111.png)

1. Klicka på **Spara alla**.

   Modellerna i `prototypes` mappen är inte längre tillgängliga för medlemmar i `content-authors` gruppen.

