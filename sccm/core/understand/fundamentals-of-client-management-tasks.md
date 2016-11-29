---
title: Principes de base de la gestion des clients | System Center Configuration Manager
description: "Découvrez les tâches que vous pouvez exécuter pour gérer les clients System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b746c051eee42bcea5c01ced359f568c5aae5fd8


---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>Principes de base des tâches de gestion des clients pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Après avoir installé des clients System Center Configuration Manager, vous pouvez les gérer en exécutant plusieurs tâches.  Vous pouvez en démarrer certaines à partir de la console Configuration Manager, tandis que d’autres peuvent être démarrées ou affichées sur un client à partir des applications Configuration Manager clientes dans le Panneau de configuration Windows.  

## <a name="the-console"></a>La console  
 À partir de la console Configuration Manager, vous pouvez effectuer diverses tâches de gestion de clients, notamment :  

-   Déployer des applications, des mises à jour logicielles, des scripts de maintenance et des systèmes d'exploitation. Vous pouvez faire en sorte que ces éléments soient installés à une date et heure spécifiées, ou les mettre à la disposition des utilisateurs pour que ceux-ci puissent les installer à la demande. Vous pouvez également configurer des applications en vue de les désinstaller.  

-   Protéger les ordinateurs contre les logiciels malveillants et menaces de sécurité, et recevoir un avertissement lorsque des problèmes sont détectés.  

-   Définir les paramètres de configuration client que vous voulez surveiller et corriger s'ils ne sont pas conformes.  

-   Recueillir des informations d'inventaire matériel et logiciel, qui comprennent la surveillance et le rapprochement des informations de licence de Microsoft.  

-   Dépanner des ordinateurs à l’aide d’un contrôle à distance.  

-   Implémenter des paramètres de gestion de l'alimentation pour gérer et surveiller la consommation d'énergie des ordinateurs.  

Pour surveiller ces opérations en quasi-temps réel, vous devez utiliser la console Configuration Manager pour voir les alertes et les informations d’état. Pour capturer des données et des tendances historiques, vous pouvez utiliser les fonctions de rapport intégrées de SQL Reporting Services.  Les clients envoient des détails au site en tant qu’état du client.  Les informations d’état du client fournissent des indications sur l’intégrité et l’activité du client ; elles peuvent être consultées dans la console ou à l’aide de rapports intégrés pour Configuration Manager. Ces données permettent d'identifier les ordinateurs qui ne répondent pas. Dans certains cas, les problèmes peuvent être résolus automatiquement.  

 Pour plus d’informations sur les tâches de gestion pour les clients, consultez [Comment gérer les clients dans System Center Configuration Manager](../../core/clients/manage/manage-clients.md) et [Comment gérer les clients pour des serveurs Linux et UNIX dans System Center Configuration Manager](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Pour en savoir plus sur l’utilisation de rapports, consultez   
            [Présentation des rapports dans System Center Configuration Manager](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="the-windows-control-panel-app"></a>L’application Panneau de configuration de Windows  
 Quand vous installez le logiciel client Configuration Manager, l’application cliente **Configuration Manager** est installée dans le Panneau de configuration. Contrairement au Centre logiciel, cette application s'adresse plus au service de support technique qu'aux utilisateurs finaux. Certaines options de configuration nécessitent des autorisations administratives locales et la plupart des options requièrent des connaissances techniques sur le fonctionnement de Configuration Manager. Vous pouvez utiliser cette application pour effectuer les tâches suivantes sur un client :  

-   Consulter les propriétés du client : numéro de version, site attribué, point de gestion avec lequel il communique, certificat utilisé (PKI ou auto-signé), etc.  

-   Vérifier que le client a correctement téléchargé la stratégie client après son installation initiale et que les paramètres client sont activés ou désactivés comme prévu, en fonction des paramètres client configurés dans la console Configuration Manager.  

-   Démarrer les actions du client, par exemple pour télécharger la stratégie client si une modification a été récemment apportée à la configuration dans la console Configuration Manager et que vous ne souhaitez pas attendre la prochaine planification.  

-   Affecter manuellement un client à un site Configuration Manager ou essayer de trouver un site et spécifier le suffixe DNS pour les points de gestion qui publient sur DNS.  

-   Configurer le cache du client qui stocke temporairement les fichiers et supprimer des fichiers du cache si vous avez besoin de plus d'espace disque pour installer les logiciels.  

-   Configurer les paramètres de gestion des clients basés sur Internet.  

-   Consulter les lignes de base de configuration qui ont été déployées sur le client, lancer une évaluation de la compatibilité et consulter les rapports de compatibilité.  



<!--HONumber=Nov16_HO1-->


