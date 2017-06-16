---
title: "Taille et échelle | Microsoft Docs"
description: "Déterminez le nombre de rôles de système de site et de sites dont vous avez besoin pour prendre en charge les appareils dans votre environnement System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
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
ms.translationtype: Human Translation
ms.sourcegitcommit: f9c43e26758d5171a6ef56e827b4b054ebc8a5e5
ms.openlocfilehash: c7ad33339e65e6e00e88f98d6e13baceb98dae77
ms.contentlocale: fr-fr
ms.lasthandoff: 12/30/2016

---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>Taille et échelle de System Center Configuration Manager en chiffres

*S’applique à : System Center Configuration Manager (Current Branch)*



Chaque déploiement de System Center Configuration Manager comporte un nombre maximal de sites, de rôles système de site et d’appareils qu’il peut prendre en charge. Ces nombres varient selon la structure hiérarchique (les types et nombres de sites que vous utilisez) et les rôles de système de site que vous déployez.  Les informations des zones suivantes peuvent vous aider à déterminer le nombre de rôles de système de site et de sites dont vous avez besoin pour prendre en charge les appareils que vous envisagez de gérer avec votre environnement.

Utilisez les informations de cette rubrique ainsi que celles contenues dans les articles suivants :
-   [Matériel recommandé](../../../core/plan-design/configs/recommended-hardware.md)
-   [Systèmes d’exploitation pris en charge pour les serveurs de système de site](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [Systèmes d’exploitation pris en charge pour les clients et appareils](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
-   [Prérequis des sites et systèmes de site](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)


Les numéros de support suivants sont basés sur l’utilisation du matériel recommandé pour Configuration Manager et les paramètres par défaut pour toutes les fonctionnalités disponibles de Configuration Manager. Si vous n’utilisez pas le matériel recommandé ou utilisez des paramètres personnalisés plus agressifs (par exemple, que vous exécutez l’inventaire matériel ou logiciel plus d’une fois tous les 7 jours, ce qui est la valeur par défaut), les performances des systèmes de site peuvent être réduites et ne pas atteindre les niveaux de support indiqués.

##  <a name="bkmk_SiteSystemScale"></a> Types de sites  
 **Site d’administration centrale :**  

-   Un site d’administration centrale peut prendre en charge jusqu’à 25 sites principaux enfants.  

**Site principal :**  

-   Chaque site principal prend en charge jusqu’à 250 sites secondaires.  

-   Le nombre de sites secondaires par site principal est basé sur des connexions réseau WAN continues et fiables. Pour les emplacements de moins de 500 clients, envisagez à un point de distribution au lieu d'un site secondaire.  

 Pour plus d’informations sur le nombre de clients et d’appareils qu’un site principal peut prendre en charge, consultez [Nombres de clients pour les hiérarchies et les sites](#bkmk_clientnumbers) dans cette rubrique.  

**Site secondaire :**  

-   Les sites secondaires ne prennent pas en charge les sites enfants.  

-   Un site d’administration centrale peut prendre en charge jusqu’à 25 sites principaux enfants.  

**Point du site web du catalogue des applications :**  

-   Vous pouvez installer plusieurs instances du point de site Web du catalogue d'applications sur des sites principaux.  

    > [!TIP]  
    >  Comme bonne pratique, installez le point du site web du catalogue d'applications et le point de service web du catalogue d'applications sur le même système de site lorsque ces points fournissent le service aux clients Intranet.  

    -   Pour améliorer les performances, envisagez prendre en charge jusqu'à 50 000 clients par instance.  

    -   Chaque instance de ce rôle de système de site prend en charge le nombre maximal de clients pris en charge par la hiérarchie.  

## <a name="bkmk_roles"></a> Rôles système de site    

**Point de service web du catalogue des applications :**  

-   Vous pouvez installer plusieurs instances du point de service web du catalogue d'applications sur des sites principaux.  

    > [!TIP]  
    >  Comme bonne pratique, installez le point du site web du catalogue d'applications et le point de service web du catalogue d'applications sur le même système de site lorsque ces points fournissent le service aux clients Intranet.  

    -   Pour améliorer les performances, envisagez prendre en charge jusqu'à 50 000 clients par instance.  

    -   Chaque instance de ce rôle de système de site prend en charge le nombre maximal de clients pris en charge par la hiérarchie.  

**Point de distribution :**  

-   Points de distribution par site :  

    -   Chaque site principal et chaque site secondaire prend en charge jusqu'à 250 points de distribution.  

    -   Chaque site principal et secondaire prend en charge jusqu’à 2 000 points de distribution supplémentaires configurés comme points de distribution d’extraction. **Par exemple**, un même site principal prend en charge 2 250 points de distribution quand 2 000 d’entre eux sont configurés comme points de distribution d’extraction.  

    -   Chaque point de distribution prend en charge jusqu'à 4 000 connexions de clients.  

    -   Un point de distribution d’extraction agit comme un client quand il accède au contenu d’un point de distribution source.  

-   Chaque site principal prend en charge un total combiné de 5 000 points de distribution maximum. Ce total inclut tous les points de distribution sur le site principal et tous les points de distribution qui appartiennent aux sites secondaires enfants du site principal.  

-   Chaque point de distribution prend en charge un total combiné allant jusqu'à 10 000 packages et applications.  

> [!WARNING]  
>  Le nombre réel de clients qu’un point de distribution peut prendre en charge dépend de la vitesse du réseau et de la configuration matérielle de l’ordinateur du point de distribution.  
>   
>  De la même façon, le nombre de points de distribution d’extraction qu’un point de distribution source peut prendre en charge dépend de la vitesse du réseau et de la configuration matérielle de l’ordinateur du point de distribution source. Mais ce nombre est également affecté par la quantité de contenu que vous avez déployé. En effet, contrairement aux clients qui accèdent généralement au contenu à des moments différents durant un déploiement, tous les points de distribution d’extraction demandent du contenu en même temps. Ils peuvent demander tout le contenu disponible et pas seulement le contenu qui leur est applicable, comme le ferait un client. Quand une trop grande charge de traitement est placée sur un point de distribution source, des retards imprévus peuvent se produire dans la distribution du contenu aux points de distribution attendus dans votre environnement.  


**Point d’état de secours :**  

-   Chaque point d'état de secours peut prendre en charge jusqu'à 100 000 clients.  

**Point de gestion :**  

-   Chaque site principal prend en charge jusqu’à 15 points de gestion.  

    > [!TIP]  
    >  N’installez pas de point de gestion sur des serveurs qui sont sur une liaison lente à partir du serveur de site principal ou du serveur de bases de données du site.  

-   Chaque site secondaire prend en charge un seul point de gestion qui doit être installé sur le serveur de site secondaire.  

 Pour plus d’informations sur le nombre de clients et d’appareils qu’un point de gestion peut prendre en charge, consultez la section [Points de gestion](#bkmk_mp) de cette rubrique.  

**Point de mise à jour logicielle :**  

-   Un point de mise à jour logicielle installé sur le serveur de site peut prendre en charge jusqu'à 25 000 clients.  

-   Un point de mise à jour logicielle distant du serveur de site peut prendre en charge jusqu’à 150 000 clients quand l’ordinateur distant répond à la configuration requise de WSUS (Windows Server Update Services) consistant à prendre en charge ce nombre de clients.  

-   Par défaut, Configuration Manager ne prend pas en charge la configuration de points de mise à jour logicielle comme clusters d’équilibrage de la charge réseau (NLB). Toutefois, vous pouvez utiliser le kit SDK Configuration Manager pour configurer jusqu’à quatre points de mise à jour logicielle sur un cluster NLB.  

##  <a name="bkmk_clientnumbers"></a> Nombres de clients pour les hiérarchies et les sites  
 Utilisez les informations suivantes pour déterminer le nombre de clients et leurs types que vous pouvez prendre en charge sur un site ou dans une hiérarchie.  

###  <a name="bkmk_cas"></a> Hiérarchie avec un site d’administration centrale  
Un site d’administration centrale prend en charge un nombre total d’appareils pouvant atteindre le nombre d’appareils répertoriés pour les trois groupes suivants :  

-   700 000 ordinateurs de bureau (exécutant Windows, Linux et UNIX)  

-   25 000 appareils exécutant Mac et Windows CE 7.0  

-   L’un des nombres suivants, selon la manière dont votre déploiement prend en charge la gestion des appareils mobiles :  

    -   100 000 appareils que vous gérez à l’aide de la gestion MDM locale  

    -   300 000 appareils cloud  

 Par exemple, dans une hiérarchie, vous pouvez prendre en charge 700 000 ordinateurs de bureau, jusqu’à 25 000 clients Mac et Windows CE 7.0, et jusqu’à 300 000 appareils cloud quand vous intégrez Microsoft Intune, soit un total de 1 025 000 appareils. Si vous prenez en charge des appareils gérés par la gestion MDM locale, la hiérarchie compte 825 000 appareils au total.  

> [!IMPORTANT]  
>  Une hiérarchie où le site d’administration centrale utilise une édition Standard de SQL Server prend en charge un maximum de 50 000 ordinateurs de bureau et appareils. L’édition de SQL Server utilisée sur un site principal autonome ne limite pas la capacité du site consistant à prendre en charge au maximum le nombre indiqué de clients.  


###  <a name="bkmk_chipri"></a> Site principal enfant  
Chaque site principal enfant dans une hiérarchie avec un site d’administration centrale prend en charge les éléments suivants :  

-   Un total de 150 000 clients et appareils, non limités à un groupe ou à un type spécifiques, à condition que la prise en charge ne dépasse pas le nombre pris en charge par la hiérarchie.  

Par exemple, un site principal qui prend en charge 25 000 ordinateurs exécutant des clients Mac et Windows CE 7.0 (la limite d’une hiérarchie) peut prendre en charge 125 000 ordinateurs de bureau supplémentaires. Le nombre total d’appareils pris en charge atteint alors la limite maximale de 150 000 prise en charge par le site principal enfant.

###  <a name="bkmk_pri"></a> Site principal autonome  
Un site principal autonome prend en charge le nombre suivant d’appareils :  

-   Total de 175 000 clients et appareils, sans dépasser :  

    -   150 000 ordinateurs de bureau (exécutant Windows, Linux et UNIX)  

    -   25 000 appareils exécutant Mac et Windows CE 7.0

    -   L’un des nombres d’éléments suivants, selon la manière dont votre déploiement prend en charge la gestion des appareils mobiles :  

        -   50 000 appareils que vous gérez à l’aide de la gestion MDM locale  

        -   150 000 appareils cloud  

Par exemple, un site principal autonome prenant en charge 150 000 ordinateurs de bureau et 10 000 clients Mac ou Windows CE 7.0 ne peut prendre en charge que 15 000 appareils supplémentaires. Ces appareils peuvent être basés sur le cloud ou gérés à l’aide de la gestion MDM locale.  

###  <a name="bkmk_sec"></a> Sites secondaires  
Les sites secondaires prennent en charge les éléments suivants :  

-   15 000 ordinateurs de bureau (exécutant Windows, Linux et UNIX)  

###  <a name="bkmk_mp"></a> Points de gestion  
Chaque point de gestion peut prendre en charge le nombre suivant d’appareils :  

-   Total de 25 000 clients et appareils, sans dépasser :  

    -   25 000 ordinateurs de bureau (exécutant Windows, Linux et UNIX)  

    -   L’un des nombres d’éléments suivants (pas les deux) :  

        -   10 000 appareils que vous gérez à l’aide de la gestion MDM locale  

        -   10 000 appareils exécutant des clients Mac et Windows CE 7.0

