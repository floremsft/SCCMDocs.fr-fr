---
title: "Présentation des regroupements | System Center Configuration Manager"
description: "Obtenez une présentation de l’utilisation des regroupements dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
caps.latest.revision: 8
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 47574218dec5069205f9dba5608c6f136fb032bc


---
# <a name="introduction-to-collections-in-system-center-configuration-manager"></a>Présentation des regroupements dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les regroupements dans System Center Configuration Manager vous permettent d’organiser les ressources en unités pouvant être gérées, et donc de créer une structure organisée représentant de manière logique les types de tâches que vous voulez effectuer. Les regroupements servent également à exécuter des opérations Configuration Manager sur plusieurs ressources à la fois. Le tableau suivant présente quelques exemples d’utilisation de regroupements dans Configuration Manager :  

|Opération|Exemple|  
|---------|-------|  
|Regroupement des ressources|Vous pouvez créer des regroupements qui rassemblent logiquement des ressources basées sur la hiérarchie de votre organisation.<br /><br /> Par exemple, vous pouvez créer un regroupement de tous les ordinateurs qui résident dans l’unité d’organisation Active Directory « Siège social de Londres ». Pour plus d’informations sur la création de ce type de regroupement, consultez [Guide pratique pour créer des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> Vous pouvez ensuite utiliser ce regroupement pour effectuer des opérations telles que la configuration des paramètres Endpoint Protection, la configuration des paramètres de gestion de l’alimentation des appareils ou l’installation du client Configuration Manager.|  
|Déploiement d’applications|Vous pouvez créer un regroupement de tous les ordinateurs sur lesquels Microsoft Office 2013 n’est pas installé, puis déployer ce logiciel sur tous les ordinateurs de ce regroupement.<br /><br /> Vous pouvez également utiliser des données de configuration requise pour l’application pour effectuer cette tâche. Pour plus d’informations, consultez [Comment créer des applications avec System Center Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|Gestion des paramètres client|Bien que les paramètres client par défaut dans Configuration Manager s’appliquent à tous les appareils et à tous les utilisateurs, vous pouvez créer des paramètres client personnalisés qui s’appliquent à un regroupement d’appareils ou d’utilisateurs.<br /><br /> Par exemple, si vous souhaitez que le contrôle à distance soit disponible sur tous les appareils hormis quelques-uns, configurez les paramètres client par défaut pour autoriser le contrôle à distance, puis configurez des paramètres client personnalisés qui interdisent le contrôle à distance. Déployez ces paramètres client personnalisés dans un regroupement qui contient les ordinateurs qui n’utiliseront pas le contrôle à distance.<br /><br /> Pour plus d’informations sur la façon d’utiliser des regroupements pour les paramètres client, consultez [À propos des paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).|  
|Gestion de l'alimentation|Pour chaque regroupement que vous créez, vous pouvez configurer des paramètres d’alimentation comme le délai de mise en veille des ordinateurs du regroupement quand ils sont inactifs.<br /><br /> Pour plus d’informations sur l’utilisation de regroupements avec la gestion de l’alimentation, consultez [Présentation de la gestion de l’alimentation](../power/introduction-to-power-management.md).|  
|Administration basée sur des rôles|Vous pouvez utiliser les regroupements avec l’administration basée sur des rôles pour contrôler quels groupes d’utilisateurs ont accès aux diverses fonctionnalités dans la console Configuration Manager.<br /><br /> Pour plus d’informations sur la façon de configurer des regroupements pour l’administration basée sur des rôles, consultez [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).|  
|Fenêtres de maintenance|Les fenêtres de maintenance permettent aux utilisateurs administratifs de définir une période pendant laquelle diverses opérations Configuration Manager peuvent être effectuées sur les membres d’un regroupement d’appareils. Vous pouvez utiliser les fenêtres de maintenance afin de vous assurer que les modifications apportées à la configuration client seront effectuées pendant des périodes qui n'affectent pas la productivité de l'organisation.<br /><br /> Pour plus d’informations sur les fenêtres de maintenance, consultez [Comment utiliser les fenêtres de maintenance dans System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).|  

 La plupart des tâches de gestion reposent sur l’utilisation d’un ou plusieurs regroupements. Par exemple, avant de pouvoir déployer des mises à jour logicielles sur des appareils, vous devez identifier un regroupement pour le déploiement des mises à jour logicielles. Même si vous pouvez utiliser le regroupement intégré Tous les systèmes, celui-ci n’est pas idéal pour les tâches de gestion. Dans un environnement autre qu’un environnement de test, il est généralement préférable de créer vos propres regroupements personnalisés pour identifier plus précisément les appareils ou les utilisateurs à gérer.  

 Les regroupements intégrés et personnalisés figurent dans les nœuds **Regroupements d’utilisateurs** et **Regroupements de périphériques** dans l’espace de travail **Ressources et Conformité** de la console Configuration Manager.  

 Les derniers regroupements visualisés apparaissent dans le nœud **Utilisateurs** et dans le nœud **Appareils** dans l’espace de travail **Ressources et Conformité** de la console Configuration Manager.  

## <a name="collection-types-in-configuration-manager"></a>Types de regroupements dans Configuration Manager  
 Configuration Manager a des regroupements intégrés que vous pouvez utiliser pour les opérations courantes. Vous pouvez créer vos propres regroupements pour des ressources propres aux besoins de votre entreprise.  

### <a name="built-in-collections"></a>Regroupements intégrés  
 Par défaut, Configuration Manager contient les regroupements suivants qui ne peuvent pas être modifiés.  

|**Nom du regroupement**|Description|  
|-------------------------|-----------------|  
|**Tous les groupes d'utilisateurs**|Contient les groupes d'utilisateurs qui sont découverts à l'aide de la découverte de groupes de sécurité Active Directory.|  
|**Tous les utilisateurs**|Contient les utilisateurs qui sont découverts à l'aide de la découverte d'utilisateurs Active Directory.|  
|**Tous les utilisateurs et groupes d'utilisateurs**|Contient tous les utilisateurs et tous les regroupements de groupes d'utilisateurs. Ce regroupement ne peut pas être modifié et contient la plus grande étendue de ressources utilisateur et groupe d'utilisateurs.|  
|**Tous les clients bureau et serveur**|Contient les appareils serveurs et de bureau qui disposent du client Configuration Manager. L'appartenance est maintenue par découverte par pulsations d'inventaire.|  
|**Tous les appareils mobiles**|Contient les appareils mobiles qui sont gérés par Configuration Manager. L'appartenance est limitée à ces appareils mobiles qui sont affectés à un site avec succès ou découverts par le connecteur Exchange Server.|  
|**Tous les systèmes**|Contient les regroupements Tous les clients bureau et serveur, Tous les appareils mobiles, Tous les ordinateurs inconnus, ainsi que tous les appareils mobiles qui sont inscrits par Microsoft Intune.<br /><br /> Ce regroupement ne peut pas être modifié et contient la plus grande étendue de ressources de périphérique.|  
|**Tous les ordinateurs inconnus**|Contient des enregistrements d'ordinateur générique pour plusieurs plates-formes informatiques. Vous pouvez utiliser ce regroupement pour déployer un système d'exploitation à l'aide d'une séquence de tâches et d'un démarrage PXE, d'un média de démarrage ou d'un média préparé.|  

### <a name="custom-collections"></a>Regroupements personnalisés  
 Quand vous créez un regroupement personnalisé dans Configuration Manager, l’appartenance de ce regroupement est déterminée par une ou plusieurs règles de regroupement. Pour plus d’informations sur la configuration des règles de regroupement, consultez [Guide pratique pour créer des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md). Vous pouvez utiliser quatre règles :  

#### <a name="direct-rule"></a>Règle directe  
 Les règles directes permettent de choisir les utilisateurs ou les ordinateurs à ajouter comme membres à un regroupement. Une règle directe permet de contrôler directement les ressources qui sont membres d'un regroupement. L’appartenance ne change pas automatiquement, sauf si une ressource est supprimée de Configuration Manager. Configuration Manager doit découvrir les ressources ou vous devez les importer pour pouvoir les ajouter à un regroupement à règle directe. Les regroupements à règle directe ont une charge administrative plus élevée que les regroupements à règle de requête, car vous devez modifier manuellement ce type de regroupement.  

#### <a name="query-rule"></a>Règle de requête  
 Les règles de requête mettent à jour dynamiquement l’appartenance à un regroupement en fonction d’une requête que Configuration Manager exécute selon un calendrier. Par exemple, vous pouvez créer un regroupement d'utilisateurs membres de l'unité d'organisation Ressources Humaines dans les services de domaine Active Directory. Contrairement aux regroupements à règle directe, cette appartenance de regroupement est mise à jour automatiquement lorsque vous ajoutez ou supprimez des utilisateurs de l'unité d'organisation Ressources Humaines. Les règles de requête enlèvent la charge administrative de l’ajout manuel des appareils dans le regroupement à l’aide d’une règle directe. Toutefois, elles offrent moins de contrôle sur les ordinateurs qui sont ajoutés au regroupement. Voici quelques exemples de règles de requête :  

-   Tous les utilisateurs dans une unité d’organisation spécifiée  

-   Tous les ordinateurs qui exécutent Windows 8  

-   Tous les ordinateurs qui ont plus de 20 Go d’espace disque libre  

#### <a name="include-collections-rule"></a>Règle Inclure des regroupements  
 La règle Inclure des regroupements permet d’inclure les membres d’un autre regroupement dans un regroupement Configuration Manager. Configuration Manager met à jour l’appartenance du regroupement actuel d’après un planning si l’appartenance du regroupement inclus change.  

#### <a name="exclude-collections-rule"></a>Règle Exclure des regroupements  
 La règle Exclure des regroupements permet d’exclure d’un regroupement Configuration Manager les membres d’un autre regroupement. Configuration Manager met à jour l’appartenance du regroupement actuel d’après un planning si l’appartenance du regroupement exclus change.  

> [!NOTE]  
>  Si un regroupement inclut des règles d'inclusion et d'exclusion de regroupement et qu'il existe un conflit, la règle d'exclusion prévaut sur la règle d'inclusion.  

## <a name="incremental-collection-updates"></a>Mises à jour incrémentielles de regroupement  
 Lorsque vous activez les mises à jour incrémentielles pour un regroupement, Configuration Manager recherche régulièrement les ressources nouvelles ou modifiées dans l’évaluation de regroupement précédente et met à jour l’appartenance d’un regroupement avec ces ressources, indépendamment d’une évaluation complète de regroupement. Par défaut, lorsque vous activez les mises à jour incrémentielles de regroupement, elles s’exécutent toutes les 5 minutes et permettent de conserver les données de regroupement à jour sans subir la surcharge d’une évaluation complète de regroupement.  

> [!NOTE]  
>  Lorsque vous créez un regroupement, les mises à jour incrémentielles sont désactivées par défaut.  



<!--HONumber=Nov16_HO1-->


