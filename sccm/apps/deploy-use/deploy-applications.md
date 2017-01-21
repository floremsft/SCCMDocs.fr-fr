---
title: "Déployer des applications | Microsoft Docs"
description: "Créez un type de déploiement ou simulez le déploiement d’une application à l’aide de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 7be9abadeb51d4f9e862f69c332756b19ce3e110
ms.openlocfilehash: a52bef3c8d12ffe2d9b13dc79cbc8950d3f36aea


---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Déployer des applications avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Avant de pouvoir déployer une application System Center Configuration Manager, vous devez créer au moins un type de déploiement pour cette application. Pour plus d’informations sur la création d’applications et de types de déploiements, consultez [Créer des applications](../../apps/deploy-use/create-applications.md).

 Vous pouvez aussi simuler un déploiement d’application. Ce type de déploiement teste l’applicabilité du déploiement d’une application sur des ordinateurs, sans installation ou désinstallation de l’application. Un déploiement simulé évalue la méthode de détection, les spécifications et les dépendances d’un type de déploiement, et génère un rapport contenant les résultats dans le nœud **Déploiements** de l’espace de travail **Surveillance**. Pour plus d’informations, consultez [Simuler des déploiements d’applications](../../apps/deploy-use/simulate-application-deployments.md).

> [!IMPORTANT]
>  Vous pouvez déployer (c’est-à-dire installer ou désinstaller) les applications nécessaires, mais pas les packages ni les mises à jour logicielles. Les appareils inscrits à la gestion MDM ne prennent pas non plus en charge les déploiements simulés, l’expérience utilisateur ou les paramètres de planification.

## <a name="deploy-an-application"></a>Déployer une application

1.  Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.

2.  Dans la liste **Applications** , sélectionnez l'application à déployer. Ensuite, sous l’onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**.

### <a name="specify-general-information-about-the-deployment"></a>Spécifier des informations générales sur le déploiement

Dans la page **Général** de l’Assistant Déploiement logiciel, spécifiez les informations suivantes :

- **Logiciel** : Indique l’application à déployer. Vous pouvez cliquer sur **Parcourir** pour sélectionner une autre application.
- **Regroupement** : Cliquez sur **Parcourir** pour sélectionner le regroupement sur lequel vous voulez déployer l’application.
- **Utiliser des groupes de points de distribution par défaut associés à ce regroupement** : Sélectionnez cette option si vous voulez stocker le contenu de l’application dans le groupe de points de distribution par défaut du regroupement. Si vous n’avez associé aucun groupe de points de distribution au regroupement sélectionné, cette option est grisée.
- **Distribuer automatiquement le contenu pour les dépendances** : Si cette option est activée et que l’un des types de déploiement de l’application contient des dépendances, alors le contenu de l’application dépendante est également envoyé aux points de distribution.

    >[!IMPORTANT]
    > Si vous mettez à jour l'application dépendante après le déploiement de l'application principale, les nouveaux contenus de la dépendance ne seront pas distribués automatiquement.

- **Commentaires (champ facultatif)** : si vous le souhaitez, entrez une description de ce déploiement.

### <a name="specify-content-options-for-the-deployment"></a>Spécifier les options de contenu pour le déploiement

Dans la page **Contenu**, cliquez sur **Ajouter** pour ajouter le contenu associé à ce déploiement aux points de distribution ou aux groupes de points de distribution. Si vous avez sélectionné **Utiliser des groupes de points de distribution par défaut associés à ce regroupement** dans la page **Général**, cette option est automatiquement renseignée et peut uniquement être modifiée par un membre du rôle de sécurité Administrateur d’application.

### <a name="specify-deployment-settings"></a>Spécifier des paramètres de déploiement

Dans la page **Paramètres de déploiement** de l’Assistant Déploiement logiciel, spécifiez les informations suivantes :

- **Action** : Dans la liste déroulante, choisissez si ce déploiement est destiné à **Installer** ou **Désinstaller** l’application.

    > [!NOTE]
    >  Si une application est déployée deux fois sur un appareil, une fois avec l'action **Installer** et une autre fois avec l'action **Désinstaller**, le déploiement de l'application avec l'action **Installer** aura la priorité.

Il n'est pas possible de modifier l'action d'un déploiement après sa création.

- **Objet** : Dans la liste déroulante, choisissez l’une des options suivantes :
    - **Disponible** : Si l’application est déployée sur un utilisateur, celui-ci peut voir l’application publiée dans le Centre logiciel et il peut l’installer à la demande.
    - **Obligatoire** : L’application est déployée automatiquement, selon la planification. Si l’état du déploiement de l’application n’est pas masqué, toute personne utilisant l’application peut suivre l’état de son déploiement et installer l’application à partir du Centre logiciel avant l’échéance.

    > [!NOTE]   
    >  Lorsque l'action de déploiement est définie sur **Désinstaller**, l'objet du déploiement est automatiquement défini sur **Obligatoire** et ne peut plus être modifié.  

- **Déployer automatiquement en fonction de la planification, qu’un utilisateur soit connecté ou non** : Si le déploiement s’effectue sur un utilisateur, sélectionnez cette option pour déployer l’application sur les appareils principaux de l’utilisateur. Ce paramètre ne nécessite pas que l'utilisateur se connecter avant que déploiement ne s'exécute. Ne sélectionnez pas cette option si l'utilisateur doit fournir une entrée pour terminer l'installation. Cette option est disponible uniquement lorsque l'objet du déploiement est **Obligatoire**.


- **Envoyer des paquets de mise en éveil** : Si l’objet du déploiement est défini sur **Obligatoire** et que cette option est sélectionnée, un paquet de mise en éveil est envoyé aux ordinateurs avant l’installation du déploiement. Ce paquet réveille les ordinateurs à l’échéance de l’installation. Pour que vous puissiez utiliser cette option, les ordinateurs et les réseaux doivent être configurés pour utiliser l'éveil par appel réseau.
- **Autoriser les clients avec une connexion Internet facturée à l’usage à télécharger le contenu une fois l’échéance d’installation atteinte, ce qui peut entraîner des frais supplémentaires** : Cette option est disponible uniquement pour les déploiements dont l’objet est **Obligatoire**.
- **Exiger l’approbation de l’administrateur si des utilisateurs demandent cette application** : Si cette option est sélectionnée, l’administrateur doit approuver toutes les demandes d’utilisateur pour l’application avant qu’elle puisse être installée. Cette option est grisée quand l’objet du déploiement est **Obligatoire** ou quand l’application est déployée sur un regroupement d’appareils.

    > [!NOTE]
    >  Les demandes d'approbation d'application sont affichées dans le nœud **Demandes d'approbation** , sous **Gestion d'applications** dans l'espace de travail **Bibliothèque de logiciels** . Si une demande ne reçoit pas d’approbation dans les 45 jours, elle est supprimée. En outre, la réinstallation du client Configuration Manager pourrait annuler des demandes d’approbation en attente.
    > Une fois que vous avez approuvé l’installation d’une application, vous pouvez ensuite choisir de refuser la demande en cliquant sur **Refuser** dans la console Configuration Manager (précédemment, ce bouton était grisé après l’approbation).
    > Cette action n’entraîne pas la désinstallation de l’application sur tous les appareils, mais elle empêche les utilisateurs d’installer de nouvelles copies de l’application à partir du Centre logiciel.



- **Mettre automatiquement à niveau toutes les versions remplacées de cette application** : Si cette option est sélectionnée, toutes les versions remplacées de l’application sont mises à niveau avec l’application de remplacement.

### <a name="specify-scheduling-settings-for-the-deployment"></a>Spécifier les paramètres de planification pour le déploiement

Dans la page **Planification** de l’Assistant Déploiement logiciel, définissez le moment où cette application sera déployée ou mise à la disposition des appareils clients.
Les options de cette page pourront différer selon si l'action de déploiement est définie sur **Disponible** ou sur **Obligatoire**.

Dans certains cas, vous pouvez accorder plus de temps aux utilisateurs pour installer les mises à jour logicielles ou les déploiements d’applications obligatoires au-delà des échéances que vous avez définies. Cela est généralement nécessaire quand un ordinateur a été éteint pendant une période de temps prolongée et qu’il doit installer un grand nombre de déploiements d’applications ou de mises à jour. Par exemple, si un utilisateur vient de rentrer de congés, il peut être amené à patienter longtemps pendant l’installation des déploiements d’applications en retard. Pour résoudre ce problème, vous pouvez désormais définir une période de grâce de mise en œuvre en déployant des paramètres du client Configuration Manager sur un regroupement.

Pour configurer la période de grâce, procédez comme suit :

- Dans la page **Agent ordinateur** des paramètres du client, configurez la nouvelle propriété **Période de grâce pour la mise en œuvre après l’échéance du déploiement (en heures)** avec une valeur comprise entre **1** et **120** heures.
- Dans la page **Planification** d’un nouveau déploiement d’application obligatoire, ou dans les propriétés d’un déploiement existant, cochez la case **Différer la mise en œuvre de ce déploiement selon les préférences de l’utilisateur, dans la limite de la période de grâce définie dans les paramètres client**. La période de grâce de mise en œuvre est utilisée par tous les déploiements pour lesquels cette case est cochée et qui sont destinés à des appareils sur lesquels vous avez également déployé le paramètre client.

Une fois l’échéance d’installation de l’application atteinte, cette dernière est installée dans la première fenêtre non professionnelle que l’utilisateur a configurée après cette période de grâce. Toutefois, l’utilisateur peut toujours ouvrir le Centre logiciel et installer l’application à tout moment, s’il le souhaite. Une fois que la période de grâce a expiré, le comportement de mise en œuvre redevient normal pour les déploiements en retard.

Si l’application que vous déployez remplace une autre application, vous pouvez définir l’échéance d’installation quand les utilisateurs reçoivent la nouvelle application. Pour cela, utilisez le paramètre **Échéance d’installation** pour mettre à niveau les utilisateurs avec l’application remplacée.

### <a name="specify-user-experience-settings-for-the-deployment"></a>Spécifier les paramètres d’expérience utilisateur pour le déploiement


Dans la page **Expérience utilisateur** de l’Assistant Déploiement logiciel, spécifiez la façon dont les utilisateurs peuvent interagir avec l’installation de l’application.

Lorsque vous déployez des applications sur des appareils Windows Embedded dont le filtre d'écriture est activé, vous pouvez choisir d'installer l'application sur un segment de recouvrement temporaire puis de valider les modifications ultérieurement, ou de valider les modifications à l'échéance de l'installation ou au cours d'une fenêtre de maintenance. Quand vous validez des modifications au moment de l’échéance d’installation ou pendant une fenêtre de maintenance, vous devez redémarrer l’appareil. Les modifications sont conservées sur l’appareil.

>[!NOTE]
    >  Lorsque vous déployez une application sur un appareil Windows Embedded, assurez-vous que l'appareil fait partie des membres d'un regroupement pour lequel une fenêtre de maintenance a été configurée. Pour plus d’informations sur l’utilisation de fenêtres de maintenance pendant le déploiement d’applications sur des appareils Windows Embedded, consultez [Créer des applications Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).

    >  The options **Software Installation** and **System restart (if required to complete the installation)** are not used if the deployment purpose is set to **Available**. You can also configure the level of notification a user sees when the application is installed.

### <a name="specify-alert-options-for-the-deployment"></a>Spécifier les options d’alerte pour le déploiement

Dans la page **Alertes** de l’Assistant Déploiement logiciel, configurez comment Configuration Manager et System Center Operations Manager génèrent des alertes pour ce déploiement. Vous pouvez configurer des seuils pour les alertes de rapport et désactiver les rapports pendant la durée du déploiement.

### <a name="associate-the-deployment-with-an-ios-app-configuration-policy"></a>Associer le déploiement à une stratégie de configuration d’application iOS

Dans la page **Stratégies de configuration des applications**, cliquez sur **Nouveau** pour associer ce déploiement à une stratégie de configuration d’application iOS (si vous en avez créé une). Pour plus d’informations sur ce type de stratégie, consultez [Configurer des applications iOS avec des stratégies de configuration des applications](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).

### <a name="finish-up"></a>Terminer

Dans la page **Résumé** de l’Assistant Déploiement logiciel, vérifiez les actions qui seront effectuées dans le cadre du déploiement, puis cliquez sur **Suivant** pour terminer l’Assistant.

Le nouveau déploiement sera affiché dans la liste **Déploiements** du nœud **Déploiements** de l'espace de travail **Surveillance** . Vous pouvez modifier les propriétés de ce déploiement ou le supprimer de l'onglet **Déploiements** du volet Détail de l'application.

## <a name="delete-an-application-deployment"></a>Supprimer le déploiement d’une application

1.  Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.

3.  Dans la liste **Applications**, sélectionnez l’application qui inclut le déploiement à supprimer.

4.  Sous l’onglet **Déploiements** de la liste *<nom_application\>*, sélectionnez le déploiement d’application à supprimer. Ensuite, sous l’onglet **Déploiement**, dans le groupe **Déploiement**, cliquez sur **Supprimer**.

 Lorsque vous supprimez un déploiement d'application, les instances déjà installées de l'application ne sont pas supprimées. Pour supprimer ces applications, vous devez déployer l’application sur des ordinateurs avec **Désinstaller**. Si vous supprimez un déploiement d’application ou que vous retirez une ressource du regroupement sur lequel le déploiement a lieu, l’application ne sera plus visible dans le Centre logiciel.

## <a name="user-notifications-for-required-deployments"></a>Notifications à l’utilisateur pour les déploiements obligatoires
Quand vous recevez des logiciels obligatoires, dans le paramètre **Répéter et me le rappeler**, vous pouvez choisir une valeur dans la liste déroulante suivante :
- **Plus tard** : Spécifie que les notifications sont planifiées selon les paramètres de notification configurés dans les paramètres de l’agent du client.
- **Durée fixe** : Indique que la notification est planifiée pour s’afficher de nouveau après la durée sélectionnée. Par exemple, si vous sélectionnez 30 minutes, la notification s’affiche de nouveau au bout de 30 minutes.

![Page Agent ordinateur dans les paramètres de l’agent du client](media/ComputerAgentSettings.png)

L’intervalle de répétition maximal est toujours basé sur les valeurs de notification configurées dans les paramètres de l’agent du client à tout instant le long de la chronologie du déploiement. Par exemple, si le paramètre **Échéance du déploiement supérieure à 24 heures, effectuer un rappel à l’utilisateur toutes les (heures)** dans la page **Agent ordinateur** est configuré pour 10 heures et qu’il reste plus de 24 heures avant l’échéance du lancement de la boîte de dialogue, vous pouvez choisir une valeur dans un ensemble d’options de répétition inférieures ou égales à 10 heures. Au fur et à mesure que l’échéance approche, la boîte de dialogue affiche moins d’options, conformément aux paramètres appropriés de l’agent du client, pour chaque composant de la chronologie du déploiement.

Par ailleurs, pour un déploiement à haut risque, comme une séquence de tâches déployant un système d’exploitation, l’expérience de notification à l’utilisateur final est désormais plus intrusive. Au lieu d’une notification temporaire sur la barre des tâches, chaque fois que vous êtes averti qu’une maintenance logicielle critique est nécessaire, une boîte de dialogue similaire à la suivante s’affiche sur votre ordinateur :

![Boîte de dialogue Logiciel requis](media/client-toast-notification.png)

## <a name="for-more-information"></a>Pour plus d’informations :
- [Paramètres de gestion des déploiements à haut risque](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Guide pratique pour configurer les paramètres client](../../core/clients/deploy/configure-client-settings.md)



<!--HONumber=Dec16_HO3-->


