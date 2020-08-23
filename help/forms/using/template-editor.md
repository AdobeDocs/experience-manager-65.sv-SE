---
title: Adaptiva formulärmallar
seo-title: Adaptiva formulärmallar
description: Skapa anpassningsbara formulärmallar genom att definiera den grundläggande strukturen och det ursprungliga formulärinnehållet med hjälp av mallredigeraren.
seo-description: Skapa anpassningsbara formulärmallar genom att definiera den grundläggande strukturen och det ursprungliga formulärinnehållet med hjälp av mallredigeraren.
uuid: 317ca3ab-f809-49a7-a063-9d0c17a35fe4
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: b21a48ba-eccd-4bb5-9b92-3039026ddf2a
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1984'
ht-degree: 0%

---


# Adaptiva formulärmallar{#adaptive-form-templates}

När du skapar ett formulär lägger du till fält och komponenter för att definiera formulärstruktur, innehåll och åtgärder i redigeraren. Du lägger till fält och komponenter i `guideRootPanel` formulärbehållaren. Med mallredigeraren kan du skapa en mall som innehåller grundläggande struktur och ursprungligt innehåll som författare kan använda för att skapa formulär.

Du vill till exempel att alla formulärförfattare ska ha vissa textrutor, navigeringsknappar och en skicka-knapp i ett registreringsformulär. Du kan skapa en mall med de komponenter som författare kan använda för att skapa ett formulär som är konsekvent med andra registreringsformulär. När författare använder mallen för att skapa ett anpassat formulär ärver det nya formuläret strukturen och komponenterna som du har angett i mallen. Med mallredigeraren kan du:

* Lägg till sidhuvud- och sidfotskomponenter i ett formulär i strukturlagret.
* Ange formulärets ursprungliga innehåll.
* Ange ett tema, skicka åtgärder.

## Arbeta med mallar {#working-with-templates}

Du kommer åt mallredigeraren på Verktyg-menyn genom att gå till **Adobe Experience Manager > Verktyg > Mallar**. Här är mallarna ordnade i mappar som är aktiverade för redigerbara mallar. AEM innehåller en global mapp för att ordna mallar. Den är dock inte aktiverad som standard. Du kan begära att administratören aktiverar den globala mappen eller skapar en ny mapp för mallar. Mer information om hur du skapar mappar finns i [Mallmappar](/help/sites-developing/page-templates-editable.md).

När du trycker för att öppna en mapp finns knappen Skapa som gör att du kan skapa en ny mall för adaptiva formulär.

### Skapa en mall {#create-template}

När du har skapat en mapp öppnar du mappen och utför följande steg för att skapa en mall:

1. I mallkonsolen trycker du på **Skapa** i den mapp du har skapat.
1. I avsnittet Välj en malltyp väljer du **Adaptiv formulärmall** och trycker på **Nästa**.

1. Ange en malltitel i avsnittet Mallinformation och tryck på **Skapa**.
Du kan ange en beskrivning och miniatyrbild som du kan se när du kan välja den skapade mallen när du redigerar formuläret.

1. Tryck på **Klar** för att återgå till konsolen eller tryck på **Öppna** för att öppna mallen i redigeraren.

### Mallredigeringsgränssnitt {#template-editor-ui}

När du öppnar en mall för redigering kan du se följande AEM Editor-komponenter:

* **Verktygsfältet** Sida innehåller följande alternativ:

   * **Växla sidopanel**: Här kan du visa eller dölja sidofältet.
   * **Sidinformation**: Här kan du ange information som publicerings-/avpubliceringstid, miniatyrbilder, klientbibliotek, sidprincip och klientbibliotek för siddesign.
   * **Emulator**: Gör att du kan simulera och anpassa utseendet för olika enheter.
   * **Lagerväljare:** Här kan du ändra lagret.
Du kan välja **Strukturlager** eller **Inledande** innehållslager. Med strukturlagret kan du lägga till och anpassa sidhuvud och sidfot. Med lagret Ursprungligt innehåll kan du anpassa formulärinnehållet.

   * **Förhandsgranska:** Gör att du kan förhandsgranska hur mallen ser ut när du publicerar den. Du kan använda Lagerväljaren och Förhandsgranska för att växla redigerings- och förhandsgranskningsläge.

* **Sidofält:** Tillhandahåller webbläsarna Innehåll, Egenskaper, Resurser och Komponenter.
* **Komponentverktygsfältet:** När du markerar en komponent visas ett verktygsfält där du kan anpassa komponenten.
* **Sida**: Det område där du lägger till innehåll för att skapa mallen.

Se [Introduktion till redigering av adaptiva formulär](../../forms/using/introduction-forms-authoring.md) för att förstå redigeraren i Touch-gränssnittet.

### Redigera en mall {#editing-a-template}

En adaptiv formulärmall skapas med två lager:

* Struktur
* Ursprungligt innehåll

Lagerväljaren är tillgänglig bredvid alternativet Förhandsgranska i skärmens övre högra hörn.

### Struktur {#structure}

När du markerar strukturlagret i mallredigeraren kan du se layoutbehållarna ovanför och under den adaptiva formulärbehållaren. Författare kan använda dessa layoutbehållare för sidhuvud och sidfot. Du kan lägga till, redigera eller anpassa sidhuvudet och sidfoten. Dra och släpp komponenten Adaptiv formulärrubrik i layoutbehållaren ovanför den adaptiva formulärbehållaren för att anpassa mallrubriken. Dra och släpp komponenten Adaptiv formulärsidfot i layoutbehållaren nedanför den adaptiva formulärbehållaren för att anpassa mallsidfoten.

![Layoutbehållare i strukturlagret](assets/header-layer-selector.png)

Layoutbehållare i strukturlagret

**S.** Layoutbehållare för rubrikkomponent **B.** Layoutbehållare för sidfotskomponent

Dra och släpp komponenten Adaptiv formulärrubrik i layoutbehållaren ovanför behållaren för adaptiv form. När du har lagt till komponenten kan du ange dess egenskaper så att du kan lägga till en logotyp och ange dess titel.

På samma sätt kan du ange copyrightinformation och företagsinformation när du drar sidfotskomponenten i layoutbehållaren nedanför den adaptiva formulärbehållaren.

![Sidhuvud och sidfot som lagts till i strukturlagret](assets/header-and-footer.png)

Sidhuvud och sidfot som lagts till i strukturlagret

#### Låsa/låsa upp komponenter i strukturlagret {#locking-unlocking-components-in-the-structure-layer}

När du redigerar mallen med strukturlagret markerat kan du låsa upp mallens sidhuvud och sidfot. Om en komponent är olåst i mallen kan formulärförfattare redigera komponenten i det adaptiva formulär som använder mallen. Genom att låsa en komponent kan formulärförfattare inte redigera den i det anpassade formuläret. Alternativet Lås är tillgängligt i komponentens verktygsfält.

Du kan till exempel lägga till rubrikkomponenten i mallen. När du markerar komponenten kan du se ett låsalternativ i komponentens verktygsfält. Vanligtvis innehåller rubriken företagsnamn och logotyp, och du vill inte att formulärförfattare ska ändra logotypen och rubriken i en mall. I ett adaptivt formulär som skapats med mallen med huvudkomponenten låst kan formulärförfattare inte ändra logotypen och företagsnamnet.

>[!NOTE]
>
>Du bör inte låsa eller låsa upp en bild eller logotyp separat i rubrikkomponenten. Du kan låsa upp rubrikkomponenten.

### Ursprungligt innehåll {#initial-content}

När alternativet Ursprungligt innehåll är markerat öppnas mallens adaptiva formulärbehållare som ett adaptivt formulär för redigering. Precis som när du skapar ett anpassat formulär kan du ange inledande inställningar, som att välja ett tema och skicka åtgärder.

Formulärförfattare använder det som bas för att skapa ett formulär. Innehållsflödesstrukturen anges i lagret Ursprungligt innehåll i mallen. Om du vill växla till att redigera det ursprungliga innehållet i formulärmallen, innan du förhandsgranskar i sidverktygsfältet, trycker du på ![listrutan](assets/canvas-drop-down.png) Canvas **> Ursprungligt innehåll**.
![Ursprungligt innehållslager i mallredigeraren](assets/initial-content-layer.png)

Ursprungligt innehållslager i mallredigeraren med adaptiv formulärbehållare markerad för att ange egenskaper.

![ursprungligt innehåll](assets/initial-content-layer-1.png)

I lagret Ursprungligt innehåll skapar du den anpassningsbara formulärmallen som författarna använder som bas. Om du redigerar en mall på samma sätt som när du redigerar ett formulär, använder du de alternativ som finns i sidofältet. Sidofältet innehåller webbläsare för innehåll, egenskaper, resurser och komponenter.

Se [Sidpanelen](../../forms/using/introduction-forms-authoring.md#sidebar).

>[!NOTE]
>
>När du väljer Lagra innehåll eller Lagra PDF som överföringsåtgärd får du ett alternativ för att ange lagringssökvägen. Om du anger en sökväg i en mall får alla formulär som skapas från den samma sökväg. Du kan ange rätt lagringssökväg eller se till att formulärförfattare uppdaterar den för att förhindra att data från alla formulär lagras på samma plats.

#### Skapa en adaptiv formulärmall med flikar och paneler  {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

Du kan till exempel skapa en mall med följande flikar:

* Allmän information
* Professional Information

Du har lagt till en logotyp, angett en rubrik och lagt till en sidfot i strukturlagret. Lås sidhuvudet och sidfoten för att hindra formulärförfattare från att redigera dem när de använder mallen för att skapa formulär.

Ändra lagret från Struktur till Inledande innehåll och börja lägga till innehåll i formuläret. Om du vill skapa en flikstruktur lägger du till en underordnad panel i guideRootPanel i behållaren för adaptivt format. Så här lägger du till en panel:

* Du kan lägga till en panel genom att trycka på **+** -knappen när du väljer alternativet **Dra komponenter här** .

* Du kan dra och släppa panelkomponenten från komponentwebbläsaren i sidofältet.
* Du kan lägga till en underordnad panel till `guideRootPanel` från komponentverktygsfältet.

Om du vill skapa flikarna Allmän information och Professionell information lägger du till två paneler på den underordnade panelen till `guideRootPanel`. Markera panelerna och tryck på ![cmpr](assets/cmppr.png) för att öppna egenskaperna i sidofältet. Ändra elementnamnen som `general-info` och `professional-info`samt rubrikerna som Allmän information respektive Professional Information. I sidlisten: tryck på innehåll för att öppna innehållsläsaren. Markera på fliken Formulärobjekt `guideRootPanel`. I redigeraren markeras guideRootPanel. Tryck på ![cmpr](assets/cmppr.png) i komponentens verktygsfält för att öppna dess egenskaper. I fältet Panellayout väljer du **Tabbar överst** och trycker på **Klar**. Flikmallstrukturen används.

#### Lägga till innehåll på flikar {#adding-content-in-tabs}

![Lägga till fält i den adaptiva formulärmallen](assets/template-edit-initial-content.png)

När du har lagt till paneler och strukturerat dem som flikar kan du lägga till fält inuti flikarna. När du markerar en flik i redigeraren visas alternativet **Dra komponenter här** . Du kan dra och släppa komponenter som textrutor, listobjekt och knappar. Du kan dra och släppa komponenter från komponentwebbläsaren i sidofältet.

Varje komponent har egenskaper som förbättrar datainhämtning och -hantering. Du kan till exempel aktivera egenskapen **Obligatoriskt fält** för en komponent. Författarna kan ange ett meddelande som kunderna ser när de inte fyller i ett obligatoriskt fält. Ange meddelandet i **egenskapen Meddelande** för obligatoriskt fält.

I exempelmallen läggs fälten Namn, Telefonnummer och Födelsedatum till på fliken Allmän information. På fliken Professional Information, Anställda, typ av anställning, läggs fält för utbildningsbehörighet till.

När du har lagt till fält kan du lägga till knappar som Skicka och Återställ.

### Aktivera mallen {#enabling-the-template}

När du skapar en mall läggs den till som ett utkast. Aktivera mallen för att använda den för att skapa anpassningsbara formulär. Så här aktiverar du en mall:

1. Navigera till **Adobe Experience Manager > Verktyg > Mallar** och öppna den mapp där du har skapat mallen.

1. Mallen som du har skapat markeras som Utkast.
1. Markera mallen och tryck på **Aktivera** i verktygsfältet.
När du skapar ett anpassat formulär kan du se mallen som visas när du ombeds att välja en mall.

## Importera eller exportera en mall {#importing-or-exporting-a-template}

Ett formulär fungerar med sin mall. När du hämtar ett adaptivt formulär som skapats med en anpassad mall hämtas inte mallen. När du importerar formuläret till en annan AEM Forms-instans importeras det utan någon mall. Om ett formulär importeras men mallen inte är tillgänglig, återges inte formuläret. Du kan paketera den anpassade mallen från `/conf` noden i `https://<server>:<port>/crx/packmgr`och portera den i den AEM Forms-instans där du vill överföra formuläret.

## Skapa ett anpassat formulär med hjälp av mallen {#creating-an-adaptive-form-using-the-template}

När du har skapat och aktiverat en mall är den tillgänglig i formulärhanteraren när du skapar ett anpassat formulär. Mer information om hur du använder en mall och skapar ett anpassat formulär finns i [Skapa ett anpassat formulär](../../forms/using/creating-adaptive-form.md).

## Ändra visningsalternativ för mallar som inte är i kartong  {#change-display-option-of-out-of-the-box-templates}

Du kan skapa anpassade mallar för adaptiva formulär för att definiera grundläggande struktur och ursprungligt innehåll. AEM Forms har också en uppsättning färdiga mallar för anpassningsbara formulär. Du kan välja att visa eller dölja mallarna.

Så här visar och döljer du mallar:

1. Logga in på AEM Forms författarinstans och gå till **Verktyg** > **Åtgärder** > **Webbkonsol**.

   >[!NOTE]
   >
   >URL:en för AEM webbkonsol är https://&#39;[server]:[port]&#39;/system/console/configMgr

1. Leta reda på och öppna konfigurationsinställningarna för **FormsManager** :

   * Markera eller avmarkera alternativet **Inkludera från i rutan AF- och AD-mallar** om du vill visa eller dölja formulärmallar.
   * Markera eller avmarkera alternativet **Inkludera AEM 6.0 AF-mallar** om du vill visa eller dölja anpassade formulärmallar som lagts till i Forms version AEM 6.0 eller AEM 6.1 men som nu är borttagna. Om det här alternativet är markerat måste konfigurationen **Inkludera i rutorna AF och AD-mallar** vara aktiverad för att det ska börja gälla.

1. Click **Save**. Visningsalternativen för mallar som inte finns i kartongen ändras.

## Recommendations {#recommendations}

* När du ändrar egenskaper för formuläret i mallredigeraren ska du inte använda egenskapen BindReference.
* Om du vill lägga till en brytpunkt skapar du den när du skapar en adaptiv formulärmall.
Mer information om brytpunkter finns i [Responsiv layout](/help/sites-authoring/responsive-layout.md).

