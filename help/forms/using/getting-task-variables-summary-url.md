---
title: Hämtar aktivitetsvariabler i sammanställnings-URL
seo-title: Getting Task Variables in Summary URL
description: Hur du återanvänder informationen om en uppgift och skapar en sammanfattande URL för att sammanfatta eller beskriva en uppgift.
seo-description: How-to reuse the information about a task and generate a Summary URL to summarize or describe a task.
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Hämtar aktivitetsvariabler i sammanställnings-URL {#getting-task-variables-in-summary-url}

Sammanfattningssidan visar uppgiftsrelaterad information. I den här artikeln beskrivs hur du kan återanvända uppgiftsrelaterad information på sammanfattningssidan.

I den här exempelstrukturen skickar en medarbetare ett ledighetsansökningsformulär. Ansökningsformuläret skickas sedan till den anställdes chef för godkännande.

1. Skapa ett exempel på en HTML-renderare (html.esp) för ResursType **Anställda/PtoApplication**.

   Återgivning förutsätter att följande egenskaper ställs in på noden:

   * namn
   * empid
   * orsak
   * varaktighet

   >[!NOTE]
   >
   >Den här återgivaren är mallen för sammanfattningssidor.

   Följande exempelkod för den här renderaren finns i:

   `apps/Employees/PtoApplication/html.esp`

   ```html
   <html>
     <body>
       <table>
       <tbody>
       <tr>
           <td>
               <h3>Employee Name: <%= currentNode.ename %></h3>
               <h3>Employee ID: <%= currentNode.eid %></h3>
               <h3>Leave duration: <%= currentNode.duration %> days</h3>
               <h3>Reason: <%= currentNode.reason %></h3>
           </td>
       </tr>
       </tbody>
       </table>
     </body>
   </html>
   ```

1. Ändra orkestreringen för att extrahera de fyra egenskaperna från skickade formulärdata. Skapa sedan en nod i CRX av typen **Anställda/PtoApplication**, med egenskaperna ifyllda.

   1. Skapa en process **skapa PTO-sammanfattning** och använda detta som en underprocess före **Tilldela uppgift** i er organisation.
   1. Definiera **employeeName**, **employeeID**, **ptoReason**, **totalDays** och **nodeName** som indatavariabler i den nya processen. Dessa variabler skickas som skickade formulärdata.

      Definiera även en utdatavariabel **ptoNodePath** som ska användas när sammanfattnings-URL anges.

   1. I **skapa PTO-sammanfattning** använder du **ange värde** för att ange indatainformation i en **nodeProperty**(**nodeProps**).

      Tangenterna på kartan ska vara desamma som tangenterna som definierades i HTML-renderaren i föregående steg.

      Lägg även till en **sling:resourceType** nyckel med värde **Anställda/PtoApplication** på kartan.

   1. Använda underprocessen **storeContent** från **ContentRepositoryConnector** i **skapa PTO-sammanfattning** -processen. Den här underprocessen skapar en CRX-nod.

      Den har tre indatavariabler:

      * **Mappsökväg**: Sökvägen där den nya CRX-noden skapas. Ange banan som **/content**.
      * **Nodnamn**: Tilldela indatavariabeln nodeName till det här fältet. Detta är en unik nodnamnssträng.
      * **Nodtyp**: Definiera typen som **nt:ostrukturerad**. Utdata för den här processen är nodePath. nodePath är CRX-sökvägen för den nyskapade noden. The ndoePath skulle vara det slutliga resultatet av **skapa PTO** sammanfattningsprocess.
   1. Skicka skickade formulärdata (**employeeName**, **employeeID**, **ptoReason** och **totalDays**) som indata till den nya processen **skapa PTO-sammanfattning**. Ta resultatet som **ptoSummaryNodePath**.


1. Definiera sammanfattnings-URL:en som ett XPath-uttryck som innehåller serverinformationen tillsammans med **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

När du öppnar en uppgift i AEM Forms arbetsyta får sammanfattnings-URL åtkomst till CRX-noden och HTML-återgivaren visar sammanfattningen.

Sammanfattningslayouten kan ändras utan att processen ändras. Sammanfattningen visas korrekt vid renderingen i HTML.
