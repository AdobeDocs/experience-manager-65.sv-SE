---
title: Koppla granskare som skickar in svar till ett formulär
seo-title: Koppla granskare som skickar in svar till ett formulär
description: Lär dig hur du associerar granskare med ett formulär i AEM Forms. Associerade granskare granskar ett formulär som skickats via formulärportalen.
seo-description: Lär dig hur du associerar granskare med ett formulär i AEM Forms. Associerade granskare granskar ett formulär som skickats via formulärportalen.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# Koppla granskare som skickar in svar till ett formulär {#associating-submission-reviewers-with-a-form}

När du skapar ett formulär kan du ange vilka användare som ska granska inskickade formulär via formulärportalen och ge feedback. Din organisation kan samla in feedback och omarbeta de inskickade formulären.

Med AEM Forms kan du associera en granskargrupp med ett formulär. Användare som läggs till i en granskningsgrupp i ett formulär kan se inskickade formulär och ge feedback.

Granskningsgrupper som tilldelats ett formulär kan bara granska inskickade svar från det angivna formuläret.

## Förutsättning {#prerequisite}

### Aktiverar gruppegenskap för inskickande granskare för adaptiva formulär med metadataschemats redigerare {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

Om du vill associera en granskargrupp med ett formulär redigerar du metadatarammet för anpassningsbara formulär. Som standard kan du inte lägga till en granskningsgrupp i ett skickat formulär.

Så här redigerar du metadataschema:

1. I redigeringsläget, under Experience Manager, klickar du på **Verktyg** > **Resurser** > **Metadata Schemas**.
1. Gå till **Forms** > **Forms Skapat i AEM.**

   Sidans URL är:

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. Välj **Anpassat formulär** och klicka på **Redigera**.
1. Klicka på **Avancerat** på sidan Redigera formulär.
1. Dra och släpp komponenten **Single Line Text** under Build Form (Skapa formulär) på fliken Avancerat.
1. Markera den tillagda textkomponenten för att se dess inställningar.

   Under Inställningar anger du `./jcr:content/metadata/form-submission-reviewer-group` i fältet Mappa till egenskap.

   Fältet för gruppen Skicka granskare i de avancerade egenskaperna för ditt adaptiva formulär aktiveras med det namn du anger under Fältetikett.

## Koppla granskare som skickar in svar till ett formulär {#associating-submission-reviewers-with-a-form-1}

Om du vill associera granskare med ett anpassat formulär skapar du en granskargrupp och lägger till användare. Lägg till den skapade granskargruppen under fältet för att skicka in formulär i formulärets avancerade egenskaper.
Med användargrupper kan du associera olika uppsättningar av granskare med olika anpassningsbara formulär. Den här funktionen förhindrar att obehöriga skickar in granskningar.

Innan du utför följande steg ska du läsa [Krav](../../forms/using/adding-reviewers-form.md#prerequisite).

Om du vill skapa en grupp och lägga till medlemmar i den går du till **Verktyg** > **Åtgärder** > **Säkerhet** > **Grupper**.
Mer information finns i [Användaradministration och -tjänster](/help/sites-administering/security.md).
Se till att du lägger till gruppen som du skapar som medlem i den körklara användargruppen: **forms-submit-reviewers**. Den här användargruppen levereras med AEM Forms och ser till att användare läggs till som granskare.

Så här associerar du användargrupper med ett anpassat formulär:

1. I redigeringsläget går du till **Forms** > **Forms &amp; Documents**.
1. Använd alternativet **Välj **för att välja ett anpassat formulär och klicka på **Visa egenskaper**.
1. Klicka på **Redigera** i fönstret Egenskaper för formuläret och klicka sedan på **ADVANCED**.
1. Ange gruppen i gruppfältet för granskare som ska skicka in och klicka på **Klar**.

   Fältet för granskningsgruppen som ska skickas visas med det namn som du angav i det redigerade metadataschemat för anpassade formulär.

>[!NOTE]
>
>Replikera användare och formulär för att säkerställa att de är tillgängliga för användare och formulär vid fjärrimplementeringen av AEM Forms.
>
>Se till att alla användare replikeras som granskningsmedlemmar i användargrupperna i fjärrimplementeringen.

