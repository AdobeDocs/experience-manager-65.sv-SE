---
title: Hantera [!DNL Adobe Stock]-resurser i [!DNL Adobe Experience Manager Assets].
description: Sök, hämta, licensiera och hantera [!DNL Adobe Stock]-resurser inifrån [!DNL Adobe Experience Manager]. Använd de licensierade mediefilerna som andra digitala resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 376940612066123a8f84fe6c30ff3002cda08079
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 3%

---


# Använd [!DNL Adobe Stock] resurser i [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

Organisationer kan integrera sin [!DNL Adobe Stock] Enterprise-plan med [!DNL Experience Manager Assets] för att se till att licensierat material finns i stor omfattning tillgängligt för kreativa projekt och marknadsföringsprojekt, med de kraftfulla resurshanteringsfunktionerna i [!DNL Experience Manager].

[!DNL Adobe Stock] ger designers och företag tillgång till miljontals utvalda och royaltyfria foton, vektorer, illustrationer, videor, mallar och 3D-resurser av hög kvalitet för alla kreativa projekt. [!DNL Experience Manager] -användare snabbt kan hitta, förhandsgranska och licensiera [!DNL Adobe Stock] resurser som har sparats i [!DNL Experience Manager], utan att behöva lämna [!DNL Experience Manager] gränssnittet.

## Förutsättningar {#prerequisites}

Integreringen kräver en Adobe Stock-plan [för](https://stockenterprise.adobe.com/) företag och [!DNL Experience Manager] 6.5 eller senare. Mer information om [!DNL Experience Manager] 6.5-Service Pack finns i [versionsinformationen](/help/release-notes/sp-release-notes.md).

## Integrera [!DNL Experience Manager] och [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

Om du vill tillåta kommunikation mellan [!DNL Experience Manager] och [!DNL Adobe Stock]skapar du en IMS-konfiguration och en [!DNL Adobe Stock] konfiguration i [!DNL Experience Manager].

>[!NOTE]
>
>Det är bara [!DNL Experience Manager] administratörer och [!DNL Admin Console] administratörer för en organisation som kan utföra integreringen eftersom den kräver administratörsbehörighet.

### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Klicka på **[!UICONTROL Create]** och välj **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Återanvänd ett befintligt certifikat eller välj **[!UICONTROL Create new certificate]**.
1. Klicka på **[!UICONTROL Create certificate]**. Ladda ned den offentliga nyckeln när du har skapat den. Klicka på **[!UICONTROL Next]**.
1. Lägg till den hämtade offentliga nyckeln till ditt [!DNL Adobe Developer Console] tjänstkonto. Klicka på **[!UICONTROL Next]**. Lämna skärmen öppen så att du kan ange värdena inom kort [!UICONTROL Adobe IMS Technical Account Configuration] .
1. Gå till [Adobe Developer Console](https://console.adobe.io). Se till att ditt konto har administratörsbehörighet för organisationen som integreringen krävs för.
1. Klicka **[!UICONTROL Create new project]** och klicka **[!UICONTROL Add API]**. Välj **[!UICONTROL Adobe Stock]** i listan över API:er som är [!UICONTROL available to you]. Välj [!UICONTROL OAUTH 2.0 Web]. Konfigurera och kopiera de olika värdena som presenteras.
1. In [!DNL Experience Manager] provide the values in the fields titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. Se [Snabbstart](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)för JWT-autentisering för mer detaljerad information om dessa värden.

<!-- TBD: Update the URL when the new URL is available. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### Skapa [!DNL Adobe Stock] konfiguration i [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Klicka **[!UICONTROL Create]** för att skapa en konfiguration och koppla den till din befintliga IMS-konfiguration. Välj `PROD` som miljöparameter.
1. I **[!UICONTROL Licensed Assets Path]** fältet låter du platsen vara som den är. Ändra inte platsen där du vill lagra [!DNL Adobe Stock] resurserna.
1. Skapa genom att lägga till alla nödvändiga egenskaper. Klicka på **[!UICONTROL Save & Close]**.
1. Lägg till [!DNL Experience Manager] användare eller grupper som kan licensiera mediefilerna.

>[!NOTE]
>
>Om det finns flera [!DNL Adobe Stock] konfigurationer väljer du den önskade konfigurationen på panelen Användarinställningar (**[!UICONTROL AEM]** > **[!UICONTROL User Icon]** > **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**).

## Använd och hantera [!DNL Adobe Stock] resurser i [!DNL Experience Manager] {#usemanage}

Med den här funktionen kan organisationer låta användarna arbeta med [!DNL Adobe Stock] resurser i [!DNL Experience Manager Assets]. I [!DNL Experience Manager] användargränssnittet kan användarna söka efter [!DNL Adobe Stock] resurser och licensiera de resurser som behövs.

När en [!DNL Adobe Stock] mediefil är licensierad i [!DNL Experience Manager]kan den användas och hanteras som en vanlig mediefil. I [!DNL Experience Manager]kan användarna söka efter och förhandsgranska resurserna. kopiera och publicera tillgångarna, dela tillgångarna på [!DNL Brand Portal], få tillgång till och använda resurserna via [!DNL Experience Manager] datorprogrammet, och så vidare.

![Söka efter Adobe Stock-resurser och filtrera resultat från arbetsytan i Adobe Experience Manager](assets/adobe-stock-search-results-workspace.png)

*Bild: Sök efter[!DNL Adobe Stock]resurser och filtrera resultat från ditt[!DNL Experience Manager]gränssnitt.*

**A.**[!DNL Adobe Stock] Sök efter resurser som liknar de resurser vars ID har angetts. **B.** Sök efter resurser som matchar ditt val av form eller orientering. **C.** Sök efter en av de resurstyper som stöds **D.** Öppna eller dölj filterrutan **E.** Licensiera och spara den valda resursen i [!DNL Experience Manager]**F.** Spara resursen i [!DNL Experience Manager] med vattenstämpel **G.** Utforska resurser på [!DNL Adobe Stock] webbplatsen som liknar den valda resursen **H.** Visa de valda resurserna på [!DNL Adobe Stock] webbplats **I.** Antal valda resurser från sökresultaten **J.** Växla mellan kortvyn och listvyn

### Hitta resurser {#find-assets}

Dina [!DNL Experience Manager] användare kan söka efter resurser i både [!DNL Experience Manager] och [!DNL Adobe Stock]. När sökplatsen inte är begränsad till [!DNL Adobe Stock]visas sökresultaten från [!DNL Experience Manager] och [!DNL Adobe Stock] .

* Om du vill söka efter [!DNL Adobe Stock] resurser klickar du på **[!UICONTROL Navigation]** > **[!UICONTROL Assets]** > **[!UICONTROL Search Adobe Stock]**.

* Om du vill söka efter resurser i [!DNL Adobe Stock] och [!DNL Experience Manager Assets]i klickar du på ![search_icon](assets/search_icon.png).

Du kan också börja skriva `Location: Adobe Stock` i sökfältet för att välja [!DNL Adobe Stock] resurser. [!DNL Experience Manager] har avancerade filtreringsfunktioner för de sökbara resurserna, vilket gör att användarna snabbt kan nollställa de resurser som behövs med hjälp av filter, som typer av resurser som stöds, bildorientering och licensierat läge.

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] resurser hämtas och lagras i [!DNL Experience Manager] databasen först när en användare antingen [sparar en resurs](/help/assets/aem-assets-adobe-stock.md#saveassets) eller [licenser och sparar en resurs](/help/assets/aem-assets-adobe-stock.md#licenseassets). Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![Sök efter filter i Experience Manager och markerade Adobe Stock-mediefiler i sökresultaten](assets/aem-search-filters2.jpg)

*Bild: Sök efter filter i[!DNL Experience Manager]och markerade[!DNL Adobe Stock]resurser i sökresultaten.*

### Spara och visa nödvändiga resurser {#saveassets}

Välj en resurs som du vill spara i [!DNL Experience Manager]. Klicka [!UICONTROL Save] i verktygsfältet överst och ange resursens namn och plats. De olicensierade resurserna sparas lokalt med en vattenstämpel.

Nästa gång du söker efter resurser markeras de sparade resurserna med ett märke som anger att resurserna är tillgängliga i [!DNL Experience Manager Assets].

>[!NOTE]
>
>De nyligen tillagda resurserna visas med märket Nytt i stället för Licensierad.

### Licensiera resurser {#licenseassets}

Användare kan licensiera [!DNL Adobe Stock] mediefiler genom att använda kvoten i sin [!DNL Adobe Stock] Enterprise-plan. När du licensierar en mediefil sparas den utan vattenstämpel och är tillgänglig för sökning och användning i [!DNL Experience Manager Assets].

![Dialogruta där du kan licensiera och spara Adobe Stock-mediefiler i Experience Manager Assets](assets/aem-stock_licenseandsave.jpg)

*Bild: Dialogruta där du kan licensiera och spara[!DNL Adobe Stock]resurser i[!DNL Experience Manager Assets].*

### Få åtkomst till metadata och resursegenskaper {#access-metadata-and-asset-properties}

Användare kan komma åt och förhandsgranska metadata, inklusive metadataegenskaperna för de resurser som sparats i [!DNL Adobe Stock] och lägga till [!DNL Experience Manager]**[!UICONTROL License References]** för en resurs. Uppdateringarna av licensreferensen synkroniseras dock inte mellan [!DNL Experience Manager] och [!DNL Adobe Stock] webbplats.

Användarna kan se egenskaperna för både, licensierade och olicensierade resurser.

![Visa och få tillgång till metadata och licensreferenser för sparade resurser](assets/metadata_properties.jpg)

*Bild: Visa och öppna metadata och licensreferenser för sparade resurser.*

## Kända begränsningar {#known-limitations}

* **Varning om redigeringsbild visas** inte: När du licensierar en bild kan du inte kontrollera om en bild endast är för redaktionellt bruk. För att förhindra eventuell felaktig användning kan administratören stänga av åtkomsten till redaktionella mediefiler från Admin Console.

* **Fel licenstyp visas**: Det är möjligt att en felaktig licenstyp visas i [!DNL Experience Manager] för en resurs. Användarna kan logga in på [!DNL Adobe Stock] webbplatsen för att se licenstypen.

* **Referensfält och metadata synkroniseras** inte: När en användare uppdaterar ett licensreferensfält uppdateras licensreferensinformationen i [!DNL Experience Manager] men inte på [!DNL Adobe Stock] webbplatsen. Om användaren uppdaterar referensfälten på [!DNL Adobe Stock] webbplatsen synkroniseras inte uppdateringarna i [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Videosjälvstudiekurs om hur du använder Adobe Stock-resurser med Experience Manager Assets](https://helpx.adobe.com/experience-manager/kt/assets/using/stock-assets-feature-video-use.html)
>* [Hjälp om Adobe Stock-företagsplaner](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Vanliga frågor om Adobe Stock](https://helpx.adobe.com/stock/faq.html)

