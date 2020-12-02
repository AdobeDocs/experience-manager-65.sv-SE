---
title: Konfigurera avancerade systemattribut
seo-title: Konfigurera avancerade systemattribut
description: Använd sidan Konfigurera avancerade systemattribut om du vill ändra vissa inställningar i konfigurationsfilen utan att behöva exportera, redigera och importera filen.
seo-description: Använd sidan Konfigurera avancerade systemattribut om du vill ändra vissa inställningar i konfigurationsfilen utan att behöva exportera, redigera och importera filen.
uuid: 6bcfbaa9-f492-46aa-97d2-00fc3e67d0d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 533ad3f7-3905-420d-8bb9-8ae8f14fb28e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 1%

---


# Konfigurera avancerade systemattribut {#configure-advanced-system-attributes}

Använd sidan Konfigurera avancerade systemattribut om du vill ändra vissa inställningar i konfigurationsfilen utan att behöva exportera, redigera och importera filen. (Se [Importera och exportera konfigurationsfilen](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

1. Klicka på **[!UICONTROL Settings > User Management > Configuration > Configure Advanced System Attributes]** i administrationskonsolen.
1. (Valfritt) Ändra något av följande sessionsattribut:

   **Tidsgräns för session (minuter):** Den tid, i minuter, som en användare loggas ut ur systemet automatiskt. Som standard AEM formulärkomponenter som Workbench efter två timmars uttid, oavsett aktivitet eller inaktivitet, och användaren måste logga in igen. Giltiga värden är `1` till `1440`. Standardvärdet är `120` (2 timmar). Den här inställningen uppdaterar `SAML/Producer/assertionValidityInMinutes`-postnyckeln i konfigurationsfilen.

   >[!NOTE]
   >
   >Du bör inte ange en tidsgräns för sessioner under 10 minuter eftersom systemet kanske inte fungerar som det ska. Det rekommenderade värdet är 10-120 (minuter).

   **Tröskelvärde för kontroll (sekunder):** En bufferttid för att kompensera fördröjningar på grund av systemtidsskillnader mellan AEM formulärprogramservrar i ett kluster. AEM blanketterar användarens inloggningstid med den tid (i sekunder) som anges i den här egenskapen. Giltiga värden är `0` till `3600`. Standardvärdet är `60`. Den här inställningen uppdaterar `SAML/Producer/assertionThresholdInSeconds`-postnyckeln i konfigurationsfilen.

   **Maximalt antal tillåtna förnyelser av en försäkran:** Det maximala antalet gånger som en användarsession kan förnyas utan att användaren behöver logga in. Giltiga värden är `0` till `9999`. Värdet `0` betyder att försäkringar inte förnyas. Standardvärdet är 10. Den här inställningen uppdaterar `SAML/Producer/maxAssertionRenewalCount`-postnyckeln i konfigurationsfilen.

1. (Valfritt) Ändra följande attribut för katalogsynkronisering:

   **Loggning av synkroniseringsstatistik:** Anger om användarhantering loggar detaljerad statistik under synkroniseringsprocessen. (Se [Aktivera eller inaktivera detaljerad loggning under synkronisering](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization).)

   **Cron-uttryck för synkroniseringsslutbehandlare:** Intervallet där användarhanteringsförsök misslyckades med synkroniseringar. (Se [Konfigurera alternativet för att försöka igen med katalogsynkronisering](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option).)

   **Timeout för kluster-jobblås i minuter:** Används i klustrade miljöer. Om synkroniseringen på en nod misslyckas och klusterlåset inte frisläpps, anger det här värdet antalet minuter som en annan nod väntar innan låset tvångsförvärvas. Standardvärdet är `15` minuter. Giltiga värden är `1` till `1440` minuter.

1. (Valfritt) Ändra följande attribut och klicka sedan på **[!UICONTROL OK]**:

   **Händelsegranskning i användarhanteraren:** Välj det här alternativet om du vill aktivera granskning av katalogsynkroniseringshändelser och av autentiseringshändelser som lyckade, misslyckade och utelåsta. Som standard är det här alternativet inte markerat om du inte har installerat en komponent som behöver granskas, till exempel Rights Management. Den här inställningen uppdaterar `APSAuditService`-postnyckeln i konfigurationsfilen.

   **Automatiskt skapande av dynamisk grupp:** Möjliggör automatiskt skapande av dynamiska grupper baserat på e-postdomäner. (Se [Skapa en dynamisk grupp](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group).)

Du kan även återgå till de ursprungliga inställningarna för användarhantering genom att klicka på Läs in igen.
