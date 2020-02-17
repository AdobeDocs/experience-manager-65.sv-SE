---
title: Integrera med Livefyre
seo-title: Integrera med Livefyre
description: Lär dig hur du integrerar Livefyres branschledande kurationsfunktioner med din AEM 6.5-instans så att du kan publicera användargenererat innehåll (UGC) från sociala nätverk till din webbplats på några minuter.
seo-description: Lär dig hur du integrerar och använder Livefyre med AEM 6.5.
uuid: c355705d-6e0f-4a33-aa1f-d2d1c818aac0
contentOwner: ind14750
content-type: reference
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: bb3fcb53-b8c3-4b1d-9125-4715f34ceb0b
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Integrera med Livefyre{#integrating-with-livefyre}

Lär dig hur du integrerar Livefyres branschledande kurationsfunktioner med din AEM 6.5-instans så att du kan publicera användargenererat innehåll (UGC) från sociala nätverk till din webbplats på några minuter.

## Komma igång {#getting-started}

### Installera Livefyre-paket för AEM {#install-livefyre-package-for-aem}

AEM 6.5 innehåller funktionspaketet Livefyre 1.2.6 förinstallerat. Det här paketet innehåller bara begränsad Livefyre-integrering med AEM Sites och måste avinstalleras innan du installerar ett uppdaterat paket. Med det senaste paketet kan du uppleva den fullständiga integrationen av Livefyre med AEM, inklusive Sites, Assets och Commerce.

>[!NOTE]
>
>Vissa funktioner i AEM-LF-paketet är beroende av SCF (Social Component Framework). Om du använder funktionspaketet Livefyre som en del av en icke-communitywebbplats måste du deklarera *cq.social.scf* som ett beroende i webbplatsens författarklienter. Om du använder LF-funktionspaketet som en del av en communitywebbplats bör detta beroende redan deklareras.

1. Klicka på ikonen **Verktyg** till vänster på AEM-hemsidan.
1. Navigera till **Distribution > Paket**.
1. Bläddra i Pakethanteraren tills du ser det förinstallerade funktionspaketet Livefyre och klicka sedan på pakettiteln **cq-social-livefyre-pkg-1.2.6.zip** för att utöka alternativen.
1. Klicka på **Mer > Avinstallera**.

   ![livefyre-aem-uninstall-64](assets/livefyre-aem-uninstall-64.png)

1. Återgå till AEM-hemsidan, klicka på Verktyg och gå sedan till **Distribution > Paketresurs**.

   En lista över funktionspaket och snabbkorrigeringar som är tillgängliga för nedladdningsskärmar.

1. Sök efter&quot;Livefyre&quot; i nyckelordssökningen och välj sedan det Livefyre-funktionspaket som motsvarar din AEM-version.

   ![livefyre-aem3-6-4](assets/livefyre-aem3-6-4.png)

1. Klicka på **Hämta** på informationssidan för funktionspaket, läs paketlicensavtalet och klicka på **Godkänn**.
1. Gå tillbaka till Pakethanteraren, leta upp det hämtade paketet och klicka på **Installera**.

   ![livefyre-aem4-6-4](assets/livefyre-aem4-6-4.png)

   Ditt Livefyre-AEM-paket är nu installerat. Innan du kan börja använda integreringsfunktionerna måste du konfigurera AEM för att använda Livefyre.

   Mer information om paket finns i [Arbeta med paket](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/package-manager.html).

   Mer information och versionsinformation om funktionspaket finns i [Funktionspaket](https://helpx.adobe.com/experience-manager/6-3/release-notes/feature-packs-release-notes.html).

### Konfigurera AEM att använda Livefyre: Skapa en konfigurationsmapp {#configure-aem-to-use-livefyre-create-a-configuration-folder}

1. På AEM-hemsidan klickar du på ikonen **Verktyg** i den vänstra listen och går sedan till **Allmänt > Konfigurationsläsaren**.
1. Klicka på **Skapa** för att öppna dialogrutan Skapa konfiguration.
1. Namnge konfigurationen och markera kryssrutan **Cloud Configurations** .

   Detta skapar en mapp under **Verktyg > Distribution > Livefyre-konfiguration** med det angivna namnet.

   ![livefyre-aem-create-config-folder](assets/livefyre-aem-create-config-folder.png)

### Konfigurera AEM att använda Livefyre: Skapa en Livefyre-konfiguration {#configure-aem-to-use-livefyre-create-a-livefyre-configuration}

Konfigurera AEM så att du kan använda din organisations Livefyre-licensreferenser, vilket möjliggör kommunikation mellan Livefyre och AEM.

1. På AEM-hemsidan klickar du på ikonen **Verktyg** i den vänstra listen och går sedan till **Distribution > Livefyre-konfiguration**.
1. Markera konfigurationsmappen där du vill skapa en ny Livefyre-konfiguration och klicka sedan på **Skapa**.

   ![create-livefyre-configuration1](assets/create-livefyre-configuration1.png)

   >[!NOTE]
   >
   >Mapparna måste ha molnkonfigurationer aktiverade i sina egenskaper innan Livefyre-konfigurationer kan läggas till i dem. Konfigurationsmappar skapas och hanteras i Configuration Browser.
   >
   >Du kan inte skapa ett namn för en konfiguration. Sökvägen till mappen som konfigurationen finns i refererar till det. Du kan bara ha en konfiguration per mapp.

1. Markera det nya Livefyre-konfigurationskortet och klicka sedan på **Egenskaper**.

   ![create-livefyre-configuration2](assets/create-livefyre-configuration2.png)

1. Ange din organisations Livefyre-uppgifter och klicka sedan på **OK**.

   ![configure-aem2](assets/configure-aem2.png)

   Öppna Livefyre studio och gå till **Inställningar > Integreringsinställningar > Autentiseringsuppgifter** för att få tillgång till den här informationen.

   Din AEM-instans är nu konfigurerad att använda Livefyre och du kan använda integreringsfunktionerna.

### Anpassa enkel inloggningsintegrering {#customize-single-sign-on-integration}

Paketet Livefyre för AEM innehåller en körklar integrering mellan AEM Communities-profiler och Livefyres SSO-tjänst.

När användare loggar in på din AEM-webbplats loggas de också in i Livefyres sociala komponenter. När en utloggad användare försöker använda en Livefyre-komponentfunktion som kräver autentisering (som att överföra ett foto), initierar Livefyre-komponenten användarautentisering.

Standardautentiseringsintegreringen kanske inte är perfekt för alla webbplatser. Om du vill matcha autentiseringsflödet på webbplatsmallarna på bästa sätt kan du åsidosätta standarddelegaten för Livefyre-autentisering efter dina behov. Gör så här:

1. Med CRXDE Lite kan du kopiera */libs/social/integrations/livefyre/components/authzablecomponent/authclientlib* till */apps/social/integrations/livefyre/components/authorizedComponent/authclientlib*.
1. Redigera och spara */apps/social/integrations/livefyre/components/authorizablecomponent/authclientlib/auth.js* för att implementera en Livefyre Auth Delegate som passar dina behov.

   Mer information om hur du anpassar en autentiseringsdelegat finns i [Identitetsintegrering](https://answers.livefyre.com/developers/identity-integration/).

   Mer information om AEM Clientlibs finns i [Använda bibliotek](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/clientlibs.html)på klientsidan.

## Använd Livefyre med AEM Sites {#use-livefyre-with-aem-sites}

### Lägg till Livefyre-komponenter på en sida {#add-livefyre-components-to-a-page}

Innan du lägger till Livefyre-komponenter på en sida i Sites måste du aktivera Livefyre för sidan genom att antingen ärva en Livefyre-molnkonfiguration från en överordnad sida eller genom att lägga till konfigurationen direkt på sidan. Se implementeringen för hur du inkluderar molntjänster på din webbplats.

När Livefyre har aktiverats för sidan måste behållare konfigureras så att Livefyre-komponenter tillåts. Mer information om hur du aktiverar olika komponenter finns i [Konfigurera komponenter i designläge](https://helpx.adobe.com/experience-manager/6-3/sites/authoring/using/default-components-designmode.html) .

>[!NOTE]
>
>Appar som kräver autentisering för att publicera fungerar inte förrän autentiseringen har konfigurerats i Anpassa enkel inloggningsintegrering.

1. På **komponentsidan** i designläge väljer du **Livefyre** på menyn för att begränsa listan till tillgängliga Livefyre-komponenter.

   ![livefyre-add](assets/livefyre-add.png)

1. Markera en Livefyre-komponent och dra den till rätt plats på sidan.
1. Välj om du vill skapa en ny Livefyre-app eller bädda in en befintlig.

   Om du bäddar in ett befintligt program ombeds du att välja programmet. Om du skapar en ny app måste appen fyllas i innan något innehåll visas. Appen kommer att skapas på Livefyre-webbplatsen och det nätverk som väljs när molnkonfigurationen Livefyre aktiverades för sidan.

   Mer information om hur du infogar komponenter finns i [Redigera sidinnehåll](https://helpx.adobe.com/experience-manager/6-3/sites/authoring/using/editing-content.html).

### Redigera en Livefyre-komponent för en AEM-sida. {#edit-a-livefyre-component-for-an-aem-page}

Du kan bara konfigurera och redigera en Livefyre-komponent i Livefyre Studio. Från AEM:

1. Klicka på Livefyre-komponenten som ska konfigureras.
1. Klicka på ikonen **Konfigurera** (skiftnyckel) för att öppna konfigurationsdialogrutan.
1. Klicka på **Gå till Livefyre Studio** om du vill redigera den här komponenten.
1. Redigera appen i Livefyre Studio.

## Använd Livefyre med AEM Assets {#use-livefyre-with-aem-assets}

### Begär rättigheter och importera UGC till AEM Assets {#request-rights-and-import-ugc-into-aem-assets}

Du kan importera användargenererat Twitter- och Instagram-innehåll (UGC) från Livefyre Studio till AEM Assets med hjälp av UGC-importeraren. När du har valt det innehåll som ska importeras måste du begära rättigheter till innehållet innan importen kan slutföras.

>[!NOTE]
>
>Innan du kan använda Assets för att importera UGC måste du konfigurera konton för konton för sociala konton och rättighetsbegäranden i Livefyre Studio. Se [Inställning: Rättighetsförfrågningar](https://marketing.adobe.com/resources/help/en_US/livefyre/c_how_requesting_rights_works.html) för mer information.

Så här importerar du UGC till AEM Assets:

1. Navigera från AEM-hemsidan till **Resurser > Filer**.
1. Klicka på **Skapa** och sedan på **Importera UGC.**

   ![livefyre-aem-import-ugc](assets/livefyre-aem-import-ugc.png)

1. Sök innehåll:

   * Från Livefyre genom att klicka på fliken UGC-bibliotek. Använd filtren och sök för att hitta innehåll från UGC-biblioteket.
   * Från Twitter och Instagram genom att klicka på fliken Twitter eller Instagram. Använd sökningen eller filtren för att hitta innehåll.

1. Markera de resurser som du vill importera. De resurser du väljer räknas automatiskt och sparas under fliken **Markerade** .
1. **Valfritt**: Klicka på fliken **Markerat** och granska det UGC-innehåll du vill importera.
1. Click **Next**.

   ![livefyre-aem-import-ugc2](assets/livefyre-aem-import-ugc2.png)

1. Välj ett av följande alternativ för varje resurs för rättighetsförfrågningar:

   För Instagram:

   * **Begär rättigheter** manuellt för att få ett meddelande som kan kopieras och klistras in och skickas manuellt till innehållsägarna via Instagram.
   * **Attributera innehållsrättigheter** manuellt för att åsidosätta rättigheterna för enskilda resurser.
   >[!NOTE]
   >
   >På grund av uppdateringar som påverkar sammanställningen av innehåll från icke-kommersiella användarkonton kan vi inte längre lägga in kommentarer åt dig eller automatiskt söka efter svar från författaren. [Klicka här om du vill veta mer](https://developers.facebook.com/blog/post/2018/04/04/facebook-api-platform-product-changes/).

   ![livefyre-aem-import-ugc3-6-4](assets/livefyre-aem-import-ugc3-6-4.png)

   För Twitter:

   * **Message Author** för att skicka ett meddelande till innehållsägaren som begär rättigheter till resursen.
   * **Attributera innehållsrättigheter** manuellt för att åsidosätta rättigheterna för enskilda resurser.


1. Klicka på **Importera**.

   Om du har skickat en Twitter-begäran om behörighet, kommer innehållsägaren att se meddelandet om rättighetsbegäran på sitt konto:

   ![livefyre-aem-rights-request-twitter](assets/livefyre-aem-rights-request-twitter.png)

   >[!NOTE]
   >
   >Twitter har begränsningar för identiska begäranden som kommer från samma konto. Om du importerar fler än ett par resurser bör du ändra meddelandena individuellt för att undvika att flaggas.

1. Klicka på **Klar** i det övre högra hörnet för att avsluta arbetsflödet för rättighetsbegäran.

   Du kan se statusen för en väntande rättighetsbegäran för en resurs i Livefyre Studio. Om innehåll väntar på en rättighetsbegäran kommer resursen inte att visas i AEM Resurser förrän rättigheter har beviljats. Resursen visas automatiskt i AEM Resurser när en rättighetsbegäran beviljas.

   För Instagram måste du spåra innehållsägarens svar och manuellt tilldela rättigheter om de ges behörighet till innehållet.

## Använd Livefyre med AEM Commerce {#use-livefyre-with-aem-commerce}

### Importera produktkataloger till Livefyre med AEM Commerce {#import-product-catalogs-into-livefyre-with-aem-commerce}

AEM Commerce-användare kan smidigt integrera sin befintliga produktkatalog i Livefyre för att öka användarengagemanget i Livefyres visualiseringsappar.

När du har importerat produktkatalogen visas produkterna i realtid i Livefyre-instansen. Om du redigerar eller tar bort artiklar i din AEM Commerce-produktkatalog uppdateras ändringarna automatiskt i Livefrye.

1. Kontrollera att du har det senaste Livefyre for AEM-paketet installerat på din AEM-instans.
1. Navigera från AEM-hemsidan till **AEM Commerce**.
1. Skapa en ny samling eller använd en befintlig samling.
1. Håll muspekaren över samlingen och klicka på **Samlingsegenskaper** (pennikonen).
1. Markera **Synkronisera med Livefyre**.
1. Fyll i **Livefyre-sidprefixet** om du vill länka den här samlingen till en viss sida i AEM.

   Sidprefixet definierar rotsökvägen där sökningen efter produktsidor börjar. Livefyre väljer den första sidan som har en tillhörande produkt. Om du vill hämta olika sidor för olika produkter behövs flera samlingar.

## AEM Support Matrix för Livefyre Apps {#aem-support-matrix-for-livefyre-apps}

| Livefyre-appar | AEM 6.1 | AEM 6.2 | AEM 6.3 | AEM 6.4 |
|---|---|---|---|---|
| Carousel | X | X | X | X |
| Chatt | X | X | X | X |
| Kommentarer | X | X | X | X |
| Bildband |  | X | X | X |
| LiveBlog | X | X | X | X |
| Karta | X | X | X | X |
| Media Wall | X | X | X | X |
| Mosaik | X | X | X | X |
| Omröstning |  | X | X | X |
| Recensioner |  | X | X | X |
| Ett kort | X | X | X | X |
| Storify 2 |  | X | X | X |
| Trender |  | X | X | X |
| Överföringsknapp |  | X | X | X |

