---
title: Modeller för innehållsfragment
seo-title: Modeller för innehållsfragment
description: Content Fragment Models används för att skapa innehållsfragment med strukturerat innehåll.
seo-description: Content Fragment Models används för att skapa innehållsfragment med strukturerat innehåll.
uuid: 73e38629-37c6-4f68-97a9-62f9783cc3d4
content-type: reference
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 9da10294-2dc8-4e82-8d32-f034e6a5aeeb
docset: aem65
feature: Content Fragments
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 20%

---


# Modeller för innehållsfragment{#content-fragment-models}

Modeller för innehållsfragment definierar innehållsstrukturen för dina [innehållsfragment](/help/assets/content-fragments/content-fragments.md).

## Aktivera modeller för innehållsfragment {#enable-content-fragment-models}

>[!CAUTION]
>
>Om du inte aktiverar **Content Fragment Models** kommer alternativet **Create** inte att vara tillgängligt för att skapa nya modeller.

Om du vill aktivera innehållsfragmentmodeller måste du:

* Aktivera användning av innehållsfragmentmodeller i [Configuration Browser](/help/sites-administering/configurations.md)
* Använda konfigurationen i resursmappen

### Aktivera modeller för innehållsfragment i Configuration Manager {#enable-content-fragment-models-in-configuration-manager}

Om du vill [skapa en ny innehållsfragmentmodell](#creating-a-content-fragment-model) måste du **först aktivera dem med Configuration Manager:**

>[!CAUTION]
>
>Delkonfigurationer (en konfiguration som är kapslad i en konfiguration) stöds inte för användning med innehållsfragment.

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Konfigurationsläsaren**.

1. Använd **Skapa** för att öppna dialogrutan där du:

   1. Ange en **titel**.
   1. Välj **Content Fragment Models** för att aktivera användningen av dem.

   ![cfm-6420-09](assets/cfm-6420-09.png)

1. Välj **Skapa** om du vill spara definitionen.

<!-- 1. Select the location appropriate to your website. -->

### Använd konfigurationen i resursmappen {#apply-the-configuration-to-your-assets-folder}

När konfigurationen **global** är aktiverad för innehållsfragmentmodeller kan alla modeller som användarna skapar användas i alla Resursmappar.

Om du vill använda andra konfigurationer (dvs. exkludera globala) med en jämförbar Assets-mapp måste du definiera kopplingen. Detta görs i **Konfiguration** på fliken **Cloud Services** i **Mappegenskaper** för önskad mapp.

## Skapa en innehållsfragmentmodell {#creating-a-content-fragment-model}

1. Navigera till **Verktyg**, **Resurser** och öppna sedan **Modeller för innehållsfragment**.
1. Navigera till den mapp som passar din [konfiguration](#enable-content-fragment-models).
1. Använd **Skapa** för att öppna guiden.

   >[!CAUTION]
   >
   >Om [användningen av innehållsfragmentmodeller inte har aktiverats](#enable-content-fragment-models) är alternativet **Skapa** inte tillgängligt.

1. Ange **modelltitel**. Du kan också lägga till en **beskrivning** om det behövs.

   ![cfm-6420-10](assets/cfm-6420-10.png)

1. Använd **Skapa** för att spara den tomma modellen. Ett meddelande visar att åtgärden lyckades, du kan välja **Öppna** om du vill redigera modellen direkt eller **Klar** om du vill återgå till konsolen.

## Definiera innehållsfragmentmodellen {#defining-your-content-fragment-model}

Modellen för innehållsfragment definierar effektivt strukturen för de resulterande innehållsfragmenten. Med modellredigeraren kan du lägga till och konfigurera obligatoriska fält:

>[!CAUTION]
>
>Om du redigerar en befintlig innehållsfragmentmodell kan det påverka beroende fragment.

1. Navigera till **Verktyg**, **Resurser** och öppna sedan **Modeller för innehållsfragment**.

1. Navigera till mappen som innehåller innehållsfragmentmodellen.
1. Öppna önskad modell för **Redigera**; använd snabbåtgärden eller välj modell och sedan åtgärden från verktygsfältet.

   När du har öppnat modellredigeraren visas följande:

   * vänster: fält har redan definierats
   * höger: **Datatyper** som är tillgängliga för att skapa fält (och **egenskaper** som kan användas när fälten har skapats)

   >[!NOTE]
   >
   >När ett fält är **obligatoriskt** markeras den **etikett** som visas i den vänstra rutan med en asterisk (*****).

   ![cfm-6420-12](assets/cfm-6420-12.png)

1. **Lägga till ett fält**

   * Dra en obligatorisk datatyp till önskad plats för ett fält:

   ![cfm-6420-11](assets/cfm-6420-11.png)

   * När ett fält har lagts till i modellen visar den högra panelen de **egenskaper** som kan definieras för den aktuella datatypen. Här definierar du vad som krävs för fältet. Till exempel:

   ![cfm-6420-13](assets/cfm-6420-13.png)

   >[!NOTE]
   För datatypen **Flerradig text** går det att definiera **standardtypen** som endera:
   * **RTF-text**

   * **Markdown**

   * **Oformaterad text**

   Om inget anges används standardvärdet **RTF** för det här fältet.
   Om du ändrar **standardtypen** i en innehållsfragmentmodell börjar detta bara gälla för ett befintligt, relaterat innehållsfragment efter att fragmentet har öppnats i redigeraren och sparats.

1. **Ta bort ett fält**

   Markera det obligatoriska fältet och klicka/tryck sedan på papperskorgsikonen. Du ombeds bekräfta åtgärden.

   ![cf-32](assets/cf-32.png)

1. När du har lagt till alla obligatoriska fält och definierat egenskaperna använder du **Spara** för att behålla definitionen. Till exempel:

   ![cfm-6420-14](assets/cfm-6420-14.png)

## Ta bort en innehållsfragmentmodell {#deleting-a-content-fragment-model}

>[!CAUTION]
Om du tar bort en innehållsfragmentmodell kan det påverka beroende fragment.

Så här tar du bort en innehållsfragmentmodell:

1. Navigera till **Verktyg**, **Resurser** och öppna sedan **Modeller för innehållsfragment**.

1. Navigera till mappen som innehåller innehållsfragmentmodellen.
1. Markera modellen följt av **Ta bort** från verktygsfältet.

   >[!NOTE]
   Om det refereras till modellen visas en varning. Vidta lämpliga åtgärder.

## Publicera en innehållsfragmentmodell {#publishing-a-content-fragment-model}

Modeller för innehållsfragment måste publiceras när/innan beroende innehållsfragment publiceras.

Så här publicerar du en innehållsfragmentmodell:

1. Navigera till **Verktyg**, **Resurser** och öppna sedan **Modeller för innehållsfragment**.

1. Navigera till mappen som innehåller innehållsfragmentmodellen.
1. Välj modell följt av **Publicera** i verktygsfältet.

   >[!NOTE]
   Om du publicerar ett innehållsfragment för vilket modellen ännu inte har publicerats, visas detta i en urvalslista och modellen publiceras med fragmentet.

