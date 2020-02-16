---
title: Konfigurera delade köer
seo-title: Konfigurera delade köer
description: Med delade köer kan du konfigurera och hantera användarköer effektivt. Lär dig hur du konfigurerar delade köer.
seo-description: Med delade köer kan du konfigurera och hantera användarköer effektivt. Lär dig hur du konfigurerar delade köer.
uuid: 69ab611d-334b-40a5-bd2d-533d4cb25eda
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc403a60-b635-4334-9bf8-2f3d2036b2f3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera delade köer{#configuring-shared-queues}

Med delade köer kan du konfigurera och hantera användarköer effektivt. En användarkö är helt enkelt alla uppgifter som tilldelats en användare. Mer information finns i [Att göra-listor](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) . Du kan tilldela, ta bort tilldelning och tilldela om användarköer beroende på organisationens behov. Du kan hantera delade köer på två sätt:

**Hantera åtkomst till en användare**

Du kan hantera åtkomsten till en vald användarkö med det här alternativet.

**Hantera åtkomst för en användare**

Med det här alternativet kan du hantera delade köer som tilldelats en vald användare.

## Hantera åtkomst till en vald användarkö {#managing-access-to-a-selected-user-queue}

Med funktionen Hantera åtkomst till en användare kan du hantera åtkomst till en vald användarkö. Du kan bevilja eller återkalla åtkomst till en vald användarkö för andra användare i organisationen. Kara Bowman är till exempel inte på kontoret. Med funktionen Hantera åtkomst till en användare kan hennes kö delas med Akira Tanaka och John Jacobs för slutförande. När Kara Bowman kommer tillbaka till kontoret senare kan du återkalla tillgången till hennes kö från Akira Tanaka och John Jacobs.

När uppgifterna har delats kan de utföras av användaren, med åtkomst till kön, med hjälp av arbetsytan.

>[!NOTE]
>
>Flex Workspace används inte i AEM-formulärsversioner.

### Konfigurera åtkomst till en vald användarkö {#configuring-access-to-a-selected-user-queue}

1. Logga in på administrationskonsolen med ett administratörskonto.
1. Välj **Tjänster** > **Formulärarbetsflöde** > **Delad kö**.

1. På fliken Hantera åtkomst till en användare söker du efter och markerar den användare vars kö du vill dela. I det nedre högra fönstret visas en lista med användare som har åtkomst till den valda användarkön.
1. Leta reda på och markera användaren i den nedre vänstra rutan. Klicka på Dela.
1. Klicka på Spara för att slutföra.

### Återkalla åtkomst till en vald användarkö {#revoking-access-to-a-selected-user-queue}

1. Logga in på administrationskonsolen med ett administratörskonto.
1. Välj **Tjänster** > **Formulärarbetsflöde** > **Delad kö**.

1. På fliken Hantera åtkomst till en användare söker du efter och markerar den användare vars kö du vill hantera.
1. I den nedre högra rutan visas en lista med användare som har åtkomst till den valda användarkön. Markera användaren och klicka på Återkalla.
1. Klicka på Spara för att slutföra.

## Hantera köer som tilldelats en användare {#managing-queues-assigned-to-a-user}

Med funktionen Hantera åtkomst av en användare kan du hantera köer som tilldelats en vald användare. Du kan bevilja eller återkalla åtkomst till användarköer för en vald användare individuellt. Du vill till exempel tilldela användarköerna Akira Tanaka och John Jacobs till Kara Bowman. Med funktionen Hantera åtkomst av en användare kan du söka efter Kara Bowman och ge åtkomst till uppgifter som tilldelats Akira Tanaka och John Jacobs. Vid ett senare tillfälle kan du återkalla Kara Bowmans åtkomst till dessa användarköer.

När användaren har tilldelats dessa uppgifter kan de slutföras med Workspace.

>[!NOTE]
>
>Flex Workspace används inte i AEM-formulärsversioner.

### Bevilja åtkomst till en vald användarkö {#granting-access-to-a-selected-user-queue}

1. Logga in på administrationskonsolen med ett administratörskonto.
1. Välj **Tjänster** > **Formulärarbetsflöde** > **Delad kö**.

1. På fliken Hantera åtkomst till en användare söker du efter och väljer den användare vars kö du vill dela. I det nedre högra fönstret visas en lista med användare som har åtkomst till den valda användarkön.
1. I den nedre vänstra rutan söker du efter och väljer användarköer som du vill dela med den valda användaren. Klicka på Dela.
1. Klicka på Spara för att slutföra.

### Återkalla åtkomst till en vald användarkö {#revoking_access_to_a_selected_user_queue-1}

1. Logga in på administrationskonsolen med ett administratörskonto.
1. Välj **Tjänster** > **Formulärarbetsflöde** > **Delad kö**.

1. På fliken Hantera åtkomst av en användare söker du efter och markerar den användare vars kö du vill hantera.
1. I den nedre högra rutan visas listan med användarköer som tilldelats den valda användaren. Markera användarkön och klicka på Återkalla.
1. Klicka på Spara för att slutföra.

