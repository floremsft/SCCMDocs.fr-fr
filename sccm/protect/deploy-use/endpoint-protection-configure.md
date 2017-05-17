---
title: Configurer Endpoint Protection | Microsoft Docs
description: "Découvrez comment configurer Configuration Manager pour mettre à jour et distribuer les définitions de programmes malveillants pour Windows Defender."
ms.custom: na
ms.date: 02/14/2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: a8218e23743dafaf8ff1166142cf2dcca1212133
ms.openlocfilehash: 6917644d6719a1ca636713aa5aebf277927123c8
ms.contentlocale: fr-fr
ms.lasthandoff: 05/17/2017


---

# <a name="configure-endpoint-protection"></a>Configurer Endpoint Protection

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour utiliser Endpoint Protection pour gérer la sécurité et les programmes malveillants sur les ordinateurs client Configuration Manager, vous devez au préalable effectuer les étapes de configuration décrites dans cette rubrique.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Comment configurer Endpoint Protection dans Configuration Manager  
 Endpoint Protection comporte des dépendances externes et des dépendances internes à Configuration Manager.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Procédure pour configurer Endpoint Protection dans Configuration Manager  
 Utilisez le tableau suivant pour les étapes, les détails et les informations complémentaires relatifs à la configuration d’Endpoint Protection.  

> [!IMPORTANT]  
>  Si vous gérez Endpoint Protection sur des ordinateurs Windows 10, vous devez configurer Configuration Manager pour mettre à jour et distribuer les définitions de programmes malveillants pour Windows Defender. Windows Defender est inclus dans Windows 10, mais vous devez encore installer SCEPInstall et configurer les paramètres client personnalisés pour Endpoint Protection (comme décrit dans l’**étape 5** ci-dessous).  

|Étapes|Détails|  
|-----------|-------------|  
|**Étape 1** : [Créer un rôle de système de site de point Endpoint Protection](endpoint-protection-site-role.md)|Pour que vous puissiez utiliser Endpoint Protection, le rôle de système de site de point Endpoint Protection doit avoir été installé. Il doit être installé sur un seul serveur de système de site et en haut de la hiérarchie sur un site d'administration centrale ou un site principal autonome. |  
|**Étape 2** : [Configurer des alertes pour Endpoint Protection](endpoint-configure-alerts.md)|Les alertes signalent à l'administrateur des événements spécifiques qui se produisent, tels qu'une infection par un logiciel malveillant. Les alertes s'affichent dans le nœud **Alertes** de l'espace de travail **Surveillance** ou éventuellement elles peuvent être envoyées par courrier électronique à des utilisateurs donnés. |  
|**Étape 3** : [Configurer les sources de mise à jour des définitions pour les clients Endpoint Protection](endpoint-definition-updates.md)|Endpoint Protection peut être configuré pour utiliser diverses sources de téléchargement des mises à jour des définitions. |  
|**Étape 4 :** [Configurer la stratégie de logiciel anti-programme malveillant par défaut et créer des stratégies de logiciel anti-programme malveillant personnalisées](endpoint-antimalware-policies.md)|La stratégie de logiciel anti-programme malveillant par défaut est appliquée au moment de l’installation du client Endpoint Protection. Les stratégies personnalisées que vous avez déployées sont appliquées par défaut dans les 60 minutes consécutives au déploiement du client. Vérifiez que vous avez configuré des stratégies anti-programme malveillant avant de déployer le client Endpoint Protection. |  
|**Étape 5**: [Configurer des paramètres client personnalisés pour Endpoint Protection](endpoint-protection-configure-client.md)|Utilisez des paramètres client personnalisés pour appliquer les paramètres configurés pour Endpoint Protection à certains regroupements d’ordinateurs dans la hiérarchie.<br /><br /> Remarque : configurez les paramètres client par défaut pour Endpoint Protection uniquement si vous voulez les appliquer à l’ensemble des ordinateurs de la hiérarchie. |  

