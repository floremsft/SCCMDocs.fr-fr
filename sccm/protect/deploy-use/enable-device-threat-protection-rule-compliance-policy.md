---
title: "Activer une règle de protection d’appareil dans une stratégie de conformité | System Center Configuration Manager"
description: "Activez une règle de protection contre les menaces mobiles dans la stratégie de conformité des appareils."
ms.custom: na
ms.date: 12/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 020f43e8-738e-4a82-91be-27b10cda9665
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c13c6268fa76ade7feb0981f9c4a6e325e393aca
ms.openlocfilehash: b4eb4768dadba7e5a635d90a87d669cc4b3869f4


---
# <a name="enable-device-threat-protection-rule-in-the-compliance-policy"></a>Activer une règle de protection contre les menaces des appareils dans la stratégie de conformité

*S’applique à : System Center Configuration Manager (Current Branch)*

Intune avec Mobile Threat Protection de Lookout vous donne la possibilité de détecter les menaces mobiles et d’évaluer les risques sur l’appareil. Vous pouvez créer une règle de stratégie de conformité dans Configuration Manager pour inclure l’évaluation des risques permettant de déterminer si l’appareil est conforme. Vous pouvez ensuite utiliser la stratégie d’accès conditionnel pour autoriser ou bloquer l’accès à Exchange, SharePoint et d’autres services, en fonction de la compatibilité des appareils.

Pour que Mobile Threat Protection de Lookout influence la stratégie de conformité de l’appareil :

* La règle **Protection contre les menaces sur les appareils** doit être activée sur la stratégie de conformité.

* La page **État de Lookout** dans la **console Administrateur Intune** doit apparaître comme étant **Active**. Pour plus d’informations et des instructions sur la façon d’activer l’intégration de Lookout, consultez la rubrique [Activer la connexion de Lookout dans Intune](enable-lookout-connection-in-intune.md).


Avant de créer la règle de protection contre les menaces sur les appareils dans la stratégie de conformité, nous vous recommandons de [configurer votre abonnement avec Mobile Threat Protection de Lookout](set-up-your-subscription-with-lookout.md), [d’activer la connexion de Lookout dans Intune](enable-lookout-connection-in-intune.md) et de [configurer l’application Lookout for Work](configure-and-deploy-lookout-for-work-apps.md). La règle de compatibilité est appliquée seulement une fois que le programme d’installation est terminé.

Pour activer la règle de protection contre les menaces sur les appareils, vous pouvez utiliser une stratégie de conformité existante ou en créer une.

Dans le cadre de l’installation de Mobile Threat Protection de Lookout, dans la [console Lookout](https://aad.lookout.com), vous avez créé une stratégie qui classifie les différentes menaces selon trois niveaux : Élevé, Moyen et Faible. Dans la stratégie de conformité Intune, vous utilisez le niveau de menace pour définir le niveau de menace maximal autorisé.

Dans la page **Règles** de l’Assistant Stratégie de conformité, définissez une nouvelle règle avec les informations suivantes :
  * Condition : niveau de risque maximal de protection contre les menaces sur les appareils.
  * Valeur : la valeur peut être une des suivantes :
    * **Aucun (sécurisé)** : il s’agit de l’option la plus sécurisée. Cela signifie que l’appareil ne peut avoir aucune menace. Si un quelconque niveau de menace est détecté, l’appareil est évalué comme non conforme.
    * **Faible** : l’appareil est considéré comme conforme si seule des menaces de niveau Faible sont présentes. Toute menace d’un niveau supérieur place l’appareil dans un état de non-conformité.
    * **Moyen** : l’appareil est évalué comme conforme si les menaces trouvées sur l’appareil sont de niveau Faible ou Moyen. Si des menaces de niveau Élevé sont détectées, l’appareil est déterminé comme étant non conforme.
    * **Élevé** : cette option est la moins sécurisée. Cette option permet en fait tous les niveaux de menaces. Elle peut être utile si vous utilisez cette solution uniquement pour la génération de rapports.

Si vous créez des stratégies d’accès conditionnel pour Office 365 et d’autres services, l’évaluation de conformité ci-dessus est prise en considération, et l’accès aux ressources d’entreprise par les appareils non conformes est bloqué jusqu’à ce que la menace soit résolue.

L’état de la protection contre les menaces sur les appareils est affiché sur le nœud **Sécurité** dans l’espace de travail **Surveillance**.
Un résumé de l’état avec les différents niveaux de menaces est affiché dans un graphique. Vous pouvez cliquer sur les sections du graphique pour voir plus d’informations, comme le nombre d’appareils signalés comme non conformes par plateforme, et les éventuelles erreurs qui sont signalées.
Vous pouvez également voir l’état des appareils individuels dans l’espace de travail **Ressources et conformité**, sous **Appareils**.  Vous pouvez ajouter les colonnes **État de conformité de l’appareil** et **Niveau de menace pour l’appareil** pour afficher l’état.  Par défaut, ces colonnes ne sont pas affichées.



<!--HONumber=Dec16_HO3-->


