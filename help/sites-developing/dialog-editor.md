---
title: Dialogruteredigeraren
seo-title: Dialog Editor
description: Dialogruteredigeraren har ett grafiskt gränssnitt för att enkelt skapa och redigera dialogrutor och ställningar
seo-description: The dialog editor provides a graphical interface for easily creating and editing dialog boxes and scaffolds
uuid: 64d3fb12-8638-441b-8595-c590d48f3072
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: b7ac457d-3689-4f5d-9ceb-ff6a9944e7eb
exl-id: 57303608-c3e1-4201-8054-1a1798613e2c
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Dialogruteredigeraren{#dialog-editor}

Dialogruteredigeraren har ett grafiskt gränssnitt för att enkelt skapa och redigera dialogrutor och ställningar.

Om du vill se hur det fungerar går du till CRXDE Lite och öppnar utforskarträdet för att `/libs/foundation/components/chart` och dubbelklicka på noden `dialog`:

![chlimage_1-247](assets/chlimage_1-247.png)

Dialogrutenoden öppnas i **dialogruteredigerare**:

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## Översikt över användargränssnittet {#user-interface-overview}

Dialogrutans redigeringsgränssnitt består av fyra rutor:

* The **palett**, längst upp till vänster. Den här rutan innehåller de widgetar som är tillgängliga för att skapa en dialogruta, t.ex. flikpaneler, textfält, markeringslistor och knappar. Du kan expandera de olika kategorierna på paletten genom att klicka på den avgränsande listen.
* The **struktur** i det nedre vänstra hörnet. I den här rutan visas den hierarkiska strukturen för noder som utgör dialogdefinitionen. Du kan se samma struktur genom att expandera dialognoden i CRXDE Lite eller CRX Content Explorer.
* The **återge** i mitten av fönstret. I det här fönstret visas hur den dialogrutedefinition som definierats i strukturpanelen återges som en faktisk dialogruta.
* The **egenskaper** fönster. I den här rutan visas egenskaperna för den nod som är markerad i strukturpanelen.

### Använda Dialog Editor {#using-the-dialog-editor}

Om du vill skapa en dialogruta drar och släpper användaren element från paletten till strukturpanelen på plats i dialogrutans definitionshierarki.

När den önskade strukturen är klar klickar användaren på **Spara**, högst upp i återgivningsrutan.

>[!CAUTION]
>
>Observera att dialogredigeraren är avsedd för att skapa är relativt enkla dialogrutor och kanske inte kan redigera mer komplexa dialogrutedefinitioner. Om dialogruteredigeraren inte tillåter redigering av en dialogstruktur, måste dialogdefinitionen skapas och/eller redigeras manuellt genom direktredigering av nodstrukturen med exempelvis CRXDE Lite eller CRX Content Explorer.

### Skapa en ny dialogruta {#creating-a-new-dialog}

Om du vill skapa en ny dialogruta måste du välja den komponent som behövs klickar du på **Skapa...** och sedan **Skapa dialogruta...**.

Ange nödvändig information och klicka sedan på **Spara alla** - nu kan du dubbelklicka på dialogrutan för att öppna den med redigeraren.

### Använda Dialogruteredigeraren för skåp {#using-the-dialog-editor-for-scaffolds}

Ett ställningar är en speciell sida som innehåller ett formulär som kan fyllas i och skickas i ett enda steg. På så sätt kan du snabbt skapa en sida med det innehåll som anges.

Formuläret som utgör ett ställningar definieras av en dialogrutedefinition, precis som en vanlig dialogruta, även om det visas på scensidan i ett annat format. Eftersom dialogrutedefinitioner används för att definiera ställningar kan du skapa ställningar med hjälp av dialogruteredigeraren. Observera, att när du använder dialogruteredigeraren på det här sättet visas dialogrutans definition i form av en dialogruta, inte som ett ställningar.

Se [Ställning](/help/sites-authoring/scaffolding.md) om du vill ha mer information om hur du använder dialogruteredigeraren för att skapa ställningar.
