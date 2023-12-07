---
title: OSGi Events for Communities-komponenter
description: OSGi-händelser skickas som kan utlösa asynkrona avlyssnare
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8049d797-e758-44c2-a89b-51d2b2fca8dc
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# OSGi Events for Communities-komponenter  {#osgi-events-for-communities-components}

## Ökning {#overview}

När medlemmar interagerar med communityfunktioner skickas OSGi-händelser som kan utlösa asynkrona avlyssnare, som meddelanden eller spel (poängsättning och märkning).

En komponents [SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) -instansen registrerar händelserna som `actions` som inträffar för en `topic`. SocialEvent innehåller en metod för att returnera en `verb` som är associerad med åtgärden. Det finns en *n-1* relation mellan `actions` och `verbs`.

Följande tabeller beskriver webbkomponenterna i den publicerade versionen `verbs` definierad för varje `topic` som kan användas.

## Ämnen och verb {#topics-and-verbs}

[Kalenderkomponent](calendar-basics-for-developers.md)
SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verb** | **Beskrivning** |
|---|---|
| POST | Medlemmen skapar en kalenderhändelse |
| LÄGG TILL | Kommentarer från en kalenderhändelse |
| UPPDATERA | Medlemmens kalenderhändelse eller kommentar har redigerats |
| DELETE | Medlemmens kalenderhändelse eller kommentar tas bort |

[Kommentarskomponent](essentials-comments.md)
SocialEvent `topic`= com/adobe/cq/social/comment

| **Verb** | **Beskrivning** |
|---|---|
| POST | Medlemmen skapar en kommentar |
| LÄGG TILL | Medlemmens svar på kommentarer |
| UPPDATERA | Medlemmens kommentar har redigerats |
| DELETE | Medlemmens kommentar har tagits bort |

[Filbibliotekskomponent](essentials-file-library.md)
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **Verb** | **Beskrivning** |
|---|---|
| POST | Medlemmen skapar en mapp |
| BIFOGA | Medlemmen överför en fil |
| UPPDATERA | Medlemmen uppdaterar en mapp eller fil |
| DELETE | Medlemmen tar bort en mapp eller fil |

[Forum-komponent](essentials-forum.md)
SocialEvent `topic`= com/adobe/cq/social/forum

| **Verb** | **Beskrivning** |
|---|---|
| POST | Medlem skapar forumämne |
| LÄGG TILL | Medlemmens svar på forumämnet |
| UPPDATERA | Ämnet eller svaret på en medlems forum redigeras |
| DELETE | Ämnet eller svaret för en medlem tas bort |

[Journalkomponent](blog-developer-basics.md)
SocialEvent `topic`= com/adobe/cq/social/journal

| **Verb** | **Beskrivning** |
|---|---|
| POST | Medlemmen skapar en bloggartikel |
| LÄGG TILL | Kommentarer till en bloggartikel |
| UPPDATERA | Medlemmens bloggartikel eller kommentar redigeras |
| DELETE | Medlemmens bloggartikel eller kommentar tas bort |

[QnA-komponent](qna-essentials.md)
SocialEvent `topic` = com/adobe/cq/social/qna

| **Verb** | **Beskrivning** |
|---|---|
| POST | Medlemmen skapar en QnA-fråga |
| LÄGG TILL | Medlem skapar ett QnA-svar |
| UPPDATERA | Medlemsens fråga eller svar har redigerats |
| MARKERA | Medlemmens svar har valts |
| AVMARKERA | Medlemmens svar har avmarkerats |
| DELETE | Medlemsens fråga eller svar tas bort |

[Granskningskomponent](reviews-basics.md)
SocialEvent `topic`= com/adobe/cq/social/review

| **Verb** | **Beskrivning** |
|---|---|
| POST | Medlemmen skapar en granskning |
| UPPDATERA | Medlemmens granskning har redigerats |
| DELETE | Medlemmens granskning har tagits bort |

[Värderingskomponent](rating-basics.md)
SocialEvent `topic`= com/adobe/cq/social/tally

| **Verb** | **Beskrivning** |
|---|---|
| LÄGG TILL KLASSIFICERING | Medlemmens innehåll har fått ett högre omdöme |
| TA BORT KLASSIFICERING | Medlemmens innehåll har nedgraderats |

[Röstkomponent](essentials-voting.md)
SocialEvent `topic`= com/adobe/cq/social/tally

| **Verb** | **Beskrivning** |
|---|---|
| LÄGG TILL RÖST | Medlemmens innehåll har röstats upp |
| TA BORT RÖSTNING | Medlemmens innehåll har inte röstats ned |

**Modereringsaktiverade komponenter**
SocialEvent `topic`= com/adobe/cq/social/moderation

| **Verb** | **Beskrivning** |
|---|---|
| NEKA | Medlemmens innehåll nekas |
| FLAGGA-SOM-OLÄMPLIGT | Medlemmens innehåll är flaggat |
| OLÄMPLIG FLAGNING SOM | Medlemmens innehåll är oflaggat |
| GODKÄNN | Medlemmens innehåll godkänns av moderatorn |
| STÄNG | Medlemmen stänger kommentarer till redigeringar och svar |
| ÖPPNA | Kommentar för att öppna igen |

## Händelser för anpassade komponenter {#events-for-custom-components}

För en anpassad komponent [Den abstrakta klassen SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) måste utökas d för att spela in komponentens händelser som `actions`som inträffar för en `topic`.

Den anpassade händelsen skulle åsidosätta metoden `getVerb()` så att `verb`returneras för varje `action`. The `verb` som returneras för en åtgärd kan vara en vanlig åtgärd (t.ex. `POST`) eller en som är specialiserad på komponenten (till exempel `ADD RATING`). Det finns en *n-1* relation mellan `actions`och `verbs`.

>[!NOTE]
>
>Se till att ett anpassat tillägg är registrerat med en lägre rankning än någon befintlig implementering i produkten.

### Pseudokod för anpassad komponenthändelse {#pseudo-code-for-custom-component-event}

[org.osgi.service.event.Event](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);
[com.adobe.cq.social.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html);
[com.adobe.granite.activitystreams.ObjectTypes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html);
[com.adobe.granite.activitystreams.Verbs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/Verbs.html);

```java
package com.mycompany.recipe;

import org.osgi.service.event.Event;
import com.adobe.cq.social.scf.core.SocialEvent;
import com.adobe.granite.activitystreams.ObjectTypes;
import com.adobe.granite.activitystreams.Verbs;

/*
 * The Recipe type, passed to RecipeEvent(), would be a custom Recipe class
 * that extends either
 * com.adobe.cq.social.scf.SocialComponent
 * or
 * com.adobe.cq.social.scf.SocialCollectionComponent
 * See https://docs.adobe.com/docs/en/aem/6-2/develop/communities/scf/server-customize.html
 */

/**
 * Defines events that are triggered on a custom component, "Recipe".
 */
public class RecipeEvent extends SocialEvent<RecipeEvent.RecipeActions> {

    private static final long serialVersionUID = 1L;
    protected static final String PARENT_PATH = "PARENT_PATH";

    /**
     * The event topic suffix for Recipe events
     */
    public static final String RECIPE_TOPIC = "recipe";

    /**
     * @param recipe - the recipe resource on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final Recipe recipe, final String userId, final RecipeEvent.RecipeActions action) {
        String recipePath = recipe.getResource().getPath();
        String parentPath = (recipe.getParentComponent() != null) ?
                             recipe.getParentComponent().getResource().getPath() :
                             recipe.getSourceComponentId();
        this(recipePath, userId, parentPath, action);
    }

    /**
     * @param recipePath - the path to the recipe resource (jcr node) on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param parentPath - the path to the parent node of the recipe resource
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final String recipePath, final String userId, final String parentPath) {
        super(RECIPE_TOPIC, recipePath, userId, action,
              new BaseEventObject(recipePath, ObjectTypes.ARTICLE),
              new BaseEventObject(parentPath, ObjectTypes.COLLECTION),
              new HashMap<String, Object>(1) {
            private static final long serialVersionUID = 1L;
            {
                if (parentPath != null) {
                    this.put(PARENT_PATH, parentPath);
                }

            }
        });
    }

    private RecipeEvent (final Event event) {
      super(event);
    }

    /**
     * List of available recipe actions that can trigger a recipe event.
     */
    public static enum RecipeActions implements SocialEvent.SocialActions {
        RecipeAdded,
        RecipeModified,
        RecipeDeleted;

        @Override
        public String getVerb() {
            switch (this) {
                case RecipeAdded:
                    return Verbs.POST;
                case RecipeModified:
                    return Verbs.UPDATE;
                case RecipeDeleted:
                    return Verbs.DELETE;
                default:
                    throw new IllegalArgumentException("Unsupported action");
            }
        }
    }

}
```

## Exempel på EventListener för att filtrera aktivitetsströmdata {#sample-eventlistener-to-filter-activity-stream-data}

Det går att lyssna på händelser i syfte att ändra vad som visas i aktivitetsströmmen.

Följande pseudokodsexempel tar bort DELETE-händelser för komponenten Comments från aktivitetsströmmen.

### Pseudokod för EventListener {#pseudo-code-for-eventlistener}

Kräver [senaste funktionspaketet](deploy-communities.md#latestfeaturepack).

```java
package my.company.comments;

import java.util.Collections;
import java.util.Map;

import org.apache.commons.lang.StringUtils;
import org.apache.felix.scr.annotations.Activate;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Modified;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.osgi.PropertiesUtil;
import org.osgi.service.component.ComponentContext;

import com.adobe.cq.social.activitystreams.listener.api.ActivityStreamProviderExtension;
import com.adobe.cq.social.commons.events.CommentEvent.CommentActions;
import com.adobe.cq.social.scf.core.SocialEvent;

@Service
@Component(metatype = true, label = "My Comment Delete Event Filter",
        description = "Prevents comment DELETE events from showing up in activity streams")
public class CommentDeleteEventActivityFilter implements ActivityStreamProviderExtension {

    @Property(name = "ranking", intValue = 10)
    protected int ranking;

    @Activate
    public void activate(final ComponentContext ctx) {
        ranking = PropertiesUtil.toInteger(ctx.getProperties().get("ranking"), 10);
    }

    @Modified
    public void update(final Map<String, Object> props) {
        ranking = PropertiesUtil.toInteger(props.get("ranking"), 10);
    }

    @Override
    public boolean evaluate(final SocialEvent<?> evt, final Resource resource) {
        if (evt.getAction() != null && evt.getAction() instanceof SocialEvent.SocialActions) {
            final SocialEvent.SocialActions action = evt.getAction();
            if (StringUtils.equals(action.getVerb(), CommentActions.DELETED.getVerb())) {
                return false;
            }
        }
        return true;
    }

    @Override
    public Map<String, ? extends Object> getActivityProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public Map<String, ? extends Object> getActorProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String getName() {
        return "My Comment Delete Event Filter";
    }

    @Override
    public Map<String, ? extends Object> getObjectProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    /* Ensure a custom extension is registered with a ranking lower than any existing implementation in the product. */
    @Override
    public int getRanking() {
        return this.ranking;
    }

    @Override
    public Map<String, ? extends Object> getTargetProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String[] getStreamProviderPid() {
        return new String[]{"*"};
    }

}
```
