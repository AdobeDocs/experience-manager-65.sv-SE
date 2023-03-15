---
title: Lägg till kommentar på exempelsida
seo-title: Add Comment to Sample Page
description: Lägga till anpassade kommentarer på en sida
seo-description: Add Custom Comments to a page
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Lägg till kommentar på exempelsida  {#add-comment-to-sample-page}

Nu när komponenterna för det anpassade kommentarsystemet finns på plats i programkatalogen (/apps) är det möjligt att använda den utökade komponenten. Instansen av kommentarsystemet på en webbplats som ska påverkas måste ange att dess resourceType ska vara det anpassade kommentarsystemet och innehålla alla nödvändiga klientbibliotek.

## Identifiera nödvändiga klienter {#identify-required-clientlibs}

Klientbiblioteken som är nödvändiga för att standardkommentarerna ska fungera är också nödvändiga för utökade kommentarer.

The [Community Components Guide](/help/communities/components-guide.md) identifierar nödvändiga klientbibliotek. Bläddra till komponentguiden och visa komponenten Kommentarer, till exempel:

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Observera de tre klientbiblioteken som krävs för att kommentarerna ska kunna återges och fungera korrekt. Dessa måste inkluderas där de utökade kommentarerna refereras och [extended Comments klientbibliotek](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![comments-component1](assets/comments-component1.png)

### Lägga till anpassade kommentarer på en sida {#add-custom-comments-to-a-page}

Eftersom det bara kan finnas ett kommentarsystem per sida är det enklare att skapa en exempelsida enligt beskrivningen i det korta [Skapa en exempelsida](/help/communities/create-sample-page.md) självstudiekurs.

När du har skapat programmet går du till designläge och gör den anpassade komponentgruppen tillgänglig så att `Alt Comments` -komponent som ska läggas till på sidan.

För att kommentaren ska visas och fungera på rätt sätt måste klientbiblioteken för kommentarer läggas till i klientlistorlistan för sidan (se [Clientlibs for Communities Components](/help/communities/clientlibs.md)).

#### Kommentarsklipp på exempelsida {#comments-clientlibs-on-sample-page}

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### Författare: Alt-kommentar på exempelsida {#author-alt-comment-on-sample-page}

![alt-comment](assets/alt-comment.png)

#### Författare: Exempelnod för sidkommentarer {#author-sample-page-comments-node}

Du kan verifiera resourceType i CRXDE genom att visa egenskaperna för kommentarnoden för exempelsidan på `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### Publicera exempelsida {#publish-sample-page}

När den anpassade komponenten har lagts till på sidan är det också nödvändigt att (re) [publicera sidan](/help/communities/sites-console.md#publishing-the-site).

#### Publicera: Alt-kommentar på exempelsida {#publish-alt-comment-on-sample-page}

När du har publicerat både det anpassade programmet och exempelsidan kan du skriva en kommentar. Vid inloggning, antingen med [demoanvändare](/help/communities/tutorials.md#demo-users) eller admin kan du publicera en kommentar.

Här är aaron.mcdonald@mailinator.com som publicerar en kommentar:

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

Nu när den utökade komponenten ser ut som den ska med standardutseendet är det dags att ändra utseendet.
