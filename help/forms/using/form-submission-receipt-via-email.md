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
source-git-commit: 94472fad34fe97740e4711d2cb35beb884db52ce

---


# Skicka en bekräftelse på att formulär har skickats via e-post{#sending-a-form-submission-acknowledgement-via-email}

## Anpassad inlämning av formulärdata {#adaptive-form-data-submission}

Adaptiva formulär innehåller flera färdiga arbetsflöden för att [skicka formulärdata till olika slutpunkter](../../forms/using/configuring-submit-actions.md) .

Åtgärden Skicka **e-post** skickar till exempel ett e-postmeddelande när ett anpassat formulär har skickats. Den kan även konfigureras för att skicka formulärdata och PDF-filen i e-postmeddelandet.

I den här artikeln beskrivs stegen för att aktivera e-poståtgärden för ett anpassat formulär och olika konfigurationer som tillhandahålls.

>[!NOTE]
>
>Du kan också använda åtgärden **E-** post-PDF för att skicka det ifyllda formuläret via e-post som en bifogad PDF-fil. Konfigurationsalternativen som är tillgängliga för den här åtgärden är samma som alternativen som är tillgängliga för åtgärden E-post. Åtgärden E-post-PDF är bara tillgänglig för XFA-baserade adaptiva formulär

## E-poståtgärd {#email-action}

Med åtgärden E-post kan en författare automatiskt skicka e-post till en eller flera mottagare när ett anpassat formulär har skickats.

>[!NOTE]
>
>Om du vill använda åtgärden E-post måste du konfigurera AEM-posttjänsten enligt beskrivningen i [Konfigurera e-posttjänsten](/help/sites-administering/notification.md#configuring the mail service).

### Aktivera e-poståtgärd i ett anpassat formulär {#enabling-email-action-on-an-adaptive-form}

1. Öppna ett anpassat formulär i redigeringsläge.

1. Klicka på **Redigera** bredvid **Början av verktygsfältet Adaptivt formulär** .

   Dialogrutan Redigera komponent öppnas.

   ![Redigera komponentdialogruta för ett anpassat formulär](assets/start_of_adp_form.png)

1. Välj fliken **Skicka-åtgärder** och välj **E-poståtgärd** i listrutan Skicka-åtgärd.

   Fliken visar alternativen för att konfigurera åtgärden E-post för det aktuella formuläret.

   ![Fliken Skicka åtgärder](assets/dialog.png)

1. Ange giltiga e-post-ID:n i fälten Mailto, CC och BCC.

   Ange ämne och e-postmeddelandets brödtext i fälten Ämne och E-postmall.

   Du kan också ange variabelplatshållare i fälten. I så fall bearbetas fältvärdena när formuläret har skickats av en slutanvändare. Mer information finns i [Använda adaptiva formulärfältsnamn för att dynamiskt skapa e-postinnehåll](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Markera Inkludera bifogade filer om formuläret innehåller bifogade filer och du vill bifoga dessa filer i e-postmeddelandet.

   >[!NOTE]
   >
   >Om du väljer åtgärden **** E-post-PDF måste du markera alternativet Inkludera bifogade filer.

1. Spara ändringarna genom att klicka på **OK** .

### Använda adaptiva formulärfältsnamn för att dynamiskt skapa e-postinnehåll {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Fältnamnen i ett adaptivt formulär kallas platshållare som ersätts med värdet i det fältet när användaren skickar formuläret.

På fliken E-poståtgärd kan du använda platshållare som bearbetas när åtgärden utförs. Det innebär att rubrikerna i e-postmeddelandet (som Mailto, CC, BCC, subject) genereras när användaren skickar formuläret.

Om du vill definiera en platshållare anger du `${<field name>}` i ett fält på fliken Skicka-åtgärder.

Om formuläret till exempel innehåller fältet **E-postadress** , med namnet `email_addr`, för att hämta användarens e-post-ID, kan du ange följande i fälten Mailto, CC eller BCC.

`${email_addr}`

När en användare skickar formuläret skickas ett e-postmeddelande till det e-post-ID som har angetts i formulärfältet `email_addr` .

>[!NOTE]
>
>Du hittar namnet på ett fält i dialogrutan **Redigera** för fältet.

Variabelplatshållare kan också användas i fälten **Ämne** och **E-postmall** .

Exempel:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Fält i upprepningsbara paneler kan inte användas som variabla platshållare.

