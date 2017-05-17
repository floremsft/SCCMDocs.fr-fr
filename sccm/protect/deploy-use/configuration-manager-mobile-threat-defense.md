---
title: "Protection contre les menaces mobiles | System Center Configuration Manager"
description: "Limitez l’accès aux ressources d’entreprise en fonction des risques liés aux applications, aux réseaux et aux appareils en utilisant Configuration Manager et les partenaires de protection contre les menaces mobiles Intune."
ms.custom: na
ms.date: 03/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c0e6824-2dfe-4700-b817-d5631e0eb872
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 266897b7ac674a369931e8ed63ff464edc10c9d8
ms.openlocfilehash: 298d879638a2d20d421b19752cb5f20f6725df14
ms.contentlocale: fr-fr
ms.lasthandoff: 05/17/2017


---
# <a name="intune-mobile-threat-defense-connectors-in-configuration-manager"></a>Connecteurs de protection contre les menaces mobiles Intune dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Grâce au [déploiement de la gestion des appareils mobiles hybride (SCCM avec Intune)](https://docs.microsoft.com/en-us/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) et à l’intégration entre Intune et les partenaires de protection contre les menaces, vous pouvez contrôler l’accès aux ressources et aux données d’entreprise en fonction de l’évaluation des risques.

Les connecteurs de protection contre les menaces mobiles Intune vous permettent d’utiliser votre fournisseur de protection contre les menaces mobiles en tant que source d’informations en matière de règles d’accès conditionnelles et de stratégies de conformité. Ainsi, les administrateurs informatiques peuvent ajouter une couche de protection aux ressources d’entreprise telles que Microsoft Exchange et Sharepoint, tout particulièrement en cas de corruption d’appareils mobiles.

## <a name="what-problem-does-this-solve"></a>Quel problème cette fonctionnalité résout-elle ?

Les entreprises doivent protéger leurs données sensibles contre diverses menaces émergentes, notamment les menaces ciblant le matériel, les applications et le réseau ainsi que les vulnérabilités du système d’exploitation.
Historiquement, les entreprises ont été proactives en matière de protection des PC contre les attaques, alors que les appareils mobiles ne sont toujours pas contrôlés et protégés. Les plateformes mobiles offrent maintenant une protection intégrée, grâce à l’isolation d’application et à la vérification des applications des App Store, entre autres, mais elles restent vulnérables aux attaques sophistiquées. Aujourd’hui, de plus en plus d’employés utilisent des appareils dans le cadre de leur travail, et ont besoin d’accéder à des informations sensibles. Or, les appareils doivent être protégés contre des attaques de plus en plus sophistiquées.

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Fonctionnement des connecteurs de protection contre les menaces mobiles Intune

Ce type de connecteur protège les ressources de l’entreprise en créant un canal de communication entre Intune et votre fournisseur de protection contre les menaces mobiles. Les partenaires de protection contre les menaces mobiles Intune proposent des applications intuitives et faciles à déployer sur les appareils mobiles. Ces applications analysent de manière active les informations sur les menaces à partager avec Intune, à des fins d’application ou de création de rapports. Par exemple, si une application de protection contre les menaces mobiles qui est connectée envoie des rapports au fournisseur de cette application indiquant qu’un téléphone est actuellement connecté à un réseau vulnérable aux attaques de l’intercepteur, il partage cette information et lui affecte un niveau de risque approprié (faible, moyen ou élevé). Cette information peut ensuite être comparée avec le niveau de risque accepté qui est configuré pour vos systèmes dans Intune, afin de déterminer si l’accès à certaines ressources doit être supprimé tant que l’appareil est infecté.

## <a name="sample-scenarios"></a>Exemples de scénarios

La solution de protection contre les menaces mobiles considère un appareil comme infecté :

![](http://i.imgur.com/Li1WUOU.png)

L’accès est accordé lorsque la menace est supprimée sur l’appareil :

![](http://i.imgur.com/VCIwpdz.png)

## <a name="mobile-threat-defense-partners"></a>Partenaires de protection contre les menaces mobiles

Découvrez comment protéger l’accès aux ressources d’entreprise en fonction des risques liés aux applications, aux réseaux et aux appareils avec :

- [Lookout](https://docs.microsoft.com/sccm/protect/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)
