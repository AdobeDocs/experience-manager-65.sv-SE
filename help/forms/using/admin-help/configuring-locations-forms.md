---
title: Konfigurera platser för formulär
seo-title: Konfigurera platser för formulär
description: Lär dig hur du konfigurerar platsen för Forms.
seo-description: Lär dig hur du konfigurerar platsen för Forms.
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera platser för formulär {#configuring-locations-for-forms}

Du kan ange URL, URI och filplatser för attribut som webbroten, platsen för de formulär som ska hämtas, den dirigerade PDF-fil som används i PDF-formulärsomformningar och cacheplatsen.

1. Klicka på Tjänster > Formulär i administrationskonsolen.
1. Ange lämpliga alternativ under Platser. Alternativen beskrivs nedan.
1. Klicka på Spara.

## Platsinställningar {#locations-settings}

**** Bas-URL: Bas-URL:en där formulärresurser som bilder och skript finns. Det här värdet krävs för HTML-omformningar som innehåller HREF-referenser till externa beroenden, som bilder eller skript. Ett sådant skript är xfasubset.js, vilket krävs för att HTML-formulär ska kunna utföra XFA-intelligens. Värdet måste vara HTTP-motsvarigheten till innehållsrots-URI.

***Obs **: Bas-URL stöder endast HTTP- eller databasprotokoll. Den stöder inte protokoll som file:///. Om du behöver komma åt en resurs, till exempel en anpassad CSS eller en URI för digitala signaturer, använder du lämpligt API-parametervärde för att ange den absoluta platsen.*

När en beroendesökväg är absolut ignoreras värdet för bas-URL. I annat fall kombineras beroendesökvägen med bas-URL:en.

Standardvärdet är en tom sträng.

Följande exempel pekar på samma innehåll (med Content Root URI och Base URL):

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**** URI för FS-webbrot: URL:en för webbprogrammet Forms. Du kan lämna rutan tom om Forms-webbprogrammet och klientprogrammet distribueras på samma programserver. URL:en till webbroten för Forms API kommer att användas.

Om Forms-webbprogrammet och klientprogrammet inte distribueras till samma programserver anger du URL:en för Forms-webbprogrammet i den här rutan, som i det här exemplet:

`https://<host name>:<port>/FormServer`

Var `host name`och `port` är servernamnet och portnumret för den server som är värd för webbprogrammet Forms.

Standardvärdet är en tom sträng.

**** Webbrot-URI: Programmets webbrot. Det här värdet kombineras med parametern sTargetURL (när sTargetURL anges som relativ), som anges med AEM-formulärets SDK, för att skapa en absolut URL för att komma åt programspecifikt webbinnehåll.

Standardvärdet är en tom sträng.

**** Innehållsrot-URI: Den URI eller absoluta plats som formulär hämtas från. Detta värde kombineras med parametern sFormQuery, som anges via API:t, för att skapa den absoluta sökvägen till det formulär som hämtas. Det här värdet kan referera till en katalog eller en webbplats som är tillgänglig via HTTP.

Standardvärdet är en tom sträng.

**** URI för XCI-konfiguration: Den relativa eller absoluta plats där XCI-filen som används för återgivning finns. För ett relativt värde antas XCI-filen finnas i den distribuerbara AEM-formulärens EAR-fil.

Standardvärdet är `com/adobe/formServer/PA/pa.xci`.

**** URI för teckensnittskarta: Den relativa eller absoluta platsen för teckensnittsmappningsfilen. För ett relativt värde antas filen finnas i den distribuerbara AEM-formulärens EAR-fil.

Teckensnittsmappningsfilen används för att skapa anpassade teckensnittsmappningar för HTML-omformningar i formulär, vilket gör att du kan ange vilket teckensnitt som ska användas när ett teckensnitt inte finns på klientdatorn.

Standardvärdet är `com/adobe/formServer/client-font-map.properties`.

Följande post är ett exempel på en post i teckensnittsmappningsfilen:

`Arial=Arial,Helvetica,sans-serif`

**** Seed PDF-fil: Den första PDF-filen som används i en PDF-formulärsomformning för att optimera leveransen. Seed PDF-filen specificerar en anpassad PDF-fil (som bara innehåller XFA-ström, bilder och teckensnittsresurser) som bifogas med formulärdesignen och data. Formuläret återges i Acrobat 7 eller senare och gäller för PDF-formulärsomformning.

Standardvärdet är en tom sträng.

**** Cacheplats: Anger platsen för Forms-diskcachen. När du ändrar den här inställningen återställs all befintlig cacheinformation från den aktuella platsen och en ny cache skapas på den nya platsen. Välj något av följande alternativ:

**** Standardplats: Det här är standardvalet. När det här alternativet är markerat skapas cachen på en plats som är beroende av den programserver som du använder:

* **** JBoss: [JBoss Home]\server\[installationstyp]\svcdata\FormServer\Cache
* **** WebLogic: [WebLogic Home]\user_projects\domains\[aem-forms Domain Name]\adobe\[forms server name]\FormServer\Cache
* **** WebSphere: [IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**** Tillfällig katalog för LC: Cachen skapas i en underkatalog till den tillfälliga AEM-formulärkatalogen, som anges i administrationskonsolen under Inställningar > Systeminställningar > Konfigurationer > Plats för tillfällig katalog. Underkatalogen heter adobeform_[servername].

>[!NOTE]
>
>Om du använder ett tillfälligt rensningsverktyg bör du tänka på att även om du tar bort de här katalogerna inte påverkar funktionaliteten så kan det påverka prestanda avsevärt under en kort tid tills det nya cacheminnet skapas. För att undvika det här problemet ska du inte ta bort de här katalogerna när du rensar den tillfälliga AEM-formulärkatalogen.

