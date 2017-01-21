---
title: "Restreindre l’accès en fonction du risque évalué | System Center Configuration Manager"
description: "Restreignez l’accès aux ressources d’entreprise en fonction du risque évalué pour l’appareil, le réseau et l’application."
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c0e6824-2dfe-4700-b817-d5631e0eb872
caps.latest.revision: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c13c6268fa76ade7feb0981f9c4a6e325e393aca
ms.openlocfilehash: 70ceac5d4ec88197ec8a08103a08d4218fac6136


---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gérer l’accès aux ressources d’entreprise en fonction du risque évalué pour l’appareil, le réseau et l’application

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez contrôler l’accès aux ressources d’entreprise à partir des appareils mobiles, en fonction de l’évaluation des risques effectuée par Lookout, une solution de protection des appareils contre les menaces qui est intégrée à Microsoft Intune. Le risque est évalué sur la base des données de télémétrie que le service Lookout collecte auprès des appareils pour les vulnérabilités du système d’exploitation, les applications malveillantes installées et les profils réseau malveillants. 

Sur la base de l’évaluation des risques signalée par Lookout grâce aux stratégies de conformité SCCM (System Center Configuration Manager), vous pouvez configurer des stratégies d’accès conditionnel et autoriser ou bloquer des appareils évalués comme non conformes en raison des menaces qui y ont été détectées.  

## <a name="what-problem-does-this-solve"></a>Quel problème cette fonctionnalité résout-elle ?
Les entreprises et les organisations doivent protéger leurs données sensibles contre diverses menaces émergentes, notamment les menaces ciblant le matériel, les applications et le réseau, ainsi que les vulnérabilités du système d’exploitation.

Depuis plusieurs années, les entreprises et les organisations ont mis en place une politique active de protection des PC contre les attaques malveillantes. En revanche, les appareils mobiles ne sont souvent pas protégés correctement. Les plateformes mobiles offrent maintenant une protection intégrée du système d’exploitation par le biais de techniques telles que l’isolation d’application et la vérification des applications des App Store, mais elles restent vulnérables aux attaques sophistiquées. Les appareils mobiles sont de plus en plus utilisés par les employés dans un cadre professionnel et nécessitent un accès à des informations parfois sensibles et stratégiques. Il est donc essentiel de protéger ces appareils contre les diverses attaques sophistiquées actuelles.

Le [déploiement de la gestion des appareils mobiles hybride (SCCM avec Intune)](https://docs.microsoft.com/en-us/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) vous permet de contrôler l’accès aux ressources et aux données d’entreprise en fonction de l’évaluation des risques fournie par des solutions de protection des appareils contre les menaces comme Lookout.

## <a name="how-do-the-hybrid-mdm-deployment-and-lookout-device-threat-protection-help-protect-company-resources"></a>Comment le déploiement de la gestion des appareils mobiles hybride et le service Lookout de protection des appareils contre les menaces vous aident-ils à protéger les ressources d’entreprise ?
Quand l’application mobile de Lookout (Lookout for Work) est exécutée sur des appareils mobiles, elle capture des données de télémétrie sur le système de fichiers, la pile réseau, l’appareil et l’application (le cas échéant), et envoie toutes ces données au service cloud Lookout de protection des appareils contre les menaces, qui calcule le risque cumulé des menaces mobiles pour l’appareil. Vous pouvez également modifier la classification des niveaux de risque des menaces dans la console Lookout pour l’adapter à vos besoins.  

La stratégie de conformité dans SCCM inclut maintenant une nouvelle règle pour la protection contre les menaces mobiles de Lookout qui est basée sur l’évaluation du risque de menaces sur les appareils réalisée par Lookout. Quand cette règle est activée, l’appareil est évalué pour vérifier s’il est conforme.

Si l’appareil est évalué comme non conforme à la stratégie de conformité, l’accès aux ressources telles que SharePoint Online et Exchange Online peut être bloqué à l’aide de stratégies d’accès conditionnel. Si l’accès est bloqué, une procédure pas à pas est indiquée aux utilisateurs finaux pour les aider à résoudre le problème et à récupérer l’accès aux ressources d’entreprise. Cette procédure pas à pas s’affiche dans l’application Lookout for Work.

## <a name="supported-platforms"></a>Plateformes prises en charge :
* **Android 4.1 et versions ultérieures**, et inscription à Microsoft Intune.
* **iOS 8 et versions ultérieures**, et inscription à Microsoft Intune.
Pour plus d’informations sur les plateformes et les langues prises en charge par Lookout, consultez cet [article](https://personal.support.lookout.com/hc/en-us/articles/114094140253).

## <a name="prerequisites"></a>Conditions préalables :
* [Déploiement de la gestion des appareils mobiles hybride](https://docs.microsoft.com/en-us/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)
* Abonnement à Microsoft Intune et Azure Active Directory.
* Abonnement d’entreprise à Lookout Mobile EndPoint Security.  Pour plus d’informations, consultez [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security)

## <a name="example-scenarios"></a>Exemples de scénarios
Voici quelques scénarios courants :
### <a name="control-access-based-on-threat-from-malicious-apps"></a>Contrôler l’accès en fonction de la menace émanant des applications malveillantes :
Quand des applications ou programmes malveillants sont détectés sur un appareil, vous pouvez empêcher l’appareil d’effectuer les opérations suivantes :
* Se connecter à la messagerie d’entreprise tant que la menace n’est pas résolue.
* Synchroniser les fichiers d’entreprise à l’aide de l’application OneDrive pour le travail.
* Accéder à des applications stratégiques.

**Accès bloqué après la détection d’applications malveillantes :**

![Diagramme illustrant une stratégie d’accès conditionnel interdisant l’accès quand l’appareil est évalué comme non conforme en raison de la présence d’applications malveillantes](../media/config-mgr-maliciousapps_blocked.png)

**Appareil débloqué pouvant accéder aux ressources d’entreprise après correction de la menace :**

![Diagramme illustrant une stratégie d’accès conditionnel accordant l’accès quand l’appareil est évalué comme conforme après correction](../media/config-mgr-maliciousapps-unblocked.png)
### <a name="control-access-based-on-threat-to-network"></a>Contrôler l’accès en fonction de la menace pour le réseau :
Détectez les menaces pour votre réseau, telles que les attaques de l’intercepteur (« Man-in-the-middle »), et restreignez l’accès aux réseaux Wi-Fi en fonction du risque évalué pour l’appareil.

**Accès au réseau par Wi-Fi bloqué :**

![Diagramme illustrant l’accès conditionnel interdisant l’accès par Wi-Fi en fonction des menaces pour le réseau](../media/config-mgr-network-wifi-blocked.png)

**Accès accordé après correction :**

![Diagramme illustrant l’accès conditionnel autorisant l’accès après correction de la menace](../media/config-mgr-network-wifi-unblocked.png)
### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Contrôler l’accès à SharePoint Online en fonction de la menace pour le réseau :

Détectez les menaces pour votre réseau, telles que les attaques de l’intercepteur, et empêchez la synchronisation des fichiers d’entreprise en fonction du risque évalué pour l’appareil.

**Accès à SharePoint Online bloqué en raison de la menace pour le réseau détectée sur l’appareil :**

![Diagramme illustrant l’accès conditionnel interdisant l’accès de l’appareil à SharePoint Online après détection de la menace](../media/config-mgr-network-spo-blocked.png)


**Accès accordé après correction :**

![Diagramme illustrant l’accès conditionnel autorisant l’accès après correction de la menace pour le réseau](../media/config-mgr-network-spo-unblocked.png)

## <a name="next-steps"></a>Étapes suivantes
Voici les principales étapes à effectuer pour implémenter cette solution :
1.  [Configurer votre abonnement avec Lookout Mobile Threat Protection](set-up-your-subscription-with-lookout.md)
2.  [Activer la connexion à Lookout MTP dans Intune](enable-lookout-connection-in-intune.md)
3.  [Configurer et déployer l’application Lookout for Work](configure-and-deploy-lookout-for-work-apps.md)
4.  [Configurer une stratégie de conformité](enable-device-threat-protection-rule-compliance-policy.md)
5.  [Résoudre les problèmes liés à l’intégration de Lookout](troubleshoot-lookout-integration.md)



<!--HONumber=Dec16_HO3-->


