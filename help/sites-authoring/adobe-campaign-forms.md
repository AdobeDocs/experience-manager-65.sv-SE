---
title: Skapa Adobe Campaign-formulär i AEM
seo-title: Skapa Adobe Campaign-formulär i AEM
description: Med AEM kan ni skapa och använda formulär som interagerar med Adobe Campaign på er webbplats
seo-description: Med AEM kan ni skapa och använda formulär som interagerar med Adobe Campaign på er webbplats
uuid: 61778ea7-c4d7-43ee-905f-f3ecb752aae2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: d53ef3e2-14ca-4444-b563-be67be15c040
translation-type: tm+mt
source-git-commit: 2451f4994a18b1566ea0efddbefcaa5bb8e41c99

---


# Skapa Adobe Campaign-formulär i AEM {#creating-adobe-campaign-forms-in-aem}

Med AEM kan ni skapa och använda formulär som interagerar med Adobe Campaign på er webbplats. Specifika fält kan infogas i formulären och mappas till Adobe Campaign-databasen.

Ni kan hantera nya kontaktprenumerationer, avbeställningar och användarprofilsdata samtidigt som ni integrerar deras data i Adobe Campaign-databasen.

Om du vill använda Adobe Campaign-formulär i AEM måste du följa de här stegen som beskrivs i det här dokumentet:

1. Gör en mall tillgänglig.
1. Skapa ett formulär.
1. Redigera formulärinnehåll.

Tre typer av formulär, som är specifika för Adobe Campaign, är tillgängliga som standard:

* Spara en profil
* Prenumerera på en tjänst
* Avbeställ en tjänst

Dessa formulär definierar en URL-parameter som godkänner den krypterade primärnyckeln för en Adobe Campaign-profil. Baserat på den här URL-parametern uppdaterar formuläret data för den associerade Adobe Campaign-profilen.

Även om du skapar de här formulären oberoende av varandra, genererar du i ett vanligt fall en personlig länk till en formulärsida i nyhetsbrevets innehåll, så att mottagarna kan öppna länken och göra ändringar i profildata (oavsett om de avregistrerar, prenumererar eller uppdaterar deras profil).

Formuläret uppdateras automatiskt baserat på användaren. Mer information finns i [Redigera formulärinnehåll](#editing-form-content) .

## Göra en mall tillgänglig {#making-a-template-available}

Innan du kan skapa formulär som är specifika för Adobe Campaign måste du göra de olika mallarna tillgängliga i ditt AEM-program.

Mer information finns i dokumentationen [för](/help/sites-developing/templates.md#template-availability)mallar.

## Skapa ett formulär {#creating-a-form}

Först och främst kontrollerar du kopplingen mellan författaren och publiceringsinstanser och Adobe Campaign fungerar. Se [Integrera med Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) eller [Integrera med Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Kontrollera att **egenskapen acMapping** på sidans **jcr:content** -nod är inställd på **mapRecipient** eller **profile** när du använder Adobe Campaign Classic eller Adobe Campaign Standard


1. I AEM navigerar du till den plats där du vill skapa en ny sida i Sites.
1. Skapa en sida och välj **Adobe Campaign Classic-profil** eller **Adobe Campaign-standardprofil** och klicka på **Nästa**.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Om den önskade mallen inte är tillgänglig läser du [Malltillgänglighet](/help/sites-developing/templates.md#template-availability).

1. Lägg till sidans namn i fältet **Namn** . Det måste vara ett giltigt JCR-namn.
1. Ange en titel i fältet **Titel** och klicka på **Skapa**.
1. Öppna sidan och välj **Öppna egenskaper** . I Cloud Services lägger du till Adobe Campaign-konfigurationen och markerar kryssrutan för att spara ändringarna.

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. På sidan, i **komponenten Formulärstart** , väljer du vilken typ av formulär det är: **Prenumerera, Avsluta prenumeration** eller **Spara profil**. Du kan bara ha en typ per formulär. Nu kan du [redigera formulärets innehåll](#editing-form-content).

## Redigera formulärinnehåll {#editing-form-content}

Formulär som riktar sig till Adobe Campaign har specifika komponenter. Dessa komponenter har ett alternativ som gör att du kan länka varje fält i formuläret till ett fält i Adobe Campaign-databasen.

>[!NOTE]
>
>Om den önskade mallen inte är tillgänglig läser du [Göra en mall tillgänglig](/help/sites-authoring/adobe-campaign.md).

I det här avsnittet beskrivs endast specifika länkar till Adobe Campaign. Mer information om en mer allmän översikt över hur du använder formulär i Adobe Experience Manager finns i [Komponenter](/help/sites-authoring/default-components-foundation.md)i redigeringsläget.

1. Välj **Öppna egenskaper** . I molntjänster lägger du till Adobe Campaign-konfigurationen och markerar kryssrutan för att spara ändringarna.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Klicka på ikonen Konfiguration på sidan i **komponenten Formulärstart** .

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Klicka på fliken **Avancerat** och välj vilken typ av formulär det är - **Prenumerera,** Avsluta prenumeration eller **Spara profil** och klicka på **OK.** Du kan bara ha en typ per formulär.

   * **Adobe Campaign: Spara profil**: Med kan du skapa eller uppdatera en mottagare i Adobe Campaign (standardvärde).
   * **Adobe Campaign: Prenumerera på tjänster**: gör att du kan hantera prenumerationer för en mottagare i Adobe Campaign.
   * **Adobe Campaign: Avbeställ tjänsterna**: Med kan du avbryta prenumerationer på en mottagare i Adobe Campaign.

1. Du måste ha en **krypterad primärnyckelkomponent** i varje formulär. Den här komponenten definierar vilken URL-parameter som ska användas för att acceptera den krypterade primärnyckeln för en Adobe Campaign-profil. I Komponenter väljer du Adobe Campaign så att bara de komponenterna visas.
1. Dra komponentens **krypterade primärnyckel** till formuläret (var som helst) och klicka eller tryck på ikonen **Konfiguration** . Ange ett namn för URL-parametern på fliken **Adobe Campaign** . Klicka eller tryck på bockmarkeringen för att spara ändringarna.

   Genererade länkar till det här formuläret måste använda den här URL-parametern och tilldela den krypterade primärnyckeln till en Adobe Campaign-profil. Den krypterade primärnyckeln måste vara rätt URL-kodad (procent).

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. Lägg till komponenter i formuläret efter behov, t.ex. textfält, datumfält, kryssrutefält, alternativfält osv. Mer information om de olika komponenterna finns i [Adobe Campaign-formulärkomponenter](/help/sites-authoring/adobe-campaign-components.md) .
1. Klicka på ikonen Konfiguration för att öppna komponenten. I **textfältskomponenten (Campaign)** ändrar du till exempel titeln och texten.

   Klicka på **Adobe Campaign** för att mappa formulärfältet till en Adobe Campaign-metadatavariabel. När du skickar formuläret uppdateras det mappade fältet i Adobe Campaign. Endast fält med matchande typer är tillgängliga i variabelväljaren (till exempel strängvariabler för textfält).

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >Du kan lägga till/ta bort fält som visas i mottagartabellen genom att följa instruktionerna här: [https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)

1. Klicka på **Publicera sida**. Sidan aktiveras på din webbplats. Du kan visa den genom att gå till din AEM-publiceringsinstans. Du kan också [testa ett formulär](#testing-a-form).

   >[!CAUTION]
   >
   >Du måste ange läsbehörigheter till den anonyma användaren i molntjänsten för att kunna använda formulär vid publicering. Tänk dock på de potentiella säkerhetsproblemen med att ge läsbehörigheter till den anonyma användaren och se till att minska risken genom att till exempel konfigurera dispatchern.

## Testa ett formulär {#testing-a-form}

När du har skapat ett formulär och redigerat formulärinnehållet kanske du vill testa att formuläret fungerar som det ska.

>[!NOTE]
>
>Du måste ha en **krypterad primärnyckelkomponent** i varje formulär. I Komponenter väljer du Adobe Campaign så att bara de komponenterna visas.
>
>I den här proceduren anger du telefonnumret manuellt, men i praktiken får användarna en länk till den här sidan (om de vill avbeställa, prenumerera eller uppdatera din profil) i ett nyhetsbrev. Paketet uppdateras automatiskt beroende på användaren.
>
>Om du vill skapa länken använder du variabeln **Huvudresursidentifierare**(Adobe Campaign Standard) eller **Krypterad identifierare** (Adobe Campaign Classic) (till exempel i en **Text &amp; Personalization-** komponent (Campaign)) som är länkad till sidan i Adobe Campaign.

För att göra detta måste du hämta EPK-filen för en Adobe Campaign-profil manuellt och sedan bifoga den till URL-adressen:

1. Så här hämtar du den krypterade primärnyckeln (EPK) för en Adobe Campaign-profil:

   * I Adobe Campaign Standard - Navigera till **Profiler och målgrupper** > **Profiler**, som listar de befintliga profilerna. Se till att tabellen visar fältet **Huvudresursidentifierare** i en kolumn (du kan konfigurera detta genom att klicka/trycka på **Konfigurera lista**). Kopiera huvudresursidentifieraren för den önskade profilen.
   * I Adobe Campaign Classic går du till **Profiler och mål** > **Mottagare**, som listar de befintliga profilerna. Se till att tabellen visar fältet **Krypterad identifierare** i en kolumn (detta kan konfigureras genom att högerklicka på en post och välja **Konfigurera lista..**). Kopiera den krypterade identifieraren för den önskade profilen.

1. I AEM öppnar du formulärsidan i publiceringsinstansen och lägger till EPK från steg 1 som en URL-parameter: Använd samma namn som du tidigare definierade i EPK-komponenten när du redigerar formuläret (till exempel: `?epk=...`)
1. Formuläret kan nu användas för att ändra data och prenumerationer som är kopplade till den länkade Adobe Campaign-profilen. När du har ändrat vissa fält och skickat in formuläret kan du verifiera i Adobe Campaign att rätt data har uppdaterats.

Data i Adobe Campaign-databasen uppdateras när ett formulär har validerats.
