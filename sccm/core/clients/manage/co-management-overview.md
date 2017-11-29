---
title: "Cogestion pour les appareils Windows 10"
description: "Découvrez comment gérer simultanément des appareils Windows 10 à l’aide de Configuration Manager et Microsoft Intune."
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: 
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: c0a577c6076630f0615f953091f35c4f3c2d0a7d
ms.sourcegitcommit: 536f7295e9ea361f1f9ead6c25f3685deb041ad8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="co-management-for-windows-10-devices"></a>Cogestion pour les appareils Windows 10    
<!-- 1350871 -->
Nombreux sont les clients qui souhaitent gérer les appareils Windows 10 comme les appareils mobiles, en recourant à une solution cloud plus simple et moins chère. Toutefois, le passage de la gestion classique à la gestion moderne peut s’avérer difficile. Dans Windows 10 version 1709 (également appelée Fall Creators Update) et ultérieure, vous pouvez joindre un appareil Windows 10 à Active Directory (AD) en local et à Azure AD sur le cloud (Azure AD hybride). À compter de Configuration Manager version 1710, la cogestion tire parti de cette amélioration et vous permet de gérer simultanément plusieurs appareils Windows 10 à l’aide de Configuration Manager et d’Intune. C’est une solution qui établit une passerelle entre la gestion classique et la gestion moderne tout en vous donnant la possibilité d’opérer cette transition selon une approche en plusieurs phases. 

Il existe deux principaux parcours pour accéder à la cogestion.  Le premier a trait à la cogestion provisionnée par Configuration Manager où les appareils Windows 10 gérés conjointement par Configuration Manager et Azure AD hybride sont inscrits dans Intune. Le second fait intervenir les appareils provisionnés par Intune qui sont inscrits dans Intune, puis installés avec le client Configuration Manager pour atteindre l’état de cogestion.  

## <a name="prerequisites"></a>Conditions préalables
Les prérequis suivants doivent être mis en place avant de pouvoir activer la cogestion. Il existe des prérequis généraux et des prérequis distincts pour les appareils dotés du client Configuration Manager et les appareils sur lesquels le client n’est pas installé.

### <a name="general-prerequisites"></a>Conditions préalables
Les prérequis généraux pour activer la cogestion sont les suivants :  

- Configuration Manager version 1710 ou ultérieure
- Azure AD
- Licence EMS ou Intune pour tous les utilisateurs
- [Inscription automatique auprès d’Azure AD](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) activée
- Abonnement Intune &#40;autorité MDM dans Intune définie sur **Intune**&#41;


   > [!Note]  
   > Si vous avez un environnement MDM hybride (Intune intégré à Configuration Manager), vous ne pouvez pas activer la cogestion. Si la migration vers la version autonome d’Intune vous intéresse, consultez [Démarrer la migration de MDM hybride vers la version autonome d’Intune](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).

### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Prérequis supplémentaires pour les appareils dotés du client Configuration Manager
- Windows  10, version 1709 (également appelée Fall Creators Update) et ultérieure
- [Jonction à Azure AD hybride](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (jonction à AD et à Azure AD)

### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Prérequis supplémentaires pour les appareils non dotés du client Configuration Manager
- Windows  10, version 1709 (également appelée Fall Creators Update) et ultérieure
- [Passerelle de gestion cloud](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) dans Configuration Manager (lorsque vous utilisez Intune pour installer le client Configuration Manager)

## <a name="workloads-you-can-switch-to-intune"></a>Charges de travail que vous pouvez basculer sur Intune
Après l’activation de la cogestion, Configuration Manager continue de gérer toutes les charges de travail. Lorsque vous pensez être prêt, vous pouvez laisser Intune gérer les charges de travail disponibles. Intune peut assurer la gestion des charges de travail suivantes.   

### <a name="compliance-policies"></a>Stratégies de conformité
Les stratégies de conformité définissent les règles et les paramètres auxquels doit se conformer un appareil pour être considéré conforme par les stratégies d’accès conditionnel. Vous pouvez également utiliser des stratégies de conformité pour surveiller et corriger les problèmes de conformité avec les appareils indépendamment de l'accès conditionnel. Pour plus d’informations, consultez [Stratégies de conformité des appareils](/sccm/mdm/deploy-use/device-compliance-policies).  

### <a name="windows-update-for-business-policies"></a>Stratégies Windows Update pour Entreprise
Les stratégies Windows Update pour Entreprise vous permettent de configurer des stratégies de report pour les mises à jour de fonctionnalités Windows 10 ou les mises à jour qualité pour les appareils Windows 10 gérés directement par Windows Update pour Entreprise. Pour plus d’informations, consultez [Configurer les stratégies de report Windows Update pour Entreprise](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="resource-access-policies"></a>Stratégies d’accès aux ressources
Les stratégies d’accès aux ressources configurent les paramètres VPN, Wi-Fi, d’e-mail et de certificat sur les appareils. Pour plus d’informations, consultez [Déployer des profils d’accès aux ressources](/sccm/protect/deploy-use/deploy-wifi-vpn-email-cert-profiles).

## <a name="architectural-overview-for-co-management"></a>Présentation de l’architecture de cogestion
Le schéma suivant montre une vue d’ensemble de l’architecture de la cogestion et son intégration aux infrastructures de Configuration Manager et d’Intune existantes.

![Schéma de l’architecture de la cogestion](./media/co-management-arch.svg)

## <a name="scenarios-to-enable-co-management"></a>Scénarios pour activer la cogestion  
Vous pouvez activer la cogestion pour les appareils Windows 10 inscrits dans Microsoft Intune et pour les clients Configuration Manager Windows 10 existants. Ces deux scénarios mènent à la gestion simultanée des appareils Windows 10 par Configuration Manager et par Intune, ainsi qu’à leur jonction à AD et à Azure AD.  

### <a name="devices-enrolled-in-intune"></a>Appareils inscrits dans Intune  
Lorsque des appareils Windows 10 sont inscrits à Intune, vous pouvez y installer le client Configuration Manager (à l’aide d’un argument de ligne de commande spécifique) pour préparer les clients à la cogestion. Ensuite, activez la cogestion à partir de la console Configuration Manager et commencez le déplacement de charges de travail spécifiques vers Intune pour des appareils Windows 10 spécifiques.  

Quant aux appareils Windows 10 qui ne sont pas encore inscrits à Intune, vous pouvez utiliser l’inscription automatique dans Azure pour les inscrire. Pour ce qui est des nouveaux appareils Windows 10, vous pouvez utiliser [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) et configurer l’expérience OOBE (Out of Box Experience) qui inclut l’inscription automatique permettant d’inscrire les appareils à Intune.  

### <a name="configuration-manager-clients"></a>Clients Configuration Manager
Lorsque vous avez des appareils Windows 10 qui sont des clients Configuration Manager, vous pouvez les inscrire et activer la cogestion depuis la console Configuration Manager. Configuration Manager déclenche l’inscription automatique dans Intune en fonction des informations de locataire Azure AD.  


## <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Actions à distance disponibles dans Intune sur Azure pour les appareils gérés conjointement
Quand un appareil Windows 10 est activé pour la cogestion, les actions à distance suivantes sont disponibles sur Azure à partir d’Intune :  
- [Réinitialisation aux paramètres d’usine](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
- [Réinitialisation sélective](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Suppression d’appareils](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Redémarrage d’un appareil](https://docs.microsoft.com/intune/device-restart)
- [Nouvelle version](https://docs.microsoft.com/intune/device-fresh-start)

## <a name="next-steps"></a>Étapes suivantes
[Préparer les appareils Windows 10 pour la cogestion](co-management-prepare.md)