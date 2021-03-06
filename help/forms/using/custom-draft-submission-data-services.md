---
title: Anpassa datatjänster för utkast och överföring
seo-title: Anpassa datatjänster för utkast och överföring
description: AEM Forms lagrar som standard utkast och skickade adaptiva formulär i en standardnod på Publish-instansen. Du kan dock konfigurera AEM Forms tjänster för utkast och inskickning av data för att anpassa lagringen av utkast och inskickade adaptiva formulär.
seo-description: AEM Forms lagrar som standard utkast och skickade adaptiva formulär i en standardnod på Publish-instansen. Du kan dock konfigurera AEM Forms tjänster för utkast och inskickning av data för att anpassa lagringen av utkast och inskickade adaptiva formulär.
uuid: c3ec1708-3b11-4142-93f0-1cffb6643f34
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 602fd6a9-9a65-411c-8475-a4082a3fdee0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Anpassa datatjänsterna för utkast och överföring {#customizing-draft-and-submission-data-services}

## Översikt {#overview}

Med AEM Forms kan användare spara ett anpassat formulär som ett utkast. Utkastfunktionen ger användarna möjlighet att behålla ett pågående formulär. Användaren kan sedan fylla i och skicka formuläret när som helst från vilken enhet som helst.

Som standard lagrar AEM Forms användardata som är kopplade till utkastet och överföringen på Publish-instansen i noden `/content/forms/fp`.

AEM Forms portalkomponenter innehåller dock datatjänster som gör att du kan anpassa implementeringen av lagring av användardata för utkast och inskickningar. Du kan till exempel lagra data i ett datalager som är implementerat i din organisation.

Om du vill anpassa lagringen av användardata måste du implementera tjänsterna [Utkastdata](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p) och [Skicka data](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p).

## Förutsättningar {#prerequisites}

* Aktivera [Forms-portalkomponenter](/help/forms/using/enabling-forms-portal-components.md)
* Skapa en [formulärportalsida](/help/forms/using/creating-form-portal-page.md)
* Aktivera [adaptiva formulär för formulärportalen](/help/forms/using/draft-submission-component.md)
* Lär dig [implementeringsinformation för anpassad lagring](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Utkastdatatjänst {#draft-data-service}

Om du vill anpassa lagringen av användarutkastdata måste du tillhandahålla implementering för alla metoder i `DraftAFDataService`-gränssnittet.

En beskrivning av metoderna och deras argument finns i följande kodexempel i gränssnittet:

```java
public interface DraftAFDataService {

 /**
  * Deletes the user data stored against the ID passed as the argument
  *
  * @param draftDataID
  * @return status for the just occurred delete draft UserData operation
  * @throws FormsPortalException
  */
 public Boolean deleteAFDraftUserData (String draftDataID) throws FormsPortalException;

 /**
  * Saves user data provided in the argument map
  *
  * @param draftUserDataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID") in case of update
  * @return userData ID would be returned which needs to be saved in metadata node
  * @throws FormsPortalException
  */
 public String saveAFUserData (Map<String, Object> draftUserDataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as the argument
  *
  * @param Draft DataID
  * @return guideState (which would then be populated in adaptive form to reload the draft) which is stored against draftDataID
  * @throws FormsPortalException
  */
 public byte[] getAFDraftUserData(String draftDataID) throws FormsPortalException;

 /**
  * Saves the attachments for current adaptive form instance
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String saveAttachments(byte[] attachmentBytes) throws FormsPortalException;
}
```

## Datatjänst för överföring {#submission-data-service}

Om du vill anpassa lagringen av användarinskickade data måste du tillhandahålla implementering för alla metoder i `SubmittedAFDataService`-gränssnittet.

En beskrivning av metoderna och deras argument finns i följande kodexempel i gränssnittet:

```java
public interface SubmittedAFDataService {

 /**
  * Submits the user data passed in argument map
  *
  * @param submittedAFUserdataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID")
  * @return userData ID is returned that needs to be saved in the metadata node
  * @throws FormsPortalException
  */
 public String submitAFUserData (Map<String, Object> submittedAFUserdataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as argument
  *
  * @param submitDataID
  * @return guideState which would be used to open DOR
  * @throws FormsPortalException
  */
 public byte[] getSubmittedAFUSerData(String submitDataID) throws FormsPortalException;

 /**
  * Deletes user data stored against the ID passed as argument
  *
  * @param Submit DataID
  * @return status of the delete operation on Submitted User data
  * @throws FormsPortalException
  */

 public Boolean deleteSubmittedAFUserData(String submitDataID) throws FormsPortalException;

 /**
  * Submits the attachment bytes passed as argument
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String submitAttachments(Object attachmentBytes) throws FormsPortalException;

}
```

