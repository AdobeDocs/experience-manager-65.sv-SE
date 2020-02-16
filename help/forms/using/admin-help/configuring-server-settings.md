---
title: Konfigurerar serverinställningar
seo-title: Konfigurerar serverinställningar
description: På sidan Serverinställningar får du tillgång till inställningar för e-post, aktivitetsmeddelanden och administratörsmeddelanden.
seo-description: På sidan Serverinställningar får du tillgång till inställningar för e-post, aktivitetsmeddelanden och administratörsmeddelanden.
uuid: 73b51ac0-56e5-4748-bb33-e3986c69eb2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e047a95e-0acb-438a-8d27-f005c0adc508
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurerar serverinställningar {#configuring-server-settings}

Sidan Serverinställningar ger åtkomst till olika inställningar för formulärarbetsflödet:

* **E-postinställningar** som aktiverar utgående e-postmeddelanden, tillsammans med e-postserverinställningarna som används för dessa meddelanden. (Se [Konfigurera e-postinställningar](configuring-server-settings.md#configuring-email-settings).)
* **Inställningar** för aktivitetsmeddelanden som aktiverar, inaktiverar eller ändrar meddelanden som skickas i e-postmeddelanden till slutanvändare och grupper om deras uppgifter. (Se [Konfigurera meddelanden för användare och grupper](configuring-server-settings.md#configuring-notifications-for-users-and-groups).)
* **Administratörsinställningar** som aktiverar, inaktiverar eller ändrar meddelanden som skickas i e-postmeddelanden för administrativa uppgifter. (Se [Konfigurera meddelanden för administratörer](configuring-server-settings.md#configuring-notifications-for-administrators).)

## Konfigurera e-postinställningar {#configuring-email-settings}

Du kan ange ett e-postkonto för formulärservern, som skickar e-postmeddelanden till AEM-formuläranvändare och -administratörer. Dessa e-postmeddelanden används för att meddela och påminna användare om uppgifter som de måste slutföra, meddela användaren om uppgifter som har nått en deadline och meddela administratören om eventuella processfel som inträffar.

Om du vill aktivera sändning av e-postmeddelanden mellan AEM-formulär och användare konfigurerar du inställningarna för utgående e-post på sidan E-postinställningar. Utgående e-post måste använda en SMTP-server.

Om du vill att AEM-formulär ska kunna ta emot och hantera inkommande e-postmeddelanden från användare skapar du en e-postslutpunkt för tjänsten Complete Task. (Se [Skapa en e-postslutpunkt för tjänsten](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)Slutför uppgift).

Om processerna har utformats och implementerats utan att e-post krävs behöver du inte konfigurera något av alternativen på sidan E-postinställningar.

### Konfigurera inställningar för utgående e-post {#configure-outgoing-email-settings}

1. Klicka på Tjänster > Formulärarbetsflöde > Serverinställningar > E-postinställningar i administrationskonsolen.
1. Välj Aktivera utgående meddelanden.
1. Skriv e-postserverns namn eller IP-adressen i rutan SMTP-server. Alla e-postmeddelanden från formulärarbetsflödet skickas från den här e-postservern.
1. I rutorna Användarnamn och Lösenord anger du det inloggningsnamn och lösenord som ska användas när SMTP-servern kräver autentisering. Lämna dem tomma om anonym inloggning tillåts.
1. I rutan E-postadress skriver du den e-postadress som ska användas som returadress för e-postmeddelanden som formulärarbetsflödet skickar.

   >[!NOTE]
   >
   >Om du använder Microsoft Exchange Server och e-postadressen är en ogiltig e-postadress kan Microsoft Exchange-servern inte skicka något e-postmeddelande till distributionslistor. Du löser problemet genom att markera alternativet **Aktivera extern kommunikation** separat för varje distributionslista på Microsoft Exchange-servern.

1. Klicka på Spara.

>[!NOTE]
>
>Om du anger felaktig information kan du klicka på Avbryt för att gå tillbaka till sidan som visades tidigare.

### Konfigurera e-postmallar för användning med AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>Flex Workspace är föråldrat för AEM-formulärreleaser.

Som standard innehåller e-postmeddelanden som skickas från AEM-formulär länkar till (borttagna för AEM-formulär i JEE) Flex Workspace. Du kan konfigurera AEM-formulär så att e-postmeddelanden skickas med länkar till AEM Forms Workspace. Mer information om fördelarna med AEM Forms Workspace (Borttaget för AEM-formulär i JEE) finns i [den här](/help/forms/using/features-html-workspace-available-flex.md) artikeln.

1. I administrationskonsolen klickar du på Hem > Tjänster > Formulärarbetsflöde > Serverinställningar > Aktivitetsmeddelanden.
1. Öppna mall för uppgiftstilldelning.
1. Ställ in mallen i åtgärdsmeddelandena på följande: `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```as3
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## Konfigurera meddelanden för användare och grupper {#configuring-notifications-for-users-and-groups}

På sidan Aktivitetsmeddelande kan du konfigurera mallar som används i arbetsflödet för formulär för att generera e-postmeddelanden som skickas till användare och grupper. Du kan anpassa och formatera meddelandena med hjälp av formulärarbetsflödesvariabler.

Du konfigurerar följande typer av meddelanden för användare och grupper:

* påminnelser
* aktivitetstilldelningar
* deadlines

Om du vill generera e-postmeddelanden för en grupp anger du en e-postadress för gruppen i Användarhantering. <!--Fix broken link See Setting up and organizing users -->När formulärarbetsflödet skickar ett e-postmeddelande till en grupp får varje medlem i gruppen som har en angiven e-postadress e-postmeddelandet. När en medlem i gruppen får ett e-postmeddelande och vill göra anspråk på uppgiften, måste medlemmen klicka på anspråkslänken i e-postmeddelandet, som öppnar sidan med uppgiftsinformation i Workspace. Därifrån kan medlemmen antingen göra anspråk på eller göra anspråk på och öppna arbetsuppgiften.

>[!NOTE]
>
>Flex Workspace används inte i AEM-formulärsversioner.

### Konfigurera påminnelser för användare eller grupper {#configure-reminders-for-users-or-groups}

Du kan skicka påminnelsemeddelanden till den tilldelade användaren eller gruppen när en deadline för att slutföra en uppgift närmar sig. Reglerna för att bestämma exakt när ett påminnelsemeddelande skickas bestäms av processutvecklaren.

1. I administrationskonsolen klickar du på Tjänster > Formulärarbetsflöde > Serverinställningar > Aktivitetsmeddelanden.
1. Klicka på Påminnelse (för användare) eller Grupp - Påminnelse (för grupper) under Meddelandetyp.
1. Välj Aktivera påminnelse eller Aktivera grupp - påminnelse.
1. (Endast användarmeddelanden) Markera Inkludera formulärdata om du vill inkludera en bifogad fil i formuläret och dess data med påminnelsemeddelandet.
1. Skriv texten för ämnesraden i e-postmeddelandet i rutan Ämne. Det här fältet är förifyllt med standardtext. Mer information om hur du anpassar det här fältet finns i [Anpassa innehållet i meddelanden](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Skriv texten för e-postmeddelandets brödtext i rutan Meddelandemall. Det här fältet är förifyllt med standardtext. Mer information om hur du anpassar det här fältet finns i [Anpassa innehållet i meddelanden](configuring-server-settings.md#customizing-the-content-of-notifications).
1. I listan Meddelandeformat väljer du det format som e-postmeddelandet skickas i, antingen HTML eller Text. Standardformatet är HTML.
1. I listan E-postkodning väljer du kodningsformatet som ska användas för e-postmeddelandet. Standardvärdet är UTF-8, som de flesta användare utanför Japan kommer att använda. Användare i Japan kan välja ISO2022-JP.
1. Klicka på Spara.

### Konfigurera meddelanden om aktivitetstilldelning för användare eller grupper {#configure-task-assignment-notifications-for-users-or-groups}

Du kan skicka meddelanden om uppgiftstilldelning till en användare eller grupp när de tilldelas en uppgift.

1. I administrationskonsolen klickar du på Tjänster > Formulärarbetsflöde > Serverinställningar > Aktivitetsmeddelanden.
1. Klicka på Uppgiftstilldelning för användare eller Grupp - Uppgiftstilldelning för grupper under Meddelandetyp.
1. Välj Aktivera aktivitetstilldelning för användare eller Aktivera grupp - Uppgiftstilldelning för grupper.
1. (Endast användarmeddelanden) Markera Inkludera formulärdata om du vill ta med en bifogad fil i formuläret och dess data i e-postmeddelandet för uppgiftstilldelning.
1. Skriv texten för ämnesraden i e-postmeddelandet i rutan Ämne. Det här fältet är förifyllt med standardtext. Mer information om hur du anpassar det här fältet finns i [Anpassa innehållet i meddelanden](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Skriv texten för e-postmeddelandets brödtext i rutan Meddelandemall. Det här fältet är förifyllt med standardtext. Mer information om hur du anpassar det här fältet finns i [Anpassa innehållet i meddelanden](configuring-server-settings.md#customizing-the-content-of-notifications).
1. I listan Meddelandeformat väljer du det format som e-postmeddelandet skickas i, antingen HTML eller Text. Standardformatet är HTML.
1. I listan E-postkodning väljer du kodningsformatet som ska användas för e-postmeddelandet. Standardvärdet är UTF-8, som de flesta användare utanför Japan kommer att använda. Användare i Japan kan välja ISO2022-JP.
1. Klicka på Spara.

### Konfigurera aviseringar om deadline för användare eller grupper {#configure-deadline-notifications-for-users-or-groups}

Du kan skicka aviseringar om deadline till användare och grupper när deadline att agera efter en tilldelad uppgift har passerat. Ett meddelande om deadline är vanligtvis informativt eftersom användaren inte längre kan agera på den tilldelade uppgiften.

1. I administrationskonsolen klickar du på Tjänster > Formulärarbetsflöde > Serverinställningar > Aktivitetsmeddelanden.
1. Klicka på Deadline (för användare) eller Grupp - Deadline (för grupper) under Meddelandetyp.
1. Välj Aktivera tidsgräns eller Aktivera grupp - tidsgräns.
1. Skriv texten för ämnesraden i e-postmeddelandet i rutan Ämne. Det här fältet är förifyllt med standardtext. Mer information om hur du anpassar det här fältet finns i [Anpassa innehållet i meddelanden](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Skriv texten för e-postmeddelandets brödtext i rutan Meddelandemall. Det här fältet är förifyllt med standardtext. Mer information om hur du anpassar det här fältet finns i [Anpassa innehållet i meddelanden](configuring-server-settings.md#customizing-the-content-of-notifications).
1. I listan Meddelandeformat väljer du det format som e-postmeddelandet skickas i, antingen HTML eller Text. Standardformatet är HTML.
1. I listan E-postkodning väljer du kodningsformatet som ska användas för e-postmeddelandet. Standardvärdet är UTF-8, som de flesta användare utanför Japan kommer att använda. Användare i Japan kan välja ISO2022-JP.
1. Klicka på Spara.

### Dölj taggen DO NOT DELETE för alla e-postmeddelanden {#hide-the-do-not-delete-tag-for-all-emails}

Du kan konfigurera e-post så att den döljs till spårningstaggen DO NOT DELETE i alla e-postmeddelanden som skickas i en mänsklig centrerad process. Mer information finns i [Så här döljer du taggen DO-NOT-DELETE med CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html)

## Konfigurera meddelanden för administratörer {#configuring-notifications-for-administrators}

Du kan konfigurera mallar som används i arbetsflödet för formulär för att generera e-postmeddelanden som skickas till administratörer.

Du konfigurerar följande typer av meddelanden för administratörer:

* fast gren
* fast åtgärd

### Konfigurera meddelanden om fasta grenar {#configure-stalled-branch-notifications}

Om en gren avbryts (avbryter processen antingen avsiktligt eller på grund av ett fel) kan du få ett e-postmeddelande skickat till en administratör eller en annan användare som sedan kan undersöka problemet.

1. I administrationskonsolen klickar du på Tjänster > Formulärarbetsflöde > Serverinställningar > Administratörsmeddelanden.
1. Klicka på Installerad gren under Meddelandetyp.
1. Välj Aktivera förinstallerad gren.
1. I rutan E-postadress skriver du de adresser till användarna som ska meddelas när en gren stannar. Använd formatet user@domain.com och avgränsa adresserna med kommatecken. Den här e-postadressen är vanligtvis till för en administratör.
1. Skriv texten för ämnesraden i e-postmeddelandet i rutan Ämne. Det här fältet är förifyllt med standardtext. Mer information om hur du anpassar det här fältet finns i [Anpassa innehållet i meddelanden](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Skriv texten för e-postmeddelandets brödtext i rutan Meddelandemall. Det här fältet är förifyllt med standardtext. Mer information om hur du anpassar det här fältet finns i [Anpassa innehållet i meddelanden](configuring-server-settings.md#customizing-the-content-of-notifications).
1. I listan Meddelandeformat väljer du det format som e-postmeddelandet skickas i, antingen HTML eller Text. Standardformatet är HTML.
1. I listan E-postkodning väljer du kodningsformatet som ska användas för e-postmeddelandet. Standardvärdet är UTF-8, som de flesta användare utanför Japan använder. Användare i Japan kan välja ISO2022-JP.
1. Klicka på Spara.

### Konfigurera meddelanden om fast åtgärd {#configure-stalled-operation-notifications}

Om en åtgärd avbryts (avbryter processen antingen avsiktligt eller på grund av ett fel) kan du få ett e-postmeddelande skickat till en administratör eller en annan användare som kan undersöka problemet.

1. I administrationskonsolen klickar du på Tjänster > Formulärarbetsflöde > Serverinställningar > Administratörsmeddelanden.
1. Klicka på Installerad åtgärd under Meddelandetyp.
1. Välj Aktivera förinstallerad åtgärd.
1. I rutan E-postadresser skriver du de adresser till användarna som ska meddelas när en åtgärd avbryts. Använd formatet user@domain.com och avgränsa adresserna med kommatecken. Den här e-postadressen är vanligtvis till för en administratör.
1. Skriv texten för ämnesraden i e-postmeddelandet i rutan Ämne. Det här fältet är förifyllt med standardtext. Mer information om hur du anpassar det här fältet finns i [Anpassa innehållet i meddelanden](configuring-server-settings.md#customizing-the-content-of-notifications)
1. Skriv texten för e-postmeddelandets brödtext i rutan Meddelandemall. Det här fältet är förifyllt med standardtext. Mer information om hur du anpassar det här fältet finns i [Anpassa innehållet i meddelanden](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Klicka på Spara.

## Anpassa innehållet i meddelanden {#customizing-the-content-of-notifications}

På sidorna Aktivitetsmeddelanden och Administratörsmeddelanden finns flera funktioner som du kan använda för att anpassa meddelandemeddelanden:

* textredigerare
* variabelväljare
* URL-generering

### RTF-redigerare {#rich-text-editor}

Området Meddelandemallar är en textredigerare som du kan använda för att generera HTML för e-postmeddelanden. Den innehåller alternativ för teckensnitt och styckeformatering, som finns under rutan Meddelandemall. Alternativen omfattar teckensnitt, storlek, format och färg samt styckejustering och punkter.

### URL-generering {#url-generation}

Endast för aktivitetsmeddelanden innehåller formulärarbetsflödet två fördefinierade URL-konfigurationer som du kan dra från listan URL-generering till rutan Meddelandemall och sedan anpassa:

* OpenTask är tillgängligt för meddelandetyperna Påminnelse och Uppgiftstilldelning. Den här URL:en innehåller en länk till arbetsytan så att användaren snabbt kan komma åt uppgiften via e-postmeddelandet. När du drar URL:en för OpenTask till rutan Meddelandemall har URL:en följande format:

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask är tillgängligt för meddelandetyperna Grupp - Påminnelse och Grupp - Aktivitetstilldelning. Den här URL:en innehåller en länk till uppgiftsinformationssidan i Workspace, där användaren kan göra anspråk på eller göra anspråk på och öppna arbetsposten. När du drar ClaimTask-URL:en till rutan Meddelandemall har URL:en följande format:

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>Flex Workspace används inte i AEM-formulärsversioner.

Om din lösning distribueras i en klustrad miljö ska du ersätta den `@@notification-host@@` med klusteradressen.

`<`*PORT *`>`är portnumret för programserverns HTTP-avlyssnare. Standardporten för HTTP-avlyssnare för de programservrar som stöds är följande:

**** JBoss: 8080

**** Oracle WebLogic Server: 7001

**** IBM WebSphere: 9080

Om du vill att de här URL-adresserna ska fungera korrekt ersätter du `<`*PORT *`>`med det portnummer som passar din miljö.

***Obs **: Om du använder ett annat anpassat webbprogram än Forms för att ge användarna tillgång till uppgifterna, måste du i stället använda ett URL-format som passar ditt anpassade program.*

### Variabelväljaren {#variable-picker}

Variabelväljarlistan innehåller användbara variabler som du kan dra och släppa i rutorna Ämne eller Meddelandemall. När du släpper en variabel i rutorna Ämne eller Meddelandemall ändras den till det faktiska variabelnamnet för formulärarbetsflödet med två @-symboler på vardera sida, till exempel `@@taskid@@`.

För påminnelser, uppgiftstilldelningar och deadlines för användare och grupper kan du använda följande variabler i rutorna Ämne och Meddelandemall:

**description** Innehållet i egenskapen Description, enligt definitionen i användarsteget (startpunkt, åtgärden Assign Task eller åtgärden Assign Multiple Tasks) för processen i Workbench.

**instruktioner** Innehållet i egenskapen Aktivitetsinstruktioner, enligt definition i användarsteget i processen i Workbench.

**notification-host** Värdnamnet för AEM-formulärprogramservern.

**process-name** Processens namn.

**operation-name** Stegen heter.

**aktivitetskid** Den unika identifieraren för den aktuella uppgiften.

**åtgärder** Skapar en numrerad lista över giltiga flöden (till exempel Godkänn, Avvisa) som mottagaren kan klicka på.

Dessutom kan du använda följande för grupppåminnelser, grupptilldelningar och gruppdeadlines:

**group-name** Namnet på gruppen som är tilldelad arbetsuppgiften.

**Obs**: *Om en variabel inte har något värde returneras ingenting.*

För fasta grenar kan du använda följande variabler i rutorna Ämne och Meddelandemall:

**filial-ID** Filidentifieraren.

**process-id** Processinstansens identifierare.

**notification-host** Värdnamnet för AEM-formulärprogramservern.

För fasta åtgärder kan du använda följande variabler i rutorna Ämne och Meddelandemall:

**action-id** Åtgärds-ID.

**filial-ID** Filidentifieraren.

**process-id** Processinstansens identifierare.

**notification-host** Värdnamnet för AEM-formulärprogramservern.

### Använda en variabel i rutan Ämne {#using-a-variable-in-the-subject-box}

Om du skriver följande text i rutan Ämne för meddelanden om aktivitetstilldelning:

`Please complete task @@taskid@@`

Användaren får ett e-postmeddelande med följande ämne om de har tilldelats uppgift 376:

`Please complete task 376`

### Använda variabler i rutan Meddelandemall {#using-variables-in-the-notification-template-box}

Om du skriver följande text i rutan Meddelandemall för meddelanden om installerade grenar:

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

Administratören får ett e-postmeddelande med följande innehåll om filialnumret är 4868 och servernamnet är `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Konfigurerar anslutningar för övervakning av affärsaktivitet {#configuring-business-activity-monitoring-connections}

Business Activity Monitoring, en valfri modul, innehåller en uppsättning operativa instrumentpaneler som ger realtidsinsyn i verksamheten och viktiga resultatindikatorer.

På sidan BAM-konfigurationsinställningar anger du anslutningarna till servern som kör BAM så att processrelaterade händelser kan spåras och överföras till servern.

1. I administrationskonsolen klickar du på Tjänster > Formulärarbetsflöde > Serverinställningar > BAM-konfigurationsinställningar.
1. Skriv namnet på servern som kör BAM i rutan BAM-värd. Standardvärdet är localhost.
1. I rutan BAM-port skriver du den port som ska användas för att ansluta till servern som kör BAM. Standardporten för BAM för JBoss är 8080, WebLogic är 7001 och WebSphere är 9080.
1. I rutan Servervärd skriver du namnet eller IP-adressen för värdformulärservern. Standardvärdet är localhost.
1. Ange det portnummer som används av formulärservern i rutan Serverport.
1. I rutorna Användarnamn och Lösenord anger du lämpligt användar-ID och lösenord för att komma åt BAM-servern. Standardanvändarnamnet är CognosNowAdmin och standardlösenordet är manager.
1. Klicka på Spara.

