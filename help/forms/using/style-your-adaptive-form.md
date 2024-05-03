---
title: Formatera ditt anpassningsbara formulär
description: Lär dig att skapa ett anpassat tema, formatera enskilda komponenter och använda Web Fonts i ett tema.
topic-tags: introduction
feature: Adaptive Forms
exl-id: 7742c3ca-1755-44c5-b70f-61309f09d1b8
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1948'
ht-degree: 0%

---

# Formatera ditt anpassningsbara formulär {#do-not-publish-style-your-adaptive-form}

Lär dig att skapa ett anpassat tema, formatera enskilda komponenter och använda Web Fonts i ett tema.

![hero-image](do-not-localize/08-style_your_adaptiveformmain.png)

Den här självstudiekursen är ett steg i [Skapa ditt första adaptiva formulär](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) serie. Adobe rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga självstudiekursen.

## Om självstudiekursen  {#about-the-tutorial}

Du kan använda teman för att ge ett anpassat formulär ett unikt utseende och en unik stil. Du kan använda färdiga teman som medföljer den anpassningsbara formulärredigeraren eller skapa egna teman. AEM [!DNL Forms] tillhandahåller [temaredigerare](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html) för att skapa egna teman. Ett och samma tema kan ge olika utseenden till samma adaptiva formulär som öppnas på mobilen, surfplattan eller datorn. Du behöver inte ha någon tidigare kunskap om CSS eller LESS för att kunna använda temaredigeraren, men du vill ha den.

I slutet av självstudiekursen bör du kunna göra följande:

* Använda ett tema i ett anpassat formulär
* Skapa ett tema för anpassningsbara formulär med temaredigeraren
* Formatera enskilda komponenter
* Bonusavsnitt: Använd Web Fonts i ett anpassat tema

Formuläret ska se ut ungefär så här när du är klar med självstudiekursen:

![Formulär med anpassat tema](assets/styled-adaptive-form.png)

## Innan du börjar {#before-you-start}

Ladda ned rubrikbilderna och logotypbilderna nedan på din dator. Rubriken på `shipping-address-add-update-form` adaptiva formulär använder rubrikbilder och logotypbilder. Bilden i sidhuvudsstil visas till höger om sidhuvudet.

[Hämta fil](assets/header-style.png)

[Hämta fil](assets/logo-1.png)

## Steg 1: Använd ett tema i det anpassade formuläret {#step-apply-a-theme-to-your-adaptive-form}

Adaptiv formulärredigerare har flera färdiga teman. Om du inte tänker använda en anpassad stil för ditt adaptiva formulär kan du även publicera dina adaptiva formulär med ett användbart tema. Temana är oberoende av anpassningsbara formulär. Du kan använda samma tema för flera adaptiva formulär.

**Så här använder du ett tema i ditt adaptiva formulär:**

1. Öppna det adaptiva formuläret för redigering.

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. Öppna egenskaper för **[!UICONTROL Adaptive Form container]**. I egenskapswebbläsaren går du till **[!UICONTROL Basic]** > **[!UICONTROL Adaptive Form Theme]**. The **[!UICONTROL Adaptive Form Theme]** I visas alla färdiga och anpassade teman. Som standard används Canvas-temat.
1. Välj ett tema på menyn **[!UICONTROL Adaptive Form Theme]** fält. Till exempel: **Undersökningstema**. Välj ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) så att du kan använda det valda temat.

   ![Adaptiv form med standardtemat](assets/default-adaptive-form.png)

   **Bild:** *Adaptiv form med standardtemat*

   ![Adaptiv form med Undersökningstemat](assets/adaptive-form-with-survey-theme.png)

   **Bild:** *Adaptiv form med Undersökningstemat*

## Steg 2: Uppdatera ditt anpassningsbara formulär {#step-update-your-adaptive-form}

Den design som visas ovan kräver ändringar i platshållartext och logotyp i ditt befintliga adaptiva formulär.

**Så här uppdaterar du ditt adaptiva formulär:**

1. Ändra den befintliga logotypen och texten för sidhuvudet. Så här tar du bort logotypen:

   1. Öppna formuläret i formulärredigeraren.

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. Välj logotypbild i [!UICONTROL header] -komponent och markera ![cmppr](assets/cmppr.png) **[!UICONTROL properties]**. I [!UICONTROL image] väljer du X för att ta bort den befintliga logotypbilden.
   1. Välj **[!UICONTROL upload]**, markerar logo.png och väljer ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) för att spara ändringarna. Bilden hämtades i [Innan du börjar](/help/forms/using/style-your-adaptive-form.md#before-you-start) -avsnitt.
   1. Markera rubriktext, `We.Retail`och markera ![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL edit]**. Ändra rubriktext till `we retail`. Använd endast fet stil på `we`in `we retail`.

      ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. Ta bort rubrik och lägg till platshållartext:

   1. Markera fältet Kund-ID och välj ![cmppr](assets/cmppr.png) egenskaper.
   1. Kopiera innehållet i **[!UICONTROL Title]** fält till **[!UICONTROL Placeholder Text]** fält.
   1. Ta bort innehållet i **[!UICONTROL Title]** fält och markera ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
   1. Upprepa de tre föregående stegen för alla textrutor, numeriska rutor och e-postfält i formuläret.

      ![updated-adaptive-form](assets/updated-adaptive-form.png)

## Steg 3: Skapa ett anpassat tema för ditt anpassade formulär {#step-create-a-custom-theme-for-your-adaptive-form}

Du kan använda [temaredigerare](/help/forms/using/themes.md) för att skapa egna teman. Temats redigerare är en kraftfull WYSIWYG-redigerare. Det är en visuell metod att använda CSS på olika komponenter i ett adaptivt formulär. Den ger finare kontroller för att formatera komponenter och paneler i ett adaptivt formulär.

Ett tema är en separat enhet som anpassningsbara formulär. Den innehåller format (CSS) för komponenterna och panelerna i ett anpassat formulär. Formaten innehåller CSS-egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet, justering och storlek. När du använder ett tema används det angivna formatet på motsvarande komponenter i ett anpassat formulär.

I den här självstudiekursen formaterar du sidhuvud och sidfot, text och numeriska komponenter, bilagekomponenter och knappar. Låt oss börja med att skapa ett tema:

### Skapa ett tema {#create-a-theme}

1. Logga in på AEM författarinstans och navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Themes]**. Standardwebbadressen är [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes).
1. Välj **[!UICONTROL Create]** och markera **[!UICONTROL Theme]**. The [!UICONTROL Create Theme] visas en sida med de fält som krävs för att skapa ett tema. The **[!UICONTROL Title]** och **[!UICONTROL Name]** fält är obligatoriska:

   * **Titel:** Ange en titel på temat. Till exempel: **Global Theme.** Titeln hjälper dig att identifiera temat från listan med teman.
   * **Namn:** Ange namnet på temat. Till exempel: **Global-Theme.** En nod med det angivna namnet skapas i databasen. När du börjar skriva en titel genereras namnfältets värde automatiskt. Du kan ändra det föreslagna värdet. Namnfältet får endast innehålla alfanumeriska tecken, bindestreck och understreck. Alla ogiltiga indata ersätts med ett bindestreck.

1. Välj **[!UICONTROL Create]**. Ett tema skapas och en dialogruta visas där du kan öppna formuläret för redigering. Välj **[!UICONTROL Open]** om du vill öppna det nya temat på en ny flik. Temat öppnas i temaredigeraren. För formatering används ett anpassat formulär som levereras med AEM [!DNL Forms].

   Mer information om hur du använder gränssnittet för temaredigeraren finns i [Om temaredigeraren](/help/forms/using/themes.md#aboutthethemeeditor).

1. Välj **[!UICONTROL Theme Options]** ![temaalternativ](assets/theme-options.png) > **[!UICONTROL Configure]**. I **[!UICONTROL Preview Form]** fält, välj **shipping-address-add-update-form** adaptiv form, välj ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png), markera **[!UICONTROL Save]**. Nu är temaredigeraren konfigurerad att använda ditt eget adaptiva formulär i stället för det adaptiva standardformatet. Välj **[!UICONTROL Cancel]** för att gå tillbaka till temaredigeraren.

   ![anpassat tema](assets/custom-theme.png)

   **Bild:** *Theme editor with the shipping-address-add-update-form adaptive form*

   ![create-a-theme](assets/create-a-theme.png)

   **Bild:** *Anpassningsbart formulär med standardformuläret*

### Formatera sidhuvud och sidfot {#style-header-and-footer}

Sidhuvud och sidfot ger ett konsekvent och distinkt utseende i en adaptiv form. I allmänhet innehåller sidhuvudet organisationens logotyp och namn, sidfoten innehåller copyrightinformation och dessa är identiska i flera former i en organisation. Så här formaterar du sidhuvud och sidfot i anpassat formulär för leverans-address-add-update-form:

1. Navigera i **[!UICONTROL Header]** > **[!UICONTROL Text]** på panelen Väljare. Väljarpanelen är till vänster om temaredigeraren. Om panelen inte visas väljer du ![växlingspanel](assets/toggle-side-panel.png) Växla sidopanel.

1. Ange följande egenskaper i dialogrutan **[!UICONTROL Text]** dragspelspanel och markera ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Egenskap | Värde |
   |---|---|
   | Font Family | Arial® |
   | Teckenfärg | FFFFFF |
   | Teckenstorlek | 54 px |

1. Välj [!UICONTROL header] widget och markera **[!UICONTROL Header]**. Alternativen för att formatera sidhuvudswidgeten visas till vänster. Expandera **[!UICONTROL Dimensions & Position]** dragspelspanel, ange **[!UICONTROL Height]** till `120px`och markera ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. Expandera **[!UICONTROL Background]** dragspelspanel för sidhuvudswidgeten, ange **[!UICONTROL Background Color]** till `F6921E.`

   Hovring **[!UICONTROL Image & Gradient]** > **[!UICONTROL + Add]**, markera **[!UICONTROL Image]**. Ange följande egenskaper och markera ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Egenskap | Värde |
   |---|---|
   | image | Överför header-style.png. Bilden hämtades i [Innan du börjar](/help/forms/using/style-your-adaptive-form.md#before-you-start) -avsnitt. |
   | Position | Höger nerifrån |
   | Passram | Ingen upprepning |

1. Välj logotypen i rubriken i temaredigeraren och välj **[!UICONTROL Header Logo]**. Expandera dragspelet Dimensioner och position, ange följande egenskaper och markera ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

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
        <li>Nederkant: -35px</li> 
        <li>Vänster: 1 rem<strong><br /> </strong></li> 
       </ul> <p><strong>Tips:</strong> Välj <img src="assets/link.png"> länkikon för att ange olika värden för varje fält.<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>Höjd</td> 
      <td>4,75rem</td> 
     </tr> 
    </tbody> 
   </table>

1. Välj sidfotswidgeten och välj **[!UICONTROL Footer]**. Expandera **[!UICONTROL Background]** dragspelspanel, ange **[!UICONTROL Background Color]** till `F6921E`och markera ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

### Formatera datainhämtningskomponenten och använd en bakgrund i det anpassade formuläret {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

Du kan använda flera komponenter i ett adaptivt formulär för att hämta data. Till exempel textruta och numerisk ruta. Du kan ange ett identiskt format för alla datainhämtningskomponenter eller ett separat format för varje komponent. I den här självstudiekursen används ett identiskt format för numeriska rutor (Kund-ID, Postnummer) och textrutor (Kund-ID, Namn, Leveransadress, Tillstånd, E-post). Så här formaterar du komponenter för datainhämtning:

1. Välj **[!UICONTROL Customer ID]** och välj **[!UICONTROL Field Widget]** alternativ. Ange följande egenskaper och markera ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Dragspel</b></td> 
      <td><b>Egenskap</b></td> 
      <td><b>Värde</b></td> 
     </tr> 
     <tr> 
      <td>Kant</td> 
      <td>Kantfärg</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>Kant</td> 
      <td>Kantradie </td> 
      <td> 
       <ul> 
        <li>Överkant: 7 px<br /> </li> 
        <li>Höger: 7 px<br /> </li> 
        <li>Nederkant: 7 px<br /> </li> 
        <li>Vänster: 7 px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Font Family</td> 
      <td>Arial®</td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Teckenfärg</td> 
      <td>939598<br /> </td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Teckenstorlek</td> 
      <td>18 px</td> 
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
        <li>Vänster: 10 rem</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. Markera det tomma området ovanför **[!UICONTROL Customer ID]** fält och markera **[!UICONTROL Responsive Panel Container]**. Ange **[!UICONTROL Background]** > **[!UICONTROL Background Color]** till F1F2F2. Välj ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   ![Behållare för responsiv panel](do-not-localize/responsive-panel-container.png)

### Formatera knapparna {#style-the-buttons}

Du kan använda ett anpassat tema för att tillämpa en identisk stil på alla knappar i det adaptiva formuläret och [infogad formatering](/help/forms/using/inline-style-adaptive-forms.md) om du vill använda ett format på en viss knapp. Så här formaterar du knapparna:

1. Välj **[!UICONTROL Submit]** och väljer **[!UICONTROL Button]** alternativ. Ange följande egenskaper och markera ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

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
      <td>Kantfärg</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Kant</td> 
      <td>Kantradie </td> 
      <td> 
       <ul> 
        <li>Överkant: 7 px<br /> </li> 
        <li>Höger: 7 px<br /> </li> 
        <li>Nederkant: 7 px<br /> </li> 
        <li>Vänster: 7 px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Text<br /> </td> 
      <td>Font Family</td> 
      <td>Arial®</td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Teckenfärg</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Teckenstorlek</td> 
      <td>18 px</td> 
     </tr> 
    </tbody> 
   </table>

1. [Använd det anpassade temat](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form), Global Theme, till din anpassningsbara form. Om formatet inte återspeglas i det adaptiva formuläret rensar du webbläsarcachen och försöker igen.

   ![style-data-capture-components](assets/style-data-capture-components.png)

## Steg 4: Formatera enskilda komponenter {#step-style-individual-components}

Vissa format gäller bara för en viss komponent. Sådana komponenter är formaterade i en adaptiv formulärredigerare.

1. Öppna det adaptiva formuläret för redigering. [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. I det övre fältet väljer du **[!UICONTROL Style]** alternativ.

   ![style-option](assets/style-option.png)

1. Välj **[!UICONTROL Attach]** och väljer ![aem_6_3_edit](assets/aem_6_3_edit.png)-ikon. Ange följande egenskaper i dialogrutan **[!UICONTROL Dimensions and Position]** dragspelspanel:

   | Egenskap | Värde |
   |---|---|
   | Float | Vänster |
   | Bredd | 10 % |

1. Välj **[!UICONTROL Government approved address proof]** och väljer ![aem_6_3_edit](assets/aem_6_3_edit.png)-ikon. Ange följande egenskaper:

   <table> 
    <tbody> 
     <tr> 
      <td><b>Dragspel</b></td> 
      <td><b>Egenskap</b></td> 
      <td><b>Värde</b></td> 
     </tr> 
     <tr> 
      <td>Dimensioner och position</td> 
      <td>Float</td> 
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
        <li>Vänster: 10 px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Dimensioner och position</td> 
      <td>Höjd</td> 
      <td>40 px</td> 
     </tr> 
     <tr> 
      <td>Dimensioner och position<br /> </td> 
      <td>Marginal</td> 
      <td><br /> 
       <ul> 
        <li>Höger: 2 rem</li> 
        <li>Vänster: 10 rem </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Bakgrund</td> 
      <td>Bakgrundsfärg</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>Kant</td> 
      <td>Kantbredd</td> 
      <td>1 px</td> 
     </tr> 
     <tr> 
      <td>Kant</td> 
      <td>Kantstil</td> 
      <td>Heldragen</td> 
     </tr> 
     <tr> 
      <td>Kant</td> 
      <td>Kantfärg</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>Kant</td> 
      <td>Kantradie</td> 
      <td>7 px</td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Font Family</td> 
      <td>Arial®</td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Teckenfärg</td> 
      <td>BCBEC0</td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Teckenstorlek</td> 
      <td>18 px</td> 
     </tr> 
     <tr> 
      <td>Text</td> 
      <td>Radhöjd</td> 
      <td>2</td> 
     </tr> 
     </tr> 
    </tbody> 
   </table>

1. Välj **[!UICONTROL Submit]** och väljer ![aem_6_3_edit](assets/aem_6_3_edit.png) -ikon. Ange följande egenskaper:

   <table> 
    <tbody> 
     <tr> 
      <td><b>Dragspel</b></td> 
      <td><b>Egenskap</b></td> 
      <td><b>Värde</b></td> 
     </tr> 
     <tr> 
      <td>Dimensioner och position</td> 
      <td>Float</td> 
      <td>Höger</td> 
     </tr> 
     <tr> 
      <td>Dimensioner och position</td> 
      <td>Marginal</td> 
      <td> 
       <ul> 
        <li>Överkant: 5 rem</li> 
        <li>Höger: 14 rem</li> 
        <li>Nederkant: 20 px</li> 
        <li>Vänster: 20 px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Bakgrund</td> 
      <td>Bakgrundsfärg</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Kant</td> 
      <td>Kantfärg</td> 
      <td>F6921E</td> 
     </tr> 
    </tbody> 
   </table>

   ![styled-adaptive-form-1](assets/styled-adaptive-form-1.png)

## Steg 5: Bonusavsnitt: Använda Web Fonts i ett anpassat tema {#step-bonus-section-using-web-fonts-in-a-custom-theme}

Du kan använda olika teckensnitt för att utforma ett anpassat formulär. Alla enheter som det adaptiva formuläret visas på kanske inte har de teckensnitt som används för att utforma det adaptiva formuläret. Du kan använda en webbteckensnittstjänst för att leverera nödvändiga teckensnitt till målenheten.

[!DNL Adobe Fonts] är en tjänst i Web Fonts. Du kan konfigurera och använda tjänsten med adaptiva formulär. Används [!DNL Adobe Fonts] i adaptiv form:
1. Sök i [bibliotek med Adobe-teckensnitt](https://fonts.adobe.com/) och välj teckensnitt för att formatera formuläret.
<!--
>[!NOTE]
>
>![typekit-to-adobe-fonts](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] is now called Adobe Fonts and is included with Creative Cloud and other subscriptions. [Learn more](https://fonts.adobe.com/).-->

>[!NOTE]
>
> Du kan lägga till taggar eller filter för att förfina teckensnittslistan.

1. Klicka på knappen &lt;/> för att lägga till familjen i ett webbprojekt, om du skulle hitta ett typsnitt du gillar.

   ![select-font-from-font-libary](assets/select-font-from-font-library.png)

   Dialogrutan Lägg till teckensnitt i ett webbprojekt visas.

   >[!NOTE]
   >
   > Du kan bara lägga till teckensnitt i ditt webbprojekt om knappen &lt;/> är tillgänglig.

2. Ge webbprojektet ett namn.
3. Markera kryssrutorna för de teckensnittsvikter och format som du vill använda.

   ![lägga till ett teckensnittsbibliotek](assets/add-a-font-window.png)

4. Välj **Klicka** för att skapa projektet.
5. Kopiera inbäddningskoden och URL-adressen från skärmen.
   ![bädda in kod och URL](assets/font-add-url.png)

6. Klicka **Klar** för att stänga webbprojektfönstret.
7. Logga in i AEM och gå till URL `http://server:port/crx/de/index.jsp#`
8. Skapa en mappstruktur i CRXDE, till exempel `/apps/[fontslibrary]/[customlibrary(clientlibrary)]`.
9. Gå till den nyskapade `clientlibs` mapp och lägg till `allowProxy` och `categories` egenskaper.
10. Navigera till `/apps/[fontslibrary]/[customlibrary(clientlibrary)]` och skapa en css-mapp.
11. Gå till den skapade CSS-mappen och skapa en fil. Skapa till exempel en fil som `fonts.css` och klistra in inbäddningskoden tillsammans med URL:en.
   ![Mappstruktur](/help/forms/using/assets/fonts-add-in-crxde.png)
12. Spara ändringarna.

>[!NOTE]
>
> Om du vill använda de tillagda anpassade teckensnitten i ett adaptivt formulär måste du se till att klientbibliotekets namn finns i **[!UICONTROL Client Library Category]** justerar med det namn som anges i kategorialternativet i mappen clientlib.

De medföljande teckensnitten är nu tillgängliga för det adaptiva formuläret via följande anpassade teckensnittsklientbibliotek.


<!--
Create Adobe Fonts Configuration

1. To create a API Token, go to **login** > **API Token** > **Make me a new API token**.

   ![API token](/help/forms/using/assets/fonts-api-token.png)

2. Once, you click **Make me a new API token**, a new token is generated. 
3. Copy the generated token for future use.
4. Now login to your AEM  author instance. On the author instance, go to **[!UICONTROL Tools]**>**[!UICONTROL Cloud Services]**> **[!UICONTROL Adobe Fonts]**.
5. Select the configuration container and click **Create**. **[UICONTROL Create Adobe Fonts Configuration]** screen appears.
    ![API token](/help/forms/using/adobe-font-configuration-screen.png)

6. Spceify the name and paste the API token in the **[!UICONTROL Kit ID]** textbox.
7. Click **Create**.



The fonts added to the **[!UICONTROL Adobe Fonts]** are available for selection in the **[!UICONTROL Text]** accordion of all the components.
1. In the theme editor, navigate to **[!UICONTROL Theme Options]** ![theme-options](assets/theme-options.png) > **[!UICONTROL Configure]**. 
2. In the **[!UICONTROL Adobe Fonts Configuration]** field, select the kit, and click **[!UICONTROL Save]**.


1. Create an [Adobe Fonts](https://fonts.adobe.com/?ref=tk.com) account, create a kit, add font Myriad Pro to the kit, publish the kit, and obtain the Kit ID. It is required to use [!DNL Adobe Fonts] (Web Fonts) in an adaptive form. 
1. In the AEM [!DNL Forms] Server, navigate to ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**. Now, open a configuration folder. If a configuration is already available, click the **[!UICONTROL Create]** button to create an instance.

   On the Create Configuration dialog, specify a **Title** for the configuration, and click **[!UICONTROL Create]**. You are redirected to the configuration page. In the [!UICONTROL Edit Component] dialog that appears, provide your **Kit ID** and click **[!UICONTROL OK]**. -->


