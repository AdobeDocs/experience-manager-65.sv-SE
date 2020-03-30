---
title: Startar och stoppar WebLogic-servern
seo-title: Startar och stoppar WebLogic-servern
description: Flera procedurer kräver att du startar eller stoppar instansen av WebLogic Server där du vill distribuera AEM-formulärmoduler. I det här dokumentet beskrivs hur du startar och stoppar WebLogic-servern.
seo-description: Flera procedurer kräver att du startar eller stoppar instansen av WebLogic Server där du vill distribuera AEM-formulärmoduler. I det här dokumentet beskrivs hur du startar och stoppar WebLogic-servern.
uuid: 957787fe-4cea-4ecd-b49a-c33023c5c309
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c908d064-6596-473a-b218-22a2496c83f7
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Startar och stoppar WebLogic-servern {#starting-and-stopping-weblogic-server}

Flera procedurer kräver att du startar eller stoppar instansen av WebLogic Server där du vill distribuera AEM-formulärmoduler. Kontrollera att WebLogic Server har stoppats eller körs, beroende på vilken åtgärd du utför.

<table>
 <thead>
  <tr>
   <th><p>Aktivitet</p></th>
   <th><p>WebLogic-tillstånd som krävs</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Skapa en WebLogic-domän</p></td>
   <td><p>Stoppad</p></td>
  </tr>
  <tr>
   <td><p>Skapa en WebLogic-hanterad server</p></td>
   <td><p>Körs</p></td>
  </tr>
  <tr>
   <td><p>Öka antalet servertrådar</p></td>
   <td><p>Körs</p></td>
  </tr>
  <tr>
   <td><p>Distribuera AEM-formulärprodukter</p></td>
   <td><p>Körs</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Om du kör WebLogic Server på Red Hat® Enterprise Linux Advanced Server 4.0 anger du miljövariabeln till 2.4.19 med hjälp av `LD_ASSUME_KERNEL` `export LD_ASSUME_KERNEL=2.4.19` kommandot. Kör sedan WebLogic Server från samma gränssnitt där du anger den här systemvariabeln.

## Starta WebLogic-server {#start-weblogic-server}

1. Gå till *[appserver root]*/user_projects/domains/*[appserverdomain]* från en kommandotolk.
1. Ange följande kommando:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

## Stoppa WebLogic-server {#stop-weblogic-server}

1. Starta administrationskonsolen för WebLogic Server genom att skriva `https://[host name]:7001/console` i URL-raden för en webbläsare.
1. Logga in med det användarnamn och lösenord som användes när den här WebLogic-konfigurationen skapades och klicka sedan på Logga in.
1. Klicka på Lås och redigera under Ändringscenter.
1. Klicka på Miljö > Servrar under Domänstruktur.
1. Klicka på AdminServer och klicka på fliken Kontroll i fönstret Inställningar för AdminServer.
1. Kontrollera att AdminServer är markerat i tabellen Serverstatus och klicka på Avsluta.
1. Välj När jobbet är klart om du vill stänga av servern eller välj Tvinga avstängning nu om du vill stoppa servern omedelbart utan att slutföra pågående åtgärder.
1. Klicka på Ja i rutan Server Life Cycle Assistant för att slutföra avstängningen.

Administrationskonsolen för WebLogic Server är inte längre tillgänglig och kommandotolken som du körde startkommandot från är tillgänglig.

## Starta administrationskonsolen för WebLogic {#start-weblogic-administration-console}

1. Om WebLogic Admin Server inte redan körs går du från en kommandotolk till *[katalogen appServer root]\user_projects\domains\[domainname]*och anger följande kommando:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

1. Gå till administrationskonsolen för WebLogic Server genom att skriva `https://[host name]:[port]/console` i URL-raden för en webbläsare, där *[porten]* är den osäkra avlyssningsporten. Portvärdet är som standard 7001.
1. På inloggningsskärmen skriver du ditt administratörsanvändarnamn och lösenord och klickar på Logga in.

## Starta nodhanteraren {#start-node-manager}

1. Kontrollera att WebLogic Server körs.
1. Gå till *[appserverroten]*/servern/bin från en ny kommandotolk.
1. Ange följande kommando:

   * (Windows) `startNodeManager.cmd`
   * (Linux, UNIX) `./startNodeManager.sh`

## Stoppa nodhanteraren {#stop-node-manager}

När du har stängt av WebLogic Server kan du stänga den kommandotolk som du kallade Node Manager för.

## Starta en WebLogic-hanterad server {#start-a-weblogic-managed-server}

>[!NOTE]
>
>Denna uppgift kan bara utföras när du har skapat en WebLogic-domän och en hanterad server.

1. Kontrollera att WebLogic-servern och nodhanteraren körs.
1. Starta administrationskonsolen för WebLogic-servern genom att skriva `https://host name]:[port]`/console&quot; på URL-raden i en webbläsare.
1. Klicka på Miljö > Servrar under Domänstruktur.
1. Klicka på fliken Kontroll i den högra rutan.
1. Välj den hanterade server som du vill starta.
1. Klicka på knappen Start under den hanterade server som du vill starta.

## Stoppa en WebLogic-hanterad server {#stop-a-weblogic-managed-server}

1. Starta administrationskonsolen för WebLogic-servern genom att skriva `https://`*[värdnamnet]:[port ]*`/console`på URL-raden i en webbläsare.
1. Klicka på Miljö > Servrar under Domänstruktur.
1. Klicka på fliken Kontroll i den högra rutan.
1. Markera den hanterade server som du vill stoppa.
1. Klicka på knappen Stäng under den hanterade server som du vill stoppa.
1. Välj När jobbet är klart om du vill stänga av servern eller välj Tvinga avstängning nu om du vill stoppa servern omedelbart utan att slutföra pågående åtgärder.
1. Klicka på Ja i rutan Server Life Cycle Assistant för att slutföra avstängningen.

