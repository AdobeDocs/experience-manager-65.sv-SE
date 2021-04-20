---
title: 'Formatera ditt anpassningsbara formulär '
seo-title: 'Formatera ditt anpassningsbara formulär '
description: 'Lär dig skapa ett anpassat tema, formatera enskilda komponenter och använda webbteckensnitt i ett tema '
seo-description: 'Lär dig skapa ett anpassat tema, formatera enskilda komponenter och använda webbteckensnitt i ett tema '
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 5%

---


# Formatera ditt adaptiva formulär {#do-not-publish-style-your-adaptive-form}

Lär dig skapa ett anpassat tema, formatera enskilda komponenter och använda webbteckensnitt i ett tema

![](do-not-localize/08-style_your_adaptiveformmain.png)

Den här självstudiekursen är ett steg i [Skapa ditt första adaptiva formulär](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)-serien. Vi rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga exemplet på självstudiekurser.

## Om självstudiekursen {#about-the-tutorial}

Du kan använda teman för att ge ett anpassat formulär ett unikt utseende och en unik stil. Du kan använda färdiga teman som medföljer redigeringsprogrammet för anpassade formulär eller skapa egna teman. AEM [!DNL Forms] tillhandahåller en [temaredigerare](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html) för att skapa anpassade teman. Ett och samma tema kan ge olika utseenden till samma adaptiva formulär som öppnas på mobilen, surfplattan eller datorn. Det krävs ingen tidigare kunskap om CSS eller LESS för att kunna använda temaredigeraren, men det är önskvärt.

I slutet av självstudiekursen kommer du att lära dig att:

* Använda ett tema i ett anpassat formulär
* Skapa ett tema för anpassningsbara formulär med temaredigeraren
* Formatera enskilda komponenter
* Bonusavsnitt: Använda webbteckensnitt i ett anpassat tema

Formuläret ser ut ungefär så här när du är klar med självstudiekursen:

![Formulär med anpassat tema](assets/styled-adaptive-form.png)

## Innan du startar {#before-you-start}

Ladda ned rubrikbilderna och logotypbilderna nedan på din dator. Rubriken för det adaptiva formuläret `shipping-address-add-update-form` använder rubrikstilen och logotypbilderna. Bilden i sidhuvudsstil visas till höger om sidhuvudet.

[Hämta fil](assets/header-style.png)

[Hämta fil](assets/logo-1.png)

## Steg 1: Använd ett tema i ditt adaptiva formulär {#step-apply-a-theme-to-your-adaptive-form}

Adaptiv formulärredigerare har flera färdiga teman. Om du inte tänker använda en anpassad stil för ditt adaptiva formulär kan du även publicera dina adaptiva formulär med ett användbart tema. Temana är oberoende av anpassningsbara formulär. Du kan använda samma tema för flera adaptiva formulär. Så här använder du ett tema i ett anpassat formulär:

1. Öppna det adaptiva formuläret för redigering.

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. Öppna egenskaperna för **[!UICONTROL Adaptive Form container]**. Navigera till **[!UICONTROL Basic]** > **[!UICONTROL Adaptive Form Theme]** i egenskapsläsaren. I fältet **[!UICONTROL Adaptive Form Theme]** visas alla färdiga och anpassade teman. Som standard används Canvas-temat.
1. Välj ett tema i fältet **[!UICONTROL Adaptive Form Theme]**. Exempel: **Undersökningstema**. Tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) för att använda det valda temat.

   ![Adaptiv form med standardtemat](assets/default-adaptive-form.png)

   **Figur:** *Adaptiv form med standardtemat*

   ![Adaptiv form med undersökningstemat](assets/adaptive-form-with-survey-theme.png)

   **Figur:** *Adaptiv form med Undersökningstemat*

## Steg 2: Uppdatera ditt adaptiva formulär {#step-update-your-adaptive-form}

Den design som visas ovan kräver ändringar i platshållartext och logotyp i ditt befintliga adaptiva formulär. Utför följande steg för att göra de ändringar som krävs:

1. Ändra den befintliga logotypen och texten för sidhuvudet. Så här tar du bort logotypen:

   1. Öppna formuläret i formulärredigeraren.

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. Tryck på logotypbilden i [!UICONTROL header]-komponenten och tryck på ![cmpr](assets/cmppr.png) **[!UICONTROL properties]**. I egenskapen [!UICONTROL image] trycker du på X för att ta bort den befintliga logotypbilden.
   1. Tryck på **[!UICONTROL upload]**, markera logotypen.png och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) för att spara ändringarna. Bilden hämtades i [Innan du startar](/help/forms/using/style-your-adaptive-form.md#before-you-start)-avsnittet.
   1. Tryck på rubriktext, `We.Retail`, och tryck på ![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL edit]**. Ändra rubriktext till `we retail`. Använd endast fet stil på `we`i `we retail`.

      ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. Ta bort rubrik och lägg till platshållartext:

   1. Tryck på fältet Kund-ID och tryck på ![cmpr](assets/cmppr.png)-egenskaper.
   1. Kopiera innehållet i **[!UICONTROL Title]**-fältet till **[!UICONTROL Placeholder Text]**-fältet.
   1. Ta bort innehållet i fältet **[!UICONTROL Title]** och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
   1. Upprepa de tre föregående stegen för alla textrutor, numeriska rutor och e-postfält i formuläret.

      ![updated-adaptive-form](assets/updated-adaptive-form.png)

## Steg 3: Skapa ett anpassat tema för ditt adaptiva formulär {#step-create-a-custom-theme-for-your-adaptive-form}

Du kan använda [temaredigeraren](/help/forms/using/themes.md) för att skapa anpassade teman. Temats redigerare är en kraftfull WYSIWYG-redigerare. Det är en visuell metod att använda CSS på olika komponenter i ett adaptivt formulär. Den ger finare kontroller för att formatera komponenter och paneler i ett adaptivt formulär.

Ett tema är en separat enhet som anpassningsbara formulär. Den innehåller format (CSS) för komponenterna och panelerna i ett anpassat formulär. Formaten innehåller CSS-egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet, justering och storlek. När du använder ett tema används det angivna formatet på motsvarande komponenter i ett anpassat formulär.

I den här självstudiekursen kommer du att formatera sidhuvud och sidfot, text och numeriska komponenter, bilagekomponenter och knappar. Låt oss börja med att skapa ett tema:

### Skapa ett tema {#create-a-theme}

1. Logga in på AEM författarinstans och navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Themes]**. Standardwebbadressen är [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes).
1. Tryck på **[!UICONTROL Create]** och välj **[!UICONTROL Theme]**. Sidan [!UICONTROL Create Theme] med de fält som krävs för att skapa ett tema visas. Fälten **[!UICONTROL Title]** och **[!UICONTROL Name]** är obligatoriska:

   * **Titel:** Ange temats titel. Exempel: **Global Theme.** Titeln hjälper dig att identifiera temat från listan med teman.
   * **Namn:** Ange temats namn. Exempel: **Global-Theme.** En nod med det angivna namnet skapas i databasen. När du börjar skriva en titel genereras värdet för namnfältet automatiskt. Du kan ändra det föreslagna värdet. Namnfältet får endast innehålla alfanumeriska tecken, bindestreck och understreck. Alla ogiltiga indata ersätts med ett bindestreck.

1. Tryck på **[!UICONTROL Create]**. Ett tema skapas och en dialogruta visas där du kan öppna formuläret för redigering. Tryck på **[!UICONTROL Open]** för att öppna det nya temat på en ny flik. Temat öppnas i temaredigeraren. För formatering används ett anpassat formulär som levereras med AEM [!DNL Forms].

   Mer information om hur du använder gränssnittet för temaredigeraren finns i [Om temaredigeraren](/help/forms/using/themes.md#aboutthethemeeditor).

1. Tryck på **[!UICONTROL Theme Options]** ![theme-options](assets/theme-options.png) > **[!UICONTROL Configure]**. I fältet **[!UICONTROL Preview Form]** väljer du det adaptiva formuläret **shipping-address-add-update-form**, trycker på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) och trycker på **[!UICONTROL Save]**. Nu är temaredigeraren konfigurerad att använda ditt eget adaptiva formulär i stället för det adaptiva standardformatet. Tryck på **[!UICONTROL Cancel]** för att återgå till temaredigeraren.

   ![anpassat tema](assets/custom-theme.png)

   **Bild:** *Theme editor med adaptiv blankett för leverans-address-add-update-form*

   ![create-a-theme](assets/create-a-theme.png)

   **Figur:** *Adaptiv form med standardformuläret*

### Formatera sidhuvud och sidfot {#style-header-and-footer}

Sidhuvud och sidfot ger ett konsekvent och distinkt utseende i en adaptiv form. I allmänhet innehåller sidhuvudet organisationens logotyp och namn, sidfoten innehåller copyrightinformation och dessa är identiska i flera former av en organisation. Gör så här för att formatera sidhuvud och sidfot i anpassat formulär för leverans-address-add-update:

1. Navigera till alternativet **[!UICONTROL Header]** > **[!UICONTROL Text]** på panelen Väljare. Väljarpanelen är till vänster om temaredigeraren. Om panelen inte visas trycker du på ![växlingspanel](assets/toggle-side-panel.png) växlingspanel.

1. Ange följande egenskaper i dragspelet **[!UICONTROL Text]** och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Egenskap | Värde |
   |---|---|
   | Teckensnittsfamilj | Arial |
   | Teckenfärg | FFFFFF |
   | Teckenstorlek | 54px |

1. Tryck på widgeten [!UICONTROL header] och tryck på **[!UICONTROL Header]**. Alternativen för att formatera sidhuvudswidgeten visas till vänster. Expandera dragspelet **[!UICONTROL Dimensions & Position]**, ställ in **[!UICONTROL Height]** på `120px` och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. Expandera dragspelsfliken **[!UICONTROL Background]** för sidhuvudswidgeten och ställ in **[!UICONTROL Background Color]** på `F6921E.`

   Håll pekaren över **[!UICONTROL Image & Gradient]** > **[!UICONTROL + Add]**, tryck **[!UICONTROL Image]**. Ange följande egenskaper och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Egenskap | Värde |
   |---|---|
   | bild | Överför header-style.png. Bilden hämtades i [Innan du startar](/help/forms/using/style-your-adaptive-form.md#before-you-start)-avsnittet. |
   | Position | Höger nerifrån |
   | Passram | Ingen upprepning |

1. Tryck på logotypen i sidhuvudet i temaredigeraren och tryck på **[!UICONTROL Header Logo]**. Expandera dragspelsfliken Dimensioner och position, ange följande egenskaper och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Marginal</b></td> 
      <td><b>Värde</b></td> 
     </tr> 
     <tr> 
      <td>Marginal</td> 
      <td> 
       <ul> 
        <li>Överkant: 1,5 rem</li> 
        <li>Underkant: -35px</li> 
        <li>Vänster: 1rem<strong><br /> </strong></li> 
       </ul> <p><strong>Tips:</strong> Tryck på  <img src="assets/link.png"> länkikonen för att ange olika värden för varje fält.<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>Höjd</td> 
      <td>4,75rem</td> 
     </tr> 
    </tbody> 
   </table>

1. Tryck på sidfotswidgeten och tryck på **[!UICONTROL Footer]**. Expandera dragspelet **[!UICONTROL Background]**, ställ in **[!UICONTROL Background Color]** på `F6921E` och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

### Formatera datainhämtningskomponenten och använd en bakgrund i det adaptiva formuläret {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

Du kan använda flera komponenter i ett adaptivt formulär för att hämta data. Till exempel textruta och numerisk ruta. Du kan ange identiska format för alla datainhämtningskomponenter eller separata format för varje komponent. I den här självstudiekursen används ett identiskt format för numeriska rutor (Kund-ID, Postnummer) och textrutor (Kund-ID, Namn, Leveransadress, Tillstånd, E-post). Så här formaterar du komponenter för datainhämtning:

1. Tryck på fältet **[!UICONTROL Customer ID]** och tryck på alternativet **[!UICONTROL Field Widget]**. Ange följande egenskaper och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Dragspel</b></td> 
      <td><b>Egenskap</b></td> 
      <td><b>Värde</b></td> 
     </tr> 
     <tr> 
      <td>Kantlinje</td> 
      <td>Kantlinjefärg</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>Kantlinje</td> 
      <td>Kantradie </td> 
      <td> 
       <ul> 
        <li>Överkant: 7px<br /> </li> 
        <li>Höger: 7px<br /> </li> 
        <li>Underkant: 7px<br /> </li> 
        <li>Vänster: 7px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Teckensnittsfamilj</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Teckenfärg</td> 
      <td>939598<br /> </td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Teckenstorlek</td> 
      <td>18px</td> 
     </tr> 
     <tr> 
      <td>Dimensioner och position</td> 
      <td>Bredd</td> 
      <td>60 %</td> 
     </tr> 
     <tr> 
      <td>Dimensioner och position</td> 
      <td>Marginal</td> 
      <td> 
       <ul> 
        <li>Vänster: 10rem</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. Tryck på det tomma området ovanför fältet **[!UICONTROL Customer ID]** och tryck på **[!UICONTROL Responsive Panel Container]**. Ange **[!UICONTROL Background]** > **[!UICONTROL Background Color]** som F1F2F2. Tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   ![](do-not-localize/responsive-panel-container.png)

### Formatera knapparna {#style-the-buttons}

Du kan använda ett anpassat tema för att tillämpa ett identiskt format på alla knappar i det adaptiva formuläret och [intern formatering](/help/forms/using/inline-style-adaptive-forms.md) för att tillämpa ett format på en viss knapp. Så här formaterar du knapparna:

1. Tryck på knappen **[!UICONTROL Submit]** och tryck på alternativet **[!UICONTROL Button]**. Ange följande egenskaper och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Dragspel</b></td> 
      <td><b>Egenskap</b></td> 
      <td><b>Värde</b></td> 
     </tr> 
     <tr> 
      <td>Bakgrund</td> 
      <td>Bakgrundsfärg</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Kant<br /> </td> 
      <td>Kantlinjefärg</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Kantlinje</td> 
      <td>Kantradie </td> 
      <td> 
       <ul> 
        <li>Överkant: 7px<br /> </li> 
        <li>Höger: 7px<br /> </li> 
        <li>Underkant: 7px<br /> </li> 
        <li>Vänster: 7px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Text<br /> </td> 
      <td>Teckensnittsfamilj</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Teckenfärg</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Teckenstorlek</td> 
      <td>18px</td> 
     </tr> 
    </tbody> 
   </table>

1. [Använd det anpassade temat](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form), Global Theme, i ditt adaptiva formulär. Om formatet inte återspeglas i det adaptiva formuläret rensar du webbläsarcachen och försöker igen.

   ![style-data-capture-components](assets/style-data-capture-components.png)

## Steg 4: Formatera enskilda komponenter {#step-style-individual-components}

Vissa format gäller bara för en viss komponent. Sådana komponenter är formaterade i en adaptiv formulärredigerare.

1. Öppna det adaptiva formuläret för redigering. [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. Välj alternativet **[!UICONTROL Style]** i det övre fältet.

   ![style-option](assets/style-option.png)

1. Tryck på knappen **[!UICONTROL Attach]** och tryck på ikonen ![aem_6_3_edit](assets/aem_6_3_edit.png). Ange följande egenskaper i dragspelet **[!UICONTROL Dimensions and Position]**:

   | Egenskap | Värde |
   |---|---|
   | Flyttal | Vänster |
   | Bredd | 10% |

1. Tryck på alternativet **[!UICONTROL Government approved address proof]** och tryck på ikonen ![aem_6_3_edit](assets/aem_6_3_edit.png). Ange följande egenskaper:

   <table> 
    <tbody> 
     <tr> 
      <td><b>Dragspel</b></td> 
      <td><b>Egenskap</b></td> 
      <td><b>Värde</b></td> 
     </tr> 
     <tr> 
      <td>Dimensioner och position</td> 
      <td>Flyttal</td> 
      <td>Vänster</td> 
     </tr> 
     <tr> 
      <td>Dimensioner och position</td> 
      <td>Bredd</td> 
      <td>73 %</td> 
     </tr> 
     <tr> 
      <td>Dimensioner och position</td> 
      <td>Utfyllnad</td> 
      <td> 
       <ul> 
        <li>Vänster: 10px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Dimensioner och position</td> 
      <td>Höjd</td> 
      <td>40px</td> 
     </tr> 
     <tr> 
      <td>Dimensioner och position<br /> </td> 
      <td>Marginal</td> 
      <td><br /> 
       <ul> 
        <li>Höger: 2 rem</li> 
        <li>Vänster: 10rem </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Bakgrund</td> 
      <td>Bakgrundsfärg</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>Kantlinje</td> 
      <td>Kantbredd</td> 
      <td>1px</td> 
     </tr> 
     <tr> 
      <td>Kantlinje</td> 
      <td>Kantstil</td> 
      <td>Heldragen</td> 
     </tr> 
     <tr> 
      <td>Kantlinje</td> 
      <td>Kantlinjefärg</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>Kantlinje</td> 
      <td>Kantradie</td> 
      <td>7px</td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Teckensnittsfamilj</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Teckenfärg</td> 
      <td>BCBEC0</td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Teckenstorlek</td> 
      <td>18px</td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Radhöjd</td> 
      <td>2</td> 
     </tr> 
     </tr> 
    </tbody> 
   </table>

1. Tryck på knappen **[!UICONTROL Submit]** och tryck på ikonen ![aem_6_3_edit](assets/aem_6_3_edit.png). Ange följande egenskaper:

   <table> 
    <tbody> 
     <tr> 
      <td><b>Dragspel</b></td> 
      <td><b>Egenskap</b></td> 
      <td><b>Värde</b></td> 
     </tr> 
     <tr> 
      <td>Dimensioner och position</td> 
      <td>Flyttal</td> 
      <td>Höger</td> 
     </tr> 
     <tr> 
      <td>Dimensioner och position</td> 
      <td>Marginal</td> 
      <td> 
       <ul> 
        <li>Överkant: 5 rem</li> 
        <li>Höger: 14rem</li> 
        <li>Underkant: 20px</li> 
        <li>Vänster: 20px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Bakgrund</td> 
      <td>Bakgrundsfärg</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Kantlinje</td> 
      <td>Kantlinjefärg</td> 
      <td>F6921E</td> 
     </tr> 
    </tbody> 
   </table>

   ![styled-adaptive-form-1](assets/styled-adaptive-form-1.png)

## Steg 5: Bonusavsnitt: Använda webbteckensnitt i ett anpassat tema {#step-bonus-section-using-web-fonts-in-a-custom-theme}

Du kan använda olika teckensnitt för att utforma ett anpassat formulär. Alla enheter som det adaptiva formuläret visas på kanske inte har de teckensnitt som används för att utforma det adaptiva formuläret. Du kan använda en webbteckensnittstjänst för att leverera nödvändiga teckensnitt till målenheten.

[!DNL Adobe Fonts] är en webbteckensnittstjänst. Du kan konfigurera och använda tjänsten med adaptiva formulär. Så här använder du [!DNL Adobe Fonts] i en adaptiv form:

>[!NOTE]
>
>![typekit-to-adobe-](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] fontsis kallas nu Adobe Fonts och ingår i prenumerationer på Creative Cloud och andra. [Läs mer](https://fonts.adobe.com/).

1. Skapa ett [Adobe Fonts](https://typekit.com/)-konto, skapa ett kit, lägg till teckensnittet Myriad Pro i paketet, publicera paketet och få ett kit-ID. Du måste använda [!DNL Adobe Fonts] (webbteckensnitt) i ett anpassat formulär.
1. På AEM [!DNL Forms]-server går du till ![adobeexperienceManager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**. Öppna nu en konfigurationsmapp. Om det redan finns en konfiguration klickar du på knappen **[!UICONTROL Create]** för att skapa en ny instans.

   I dialogrutan Skapa konfiguration anger du en **titel** för konfigurationen och klickar på **[!UICONTROL Create]**. Du omdirigeras till konfigurationssidan. Ange ditt **kit-ID** i dialogrutan [!UICONTROL Edit Component] som visas och klicka på **[!UICONTROL OK]**.

1. Konfigurera temat så att det använder konfigurationen [!DNL Adobe Fonts]. Öppna **[!UICONTROL Global Theme]** i temaredigeraren på författarinstansen. Gå till **[!UICONTROL Theme Options]** ![theme-options](assets/theme-options.png) > **[!UICONTROL Configure]** i temaredigeraren. I fältet **[!UICONTROL Adobe Fonts Configuration]** väljer du paketet och klickar på **[!UICONTROL Save]**.

   Teckensnitten som läggs till i **[!UICONTROL Adobe Fonts]** är tillgängliga för markering i dragspelet **[!UICONTROL Text]** för alla komponenter.

