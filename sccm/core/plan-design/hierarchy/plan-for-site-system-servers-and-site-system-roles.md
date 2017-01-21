---
title: "Planifier des rôles de système de site | Documents Microsoft"
description: "Envisagez l’utilisation de serveurs de système de site et de rôles de système de site au moment de planifier votre hiérarchie System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
caps.latest.revision: 11
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2b00cfcec0959716d69a1605018f33d30287fee9
ms.openlocfilehash: a2e57aac01fff3c28b4acfcf58bcd786bd3e62c4


---
# <a name="plan-for-site-system-servers-and-site-system-roles-for-system-center-configuration-manager"></a>Planifier des serveurs de système de site et des rôles système de site pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Chaque site System Center Configuration Manager que vous installez se compose d’un serveur de site qui est un **serveur de système de site**. Le site peut également inclure des serveurs de système de site supplémentaires sur des ordinateurs distants par rapport au serveur de site.   Les serveurs de système de site (serveur de site ou serveur de système de site distant) prennent en charge les **rôles de système de site**.


##  <a name="a-namebkmksiteserversa-site-system-servers"></a><a name="bkmk_siteservers"></a> Serveurs de système de site  
 Lorsque vous installez un rôle système de site sur un ordinateur, celui-ci devient un serveur de système de site. Sur chaque site, vous pouvez installer un ou plusieurs serveurs de système de site supplémentaires. Vous pouvez également décider de ne pas installer de serveur de système de site supplémentaire et exécuter tous les rôles système de site directement sur l’ordinateur serveur de site.  Chaque serveur de système de site prend en charge un ou plusieurs rôles système de site et vous aide à étendre les fonctionnalités et la capacité d’un site en partageant la charge de traitement du processeur que les rôles système de site font peser sur un serveur.  

 Lorsque vous envisagez l’ajout d’un serveur de système de site, assurez-vous que le serveur remplit les conditions préalables à l’utilisation souhaitée, et se trouve dans un emplacement réseau disposant d’une bande passante suffisante pour communiquer avec les points de terminaison prévus, dont le serveur de site, les ressources du domaine, l’emplacement cloud, les serveurs de système de site et les clients.  

 Si vous configurez le serveur de système de site avec un proxy pour une utilisation par des rôles de système de site, consultez [Rôles système de site pouvant utiliser un serveur proxy](#bkmk_proxy)  

##  <a name="a-namebkmkplanrolesa-site-system-roles"></a><a name="bkmk_planroles"></a> Site system roles  
 Des rôles système de site sont installés sur un ordinateur pour fournir au site des fonctionnalités supplémentaires. En voici quelques exemples :  

-   Points de gestion supplémentaires pour que le site puisse prendre en charge plus d’appareils, jusqu’à la capacité de prise en charge des sites  

-   Points de distribution supplémentaires pour développer votre infrastructure de contenu, ce qui améliore les performances des distributions de contenu aux appareils et utilisateurs  

-   Un ou plusieurs rôles de système de site spécifiques aux fonctionnalités, comme un point de mise à jour logicielle, qui vous permettent de gérer les mises à jour logicielles pour des appareils gérés, ou un point de Reporting Services afin de pouvoir exécuter des rapports pour analyser et comprendre ou partager des informations sur le déploiement  


Les différents sites Configuration Manager peuvent prendre en charge un ensemble différent de rôles de système de site. Les rôles système de site pris en charge dépendent du type de site (site d’administration centrale, site principal ou site secondaire). La topologie de votre hiérarchie peut limiter le placement de certains rôles sur certains types de sites. Par exemple, le point de connexion de service est pris en charge uniquement sur le site de niveau supérieur de la hiérarchie, qui peut être un site d’administration centrale ou un site principal autonome. Ce rôle n’est pas pris en charge sur un site principal enfant ou sur des sites secondaires.  

Après l’installation d’un site, vous pouvez déplacer certains rôles de système de site à partir de leur emplacement par défaut sur le serveur de site vers un autre serveur (tel que le point de gestion ou le point de distribution installés par défaut sur un serveur de site principal ou secondaire). Vous pouvez également installer des instances supplémentaires de certains rôles système de site pour étendre les capacités de votre site (fournir plus de services aux clients) et satisfaire les besoins de votre entreprise. Certains rôles sont obligatoires, tandis que d’autres sont facultatifs :  

-   **Serveur de site Configuration Manager** : ce rôle identifie le serveur sur lequel le programme d’installation de Configuration Manager est exécuté pour installer un site, ou le serveur sur lequel vous installez un site secondaire. Ce rôle ne peut pas être déplacé ni désinstallé tant que le site n’a pas été désinstallé.  

-   **Système de site Configuration Manager** : ce rôle est attribué à tout ordinateur sur lequel vous installez un site ou un rôle de système de site.  Ce rôle ne peut pas être déplacé ni désinstallé tant que le dernier rôle de système de site n’a pas été supprimé de l’ordinateur.  

-   **Rôle de système de site de composant Configuration Manager** : ce rôle identifie un système de site qui exécute une instance du service SMS Executive. Il est nécessaire à la prise en charge d’autres rôles, tels que des points de gestion. Ce rôle ne peut pas être déplacé ni désinstallé tant que le dernier rôle de système de site applicable n’a pas été supprimé de l’ordinateur.  

-   **Serveur de base de données de site Configuration Manager** : ce rôle est attribué aux serveurs de système de site qui détiennent une instance de la base de données d’un site.  Ce rôle ne peut être déplacé vers un nouveau serveur qu’en modifiant le site pour utiliser un autre serveur SQL Server pour héberger la base de données du site.  

-   **Fournisseur SMS** : ce rôle est attribué à chaque ordinateur qui héberge une instance du fournisseur SMS, interface entre une console Configuration Manager et la base de données du site.  Par défaut, ce rôle s’installe automatiquement sur le serveur de site d’un site d’administration centrale et de sites principaux, et vous pouvez installer des instances supplémentaires sur chaque site pour fournir à des utilisateurs administratifs supplémentaires l’accès administratif à un site.  

     Contrairement à la plupart des rôles de système de site qui s’installent à partir de la console, pour installer des fournisseurs supplémentaires, vous devez exécuter le programme d’installation de Configuration Manager pour [gérer le fournisseur SMS](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider), puis installer des fournisseurs supplémentaires sur d’autres ordinateurs. Vous ne pouvez installer qu’une seule instance du fournisseur SMS sur un ordinateur, et celui-ci doit être dans le même domaine que le serveur de site.  

-   **Point de service web du catalogue des applications** : rôle de système de site qui fournit des informations logicielles au site web du catalogue des applications à partir de la bibliothèque de logiciels. Bien que ce rôle soit pris en charge uniquement sur des sites principaux, vous pouvez en installer plusieurs instances sur un site ou sur plusieurs sites dans la même hiérarchie.  

-   **Point du site web du catalogue des applications** : rôle de système de site fournissant aux utilisateurs une liste des logiciels disponibles dans le catalogue des applications. Bien que ce rôle soit pris en charge uniquement sur des sites principaux, vous pouvez en installer plusieurs instances sur un site ou sur plusieurs sites dans la même hiérarchie.  

     Si le catalogue d'applications prend en charge des ordinateurs clients sur Internet, comme meilleure pratique de sécurité, installez le point de site Web du catalogue des applications dans un réseau de périmètre et le point de service Web du catalogue des applications sur l'intranet.  

-   **Point de synchronisation Asset Intelligence** : rôle de système de site qui se connecte à Microsoft pour télécharger des informations pour le catalogue Asset Intelligence et charger des titres sans catégorie afin qu’ils puissent être examinés en vue d’être ajoutés à un prochain catalogue.  Une hiérarchie ne prend en charge qu’une seule instance de ce rôle, qui doit être sur le site de niveau supérieur de votre hiérarchie (site d’administration centrale ou site principal autonome). Si vous étendez un site principal autonome vers une hiérarchie plus importante, vous devez désinstaller ce rôle du site principal pour pouvoir l’installer ensuite sur le site d’administration centrale.   Pour plus d’informations, consultez [Asset Intelligence dans System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Point d’enregistrement de certificat** : rôle de système de site qui communique avec un serveur exécutant le service d’inscription de périphériques réseau pour gérer les demandes de certificat d’appareil qui utilisent le protocole SCEP (Simple Certificate Enrollment Protocol).  Ce rôle est pris en charge uniquement sur des sites principaux et le site d’administration centrale.   Bien qu’un point d’enregistrement de certificat unique puisse fournir une fonctionnalité à une hiérarchie entière, pour faciliter l’équilibrage de la charge des demandes de certificat, vous pouvez installer plusieurs instances de ce rôle sur un site et sur plusieurs sites dans la même hiérarchie. Quand plusieurs instances existent dans une hiérarchie, des clients sont affectés de façon aléatoire à l’un des points d’enregistrement de certificat.  

     Chaque point d'enregistrement de certificat requiert l'accès à une instance distincte d'un service d'inscription d'appareils réseau. Vous ne pouvez pas configurer plusieurs points d'enregistrement de certificat pour utiliser le même service d'inscription d'appareils réseau. En outre, le point d’enregistrement de certificat ne doit pas être installé sur le serveur exécutant le service d’inscription de périphérique réseau.  

- **Point de connexion de la passerelle de gestion cloud** : rôle de système de site pour communiquer avec la [passerelle de gestion cloud](/sccm/core/clients/manage/setup-cloud-management-gateway). 

-   **Point de distribution** : rôle de système de site qui contient des fichiers sources que les clients peuvent télécharger, notamment le contenu de l’application, les packages logiciels, les mises à jour logicielles, les images du système d’exploitation et les images de démarrage. Par défaut, ce rôle est installé sur l’ordinateur du serveur de site de nouveaux sites principaux et secondaires lors de l’installation du site, mais n’est pas pris en charge sur un site d’administration centrale.  Vous pouvez installer plusieurs instances de ce rôle sur un site pris en charge et sur plusieurs sites dans la même hiérarchie.  Pour plus d’informations, consultez [Concepts fondamentaux de la gestion de contenu dans System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) et [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   **Point d’état de secours** : rôle de système de site qui vous aide à surveiller l’installation du client et à identifier les clients qui ne sont pas gérés, car ils ne peuvent pas communiquer avec leur point de gestion.  Bien que ce rôle soit pris en charge uniquement sur des sites principaux, vous pouvez en installer plusieurs instances sur un site et sur plusieurs sites dans la même hiérarchie.  Pour plus d'informations, voir [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).


-   **Point Endpoint Protection** : rôle de système de site utilisé par Configuration Manager pour accepter les termes du contrat de licence Endpoint Protection et pour configurer l’appartenance par défaut pour Cloud Protection Service (anciennement MAPS). Une hiérarchie ne prend en charge qu’une seule instance de ce rôle, qui doit être sur le site de niveau supérieur de votre hiérarchie (site d’administration centrale ou site principal autonome). Si vous étendez un site principal autonome vers une hiérarchie plus importante, vous devez désinstaller ce rôle du site principal pour pouvoir l’installer ensuite sur le site d’administration centrale. Pour plus d’informations, consultez [Endpoint Protection dans System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

-   **Point d’inscription** : rôle de système de site qui utilise des certificats PKI pour permettre à Configuration Manager d’inscrire des appareils mobiles et des ordinateurs Mac. Bien que ce rôle soit pris en charge uniquement sur des sites principaux, vous pouvez en installer plusieurs instances sur un site ou sur plusieurs sites dans la même hiérarchie.  

     Si un utilisateur inscrit des appareils mobiles à l’aide de Configuration Manager et que son compte Active Directory se trouve dans une forêt non approuvée par la forêt du serveur de site, vous devez installer un point d’inscription dans la forêt de l’utilisateur pour permettre l’authentification de ce dernier.  

-   **Point proxy d’inscription** : rôle de système de site qui gère les demandes d’inscription Configuration Manager émanant des appareils mobiles et des ordinateurs Mac. Bien que ce rôle soit pris en charge uniquement sur des sites principaux, vous pouvez en installer plusieurs instances sur un site ou sur plusieurs sites dans la même hiérarchie.  

     Lors de la prise en charge d'appareils mobiles sur Internet, comme meilleure pratique de sécurité, installez le point proxy d'inscription dans un réseau de périmètre et le point d'inscription sur l'intranet.  

-   **Connecteur du serveur Exchange Server** : pour plus d’informations, consultez [Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)  

-   **Point de gestion** : rôle de système de site qui fournit aux clients des informations sur l’emplacement du service et de la stratégie, et reçoit les données de configuration de la part des clients.  
    Par défaut, ce rôle est installé sur l’ordinateur du serveur de site de nouveaux sites principaux et secondaires lors de l’installation du site. Les sites principaux prennent en charge plusieurs instances de ce rôle, et les sites secondaires prennent en charge un seul point de gestion pour fournir un point de contact local permettant aux clients d’obtenir des stratégies ordinateur et utilisateur (un point de gestion sur un site secondaire est appelé point de gestion proxy).  

     Des points de gestion peuvent être configurés pour prendre en charge les protocoles HTTP ou HTTPS, ainsi que les appareils mobiles que vous gérez via la fonctionnalité de gestion des appareils mobiles locale de System Center Configuration Manager. Vous pouvez utiliser des [réplicas de base de données pour les points de gestion de System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) pour réduire la charge processeur placée sur le serveur de base de données du site par les points de gestion à mesure qu’ils traitent les demandes des clients.  

-   **Point de Reporting Services** : rôle de système de site qui s’intègre à SQL Server Reporting Services pour créer et gérer des rapports pour Configuration Manager. Ce rôle est pris en charge sur des sites principaux et le site d’administration centrale, et vous pouvez en installer plusieurs instances sur un site pris en charge. Pour plus d’informations, consultez [Planification de la création de rapports dans System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md).  

-   **Point de connexion de service** : rôle de système de site permettant de gérer les appareils mobiles avec Microsoft Intune et la gestion MDM locale. Ce rôle charge aussi les données d’utilisation de votre site sur le serveur, et est nécessaire pour mettre les mises à jour de Configuration Manager à disposition dans la console Configuration Manager. Une hiérarchie ne prend en charge qu’une seule instance de ce rôle, qui doit être sur le site de niveau supérieur de votre hiérarchie (site d’administration centrale ou site principal autonome). Si vous étendez un site principal autonome vers une hiérarchie plus importante, vous devez désinstaller ce rôle du site principal pour pouvoir l’installer ensuite sur le site d’administration centrale. Pour plus d’informations, voir [À propos du point de connexion de service dans System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   **Point de mise à jour logicielle** : rôle de système de site qui s’intègre à Windows Server Update Services (WSUS) pour fournir les mises à jour logicielles aux clients Configuration Manager. Ce rôle est pris en charge sur tous les sites :  

    -   Installez ce système de site sur le site d’administration centrale pour une synchronisation avec Windows Server Update Services.  

    -   Configurez chaque instance de ce rôle sur les sites principaux enfants pour une synchronisation avec le site d’administration centrale.  

    -   Envisagez d’installer un point de mise à jour logicielle sur des sites secondaires quand le transfert de données sur le réseau est lent.  

    Pour plus d’informations, consultez [Planifier les mises à jour logicielles dans System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

-   **Point de migration d’état** : rôle de système de site qui stocke les données d’état utilisateur quand un ordinateur est migré vers un nouveau système d’exploitation. Ce rôle est pris en charge sur des sites principaux et secondaires, et vous pouvez en installer plusieurs instances sur un site et sur plusieurs sites dans la même hiérarchie. Pour plus d’informations sur le stockage de l’état utilisateur quand vous déployez un système d’exploitation, consultez [Gérer l’état utilisateur dans System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   **Point du programme de validation d’intégrité système** : bien que ce rôle de système de site reste visible dans la console Configuration Manager, il n’est plus utilisé avec System Center Configuration Manager.  

##  <a name="a-namebkmkproxya-site-system-roles-that-can-use-a-proxy-server"></a><a name="bkmk_proxy"></a> Rôles système de site pouvant utiliser un serveur proxy  
 Certains rôles de système de site Configuration Manager ont besoin de connexions à Internet et utilisent un serveur proxy quand le serveur de système de site hébergeant le rôle est configuré pour cela. En règle générale, cette connexion est établie dans le contexte du **système** de l’ordinateur sur lequel le rôle de système de site est installé et ne peut pas utiliser une configuration du proxy pour les comptes d’utilisateurs standard. Quand un serveur proxy est requis pour établir une connexion à Internet, vous devez configurer l’ordinateur pour utiliser un serveur proxy :  

-   Vous pouvez configurer un serveur proxy lors de l’installation d’un rôle système de site.  

-   Vous pouvez ajouter ou modifier une configuration de serveur proxy quand vous utilisez la console Configuration Manager.  

-   Tous les rôles système de site sur un serveur de système de site qui peuvent utiliser une configuration du serveur proxy utilisent la même configuration. S’il est nécessaire que différents rôles système de site utilisent des serveurs proxy distincts, vous devez installer les rôles système de site sur des serveurs de système de site séparés.  

-   Si vous modifiez la configuration du serveur proxy, ou installez un nouveau rôle système de site sur un ordinateur ayant déjà une configuration du serveur proxy, la configuration d’origine est remplacée par la nouvelle.  


Pour connaître les procédures de configuration du serveur proxy pour des rôles de système de site, consultez la rubrique [Ajouter des rôles de système de site pour System Center Configuration Manager](../../../core/servers/deploy/configure/add-site-system-roles.md).  

Les rôles système de site pouvant utiliser un serveur proxy sont les suivants :  

-   **Point de synchronisation Asset Intelligence** : ce rôle de système de site se connecte à Microsoft et utilise une configuration de serveur proxy sur l’ordinateur hébergeant le point de synchronisation Asset Intelligence.  

-   **Point de distribution cloud** : quand vous utilisez un point de distribution cloud, le site principal qui gère ce point de distribution doit être en mesure de se connecter à Microsoft Azure pour préparer et analyser le contenu, et le distribuer au point de distribution. Si un serveur proxy est requis pour cette connexion, vous devez configurer le serveur proxy sur le serveur de site principal. Vous ne pouvez pas configurer un serveur proxy sur le point de distribution cloud dans Windows Azure.  Pour plus d’informations, consultez la section [Configurer les paramètres de proxy pour des sites principaux gérant des services cloud](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#BKMK_ConfigProxyforCloud) de la rubrique [Install cloud-based distribution points in Microsoft Azure for System Center Configuration Manager](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md) (Installer des points de distribution cloud dans Microsoft Azure pour System Center Configuration Manager).  

-   **Connecteur du serveur Exchange Server** : ce rôle de système de site se connecte à un serveur Exchange Server et utilise une configuration de serveur proxy sur l’ordinateur hébergeant le connecteur Exchange Server.  

-   **Point de mise à jour logicielle** : ce rôle de système de site peut nécessiter des connexions à Microsoft Update pour télécharger des correctifs et synchroniser les informations sur les mises à jour. En règle générale, lors de la configuration du serveur proxy, chaque rôle de système de site sur l'ordinateur qui prend en charge l'utilisation du serveur proxy utilise le serveur proxy sans aucune configuration supplémentaire. Le point de mise à jour logicielle est une exception à cette règle. Par défaut, un point de mise à jour logicielle n'utilise pas de serveur proxy disponible, sauf si vous activez également les options suivantes lors de la configuration du point de mise à jour logicielle :  

    -   **Utiliser un serveur proxy lors de la synchronisation des mises à jour logicielles**  

    -   **Utiliser un serveur proxy lors du téléchargement du contenu avec des règles de déploiement automatiques**  

    > [!TIP]  
    >  Un serveur proxy doit être configuré sur le serveur de système de site qui héberge le point de mise à jour logicielle avant de pouvoir sélectionner l'une des deux options. Le serveur proxy est utilisé uniquement pour les options spécifiques que vous sélectionnez.  

 Pour plus d’informations sur les serveurs proxy associés aux points de mise à jour logicielle, consultez la section Paramètres du serveur proxy de la rubrique [Installer un point de mise à jour logicielle](../../../sum/get-started/install-a-software-update-point.md).  

-   **Point de connexion de service** : quand ce rôle de système de site est configuré pour être en ligne (et non hors connexion), il se connecte à Microsoft Intune et au service cloud Microsoft.  



<!--HONumber=Dec16_HO3-->


