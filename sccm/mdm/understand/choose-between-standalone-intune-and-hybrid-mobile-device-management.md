---
title: Choisir entre Intune autonome et la gestion des appareils mobiles hybride | Microsoft Docs
description: "Choisissez de déployer la gestion des appareils mobiles hybride avec Intune et Configuration Manager ou d’exécuter Intune de façon autonome."
ms.custom: na
ms.date: 11/07/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a5c9e312641d91ff297fbcfa6066a93c2a0e1ee0
ms.openlocfilehash: 3480484a96e96a191b4f02208fcf838db5cb6ba7

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Choisir entre Intune autonome et la gestion des appareils mobiles hybride avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

L’une des questions les plus fréquentes relatives à la gestion des appareils mobiles avec Microsoft Intune est la suivante : « Dois-je intégrer Intune à Configuration Manager (gestion des appareils mobiles hybride) ou exécuter Intune autonome dans la configuration cloud ? ». Pour répondre à cette question, vous devez comparer attentivement les deux options et tenir compte des mises à jour qui seront apportées à Intune début 2017.

## <a name="what-is-intune-standalone"></a>En quoi consiste Intune autonome ?

Intune autonome est une solution cloud de gestion des appareils mobiles qui n’implique aucune ressource locale et qui est gérée à l’aide d’une console web accessible n’importe où dans le monde. Les centres de données Intune sont hébergés en Amérique du Nord, en Europe et en Asie. Intune étant un service cloud, vous pouvez déployer la gestion Intune sur vos appareils dans des délais relativement courts. Vous pouvez également choisir Intune autonome si votre organisation effectue la transition vers le cloud.

## <a name="what-is-hybrid-mdm-with-configuration-manager"></a>En quoi consiste la gestion des appareils mobiles hybride avec Configuration Manager ?

La gestion des appareils mobiles hybride est une solution qui utilise Intune comme canal de remise des stratégies, profils et applications aux appareils. En revanche, elle utilise l’infrastructure locale de Configuration Manager pour stocker et administrer le contenu et gérer les appareils. Vous pouvez choisir la gestion des appareils mobiles hybride si vous avez déjà réalisé des investissements importants dans Configuration Manager et que vous souhaitez étendre son utilisation à la gestion des appareils mobiles. Une implémentation hybride vous offre un « contrôle unifié », ce qui signifie que vous pouvez utiliser la même infrastructure locale et la même console d’administration pour gérer d’une part des appareils mobiles avec Intune et, d’autre part, des PC et des serveurs avec le client Configuration Manager traditionnel.

## <a name="whats-coming-to-intune-standalone-in-early-2017"></a>Nouvelles fonctionnalités d’Intune autonome prévues pour le début de l’année 2017

Si vous devez choisir entre Intune autonome et la gestion des appareils mobiles hybride, tenez compte des nouvelles fonctionnalités d’Intune autonome qui seront dévoilées début 2017. Jusqu’à présent, ce sont les fonctionnalités avancées de la gestion des appareils mobiles hybride qui incitaient certains clients à préférer cette approche à Intune autonome :

-   Accès par programmation (API) : options de gestion SDK et PowerShell

-   Rapports personnalisés : création de rapports personnalisés

-   Contrôle d’accès en fonction du rôle : restriction de l’accès aux fonctions d’administration en fonction des rôles affectés

-   Mise à l’échelle : déploiement et gestion de plus de 50 000 appareils mobiles

-   Contrôle unifié : gestion des PC clients traditionnels et des appareils gérés par Intune dans la même console

Si vous commencez à planifier votre déploiement Intune aujourd’hui et que vous disposez d’une fenêtre de plusieurs mois pour le pilotage, les tests d’acceptation et le déploiement, vous pouvez envisager de choisir Intune autonome compte tenu des nouvelles fonctionnalités qui seront introduites dans le service cloud. Durant le premier semestre de l’année 2017, Intune autonome fera l’objet de mises à jour pour recevoir la plupart des fonctionnalités avancées d’un déploiement hybride avec Configuration Manager. Intune autonome sera bientôt hébergé sur la plateforme cloud Microsoft Azure où il bénéficiera, outre d’une scalabilité accrue, des fonctionnalités suivantes : accès en fonction du rôle par le biais du portail Azure, création de rapports personnalisés et accès par programmation par le biais de l’API Graph Azure.

Vous pouvez passer de la gestion hybride à Intune autonome et vice versa, mais cette opération nécessite l’intervention du support technique de Microsoft. Vous devez aussi désinscrire et réinscrire tous les appareils après la modification de l’autorité de gestion.  Microsoft s’efforce actuellement d’optimiser l’expérience associée au changement de configuration. Les améliorations seront incluses dans une future mise à jour du service.



<!--HONumber=Dec16_HO3-->


