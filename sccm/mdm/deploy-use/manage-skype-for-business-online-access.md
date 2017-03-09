---
title: "Gérer l’accès à Skype Entreprise Online | Microsoft Docs"
description: "Apprenez à utiliser la stratégie d’accès conditionnel pour gérer l’accès à Skype Entreprise Online."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71c44250-626e-482c-8794-434c6aeb2fb1
caps.latest.revision: 6
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: c39303c2e1a30ff4d7f27bd617a85516dd4cd15d
ms.lasthandoff: 03/06/2017


---
# <a name="manage-skype-for-business-online-access"></a>Gérer l’accès à Skype Entreprise Online

*S’applique à : System Center Configuration Manager (Current Branch)*


Vous pouvez utiliser une stratégie d’accès conditionnel pour  **Skype Entreprise Online** pour gérer l’accès à Skype Entreprise Online en fonction des conditions que vous spécifiez.  


 Quand un utilisateur ciblé tente d’utiliser Skype Entreprise Online sur son appareil, voici l’évaluation qui se produit :![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>Conditions préalables  

-   Activez l’authentification moderne pour Skype Entreprise Online. Remplissez ce [formulaire de connexion](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) pour vous inscrire au programme d’authentification moderne.  

-   Tous vos utilisateurs finaux doivent utiliser Skype Entreprise Online. Si vous avez un déploiement avec Skype Entreprise Online et Skype Entreprise en local, la stratégie d’accès conditionnel n’est pas appliquée aux utilisateurs finaux.  

-   L’appareil devant accéder à Skype Entreprise Online doit :  

    -   être un appareil Android ou iOS ;  

    -   être inscrit auprès d’Intune ;  

    -   être conforme à toutes les stratégies de conformité Intune déployées.  

 L’état de l’appareil est stocké dans Azure Active Directory, qui accorde ou bloque l’accès aux fichiers en fonction des conditions que vous spécifiez.  
Si une condition n'est pas remplie, l'utilisateur reçoit l'un des messages suivants quand il tente de se connecter :  

-   Si l’appareil n’est pas inscrit auprès d’Intune ou dans Azure Active Directory, l’utilisateur reçoit un message contenant des instructions pour installer l’application Portail d’entreprise et inscrire l’appareil.  

-   Si l’appareil n’est pas conforme, l’utilisateur reçoit un message le dirigeant vers le site web ou l’application Portail d’entreprise, où il peut trouver des informations sur le problème et des solutions pour y remédier.  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>Configurer l’accès conditionnel pour Skype Entreprise Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Étape 1 : configurer les groupes de sécurité Active Directory  
 Avant de commencer, configurez les groupes de sécurité Azure Active Directory pour la stratégie d'accès conditionnel. Vous pouvez configurer ces groupes dans le Centre d’administration Office 365. Ces groupes contiennent les utilisateurs qui seront ciblés par la stratégie ou exemptés de celle-ci. Quand un utilisateur est ciblé par une stratégie, chaque appareil qu'il utilise doit être conforme à cette stratégie pour qu'il puisse accéder aux ressources.  

 Vous pouvez spécifier deux types de groupes à utiliser pour la stratégie de Skype Entreprise :  

-   Groupes ciblés : groupes d’utilisateurs auxquels s’applique la stratégie.  

-   Groupes exemptés : groupes d’utilisateurs exempts de la stratégie (facultatif).  
    Si un utilisateur se trouve dans les deux groupes, il est exempt de la stratégie.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Étape 2 : configurer et déployer une stratégie de conformité  
 Veillez à créer et à déployer une stratégie de conformité sur tous les appareils ciblés par la stratégie Skype Entreprise Online.  

 Pour plus d’informations sur la configuration de la stratégie de conformité, consultez [Gérer des stratégies de conformité d’appareils dans System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!NOTE]  
>  Si vous n’avez pas déployé de stratégie de conformité, mais activez la stratégie Skype Entreprise Online, tous les appareils ciblés sont autorisés à accéder s’ils sont inscrits auprès d’Intune.  

 Quand vous êtes prêt, passez à l’Étape 3.  

### <a name="step-3-configure-the-skype-for-business-online-policy"></a>Étape 3 : configurer la stratégie Skype Entreprise Online  
 Ensuite, configurez la stratégie de manière à restreindre l’accès à Skype Entreprise Online aux seuls périphériques gérés et conformes. Cette stratégie sera stockée dans Azure Active Directory.  

1.  Dans la [Console d’administration Microsoft Intune](https://manage.microsoft.com), cliquez sur **Stratégie** > **Accès conditionnel** > **Stratégie Skype Entreprise Online**.  

     ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2.  Sélectionnez **Activer la stratégie d’accès conditionnel**.  

3.  Sous **Accès à l’application**, vous pouvez choisir d’appliquer la stratégie d’accès conditionnel à :  

    -   iOS  

    -   Android  

4.  Sous **Groupes ciblés**, cliquez sur **Modifier** pour sélectionner les groupes de sécurité Active Directory auxquels la stratégie sera appliquée. Vous avez la possibilité de cibler cette stratégie sur tous les utilisateurs ou uniquement sur un groupe sélectionné d’utilisateurs.  

5.  Sous **Groupes exemptés**, vous pouvez éventuellement cliquez sur **Modifier** pour sélectionner les groupes de sécurité Azure Active Directory exempts de cette stratégie.  

6.  Une fois terminé, cliquez sur **Enregistrer**.  

 Vous avez maintenant configuré l’accès conditionnel pour Skype Entreprise Online. La stratégie d'accès conditionnel prend effet immédiatement. Il est donc inutile de la déployer.  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>analyser la conformité et les stratégies d'accès conditionnel  
 Dans l’espace de travail Groupes, vous pouvez afficher l’état de l’accès conditionnel de vos appareils.  

 Sélectionnez un groupe d’appareils mobiles quelconque puis, sous l’onglet **Appareils** , sélectionnez l’un des **Filtres**suivants :  

-   **Appareils non enregistrés avec AAD** : l’accès à Skype Entreprise Online est bloqué pour ces appareils.  

-   **Appareils non conformes** : l’accès à Skype Entreprise Online est bloqué pour ces appareils.  

-   **Appareils enregistrés avec AAD et conformes** : ces appareils peuvent accéder à Skype Entreprise Online.  

### <a name="see-also"></a>Voir aussi  

 [Gérer des stratégies de conformité d’appareils dans System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)

