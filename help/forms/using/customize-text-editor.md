---
title: Anpassa textredigeraren
description: Lär dig hur du anpassar textredigeraren i en Adobe Experience Manager Forms-miljö.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 1dd3f55c-24f7-4331-a9a3-c9223e613fec
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# Anpassa textredigeraren{#customize-text-editor}

## Ökning {#overview}

Du kan anpassa textredigeraren i Hantera resurser och Skapa korrespondensgränssnitt för att lägga till fler teckensnitt och teckenstorlekar. De här teckensnitten är engelska och icke-engelska, till exempel japanska, teckensnitt.

Du kan anpassa för att ändra följande i teckensnittsinställningarna:

* Teckensnittsfamilj och -storlek
* Egenskaper som höjd och teckenavstånd
* Standardvärden för teckensnittsfamilj och -storlek, höjd, teckenavstånd och datumformat
* Punktindrag

Gör följande:

1. [Anpassa teckensnitt genom att redigera filen tbxeditor-config.xml i CRX](#customizefonts)
1. [Lägga till anpassade teckensnitt på klientdatorn](#addcustomfonts)

## Anpassa teckensnitt genom att redigera filen tbxeditor-config.xml i CRX {#customizefonts}

Så här anpassar du teckensnitt genom att redigera filen tbxeditor-config.xml:

1. Gå till `https://'[server]:[port]'/[ContextPath]/crx/de` och logga in som administratör.
1. I programmappen skapar du en mapp med namnet config med en sökväg/struktur som liknar konfigurationsmappen, som finns på libs/fd/cm/config, enligt följande:

   1. Högerklicka på objektmappen i följande sökväg och välj **Överläggsnod**:

      `/libs/fd/cm/config`

      ![Överläggsnod](assets/1-1.png)

   1. Kontrollera att dialogrutan Overlay Node har följande värden:

      **Sökväg:** /libs/fd/cm/config

      **Plats:** /apps/

      **Matcha nodtyper:** Markerad

      ![Överläggsnod](assets/2.png)

   1. Klicka **OK**. Mappstrukturen skapas i programmappen.

   1. Klicka **Spara alla**.

1. Skapa en kopia av filen tbxeditor-config.xml i den nya konfigurationsmappen genom att följa stegen nedan:

   1. Högerklicka på filen tbxeditor-config.xml på libs/fd/cm/config och välj **Kopiera**.
   1. Högerklicka på följande mapp och välj **Klistra in:**

      `apps/fd/cm/config`

   1. Namnet på den inklistrade filen är som standard `copy of tbxeditor-config.xml.` Byt namn på filen till `tbxeditor-config.xml` och klicka **Spara alla**.

1. Öppna filen tbxeditor-config.xml i apps/fd/cm/config och gör sedan nödvändiga ändringar.

   1. Dubbelklicka på filen tbxeditor-config.xml i apps/fd/cm/config. Filen öppnas.

      ```xml
      <editorConfig>
         <bulletIndent>0.25in</bulletIndent>
      
         <defaultDateFormat>DD-MM-YYYY</defaultDateFormat>
      
         <fonts>
            <default>Times New Roman</default>
            <font>_sans</font>
            <font>_serif</font>
            <font>_typewriter</font>
            <font>Arial</font>
            <font>Courier</font>
            <font>Courier New</font>
            <font>Geneva</font>
            <font>Georgia</font>
            <font>Helvetica</font>
            <font>Tahoma</font>
            <font>Times New Roman</font>
            <font>Times</font>
            <font>Verdana</font>
         </fonts>
      
         <fontSizes>
            <default>12</default>
            <fontSize>8</fontSize>
            <fontSize>9</fontSize>
            <fontSize>10</fontSize>
            <fontSize>11</fontSize>
            <fontSize>12</fontSize>
            <fontSize>14</fontSize>
            <fontSize>16</fontSize>
            <fontSize>18</fontSize>
            <fontSize>20</fontSize>
            <fontSize>22</fontSize>
            <fontSize>24</fontSize>
            <fontSize>26</fontSize>
            <fontSize>28</fontSize>
            <fontSize>36</fontSize>
            <fontSize>48</fontSize>
            <fontSize>72</fontSize>
         </fontSizes>
      
         <lineHeights>
            <default>2</default>     
            <lineHeight>2</lineHeight>
            <lineHeight>3</lineHeight>
            <lineHeight>4</lineHeight>
            <lineHeight>5</lineHeight>
            <lineHeight>6</lineHeight>
            <lineHeight>7</lineHeight>
            <lineHeight>8</lineHeight>
            <lineHeight>9</lineHeight>
            <lineHeight>10</lineHeight>
            <lineHeight>11</lineHeight>
            <lineHeight>12</lineHeight>
            <lineHeight>13</lineHeight>
            <lineHeight>14</lineHeight>
            <lineHeight>15</lineHeight>
            <lineHeight>16</lineHeight>
         </lineHeights>
      
         <letterSpacings>
            <default>0</default>
            <letterSpacing>0</letterSpacing>
            <letterSpacing>1</letterSpacing>
            <letterSpacing>2</letterSpacing>
            <letterSpacing>3</letterSpacing>
            <letterSpacing>4</letterSpacing>
            <letterSpacing>5</letterSpacing>
            <letterSpacing>6</letterSpacing>
            <letterSpacing>7</letterSpacing>
            <letterSpacing>8</letterSpacing>
            <letterSpacing>9</letterSpacing>
            <letterSpacing>10</letterSpacing>
            <letterSpacing>11</letterSpacing>
            <letterSpacing>12</letterSpacing>
            <letterSpacing>13</letterSpacing>
            <letterSpacing>14</letterSpacing>
            <letterSpacing>15</letterSpacing>
            <letterSpacing>16</letterSpacing>
         </letterSpacings>
      </editorConfig>
      ```

   1. Gör önskade ändringar i filen så att du kan ändra följande i teckensnittsinställningarna:

      * Lägg till eller ta bort teckensnittsfamilj och -storlek
      * Egenskaper som höjd och teckenavstånd
      * Standardvärden för teckensnittsfamilj och -storlek, höjd, teckenavstånd och datumformat
      * Punktindrag

      Om du till exempel vill lägga till ett japanskt teckensnitt med namnet Sazanami Mincho Medium måste du göra följande i XML-filen: `<font>Sazanami Mincho Medium</font>`. Du måste också ha det här teckensnittet installerat på klientdatorn för att kunna komma åt och arbeta med teckensnittsanpassningen. Mer information finns i [Lägga till anpassade teckensnitt på klientdatorn](#addcustomfonts).

      Du kan också ändra standardinställningarna för olika delar av texten och ta bort teckensnitten från textredigeraren genom att ta bort posterna.

   1. Klicka **Spara alla**.

## Lägga till anpassade teckensnitt på klientdatorn {#addcustomfonts}

När du öppnar ett teckensnitt i textredigeraren för Korrespondenshantering måste det finnas på klientdatorn som du använder för att få åtkomst till Correspondence Management. För att kunna använda ett anpassat teckensnitt i textredigeraren måste du först installera det på klientdatorn.

Mer information om hur du installerar teckensnitt finns i:

* [Installera eller avinstallera teckensnitt i Windows](https://windows.microsoft.com/en-us/windows-vista/install-or-uninstall-fonts)
* [Mac Basics: Font Book](https://support.apple.com/en-us/HT201749)

## Få tillgång till teckensnittsanpassningar {#access-font-customizations}

När du har ändrat teckensnitt i `tbxeditor-config.xml` filen i CRX och de teckensnitt som krävs på klientdatorn som används för att få åtkomst till AEM Forms visas ändringarna i textredigeraren.

Till exempel har teckensnittet Sazanami Mincho Medium lagts till i [Anpassa teckensnitt genom att redigera filen tbxeditor-config.xml i CRX](#customizefonts) proceduren visas i textredigerarens användargränssnitt enligt följande:

![sazanamiminchointext](assets/sazanamiminchointext.png)

>[!NOTE]
>
>Om du vill visa text på japanska måste du först ange texten med japanska tecken. När du använder ett anpassat japanskt teckensnitt formateras texten endast på ett visst sätt. Användning av ett anpassat japanskt teckensnitt ändrar inte engelska eller andra tecken till japanska tecken.
