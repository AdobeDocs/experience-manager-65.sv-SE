---
title: Aktivera filkonvertering med flera trådar
seo-title: Aktivera filkonvertering med flera trådar
description: Lär dig hur du aktiverar filkonvertering med flera trådar.
seo-description: Lär dig hur du aktiverar filkonvertering med flera trådar.
uuid: 830c78aa-4f68-4e01-8b24-69a0275689c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 85d655bb-1b6b-4b4d-ae39-eca3ef9b7fd7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Aktivera filkonvertering med flera trådar {#enabling-multi-threaded-file-conversions}

Med PDF Generator kan du aktivera flertrådiga filkonverteringar för vissa typer av filer. Konvertering av flertrådade filer förbättrar prestanda för PDF Generator genom att det kan utföra flera konverteringar samtidigt.

## Möjliggör flertrådskonvertering av dokument i OpenOffice, Word och PowerPoint {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

Som standard kan PDF Generator bara konvertera ett OpenOffice-, Microsoft Word- eller PowerPoint-dokument åt gången. Om du aktiverar flertrådskonvertering kan PDF Generator konvertera fler än ett av dokumenten samtidigt. PDF Generator startar flera instanser av OpenOffice eller PDFMaker (används för att utföra Word- och PowerPoint-konverteringar).

>[!NOTE]
>
>Flertrådade filkonverteringar stöds inte i Microsoft Word 2003 och PowerPoint 2003. Om du vill aktivera flertrådskonvertering uppgraderar du till Microsoft Word 2007 och PowerPoint 2007 eller Microsoft Word 2010 och PowerPoint 2010.

>[!NOTE]
>
>Flertrådade filkonverteringar stöds inte i Microsoft Excel, Microsoft Visio, Microsoft Project eller Microsoft Publisher.

Varje instans av OpenOffice eller PDFMaker startas med ett separat användarkonto. Varje användarkonto som du lägger till måste vara en giltig användare med administratörsbehörighet på formulärserverdatorn. I en klustrad miljö måste samma uppsättning användare vara giltiga för alla noder i klustret.

På sidan Användarkonton i administrationskonsolen kan du ange vilka användarkonton som ska användas för filkonvertering med flera trådar. Du kan lägga till konton, ta bort dem eller ändra kontolösenord. Om du kör PDF Generator på Windows Server 2003 eller Windows Server 2008 ska du lägga till minst tre användarkonton med administratörsbehörighet.

När du lägger till användare för OpenOffice, Microsoft Word eller Microsoft PowerPoint på Windows Server 2003 eller 2008, eller för OpenOffice på Linux eller Sun™ Solaris™, stänger du de inledande dialogrutorna för aktivering för alla användare.

### Lägg till rättigheten att ersätta token på processnivå {#add-the-right-to-replace-the-process-level-token}

I ett Windows-operativsystem måste administratörens användarkonton som används för PDF-konvertering (PDFG-användare) ersätta tokenbehörighet på processnivå. Du kan lägga till den här rättigheten med hjälp av grupprincipredigeraren:

1. Klicka på Kör på Start-menyn i Windows och ange gpedit.msc.
1. Klicka på Lokal datorprincip > Datorkonfiguration > Windows-inställningar > Skyddsinställningar > Lokala principer > Tilldelning av användarrättigheter. Redigera principen *Ersätt en token* på processnivå så att den omfattar gruppen Administratörer.
1. Lägg till användaren i posten Ersätt en processnivåtoken.

### Ytterligare konfiguration krävs för OpenOffice, Microsoft Word och Microsoft PowerPoint på Windows Server 2008 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Om du kör OpenOffice, Microsoft Word eller Microsoft PowerPoint på Windows Server 2008 inaktiverar du UAC för varje användare som läggs till.

1. Klicka på Kontrollpanelen > Användarkonton > Aktivera eller inaktivera Kontroll av användarkonto.
1. Avmarkera rutan Använd UAC (User Account Control) för att skydda datorn och klicka på OK.
1. Starta om datorn för att inställningarna ska börja gälla.

### Ytterligare konfiguration krävs för OpenOffice på Linux eller Solaris {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. Lägg till användarkonton. (Se [Lägga till ett användarkonto](enabling-multi-threaded-file-conversions.md#add-a-user-account).)
1. Därefter gör du ändringar i filen /etc/sudoers. Standardbehörigheten för den här filen är 440. Ändra behörigheten för den här filen till skrivbar.
1. Lägg till poster för ytterligare användare (andra än administratören som kör formulärservern) i filen /etc/sudoers. Om du till exempel kör AEM-formulär som en användare med namnet lcadm och en server med namnet myhost, och du vill personifiera användare1 och användare2, lägger du till följande poster i /etc/sudoers:

   ```as3
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   Med den här konfigurationen kan lcadm köra valfritt kommando på värden&quot;myhost&quot; som&quot;user1&quot; eller&quot;user2&quot; utan att fråga efter lösenord.

   >[!NOTE]
   >
   >Se till att du har tilldelat användarrollerna system och PDFG till user1 och user2. Information om hur du tilldelar PDFG-roll till en användare finns i [Lägga till ett användarkonto](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. I /etc/sudoers-filen kan du söka efter och kommentera den här raden genom att lägga till ett nummertecken (#) i början av raden:

   ```as3
   Defaults requiretty
   ```

   Detta gör att du kan lägga till Linux-användare.

1. Ändra behörigheten för filen etc/sudoers tillbaka till 440.
1. Tillåt alla användare som du har lagt till via [Lägg till ett användarkonto](enabling-multi-threaded-file-conversions.md#add-a-user-account) att ansluta till formulärservern. Om du till exempel vill ge en lokal användare med namnet user1 behörighet att ansluta till formulärservern använder du följande kommando

   `xhost +local:user1@`

   Mer information finns i dokumentationen för kommandot xhost.

1. Starta om servern.

>[!NOTE]
>
>OpenOffice måste vara installerat på en katalogplats som alla PDFG-användare har åtkomst till. Du kan verifiera detta genom att logga in som PDFG-användare och kontrollera om du kan starta OpenOffice utan problem.

### Lägg till ett användarkonto {#add-a-user-account}

1. I administrationskonsolen klickar du på Tjänster > PDF Generator > Användarkonton.
1. Klicka på Lägg till och ange användarnamnet och lösenordet för en användare som har administratörsbehörighet på formulärservern. Om du konfigurerar användare för OpenOffice stänger du de inledande dialogrutorna för OpenOffice-aktivering.

   >[!NOTE]
   >
   >Om du konfigurerar användare för OpenOffice kan antalet instanser av OpenOffice inte vara större än antalet användarkonton som anges i det här steget.

1. Starta om formulärservern.

### Ta bort en användare från listan som används för filkonvertering med flera trådar {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. I administrationskonsolen klickar du på Tjänster > PDF Generator > Användarkonton.
1. Klicka i kryssrutan bredvid användaren som du vill ta bort och klicka på Ta bort.
1. Klicka på Ta bort på bekräftelsesidan.
1. Starta om formulärservern.

### Ändra lösenordet för ett konto {#change-the-password-for-an-account}

1. I administrationskonsolen klickar du på Tjänster > PDF Generator > Användarkonton.
1. Klicka på användarnamnet och ange och bekräfta det nya lösenordet. Lösenordet måste matcha användarens systemlösenord.

