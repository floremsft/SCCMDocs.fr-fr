---
title: "Liste de contrôle pour 1602 | Microsoft Docs"
description: "Découvrez les actions à entreprendre avant d’effectuer la mise à jour de System Center Configuration Manager version 1511 vers la version 1602."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
caps.latest.revision: 13
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 78f8e9474afe208c5d91d27e8d2a202f4ed6154e


---
# <a name="checklist-for-installing-update-1602-for-system-center-configuration-manager"></a>Liste de contrôle pour l’installation de la mise à jour 1602 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de mettre à jour System Center Configuration Manager version 1511 vers la version 1602, passez en revue les informations et la liste de contrôle suivantes pour connaître les mesures à prendre avant de commencer la mise à jour.  

 **À propos de l’installation de la mise à jour 1602 :**  

 Vous ne pouvez installer la mise à jour 1602 que sur le site de niveau supérieur de votre hiérarchie. Cela signifie que vous lancez l’installation à partir de votre site d’administration centrale si en avez un, ou à partir de votre site principal autonome.  

-   Les sites principaux enfants installent automatiquement la mise à jour après que le site d’administration centrale a fini de l’installer. Vous pouvez utiliser des fenêtres de maintenance pour contrôler le moment auquel le site installe les mises à jour. Depuis la publication de la mise à jour 1602, les fenêtres de maintenance sont également nommées fenêtres de service. Pour plus d’informations, consultez [Fenêtres de service pour les serveurs de site](../../../core/servers/manage/install-in-console-updates.md#bkmk_ServiceWindow).  

-   Après que le site parent principal a installé la mise à jour, vous devez mettre à jour manuellement les sites secondaires à partir de la console Configuration Manager. La mise à jour automatique des serveurs de sites secondaires n’est pas prise en charge.  

Lorsque le serveur de site installe la mise à jour, les rôles système de site installés sur le serveur de site et sur des ordinateurs distants se mettent à jour automatiquement. Par conséquent, avant d’installer la mise à jour, assurez-vous que chaque serveur de système de site remplit les nouvelles conditions préalables pour l’opération avec la nouvelle version de mise à jour.  

La première fois que vous utilisez une console Configuration Manager après la mise à jour, vous êtes invité à mettre à jour cette console.  Pour cela, vous devez exécuter le programme d’installation de Configuration Manager sur l’ordinateur hébergeant la console, puis sélectionner l’option de mise à jour de la console. Nous vous recommandons de ne pas retarder l’installation de la mise à jour sur la console.  

 **Liste de contrôle :**  

 **Vérifiez que tous les sites exécutent une version prise en charge de System Center Configuration Manager :**  chaque serveur de site dans la hiérarchie doit exécuter System Center Configuration Manager version 1511 avant le démarrage de l’installation de la mise à jour 1602.  

 **Examinez les versions installées de .NET sur les serveurs de système de site :** quand un site installe la mise à jour 1602, Configuration Manager installe automatiquement le .NET Framework 4.5.2 sur chaque ordinateur hébergeant un des rôles de système de site suivants si le .NET Framework 4.5 ou version ultérieure n’est pas encore installé :  

-   point proxy d'inscription  

-   point d'inscription  

-   point de gestion  

-   point de connexion de service  

Cette installation peut mettre le serveur de système de site en état d’attente de redémarrage, et signaler des erreurs sur l’Afficheur des messages d’état du composant Configuration Manager. En outre, des applications .NET sur le serveur peuvent présenter des défaillances aléatoires jusqu’au redémarrage du serveur.  

 Pour plus d’informations, consultez [Prérequis des sites et systèmes de site](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Examinez l’état du site et de la hiérarchie, et vérifiez l’absence de tout problème non résolu :** avant de mettre à jour un site, résolvez tous les problèmes opérationnels pour le serveur de site, le serveur de bases de données du site et les rôles de système de site installés sur des ordinateurs distants. Une mise à niveau de site peut échouer en raison de l’existence de problèmes opérationnels.  
 Pour plus d’informations, consultez [Utiliser des alertes et le système d’état pour System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Examinez la réplication des fichiers et données entre sites :**  vérifiez que la réplication des fichiers et bases de données entre les sites est opérationnelle et active. Des retards ou travaux en souffrance dans ces domaines peuvent perturber ou empêcher la mise à jour.    
Pour la réplication de la base de données, vous pouvez utiliser l’Analyseur de lien de réplication pour faciliter la résolution des problèmes avant de commencer la mise à jour.    
 Pour plus d’informations, consultez   
[À propos de l’analyseur de lien de réplication](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) dans la rubrique [Surveiller l’infrastructure de la hiérarchie et de la réplication dans System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

 **Installez toutes les mises à jour critiques applicables pour les systèmes d’exploitation sur les ordinateurs hébergeant le site, le serveur de base de données du site et les rôles de système de site distants :** avant d’installer une mise à jour pour Configuration Manager, installez toutes les mises à jour critiques pour chaque système de site concerné. Si vous installez une mise à jour qui nécessite un redémarrage, redémarrez les ordinateurs concernés avant d'entreprendre la mise à jour.  

 **Désactivez les réplicas de base de données pour les points de gestion sur les sites principaux :** Configuration Manager ne peut pas mettre à jour correctement un site principal ayant un réplica de base de données activé pour des points de gestion. Désactivez la réplication de base de données avant de :  

-   Créer une sauvegarde de la base de données pour tester la mise à niveau de base de données  

-   Installer une mise à jour pour Configuration Manager  

Pour plus d'informations, voir   
[Réplicas de base de données pour les points de gestion de System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)  

 **Reconfigurez les points de mise à jour logicielle qui utilisent des équilibrages de la charge réseau :** Configuration Manager ne peut pas mettre à jour un site utilisant un cluster d’équilibrage de la charge réseau (NLB) pour héberger des points de mise à jour logicielle.  
Si vous utilisez des clusters NLB pour les points de mise à jour logicielle, utilisez PowerShell pour supprimer le cluster NLB.    

 Pour plus d’informations, consultez [Planifier les mises à jour logicielles dans System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

 **Désactivez toutes les tâches de maintenance de site sur chaque site pendant la durée de l’installation de la mise à jour sur celui-ci :** avant d’installer une mise à jour, désactivez toute tâche de maintenance de site susceptible de s’exécuter pendant que le processus de mise à jour est actif. Cela inclut, sans toutefois s'y limiter, les tâches suivantes :  

-   Serveur de site de sauvegarde  

-   Supprimer les anciennes opérations du client  

-   Supprimer les données de découverte anciennes  

Si une tâche de maintenance de base de données du site s’exécute pendant l’installation de la mise à jour, celle-ci peut échouer. Avant de désactiver une tâche, enregistrez sa planification afin de pouvoir restaurer sa configuration une fois la mise à jour installée.  
 Pour plus d’informations, consultez [Tâches de maintenance pour System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) et [Référence des tâches de maintenance pour System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 **Créez une sauvegarde de la base de données du site d’administration centrale et des sites principaux :** avant de mettre à jour un site, sauvegardez sa base de données pour être certain de disposer d’une sauvegarde correcte utilisable en cas de récupération d’urgence.   
Pour plus d'informations, consultez [Backup and recovery for System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

 **Sauvegardez un fichier Configuration.mof personnalisé :** si vous utilisez un fichier Configuration.mof personnalisé pour définir les classes de données que vous utilisez avec l’inventaire matériel, créez une sauvegarde de ce fichier avant de mettre à jour le site. Ensuite, après la mise à jour, restaurez ce fichier sur votre site version 1602. Lors de la mise à jour d’un site, le fichier actuel est remplacé par sa version d’origine (par défaut). Pour plus d’informations sur l’utilisation de ce fichier, consultez [Comment étendre l’inventaire matériel dans System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 **Testez la mise à niveau de la base de données sur une copie de la dernière sauvegarde de la base de données du site :** avant de mettre à jour un site d’administration centrale ou un site principal System Center Configuration Manager, testez le processus de mise à niveau de la base de données du site sur une copie de celle-ci.  

-   Vous devez tester le processus de mise à niveau de base de données de site, car quand vous mettez à niveau un site, la base de données peut être modifiée.  

-   Bien que le test de mise à niveau ne soit pas obligatoire, il peut identifier des problèmes liés à la mise à niveau avant que votre base de données de production ne soit affectée.  

-   Un échec de mise à niveau de base de données de site peut rendre votre base de données de site inutilisable, et une récupération de site peut s’avérer nécessaire pour rétablir les fonctionnalités.  

-   Bien que la base de données de site soit partagée entre les sites d’une même hiérarchie, prévoyez de tester la base de données sur chacun des sites concernés avant de procéder à leur mise à niveau.  

-   Si vous utilisez des réplicas de base de données pour les points de gestion d’un site principal, désactivez la réplication avant de créer la sauvegarde de la base de données de site.  

Configuration Manager ne prend en charge ni la sauvegarde des sites secondaires ni la mise à niveau de test d’une base de données de site secondaire.   
L'exécution d'un test de mise à niveau de base de données sur la base de données de site de production n'est pas prise en charge. Cette opération met à jour la base de données du site et pourrait rendre celui-ci inutilisable. Pour plus d’informations, consultez la section [Tester la mise à niveau de base de données de site](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_test) dans [Mettre à niveau vers System Center Configuration Manager](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

 **Planifiez un test du client :** quand vous installez une mise à jour qui affecte le client, vous pouvez la tester en mode préproduction avant de procéder au déploiement et à la mise à niveau de votre client actif.   
 Pour tirer parti de cette option, avant de commencer l’installation de la mise à jour, vous devez configurer votre site afin qu’il prenne en charge les mises à niveau automatiques à des fins de pré-production. Pour plus d’informations, consultez [Mettre à niveau les clients dans System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) et   
[Guide pratique pour tester les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md)  

 **Planifiez l’utilisation de fenêtres de maintenance**  
 **pour contrôler le moment où les serveurs de site installent les mises à jour :** vous pouvez utiliser les fenêtres de maintenance pour définir une période applicable à un serveur de site principal, au cours de laquelle des mises à jour de ce site peuvent être installées.   
Cela peut vous aider à contrôler le moment où les sites au sein de votre hiérarchie installent la mise à jour.   
Depuis la publication de la mise à jour 1602, les fenêtres de maintenance sont également nommées fenêtres de service. Pour plus d’informations, consultez [Fenêtres de service pour les serveurs de site](../../../core/servers/manage/install-in-console-updates.md#bkmk_ServiceWindow).  

 **Exécutez l’Outil de vérification des conditions préalables :**  avant d’installer la mise à jour 1602, vous pouvez exécuter l’Outil de vérification des conditions préalables indépendamment de l’installation de la mise à jour. Lorsque vous installez la mise à jour sur le site, l’outil de vérification de la configuration requise s’exécute à nouveau.  
Pour plus d’informations, consultez **Étape 3 : exécuter l’Outil de vérification des conditions préalables avant d’installer une mise à jour** dans la rubrique [Mises à jour pour System Center Configuration Manager](../../../core/servers/manage/updates.md).  

> [!IMPORTANT]  
>  Lorsque l’outil de vérification de la configuration requise s’exécute dans le cadre de l’installation d’une mise à jour ou indépendamment de celle-ci, le processus met à jour certains fichiers sources du produit qui sont utilisés pour les tâches de maintenance de site. Par conséquent, après l’exécution de l’Outil de vérification des prérequis, mais avant l’installation de la mise à jour 1602, si vous devez effectuer une tâche de maintenance de site, exécutez **Setupwfe.exe** (programme d’installation de Configuration Manager) à partir du dossier CD.Latest sur le serveur du site.  

 **Mettez à jour les sites :** vous êtes maintenant prêt à commencer l’installation de la mise à jour pour votre hiérarchie.  
  Nous vous recommandons de planifier l’installation de la mise à jour en dehors des heures de bureau normales pour chaque site, lorsque le processus d’installation de la mise à jour et ses actions pour réinstaller les composants du site et les rôles système de site auront le moins d’effet sur les opérations de votre entreprise. Pour plus d’informations, consultez [Mises à jour pour System Center Configuration Manager](../../../core/servers/manage/updates.md).  

## <a name="see-also"></a>Voir aussi  
 [Mises à jour pour System Center Configuration Manager](../../../core/servers/manage/updates.md)



<!--HONumber=Dec16_HO3-->


