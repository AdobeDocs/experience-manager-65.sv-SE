---
title: Programfixar för AEM Forms
description: Innehåller information om hur du hämtar och installerar en snabbkorrigering för AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 9d5ad43703d2fb3c1d40e10578f5289510a18230
workflow-type: tm+mt
source-wordcount: '1989'
ht-degree: 0%

---

# Adobe Experience Manager Forms Hotfixes{#aem-form-hotfix}

I den här artikeln listas de viktiga korrigeringar som har implementerats för att åtgärda kända fel, förbättra systemstabiliteten och förbättra AEM Forms övergripande prestanda.

>[!NOTE]
>
> Programfixarna är avsedda att vara kumulativa och omfattar alla föregående korrigeringar. När du tillämpar den senaste snabbkorrigeringen på en release åtgärdar den inte bara det senaste problemet utan även alla tidigare felkorrigeringar och förbättringar.

## Programfixar för AEM Forms {#hotfix-for-aem-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Datum</strong></td>
    <td><strong>Länk för hämtning av snabbkorrigeringar (länken AEM Software Distribution)</strong></td>
    <td><strong>Åtgärdade problem</strong></td>
  </tr>
  <tr>
    <td>
      <strong>14 okt 2025</strong><br>
      <em>Gäller för:</em> ImgToPdf misslyckas med AEM Forms SP23 Jboss Hotfix3(109)<br>
    </td>
    <td>
    <ul> Kontakta [Adobe Experience Manager Forms Support](https://business.adobe.com/in/support/main.html) om du vill ha en lösning
    </ul>
    </td>
    <td>
    <ul>
    <li> <b>(FORMS-22029):</b> Förbättrar tillförlitligheten i PDF-konverteringen genom att åtgärda ett problem där PDF Generator (PDFG) inte kan konvertera bildfiler till PDF efter uppgradering till SP23 med hotfix 3, vilket kan orsaka oväntade efterbearbetningsfel.
      <ul>
  <tr>
    <td>
      <strong>23 september 2025</strong><br>
    </td>
    <td>
    <ul>
    <li><strong>Jboss:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/jboss/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-jboss.zip">Programfix3 för AEM Service Pack 6.5.23.0 i Windows för JBoss JEE-server</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/jboss/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-jboss.tar.gz">Hotfix3 för AEM Service Pack 6.5.23.0 i Linux för JBoss JEE-server</a></li>
    <li><strong>Webblogik:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/weblogic/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-weblogic.zip">Programfix3 för AEM Service Pack 6.5.23.0 i Windows för Weblogic JEE-server</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/weblogic/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-weblogic.tar.gz">Hotfix3 för AEM Service Pack 6.5.23.0 i Linux för Weblogic JEE-server</a></li>
    <li><strong>Webbsfär:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/websphere/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-websphere.zip">Programfix3 för AEM Service Pack 6.5.23.0 i Windows för Websphere JEE-server</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/websphere/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-websphere.tar.gz">Hotfix3 för AEM Service Pack 6.5.23.0 i Linux för Websphere JEE-server</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <strong>Den här snabbkorrigeringen åtgärdar följande:</strong> 
    <li> <b>(FORMS-21378):</b> Förbättrad tillförlitlighet för inskickning av formulär genom att åtgärda ett problem där inskickning misslyckas när serversidesvalidering (SSV) är aktiverat och beräknad Meta Info är tom.

<li> <b>(FORMS-21721):</b> Förbättrat problem där konverteringar mellan PS till PDF och HTML till PDF (WebKit) misslyckas efter att snabbkorrigering 2 distribuerats utöver 6.5.23.0. 
    </li>
    </ul>
    </td>    
  </tr>
    </ul>
    </td>
  <tr>
    <td>
      <strong>5 aug 2025</strong><br>
      <em>Gäller för:</em> AEM 6.5 Forms Service Pack 23 <br>
      <em>Installationsanvisningar:</em>
      <a href="/help/forms/using/mitigating-xxe-and-configuration-vulnerabilities-for-experience-manager-forms-jee.md#option-1-for-users-on-version-65230-install-latest-hotfix">
        Felsökning av XXE, konfiguration och fjärrexekvering av kod (CVE-2025-49533) - sårbarheter för AEM Forms i JEE
      </a>
    </td>
    <td>
    <ul>
    <li><strong>Jboss:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-jboss.zip">Hotfix2 för AEM Service Pack 6.5.23.0 i Windows för JBoss JEE-server</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-jboss.tar.gz">Hotfix2 för AEM Service Pack 6.5.23.0 i Linux för JBoss JEE-server</a></li>
    <li><strong>Webblogik:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-weblogic.zip">Hotfix2 för AEM Service Pack 6.5.23.0 i Windows för Weblogic JEE-server</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-weblogic.tar.gz">Hotfix2 för AEM Service Pack 6.5.23.0 i Linux för Weblogic JEE-server</a></li>
    <li><strong>Webbsfär:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-websphere.zip">Programfix2 för AEM Service Pack 6.5.23.0 i Windows för Websphere JEE-server</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-websphere.zip">Hotfix2 för AEM Service Pack 6.5.23.0 i Linux för Websphere JEE-server</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li>Förbättrad säkerhet genom att åtgärda en RCE-säkerhetslucka (Remote Code Execution) i Adobe Experience Manager (AEM) Forms. Problemet var relaterat till utvecklingsläget Struts i användargränssnittet för administratörer, som gjorde det möjligt att utvärdera OGNL (Object-Graph Navigation Language) med hjälp av felsökningsfunktionen. Med den här korrigeringen ser du till att utvecklingsläget Struts är inaktiverat och att lämpliga säkerhetsfilter tillämpas för att förhindra obehörig åtkomst.</li>
    <li>Förbättrat skydd mot sårbarheter i XML (Extensible Markup Language) External Entity (XXE) i EDC-modulen i Adobe Experience Manager (AEM) Forms. Säkerhetsluckorna berodde på felaktig hantering av XML-dokument utan XXE-skydd, vilket kan leda till lokal läsning av filer. Programfixen innehåller:
      <ul>
        <li>Kontrollera att DocumentBuilderFactory som används i klassen SecurityCheckHandler har konfigurerats för att förhindra XXE-attacker.</li>
        <li>Uppdatera ECDC:s webbtjänst för att hantera XML-dokument på ett säkert sätt och förhindra obehörig åtkomst till lokala filer.</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>
      <strong>5 aug 2025</strong><br>
      <em>Gäller för:</em> AEM 6.5 Forms Service Pack 18 - 22<br>
      <em>Installationsanvisningar:</em>
      <a href="/help/forms/using/mitigating-xxe-and-configuration-vulnerabilities-for-experience-manager-forms-jee.md#option-2-for-users-on-65180---65220-manual-hotfix-installation">
        Manuell installation av hotfix för Service Pack 18-22
      </a>
    </td>
    <td>
    <ul>
    <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-xxe-configuration-hotfix.zip">Programfix för AEM 6.5 Forms Service Pack 18 - AEM 6.5 Forms Service Pack 22 </a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li>Förbättrad säkerhet genom att åtgärda en RCE-säkerhetslucka (Remote Code Execution) i Adobe Experience Manager (AEM) Forms. Problemet var relaterat till utvecklingsläget Struts i användargränssnittet för administratörer, som gjorde det möjligt att utvärdera OGNL (Object-Graph Navigation Language) med hjälp av felsökningsfunktionen. Med den här korrigeringen ser du till att utvecklingsläget Struts är inaktiverat och att lämpliga säkerhetsfilter tillämpas för att förhindra obehörig åtkomst.</li>
    <li>Förbättrat skydd mot Extensible Markup Language (XML) External Entity (XXE)-sårbarheter i dokumentsäkerhetsmodulen i Adobe Experience Manager (AEM) Forms. Säkerhetsluckorna berodde på felaktig hantering av XML-dokument utan XXE-skydd, vilket kan leda till lokal läsning av filer. Programfixen innehåller:
      <ul>
        <li>Kontrollera att DocumentBuilderFactory som används i klassen SecurityCheckHandler har konfigurerats för att förhindra XXE-attacker.</li>
        <li>Uppdaterar webbtjänsten Dokumentsäkerhet för att hantera XML-dokument på ett säkert sätt och förhindrar obehörig åtkomst till lokala filer.</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>10 juli 2025-</td>
    <td>
    <ul>
    <li><strong>Jboss:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-win-jboss.zip">Programfix för AEM Service Pack 6.5.23.0 i Windows för JBoss JEE-server</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-jboss.tar.gz">Programfix för AEM Service Pack 6.5.23.0 i Linux för JBoss JEE-server</a></li>
    <li><strong>Webblogik:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-win-weblogic.zip">Programfix för AEM Service Pack 6.5.23.0 i Windows för Weblogic JEE-server</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-weblogic.tar.gz">Programfix för AEM Service Pack 6.5.23.0 i Linux för Weblogic JEE-server</a></li>
    <li><strong>Webbsfär:</strong></li>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-win-websphere.zip">Programfix för AEM Service Pack 6.5.23.0 i Windows för Websphere JEE-server</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-websphere.tar.gz">Programfix för AEM Service Pack 6.5.23.0 i Linux för Websphere JEE-server</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li><strong>Den här snabbkorrigeringen åtgärdar följande:</strong>
      <ul>
        <li><strong>FORMS-20533:</strong> AEM Forms innehåller nu en uppgradering av Struts-versionen från 2.5.33 till 6.x för formulärkomponenten. Detta ger tidigare missade strängändringar som inte ingick i SP23. Supporten lades till via en hotfix som du kan ladda ned och installera för att lägga till stöd för den senaste versionen av Struts.</li>
        <li><strong>FORMS-20532:</strong> AEM Forms innehåller nu en uppgradering av Struts-versionen från 2.5.33 till 6.x för utdatakomponenten. Detta ger tidigare missade strängändringar som inte ingick i SP23. Supporten lades till via en hotfix som du kan ladda ned och installera för att lägga till stöd för den senaste versionen av Struts.</li>
        <li><strong>FORMS-20203:</strong> När en användare uppgraderar från AEM Service Pack 2.5.x till AEM Forms Service Pack 6.x visas inte alla konfigurationer i principgränssnittet, t.ex. alternativet att lägga till en vattenstämpel. Du kan hämta och installera programfixen för att lösa problemet.</li>
        <li><strong>FORMS-20360:</strong> Efter uppgradering till AEM Forms Service Pack 6.5.23.0 misslyckas ImageToPDF-konverteringstjänsten med felet:<br>
        <code>17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp</code><br>
        Du kan hämta och installera programfixen för att lösa problemet.</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>26 mars 2025 </br> </br> Följ anvisningarna <a href="/help/forms/using/mitigating-spring-framework-vulnerabilities-for-aem-forms-on-jee.md"> Minska sårbarheten för vårregelverket för AEM Forms i JEE </a> för att installera den här korrigeringen.</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-win-jboss.tar.gz">Programfix för AEM Service Pack 6.5.22.0 i Windows för JBoss JEE-server </a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-jboss.tar.gz">Programfix för AEM Service Pack 6.5.22.0 i Linux för JBoss JEE-server </a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-win-weblogic.tar.gz">Programfix för AEM Service Pack 6.5.22.0 i Windows för Weblogic JEE-server </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-weblogic.tar.gz">Programfix för AEM Service Pack 6.5.2.0 i Linux för Weblogic JEE-server</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-win-websphere.tar.gz">Programfix för AEM Service Pack 6.5.22.0 i Windows för Websphere JEE-server </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-websphere.tar.gz">Programfix för AEM Service Pack 6.5.22.0 i Linux för Websphere JEE-server</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Minska vårens ramverk - sårbarheter för AEM Forms i JEE</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>10 juli 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-jboss.zip.zip">Programfix för AEM Service Pack 6.5.21.0 i Windows för JBoss JEE-server </a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-jboss.tar.gz">Programfix för AEM Service Pack 6.5.21.0 i Linux för JBoss JEE-server </a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-websphere.zip.zip">Programfix för AEM Service Pack 6.5.21.0 i Windows för Webshpere JEE-server </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-websphere.tar.gz">Programfix för AEM Service Pack 6.5.21.0 i Linux för Webshpere JEE-server</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-weblogic.zip.zip">Programfix för AEM Service Pack 6.5.21.0 i Windows för Weblogic JEE-server </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-weblogic.tar.gz">Programfix för AEM Service Pack 6.5.21.0 i Linux för Weblogic JEE-server</a> </li>
     </ul>
     </td>
    <td>
    <ul><li>När en användare uppdaterar till AEM Forms Service Pack 20 (6.5.20.0) på JEE-servern och genererar PDF-filer med hjälp av utdatatjänster, återges PDF-filerna med tillgänglighetsproblem. (LC-3922112)</li><li>Taggade PDF-filer som genererats med utdatatjänsten i AEM Forms JEE visar "Olämplig strukturvarning". (LC-3922038)</li><li>När ett formulär skickas i AEM Forms JEE tas instanser av ett upprepat XML-element bort från data. (LC-3922017)</li><li>När en användare i en Linux-miljö återger ett adaptivt formulär (i JEE) i HTML återges det inte korrekt. (LC-3921957)</li><li>När en användare konverterar en XTG-fil till PostScript-format med hjälp av utdatatjänsten i AEM Forms JEE misslyckas den med följande fel: AEM_OUT_001_003: Oväntat undantag: PAExecute-fel: XFA_RENDER_FAILURE. (LC-3921720)</li><li>När en användare har uppgraderat till AEM Forms Service Pack 18 (6.5.18.0) på JEE-servern återges inte HTML5 eller PDF forms och XMLFM-krascher när användaren skickar ett formulär. (LC-3921718)
    </ul>
    </td>    
  </tr>
  <tr>
    <td>21 juni 2024</td>
     <td>
     <ul>
     <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0">Programfix för AEM Service Pack 6.5.21.0 eller AEM Forms Service Pack 6.5.22.0 på JBoss JEE-server </a> </li>
      <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0">Programfix för AEM Service Pack 6.5.21.0 eller AEM Forms Service Pack 6.5.22.0 på Weblogic JEE-server </a> </li>
       <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0">Programfix för AEM Service Pack 6.5.21.0 eller AEM Forms Service Pack 6.5.22.0 på JEE-webbserver </a> </li>
        <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0">Programfix för AEM Service Pack 6.5.21.0 eller AEM Forms Service Pack 6.5.22.0 på OSGi-server </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li> När du har uppgraderat till AEM Forms Service Pack 6.5.21.0 eller AEM Forms Service Pack 6.5.22.0 kan tjänsten PaperCapture inte utföra OCR-åtgärder (Optical Character Recognition) på PDF-filer. Installationsanvisningar finns i artikeln <a href="/help/forms/using/papercapture-service-resolution.md"> troubleshooting</a> (Felsökning).(CQDOC-21680) </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>21 juni 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fccm-ccr-content-10.0.206.zip">Programfix för AEM Service Pack 6.5.21.0 </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Utkastbrev med XML-data fastnar i inläsningsläget under förhandsgranskningen. Instruktioner för hämtning och installation av snabbkorrigeringen finns i avsnittet <a href="#install-hotfix"> Hämta och installera snabbkorrigering för formulärproblem </a>.(FORMS-14521)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>16 maj 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1192-010.zip">Programfix för AEM Service Pack 6.5.20.0 för Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1192-010.zip">Programfix för AEM Service Pack 6.5.20.0 för Linux </a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1192-010.zip">Programfix för AEM Service Pack 6.5.20.0 för Apple macOS</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>I ett adaptivt formulär som baseras på en XDP-fil med inbäddade skript i kryssrutor, körs inte skripten för element efter sådana kryssrutor. Det finns en programfix för den här utgåvan. (FORMS-1424) </li>
     <li> Rader i datumväljarwidgeten trunkeras när du går igenom flera månader i snabbwidgeten för fält med redigerings-/visningsmönster. Det finns en programfix för den här utgåvan. (FORMS-13620) </li>
     <li>Det går inte att skicka formulär när DOR-tjänsten (Document of Record) används i serverdelen. Felmeddelandet som påträffades är: "Det gick inte att skicka åtgärden eftersom formulärresursen inte är korrekt tilldelad." (FORMS-13798) </li>
     <li>När ett anpassat formulär skickas från en Adobe Experience Manager Publish-instans till ett Adobe Experience Manager-arbetsflöde, kan arbetsflödet inte spara de bifogade filerna.  (FORMS-14209) </li>
     <li> När du installerar AEM 6.5 Forms Service Pack 20-paketet (AEM Forms-tilläggspaket för SP20) uppvisar AEM Sites användargränssnitt en avsevärd prestandaförsämring.  (FORMS-13791) </li>
     <li>Förifyllningstjänsten misslyckas med ett null-pekarundantag i Interactive Communications. (CQDOC-21355)</li>
     <li>Konfigurationer som använder den gamla molntjänsten för Adobe Analytics med användarautentiserad autentisering fungerar inte korrekt, vilket gör att analysreglerna inte kan köras. (FORMS-15428)
    </ul>
    </td>    
  </tr>
  <tr>
    <td>29 januari 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">Programfix för AEM Service Pack 6.5.19.0 för Windows på JEE-server</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>På AEM Forms på JEE-servern kan HTML5 Forms som använder kontextsökvägen inte återges. (FORMS-12485, FORMS-12691).</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>29 januari 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">Programfix för AEM Service Pack 6.5.18.0 för Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">Programfix för AEM Service Pack 6.5.18.0 för Linux</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">Programfix för AEM Service Pack 6.5.18.0 för Apple macOS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li> Komponenten Skriptsignatur som är klar att användas kan inte återges för en förhandsgranskning i ett anpassat formulär. (FORMS-12073).</li>
    </ul>
    </td>    
   </tr>
   <tr>
    <td>20 november 2023</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Programfix för AEM Service Pack 6.5.18.0 för Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Programfix för AEM Service Pack 6.5.18.0 för Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Programfix för AEM Service Pack 6.5.18.0 för Apple macOS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Inline-signering slutar fungera när en omdirigerings-URL anges i stödlinjebehållaren för ett adaptivt formulär. (FORMS-10493)</li>
    <li>DoR-mallar (Document of Record) kan inte publiceras för lokaliserade adaptiva Forms. (FORMS-10535)</li>
    <li>Interaktiv kommunikation med stora textbundna bilder kan inte öppnas i redigeringsläge. (FORMS-10578)</li>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## Hämta och installera en OSGi-hotfix {#download-install-hotfix}

Utför följande steg för att hämta och installera programfixen:

1. Hämta [snabbkorrigering](#hotfix-for-adaptive-forms) från länken för programdistribution.
1. Extrahera Hotfix-arkivfilen så att du kan hämta Experience Manager-paketfiler (.zip) och paketfiler (.jar).
1. Överför och installera paketet (.zip) via [Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Öppna konfigurationshanterarpaketen `https://server:host/system/console/bundles`, ladda upp och installera paketet (.jar). Programfixen är installerad.

## Installera en JEE-korrigering {#download-install-jee-patch}

Anvisningar om hur du installerar en JEE-korrigering finns i [dokumentationen för AEM Forms JEE-korrigeringsprogrammet](/help/release-notes/jee-patch-installer-65.md).


## Ladda ned och installera snabbkorrigering för problem med utkast {#install-hotfix}

Så här löser du problemet:

1. Hämta [snabbkorrigeringen](#hotfix-for-adaptive-forms) från portalen för programvarudistribution.
2. Överför och installera paketet (.zip) med [CRX Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
