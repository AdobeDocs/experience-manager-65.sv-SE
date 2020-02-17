---
title: Importera och exportera globala inställningar
seo-title: Importera och exportera globala inställningar
description: Du kan importera och exportera sökmallsdefinitioner och globala inställningar för arbetsytan.
seo-description: Du kan importera och exportera sökmallsdefinitioner och globala inställningar för arbetsytan.
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
translation-type: tm+mt
source-git-commit: 687cdacc2868de16a4df968dddedd330ce3317bb

---


# Importera och exportera globala inställningar {#importing-and-exporting-global-settings}

Du kan importera och exportera sökmallsdefinitioner och globala inställningar för arbetsytan.

>[!NOTE]
>
>Flex Workspace används inte i AEM-formulärsversioner.

Du kan till exempel gå från en utvecklingsmiljö till en produktionsmiljö genom att exportera sökmallsdefinitionerna och globala inställningar från en miljö och importera dem till en annan.

När du har exporterat den globala inställningsfilen kan du ändra inställningarna i en XML- eller textredigerare. De enda inställningar du kan behöva redigera är JChannelConnectionProperties, formViewOnly och specialRoutes. Mer information finns i [Globala inställningar](importing-exporting-global-settings.md#workspace-global-settings)för arbetsytan.


>[!NOTE]
>
>Om du ändrar händelseegenskaperna i den globala inställningsfilen måste du starta om servern.

## Importera en sökmallsdefinition {#import-a-search-template-definition}

1. I administrationskonsolen klickar du på Tjänster > Arbetsyta > Global administration.
1. Klicka på Välj fil under Importera sökmallsdefinition och välj sökmallen. Du kan bara importera sökmallsdefinitioner som ursprungligen exporterades från en instans av Workspace.
1. Klicka på Importera.

## Exportera en sökmallsdefinition {#export-a-search-template-definition}

1. På sidan Global administration, under Exportera sökmallsdefinition, klickar du på Lista alla.
1. I listan med sökmallar väljer du den mall som ska exporteras.

   >[!NOTE]
   >
   >Du kan markera mer än en mall, men bara den senast markerade mallen exporteras.

1. Klicka på Exportera och spara sedan filen på datorn.

## Importera globala inställningar {#import-global-settings}

1. På sidan Global administration, under Importera globala inställningar, klickar du på Välj fil och väljer den globala inställningsfilen. Den globala inställningsfilen måste vara i XML-format.
1. Klicka på Importera.

## Exportera globala inställningar {#export-global-settings}

1. Klicka på Exportera under Exportera globala inställningar på sidan Global administration.
1. Spara filen på datorn.

## Globala inställningar för arbetsyta {#workspace-global-settings}

Du kan ändra den globala inställningsfilen; De enda inställningar du kan behöva redigera är JChannelConnectionProperties, formViewOnly och specialRoutes.

>[!NOTE]
>
>Flex Workspace används inte i AEM-formulärsversioner.

Den globala inställningsfilen för arbetsytan innehåller följande inställningar:

### specialRoutes, inställningar {#specialroutes-settings}

Inställningarna för *specialRoutes* anger egenskaperna för de särskilda vägarna, godkänn och Neka, i Workspace. I vissa situationer visas knapparna för dessa vägar på aktivitetskortet i Workspace, och användaren kan markera dem utan att öppna formuläret. Du kan ändra inställningarna för specialRoutes i den globala inställningsfilen för att lägga till anpassade namn för godkännande och neka eller för att skapa ytterligare vägar.

**** client_specialRoutes_route_acceptable_style: Namnet på det format som finns i arbetsytetemat, som identifierar ikonerna för att godkänna. Formatet måste innehålla värden för en aktiverad ikon och en inaktiverad ikon. Om du vill definiera ett format för en anpassad knapp måste du använda följande mall:
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` Arbetsytans CSS-fil är inbäddad i filen workspace-theme.swf, som finns i filen adobe-workspace-client.ear > adobe-workspace-client.war. Om du vill ändra utseendet på arbetsytan måste du kompilera om filen workspace-theme.swf.

**** client_specialRoutes_route_deny_names: Olika strängar som en Workbench-användare kan använda för att tolkas som&quot;deny&quot;. Strängarna är skiftlägeskänsliga. Standardvärdet är t.ex. Neka. Om Workbench-användaren använder ordet Neka i en process känns ordet inte igen. Ordet Neka måste läggas till i den här inställningen för att flödesknappen ska kunna anpassas och ha formatet tillämpat på den.

**** client_specialRoutes_route_deny_style: Namnet på det format som finns i temafilen för arbetsytan där knappikonerna för att neka visas. Formatet måste innehålla värden för en aktiverad ikon och en inaktiverad ikon. `  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` Om du vill definiera ett format för en anpassad knapp måste du använda följande mall:
**client_** specialRoutes_route_approved_names: Olika strängar som en Workbench-användare kan använda för att tolkas som&quot;Godkänn&quot;. Strängarna är skiftlägeskänsliga. Standardvärdet är t.ex. Godkänt. Om Workbench-användaren använder ordet Godkänn i en process känns ordet inte igen. För att flödesknappen ska kunna anpassas måste ordet Godkänn läggas till i den här inställningen.

**** client_specialRoutes_names: Nycklarna som används för att hitta det anpassade strängvärdet från resursfilerna. Varje post i den här inställningen måste innehålla värdena för namnen och formatet.

### JGroup-inställningar {#jgroup-settings}

De här inställningarna visas endast om du har uppgraderat från Adobe LiveCycle ES 2.5 eller tidigare.

**** server_remoteevents_ClientTimeoutMilliseconds: Den längsta tid som JGroup väntar på händelsemeddelanden. Den här inställningen bör inte ändras.

**** server_remoteevents_ServerTimeoutMilliseconds: Tidsgränsen för att ta emot JGroup-meddelanden på servern. Det här alternativet anger fördröjningen för att skicka meddelanden från servern till klienten.

**** server_remoteevents_JChannelConnectionProperties: Anslutningsegenskaperna för JGroup som används för att kommunicera mellan servern (där en tjänsthändelse bearbetas av RemoteEvent-tjänsten) och alla instanser av Workspace.

Du kan behöva ändra UDP-värdena för multicast-IP-adressen (mcast_addr), multicast-IP-porten (mcast_port) och TTL för multicast-paketen (ip_ttl). Som standard genereras IP-adressen och portvärdena för multicast slumpmässigt och i allmänhet behöver värdena inte ändras. Om ditt företag har några nätverksprinciper för specifika multicast-intervall för IP-adresser för multicast kan du behöva ändra värdena.

***Obs **: TTL-värdet måste vara större än antalet nätverksväxlar mellan servrarna i klustret. Om värdet är för högt kan det dock göra så att multicast-paket färdas in i undernät, där de tas bort.*

De återstående egenskaperna i den här inställningen bör inte ändras.

**** server_remoteevents_JGroupName: Namnet på den JGroup som används för fjärrhändelsekommunikation. Detta värde genereras slumpmässigt för att undvika konflikter i kluster. Det här värdet bör inte ändras.

Mer information om JGroups och Workspace finns i [JGroups and AEM forms Workspace - Explached](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

### formView-inställningar {#formview-settings}

**** client_formView_openFormInFullScreen: Om du vill visa alla formulär i arbetsytan i helskärmsläge anger du det här alternativet till true. Som standard är det här alternativet inställt på false och formulär visas inte i helskärmsläge. Observera att användartjänsten innehåller ett alternativ för att öppna dokumentet som är kopplat till en uppgift i helskärmsläge. På så sätt kan du styra visningen på basis av de enskilda processerna.

**** client_route_formViewOnly: När värdet är True visas inte vägar i kortvyn eller listvyn i Workspace. Standardvärdet är Falskt, vilket innebär att vägarna visas i kortvyn och listvyn.

### Andra inställningar {#other-settings}

**** client_mimeTypes_openOutsideBrowser: MIME-typen för dokument som öppnas utanför Workspace-webbläsarinstansen. Om din organisations processer kräver ytterligare en MIME-typ anger du den här. Standardvärdena är:

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**** client_customUI_caching: Cachelagrar ett anpassat uppgiftsanvändargränssnitt.

**** server_debugLevel: Ändra inte den här inställningen.

**** client_pollingInterval: Anger avsökningsintervallet (i sekunder) som används på Flex-arbetsytan (borttagen för AEM-formulär i JEE) för att identifiera nya och ändrade uppgifter. Standardvärdet är 3 sekunder. Detta fungerar inte för AEM Forms Workspace.

**** client_systemContext_name: Ange ett anpassat namn (t.ex. Medborgare) som ska visas i fältet Lägg till av (på fliken Bifogade filer) för de bifogade filerna för en uppgift i AEM Forms Workspace.

Så här definierar du det anpassade namnet:

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

**Obs**: Standardvisningsnamnet *för demoprogrammet är **Medborgare**. För ett anpassat program som du skapar är standardvisningsnamnet **Systemkontextkonto**.***** client_idleTimeout: När en användare är inaktiv under en viss tid förfaller AEM Forms Workspace-sessionen. Om du vill aktivera funktionen lägger du till en post i Globala inställningar &lt;client_idleTimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idleTimeout>. Du kan ange värdet 0 om du vill inaktivera tidsgränsen för inaktivitet. Tiden anges i sekunder.
