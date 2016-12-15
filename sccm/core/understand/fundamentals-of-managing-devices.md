---
title: Notions de base de la gestion des appareils | Documents Microsoft
description: "Découvrez comment gérer des appareils dans System Center Configuration Manager."
ms.custom: na
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
caps.latest.revision: 6
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 17b36eae97272c408fce20e1f88812dafc984773
ms.openlocfilehash: b907975db5b5ffa6fefef58902319b987e57dca6


---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>Notions de base de la gestion des appareils avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager peut gérer deux grandes catégories d’appareils :

Les **clients** sont des appareils comme les stations de travail, les ordinateurs portables, les serveurs et les appareils mobiles sur lesquels vous installez le logiciel client Configuration Manager. Certaines fonctions de gestion, comme l’inventaire matériel, nécessitent ce logiciel client.  

Les **appareils gérés** peuvent inclure des *clients*, mais ce sont en général des appareils mobiles où vous n’installez pas le logiciel client Configuration Manager, et que vous gérez à l’aide de Microsoft Intune ou de la gestion des appareils mobiles (MDM) locale intégrée à Configuration Manager.

Vous pouvez aussi regrouper et identifier des appareils en fonction de l’utilisateur et pas seulement du type de client.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Gestion des appareils avec le client Configuration Manager

Pour gérer un appareil à l’aide du logiciel client Configuration Manager, vous devez découvrir l’appareil sur votre réseau et déployer le logiciel client sur cet appareil, ou installer manuellement le logiciel client sur un nouvel ordinateur et joindre ensuite cet ordinateur à votre site quand il est joint à votre réseau. Pour découvrir les appareils sur lesquels le logiciel client n’est pas encore installé, exécutez une ou plusieurs des méthodes de découverte intégrées. Après la découverte d’un appareil, vous pouvez utiliser une des différentes méthodes disponibles pour installer le logiciel client. Pour plus d’informations sur l’utilisation de la découverte, consultez [Exécuter la découverte pour System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

 Après la découverte des appareils pris en charge pour exécuter le logiciel client Configuration Manager, installez le logiciel avec l’une des méthodes disponibles. Une fois le logiciel installé et le client affecté à un site principal, vous pouvez commencer à gérer le périphérique.  Les méthodes d’installation courantes incluent l’Installation Push du client, l’installation basée sur une mise à jour logicielle, l’utilisation d’une stratégie de groupe, l’installation manuelle sur un ordinateur, ou l’inclusion du client dans une image de système d’exploitation que vous déployez.  

 Une fois le client installé, vous pouvez simplifier les tâches de gestion des périphériques en utilisant des regroupements. Les regroupements sont des groupes d’appareils ou d’utilisateurs que vous créez afin de pouvoir les gérer en tant que groupe. Imaginons, par exemple, que vous souhaitez installer une application d’appareil mobile sur tous les appareils mobiles inscrits par Configuration Manager. Dans ce cas, vous pouvez utiliser le regroupement **Tous les appareils mobiles**.  

 Pour plus d’informations, consultez ces rubriques :  

-   [Choisir une solution de gestion d’appareils pour System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  

-   [Méthodes d’installation du client dans System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [Présentation des regroupements dans System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Paramètres du client  
 Quand vous installez Configuration Manager pour la première fois, tous les clients de la hiérarchie sont configurés avec les paramètres client par défaut. Vous pouvez ensuite modifier ces paramètres, si vous le souhaitez. Ces paramètres client incluent des options de configuration telles que la fréquence de communication entre les appareils et le site, l’activation ou non des mises à jour logicielles et d’autres opérations de gestion pour le client, et la possibilité ou non pour l’utilisateur d’inscrire ses appareils mobiles pour qu’ils soient gérés par Configuration Manager.  

Vous pouvez créer des paramètres client personnalisés et les affecter ensuite à des regroupements.  Les membres du regroupement sont configurés pour utiliser les paramètres personnalisés, et vous pouvez créer plusieurs paramètres du client personnalisés qui s’appliquent dans l’ordre (numérique) que vous spécifiez.  En cas de conflit entre paramètres, le paramètre dont le numéro d’ordre est le plus petit remplace les autres paramètres.  

Le schéma ci-dessous montre comment créer et appliquer des paramètres client personnalisés.  

 ![Paramètres du client](media/ClientSettings.gif)  

 Pour en savoir plus sur les paramètres client, consultez  
                [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) et [À propos des paramètres client dans System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

## <a name="managing-devices-without-the-configuration-manager-client"></a>Gestion des appareils sans client Configuration Manager  
 Configuration Manager prend en charge la gestion de certains appareils où le logiciel client n’est pas installé (et qui ne sont pas gérés par Microsoft Intune). Pour plus d’informations, consultez [Gérer des appareils mobiles avec une infrastructure locale dans System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) et [Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-based-management"></a>Gestion basée sur l’utilisateur  
 Regroupements Configuration Manager d’utilisateurs des Services de domaine Active Directory. Quand vous utilisez un regroupement d’utilisateurs, vous pouvez installer des logiciels sur tous les ordinateurs auxquels les membres du regroupement se connectent, puis configurer une **affinité entre utilisateur et appareil** afin que le logiciel que vous déployez s’installe uniquement sur les appareils spécifiés comme appareil principal d’un utilisateur. Un utilisateur peut posséder un ou plusieurs appareils principaux.  

 Pour contrôler la façon dont les logiciels sont déployés, les utilisateurs peuvent notamment se servir de l’interface client d’ordinateur, le **Centre logiciel**. Le Centre logiciel est automatiquement installé sur les ordinateurs clients. Les utilisateurs peuvent y accéder à partir du menu Démarrer. Le Centre logiciel permet aux utilisateurs de gérer leurs propres logiciels et d’effectuer les opérations suivantes :  

-   Installer le logiciel  

-   Planifier l'installation automatique du logiciel en dehors des heures de travail  

-   Configurer quand Configuration Manager peut installer le logiciel sur l’appareil d’un utilisateur  

-   Configurer les paramètres d’accès pour le contrôle à distance, si le contrôle à distance est activé dans Configuration Manager  

-   Configurer les options de gestion de l'alimentation si un utilisateur administratif l'a autorisé  

 Un lien du Centre logiciel permet aux utilisateurs de se connecter au **catalogue d’applications**, où ils peuvent rechercher, installer et demander des logiciels. En outre, le catalogue d’applications permet aux utilisateurs de configurer certains paramètres de préférence, de réinitialiser leurs appareils mobiles, et (lorsque vous autorisez cette configuration) de spécifier leurs propres appareils principaux pour l’affinité entre utilisateur et appareil.   

 Comme le Catalogue d'applications est un site Web hébergé par IIS, les utilisateurs peuvent également accéder au Catalogue d'applications directement à partir d'un navigateur, à partir de l'Intranet ou à partir d'Internet.  



<!--HONumber=Dec16_HO1-->


