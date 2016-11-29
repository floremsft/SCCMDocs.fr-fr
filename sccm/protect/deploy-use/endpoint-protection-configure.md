---
title: Configurer Endpoint Protection | System Center Configuration Manager
description: "Découvrez comment configurer Configuration Manager pour mettre à jour et distribuer les définitions de programmes malveillants pour Windows Defender."
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
ms.openlocfilehash: c13ea976057a4267eb6ed0d5c5852b165de868cb


---

# <a name="configure-endpoint-protection-in-system-center-configuration-manager"></a>Configurer Endpoint Protection dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour utiliser Endpoint Protection pour gérer la sécurité et les programmes malveillants sur les ordinateurs client Configuration Manager, vous devez au préalable effectuer les étapes de configuration décrites dans cette rubrique.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Comment configurer Endpoint Protection dans Configuration Manager  
 Endpoint Protection comporte des dépendances externes et des dépendances internes à Configuration Manager.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Procédure pour configurer Endpoint Protection dans Configuration Manager  
 Utilisez le tableau suivant pour les étapes, les détails et les informations complémentaires relatifs à la configuration d’Endpoint Protection.  

> [!IMPORTANT]  
>  Si vous gérez Endpoint Protection sur des ordinateurs Windows 10, vous devez configurer Configuration Manager pour mettre à jour et distribuer les définitions de programmes malveillants pour Windows Defender. Windows Defender est inclus dans Windows 10, mais vous devez encore installer SCEPInstall et configurer les paramètres client personnalisés pour Endpoint Protection (comme décrit dans l’**étape 5** ci-dessous).  

|Étapes|Détails|  
|-----------|-------------|  
|**Étape 1** : Créer un rôle de système de site de point Endpoint Protection|Pour que vous puissiez utiliser Endpoint Protection, le rôle de système de site de point Endpoint Protection doit avoir été installé. Il doit être installé sur un seul serveur de système de site et en haut de la hiérarchie sur un site d'administration centrale ou un site principal autonome. Consultez [Étape 1 : Créer un rôle de système de site de point Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_Step1) dans cette rubrique.|  
|**Étape 2** : Configurer des alertes pour Endpoint Protection|Les alertes signalent à l'administrateur des événements spécifiques qui se produisent, tels qu'une infection par un logiciel malveillant. Les alertes s'affichent dans le nœud **Alertes** de l'espace de travail **Surveillance** ou éventuellement elles peuvent être envoyées par courrier électronique à des utilisateurs donnés. Consultez [Étape 2 : Configurer des alertes pour Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_EPalerts).|  
|**Étape 3** : Configurer les sources des mises à jour des définitions pour les clients Endpoint Protection|Endpoint Protection peut être configuré pour utiliser diverses sources de téléchargement des mises à jour des définitions. Consultez [Étape 3 : Configurer les sources des mises à jour des définitions pour les clients Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_EPdefs).|  
|**Étape 4 :** Configurer la stratégie de logiciel anti-programme malveillant par défaut et créer des stratégies de logiciel anti-programme malveillant personnalisées.|La stratégie de logiciel anti-programme malveillant par défaut est appliquée au moment de l’installation du client Endpoint Protection. Les stratégies personnalisées que vous avez déployées sont appliquées par défaut dans les 60 minutes consécutives au déploiement du client. Assurez-vous d’avoir configuré des stratégies de logiciel anti-programme malveillant avant de déployer le client Endpoint Protection. Consultez [Comment créer et déployer des stratégies anti-programme malveillant pour Endpoint Protection dans System Center Configuration Manager](../../protect/deploy-use/endpoint-antimalware-policies.md).|  
|**Étape 5 :** Configurer des paramètres client personnalisés pour Endpoint Protection.|Utilisez des paramètres client personnalisés pour appliquer les paramètres configurés pour Endpoint Protection à certains regroupements d’ordinateurs dans la hiérarchie.<br /><br /> Remarque : configurez les paramètres client par défaut pour Endpoint Protection uniquement si vous voulez les appliquer à l’ensemble des ordinateurs de la hiérarchie. Consultez [Étape 5 : Configurer des paramètres client personnalisés pour Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_EPclient) dans cette rubrique.|  



<!--HONumber=Nov16_HO1-->


