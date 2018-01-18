---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: "Créer un Singleton dans OData v4, à l’aide des API 2.2 Web | Documents Microsoft"
author: rick-anderson
description: "Cette rubrique montre comment définir un singleton dans un point de terminaison OData 2.2 d’API Web."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/27/2014
ms.topic: article
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 92c5056548b1e39defb28ac36f83b001dd108f5f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2017
---
<a name="create-a-singleton-in-odata-v4-using-web-api-22"></a><span data-ttu-id="e7b30-103">Créer un Singleton dans OData v4, à l’aide de Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="e7b30-103">Create a Singleton in OData v4 Using Web API 2.2</span></span>
====================
<span data-ttu-id="e7b30-104">par Zoe Luo</span><span class="sxs-lookup"><span data-stu-id="e7b30-104">by Zoe Luo</span></span>

> <span data-ttu-id="e7b30-105">En règle générale, une entité est uniquement accessible si elle a été encapsulé dans un jeu d’entités.</span><span class="sxs-lookup"><span data-stu-id="e7b30-105">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="e7b30-106">Mais OData v4 fournit deux options supplémentaires, Singleton et relation contenant-contenu, qui prend en charge WebAPI 2.2.</span><span class="sxs-lookup"><span data-stu-id="e7b30-106">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>


<span data-ttu-id="e7b30-107">Cet article explique comment définir un singleton dans un point de terminaison OData 2.2 d’API Web.</span><span class="sxs-lookup"><span data-stu-id="e7b30-107">This article shows how to define a singleton in an OData endpoint in Web API 2.2.</span></span> <span data-ttu-id="e7b30-108">Pour plus d’informations sur l’un singleton est et comment vous pouvez bénéficier de l’utiliser, consultez [à l’aide d’un singleton pour définir votre entité spéciale](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span><span class="sxs-lookup"><span data-stu-id="e7b30-108">For information on what a singleton is and how you can benefit from using it, see [Using a singleton to define your special entity](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span></span> <span data-ttu-id="e7b30-109">Pour créer un point de terminaison OData V4 dans l’API Web, consultez [créer un Using ASP.NET Web API 2.2 OData v4 point de terminaison](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="e7b30-109">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span> 

<span data-ttu-id="e7b30-110">Nous allons créer un singleton dans votre projet d’API Web à l’aide du modèle de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="e7b30-110">We'll create a singleton in your Web API project using the following data model:</span></span>

![Modèle de données](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

<span data-ttu-id="e7b30-112">Un singleton nommé `Umbrella` sont définies selon le type `Company`et une entité nommée `Employees` sont définies selon le type `Employee`.</span><span class="sxs-lookup"><span data-stu-id="e7b30-112">A singleton named `Umbrella` will be defined based on type `Company`, and an entity set named `Employees` will be defined based on type `Employee`.</span></span>

<span data-ttu-id="e7b30-113">La solution utilisée dans ce didacticiel peut être téléchargée à partir de [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span><span class="sxs-lookup"><span data-stu-id="e7b30-113">The solution used in this tutorial can be downloaded from [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span></span>

## <a name="define-the-data-model"></a><span data-ttu-id="e7b30-114">Définir le modèle de données</span><span class="sxs-lookup"><span data-stu-id="e7b30-114">Define the data model</span></span>

1. <span data-ttu-id="e7b30-115">Définir les types CLR.</span><span class="sxs-lookup"><span data-stu-id="e7b30-115">Define the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. <span data-ttu-id="e7b30-116">Générer le modèle EDM basé sur les types CLR.</span><span class="sxs-lookup"><span data-stu-id="e7b30-116">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="e7b30-117">Ici, `builder.Singleton<Company>("Umbrella")` indique le Générateur de modèles pour créer un singleton nommé `Umbrella` dans le modèle EDM.</span><span class="sxs-lookup"><span data-stu-id="e7b30-117">Here, `builder.Singleton<Company>("Umbrella")` tells the model builder to create a singleton named `Umbrella` in the EDM model.</span></span>

    <span data-ttu-id="e7b30-118">Les métadonnées générées seront présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="e7b30-118">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    <span data-ttu-id="e7b30-119">À partir des métadonnées, nous pouvons voir que la propriété de navigation `Company` dans les `Employees` jeu d’entités est lié à singleton `Umbrella`.</span><span class="sxs-lookup"><span data-stu-id="e7b30-119">From the metadata we can see that the navigation property `Company` in the `Employees` entity set is bound to the singleton `Umbrella`.</span></span> <span data-ttu-id="e7b30-120">La liaison est effectuée automatiquement par `ODataConventionModelBuilder`, étant donné que seuls `Umbrella` a le `Company` type.</span><span class="sxs-lookup"><span data-stu-id="e7b30-120">The binding is done automatically by `ODataConventionModelBuilder`, since only `Umbrella` has the `Company` type.</span></span> <span data-ttu-id="e7b30-121">S’il existe toute ambiguïté dans le modèle, vous pouvez utiliser `HasSingletonBinding` lier explicitement une propriété de navigation à un singleton ; `HasSingletonBinding` a le même effet que l’utilisation de la `Singleton` attribut dans la définition du type CLR :</span><span class="sxs-lookup"><span data-stu-id="e7b30-121">If there is any ambiguity in the model, you can use `HasSingletonBinding` to explicitly bind a navigation property to a singleton; `HasSingletonBinding` has the same effect as using the `Singleton` attribute in the CLR type definition:</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a><span data-ttu-id="e7b30-122">Définissez le contrôleur de singleton</span><span class="sxs-lookup"><span data-stu-id="e7b30-122">Define the singleton controller</span></span>

<span data-ttu-id="e7b30-123">Comme le contrôleur de l’EntitySet, le contrôleur de singleton hérite `ODataController`, et le nom du contrôleur singleton doit être `[singletonName]Controller`.</span><span class="sxs-lookup"><span data-stu-id="e7b30-123">Like the EntitySet controller, the singleton controller inherits from `ODataController`, and the singleton controller name should be `[singletonName]Controller`.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

<span data-ttu-id="e7b30-124">Afin de gérer les différents types de requêtes, les actions sont requises pour être prédéfinies dans le contrôleur.</span><span class="sxs-lookup"><span data-stu-id="e7b30-124">In order to handle different kinds of requests, actions are required to be pre-defined in the controller.</span></span> <span data-ttu-id="e7b30-125">**Attribut de routage** est activée par défaut dans WebApi 2.2.</span><span class="sxs-lookup"><span data-stu-id="e7b30-125">**Attribute routing** is enabled by default in WebApi 2.2.</span></span> <span data-ttu-id="e7b30-126">Par exemple, pour définir une action pour gérer les requêtes `Revenue` de `Company` à l’aide de routage d’attributs, utilisez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e7b30-126">For example, to define an action to handle querying `Revenue` from `Company` using attribute routing, use the following:</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

<span data-ttu-id="e7b30-127">Si vous n’êtes pas prêt définir les attributs pour chaque action, simplement définir vos actions suivant [Conventions de routage OData](../odata-routing-conventions.md).</span><span class="sxs-lookup"><span data-stu-id="e7b30-127">If you are not willing to define attributes for each action, just define your actions following [OData Routing Conventions](../odata-routing-conventions.md).</span></span> <span data-ttu-id="e7b30-128">Dans la mesure où une clé n’est pas requise pour l’interrogation d’un singleton, les actions définies dans le contrôleur de singleton sont légèrement différentes de ceux indiqués dans le contrôleur entityset.</span><span class="sxs-lookup"><span data-stu-id="e7b30-128">Since a key is not required for querying a singleton, the actions defined in the singleton controller are slightly different from actions defined in the entityset controller.</span></span>

<span data-ttu-id="e7b30-129">Pour référence, les signatures de méthode pour chaque définition de l’action dans le contrôleur de singleton sont répertoriées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e7b30-129">For reference, method signatures for every action definition in the singleton controller are listed below.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

<span data-ttu-id="e7b30-130">Cela est en fait, vous devez simplement sur le côté service.</span><span class="sxs-lookup"><span data-stu-id="e7b30-130">Basically, this is all you need to do on the service side.</span></span> <span data-ttu-id="e7b30-131">Le [exemple de projet](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) contient tout le code pour la solution et le client OData qui montre comment utiliser le singleton.</span><span class="sxs-lookup"><span data-stu-id="e7b30-131">The [sample project](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) contains all of the code for the solution and the OData client that shows how to use the singleton.</span></span> <span data-ttu-id="e7b30-132">Le client est construit en suivant les étapes dans [créer une application de Client OData v4](create-an-odata-v4-client-app.md).</span><span class="sxs-lookup"><span data-stu-id="e7b30-132">The client is built by following the steps in [Create an OData v4 Client App](create-an-odata-v4-client-app.md).</span></span>

<span data-ttu-id="e7b30-133">.</span><span class="sxs-lookup"><span data-stu-id="e7b30-133">.</span></span> 

<span data-ttu-id="e7b30-134">*Merci d’avoir à Leo Hu pour le contenu d’origine de cet article.*</span><span class="sxs-lookup"><span data-stu-id="e7b30-134">*Thanks to Leo Hu for the original content of this article.*</span></span>