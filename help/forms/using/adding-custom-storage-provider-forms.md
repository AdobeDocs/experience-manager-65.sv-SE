---
title: Anpassad lagring för utkast och inskickningskomponenter
seo-title: Anpassad lagring för utkast och inskickningskomponenter
description: Se hur du kan anpassa lagring av användardata för utkast och inskickade data.
seo-description: Se hur du kan anpassa lagring av användardata för utkast och inskickade data.
uuid: ac2e80ee-a9c7-44e6-801e-fe5a840cb7f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 154255e7-468a-42e6-a33d-eee691cf854d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Anpassad lagring för utkast och inskickningskomponenter {#custom-storage-for-drafts-and-submissions-component}

## Översikt {#overview}

Med AEM Forms kan du spara ett formulär som ett utkast. Med utkastsfunktionen kan du underhålla ett pågående formulär som du kan fylla i och skicka senare från vilken enhet som helst.

Som standard lagrar AEM Forms de användardata som är kopplade till utkastet och överföringen av ett formulär på `/content/forms/fp` noden i Publish-instansen. Dessutom innehåller AEM Forms-portalkomponenterna datatjänster som du kan använda för att anpassa implementeringen av lagring av användardata för utkast och överföringar. Du kan till exempel lagra användardata i ett datalager.

## Förutsättningar {#prerequisites}

* Aktivera komponenter för [formulärportalen](/help/forms/using/enabling-forms-portal-components.md)
* Skapa en [formulärportalsida](/help/forms/using/creating-form-portal-page.md)
* Aktivera [anpassningsbara formulär för formulärportalen](/help/forms/using/draft-submission-component.md)
* Lär dig [implementeringsinformation för anpassad lagring](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Utkastdatatjänst {#draft-data-service}

Om du vill anpassa lagringen av användardata för utkast måste du implementera alla metoder i `DraftDataService` gränssnittet. I följande exempelkod beskrivs metoderna och argumenten.

```java
/**
 * DraftDataService service will get/delete/save user data (attachments and form data) filled with a draft instance of Form
 */

public interface DraftDataService {

    /**
     * To save/modify user data for this userDataID, it will be null in case of creation
     * @param draftDataID: unique identifier associated with the form data
     * @param formName: name of the form whose draft is being saved
     * @param formData: user data associated with this draft
     * @return userdataID corresponding to which user data has been stored and which can be used later to retrieve this user data
     * @throws FormsPortalException
     */
    public String saveData (String draftDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Returns the user data stored against the ID passed as the argument
     * @param userDataID: unique data id for user data associated with a draft
     * @return user data associated with this data ID
     * @throws FormsPortalException
     */

    public byte[] getData (String userDataID) throws FormsPortalException;

    /**
     * To delete data associated with this draft
     * @param userDataID: unique data id for data associated with a draft
     * @return status of delete operation on data associated with this draft
     * @throws FormsPortalException
     */

    public boolean deleteData (String userDataID) throws FormsPortalException;

    /**
     * Saves the attachment for current form instance
     * @param attachmentsBytes: byte array of the attachment to be saved
     * @return unique id (attachmentID) for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment (byte[] attachmentBytes) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

## Datatjänst för överföring {#submission-data-service}

Om du vill anpassa lagringen av användardata för överföring måste du implementera alla metoder i `SubmitDataService` gränssnittet. I följande exempelkod beskrivs metoderna och argumenten.

```java
/**
 * SubmitDataService service will get/delete/submit user data (attachments and form data) filled with a submission of Form
 */
public interface SubmitDataService {

    /**
     * Submits the user data passed in argument map
     * @param userDataID, unique identifier associated with this user data
     * @param formName, name of the form whose draft is being submitted
     * @param formData, user data associated with this submission
     * @return userdataID, corresponding to which the user data has been stored and which can be used later to retrieve this data
     * @throws FormsPortalException
     */
    public String saveData (String userDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Submits the user data provided as byte array
     * @param id
     * @param data
     * @return id corresponding to saved data
     * @throws FormsPortalException
     */
    public String saveData (String id, byte[] data) throws FormsPortalException;

    /** Submits the user data provided as byte array asynchronously for the user name provided in the options map
     * @param data data to be saved in bytes
     * @param options map containing options that affect this save
     * @return id of the saved data instance
     */
    public String saveDataAsynchronusly(byte[] data, Map<String, Object> options) throws FormsPortalException;

    /**
     * Gets the user data stored against the ID passed as argument
     * @param userDataID: unique id associated with this user data for this submission
     * @return user data associated with this submission
     * @throws FormsPortalException
     */
    public byte[] getData(String userDataID) throws FormsPortalException;

    /**
     * Deletes user data stored against the userDataID
     * @param userDataID: unique id associated with this user data for this submission
     * @return status of the delete operation on this submission
     * @throws FormsPortalException
     */

    public boolean deleteData(String userDataID) throws FormsPortalException;

    /**
     * Submits the attachment bytes passed as argument
     * @param attachmentsBytes: would expect byte array of the attachment for this submission
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment(byte[] attachmentBytes) throws FormsPortalException;

    /** Submits the attachment bytes passed as argument asynchronously for the user id provided in options map.
     * @param attachmentBytes would expect byte array of the attachment for this submission
     * @param options map containing options that affect this save
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachmentAsynchronously(byte[] attachmentBytes, Map<String, Object> options) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: Unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

Formulärportalen använder ett UUID-koncept (Universally Unique Identifier) för att generera ett unikt ID för varje utkast och skickat formulär. Du kan också generera ett unikt ID. Du kan implementera gränssnittet FPKeyGeneratorService, åsidosätta dess metoder och utveckla en anpassad logik för att generera ett anpassat unikt ID för varje utkast och skickat formulär. Ange också tjänstrankning för implementering av anpassad ID-generering som är högre än 0. Det ser till att den anpassade implementeringen används i stället för standardimplementeringen.

```java
public interface FPKeyGeneratorService {
    /**
     * returns a unique id for draft and submission
     *
     * @param none
     * @return unique id in string format as per the implementation
     * @throws FormsPortalException
     */
    public String getUniqueId() throws FormsPortalException;
}
```

Du kan använda anteckningen nedan för att öka rankningen för anpassade ID:n som genereras med ovanstående kod:

`@Properties(value = { @Property(name = "service.ranking", intValue = 15) } )`

Om du vill använda ovanstående kommentar importerar du följande till ditt projekt:

```
import org.apache.felix.scr.annotations.Properties;
 import org.apache.felix.scr.annotations.Property;
```

