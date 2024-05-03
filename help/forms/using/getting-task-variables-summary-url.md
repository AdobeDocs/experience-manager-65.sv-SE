---
title: Hämtar aktivitetsvariabler i sammanställnings-URL
description: Hur du återanvänder informationen om en uppgift och skapar en sammanfattande URL för att sammanfatta eller beskriva en uppgift.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '431'
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

      Definiera även en utdatavariabel **ptoNodePath** som används när sammanfattnings-URL anges.

   1. I **skapa PTO-sammanfattning** -processen, använda **ange värde** för att ange indatainformation i en **nodeProperty**(**nodeProps**).

      Tangenterna på kartan ska vara desamma som tangenterna som definierades i HTML-renderaren i föregående steg.

      Lägg även till en **sling:resourceType** nyckel med värde **Anställda/PtoApplication** på kartan.

   1. Använda underprocessen **storeContent** från **ContentRepositoryConnector** i **skapa PTO-sammanfattning** -processen. Den här underprocessen skapar en CRX-nod.

      Den har tre indatavariabler:

      * **Mappsökväg**: Den sökväg där den nya CRX-noden skapas. Ange banan som **/content**.
      * **Nodnamn**: Tilldela indatavariabeln nodeName till det här fältet. Detta är en unik nodnamnssträng.
      * **Nodtyp**: Definiera typen som **nt:ostrukturerad**. Utdata för den här processen är nodePath. nodePath är CRX-sökvägen för den nyskapade noden. The ndoePath skulle vara det slutliga resultatet av **skapa PTO** sammanfattningsprocess.

   1. Skicka skickade formulärdata (**employeeName**, **employeeID**, **ptoReason** och **totalDays**) som indata till den nya processen **skapa PTO-sammanfattning**. Ta resultatet som **ptoSummaryNodePath**.

1. Definiera sammanfattnings-URL som ett XPath-uttryck som innehåller serverinformationen tillsammans med **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

När du öppnar en uppgift i AEM Forms arbetsyta får sammanfattnings-URL åtkomst till CRX-noden och HTML-återgivaren visar sammanfattningen.

Sammanfattningslayouten kan ändras utan att processen ändras. Sammanfattningen visas korrekt vid renderingen i HTML.
