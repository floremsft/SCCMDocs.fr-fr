---
title: Basculer les charges de travail de Configuration Manager sur Intune
description: "Découvrez comment basculer les charges de travail actuellement gérées par Configuration Manager vers Microsoft Intune."
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: 
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 60aff996ec598cff7572a0e88c631dc9c509e007
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>Basculer les charges de travail de Configuration Manager sur Intune
Dans [Préparer les appareils Windows 10 pour la cogestion](co-management-prepare.md), vous avez préparé les appareils Windows 10 à la cogestion. Ces appareils sont désormais joints à AD et à Azure AD, ils sont inscrits dans Intune et ont le client Configuration Manager. Vous avez probablement encore des appareils Windows 10 joints à AD et qui ont le client Configuration Manager, mais qui ne sont pas joints à Azure AD ni inscrits à Intune. La procédure suivante présente les étapes permettant d’activer la cogestion et de préparer le reste de vos appareils Windows 10 (les clients Configuration Manager sans inscription à Intune) pour la cogestion ; elle vous sert également à lancer le basculement de charges de travail spécifiques de Configuration Manager vers Intune.

1. Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Services cloud** > **Cogestion**.    
2. Sous l’onglet Accueil, dans le groupe Gérer, choisissez  **Configurer la cogestion** pour ouvrir l’Assistant Configuration de la cogestion.    
3. Dans la page Abonnement, cliquez sur **Se connecter** et connectez-vous à votre locataire Intune, puis cliquez sur **Suivant**.   
4. Dans la page Activation, choisissez **Pilote** ou **Tout** pour activer l’inscription automatique dans Intune, puis cliquez sur **Suivant**. Lorsque vous choisissez **Pilote**, seuls les clients Configuration Manager membres du groupe pilote sont automatiquement inscrits à Intune. Cela vous permet d’activer la cogestion sur une partie des clients pour tester initialement la cogestion et la déployer au moyen d’une approche progressive. Vous pouvez utiliser la ligne de commande pour déployer le client Configuration Manager en tant qu’application dans Intune pour les appareils déjà inscrits à Intune. Pour plus d’informations, consultez [Appareils Windows 10 inscrits à Intune](co-management-prepare.md#windows-10-devices-enrolled-in-intune).
5. Dans la page Charges de travail, choisissez de basculer ou non les charges de travail Configuration Manager devant être gérées par Intune pilote ou Intune, puis cliquez sur **Suivant**. Le paramètre **Intune pilote** bascule la charge de travail associée uniquement pour les appareils inclus dans le groupe pilote. Le paramètre **Intune** bascule la charge de travail associée pour tous les appareils Windows 10 cogérés. 
        
   > [!Important]    
   > Avant de basculer toutes les charges de travail, vérifiez que la charge de travail correspondante dans Intune a été correctement configurée et déployée. Ainsi, vous garantissez que les charges de travail sont toujours gérées par un des outils de gestion de vos appareils.   
1. Dans la page Préparation, configurez les paramètres suivants et cliquez sur **Suivant** :
    - **Pilote** : le groupe pilote contient un ou plusieurs regroupements que vous sélectionnez. Utilisez ce groupe dans le cadre de votre déploiement progressif de la cogestion. Vous pouvez commencer par un regroupement test peu volumineux, puis ajouter d’autres regroupements à ce groupe pilote au fur et à mesure que vous déployez la cogestion pour d’autres utilisateurs et appareils. À tout moment, vous pouvez modifier les regroupements dans le groupe pilote à partir des propriétés de cogestion.
    - **Production** : configurez le **groupe d’exclusions** avec un ou plusieurs regroupements. Les appareils membres d’une des collections de ce groupe sont exclus de l’utilisation de la cogestion. 
2. Pour activer la cogestion, terminez l’Assistant.  

## <a name="modify-your-co-management-settings"></a>Modifier les paramètres de cogestion
Après avoir activé la cogestion à l’aide de l’Assistant, vous pouvez modifier les paramètres dans les propriétés de cogestion.  
- Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Services cloud** > **Cogestion**.  
Sélectionnez l’objet de cogestion, cliquez sur l’onglet Accueil, puis sur **Propriétés**. 

## <a name="monitor-co-management"></a>Surveiller la cogestion
Après avoir activé la cogestion, vous pouvez surveiller les appareils de cogestion à l’aide des méthodes suivantes :
- **Vue SQL et classe WMI** : vous pouvez interroger la vue SQL **v&#95;ClientCoManagementState** dans la base de données du site Configuration Manager ou la classe WMI **SMS&#95;Client&#95;ComanagementState**. Avec les informations contenues dans la classe WMI, vous pouvez créer des regroupements personnalisés dans Configuration Manager pour vous aider à déterminer l’état du déploiement de la cogestion. Pour plus d’informations, consultez [Guide pratique pour créer des regroupements](/sccm/core/clients/manage/collections/create-collections). Les champs suivants sont disponibles dans la vue SQL et la classe WMI : 
    - **MachineID** : spécifie un ID d’appareil unique pour le client Configuration Manager.
    - **MDMEnrolled** : spécifie si l’appareil est inscrit à la gestion des appareils mobiles. 
    - **Authority** : spécifie l’autorité pour laquelle l’appareil est inscrit.
    - **ComgmtPolicyPresent** : spécifie si la stratégie de cogestion Configuration Manager existe sur le client. Si la valeur **MDMEnrolled** est **0**, l’appareil n’est pas cogéré, que la stratégie de cogestion existe sur le client ou non.

   > [!Note]    
   > Un appareil est cogéré quand les champs **MDMEnrolled** et **ComgmtPolicyPresent** ont tous les deux la valeur **1**.

- **Stratégies de déploiement** : il existe deux stratégies créées dans **Surveillance** > **Déploiements** ; une stratégie pour le groupe pilote et une stratégie pour la production. Ces stratégies signalent uniquement le nombre d’appareils auxquels Configuration Manager a appliqué la stratégie. Elles ne considèrent pas le nombre d’appareils inscrits dans Intune, ce qui est obligatoire pour pouvoir cogérer des appareils.  

## <a name="check-compliance-for-co-managed-devices"></a>Vérifier la conformité des appareils cogérés
Les utilisateurs peuvent utiliser le Centre logiciel pour vérifier la conformité de leurs appareils Windows 10 cogérés, que l’accès conditionnel soit géré par Configuration Manager ou par Intune. Ils peuvent également vérifier la conformité à l’aide de l’application Portail d’entreprise quand l’accès conditionnel est géré par Intune.

## <a name="next-steps"></a>Étapes suivantes
Utilisez les ressources suivantes pour vous aider à gérer les charges de travail que vous basculez vers Intune :
- [Stratégies de conformité des appareils](https://docs.microsoft.com/intune/device-compliance-get-started)
- [Stratégies d’accès aux ressources](https://docs.microsoft.com/intune/device-profiles)
- [Stratégies Windows Update pour Entreprise](https://docs.microsoft.com/intune/windows-update-for-business-configure)
