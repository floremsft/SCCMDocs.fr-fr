---
title: Utiliser des services cloud | System Center Configuration Manager
description: "Configurer des ressources cloud pour System Center Configuration Manager afin de compléter votre infrastructure locale."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 72e01c23ab597ad5a446492c3dc371aa50b9d949
ms.openlocfilehash: 9440123f6f13e19723657e7b4d5627f3a349a3b4


---
# <a name="use-cloud-services-with-system-center-configuration-manager"></a>Utiliser des services cloud avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager prend en charge plusieurs options de cloud qui complètent votre infrastructure locale et peuvent aider à résoudre certains problèmes comme :  

-   Gérer les appareils BYOD (en utilisant Intune pour la gestion des appareils mobiles)  

-   Fournir des ressources de contenu à des clients isolés ou des ressources de l’intranet à l’extérieur du pare-feu de l’entreprise (utilisation de points de distribution cloud)  

-   Monter en charge l’infrastructure quand le matériel physique n’est pas disponible ou placé de façon logique pour répondre à vos besoins (utilisation de machines virtuelles Microsoft Azure)  

La configuration de ressources cloud n’est pas indispensable avant de déployer Configuration Manager, mais il peut être utile de comprendre ces options avant d’aller plus en avant dans un plan de conception de hiérarchie. L’utilisation de ressources cloud peut vous faire gagner du temps et économiser de l’argent, mais aussi résoudre des problèmes qu’une infrastructure locale ne peut pas résoudre.  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Ressources cloud que vous pouvez utiliser avec Configuration Manager  
 Chaque option présente des conditions d’utilisation différentes. Vous devez donc étudier plus en détail les conditions préalables, les limitations et les coûts supplémentaires possibles selon le niveau d’utilisation pour chacune des options.  

-   Pour plus d'informations sur les points de distribution cloud, voir [Installer des points de distribution cloud](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure).

-   Pour plus d'informations sur Windows Azure, voir [Windows Azure](http://go.microsoft.com/fwlink/p/?LinkId=262965) dans la bibliothèque MSDN.  

### <a name="microsoft-azure-virtual-machines-for-cloud-based-infrastructure"></a>Machines virtuelles Microsoft Azure (pour infrastructure cloud)  
 Configuration Manager prend en charge l’utilisation d’ordinateurs exécutés en tant que machines virtuelles Azure, de la même manière que les ordinateurs exécutés localement dans votre réseau physique d’entreprise. Vous pouvez utiliser des machines virtuelles Azure dans les scénarios suivants :  

-   **Scénario 1** : vous pouvez exécuter Configuration Manager sur une machine virtuelle et l’utiliser pour gérer des clients installés sur d’autres machines virtuelles.  

-   **Scénario 2** : vous pouvez exécuter Configuration Manager sur une machine virtuelle et l’utiliser pour gérer des clients qui ne s’exécutent pas dans Azure.  

-   **Scénario 3** : vous pouvez exécuter différents rôles de système de site Configuration Manager sur des machines virtuelles tout en exécutant d’autres rôles sur votre réseau physique d’entreprise (avec une connectivité réseau appropriée pour les communications).  

La configuration requise en matière de réseaux, de systèmes d’exploitation et de matériel qui s’applique à l’installation de Configuration Manager sur votre réseau physique d’entreprise est la même que celle qui s’applique à l’installation de Configuration Manager dans Microsoft Azure.  

L’utilisation de machines virtuelles Azure nécessite de disposer d’un abonnement Azure et peut occasionner des frais en fonction du nombre et de la configuration de vos machines virtuelles, ainsi que du niveau d’utilisation des ressources cloud.  

En outre, les sites et les clients Configuration Manager qui s'exécutent sur des machines virtuelles Azure sont soumis aux mêmes exigences de licence que les installations locales.  

### <a name="microsoft-azure-services-for-cloud-based-distribution-points"></a>Services Microsoft Azure (pour points de distribution cloud)  
 Vous pouvez utiliser un service Azure pour héberger un point de distribution Configuration Manager, appelé point de distribution cloud.  Vous pouvez [utiliser un point de distribution cloud avec System Center Configuration Manager](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) en même temps que des points de distribution locaux et des points de distribution déployés sur des machines virtuelles Azure.  

 Cela diffère de l’utilisation d’une machine virtuelle Azure sur laquelle vous déployez un rôle de système de site. Points de distribution cloud :  

-   Ils s’exécutent comme service dans Microsoft Azure, et non sur une machine virtuelle.  

-   Ils se mettent automatiquement à l’échelle pour répondre à l’augmentation des demandes de contenu des clients.  

-   Ils prennent en charge les clients sur Internet et l’intranet.  

Pour pouvoir héberger des points de distribution sur Azure, vous avez besoin d’un abonnement Azure et les frais qui vous sont facturés varient en fonction de la quantité de données qui transitent par le service.  

### <a name="microsoft-intune-for-mobile-device-management"></a>Microsoft Intune (pour gestion des appareils mobiles)  
 Vous pouvez intégrer votre abonnement Microsoft Intune avec Configuration Manager pour permettre la gestion des appareils à l’aide du service Intune. Cette intégration présente les caractéristiques suivantes :  

-   Il s’agit d’une configuration hybride qui étend Configuration Manager (ou Intune selon votre perspective) pour prendre en charge une grande variété d’appareils.  

-   Elle requiert le rôle de système de site Connecteur Microsoft Intune.  

-   Elle nécessite que vous disposiez d’un abonnement Intune distinct avec un nombre suffisant de licences pour les appareils que vous voulez gérer avec Intune.  

Même si Intune utilise Microsoft Azure, vous n’êtes pas tenu de configurer Azure de façon indépendante, et vous ne vous exposez pas à des coûts en supplément de ceux de l’abonnement Intune.  

### <a name="additional-configuration-manager-capabilities"></a>Fonctionnalités supplémentaires de Configuration Manager  
 Certaines fonctionnalités de Configuration Manager peuvent se connecter à des services cloud, par exemple :  

-   Windows Server Update Services (WSUS)  

-   Le cloud du service Configuration Manager pour télécharger les mises à jour de Configuration Manager  

Pour utiliser ces fonctionnalités supplémentaires, vous n’avez pas besoin d’avoir un abonnement Azure, ni de configurer des connexions, certificats ou services particuliers dans le cloud. En effet, ces fonctionnalités sont automatiquement gérées par Configuration Manager à votre place.  Vous devez seulement veiller à ce que les systèmes de site et les appareils puissent accéder aux URL Internet.  

##  <a name="a-namebkmkcloudseca-security-for-cloud-based-services"></a><a name="BKMK_CloudSec"></a> Sécurité des services cloud  
 Configuration Manager utilise des certificats pour configurer votre contenu dans Microsoft Azure et y accéder, et pour gérer les services que vous utilisez. Configuration Manager chiffre les données que vous stockez dans Microsoft Azure, mais n’introduit pas de contrôles de données ou de sécurité en plus de ceux fournis par Microsoft Azure.  

 Pour plus d’informations, consultez les détails des différents scénarios de ressources cloud. Vous pouvez également consulter les rubriques suivantes sur la sécurité dans Microsoft Azure :  

-   [Microsoft Azure : Comprendre la gestion des comptes de sécurité dans Microsoft Azure](http://go.microsoft.com/fwlink/p/?LinkId=262968)  

-   [Windows Azure Security Overview (Présentation des fonctionnalités de sécurité de Windows Azure)](http://go.microsoft.com/fwlink/p/?LinkId=262970)  

-   [Get Past the Security Crossroads in Your Cloud Migration (Franchir les barrières de sécurité dans le cadre d'une migration vers le cloud)](http://go.microsoft.com/fwlink/p/?LinkId=262971)  

-   [La sécurité des données avec Azure - partie 1 sur 2](http://go.microsoft.com/fwlink/p/?LinkId=262974)  



<!--HONumber=Nov16_HO1-->


