---
title: Hämtar aktivitetsvariabler i sammanställnings-URL
seo-title: Hämtar aktivitetsvariabler i sammanställnings-URL
description: Hur du återanvänder informationen om en uppgift och skapar en sammanfattande URL för att sammanfatta eller beskriva en uppgift.
seo-description: Hur du återanvänder informationen om en uppgift och skapar en sammanfattande URL för att sammanfatta eller beskriva en uppgift.
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---


# Hämtar aktivitetsvariabler i sammanfattnings-URL {#getting-task-variables-in-summary-url}

Sammanfattningssidan visar uppgiftsrelaterad information. I den här artikeln beskrivs hur du kan återanvända uppgiftsrelaterad information på sammanfattningssidan.

I den här exempelstrukturen skickar en medarbetare ett ledighetsansökningsformulär. Ansökningsformuläret skickas sedan till den anställdes chef för godkännande.

1. Skapa ett exempel på en HTML-renderare (html.esp) för resourceType **Employees/PtoApplication**.

   Återgivning förutsätter att följande egenskaper ställs in på noden:

   * namn
   * empid
   * reason
   * duration

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

1. Ändra orkestreringen för att extrahera de fyra egenskaperna från skickade formulärdata. Sedan skapar du en nod i CRX av typen **Employees/PtoApplication**, med egenskaperna ifyllda.

   1. Skapa en process **skapa en PTO-sammanfattning** och använd den som en underprocess före **Tilldela uppgift**-åtgärden i din organisation.
   1. Definiera **employeeName**, **employeeID**, **ptoReason**, **totalDays** och **nodeName** som indatavariabler i den nya processen. Dessa variabler skickas som skickade formulärdata.

      Definiera också en utdatavariabel **ptoNodePath** som ska användas när sammanfattnings-URL anges.

   1. I processen **skapa PTO-sammanfattning** använder du **set value**-komponenten för att ange indatainformation i en **nodeProperty**(**nodeProps**)-mappning.

      Tangenterna på kartan ska vara samma som tangenterna som definierades i HTML-återgivningen i föregående steg.

      Lägg även till en **sling:resourceType**-nyckel med värdet **Employees/PtoApplication** på kartan.

   1. Använd underprocessen **storeContent** från tjänsten **ContentRepositoryConnector** i **skapa PTO-sammanfattning**-processen. Den här underprocessen skapar en CRX-nod.

      Den har tre indatavariabler:

      * **Mappsökväg**: Sökvägen där den nya CRX-noden skapas. Ange sökvägen som **/content**.
      * **Nodnamn**: Tilldela indatavariabeln nodeName till det här fältet. Detta är en unik nodnamnssträng.
      * **Nodtyp**: Definiera typen som  **not:undefined**. Utdata för den här processen är nodePath. nodePath är CRX-sökvägen för den nyskapade noden. ndoePath skulle vara det slutliga resultatet av sammanfattningsprocessen **skapa PTO**.
   1. Skicka skickade formulärdata (**employeeName**, **employeeID**, **ptoReason** och **totalDays**) som indata till den nya processen **skapa PTO-sammanfattning**. Ta utdata som **ptoSummaryNodePath**.


1. Definiera sammanfattnings-URL:en som ett XPath-uttryck som innehåller serverinformationen tillsammans med **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

När du öppnar en uppgift på arbetsytan i AEM Forms får sammanfattnings-URL åtkomst till CRX-noden och HTML-återgivaren visar sammanfattningen.

Sammanfattningslayouten kan ändras utan att processen ändras. HTML-återgivaren visar sammanfattningen korrekt.
