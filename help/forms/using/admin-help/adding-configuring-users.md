---
title: Lägga till och konfigurera användare
description: Med inställningarna för användarhantering i administrationskonsolen kan du skapa eller ta bort användare och konfigurera andra användarinställningar.
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
exl-id: 50eea35d-d844-4f4b-9cbe-7d84bd6b1e3b
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 0%

---

# Lägga till och konfigurera användare {#adding-and-configuring-users}

Användar- och gruppinformation lagras i ett tredjepartslagringssystem, till exempel en LDAP-katalog. Användarhantering skriver inte till lagringssystemet från tredje part. I stället synkroniseras användar- och gruppinformationen med sin egen databas med användarhanteringen

## Skapa en användare {#create-a-user}

När du skapar användare kan du lägga till dem i grupper och tilldela roller till dem.

1. I administrationskonsolen klickar du på **[!UICONTROL Settings > User Management > Users and Groups]** och klicka **[!UICONTROL New User]**. .
1. Under **[!UICONTROL General Settings]**, anger information efter behov och klickar sedan på **[!UICONTROL Next]**. Mer information om inställningarna finns i [Användarinställningar](adding-configuring-users.md#user-settings).
1. (Valfritt) Om du vill lägga till användaren i en grupp klickar du på **[!UICONTROL Find Groups]** och gör följande:

   * I **[!UICONTROL Find]** skriver du hela eller delar av gruppnamnet.
   * Välj den domän som ska sökas igenom, välj det antal objekt som ska visas och klicka på **[!UICONTROL Find]**.
   * (Valfritt) Om du vill visa gruppinformation markerar du gruppnamnet och klickar sedan på **[!UICONTROL OK]** för att återgå till sökresultatsidan.
   * Markera kryssrutan för gruppen och klicka på **[!UICONTROL OK]**.
   * Klicka på **[!UICONTROL Next]**.

1. (Valfritt) Om du vill tilldela användare roller klickar du på **[!UICONTROL Find Roles]** markerar du kryssrutan för de roller som ska tilldelas och klickar sedan på **[!UICONTROL OK]**.
1. Klicka på **[!UICONTROL Finish]**.

   >[!NOTE]
   >
   >Om du stöter på inloggningsproblem med användaren kan du läsa [AEM Forms på JEE-användare kan inte logga in på AEM Forms på OSGi-sidan](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html).

## Användarinställningar {#user-settings}

Ange följande inställningar när du skapar eller redigerar en användare.

**Kanoniskt namn:** (Obligatoriskt) Unik identifierare för användaren. Varje användare och grupp i en domän måste ha ett unikt kanoniskt namn. Markera kryssrutan Systemgenererad om du vill att användarhantering ska tilldela ett unikt värde eller avmarkera kryssrutan och ange ett anpassat värde för det kanoniska namnet.

Undvik att använda understreck (_) i kanoniska namn, till exempel `sample_user`. När du söker efter användare baserat på deras kanoniska namn, returneras inte användare som innehåller understreck.

**Förnamn:** (Obligatoriskt) Användarens angivna namn

**Efternamn:** (obligatoriskt) Användarens familjenamn

**Namn:** Användarens fullständiga namn eller visningsnamn. Om till exempel Förnamn = Gloria och Efternamn = Rios, används Gemensamt namn = Gloria Rios.

**E-post:** Användarens e-postadress

**Telefon:** Användarens telefonnummer

**Beskrivning:** Valfri beskrivning. Använd det här fältet som det passar din organisations behov.

**Adress:** Användarens postadress

**Organisation:** Organisation som användaren tillhör

**E-postalias:** Användarens e-postalias. Avgränsa e-postalias med kommatecken.

**Domän:** Domän som användaren tillhör

**Språk:** Användarens ISO-språk

**Affärskalendernyckel:** Ger dig möjlighet att mappa en affärskalender till en användare baserat på värdet för den här inställningen. Affärskalendrar definierar affärsdagar och icke-affärsdagar. AEM kan använda affärskalendrar vid beräkning av framtida datum och tidpunkter för händelser som påminnelser, deadlines och eskalering. Hur du tilldelar användare affärskalendernycklar beror på om du använder en företagsdomän, lokal domän eller hybriddomän. (Se [Lägga till domäner](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

Om du använder en lokal domän eller hybriddomän lagras information om användare endast i databasen för användarhantering. För de här användarna anger du en sträng i Business Calendar Key. Mappa sedan affärsbokskalenyckeln (strängen) till en affärskalender i ett formulärarbetsflöde.

Om du använder en företagsdomän finns information om användare i ett tredjepartslagringssystem, till exempel en LDAP-katalog. Användarhantering synkroniserar användarinformation från katalogen med databasen för användarhantering. Med den här funktionen kan du mappa en affärskalendernyckel till ett fält i LDAP-katalogen. Tänk dig till exempel ett scenario där varje användarpost i din katalog innehåller ett landfält och du vill tilldela affärskalendrar baserat på det land där användaren finns. I det här fallet anger du landfältsnamnet som värde för nyckelinställningen för affärskalender. Du kan sedan mappa affärskalendernycklarna (de värden som definieras för landfältet i LDAP-katalogen) till affärskalendrar i formulärarbetsflödet.

Mer information om affärskalendrar, inklusive hur du mappar affärskalendernycklar till affärskalendrar finns i [Konfigurera affärskalendrar](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

Begränsa namnet till färre än 53 tecken. Ett kortare namn förhindrar problem med att visa affärskalendernyckeln på processhanteringssidorna i administrationskonsolen.

**Användar-ID:** (Obligatoriskt) Användar-ID som användaren använder för att logga in. Användar-ID är inte skiftlägeskänsligt och måste vara unikt i domänen.

I företagsdomäner ska du använda ett icke-DN-attribut som användar-ID eftersom användarens unika namn kan ändras om användaren flyttar till en annan del av organisationen. Den här inställningen beror på katalogservern. Värdet är `objectGUID` för Active Directory 2003, `nsuniqueID` för Sun™ One, och `guid` för eDirectory.

Kontrollera att användar-ID:t är unikt. Använd inte en som tilldelats en borttagen användare.

AEM kan inte skilja mellan användarkonton som har identiska användar-ID:n och lösenord, men som tillhör olika domäner. För att undvika det här problemet ska du inte skapa konton som har samma användar-ID på flera domäner.

När du använder SQL Server som databas kan du inte skapa ett användar-ID som är längre än 255 tecken.

När du använder MySQL kan användar-ID:t innehålla utökade tecken. När en jämförelse görs mellan två strängar, till exempel abcde och âbcdé, anses de vara samma. Om till exempel en ny användare har lagts till i databasen vid synkronisering, görs en jämförelse för att kontrollera om det finns en användare med samma användar-ID i databasen. Om användare *abcde* finns i databasen när den nya användaren *âbcdé* läggs till kan jämförelsen inte skilja mellan de två namnen. Det antas att användaren finns i databasen och att den nya användaren ignoreras och inte läggs till.

Undvik att skapa användarnamn som börjar med ett nummertecken (#). Vid uppgiftssökningar returneras inga resultat för de användarnamnen. (Se [Arbeta med uppgifter](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**Lösenord och Bekräfta lösenord:** Lösenord som användaren använder för att logga in. Det måste innehålla minst åtta tecken. Inget lösenord krävs för en användare som är en del av en hybriddomän.

## Visa information om en användare {#view-details-about-a-user}

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Användare och grupper.
1. Ange information för att begränsa sökningen och markera Användare i listan In och klicka sedan på Sök. Resultatet av sökningen visas längst ned på sidan. Du kan sortera listan genom att klicka på någon av kolumnrubrikerna.
1. Klicka på namnet på den användare som du vill visa information om. På sidan Redigera användare visas information om användaren nedan:

   * Allmän identifieringsinformation, som namn, e-postadress, adress, domän och organisation
   * Roller som tilldelats användaren
   * Grupper som användaren är medlem i

## Ändra lösenordet för en lokal användare {#change-the-password-for-a-local-user}

1. I administrationskonsolen klickar du på **[!UICONTROL Settings > User Management > Users and Groups]**.
1. Ange information om du vill begränsa sökningen efter en viss användare och klicka på **[!UICONTROL Find]**. Resultatet av sökningen visas längst ned på sidan. Du kan sortera listan genom att klicka på någon av kolumnrubrikerna.
1. Klicka på användarens namn och klicka sedan på **[!UICONTROL Change Password]**.
1. Skriv och bekräfta det nya lösenordet och klicka sedan på **[!UICONTROL OK]**. Lösenordet måste innehålla minst åtta tecken.

## Redigera en användares egenskaper {#edit-a-user-s-properties}

1. I administrationskonsolen klickar du på **[!UICONTROL Settings > User Management > Users and Groups]**.
1. Gör följande för att hitta användaren att redigera:

   * I **[!UICONTROL Find]** anger du sökvillkoren.
   * I **[!UICONTROL Using]** lista, välj **[!UICONTROL Name]**, **[!UICONTROL Email]**, eller **[!UICONTROL User ID]**.
   * I **[!UICONTROL In list]**, markera **[!UICONTROL Users]**.
   * Markera domänen, markera antalet objekt som ska visas och klicka sedan på **[!UICONTROL Find]**.

1. Klicka på den användare som du vill redigera.
1. För en användare som är en del av en lokal domän eller hybriddomän, på **[!UICONTROL Detail]** -fliken, redigera **[!UICONTROL General Settings]** och **[!UICONTROL Login Settings]** och klicka **[!UICONTROL Save]**. Mer information om inställningarna finns i [Användarinställningar](adding-configuring-users.md#user-settings). Du kan inte redigera de allmänna inställningarna och inloggningsinställningarna för en användare som tillhör en företagsdomän.
1. Om du vill redigera gruppinställningarna för användaren klickar du på **[!UICONTROL Group Membership]** och göra följande:

   * Klicka **[!UICONTROL Find Group]** och fyll i sökinformationen.
   * Om du vill lägga till användaren i en ny grupp markerar du kryssrutan för gruppen och klickar på **[!UICONTROL OK]** och klicka sedan på **[!UICONTROL Save]**.

   >[!NOTE]
   >
   >Lokala användare kan inte läggas till i kataloggrupper. Kataloganvändare kan dock läggas till i lokala grupper.

   * Om du vill ta bort användaren från en grupp markerar du kryssrutan för gruppen och klickar på **[!UICONTROL Delete]** och klicka sedan på **[!UICONTROL Save]**.

1. Om du vill redigera användarens roller klickar du på **[!UICONTROL Role Assignments]** och göra följande:

   * Om du vill visa en lista med roller klickar du på **[!UICONTROL Find Roles]**.
   * Om du vill lägga till en roll markerar du kryssrutan för rollen och klickar på **[!UICONTROL OK]** och klicka sedan på **[!UICONTROL Save]**.
   * Om du vill ta bort en roll markerar du kryssrutan för rollen och klickar på **[!UICONTROL Unassign]** och klicka sedan på **[!UICONTROL Save]**.

## Ta bort en användare {#delete-a-user}

1. I administrationskonsolen klickar du på **[!UICONTROL Settings > User Management > Users and Groups]**.
1. Gör följande för att hitta användaren som ska tas bort:

   * I **[!UICONTROL Find]** anger du sökvillkoren.
   * I **[!UICONTROL Using]** lista, välj **[!UICONTROL Name]**, **[!UICONTROL Email]**, eller **[!UICONTROL User ID]**.
   * I **[!UICONTROL In list]**, markera **[!UICONTROL Users]**.
   * Markera domänen, markera antalet objekt som ska visas och klicka sedan på **[!UICONTROL Find]**.

1. Markera kryssrutan för användaren och klicka på **[!UICONTROL Delete]** och klicka sedan på **[!UICONTROL OK]**.

>[!NOTE]
>
>AEM Forms på JEE tillåter även användare av AEM formulär som körs på en OSGi att identifieras som AEM användare. Detta krävs för scenarier där enkel inloggning mellan AEM Forms på JEE och AEM som körs på en OSGi krävs (till exempel arbetsytan HTML). Ovannämnda borttagningsåtgärd tar endast bort en användare från AEM Forms på JEE. Användaren tas inte bort från AEM Forms add-on som körs i OSGi-miljö. Alla inloggningsförsök som görs efter att användaren har tagits bort (ett inloggningsförsök till AEM Forms JEE-tilläggsserver eller AEM Forms-tillägg i OSGi-miljö) nekas.

## Skapa felhanterare för anpassad inloggning {#create-custom-login-error-handler}

Om en användare utan de obligatoriska AEM och CQ-behörigheterna försöker logga in i följande program som är inbäddade i CQ, dirigeras användaren till standardsidan för CQ 404 som innehåller felspårningen:

* Correspondence Management-lösning
* Arbetsytan AEM formulär

  ***anteckning **: Flex Workspace är föråldrat för AEM formulärrelease.*

* formulärhanterare
* Processrapportering

CQ har en mekanism som åsidosätter standardhanteraren 404 jsp.

Mer information om hur du anpassar felhanteringssidan finns i [Anpassa sidor som visas av felhanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html?lang=en) i Adobe Experience Manager-dokumentationen.
