---
title: Upgrade Analytics | System Center Configuration Manager
description: "Intégrez Upgrade Analytics à Configuration Manager. Accédez aux données de compatibilité de mise à niveau dans votre console d’administration. Ciblez des appareils pour la mise à niveau ou la mise à jour."
keywords: 
author: brenduns
ms.author: brenduns
manager: angerobe
ms.date: 12/3/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
translationtype: Human Translation
ms.sourcegitcommit: 831d8a66c827d246069c7415cdce7a7c4bb95b33
ms.openlocfilehash: 07747b86bad0d1ce6302521093fc3c4433c59325


---

# <a name="integrate-upgrade-analytics-with-system-center-configuration-manager"></a>Intégrer Upgrade Analytics à System Center Configuration Manager

Upgrade Analytics vous permet d’évaluer et d’analyser l’état de préparation de l’appareil et la compatibilité avec Windows 10 pour faciliter et améliorer les mises à niveau. Intégrer Upgrade Analytics à Configuration Manager pour accéder aux données de compatibilité de mise à niveau du client dans la console d’administration de Configuration Manager. Vous pouvez ensuite cibler des appareils pour la mise à niveau ou la mise à jour dans la liste d’appareils.

Upgrade Analytics est une solution incluse dans Microsoft Operations Management Suite (OMS). Pour en savoir plus sur Upgrade Analytics, consultez [Bien démarrer avec Upgrade Analytics](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started).

## <a name="configure-clients"></a>Configurer des clients

Il existe plusieurs étapes de configuration pour vérifier que vos clients peuvent fournir des données à Upgrade Analytics :

-  Configurez les paramètres de télémétrie du client comme décrit dans [Configurer la télémétrie Windows dans votre organisation](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).
-  Installez les bases de connaissances décrites dans la section *Deploy the compatibility update and related KBs* (Déployer la mise à jour de compatibilité et les bases de connaissances associées) de [Get started with Upgrade Analytics](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started) (Bien démarrer avec Upgrade Analytics).

    > [!NOTE]
    > Vous pouvez télécharger un script pour automatiser de nombreuses tâches d’installation du client. Consultez la section *Run the Upgrade Analytics deployment script* (Exécuter le script de déploiement Upgrade Analytics) de [Get started with Upgrade Analytics](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started) (Bien démarrer avec Upgrade Analytics) pour plus d’informations sur le script.

## <a name="create-a-connection-to-upgrade-analytics"></a>Créer une connexion à Upgrade Analytics

### <a name="prerequisites"></a>Conditions préalables

- Pour ajouter la connexion, votre environnement Configuration Manager doit d’abord configurer un [point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point) dans un [mode en ligne](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/). Quand vous ajoutez la connexion à votre environnement, Microsoft Monitoring Agent est également installé sur l’ordinateur exécutant ce rôle de système de site.
- Inscrivez Configuration Manager comme outil de gestion « Application web et/ou API web » et obtenez l’[ID de client résultant de cette inscription](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Créer une clé de client pour l’outil de gestion inscrit dans Azure Active Directory.
- Dans le portail de gestion Azure, accordez à l’application web inscrite l’autorisation d’accès à OMS, comme décrit dans [Accorder à Configuration Manager les autorisations d’accès à OMS](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

    > [!IMPORTANT]
    > Quand vous configurez l’autorisation d’accès à OMS, choisissez le rôle **Collaborateur** et accordez-lui les autorisations sur le groupe de ressources de l’application inscrite.

### <a name="create-the-connection"></a>Créer la connexion

1.  Dans la console Configuration Manager, choisissez **Administration** > **Services cloud** > **Connecteur Upgrade Analytics** > **Créer une connexion à Upgrade Analytics** pour démarrer l’**Assistant Ajout d’une connexion Upgrade Analytics**.
3.  Dans l’écran **Azure Active Directory**, indiquez les valeurs de **Locataire**, **ID de client**, et **Clé secrète du client**, puis sélectionnez **Suivant**.
4.  Dans l’écran **Upgrade Analytics**, définissez vos paramètres de connexion en renseignant les champs **Abonnement Azure**, **Groupe de ressources Azure** et **Espace de travail Operations Management Suite**.
5.  Vérifiez vos paramètres de connexion dans l’écran **Résumé**, puis sélectionnez **Suivant**.

    > [!NOTE]
    > Vous devez connecter Upgrade Analytics au site de niveau supérieur de votre hiérarchie. Si vous connectez Upgrade Analytics à un site principal autonome et que vous ajoutez ensuite un site d’administration centrale à votre environnement, vous devez supprimer et recréer la connexion OMS au sein de la nouvelle hiérarchie.

### <a name="complete-upgrade-analytics-tasks"></a>Effectuer des tâches Upgrade Analytics  

Une fois que vous avez créé la connexion dans Configuration Manager, effectuez ces tâches, comme décrit dans [Get started with Upgrade Analytics](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started) (Bien démarrer avec Upgrade Analytics).  

1. Ajoutez le service UpgradeAnalytics à l’espace de travail OMS.  
2. Générez un ID commercial.  
3. Abonnez-vous à Upgrade Analytics.   

## <a name="use-the-upgrade-analytics-deployment-script"></a>Utiliser le script de déploiement Upgrade Analytics  

Vous pouvez automatiser de nombreuses tâches Upgrade Analytics et résoudre des problèmes de partage de données avec le **script de déploiement Microsoft Upgrade Analytics**.  
Le script de déploiement Upgrade Analytics effectue les tâches suivantes :  

- Définit la clé ID commercial et les clés CommercialDataOptIn et RequestAllAppraiserVersions.  
- Vérifie que les ordinateurs des utilisateurs peuvent envoyer des données à Microsoft.  
- Vérifie si l’ordinateur a un redémarrage en attente.   
- Vérifie que la dernière version du package de bases de connaissances 10.0.x est installée (nécessite la version 10.0.14913 ou ultérieure).  
- S’il est activé, active le mode détaillé pour la résolution des problèmes.  
- Lance la collecte des données de télémétrie dont Microsoft a besoin pour évaluer l’état de préparation de votre organisation pour la mise à niveau.  
- S’il est activé, affiche la progression du script dans une fenêtre de commande, ce qui vous apporte une visibilité sur les problèmes (réussite ou échec de chaque étape), et/ou écrit dans le fichier journal.  

### <a name="to-run-the-upgrade-analytics-deployment-script"></a>Pour utiliser le script de déploiement Upgrade Analytics :  

1. Téléchargez le [script de déploiement Upgrade Analytics](https://go.microsoft.com/fwlink/?LinkID=822966&clcid=0x409) et extrayez UpgradeAnalytics.zip. Les fichiers du dossier **Diagnostics** sont nécessaires uniquement si vous projetez d’exécuter le script en mode de résolution de problèmes.  
2. Modifiez ces paramètres dans RunConfig.bat :  
- Emplacement de stockage des informations du journal. Exemple : %SystemDrive%\UADiagnostics. Vous pouvez stocker les informations du journal dans un partage de fichiers distant ou un répertoire local. Si le script ne peut pas créer le fichier journal dans le chemin indiqué, il crée les fichiers journaux dans le lecteur contenant le répertoire Windows.  
- Clé ID commercial.  
- Par défaut, le script envoie les informations du journal à la console et au fichier journal. Pour modifier le comportement par défaut, utilisez l’une des options suivantes :  
    - logMode = 0 écrit les informations dans la console uniquement  
    - logMode = 1 écrit les informations dans le fichier et la console  
    - logMode = 2 écrit les informations dans le fichier uniquement  
    - Pour la résolution des problèmes, définissez **isVerboseLogging** avec la valeur **$true** pour générer des informations de journal pouvant faciliter le diagnostic des problèmes. Par défaut, **isVerboseLogging** a la valeur **$false**. Vérifiez que le dossier Diagnostics est installé dans le même répertoire que le script pour utiliser ce mode.  
    - Informez les utilisateurs s’ils doivent redémarrer leur ordinateur. Par défaut, ce paramètre est désactivé.  

3. Une fois que vous avez modifié les paramètres dans RunConfig.bat, exécutez le script en tant qu’administrateur.  


## <a name="view-microsoft-upgrade-analytics-properties-in-configuration-manager"></a>Afficher les propriétés de Microsoft Upgrade Analytics dans Configuration Manager  

1.  Dans la console Configuration Manager, accédez à **Services cloud**, puis choisissez **Connecteur OMS** pour ouvrir la page **Propriétés de connexion OMS**.  

2.  Cette page contient deux onglets :
  * L’onglet **Azure Active Directory** affiche votre **Locataire**, l’**ID Client**, l’**Expiration de la clé secrète client** et vous permet de **vérifier** votre **Clé secrète client** si elle a expiré.
  * L’onglet **Upgrade Analytics** affiche vos valeurs pour les champs **Abonnement Azure**, **Groupe de ressources Azure** et **Espace de travail Operations Management Suite**.

## <a name="view-and-use-the-upgrade-information"></a>Afficher et utiliser les informations de mise à niveau

Une fois que vous avez intégré Upgrade Analytics à Configuration Manager, vous pouvez afficher l’analyse de la préparation de vos clients pour la mise à niveau et agir en conséquence.

1. Dans la console Configuration Manager, choisissez **Surveillance** > **Vue d’ensemble** > **Upgrade Analytics**.
2. Passez en revue les données, notamment l’état de préparation à la mise à niveau et le pourcentage d’appareils Windows qui envoient des données de télémétrie.
3. Vous pouvez filtrer le tableau de bord pour afficher les données d’appareils dans des regroupements spécifiques.
4. Vous pouvez afficher les appareils dans un état de préparation particulier et créer un regroupement dynamique pour ces derniers afin de pouvoir les mettre à niveau s’ils sont prêts ou effectuer les actions nécessaires pour les préparer à la mise à niveau.



<!--HONumber=Feb17_HO2-->


