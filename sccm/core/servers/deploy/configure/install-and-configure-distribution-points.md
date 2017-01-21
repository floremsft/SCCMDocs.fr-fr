---
title: "Gérer les points de distribution | Microsoft Docs"
description: "Hébergez le contenu (fichiers et logiciels) que vous déployez pour les appareils et les utilisateurs à l’aide de points de distribution. Voici comment les installer et les configurer."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: 8684bf1231ff9d663717b4c9874dac98d50e3647

---
# <a name="install-and-configure-distribution-points-for-system-center-configuration-manager"></a>Installer et configurer des points de distribution pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez installer des points de distribution System Center Configuration Manager pour héberger le contenu (fichiers et logiciels) que vous déployez pour les appareils et les utilisateurs. Vous pouvez aussi créer des groupes de points de distribution de façon à simplifier la gestion des points de distribution, ainsi que la distribution du contenu aux points de distribution.  

 Pendant que vous **installez un nouveau point de distribution** (à l’aide de l’Assistant Installation) ou que vous **gérez les propriétés d’un point de distribution existant** (en modifiant les propriétés des points de distribution), vous pouvez configurer la plupart des paramètres de point de distribution. Cependant, certains paramètres sont disponibles seulement pendant l’installation ou la modification, mais pas les deux :  

-   **Paramètres disponibles seulement pendant l’installation d’un point distribution** :  

    -   Autoriser Configuration Manager à installer IIS sur l’ordinateur du point de distribution  

    -   Configurer les paramètres d’espace disque pour le point de distribution  

-   **Paramètres disponibles seulement pendant la modification des propriétés d’un point distribution** :  

    -   Gérer les relations d’un groupe de points de distribution  

    -   Afficher le contenu déployé sur le point de distribution  

    -   Configurer des limites de taux pour les transferts de données vers les points de distribution  

    -   Configurer des planifications pour les transferts de données vers les points de distribution  

##  <a name="a-namebkmkinstalla-install-a-distribution-point"></a><a name="bkmk_install"></a> Installer un point de distribution  
 Vous devez désigner un serveur de système de site en tant que point de distribution pour rendre le contenu disponible pour les ordinateurs clients. Vous pouvez ajouter un rôle de site de point de distribution à un nouveau serveur de système de site ou ajouter le rôle de site à un système de site existant.  

 Quand vous installez un nouveau point de distribution, vous utilisez un Assistant d’installation qui vous guide à travers les paramètres disponibles. Avant de commencer, tenez compte des points suivants :  

-   Pour créer et configurer un point de distribution, vous devez disposer des autorisations de sécurité suivantes :  

    -   **Lecture** pour l'objet **Point de distribution**  

    -   **Copier vers le point de distribution** pour l'objet **Point de distribution**  

    -   **Modifier** pour l'objet **Site**  

    -   **Gérer des certificats pour le déploiement de système d'exploitation** pour l'objet **Site**  

-   IIS doit être installé sur le serveur qui hébergera le point de distribution. Quand vous installez le rôle de système de site, Configuration Manager peut installer et configurer IIS automatiquement.  

Suivez les procédures de base ci-dessous pour installer ou modifier un point de distribution et reportez-vous à la section [Configuration des points de distribution](#bkmk_configs) de cette rubrique pour connaître les détails des différentes options de configuration disponibles.  

#### <a name="to-install-a-distribution-point"></a>Pour installer un point de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Administration** >  **Configuration du site** > **Serveurs et rôles de système de site**.  

2.  Ajoutez le rôle de système de site de point de distribution à un serveur de système de site nouveau ou existant :  

    -   **Nouveau serveur de système de site**: sous l’onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un serveur de système de site**. L'Assistant Création de serveur de système de site s'ouvre.  

    -   **Serveur de système de site existant**: Cliquez sur le serveur sur lequel vous souhaitez installer le rôle de système de site de point de distribution. Lorsque vous cliquez sur un serveur, la liste des rôles de système de site déjà installés sur le serveur s'affiche dans le panneau des résultats.  

         Sur l'onglet **Accueil** , dans le groupe **Serveur** , cliquez sur **Ajouter des rôles de système de site**. L'Assistant Ajout de rôles de système de site s'ouvre.  

3.  Sur la page **Général** , spécifiez les paramètres généraux du serveur de système de site. Lorsque vous ajoutez le point de distribution à un serveur de système de site existant, vérifiez les valeurs qui ont été précédemment configurées.  

4.  Sur la page **Sélection du rôle système** , sélectionnez **Point de distribution** dans la liste des rôles disponibles, puis cliquez sur **Suivant**.  

5.  Pour les pages suivantes de l’Assistant, aidez-vous de la section [Configuration des points de distribution](#bkmk_configs) pour compléter chaque page de l’Assistant quand vous y êtes invité.  

     Par exemple, si vous souhaitez installer le point de distribution en tant que point de distribution d’extraction, sélectionnez **Activer ce point de distribution pour extraire le contenu à partir d’autres points de distribution**, puis procédez aux configurations supplémentaires requises par les points de distribution d’extraction.  

6.  Après avoir fermé l'Assistant, le rôle de site de point de distribution est ajouté au serveur de système de site.  

#### <a name="to-modify-a-distribution-point"></a>Pour modifier un point de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Administration** >  **Points de distribution**, puis sélectionnez le point de distribution à configurer.  

2.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

3.  Aidez-vous des informations de la section [Configuration des points de distribution](#bkmk_configs) pour modifier les propriétés du point de distribution.  

4.  Après avoir apporté les modifications voulues, enregistrez vos paramètres et fermez la page de propriétés du point de distribution.  

##  <a name="a-namebkmkmanagea-manage-distribution-point-groups"></a><a name="bkmk_manage"></a> Gérer les groupes de points de distribution  
 Les groupes de points de distribution fournissent un regroupement logique de points de distribution pour la distribution de contenu. Vous pouvez utiliser ces groupes pour gérer et surveiller le contenu depuis un emplacement central pour les points de distribution qui s’étendent sur plusieurs sites.  

-   Vous pouvez ajouter un ou plusieurs points de distribution à partir de n’importe quel site de la hiérarchie vers un groupe de points de distribution.  

-   Vous pouvez ajouter un point de distribution à plusieurs groupes de points de distribution.  

-   Si vous distribuez du contenu vers un groupe de points de distribution, Configuration Manager distribue le contenu à tous les points de distribution qui sont membres de ce groupe.  

-   Si vous ajoutez un point de distribution au groupe de points de distribution après une distribution de contenu initiale, Configuration Manager distribue automatiquement le contenu au nouveau membre du point de distribution.  

-   Vous pouvez associer un regroupement à un groupe de points de distribution. Si vous distribuez ensuite du contenu vers ce regroupement, Configuration Manager détermine les groupes de points de distribution qui sont associés au regroupement, puis distribue le contenu à tous les points de distribution qui sont membres de ces groupes.  

    > [!NOTE]  
    >  Si vous avez déjà distribué le contenu à un regroupement, puis que vous associez ce regroupement à un nouveau groupe de points de distribution, vous devez redistribuer le contenu au regroupement pour que le contenu puisse être distribué au nouveau groupe.  

#### <a name="to-create-and-configure-a-new-distribution-point-group"></a>Pour créer et configurer un nouveau groupe de points de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Groupes de points de distribution**.  

2.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un groupe**.  

3.  Entrez le nom et la description du groupe de points de distribution.  

4.  Dans l'onglet **Regroupements** , cliquez sur **Ajouter**, sélectionnez les regroupements que vous souhaitez associer au groupe de points de distribution, puis cliquez sur **OK**.  

5.  Dans l'onglet **Membres** , cliquez sur **Ajouter**, sélectionnez les points de distribution que vous souhaitez ajouter comme membres du groupe de points de distribution, puis cliquez sur **OK**.  

6.  Cliquez sur **OK** pour créer le groupe de points de distribution.  

#### <a name="to-add-distribution-points-and-associate-collections-to-an-existing-distribution-point-group"></a>Pour ajouter des points de distribution et associer des regroupements à un groupe de points de distribution existant  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Groupes de points de distribution**.  

2.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

3.  Dans l'onglet **Regroupements** , cliquez sur **Ajouter** pour sélectionner les regroupements que vous souhaitez associer au groupe de points de distribution, puis cliquez sur **OK**.  

4.  Dans l'onglet **Membres** , cliquez sur **Ajouter** pour sélectionner les points de distribution que vous souhaitez ajouter comme membres du groupe de points de distribution, puis cliquez sur **OK**.  

5.  Cliquez sur **OK** pour enregistrer les modifications apportées au groupe de points de distribution.  

#### <a name="to-add-selected-distribution-points-to-a-new-distribution-point-group"></a>Pour ajouter les points de distribution sélectionnés à un nouveau groupe de points de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Points de distribution**, puis sélectionnez les points de distribution à ajouter au nouveau groupe de points de distribution.  

2.  Dans l'onglet **Accueil** , dans le groupe **Point de distribution** , développez **Ajouter les éléments sélectionnés**, puis cliquez sur **Ajouter les éléments sélectionnés au nouveau groupe de points de distribution**.  

3.  Entrez le nom et la description du groupe de points de distribution.  

4.  Dans l'onglet **Regroupements** , cliquez sur **Ajouter** pour sélectionner les regroupements que vous souhaitez associer au groupe de points de distribution, puis cliquez sur **OK**.  

5.  Sous l’onglet **Membres**, confirmez votre souhait de voir Configuration Manager ajouter les points de distribution répertoriés en tant que membres du groupe de points de distribution. Cliquez sur **Ajouter** pour modifier les points de distribution que vous souhaitez ajouter en tant que membres du groupe de points de distribution, puis cliquez sur **OK**.  

6.  Cliquez sur **OK** pour créer le groupe de points de distribution.  

#### <a name="to-add-selected-distribution-points-to-existing-distribution-point-groups"></a>Pour ajouter les points de distribution sélectionnés à des groupes de points de distribution existants  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Points de distribution**, puis sélectionnez les points de distribution à ajouter au nouveau groupe de points de distribution.  

2.  Dans l'onglet **Accueil** , dans le groupe **Point de distribution** , développez **Ajouter les éléments sélectionnés**, puis cliquez sur **Ajouter les éléments sélectionnés à des groupes de points de distribution existants**.  

3.  Dans **Groupes de points de distribution disponibles**, sélectionnez les groupes de points de distribution dont les points de distribution sélectionnés doivent être ajoutés en tant que membres, puis cliquez sur **OK**.  

##  <a name="a-namebkmkconfigsa-distribution-point-configurations"></a><a name="bkmk_configs"></a> Configurations des points de distribution  
 Chaque point de distribution prend en charge plusieurs configurations différentes. Toutefois, tous les types de point de distribution ne prennent pas en charge toutes les configurations. Par exemple, les points de distribution cloud ne prennent pas en charge les déploiements de contenu activés pour PXE ou la multidiffusion. Les rubriques suivantes contiennent des informations sur des limitations bien précises :  

-   [Utiliser un point de distribution cloud avec System Center Configuration Manager](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

-   [Utiliser un point de distribution d’extraction avec System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

Les sections suivantes décrivent les configurations que vous pouvez sélectionner pendant l’installation d’un nouveau point de distribution ou la modification des propriétés d’un point de distribution existant :  

### <a name="general"></a>Général  
 Configurez les paramètres généraux des points de distribution :  

-   **Installer et configurer IIS si requis par Configuration Manager** : sélectionnez ce paramètre pour permettre à Configuration Manager d’installer et configurer Internet Information Services (IIS) sur le serveur si IIS n’est pas déjà installé. Les services Internet doivent être installés sur tous les points de distribution. Si les services Internet ne sont pas installés sur le serveur et si vous ne sélectionnez pas ce paramètre, vous devez installer les services Internet avant que le point de distribution puisse être installé avec succès.  

    > [!NOTE]  
    >  Cette option est disponible uniquement lorsque vous installez un nouveau point de distribution.  

-   **Configurez la manière dont les appareils clients communiquent avec le point de distribution** : l’utilisation de HTTP et de HTTPS présente des avantages et des inconvénients. Pour plus d’informations, consultez *Bonnes pratiques de sécurité pour la gestion de contenu* dans [Concepts fondamentaux de la gestion de contenu dans System Center Configuration Manager](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   **Autoriser les clients à se connecter anonymement** : ce paramètre indique si le point de distribution autorise les connexions anonymes des clients Configuration Manager à la bibliothèque de contenu.  

    > [!IMPORTANT]  
    >  La réparation d’une application Windows Installer sur un client peut échouer si vous n’utilisez pas ce paramètre.  
    >   
    >  -   Quand vous déployez une application Windows Installer sur un client Configuration Manager, Configuration Manager télécharge le fichier dans le cache local du client, puis le fichier est supprimé à la fin de l’installation.  
    > -   Le client Configuration Manager met à jour la liste source Windows Installer des applications Windows Installer installées avec le chemin de contenu de la bibliothèque de contenu sur les points de distribution associés.  
    > -   Par la suite, si vous démarrez l’action de réparation via Ajout/Suppression de programmes sur un client Configuration Manager, MSIExec tente d’accéder au chemin de contenu avec un compte d’utilisateur anonyme.  
    >   
    >  Vous pouvez toutefois changer ce comportement en installant la mise à jour décrite dans l’article de la Base de connaissances Microsoft [2619572](http://go.microsoft.com/fwlink/?LinkId=279699) et en modifiant une clé de Registre.  
    >   
    >  -   Une fois la mise à jour installée sur les clients, MSIExec accède au chemin de contenu en utilisant le compte d’utilisateur actuellement connecté, sauf si vous activez le paramètre **Autoriser les clients à se connecter anonymement**.  

-   **Créez un certificat auto-signé ou importez un certificat client d’infrastructure à clé publique (PKI) pour le point de distribution**. Le certificat remplit les fonctions suivantes :  

    -   Il authentifie le point de distribution à un point de gestion avant que le point de distribution n'envoie des messages d'état.  

    -   Lorsque la case **Activer la prise en charge PXE pour les clients** est sélectionnée sur la page **Paramètres PXE** , le certificat est envoyé aux ordinateurs qui effectuent un démarrage PXE afin qu'ils puissent se connecter à un point de gestion pendant le déploiement du système d'exploitation.  

    Lorsque tous vos points de gestion du site sont configurés pour le protocole HTTP, créez un certificat auto-signé. Lorsque vos points de gestion sont configurés pour le protocole HTTPS, importez un certificat client PKI.  

    Pour importer le certificat, accédez à un fichier PKCS (Public Key Cryptography Standard) (PKCS #12) qui contient un certificat PKI avec les spécifications suivantes pour Configuration Manager :  

    -   L'utilisation prévue doit inclure l'authentification du client.  

    -   La clé privée doit être activée pour l'exportation.  

    > [!TIP]  
    >  Il n'existe aucune exigence particulière pour l'objet du certificat ou le nom alternatif d'objet du certificat (SAN), et vous pouvez utiliser le même certificat pour plusieurs points de distribution.  

     Pour plus d’informations sur la configuration requise pour les certificats, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

     Pour obtenir un exemple de déploiement de ce certificat, consultez la section *Déploiement du certificat client pour les points de distribution* de la rubrique [Exemple détaillé de déploiement des certificats PKI pour Configuration Manager : Autorité de certification Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

-   **Activer ce point de distribution pour le contenu préparé** : sélectionnez ce paramètre pour activer le point de distribution du contenu préparé. Lorsque ce paramètre est sélectionné, vous pouvez configurer le comportement de distribution lors de la distribution du contenu. Vous pouvez choisir de toujours préparer le contenu sur le point de distribution, de préparer le contenu initial pour le package, mais d'utiliser le processus normal de distribution du contenu lorsqu'il existe des mises à jour du contenu, ou de toujours utiliser le processus normal de distribution du contenu pour le contenu du package.  

### <a name="drive-settings"></a>Paramètres du lecteur  

> [!NOTE]  
>  Ces options sont disponibles uniquement quand vous installez un nouveau point de distribution.  

Spécifiez les paramètres du lecteur pour le point de distribution. Vous pouvez configurer jusqu’à deux lecteurs de disque pour la bibliothèque de contenu et deux lecteurs de disque pour le partage de package, même si Configuration Manager peut utiliser des lecteurs supplémentaires quand les deux premiers atteignent la réserve d’espace libre configurée sur le lecteur. La page **Paramètres du lecteur** permet de configurer la priorité des lecteurs de disque et la quantité d'espace disque libre restant sur chaque lecteur de disque.  

-   **Réserve d’espace libre sur le lecteur (Mo)** : la valeur que vous configurez pour ce paramètre détermine la quantité d’espace libre sur un lecteur avant que Configuration Manager choisisse un autre lecteur et poursuive le processus de copie sur ce lecteur. Les fichiers de contenu peuvent s'étendre sur plusieurs lecteurs.  

-   **Emplacements du contenu** : spécifiez les emplacements du contenu pour la bibliothèque de contenu et le partage de package. Configuration Manager copie le contenu à l’emplacement de contenu principal jusqu’à ce que la quantité d’espace libre atteigne la valeur spécifiée dans **Réserve d’espace libre sur le lecteur (Mo)**. Par défaut, les emplacements du contenu sont définis sur **Automatique**. L'emplacement de contenu principal est défini sur le lecteur de disque disposant de plus d'espace lors de l'installation ; l'emplacement secondaire, quant à lui, est attribué au lecteur de disque disposant de plus d'espace suivant. Quand le lecteur principal et le lecteur secondaire atteignent la réserve d’espace libre sur le lecteur, Configuration Manager sélectionne un autre lecteur disponible ayant le plus d’espace disque libre et poursuit le processus de copie.  

> [!NOTE]  
>  Pour empêcher l’installation de Configuration Manager sur un lecteur spécifique, créez un fichier vide intitulé **no_sms_on_drive.sms** et copiez-le dans le dossier racine du lecteur avant d’installer le point de distribution.  

### <a name="pull-distribution-point"></a>Point de distribution d’extraction  
Quand vous sélectionnez **Activer ce point de distribution pour extraire le contenu à partir d’autres points de distribution**, vous modifiez la méthode employée par l’ordinateur pour obtenir le contenu que vous distribuez sur le point de distribution. Ce point de distribution devient un point de distribution d’extraction.  

Pour chaque point de distribution d’extraction que vous configurez, vous devez spécifier le ou les points de distribution sources à partir desquels le point de distribution d’extraction obtient le contenu.  

-   Cliquez sur **Ajouter**, puis sélectionnez un ou plusieurs des points de distribution disponibles comme points de distribution source.  

-   Cliquez sur **Supprimer** pour supprimer le point de distribution sélectionné des points de distribution source.  

-   Utilisez les boutons fléchés pour définir l'ordre dans lequel les points de distribution source sont contactés par le point de distribution d'extraction lorsque ce dernier essaie de transférer du contenu. Les points de distribution associés à la valeur la plus faible sont contactés en premier.  

### <a name="pxe"></a>Environnement PXE  
Indiquez si vous souhaitez activer l'environnement PXE sur le point de distribution. Quand vous activez l’environnement PXE, Configuration Manager installe les services de déploiement Windows sur le serveur, si nécessaire. Le service de déploiement Windows effectue le démarrage PXE pour installer des systèmes d'exploitation. Après avoir effectué toutes les étapes de l’Assistant pour créer le point de distribution, Configuration Manager installe un fournisseur dans les services de déploiement Windows qui utilisent les fonctions de démarrage PXE.  

Lorsque vous sélectionnez **Activer la prise en charge PXE pour les clients**, configurez les paramètres suivants :  

-   **Autoriser ce point de distribution à répondre aux requêtes PXE entrantes**: permet de spécifier si les Services de déploiement Windows doivent être activés, pour qu'ils répondent aux demandes de service PXE. Utilisez cette case à cocher pour activer et désactiver le service sans supprimer la fonctionnalité PXE du point de distribution.  

-   **Activer la prise en charge d’ordinateur inconnu** : indiquez si la prise en charge des ordinateurs non gérés par Configuration Manager doit être activée.  

-   **Exiger un mot de passe lorsque les ordinateurs utilisent PXE**: pour renforcer la sécurité de vos déploiements PXE, spécifiez un mot de passe fort.  

-   **Affinité entre appareil et utilisateur**: indiquez de quelle manière le point de distribution doit associer les utilisateurs à l'ordinateur de destination dans le cadre des déploiements PXE. Sélectionnez l'une des options suivantes :  

    -   **Autoriser une affinité entre appareil et utilisateur avec approbation automatique**: sélectionnez ce paramètre pour associer automatiquement les utilisateurs à l'ordinateur de destination sans attendre l'approbation.  

    -   **Autoriser une affinité entre appareil et utilisateur en attente de l'approbation de l'administrateur**: sélectionnez ce paramètre pour attendre l'approbation d'un utilisateur administratif avant d'associer des utilisateurs à l'ordinateur de destination.  

    -   **Ne pas autoriser d'affinité entre appareil et utilisateur**: sélectionnez ce paramètre pour empêcher l'association d'utilisateurs à l'ordinateur de destination.  

     Pour plus d’informations sur l’affinité entre utilisateur et appareil, consultez [Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil dans System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

-   **Interfaces réseau**: Spécifiez que le point de distribution répond aux requêtes PXE à partir de toutes les interfaces réseau ou d'interfaces réseau spécifiques. Si le point de distribution répond à interface réseau spécifique, vous devez fournir l'adresse MAC pour chaque interface réseau.  

-   **Spécifier le délai de réponse du serveur PXE (secondes)**: Indique, en secondes, le délai d'attente du point du point de distribution à l'issue duquel il répond aux requêtes des ordinateurs lorsque plusieurs points de distribution PXE sont utilisés. Par défaut, le point de service PXE de Configuration Manager répond d’abord aux demandes PXE du réseau.  

> [!NOTE]  
>  Le protocole PXE permet de démarrer les déploiements de système d’exploitation sur les ordinateurs clients Configuration Manager. Configuration Manager utilise le rôle de site du point de distribution PXE pour lancer le processus de déploiement du système d’exploitation. Le point de distribution PXE doit être configuré pour répondre aux demandes de démarrage PXE que les clients Configuration Manager effectuent sur le réseau et pour interagir avec l’infrastructure Configuration Manager afin de déterminer les actions de déploiement appropriées à entreprendre.  

### <a name="multicast"></a>Multidiffusion  
Indiquez si vous souhaitez activer la multidiffusion sur le point de distribution. Quand vous activez la multidiffusion, Configuration Manager installe les services de déploiement Windows sur le serveur, si nécessaire.  

Lorsque vous activez la case à cocher **Activer la multidiffusion pour envoyer simultanément des données à plusieurs clients** , configurez les paramètres suivants :  

-   **Compte de connexion multidiffusion** : indiquez le compte à utiliser quand vous configurez des connexions de base de données Configuration Manager pour la multidiffusion.  

-   **Paramètres de l'adresse de multidiffusion**: Spécifiez les adresses IP utilisées pour envoyer des données vers les ordinateurs de destination. Par défaut; l'adresse IP est fournie par un serveur DCHP chargé de distribuer des adresses de multidiffusion. Selon l'environnement réseau, vous pouvez spécifier une plage d'adresses IP entre 239.0.0.0 et 239.255.255.255.  

    > [!IMPORTANT]  
    >  Les adresses IP que vous configurez doivent être accessibles par les ordinateurs de destination qui demandent l'image du système d'exploitation. Vérifiez que les routeurs et pare-feu autorisent le trafic de multidiffusion entre l'ordinateur de destination et le serveur de site.  

-   **Étendue du port UDP pour la multidiffusion**: Spécifiez la plage de ports UDP utilisés pour envoyer des données vers les ordinateurs de destination.  

    > [!IMPORTANT]  
    >  Les ports UDP doivent être accessibles par les ordinateurs de destination qui demandent l'image du système d'exploitation. Vérifiez que les routeurs et pare-feu autorisent le trafic de multidiffusion entre l'ordinateur de destination et le serveur de site.  

-   **Taux de transfert client**: Sélectionnez la vitesse de transfert utilisée pour télécharger des données sur les ordinateurs de destination.  

-   **Nombre maximum de clients**: Spécifiez le nombre maximal d'ordinateurs de destination qui peuvent télécharger le système d'exploitation à partir de ce point de distribution.  

-   **Activer la multidiffusion planifiée** : indiquez comment Configuration Manager contrôle le lancement du déploiement des systèmes d’exploitation sur les ordinateurs de destination. Lorsque cette option est sélectionnée, configurez les options suivantes :  

    -   **Délai de démarrage de session (en minutes)** : indiquez le nombre de minutes écoulé avant que Configuration Manager réponde à la première demande de déploiement.  

    -   **Taille minimale de la session (clients)** : indiquez le nombre de demandes qui doivent être reçues avant que Configuration Manager commence à déployer le système d’exploitation.  

> [!NOTE]  
>  Les déploiements de multidiffusion économisent la bande passante réseau en envoyant de manière simultanée des données à plusieurs clients Configuration Manager au lieu d’envoyer une copie des données à chaque client via une connexion distincte. Pour plus d’informations sur l’utilisation de la multidiffusion pour le déploiement de systèmes d’exploitation, consultez [Utiliser la multidiffusion pour Windows sur le réseau avec System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

### <a name="group-relationships"></a>Relations de groupe  

> [!NOTE]  
>  Ces options sont disponibles uniquement quand vous modifiez les propriétés d’un point de distribution déjà installé  

Gérez les groupes de points de distribution dont ce point de distribution est membre.  

Pour ajouter ce point de distribution en tant que membre à un groupe de points de distribution existant, cliquez sur **Ajouter**. Sélectionnez un groupe de points de distribution existant dans la liste de la boîte de dialogue **Ajouter aux groupes de points de distribution** , puis cliquez sur **OK**.  

Pour supprimer ce point de distribution d'un groupe de points de distribution, sélectionnez le groupe de points de distribution dans la liste, puis cliquez sur **Supprimer**.  

### <a name="content"></a>Content  

> [!NOTE]  
>  Ces options sont disponibles uniquement quand vous modifiez les propriétés d’un point de distribution déjà installé  

Gérez le contenu qui a été distribué au point de distribution. La section des packages de déploiement fournit une liste des packages distribués à ce point de distribution. Vous pouvez sélectionner un package dans la liste, puis effectuer les actions suivantes :  

-   **Valider**: Démarre le processus de validation de l'intégrité des fichiers de contenu dans le package. Pour afficher les résultats du processus de validation du contenu, dans l'espace de travail **Surveillance** , développez **État de distribution**, puis cliquez sur le nœud **État du contenu** .  

-   **Redistribuer**: Copie tous les fichiers de contenu dans le package vers le point de distribution et remplace les fichiers existants. Vous utilisez généralement cette opération pour réparer les fichiers de contenu dans le package.  

-   **Supprimer**: Supprime les fichiers de contenu du point de distribution du package.  

### <a name="content-validation"></a>Validation du contenu  
Indiquez si vous souhaitez définir une planification pour valider l'intégrité des fichiers de contenu sur le point de distribution. Quand vous activez la validation de contenu selon une planification, Configuration Manager démarre le processus à l’heure planifiée, et tout le contenu est vérifié sur le point de distribution. Vous pouvez également configurer la priorité de la validation du contenu. Par défaut, la priorité est définie sur **La plus faible**.  

Pour afficher les résultats du processus de validation du contenu, dans l'espace de travail **Surveillance** , développez **État de distribution**, puis cliquez sur le nœud **État du contenu** . Le contenu de chaque type de package (par exemple, application, package de mises à jour logicielles et image de démarrage) s'affiche.  

> [!WARNING]  
>  Quand vous planifiez la validation du contenu en utilisant l’heure locale de l’ordinateur, la planification affichée dans la console Configuration Manager est exprimée en heure UTC.  

### <a name="boundary-group"></a>Groupes de limites  
Gérez les groupes de limites pour lesquels ce point de distribution est attribué. Vous pouvez associer des groupes de limites à un point de distribution. Au cours de déploiement de contenu, les clients doivent se trouver dans un groupe de limites associé au point de distribution pour l'utiliser en tant qu'emplacement source pour le contenu.
En outre :
- À compter de la version 1610, vous pouvez cocher **Autoriser les clients à utiliser ce système de site en tant qu’emplacement source de secours du contenu** pour permettre aux clients en dehors de ces groupes de limites de revenir et d’utiliser le point de distribution en tant qu’emplacement source pour le contenu si aucun autre point de distribution n’est disponible. Pour plus d’informations sur les groupes de limites, consultez [Groupes de limites pour les versions 1511, 1602 et 1606](/sccm/core/servers/deploy/configur/boundary-groups-for-1511-1602-and-1606). Pour les points de distribution préférés, consultez [Concepts fondamentaux de la gestion de contenu dans System Center Configuration Manager](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).
- Avec la version 1610 ou ultérieure, vous configurez des *relations* de groupe de limites qui définissent à quel moment et auprès de quels groupes de limites un client peut effectuer une action de secours pour trouver du contenu. Pour plus d’informations, consultez [Groupes de limites](/sccm/core/servers/deploy/configur/define-site-boundaries-and-boundary-groups#boundary-groups).


### <a name="schedule"></a>Planification  

> [!NOTE]  
>  Ces options sont disponibles uniquement quand vous modifiez les propriétés d’un point de distribution déjà installé  

> [!TIP]  
>  Cet onglet est disponible uniquement lorsque vous modifiez les propriétés d'un point de distribution distant de l'ordinateur du serveur de site.  

 Indiquez s’il convient de configurer une planification qui limite la période de transfert de données de Configuration Manager vers le point de distribution.  

> [!IMPORTANT]  
>  La planification est basée sur le fuseau horaire du site émetteur, et non sur celui du point de distribution.  

Pour restreindre les données, sélectionnez la période, puis l'un des paramètres suivants sous **Disponibilité**:  

-   **Ouvrir pour toutes les priorités** : indique que Configuration Manager envoie les données au point de distribution sans restriction.  

-   **Autoriser les priorités moyennes et élevées** : indique que Configuration Manager n’envoie au point de distribution que les données de priorité moyenne et élevée.  

-   **Autoriser uniquement la priorité élevée** : indique que Configuration Manager n’envoie au point de distribution que les données de priorité élevée.  

-   **Fermé** : indique que Configuration Manager n’envoie pas de données au point de distribution.  

Vous pouvez limiter les données par priorité ou fermer la connexion durant des périodes sélectionnées.  

### <a name="rate-limits"></a>Limites du taux de transfert  

> [!NOTE]  
>  Ces options sont disponibles uniquement quand vous modifiez les propriétés d’un point de distribution déjà installé  

> [!TIP]  
>  Cet onglet est disponible uniquement lorsque vous modifiez les propriétés d'un point de distribution distant de l'ordinateur du serveur de site.  

Spécifiez si vous souhaitez configurer des limites du taux de transfert pour contrôler la bande passante réseau utilisée lors du transfert de contenu vers le point de distribution. Vous pouvez choisir parmi les options suivantes :  

-   **Illimité lors de l’expédition de données à cette destination** : indique que Configuration Manager envoie le contenu au point de distribution sans aucune limite de taux de transfert.  

-   **Mode impulsion**: spécifie la taille des blocs de données qui sont envoyés vers le point de distribution. Vous pouvez également spécifier un délai entre l'envoi de chaque bloc de données. Utilisez cette option lorsque vous devez envoyer des données via une connexion réseau de très faible bande passante vers le point de distribution. Par exemple, vous pouvez forcer l'envoi de 1 Ko de données toutes les cinq secondes, quelle que soit la vitesse de la liaison ou son utilisation.  

-   **Limité aux taux de transfert maximaux indiqués par heure**: spécifiez ce paramètre pour qu'un site envoie des données à un point de distribution en utilisant uniquement le pourcentage de temps que vous avez configuré. Quand vous utilisez cette option, Configuration Manager n’identifie pas la bande passante disponible du réseau, mais divise plutôt le temps dont il dispose pour envoyer les données par tranches de temps plus petites. Puis les données sont envoyées pendant une courte plage horaire, suivie de plages horaires pendant lesquelles aucune donnée n'est envoyée. Par exemple, si le taux maximal est fixé à **50 %**, Configuration Manager transmet les données sur une période, qui est suivie d’une période égale où aucune donnée n’est envoyée. La taille effective des donnés ou la taille des blocs de données ne sont pas gérées. En revanche, seule la durée pendant laquelle des données sont envoyées est gérée.  



<!--HONumber=Dec16_HO3-->


