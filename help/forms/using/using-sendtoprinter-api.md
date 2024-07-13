---
title: Använda API:t sendToPrinter
description: Skicka ett dokument till skrivaren med hjälp av tjänsten sendToPrinter.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services,APIs & Integrations
exl-id: 585d4053-1056-4d2b-a9df-9516775afe50
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# Använda API:t sendToPrinter {#using-the-sendtoprinter-api}

## Ökning {#overview}

I AEM Forms kan du använda tjänsten SendToPrinter för att skicka ett dokument till skrivaren. Tjänsten SendToPrinter stöder följande åtkomstmekanismer för utskrift:

* **Direkttillgänglig skrivare** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **Indirekt tillgänglig skrivare** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

  När du skickar ett dokument till en skrivare anger du ett av följande utskriftsprotokoll:

   * **CUPS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * &quot;**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * &quot;**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIF**: Utdatatjänsten stöder utskriftsprotokollet Common Internet File System (CIF).

## Använda tjänsten SendToPrinter {#using-sendtoprinter-service}

Tabellen nedan listar:

* information om printerName eller printServer som ska användas för olika protokoll.
* värde eller undantag som en skrivare returnerar för olika kombinationer av skrivarserverns URI och skrivarens namn

| Protokoll (åtkomstmekanism) | Utskriftsserverns URI (PrinterSpec.printServer) | Skrivarens namn (PrinterSpec.printerName) | Resultat |
|--- |--- |--- |--- |
| SharedPrinter | Alla | Tom | Undantag: Det obligatoriska argumentet sPrinterName får inte vara tomt. |
| SharedPrinter | Alla | Ogiltig | Ett undantag är att skrivaren inte kan hittas. |
| SharedPrinter | Alla | Giltig | Utskriften är klar. |
| LPD | Tom | Alla | ett undantag som anger att det obligatoriska argumentet sPrintServerUri inte får vara tomt. |
| LPD | Ogiltig | Tom | ett undantag som anger att det obligatoriska argumentet sPrinterName inte får vara tomt. |
| LPD | Ogiltig | Inte tom | ett undantag som anger att sPrintServerUri inte hittas. |
| LPD | Giltig | Ogiltig | ett undantag som anger att skrivaren inte kan hittas. |
| LPD | Giltig | Giltig | Utskriften är klar. |
| CUPS | Tom | Alla | ett undantag som anger att det obligatoriska argumentet sPrintServerUri inte får vara tomt. |
| CUPS | Ogiltig | Alla | ett undantag som anger att skrivaren inte kan hittas. |
| CUPS | Giltig | Alla | Utskriften är klar. |
| DirectIP | Tom | Alla | ett undantag som anger att det obligatoriska argumentet sPrintServerUri inte får vara tomt. |
| DirectIP | Ogiltig | Alla | ett undantag som anger att skrivaren inte kan hittas. |
| DirectIP | Giltig | Alla | Utskriften är klar. |
| CIF | Giltig | Tom | Utskriften är klar. |
| CIF | Ogiltig | Alla | ett okänt fel vid utskrift med CIF. |
| CIF | Tom | Alla | ett undantag som anger att det obligatoriska argumentet sPrintServerUri inte får vara tomt. |

## Autentiseringsstöd {#authentication-support}

Autentisering stöds bara för CIF utskrift. Ange användarnamn/lösenord/domän i PrinterSpec för att autentisera. Du kan kryptera ett lösenord med AEM Granite CypernSupport-tjänsten genom att utföra följande steg:

1. Gå till https://&lt;server>:&lt;port>/system/console.

1. Gå till **[!UICONTROL Main]** > **[!UICONTROL Crypto Support]**.

1. Ange oformaterad text och klicka på **[!UICONTROL Protect]**.
