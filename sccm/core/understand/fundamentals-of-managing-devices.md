---
title: Notions de base de la gestion des appareils | System Center Configuration Manager
description: "Découvrez comment gérer des appareils dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
caps.latest.revision: 6
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f4d39f31723711a7f5ec2b1aa39e81d3a3188029


---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>Notions de base de la gestion des appareils avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager peut gérer deux grandes catégories d’appareils.

La première catégorie, celle des **clients**, comprend les appareils tels que les stations de travail, ordinateurs portables, serveurs et appareils mobiles sur lesquels est installé le logiciel client Configuration Manager qui permet de les gérer.   

La seconde catégorie, celle des **appareils gérés**, peut inclure des clients, mais plus généralement, elle comprend les appareils mobiles sans logiciel client Configuration Manager que vous gérez à l’aide de Microsoft Intune ou en utilisant la gestion des appareils mobiles (MDM) locale intégrée à Configuration Manager.

Outre la gestion des appareils avec ou sans le logiciel client Configuration Manager, vous pouvez utiliser la gestion centrée sur l’utilisateur pour faciliter le regroupement et l’identification des appareils que vous gérez.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Gestion des appareils avec le client Configuration Manager

 La gestion des clients inclut des opérations telles que la collecte de l’inventaire matériel ou logiciel à partir des périphériques, l’installation de nouveaux logiciels sur des appareils, ou la définition des paramètres d’analyse ou d’application de la conformité à une configuration spécifique. Certaines fonctions de gestion, tel l’inventaire matériel, requièrent que le périphérique exécute le logiciel client Configuration Manager. D’autres opérations, telle l’installation (déploiement) de logiciels sur un périphérique, sont prises en charge pour tous les périphériques gérés.  

 Pour gérer un appareil à l’aide du logiciel client Configuration Manager, vous devez soit détecter l’appareil sur votre réseau et déployer (installer) le logiciel client sur cet appareil, soit installer manuellement le logiciel client sur un nouvel ordinateur et associer ensuite cet ordinateur à votre site quand il est joint à votre réseau. Pour découvrir les périphériques sur lesquels le logiciel client n’est pas encore installé, vous exécutez une ou plusieurs des méthodes de découverte intégrées. Après la découverte d’un périphérique, vous pouvez utiliser une des méthodes disponibles pour installer le logiciel client. Pour plus d’informations sur l’utilisation de la découverte, consultez [Exécuter la découverte pour System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

 Après la découverte des appareils pris en charge pour exécuter le logiciel client Configuration Manager, installez le logiciel avec l’une des méthodes disponibles. Une fois le logiciel installé et le client affecté à un site principal, vous pouvez commencer à gérer le périphérique.  Les méthodes d’installation courantes incluent l’Installation Push du client, l’installation basée sur une mise à jour logicielle, l’utilisation d’une stratégie de groupe, l’installation manuelle sur un ordinateur, ou l’inclusion du client dans une image de système d’exploitation que vous déployez.  

 Une fois le client installé, vous pouvez simplifier les tâches de gestion des périphériques en utilisant des regroupements. Ces derniers sont des groupes logiques d’appareils ou d’utilisateurs que vous créez pour effectuer des tâches de gestion sur plusieurs appareils qui partagent un ensemble de critères. Imaginons, par exemple, que vous souhaitez installer une application d’appareil mobile sur tous les appareils mobiles inscrits par Configuration Manager. Dans ce cas, vous pouvez utiliser le regroupement **Tous les appareils mobiles** , qui exclut automatiquement les ordinateurs. Vous pouvez créer vos propres regroupements conformément aux besoins de votre entreprise afin de regrouper logiquement les appareils que vous gérez.  

 Pour plus d’informations, voir les rubriques suivantes :  

-   [Choisir une solution de gestion d’appareils pour System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  

-   [Méthodes d’installation du client dans System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [Présentation des regroupements dans System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Paramètres du client  
 Quand vous installez Configuration Manager pour la première fois, tous les clients de la hiérarchie sont configurés avec les paramètres client par défaut. Vous pouvez ensuite modifier ces paramètres, si vous le souhaitez. Ces paramètres client incluent des options de configuration telles que la fréquence de communication entre les appareils et le site, l’activation ou non des mises à jour logicielles et d’autres opérations de gestion pour le client, et la possibilité ou non pour l’utilisateur d’inscrire ses appareils mobiles pour qu’ils soient gérés par Configuration Manager.  

 Si vous devez appliquer différents paramètres client à certains groupes d'utilisateurs ou d'appareils, créez des paramètres client personnalisés et attribuez-les à des regroupements.  Les membres du regroupement sont configurés pour utiliser les paramètres personnalisés, et vous pouvez créer plusieurs paramètres du client personnalisés qui s’appliquent dans l’ordre (numérique) que vous spécifiez.  En cas de conflit entre paramètres, le paramètre dont le numéro d’ordre est le plus petit remplace les autres paramètres.  

 Le schéma ci-dessous montre comment créer et appliquer des paramètres client personnalisés.  

 ![Paramètres du client](media/ClientSettings.gif)  

 Pour en savoir plus sur les paramètres client, consultez  
                [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) et [À propos des paramètres client dans System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

## <a name="managing-devices-without-the-configuration-manager-client"></a>Gestion des appareils sans client Configuration Manager  
 Configuration Manager prend en charge la gestion de certains appareils qui n’ont pas le logiciel client et qui ne sont pas gérés à l’aide de Microsoft Intune. Pour plus d’informations, consultez [Gérer des appareils mobiles avec une infrastructure locale dans System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) et [Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-centric-management"></a>Gestion centrée sur l'utilisateur  
 Outre les regroupements d'appareils, des regroupements d'utilisateurs contenant les utilisateurs des services de domaine Active Directory sont également disponibles. Quand vous utilisez un regroupement d’utilisateurs, vous pouvez installer le logiciel sur tous les ordinateurs membres du regroupement, vous connecter à celui-ci, puis configurer une **affinité entre utilisateur et périphérique** afin que le logiciel que vous déployez s’installe uniquement sur les appareils spécifiés en tant qu’appareils principaux des utilisateurs. Ces appareils sont appelés « appareils principaux ». Un utilisateur peut posséder un ou plusieurs appareils principaux.  

 Pour contrôler la façon dont les logiciels sont déployés, les utilisateurs peuvent notamment se servir de l’interface client d’ordinateur, le **Centre logiciel**. Le Centre logiciel est automatiquement installé sur les ordinateurs clients. Les utilisateurs peuvent y accéder à partir du menu Démarrer. Le Centre logiciel permet aux utilisateurs de gérer leurs propres logiciels et d’effectuer les opérations suivantes :  

-   Installer le logiciel  

-   Planifier l'installation automatique du logiciel en dehors des heures de travail  

-   Configurer quand Configuration Manager peut installer le logiciel sur l’appareil d’un utilisateur  

-   Configurer les paramètres d’accès pour le contrôle à distance, si le contrôle à distance est activé dans Configuration Manager  

-   Configurer les options de gestion de l'alimentation si un utilisateur administratif l'a autorisé  

 Un lien du Centre logiciel permet aux utilisateurs de se connecter au **catalogue d’applications**, où ils peuvent rechercher, installer et demander des logiciels. En outre, le catalogue d’applications permet aux utilisateurs de configurer certains paramètres de préférence, de réinitialiser leurs appareils mobiles, et (lorsque vous autorisez cette configuration) de spécifier leurs propres appareils principaux pour l’affinité entre utilisateur et appareil. (D’autres méthodes de configuration des informations relatives à l’affinité entre appareil et utilisateur incluent l’importation d’informations à partir d’un fichier et la génération automatique à partir des données d’utilisation.)  

 Comme le Catalogue d'applications est un site Web hébergé par IIS, les utilisateurs peuvent également accéder au Catalogue d'applications directement à partir d'un navigateur, à partir de l'Intranet ou à partir d'Internet.  



<!--HONumber=Nov16_HO1-->


