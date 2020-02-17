---
title: Skapa eller konfigurera en bevakad mapp
seo-title: Skapa eller konfigurera en bevakad mapp
description: Lär dig hur du skapar eller tar bort en bevakad mapp eller ändrar egenskaperna för en befintlig bevakad mapp.
seo-description: Lär dig hur du skapar eller tar bort en bevakad mapp eller ändrar egenskaperna för en befintlig bevakad mapp.
uuid: 659d4d8c-99b8-40dd-b884-bfee4d476fe1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 0ce7b338-6686-49b3-b58b-e7ab6b670708
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30

---


# Skapa eller konfigurera en bevakad mapp {#create-or-configure-a-watched-folder}

En administratör kan konfigurera en nätverksmapp, en så kallad *bevakad mapp*, så att när en användare placerar en fil (till exempel en PDF-fil) i den bevakade mappen, startas en förkonfigurerad åtgärd och filen ändras. När den angivna åtgärden har utförts sparas den ändrade filen i en angiven utdatamapp. Mer information om hur du administrerar en bevakad mapp finns i [Administrationshjälp](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

Du kan använda användargränssnittet för bevakad mapp för att:

* Skapa en bevakad mapp
* Ändra egenskaper för en befintlig bevakad mapp
* Ta bort en bevakad mapp

## Skapa en bevakad mapp {#create-a-watched-folder}

Innan du konfigurerar en bevakad mapp bör du kontrollera följande:

* Bevakade mappar är en avancerad funktion i AEM-formulär. AEM-formulärtilläggspaket krävs för att funktionen ska fungera. Kontrollera att lämpligt AEM Forms-tilläggspaket är installerat och konfigurerat.
* Du kan skapa den bevakade mappen i en delad eller lokal lagringsplats. Se till att AEM-formuläranvändare som är konfigurerade att köra den bevakade mappen har läs- och skrivbehörigheter i den bevakade mappen.
* Du kan använda en tjänst, ett arbetsflöde eller ett skript för att automatisera en åtgärd med bevakad mapp. Kontrollera att motsvarande tjänst, arbetsflöde eller skript har skapats och är redo att köras. Mer information om hur du skapar en tjänst, ett arbetsflöde och ett skript finns i [Olika metoder för att bearbeta filer](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files).
* En bevakad mapp har olika egenskaper, se Egenskaper för [bevakad mapp](/help/forms/using/watched-folder-in-aem-forms.md#main-pars-header-1).

Så här skapar du en bevakad mapp:

1. Tryck på **Adobe Experience Manager** -ikonen i skärmens övre vänstra hörn.
1. Tryck på **Verktyg** > **Formulär** > **Konfigurera bevakad mapp.** En lista över redan konfigurerade bevakade mappar visas.
1. Tryck på **Nytt**. En lista över fält som krävs för att skapa den bevakade mappen visas:

   * **Namn**: Identifierar den bevakade mappen. Använd bara alfanumeriska tecken som namn.
   * **Sökväg**: Anger platsen för bevakad mapp. I en klustrad miljö måste den här inställningen peka på en delad nätverksmapp som är tillgänglig för alla användare som kör AEM på olika noder i ett kluster.
   * **Bearbeta filer med**: Den typ av process som ska startas. Du kan ange arbetsflöde, skript eller tjänst.
   * **Tjänstnamn/skriptsökväg/arbetsflödessökväg**: Fältets beteende baseras på det värde som anges för fältet **Bearbeta filer med** . Du kan ange följande värden:

      * Ange arbetsflödesmodellen som ska köras i Arbetsflöde. Till exempel /etc/workflow/models/&lt;arbetsflödes_namn>/jcr:content/model
      * I Skript anger du JCR-sökvägen för skriptet som ska köras. Till exempel /etc/watchfolder/test/testScript.ecma
      * Under Tjänst anger du det filter som används för att hitta en OSGi-tjänst. Tjänsten är registrerad som en implementering av gränssnittet com.adobe.aemfd.watchfolder.service.api.ContentProcessor. Följande kod är till exempel en anpassad implementering av gränssnittet ContentProcessor med en anpassad (foo=bar) egenskap.
   >[!NOTE]
   >
   >Om du har valt **Service** för fältet **Bearbeta filer med** måste värdet för fältet Service Name(inputProcessorType) omslutas av parenteser. Till exempel (foo=bar).

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **Mönster** för utdatafil: Ange en semikolonavgränsad lista (;) med mönster som en bevakad mapp använder för att bestämma namn och plats för utdatafiler och -mappar. Mer information om filmönster finns i [Om filmönster](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).


1. Tryck på **Avancerat**. Den avancerade fliken innehåller fler fält. De flesta av dessa fält innehåller ett standardvärde.

   * **** Nyttolastmappningsfilter: När du skapar en bevakad mapp skapas en mappstruktur i den mapp som bevakas. Mappstrukturen har mapparna stage, result, preserve, input och error. Mappstrukturen kan fungera som indatanyttolast för arbetsflödet och acceptera utdata från ett arbetsflöde. Den kan även visa eventuella felpunkter. Strukturen för en nyttolast skiljer sig från strukturen för en bevakad mapp. Du kan skriva egna skript för att mappa strukturen för en bevakad mapp till nyttolasten. Ett sådant skript kallas nyttolastmappningsfilter. Det finns två körklara implementeringar av nyttolastmappare. Om du inte har [någon anpassad implementering](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter)kan du använda en körklar implementering:

      * **** Standardmappare: Använd standardnyttolastmapparen för att behålla in- och utdatamaterialet för de bevakade mapparna i separata in- och utdatamappar i nyttolasten.
      * **** Enkel filbaserad nyttolastmappare: Använd den enkla filbaserade nyttolastmapparen för att behålla in- och utdatamaterialet direkt i nyttolastmappen. Ingen extra hierarki skapas, som standardmappare.
   * **Körningsläge**: Ange en kommaavgränsad lista över tillåtna körningslägen för arbetsflödeskörning.
   * **Timeout för mellanlagrade filer efter**: Ange hur många sekunder som ska vänta innan en indatafil/indatamapp som redan har hämtats för bearbetning behandlas som att tidsgränsen har överskridits och markerats som ett fel. Timeout-mekanismen aktiveras bara när värdet för den här egenskapen är ett positivt tal.
   * **Ta bort mellanlagrade filer med timeout vid begränsning**: Om det här alternativet är aktiverat aktiveras funktionen **Timeout Stage Files After** (Tid out Stage Files After) bara när strypning är aktiverat för den bevakade mappen.
   * **** Sök igenom indatamapp efter varje: Ange tidsintervallet, i sekunder, för att söka efter indata i den bevakade mappen. Om inte inställningen Gräns är aktiverad ska avsökningsintervallet vara längre än tiden för att bearbeta ett genomsnittligt jobb. annars kan systemet överbelastas. Intervallets värde måste vara större än eller lika med ett.
   * **Exkludera filmönster**: Ange en semikolonavgränsad lista (;) med mönster som en bevakad mapp använder för att avgöra vilka filer och mappar som ska skannas och plockas upp. Alla filer eller mappar med det angivna mönstret skannas inte för bearbetning. Mer information om filmönster finns i [Om filmönster](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Inkludera filmönster**: Ange en semikolonavgränsad lista (;) med mönster som den bevakade mappen använder för att avgöra vilka mappar och filer som ska genomsökas och hämtas. Om till exempel Inkludera filmönster är indata&amp;ast;, alla filer och mappar som matchar indata&amp;ast; plockas upp. Standardvärdet är &amp;ast; och anger alla filer och mappar. Mer information om filmönster finns i [Om filmönster](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **** Väntetid: Ange i millisekunder hur lång tid du vill vänta innan du skannar en mapp eller fil efter att den har skapats. Om väntetiden till exempel är 3 600 000 millisekunder (en timme) och filen skapades för en minut sedan, kommer filen att hämtas efter 59 eller fler minuter. Standardvärdet är 0.

      Den här inställningen är användbar för att säkerställa att allt innehåll i filen eller mappen kopieras till indatamappen. Om du till exempel har en stor fil att bearbeta och det tar tio minuter att hämta filen, ställer du in väntetiden på 10&amp;ast;60 &amp;ast;1000 millisekunder. Det här intervallet förhindrar att den bevakade mappen skannar filen om den inte är tio minuter gammal.

   * **** Ta bort resultat som är äldre än: Ange hur många dagar du vill vänta innan filerna och mapparna som är äldre än det angivna värdet tas bort. Den här inställningen är användbar för att säkerställa att resultatmappen inte blir full. Värdet -1 dagar anger att resultatmappen aldrig ska tas bort. Standardvärdet är -1.
   * **** Namn på resultatmapp: Ange namnet på mappen där resultaten ska lagras. Om resultaten inte visas i den här mappen kontrollerar du felmappen. Skrivskyddade filer bearbetas inte och sparas i felmappen. Du kan använda en absolut eller relativ sökväg med följande filmönster:

      * %F = filnamnsprefix
      * %E = filnamnstillägg
      * %Y = år (full)
      * %y = år (de två sista siffrorna)
      * %M = månad
      * %D = dag i månaden
      * %d = dag på året
      * %H = timme (24-timmars klocka)
      * %h = timme (12-timmars klocka)
      * %m = minut
      * %s = sekund
      * %l = millisekund
      * %R = slumptal (mellan 0 och 9)
      * %P = process- eller jobb-ID
      * Om det till exempel är 2009-08-17 och du anger C:/Test/WF0/error/%Y/%M/%D/%H/ är resultatmappen C:/Test/WF0/error/2009/07/17/20.
      * Om sökvägen inte är absolut men relativ skapas mappen i den bevakade mappen. Standardvärdet är result/%Y/%M/%D/, som är resultatmappen i den bevakade mappen. Mer information om filmönster finns i [Om filmönster](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **** Namn på felmapp: Ange mappen där misslyckade filer sparas. Den här platsen är alltid relativ till den bevakade mappen. Du kan använda filmönster enligt beskrivningen för resultatmappen.
   * **** Bevara mappnamn: Ange den mapp där filerna ska lagras efter att sökningen och hämtningen har slutförts. Sökvägen kan vara en absolut, relativ eller null-katalog. Du kan använda filmönster enligt beskrivningen för resultatmappen. Standardvärdet är preserve/%Y/%M/%D/.
   * **** Batchstorlek: Ange antalet filer eller mappar som ska hämtas per skanning. Den förhindrar att systemet överbelastas. Om du läser in för många filer samtidigt kan det orsaka en krasch. Standardvärdet är 2.

      Om skanningsintervallet är litet genomsöks indatamappen ofta av trådarna. Om filer ofta placeras i den bevakade mappen bör du hålla sökintervallet litet. Om filerna tas bort sällan bör du använda ett större inläsningsintervall så att de andra tjänsterna kan använda trådarna.

   * **** Begränsning på: När det här alternativet är aktiverat begränsas antalet bevakade mappjobb som AEM-formulär bearbetar vid en given tidpunkt. Värdet för Batchstorlek avgör det maximala antalet jobb. For more information, see [throttling](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **Skriv över befintliga filer med liknande namn**: När värdet är True skrivs filerna i resultatmappen och i den bevarade mappen över. Om värdet är Falskt används filer och mappar med ett numeriskt indexsuffix för namnet. Standardvärdet är Falskt.
   * **** Bevara filer vid fel: Om du anger True bevaras indatafilerna om fel uppstår. Standardvärdet är true.
   * **** Inkludera filer med mönster: Ange en semikolonavgränsad lista (;) med mönster som den bevakade mappen använder för att avgöra vilka mappar och filer som ska genomsökas och hämtas. Om till exempel Inkludera filmönster är indata hämtas alla filer och mappar som matchar indata. Mer information finns i [Administrationshjälp](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **** Anropa bevakad mapp asynkront: Identifierar anropstypen som asynkron eller synkron. Standardvärdet är asynkront. Asynkron rekommenderas för långvariga processer, medan synkron rekommenderas för tillfälliga eller kortvariga processer.
   * **** Aktivera bevakad mapp: När det här alternativet är aktiverat aktiveras den bevakade mappen. Standardvärdet är True.



## Ändra egenskaper för en befintlig bevakad mapp {#modify-properties-of-an-existing-watched-folder}

Förutom att ändra namnet på den bevakade mappen kan du ändra alla egenskaper i en befintlig bevakad mapp. Så här ändrar du egenskaper för en bevakad mapp:

1. Tryck på **Adobe Experience Manager** -ikonen längst upp till vänster på skärmen.
1. Tryck på **Verktyg** > **Formulär** > **Konfigurera bevakad mapp.** En lista över redan konfigurerade bevakade mappar visas.
1. Till vänster på skärmen Bevakade mappar markerar du bevakningsmappen och trycker på **Redigera.** En lista över fält som krävs för att skapa den bevakade mappen visas. De fält som visas på fliken **Grundläggande** är obligatoriska. Den avancerade fliken innehåller fler fält. De flesta av dessa fält innehåller ett standardvärde. Du kan ändra dessa egenskaper efter dina behov.
1. När du har ändrat egenskaperna trycker du på **Uppdatera**. De ändrade egenskaperna sparas.

