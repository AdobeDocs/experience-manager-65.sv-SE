---
title: 'Formatera ditt anpassningsbara formulär '
seo-title: 'Formatera ditt anpassningsbara formulär '
description: 'Lär dig skapa ett anpassat tema, formatera enskilda komponenter och använda webbteckensnitt i ett tema '
seo-description: 'Lär dig skapa ett anpassat tema, formatera enskilda komponenter och använda webbteckensnitt i ett tema '
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
translation-type: tm+mt
source-git-commit: b2fd6e0412ee0dacf7b68f4a0b219804dd4a6150

---


# Formatera ditt anpassningsbara formulär {#do-not-publish-style-your-adaptive-form}

Lär dig skapa ett anpassat tema, formatera enskilda komponenter och använda webbteckensnitt i ett tema

![](do-not-localize/08-style_your_adaptiveformmain.png)

Den här självstudiekursen är ett steg i serien [Create Your First Adaptive Form](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) . Vi rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga exemplet på självstudiekurser.

## Om självstudiekursen {#about-the-tutorial}

Du kan använda teman för att ge ett anpassat formulär ett unikt utseende och en unik stil. Du kan använda färdiga teman som medföljer redigeringsprogrammet för anpassade formulär eller skapa egna teman. I AEM Forms finns en [temaredigerare](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html) för att skapa anpassade teman. Ett och samma tema kan ge olika utseenden till samma adaptiva formulär som öppnas på mobilen, surfplattan eller datorn. Du behöver inte ha någon tidigare kunskap om CSS eller LESS för att kunna använda temaredigeraren, men du vill ha den.

I slutet av självstudiekursen kommer du att lära dig att:

* Använda ett tema i ett anpassat formulär
* Skapa ett tema för anpassningsbara formulär med temaredigeraren
* Formatera enskilda komponenter
* Bonusavsnitt: Använda webbteckensnitt i ett anpassat tema

Formuläret ser ut ungefär så här när du är klar med självstudiekursen:

![Formulär med anpassat tema](assets/styled-adaptive-form.png)

## Innan du startar {#before-you-start}

Ladda ned rubrikbilderna och logotypbilderna nedan på din dator. Rubriken på det `shipping-address-add-update-form` adaptiva formuläret använder rubrikbilderna och logotypbilderna. Bilden i sidhuvudsstil visas till höger om sidhuvudet.

[Hämta fil](assets/header-style.png)

[Hämta fil](assets/logo-1.png)

## Steg 1: Använd ett tema i det anpassade formuläret {#step-apply-a-theme-to-your-adaptive-form}

Adaptiv formulärredigerare har flera färdiga teman. Om du inte tänker använda en anpassad stil för ditt adaptiva formulär kan du även publicera dina adaptiva formulär med ett användbart tema. Temana är oberoende av anpassningsbara formulär. Du kan använda samma tema för flera adaptiva formulär. Så här använder du ett tema i ett anpassat formulär:

1. Öppna det adaptiva formuläret för redigering.

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. Öppna egenskaper för behållaren för **adaptivt formulär**. Navigera till **Grundläggande** > **Adaptivt formulärtema** i egenskapswebbläsaren. I fältet **Adaptivt** formulärtema visas alla färdiga och anpassade teman. Som standard används Canvas-temat.
1. Välj ett tema i fältet **Adaptivt** formulärtema. Exempel: **Undersökningsämne**. Tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) för att använda det valda temat.

![Adaptiv form med standardtemat](assets/default-adaptive-form.png)

**** Bild: Anpassa form *med standardtemat*

![Adaptiv form med undersökningstemat](assets/adaptive-form-with-survey-theme.png)

**** Bild: *Adaptiv form med Undersökningstemat*

## Steg 2: Uppdatera ditt anpassningsbara formulär {#step-update-your-adaptive-form}

Den design som visas ovan kräver ändringar i platshållartext och logotyp i ditt befintliga adaptiva formulär. Utför följande steg för att göra de ändringar som krävs:

1. Ändra den befintliga logotypen och texten för sidhuvudet. Så här tar du bort logotypen:

   1. Öppna formuläret i formulärredigeraren.

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. Tryck på logotypbilden i rubrikkomponenten och tryck på ![cmpr](assets/cmppr.png) -egenskaper. Tryck på X i egenskapen image för att ta bort den befintliga logotypbilden.
   1. Tryck på upload, välj logo.png och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) för att spara ändringarna. Bilden hämtades i avsnittet [Innan du började](/help/forms/using/style-your-adaptive-form.md#before-you-start) .
   1. Tryck på rubriktext `We.Retail`och tryck på ![aem_6_3_edit](assets/aem_6_3_edit.png) **edit**. Ändra rubriktext till `we retail`. Använd endast fet stil `we`i `we retail`.
   ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. Ta bort rubrik och lägg till platshållartext:

   1. Tryck på fältet Kund-ID och tryck på ![cmpr](assets/cmppr.png) -egenskaper.
   1. Kopiera innehållet i **titelfältet** till **platshållartextfältet** .
   1. Ta bort innehållet i fältet **Titel** och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
   1. Upprepa de tre föregående stegen för alla textrutor, numeriska rutor och e-postfält i formuläret.
   ![updated-adaptive-form](assets/updated-adaptive-form.png)

## Steg 3: Skapa ett anpassat tema för ditt anpassade formulär {#step-create-a-custom-theme-for-your-adaptive-form}

Du kan använda [temaredigeraren](/help/forms/using/themes.md) för att skapa anpassade teman. Temats redigerare är en kraftfull WYSIWYG-redigerare. Det är en visuell metod att använda CSS på olika komponenter i ett adaptivt formulär. Den ger finare kontroller för att formatera komponenter och paneler i ett adaptivt formulär.

Ett tema är en separat enhet som anpassningsbara formulär. Den innehåller format (CSS) för komponenterna och panelerna i ett anpassat formulär. Formaten innehåller CSS-egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet, justering och storlek. När du använder ett tema används det angivna formatet på motsvarande komponenter i ett anpassat formulär.

I den här självstudiekursen kommer du att formatera sidhuvud och sidfot, text och numeriska komponenter, bilagekomponenter och knappar. Låt oss börja med att skapa ett tema:

### Skapa ett tema {#create-a-theme}

1. Logga in på AEM-författarinstansen och gå till **Adobe Experience Manager** > **Formulär** > **Teman**. Standardwebbadressen är [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes).
1. Tryck på **[!UICONTROL Skapa]** och välj **[!UICONTROL tema]**. Sidan Skapa tema med de fält som krävs för att skapa ett tema visas. Fälten Titel och Namn är obligatoriska:

   * **** Titel: Ange en titel på temat. Exempel: **Globalt tema.** Titeln hjälper dig att identifiera temat från listan med teman.
   * **** Namn: Ange namnet på temat. Exempel: **Global-Theme.** En nod med det angivna namnet skapas i databasen. När du börjar skriva en titel genereras värdet för namnfältet automatiskt. Du kan ändra det föreslagna värdet. Namnfältet får endast innehålla alfanumeriska tecken, bindestreck och understreck. Alla ogiltiga indata ersätts med ett bindestreck.

1. Tryck på **Skapa**. Ett tema skapas och en dialogruta visas där du kan öppna formuläret för redigering. Tryck på **Öppna** för att öppna det nya temat på en ny flik. Temat öppnas i temaredigeraren. För formatering används ett anpassat formulär som levereras med AEM Forms.

   Mer information om hur du använder temaredigeringsgränssnittet finns i [Om temaredigeraren](/help/forms/using/themes.md#aboutthethemeeditor).

1. Tryck på **Temaalternativ** för ![tema >](assets/theme-options.png) **Konfigurera**. I fältet **Förhandsgranska formulär** väljer du det adaptiva formuläret **shipping-address-add-update-form** , trycker på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)och trycker på **Save**. Nu är temaredigeraren konfigurerad att använda ditt eget adaptiva formulär i stället för det adaptiva standardformatet. Tryck på **Avbryt** för att återgå till temaredigeraren.

   ![anpassat tema](assets/custom-theme.png)

   **** Bild: Redigera *teman med anpassningsbara formulär för leverans-adress-add-update-form*

   ![create-a-theme](assets/create-a-theme.png)

   **** Bild: Anpassningsbart *formulär med standardformuläret*

### Formatera sidhuvud och sidfot {#style-header-and-footer}

Sidhuvud och sidfot ger ett konsekvent och distinkt utseende i en adaptiv form. I allmänhet innehåller sidhuvudet organisationens logotyp och namn, sidfoten innehåller copyrightinformation och dessa är identiska i flera former av en organisation. Gör så här för att formatera sidhuvud och sidfot i anpassat formulär för leverans-address-add-update:

1. Navigera till alternativet **Sidhuvud** > **Text** på panelen Väljare. Väljarpanelen är till vänster om temaredigeraren. Om panelen inte visas trycker du på ![](https://helpx.adobe.com/content/dam/help/en/aem-forms/6-2/toggle-side-panel.png) Växla sidopanel.

1. Ange följande egenskaper i dragspelet **Text** och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Egenskap | Värde |
   |---|---|
   | Teckensnittsfamilj | Arial |
   | Teckenfärg | FFFFFF |
   | Teckenstorlek | 54px |

1. Tryck på sidhuvudswidgeten och tryck på **Sidhuvud**. Alternativen för att formatera sidhuvudswidgeten visas till vänster. Expandera dragspelsfliken **Dimensioner och position** , ställ in **Höjd** på `120px`och tryck sedan på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. Expandera bakgrundsdragspelet i sidwidgeten och ange **bakgrundsfärgen** till `F6921E.`

   Håll muspekaren över **Bild och övertoning** > **+ Lägg** till och tryck på **Bild**. Ange följande egenskaper och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Egenskap | Värde |
   |---|---|
   | image | Överför header-style.png. Bilden hämtades i avsnittet [Innan du började](/help/forms/using/style-your-adaptive-form.md#before-you-start) . |
   | Position | Höger nerifrån |
   | Passram | Ingen upprepning |

1. Tryck på logotypen i sidhuvudet i temaredigeraren och tryck på **rubriklogotypen**. Expandera dragspelet Dimensioner och position, ange följande egenskaper och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

<table> 
 <tbody> 
  <tr> 
   <td>Marginal</td> 
   <td>Värde</td> 
  </tr> 
  <tr> 
   <td>Marginal</td> 
   <td> 
    <ul> 
     <li>Överkant: 1,5 rem</li> 
     <li>Underkant: -35px</li> 
     <li>Vänster: 1rem<strong><br /></strong></li> 
    </ul> <p><strong></strong> Tips: Tryck på <img src="assets/link.png"> länkikonen för att ange olika värden för varje fält.<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Höjd</td> 
   <td>4.75rem</td> 
  </tr> 
 </tbody> 
</table>

1. Tryck på sidfotswidgeten och tryck på **Sidfot**. Expandera **bakgrundsfärg** , ställ in **bakgrundsfärg** på `F6921E`och tryck sedan på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

### Formatera datainhämtningskomponenten och använd en bakgrund i det anpassade formuläret {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

Du kan använda flera komponenter i ett adaptivt formulär för att hämta data. Till exempel textruta och numerisk ruta. Du kan ange identiska format för alla datainhämtningskomponenter eller separata format för varje komponent. I den här självstudiekursen används ett identiskt format för numeriska rutor (Kund-ID, Postnummer) och textrutor (Kund-ID, Namn, Leveransadress, Tillstånd, E-post). Så här formaterar du komponenter för datainhämtning:

1. Tryck på fältet Kund-ID och tryck på alternativet **Fältwidget** . Ange följande egenskaper och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

<table> 
 <tbody> 
  <tr> 
   <td>Dragspel</td> 
   <td>Egenskap</td> 
   <td>Värde</td> 
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
   <td>Mått och position</td> 
   <td>Bredd</td> 
   <td>60%</td> 
  </tr> 
  <tr> 
   <td>Mått och position</td> 
   <td>Marginal</td> 
   <td> 
    <ul> 
     <li>Vänster: 10rem</li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

1. Tryck på det tomma området ovanför fältet Kund-ID och tryck på **responsiv panelbehållare**. Ställ in F1F2F2 som **Bakgrund** > **Bakgrundsfärg** . Tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   ![](do-not-localize/responsive-panel-container.png)

### Formatera knapparna {#style-the-buttons}

Du kan använda ett anpassat tema för att tillämpa ett identiskt format på alla knappar i det adaptiva formuläret och [textbundna format](/help/forms/using/inline-style-adaptive-forms.md) för att tillämpa ett format på en viss knapp. Så här formaterar du knapparna:

1. Tryck på knappen **Skicka** och tryck på **knappen** . Ange följande egenskaper och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

<table> 
 <tbody> 
  <tr> 
   <td>Dragspel</td> 
   <td>Egenskap</td> 
   <td>Värde</td> 
  </tr> 
  <tr> 
   <td>Bakgrund</td> 
   <td>Bakgrundsfärg</td> 
   <td>F6921E</td> 
  </tr> 
  <tr> 
   <td>Border<br /> </td> 
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
1. Välj alternativet **Format** i det övre fältet.

   ![style-option](assets/style-option.png)

1. Tryck på knappen **Bifoga** och tryck på ![aem_6_3_](assets/aem_6_3_edit.png)editicon. Ange följande egenskaper i dragspelet **Dimensioner och position** :

   | Egenskap | Värde |
   |---|---|
   | Flyttal | Vänster |
   | Bredd | 10% |

1. Tryck på alternativet **Government approved address proof** (Godkänt av myndigheter) och tryck på ![aem_6_3_](assets/aem_6_3_edit.png)editicon. Ange följande egenskaper:

<table> 
 <tbody> 
  <tr> 
   <td>Dragspel</td> 
   <td>Egenskap</td> 
   <td>Värde</td> 
  </tr> 
  <tr> 
   <td>Mått och position</td> 
   <td>Flyttal</td> 
   <td>Vänster</td> 
  </tr> 
  <tr> 
   <td>Mått och position</td> 
   <td>Bredd</td> 
   <td>73%</td> 
  </tr> 
  <tr> 
   <td>Mått och position</td> 
   <td>Utfyllnad</td> 
   <td> 
    <ul> 
     <li>Vänster: 10px</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Mått och position</td> 
   <td>Höjd</td> 
   <td>40px</td> 
  </tr> 
  <tr> 
   <td>Mått och position<br /> </td> 
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
 </tbody> 
</table>

1. Tryck på **Skicka** -knappen och tryck på ![aem_6_3_edit](assets/aem_6_3_edit.png) -ikonen. Ange följande egenskaper:

<table> 
 <tbody> 
  <tr> 
   <td>Dragspel</td> 
   <td>Egenskap</td> 
   <td>Värde</td> 
  </tr> 
  <tr> 
   <td>Mått och position</td> 
   <td>Flyttal</td> 
   <td>Höger</td> 
  </tr> 
  <tr> 
   <td>Mått och position</td> 
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

## Steg 5:Bonusavsnitt: Använda webbteckensnitt i ett anpassat tema {#step-bonus-section-using-web-fonts-in-a-custom-theme}

Du kan använda olika teckensnitt för att utforma ett anpassat formulär. Alla enheter som det adaptiva formuläret visas på kanske inte har de teckensnitt som används för att utforma det adaptiva formuläret. Du kan använda en webbteckensnittstjänst för att leverera nödvändiga teckensnitt till målenheten.

Adobe Typekit är en webbteckensnittstjänst. Du kan konfigurera och använda tjänsten med adaptiva formulär. Så här använder du Adobe Typekit i en adaptiv form:

>[!NOTE]
>
>![Typekit-to-adobe-fonts](assets/typekit-to-adobe-fonts.png) heter nu Adobe Fonts och ingår i Creative Cloud och andra prenumerationer. [Läs mer](https://fonts.adobe.com/).

1. Skapa ett [Adobe Typekit](https://typekit.com/) -konto, skapa ett kit, lägg till teckensnittet Myriad Pro i paketet, publicera paketet och få ditt Kit-ID. Du måste använda Adobe Typekit-teckensnitt (webbteckensnitt) i en anpassningsbar form.
1. Navigera till ![adobeexperienceManager](assets/adobeexperiencemanager.png) **Adobe Experience Manager** > **Tools** ![hammer](assets/hammer.png) > **Deployment** ****> Cloud Services på AEM Forms-servern. På sidan Cloud Services går du till **Tredjepartstjänster** > **Typekit** och klickar på **Configure** Now under Typekit. Om det redan finns en konfiguration klickar du på plusknappen (+) för att skapa en ny instans.

   I dialogrutan Skapa konfiguration anger du en **rubrik** för konfigurationen och klickar på **Skapa**. Du omdirigeras till konfigurationssidan. Ange ditt **kit-ID** i dialogrutan Redigera komponent som visas och klicka på **OK**.

1. Konfigurera temat så att det använder TypeKit-konfigurationen. Öppna **Global Theme** i temaredigeraren på författarinstansen. Gå till Temaalternativ ![för temaalternativ](assets/theme-options.png) > Konfigurera i temaredigeraren. Markera paketet i **fältet Typekit-konfiguration** och klicka på **Spara**.

   De teckensnitt som läggs till i Typekit kan väljas i **textdragspelsfönstret** för alla komponenter.

