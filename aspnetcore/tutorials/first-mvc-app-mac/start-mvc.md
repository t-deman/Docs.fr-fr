---
title: "Bien démarrer avec ASP.NET Core MVC et Visual Studio pour Mac"
author: rick-anderson
description: "Bien démarrer avec ASP.NET Core MVC et Visual Studio"
ms.author: riande
manager: wpickett
ms.date: 8/23/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app-mac/start-mvc
ms.openlocfilehash: 51c0477c40885d3aaaa7562f8baba0a94cb4f920
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="getting-started-with-aspnet-core-mvc-and-visual-studio-for-mac"></a>Bien démarrer avec ASP.NET Core MVC et Visual Studio pour Mac

Par [Rick Anderson](https://twitter.com/RickAndMSFT)

Ce didacticiel présente les principes de base de la génération d’une application web ASP.NET Core MVC à l’aide de [Visual Studio pour Mac](https://www.visualstudio.com/vs/visual-studio-mac/). 

[!INCLUDE[consider RP](../../includes/razor.md)]

Il existe trois versions de ce didacticiel :

* macOS : [Créer une application ASP.NET Core MVC avec Visual Studio pour Mac](xref:tutorials/first-mvc-app-mac/start-mvc)
* Windows : [Créer une application ASP.NET Core MVC avec Visual Studio](xref:tutorials/first-mvc-app/start-mvc)
* Linux, macOS et Windows : [Créer une application ASP.NET Core MVC avec Visual Studio Code](xref:tutorials/first-mvc-app-xplat/start-mvc)

## <a name="prerequisites"></a>Prérequis

Ce didacticiel nécessite le [SDK .NET Core 2.0.0](https://www.microsoft.com/net/core) ou version ultérieure.

Installez les éléments suivants :

- [SDK .NET Core 2.0.0 ](https://www.microsoft.com/net/core) ou version ultérieure
- [Visual Studio pour Mac](https://www.visualstudio.com/vs/visual-studio-mac/)

## <a name="create-a-web-app"></a>Créer une application web

Dans Visual Studio, sélectionnez **Fichier > Nouvelle solution**.

![macOS - Nouvelle solution](../first-web-api-mac/_static/sln.png)

Sélectionnez **Application .NET Core > ASP.NET Core > Application web > Suivant**.

![macOS - Boîte de dialogue Nouveau projet](start-mvc/1.png)

Nommez le projet **MvcMovie**, puis sélectionnez **Créer**.

![macOS - Boîte de dialogue Nouveau projet](start-mvc/2.png)

### <a name="launch-the-app"></a>Lancer l’application

Dans Visual Studio, sélectionnez **Exécuter > Exécuter sans débogage** pour lancer l’application. Visual Studio démarre [Kestrel](xref:fundamentals/servers/index#kestrel), lance un navigateur et accède à `http://localhost:port`, où *port* est un numéro de port choisi au hasard.

![Navigateur avec le nouveau projet](start-mvc/b1.png)

* La barre d’adresses affiche `localhost:port#` au lieu de quelque chose qui ressemble à `example.com`. En effet, `localhost` est le nom d’hôte standard de votre ordinateur local. Quand Visual Studio crée un projet web, un port aléatoire est utilisé pour le serveur web. Quand vous exécutez l’application, vous voyez un autre numéro de port.
* Vous pouvez lancer l’application en mode débogage ou non-débogage à partir du menu **Exécuter**.

Le modèle par défaut donne des liens **Accueil, À propos** et **Contact**. L’image de navigateur ci-dessus ne montre pas ces liens. En fonction de la taille de votre navigateur, vous devrez peut-être cliquer sur l’icône de navigation pour les afficher.

![Navigateur avec le nouveau projet](start-mvc/b2.png)

Dans la prochaine partie de ce didacticiel, vous allez découvrir MVC et commencer à écrire du code.

>[!div class="step-by-step"]
[Next](adding-controller.md)  
