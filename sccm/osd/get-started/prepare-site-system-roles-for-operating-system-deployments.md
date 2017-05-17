---
title: "Préparer les rôles de système de site pour les déploiements de système d’exploitation | Microsoft Docs"
description: "Configurez les rôles de système de site avant de déployer des systèmes d’exploitation dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
caps.latest.revision: 11
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 761c3f58f7c57d8f87ee802da37821895062546d
ms.openlocfilehash: 11c0f169afebdb071fefb5ce300fd1ae3481a94f
ms.contentlocale: fr-fr
ms.lasthandoff: 05/17/2017


---
# <a name="prepare-site-system-roles-for-operating-system-deployments-with-system-center-configuration-manager"></a>Préparer les rôles de système de site pour les déploiements de système d’exploitation avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour déployer des systèmes d’exploitation dans System Center Configuration Manager, vous devez d’abord préparer les rôles de système de site suivants qui appellent des configurations et des considérations spécifiques.

##  <a name="BKMK_DistributionPoints"></a> Points de distribution  
 Le rôle de système de site du point de distribution contient des fichiers sources que les clients peuvent télécharger, notamment le contenu de l’application, les mises à jour logicielles, les images du système d’exploitation et les images de démarrage. Vous pouvez contrôler la distribution du contenu à l'aide de la bande passante, de la limitation et des options de planification.  

 Il est important d’avoir suffisamment de points de distribution pour prendre en charge le déploiement de systèmes d’exploitation sur des ordinateurs. Il est également déterminant de planifier le placement de ces points de distribution dans votre hiérarchie. Vous trouverez la plupart de ces informations de planification dans [Gérer le contenu et l’infrastructure de contenu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md). Toutefois, d’autres éléments doivent être pris en compte lors de la planification de points de distribution spécifiques au déploiement de systèmes d’exploitation.  

###  <a name="BKMK_AdditionalPlanning"></a> Considérations de planification supplémentaires concernant les points de distribution  
 Tenez compte des points supplémentaires suivants dans le cadre de la planification de points de distribution :  

-   **Comment empêcher les déploiements de systèmes d’exploitation indésirables ?**  

     Configuration Manager ne fait pas la distinction entre les serveurs de site et les autres ordinateurs de destination d’un regroupement. Si vous déployez une séquence de tâches obligatoire sur un regroupement qui contient un serveur de site, le serveur de site exécute la séquence de tâches de la même manière que les autres ordinateurs du regroupement exécutent la séquence de tâches. Vérifiez que votre déploiement de système d’exploitation utilise un regroupement qui contient les clients devant exécuter le déploiement.  

     Vous pouvez gérer le comportement des déploiements de séquences de tâches à haut risque. Un déploiement à haut risque, qui est installé automatiquement sur un client, est susceptible d’entraîner des résultats indésirables. Il s’agit par exemple d’une séquence de tâches ayant l’objectif Obligatoire qui déploie un système d’exploitation. Pour réduire le risque lié à un déploiement à haut risque indésirable, vous pouvez configurer des paramètres de vérification de déploiement. Pour plus d’informations, consultez [Paramètres de gestion des déploiements à haut risque](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

-   **Combien d’ordinateurs peuvent recevoir simultanément une image de système d’exploitation à partir d’un point de distribution unique ?**  

     Pour estimer le nombre de points de distribution dont vous avez besoin, vous devez prendre en compte la vitesse de traitement et l’E/S disque du point de distribution, la bande passante disponible sur le réseau et les effets de la taille du package d’images sur ces ressources. Par exemple, sur un réseau Ethernet de 100 mégaoctets (Mo), le nombre maximal d'ordinateurs capables de traiter un package d'images de 4 gigaoctets (Go) en une heure est de 11 si vous ne tenez pas compte des autres facteurs de ressources de serveur.  

     `100 Megabits/sec = 12.5 Megabytes/sec = 750 Megabytes/min = 45 Gigabytes/hour = 11 images @ 4GB per image.`  

     Si vous devez déployer un système d’exploitation sur un nombre spécifique d’ordinateurs dans un délai spécifique, distribuez l’image sur un nombre approprié de points de distribution.  

-   **Puis-je déployer un système d’exploitation sur un point de distribution ?**  

     Vous pouvez déployer un système d’exploitation sur un point de distribution, mais l’image du système d’exploitation doit être reçue à partir d’un autre point de distribution.  

###  <a name="BKMK_PXEDistributionPoint"></a> Configuration de points de distribution pour accepter des requêtes PXE  
 Pour déployer des systèmes d’exploitation sur des clients Configuration Manager qui effectuent des demandes de démarrage PXE, vous devez configurer un ou plusieurs points de distribution pour accepter les demandes PXE. Une fois le point de distribution configuré, il répond à la demande de démarrage PXE et détermine l’action de déploiement appropriée à prendre.

> [!IMPORTANT]  
>  [Windows Deployment Services](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDS) doit être installé sur tous les points de distribution compatibles PXE.  

 Utilisez la procédure suivante pour modifier un point de distribution existant afin qu'il puisse accepter les requêtes PXE. Pour plus d’informations sur la façon d’installer un nouveau point de distribution, consultez [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  

#### <a name="to-modify-an-existing-distribution-point-to-accept-pxe-requests"></a>Pour modifier un point de distribution existant afin d'accepter les requêtes PXE  

1.  Dans la console Configuration Manager, cliquez sur **Administration**, développez **Vue d’ensemble**, puis cliquez sur **Points de distribution**.  

2.  Sélectionnez le point de distribution à configurer et, sur l’onglet **Accueil** du groupe **Propriétés** , cliquez sur **Propriétés**.  

3.  Sur la page des propriétés pour le point de distribution, cliquez sur l'onglet **PXE** . et sélectionnez **Activer la prise en charge PXE pour les clients** pour activer PXE sur ce point de distribution.  

4.  Cliquez sur **Oui** dans la boîte de dialogue **Consulter les ports requis pour PXE** pour confirmer que vous souhaitez activer PXE. Configuration Manager configure automatiquement les ports par défaut sur un Pare-feu Windows. Vous devez configurer manuellement les ports si vous utilisez un autre pare-feu.  

    > [!NOTE]  
    >  Si WDS et DHCP sont installés sur le même serveur, vous devez configurer WDS pour écouter sur un port différent (étant donné que DHCP écoute sur le même port). Pour plus d’informations, consultez [Considérations quand vous avez WDS et DHCP sur le même serveur](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP).  

5.  Sélectionnez **Autoriser ce point de distribution à répondre aux requêtes PXE entrantes** pour que WDS réponde aux demandes de service PXE entrantes. Vous pouvez utiliser ce paramètre pour activer et désactiver le service sans supprimer la fonctionnalité PXE du point de distribution.  

6.  Pour déployer des systèmes d’exploitation sur des ordinateurs qui ne sont pas gérés par Configuration Manager, sélectionnez  **Activer la prise en charge d’ordinateur inconnu**.  

7.  Sélectionnez **Exiger un mot de passe lorsque les ordinateurs utilisent PXE**, puis indiquez un mot de passe fort pour renforcer la sécurité de votre déploiement PXE.  

8.  In the **Affinité entre périphérique et utilisateur** , indiquez de quelle façon vous souhaitez que le point de distribution associe des utilisateurs à l’ordinateur de destination pour les déploiements PXE.  

    -   Sélectionnez **Ne pas utiliser d’affinité entre périphérique et utilisateur** pour ne pas associer les utilisateurs à l’ordinateur de destination.  

    -   Sélectionnez **Autoriser l'affinité entre périphérique et utilisateur avec l'approbation manuelle** pour attendre l'approbation d'un utilisateur administratif avant que les utilisateurs soient associés à l'ordinateur de destination.  

    -   Sélectionnez **Autoriser l'affinité entre périphérique et utilisateur avec l'approbation automatique** pour associer automatiquement les utilisateurs à l'ordinateur de destination sans attendre l'approbation.  

     Pour plus d’informations, consultez [Associer des utilisateurs à un ordinateur de destination](../get-started/associate-users-with-a-destination-computer.md).  

9. Spécifiez que le point de distribution répond aux requêtes PXE à partir de toutes les interfaces réseau ou d'interfaces réseau spécifiques. Si vous voulez que le point de distribution réponde à des interfaces réseau spécifiques, vous devez fournir l’adresse MAC pour chaque interface réseau.  

10. Indiquez, en secondes, le délai d'attente du point de distribution à l'issue duquel il répond aux requêtes des ordinateurs lorsque plusieurs points de distribution PXE sont utilisés.  

11. Cliquez sur **OK** pour mettre à jour les propriétés du point de distribution.  

###  <a name="BKMK_RamDiskTFTP"></a> Personnalisation des tailles de bloc et de fenêtre TFTP RamDisk pour les points de distribution compatibles PXE  
Vous pouvez personnaliser la taille de bloc TFTP RamDisk et, à compter de Configuration Manager version 1606, la taille de fenêtre pour les points de distribution compatibles PXE. Si vous avez personnalisé votre réseau, cela peut occasionner un échec de téléchargement de l’image de démarrage avec une erreur de délai d’attente résultant d’une taille excessive de bloc ou de fenêtre. La personnalisation des tailles de bloc et de fenêtre TFTP RamDisk permet d’optimiser le trafic TFTP lors de l’utilisation de PXE en réponse à des besoins réseau spécifiques.   
Vous devez tester les paramètres personnalisés dans votre environnement pour déterminer la configuration la plus efficace.  

-   **Taille de bloc TFTP**: la taille de bloc est la taille des paquets de données que le serveur envoie au client qui télécharge le fichier (comme indiqué dans RFC 2347). Plus la taille de bloc est importante, moins le serveur envoie de paquets. Il y a donc moins de délais d’aller et retour entre le serveur et le client. Toutefois, une taille de bloc importante entraîne une fragmentation des paquets, incompatible avec la plupart des implémentations du client PXE.  

-   **Taille de fenêtre TFTP**: le protocole TFTP nécessite le renvoi d’un paquet d’accusé de réception (ACK) pour chaque bloc de données envoyé. Le serveur n’envoie pas le bloc suivant dans la séquence tant qu’il n’a pas reçu le paquet ACK pour le bloc précédent. Le fenêtrage TFTP est une fonctionnalité des Services de déploiement Windows qui permet de définir le nombre de blocs de données nécessaires pour le remplissage d’une fenêtre. Le serveur envoie les blocs de données dos à dos jusqu’à ce que la fenêtre soit remplie, et le client renvoie un paquet ACK. L’augmentation de cette taille de fenêtre réduit le nombre de délais d’aller et retour entre le client et le serveur, et raccourcit le temps global nécessaire au téléchargement d’une image de démarrage.  


#### <a name="to-modify-the-ramdisk-tftp-window-size"></a>Pour modifier la taille de fenêtre TFTP RamDisk  

-   Ajoutez la clé de Registre suivante aux points de distribution compatibles PXE pour personnaliser la taille de fenêtre TFTP RamDisk :  

     **Emplacement**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nom : RamDiskTFTPWindowSize  

     **Type**: REG_DWORD  

     **Valeur** : &lt;taille de fenêtre personnalisée>  

 La valeur par défaut est 1 (1 bloc de données remplit la fenêtre).  

#### <a name="to-modify-the-ramdisk-tftp-block-size"></a>Pour modifier la taille de bloc TFTP RamDisk  

-   Ajoutez la clé de Registre suivante aux points de distribution compatibles PXE pour personnaliser la taille de fenêtre TFTP RamDisk :  

     **Emplacement**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nom : RamDiskTFTPBlockSize  

     **Type**: REG_DWORD  

     **Valeur** : &lt;taille de bloc personnalisée>  

 La valeur par défaut est 4096 (4k).  


###  <a name="BKMK_DPMulticast"></a> Configurer des points de distribution pour prendre en charge la multidiffusion  
 La multidiffusion est une méthode d’optimisation réseau que vous pouvez utiliser sur des points de distribution quand plusieurs clients sont susceptibles de télécharger la même image de système d’exploitation simultanément. En cas d’utilisation de la multidiffusion, plusieurs ordinateurs peuvent télécharger simultanément l’image de système d’exploitation quand elle est multidiffusée par le point de distribution, plutôt que de faire en sorte que le point de distribution envoie une copie des données à chaque client à l’aide d’une connexion distincte. Vous devez configurer au moins un point de distribution pour prendre en charge la multidiffusion. Pour plus d’informations, consultez [Utiliser la multidiffusion pour déployer Windows sur le réseau](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 Avant de déployer le système d'exploitation, vous devez configurer un point de distribution pour prendre en charge la multidiffusion. Pour modifier un point de distribution existant afin de prendre en charge la multidiffusion, procédez comme suit. Pour plus d’informations sur l’installation d’un nouveau point de distribution, consultez [Install and configure distribution points](../../core/servers/deploy/configure/install-and-configure-distribution-points.md) (Installer et modifier des points de distribution).

#### <a name="to-enable-multicast-for-a-distribution-point"></a>Pour activer la multidiffusion pour un point de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Vue d'ensemble**, puis sélectionnez le nœud **Points de distribution** .  

3.  Sélectionnez le point de distribution que vous souhaitez utiliser pour procéder à la multidiffusion de l'image du système d'exploitation.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Sélectionnez l'onglet **Multidiffusion** et configurez les options suivantes :  

    -   **Activer la multidiffusion**: vous devez sélectionner cette option pour que le point de distribution prenne en charge la multidiffusion.  

    -   **Compte de connexion multidiffusion**: spécifiez un compte pour vous connecter à la base de données de site.  

    -   **Paramètres de l’adresse de multidiffusion**: spécifiez les adresses IP pour envoyer des données vers les ordinateurs de destination. Par défaut; l'adresse IP est fournie par un serveur DCHP chargé de distribuer des adresses de multidiffusion. Selon l'environnement réseau, vous pouvez spécifier une plage d'adresses IP entre 239.0.0.0 et 239.255.255.255.  

        > [!IMPORTANT]  
        >  Ces adresses IP doivent être accessibles par les ordinateurs de destination qui demandent l'image du système d'exploitation. Cela signifie que les routeurs et pare-feu entre l'ordinateur de destination et le serveur de site doivent être configurés pour autoriser le trafic de multidiffusion.  

    -   **Étendue du port UDP**: Spécifiez la plage de ports UDP pour envoyer des données aux ordinateurs de destination.  

        > [!IMPORTANT]  
        >  Ces ports doivent être accessibles par les ordinateurs de destination qui demandent l'image du système d'exploitation. Cela signifie que les routeurs et pare-feu entre l'ordinateur de destination et le serveur de site doivent être configurés pour autoriser le trafic de multidiffusion.  

    -   **Multidiffusion planifiée activée** : indiquez comment Configuration Manager contrôle le lancement du déploiement des systèmes d’exploitation sur les ordinateurs de destination. Cliquez sur **Multidiffusion planifiée activée**, puis sélectionnez les options suivantes.  

         Dans la zone **Délai de démarrage de session**, indiquez le temps de réponse en minutes de Configuration Manager à la première demande de déploiement.  

         Dans la zone **Taille minimale de la session**, indiquez le nombre de demandes qui doivent être reçues avant que Configuration Manager commence à déployer le système d’exploitation.  

    -   **Taux de transfert**: Sélectionnez la vitesse de transfert pour télécharger des données sur les ordinateurs de destination.  

    -   **Nombre maximum de clients**: Spécifiez le nombre maximal d'ordinateurs de destination qui peuvent télécharger le système d'exploitation à partir de ce point de distribution.  

6.  Cliquez sur **OK**.  

##  <a name="BKMK_StateMigrationPoints"></a> Point de migration d'état  
 Le point de migration d'état stocke les données d'état utilisateur qui sont capturées sur un seul ordinateur puis restaurées sur un autre ordinateur. Toutefois, quand vous capturez des paramètres utilisateur pour un déploiement de système d’exploitation sur le même ordinateur, comme un déploiement où vous actualisez le système d’exploitation sur l’ordinateur de destination, vous pouvez choisir de stocker les données sur le même ordinateur à l’aide de liens physiques ou d’utiliser un point de migration d’état. Pour certains déploiements d’ordinateur, quand vous créez le magasin d’état, Configuration Manager crée automatiquement une association entre le magasin d’état et l’ordinateur de destination. Au moment de planifier le point de migration d'état, tenez compte des facteurs suivants :  

### <a name="user-state-size"></a>Taille de l’état utilisateur  
 La taille de l'état utilisateur affecte directement le stockage sur disque sur le point de migration d'état, ainsi que les performances réseau au cours de la migration. Réfléchissez à la taille de l'état utilisateur et au nombre d'ordinateurs à migrer. Pensez également aux paramètres à migrer à partir de l'ordinateur. Par exemple, si le dossier **Mes documents** est déjà sauvegardé sur un serveur, peut-être n’avez-vous pas besoin de le migrer dans le cadre du déploiement d’image. Évitez les migrations inutiles afin de réduire la taille globale de l'état utilisateur et diminuer les effets que cela aurait autrement sur les performances réseau et le stockage sur disque sur le point de migration d'état.  

### <a name="user-state-migration-tool"></a>Outil de migration de l'état utilisateur  
 Pour capturer et restaurer l'état utilisateur pendant le déploiement des systèmes d'exploitation, vous devez utiliser un package de l'outil de migration de l'état utilisateur (USMT) qui pointe vers les fichiers sources USMT. Configuration Manager crée automatiquement ce package dans la console Configuration Manager dans **Bibliothèque de logiciels** > **Gestion des applications** > **Packages**. Configuration Manager utilise USMT 10.0, qui est distribué dans le Kit de déploiement et d’évaluation Windows (Windows ADK), pour capturer l’état utilisateur d’un système d’exploitation et le restaurer sur un autre système d’exploitation.  

 Pour obtenir une description de différents scénarios de migration pour USMT 10.0, consultez [Scénarios de migration courants](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx).  

### <a name="retention-policy"></a>Stratégie de rétention  
 Lors de la configuration du point de migration d'état, vous pouvez spécifier la durée de conservation des données d'état utilisateur stockées sur ce point. La durée de conservation des données sur le point de migration d'état dépend de deux éléments :  

-   L'effet que les données stockées ont sur le stockage sur disque.  

-   La nécessité potentielle de conserver les données pendant un certain temps dans le cas où vous devez migrer à nouveau les données.  

 La migration de l’état se produit en deux phases : la capture des données et la restauration des données. Quand vous capturez des données, les données d’état utilisateur sont collectées et enregistrées sur le point de migration d’état. Lorsque vous restaurez les données, les données d'état utilisateur sont récupérées depuis le point de migration d'état et écrites sur l'ordinateur de destination, puis l'étape de séquence de tâches **Libérer le magasin d'état** libère les données stockées. Lorsque les données sont libérées, le minuteur de rétention démarre. Si vous choisissez de supprimer immédiatement les données migrées, les données d'état utilisateur sont supprimées dès qu'elles sont publiées. Si vous choisissez de conserver les données pendant un certain temps, les données seront supprimées une fois cette période écoulée, après la publication des données d'état. Plus la période de rétention définie est longue, plus l'espace disque dont vous pouvez avoir besoin est grand.  

### <a name="select-drive-to-store-user-state-migration-data"></a>Sélectionner le disque pour stocker les données de migration d’état utilisateur  
 Lorsque vous configurez le point de migration d'état, vous devez spécifier le lecteur sur le serveur pour stocker les données de migration d'état utilisateur. Vous sélectionnez un lecteur à partir d'une liste de lecteurs fixe. Toutefois, certains de ces lecteurs peuvent représenter des lecteurs non inscriptibles, tels que le lecteur de CD, ou un lecteur de partage non réseau. De plus, certaines lettres de lecteur peuvent ne pas être mappées vers des lecteurs sur l'ordinateur. Lorsque vous configurez le point de migration d'état, vous devez spécifier un lecteur partagé, accessible en écriture.  

### <a name="configure-a-state-migration-point"></a>Configuration d'un point de migration d'état  
 Vous pouvez utiliser les méthodes suivantes afin de configurer un point de migration d'état pour stocker les données d'état utilisateur :  

-   Utilisez l' **Assistant Création d'un serveur de système de site** pour créer un nouveau serveur de système de site pour le point de migration d'état.  

-   Utilisez l' **Assistant Ajout des rôles de système de site** pour ajouter un point de migration d'état à un serveur existant.  

 Lorsque vous utilisez ces Assistants, vous êtes invité à fournir les informations suivantes pour le point de migration d'état :  

-   Les dossiers pour stocker les données d'état utilisateur.  

-   Le nombre maximal de clients pouvant stocker des données sur le point de migration d'état.  

-   L'espace libre minimum pour le point de migration d'état pour stocker les données d'état utilisateur.  

-   La stratégie de suppression du rôle. Vous pouvez spécifier que les données d'état utilisateur sont supprimées immédiatement après leur restauration sur un ordinateur, ou après un nombre de jours spécifique après la restauration des données utilisateur sur un ordinateur.  

-   Si le point de migration d’état répond uniquement aux demandes de restauration des données d’état utilisateur. Lorsque vous activez cette option, vous ne pouvez pas utiliser le point de migration d'état pour stocker les données d'état utilisateur.  

 Pour connaître les étapes à suivre pour installer un rôle de système de site, consultez [Ajouter des rôles de système de site](../../core/servers/deploy/configure/add-site-system-roles.md).  

