---
title: Skriva ut kanal och webbkanal
description: Importera utskriftskanalmallar samt skapa och aktivera webbkanalsmallar
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: cd7dbdac-dc76-4a1f-b850-0a9f47ae08de
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---

# Skriva ut kanal och webbkanal{#print-channel-and-web-channel}

Interaktiv kommunikation kan distribueras via två kanaler: tryck och webb. Tryckkanalen används för att skapa PDF- och pappersdokument, t.ex. ett tryckt brev som påminnelse om betalning av försäkringspremier, medan webbkanalen används för att leverera onlineupplevelser, t.ex. kreditkortsutdrag på en webbplats.

Författare av interaktiv kommunikation kan återanvända resurser som dokumentfragment och bilder för att skapa både utskrifts- och webbversioner av interaktiv kommunikation.

En av förutsättningarna för [Skapa en interaktiv kommunikation](../../forms/using/create-interactive-communication.md) ska ha mallarna för utskrift och/eller webbkanal tillgängliga på servern. Mallförfattare skapar själva webbkanalsmallen i AEM, men utskriftskanalmallen XDP skapas i Adobe Forms Designer och överförs till servern.

## Utskriftskanal {#printchannel}

Utskriftskanalen i en interaktiv kommunikation använder XFA-formulärmallen, XDP. En XDP är utformad i Adobe Forms Designer. Mer information om hur du skapar utskriftskanalmallar finns i [Layoutdesign](../../forms/using/layout-design-details.md). Om du vill använda en utskriftskanalmall i din interaktiva kommunikation måste du överföra mallen till AEM Forms-servern.

### Ladda upp utskriftskanalmall för interaktiv kommunikation {#upload-interactive-communication-print-channel-template}

Om du vill överföra mallen måste du vara medlem i gruppen formulär-användare. Följ de här stegen för att överföra utskriftskanalmallen (XDP) till AEM Forms:

1. Välj **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.

1. Välj **[!UICONTROL Create]** > **[!UICONTROL File Upload]**.

   Navigera och välj lämplig utskriftskanalmall (XDP) och välj **[!UICONTROL Open]**.

## Webbkanal {#web-channel}

Mallförfattare och administratörer kan skapa, redigera och aktivera webbmallar. Om du vill att andra användare ska kunna skapa webbmallar måste du ge dem behörighet. Mer information finns i [Behörighetsadministration för användare, grupp och åtkomst](/help/sites-administering/user-group-ac-admin.md).

### Redigerar webbkanalsmall {#authoring-web-channel-template}

Om du vill skapa en webbkanalmall måste du först skapa en mallmapp. När du har skapat en webbmall i en mallmapp måste du aktivera mallen så att formuläranvändarna kan skapa en webbkanal för en interaktiv kommunikation som är baserad på mallen.

Så här skapar du en webbkanalsmall:

1. Skapa en mallmapp om du vill behålla dina webbmallar för interaktiv kommunikation, om du inte redan har en. Mer information finns i Mallmappar i [Sidmallar - redigerbara](/help/sites-developing/page-templates-editable.md).

   1. Välj **[!UICONTROL Tools]** ![verktyg](assets/tools.png) > **[!UICONTROL Configuration Browser]**.
      * Se [Konfigurationsläsaren](/help/sites-administering/configurations.md) mer information.
   1. På sidan Configuration Browser väljer du **[!UICONTROL Create]**.
   1. I dialogrutan Skapa konfiguration anger du en rubrik för mappen och markerar **[!UICONTROL Editable Templates]** och markera **[!UICONTROL Create]**.

      Mappen skapas och visas på sidan Konfigurationsläsare.

1. Navigera till rätt mallmapp och skapa en webbmall.

   1. Navigera till rätt mallmapp genom att välja **[!UICONTROL Tools]** > **[!UICONTROL Templates]** > **`[Folder]`**.
   1. Välj **[!UICONTROL Create]**.
   1. Välj **[!UICONTROL Interactive Communication - Web Channel]** och markera **[!UICONTROL Next]**.
   1. Ange en malltitel och beskrivning och välj sedan **[!UICONTROL Create]**.

      Mallen skapas och en dialogruta visas.

   1. Välj **[!UICONTROL Open]** för att öppna mallen som du har skapat i mallredigeraren.

      Mallredigeraren visas.

      ![webbkanalmall](assets/webchanneltemplate.png)

      När du skapar eller redigerar en mall finns det olika aspekter som mallskaparen kan definiera. Att skapa eller redigera en mall liknar att skapa sidor. Mer information finns i Redigera mallar - Mallförfattare i [Skapa sidmallar](/help/sites-authoring/templates.md).

1. Aktivera mallen om du vill tillåta att den här mallen används för att skapa interaktiv kommunikation.

   1. Välj **[!UICONTROL Tools]** ![verktyg](assets/tools.png) > **[!UICONTROL Templates]**.
   1. Navigera till rätt mall, markera den och markera **[!UICONTROL Enable]** och i varningsmeddelandet väljer du **[!UICONTROL Enable]**.

      Mallen är aktiverad och dess status visas som Aktiverad. Nu kan du skapa en interaktiv kommunikation där du kan använda den nya webbkanalsmallen.

### Skriva ut kanal som master för webbkanal {#print-channel-as-master-for-web-channel}

När du skapar en interaktiv kommunikation kan författare välja det här alternativet för att skapa webbkanalen synkroniserat med utskriftskanalen. Om du använder en tryckkanal som huvudkanal för webbkanalen kan du säkerställa att innehållet, arvet och databindningen för webbkanalen hämtas från tryckkanalen och att ändringarna som görs i den kan återspeglas i webbkanalen. De som skapar interaktiv kommunikation får dock bryta arvet för specifika komponenter i webbkanalen efter behov.

![Skriva ut kanal som master](assets/create_ic_print_master_new.png) ![Webbkanal med utskriftskanal som master](assets/create_ic_print_master_web_new.png)
