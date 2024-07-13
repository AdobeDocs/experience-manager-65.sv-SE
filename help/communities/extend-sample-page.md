---
title: Lägg till kommentar på exempelsida
description: Lär dig hur en instans av en webbplats kommentarsystem måste ange att dess resourceType ska vara det anpassade kommentarsystemet och innehålla alla nödvändiga klientbibliotek.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# Lägg till kommentar på exempelsida  {#add-comment-to-sample-page}

Nu när komponenterna för det anpassade kommentarsystemet finns på plats i programkatalogen (/apps) är det möjligt att använda den utökade komponenten. Instansen av kommentarsystemet på en webbplats som ska påverkas måste ange att dess resourceType ska vara det anpassade kommentarsystemet och innehålla alla nödvändiga klientbibliotek.

## Identifiera nödvändiga klienter {#identify-required-clientlibs}

Klientbiblioteken som är nödvändiga för att standardkommentarerna ska fungera är också nödvändiga för utökade kommentarer.

[Community Components Guide](/help/communities/components-guide.md) identifierar nödvändiga klientbibliotek. Bläddra till komponentguiden och visa komponenten Kommentarer, till exempel:

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Observera de tre klientbiblioteken som krävs för att kommentarerna ska kunna återges och fungera korrekt. Dessa måste inkluderas där de utökade kommentarerna refereras och klientbiblioteket [extended Comments](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![comments-component1](assets/comments-component1.png)

### Lägga till anpassade kommentarer på en sida {#add-custom-comments-to-a-page}

Eftersom det bara kan finnas ett kommentarsystem per sida är det enklare att skapa en exempelsida enligt beskrivningen i [skapa en exempelsida](/help/communities/create-sample-page.md)-självstudiekursen.

När du har skapat filen går du till designläge och gör den tillgänglig för komponentgruppen Anpassad så att komponenten `Alt Comments` kan läggas till på sidan.

För att kommentaren ska visas och fungera på rätt sätt måste klientbiblioteken för kommentarer läggas till i klientlistorlistan för sidan (se [Klientlibs for Communities Components](/help/communities/clientlibs.md)).

#### Kommentarsklipp på exempelsida {#comments-clientlibs-on-sample-page}

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### Författare: Alt-kommentar på exempelsida {#author-alt-comment-on-sample-page}

![alt-comment](assets/alt-comment.png)

#### Författare: Exempelkommentarsnod för sida {#author-sample-page-comments-node}

Du kan verifiera resourceType i CRXDE genom att visa egenskaperna för kommentarnoden för exempelsidan på `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### Publish exempelsida {#publish-sample-page}

När den anpassade komponenten har lagts till på sidan är det också nödvändigt att (re) [publicera sidan](/help/communities/sites-console.md#publishing-the-site).

#### Publish: Alt-kommentar på exempelsida {#publish-alt-comment-on-sample-page}

När du har publicerat både det anpassade programmet och exempelsidan kan du skriva en kommentar. När du är inloggad, antingen med en [demoanvändare](/help/communities/tutorials.md#demo-users) eller administratör, kan du publicera en kommentar.

Här är aaron.mcdonald@mailinator.com en kommentar:

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

Nu när den utökade komponenten ser ut som den ska med standardutseendet är det dags att ändra utseendet.
