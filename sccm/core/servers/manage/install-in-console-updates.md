---
title: "Mises à jour dans la console | Microsoft Docs"
description: "System Center Configuration Manager se synchronise avec le cloud Microsoft pour obtenir les mises à jour que vous pouvez installer dans la console."
ms.custom: na
ms.date: 2/1/2017
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
ms.sourcegitcommit: 2f90f3204b3c31caaed1359e11451285b21eef50
ms.openlocfilehash: b3a58503ea4d49825e93ea3a2e9bfedf975145e6


---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Installation de mises à jour dans la console pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager se synchronise avec le service cloud Microsoft pour obtenir des mises à jour que vous pouvez ensuite installer dans la console Configuration Manager.

## <a name="get-available-updates"></a>Obtenir les mises à jour disponibles
Seules les mises à jour qui s’appliquent à votre infrastructure et à votre version sont téléchargées et mises à disposition dans votre hiérarchie. Cette synchronisation peut être automatique ou manuelle, selon la manière dont vous configurez le point de connexion de service pour votre hiérarchie :

-   En **mode en ligne**, le point de connexion de service se connecte automatiquement au service cloud Microsoft et télécharge les mises à jour applicables.  

     Par défaut, Configuration Manager vérifie la disponibilité de nouvelles mises à jour toutes les 24 heures. À compter de la version 1602 ou ultérieure, vous pouvez aussi vérifier la disponibilité de mises à jour immédiatement en cliquant sur **Rechercher les mises à jour** dans le nœud **Administration** > **Services cloud** > **Mises à jour et maintenance** de la console Configuration Manager.  

-   En **mode hors connexion**, le point de connexion de service ne se connecte pas au service cloud Microsoft et vous devez manuellement [Utiliser l’outil de connexion de service pour System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md) pour télécharger puis importer les mises à jour disponibles.  

> [!NOTE]  
>  Outre les mises à jour que vous obtenez lors de la synchronisation avec le service cloud Microsoft, des correctifs hors bande qui s’installent à l’aide de l’ [outil d’inscription de mise à jour](http://technet.microsoft.com/library/mt691544.aspx) sont également importés dans votre console, où vous pouvez ensuite les sélectionner pour les installer.  

Une fois les mises à jour synchronisées, vous pouvez les afficher dans la console Configuration Manager en accédant au nœud **Administration** > **Services cloud** > **Mises à jour et maintenance** :  

-   Les mises à jour que vous n’avez pas installées apparaissent **Disponibles**.

-   Les mises à jour que vous avez installées apparaissent **Installées**.  À compter de la version 1606, seule la dernière mise à jour installée est affichée, et vous pouvez cliquer sur le bouton **Historique** sur le ruban pour afficher les mises à jour installées précédemment.



Avant de configurer le point de connexion de service, vous devez comprendre et planifier la mesure dans laquelle ses utilisations supplémentaires peuvent avoir une incidence sur la façon dont vous configurez ce rôle de système de site :  

-   Le point de connexion de service est utilisé pour charger les informations d’utilisation relatives à votre site. Ces informations permettent au service cloud de Microsoft d’identifier les mises à jour disponibles pour la version actuelle de votre infrastructure. Pour plus d’informations, consultez [Données d’utilisation et de diagnostic pour System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

-   Le point de connexion de service permet de gérer des appareils avec Microsoft Intune et à l’aide de la fonctionnalité de gestion des appareils mobiles locale de Configuration Manager. Pour plus d’informations, consultez [Gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

Pour mieux comprendre ce qui se passe quand des mises à jour sont téléchargées, consultez :  

-   [Organigramme - Téléchargement des mises à jour pour System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md)

-   [Organigramme - Réplication des mises à jour pour System Center Configuration Manager](../../../core/servers/manage/update-replication-flowchart.md)  

## <a name="permissions-to-view-and-manage-updates-and-features"></a>Autorisations d’afficher et de gérer les mises à jour et les fonctionnalités
Avant d’installer la mise à jour 1606, pour pouvoir afficher les mises à jour sur la console, un utilisateur doit avoir un rôle de sécurité incluant l’autorisation **Lecture** dans le groupe d’autorisations **Site**, et l’étendue de sécurité **Tous**. À compter de la mise à jour 1606, une nouvelle classe de sécurité d’administration basée sur des rôles nommée **Packages de mise à jour** est introduite. Elle accorde l’autorisation d’afficher et de gérer les mises à jour dans la console Configuration Manager.    

**À propos de la classe Packages de mise à jour :**  
Par défaut, **Packages de mise à jour** (SMS_CM_Updatepackages) fait partie des rôles de sécurité intégrés suivants avec les autorisations répertoriées :
 -  **Administrateur complet** avec autorisations **Modifier** et **Lecture** :
    -   Un utilisateur disposant de ce rôle de sécurité et de l’accès à l’étendue de sécurité **Tout** peut afficher les mises à jour, installer des mises à jour et activer des fonctionnalités pendant l’installation, et activer des fonctionnalités après l’installation de la mise à jour.
    - Un utilisateur disposant de ce rôle de sécurité et de l’accès à l’étendue de sécurité **Par défaut** peut afficher les mises à jour, installer des mises à jour et activer des fonctionnalités pendant l’installation, et afficher les fonctionnalités après l’installation d’une mise à jour mais pas activer les fonctionnalités une fois la mise à jour installée.

- **Analyste en lecture seule** avec autorisations **Lecture** :
  -  Un utilisateur disposant de ce rôle de sécurité et de l’accès à l’étendue **Par défaut** peut afficher les mises à jour mais pas les installer, et peut afficher les fonctionnalités après l’installation d’une mise à jour mais pas les activer.

**Résumé des autorisations nécessaires pour les mises à jour et la maintenance :**   
  - Utilisez un compte affecté à un rôle de sécurité qui comprend la classe **Packages de mise à jour** avec les autorisations **Modifier** et **Lecture** .
  - L’étendue **Par défaut** doit être affectée au compte.

**Pour uniquement afficher les mises à jour**:
  - Utilisez un compte affecté à un rôle de sécurité qui comprend la classe **Packages de mise à jour** avec uniquement l’autorisation **Lecture** .
  - L’étendue **Par défaut** doit être affectée au compte.

**Pour activer des fonctionnalités une fois les mises à jour installées :**
  -   Utilisez un compte affecté à un rôle de sécurité qui comprend la classe **Packages de mise à jour** avec les autorisations **Modifier** et **Lecture** .
  -  L’étendue **Tout** doit être affectée au compte.






##  <a name="a-namebkmkbeforeinstalla-before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a> Avant d’installer une mise à jour dans la console  
 Passez en revue les étapes suivantes avant d’installer les mises à jour à partir de la console Configuration Manager :  

###  <a name="a-namebkmkstep1a-step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a> Étape 1 : consulter la liste de contrôle de mise à jour  
Avant d’installer une nouvelle mise à jour à partir de la console Configuration Manager, passez en revue la liste de contrôle de mise à jour applicable pour connaître les actions à entreprendre avant de lancer la mise à jour :  

-   Mise à niveau vers la version 1511 : [Mettre à niveau vers System Center Configuration Manager](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)    

-   Mettre à jour vers la version 1602 à partir de la version 1511 : consultez [Liste de contrôle pour l’installation de la mise à jour 1602](../../../core/servers/manage/checklist-for-installing-update-1602.md)

- Mettre à jour vers la version 1606 à partir de la version 1511 ou 1602 : consultez [Liste de contrôle pour l’installation de la mise à jour 1606](../../../core/servers/manage/checklist-for-installing-update-1606.md)  

- Mettre à jour vers la version 1610 à partir de la version 1511, 1602 ou 1606 : consultez [Liste de contrôle pour l’installation de la mise à jour 1610](../../../core/servers/manage/checklist-for-installing-update-1610.md)  

###  <a name="a-namebkmkstep2a-step-2-test-the-database-upgrade-before-installing-an-update"></a><a name="bkmk_step2"></a> Étape 2 : tester la mise à niveau de base de données avant d’installer une mise à jour  
Avant d’installer une nouvelle mise à jour dans votre hiérarchie, telle la mise à jour 1602, vous devez tester la mise à niveau de la base de données de votre site. Le nom de l’option de ligne de commande permettant de tester l’installation d’une mise à jour sur une sauvegarde de la base de données de votre site est **testdbupgrade**.  

Contrairement aux versions précédentes de Configuration Manager, si l’installation d’une mise à jour échoue, vous n’avez pas besoin de procéder à une récupération de site. Vous pouvez tenter à nouveau l’installation de la mise à jour. Par conséquent, si le test de la mise à niveau de la base de données est moins important que dans les versions antérieures du produit, cette étape reste recommandée.  

#### <a name="to-run-testdbupgrade-before-installing-an-update"></a>Pour exécuter testdbupgrade avant d’installer une mise à jour  

1.  Obtenez un ensemble de fichiers sources à partir du dossier **CD.Latest** d’un site exécutant la version vers laquelle vous prévoyez d’effectuer la mise à jour. Vous pouvez être contraint d’installer d’abord un site dans un environnement lab ou de test exécutant cette version de System Center Configuration Manager.  

     Le dossier **CD.Latest** d’un site contient les fichiers sources pour cette version. Vous devez utiliser ceux-ci pour exécuter le test de mise à niveau de la base de données de votre site. Pour plus d’informations, consultez [Le dossier CD.Latest pour System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md).  

     Par exemple, si votre site s’exécute la version 1501 et que vous souhaitez opérer une mise à jour vers la version 1602, vous devez obtenir un dossier CD.Latest à partir d’un site déjà mis à jour vers la version 1602. En règle générale, vous pouvez installer un site nouveau et temporaire dans un environnement lab, puis procéder à une mise à niveau vers la version 1602 pour créer le dossier CD.Latest avec les fichiers requis.  

2.  Copiez le dossier CD.Latest vers un emplacement sur le serveur SQL Server que comptez utiliser pour tester la mise à niveau de la base de données. (Voir l’étape suivante).  

3.  Créez une sauvegarde de la base de données de site dont vous souhaitez tester la mise à niveau, puis restaurez une copie de cette base de données sur une instance de SQL Server qui n’héberge pas de site Configuration Manager. Le serveur SQL Server doit utiliser la même édition de SQL Server que la base de données de votre site.  

4.  Après avoir restauré la copie de la base de données, exécutez **Setup** à partir du dossier CD.Latest que vous avez copié à partir de votre environnement lab ou de test. Lorsque vous exécutez le programme d'installation, utilisez l'option de ligne de commande **/TESTDBUPGRADE** . Si l'instance SQL Server qui héberge la copie de la base de données n'est pas l'instance par défaut, vous devez également fournir les arguments de ligne de commande pour identifier l'instance qui héberge la copie de la base de données du site.  

     Par exemple, vous prévoyez de mettre à niveau une base de données de site dont le nom de base de données est SMS_ABC. Vous restaurez une copie de cette base de données de site sur une instance prise en charge de SQL Server ayant pour nom d'instance DBTest. Pour tester une mise à niveau de cette copie de la base de données du site, utilisez la ligne de commande suivante : **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     Vous trouverez Setup.exe à l’emplacement suivant sur le média source de System Center Configuration Manager : **SMSSETUP\BIN\X64**.  

5.  Sur l’instance de SQL Server exécutant le test de la mise à niveau de la base de données, examinez le fichier ConfigMgrSetup.log à la racine du lecteur système afin de déterminer la progression et l’issue du test :  

     Si le test de mise à niveau de la base de données du site échoue, remédiez aux problèmes liés à cet échec, créez une sauvegarde de la base de données du site, puis testez la mise à niveau de la nouvelle copie de la base de données du site.  

     Une fois que le processus a abouti, vous pouvez supprimer la copie de la base de données.  

    > [!NOTE]  
    >  Il n'est pas possible de restaurer la copie de la base de données du site que vous utilisez dans le cadre du test de mise à niveau afin de l'utiliser comme base de données d'un site quelconque.  

###  <a name="a-namebkmkstep3a-step-3-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step3"></a> Étape 3 : exécuter l’outil de vérification de la configuration requise avant d’installer une mise à jour  
Avant d’installer une mise à jour, envisagez d’exécuter la vérification de la configuration requise pour cette mise à jour. Si vous effectuez cette vérification avant d’installer une mise à jour :  

-   Les fichiers de mise à jour sont répliqués vers d’autres sites avant l’installation de la mise à jour  

-   La vérification des conditions préalables est automatiquement réexécutée lorsque vous choisissez d’installer la mise à jour.  

Par la suite, lorsque vous installez une mise à jour, vous pouvez configurer la mise à jour afin d’ignorer les avertissements relatifs à la vérification des conditions préalables.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Pour exécuter l’outil de vérification des conditions préalables avant d’installer une mise à jour  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Services cloud** > **Mises à jour et maintenance**.  

2.  Cliquez avec le bouton droit sur le package de mise à jour pour lequel vous souhaitez exécuter la vérification de la configuration requise.  

3.  Choisissez **Exécuter la vérification de la condition préalable**.  Vous pouvez consulter le  

     Lorsque vous exécutez la vérification des conditions préalables, le contenu de la mise à jour est répliqué sur des sites enfants.  Vous pouvez consulter le fichier **distmgr.log** sur le serveur du site pour vérifier que le contenu est répliqué correctement.  

4.  Pour afficher les résultats de la vérification, dans la console Configuration Manager, accédez à **Surveillance** > **État des mises à jour et de la maintenance**, puis recherchez l’état de la condition préalable. Vous pouvez également consulter le fichier ConfigMgrPrereq.log sur le serveur du site pour plus de détails.  



##  <a name="a-namebkmkinstalla-install-in-console-updates"></a><a name="bkmk_install"></a> Installation de mises à jour dans la console  
 Quand vous êtes prêt à installer des mises à jour à partir de la console Configuration Manager, commencez par le site de niveau supérieur de votre hiérarchie. Il s’agit soit du site d’administration centrale, soit d’un site principal autonome.  

 Nous vous recommandons de planifier l’installation de la mise à jour en dehors des heures de bureau normales pour chaque site, lorsque le processus d’installation de la mise à jour et ses actions pour réinstaller les composants du site et les rôles système de site auront le moins d’effet sur les opérations de votre entreprise.  

-   Les sites principaux enfants démarrent la mise à jour automatiquement après que le site d’administration centrale a installé la mise à jour. Il s’agit du processus par défaut et recommandé. Vous pouvez cependant utiliser des [fenêtres de maintenance pour les serveurs de site](/sccm/core/servers/manage/service-windows) pour contrôler à quel moment le site principal installe les mises à jour.  

-   Après la mise à jour du site principal parent, vous devez mettre à jour manuellement les sites secondaires à partir de la console Configuration Manager. La mise à jour automatique des serveurs de sites secondaires n’est pas prise en charge.  

-   Quand vous utilisez une console Configuration Manager après la mise à jour du site, vous êtes invité à mettre à jour la console.  

-  Après avoir mené à bien l’installation d’une mise à jour, le serveur de site met automatiquement à jour tous les rôles de système de site applicables.  Le seul inconvénient concerne les points de distribution :
  - En raison des modifications introduites dans la mise à jour 1606, quand vous installez une mise à jour sur un site qui exécute déjà la version 1606 ou ultérieure, l’ensemble des points de distribution ne se mettent plus en mode hors connexion pour se mettre en jour en même temps. Au lieu de cela, le serveur de site utilise les paramètres de distribution de contenu du site pour distribuer la mise à jour à un sous-ensemble de points de distribution à la fois. Résultat : seuls certains points de distribution passent en mode hors connexion pour l’installation de la mise à jour. Ainsi, les points de distribution dont la mise à jour n’a pas encore commencé ou est terminée restent en ligne et peuvent fournir du contenu aux clients.


###  <a name="a-namebkmkoverviewa-overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a> Vue d’ensemble de l’installation d’une mise à jour dans la console  
**1. Au démarrage de l’installation de la mise à jour**  
L’Assistant Mises à jour affiche la liste des zones de produit auxquelles s’applique la mise à jour.  

-   Dans la page **Général** de l’Assistant, vous pouvez configurer les **Avertissements relatifs à la configuration requise**.  
      -   Les erreurs de configuration requise bloquent toujours l’installation de la mise à jour. Vous devez les résoudre avant de réessayer d’installer correctement la mise à jour. Pour plus d’informations, consultez [Nouvelle tentative d’installation d’une mise à jour ayant échoué](#bkmk_retry) .  

    -   Des avertissements de configuration requise peuvent également bloquer l’installation de la mise à jour. Vous devez les résoudre avant de réessayer d’installer la mise à jour.   Pour plus d’informations, consultez [Nouvelle tentative d’installation d’une mise à jour ayant échoué](#bkmk_retry) .  
    -   L’option **Ignorer les avertissements relatifs aux conditions requises et installer cette mise à jour sans tenir compte des manquements à la configuration requise**définit une condition pour l’installation de la mise à jour qui ignore les avertissements de configuration requise et autorise la poursuite de l’installation de la mise à jour. Si vous n’activez pas cette option, l’installation de la mise à jour s’arrête en cas d’avertissement. Si vous n’avez pas exécuté la vérification de la configuration requise et résolu les avertissements de condition requise pour un site, nous vous déconseillons d’utiliser de cette option.  

      À compter de la version 1606, dans les espaces de travail **Administration** et **Surveillance** , le nœud Mises à jour et maintenance comprend un bouton sur le ruban nommé **Ignorer les avertissements de configuration requise**. Ce bouton est disponible quand un package de mise à jour ne parvient pas à terminer l’installation en raison des avertissements de vérification de la condition préalable.  Par exemple, si vous installez une mise à jour sans utiliser l’option Ignorer les avertissements de configuration requise (à partir de l’Assistant Mises à jour) et que l’installation de la mise à jour s’arrête avec un état d’avertissement de configuration requise mais aucune erreur, vous pouvez sélectionner ultérieurement **Ignorer les avertissements de configuration requise** dans le ruban pour déclencher une continuation automatique de cette installation de mise à jour qui ignore ensuite les avertissements de configuration requise.  Quand vous utilisez cette option, l’installation de la mise à jour se poursuit automatiquement après quelques minutes.



-   Quand une mise à jour s’applique au client Configuration Manager, une option vous est proposée pour tester la mise à jour du client avec un ensemble limité de clients. Pour plus d’informations, consultez [Guide pratique pour tester les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**2. Pendant l’installation de la mise à jour**  
Au cours de l’installation de la mise à jour, Configuration Manager :  

-   réinstalle tous les composants concernés, comme les rôles de système de site ou la console Configuration Manager ;  

-   gère les mises à jour des clients en fonction des sélections que vous avez effectuées pour le test du client et pour les [mises à niveau automatiques du client](https://technet.microsoft.com/library/mt627885.aspx) ;  

-   n’a pas besoin de redémarrer les serveurs de système de site dans le cadre de la mise à jour (à moins que .NET soit installé en relation avec une condition préalable à l’installation des rôles système de site).  

> [!TIP]  
>  Pendant l’installation de mises à jour, Configuration Manager met aussi à jour le dossier CD.Latest utilisé pendant la récupération d’un site.  

**3. Surveiller l’état d’avancement de l’installation de mises à jour**  
Pour surveiller l’état d’avancement, procédez comme suit :  

-   Dans la console Configuration Manager, accédez au nœud **Administration** > **Services cloud** > **Mises à jour et maintenance**. Ce nœud affiche l’état d’installation de tous les packages de mise à jour.


-   Dans la console Configuration Manager, accédez au nœud **Administration** > **Vue d’ensemble** > **Mises à jour et maintenance**. Ce nœud affiche l’état d’installation uniquement du package de mise à jour en cours d’installation.  

    À compter de la version 1606, l’installation du pack de mise à jour est décomposée en différentes phases pour faciliter la surveillance. Pour chaque phase, il existe désormais des détails supplémentaires, notamment le fichier journal à afficher pour obtenir plus d’informations :  
    -   **Téléchargement** (cette phase s’applique uniquement au site de niveau supérieur où est installé le rôle de système de site de point de connexion de service)
    -   **Réplication**
    -   **Vérification de la configuration requise**
    -   **Installation**
    -   **Après l’installation** (cette phase s’applique depuis la version 1610)

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

-   lorsque vous ouvrez la console ;  

-   lorsque vous accédez à un nouveau nœud dans une console ouverte.  

Nous vous recommandons d’installer la mise à jour immédiatement au lieu de la reporter.  

Une fois la mise à niveau de la console terminée, vous pouvez vérifier que les versions de la console et du site sont correctes. Accédez à **À propos de System Center Configuration Manager** dans le coin supérieur gauche de la console où s’affichent les nouvelles versions du site et de la console.  

###  <a name="a-namebkmktoptiera-to-start-the-update-installation-at-the-top-tier-site"></a><a name="bkmk_toptier"></a> Pour démarrer l’installation de la mise à jour sur le site de niveau supérieur  
Sur le site de niveau supérieur de votre hiérarchie, dans la console Configuration Manager, accédez à **Administration** > **Services cloud** > **Mises à jour et maintenance**, sélectionnez une mise à jour **Disponible**, puis cliquez sur **Installer le pack de mise à jour**.  

###  <a name="a-namebkmksecondarya-to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a> Pour démarrer l’installation de la mise à jour sur un site secondaire  
Après la mise à jour du site principal parent d’un site secondaire, vous pouvez mettre à jour ce dernier à partir de la console Configuration Manager.  Pour ce faire, vous utilisez l’ **Assistant Mise à niveau d’un site secondaire**.  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Configuration du site** > **Sites**, sélectionnez le site à mettre à jour puis, sous l’onglet Accueil, dans le groupe Site, cliquez sur **Mettre à niveau**.  

2.  Cliquez sur **Oui** pour démarrer la mise à jour du site secondaire.  

Pour analyser l’installation de la mise à jour sur un site secondaire, sélectionnez le serveur de site secondaire puis, sous l’onglet Accueil, dans le Groupe de sites, cliquez sur **Afficher l’état d’installation**. Vous pouvez également ajouter la colonne **Version** à l’affichage de la console pour voir la version de chaque site secondaire.  

À l’issue de la mise à jour d’un site secondaire, si l’état dans la console ne s’actualise pas ou laisse supposer que la mise à jour a échoué, vous pouvez utiliser l’option **Réessayer l’installation**. Cette option ne réinstalle pas la mise à jour sur un site secondaire qui a correctement installé la mise à jour ; elle force la console à mettre à jour l’état.


##  <a name="a-namebkmkretrya-retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a> Nouvelle tentative d’installation d’une mise à jour ayant échoué  
Quand l’installation d’une mise à jour échoue, passez en revue les commentaires dans la console pour identifier les résolutions des avertissements et erreurs.  Vous pouvez également consulter le fichier ConfigMgrPrereq.log sur le serveur du site pour plus de détails. Avant de réessayer l’installation d’une mise à jour, vous devez résoudre les erreurs et devrez résoudre les avertissements.  

Quand vous êtes prêt à réessayer l’installation d’une mise à jour, sélectionnez la mise à jour ayant échoué, puis sélectionnez une option applicable. Le comportement de nouvelle tentative d’installation de mise à jour dépend du nœud à partir duquel vous lancez la nouvelle tentative et de l’option de nouvelle tentative que vous utilisez :  

1.  **Réessayer l’installation pour la hiérarchie :**  
Vous pouvez réessayer l’installation d’une mise à jour pour l’ensemble de la hiérarchie lorsque cette mise à jour est dans l’un des états suivants :  

    -   La vérification de la configuration requise a généré un ou plusieurs avertissements, et l’option permettant d’ignorer les avertissements de vérification n’a pas été activée dans l’Assistant Mise à jour (la valeur des mises à jour pour **Ignorer l’avertissement de condition préalable** dans le nœud Mises à jour et maintenance est **Non**).   
    -   La vérification de la configuration requise a échoué.    
    -   L’installation a échoué.
    -   La réplication du contenu sur le site a échoué.   

    Accédez à **Administration** > **Services cloud** > **Mises à jour et maintenance**, sélectionnez la mise à jour, puis cliquez sur l’un des éléments suivants :  

    -   **Nouvelle tentative** : quand vous exécutez Nouvelle tentative à partir de ce nœud, l’installation de la mise à jour redémarre et ignore automatiquement les avertissements de configuration requise. Elle réplique également à nouveau le contenu pour la mise à jour si la réplication a échoué précédemment.
    - **Ignorer les avertissements de configuration requise** : à compter de la version 1606, si l’installation de la mise à jour s’arrête en raison d’un avertissement, vous pouvez cliquer sur Ignorer les avertissements de configuration requise. Cette action permet à l’installation de la mise à jour de continuer (après quelques minutes) et utilise l’option pour ignorer les avertissements de configuration requise.   

2.  **Réessayer l’installation pour le site :**  
 Vous pouvez réessayer l’installation d’une mise à jour sur un site spécifique lorsque cette mise à jour est dans l’un des états suivants :  

    -   La vérification de la configuration requise a généré un ou plusieurs avertissements, et l’option permettant d’ignorer les avertissements de vérification n’a pas été activée dans l’Assistant Mise à jour (la valeur des mises à jour pour **Ignorer l’avertissement de condition préalable** dans le nœud Mises à jour et maintenance est **Non**).  
    -   La vérification de la configuration requise a échoué.    
    -   L’installation a échoué.    

    Accédez à **Surveillance** > **Vue d’ensemble** > **État de la maintenance de site**, sélectionnez la mise à jour, puis cliquez sur l’un des éléments suivants :

       - **Nouvelle tentative** : quand vous exécutez Nouvelle tentative à partir de ce nœud, vous redémarrez l’installation de la mise à jour uniquement sur ce site. Contrairement à l’option Nouvelle tentative du nœud Mises à jour et maintenance, cette nouvelle tentative n’ignore pas les avertissements de configuration requise.
       -    **Ignorer les avertissements de configuration requise** : à compter de la version 1606, si l’installation de la mise à jour s’arrête en raison d’un avertissement, vous pouvez cliquer sur Ignorer les avertissements de configuration requise. Cette action permet à l’installation de la mise à jour de continuer (après quelques minutes) et utilise l’option pour ignorer les avertissements de configuration requise.

##  <a name="a-namebkmkaftera-after-a-site-installs-an-update"></a><a name="bkmk_after"></a> Après l’installation d’une mise à jour sur un site  
Utilisez la liste de vérification suivante pour effectuer les tâches courantes et les configurations nécessaires après des mises à jour de site :  

**Vérifier que la réplication de site à site est active :** dans la console Configuration Manager, accédez aux emplacements suivants pour consulter l’état et vérifier que la réplication est active :  

-   **Surveillance** > **Vue d’ensemble** > **Hiérarchie de site**  

-   **Surveillance** > **Vue d’ensemble** > **Réplication de base de données**  

Pour plus d’informations, consultez [Surveiller l’infrastructure de la hiérarchie et de la réplication dans System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) et [À propos de l’analyseur de lien de réplication](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Vérifier que les serveurs de site et les serveurs de système de site distants ont redémarré (si nécessaire) :** examinez l’infrastructure de votre site et vérifiez que les serveurs de site et serveurs de système de site (distants du serveur de site) appropriés ont redémarré correctement.  En règle générale, cela est prévu uniquement quand Configuration Manager installe .NET en tant que condition préalable pour un rôle de système de site.  

 **Mettre à jour les consoles Configuration Manager autonomes :** vérifiez que toutes les consoles Configuration Manager distantes ont été mises à jour vers la même version. Vous êtes invité à mettre à jour la console dans les cas suivants :  

-   lorsque vous accédez à un nouveau nœud dans la console ;  

-   lorsque vous ouvrez la console ;  

**Reconfigurer les réplicas de base de données pour les points de gestion sur les sites principaux :** si vous utilisez des réplicas de base de données pour les points de gestion sur les sites principaux, vous devez désinstaller les réplicas de base de données avant de mettre à jour le site. Après avoir mis à niveau un site principal, reconfigurez le réplica de base de données pour les points de gestion. Pour plus d’informations, consultez [Réplicas de base de données pour les points de gestion de System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigurer les tâches de maintenance de base de données désactivées avant la mise à jour :** si vous avez désactivé les [Tâches de maintenance pour System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) de la base de données sur un site avant la mise à jour, reconfigurez ces tâches sur le site en utilisant les paramètres qui étaient en vigueur avant la mise à jour.  

**Mettre à niveau les clients** : pour plus d’informations sur la façon de mettre à niveau les clients existants et sur la façon d’installer de nouveaux clients, consultez [Comment mettre à niveau les clients pour les ordinateurs Windows dans System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

**Configurations supplémentaires :** examinez les modifications que vous avez apportées avant de commencer la mise à jour, puis restaurez ces configurations sur vos sites et votre hiérarchie.  

##  <a name="a-namebkmkoptionsa-enable-optional-features-from-updates"></a><a name="bkmk_options"></a> Activation de fonctionnalités facultatives de mises à jour  
Lorsque vous installez une mise à jour incluant une ou plusieurs fonctionnalités facultatives, vous avez la possibilité d’activer celles-ci dans votre hiérarchie.  Vous pouvez le faire au moment de l’installation de la mise à jour, ou revenir à la console par la suite, puis activer les fonctionnalités facultatives.

Pour afficher les fonctionnalités disponibles et leur état, dans la console, accédez à **Administration** > **Services cloud** > **Mises à jour et maintenance** > **Fonctionnalités**.

Quand une fonctionnalité n’est pas facultative, elle s’installe automatiquement et n’apparaît pas dans le nœud **Fonctionnalités** .  

##  <a name="a-namebkmkprereleasea-use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a> Utiliser des fonctionnalités de préversions de mises à jour
À compter de la version 1606, vous devez donner votre consentement pour utiliser les fonctionnalités de préversion de System Center Configuration Manager avant de pouvoir les sélectionner et permettre leur utilisation.  

Des fonctionnalités en version préliminaire sont incluses dans le produit à des fins de test anticipé en environnement de production, mais ne doivent pas être considérées comme prêtes pour une utilisation en production.

Pour donner votre consentement, dans la console, accédez à **Administration** > **Configuration du site** > **Sites**, puis sélectionnez **Paramètres de hiérarchie**. Sous l’onglet **Général** , sélectionnez **Accepter d’utiliser les fonctionnalités en version préliminaire**.
 -  Le consentement est une action à effectuer une seule fois par hiérarchie et elle ne peut pas être annulée.  
 -  Tant que vous n’avez pas donné votre consentement, vous ne pouvez pas activer les nouvelles fonctionnalités de préversion fournies avec la mise à jour 1606 ou une version ultérieure de mise à jour.

 > [!NOTE]
 > Si vous avez activé des fonctionnalités de préversion de la mise à jour 1602 avant d’installer la mise à jour 1606, ces fonctionnalités restent activées après l’installation de la mise à jour 1606 même si vous ne donnez pas votre consentement pour utiliser les fonctionnalités de préversion.

Quand votre hiérarchie exécute la version 1606 ou ultérieure et que vous installez une mise à jour qui comprend des fonctionnalités de préversion, ces fonctionnalités sont visibles dans l’Assistant Maintenance et mises à jour avec les fonctionnalités standard incluses dans la mise à jour :
  - **Si vous avez donné votre consentement :** vous pouvez activer les fonctionnalités à partir de l’Assistant Maintenance et mises à jour quand vous installez la mise à jour. Pour ce faire, sélectionnez les fonctionnalités de préversion, comme vous le feriez pour toute autre fonctionnalité.     

    Si vous le souhaitez, vous pouvez attendre pour activer une fonctionnalité en préversion par la suite à partir du nœud **Administration** > **Services cloud** > **Mises à jour et maintenance** > **Fonctionnalités** de la console. Pour ce faire, dans le nœud Fonctionnalités, sélectionnez la fonctionnalité puis cliquez sur **Activer**. (Cette option est grisée et inaccessible tant que vous n’avez pas donné votre consentement.)  
  -   **Si vous n’avez pas donné votre consentement :** quand vous installez une mise à jour, les fonctionnalités de préversion sont visibles dans l’Assistant Maintenance et mises à jour, mais elles sont grisées et ne peuvent pas être activées. Après l’installation de la mise à jour, vous pouvez afficher ces fonctionnalités dans le nœud Fonctionnalités, mais pas les activer tant que vous n’avez pas donné votre consentement dans les paramètres de la hiérarchie.

 > [!TIP]
 > Quand vous installez la mise à jour 1606, les fonctionnalités de préversion qui sont fournies dans la mise à jour 1606 ne sont pas visibles dans l’Assistant Maintenance et mises à jour et ne peuvent pas être activées à ce moment-là. Après l’installation de la mise à jour 1606, vous pouvez afficher les fonctionnalités de préversion qu’elle contient dans le nœud Fonctionnalités.

Si vous avez donné votre consentement sur un site principal autonome, puis que vous avez développé la hiérarchie en installant un nouveau site d’administration centrale, vous devez redonner votre consentement sur le site d’administration centrale.

**Les fonctionnalités en préversion disponibles sont les suivantes** :

 |Fonctionnalité                    |Ajoutée en préversion |Ajoutée en version complète |  
|----------------------------|---------------------|------------------------|
| Cache d’homologue pour la distribution de contenu aux clients |  [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Passerelle de gestion cloud |  [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Tableau de bord Sources de données du client |  [Version 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Connecteur OMS (Microsoft Operations Management Suite)  | [Version 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Maintenance d’un regroupement prenant en charge les clusters (maintenance d’un groupe de serveurs)| [Version 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|Accès conditionnel pour les PC gérés par System Center Configuration Manager | [Version 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)                        |


## <a name="known-issues"></a>Problèmes connus

###  <a name="a-namebkmkfaqa-why-dont-i-see-certain-updates-in-my-console"></a><a name="bkmk_faq"></a> Pourquoi certaines mises à jour ne s’affichent pas dans ma console ?  
 Si vous ne trouvez une mise à jour spécifique ou des mises à jour quelconques dans votre console après une synchronisation réussie avec le service cloud Microsoft, les causes possibles sont les suivantes :  

-   La mise à jour requiert une configuration que votre infrastructure n’utilise pas, ou votre version actuelle du produit ne remplit pas une condition préalable pour la réception de la mise à jour.  

     Si vous pensez que vous disposez des configurations requises ou remplissez d’autres conditions préalables pour une mise à jour manquante, vérifiez que votre point de connexion de service est en mode en ligne, puis utilisez l’option **Rechercher les mises à jour** dans le nœud Mises à jour et maintenance pour forcer la vérification.  Si vous êtes en mode hors connexion, vous devez recourir à l’outil de connexion au service pour synchroniser manuellement le service cloud.  

-   Votre compte ne dispose pas des autorisations d’administration basée sur des rôles appropriées pour afficher les mises à jour dans la console Configuration Manager.

    Pour plus d’informations sur les autorisations requises pour afficher les mises à jour et activer les fonctionnalités à partir de la console, consultez [Autorisations de gérer les mises à jour](../../../core/servers/manage/install-in-console-updates.md#permissions-to-view-and-manage-updates-and-features) dans cette rubrique.

### <a name="why-do-i-see-two-updates-for-version-1610"></a>Pourquoi deux mises à jour sont-elles proposées pour la version 1610 ?
Il peut arriver que deux mises à jour vers la version 1610 soient répertoriées dans la console. Les mises à jour ont des dates différentes. Ce cas de figure se présente si l’une des conditions suivantes est remplie :   
-   Après la publication de la version 1610, vous avez installé une version antérieure (par exemple, la version 1606).

-   Votre hiérarchie exécute la version 1511 ou 1602 et vous n’avez pas pu télécharger la version 1606.

Il existe deux mises à jour vers la version 1610, car des modifications mineures ont été apportées à certains binaires de fichier après la publication de la première mise à jour. Ces modifications n’affectent pas les fonctionnalités de Configuration Manager ni la mise à jour.

Si les deux mises à jour sont disponibles dans la console, nous vous recommandons d’installer la plus récente. Toutefois, étant donné que les mises à jour offrent les mêmes fonctionnalités, aucune action de votre part n’est nécessaire si l’une d’entre elles est déjà installée.
-   Si vous avez installé l’ancienne mise à jour, il est inutile d’installer la mise à jour plus récente. Toutefois, si vous installez la mise à jour la plus récente après l’installation de la première mise à jour, les binaires en question sont mis à jour, mais aucune modification supplémentaire n’est apportée et aucune action supplémentaire de votre part n’est nécessaire.

-   Si vous avez installé la dernière mise à jour et que vous installez ensuite l’ancienne, aucune action supplémentaire n’est nécessaire. Cela est dû au fait que les derniers binaires qui sont déjà installés ne sont pas remplacés par les mêmes binaires de la mise à jour d’origine.



<!--HONumber=Feb17_HO1-->


