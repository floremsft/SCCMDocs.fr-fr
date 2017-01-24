---
title: "Taille et l’échelle | Microsoft Docs"
description: "Déterminez le nombre de rôles système de site et de sites dont vous aurez besoin pour prendre en charge les appareils dans votre environnement System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 453d934d693d58e98cf800988dff702400daaf95

---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>Taille et échelle de System Center Configuration Manager en chiffres

*S’applique à : System Center Configuration Manager (Current Branch)*



Chaque déploiement de System Center Configuration Manager comporte un nombre maximal de sites, de rôles système de site et d’appareils qu’il peut prendre en charge. Ces nombres varient selon la structure hiérarchique (les types et nombres de sites que vous utilisez) et les rôles système de site que vous déployez.  Les informations contenues dans les sections suivantes peuvent vous aider à déterminer le nombre de rôles système de site et de sites dont vous avez besoin pour prendre en charge les appareils que vous envisagez de gérer avec votre environnement.

Utilisez les informations de cette rubrique ainsi que celles contenues dans les articles suivants :
-   [Matériel recommandé](../../../core/plan-design/configs/recommended-hardware.md)
-   [Systèmes d’exploitation pris en charge pour les serveurs de système de site](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [Systèmes d’exploitation pris en charge pour les clients et appareils](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
-   [Prérequis des sites et systèmes de site](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)

Les nombres indiqués dans cet article se basent sur l’utilisation du matériel recommandé pour Configuration Manager. Quand vous n’utilisez pas le matériel recommandé, les performances des systèmes de site peuvent se dégrader et ne pas correspondre aux niveaux indiqués de prise en charge.

##  <a name="a-namebkmksitesystemscalea-site-types"></a><a name="bkmk_SiteSystemScale"></a> Types de sites  
 **Site d’administration centrale :**  

-   Un site d’administration centrale peut prendre en charge jusqu’à 25 sites principaux enfants.  

**Site principal :**  

-   Chaque site principal prend en charge jusqu’à 250 sites secondaires.  

-   Le nombre de sites secondaires par site principal est basé sur des connexions réseau WAN continues et fiables. Pour les emplacements de moins de 500 clients, envisagez à un point de distribution au lieu d'un site secondaire.  

 Pour plus d’informations sur les nombres de clients et d’appareils qu’un site principal peut prendre en charge, consultez [Nombres de clients pour les hiérarchies et les sites](#bkmk_clientnumbers) dans cette rubrique.  

**Site secondaire :**  

-   Les sites secondaires ne prennent pas en charge les sites enfants.  

-   Un site d’administration centrale peut prendre en charge jusqu’à 25 sites principaux enfants.  

**Point du site web du catalogue des applications :**  

-   Vous pouvez installer plusieurs instances du point de site Web du catalogue d'applications sur des sites principaux.  

    > [!TIP]  
    >  Comme meilleure pratique, installez le point du site Web du catalogue d'applications et le point de service Web du catalogue d'applications sur le même système de site lorsque ces points fournissent le service aux clients Intranet.  

    -   Pour améliorer les performances, envisagez prendre en charge jusqu'à 50 000 clients par instance.  

    -   Chaque instance de ce rôle de système de site prend en charge le nombre maximal de clients pris en charge par la hiérarchie.  

## <a name="a-namebkmkrolesa-site-system-roles"></a><a name="bkmk_roles"></a> Rôles système de site    

**Point de service web du catalogue des applications :**  

-   Vous pouvez installer plusieurs instances du point de service web du catalogue d'applications sur des sites principaux.  

    > [!TIP]  
    >  Comme bonne pratique, installez le point du site web du catalogue d'applications et le point de service web du catalogue d'applications sur le même système de site lorsque ces points fournissent le service aux clients Intranet.  

    -   Pour améliorer les performances, envisagez prendre en charge jusqu'à 50 000 clients par instance.  

    -   Chaque instance de ce rôle de système de site prend en charge le nombre maximal de clients pris en charge par la hiérarchie.  

**Point de distribution :**  

-   Points de distribution par site :  

    -   Chaque site principal et chaque site secondaire prend en charge jusqu'à 250 points de distribution.  

    -   Chaque site principal et chaque secondaire prend en charge jusqu'à 2 000 points de distribution supplémentaires configurés comme points de distribution d'extraction. **Par exemple**, un même site principal prend en charge 2 250 points de distribution quand 2 000 d’entre eux sont configurés comme points de distribution d’extraction.  

    -   Chaque point de distribution prend en charge jusqu'à 4 000 connexions de clients.  

    -   Un point de distribution d'extraction agit comme un client quand il accède à du contenu à partir d'un point de distribution source.  

-   Chaque site principal prend en charge un total combiné de 5 000 points de distribution maximum. Ce total inclut tous les points de distribution sur le site principal et tous les points de distribution qui appartiennent à des sites secondaires enfants du site principal.  

-   Chaque point de distribution prend en charge un total combiné allant jusqu'à 10 000 packages et applications.  

> [!WARNING]  
>  Le nombre réel de clients qu'un point de distribution peut prendre en charge dépend de la vitesse du réseau et de la configuration matérielle de l'ordinateur du point de distribution.  
>   
>  Le nombre de points de distribution d'extraction pris en charge par un point de distribution source dépend de même de la vitesse du réseau et de la configuration matérielle de l'ordinateur du point de distribution source, mais il est également affecté par la quantité de contenu que vous avez déployé. La raison en est que, contrairement aux clients qui accèdent généralement au contenu à des moments différents au cours d'une fenêtre de déploiements, tous les points de distribution d'extraction demandent du contenu en même temps, et ils peuvent demander tout le contenu disponible et pas seulement le contenu qui leur est applicable, comme le ferait un client. Quand une trop grande part d'une charge de traitement est placée sur un point de distribution source, cela peut entraîner des retards imprévus dans la distribution du contenu aux points de distribution attendus dans votre environnement.  


**Point d’état de secours :**  

-   Chaque point d'état de secours peut prendre en charge jusqu'à 100 000 clients.  

**Point de gestion :**  

-   Chaque site principal prend en charge jusqu’à 15 points de gestion.  

    > [!TIP]  
    >  N’installez pas de points de gestion sur des serveurs qui sont sur une liaison lente à partir du serveur de site principal ou du serveur de bases de données du site.  

-   Chaque site secondaire prend en charge un seul point de gestion qui doit être installé sur le serveur de site secondaire.  

 Pour plus d’informations sur les nombres de clients et d’appareils qu’un point de gestion peut prendre en charge, consultez la section [Points de gestion](#bkmk_mp) de cette rubrique.  

**Point de mise à jour logicielle :**  

-   Un point de mise à jour logicielle installé sur le serveur de site peut prendre en charge jusqu'à 25 000 clients.  

-   Un point de mise à jour logicielle distant du serveur de site peut prendre en charge jusqu’à 150 000 clients quand l’ordinateur distant présente la configuration requise de WSUS pour prendre en charge ce nombre de clients.  

-   Par défaut, Configuration Manager ne prend pas en charge la configuration de points de mise à jour logicielle comme clusters d’équilibrage de la charge réseau (NLB). Toutefois, vous pouvez utiliser le SDK Configuration Manager pour configurer jusqu’à quatre points de mise à jour logicielle sur un cluster d’équilibrage de la charge réseau (NLB).  

##  <a name="a-namebkmkclientnumbersa-client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a> Nombres de clients pour les hiérarchies et les sites  
 Utilisez les informations suivantes pour déterminer le nombre de clients, et leurs types, que vous pouvez prendre en charge sur un site ou dans une hiérarchie.  

###  <a name="a-namebkmkcasa-hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a> Hiérarchie avec un site d’administration centrale  
Un site d’administration centrale prend en charge un nombre total d’appareils pouvant atteindre le nombre d’appareils répertoriés pour les trois groupes suivants :  

-   700 000 ordinateurs de bureau (exécutant Windows, Linux et UNIX)  

-   25 000 appareils exécutant Mac et Windows CE 7.0  

-   L’un des nombres d’éléments suivants, selon la manière dont votre déploiement prend en charge la gestion des appareils mobiles :  

    -   100 000 appareils que vous gérez avec des applications MDM locales  

    -   300 000 appareils cloud  

 Par exemple, dans une hiérarchie, vous pouvez prendre en charge 700 000 ordinateurs de bureau, jusqu’à 25 000 clients Mac et Windows CE 7.0, et jusqu’à 300 000 appareils cloud lorsque vous intégrez Microsoft Intune, soit un total de 1 025 000 appareils.  Si vous prenez en charge des appareils gérés par des applications MDM locales, la hiérarchie totalise 825 000 appareils.  

> [!IMPORTANT]  
>  Une hiérarchie où le site d’administration centrale utilise une édition Standard de SQL Server, prend en charge un maximum de 50 000 ordinateurs de bureau et appareils. L’édition de SQL Server utilisée sur un site principal autonome ne limite pas cette capacité de sites pour prendre en charge jusqu’au nombre indiqué de clients.  


###  <a name="a-namebkmkchipria-child-primary-site"></a><a name="bkmk_chipri"></a> Site principal enfant  
Chaque site principal enfant dans une hiérarchie avec un site d’administration centrale prend en charge les éléments suivants :  

-   Total de 150 000 clients et appareils, non limités à un groupe ou à un type spécifiques, pour autant que le prise en charge ne dépasse pas le nombre pris en charge pour la hiérarchie  

Par exemple, un site principal qui prend en charge 25 000 ordinateurs Mac et Windows CE 7.0 (car c’est la limite d’une hiérarchie), peut alors prendre en charge 125 000 ordinateurs de bureau supplémentaires, pour atteindre le nombre total d’appareils pris en charge à la limite maximale prise en charge du nombre de sites principaux enfants s’élevant à 150 000.

###  <a name="a-namebkmkpria-stand-alone-primary-site"></a><a name="bkmk_pri"></a> Site principal autonome  
Un site principal autonome prend en charge le nombre suivant d’appareils :  

-   Total de 175 000 clients et appareils, sans dépasser :  

    -   150 000 ordinateurs de bureau (exécutant Windows, Linux et UNIX)  

    -   25 000 appareils exécutant Mac et Windows CE 7.0  

    -   L’un des nombres d’éléments suivants, selon la manière dont votre déploiement prend en charge la gestion des appareils mobiles :  

        -   50 000 appareils que vous gérez avec des applications MDM locales  

        -   150 000 appareils cloud  

Par exemple, un site principal autonome prenant en charge 150 000 ordinateurs de bureau et 10 000 clients Mac ou Windows CE 7.0 ne peut prendre en charge que 15 000 appareils supplémentaires. Ceux-ci peuvent être basés sur le cloud ou gérés à l’aide de la gestion MDM locale.  

###  <a name="a-namebkmkseca-secondary-sites"></a><a name="bkmk_sec"></a> Sites secondaires  
Les sites secondaires prennent en charge les éléments suivants :  

-   15 000 ordinateurs de bureau (exécutant Windows, Linux et UNIX)  

###  <a name="a-namebkmkmpa-management-points"></a><a name="bkmk_mp"></a> Points de gestion  
Chaque point de gestion peut prendre en charge le nombre suivant d’appareils :  

-   Total de 25 000 clients et appareils, sans dépasser :  

    -   25 000 ordinateurs de bureau (exécutant Windows, Linux et UNIX)  

    -   L’un des nombres d’éléments suivants (pas les deux) :  

        -   10 000 appareils gérés à l’aide de la gestion MDM locale  

        -   10 000 appareils exécutant Mac et Windows CE 7.0  



<!--HONumber=Dec16_HO3-->


