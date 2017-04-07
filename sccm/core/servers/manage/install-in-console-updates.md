---
title: "Mises à jour dans la console | Microsoft Docs"
description: "System Center Configuration Manager se synchronise avec le cloud Microsoft pour obtenir les mises à jour que vous pouvez installer dans la console."
ms.custom: na
ms.date: 3/7/2017
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
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 3b50ada9f63e41d1b6f01009c141b8f361f5180e
ms.lasthandoff: 03/27/2017


---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Installation de mises à jour dans la console pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager se synchronise avec le service cloud Microsoft pour obtenir les mises à jour. Vous pouvez installer ces mises à jour à partir de la console Configuration Manager.

## <a name="get-available-updates"></a>Obtenir les mises à jour disponibles
Seules les mises à jour qui s’appliquent à votre infrastructure et à votre version sont téléchargées et mises à disposition dans votre hiérarchie. Cette synchronisation peut être automatique ou manuelle, selon la manière dont vous configurez le point de connexion de service pour votre hiérarchie :

-   En **mode en ligne**, le point de connexion de service se connecte automatiquement au service cloud Microsoft et télécharge les mises à jour applicables.  

     Par défaut, Configuration Manager vérifie la disponibilité de nouvelles mises à jour toutes les 24 heures. Vous pouvez également rechercher des mises à jour immédiatement en choisissant **Rechercher les mises à jour** dans le nœud **Administration** > **Mises à jour et maintenance** de la console Configuration Manager. (Avant la version 1702, ce nœud se trouvait sous **Administration** > **Services de cloud**.)

-   En **mode hors connexion**, le point de connexion de service ne se connecte pas au service cloud Microsoft. Vous devez manuellement [utiliser l’outil de connexion de service pour System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md) pour télécharger et importer les mises à jour disponibles.  

> [!NOTE]  
>  Outre les mises à jour que vous obtenez lors de la synchronisation avec le service cloud Microsoft, les correctifs hors bande installés par l’[outil Inscription de la mise à jour](http://technet.microsoft.com/library/mt691544.aspx) sont également importés dans votre console, où vous pouvez ensuite les sélectionner pour les installer.  

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
Pour qu’un utilisateur puisse afficher les mises à jour dans la console, un rôle de sécurité d’administration incluant la classe de sécurité nommée **Packages de mise à jour** doit lui être affecté. Cette classe accorde l’autorisation d’afficher et de gérer les mises à jour dans la console Configuration Manager.    

**À propos de la classe Packages de mise à jour :**  
Par défaut, **Packages de mise à jour** (SMS_CM_Updatepackages) fait partie des rôles de sécurité intégrés suivants avec les autorisations répertoriées :
 -  **Administrateur complet** avec autorisations **Modifier** et **Lecture** :
    -   Un utilisateur disposant de ce rôle de sécurité et de l’accès à l’étendue de sécurité **Tout** peut afficher les mises à jour, installer des mises à jour et activer des fonctionnalités pendant l’installation. Il peut également activer des fonctionnalités individuelles après l’installation de la mise à jour.
    - Un utilisateur disposant de ce rôle de sécurité et de l’accès à l’étendue de sécurité **Par défaut** peut afficher les mises à jour, installer des mises à jour et activer des fonctionnalités pendant l’installation. Il peut également afficher les fonctionnalités après l’installation d’une mise à jour. En revanche, cet utilisateur ne peut pas activer les fonctionnalités après l’installation de la mise à jour.

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

###  <a name="bkmk_step2"></a> Étape 2 : tester la mise à niveau de base de données avant d’installer une mise à jour  
Les informations de cette étape s’appliquent uniquement à l’installation d’une *mise à jour* pour un site System Center Configuration Manager. Si vous effectuez une *mise à niveau* d’un site System Center 2012 Configuration Manager vers System Center Configuration Manager, consultez [Tester la mise à niveau de base de données de site](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#a-namebkmktesta-test-the-site-database-upgrade).

Avant d’installer une nouvelle mise à jour dans votre hiérarchie, telle que la mise à jour 1610, vous pouvez tester la mise à niveau de votre base de données de site. Le nom de l’option en ligne de commande permettant de tester l’installation d’une mise à jour sur une sauvegarde de votre base de données de site est **testdbupgrade**.  

Si l’installation d’une mise à jour échoue, vous ne devriez pas avoir besoin de procéder à une récupération de site. Au lieu de cela, vous pouvez réessayer l’installation de la mise à jour. Par conséquent, même si le test de mise à niveau de la base de données est moins important que dans les versions antérieures du produit, telles que System Center 2012 Configuration Manager, cette étape reste recommandée.


#### <a name="to-run-testdbupgrade-before-installing-an-update"></a>Pour exécuter testdbupgrade avant d’installer une mise à jour  

1.  Obtenez un ensemble de fichiers sources à partir du dossier **CD.Latest** d’un site qui exécute la version vers laquelle vous prévoyez d’effectuer la mise à jour. Vous pouvez être contraint d’installer d’abord un site dans un environnement lab ou de test exécutant cette version de System Center Configuration Manager.  

     Le dossier **CD.Latest** d’un site contient les fichiers sources pour cette version. Vous devez utiliser ceux-ci pour exécuter le test de mise à niveau de la base de données de votre site. Pour plus d’informations, voir [Dossier CD.Latest pour System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md).  

     Par exemple, si votre site exécute la version 1606 et que vous souhaitez mettre à jour vers la version 1610, vous devez obtenir un dossier CD.Latest d’un site qui a déjà effectué la mise à jour vers la version 1610. En règle générale, vous pouvez installer un nouveau site temporaire dans un environnement lab, puis procéder à sa mise à niveau vers la version 1610 pour créer le dossier CD.Latest avec les fichiers requis.  

2.  Copiez le dossier CD.Latest vers un emplacement sur l’instance SQL Server que vous utiliserez pour tester la mise à niveau de la base de données.

3.  Créez une sauvegarde de la base de données de site dont vous souhaitez tester la mise à niveau, puis restaurez une copie de cette base de données sur une instance de SQL Server qui n’héberge pas de site Configuration Manager. L’instance SQL Server doit utiliser la même édition de SQL Server que votre base de données de site.  

4.  Après avoir restauré la copie de la base de données, exécutez **Setup** à partir du dossier CD.Latest que vous avez copié à partir de votre environnement lab ou de test. Lorsque vous exécutez le programme d'installation, utilisez l'option de ligne de commande **/TESTDBUPGRADE** . Si l'instance SQL Server qui héberge la copie de la base de données n'est pas l'instance par défaut, vous devez également fournir les arguments de ligne de commande pour identifier l'instance qui héberge la copie de la base de données du site.  

     Par exemple, supposons que vous prévoyez de mettre à niveau une base de données de site dont le nom est SMS_ABC. Vous restaurez une copie de cette base de données de site sur une instance prise en charge de SQL Server ayant pour nom d'instance DBTest. Pour tester une mise à niveau de cette copie de la base de données du site, utilisez la ligne de commande suivante : **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     Vous trouverez Setup.exe à l’emplacement suivant sur le média source de System Center Configuration Manager : **SMSSETUP\BIN\X64**.  

5.  Sur l’instance de SQL Server exécutant le test de la mise à niveau de la base de données, examinez le fichier ConfigMgrSetup.log à la racine du lecteur système afin de déterminer la progression et l’issue du test :  

     Si le test de mise à niveau de la base de données du site échoue, corrigez les problèmes liés à cet échec, créez une sauvegarde de la base de données du site, puis testez la mise à niveau de la nouvelle copie de la base de données du site.  

     Une fois que le processus a abouti, vous pouvez supprimer la copie de la base de données.  

    > [!NOTE]  
    >  Il n'est pas possible de restaurer la copie de la base de données du site que vous utilisez dans le cadre du test de mise à niveau afin de l'utiliser comme base de données d'un site quelconque.  

###  <a name="bkmk_step3"></a> Étape 3 : exécuter l’Outil de vérification des prérequis avant d’installer une mise à jour  
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

 Nous vous recommandons de prévoir d’installer la mise à jour en dehors des heures de bureau normales pour chaque site. Le processus d’installation de la mise à jour et ses actions pour réinstaller les composants du site et les rôles système de site auront alors le moins d’effet sur l’activité de votre entreprise.  

-   Les sites principaux enfants démarrent la mise à jour automatiquement après que le site d’administration centrale a installé la mise à jour. Il s’agit du processus par défaut et recommandé. Vous pouvez cependant utiliser des [fenêtres de maintenance pour les serveurs de site](/sccm/core/servers/manage/service-windows) pour contrôler à quel moment le site principal installe les mises à jour.  

-   Après la mise à jour du site principal parent, vous devez mettre à jour manuellement les sites secondaires à partir de la console Configuration Manager. La mise à jour automatique des serveurs de sites secondaires n’est pas prise en charge.  

-   Quand vous utilisez une console Configuration Manager, vous êtes invité à mettre à jour la console après la mise à jour du site.  

-  Après avoir mené à bien l’installation d’une mise à jour, le serveur de site met automatiquement à jour tous les rôles de système de site applicables.  Le seul inconvénient concerne les points de distribution. Lors de l’installation d’une mise à jour, tous les points de distribution ne sont pas réinstallés et mis hors connexion pour être mis à jour simultanément. Au lieu de cela, le serveur de site utilise les paramètres de distribution de contenu du site pour distribuer la mise à jour à un sous-ensemble de points de distribution à la fois. Résultat : seuls certains points de distribution passent en mode hors connexion pour l’installation de la mise à jour. Ainsi, les points de distribution dont la mise à jour n’a pas encore commencé ou est terminée restent en ligne et peuvent fournir du contenu aux clients.


###  <a name="bkmk_overview"></a> Vue d’ensemble de l’installation d’une mise à jour dans la console  
**1. Au démarrage de l’installation de la mise à jour**  
L’Assistant Mises à jour affiche la liste des zones de produit auxquelles s’applique la mise à jour.  

-   Dans la page **Général** de l’Assistant, vous pouvez configurer les **Avertissements relatifs à la configuration requise**.  
      -   Les erreurs de configuration requise bloquent toujours l’installation de la mise à jour. Vous devez corriger les erreurs avant de réessayer d’installer correctement la mise à jour. Pour plus d’informations, consultez [Nouvelle tentative d’installation d’une mise à jour ayant échoué](#bkmk_retry) .  

    -   Des avertissements de configuration requise peuvent également bloquer l’installation de la mise à jour. Vous devez corriger les avertissements avant de réessayer d’installer la mise à jour. Pour plus d’informations, consultez [Nouvelle tentative d’installation d’une mise à jour ayant échoué](#bkmk_retry) .  
    -   L’option **Ignorer les avertissements relatifs aux conditions requises et installer cette mise à jour sans tenir compte des manquements à la configuration requise** définit une condition pour l’installation de la mise à jour qui ignore les avertissements relatifs aux prérequis. Cela permet de poursuivre l’installation de la mise à jour. Si vous ne sélectionnez pas cette option, l’installation de la mise à jour s’arrête en cas d’avertissement. Si vous n’avez pas exécuté la vérification des prérequis et corrigé les avertissements relatifs aux prérequis pour un site, nous vous déconseillons d’utiliser cette option.  

      Dans les espaces de travail **Administration** et **Surveillance**, le nœud Mises à jour et maintenance affiche un bouton **Ignorer les avertissements de configuration requise** sur le ruban. Ce bouton devient disponible quand l’installation d’un package de mise à jour n’arrive pas à terme en raison d’avertissements de vérification des prérequis. Par exemple, si vous installez une mise à jour sans utiliser l’option Ignorer les avertissements de configuration requise (dans l’Assistant Mises à jour) et que l’installation de la mise à jour s’arrête avec un état d’avertissement de configuration requise mais sans erreur, vous pouvez ultérieurement choisir **Ignorer les avertissements de configuration requise** dans le ruban pour déclencher la poursuite automatique de cette installation de mise à jour qui ignorera ensuite les avertissements relatifs aux prérequis. Quand vous utilisez cette option, l’installation de la mise à jour se poursuit automatiquement après quelques minutes.



-   Quand une mise à jour s’applique au client Configuration Manager, une option vous est proposée pour tester la mise à jour du client avec un ensemble limité de clients. Pour plus d’informations, consultez [Guide pratique pour tester les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**2. Pendant l’installation de la mise à jour**  
Au cours de l’installation de la mise à jour, Configuration Manager :  

-   réinstalle tous les composants concernés, comme les rôles de système de site ou la console Configuration Manager ;  

-   gère les mises à jour des clients en fonction des sélections que vous avez effectuées pour le test du client et pour les [mises à niveau automatiques du client](https://technet.microsoft.com/library/mt627885.aspx) ;  

-   n’a pas besoin de redémarrer les serveurs de système de site dans le cadre de la mise à jour (à moins que .NET soit installé en raison d’un prérequis lié aux rôles de système de site).  

> [!TIP]  
>  Lors de l’installation des mises à jour, Configuration Manager met aussi à jour le dossier CD.Latest. Ce dossier est utilisé pendant la récupération d’un site.  

**3. Surveiller l’état d’avancement de l’installation de mises à jour**  
Pour surveiller l’état d’avancement, procédez comme suit :  

-   Dans la console Configuration Manager : nœud **Administration** > **Mises à jour et maintenance**. Ce nœud affiche l’état d’installation de tous les packages de mise à jour.


-   Dans la console Configuration Manager, accédez au nœud **Administration** > **Vue d’ensemble** > **Mises à jour et maintenance**. Ce nœud affiche l’état d’installation uniquement du package de mise à jour en cours d’installation.  

  L’installation du pack de mise à jour est décomposée selon les phases suivantes pour faciliter la surveillance. Pour chaque phase, des détails supplémentaires indiquent le fichier journal à consulter pour obtenir plus d’informations :  
    -   **Téléchargement** (cette phase s’applique uniquement au site de niveau supérieur où est installé le rôle de système de site de point de connexion de service)
    -   **Réplication**
    -   **Vérification des prérequis**
    -   **Installation**
    -   **Après l’installation** (cette phase a été introduite avec la version 1610)

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

À l’issue de la mise à jour d’un site secondaire, si l’état dans la console n’est pas actualisé ou laisse supposer que la mise à jour a échoué, vous pouvez utiliser l’option **Réessayer l’installation**. Cette option ne réinstalle pas la mise à jour sur un site secondaire qui a correctement installé la mise à jour ; elle force la console à mettre à jour l’état.


##  <a name="bkmk_retry"></a> Nouvelle tentative d’installation d’une mise à jour ayant échoué  
Quand l’installation d’une mise à jour échoue, passez en revue les commentaires dans la console pour identifier les résolutions possibles des avertissements et des erreurs. Vous pouvez également consulter le fichier ConfigMgrPrereq.log sur le serveur du site pour plus de détails. Avant de réessayer l’installation d’une mise à jour, vous devez corriger les erreurs et il est recommandé de corriger aussi les avertissements.  

Quand vous êtes prêt à réessayer l’installation d’une mise à jour, sélectionnez la mise à jour ayant échoué, puis choisissez une option applicable. Le comportement de nouvelle tentative d’installation de mise à jour dépend du nœud où vous lancez la nouvelle tentative et de l’option de nouvelle tentative que vous utilisez.  

1.  **Réessayer l’installation pour la hiérarchie :**  
Vous pouvez réessayer l’installation d’une mise à jour pour l’ensemble de la hiérarchie lorsque cette mise à jour est dans l’un des états suivants :  

    -   La vérification des prérequis a généré un ou plusieurs avertissements, et l’option permettant d’ignorer les avertissements de vérification des prérequis n’a pas été activée dans l’Assistant Mise à jour. (La valeur de mise à jour pour **Ignorer l’avertissement de condition préalable** dans le nœud **Mises à jour et maintenance** est **Non**.)   
    -   La vérification des prérequis a échoué.    
    -   L’installation a échoué.
    -   La réplication du contenu sur le site a échoué.   

    Accédez à **Administration** > **Mises à jour et maintenance**, sélectionnez la mise à jour, puis choisissez l’un des éléments suivants :  

    -   **Nouvelle tentative** : quand vous exécutez **Nouvelle tentative** à partir de ce nœud, l’installation de la mise à jour redémarre et ignore automatiquement les avertissements relatifs aux prérequis. Elle réplique également à nouveau le contenu pour la mise à jour si la réplication a échoué précédemment.
    - **Ignorer les avertissements de configuration requise** : à compter de la version 1606, si l’installation de la mise à jour s’arrête en raison d’un avertissement, vous pouvez choisir **Ignorer les avertissements de configuration requise**. Cette action permet à l’installation de la mise à jour de continuer (après quelques minutes) et utilise l’option pour ignorer les avertissements de configuration requise.   

2.  **Réessayer l’installation pour le site :**  
 Vous pouvez réessayer l’installation d’une mise à jour sur un site spécifique lorsque cette mise à jour est dans l’un des états suivants :  

    -   La vérification des prérequis a généré un ou plusieurs avertissements, et l’option permettant d’ignorer les avertissements de vérification des prérequis n’a pas été activée dans l’Assistant Mise à jour (la valeur de mise à jour pour **Ignorer l’avertissement de condition préalable** dans le nœud Mises à jour et maintenance est **Non**).  
    -   La vérification des prérequis a échoué.    
    -   L’installation a échoué.    

    Accédez à **Surveillance** > **Vue d’ensemble** > **État de la maintenance de site**, sélectionnez la mise à jour, puis cliquez sur l’un des éléments suivants :

       - **Nouvelle tentative** : quand vous exécutez **Nouvelle tentative** à partir de ce nœud, vous redémarrez l’installation de la mise à jour uniquement sur ce site. Contrairement à l’exécution de **Nouvelle tentative** à partir du nœud **Mises à jour et maintenance**, cette nouvelle tentative n’ignore pas les avertissements relatifs aux prérequis.
       -    **Ignorer les avertissements de configuration requise** : à compter de la version 1606, si l’installation de la mise à jour s’arrête en raison d’un avertissement, vous pouvez cliquer sur **Ignorer les avertissements de configuration requise**. Cette action permet à l’installation de la mise à jour de continuer (après quelques minutes) et utilise l’option pour ignorer les avertissements de prérequis.

##  <a name="bkmk_after"></a> Après l’installation d’une mise à jour sur un site  
Utilisez la liste de vérification suivante pour effectuer les tâches courantes et les configurations nécessaires après la mise à jour d’un site.   

**Vérifier que la réplication de site à site est active :** dans la console Configuration Manager, accédez aux emplacements suivants pour consulter l’état et vérifier que la réplication est active :  

-   **Surveillance** > **Vue d’ensemble** > **Hiérarchie de site**  

-   **Surveillance** > **Vue d’ensemble** > **Réplication de base de données**  

Pour plus d’informations, consultez [Surveiller l’infrastructure de la hiérarchie et de la réplication dans System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) et [À propos de l’analyseur de lien de réplication](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Vérifier que les serveurs de site et les serveurs de système de site distants ont redémarré (si nécessaire) :** examinez l’infrastructure de votre site et vérifiez que les serveurs de site et serveurs de système de site (distants du serveur de site) appropriés ont redémarré correctement.  En règle générale, cela est prévu uniquement quand Configuration Manager installe .NET en tant que prérequis pour un rôle de système de site.  

 **Mettre à jour les consoles Configuration Manager autonomes :** vérifiez que toutes les consoles Configuration Manager distantes ont été mises à jour vers la même version. Vous êtes invité à mettre à jour la console dans les cas suivants :  

-   lorsque vous accédez à un nouveau nœud dans la console ;  

-   lorsque vous ouvrez la console.

**Reconfigurer les réplicas de base de données pour les points de gestion sur les sites principaux :** si vous utilisez des réplicas de base de données pour les points de gestion sur les sites principaux, vous devez désinstaller les réplicas de base de données avant de mettre à jour le site. Après avoir mis à niveau un site principal, reconfigurez le réplica de base de données pour les points de gestion. Pour plus d’informations, consultez [Réplicas de base de données pour les points de gestion de System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigurer les tâches de maintenance de base de données désactivées avant la mise à jour :** si vous avez désactivé les [tâches de maintenance pour System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) de la base de données sur un site avant la mise à jour, reconfigurez ces tâches sur le site. Utilisez les mêmes paramètres qui étaient en vigueur avant la mise à jour.  

**Mettre à niveau les clients** : pour plus d’informations sur la façon de mettre à niveau les clients existants et sur la façon d’installer de nouveaux clients, consultez [Comment mettre à niveau les clients pour les ordinateurs Windows dans System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

**Configurations supplémentaires :** examinez les modifications que vous avez apportées avant de commencer la mise à jour, puis restaurez ces configurations sur vos sites et votre hiérarchie.  

##  <a name="bkmk_options"></a> Activation de fonctionnalités facultatives de mises à jour  
Lorsque vous installez une mise à jour incluant une ou plusieurs fonctionnalités facultatives, vous avez la possibilité d’activer celles-ci dans votre hiérarchie.  Vous pouvez le faire au moment de l’installation de la mise à jour ou revenir à la console ultérieurement pour activer les fonctionnalités facultatives.

Pour afficher les fonctionnalités disponibles et leur état, dans la console, accédez à **Administration** > **Mises à jour et maintenance** > **Fonctionnalités**.

Quand une fonctionnalité n’est pas facultative, elle est installée automatiquement et n’apparaît pas dans le nœud **Fonctionnalités**.  

##  <a name="bkmk_prerelease"></a> Utiliser des fonctionnalités de préversions de mises à jour
Les fonctionnalités de préversion sont des fonctions incluses dans la branche Current Branch à des fins de test préalable dans un environnement de production. Ces fonctionnalités peuvent être utilisées dans un environnement de production, mais ne doivent pas être considérées comme prêtes pour la production. Pour en savoir plus sur les fonctionnalités de préversion, y compris sur la façon de les activer dans votre environnement, consultez [Fonctionnalités de préversion](/sccm/core/servers/manage/pre-release-features).                |


## <a name="known-issues"></a>Problèmes connus

###  <a name="bkmk_faq"></a> Pourquoi certaines mises à jour ne s’affichent pas dans ma console ?  
 Si vous ne trouvez pas une mise à jour spécifique (ou des mises à jour quelconques) dans votre console après une synchronisation réussie avec le service cloud Microsoft, les causes possibles sont les suivantes :  

-   La mise à jour requiert une configuration que votre infrastructure n’utilise pas, ou votre version actuelle du produit ne remplit pas une condition préalable pour la réception de la mise à jour.  

     Si vous pensez que vous disposez des configurations requises ou que vous satisfaites d’autres prérequis pour une mise à jour manquante, vérifiez que votre point de connexion de service est en mode en ligne. Ensuite, utilisez l’option **Rechercher les mises à jour** dans le nœud **Mises à jour et maintenance** pour forcer la vérification.  Si vous êtes en mode hors connexion, vous devez recourir à l’outil de connexion au service pour synchroniser manuellement le service cloud.  

-   Votre compte ne dispose pas des autorisations d’administration basée sur des rôles appropriées pour afficher les mises à jour dans la console Configuration Manager.

    Pour plus d’informations sur les autorisations requises pour afficher les mises à jour et activer les fonctionnalités à partir de la console, consultez [Autorisations de gérer les mises à jour](../../../core/servers/manage/install-in-console-updates.md#assign-permissions-to-view-and-manage-updates-and-features) dans cette rubrique.

### <a name="why-do-i-see-two-updates-for-version-1610"></a>Pourquoi deux mises à jour sont-elles proposées pour la version 1610 ?
Il peut arriver que deux mises à jour vers la version 1610 soient répertoriées dans la console. Les mises à jour ont des dates différentes. Ce cas de figure se présente si l’une des conditions suivantes est remplie :   
-    Après la publication de la version 1610, vous avez installé une version antérieure (par exemple, la version 1606).

-    Votre hiérarchie exécute la version 1511 ou 1602 et vous n’avez pas pu télécharger la version 1606.

Il existe deux mises à jour vers la version 1610, car des modifications mineures ont été apportées à certains binaires de fichier après la publication de la première mise à jour. Ces modifications n’affectent pas les fonctionnalités de Configuration Manager ni la mise à jour.

Si les deux mises à jour sont disponibles dans la console, nous vous recommandons d’installer la plus récente. Toutefois, étant donné que les mises à jour offrent les mêmes fonctionnalités, aucune action de votre part n’est nécessaire si l’une d’entre elles est déjà installée.
-    Si vous avez installé l’ancienne mise à jour, il est inutile d’installer la mise à jour plus récente. Toutefois, si vous installez la mise à jour la plus récente après l’installation de la première mise à jour, les binaires en question sont mis à jour, mais aucune modification supplémentaire n’est apportée et aucune action supplémentaire de votre part n’est nécessaire.

-    Si vous avez installé la dernière mise à jour et que vous installez ensuite l’ancienne, aucune action supplémentaire n’est nécessaire. Cela est dû au fait que les derniers binaires qui sont déjà installés ne sont pas remplacés par les mêmes binaires de la mise à jour d’origine.

