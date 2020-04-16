---
title: Skicka en bekräftelse på att formulär har skickats via e-post
seo-title: Skicka en bekräftelse på att formulär har skickats via e-post
description: Med AEM Forms kan du konfigurera e-poståtgärden som skickar en bekräftelse till en användare när formuläret skickas.
seo-description: Med AEM Forms kan du konfigurera e-poståtgärden som skickar en bekräftelse till en användare när formuläret skickas.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
translation-type: tm+mt
source-git-commit: acc2a3977353386d7e1dfd1344a61d78812fe3fc

---


# Skicka en bekräftelse på att formulär har skickats via e-post {#sending-a-form-submission-acknowledgement-via-email}

## Anpassad inlämning av formulärdata {#adaptive-form-data-submission}

Adaptiva formulär innehåller flera färdiga arbetsflöden för att [skicka formulärdata till olika slutpunkter](../../forms/using/configuring-submit-actions.md) .

Åtgärden **[!UICONTROL Skicka e-post]** skickar till exempel ett e-postmeddelande när ett anpassat formulär har skickats. Den kan även konfigureras för att skicka formulärdata och PDF-filen i e-postmeddelandet.

I den här artikeln beskrivs stegen för att aktivera e-poståtgärden för ett anpassat formulär och olika konfigurationer som tillhandahålls.

>[!NOTE]
>
>Du kan också använda alternativet **[!UICONTROL Skicka PDF via e-post]** för att skicka det ifyllda formuläret via e-post som en bifogad PDF-fil. De konfigurationsalternativ som är tillgängliga för den här åtgärden är samma som de alternativ som är tillgängliga för åtgärden **[!UICONTROL Skicka e-post]** . Åtgärden E-post-PDF är bara tillgänglig för XFA-baserade adaptiva formulär

## Skicka e-poståtgärd {#email-action}

Med åtgärden Skicka e-post kan en författare automatiskt skicka e-post till en eller flera mottagare när ett anpassat formulär har skickats.

>[!NOTE]
>
>Om du vill använda åtgärden Skicka e-post måste du konfigurera AEM-e-posttjänsten enligt beskrivningen i [Konfigurera e-posttjänsten](/help/sites-administering/notification.md#configuring-the-mail-service).

### Aktivera åtgärden Skicka e-post i ett anpassat formulär {#enabling-email-action-on-an-adaptive-form}

1. Öppna ett anpassat formulär i **[!UICONTROL redigeringsläge]** .

1. På fliken **[!UICONTROL Innehåll]** trycker du på **[!UICONTROL Formulärbehållare]** och sedan på ![Konfigurera](assets/configure-icon.svg) för att visa de adaptiva formuläregenskaperna.

1. I delen **[!UICONTROL Skicka]** väljer du **[!UICONTROL Skicka e-post]** i **[!UICONTROL listrutan]** Skicka åtgärd.

   ![Skicka funktionsmakron](assets/submission-actions.png)

1. Ange giltiga e-post-ID:n i fälten **[!UICONTROL Till]**, **[!UICONTROL CC]** och **[!UICONTROL BCC]** .

   Ange ämne och brödtext för e-postmeddelandet i fälten **[!UICONTROL Ämne]** och **[!UICONTROL E-postmall]** .

   Du kan också ange variabelplatshållare i fälten. I så fall bearbetas fältvärdena när formuläret har skickats av en slutanvändare. Mer information finns i [Använda adaptiva formulärfältsnamn för att dynamiskt skapa e-postinnehåll](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Markera **[!UICONTROL Inkludera bifogade filer]** om formuläret innehåller bifogade filer och du vill bifoga dessa filer i e-postmeddelandet.

   >[!NOTE]
   >
   >Om du väljer alternativet **[!UICONTROL Skicka PDF via e-post]** måste du markera alternativet Inkludera bilagor.

1. Click ![save](assets/save_icon.svg) to save the changes.

### Använda adaptiva formulärfältsnamn för att dynamiskt skapa e-postinnehåll {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Fältnamnen i ett adaptivt formulär kallas platshållare som ersätts med värdet i det fältet när användaren skickar formuläret.

I åtgärden **[!UICONTROL Skicka e-post]** kan du använda platshållare som bearbetas när åtgärden utförs. Det innebär att rubrikerna i e-postmeddelandet (till exempel **[!UICONTROL Till]**, **[!UICONTROL CC]**, **[!UICONTROL Hemlig kopia]** och **[!UICONTROL Ämne]**) genereras när användaren skickar formuläret.

Om du vill definiera en platshållare anger du `${<field name>}` i ett fält efter att du har valt **[!UICONTROL Skicka e-post]** som Skicka-åtgärd.

Om formuläret till exempel innehåller fältet **[!UICONTROL E-postadress]** , med namnet `email_addr`, för att hämta användarens e-post-ID, kan du ange följande i fälten **[!UICONTROL Till]**, **[!UICONTROL CC]** eller **[!UICONTROL Hemlig kopia]** .

`${email_addr}`

När en användare skickar formuläret skickas ett e-postmeddelande till det e-post-ID som har angetts i formulärfältet `email_addr` .

>[!NOTE]
>
>Du hittar namnet på ett fält i dialogrutan **[!UICONTROL Redigera]** för fältet.

Variabelplatshållare kan också användas i fälten **[!UICONTROL Ämne]** och **[!UICONTROL E-postmall]** .

Exempel:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Fält i upprepningsbara paneler kan inte användas som variabla platshållare.

