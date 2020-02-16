---
title: Konfigurera lagringstjänster för utkast och överföringar
seo-title: Konfigurera lagringstjänster för utkast och överföringar
description: Lär dig hur du konfigurerar lagring för utkast och överföringar
seo-description: Lär dig hur du konfigurerar lagring för utkast och överföringar
uuid: 2f4efc07-312c-4908-8c91-84f4e6c5ad25
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6ebb6420-68b6-4abc-b298-c252db038416
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542

---


# Konfigurera lagringstjänster för utkast och överföringar {#configuring-storage-services-for-drafts-and-submissions}

## Översikt {#overview}

Med AEM Forms kan du lagra:

* **Utkast**: Ett pågående formulär som slutanvändarna fyller i och sparar för senare och skickar därefter.

* **Sändningar**: Skickade formulär som innehåller användardata.

AEM Forms Portal-data och metadatatjänster har stöd för utkast och inskickningar. Som standard lagras data i publiceringsinstansen, som sedan återreplikeras till den konfigurerade författarinstansen så att den blir tillgänglig för körning till andra publiceringsinstanser.

Problemet med den befintliga användningsklara metoden är att den lagrar alla data i publiceringsinstansen, inklusive data som kan vara personligt identifierbar information (PII).

Utöver det ovan nämnda standardtillvägagångssättet finns det även en alternativ implementering för att direkt överföra formulärdata till bearbetning i stället för att spara dem lokalt. Kunder som oroar sig för lagring av potentiellt känsliga data på en publiceringsinstans kan välja den alternativa implementering som data skickas till en bearbetningsserver. Eftersom bearbetningen sker på författarinstansen ligger den vanligtvis kvar i en säker zon.

>[!NOTE]
>
>När du använder formulärportalens överföringsåtgärd eller aktiverar alternativet Lagra data i formulärportalen i anpassad form, lagras formulärdata i AEM-databasen. I en produktionsmiljö bör du inte lagra utkast eller inskickade formulärdata i AEM-databasen. Istället måste ni integrera utkasten och skicka-komponenten med en säker lagringsplats, t.ex. en företagsdatabas, för att lagra utkast och skickade formulärdata.
>
>Mer information finns i [Exempel på hur du integrerar utkast och inskickningskomponenter med databaser](/help/forms/using/integrate-draft-submission-database.md).

## Konfigurera formulärportalutkast och skicka-tjänster {#configuring-forms-portal-drafts-and-submissions-services}

I AEM Web Console Configuration (Konfiguration av AEM-webbkonsol) `https://[host]:[port]/system/console/configMgr`klickar du för att öppna **formulärportalen, utkast och inskickningskonfiguration** i redigeringsläge.

Ange värden för egenskaper baserat på dina krav enligt beskrivningen nedan:

### Körklara tjänster för lagring av data i publiceringsinstansen {#out-of-the-box-services-to-store-data-on-publish-instance}

Data replikeras omvänt till den konfigurerade författarinstansen.

<table>
 <tbody>
  <tr>
   <th>Egenskap</th>
   <th>Värde</th>
  </tr>
  <tr>
   <td>Forms Portal Draft Data Service (identifierare för draft data service (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Form Portal Draft Metadata Service (identifierare för utkast till metadatatjänst (<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal Submit Data Service (identifierare för Skicka data service (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Metadatatjänst för att skicka formulär (identifierare för tjänsten Skicka metadata (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### Utgångstjänster för lagring av data på fjärrbearbetningsinstansen {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

Data skickas direkt till den konfigurerade fjärrinstansen

<table>
 <tbody>
  <tr>
   <th>Egenskap</th>
   <th>Värde</th>
  </tr>
  <tr>
   <td>Forms Portal Draft Data Service (identifierare för draft data service (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Form Portal Draft Metadata Service (identifierare för utkast till metadatatjänst (<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal Submit Data Service (identifierare för Skicka data service (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Metadatatjänst för att skicka formulär (identifierare för tjänsten Skicka metadata (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

Förutom konfigurationen ovan anger du information om den konfigurerade fjärrbearbetningsinstansen.

I AEM Web Console Configuration ( `https://[host]:[port]/system/console/configMgr`) klickar du för att öppna **AEM DS Settings Service** i redigeringsläge. I dialogrutan för AEM DS-inställningstjänsten anger du information om hur server-URL:en bearbetas, användarnamn och lösenord för servern.

>[!NOTE]
>
>Ett exempel på implementering finns också för lagring av användardata i en databas. Mer information om hur du konfigurerar data- och metadatatjänster för att lagra användardata i en extern databas finns i [Exempel för att integrera komponenten för utkast och överföringar med databasen](/help/forms/using/integrate-draft-submission-database.md).

