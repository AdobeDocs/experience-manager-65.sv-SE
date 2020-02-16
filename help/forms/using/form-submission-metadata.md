---
title: Lägga till information från användardata i metadata för att skicka formulär
seo-title: Lägga till information från användardata i metadata för att skicka formulär
description: 'Lär dig hur du lägger till information i metadata för ett skickat formulär med användardata. '
seo-description: 'Lär dig hur du lägger till information i metadata för ett skickat formulär med användardata. '
uuid: c3eea3c0-31f8-4bf8-b5cf-34f907bdbdba
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2c971da0-5bd5-40d1-820d-4efc2a44b49d
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Lägga till information från användardata i metadata för att skicka formulär{#adding-information-from-user-data-to-form-submission-metadata}

Du kan använda värden som anges i ett element i formuläret för att beräkna metadatafält för ett utkast eller en formulärsändning. Med metadata kan du filtrera innehåll baserat på användardata. En användare skriver till exempel John Doe i namnfältet i ditt formulär. Du kan använda den här informationen för att beräkna metadata som kan kategorisera överföringen under den initiala JD:n.

Om du vill beräkna metadatafält med värden som användaren anger lägger du till formulärelement i metadata. När en användare anger ett värde i det elementet används värdet för att beräkna information. Den här informationen läggs till i metadata. När du lägger till ett element som ett metadatafält anger du en nyckel för det. Nyckeln läggs till som ett fält i metadata och den beräknade informationen loggas mot det.

Ett sjukförsäkringsföretag publicerar t.ex. en blankett. I det här formuläret hämtar ett fält slutanvändarnas ålder. Kunden vill kontrollera alla inskickade data i ett visst åldersintervall efter att ett antal användare har skickat in formuläret. Istället för att gå igenom alla data som kompliceras av allt fler formulär, hjälper extra metadata kunden. Formulärets författare kan konfigurera vilka egenskaper/data som fylls i av slutanvändaren som lagras på den översta nivån så att sökningen blir så enkel som möjligt. Ytterligare metadata är användarfylld information som lagras på den översta nivån i metadatanoden, enligt författarens inställningar.

Ta ett exempel på ett formulär som innehåller e-post-ID och telefonnummer. När en användare besöker det här formuläret anonymt och överger formuläret kan författaren konfigurera formuläret så att e-post-ID och telefonnummer sparas automatiskt. Det här formuläret sparas automatiskt och telefonnumret och e-post-ID lagras i metadatanoden i utkastet. Ett användningsfall för den här konfigurationen är kontrollpanelen för lead-hantering.

## Lägga till formulärelement i metadata {#adding-form-elements-to-metadata}

Gör så här för att lägga till ett element i metadata:

1. Öppna det anpassningsbara formuläret i redigeringsläge.\
   Om du vill öppna formuläret i redigeringsläge markerar du formuläret i formulärhanteraren och trycker på **Öppna**.
1. Markera en komponent i redigeringsläget, tryck på ![fältnivå](assets/field-level.png) > **Adaptiv formulärbehållare** och sedan på ![cmpr](assets/cmppr.png).
1. Klicka på **Metadata** i sidofältet.
1. Klicka på **Lägg till** i avsnittet Metadata.
1. Använd fältet Värde på fliken Metadata för att lägga till skript. De skript du lägger till samlar in data från element i formuläret och beräknar värden som matas in i metadata.

   Till exempel loggas **true** i metadata om den angivna åldern är större än 21 och **false** loggas om den är mindre än 21. Du anger följande skript på fliken Metadata:

   `(agebox.value >= 21) ? true : false`

   ![Metadatascript](assets/add-element-metadata.png)

   Skript som anges på fliken Metadata

1. Click **OK**.

När en användare har angett data i elementet som har markerats som ett metadatafält loggas den beräknade informationen i metadata. Du kan se metadata i databasen som du konfigurerade för att lagra metadata.

## Se uppdaterade metadata för inlämning av formulär: {#seeing-updated-form-nbsp-submission-metadata}

I exemplet ovan lagras metadata i CRX-databasen. Metadata ser ut så här:

![Metadata](assets/metadata_entry_new.png)

Om du lägger till ett kryssruteelement i metadata lagras markerade värden som en kommaavgränsad sträng. Du kan till exempel lägga till en kryssrutekomponent i formuläret och ange dess namn som `checkbox1`. I kryssrutans komponentegenskaper lägger du till objekten Körningslicens, Personnummer och Passport för värdena 0, 1 och 2.

![Lagra flera värden från en kryssruta](assets/checkbox-metadata.png)

Du väljer en adaptiv formulärbehållare och i formuläregenskaperna lägger du till en metadatanyckel `cb1` som lagrar `checkbox1.value`och publicerar formuläret. När kunden fyller i formuläret väljer kunden passnummer och personnummer i kryssrutefältet. Värdena 1 och 2 lagras som 1 och 2 i fältet cb1 i metadata för överföringen.

![Metadatapost för flera värden som är markerade i ett kryssrutefält](assets/metadata-entry.png)

>[!NOTE]
>
>Exemplet ovan är endast avsett för inlärning. Kontrollera att du letar efter metadata på rätt plats som konfigurerats i implementeringen av AEM Forms.

