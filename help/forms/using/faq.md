---
title: Vanliga frågor och svar om HTML5-formulär
seo-title: Vanliga frågor och svar om HTML5-formulär
description: Vanliga frågor och svar om layout, skriptstöd och omfång för HTML5-formulär.
seo-description: Vanliga frågor och svar om layout, skriptstöd och omfång för HTML5-formulär.
uuid: 398e31de-3e46-4288-b3cd-39d51fa17abc
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4b676e7e-191f-4a19-8b8f-fc3e30244b59
docset: aem65
translation-type: tm+mt
source-git-commit: 19299fb5fc764d0e71c0ea3a5ec2286183dd6861

---


# Vanliga frågor och svar om HTML5-formulär{#frequently-asked-questions-faq-for-html-forms}

Det finns några vanliga frågor (FAQ) om layout, skriptstöd och omfång för HTML5-formulär.

## Layout {#layout}

1. Varför visas inte streckkoder och signaturfält i mitt formulär?

   Svar: Streckkoder och signaturfält är inte relevanta i HTML- och mobilscenarier. Dessa fält visas som icke-interaktiva områden. Men AEM Forms Designer har ett nytt signaturskriptfält som kan användas istället för signaturfält. Du kan också lägga till en [anpassad widget](../../forms/using/custom-widgets.md) för streckkoder och integrera den.

1. Stöds RTF för XFA-textfältet?

   Svar: XFA-fältet, som tillåter avancerat innehåll i AEM Forms Designer, stöds inte och återges som normal text utan stöd för formatering av texten från användargränssnittet. Dessutom visas XFA-fält med kombinationsegenskaper som ett vanligt fält, även om det fortfarande finns begränsningar för antalet tillåtna tecken baserat på värdet för kombinationssiffror.

1. Finns det några begränsningar för användning av repeterbara delformulär?

   Svar: Upprepningsbara delformulär ska ha ett initialt antal på 1 eller fler. Upprepningsbara delformulär med ett ursprungligt värde på noll stöds inte. Du kan också välja att använda ett repeterbart delformulär och inte visa det när formuläret läses in. Så här uppnår du användningsfallet:

   1. Ange startvärdet för det repeterbara delformuläret till 1.

      ![inledande räkning](assets/intial-count.png)

   1. Använd händelsen initialize för formuläret för att dölja den primära instansen av delformuläret. Koden nedan döljer till exempel den primära instansen av delformuläret vid formulärinitiering. Den verifierar också apptypen för att säkerställa att skriptet bara körs på klientsidan:

      ```
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. Öppna skriptet för att lägga till en instans av delformuläret för redigering. Lägg till koden som nedan för att lägga till en instans av delformulärsskriptet.

      Koden nedan kontrollerar den dolda instansen av delformuläret. Om den dolda instansen av delformuläret hittas tar du bort den dolda instansen av delformuläret och infogar en ny instans av delformuläret. Om den dolda instansen av delformuläret inte hittas infogar du bara en ny instans av delformuläret.

      ```
      if (RepeatSubform.presence == "hidden")
      {
      RepeatSubform.instanceManager.insertInstance(0);
      RepeatSubform.instanceManager.removeInstance(1);
      }
      else
      {
      RepeatSubform.instanceManager.addInstance(1);
      }
      ```

   1. Öppna skriptet för att ta bort en instans av delformuläret för redigering. Lägg till koden så här för att ta bort en instans av skriptet Delformulär.

      Antal kodkontroller för delformulären. Om antalet delformulär är 1 döljs delformuläret i stället för att delformuläret tas bort.

      ```
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. Öppna händelsen för att skicka formuläret i förväg för redigering. Lägg till följande skript i händelsen för att ta bort den dolda instansen av skriptet innan du redigerar. Det förhindrar att data i det dolda delformuläret skickas in.

      ```
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. Finns det några begränsningar när det gäller att använda dolda delformulär?

   Svar: Ett dolt delformulär med komplex hierarki som delas upp på flera sidor orsakar layoutproblem. Du kan komma runt problemet genom att markera delformuläret som synligt från början och sedan dölja det i ett initieringsskript baserat på viss logik eller data.

1. Varför viss text trunkeras eller visas felaktigt i HTML5?

   Svar: Om ett Draw- eller Caption-textelement inte har fått tillräckligt med utrymme för att visa innehåll, visas texten som trunkerad i mobil formuläråtergivning. Den här trunkeringen visas också i designvyn i AEM Forms Designer. Även om den här trunkeringen kan hanteras i PDF-filer kan den inte hanteras i HTML5-formulär. Du kan undvika problemet genom att ange tillräckligt med utrymme för att rita eller bildtext så att den inte kortas av i designläget i AEM Forms Designer.

1. Jag observerar layoutproblem med saknat innehåll eller överlappande innehåll. Vad är orsaken?

   Svar: Om det finns ett element av typen Rita text eller Rita bild tillsammans med ett annat överlappande element på samma plats (till exempel en rektangel), visas inte innehållet i Rita text om det kommer senare i dokumentordningen (i hierarkivyn i AEM Forms Designer). PDF har stöd för genomskinliga lager, men HTML/webbläsare har inte stöd för genomskinliga lager.

1. Varför visas vissa teckensnitt i HTML-formuläret på ett annat sätt än de som används när formuläret utformas?

   Svar: HTML5-formulär bäddar inte in teckensnitt (till skillnad från PDF-formulär där teckensnitt är inbäddade i formuläret). För att HTML-versionen av formuläret ska kunna återges som förväntat måste teckensnitten som anges i XDP-filen vara tillgängliga på servern och på klientdatorn. Om de nödvändiga teckensnitten inte finns på servern används de som standard. Om du dessutom använder teckensnitt i formulärmallen som inte finns på klientenheten, används webbläsarens standardteckensnitt för att återge texten.

1. Stöds vAlign- och hAlign-attribut i HTML-formulär?

   Ja, attributen vAlign och hAlign stöds. Attributet vAlign stöds inte i Internet Explorer och i flerradsfält.

1. Har HTML5-formulär stöd för hebreiska tecken?

   HTML5-formulär har stöd för hebreiska tecken i alla webbläsare utom Microsoft Internet Explorer.

1. Har HTML5-formulär några begränsningar för numeriska fält?

   Svar: Ja, HTML5-formulär har några begränsningar. Om antalet siffror är fler än antalet som anges i bildsatsen, lokaliseras inte siffrorna och visas på engelska.

1. Varför är HTML-formulär större än PDF-formulär?

   Det krävs många mellanliggande datastrukturer och objekt som formulärdom, datatilldom och layoutdom för att återge en XDP till ett HTML-formulär.

   För PDF-formulär har Adobe Acrobat en inbyggd XTG-motor för att skapa mellanliggande datastrukturer och objekt. Acrobat hanterar också layout och skript.

   För HTML5-formulär har webbläsarna ingen inbyggd XTG-motor för att skapa mellanliggande datastrukturer och objekt från rå XDP-byte. För HTML5-formulär genereras därför mellanliggande strukturer på servern och skickas till klienten. På klienten använder javascript-baserade skript- och layoutmotorer dessa mellanliggande strukturer.

   Storleken på den mellanliggande strukturen beror på storleken på den ursprungliga XDP-filen och de data som sammanfogas med XDP-filen.

1. Finns det några begränsningar när det gäller att använda tabeller i min xdp?

   Svar: Komplexa tabeller orsakar problem vid återgivning.

   * Avsnitt (SubformSet) inuti en tabell stöds inte.
   * Tabellhuvuds- och sidfotsrader i vissa tabeller markeras för upprepning. Att dela upp sådana tabeller på flera sidor kan få vissa problem.

1. Har tillgängliga tabeller några begränsningar?

   Svar: Ja, tillgängliga tabeller har följande begränsningar:

   * Kapslade tabeller och delformulär i en tabell stöds inte.
   * Rubriker stöds bara för tabellens övre och vänstra kolumner. Huvuden stöds inte för element i mellantabeller. Du kan använda rubriker på flera rad- och kolumnrubriker, förutsatt att alla sådana rader och kolumner finns tillsammans med den översta raden eller kolumnen längst till vänster i tabellen.
   * `Rowspan`och `colspan`från en slumpmässig plats i tabellen stöds inte.

   * Du kan inte lägga till eller ta bort instanser av rader som innehåller element med ett radintervallvärde som är större än 1.

1. Vilken läsordning har skärmläsare verktygstips och bildtexter?

   * När både bildtext och verktygstips finns, läses den enda bildtexten. Om bildtexten inte är tillgänglig läses funktionsbeskrivningen. Du kan också ange prioritet för läsning i en XDP-fil med hjälp av formulärdesignern
   * När du håller muspekaren över ett element visas verktygstipset. Om funktionsbeskrivningen inte är tillgänglig visas taltext. Om taltext inte är tillgänglig visas fältnamnet.

1. När du håller pekaren över ett fält visas ett verktygstips. Hur inaktiverar man det?

   Om du vill inaktivera verktygstipset vid hovring väljer du ingen på hjälpmedelspanelen i Designer.

1. I Designer kan en användare konfigurera anpassade utseendeegenskaper för alternativknappar och kryssrutor. Tar HTML5-formulär hänsyn till anpassade utseendeegenskaper när formulären återges?

   Svar: HTML5-formulär ignorerar de anpassade utseendeegenskaperna för alternativknappar och kryssrutor. Alternativknapparna och kryssrutorna visas enligt specifikationerna för den underliggande webbläsaren.

1. När ett HTML5-formulär öppnas i en webbläsare som stöds justeras inte kanten på de fält som placeras intill korrekt, eller så visas delformulär som överlappande. När samma HTML5-formulär förhandsgranskas i Forms Designer visas inte fälten och layouten feljusterade och delformulären visas på rätt plats. Hur löser jag problemet?

   När ett delformulär är inställt på att flöda innehåll och delformuläret har ett dolt ramelement, justeras inte kanten på de fält som placeras inåt korrekt eller så visas delformulär som överlappande. Du kan lösa problemet genom att ta bort eller kommentera dolda &lt;border>-element från motsvarande XDP. Följande &lt;border>-element markeras som en kommentar:

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. Varför fungerar inte skärmläsare korrekt med fältobjektet Datum/tid?

   Skärmläsare stöder inte datum-/tidsfält. Du kan dock manuellt ange datum/tid för fältet så att skärmläsaren läser det. Använd verktygstips eller skärmläsartext för att instruera användaren att manuellt välja datum/tid för fältet.

### Skript {#scripting}

1. Finns det några begränsningar i JavaScript-implementeringen för HTML-formulär?

   Svar:

   * Stödet för xfa.connectionSet-skriptet är begränsat. För connectionSet stöds endast anrop på serversidan av webbtjänsten. Mer information finns i [Skriptstöd](/help/forms/using/scripting-support.md).
   * Det finns inget stöd för $record och $data i klientskript. Men om skripten skrivs i ett formReady, layoutReady-block fungerar skripten fortfarande eftersom dessa händelser körs på serversidan.
   * XFA Draw-elementspecifika skript som ändring av Draw-texten (eller bildtext i fälten) stöds inte.

1. Finns det några begränsningar för att använda FormCalc?

   Svar: Endast en delmängd av formCalc-skripten är för närvarande implementerade. Mer information finns i [Skriptstöd](/help/forms/using/scripting-support.md).

1. Finns det någon rekommenderad namnkonvention och finns det några reserverade nyckelord att undvika?

   * I AEM Forms Designer rekommenderar vi att du inte börjar namnet på ett objekt (till exempel ett delformulär eller ett textfält) med ett understreck (_). Om du vill använda understreck i början av namnet lägger du till ett prefix efter understrecket _&lt;prefix>&lt;objectname>.
   *  Alla HTML5-formulär-API:er är reserverade nyckelord. Använd ett namn som inte är identiskt med API:erna för [HTML5-formulär för anpassade API:er](/help/forms/using/scripting-support.md).

1. Har HTML5-formulär stöd för flytande fält?

   Ja, HTML5-formulär har stöd för flytande fält. Om du vill aktivera flytande fält lägger du till följande egenskap i återgivningsprofilen:

   >[!NOTE]
   >
   >Som standard är fälten inte aktiverade för flytande. Du kan använda Forms Designer för att ange den flytande egenskapen för fälten.

   1. Öppna CRXde lite och navigera till `/content/xfaforms/profiles/default` noden.
   1. Lägg till en egenskap `mfDataDependentFloatingField`av typen String och ställ in värdet för egenskapen på `true`.
   1. Klicka på **Spara alla**. Nu aktiveras de flytande fälten för HTML-formulären med den uppdaterade återgivningsprofilen.

      >[!NOTE]
      >
      >Om du vill aktivera flytande fält för ett visst formulär utan att uppdatera återgivningsprofilen skickar du egenskapen mfDataDependentFloatingField=true som en URL-parameter.

1. Körs initieringsskriptet och formulärready-händelsen flera gånger i HTML5-formulär?

   Ja, initieringsskripten och formulärfärdiga händelser körs flera gånger, minst en gång på servern och en gång på klientsidan. Det rekommenderas att skriva skript som initialize eller form:ready-händelser baserat på viss affärslogik (formulär- eller fältdata) så att åtgärden utförs baserat på data och idempotent (om data är samma).

### Utforma XDP {#designing-xdp}

1. Finns det några reserverade nyckelord i HTML5-formulär?

   Svar: Alla HTML5-formulär-API:er är reserverade nyckelord. Använd ett namn som inte är identiskt med API:erna för [HTML5-formulär för anpassade API:er](/help/forms/using/scripting-support.md). Förutom reserverade nyckelord bör du lägga till ett unikt prefix efter understrecket om du använder objektnamn som börjar med ett understreck (_). Genom att lägga till ett prefix undviker du eventuella konflikter med interna API:er för HTML5-formulär. Exempel, `_fpField1`

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
