---
title: Skicka en bekräftelse på att formulär har skickats via e-post
seo-title: Sending a form submission acknowledgement via email
description: Med AEM Forms kan du konfigurera e-poståtgärden som skickar en bekräftelse till en användare när formuläret skickas.
seo-description: AEM Forms lets you configure the email submit action that sends an acknowledgement to a user on submitting the form.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Skicka en bekräftelse på att formulär har skickats via e-post {#sending-a-form-submission-acknowledgement-via-email}

## Anpassad inlämning av formulärdata {#adaptive-form-data-submission}

Adaptiva formulär har flera färdiga funktioner [skicka funktionsmakron](../../forms/using/configuring-submit-actions.md) arbetsflöden för att skicka formulärdata till olika slutpunkter.

Till exempel **[!UICONTROL Send email]** skicka ett e-postmeddelande när ett anpassat formulär har skickats. Den kan även konfigureras för att skicka formulärdata och PDF i e-postmeddelandet.

I den här artikeln beskrivs stegen för att aktivera e-poståtgärden för ett anpassat formulär och olika konfigurationer som tillhandahålls.

>[!NOTE]
>
>Du kan också använda **[!UICONTROL Send PDF via email]** möjlighet att skicka det ifyllda formuläret via e-post som en bifogad fil i PDF. Konfigurationsalternativen som är tillgängliga för den här åtgärden är samma som de alternativ som är tillgängliga för **[!UICONTROL Send email]** åtgärd. Åtgärden Email PDF är bara tillgänglig för XFA-baserade adaptiva formulär

## Skicka e-poståtgärd {#email-action}

Med åtgärden Skicka e-post kan en författare automatiskt skicka e-post till en eller flera mottagare när ett anpassat formulär har skickats.

>[!NOTE]
>
>Om du vill använda åtgärden Skicka e-post måste du konfigurera tjänsten AEM e-post enligt beskrivningen i [Konfigurera e-posttjänsten](/help/sites-administering/notification.md#configuring-the-mail-service).

### Aktivera åtgärden Skicka e-post i ett anpassat formulär {#enabling-email-action-on-an-adaptive-form}

1. Öppna ett anpassat formulär i **[!UICONTROL edit]** läge.

1. I **[!UICONTROL Content]** flik, välja **[!UICONTROL Form Container]** och markera ![konfigurera](assets/configure-icon.svg) för att visa anpassade formuläregenskaper.

1. I **[!UICONTROL Submission]** avsnitt, markera **[!UICONTROL Send email]** från **[!UICONTROL Submit Action]** listruta.

   ![Skicka funktionsmakron](assets/submission-actions.png)

1. Ange giltiga e-post-ID i **[!UICONTROL To]**, **[!UICONTROL CC]** och **[!UICONTROL BCC]** fält.

   Ange ämne och brödtext för e-postmeddelandet i dialogrutan **[!UICONTROL Subject]** och **[!UICONTROL Email Template]** fält.

   Du kan också ange variabelplatshållare i fälten. I så fall bearbetas fältvärdena när formuläret har skickats av en slutanvändare. Mer information finns i [Använda adaptiva formulärfältsnamn för att dynamiskt skapa e-postinnehåll](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Välj **[!UICONTROL Include attachments]** om formuläret innehåller bifogade filer och du vill bifoga dessa filer i e-postmeddelandet.

   >[!NOTE]
   >
   >Om du väljer **[!UICONTROL Send PDF via Email]** måste du markera alternativet Inkludera bifogade filer.

1. Klicka ![spara](assets/save_icon.svg) för att spara ändringarna.

### Använda adaptiva formulärfältsnamn för att dynamiskt skapa e-postinnehåll {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Fältnamnen i ett adaptivt formulär kallas platshållare som ersätts med värdet i det fältet när användaren skickar formuläret.

I **[!UICONTROL Send email]** kan du använda platshållare som bearbetas när åtgärden utförs. Det betyder att e-postens rubriker (som **[!UICONTROL To]**, **[!UICONTROL CC]**, **[!UICONTROL BCC]**, **[!UICONTROL Subject]**) genereras när användaren skickar formuläret.

Om du vill definiera en platshållare anger du `${<field name>}` i ett fält efter markering **[!UICONTROL Send email]** som Skicka-åtgärd.

Om formuläret till exempel innehåller **[!UICONTROL Email address]** fält, namngivna `email_addr`för att hämta användarens e-post-ID kan du ange följande i **[!UICONTROL To]**, **[!UICONTROL CC]**, eller **[!UICONTROL BCC]** fält.

`${email_addr}`

När en användare skickar formuläret skickas ett e-postmeddelande till det e-post-ID som anges i `email_addr` formulärfält.

>[!NOTE]
>
>Du hittar namnet på ett fält i **[!UICONTROL Edit]** för fältet.

Variabelplatshållare kan också användas i **[!UICONTROL Subject]** och **[!UICONTROL Email Template]** fält.

Till exempel:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Fält i upprepningsbara paneler kan inte användas som variabla platshållare.
