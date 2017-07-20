---
title: "Mises à jour dans la console | Microsoft Docs"
description: "System Center Configuration Manager se synchronise avec le cloud Microsoft pour obtenir les mises à jour que vous pouvez installer dans la console."
ms.custom: na
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 3619a73d3a39659de927e1711a7ec81de9918064
ms.openlocfilehash: 34ddb646137aaf1160d850ba7c1e0109f467225d
ms.contentlocale: fr-fr
ms.lasthandoff: 06/13/2017


---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Installation de mises à jour dans la console pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager se synchronise avec le service cloud Microsoft pour obtenir les mises à jour. Vous pouvez installer ces mises à jour à partir de la console Configuration Manager.

## <a name="get-available-updates"></a>Obtenir les mises à jour disponibles
Seules les mises à jour qui s’appliquent à votre infrastructure et à votre version sont téléchargées et mises à disposition dans votre hiérarchie. Cette synchronisation peut être automatique ou manuelle, selon la manière dont vous configurez le point de connexion de service pour votre hiérarchie :

-   En **mode en ligne**, le point de connexion de service se connecte automatiquement au service cloud Microsoft et télécharge les mises à jour applicables.  

     Par défaut, Configuration Manager vérifie la disponibilité de nouvelles mises à jour toutes les 24 heures. Vous pouvez également rechercher des mises à jour immédiatement en choisissant **Rechercher les mises à jour** dans le nœud **Administration** > **Mises à jour et maintenance** de la console Configuration Manager. (Avant la version 1702, ce nœud se trouvait sous **Administration** > **Services de cloud**.)

-   En **mode hors connexion**, le point de connexion de service ne se connecte pas au service cloud Microsoft. Pour télécharger puis importer les mises à jour disponibles, [utilisez l’outil de connexion de service pour System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

> [!NOTE]  
>   Vous pouvez importer des correctifs hors bande dans votre console. Pour cela, utilisez l’[outil Inscription de la mise à jour](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes). Ces correctifs hors bande complètent les mises à jour que vous obtenez lors de la synchronisation avec le service Microsoft Cloud.


Une fois les mises à jour synchronisées, vous pouvez les afficher dans la console Configuration Manager en accédant au nœud **Administration** > **Mises à jour et maintenance** :  

-   Les mises à jour que vous n’avez pas installées apparaissent **Disponibles**.

-   Les mises à jour que vous avez installées apparaissent **Installées**.  Seule la mise à jour installée le plus récemment s’affiche. Vous pouvez choisir le bouton **Historique** sur le ruban pour afficher les mises à jour installées précédemment.



Avant de configurer le point de connexion de service, vous devez comprendre et planifier ses utilisations supplémentaires. Les utilisations suivantes peuvent affecter la façon dont vous configurez ce rôle de système de site :  

-   Le point de connexion de service est utilisé pour charger les informations d’utilisation relatives à votre site. Ces informations permettent au service cloud de Microsoft d’identifier les mises à jour disponibles pour la version actuelle de votre infrastructure. Pour plus d’informations, consultez [Données d’utilisation et de diagnostic pour System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

-   Le point de connexion de service permet de gérer des appareils avec Microsoft Intune et à l’aide de la fonctionnalité de gestion des appareils mobiles locale de Configuration Manager. Pour plus d’informations, consultez [Gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

Pour mieux comprendre ce qui se passe quand des mises à jour sont téléchargées, consultez :  

-   [Organigramme - Téléchargement des mises à jour pour System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md)

-   [Organigramme - Réplication des mises à jour pour System Center Configuration Manager](../../../core/servers/manage/update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Attribuer les autorisations d’afficher et de gérer les mises à jour et les fonctionnalités
Pour qu’un utilisateur puisse afficher les mises à jour dans la console, un rôle de sécurité d’administration incluant la classe de sécurité **Packages de mise à jour** doit lui être attribué. Cette classe accorde l’autorisation d’afficher et de gérer les mises à jour dans la console Configuration Manager.    

**À propos de la classe Packages de mise à jour :**  
Par défaut, **Packages de mise à jour** (SMS_CM_Updatepackages) fait partie des rôles de sécurité intégrés suivants avec les autorisations répertoriées :
 -  **Administrateur complet** avec autorisations **Modifier** et **Lecture** :
    -   Un utilisateur disposant de ce rôle de sécurité et de l’accès à l’étendue de sécurité **Tout** peut afficher et installer les mises à jour. L’utilisateur peut également activer des fonctionnalités pendant l’installation et activer des fonctionnalités individuelles une fois la mise à jour installée.
    - Un utilisateur disposant de ce rôle de sécurité et de l’accès à l’étendue de sécurité **Par défaut** peut afficher et installer les mises à jour. L’utilisateur peut également activer des fonctionnalités pendant l’installation et afficher des fonctionnalités une fois la mise à jour installée. En revanche, cet utilisateur ne peut pas activer les fonctionnalités après l’installation de la mise à jour.

- **Analyste en lecture seule** avec autorisations **Lecture** :
  -  Un utilisateur disposant de ce rôle de sécurité et de l’accès à l’étendue **Par défaut** peut afficher les mises à jour mais pas les installer. Il peut également afficher les fonctionnalités après l’installation d’une mise à jour mais pas les activer.

**Autorisations requises pour les mises à jour et la maintenance :**   
  - Utilisez un compte affecté à un rôle de sécurité qui comprend la classe **Packages de mise à jour** avec les autorisations **Modifier** et **Lecture** .
  - L’étendue **Par défaut** doit être affectée au compte.

**Autorisations pour uniquement afficher les mises à jour** :
  - Utilisez un compte affecté à un rôle de sécurité qui comprend la classe **Packages de mise à jour** avec uniquement l’autorisation **Lecture** .
  - L’étendue **Par défaut** doit être affectée au compte.

**Autorisations requises pour activer des fonctionnalités après l’installation de mises à jour :**
  -  Utilisez un compte affecté à un rôle de sécurité qui comprend la classe **Packages de mise à jour** avec les autorisations **Modifier** et **Lecture** .
  -  L’étendue **Tout** doit être affectée au compte.



##  <a name="bkmk_beforeinstall"></a> Avant d’installer une mise à jour dans la console  
 Passez en revue les étapes suivantes avant d’installer une mise à jour à partir de la console Configuration Manager.  

###  <a name="bkmk_step1"></a> Étape 1 : consulter la liste de contrôle de mise à jour  
Passez en revue la liste de contrôle de mise à jour applicable pour connaître les actions à entreprendre avant de lancer la mise à jour :

- Mise à jour vers la version 1606 : consultez [Liste de contrôle pour l’installation de la mise à jour 1606](../../../core/servers/manage/checklist-for-installing-update-1606.md).  

- Mise à jour de la version 1606 vers la version 1610 : consultez [Liste de contrôle pour l’installation de la mise à jour 1610](../../../core/servers/manage/checklist-for-installing-update-1610.md).  

- Mise à jour de la version 1606 ou 1610 vers la version 1702 : consultez [Liste de contrôle pour l’installation de la mise à jour 1702](../../../core/servers/manage/checklist-for-installing-update-1702.md).

<!-- Removed as update guidance 6/6/2017. The Test DB Upgrade details are no longer recommended nor required. They live on in a new topic for customers who still want to use them. -->

###  <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a>Étape 2 : exécuter l’Outil de vérification des prérequis avant d’installer une mise à jour  
Avant d’installer une mise à jour, envisagez d’exécuter la vérification des prérequis pour cette mise à jour. Si vous effectuez cette vérification avant d’installer une mise à jour :  

-   Les fichiers de mise à jour sont répliqués vers d’autres sites avant l’installation de la mise à jour.  

-   La vérification des prérequis est automatiquement réexécutée lorsque vous choisissez d’installer la mise à jour.  

Par la suite, lorsque vous installez la mise à jour, vous pouvez configurer la mise à jour de manière à ignorer les avertissements relatifs à la vérification des prérequis.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Pour exécuter l’Outil de vérification des prérequis avant d’installer une mise à jour  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Mises à jour et maintenance**.   

2.  Cliquez avec le bouton droit sur le package de mise à jour pour lequel vous souhaitez exécuter la vérification des prérequis.  

3.  Choisissez **Exécuter la vérification de la condition préalable**.  

     Lorsque vous exécutez la vérification des prérequis, le contenu de la mise à jour est répliqué sur des sites enfants.  Vous pouvez consulter le fichier distmgr.log sur le serveur du site pour vérifier que le contenu est répliqué correctement.  

4.  Pour afficher les résultats de la vérification, dans la console Configuration Manager, accédez à **Surveillance** > **État des mises à jour et de la maintenance**, puis recherchez l’état du prérequis. Vous pouvez également consulter le fichier ConfigMgrPrereq.log sur le serveur du site pour plus de détails.  



##  <a name="bkmk_install"></a> Installation de mises à jour dans la console  
 Quand vous êtes prêt à installer des mises à jour à partir de la console Configuration Manager, commencez par le site de niveau supérieur de votre hiérarchie. Il s’agit soit du site d’administration centrale, soit d’un site principal autonome.  

 Nous vous recommandons d’installer la mise à jour en dehors des heures de bureau normales pour chaque site afin de minimiser l’impact sur les opérations commerciales. En effet, l’installation de la mise à jour peut inclure des actions telles que la réinstallation des composants de site et des rôles de système de site.  

-   Les sites principaux enfants démarrent la mise à jour automatiquement après que le site d’administration centrale a installé la mise à jour. Il s’agit du processus par défaut et recommandé. Vous pouvez cependant utiliser des [fenêtres de maintenance pour les serveurs de site](/sccm/core/servers/manage/service-windows) pour contrôler à quel moment le site principal installe les mises à jour.  

-   Après la mise à jour du site principal parent, mettez à jour manuellement les sites secondaires à partir de la console Configuration Manager. La mise à jour automatique des serveurs de sites secondaires n’est pas prise en charge.  

-   Quand vous utilisez une console Configuration Manager, vous êtes invité à mettre à jour la console après la mise à jour du site.  

-  Après avoir mené à bien l’installation d’une mise à jour, le serveur de site met automatiquement à jour tous les rôles de système de site applicables.  Le seul inconvénient concerne les points de distribution. Lors de l’installation d’une mise à jour, tous les points de distribution ne sont pas réinstallés et mis hors connexion pour être mis à jour simultanément. Au lieu de cela, le serveur de site utilise les paramètres de distribution de contenu du site pour distribuer la mise à jour à un sous-ensemble de points de distribution à la fois. Résultat : seuls certains points de distribution passent en mode hors connexion pour l’installation de la mise à jour. Les points de distribution dont la mise à jour n’a pas commencé ou est terminée restent en ligne et peuvent fournir du contenu aux clients.


###  <a name="bkmk_overview"></a> Vue d’ensemble de l’installation d’une mise à jour dans la console  
**1. Au démarrage de l’installation de la mise à jour**  
L’Assistant Mises à jour affiche la liste des zones de produit auxquelles s’applique la mise à jour.  

-   Dans la page **Général** de l’Assistant, vous pouvez configurer les **Avertissements relatifs à la configuration requise**.  
      -   Les erreurs de configuration requise bloquent toujours l’installation de la mise à jour. Corrigez les erreurs avant de réessayer d’installer correctement la mise à jour. Pour plus d’informations, consultez [Nouvelle tentative d’installation d’une mise à jour ayant échoué](#bkmk_retry) .  

    -   Des avertissements de configuration requise peuvent également bloquer l’installation de la mise à jour. Corrigez les avertissements avant de réessayer d’installer la mise à jour. Pour plus d’informations, consultez [Nouvelle tentative d’installation d’une mise à jour ayant échoué](#bkmk_retry).  
    -   L’option **Ignorer les avertissements relatifs aux conditions requises et installer cette mise à jour sans tenir compte des manquements à la configuration requise** définit une condition pour l’installation de la mise à jour qui ignore les avertissements relatifs aux prérequis. Cela permet de poursuivre l’installation de la mise à jour. Si vous ne sélectionnez pas cette option, l’installation de la mise à jour s’arrête en cas d’avertissement. Si vous n’avez pas exécuté la vérification des prérequis et corrigé les avertissements relatifs aux prérequis pour un site, nous vous déconseillons d’utiliser cette option.  

      Dans les espaces de travail **Administration** et **Surveillance**, le nœud Mises à jour et maintenance affiche un bouton **Ignorer les avertissements de configuration requise** sur le ruban. Ce bouton devient disponible quand l’installation d’un package de mise à jour n’arrive pas à terme en raison d’avertissements de vérification des prérequis. Par exemple, vous installez une mise à jour sans utiliser l’option pour ignorer les avertissements de configuration requise (à partir de l’Assistant Mises à jour). L’installation de la mise à jour s’interrompt, avec un état d’avertissement de configuration requise, mais sans erreur. Vous pouvez plus tard choisir d’**ignorer les avertissements de configuration requise** dans le ruban pour poursuivre automatiquement l’installation de cette mise à jour en ignorant les avertissements de configuration requise. Quand vous utilisez cette option, l’installation de la mise à jour se poursuit automatiquement après quelques minutes.



-   Quand une mise à jour s’applique au client Configuration Manager, une option vous est proposée pour tester la mise à jour du client avec un ensemble limité de clients. Pour plus d’informations, consultez [Guide pratique pour tester les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**2. Pendant l’installation de la mise à jour**  
Au cours de l’installation de la mise à jour, Configuration Manager :  

-   réinstalle tous les composants concernés, comme les rôles de système de site ou la console Configuration Manager ;  

-   gère les mises à jour des clients en fonction des sélections que vous avez effectuées pour le test du client et pour les [mises à niveau automatiques du client](https://technet.microsoft.com/library/mt627885.aspx) ;  

-   n’a pas besoin de redémarrer les serveurs de système de site dans le cadre de la mise à jour, à moins que .NET soit installé en raison d’un prérequis lié aux rôles de système de site.  

> [!TIP]  
>  Lors de l’installation des mises à jour, Configuration Manager met aussi à jour le dossier CD.Latest. Ce dossier est utilisé pendant la récupération d’un site.  

**3. Surveiller l’état d’avancement de l’installation de mises à jour**  
Pour surveiller l’état d’avancement, procédez comme suit :  

-   Dans la console Configuration Manager : nœud **Administration** > **Mises à jour et maintenance**. Ce nœud affiche l’état d’installation de tous les packages de mise à jour.


-   Dans la console Configuration Manager, accédez au nœud **Administration** > **Vue d’ensemble** > **Mises à jour et maintenance**. Ce nœud affiche l’état d’installation uniquement du package de mise à jour en cours d’installation.  

    L’installation du pack de mise à jour est décomposée selon les phases suivantes pour faciliter la surveillance. Pour chaque phase, des détails supplémentaires indiquent le fichier journal à consulter pour obtenir plus d’informations :  
    -   **Téléchargement** (cette phase s’applique uniquement au site de niveau supérieur où est installé le site du point de connexion de service.)   

    -   **Réplication**   

    -   **Vérification des prérequis**   

    -   **Installation**    

    -   **Après l’installation** (les [tâches post-installation](#post-installation-tasks) ont été introduites avec la version 1610.)  

-   Vous pouvez consulter le fichier **CMUpdate.log** dans **&lt;<Répertoire_Installation_ConfiMgr>\Logs**  

**4. Après l’installation de la mise à jour**  
Une fois l’installation de la mise à jour sur le premier site terminée :  

-   Les sites principaux enfants installent automatiquement la mise à jour. Aucune action supplémentaire n’est requise.  

-   Les sites secondaires doivent être mis à jour manuellement dans la console Configuration Manager.
> [!TIP]
> Bien que la version d’un site secondaire n’apparaisse pas dans la console, vous pouvez utiliser le Kit de développement logiciel (SDK) Configuration Manager pour vérifier la version d’un site. Voir [SMS_Site Server WMI Class](https://technet.microsoft.com/library/hh442832(CMSDK.16).aspx) (Classe WMI serveur SMS_Site).


-   Tant que tous les sites de votre hiérarchie n’ont pas été mis à jour vers la nouvelle version, la hiérarchie fonctionne en mode mixte de versions. Pour plus d'informations, voir [Interopérabilité entre les différentes versions de System Center Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

**5.   Mettre à jour des consoles Configuration Manager**  
Dès lors qu’un site d’administration centrale ou un site principal est mis à jour, chaque console Configuration Manager qui se connecte à ce site doit aussi être mise à jour. Vous êtes invité à mettre à jour une console dans les cas suivants :  

-   lorsque vous ouvrez la console ;  

-   lorsque vous accédez à un nouveau nœud dans une console ouverte.  

Nous vous recommandons d’installer la mise à jour immédiatement.  

Une fois la mise à niveau de la console terminée, vous pouvez vérifier que les versions de la console et du site sont correctes. Accédez à **À propos de System Center Configuration Manager** en haut à gauche de la console.  

###  <a name="bkmk_toptier"></a> Pour démarrer l’installation de la mise à jour sur le site de niveau supérieur  
Sur le site de niveau supérieur de votre hiérarchie, dans la console Configuration Manager, accédez à **Administration** > **Mises à jour et maintenance**, sélectionnez une mise à jour **Disponible**, puis cliquez sur **Installer le package de mise à jour**.  

###  <a name="bkmk_secondary"></a> Pour démarrer l’installation de la mise à jour sur un site secondaire  
Après la mise à jour du site principal parent d’un site secondaire, vous pouvez mettre à jour ce dernier à partir de la console Configuration Manager.  Pour ce faire, vous utilisez l’ **Assistant Mise à niveau d’un site secondaire**.  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Configuration du site** > **Sites**, sélectionnez le site à mettre à jour, puis, sous l’onglet Accueil, dans le groupe **Site**, choisissez **Mettre à niveau**.  

2.  Cliquez sur **Oui** pour démarrer la mise à jour du site secondaire.  

Pour surveiller l’installation de la mise à jour sur un site secondaire, sélectionnez le serveur de site secondaire. Ensuite, sous l’onglet **Accueil**, dans le groupe **Site**, choisissez **Afficher l’état d’installation**. Vous pouvez également ajouter la colonne **Version** à l’affichage de la console pour voir la version de chaque site secondaire.  

À l’issue de la mise à jour d’un site secondaire, si l’état dans la console ne s’actualise pas ou laisse supposer que la mise à jour a échoué, utilisez l’option **Réessayer l’installation**. Cette option ne réinstalle pas la mise à jour sur un site secondaire qui a correctement installé la mise à jour ; elle force la console à mettre à jour l’état.

### <a name="post-installation-tasks"></a>Tâches post-installation
Depuis la version 1610, vous pouvez afficher des informations sur les tâches post-installation.

Lorsqu’un site installe une mise à jour, plusieurs tâches ne peuvent pas démarrer tant que la mise à jour n’est pas installée sur le serveur de site. Voici une liste des tâches post-installation essentielles aux opérations de site et de hiérarchie. Ces tâches étant critiques, elles sont activement surveillées. D’autres tâches ne sont pas directement surveillées, par exemple la réinstallation de rôles de système de site. Pour afficher l’état des tâches post-installation critiques, sélectionnez une tâche **post-installation** lorsque vous surveillez l’installation de la mise à jour d’un site.

Toutes les tâches ne se terminent pas immédiatement. Certaines tâches ne démarrent pas tant que chaque site n’a pas terminé l’installation de la mise à jour. Les nouvelles fonctionnalités que vous souhaitez utiliser peuvent donc être retardées en attendant la fin de ces tâches. Par exemple, étant donné que l’activation des nouvelles fonctionnalités ne démarre pas tant que tous les sites ont terminé l’installation de la mise à jour, ces nouvelles fonctionnalités peuvent ne pas être visibles pendant un certain temps.

Les tâches post-installation incluent :

-   **Installation du service SMS_EXECUTIVE**
  -   Service critique qui s’exécute sur le serveur de site.
  -   La réinstallation de ce service devrait s’exécuter rapidement.


-   **Installation du composant SMS_DATABASE_NOTIFICATION_MONITOR**
  -   Thread de composant de site critique du service SMS_EXECUTIVE.
  -   La réinstallation de ce service devrait s’exécuter rapidement.


-   **Installation du composant SMS_HIERARCHY_MANAGER**
  -   Composant de site critique qui s’exécute sur le serveur de site.
  -   Responsable de la réinstallation des rôles de système de site sur les serveurs de système de site.  L’état de la réinstallation d’un rôle de système de site individuel n’apparaît pas.
  -   La réinstallation de ce service devrait s’exécuter rapidement.


-   **Installation du composant SMS_REPLICATION_CONFIGURATION_MONITOR**
  -   Composant de site critique qui s’exécute sur le serveur de site.
  -   La réinstallation de ce service devrait s’exécuter rapidement.


-   **Installation du composant SMS_POLICY_PROVIDER**
  -   Composant de site critique qui s’exécute uniquement sur les sites principaux.
  -   La réinstallation de ce service devrait s’exécuter rapidement.


-   **Surveillance de l’initialisation de la réplication**   
  -   Cette tâche s’affiche uniquement sur le site d’administration centrale et sur les sites principaux enfants.
  -   Dépend de SMS_REPLICATION_CONFIGURATION_MONITOR.
  -   Devrait s’exécuter rapidement.


-   **Mise à jour du package de préproduction du client Configuration Manager**    
  -   S’affiche même lorsque client de préproduction (également appelé pilotage du client) n’est pas activé pour être utilisé.
  -   Ne commence pas tant que tous les sites dans la hiérarchie n’ont pas terminé l’installation de la mise à jour.


-   **Mise à jour du dossier du client sur le serveur de site**
  -   Ne s’affiche pas si vous utilisez le client en préproduction.  
  -   Devrait s’exécuter rapidement.


-   **Mise à jour du package du client Configuration Manager**
  -   Ne s’affiche pas si vous utilisez le client en préproduction.  
  -   Se termine uniquement une fois que tous les sites ont installé la mise à jour.  


-   **Activation des fonctionnalités**
  -   S’affiche uniquement sur le site de niveau supérieur de la hiérarchie.
  -   Ne commence pas tant que tous les sites dans la hiérarchie n’ont pas terminé l’installation de la mise à jour.
  -   Les fonctionnalités individuelles ne sont pas affichées.


##  <a name="bkmk_retry"></a> Nouvelle tentative d’installation d’une mise à jour ayant échoué  
Quand l’installation d’une mise à jour échoue, passez en revue les commentaires dans la console pour identifier les résolutions possibles des avertissements et des erreurs. Vous pouvez également consulter le fichier ConfigMgrPrereq.log sur le serveur du site pour plus de détails. Avant de réessayer l’installation d’une mise à jour, vous devez corriger les erreurs et il est recommandé de corriger aussi les avertissements.  

Quand vous êtes prêt à réessayer l’installation d’une mise à jour, sélectionnez la mise à jour ayant échoué, puis choisissez une option applicable. Le comportement de nouvelle tentative d’installation de mise à jour dépend du nœud où vous lancez la nouvelle tentative et de l’option de nouvelle tentative que vous utilisez.  

1.  **Réessayer l’installation pour la hiérarchie :**  
Vous pouvez réessayer l’installation d’une mise à jour pour l’ensemble de la hiérarchie lorsque cette mise à jour est dans l’un des états suivants :  

    -   La vérification des prérequis a généré un ou plusieurs avertissements, et l’option permettant d’ignorer les avertissements de vérification des prérequis n’a pas été activée dans l’Assistant Mise à jour. (La valeur de mise à jour pour **Ignorer l’avertissement de condition préalable** dans le nœud **Mises à jour et maintenance** est **Non**.)   
    -   La vérification des prérequis a échoué.    
    -   L’installation a échoué.
    -   La réplication du contenu sur le site a échoué.   

    Accédez à **Administration** > **Mises à jour et maintenance**, sélectionnez la mise à jour, puis choisissez l’une des options suivantes :  

    -   **Nouvelle tentative** : quand vous exécutez **Nouvelle tentative** à partir de ce nœud, l’installation de la mise à jour redémarre et ignore automatiquement les avertissements relatifs aux prérequis. Le contenu pour la mise à jour est uniquement répliqué si la réplication a échoué précédemment.
    - **Ignorer les avertissements de configuration requise** : à compter de la version 1606, si l’installation de la mise à jour s’arrête en raison d’un avertissement, vous pouvez choisir **Ignorer les avertissements de configuration requise**. Cette action permet à l’installation de la mise à jour de continuer (après quelques minutes) et utilise l’option pour ignorer les avertissements de configuration requise.   

2.  **Réessayer l’installation pour le site :**  
 Vous pouvez réessayer l’installation d’une mise à jour sur un site spécifique lorsque cette mise à jour est dans l’un des états suivants :  

    -   La vérification des prérequis a généré un ou plusieurs avertissements, et l’option permettant d’ignorer les avertissements de vérification des prérequis n’a pas été activée dans l’Assistant Mise à jour. (La valeur de mise à jour pour **Ignorer l’avertissement de condition préalable** dans le nœud Mises à jour et maintenance est **Non**.)  
    -   La vérification des prérequis a échoué.    
    -   L’installation a échoué.    

    Accédez à **Surveillance** > **Vue d’ensemble** > **État de la maintenance de site**, sélectionnez la mise à jour, puis cliquez sur l’une des options suivantes :

       - **Nouvelle tentative** : quand vous exécutez **Nouvelle tentative** à partir de ce nœud, vous redémarrez l’installation de la mise à jour uniquement sur ce site. Contrairement à l’exécution de **Nouvelle tentative** à partir du nœud **Mises à jour et maintenance**, cette nouvelle tentative n’ignore pas les avertissements relatifs aux prérequis.
       -    **Ignorer les avertissements de configuration requise** : à compter de la version 1606, si l’installation de la mise à jour s’arrête en raison d’un avertissement, vous pouvez cliquer sur **Ignorer les avertissements de configuration requise**. Cette action permet à l’installation de la mise à jour de continuer (après quelques minutes) et utilise l’option pour ignorer les avertissements de prérequis.

##  <a name="bkmk_after"></a> Après l’installation d’une mise à jour sur un site  
Utilisez la liste de vérification suivante pour effectuer les tâches courantes et les configurations nécessaires après la mise à jour d’un site.   

**Vérifier que la réplication de site à site est active :** dans la console Configuration Manager, accédez aux emplacements suivants pour consulter l’état et vérifier que la réplication est active :  

-   **Surveillance** > **Vue d’ensemble** > **Hiérarchie de site**  

-   **Surveillance** > **Vue d’ensemble** > **Réplication de base de données**  

Pour plus d’informations, consultez [Surveiller l’infrastructure de la hiérarchie et de la réplication dans System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) et [À propos de l’analyseur de lien de réplication](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Vérifier que les serveurs de site et les serveurs de système de site distants ont redémarré (si nécessaire) :** examinez l’infrastructure de votre site et vérifiez que les serveurs de site et serveurs de système de site appropriés ont redémarré correctement. En règle générale, les serveurs de site redémarrent uniquement quand Configuration Manager installe .NET en tant que prérequis pour un rôle de système de site.  

 **Mettre à jour les consoles Configuration Manager autonomes :** vérifiez que toutes les consoles Configuration Manager distantes ont été mises à jour vers la même version. Vous êtes invité à mettre à jour la console dans les cas suivants :  

-   lorsque vous accédez à un nouveau nœud dans la console ;  

-   lorsque vous ouvrez la console.

**Reconfigurer les réplicas de base de données pour les points de gestion sur les sites principaux :** si vous utilisez des réplicas de base de données pour les points de gestion sur les sites principaux, vous devez désinstaller les réplicas de base de données avant de mettre à jour le site. Après avoir mis à niveau un site principal, reconfigurez le réplica de base de données pour les points de gestion. Pour plus d’informations, consultez [Réplicas de base de données pour les points de gestion de System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigurer les tâches de maintenance de base de données désactivées avant la mise à jour :** si vous avez désactivé les [tâches de maintenance](../../../core/servers/manage/maintenance-tasks.md) sur un site avant d’installer la mise à jour, reconfigurez ces tâches sur le site. Utilisez les mêmes paramètres qui étaient en vigueur avant la mise à jour.  

**Mettre à niveau les clients :** pour plus d’informations, consultez [Guide pratique pour mettre à niveau les clients pour les ordinateurs Windows dans System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

**Configurations supplémentaires :** examinez les modifications que vous avez apportées avant de commencer la mise à jour, puis restaurez ces configurations sur vos sites et votre hiérarchie.  

##  <a name="bkmk_options"></a> Activation de fonctionnalités facultatives de mises à jour  
Lorsqu’une mise à jour inclut une ou plusieurs fonctionnalités facultatives, vous avez la possibilité d’activer celles-ci dans votre hiérarchie.  Vous pouvez activer les fonctionnalités au moment de l’installation de la mise à jour ou revenir à la console ultérieurement pour activer les fonctionnalités facultatives.

Pour afficher les fonctionnalités disponibles et leur état, dans la console, accédez à **Administration** > **Mises à jour et maintenance** > **Fonctionnalités**.

Quand une fonctionnalité n’est pas facultative, elle est installée automatiquement et n’apparaît pas dans le nœud **Fonctionnalités**.  


Quand vous activez une nouvelle fonctionnalité ou une fonctionnalité en préversion, le Gestionnaire de hiérarchie de Configuration Manager (HMAN) doit traiter le changement avant que cette fonctionnalité ne soit disponible. Le traitement du changement est souvent immédiat, mais il peut prendre jusqu’à 30 minutes en fonction du cycle de traitement HMAN. Une fois le changement traité, vous devez redémarrer la console pour voir la nouvelle interface utilisateur associée à cette fonctionnalité.


##  <a name="bkmk_prerelease"></a> Utiliser des fonctionnalités de préversions de mises à jour
Les fonctionnalités de préversion sont incluses dans la branche Current Branch à des fins de test préalable dans un environnement de production. Vous pouvez utiliser ces fonctionnalités dans un environnement de production, mais elles ne doivent pas être considérées comme prêtes pour la production. Pour en savoir plus sur les fonctionnalités de préversion, y compris sur la façon de les activer dans votre environnement, consultez [Fonctionnalités de préversion](/sccm/core/servers/manage/pre-release-features).             


## <a name="known-issues"></a>Problèmes connus

###  <a name="bkmk_faq"></a> Pourquoi certaines mises à jour ne s’affichent pas dans ma console ?  
 Si vous ne trouvez pas une mise à jour spécifique dans votre console après une synchronisation réussie avec le service cloud Microsoft, les causes possibles sont les suivantes :  

-   La mise à jour requiert une configuration que votre infrastructure n’utilise pas, ou votre version actuelle du produit ne remplit pas une condition préalable pour la réception de la mise à jour.  

     Si vous pensez que vous disposez des configurations requises et prérequis pour une mise à jour manquante, vérifiez que votre point de connexion de service est en mode en ligne. Ensuite, utilisez l’option **Rechercher les mises à jour** dans le nœud **Mises à jour et maintenance** pour forcer la vérification.  Si vous êtes en mode hors connexion, vous devez recourir à l’outil de connexion au service pour synchroniser manuellement le service cloud.  

-   Votre compte ne dispose pas des autorisations d’administration basée sur des rôles appropriées pour afficher les mises à jour dans la console Configuration Manager.

    Pour plus d’informations sur les autorisations requises pour afficher les mises à jour et activer les fonctionnalités à partir de la console, consultez [Autorisations de gérer les mises à jour](../../../core/servers/manage/install-in-console-updates.md#assign-permissions-to-view-and-manage-updates-and-features) dans cette rubrique.

### <a name="why-do-i-see-two-updates-for-version-1610"></a>Pourquoi deux mises à jour sont-elles proposées pour la version 1610 ?
Il peut arriver que deux mises à jour vers la version 1610 soient répertoriées dans la console. Les mises à jour ont des dates différentes. Ces deux mises à jour s’affichent lorsqu’une des conditions suivantes est vraie :   
-   Après la publication de la version 1610, vous avez installé une version antérieure (par exemple, la version 1606).

-   Votre hiérarchie exécute la version 1511 ou 1602 et vous n’avez pas pu télécharger la version 1606

Il existe deux mises à jour vers la version 1610, car des modifications mineures ont été apportées à certains binaires de fichier après la publication de la première mise à jour. Ces modifications n’affectent pas les fonctionnalités de Configuration Manager ni la mise à jour.

Si les deux mises à jour sont disponibles dans la console, nous vous recommandons d’installer la plus récente. Toutefois, étant donné que les mises à jour offrent les mêmes fonctionnalités, aucune action de votre part n’est nécessaire si vous avez déjà installé l’une d’entre elles.
-   Si vous avez installé l’ancienne mise à jour, il est inutile d’installer la mise à jour plus récente. Toutefois, si vous installez la nouvelle mise à jour après avoir installé la première mise à jour, les fichiers binaires en question seront mis à jour. Aucune modification supplémentaire ne se produit, et aucune action supplémentaire de votre part n’est nécessaire.

-   Si vous avez installé la dernière mise à jour et que vous installez ensuite l’ancienne, aucune action supplémentaire n’est nécessaire. Cela est dû au fait que les derniers binaires qui sont déjà installés ne sont pas remplacés par les mêmes binaires de la mise à jour d’origine.

