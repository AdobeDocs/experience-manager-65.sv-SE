---
title: Integrera AEM-formulärarbetsytan med Microsoft Office SharePoint Server
seo-title: Integrera AEM-formulärarbetsytan med Microsoft Office SharePoint Server
description: 'Du kan integrera AEM-formulärarbetsytan med Microsoft Office SharePoint Server. '
seo-description: 'Du kan integrera AEM-formulärarbetsytan med Microsoft Office SharePoint Server. '
uuid: 69d51bdf-729f-4eea-8fae-1e2b8aacaae6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8990b422-f4f6-4080-871a-33cdf7ca6455
docset: aem65
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4

---


# Integrera AEM-formulärarbetsytan med Microsoft Office SharePoint Server{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**- Krav**

**Nödvändig kunskap** Innan du kan lägga till AEM Forms Workspace på SharePoint Server måste du ha tillgång till SharePoint Server med rätt behörighet och du måste känna till URL:en för att få tillgång till Workspace. Stegen nedan förutsätter att du har kunskap om SharePoint Server. Mer information om webbdelar i SharePoint Server finns i Webbdelar i Windows SharePoint Services.

**Användarnivå**- början

Du kan använda AEM Forms Workspace som en webbdel i Microsoft Office SharePoint Server( t.ex. Microsoft Office SharePoint Server 2007). Användare har tillgång till AEM Forms Workspace genom att ansluta till SharePoint-servern via en webbläsare för att ge en enhetlig upplevelse. I den här artikeln får du lära dig de grundläggande stegen för att visa AEM Forms Workspace som en webbdel i Microsoft Office SharePoint Server. Du kan utföra stegen som beskrivs i den här artikeln för att ge en enhetlig upplevelse så att användare som ansluter till din SharePoint-server kan komma åt AEM Forms Workspace från samma port.

>[!NOTE]
>
>Stegen i den här artikeln är specifika för Microsoft SharePoint Server 2007. Du kan också konfigurera HTML Workspace med andra versioner av Microsoft SharePoint som stöds.

## Integrera AEM Forms Workspace med Microsoft Office SharePoint Server 2007 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

Utför följande steg för att integrera AEM Forms Workspace i en webbdel:

1. I en webbläsare navigerar du till SharePoint-webbplatsen, till exempel, `https://[myMOSSserver]:44299/default.aspx` där `[myMOSSserver]` är namnet eller IP-adressen för SharePoint-servern.

   >[!NOTE]
   >
   >44299 är standardportnumret för SharePoint-servern. Portnumret beror på din installation av SharePoint Server.

1. Klicka på **Webbplatsåtgärder** längst upp till höger på webbsidan och välj **Redigera sida**.
1. Klicka på knappen **Lägg till en webbdel** .
1. I dialogrutan Lägg till webbdelar - webbsida, under Övrigt, väljer du **Webbdel** för sidvisning och klickar sedan på **Lägg till**.
1. Klicka på **redigera** i rutan Webbdel i sidvisningsprogrammet och välj **Ändra delad webbdel**.

   >[!NOTE]
   >
   >Rutan Webbdel för sidvisningsprogrammet visas under knappen **Lägg till en webbdel** som du klickade på i steg 3 enligt följande bild (bild 1):

   ![Sidvisningsprogrammets webbdelsruta i Microsoft Office SharePoint-servern.](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   Figur 1. - Rutan Webbdel för sidvisning på Microsoft Office SharePoint-servern.

1. Utför följande åtgärder på sidan för sidvisningsprogrammet:

   1. I rutan Länk anger du URL:en för AEM Forms Workspace, t.ex. `https://[AEM_forms_Server]:8080/lc/ws` där `[AEM_forms_Server]` representerar IP:t eller namnet på AEM-formulärservern.
   1. Klicka på **Utseende** och ändra höjd, bredd och titel så att du kan se hela gränssnittet i arbetsytan. Du kan till exempel ange höjd och bredd till 6 tum respektive 11 tum.
   1. Klicka på **Testa länk**. Ett nytt webbläsarfönster visas med arbetsytan.
   1. (Valfritt) Klicka på **Layout** och ändra layouten för arbetsytan i webbdelen.
   1. (Valfritt) Klicka på **Avancerat** och ändra andra inställningar, till exempel beskrivningen och om arbetsytan kan minimeras eller stängas i webbdelen.

      Klicka på **Använd**.

1. Klicka på **Avsluta redigeringsläge** och kontrollera att du har åtkomst till arbetsytan.

När du har utfört stegen ovan ser SharePoint-webbplatsen ut ungefär som på följande bild (bild 2):

![AEM Forms Workspace är integrerat med Microsoft Office SharePoint Server](assets/aem-forms-workspace.jpg)

Bild 2 - AEM Forms Workspace är integrerat med Microsoft Office SharePoint Server

