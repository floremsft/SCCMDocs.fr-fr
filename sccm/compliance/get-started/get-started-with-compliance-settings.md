---
title: "Bien démarrer avec les paramètres de compatibilité | Microsoft Docs"
description: "Découvrez le fonctionnement des paramètres de compatibilité dans System Center Configuration Manager. Découvrez également les concepts fondamentaux que vous devez connaître."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
caps.latest.revision: "11"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f16c87dfd0c4f80d96aedf7f5f7497f2bbd4752a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2017
---
# <a name="get-started-with-compliance-settings-in-system-center-configuration-manager"></a>Prise en main des paramètres de compatibilité dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de commencer à créer des éléments de configuration System Center Configuration Manager, vous devez parcourir cette rubrique pour comprendre comment fonctionnent les paramètres de compatibilité et pour découvrir certains concepts fondamentaux.  

## <a name="how-compliance-settings-works"></a>Fonctionnement des paramètres de compatibilité  
 Les paramètres de compatibilité vous permettent de gérer la configuration et la conformité des serveurs, ordinateurs portables, ordinateurs de bureau et appareils mobiles de votre organisation.  

 Les éléments de configuration se répartissent en deux catégories principales :  

-   **Paramètres pour les appareils gérés par le client Configuration Manager** : il s’agit généralement d’appareils sur lesquels vous avez installé le logiciel client Configuration Manager, grâce auquel vous pouvez gérer ces appareils.  

-   **Paramètres pour les appareils gérés sans le client Configuration Manager** : il s’agit généralement d’appareils qui sont gérés avec Microsoft Intune ou par le biais de la gestion des appareils locale de Configuration Manager.  

## <a name="what-devices-are-supported"></a>Quels sont les appareils pris en charge ?  


|Type d'appareil|Plus d'informations|  
|------------|----------------------|  
|Ordinateurs Windows (avec le client Configuration Manager)|Permet de créer des éléments de configuration personnalisés afin d’évaluer des éléments tels que les clés de Registre, les fichiers et les attributs Active Directory.<br /><br /> Quand vous utilisez le type d’élément de configuration Windows 10, vous sélectionnez les paramètres de votre choix dans une liste prédéfinie.|  
|Ordinateurs Windows (inscrits auprès de Microsoft Intune)|Sélectionnez les paramètres de votre choix dans une liste prédéfinie.|  
|Appareils iOS (inscrits auprès de Microsoft Intune)|Sélectionnez les paramètres de votre choix dans une liste prédéfinie.|  
|Appareils Android (inscrits auprès de Microsoft Intune)|Sélectionnez les paramètres de votre choix dans une liste prédéfinie.|  
|Appareils Windows Phone (inscrits auprès de Microsoft Intune)|Sélectionnez les paramètres de votre choix dans une liste prédéfinie.|  
|Ordinateurs Mac (avec le client Configuration Manager)|Permet de créer des éléments de configuration personnalisés afin d’évaluer des éléments tels que les préférences Mac OS X, les valeurs (liste de propriétés) et les résultats retournés par un script.|  
|Ordinateurs Mac (inscrits auprès de Microsoft Intune)|Sélectionnez les paramètres de votre choix dans une liste prédéfinie.|  

## <a name="what-is-a-configuration-item"></a>Qu’est-ce qu’un élément de configuration ?  
 Un élément de configuration peut être considéré comme un conteneur qui stocke les informations suivantes (les informations que vous configurez varient selon le type d’élément de configuration) :  

-   **Informations sur la méthode de détection** (pour les éléments de configuration Windows qui contiennent des paramètres d’application uniquement) : permettent de déterminer si une application est installée en détectant le fichier Windows Installer de l’application ou en utilisant un script personnalisé.  

-   **Paramètres** : les paramètres représentent les critères de l’entreprise ou critères techniques à utiliser pour évaluer la compatibilité sur les appareils clients. Vous pouvez configurer un nouveau paramètre ou accéder à un paramètre existant sur un ordinateur de référence.  

-   **Règles de compatibilité** : les règles de compatibilité spécifient les critères qui définissent la compatibilité d’un paramètre d’élément de configuration. Avant que la compatibilité d'un paramètre puisse être évaluée, celui-ci doit comporter au moins une règle de compatibilité. Certains paramètres permettent de corriger les valeurs qui sont jugées non compatibles. Vous pouvez créer de nouvelles règles ou rechercher un paramètre existant dans tout élément de configuration afin de sélectionner les règles qu’il contient.  

-   **Plateformes prises en charge** : plateformes d’appareils définis par vos soins, sur lesquelles la compatibilité de l’élément de configuration doit être évaluée. Si vous déployez un élément de configuration sur un appareil qui ne figure pas dans la liste des plateformes prises en charge, sa compatibilité n’est pas évaluée.  

## <a name="what-is-a-configuration-baseline"></a>Qu’est-ce qu’une base de référence de configuration ?  
 La conformité est évaluée en définissant une base de référence de configuration contenant les éléments de configuration que vous souhaitez évaluer ainsi que les paramètres et les règles qui régissent le niveau de conformité nécessaire. Les bonnes pratiques définies par Microsoft et d’autres fournisseurs vous invitent à importer ces données de configuration à partir du web dans des packs de configuration de Microsoft System Center Configuration Manager, puis à les importer dans Configuration Manager. Vous pouvez également créer des éléments de configuration et des bases de référence de configuration.  

 Après avoir défini une base de référence de configuration, vous pouvez la déployer vers les utilisateurs et les appareils par le biais de regroupements et évaluer la compatibilité de ses paramètres selon une planification. Vous pouvez déployer plusieurs bases de référence de configuration sur les appareils et bénéficier ainsi d’un niveau de contrôle élevé.  

 Les périphériques client évaluent leur conformité par rapport à chaque ligne de base de configuration déployée et signalent immédiatement les résultats au site à l'aide de messages d'état. Si un appareil client n’est pas actuellement connecté au réseau mais a téléchargé les éléments de configuration référencés dans une base de référence de configuration déployée, la conformité de la base de référence de configuration est évaluée. Les informations de conformité sont envoyées au moment de la reconnexion.  

 Vous pouvez surveiller les résultats de l’évaluation de la compatibilité de la base de référence de configuration à partir du nœud **Déploiements** dans l’espace de travail **Surveillance** de la console Configuration Manager pour afficher les causes les plus courantes de non-conformité, d’erreurs et le nombre d’utilisateurs et d’appareils affectés. Vous pouvez également exécuter des rapports de paramètres de compatibilité afin de trouver d’autres détails, notamment les appareils qui sont conformes ou non, ainsi que l’élément de la base de référence de configuration qui est à l’origine de la non-conformité de l’ordinateur. Vous pouvez également afficher les résultats de l’évaluation de la compatibilité à partir d’ordinateurs Windows exécutant le logiciel client Configuration Manager, à l’aide de l’onglet **Configurations** de **Configuration Manager** dans le panneau de configuration.  

## <a name="user-data-and-profiles-configuration-items"></a>Éléments de configuration des données et profils utilisateur  
 Les éléments de configuration de données et profils utilisateur contiennent des paramètres qui contrôlent la manière dont les utilisateurs inclus dans votre hiérarchie gèrent la redirection des dossiers, les fichiers hors connexion et les profils itinérants sur les ordinateurs qui exécutent Windows 8 et version ultérieure. Vous pouvez les déployer sur des regroupements d’utilisateurs, puis surveiller leur conformité à partir du nœud **Surveillance** de la console Configuration Manager. Contrairement aux autres éléments de configuration, vous n’ajoutez pas ces éléments à des bases de référence de configuration avant de les déployer. Vous pouvez les déployer directement avec la boîte de dialogue **Déployer un élément de configuration des données et profils utilisateur** .  

 Pour plus d’informations, consultez [Créer des éléments de configuration des données et profils utilisateur](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  

## <a name="remote-connection-profiles"></a>Profils de connexion à distance  
 Les profils de connexion à distance dans fournissent un ensemble d’outils et de ressources pour vous aider à créer, déployer et surveiller des paramètres de connexion à distance sur des appareils de votre organisation. En déployant ces paramètres, vous réduisez l'effort fourni par les utilisateurs pour se connecter à leurs ordinateurs sur le réseau d'entreprise.  

Pour plus d’informations, consultez [Créer des profils de connexion à distance](/sccm/compliance/deploy-use/create-remote-connection-profiles).  

## <a name="windows-edition-upgrade"></a>Mise à niveau des éditions de Windows
La stratégie de mise à niveau d’édition vous permet de mettre automatiquement à niveau les appareils qui exécutent certaines versions de Windows 10 vers une version plus récente en fournissant un nouveau fichier de licence ou une nouvelle clé de produit.

Pour plus d’informations, consultez [Mettre à niveau des appareils Windows avec la stratégie de mise à niveau d’édition](/sccm/compliance/deploy-use/upgrade-windows-version).
