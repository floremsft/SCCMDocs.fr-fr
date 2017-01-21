---
title: "Téléchargeur d’installation | System Center Configuration Manager"
description: "Découvrez les fonctions de cette application autonome, qui a été conçue pour vérifier que votre installation de site utilise les dernières actuelles des fichiers d’installation clés."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 574e4d450126d2c4411292b6dd52e18049d296f6

---
# <a name="setup-downloader-for-system-center-configuration-manager"></a>Téléchargeur d’installation pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant d’exécuter le programme d’installation pour installer ou mettre à niveau un site System Center Configuration Manager, vous pouvez utiliser cette application autonome (**Setupdl.exe**) de la version de Configuration Manager que vous souhaitez installer pour télécharger les fichiers d’installation mis à jour requis par le programme d’installation.  

L’utilisation des fichiers d’installation mis à jour garantit que votre installation de site utilise les dernières versions des fichiers d’installation clés :  

-   Quand vous utilisez le téléchargeur d’installation pour télécharger des fichiers avant de démarrer le programme d’installation, vous devez spécifier le dossier qui contiendra les fichiers.  

-   Le compte que vous utilisez pour exécuter le téléchargeur d’installation doit avoir des autorisations **Contrôle intégral** sur le dossier de téléchargement.  

-   Quand vous exécutez le programme d’installation pour installer ou mettre à niveau un site, vous pouvez lui demander d’utiliser cette copie locale des fichiers téléchargés précédemment. Cela évite au programme d’installation de devoir se connecter à Microsoft au démarrage de l’installation ou de la mise à niveau du site.  

-   Vous pouvez utiliser la même copie locale des fichiers d’installation pour des installations ou mises à niveau de sites ultérieures.  

Le téléchargeur d’installation télécharge les types de fichiers suivants :  

-   Fichiers redistribuables requis  

-   Modules linguistiques  

-   Dernières mises à jour de produit pour le programme d’installation  

Deux options sont possibles pour exécuter le téléchargeur d’installation :  

## <a name="run-setup-downloader-with-the-user-interface"></a>Exécuter le téléchargeur d’installation avec l’interface utilisateur  

1.  Sur un ordinateur disposant d’un accès Internet, ouvrez l’Explorateur Windows et accédez à **&lt;Média_Installation_ConfigMgr\>\SMSSETUP\BIN\X64**.  

2.  Double-cliquez sur **Setupdl.exe**. Le téléchargeur d'installation s'ouvre.  

3.  Spécifiez le chemin du dossier où seront hébergés les fichiers d’installation mis à jour, puis cliquez sur **Télécharger**. Le téléchargeur d'installation vérifie les fichiers qui se trouvent actuellement dans le dossier de téléchargement, puis télécharge uniquement les fichiers manquants ou qui sont plus récents que les fichiers existants. Le téléchargeur d'installation crée des sous-dossiers pour les langues téléchargées. Le téléchargeur d'installation crée le dossier si celui-ci n'existe pas.  

4.  Examinez les résultats du téléchargement dans le fichier **ConfigMgrSetup.log** situé à la racine du lecteur C.  

## <a name="run-setup-downloader-from-a-command-prompt"></a>Exécuter le téléchargeur d’installation à partir d’une invite de commandes  

1.  Ouvrez une fenêtre d’invite de commandes et accédez à **&lt;Média_Installation_ConfigMgr\>\SMSSETUP\BIN\X64**.  

2.  Exécutez **setupdl.exe** pour ouvrir le téléchargeur d’installation. Si vous le souhaitez, vous pouvez utiliser les options de ligne de commande suivantes avec setupdl.exe :  

    -   **/VERIFY** : utilisez cette option pour vérifier les fichiers dans le dossier de téléchargement, notamment les fichiers de langues. Examinez la liste des fichiers obsolètes dans le fichier ConfigMgrSetup.log situé à la racine du lecteur C. Aucun fichier n'est téléchargé lorsque vous utilisez cette option.  

    -   **/VERIFYLANG** : utilisez cette option pour vérifier les fichiers de langues dans le dossier de téléchargement. Examinez la liste des fichiers de langue obsolètes dans le fichier ConfigMgrSetup.log situé à la racine du lecteur C.  

    -   **/LANG** : utilisez cette option pour télécharger uniquement les fichiers de langues dans le dossier de téléchargement.  

    -   **/NOUI** : utilisez cette option pour démarrer le téléchargeur d’installation sans afficher l’interface utilisateur. Quand vous utilisez cette option, vous devez spécifier le **chemin de téléchargement** dans la ligne de commande.  

    -   **&lt;chemin_téléchargement\>** : vous pouvez spécifier le chemin du dossier de téléchargement pour démarrer automatiquement la vérification ou le processus de téléchargement. Vous devez spécifier le chemin de téléchargement quand vous utilisez l’option **/NOUI**. Si vous ne spécifiez pas un chemin de téléchargement, vous devez le faire à l'ouverture du téléchargeur d'installation. Le téléchargeur d'installation crée le dossier si celui-ci n'existe pas.  

    Exemples d'utilisation :  

    -   **setupd &lt;chemin_téléchargement\>**  

        -   Le téléchargeur d’installation démarre, vérifie les fichiers dans le dossier de téléchargement spécifié, puis télécharge uniquement les fichiers manquants ou plus récents que les fichiers existants.  

    -   **setupdl /VERIFY &lt;chemin_téléchargement\>**  

        -   Le téléchargeur d’installation démarre et vérifie les fichiers dans le dossier de téléchargement spécifié.  

    -   **setupdl /NOUI &lt;chemin_téléchargement\>**  

        -   Le téléchargeur d’installation démarre, vérifie les fichiers dans le dossier de téléchargement spécifié, puis télécharge uniquement les fichiers manquants ou plus récents que les fichiers existants.  

    -   **setupdl /LANG &lt;chemin_téléchargement\>**  

        -   Le téléchargeur d’installation démarre, vérifie les fichiers de langue dans le dossier de téléchargement spécifié, puis télécharge uniquement les fichiers de langue manquants ou plus récents que les fichiers existants.  

    -   **setupdl /VERIFY**  

        -   Le téléchargeur d'installation démarre, et vous devez alors spécifier le chemin d'accès vers le dossier de téléchargement. Ensuite, après avoir cliqué sur Vérifier, le téléchargeur d’installation vérifie les fichiers dans le dossier de téléchargement.  

3.  Examinez les résultats du téléchargement dans le fichier **ConfigMgrSetup.log** situé à la racine du lecteur C.  



<!--HONumber=Nov16_HO1-->


