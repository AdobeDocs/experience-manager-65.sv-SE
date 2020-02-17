---
title: Exportera Experience Fragments till Adobe Target
seo-title: Exportera Experience Fragments till Adobe Target
description: Exportera Experience Fragments till Adobe Target
seo-description: Exportera Experience Fragments till Adobe Target
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
translation-type: tm+mt
source-git-commit: 6723b12bebba2f239c0886e5f378f1dc70e5e247

---


# Exportera Experience Fragments till Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>Vissa funktioner på den här sidan kräver att du använder AEM 6.5.3.0.
>
>6.5.3.0
>
>* **Externalizer-domäner** kan nu väljas.
>
>
6.5.2.0:
>
>* Upplevelsefragment kan exporteras till:
   >   * standardarbetsytan.
   >   * en namngiven arbetsyta som anges i molnkonfigurationen.
>* AEM måste vara [integrerat med Adobe Target med hjälp av Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md).
>
>
AEM 6.5.0.0 och 6.5.1.0:
>
>* AEM Experience Fragments exporteras till standardarbetsytan i Adobe Target.
>* AEM måste integreras med Adobe Target enligt instruktionerna under [Integrering med Adobe Target](/help/sites-administering/target.md).


Du kan exportera [Experience Fragments](/help/sites-authoring/experience-fragments.md), som har skapats i Adobe Experience Manager (AEM), till Adobe Target (Target). De kan sedan användas som erbjudanden i Target-aktiviteter för att testa och personalisera upplevelser i stor skala.

Det finns tre formatalternativ för att exportera en Experience Fragment till Adobe Target:

* HTML (standard): Stöd för leverans av webb- och hybridinnehåll
* JSON: Stöd för leverans av headless-material
* HTML och JSON

AEM Experience Fragments kan exporteras till standardarbetsytan i Adobe Target eller till användardefinierade arbetsytor för Adobe Target. Detta görs via Adobe I/O, som AEM måste [integreras med Adobe Target med hjälp av Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md).

>[!NOTE]
>
>Adobe Target-arbetsytorna finns inte i Adobe Target. De definieras och hanteras i Adobe IMS (Identity Management System) och väljs sedan ut för användning i olika lösningar med hjälp av Adobe I/O-integreringar.

>[!NOTE]
>
>Adobe Target-arbetsytor kan användas för att tillåta medlemmar i en organisation (grupp) att skapa och hantera erbjudanden och aktiviteter endast för den här organisationen. utan att ge åtkomst till andra användare. Till exempel landsspecifika organisationer inom ett globalt område.

>[!NOTE]
>
>Mer information finns också i:
>
>* [Utveckling med Adobe Target](https://www.adobe.io/apis/experiencecloud/target.html)
>* [Kärnkomponenter - Upplevelsefragment](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)
>



## Förutsättningar {#prerequisites}

>[!CAUTION]
>
>Vissa funktioner på den här sidan kräver att du använder AEM 6.5.3.0.

Du måste utföra olika åtgärder:

1. Du måste [integrera AEM med Adobe Target med Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md).
2. Experience Fragments exporteras från AEM-författarinstansen, så du måste [konfigurera AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) för författarinstansen för att se till att alla referenser i Experience Fragment är externaliserade för webbleverans.

   >[!NOTE]
   >
   >För läntredigering som inte omfattas av standardinställningen är [Experience Fragment Link Rewriter-providern](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) tillgänglig. Med detta kan ni utveckla anpassade regler för er instans.

## Lägg till molnkonfigurationen {#add-the-cloud-configuration}

Innan du exporterar ett fragment måste du lägga till **molnkonfigurationen** för **Adobe Target** i fragmentet eller mappen. Detta gör även att du kan:

* ange de formatalternativ som ska användas för exporten
* välj en målarbetsyta som mål
* välj en externaliseringsdomän för att skriva om referenser i Experience Fragment (valfritt)

De obligatoriska alternativen kan väljas i **Sidegenskaper** för den mapp och/eller det fragment som krävs. specifikationen ärvs vid behov.

1. Gå till konsolen **Experience Fragments** .

1. Öppna **Sidegenskaper** för rätt mapp eller fragment.

   >[!NOTE]
   >
   >Om du lägger till molnkonfigurationen i den överordnade Experience Fragment-mappen ärvs konfigurationen av alla underordnade.
   >
   >
   >Om du lägger till molnkonfigurationen i själva Experience Fragment ärvs konfigurationen av alla variationer.

1. Välj fliken **Molntjänster** .

1. Välj **Adobe Target** i listrutan under Konfiguration **av** molntjänster.

1. 
   >[!NOTE]
   >
   >JSON-formatet i ett Experience Fragment-erbjudande kan anpassas. Om du vill göra det definierar du en Customer Experience Fragment-komponent och kommenterar sedan hur egenskaperna ska exporteras i komponentens Sling Model.
   >
   >Se kärnkomponenten:
   >
   >[Kärnkomponenter - Upplevelsefragment](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   Under **Adobe Target** väljer du:

   * lämplig konfiguration
   * det obligatoriska formatalternativet
   * en Adobe Target-arbetsyta
   * om det behövs - externaliseringsdomänen
   >[!CAUTION]
   >
   >Externeringsdomänen är valfri. En AEM-externalisering konfigureras när du vill att det exporterade innehållet ska peka på en specifik *publiceringsdomän* . Mer information finns i [Konfigurera AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer).

   För en mapp:

   ![Mapp - molntjänster](assets/xf-target-integration-01.png "Mapp - molntjänster")

1. **Spara och stäng**.

## Exportera en Experience Fragment till Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>För medieresurser, till exempel bilder, exporteras bara en referens till Target. Resursen lagras i AEM Resurser och levereras från AEM-publiceringsinstansen.
>
>På grund av detta måste Experience Fragment, med alla relaterade resurser, publiceras före export till Target.

Så här exporterar du ett upplevelsefragment från AEM till Target (efter att du har angett molnkonfigurationen):

1. Navigera till Experience Fragment-konsolen.
1. Välj den Experience Fragment som du vill exportera till mål.

   >[!NOTE]
   >
   >Det måste vara en webbvariant för Experience Fragment.

1. Tryck/klicka på **Exportera till Adobe Target**.

   >[!NOTE]
   >
   >Om Experience Fragment redan har exporterats väljer du **Uppdatera i Adobe Target**.

1. Tryck/klicka på **Exportera utan publicering** eller **Publicera** efter behov.

   >[!NOTE]
   >
   >Om du väljer **Publicera** publiceras upplevelsefragmentet direkt och skickas till Target.

1. Tryck/klicka på **OK** i bekräftelsedialogrutan.

   Ditt upplevelsefragment bör nu finnas i Target.

   >[!NOTE]
   >
   >[Olika detaljer](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) om exporten visas i **listvyn** i konsolen och i **Egenskaper**.

   >[!NOTE]
   >
   >När du visar ett Experience Fragment i Adobe Target är det *senaste ändringsdatumet* som visas det datum då fragmentet senast ändrades i AEM, inte det datum då fragmentet senast exporterades till Adobe Target.

>[!NOTE]
>
>Du kan också exportera från sidredigeraren med hjälp av jämförbara kommandon på menyn [Sidinformation](/help/sites-authoring/author-environment-tools.md#page-information) .

## Använda dina upplevelsefragment i Adobe Target {#using-your-experience-fragments-in-adobe-target}

När du har utfört de föregående åtgärderna visas upplevelsefragmentet på sidan Erbjudanden i Target. Ta en titt på den [specifika Target-dokumentationen](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) och lär dig mer om vad du kan uppnå där.

>[!NOTE]
>
>När du visar ett Experience Fragment i Adobe Target är det *senaste ändringsdatumet* som visas det datum då fragmentet senast ändrades i AEM, inte det datum då fragmentet senast exporterades till Adobe Target.

## Ta bort ett Experience Fragment som redan har exporterats till Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

Om du tar bort ett Experience Fragment som redan har exporterats till Target kan det orsaka problem om fragmentet redan används i ett erbjudande i Target. Om du tar bort fragmentet blir erbjudandet oanvändbart eftersom fragmentinnehållet levereras av AEM.

För att undvika sådana situationer:

* Om Experience Fragment inte används för närvarande i en aktivitet kan användaren ta bort fragmentet utan ett varningsmeddelande.
* Om Experience Fragment används av en aktivitet i Target får AEM-användaren ett felmeddelande om eventuella konsekvenser som en borttagning av fragmentet kan ha för aktiviteten.

   Felmeddelandet i AEM förhindrar inte användaren från att (tvinga) ta bort Experience Fragment. Om Experience Fragment tas bort:

   * Target-erbjudandet med AEM Experience Fragment kan visa oönskat beteende

      * Erbjudandet kommer troligtvis fortfarande att återges eftersom Experience Fragment HTML överfördes till Target
      * Eventuella referenser i Experience Fragment kanske inte fungerar korrekt om refererade resurser även har tagits bort i AEM.
   * Det är förstås inte möjligt att göra ytterligare ändringar i Experience Fragment eftersom Experience Fragment inte längre finns i AEM.