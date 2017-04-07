---
title: Dossier CD.Latest | Microsoft Docs
description: "Découvrez le nouveau processus de mise à jour qui permet de remettre les mises à jour du produit à partir de la console Configuration Manager."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 9cbda4db3c8fcd0bc039e9bb0f490af519b7d04b
ms.lasthandoff: 03/27/2017


---
# <a name="the-cdlatest-folder-for-system-center-configuration-manager"></a>Dossier CD.Latest pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager inaugure un nouveau processus de mise à jour qui permet de remettre les mises à jour du produit à partir de la console Configuration Manager. Pour prendre en charge cette nouvelle méthode de mise à jour de Configuration Manager, un nouveau dossier est créé sous le nom **CD.Latest** : il contient une copie des fichiers d’installation de Configuration Manager pour la version mise à jour de votre site.  

À compter de la mise à jour 1606, le dossier CD.Latest contient un dossier nommé **Redist** qui contient les fichiers redistribuables téléchargés et utilisés par le programme d’installation. Ces fichiers sont mis en correspondance avec la version des fichiers de Configuration Manager dans ce dossier CD.Latest. Quand vous exécutez le programme d’installation à partir d’un dossier CD.Latest, vous devez utiliser les fichiers qui correspondent à cette version du programme d’installation. Pour ce faire, vous pouvez faire en sorte que le programme d’installation télécharge les fichiers nouveaux et existants à partir de Microsoft, ou faire en sorte qu’il utilise les fichiers présents dans le dossier Redist du dossier CD.Latest.

Toutefois, le média de base de référence, comme la version de base de référence 1606 publiée en octobre 2016, ne comprend pas de dossier Redist. Le dossier Redist n’est créé qu’au terme de l’installation d’une mise à jour dans la console. En attendant, utilisez le dossier Redist auquel vous avez eu recours lors de l’installation de sites à partir du média de base de référence.  

> [!TIP]
> Si vous n’avez pas encore installé la version 1606, vous devez vérifier que les fichiers de redistribution que vous utilisez sont à jour. Si vous n’avez pas téléchargé les fichiers de redistribution récemment, prévoyez d’autoriser le programme d’installation à le faire à partir du site web de Microsoft.   

 Vous trouverez ci-dessous des scénarios permettant de créer ou de mettre à jour le dossier CD.Latest sur un serveur de site d’administration centrale ou de site principal :  

-   Vous installez une mise à jour ou un correctif logiciel à partir de la console Configuration Manager : le dossier est créé ou mis à jour dans le dossier d’installation de Configuration Manager.  

-   Vous exécutez la tâche de sauvegarde intégrée de Configuration Manager : le dossier est créé ou mis à jour à l’emplacement du dossier de sauvegarde désigné.  

-  Depuis la version 1606, le dossier CD.Latest est créé lorsque vous installez un nouveau site en utilisant un support de la base de référence (version 1606 par exemple).

Les fichiers sources du dossier CD.Latest sont pris en charge pour les opérations suivantes :  

1.  **Sauvegarde et récupération :** pour récupérer un site, vous devez utiliser les fichiers source d’un dossier CD.Latest correspondant à votre site. Lorsque vous exécutez une sauvegarde de site à l’aide de la tâche de sauvegarde de site intégrée, le dossier CD.Latest est inclus dans le cadre de la sauvegarde.

    -   **Quand vous réinstallez le site dans le cadre d’une récupération de site** , vous installez le site à partir du dossier CD.Latest inclus dans votre sauvegarde. Cette opération installe le site à l’aide des versions de fichier correspondant à la sauvegarde et à la base de données de votre site.  Si vous n’avez pas accès à la version appropriée du dossier CD.Latest, vous pouvez obtenir un dossier CD.Latest avec les versions de fichiers appropriées en installant un site dans un environnement de laboratoire, puis en mettant à jour ce site afin qu’il corresponde à la version que vous souhaitez récupérer.

        > [!IMPORTANT]  
        >  Si le dossier CD.Latest approprié et son contenu ne sont pas disponibles, vous ne pouvez pas récupérer un site et devez le réinstaller.  

    -   Lorsque vous n’avez pas de dossier CD.Latest mais disposez d’un site principal enfant ou d’un site d’administration centrale opérationnels, vous pouvez utiliser ce site en tant que site de référence pour la récupération d’un site.  

2.  **Pour installer un site principal enfant :** quand vous souhaitez installer un nouveau site principal enfant sous un site d’administration centrale qui a installé une ou plusieurs mises à jour dans la console, vous devez utiliser le programme d’installation et les fichiers sources figurant dans le dossier CD.Latest du site d’administration centrale. Lorsque le programme d’installation s’exécute à partir d’une copie du dossier CD.Latest figurant sur le site d’administration centrale, il utilise les fichiers sources d’installation correspondant à la version du site d’administration centrale. Pour plus d’informations, consultez [Utiliser l’Assistant Installation pour installer des sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  

3.  **Pour étendre un site principal autonome :** quand vous étendez un site principal autonome en installant un nouveau site d’administration centrale, vous devez utiliser le programme d’installation et les fichiers sources figurant dans le dossier CD.Latest du site principal pour installer le nouveau site d’administration centrale. Lorsque vous exécutez à partir d’une copie du dossier CD.Latest du site principal, les fichiers sources d’installation utilisés correspondent à la version du site principal. Pour plus d’informations, consultez [Étendre un site principal autonome](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)) dans [Utiliser l’Assistant Installation pour installer des sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).

> [!IMPORTANT]  
>  Les fichiers sources mis à jour du dossier CD.Latest ne sont pas pris en charge pour les opérations suivantes :  
>   
>  -   installation d’un nouveau site pour une nouvelle hiérarchie ;  
>  -   Mise à niveau d’un site Microsoft System Center 2012 Configuration Manager vers System Center Configuration Manager

