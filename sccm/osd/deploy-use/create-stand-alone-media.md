---
title: "Créer un média autonome"
titleSuffix: Configuration Manager
description: "Utilisez un média autonome pour déployer le système d’exploitation sur un ordinateur sans connexion à un site Configuration Manager ou utilisant le réseau."
ms.custom: na
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
caps.latest.revision: "21"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 533b3942136255dd396df81529dad100d4db0a95
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="create-stand-alone-media-with-system-center-configuration-manager"></a>Créer un média autonome avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Un média autonome dans Configuration Manager contient tout ce qui est nécessaire pour déployer le système d’exploitation sur un ordinateur sans connexion à un site Configuration Manager ou utilisant le réseau. Utilisez un média autonome avec les scénarios de déploiement de système d’exploitation suivants :  

-   [Actualiser un ordinateur existant avec une nouvelle version de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installer une nouvelle version de Windows sur un nouvel ordinateur (système nu)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Effectuer une mise à niveau de Windows vers la dernière version](upgrade-windows-to-the-latest-version.md)  

Le média autonome inclut la séquence de tâches qui automatise la procédure d’installation du système d’exploitation et tout autre contenu nécessaire, notamment l’image de démarrage, l’image du système d’exploitation et les pilotes de périphérique. Étant donné que tous les éléments nécessaires au déploiement du système d’exploitation sont stockés sur le média autonome, l’espace disque requis pour le média autonome est beaucoup plus important que l’espace disque requis pour d’autres types de média. Lorsque vous créez un média autonome sur un site d’administration centrale, le client récupère le code de site qui lui est attribué à partir d’Active Directory. Le média autonome créé sur les sites enfants attribue automatiquement au client le code de site pour ce site.  

##  <a name="BKMK_CreateStandAloneMedia"></a> Créer un média autonome  
Avant de créer un média autonome à l’aide de l’Assistant Création d’un média de séquence de tâches, vérifiez que les conditions suivantes sont remplies :  

### <a name="create-a-task-sequence-to-deploy-an-operating-system"></a>Créer une séquence de tâches pour déployer un système d’exploitation
Dans le cadre du média autonome, vous devez spécifier la séquence de tâches destinée à déployer un système d’exploitation. Pour connaître les étapes permettant de créer une séquence de tâches, consultez [Créer une séquence de tâches pour installer un système d’exploitation dans System Center Configuration Manager](create-a-task-sequence-to-install-an-operating-system.md).

Les actions suivantes ne sont pas prises en charge pour le média autonome :
- Étape Appliquer automatiquement les pilotes dans la séquence de tâches. L’application automatique des pilotes de périphérique présents dans le catalogue de pilotes n’est pas prise en charge, mais vous pouvez choisir l’étape Appliquer le package de pilotes pour mettre à la disposition du programme d’installation de Windows un ensemble de pilotes spécifique.
- Étape Télécharger le contenu du package dans la séquence de tâches. Les informations de point de gestion ne sont pas disponibles sur un média autonome. Par conséquent, l’étape échoue lors de la tentative d’énumération des emplacements de contenu.
- Installation de mises à jour logicielles.
- Installation du logiciel avant le déploiement du système d’exploitation.
- Séquences de tâches pour les déploiements autres que les déploiements de système d’exploitation.
- Association d'utilisateurs à l'ordinateur de destination pour prendre en charge l'affinité entre appareil et utilisateur.
- Le package dynamique s'installe via la tâche Installer les packages.
- L'application dynamique s'installe via la tâche Installer l'application.

> [!NOTE]    
> Si votre séquence de tâches servant à déployer un système d’exploitation comprend l’étape [Installer le package](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) et que vous créez le média autonome sur un site d’administration centrale, une erreur peut se produire. Le site d'administration centrale ne dispose pas des stratégies de configuration de client requises pour activer l'agent de distribution logicielle au cours de l'exécution de la séquence de tâches. L’erreur suivante peut apparaître dans le fichier CreateTsMedia.log :    
>     
> "WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"    
> 
> Dans le cas d’un média autonome qui comprend une étape **Installer le package**, vous devez créer le média autonome sur un site principal sur lequel l’agent de distribution logicielle est activé ou ajouter une étape [Exécuter la ligne de commande](../understand/task-sequence-steps.md#BKMK_RunCommandLine) après l’étape [Configurer Windows et ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) et avant la première étape **Installer le package** de la séquence de tâches. L'étape **Exécuter la ligne de commande** exécute une commande de ligne de commande WMIC pour activer l'agent de distribution logicielle avant l'exécution de la première étape Installer le package. Vous pouvez utiliser la ligne de commande suivante dans l'étape **Exécuter la ligne de commande** de votre séquence de tâches :    
>    
> *WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE*


> [!IMPORTANT]    
> Lorsque vous utilisez l’étape de la séquence de tâches **Configurer Windows et ConfigMgr** dans la séquence de tâches du système d’exploitation, ne sélectionnez pas le paramètre **Utiliser le package client de préproduction quand il est disponible** pour le média autonome. Si ce paramètre est sélectionné et que le package client de préproduction est disponible, il sera utilisé dans le média autonome. Cette fonctionnalité n’est pas prise en charge. Pour plus d’informations sur ce paramètre, consultez [Configurer Windows et ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr).


### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuer tout le contenu associé à la séquence de tâches
Vous devez distribuer tout le contenu exigé par la séquence de tâches à au moins un point de distribution. Cela inclut l’image de démarrage, l’image du système d’exploitation et les autres fichiers associés. L'Assistant collecte les informations à partir du point de distribution lorsqu'il crée le média autonome. Vous devez disposer de droits d’accès en **Lecture** à la bibliothèque de contenu sur ce point de distribution.  Pour plus d’informations, consultez [Distribuer du contenu référencé par une séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS).

### <a name="prepare-the-removable-usb-drive"></a>Préparer le lecteur USB amovible
*Lecteur USB amovible :*

Si vous envisagez d’utiliser un lecteur USB amovible, ce dernier doit être connecté à l’ordinateur sur lequel est exécuté l’Assistant et il doit être détectable par Windows en tant que périphérique amovible. L’Assistant écrit directement sur le lecteur USB quand il crée le média. Le média autonome utilise un système de fichiers FAT32. Vous ne pouvez pas créer de média autonome sur un disque mémoire flash USB dont le contenu inclut un fichier d'une taille supérieure à 4 Go.

### <a name="create-an-output-folder"></a>Créer un dossier de sortie
*Ensemble de CD/DVD :*

Avant d'exécuter l'Assistant Création d'un média de séquence de tâches afin de créer un média pour un ensemble de CD ou DVD, vous devez créer un dossier pour les fichiers de sortie créés par l'Assistant. Le média créé pour un ensemble de CD ou DVD est écrit sous forme de fichiers .iso directement dans le dossier.


 Utilisez la procédure suivante pour créer un média autonome pour un lecteur USB amovible ou un ensemble de CD/DVD.  

## <a name="to-create-stand-alone-media"></a>Pour créer un média autonome  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un média de séquence de tâches** pour démarrer l'Assistant Création d'un média de séquence de tâches.  

4.  Sur la page **Sélectionner le type de média** , spécifiez les options suivantes, puis cliquez sur **Suivant**.  

    -   Sélectionnez **Média autonome**.  

    -   Éventuellement, si vous souhaitez autoriser le déploiement du système d'exploitation sans intervention de l'utilisateur, sélectionnez **Autoriser le déploiement du système d'exploitation de manière autonome**. Lorsque vous sélectionnez cette option, l'utilisateur n'est pas invité à fournir des informations de configuration réseau ou des séquences de tâches facultatives. Toutefois, l'utilisateur est toujours invité à fournir un mot de passe si le média est configuré avec la protection par mot de passe.  

5.  Dans la page **Type de média** , spécifiez si le média est un disque mémoire flash ou un ensemble de CD/DVD, puis cliquez pour configurer les éléments suivants :  

    > [!IMPORTANT]  
    >  Le média autonome utilise un système de fichiers FAT32. Vous ne pouvez pas créer de média autonome sur un disque mémoire flash USB dont le contenu inclut un fichier d'une taille supérieure à 4 Go.  

    -   Si vous sélectionnez **Périphérique flash USB**, spécifiez le lecteur sur lequel stocker le contenu.  

    -   Si vous sélectionnez **Ensemble CD/DVD**, spécifiez la capacité du média et le nom et le chemin d'accès des fichiers de sortie. L'Assistant écrit les fichiers de sortie à cet emplacement. Par exemple : **\\\nom_serveur\dossier\fichier_sortie.iso**  

         Si la capacité du média est insuffisante pour stocker l’ensemble du contenu, plusieurs fichiers sont créés et vous devez stocker le contenu sur plusieurs CD ou DVD. Quand plusieurs médias sont nécessaires, Configuration Manager ajoute un numéro de séquence au nom de chaque fichier de sortie qu’il crée. De plus, si vous déployez une application en même temps que le système d’exploitation et que cette application ne peut pas tenir sur un seul média, Configuration Manager stocke l’application sur plusieurs médias. Quand le média autonome est exécuté, Configuration Manager invite l’utilisateur à insérer le média suivant sur lequel l’application est stockée.   

         > [!IMPORTANT]  
         >  Si vous sélectionnez une image .iso existante, l'Assistant Média de séquence de tâches supprime cette image du lecteur ou du partage dès lors que vous passez à la page suivante de l'Assistant. L'image existante est supprimée même si vous annulez ensuite l'Assistant.  

     Cliquez sur **Suivant**.  

6.  Sur la page **Sécurité**, choisissez parmi les paramètres suivants, puis cliquez sur **Suivant** :
    - **Protéger le média à l’aide d’un mot de passe** : entrez un mot de passe fort pour protéger le média. Si vous spécifiez un mot de passe, celui-ci est requis pour utiliser le média.  

        > [!IMPORTANT]  
        >  Sur un média autonome, seules les étapes de séquence de tâches et leurs variables sont chiffrées. Le reste du contenu du média n'est pas chiffré, donc n'incluez pas d'informations sensibles dans les scripts de séquence de tâches. Stockez et mettez en œuvre toutes les informations sensibles en utilisant des variables de séquence de tâches.  

    - **Sélectionner une plage de dates pour que le média autonome soit valide** (à partir de la version 1702) : définissez des dates de début et d’expiration facultatives sur le média. Ces paramètres sont désactivés par défaut. Les dates sont comparées à l’heure système de l’ordinateur avant l’exécution du support autonome. Lorsque l’heure du système est antérieure à l’heure de début ou ultérieure à l’heure d’expiration, le support autonome n’est pas démarré. Ces options sont également disponibles avec l’applet de commande New-CMStandaloneMedia PowerShell.
7.  Sur la page **CD/DVD autonome** , spécifiez la séquence de tâches qui déploie le système d'exploitation, puis cliquez sur **Suivant**. Choisissez **Détecter les dépendances d’application associées et les ajouter à ce média** afin d’ajouter du contenu au média autonome pour les dépendances d’application.
    > [!TIP]
    > Si les dépendances d’application attendues ne s’affichent pas, désélectionnez, puis sélectionnez à nouveau le paramètre **Détecter les dépendances d’application associées et les ajouter à ce média** pour actualiser la liste.

    L'Assistant vous permet de sélectionner uniquement les séquences de tâches qui sont associées à une image de démarrage.  

8. Sur la page **Sélectionner une application** (disponible à partir de la version 1702), spécifiez le contenu d’application à inclure dans le fichier du média, puis cliquez sur **Suivant**.
9. Sur la page **Sélectionner un package** (disponible à partir de la version 1702), spécifiez le contenu de package à inclure dans le fichier du média, puis cliquez sur **Suivant**.
10. Sur la page **Sélectionner le package de pilotes** (disponible à partir de la version 1702), spécifiez le contenu de package de pilotes à inclure dans le fichier du média, puis cliquez sur **Suivant**.
11.  Dans la page **Points de distribution** , spécifiez les points de distribution comprenant le contenu requis par la séquence de tâches, puis cliquez sur **Suivant**.  

     Configuration Manager n’affiche que les points de distribution qui disposent du contenu. Vous devez distribuer tout le contenu associé à la séquence de tâches (image de démarrage, image du système d’exploitation, etc.) sur au moins un point de distribution avant de continuer. Une fois le contenu distribué, vous pouvez redémarrer l’Assistant ou supprimer des points de distribution que vous avez déjà sélectionnés dans cette page, aller à la page précédente, puis revenir à la page **Points de distribution** pour actualiser la liste des points de distribution. Pour plus d’informations sur la distribution de contenu, consultez [Distribuer du contenu référencé par une séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS). Pour plus d’informations sur les points de distribution et la gestion de contenu, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    > [!NOTE]  
    >  Vous devez disposer de droits d’accès en **Lecture** à la bibliothèque de contenu sur les points de distribution.  

12. Sur la page **Personnalisation** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   Spécifiez les variables que la séquence de tâches utilise pour déployer le système d'exploitation.  

    -   Spécifiez les commandes de prédémarrage que vous voulez exécuter avant la séquence de tâches. Les commandes de prédémarrage sont un script ou un exécutable qui peut interagir avec l'utilisateur dans Windows PE avant que la séquence de tâches s'exécute pour installer le système d'exploitation. Pour plus d’informations sur les commandes de prédémarrage pour les médias, consultez [Commandes de prédémarrage pour les médias de séquence de tâches dans System Center Configuration Manager](../understand/prestart-commands-for-task-sequence-media.md).  

         Si vous le souhaitez, sélectionnez **Inclure les fichiers pour la commande de prédémarrage** pour inclure tous les fichiers requis pour la commande de prédémarrage.  

        > [!TIP]  
        >  Lors de la création du média de séquence de tâches, la séquence de tâches écrit l’ID du package et la ligne de commande de prédémarrage, dont la valeur des variables de la séquence de tâches, dans le fichier journal CreateTSMedia.log sur l’ordinateur qui exécute la console Configuration Manager. Vous pouvez consulter ce fichier journal pour vérifier la valeur des variables de séquence de tâches.  

13. Effectuez toutes les étapes de l'Assistant.  

 Les fichiers de média autonome (.iso) sont créés dans le dossier de destination. Si vous avez sélectionné **CD/DVD autonome**, vous pouvez maintenant copier les fichiers de sortie sur un ensemble de CD ou DVD.  

##  <a name="BKMK_StandAloneMediaTSExample"></a> Exemple de séquence de tâches pour un média autonome  
 Utilisez le tableau suivant comme guide lorsque vous créez une séquence de tâches afin de déployer un système d'exploitation à l'aide d'un média autonome. Ce tableau vous aidera à définir la séquence générale des étapes de votre séquence de tâches. Il vous permettra également d'organiser et de structurer ces étapes en groupes logiques. La séquence de tâches que vous créez peut être différente de celle de cet exemple, et elle peut contenir un nombre de groupes et d'étapes de séquence de tâches plus ou moins important.  

> [!NOTE]  
>  Vous devez toujours utiliser l'Assistant Média de séquence de tâches pour créer un média autonome.  

|Groupe ou étape de séquence de tâches|Description|  
|---------------------------------|-----------------|  
|Capturer les fichiers et les paramètres - **(Nouveau groupe de séquences de tâches)**|Créez un groupe de séquences de tâches. Un groupe de séquences de tâches regroupe des étapes de séquence de tâches similaires pour une meilleure organisation et un contrôle plus efficace des erreurs.|  
|Capturer les paramètres Windows|Utilisez cette étape de séquence de tâches pour identifier les paramètres Microsoft Windows qui sont capturés à partir du système d'exploitation existant sur l'ordinateur de destination avant de créer de nouvelles images. Vous pouvez capturer le nom de l'ordinateur, les informations utilisateur et organisationnelles et les paramètres des fuseaux horaires.|  
|Capturer les paramètres réseau|Utilisez cette étape de séquence de tâches pour capturer les paramètres réseau à partir de l'ordinateur qui reçoit la séquence de tâches. Vous pouvez capturer l'appartenance au domaine ou au groupe de travail de l'ordinateur et les informations du paramètre de la carte réseau.|  
|Capturer les paramètres et fichiers utilisateur - **(Nouveau sous-groupe de séquences de tâches)**|Créez un groupe de séquences de tâches au sein d'un groupe de séquences de tâches. Ce sous-groupe contient les étapes nécessaires à la capture des données d'état utilisateur à partir du système d'exploitation existant sur l'ordinateur de destination avant de créer de nouvelles images. Comme le groupe initial que vous avez ajouté, ce sous-groupe regroupe des étapes de séquence de tâches similaires pour une meilleure organisation et un contrôle plus efficace des erreurs.|  
|Définir l'emplacement d'état local|Utilisez cette étape de séquence de tâches pour spécifier un emplacement local à l'aide de la variable de séquence de tâches du chemin protégé. L'état utilisateur est stocké dans un répertoire protégé sur le disque dur.|  
|Capturer l'état utilisateur|Utilisez cette étape de séquence de tâches pour capturer les fichiers et paramètres utilisateur que vous souhaitez migrer sur le nouveau système d'exploitation.|  
|Installer le système d'exploitation - **(Nouveau groupe de séquences de tâches)**|Créez un autre sous-groupe de séquences de tâches. Ce sous-groupe contient les étapes nécessaires à l'installation du système d'exploitation.|  
|Redémarrer sur Windows PE ou disque dur|Utilisez cette étape de séquence de tâches pour spécifier les options de redémarrage pour l'ordinateur qui reçoit cette séquence de tâches. Cette étape affichera un message destiné à l'utilisateur et lui indiquant que l'ordinateur sera redémarré afin de poursuivre l'installation.<br /><br /> Cette étape utilise la variable de séquence de tâches **_SMSTSInWinPE** en lecture seule. Si la valeur associée est **false,** l'étape de la séquence de tâches se poursuivra.|  
|Appliquer le système d'exploitation|Utilisez cette étape de séquence de tâches pour installer une image de système d'exploitation sur l'ordinateur de destination. Cette étape supprime tous les fichiers de ce volume (à l’exception des fichiers de contrôle propres à Configuration Manager), puis applique toutes les images de volume contenues dans le fichier WIM au volume de disque séquentiel correspondant. Vous pouvez également spécifier un fichier de réponse **sysprep** pour configurer la partition de disque à utiliser pour l’installation.|  
|Appliquer les paramètres Windows|Utilisez cette étape de séquence de tâches pour configurer les informations de configuration des paramètres Windows pour l'ordinateur de destination. Les paramètres Windows que vous pouvez appliquer sont les informations utilisateur et organisationnelles, les informations principales sur le produit ou la clé de licence, les fuseaux horaires et le mot passe administrateur local.|  
|Appliquer les paramètres réseau|Utilisez cette étape de séquence de tâches pour spécifier les informations de configuration du réseau ou du groupe de travail pour l'ordinateur de destination. Vous pouvez également indiquer si l'ordinateur utilise un serveur DHCP ou vous pouvez attribuer en mode statique les informations de l'adresse IP.|  
|Appliquer le package de pilotes|Utilisez cette étape de séquence de tâches pour que tous les pilotes de périphérique d'un package de pilotes puissent être utilisés par le programme d'installation de Windows. Tous les pilotes de périphériques nécessaires doivent être contenus sur le média autonome.|  
|Configurer le système d'exploitation - **(Nouveau groupe de séquences de tâches)**|Créez un autre sous-groupe de séquences de tâches. Ce sous-groupe contient les étapes nécessaires à l’installation du client Configuration Manager.|  
|Configurer Windows et ConfigMgr|Cette étape de séquence de tâches permet d’installer le logiciel client Configuration Manager. Configuration Manager installe et inscrit le GUID du client Configuration Manager. Vous pouvez définir les paramètres d'installation nécessaires à partir de la fenêtre **Propriétés d'installation** .|  
|Restaurer les fichiers et paramètres utilisateur - **(Nouveau sous-groupe de séquences de tâches)**|Créez un autre sous-groupe de séquences de tâches. Ce sous-groupe contient les étapes nécessaires à la restauration de l'état utilisateur.|  
|Restaurer l'état utilisateur|Utilisez cette étape de séquence de tâches pour lancer l'outil de migration de l'état utilisateur afin de restaurer l'état et les paramètres utilisateur qui ont été capturés à partir de l'action Capturer l'état utilisateur sur l'ordinateur de destination.|  
