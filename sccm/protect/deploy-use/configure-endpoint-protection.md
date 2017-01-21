---
title: "Configuration d’Endpoint Protection | System Center Configuration Manager"
description: "Apprenez à gérer la sécurité et les logiciels malveillants sur les ordinateurs clients dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5905ab3f63a9956909f3d26136a377ca2f65b71c


---
# <a name="configuring-endpoint-protection-in-system-center-configuration-manager"></a>Configuration d’Endpoint Protection dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant d’utiliser Endpoint Protection pour gérer la sécurité et les programmes malveillants sur des ordinateurs clients Configuration Manager, configurez-le en vous aidant de cette rubrique.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Comment configurer Endpoint Protection dans Configuration Manager  
 Dans Configuration Manager, Endpoint Protection présente des dépendances à l’intérieur et à l’extérieur du produit.  

### <a name="configure-endpoint-protection-in-configuration-manager"></a>Configurer Endpoint Protection dans Configuration Manager  
La configuration d’Endpoint Protection s’effectue en cinq étapes.

|Étape|Détails|
|---|----|
|Étape 1|[Création d’un rôle de système de site de point Endpoint Protection](endpoint-protection-site-role.md) : installez le rôle de système de site de point Endpoint Protection. |
|Étape 2|[Configuration d’alertes pour Endpoint Protection](endpoint-configure-alerts.md) : configurez des alertes Endpoint Protection pour notifier les administrateurs à propos d’événements de sécurité spécifiques se produisant dans votre hiérarchie.|
|Étape 3 | [Configuration des sources de mises à jour de définitions pour les clients Endpoint Protection](endpoint-definition-updates.md) : choisissez l’une des méthodes proposées pour tenir à jour les définitions de logiciel anti-programme malveillant sur les ordinateurs clients.|
|Étape 4|[Configuration de la stratégie de logiciel anti-programme malveillant par défaut et création de stratégies de logiciel anti-programme malveillant personnalisées](endpoint-antimalware-policies.md) : la stratégie de logiciel anti-programme malveillant par défaut est appliquée pendant l’installation du client Endpoint Protection ; les stratégies personnalisées sont appliquées dans un délai de 60 minutes après le déploiement du client.|
|Étape 5|[Configuration des paramètres client personnalisés pour Endpoint Protection](endpoint-protection-configure-client.md) : configurez les paramètres client personnalisés pour Endpoint Protection pour les déployer sur les regroupements d’ordinateurs.|

> [!IMPORTANT]  
>  Si vous gérez Endpoint Protection pour les ordinateurs Windows 10, vous devez configurer Configuration Manager pour mettre à jour et distribuer les définitions de logiciel anti-programme malveillant pour Windows Defender. Windows Defender est inclus dans Windows 10, mais vous devez quand même installer SCEPInstall et configurer les paramètres client personnalisés pour Endpoint Protection (étape 5).  



<!--HONumber=Nov16_HO1-->


