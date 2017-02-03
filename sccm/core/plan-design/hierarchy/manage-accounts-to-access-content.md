---
title: "Comptes pour accéder au contenu | Microsoft Docs"
description: "En savoir plus sur les comptes où les clients accèdent au contenu System Center Configuration Manager."
ms.custom: na
ms.date: 1/4/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7df9d0f-fbde-47eb-97e7-3d29536424fa
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 4d34a272a93100426cccd2308c5b3b0b0ae94a60
ms.openlocfilehash: ee83aa6fdbd1a82384a4684055ed72620a3f474e

---
# <a name="manage-accounts-to-access-content-in-system-center-configuration-manager"></a>Gérer les comptes pour accéder au contenu dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de déployer du contenu dans System Center Configuration Manager, vous devez déterminer de quelle façon les clients accèderont à ce contenu à partir des points de distribution.  

-   **Compte d’accès réseau** : compte utilisé par les clients pour se connecter à un point de distribution et accéder au contenu. Par défaut, les clients essaient d’abord d’utiliser leur compte d’ordinateur.  

     Ce compte est également utilisé par les points de distribution d’extraction pour obtenir le contenu d’un point de distribution source dans une forêt distante.  

-   **Compte d’accès au package** : par défaut, Configuration Manager permet aux comptes intégrés appelés **Utilisateurs** et **Administrateurs** d’accéder au contenu d’un point de distribution. Vous pouvez configurer des autorisations supplémentaires pour limiter l’accès.  

-   **Compte de connexion multidiffusion** : compte utilisé pour les déploiements de système d’exploitation.  

##  <a name="a-namebkmknaaa-network-access-account"></a><a name="bkmk_NAA"></a> Compte d’accès réseau  
 Les ordinateurs clients utilisent le compte d'accès réseau lorsqu'ils ne peuvent pas utiliser le compte de leur ordinateur local pour accéder au contenu des points de distribution. Cela s'applique par exemple aux clients de groupes de travail et aux ordinateurs de domaines non approuvés. Ce compte peut également être utilisé pendant le déploiement du système d'exploitation si l'ordinateur qui installe le système d'exploitation ne possède pas encore de compte d'ordinateur sur le domaine.  

-   Les clients utilisent uniquement le compte d’accès réseau pour accéder aux ressources du réseau.  

-   Vous pouvez configurer plusieurs comptes à utiliser comme compte d’accès réseau sur chaque site principal.  

-   Les clients tentent d’abord d’accéder au contenu sur un point de distribution à l’aide de leur compte *nom_ordinateur*$. Si l’accès avec ce compte n’est pas possible, ils tentent alors d’utiliser un compte d’accès réseau. Ensuite, les clients continuent d’essayer d’utiliser le compte d’accès réseau, même en cas d’échec antérieur.  

**Autorisations** : accordez les autorisations minimales appropriées à ce compte pour qu’il puisse accéder au logiciel permettant d’obtenir le contenu demandé par le client.  

-   Le compte doit avoir le droit **Accéder à cet ordinateur à partir du réseau** sur le point de distribution.  

-   Créez le compte dans n'importe quel domaine fournissant l'accès nécessaire aux ressources. Le compte d'accès réseau doit toujours inclure un nom de domaine. La sécurité directe n’est pas prise en charge pour ce compte. Si vous disposez de points de distribution dans plusieurs domaines, créez le compte dans un domaine approuvé.  

> [!TIP]  
>  Pour éviter les verrouillages de compte, ne modifiez pas le mot de passe d'un compte d'accès réseau existant. Au lieu de cela, créez un compte et configurez le nouveau compte dans Configuration Manager. Après un délai suffisant pendant lequel tous les clients ont reçu les informations du nouveau compte, supprimez l'ancien compte des dossiers partagés du réseau et supprimez le compte.  

> [!IMPORTANT]  
>  N'accordez pas à ce compte des autorisations d'ouverture de session interactive.  
>   
>  N'accordez pas à ce compte le droit de joindre les ordinateurs au domaine. Si vous devez joindre les ordinateurs au domaine au cours d'une séquence de tâches, utilisez le compte de jonction de domaine de l'Éditeur de séquence de tâches.  

### <a name="to-configure-the-network-access-account"></a>Pour configurer le compte d'accès réseau  

1.  Dans la console Configuration Manager, cliquez sur **Administration** >   **Configuration du site** >  **Sites**, puis sélectionnez le site.  

2.  Dans le groupe **Paramètres**, cliquez sur **Configurer les composants de site** > **Distribution de logiciels**.  

3.  Cliquez sur l’onglet **Compte d’accès réseau**. Configurez un ou plusieurs comptes, puis cliquez sur **OK**.  

##  <a name="a-namebkmkpaaa-package-access-accounts"></a><a name="bkmk_Paa"></a> Comptes d’accès aux packages  
 Les comptes d'accès au package vous permettent de définir des autorisations NTFS pour spécifier les utilisateurs et les groupes d'utilisateurs qui peuvent accéder à un contenu de package sur des points de distribution. Par défaut, Configuration Manager permet d’accéder uniquement aux **Utilisateurs** et **Administrateurs** de comptes d’accès génériques, mais vous pouvez contrôler l’accès pour les ordinateurs clients en utilisant des groupes ou des comptes Windows supplémentaires. Les appareils mobiles récupèrent toujours le contenu du package de façon anonyme, c’est pourquoi ils n’utilisent pas les comptes d’accès au package.  

 Par défaut, quand Configuration Manager copie les fichiers de contenu d’un package sur un point de distribution, il accorde un accès en **Lecture** au groupe **Utilisateurs** local et un **Contrôle intégral** au groupe **Administrateurs** local. Les autorisations requises dépendent du package. Si vous avez des clients dans des groupes de travail ou dans des forêts non approuvées, ceux-ci utiliseront le compte d'accès réseau pour accéder au contenu du package. Assurez-vous que le compte d'accès réseau bénéficie d'autorisations sur le package à l'aide des comptes d'accès au package définis.  

 Utilisez des comptes dans un domaine susceptible d'accéder aux points de distribution. Si vous créez ou modifiez le compte une fois le package créé, vous devez redistribuer le package. La mise à jour du package ne modifie pas les autorisations de système de fichiers NTFS sur le package.  

 Il est inutile d'ajouter le compte d'accès réseau comme un compte d'accès au package, car l'appartenance au groupe **Utilisateurs** l'ajoute automatiquement. Le fait de restreindre le compte d'accès au package au compte d'accès réseau uniquement n'empêche pas les clients d'accéder au package.  

### <a name="to-manage-access-accounts"></a>Pour gérer les comptes d'accès  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l’espace de travail **Bibliothèque de logiciels**, sélectionnez l’une de ces étapes suivantes pour le type de contenu dont vous souhaitez gérer les comptes d’accès :  

    -   **Applications** : Développez **Gestion d'applications**, cliquez sur **Applications**, puis sélectionnez les applications dont vous souhaitez gérer les comptes d'accès.  

    -   **Packages** : Développez **Gestion d'applications**, cliquez sur **Packages**, puis sélectionnez les packages dont vous souhaitez gérer les comptes d'accès.  

    -   **Packages de déploiement**: Développez **Mises à jour logicielles**, cliquez sur **Packages de déploiement**, puis sélectionnez les packages de déploiement dont vous souhaitez gérer les comptes d'accès.  

    -   **Packages de pilotes**: Développez **Systèmes d'exploitation**, cliquez sur **Packages de pilotes**, puis sélectionnez les packages de pilotes dont vous souhaitez gérer les comptes d'accès.  

    -   **Images du système d'exploitation**: Développez **Systèmes d'exploitation**, cliquez sur **Images du système d'exploitation**, puis sélectionnez les images du système d'exploitation dont vous souhaitez gérer les comptes d'accès.  

    -   **Programmes d'installation de système d'exploitation**: Développez **Systèmes d'exploitation**, cliquez sur **Programmes d'installation de système d'exploitation**, puis sélectionnez les programmes d'installation de système d'exploitation dont vous souhaitez gérer les comptes d'accès.  

    -   **Images de démarrage**: Développez **Systèmes d'exploitation**, cliquez sur **Images de démarrage**, puis sélectionnez les images de démarrage dont vous souhaitez gérer les comptes d'accès.  

3.  Cliquez avec le bouton droit sur l'objet sélectionné, puis cliquez sur **Gérer des comptes d'accès**.  

4.  Dans la boîte de dialogue **Ajouter un compte**, spécifiez le type du compte auquel les droits d’accès au contenu seront accordés, puis indiquez les droits d’accès associés au compte.  

    > [!NOTE]  
    >  Quand vous ajoutez un nom d’utilisateur au compte et que Configuration Manager trouve un compte d’utilisateur local et un compte d’utilisateur de domaine portant ce nom, Configuration Manager définit les droits d’accès du compte d’utilisateur de domaine.  

##  <a name="a-namebkmkmultia-multicast-connection-account"></a><a name="bkmk_multi"></a> Compte de connexion multidiffusion  
 Le compte de connexion multidiffusion est utilisé par des points de distribution qui sont configurés pour la multidiffusion afin de lire les informations de la base de données de site.  

-   Vous spécifiez un compte à utiliser quand vous configurez des connexions de base de données Configuration Manager pour la multidiffusion.  

-   Le compte d’ordinateur du point de distribution est utilisé par défaut, mais vous pouvez configurer un compte d’utilisateur à la place.  

-   Si la base de données de site se trouve dans une forêt non approuvée, vous devez spécifier un compte d’utilisateur.  

-   Le compte doit avoir des autorisations de **lecture** pour la base de données de site.  

Par exemple, si votre centre de données dispose d'un réseau de périmètre dans une forêt autre que celle du serveur de site et de la base de données du site, vous pouvez utiliser ce compte pour lire les informations sur la multidiffusion à partir de la base de données du site.  
Si vous créez ce compte, créez-le en tant que compte local doté de droits limités sur l’ordinateur qui exécute Microsoft SQL Server.  

> [!IMPORTANT]  
>  N'accordez pas à ce compte des autorisations d'ouverture de session interactive  



<!--HONumber=Jan17_HO1-->


