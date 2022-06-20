---
title: Generera renderingar endast för placering för Adobe InDesign
description: Generera FPO-återgivningar av nya och befintliga resurser med hjälp av Experience Manager Assets arbetsflöde och ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 1e4ddd73-a31c-4ddd-94eb-1dac6a4835b3
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 1%

---

# Generera renderingar endast för placering för Adobe InDesign {#fpo-renditions}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/configure-fpo-renditions.html?lang=en) |
| AEM 6.5 | Den här artikeln |

När man lägger in stora mängder material från Experience Manager i Adobe InDesign-dokument måste man vänta ett tag efter det [placera en resurs](https://helpx.adobe.com/indesign/using/placing-graphics.html). Användaren kan inte använda InDesign. Detta stör det kreativa flödet och påverkar användarupplevelsen negativt. Med Adobe kan du tillfälligt placera små renderingar i InDesign-dokument till att börja med. När det slutliga resultatet behövs, till exempel för tryck- och publiceringsarbetsflöden, ersätter det ursprungliga, högupplösta materialet den tillfälliga återgivningen i bakgrunden. Denna asynkrona uppdatering i bakgrunden snabbar upp designprocessen för att öka produktiviteten och hindrar inte den kreativa processen.

Adobe Experience Manager (AEM) innehåller renderingar som endast används för placering (FPO). Dessa FPO-återgivningar har en liten filstorlek men har samma proportioner. Om det inte finns någon FPO-återgivning tillgänglig för en resurs använder Adobe InDesign den ursprungliga resursen i stället. Denna reservfunktion säkerställer att det kreativa arbetsflödet fortsätter utan avbrott.

## Metod för att generera FPO-återgivningar {#approach-to-generate-fpo-renditions}

I Experience Manager kan många metoder bearbeta bilder som kan användas för att generera FPO-återgivningar. De två vanligaste metoderna är att använda inbyggda arbetsflöden i Experience Manager och att använda ImageMagick. Med dessa två metoder kan du konfigurera återgivningsgenerering för nyligen överförda resurser och för de resurser som finns i Experience Manager.

Du kan använda ImageMagick för att bearbeta bilder, inklusive för att generera FPO-återgivningar. Sådana återgivningar nedsamplas, vilket innebär att återgivningens pixeldimensioner minskas proportionellt om den ursprungliga bilden har PPI större än 72. Se [installera och konfigurera ImageMagick så att det fungerar med Experience Manager Assets](best-practices-for-imagemagick.md).

|  | Använda det Experience Manager byggda arbetsflödet | Använda arbetsflödet i ImageMagick | Anmärkningar |
|--- |--- |---|--- |
| För nya resurser | Aktivera FPO-återgivning ([help](#generate-renditions-of-new-assets-using-aem-workflow)) | Kommandoraden Lägg till ImageMagick i arbetsflödet för Experience Manager ([help](#generate-renditions-of-new-assets-using-imagemagick)) | Experience Manager kör arbetsflödet DAM Update Assets för varje överföring. |
| För befintliga resurser | Aktivera FPO-återgivning i ett nytt dedikerat Experience Manager-arbetsflöde ([help](#generate-renditions-of-existing-assets-using-aem-workflow)) | Lägg till ImageMagick-kommandorad i ett nytt dedikerat Experience Manager-arbetsflöde ([help](#generate-renditions-of-existing-assets-using-imagemagick)) | FPO-återgivningar av befintliga resurser kan skapas vid behov eller gruppvis. |

>[!CAUTION]
>
>Skapa arbetsflöden för att generera återgivningar genom att ändra en kopia av standardarbetsflödena. Det förhindrar att ändringar skrivs över när Experience Manager uppdateras, till exempel genom att installera ett nytt Service Pack.

## Generera återgivningar av nya resurser med hjälp av arbetsflödet i Experience Manager {#generate-renditions-of-new-assets-using-aem-workflow}

Så här konfigurerar du arbetsflödesmodellen DAM Update Asset för att aktivera generering av återgivning:

1. Klicka på **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**. Välj **[!UICONTROL DAM Update Asset]** modell och klicka **[!UICONTROL Edit]**.

1. Välj **[!UICONTROL Process Thumbnails]** steg och klicka **[!UICONTROL Configure]**.

1. Klicka på fliken **[!UICONTROL FPO Rendition]**. Välj **[!UICONTROL Enable FPO rendition creation]**.

   ![fpo_rendition_damupdateasset_model](assets/fpo_rendition_damupdateasset_model.png)

1. Justera **[!UICONTROL Quality]** och lägga till eller ändra **[!UICONTROL Format List]** värden efter behov. Som standard är listan med MIME-typer för att generera FPO-återgivningen pjpeg, jpeg, jpg, gif, png, x-png och tiff. Klicka på **[!UICONTROL Done]**.

   >[!NOTE]
   >
   >Återgivningsgenerering stöds för filtyperna JPEG, GIF, PNG, TIFF, PSD och BMP.

1. Om du vill aktivera ändringarna klickar du på **[!UICONTROL Sync]**.

>[!NOTE]
>
>Bilder som är större än 1 280 pixlar på en sida behåller inte pixelmåtten i FPO-återgivningen.

## Generera återgivningar av nya resurser med ImageMagick {#generate-renditions-of-new-assets-using-imagemagick}

I Experience Manager körs arbetsflödet för DAM-uppdatering av tillgångar när en ny resurs överförs. Om du vill använda ImageMagick för att bearbeta återgivningar av nyligen överförda resurser lägger du till ett nytt kommando i arbetsflödesmodellen.

1. Klicka på **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.

1. Välj **[!UICONTROL DAM Update Asset]** modell och klicka **[!UICONTROL Edit]**.

1. Klicka **[!UICONTROL Toggle Side Panel]** i det övre vänstra hörnet och sök efter kommandoradssteg.

1. Dra **[!UICONTROL Command Line]** och lägga till det före **[!UICONTROL Process Thumbnails]** steg.

1. Välj **[!UICONTROL Command Line]** steg och klicka **[!UICONTROL Configure]**.

1. Lägg till önskad information som anpassad **[!UICONTROL Title]** och **[!UICONTROL Description]**. Exempel: FPO-återgivning (som drivs av ImageMagick).

1. I **[!UICONTROL Arguments]** flik, lägga till relevant **[!UICONTROL Mime Types]** om du vill visa en lista med filformat som kommandot gäller för.

   ![imagemagick-mimeType](assets/imagemagick-mimetype.png)

1. I **[!UICONTROL Arguments]** -fliken, i **[!UICONTROL Commands]** lägger du till ett relevant ImageMagick-kommando för att generera FPO-återgivningar.

   Nedan visas ett exempelkommando som genererar FPO-återgivningar i JPEG-format, nedsamplat till 72 PPI, med 10 % kvalitetsinställning och hanterar Adobe Photoshop-filer med flera lager genom att förenkla utdata:

   `convert -quality 10% -units PixelsPerInch ${filename} -resample 72 -flatten cq5dam.fpo.jpeg`

1. Om du vill aktivera ändringarna klickar du på **[!UICONTROL Sync]**.

Mer information om funktioner för kommandoraden i ImageMagick finns i [https://imagemagick.org](https://imagemagick.org).

## Generera återgivningar av befintliga resurser med hjälp av arbetsflödet i Experience Manager {#generate-renditions-of-existing-assets-using-aem-workflow}

Om du vill använda arbetsflödet i Experience Manager för att generera en FPO-återgivning av befintliga resurser skapar du en dedikerad arbetsflödesmodell som använder det inbyggda FPO-återgivningsalternativet.

1. Klicka på **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.

1. Om du vill skapa en modell klickar du på **[!UICONTROL Create]** > **[!UICONTROL Create Model]**.

1. Lägg till en meningsfull **[!UICONTROL Title]** och **[!UICONTROL Name]**.

1. Markera modellen och klicka på **[!UICONTROL Edit]**. Klicka **[!UICONTROL Page Information]** > **[!UICONTROL Open Properties]** och sedan markera **[!UICONTROL Transient Workflow]**. Detta förbättrar skalbarhet och prestanda.

1. Klicka **[!UICONTROL Save]** och **[!UICONTROL Close]**.

1. Klicka **[!UICONTROL Toggle Side Panel]** i det övre vänstra hörnet och sök efter processminiatyrbilder.

1. Välj **[!UICONTROL Process Thumbnails]** och klicka **[!UICONTROL Configure]**. Följ [konfiguration för att generera återgivning av nya resurser med hjälp av arbetsflödet i Experience Manager](#generate-renditions-of-new-assets-using-aem-workflow).

1. Om du vill aktivera ändringarna klickar du på **[!UICONTROL Sync]**.


## Generera återgivningar av befintliga resurser med ImageMagick {#generate-renditions-of-existing-assets-using-imagemagick}

Om du vill använda bearbetningsfunktionerna i ImageMagick för att generera en FPO-återgivning av befintliga resurser skapar du en dedikerad arbetsflödesmodell som använder kommandoraden i ImageMagick för att göra detta.

1. Följ steg 1 till steg 3 från [konfiguration för att generera återgivning av befintliga resurser med hjälp av arbetsflödet i Experience Manager](#generate-renditions-of-existing-assets-using-aem-workflow) -avsnitt.

1. Följ steg 4 till steg 8 från [konfiguration för att generera återgivning av nya resurser med ImageMagick](#generate-renditions-of-new-assets-using-imagemagick) -avsnitt.


## Visa FPO-återgivningar {#view-fpo-renditions}

Du kan kontrollera de genererade FPO-återgivningarna när arbetsflödet har slutförts. Klicka på resursen i Experience Manager Assets användargränssnitt för att öppna en stor förhandsvisning. Öppna den vänstra listen och välj Återgivningar. Du kan även använda kortkommandot `Alt + 3` när förhandsgranskningen är öppen.

Klicka **[!UICONTROL FPO rendition]** för att läsa in förhandsgranskningen. Du kan även högerklicka på återgivningen och spara den i filsystemet.

![rendition_list](assets/rendition_list.png)


## Tips och begränsningar {#tips-limitations}

* Om du vill använda ImageMagick-baserad konfiguration installerar du ImageMagick på samma dator som Experience Manager.
* Om du vill generera FPO-återgivningar av många resurser eller av hela databasen ska du planera och köra arbetsflödena under låg trafiktid. Att generera FPO-renderingar för ett stort antal resurser är en resurskrävande aktivitet och Experience Manager-servrarna måste ha tillräcklig processorkraft och tillräckligt med minne.
* För prestanda och skalbarhet, se [Finjustera ImageMagick](performance-tuning-guidelines.md).
* Mer information om allmän kommandoradshantering för resurser finns i [kommandoradshanterare för att bearbeta resurser](media-handlers.md).
