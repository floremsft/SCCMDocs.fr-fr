---
title: "Gérer les images de démarrage - Configuration Manager | Microsoft Docs"
description: "Découvrez comment utiliser Configuration Manager pour gérer les images de démarrage Windows PE que vous utilisez pendant un déploiement de système d’exploitation."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
caps.latest.revision: 23
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 70034213442f4c3d5a28ab65c2ceb51aa64320ad
ms.openlocfilehash: 207975538b63390fb5789b19c519db89db62e0a5
ms.lasthandoff: 03/31/2017


---
# <a name="manage-boot-images-with-system-center-configuration-manager"></a>Gérer les images de démarrage avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une image de démarrage dans Configuration Manager est une image [Windows PE (WinPE)](https://msdn.microsoft.com/library/windows/hardware/dn938389%28v=vs.85%29.aspx) utilisée pendant un déploiement de système d’exploitation. Les images de démarrage servent à démarrer un ordinateur dans WinPE, qui est un système d’exploitation minimal avec des composants et des services limités qui préparent l’ordinateur de destination pour l’installation de Windows.  Aidez-vous des informations des sections suivantes pour gérer les images de démarrage.

##  <a name="BKMK_BootImageDefault"></a> Images de démarrage par défaut  
À compter de la version 1702, quand vous mettez à niveau la version du Windows ADK et qu’ensuite vous mettez à jour Configuration Manager avec la dernière version, les images de démarrage par défaut sont mises à jour. Ceci inclut la nouvelle version de Windows PE du Windows ADK mis à jour et la nouvelle version du client Configuration Manager. Toutes les personnalisations restent inchangées. Les images de démarrage personnalisées ne sont pas mises à jour. Avant la version 1702, vous deviez mettre à jour manuellement l’image de démarrage pour utiliser la nouvelle version du Windows ADK.

Quand vous mettez à niveau Configuration Manager vers une nouvelle version majeure par le biais du processus d’installation, Configuration Manager peut mettre à jour les images de démarrage par défaut, ainsi que les images de démarrage personnalisées basées sur les images de démarrage par défaut stockées dans l’emplacement par défaut.

Les options que vous configurez sur les images de démarrage par défaut au niveau du site (par exemple, des composants facultatifs) sont transmises lors de la mise à jour des images de démarrage, dont les pilotes. Les objets pilotes de source doivent être valides, notamment les fichiers sources de pilotes. Autrement, les pilotes ne seront pas ajoutés aux images de démarrage mises à jour sur le site. Les autres images de démarrage non basées sur les images de démarrage par défaut, même si elles sont basées sur la même version de Windows ADK, ne sont pas mises à jour. Une fois les images de démarrage mises à jour, vous devez les redistribuer aux points de distribution. Tout support utilisant les images de démarrage doit être recréé. Si vous ne souhaitez pas que vos images de démarrage par défaut/personnalisées soient automatiquement mises à jour, vous devez les stocker à un autre emplacement.  


## <a name="BKMK_BootImageDefault"></a> Images de démarrage par défaut
Configuration Manager fournit deux images de démarrage par défaut : une pour la prise en charge des plateformes x86 et une autre pour la prise en charge des plateformes x64. Ces images sont stockées dans le dossier \\\\*nom_serveur*>\SMS_<*code_site*>\osd\boot\\<*x64*> ou <*i386*>. Les images de démarrage par défaut sont mises à jour ou régénérées selon l’action que vous effectuez.

**Utiliser les mises à jour et la maintenance pour installer la dernière version de Configuration Manager** À compter de la version 1702, quand vous mettez à niveau la version du Windows ADK et que vous utilisez les mises à jour et la maintenance pour installer la dernière version de Configuration Manager, ce dernier régénère les images de démarrage par défaut. Ceci inclut la nouvelle version de Windows PE du Windows ADK mis à jour, la nouvelle version du client Configuration Manager, les pilotes, les personnalisations, etc. Les images de démarrage personnalisées ne sont pas modifiées. 

Avant la version 1702, Configuration Manager mettait à jour l’image de démarrage existante (boot.wim) avec les composants du client, les pilotes, les personnalisations, etc. Toutefois, il n’utilisait pas la dernière version de Windows PE du Windows ADK. Vous deviez modifier manuellement l’image de démarrage pour utiliser la nouvelle version du Windows ADK.

**Mise à niveau de Configuration Manager 2012 vers Configuration Manager Current Branch (CB)** Quand vous mettez à niveau Configuration Manager 2012 vers Configuration Manager CB par le biais du processus d’installation, Configuration Manager régénère les images de démarrage par défaut. Ceci inclut la nouvelle version de Windows PE du Windows ADK mis à jour et la nouvelle version du client Configuration Manager. Toutes les personnalisations restent inchangées. Les images de démarrage personnalisées ne sont pas modifiées.

**Mettre à jour les points de distribution avec l’image de démarrage** Quand vous utilisez l’action **Mettre à jour les points de distribution** à partir du nœud **Images de démarrage** dans la console Configuration Manager, Configuration Manager met à jour les images de démarrage par défaut avec les composants du client, les pilotes, les personnalisations, etc. Toutefois, il n’utilise pas la dernière version de Windows PE du Windows ADK. Les images de démarrage personnalisées ne sont pas modifiées.

Pour toute action indiquée ci-dessus, tenez également compte de ce qui suit :
- Les objets de pilotes de source doivent être valides, notamment les fichiers sources des pilotes. Sinon, les pilotes ne sont pas ajoutés aux images de démarrage sur le site.
- Les images de démarrage non basées sur les images de démarrage par défaut, même si elles utilisent la même version de Windows ADK, ne sont pas modifiées.
- Vous devez redistribuer les images de démarrage modifiées aux points de distribution.
- Vous devez recréer tous les médias qui utilisent les images de démarrage modifiées.
- Si vous ne souhaitez pas que vos images de démarrage personnalisées/par défaut soient automatiquement mises à jour, ne les stockez pas à l’emplacement par défaut.

> [!NOTE]
> L’outil Journal de suivi de Configuration Manager est ajouté à toutes les images de démarrage que vous ajoutez à la **bibliothèque de logiciels**. Quand vous êtes dans Windows PE, vous pouvez démarrer l’outil Journal de suivi de Configuration Manager en tapant **CMTrace** à partir d’une invite de commandes.  

##  <a name="BKMK_BootImageCustom"></a> Personnaliser une image de démarrage  
 Vous pouvez personnaliser ou [modifier une image de démarrage](#BKMK_ModifyBootImages) depuis la console Configuration Manager si cette image est basée sur une version de Windows PE de la version prise en charge de Windows ADK. Quand un site est mis à niveau avec une nouvelle version et qu’une nouvelle version de Windows ADK est installée, les images de démarrage personnalisées (ne figurant pas dans l’emplacement d’image de démarrage par défaut) ne sont pas mises à jour avec la nouvelle version de Windows ADK. Dans ce cas, vous ne pouvez plus personnaliser les images de démarrage dans la console Configuration Manager. En revanche, elles continuent à fonctionner comme avant la mise à niveau.  

 Quand une image de démarrage est basée sur une autre version de Windows ADK installée sur un site, vous devez personnaliser les images de démarrage à l’aide d’une autre méthode, par exemple en vous servant de l’outil de ligne de commande Gestion et maintenance des images de déploiement (DISM) intégré dans Windows AIK et Windows ADK. Pour plus d’informations, consultez [Personnaliser les images de démarrage](customize-boot-images.md).  

##  <a name="BKMK_AddBootImages"></a> Ajouter une image de démarrage  

 Au moment de l’installation du site, Configuration Manager ajoute automatiquement des images de démarrage qui sont basées sur une version de WinPE de la version prise en charge de Windows ADK. Dans certaines versions de Configuration Manager, vous pouvez ajouter des images de démarrage basées sur une version de WinPE différente de la version prise en charge de Windows ADK.  Une erreur se produit si vous essayez d’ajouter une image de démarrage qui contient une version non prise en charge de WinPE.  

 Vous trouverez ci-dessous des informations sur la version prise en charge de Windows ADK, la version de Windows PE sur laquelle l’image de démarrage est basée et qui peut être personnalisée à partir de la console Configuration Manager, ainsi que les versions de Windows PE sur lesquelles l’image de démarrage est basée et que vous pouvez personnaliser à l’aide de DISM avant d’ajouter l’image à Configuration Manager.  

-   **Version de Windows ADK**  

     Windows ADK pour Windows 10  

-   **Versions de Windows PE pour les images de démarrage personnalisables à partir de la console Configuration Manager**  

     Windows PE 10  

-   **Versions prises en charge de Windows PE pour les images de démarrage non personnalisables à partir de la console Configuration Manager**  

     Windows PE 3.1<sup>1</sup> et Windows PE 5  

     <sup>1</sup> Vous pouvez ajouter une image de démarrage à Configuration Manager uniquement si elle est basée sur Windows PE 3.1. Installez le supplément Windows AIK pour Windows 7 SP1 pour mettre à niveau Windows AIK pour Windows 7 (basé sur Windows PE 3) avec le supplément Windows AIK pour Windows 7 SP1 (basé sur Windows PE 3.1). Vous pouvez télécharger le supplément Windows AIK pour Windows 7 SP1 depuis le [Centre de téléchargement Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

     Par exemple, si vous utilisez Configuration Manager, vous pouvez personnaliser les images de démarrage de Windows ADK pour Windows 10 (basées sur Windows PE 10) depuis la console Configuration Manager. Toutefois, si les images de démarrage basées sur Windows PE 5 sont prises en charge, vous devez les personnaliser depuis un autre ordinateur et utiliser la version de DISM installée avec Windows ADK pour Windows 8. Ensuite, vous pouvez ajouter l’image de démarrage à la console Configuration Manager. Pour plus d’informations sur la procédure à suivre pour personnaliser une image de démarrage (ajouter des composants et pilotes facultatifs), activer la prise en charge des commandes pour l’image de démarrage, ajouter l’image de démarrage à la console Configuration Manager et mettre à jour les points de distribution avec l’image de démarrage, consultez [Personnaliser les images de démarrage](customize-boot-images.md).

 Pour ajouter une image de démarrage manuellement, procédez comme suit.  

#### <a name="to-add-a-boot-image"></a>Pour ajouter une image de démarrage  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Images de démarrage**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Ajouter une image de démarrage** pour démarrer l'Assistant Ajout d'une image de démarrage.  

4.  Sur la page **Source de données** , spécifiez les options suivantes et cliquez sur **Suivant**.  

    -   Dans la zone **Chemin d'accès** , indiquez le chemin d'accès au fichier WIM de l'image de démarrage.  

         Le chemin d'accès spécifié doit être un chemin d'accès réseau valide au format UNC. Exemple : \\\\<*nom_serveur*\\<*nom_partage*>\\<*nom_image_démarrage*>.wim.  

    -   Sélectionnez l'image de démarrage dans la liste déroulante **Image de démarrage** . Si le fichier WIM contient plusieurs images de démarrage, sélectionnez l’image appropriée.  

5.  Dans la page **Général**  , spécifiez les options suivantes et cliquez sur **Suivant**.  

    -   Dans la zone **Nom** , spécifiez un nom unique pour l'image de démarrage.  

    -   Dans la zone **Version** , spécifiez un numéro de version pour l'image de démarrage.  

    -   Dans la zone **Commentaire** , spécifiez une description sommaire de l'utilisation de l'image de démarrage.  

6.  Effectuez toutes les étapes de l'Assistant.  

 L’image de démarrage est maintenant répertoriée dans le nœud **Image de démarrage** de la console Configuration Manager. Toutefois, avant de pouvoir utiliser l'image de démarrage pour déployer un système d'exploitation, vous devez la distribuer sur des points de distribution, des groupes de points de distribution ou des regroupements associés à des groupes de points de distribution.  

> [!NOTE]  
>  Quand vous sélectionnez le nœud **Image de démarrage** dans la console Configuration Manager, la colonne **Taille (Ko)** affiche la taille décompressée de chaque image de démarrage. Toutefois, quand Configuration Manager envoie une image de démarrage via le réseau, il envoie en fait une copie compressée de l’image, qui est généralement beaucoup plus petite que la taille indiquée dans la colonne **Taille (Ko)**.  

##  <a name="BKMK_DistributeBootImages"></a> Distribuer des images de démarrage à un point de distribution  
 Les images de démarrage sont distribuées aux points de distribution de la même façon que vous distribuez d'autre contenu. Dans la plupart des cas, vous devez distribuer l’image de démarrage à au moins un point de distribution avant de déployer un système d’exploitation et de créer des médias.  

> [!NOTE]  
>  Pour utiliser PXE pour déployer un système d’exploitation, considérez les éléments suivants avant de distribuer l’image de démarrage :  
>   
>  -   Le point de distribution doit être configuré pour accepter les demandes PXE.  
> -   Vous devez distribuer une image de démarrage PXE x86 et une image de démarrage PXE x64 à au moins un point de distribution PXE.  
> -   Configuration Manager distribue les images de démarrage vers le dossier **RemoteInstall** du point de distribution compatible PXE.  
>   
>  Pour plus d’informations sur l’utilisation de PXE pour déployer des systèmes d’exploitation, consultez [Utiliser PXE pour déployer Windows sur le réseau](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Pour découvrir comment distribuer une image de démarrage, consultez [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).  

##  <a name="BKMK_ModifyBootImages"></a> Modifier une image de démarrage  
 Vous pouvez ajouter des pilotes de périphérique à l’image de démarrage, en supprimer de celle-ci ou modifier les propriétés associées à l’image. Les pilotes de périphérique que vous ajoutez ou supprimez peuvent inclure des pilotes de périphérique de stockage de masse ou de cartes réseau. Quand vous modifiez des images de démarrage, tenez compte des facteurs suivants :  

-   Vous devez importer et activer les pilotes de périphérique dans le catalogue de pilotes de périphérique avant de les ajouter à l’image de démarrage.  

-   Quand vous modifiez une image de démarrage, cette image ne modifie aucun des packages associés auxquels l’image de démarrage fait référence.  

-   Après avoir modifié une image de démarrage, vous devez la **mettre à jour** sur les points de distribution où elle se trouve déjà afin que la version la plus récente de l’image de démarrage soit disponible. Pour plus d’informations, voir [Manage content you have distributed](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkmanagea-manage-the-content-you-have-distributed).  

 Utilisez la procédure suivante pour modifier une image de démarrage.  

#### <a name="to-modify-the-properties-of-a-boot-image"></a>Pour modifier les propriétés d'une image de démarrage  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Images de démarrage**.  

3.  Sélectionnez l'image de démarrage à modifier.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés** pour ouvrir la boîte de dialogue **Propriétés** de l'image de démarrage.  

5.  Définissez les paramètres suivants pour modifier le comportement de l'image de démarrage :  

    -   Dans l'onglet **Images** , si vous avez modifié les propriétés de l'image de démarrage à l'aide d'un outil externe, cliquez sur **Recharger**.  

    -   Sous l’onglet **Pilotes** , ajoutez les pilotes de périphérique Windows nécessaires pour démarrer WinPE. Lorsque vous ajoutez des pilotes de périphérique, considérez les éléments suivants :  

        -   Sélectionnez **Masquer les pilotes qui ne correspondent pas à l’architecture de l’image de démarrage** pour afficher uniquement les pilotes de l’architecture de l’image de démarrage. L'architecture est basée sur l'architecture signalée dans le fichier .INF du fabricant.  

        -   Sélectionnez **Masquer les pilotes hors classe de stockage ou réseau (pour les images de démarrage)** pour n’afficher que les pilotes réseau et de stockage, et masquer les autres pilotes qui ne sont généralement pas nécessaires pour les images de démarrage, tels que les pilotes vidéo ou les pilotes de modem.  

        -   Sélectionnez **Masquer les pilotes qui ne sont pas signés numériquement** pour masquer les pilotes qui ne sont pas signés numériquement.  

        -   Nous vous conseillons de n’ajouter que des cartes réseau et des pilotes de stockage de masse à l’image de démarrage sauf s’il existe des exigences pour que d’autres pilotes fassent partie de WinPE.  

        -   Dans la mesure où WinPE est déjà fourni avec de nombreux pilotes intégrés, ajoutez uniquement les cartes réseau et les pilotes de stockage de masse qui ne sont pas fournis par WinPE.  

        -   Assurez-vous que les pilotes que vous ajoutez à l’image de démarrage correspondent à l’architecture de l’image de démarrage.  

        > [!NOTE]  
        >  Vous devez importer les pilotes de périphérique dans le catalogue de pilotes avant de les ajouter à une image de démarrage. Pour plus d’informations sur l’importation de pilotes de périphérique, consultez [Gérer les pilotes](manage-drivers.md).  

    -   Dans l'onglet **Personnalisation** , sélectionnez l'un des paramètres suivants :  

        -   Activez la case à cocher **Activer une commande de prédémarrage** pour spécifier une commande à exécuter avant l'exécution de la séquence de tâches. Lorsque des commandes de prédémarrage sont activées, vous pouvez spécifier la ligne de commande exécutée, si des fichiers de support sont requis pour exécuter la commande et l'emplacement source de ces fichiers de support.  

            > [!WARNING]  
            >  Vous devez ajouter **cmd /c** au début de la ligne de commande. Si vous ne spécifiez pas **cmd /c**, la commande ne se ferme pas après son exécution. Le déploiement continue à attendre que l’exécution de la commande s’achève, et ne démarre aucune autre commande ou action configurées.  

            > [!TIP]  
            >  Lors de la création du média de séquence de tâches, la séquence de tâches écrit l’ID du package et la ligne de commande de prédémarrage, y compris la valeur des variables de la séquence de tâches, dans le fichier journal CreateTSMedia.log sur l’ordinateur qui exécute la console Configuration Manager. Vous pouvez consulter ce fichier journal pour vérifier la valeur des variables de séquence de tâches.  

        -   Définissez les paramètres **Arrière-plan Windows PE** pour spécifier si vous souhaitez utiliser l’arrière-plan de WinPE par défaut ou un arrière-plan personnalisé.  

        -   Sélectionnez **Activer la prise en charge des commandes (test uniquement)** pour ouvrir une invite de commande à l’aide de la touche **F8** durant le déploiement de l’image de démarrage. Ceci est utile pour la résolution des problèmes alors que vous testez votre déploiement. Il n'est pas conseillé d'utiliser ce paramètre dans un déploiement de production.  

        -   Configurez l’espace de travail de l’image Windows PE, qui correspond au stockage temporaire (disque RAM) utilisé par WinPE. Par exemple, quand une application est exécutée dans WinPE et doit écrire des fichiers temporaires, WinPE redirige les fichiers vers l’espace de travail en mémoire afin de simuler la présence d’un disque dur. Par défaut, WinPE alloue 32 mégaoctets (Mo) de mémoire inscriptible.  

    -   Dans l'onglet **Source de données** , mettez à jour les paramètres suivants :  

        -   Définissez **Chemin d’accès à l’image** et **Index d’images** pour modifier le fichier source de l’image de démarrage.  

        -   Sélectionnez **Mettre à jour les points de distribution soumis à un calendrier** pour créer un calendrier durant la mise à jour de l’image de démarrage.  

        -   Sélectionnez **Conserver le contenu dans la mémoire cache du client** si vous ne voulez pas que le contenu de ce package expire dans la mémoire cache du client pour faire de la place pour d’autre contenu.  

        -   Sélectionnez **Activer la réplication différentielle binaire** pour spécifier que seuls les fichiers modifiés sont distribués pendant la mise à jour du package d’images de démarrage sur le point de distribution. Ce paramètre réduit le trafic réseau entre les sites, particulièrement pour les packages d'images de démarrage volumineux présentant peu de modifications.  

        -   Si l’image de démarrage est utilisée dans un déploiement compatible PXE, sélectionnez **Déployer cette image de démarrage depuis le point de distribution PXE**.  

            > [!NOTE]  
            >  Pour plus d’informations, consultez [Utiliser PXE pour déployer Windows sur le réseau](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   Dans l'onglet **Accès aux données** , sélectionnez l'un des paramètres suivants :  

        -   Définissez les **Paramètres de partage de package** si vous voulez que les clients installent le contenu dans ce package à partir du réseau.  

        -   Définissez les **Paramètres de mise à jour de package** pour spécifier de quelle manière Configuration Manager déconnecte les utilisateurs du point de distribution. Il est possible que Configuration Manager ne puisse pas mettre à jour l’image de démarrage quand des utilisateurs sont connectés au point de distribution.  

    -   Dans l'onglet **Paramètres de distribution** , sélectionnez l'un des paramètres suivants :  

        -   Dans la liste **Priorité de distribution**, spécifiez le niveau de priorité que vous voulez que Configuration Manager utilise quand plusieurs packages sont distribués vers le même point de distribution.  

        -   Sélectionnez **Distribuer le contenu pour ce package vers les points de distribution préférés** si vous voulez activer la distribution de contenu à la demande vers des points de distribution préférés. Lorsque ce paramètre est activé, le point de gestion distribue le contenu à tous les points de distribution préférés lorsqu'un client demande le contenu pour le package et que le contenu n'est disponible sur aucun point de distribution préféré.  

        -   Définissez les **Paramètres du point de distribution préparé** pour spécifier la manière dont l'image de démarrage doit être distribuée vers les points de distribution activés pour le contenu préparé.  

            > [!NOTE]  
            >  Pour plus d’informations sur le contenu préparé, consultez [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content).  

    -   Dans l'onglet **Emplacements du contenu** , sélectionnez le point de distribution ou le groupe de points de distribution et effectuez l'une des actions suivantes :  

        -   Cliquez sur **Redistribuer** pour distribuer à nouveau l'image de démarrage vers le point de distribution ou le groupe de points de distribution sélectionné.  

        -   Cliquez sur **Valider** pour vérifier l'intégrité du package d'images de démarrage sur le point de distribution ou le groupe de points de distribution sélectionné.  

    -   Sous l’onglet **Composants facultatifs**, spécifiez les composants à ajouter à Windows PE pour être utilisés avec Configuration Manager. Pour plus d’informations sur les composants facultatifs disponibles, consultez [WinPE : Ajouter des packages (informations de référence sur les composants facultatifs)](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx).  

    -   Dans l'onglet **Sécurité** , sélectionnez un utilisateur administratif et modifiez les opérations qu'il peut effectuer.  

6.  Après avoir configuré les propriétés, cliquez sur **OK**.  

##  <a name="BKMK_BootImagePXE"></a> Configurer une image de démarrage pour un déploiement à partir d’un point de distribution PXE  
 Avant de pouvoir utiliser une image de démarrage pour un déploiement de système d’exploitation PXE, vous devez configurer l’image de démarrage pour un déploiement à partir d’un point de distribution PXE.  

#### <a name="to-configure-a-boot-image-to-deploy-from-a-pxe-enabled-distribution-point"></a>Pour configurer une image de démarrage pour un déploiement à partir d’un point de distribution PXE  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Images de démarrage**.  

3.  Sélectionnez l'image de démarrage à modifier.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés** pour ouvrir la boîte de dialogue **Propriétés** de l'image de démarrage.  

5.  Sous l’onglet **Source de données** , sélectionnez **Déployer cette image de démarrage depuis le point de distribution PXE**.  

    > [!NOTE]  
    >  Pour plus d’informations, consultez [Utiliser PXE pour déployer Windows sur le réseau](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

6.  Après avoir configuré les propriétés, cliquez sur **OK**.  

##  <a name="BKMK_BootImageLanguage"></a> Configurer plusieurs langues pour le déploiement d’images de démarrage  
 Les images de démarrage sont indépendantes de la langue. Vous pouvez ainsi utiliser une image de démarrage qui affichera le texte de la séquence de tâches en plusieurs langues en mode WinPE, à condition d’inclure la prise en charge des langues adéquates dans les composants facultatifs Windows PE et de définir la variable de séquence de tâches appropriée pour indiquer la langue à afficher. La langue du système d’exploitation que vous déployez est indépendante de la langue affichée en mode WinPE, quelle que soit la version de Configuration Manager utilisée. La langue présentée à l'utilisateur est déterminée comme suit :  

-   Quand un utilisateur exécute la séquence de tâches à partir d’un système d’exploitation existant, Configuration Manager utilise automatiquement la langue configurée pour l’utilisateur. Quand la séquence de tâches est exécutée automatiquement à une échéance de déploiement obligatoire, Configuration Manager utilise la langue du système d’exploitation.  

-   Dans le cas des déploiements de système d'exploitation qui utilisent PXE ou un média, vous pouvez définir la valeur de l'ID de langue dans la variable SMSTSLanguageFolder, dans le cadre d'une commande de prédémarrage. Quand l’ordinateur démarre dans WinPE, les messages sont affichés dans la langue que vous avez spécifiée dans la variable. En cas d’erreur durant l’accès au fichier de ressources de langue figurant dans le dossier spécifié ou si la variable n’est pas définie, les messages sont affichés dans la langue de WinPE.  

    > [!NOTE]  
    >  Quand le média est protégé par un mot de passe, le texte qui invite l’utilisateur à entrer le mot de passe est toujours affiché dans la langue de WinPE.  

 Pour définir la langue de WinPE pour les déploiements PXE ou les déploiements de système d’exploitation établis par un média, suivez la procédure ci-dessous.  

#### <a name="to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-operating-system-deployment"></a>Pour définir la langue de Windows PE pour un déploiement PXE ou un déploiement de système d'exploitation établi par un média  

1.  Avant de mettre à jour l'image de démarrage, vérifiez que le fichier de ressources de la séquence de tâche appropriée (tsres.dll) se trouve bien dans le dossier de langue correspondant sur le serveur de site. Par exemple, le fichier de ressources anglais se trouve à l’emplacement suivant : <*dossier_installation_ConfigMgr*> \OSD\bin\x64\00000409\tsres.dll.  

2.  Dans le cadre de votre commande de prédémarrage, affectez l'ID de langue approprié à la variable d'environnement SMSTSLanguageFolder. Vous devez spécifier l'ID de langue au format décimal, et non hexadécimal. Par exemple, pour configurer l'ID de langue sur l'anglais, vous devez spécifier la valeur décimale 1033 au lieu de la valeur hexadécimale 00000409 utilisée comme nom de dossier.  

