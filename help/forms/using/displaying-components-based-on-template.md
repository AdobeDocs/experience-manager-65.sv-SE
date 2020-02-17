---
title: Visa komponenter baserat på den mall som används
seo-title: Visa komponenter baserat på den mall som används
description: När du skapar ett formulär ska du lära dig hur du kan aktivera komponenter i sidofältet baserat på den valda mallen.
seo-description: När du skapar ett formulär ska du lära dig hur du kan aktivera komponenter i sidofältet baserat på den valda mallen.
uuid: 790d201b-318d-4d02-9bc5-9d6bc41d057a
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
discoiquuid: f658da57-0134-4458-9ef9-a99787b66742
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# Visa komponenter baserat på den mall som används{#displaying-components-based-on-the-template-used}

När en formulärförfattare skapar ett anpassat formulär med hjälp av en [mall](../../forms/using/template-editor.md)kan formulärförfattaren se och använda specifika komponenter som är baserade på en mallprofil. Du kan ange en innehållsprincip för mallar där du kan välja en grupp komponenter som formulärförfattaren ser när formuläret skapas.

## Ändra innehållsprincipen för en mall {#changing-the-content-policy-of-a-template}

När du skapar en mall skapas den under `/conf` i innehållsdatabasen. Baserat på de mappar du har skapat i `/conf` katalogen är sökvägen till mallen: `/conf/<your-folder>/settings/wcm/templates/<your-template>`.

Följ de här stegen för att visa komponenterna i sidofältet baserat på en malls innehållsprincip:

1. Öppna CRXDE lite.\
   Webbadress: `https://<server>:<port>/crx/de/index.jsp`
1. I CRXDE navigerar du till mappen där mallen skapas.

   Exempel: `/conf/<your-folder>/`

1. I CRXDE navigerar du till: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   Om du vill välja en grupp komponenter krävs en ny innehållsprincip. Om du vill skapa en ny princip kopierar och klistrar du in standardprincipen och byter namn på den.

   Sökvägen till standardinnehållsprincipen är: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   Kopiera och klistra in standardprincipen i `gridFluidLayout` mappen och byt namn på den. Exempel, `myPolicy`.

   ![Kopierar standardprinciper](assets/crx-default1.png)

1. Välj den nya profilen som du skapar och välj **komponentegenskapen** på den högra panelen med typen `string[]`.

   När du markerar och öppnar komponentegenskapen visas dialogrutan Redigera komponenter. I dialogrutan Redigera komponenter kan du lägga till eller ta bort komponentgrupper med knapparna **+** och **-** . Du kan lägga till komponentgrupper som innehåller komponenter som du vill att författarna ska använda.

   ![Lägga till eller ta bort komponenter i profilen](assets/add-components-list1.png)

   När du har lagt till en komponentgrupp uppdaterar du listan genom att klicka på **OK** . Klicka sedan på **Spara alla** ovanför adressfältet för CRXDE och uppdatera.

1. I mallen ändrar du innehållsprincipen från standard till den nya profilen som du skapade. ( `myPolicy` i det här exemplet.)

   Om du vill ändra profilen går du till CRXDE `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`.

   I `cq:policy` egenskapen ändrar du `default` till det nya principnamnet ( `myPolicy`).

   ![Uppdaterad princip för mallinnehåll](assets/updated-policy.png)

   När du skapar ett formulär som du skapar med hjälp av mallen kan du se de komponenter som lagts till i sidofältet.

