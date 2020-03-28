---
title: OSGi Events for Communities-komponenter
seo-title: OSGi Events for Communities-komponenter
description: OSGi-händelser skickas som kan utlösa asynkrona avlyssnare
seo-description: OSGi-händelser skickas som kan utlösa asynkrona avlyssnare
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# OSGi Events for Communities-komponenter {#osgi-events-for-communities-components}

## Översikt {#overview}

När medlemmar interagerar med communityfunktioner skickas OSGi-händelser som kan utlösa asynkrona avlyssnare, som meddelanden eller spel (poängsättning och märkning).

En komponents [SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) -instans registrerar händelserna som `actions` de inträffar för en `topic`. SocialEvent innehåller en metod för att returnera en `verb` associerad åtgärd. Det finns en *n-1* -relation mellan `actions` och `verbs`.

För de webbdelar som levereras i releasen beskrivs i följande tabeller `verbs` definierade för varje `topic` tillgänglig för användning.

## Ämnen och verb {#topics-and-verbs}

[Calendar Component](calendar-basics-for-developers.md)SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en kalenderhändelse |
| LÄGG TILL | kommentarer från medlemmar i en kalenderhändelse |
| UPPDATERA | medlemmens kalenderhändelse eller -kommentar har redigerats |
| TA BORT | medlemmens kalenderhändelse eller -kommentar tas bort |

[Comments Component](essentials-comments.md)SocialEvent `topic`= com/adobe/cq/social/comment

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en kommentar |
| LÄGG TILL | medlemssvar på kommentarer |
| UPPDATERA | Medlemmens kommentar har redigerats |
| TA BORT | medlemmens kommentar har tagits bort |

[File Library Component](essentials-file-library.md)SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en mapp |
| BIFOGA | medlem överför en fil |
| UPPDATERA | medlemmen uppdaterar en mapp eller fil |
| TA BORT | medlem tar bort en mapp eller fil |

[Forum Component](essentials-forum.md)SocialEvent `topic`= com/adobe/cq/social/forum

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar forumämne |
| LÄGG TILL | medlemssvar på forumämnet |
| UPPDATERA | Medlemmens forumämne eller svar har redigerats |
| TA BORT | forumämnet eller svaret för en medlem tas bort |

[Journal Component](blog-developer-basics.md)SocialEvent `topic`= com/adobe/cq/social/journal

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en bloggartikel |
| LÄGG TILL | kommentarerna på en bloggartikel |
| UPPDATERA | Medlemmens bloggartikel eller kommentar redigeras |
| TA BORT | Medlemmens bloggartikel eller kommentar tas bort |

[QnA Component](qna-essentials.md)SocialEvent `topic` = com/adobe/cq/social/qna

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en QnA-fråga |
| LÄGG TILL | medlem skapar ett QnA-svar |
| UPPDATERA | -medlemmens fråga eller svar har redigerats |
| MARKERA | Medlemmens svar har valts |
| AVMARKERA | Medlemmens svar är avmarkerat |
| TA BORT | en medlems fråga eller svar tas bort |

[Review Component](reviews-basics.md)SocialEvent `topic`= com/adobe/cq/social/review

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar granskning |
| UPPDATERA | Medlemmens granskning har redigerats |
| TA BORT | Medlemmens granskning har tagits bort |

[Värderingskomponent](rating-basics.md)SocialEvent `topic`= com/adobe/cq/social/tally

| **Verb** | **Beskrivning** |
|---|---|
| LÄGG TILL KLASSIFICERING | Medlemmens innehåll har fått en högre gradering |
| TA BORT KLASSIFICERING | medlemmens innehåll har nedgraderats |

[Röstkomponent](essentials-voting.md)SocialEvent `topic`= com/adobe/cq/social/tally

| **Verb** | **Beskrivning** |
|---|---|
| LÄGG TILL RÖST | Medlemmens innehåll har röstats upp |
| TA BORT RÖSTNING | Medlemmens innehåll har inte röstats ned |

**Moderation-enabled Components** SocialEvent `topic`= com/adobe/cq/social/moderation

| **Verb** | **Beskrivning** |
|---|---|
| NEKA | medlemmens innehåll nekas |
| FLAGGA-SOM-OLÄMPLIGT | medlemmens innehåll är flaggat |
| OLÄMPLIG FLAGNING SOM | medlemmens innehåll är oflaggat |
| ACCEPTERA | Medlemmens innehåll godkänns av moderatorn |
| STÄNG | medlem stänger kommentarer till redigeringar och svar |
| ÖPPNA | medlem öppnar kommentaren igen |

## Händelser för anpassade komponenter {#events-for-custom-components}

För en anpassad komponent måste den abstrakta [klassen](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) SocialEvent utökas till d för att spela in komponentens händelser som `actions`de inträffar för en `topic`.

Den anpassade händelsen åsidosätter metoden `getVerb()` så att en lämplig händelse `verb`returneras för varje `action`. Den `verb` som returneras för en åtgärd kan vara en vanlig (t.ex. `POST`) eller en speciell komponent (t.ex. `ADD RATING`). Det finns en *n-1* -relation mellan `actions`och `verbs`.

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

Kräver [det senaste funktionspaketet](deploy-communities.md#latestfeaturepack).

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

