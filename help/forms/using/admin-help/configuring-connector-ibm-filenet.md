---
title: Konfigurera Connector för IBM FileNet
description: Lär dig hur du konfigurerar anslutningsprogrammet för IBM FileNet för att möjliggöra kommunikation mellan AEM och IBM FileNet.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f4045df5-a35b-41d7-910e-971017148597
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---

# Konfigurera Connector för IBM FileNet {#configuring-connector-for-ibm-filenet}

Koppling för IBM FileNet möjliggör kommunikation mellan AEM och IBM FileNet. Mer bakgrundsinformation finns i &quot;Connectors for ECM&quot; i [Tjänstreferens](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>I tidigare versioner kunde resurserna lagras i en ECM-databas. I den här versionen lagras resurser i AEM för inbyggda formulär och databasleverantörstjänsterna har tagits bort. Överföring av resurser från en ECM-databas till databasen med AEM formulär sker när du uppgraderar till AEM formulär. Mer information finns i uppgraderingsguiden för AEM formulär för programservern.

## Konfigurera anslutningen till innehållsmotorn {#configure-the-connection-to-the-content-engine}

IBM FileNet P8 Content Engine tillhandahåller programvarutjänster för hantering av företagsinnehåll och kunddefinierade affärsobjekt i FileNet-innehållsarkiv.

1. I administrationskonsolen klickar du på Tjänster > Koppling för IBM FileNet.
1. I rutan URL för innehållsmotor anger du den fullständiga anslutnings-URL:en. Till exempel:

   Om du använder FileNet Content Engine 4.x med CEWS-transport anger du:

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   Om du använder FileNet Content Engine 4.x med EJB-transport, som bara stöds av WebLogic, anger du:

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. Välj en av följande skyddsnivåer i listan över autentiseringsskyddssystem:

   * **Rensa:** Skickar autentiseringsuppgifter i oskyddat läge över nätverket
   * **Symmetrisk:** Skickar krypterade inloggningsuppgifter i nätverket

1. Ange sökvägen till krypteringsfilen i rutan Plats för krypteringsfil:

   * Om du valde Rensa som autentiseringsskyddsschema ignoreras det här nyckelordet och dess värde.
   * Om du valde Symmetric som autentiseringsskyddsschema pekar den sökväg du anger på platsen för en krypteringsfil på Forms Server som innehåller de kryptografiska nycklar som ska användas.

1. I rutan Standardobjektarkiv anger du den objektarkivkoppling som AEM formulär ansluter till som standard.
1. I rutan Användarnamn anger du användarnamnet för en användare som har behörighet till standardobjektarkivet som du angav i föregående steg.
1. Ange användarens lösenord i rutan Lösenord och klicka på Spara.

## Konfigurera inställningar för processmotorn {#configure-the-process-engine-settings}

Koppling för IBM FileNet innehåller Process Engine Connector för tjänsten IBM FileNet, som används för att interagera med IBM FileNet Process Engine. Du kan konfigurera inställningar för den här tjänsten.

1. Klicka på Tjänster > Koppling för IBM FileNet i administrationskonsolen.
1. Om du vill aktivera användningen av Process Engine Connector för IBM FileNet-tjänsten väljer du Använd anslutningstjänsten för processmotor.
1. Ange värdnamnet eller IP-adressen och portnumret följt av processrouterns namn i rutan Processrouter/Anslutningspunkt. Till exempel:

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. I rutan Användarnamn anger du det användarnamn som används för att ansluta till processmotorn.
1. I rutan Lösenord anger du lösenordet som används för att ansluta till processmotorn och klickar på Spara.

## Validering av tjänstinställningar {#validation-of-service-settings}

Om du anger ett felaktigt användarnamn eller lösenord när du konfigurerar anslutningen till innehållsmotorn eller processmotorinställningarna får du följande resultat, beroende på om tjänsterna körs för närvarande:

* Om både databasprovidertjänsten för IBM FileNet och Content Repository Connector för IBM FileNet-tjänsten stoppas visas inget fel när du sparar tjänstens konfigurationsinformation. Nästa gång du startar tjänsten genereras dock ett undantag och tjänsten kommer inte att starta.
* Om antingen databasprovidertjänsten för IBM FileNet eller Content Repository Connector för IBM FileNet-tjänsten startas försöker tjänsten att omedelbart validera inloggningsinformationen när du sparar tjänstens konfigurationsinformation. I det här fallet inträffar ett fel och konfigurationsinformationen sparas inte.

## Ändra databasens tjänstleverantör {#change-the-repository-service-provider}

Du kan konfigurera vilken databastjänstleverantör som ska användas med FileNet. Databastjänstanrop delegeras till providern som du konfigurerar.

Följande alternativ är tillgängliga:

**Aktuellt databasprovidernamn:** Namnet på den aktuella databastjänstprovidern

**IBM FileNet-databasprovider:** Gör FileNet-databasprovidern till databasprovidern. Det här alternativet har tagits bort.

**databasprovider:** Gör den inbyggda databasprovidern till databasprovidern

>[!NOTE]
>
>Om du vill välja en annan databastjänstleverantör än de som anges konfigurerar du RepositoryService i Program och tjänster. <!-- Fix broken link(See Managing Services) -->

1. I administrationskonsolen klickar du på Tjänster > Koppling för IBM FileNet.
1. Välj den alternativa databastjänstleverantören under Information om databastjänstleverantör och klicka sedan på Spara.
