---
title: Upgrade Readiness | System Center Configuration Manager
description: "Intégrez Upgrade Readiness à Configuration Manager. Accédez aux données de compatibilité de mise à niveau dans votre console d’administration. Ciblez des appareils pour la mise à niveau ou la mise à jour."
keywords: 
author: mattbriggs
ms.author: mabrigg
manager: angerobe
ms.date: 7/31/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: b1f4cd4a6f19a02d2b2dc3f9a841aeeb2a1403dd
ms.contentlocale: fr-fr
ms.lasthandoff: 07/29/2017

---

# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>Intégrer Upgrade Readiness à System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Upgrade Readiness (anciennement Upgrade Analytics) vous permet d’évaluer et d’analyser l’état de préparation des appareils et leur compatibilité avec Windows 10. Intégrez Upgrade Readiness à Configuration Manager pour accéder aux données de compatibilité de mise à niveau du client dans la console d’administration de Configuration Manager. Vous pouvez cibler des appareils pour la mise à niveau ou la mise à jour dans la liste d’appareils.

Upgrade Readiness est une solution incluse dans Microsoft Operations Management Suite (OMS). Pour en savoir plus sur Upgrade Readiness, consultez [Bien démarrer avec Upgrade Readiness](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).

## <a name="configure-clients"></a>Configurer des clients

Il existe plusieurs étapes de configuration pour vérifier que vos clients peuvent fournir des données à Upgrade Readiness :

-  Configurez les paramètres de télémétrie du client comme décrit dans [Configurer la télémétrie Windows dans votre organisation](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).
-  Installez les bases de connaissances décrites dans la section *Déployer la mise à jour de compatibilité et les bases de connaissances associées* de l’article [Bien démarrer avec Upgrade Readiness](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).

    > [!NOTE]
    > Vous pouvez télécharger un script pour automatiser de nombreuses tâches d’installation du client. Consultez la section *Exécuter le script de déploiement d’Upgrade Readiness* de la rubrique [Bien démarrer avec Upgrade Readiness](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness) pour plus d’informations sur le script.

## <a name="connect-to-upgrade-readiness"></a>Se connecter à Upgrade Readiness

### <a name="prerequisites"></a>Prérequis

À compter de Current Branch version 1706, l’Assistant Services Azure est utilisé pour simplifier le processus de configuration des services Azure que vous utilisez avec Configuration Manager. Pour pouvoir utiliser l’Assistant, vous devez configurer une application web Azure. Pour plus d’informations, consultez [Assistant Services Azure](/sccm/core/servers/deploy/configureazure-services-wizard).

### <a name="use-the-azure-wizard-to-create-the-connection"></a>Utiliser l’Assistant Azure pour créer la connexion

1.  Dans l’espace de travail **Administration** de la console Configuration Manager, développez **Services cloud**, puis cliquez sur **Services Azure**.
2.  Sur l’onglet **Accueil**, sous le groupe **Services Azure**, cliquez sur **Configurer les services Azure**.
3.  Tapez un nom convivial dans la page Services Azure. Vous pouvez également taper une description. Ensuite, sélectionnez **Connecteur Upgrade Readiness** et cliquez sur **Suivant**.
4.  Dans la page Application, spécifiez votre environnement Azure. Cliquez sur **Parcourir** pour configurer une application serveur.
5.  Cliquez sur **Importer** pour vous connecter à votre application Web dans Azure.
    -  Tapez le **Nom du locataire Azure AD**.
    -  Tapez l’**ID du locataire Azure AD**.
    -  Tapez le **Nom de l’application**.
    -  Tapez l’**ID du client**.
    -  Tapez la **Clé secrète**.
    -  Sélectionnez la date d’expiration dans **Expiration de la clé secrète**.
    -  Tapez une URL dans **URI d’ID d’application**.
    -  Cliquez sur **Vérifier**, puis sur **OK**.

6.  Spécifiez la connexion à Upgrade Readiness dans la page Configuration. Sélectionnez les valeurs suivantes :  
    -  Abonnements Azure
    -  Groupe de ressources Azure
    -  Espace de travail Windows Analytics
8.  Cliquez sur **Suivant**. Vous pouvez passer en revue votre connexion dans la page Résumé. 

## <a name="complete-upgrade-readiness-tasks"></a>Effectuer les tâches d’Upgrade Readiness  

Une fois la connexion créée, effectuez les tâches suivantes. Celle-ci sont décrites dans [Bien démarrer avec Upgrade Readiness](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).  

1. Ajoutez le service UpgradeReadiness à l’espace de travail OMS.  
2. Générez un ID commercial.  
3. Abonnez-vous à Upgrade Readiness.   

## <a name="use-the-upgrade-readiness-deployment-script"></a>Utiliser le script de déploiement d’Upgrade Readiness  

Vous pouvez automatiser de nombreuses tâches d’Upgrade Readiness et résoudre des problèmes de partage de données avec le **script de déploiement de Microsoft Upgrade Readiness**.  
Le script de déploiement d’Upgrade Readiness effectue les tâches suivantes :  

- Définit la clé ID commercial et les clés CommercialDataOptIn et RequestAllAppraiserVersions.  
- Vérifie que les ordinateurs des utilisateurs peuvent envoyer des données à Microsoft.  
- Vérifie si l’ordinateur a un redémarrage en attente.   
- Vérifie que la dernière version du package de bases de connaissances 10.0.x est installée (nécessite la version 10.0.14913 ou ultérieure).  
- S’il est activé, active le mode détaillé pour la résolution des problèmes.  
- Lance la collecte des données de télémétrie dont Microsoft a besoin pour évaluer l’état de préparation de votre organisation pour la mise à niveau.  
- S’il est activé, affiche la progression du script dans une fenêtre cmd. Vous bénéficiez ainsi d’une visibilité des problèmes (succès ou échec pour chaque étape) et/ou des écritures dans le fichier journal.  

## <a name="to-run-the-upgrade-readiness-deployment-script"></a>Pour exécuter le script de déploiement d’Upgrade Readiness :  

1. Téléchargez le [script de déploiement d’Upgrade Readiness](https://go.microsoft.com/fwlink/?LinkID=822966&clcid=0x409) et extrayez UpgradeReadiness.zip. Les fichiers du dossier **Diagnostics** sont nécessaires uniquement si vous projetez d’exécuter le script en mode de résolution de problèmes.  
2. Modifiez ces paramètres dans RunConfig.bat :  
- Emplacement de stockage des informations du journal. Exemple : %SystemDrive%\URDiagnostics. Vous pouvez stocker les informations du journal dans un partage de fichiers distant ou un répertoire local. Si le script ne peut pas créer le fichier journal dans le chemin indiqué, il crée les fichiers journaux dans le lecteur contenant le répertoire Windows.  
- Clé ID commercial.  
- Par défaut, le script envoie les informations du journal à la console et au fichier journal. Pour modifier le comportement par défaut, utilisez l’une des options suivantes :  
    - logMode = 0 écrit les informations dans la console uniquement  
    - logMode = 1 écrit les informations dans le fichier et la console  
    - logMode = 2 écrit les informations dans le fichier uniquement  
    - Pour la résolution des problèmes, définissez **isVerboseLogging** avec la valeur **$true** pour générer des informations de journal pouvant faciliter le diagnostic des problèmes. Par défaut, **isVerboseLogging** a la valeur **$false**. Vérifiez que le dossier Diagnostics est installé dans le même répertoire que le script pour utiliser ce mode.  
    - Informez les utilisateurs s’ils doivent redémarrer leur ordinateur. Par défaut, ce paramètre est désactivé.  

3. Une fois que vous avez modifié les paramètres dans RunConfig.bat, exécutez le script en tant qu’administrateur.  


## <a name="view-microsoft-upgrade-readiness-properties-in-configuration-manager"></a>Afficher les propriétés de Microsoft Upgrade Readiness dans Configuration Manager  

1.  Dans la console Configuration Manager, accédez à **Services cloud**, puis choisissez **Connecteur OMS** pour ouvrir la page **Propriétés de connexion OMS**.  

2.  Cette page contient deux onglets :
  * L’onglet **Azure Active Directory** affiche votre **Locataire**, l’**ID Client**, l’**Expiration de la clé secrète client** et vous permet de **vérifier** votre **Clé secrète client** si elle a expiré.
  * L’onglet **Upgrade Readiness** affiche vos valeurs pour les champs **Abonnement Azure**, **Groupe de ressources Azure** et **Espace de travail Operations Management Suite**.

## <a name="view-and-use-the-upgrade-information"></a>Afficher et utiliser les informations de mise à niveau

Une fois que vous avez intégré Upgrade Readiness à Configuration Manager, vous pouvez afficher l’analyse de la préparation de vos clients pour la mise à niveau et agir en conséquence.

1. Dans la console Configuration Manager, choisissez **Surveillance** > **Vue d’ensemble** > **Upgrade Readiness**.
2. Passez en revue les données, notamment l’état de préparation à la mise à niveau et le pourcentage d’appareils Windows qui envoient des données de télémétrie.
3. Vous pouvez filtrer le tableau de bord pour afficher les données d’appareils dans des regroupements spécifiques.
4. Vous pouvez afficher les appareils dans un état de préparation particulier et créer un regroupement dynamique pour ces derniers afin de pouvoir les mettre à niveau s’ils sont prêts ou effectuer les actions nécessaires pour les préparer à la mise à niveau.

## <a name="create-a-connection-to-upgrade-readiness-1702-and-earlier"></a>Créer une connexion à Upgrade Readiness (1702 et antérieur)

Avant la branche 1706 de Configuration Manager, vous deviez effectuer les étapes suivantes pour créer une connexion à Upgrade Readiness.

### <a name="prerequisites"></a>Prérequis

- Pour ajouter la connexion, votre environnement Configuration Manager doit d’abord configurer un [point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point) dans un [mode en ligne](https://azure.microsoft.com/documentation/articles/resource-group-create-service-principal-portal/). Quand vous ajoutez la connexion à votre environnement, Microsoft Monitoring Agent est également installé sur l’ordinateur exécutant ce rôle de système de site.
- Inscrivez Configuration Manager comme outil de gestion « Application web et/ou API web » et obtenez l’[ID de client résultant de cette inscription](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Créer une clé de client pour l’outil de gestion inscrit dans Azure Active Directory.
- Dans le portail Azure, autorisez l’application web inscrite à accéder à OMS en suivant les étapes décrites dans [Accorder à Configuration Manager les autorisations d’accès à OMS](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

    > [!IMPORTANT]
    > Quand vous configurez l’autorisation d’accès à OMS, choisissez le rôle **Collaborateur** et accordez-lui les autorisations sur le groupe de ressources de l’application inscrite.

### <a name="create-the-connection"></a>Créer la connexion

1.  Dans la console Configuration Manager, choisissez **Administration** > **Services cloud** > **Connecteur Upgrade Readiness** > **Créer une connexion à Upgrade Analytics** pour démarrer l’**Assistant Ajout d’une connexion Upgrade Analytics**.
3.  Dans l’écran **Azure Active Directory**, indiquez les valeurs de **Locataire**, **ID de client** et **Clé secrète du client**, puis sélectionnez **Suivant**.
4.  Dans l’écran **Upgrade Readiness**, définissez vos paramètres de connexion en renseignant les champs **Abonnement Azure**, **Groupe de ressources Azure** et **Espace de travail Operations Management Suite**.
5.  Vérifiez vos paramètres de connexion dans l’écran **Résumé**, puis sélectionnez **Suivant**.

    > [!NOTE]
    > Vous devez connecter Upgrade Readiness au site de niveau supérieur de votre hiérarchie. Si vous connectez Upgrade Readiness à un site principal autonome et que vous ajoutez ensuite un site d’administration centrale à votre environnement, vous devez supprimer et recréer la connexion OMS au sein de la nouvelle hiérarchie.

