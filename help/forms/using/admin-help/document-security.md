---
title: 'Om dokumentsäkerhet '
seo-title: 'Om dokumentsäkerhet '
description: Lär dig hur du kan skapa, lagra och använda fördefinierade sekretessinställningar och distribuera information på ett säkert sätt med dokumentsäkerhet.
seo-description: Lär dig hur du kan skapa, lagra och använda fördefinierade sekretessinställningar och distribuera information på ett säkert sätt med dokumentsäkerhet.
uuid: e4fba2a4-f3c1-4b20-8e05-8e241b40ebd0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1820cb38-ba70-4cce-8895-290524bdd9bf
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Om dokumentsäkerhet {#about-document-security}

Dokumentsäkerheten säkerställer att bara behöriga användare kan använda dina dokument. Med dokumentsäkerhet kan du distribuera all information som du har sparat i ett format som stöds. Filformat som stöds är:

* Adobe PDF-filer
* Microsoft® Word-, Excel- och PowerPoint-filer

Mer information om hur skyddsprofiler skyddar filtyper som stöds finns i [Ytterligare dokumentsäkerhetsinformation](https://www.adobe.com/go/learn_aemforms_doc_security_63).

Med dokumentsäkerhet kan du enkelt skapa, lagra och använda fördefinierade sekretessinställningar i dina dokument. För att förhindra att information sprids utanför räckhåll kan du också övervaka och styra hur mottagarna använder dokumenten när du har distribuerat dem.

Du kan skydda dokument med hjälp av profiler. En *policy* är en samling information som innehåller sekretessinställningar och en lista över behöriga användare. De sekretessinställningar du anger i en profil avgör hur en mottagare kan använda ett dokument som du tillämpar profilen på. Du kan till exempel ange om mottagarna ska kunna skriva ut eller kopiera text, redigera text eller lägga till signaturer och kommentarer i skyddade dokument.

Dokumentsäkerhetsanvändare skapar profiler via slutanvändarens webbsidor. Administratörer använder webbsidorna för dokumentsäkerhet för att skapa profiluppsättningar som innehåller delade profiler som är tillgängliga för alla behöriga användare.

Även om profiler lagras i dokumentsäkerhet kan du tillämpa dem på dokument via ditt klientprogram. Hur du tillämpar profiler på PDF-dokument beskrivs i detalj i *Acrobat-hjälpen*. Regler som används i andra program, t.ex. Microsoft Office, finns i hjälpen *för* Acrobat Reader DC-tillägg för programmet.

När du tillämpar en profil på ett dokument skyddar sekretessinställningarna som anges i profilen den information som dokumentet innehåller. Sekretessinställningarna skyddar även alla filer (text, ljud eller video) i ett PDF-dokument. Du kan distribuera det profilskyddade dokumentet till mottagare som har behörighet enligt profilen.

**Åtkomstkontroll och -granskning av dokument**

Genom att använda en skyddsprofil får du full kontroll över dokumentet, även sedan du distribuerat det. Du kan övervaka dokumentet, göra ändringar i profilen, hindra användare från att fortsätta få åtkomst till dokumentet och växla den profil som tillämpas på dokumentet.

Med dokumentsäkerhet kan du övervaka skyddsskyddade dokument och spåra händelser, t.ex. när en behörig eller obehörig användare försöker öppna dokumentet.

**Komponenter**

Dokumentsäkerhet består av en server och ett användargränssnitt:

**** Server: Den centrala komponent genom vilken dokumentsäkerhet utför transaktioner som användarautentisering, hantering av profiler i realtid och tillämpning av sekretess. Servern har också ett centralt arkiv för policyer, granskningsposter och annan relaterad information.

**** Webbsidor: Gränssnittet där du skapar profiler, hanterar profilskyddade dokument och övervakar händelser som är kopplade till profilskyddade dokument. Administratörer kan också konfigurera globala alternativ som användarautentisering, granskning och meddelanden för inbjudna användare samt hantera inbjudna användarkonton.

![rm_psworkflow](assets/rm_psworkflow.png)

Stegen i bilden är följande:

1. Dokumentägaren skapar profiler med hjälp av webbsidorna. Dokumentägare kan skapa egna profiler som bara är tillgängliga för dem. Administratörer och koordinatorer för principuppsättningar kan skapa delade principer i principuppsättningar som är tillgängliga för behöriga användare.
1. Dokumentägaren tillämpar profilen och sparar och distribuerar sedan dokumentet. Dokumentet kan distribueras via e-post, via en nätverksmapp eller på en webbplats.
1. Mottagaren öppnar dokumentet i lämpligt klientprogram. Mottagaren kan använda dokumentet enligt sin policy.
1. Dokumentägaren, principuppsättningskoordinatorn eller administratören kan spåra dokument och ändra åtkomsten till dem via webbsidorna.

## Om dokumentsäkerhetsanvändare {#about-document-security-users}

Olika typer av användare arbetar med dokumentsäkerhet för att utföra olika uppgifter:

* Systemadministratören eller annan person som arbetar med informationssystem installerar och konfigurerar dokumentsäkerhet. Den här personen kan även vara ansvarig för att konfigurera globala inställningar för servern, webbsidor, profiler och dokument.

   De här inställningarna kan t.ex. innehålla en grundläggande säkerhets-URL, gransknings- och sekretessmeddelanden, inbjudna användarregistreringsmeddelanden och standardavtalsperioder.

* Dokumentsäkerhetsadministratörer kan skapa profiler och uppsättningar av profiler samt hantera profilskyddade dokument för användare efter behov. De skapar även inbjudna användarkonton och övervakar system, dokument, användare, policy, principuppsättning och anpassade händelser. De kan också ansvara för att konfigurera den globala servern samt webbsidan och principinställningarna tillsammans med en systemadministratör.

   Administratörer kan tilldela användare följande roller i området för användarhantering i administrationskonsolen. Användare som tilldelas dessa roller utför sina uppgifter i dokumentets säkerhetsgränssnitt i administrationskonsolen.

   **Superadministratör för dokumentsäkerhet**

   Användare med den här rollen har åtkomst till alla dokumentskyddsinställningar i administrationskonsolen. Dessa behörigheter är associerade med rollen:

   * Hantera konfiguration
   * Hantera princip
   * Hantera principuppsättningar
   * Hantera dokument
   * Hantera dokumentutgivare
   *  Hantera inbjudna och lokala användare
   * Visa händelser
   * Delegera
   * Bjud in externa användare
   **Dokumentsäkerhetsadministratör**

   Användare med den här rollen kan konfigurera dokumentsäkerhetsservern med hjälp av sidan Konfiguration i dokumentsäkerhetsavsnittet i administrationskonsolen. Den här behörigheten är associerad med rollen Hantera konfiguration.

   ***Obs **: Användare med den här rollen måste också ha administratörskonsolens användarroll för att kunna logga in på administrationskonsolen och redigera alla konfigurationsrelaterade inställningar.*

   **Administratör för dokumentsäkerhetsprincip**

   Användare med den här rollen kan använda dokumentsäkerhetsdelen i administrationskonsolen för att redigera andra användares profiler och för att skapa, redigera och ta bort principuppsättningar. När en administratör för en principuppsättning skapar en principuppsättning kan de tilldela en principuppsättningskoordinator till den uppsättningen. Dessa behörigheter är associerade med rollen:

   * Hantera princip
   * Hantera principuppsättningar
   * Hantera dokument
   * Hantera dokumentutgivare
   * Visa händelser
   * Delegera
   ***Obs **: Användare med den här rollen måste också ha administratörskonsolens användarroll för att kunna logga in på administrationskonsolen och redigera alla konfigurationsrelaterade inställningar.*

   **Dokumentsäkerhet hanterar inbjudna och lokala användare**

   Användare med den här rollen kan utföra de uppgifter som krävs för att hantera alla inbjudna och lokala användare på relevanta dokumentsäkerhetswebbsidor. Dessa behörigheter är associerade med rollen:

   *  Hantera inbjudna och lokala användare
   * Bjud in externa användare
   * Åtkomst till slutanvändarens webbsidor
   ***Obs **: Användare med den här rollen måste också ha administratörskonsolens användarroll för att kunna logga in på administrationskonsolen och redigera alla konfigurationsrelaterade inställningar.*

   **Inbjudan till dokumentsäkerhet**

   Användare med den här rollen kan bjuda in användare. Dessa behörigheter är associerade med rollen:

   * Bjud in externa användare
   * Åtkomst till slutanvändarens webbsidor
   **Slutanvändare för dokumentsäkerhet**

   Användare med den här rollen har åtkomst till slutanvändarens webbsidor för dokumentsäkerhet. Den här rollen kan även tilldelas administratörer så att administratörer kan skapa profiler med hjälp av slutanvändarsidorna. Den här behörigheten är associerad med rollen Åtkomst till slutanvändarens webbsidor.

* Användare inom organisationen som har giltiga dokumentsäkerhetskonton skapar egna profiler, använder profiler för att skydda dokument, spåra och hantera sina profilskyddade dokument och övervakar händelser som är relaterade till deras dokument.
* Koordinatorer för principuppsättningar hanterar dokument, visar händelser och hanterar andra koordinatorer för principuppsättningar (baserat på deras behörigheter). Administratörer utser användare till principuppsättningskoordinatorer för särskilda principuppsättningar.
* Användare som är externa för din organisation (t.ex. en affärspartner) kan använda profilskyddade dokument om de finns i dokumentets säkerhetskatalog, om administratören skapar ett konto åt dem eller om de registrerar sig för dokumentsäkerhet via en automatiserad e-postinbjudan. Beroende på hur administratören aktiverar åtkomstinställningarna kan de inbjudna användarna även ha behörighet att tillämpa profiler på dokument, att skapa, ändra och ta bort sina profiler samt att bjuda in andra externa användare att använda sina profilskyddade dokument.
* Utvecklare använder AEM Forms SDK för att integrera anpassade program med dokumentsäkerhet.

Administratörer för dokumentsäkerhet kan skapa anpassade roller med följande behörigheter i Användarhantering:

* Konfiguration av hantering av dokumentsäkerhet
* Dokumentsäkerhet Hantera inbjudna och lokala användare
* Dokumentsäkerhet Hantera principuppsättningar
* Dokumentsäkerhet Hantera principuppsättningar
* Vyserverhändelser för dokumentsäkerhet
* Ägare av dokumentskyddsändringsprincip

## Profiler och policyskyddade dokument {#policies-and-policy-protected-documents}

En *profil* definierar en uppsättning sekretessinställningar och användare som kan komma åt ett dokument som profilen tillämpas på. En profil gör det även möjligt att ändra behörigheter för ett dokument dynamiskt. Den person som skyddar dokumentet får behörighet att ändra sekretessinställningarna för att återkalla åtkomst till dokumentet eller för att ändra profilen.

Policyskydd kan tillämpas på ett PDF-dokument med Adobe Acrobat® Pro och Acrobat Standard. Skyddet av profilen kan tillämpas på andra filtyper, t.ex. Microsoft Word-, Excel- och PowerPoint-filer, genom att använda klientprogrammet med rätt Acrobat Reader DC-tillägg installerat.

### Hur policyer fungerar {#how-policies-work}

Profilerna innehåller information om behöriga användare och sekretessinställningar som ska gälla för dokumenten. Användare kan vara vem som helst i din organisation, liksom personer som är externa i din organisation och som har ett konto. Om administratören aktiverar funktionen för användarinbjudan går det till och med att lägga till nya användare i profiler, vilket initierar en e-postprocess för registreringsinbjudan.

Sekretessinställningarna i en profil avgör hur mottagarna kan använda dokumentet. Du kan till exempel ange om mottagarna ska kunna skriva ut eller kopiera text, göra ändringar eller lägga till signaturer och kommentarer i skyddade dokument. Samma policy kan även ange olika sekretessinställningar för specifika användare.

>[!NOTE]
>
>Sekretessinställningar som tillämpas via en profil åsidosätter inställningar som kan ha tillämpats på ett PDF-dokument i Acrobat med hjälp av säkerhetsalternativen för lösenord och certifikat. (Mer information finns i hjälpen för Acrobat.)

Användare och administratörer kan skapa profiler via webbsidorna för dokumentsäkerhet. Endast en profil åt gången kan tillämpas på ett dokument. Du kan tillämpa en profil på något av följande sätt:

* Öppna dokumentet i Acrobat eller något annat klientprogram och välj en skyddsprofil för dokumentet.
* Skicka ett dokument som en e-postbilaga i Microsoft Outlook. I det här fallet kan du välja en profil från en lista med profiler eller välja en automatiskt genererad profil som Acrobat skapar med en standarduppsättning med sekretessinställningar för att skydda dokumentet endast för e-postmeddelandemottagarna.

En profil kan tas bort från ett dokument med hjälp av klientprogrammet.

![rm_psonline_policy](assets/rm_psonline_policy.png)

Stegen i diagrammet är följande:

1. Dokumentägaren skyddar dokumentet från ett klientprogram som stöds med en profil som tillåter onlineanvändning.
1. Dokumentsäkerhet skapar en dokumentlicens och dokumentnycklar och krypterar profilen. Dokumentlicensen, den krypterade regeln och dokumentnyckeln returneras till klientprogrammet.
1. Dokumentet krypteras med dokumentnyckeln och dokumentnyckeln ignoreras. Dokumentet bäddar nu in licensen och policyn. Dessa åtgärder utförs i det klientprogram som stöds.

När du tillämpar en profil på ett dokument, skyddas den information som dokumentet innehåller, inklusive eventuella filer (text, ljud eller video) i PDF-dokument av de sekretessinställningar som anges i profilen. Dokumentskydd genererar licens- och krypteringsinformation som sedan bäddas in i dokumentet. När du distribuerar dokumentet kan dokumentskyddet autentisera de mottagare som försöker öppna dokumentet och ge behörighet enligt de behörigheter som anges i profilen.

Om offlineanvändning är aktiverad kan mottagarna även använda principskyddade dokument offline (utan en aktiv Internet- eller nätverksanslutning) under den tidsperiod som anges i profilen.

### Hur policyskyddade dokument fungerar {#how-policy-protected-documents-work}

Om du vill öppna och använda profilskyddade dokument måste profilen innehålla ditt namn som mottagare och du måste ha ett giltigt dokumentsäkerhetskonto. För PDF-dokument behöver du Acrobat eller Adobe Reader®. För andra filtyper måste du ha rätt program för filen med Acrobat Reader DC-tillägg installerade.

När du försöker öppna ett policyskyddat dokument ansluter Acrobat, Adobe Reader eller Acrobat Reader DC-tilläggen till dokumentsäkerheten för att autentisera dig. Sedan kan du logga in. Om dokumentanvändningen granskas visas ett meddelande. När dokumentskyddet har fastställt vilka dokumentbehörigheter som ska beviljas, hanteras dekrypteringen av dokumentet. Du kan sedan använda dokumentet enligt inställningarna för sekretesspolicyn.

![rm_psopen_online](assets/rm_psopen_online.png)

Stegen i diagrammet är följande:

1. Dokumentanvändaren öppnar dokumentet i ett klientprogram som stöds och autentiserar med servern. Dokumentets identifierare skickas till dokumentets säkerhetsserver.
1. Dokumentsäkerhet autentiserar användarna, kontrollerar principen för auktorisering och skapar en voucher. Verifikationen (som innehåller dokumentnyckeln och behörigheterna) returneras till klientprogrammet.
1. Dokumentet dekrypteras med dokumentnyckeln och dokumentnyckeln ignoreras. Dokumentet kan sedan användas enligt sekretessinställningarna för profilen. Dessa åtgärder utförs i det klientprogram som stöds.

Du kan fortsätta använda ett dokument under följande förhållanden:

* Oändligt eller för giltighetsperioden som anges i policyn
* Tills administratören eller personen som tillämpade policyn återkallar åtkomsten till dokumentet eller ändrar policyn

Du kan också använda principskyddade dokument offline (utan Internet- eller nätverksanslutning) om profilen tillåter åtkomst offline. Du måste först logga in på dokumentsäkerhet för att synkronisera dokumentet. Du kan sedan använda dokumentet under den offlinelåneperiod som anges i profilen.

När offlinelåneperioden är slut måste du synkronisera dokumentet igen med dokumentsäkerhet, antingen genom att gå online och öppna ett policyskyddat dokument eller genom att använda ett kommando i klientprogrammet. (Mer information finns i *Acrobat-hjälpen* eller i hjälpen *för lämpliga* Acrobat Reader DC-tillägg.)

Om du sparar en kopia av ett principskyddat dokument med menykommandot Spara eller Spara som, används profilen automatiskt för det nya dokumentet. Händelser som försök att öppna det nya dokumentet granskas också och registreras för det ursprungliga dokumentet.

## Policyuppsättningar {#policy-sets}

*Policyuppsättningar* används för att gruppera en uppsättning principer som har ett gemensamt affärssyfte. Dessa principuppsättningar görs sedan tillgängliga för en delmängd av användarna i systemet.

Varje principuppsättning kan ha en eller flera associerade principuppsättningskoordinatorer. Principuppsättningens koordinator är en administratör eller en användare som har ytterligare behörigheter. Koordinatorn för *principuppsättning* är vanligtvis en specialist i organisationen som bäst kan skapa policyer i en viss principuppsättning.

Koordinatorer för principuppsättningar kan utföra följande uppgifter:

* Skapa nya profiler
* Redigera och ta bort profiler i principuppsättningen
* Redigera inställningar för principuppsättning
* Lägga till och ta bort koordinatorer för principuppsättningar
* Visa policy- och dokumenthändelser för alla profiler eller dokument i principuppsättningen
* Återkalla åtkomst till dokument
* Byt profil för dokumentet.

Policyuppsättningar skapas och tas bort på webbsidorna för dokumentsäkerhetsadministration av administratörer och koordinatorer för principuppsättningar som har behörighet att göra det.

Policyuppsättningar är vanligtvis tillgängliga för ett begränsat antal användare genom att ange vilka användare eller grupper inom en domän som kan använda profilerna från den principuppsättning som skydd för dokument.

När dokumentsäkerhet är installerat skapas en standardprincipuppsättning som kallas *global principuppsättning*. Administratören som installerade programvaran hanterar den här principinställningen.
