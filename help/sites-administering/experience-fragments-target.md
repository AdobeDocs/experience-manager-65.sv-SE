---
title: Exportera Experience Fragments till Adobe Target
seo-title: Exporting Experience Fragments to Adobe Target
description: Exportera Experience Fragments till Adobe Target
seo-description: Exporting Experience Fragments to Adobe Target
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
exl-id: f2921349-de8f-4bc1-afa2-aeace99cfc5c
source-git-commit: 72012fa441edb01deb7e557b707fb068d8e9892e
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---

# Exportera Experience Fragments till Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>Vissa funktioner på den här sidan kräver att AEM 6.5.3.0 (eller senare) används.
>
>6.5.3.0:
>
>* **Externalizer-domäner** kan nu markeras.
   >  **Obs!** Externalizer-domäner är bara relevanta för innehållet i Experience Fragment som skickas till Target, och inte för metadata som Visa erbjudandeinnehåll.
>
>6.5.2.0:
>
>* Upplevelsefragment kan exporteras till:
   >
   >   * standardarbetsytan.
   >   * en namngiven arbetsyta som anges i molnkonfigurationen.
   >   * **Obs!** För export till särskilda arbetsytor krävs Adobe Target Premium.
>
>* AEM måste vara [integrerat med Adobe Target med IMS](/help/sites-administering/integration-target-ims.md).
>
>AEM 6.5.0.0 och 6.5.1.0:
>
>* AEM Experience Fragments exporteras till standardarbetsytan i Adobe Target.
>* AEM måste integreras med Adobe Target enligt instruktionerna i [Integrera med Adobe Target](/help/sites-administering/target.md).


Du kan exportera [Upplevelsefragment](/help/sites-authoring/experience-fragments.md), som har skapats i Adobe Experience Manager (AEM), till Adobe Target (Target). De kan sedan användas som erbjudanden i Target-aktiviteter för att testa och personalisera upplevelser i stor skala.

Det finns tre formatalternativ för att exportera ett Experience Fragment till Adobe Target:

* HTML (standard): Stöd för leverans av webb- och hybridinnehåll
* JSON: Stöd för leverans av headless-material
* HTML &amp; JSON

AEM Experience Fragments kan exporteras till standardarbetsytan i Adobe Target eller till användardefinierade arbetsytor för Adobe Target. Detta görs med Adobe Developer Console, som AEM måste använda [integrerat med Adobe Target med IMS](/help/sites-administering/integration-target-ims.md).

>[!NOTE]
>
>Adobe Target arbetsytor finns inte i själva Adobe Target. De definieras och hanteras i Adobe IMS (Identity Management System) och väljs sedan ut för användning i olika lösningar med hjälp av integreringar från Adobe Developer Console.

>[!NOTE]
>
>Adobe Target arbetsytor kan endast användas för att tillåta medlemmar i en organisation (grupp) att skapa och hantera erbjudanden och aktiviteter för denna organisation. utan att ge åtkomst till andra användare. Till exempel landsspecifika organisationer inom ett globalt område.

>[!NOTE]
>
>Mer information finns även i:
>
>* [Utveckling av Adobe Target](https://www.adobe.io/apis/experiencecloud/target.html)
>* [Kärnkomponenter - Upplevelsefragment](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)
>


## Förutsättningar {#prerequisites}

>[!CAUTION]
>
>Vissa funktioner på den här sidan kräver att AEM 6.5.3.0 används.

Du måste utföra olika åtgärder:

1. Du måste [integrera AEM med Adobe Target med IMS](/help/sites-administering/integration-target-ims.md).
2. Experience Fragments exporteras från AEM författarinstans, så du måste [Konfigurera AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) på författarinstansen för att säkerställa att alla referenser i Experience Fragment är externaliserade för webbleverans.

   >[!NOTE]
   >
   >För ländrörning som inte omfattas av standardinställningen används [Experience Fragment Link Rewriter-provider](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) är tillgängligt. Med detta kan ni utveckla anpassade regler för er instans.

## Lägg till molnkonfigurationen {#add-the-cloud-configuration}

Innan du exporterar ett fragment måste du lägga till **Molnkonfiguration** for **Adobe Target** till fragmentet eller mappen. Detta gör även att du kan:

* ange de formatalternativ som ska användas för exporten
* välj en målarbetsyta som mål
* välj en externaliseringsdomän för att skriva om referenser i Experience Fragment (valfritt)

De obligatoriska alternativen kan väljas i **Sidegenskaper** av den mapp och/eller det fragment som krävs, specifikationen ärvs vid behov.

1. Navigera till **Upplevelsefragment** konsol.

1. Öppna **Sidegenskaper** för rätt mapp eller fragment.

   >[!NOTE]
   >
   >Om du lägger till molnkonfigurationen i den överordnade Experience Fragment-mappen ärvs konfigurationen av alla underordnade.
   >
   >
   >Om du lägger till molnkonfigurationen i själva Experience Fragment ärvs konfigurationen av alla variationer.

1. Välj **Cloud Services** -fliken.

1. Under **Konfiguration av Cloud Service**, markera **Adobe Target** i listrutan.

   >[!NOTE]
   >
   >JSON-formatet i ett Experience Fragment-erbjudande kan anpassas. Om du vill göra det definierar du en Customer Experience Fragment-komponent och kommenterar sedan hur dess egenskaper ska exporteras i komponentens Sling Model.
   >
   >Se kärnkomponenten:
   >
   >[Kärnkomponenter - Upplevelsefragment](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   Under **Adobe Target** välj:

   * lämplig konfiguration
   * det obligatoriska formatalternativet
   * en Adobe Target-arbetsyta
   * om det behövs - externaliseringsdomänen

   >[!CAUTION]
   >
   >Externeringsdomänen är valfri.
   >
   > En AEM externaliserare konfigureras när du vill att det exporterade innehållet ska peka mot en viss *publicera* domän. Mer information finns i [Konfigurera AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer).
   >
   > Observera också att Externalizer-domäner bara är relevanta för innehållet i Experience Fragment som skickas till Target, och inte för metadata som Visa erbjudandeinnehåll.

   För en mapp:

   ![Mapp - Cloud Services](assets/xf-target-integration-01.png "Mapp - Cloud Services")

1. **Spara och stäng**.

## Exportera ett Experience Fragment till Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>För medieresurser, till exempel bilder, exporteras bara en referens till Target. Resursen lagras i AEM Assets och levereras från den AEM publiceringsinstansen.
>
>På grund av detta måste Experience Fragment, med alla relaterade resurser, publiceras före export till Target.

Så här exporterar du ett upplevelsefragment från AEM till mål (efter att du har angett molnkonfigurationen):

1. Navigera till Experience Fragment-konsolen.
1. Välj den Experience Fragment som du vill exportera till mål.

   >[!NOTE]
   >
   >Det måste vara en webbvariant för Experience Fragment.

1. Tryck/klicka **Exportera till Adobe Target**.

   >[!NOTE]
   >
   >Om Experience Fragment redan har exporterats väljer du **Uppdatera i Adobe Target**.

1. Tryck/klicka **Exportera utan publicering** eller **Publicera** efter behov.

   >[!NOTE]
   >
   >Markera **Publicera** publicerar upplevelsefragmentet direkt och skickar det till Target.

1. Tryck/klicka **OK** i bekräftelsedialogrutan.

   Ditt upplevelsefragment bör nu finnas i Target.

   >[!NOTE]
   >
   >[Olika detaljer](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) av exporten visas i **Listvy** av konsolen och **Egenskaper**.

   >[!NOTE]
   >
   >När du visar ett Experience Fragment i Adobe Target *senast ändrad* datum som visas är det datum då fragmentet senast ändrades i AEM, inte det datum då fragmentet senast exporterades till Adobe Target.

>[!NOTE]
>
>Du kan också exportera från sidredigeraren med jämförbara kommandon i [Sidinformation](/help/sites-authoring/author-environment-tools.md#page-information) -menyn.

## Använda dina upplevelsefragment i Adobe Target {#using-your-experience-fragments-in-adobe-target}

När du har utfört de föregående åtgärderna visas upplevelsefragmentet på sidan Erbjudanden i Target. Ta en titt på [specifik Target-dokumentation](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) om du vill veta vad du kan uppnå där.

>[!NOTE]
>
>När du visar ett Experience Fragment i Adobe Target *senast ändrad* datum som visas är det datum då fragmentet senast ändrades i AEM, inte det datum då fragmentet senast exporterades till Adobe Target.

## Ta bort ett Experience Fragment som redan har exporterats till Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

Om du tar bort ett Experience Fragment som redan har exporterats till Target kan det orsaka problem om fragmentet redan används i ett erbjudande i Target. Om du tar bort fragmentet blir erbjudandet oanvändbart eftersom fragmentinnehållet levereras av AEM.

För att undvika sådana situationer:

* Om Experience Fragment inte används för närvarande i en aktivitet kan AEM användaren ta bort fragmentet utan ett varningsmeddelande.
* Om Experience Fragment används för närvarande av en aktivitet i Target får AEM ett felmeddelande om eventuella konsekvenser som en borttagning av fragmentet kan ha för aktiviteten.

   Felmeddelandet i AEM förhindrar inte användaren från att (tvinga) ta bort Experience Fragment. Om Experience Fragment tas bort:

   * Målerbjudandet med AEM Experience Fragment kan visa oönskat beteende

      * Erbjudandet kommer troligtvis fortfarande att återges eftersom Experience Fragment HTML flyttades till Target
      * Eventuella referenser i Experience Fragment kanske inte fungerar korrekt om refererade resurser också tas bort i AEM.
   * Det är förstås inte möjligt att göra ytterligare ändringar i Experience Fragment eftersom Experience Fragment inte längre finns i AEM.
