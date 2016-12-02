---
title: "Rôles de système de site pour les clients | System Center Configuration Manager"
description: "Déterminez les rôles de système de site pour les clients dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
caps.latest.revision: 9
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 17f28ff5addfbfbab251bdb72be9b405487d1403


---
# <a name="determine-the-site-system-roles-for-system-center-configuration-manager-clients"></a>Déterminer les rôles de système de site pour les clients System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les informations de cet article pour déterminer les systèmes de site dont vous avez besoin pour déployer les clients Configuration Manager :  

 Pour plus d’informations sur l’emplacement d’installation des rôles de système de site requis dans la hiérarchie, consultez [Concevoir une hiérarchie de sites pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

 Pour plus d’informations sur l’installation et la configuration des rôles de système de site dont vous avez besoin, consultez [Installer des rôles de système de site](../../../../core/servers/deploy/configure/install-site-system-roles.md).  

##  <a name="a-namebkmkdeterminempa-determine-whether-you-require-a-management-point"></a><a name="BKMK_Determine_MP"></a> Déterminer si vous avez besoin d’un point de gestion  
 Par défaut, tous les ordinateurs clients Windows utilisent un point de distribution pour installer le client Configuration Manager. En cas d’indisponibilité du point de distribution, ils peuvent basculer sur un point de gestion. Toutefois, vous pouvez installer des clients Windows sur les ordinateurs à partir d’une autre source, en utilisant la propriété de ligne de commande CCMSetup **/source:<chemin_accès\>**.. Par exemple, cela peut être approprié si vous installez des clients sur Internet. Vous pouvez toutefois vouloir éviter d'envoyer des paquets réseau entre les ordinateurs et le point de gestion lors de l'installation du client, par exemple parce qu'un pare-feu bloque les ports nécessaires à votre méthode d'installation ou parce que vous disposez d'une connexion à faible bande passante. Toutefois, tous les clients doivent communiquer avec un point de gestion à attribuer à un site et pour être gérés par Configuration Manager.  

 Pour plus d’informations sur la propriété de ligne de commande CCMSetup **/source:<chemin_accès\>**, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

 Lorsque vous installez plusieurs points de gestion dans la hiérarchie, les clients se connectent automatiquement au point le plus approprié, en fonction des forêts auxquelles ils appartiennent et de leur emplacement réseau. Vous ne pouvez pas installer plusieurs points de gestion dans un site secondaire.  

 Les ordinateurs clients Mac et les clients d’appareil mobile que vous inscrivez à l’aide de Configuration Manager nécessitent dans tous les cas un point de gestion pour l’installation du client. Ce point de gestion doit se trouver dans un site principal. Il doit en outre être configuré pour prendre en charge les appareils mobiles et doit accepter les connexions de clients via Internet. Ces clients ne peuvent pas utiliser les points de gestion des sites secondaires ni se connecter aux points de gestion d'autres sites principaux.  

##  <a name="a-namebkmkdeterminefspa-determine-whether-you-require-a-fallback-status-point"></a><a name="BKMK_Determine_FSP"></a> Déterminer si vous avez besoin d’un point d’état de secours  
 Vous pouvez utiliser un point d'état de secours pour surveiller le déploiement du client sur les ordinateurs Windows et identifier sur ces ordinateurs les clients qui ne sont pas gérés parce qu'ils ne peuvent pas communiquer avec un point de gestion. Les ordinateurs Mac, les appareils mobiles inscrits par le biais de Configuration Manager et les appareils mobiles gérés à l’aide du connecteur du serveur Exchange Server n’utilisent pas de point d’état de secours.  

> [!NOTE]  
>  Un point d'état de secours n'est pas nécessaire pour surveiller l'activité et l'intégrité du client.  

 Le point d'état de secours communique toujours avec les clients via un protocole HTTP, qui utilise des connexions non authentifiées et envoie les données en texte clair. Ainsi, le point d'état de secours est vulnérable aux attaques, en particulier lorsqu'il est utilisé avec la gestion de clients basés sur Internet. Pour réduire la surface d'attaque, dédiez toujours un serveur à l'exécution du point d'état de secours et n'installez aucun autre rôle de système de site sur le même serveur, dans un environnement de production.  

 Installez un point d'état de secours si toutes les conditions suivantes s'appliquent :  

-   Vous souhaitez que les erreurs de communication avec les clients des ordinateurs Windows soient envoyées au site, même si ces ordinateurs clients ne peuvent pas communiquer avec un point de gestion.  

-   Vous souhaitez utiliser les rapports de déploiement de client Configuration Manager, qui contiennent les données envoyées par le point d’état de secours.  

-   Vous disposez d'un serveur dédié pour ce rôle de système de site et avez en outre mis en place des mesures de sécurité pour renforcer la protection du serveur contre les attaques.  

-   Les avantages que présentent l'utilisation d'un point d'état de secours compensent les risques de sécurité liés aux connexions non authentifiées et aux transferts de texte en clair, sur du trafic HTTP.  

 N'installez pas de point d'état de secours dans le cas suivant :  

-   Les risques de sécurité liés à l'exécution d'un site Web avec des connexions non authentifiées et des transferts de texte en clair dépassent les avantages de l'identification des problèmes de communication du client.  

##  <a name="a-namebkmkdeterminerspa-determine-whether-you-require-a-reporting-services-point"></a><a name="BKMK_Determine_RSP"></a> Déterminer si vous avez besoin d’un point de Reporting Services  
 Configuration Manager fournit de nombreux rapports pour vous aider à surveiller l’installation, l’attribution et la gestion des clients sur la console Configuration Manager. Certains rapports sur le déploiement du client exigent que des clients soient attribués à un point d'état de secours.  

 Même si les rapports ne sont pas nécessaires pour déployer des clients et même si vous pouvez consulter des informations détaillées sur le déploiement dans la console Configuration Manager ou dans les fichiers journaux du client, les rapports du client offrent des informations importantes pour vous aider à surveiller et à dépanner le déploiement du client.  

##  <a name="a-namebkmkdetermineenrollmentpointsa-determine-whether-you-require-an-enrollment-point-and-an-enrollment-proxy-point"></a><a name="BKMK_Determine_EnrollmentPoints"></a> Déterminer si vous avez besoin d’un point d’inscription et d’un point proxy d’inscription  
 Configuration Manager a besoin du point d’inscription et du point proxy d’inscription pour inscrire les appareils mobiles et les certificats des ordinateurs Mac. Ces rôles de système de site ne sont pas requis dans les trois cas suivants : si vous avez l’intention de gérer les appareils mobiles à l’aide du connecteur du serveur Exchange Server, si vous installez le client d’appareil mobile hérité (Windows CE, par exemple) ou encore si vous demandez et installez le certificat client sur des ordinateurs Mac indépendamment de Configuration Manager.  

##  <a name="a-namebkmkdeterminedpa-determine-whether-you-require-a-distribution-point"></a><a name="BKMK_Determine_DP"></a> Déterminer si vous avez besoin d’un point de distribution  
 Aucun point de distribution n’est requis pour installer les clients Configuration Manager sur les ordinateurs Windows, mais Configuration Manager utilise par défaut un point de distribution pour installer les fichiers sources du client sur ces ordinateurs. Si nécessaire, il peut également télécharger ces fichiers auprès d’un point de gestion. Les points de distribution ne sont pas utilisés pour installer des clients d’appareils mobiles qui sont inscrits auprès de Configuration Manager, mais ils sont utilisés si vous installez le client hérité de l’appareil mobile. Si vous installez le client Configuration Manager dans le cadre d’un déploiement de système d’exploitation, l’image du système d’exploitation est stockée et récupérée à partir d’un point de distribution.  

 Bien que les points de distribution ne soient pas indispensables pour installer la plupart des clients Configuration Manager, vous aurez besoin de points de distribution pour installer des logiciels tels que les applications et mises à jour logicielles sur les clients.  

##  <a name="a-namebkmkdetermineapplicationcatalogpointsa-determine-whether-you-require-an-application-catalog-website-point-and-an-application-catalog-web-services-point"></a><a name="BKMK_Determine_ApplicationCatalogPoints"></a> Déterminer si vous avez besoin d’un point du site web du catalogue des applications et d’un point de service web du catalogue des applications  
 Le point du site Web du catalogue des applications et le point de service Web du catalogue des applications ne sont pas requis dans le cadre du déploiement de clients. Cependant, il peut être utile de les installer dans le cadre du processus de déploiement des clients, pour que les utilisateurs puissent effectuer les actions suivantes dès que le client Configuration Manager est installé sur les ordinateurs Windows :  

-   Réinitialiser les appareils mobiles.  

-   Recherchez et installez des applications à partir du catalogue d'applications.  

-   Déployez des applications auprès des utilisateurs et des appareils en utilisant l'objet de déploiement **Disponible**.  



<!--HONumber=Nov16_HO1-->


