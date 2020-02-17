---
title: Lägg till kommentar på exempelsida
seo-title: Lägg till kommentar på exempelsida
description: Lägga till anpassade kommentarer på en sida
seo-description: Lägga till anpassade kommentarer på en sida
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Lägg till kommentar på exempelsida {#add-comment-to-sample-page}

Nu när komponenterna för det anpassade kommentarsystemet finns på plats i programkatalogen (/apps) är det möjligt att använda den utökade komponenten. Instansen av kommentarsystemet på en webbplats som ska påverkas måste ange att dess resourceType ska vara det anpassade kommentarsystemet och innehålla alla nödvändiga klientbibliotek.

## Identifiera nödvändiga klienter {#identify-required-clientlibs}

Klientbiblioteken som är nödvändiga för att standardkommentarerna ska fungera är också nödvändiga för utökade kommentarer.

I [Community Components Guide](/help/communities/components-guide.md) identifieras nödvändiga klientbibliotek. Bläddra till komponentguiden och visa komponenten Kommentarer, till exempel:

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Observera de tre klientbiblioteken som krävs för att kommentarerna ska kunna återges och fungera korrekt. Dessa måste inkluderas där de utökade kommentarerna refereras och de [utökade kommentarernas klientbibliotek](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![chlimage_1-79](assets/chlimage_1-79.png)

### Lägga till anpassade kommentarer på en sida {#add-custom-comments-to-a-page}

Eftersom det bara kan finnas ett kommentarsystem per sida är det enklare att skapa en exempelsida enligt beskrivningen i den korta [självstudiekursen Skapa en exempelsida](/help/communities/create-sample-page.md) .

Öppna designläget och gör komponentgruppen Egen tillgänglig så att `Alt Comments` komponenten kan läggas till på sidan.

För att kommentaren ska visas och fungera på rätt sätt måste klientbiblioteken för kommentarer läggas till i klientlistorlistan för sidan (se [Klientlibs for Communities Components](/help/communities/clientlibs.md)).

#### Kommentarsklipp på exempelsida {#comments-clientlibs-on-sample-page}

![Kommentarsklipp på exempelsida](assets/chlimage_1-80.png)

#### Författare: Alt-kommentar på exempelsida {#author-alt-comment-on-sample-page}

![Alt-kommentar på exempelsida](assets/chlimage_1-81.png)

#### Författare: Exempelnod för sidkommentarer {#author-sample-page-comments-node}

Du kan verifiera resourceType i CRXDE genom att visa egenskaperna för kommentarnoden för exempelsidan på `/content/sites/sample/en/jcr:content/content/primary/comments`.

![chlimage_1-82](assets/chlimage_1-82.png)

#### Publicera exempelsida {#publish-sample-page}

När den anpassade komponenten har lagts till på sidan är det också nödvändigt att (återpublicera) [sidan](/help/communities/sites-console.md#publishing-the-site).

#### Publicera: Alt-kommentar på exempelsida {#publish-alt-comment-on-sample-page}

När du har publicerat både det anpassade programmet och exempelsidan kan du skriva en kommentar. När du är inloggad, antingen med en [demoanvändare](/help/communities/tutorials.md#demo-users) eller administratör, kan du publicera en kommentar.

Här är aaron.mcdonald@mailinator.com som publicerar en kommentar:

![chlimage_1-83](assets/chlimage_1-83.png) ![chlimage_1-84](assets/chlimage_1-84.png)

Nu när den utökade komponenten ser ut som den ska med standardutseendet är det dags att ändra utseendet.