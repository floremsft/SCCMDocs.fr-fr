---
title: "Choisir une solution de gestion d’appareils pour System Center Configuration Manager"
description: "Découvrez les solutions offertes par System Center Configuration Manager pour la gestion des PC, des serveurs et des appareils."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
caps.latest.revision: 14
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b64135826dd49c594167999aebd322fa3ed61345


---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>Choisir une solution de gestion d’appareils pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager propose différentes solutions pour la gestion des PC, des serveurs et des appareils. Choisissez la solution qui vous convient en fonction des plateformes d’appareils que vous devez gérer et des fonctionnalités de gestion dont vous avez besoin.  


##  <a name="a-namebkmkoverviewa-overview-of-device-management-solutions"></a><a name="bkmk_overview"></a> Vue d’ensemble des solutions de gestion d’appareils  
 Les options permettant de gérer des ordinateurs et des appareils avec Configuration Manager sont les suivantes :  

-   **Gestion des appareils avec le client Configuration Manager**  

     Cette option, qui nécessite l’installation de l’application cliente Configuration Manager sur chaque appareil géré, offre la gamme de fonctionnalités la plus étendue pour gérer les PC, les serveurs et les autres appareils de votre environnement. Cette méthode de gestion des appareils est celle proposée par Configuration Manager depuis son lancement.  

     Pour plus d’informations sur cette solution, consultez [Méthodes d’installation du client dans System Center Configuration Manager](/sccm/core/client/deploy/plan/client-installation-methods).  

-   **Gestion des appareils mobiles avec une infrastructure Configuration Manager locale**  

     Cette option utilise les fonctionnalités de gestion des appareils intégrées aux systèmes d’exploitation de certaines plateformes d’appareils. Bien qu’elle ne soit pas aussi exhaustive que la gestion basée sur le client, la gestion des appareils mobiles locale fournit une approche de gestion plus légère qui fait appel aux ressources Configuration Manager locales pour atteindre et gérer les appareils. La gestion des appareils mobiles locale n’est pour l’instant prise en charge que sur les PC et les appareils mobiles Windows 10.  

     Pour plus d’informations sur cette solution, consultez [Gérer des appareils mobiles avec une infrastructure locale dans System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

-   **Gestion des appareils mobiles avec Microsoft Intune (hybride)**  

     Cette option est appelée gestion des appareils mobiles hybride.  Elle utilise Microsoft Intune pour inscrire et gérer des appareils au lieu d’utiliser les ressources locales Configuration Manager. Même si Intune gère les appareils, vous contrôlez les tâches de gestion dans la console Configuration Manager. Cette option prend en charge tous les principaux systèmes d’exploitation pour appareils mobiles, y compris Windows 10 Mobile, Windows Phone, iOS et Android. Elle permet également de gérer les ordinateurs Windows 8.1 et Windows 10 de votre organisation.  

     Pour plus d’informations sur cette solution, consultez [Gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune](../../mdm/plan-design/hybrid-mobile-device-management.md).  

-   **Gestion des appareils mobiles avec Exchange**  

     Cette option, qui s’appuie sur le connecteur Exchange Server pour connecter plusieurs serveurs Exchange à Configuration Manager, centralise la gestion des appareils qui peuvent se connecter à Exchange ActiveSync. Vous pouvez configurer les fonctionnalités de gestion des appareils mobiles d’Exchange, telles que la réinitialisation à distance de l’appareil et le contrôle des paramètres de plusieurs serveurs Exchange, dans la console Configuration Manager.  

     Pour plus d’informations sur cette solution, consultez [Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

 Vous pouvez utiliser ces solutions de gestion des appareils par elles-mêmes ou les combiner entre elles. Par exemple, vous pouvez utiliser l’approche de gestion basée sur le client pour couvrir la gestion des ordinateurs et des serveurs de votre organisation et utiliser la gestion basée sur Intune pour prendre en charge les appareils mobiles. En combinant les méthodes de cette façon, vous pouvez répondre à tous vos besoins en matière de gestion d’appareils et contrôler le tout à partir de la console Configuration Manager.  

##  <a name="a-namebkmkcomp1a-compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a><a name="bkmk_comp1"></a> Comparer les solutions de gestion des appareils en fonction des plateformes d’appareils mobiles prises en charge  

|Plate-forme|Avec le client Configuration Manager|Configuration Manager avec Microsoft Intune (hybride)|Gestion des appareils mobiles locale|Configuration Manager avec Exchange|  
|--------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Android||Oui||Oui|  
|iOS||Oui||Oui|  
|Mac OS X|Oui|||Oui|  
|UNIX/Linux|Oui|||Oui|  
|Windows 10|Oui|Oui|Oui|Oui|  
|Windows 10 Mobile||Oui|Oui|Oui|  
|Windows (versions précédentes)|Oui|Oui||Oui|  
|Windows CE|Oui (avec le client hérité de l’appareil mobile)|||Oui|  
|Windows Embedded|Oui||||  
|Windows Phone||Oui||Oui|  
|Windows Server|Oui|||Oui|  

 Pour obtenir la liste complète des plateformes prises en charge, consultez [Systèmes d’exploitation pris en charge pour les clients et les appareils pour System Center Configuration Manager](configs\supported-operating-systems-for-clients-and-devices.md).

##  <a name="a-namebkmkcomp2a-compare-mobile-device-management-solutions-based-on-management-functionality"></a><a name="bkmk_comp2"></a> Comparer les solutions de gestion des appareils mobiles en fonction des fonctionnalités de gestion  

|Fonctionnalité de gestion|Avec le client Configuration Manager|Configuration Manager avec Microsoft Intune (hybride)|Gestion des appareils mobiles locale|Configuration Manager avec Exchange|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Sécurité de l’infrastructure à clé publique (PKI) entre l’appareil mobile et Configuration Manager à l’aide de l’authentification mutuelle et SSL pour le chiffrement des transferts de données|Oui|Oui|Oui||  
|Installation du client|Oui||||  
|Prise en charge via Internet|Oui||||  
|découverte,|Oui|||Oui|  
|Inventaire matériel|Oui|Oui|Oui|Oui|  
|Inventaire logiciel|Oui|||Oui|  
|Paramètres|Oui|Oui|Oui|Oui|  
|Déploiement logiciel|Oui|Oui|Oui||  
|Surveillance avec point d’état de secours|Oui||||  
|Connexions aux points de gestion|Oui||Oui||  
|Connexions aux points de distribution|Oui|Oui|Oui||  
|Blocage à partir de Configuration Manager|Oui|Oui|Oui||  
|Mise en quarantaine et blocage à partir d’Exchange Server (et Configuration Manager)||||Oui|  
|Réinitialisation à distance|Oui|Oui|Oui|Oui|  



<!--HONumber=Nov16_HO1-->


