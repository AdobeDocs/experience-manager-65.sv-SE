---
title: Skapa en anpassad anpassad formulärmall
description: I den här artikeln beskrivs hur du skapar anpassade formulärmallar.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 35b50573-0be8-469d-a1ac-f51b9aaa5fef
source-git-commit: 0aa929021aa724e4ec18d49fea26f8c0b0538bdc
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# Skapa en anpassad anpassad formulärmall{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms har infört dynamiska mallar. Du kan använda AEM Sites mallredigerare för att [skapa eller redigera dynamiska mallar](../../forms/using/template-editor.md). Mallarna som nämns i artikeln nedan är statiska mallar. Dessa är inte tillgängliga i en standardinstallation. [Installera kompatibilitetspaket](../../forms/using/compatibility-package.md) för att få tillgång till mallarna i din miljö.

## Förutsättningar {#prerequisites}

* Förståelse av AEM [Sidmall](/help/sites-authoring/templates.md) och [Adaptiv formulärredigering](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* Förståelse av AEM [Bibliotek på klientsidan](/help/sites-developing/clientlibs.md)

## Adaptiv formulärmall {#adaptive-form-template}

En mall för anpassat formulär är en AEM sidmall med vissa egenskaper och innehållsstruktur som används för att skapa anpassningsbara formulär. Mallen innehåller förkonfigurerade layouter, format och grundläggande innehållsstruktur.

När du har skapat ett formulär återspeglas inte ändringarna i den ursprungliga mallinnehållsstrukturen i formuläret.

## Standardmallar för anpassningsbara formulär {#default-adaptive-form-templates}

AEM QuickStart innehåller följande adaptiva formulärmallar:

* Undersökningsmall: Gör att du kan skapa ett anpassat formulär med hjälp av layouten Responsiv som har flera kolumner konfigurerade. Layouten justeras automatiskt baserat på dimensionerna för de olika skärmar som du vill visa formuläret på.
* Enkel registreringsmall: Gör att du kan skapa ett anpassningsbart formulär i flera steg med hjälp av en guidelayout. I den här layouten kan du ange ett uttryck för stegfärdigställande för varje steg, som valideras innan guiden fortsätter till nästa steg.
* Registreringsmall med flikar: Gör att du kan skapa ett anpassningsbart formulär med flera flikar i en tabbar-till-vänster-layout där du kan besöka flikar i valfri slumpmässig ordning.
* Avancerad registreringsmall: Skapa ett formulär med flera flikar och guider. Den har en tabbar till vänster-layout där du kan gå till flikarna i valfri ordning. Den använder Adobe Document Cloud designtjänster för signering och verifiering.
* Tom mall: Skapa ett formulär utan sidhuvud, sidfot och ursprungligt innehåll. Du kan lägga till komponenter som textrutor, knappar och bilder. Med den tomma mallen kan du skapa ett formulär som du [bädda in AEM webbplatssidor](/help/forms/using/embed-adaptive-form-aem-sites.md).

Mallarna har `sling:resourceType` -egenskapen ställs in på motsvarande sidkomponent. Sidkomponenten återger CQ-sidan med adaptiv formulärbehållare, som i sin tur återger adaptiv form.

I följande tabell räknas associationen mellan mallar och sidkomponenter upp:

<table>
 <tbody>
  <tr>
   <td><p><strong>Mall</strong></p> </td>
   <td><p><strong>Sidkomponent</strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/survey</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/simpleEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenrollment</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advancedRotering</p> </td>
  </tr>
 </tbody>
</table>

## Skapa en adaptiv formulärmall med mallredigeraren {#creating-an-adaptive-form-template-using-template-editor}

Du kan ange strukturen och det ursprungliga innehållet i ett anpassat formulär med mallredigeraren. Du vill till exempel att alla formulärförfattare ska ha få textrutor, navigeringsknappar och en skicka-knapp i ett registreringsformulär. Du kan skapa en mall som författare kan använda för att skapa ett formulär som är konsekvent med andra registreringsformulär. AEM mallredigerare:

* Lägga till sidhuvud- och sidfotskomponenter i ett formulär i strukturlagret
* Ange formulärets ursprungliga innehåll.
* Ange ett tema.
* Ange åtgärder som att skicka, återställa och navigera.

Mer information finns i [Mallredigerare](../../forms/using/template-editor.md).

## Skapa en anpassad formulärmall från CRXDE {#creating-an-adaptive-form-template-from-crxde}

I stället för att använda de tillgängliga mallarna kan du skapa en mall och använda den för att skapa anpassade formulär. Anpassade mallar baseras på olika sidkomponenter som refererar till adaptiva formulärbehållare och sidelement, t.ex. sidhuvud och sidfot.

Du kan skapa de här komponenterna med bassidkomponenten för webbplatsen. Du kan också utöka sidkomponenten i det adaptiva formuläret som finns i rutmallarna.

Utför följande steg för att skapa en anpassad mall, till exempel simpleEnrollmentTemplate.

1. Navigera till CRXDE Lite i redigeringsinstansen.

1. Skapa mappstrukturen för programmet i katalogen /apps. Om programnamnet till exempel är mitt eget skapar du en mapp med det här namnet. Programmappen innehåller vanligtvis komponenter, konfiguration, mallar, src och installationskataloger. I det här exemplet skapar du mapparna för komponenter, konfiguration och mallar.

1. Navigera till mappen /libs/fd/af/templates.
1. Kopiera `simpleEnrollmentTemplate` nod.
1. Navigera till mappen /apps/mycompany/templates. Högerklicka på den och välj **[!UICONTROL Paste]**.
1. Om det behövs byter du namn på mallnoden som du kopierade. Du kan t.ex. byta namn på den som en registreringsmall.

1. Navigera till platsen /apps/mycompany/templates/enrollment-template.

1. Ändra `jcr:title` och `jcr:description` egenskaper för `jcr:content` för att skilja mallen från mallen som du kopierade.

1. The `jcr:content` noden i den ändrade mallen innehåller `guideContainer` och `guideformtitle` -komponenter. `guideContainer` är den behållare som innehåller det adaptiva formuläret. The `guideformtitle` -komponenten visar programnamnet, beskrivningen och så vidare.

   I stället för `guideformtitle`kan du ta med en anpassad komponent eller `parsys` -komponenten. Ta till exempel bort `guideformtitle`och lägga till en anpassad komponent eller `parsys` komponentnod. Se till att `sling:resourceType` -egenskapen för komponenten refererar till komponenten och det är definierat på sidan `component.jsp` -fil.

1. Navigera till platsen /apps/mycompany/templates/enrollment-template/jcr:content.

1. Öppna **[!UICONTROL Properties]** och ändra värdet på `cq:designPath` till /etc/designs/mincompany.

1. Skapa nu en /etc/designs/mycompany-nod för `cq:Page` typ.

## Skapa en adaptiv komponent för formulärsidor {#create-an-adaptive-form-page-component}

Den anpassade mallen har samma format som standardmallen eftersom mallen refererar till sidkomponenten /libs/fd/af/components/page/base. Du kan hitta komponentreferensen som egenskapen `sling:resourceType` definieras på noden /apps/mycompany/templates/enrollment-template/jcr:content. Eftersom basen är en kärnproduktkomponent, ska du inte ändra den här komponenten.

1. Navigera till noden /apps/mycompany/templates/enrollment-template/jcr:content och ändra egenskapens värde `sling:resourceType` till /apps/mycompany/components/page/enrollmentpage
1. Kopiera noden /libs/fd/af/components/page/base till mappen /apps/mycompany/components/page.

1. Byt namn på den kopierade komponenten till `enrollmentpage`.

1. **(Endast om du redan har en innehållssida)** Utför följande steg (a-d) om du har en befintlig `contentpage`-komponent för din webbplats. Om du inte har någon befintlig `contentpage`kan du lämna `resourceSuperType`egenskapen så att den pekar på den körklara bassidan.

   1. För `enrollmentpage` nod, ange egenskapens värde `sling:resourceSuperType` till mincompany/components/page/contentpage. The `contentpage` är bassidkomponenten för -platsen. Andra sidkomponenter kan utöka den. Ta bort skriptfiler under `enrollmentpage`, förutom `head.jsp`, `content.jsp`och `library.jsp`. The `sling:resourceSuperType` -komponent, som `contentpage` i det här fallet innehåller alla sådana skript. Sidhuvuden, inklusive navigeringsfält och sidfötter, ärvs från `contentpage` -komponenten.

   1. Öppna filen `head.jsp`.

      JSP-filen innehåller raden `<cq.include script="library.jsp"/>`.

      The `library.jsp` filen innehåller `guide.theme.simpleEnrollment` klientbibliotek, som innehåller formateringen för det adaptiva formuläret.

      Sidkomponenten `enrollmentpage` har en exklusiv `head.jsp` som åsidosätter `head.jsp` filen `contentpage` -komponenten.

   1. Inkludera alla skript i `head.jsp` filen för `contentpage` -komponenten till `head.jsp` filen för `enrollmentpage` -komponenten.
   1. I `content.jsp` kan du lägga till ytterligare sidinnehåll eller referenser till andra komponenter som inkluderas när en sida återges. Om du till exempel lägger till den anpassade komponenten `applicationformheader`ska du se till att du lägger till följande referens till komponenten i JSP-filen:

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      Om du lägger till en `parsys` -komponenten i mallnodstrukturen, även den anpassade komponenten.

## Skapa ett adaptivt formulärklientbibliotek {#creating-an-adaptive-form-client-library}

The `head.jsp` filen `enrollmentpage` -komponenten för den nya mallen innehåller ett klientbibliotek `guide.theme.simpleEnrollment`. Standardmallen använder även det här klientbiblioteket. Ändra formatet i den nya mallen på något av följande sätt:

* Definiera ett anpassat tema och ersätt standardtemat `guide.theme.simpleEnrollment` med det anpassade temat.
* Definiera ett nytt klientbibliotek under /etc/designs/mincompany. Inkludera klientbiblioteket efter standardtemaposten på jsp-sidan. Inkludera alla åsidosatta format och ytterligare JavaScript-filer i klientbiblioteket.

>[!NOTE]
>
>Temat avser ett klientbibliotek som ingår i sidkomponenten som används för att återge ett anpassat formulär. Klientbiblioteket styr huvudsakligen utseendet på ett anpassat formulär.
