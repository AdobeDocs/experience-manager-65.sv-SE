---
title: Använda klottrar i HTML5-formulär
description: HTML5-formulär används i allt större utsträckning på enheter med pekskärm, och ett vanligt krav är att stödja signaturer. Att signera dokument på mobila enheter har blivit ett accepterat sätt att signera formulär på mobila enheter.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
docset: aem65
feature: Forms Designer
exl-id: 2025182f-195b-40d0-aee7-67669f55b964
source-git-commit: 744cfcee691ea71f33cd56509f65d4f640d4c6e3
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# Använda klottrar i HTML5-formulär{#using-scribble-signature-in-html-forms}

HTML5-formulär används i allt större utsträckning på enheter med pekskärm, och ett vanligt krav är att stödja signaturer. Skript (skrivande med en penna eller ett finger) blir ett accepterat sätt att signera formulär på mobila enheter. HTML5-formulär och Forms Designer aktiverar nu alternativet att ha ett signaturfält med klotter i formuläret. När formuläret återges i webbläsaren kan du signera dessa fält med en penna, mus eller touchpenna.

## Designa ett formulär med fältet Klottsignatur {#how-to-design-a-form-using-scribble-signature-field}

1. Öppna ett formulär i Forms Designer.
1. Dra och släpp signaturfältet på sidan.

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >Dimensioner av det fält som är markerat i Forms Designer visas när fältet återges. Dimensionen för den återgivna signaturrutan beräknas dock baserat på fältets proportioner, inte på dimensionen som anges i Forms Designer.

1. Konfigurera signaturskriptfältet.

   Som standard markeras geopositioneringsinformation som obligatorisk under signeringsprocessen i iPad i fältet Signature Scribble (och är valfritt för andra enheter). Det här standardbeteendet kan åsidosättas genom att ändra värdet för `geoLocMandatoryOnIpad` -egenskap. Den här egenskapen visas som extras i signaturskriptfältet. Stegen för att ändra den är:

   1. Markera fältet Skript för signatur i formuläret.
   1. Välj **XML-källa** -fliken.

      >[!NOTE]
      >
      >Öppna fliken XML-källa genom att klicka på **Visa** > **XML-källa**.

   1. Leta reda på `<ui>` i `<field>` tagga och ändra källkoden så att den ser ut så här:

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. Välj **Designvy** -fliken. I bekräftelserutan klickar du på **Ja**.
   1. Spara formuläret.

1. Återge formuläret i en enhet/webbläsare som stöds.

## Gränssnitt med klottersignaturer {#interfacing-with-the-scribble-signatures}

### Signering {#signing}

När ett signaturskriptfält har lagts till i formuläret och återgetts öppnas en dialogruta när du klickar eller trycker på fältet. Användaren kan klottra en signatur i ritområdet som definieras av en prickad rektangel med en mus, ett finger eller en penna.

![geolokalisering](assets/geolocation.png)

**S.** Pensel **B.** Suddgummi **C.** Geolokalisering **D.** Geoplatsinformation

### Geotaggning {#geo-tagging}

När du klickar på ikonen för geopositionering när du skapar klottret bäddas geografisk plats och tidsinformation in i fältet.

>[!NOTE]
>
I iPad är det som standard obligatoriskt att bädda in geolokaliseringsinformation.

I iPad visas inte geopositioneringsikonen som standard och geopositioneringsinformationen bäddas in automatiskt när du klickar på **OK**.

För iPad kan den här inställningen ändras genom att värdet för `geoLocManadatoryOnIpad` parameter till `0`, i fältets init-parametrar.

* När geopositioneringsinformation är obligatorisk visas ett reducerat ritområde för användaren. Geopositionstext läggs till när användaren klickar på **OK** på det återstående området.
* I andra fall visas användaren med en fullständig rityta. Om användaren väljer att bädda in geopositioneringsinformation, ändras storleken på det här området så att det får plats med geopositioneringstext.

### Rensa en signatur {#clearing-a-signature}

När du använder den här funktionen kan användaren klicka på **Suddgummi** för att rensa fältet och börja om från början. Om geopositioneringsinformation lades till rensas den också.

### Spara en signatur {#saving-a-signature}

Klicka på **OK** -ikonen sparar klottret som en bild i fältet. Bilden och värdena kan skickas till servern för vidare bearbetning. När en användare har klickat **OK**, är klottret låst. Det går inte att redigera signaturen igen med hjälp av klotterwidgeten.

Om du trycker eller klickar på fältet Klottra öppnas dialogrutan i skrivskyddat läge.

![3](assets/3.png)

### Välja ritstiftsstorlek {#selecting-pen-size}

Klicka på **Penslar** om du vill visa en lista med tillgängliga ritstiftsstorlekar. Klicka på en ritstiftsstorlek om du vill använda motsvarande penna.

### Ta bort signaturer från formuläret {#delete-signatures-from-the-form}

Så här tar du bort signaturer från formuläret:

* (Mobila enheter) Tryck länge på signaturfältet och välj **Ja**.
* (Skrivbord) Håll markören över signaturfältet och klicka på knappen **Avbryt** och klickar på **Ja**.
