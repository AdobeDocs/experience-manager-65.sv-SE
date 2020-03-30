---
title: Hantera agentsignaturbilder
seo-title: Hantera agentsignaturbilder
description: När du har skapat en brevmall kan du använda den för att skapa korrespondens i AEM Forms genom att hantera data, innehåll och bilagor.
seo-description: När du har skapat en brevmall kan du använda den för att skapa korrespondens i AEM Forms genom att hantera data, innehåll och bilagor.
uuid: 48b2697e-6065-4e23-9aa8-333e7b11ede1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: a81cdd53-f0fb-4ac5-b2ec-c19aeee7186e
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Hantera agentsignaturbilder{#manage-agent-signature-images}

## Översikt {#overview}

I Korrespondenshantering kan du använda en bild för att återge agentsignaturer med bokstäver. När du har konfigurerat agentsignaturbilden kan du återge agentsignaturbilden i brevet som signaturen för avsändaragenten när du skapar en bokstav.

AgentSignatureImage DDE är en beräknad DDE som representerar agentens signaturbild. Uttrycket för denna beräknade DDE använder en ny anpassad funktion som exponeras av byggblocket Expression Manager. Den här anpassade funktionen tar agentID och agentFolder som indataparametrar och hämtar bildinnehållet baserat på dessa parametrar. Systemets dataordlista SystemContext ger bokstäver i Correspondence Management tillgång till information i den aktuella systemkontexten. Systemkontexten innehåller information om den inloggade användaren och aktiva konfigurationsparametrar.

Du kan lägga till bilder under mappen cmouseRoot. I [Konfiguration](/help/forms/using/cm-configuration-properties.md)av korrespondenshantering kan du med hjälp av egenskapen CM-användarrot ändra mappen som agentsignaturbilden hämtas från.

Värdet för agentFolder DDE hämtas från CMUserRoot-konfigurationsparametern för konfigurationsegenskaperna för Correspondence Management. Som standard pekar den här konfigurationsparametern på /content/cmUserRoot i CRX-databasen. Du kan ändra värdet på CMUserRoot-konfigurationen i Configuration Properties.
Du kan också åsidosätta standardfunktionen för anpassade funktioner för att definiera din egen logik för att hämta användarsignaturbilden.

## Lägger till agentsignaturbild {#adding-agent-signature-image}

1. Kontrollera att agentsignaturbilden har samma namn som användarens AEM-användarnamn. (Tillägg krävs inte för bildens filnamn.)
1. I CRX skapar du en mapp med namnet `cmUserRoot` i innehållsmappen.

   1. Gå till `https://'[server]:[port]'/crx/de`. Logga in som administratör om det behövs.

   1. Högerklicka på **innehållsmappen** och välj **Skapa** > **Skapa mapp**.

      ![Skapa mapp](assets/1_createnode_cmuserroot.png)

   1. I dialogrutan Skapa mapp anger du namnet på mappen som `cmUserRoot`. Klicka på **Spara alla**.

      >[!NOTE]
      >
      >cmUserRoot är standardplatsen där AEM söker efter agentsignaturbilden. Du kan dock ändra den genom att redigera egenskapen CM-användarrot i konfigurationsegenskaperna [för](/help/forms/using/cm-configuration-properties.md)korrespondenshantering.

1. I Innehållsutforskaren navigerar du till mappen cmUserRoot och lägger till agentsignaturbilden i den.

   1. Gå till `https://'[server]:[port]'/crx/explorer/index.jsp`. Logga in som administratör om det behövs.
   1. Klicka på **Innehållsutforskaren**. Innehållsutforskaren öppnas i ett nytt fönster.
   1. Navigera till mappen cmUserRoot i Innehållsutforskaren och markera den. Högerklicka på **mappen cmUserRoot** och välj **Ny nod**.

      ![Ny nod i cmUserRoot](assets/2_cmuserroot_newnode.png)

      Gör följande poster i raden för ny nod och klicka sedan på den gröna bockmarkeringen.

      **Namn:** JohnDoe (eller namnet på din agentsignaturfil)

      **Typ:** nt:fil

      Under `cmUserRoot` mappen skapas en ny mapp med namnet `JohnDoe` (eller namnet som du angav i föregående steg).

   1. Klicka på den nya mappen som du har skapat (här `JohnDoe`). Innehållsutforskaren visar mappens innehåll som nedtonat.

   1. Dubbelklicka på egenskapen **jcr:content** , ange dess typ som **not:resource** och klicka sedan på den gröna bockmarkeringen för att spara posten.

      Om egenskapen inte finns skapar du först en egenskap med namnet jcr:content.

      ![jcr:egenskapen content](assets/3_jcrcontentntresource.png)

      Bland de underordnade egenskaperna för jcr:content finns jcr:data, som är nedtonat. Dubbelklicka på jcr:data. Egenskapen kan redigeras och knappen Välj fil visas i posten. Klicka på **Välj fil** och välj den bildfil som du vill använda som logotyp. Bildfilen behöver inte ha något tillägg.

      ![JCR-data](assets/5_jcrdata.png)
   Klicka på **Spara alla**.

1. Kontrollera att den XDP\layout som du använder i bokstaven har ett bildfält längst ned till vänster (eller någon annan lämplig plats i layouten där du vill återge signaturen) för att återge signaturbilden.
1. När du skapar korrespondensen väljer du ett bildfält för signaturbilden på fliken Data enligt följande:

   1. Välj System på snabbmenyn Länkningstyp i den högra rutan.

   1. Välj DDE för agentSignatureImage i listan i panelen Dataelement för SystemContext DD.

   1. Spara brevet.

1. När brevet återges kan du se din signatur i förhandsvisningen av bokstaven i bildfältet enligt layouten.

   ![Agentsignaturbild i brevet](assets/letterwithsignature.png)

