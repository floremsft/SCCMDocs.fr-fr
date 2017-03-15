---
title: "Attestation d’intégrité | Microsoft Docs"
description: "Découvrez les fonctionnalités d’attestation d’intégrité de l’appareil disponibles dans la console Configuration Manager."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
caps.latest.revision: 17
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: cb42b6f324dc0019c2109be4d91e0eab4dca4d70
ms.openlocfilehash: 9d88e93c1382d5804598f2db258f325954e328b1
ms.lasthandoff: 03/08/2017


---
# <a name="health-attestation-for-system-center-configuration-manager"></a>Attestation d’intégrité pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les administrateurs peuvent consulter l’état de l’[attestation d’intégrité des appareils Windows 10](https://technet.microsoft.com/library/mt592023.aspx) dans la console Configuration Manager.  Cette fonctionnalité est disponible pour les PC et les ressources locales gérés par Configuration Manager et les appareils mobiles gérés avec Microsoft Intune. Les administrateurs peuvent spécifier si le signalement s’effectue par le biais du cloud ou de l’infrastructure locale. Les PC clients sans accès à Internet peuvent ainsi activer et surveiller des appareils à l’aide de l’attestation d’intégrité. L’attestation de l’intégrité des appareils permet à l’administrateur de s’assurer que les configurations dignes de confiance suivantes de BIOS, de module de plateforme sécurisée (TPM) et de logiciel de démarrage sont activées sur les ordinateurs clients :  

-   Logiciel anti-programme malveillant à lancement anticipé - Un logiciel anti-programme malveillant à lancement anticipé (ELAM) protège votre ordinateur au démarrage et avant l’initialisation de pilotes tiers. [Comment activer le logiciel anti-programme malveillant à lancement anticipé (ELAM)](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker - Le chiffrement de lecteur BitLocker Windows est un logiciel qui vous permet de chiffrer toutes les données stockées sur le volume hébergeant le système d’exploitation Windows.  [Comment activer Bitlocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Démarrage sécurisé - Le démarrage sécurisé est une norme de sécurité développée par des membres du secteur de la fabrication de PC pour s’assurer que votre ordinateur démarre en utilisant uniquement des logiciels approuvés par le fabricant de l’ordinateur. [En savoir plus sur le démarrage sécurisé](https://technet.microsoft.com/library/hh824987.aspx)  
-   Intégrité du code - L’intégrité du code est une fonctionnalité qui améliore la sécurité du système d’exploitation en validant l’intégrité d’un fichier de pilote ou système chaque fois qu’il est chargé en mémoire. [En savoir plus sur l’intégrité du code](https://technet.microsoft.com/library/dd348642.aspx)  


##  <a name="device-health-attestation"></a>Attestation de l’intégrité des appareils  
 L’attestation d’intégrité des appareils Configuration Manager affiche les informations suivantes :  

-   **État d’attestation d’intégrité** : indique la répartition des appareils en état conforme, non conforme, d’erreur ou inconnu.  
-   **Appareils signalant une attestation d’intégrité** : indique le pourcentage d’appareils signalant l’état d’attestation d’intégrité.  
-   **Appareils non conformes par type de client** : indique la répartition des appareils mobiles et ordinateurs non conformes.  
-   **Principaux paramètres manquants de l’attestation d’intégrité** : indique le nombre d’appareils auxquels un paramètre d’attestation d’intégrité manque, répertoriés par paramètre manquant.  

 **Configuration requise :**  

-   Appareils clients exécutant Windows&10;  
-   Windows Server 2016 avec [attestation d’intégrité de l’appareil activée](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation)
-    2 modules de plateforme sécurisée (TPM) activés  
-   Débloquer la communication entre l’agent du client Configuration Manager et le service d’attestation d’intégrité has.spserv.microsoft.com (port 443)

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Comment activer la communication avec le service d’attestation d’intégrité sur des ordinateurs clients Configuration Manager  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Vue d’ensemble** > **Paramètres client**.  Sélectionnez l’onglet des paramètres de l’ **Agent ordinateur** .  

2.  Dans la boîte de dialogue **Paramètres par défaut** , sélectionnez **Agent ordinateur** , puis accédez à **Activer la communication avec le service d’attestation d’intégrité**.  

3.  Affectez la valeur **Oui** à **Activer la communication avec le service d’attestation d’intégrité**, puis cliquez sur **OK**.  

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Comment activer la communication avec le service d’attestation d’intégrité local sur des ordinateurs clients Configuration Manager


1. Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Paramètres client**, puis affectez la valeur **Oui** à **Utiliser le service d’attestation d’intégrité local**.


2. Spécifiez l’ **URL du service d’attestation d’intégrité local**, puis cliquez sur **OK**.

## <a name="how-to-view-health-attestation"></a>Comment afficher l’attestation d’intégrité  


1.  Pour afficher l’attestation d’intégrité de l’appareil, dans la console Configuration Manager, accédez à l’espace de travail **Surveillance** , cliquez sur le nœud **Sécurité** , puis sur **Attestation d’intégrité**.  

2.  L’attestation d’intégrité de l’appareil s’affiche.  

 L’état de l’attestation d’intégrité de l’appareil client permet de définir des règles d’accès conditionnel dans des stratégies de conformité pour les appareils gérés par Configuration Manager avec Microsoft Intune. Pour plus d’informations, consultez [Gérer les stratégies de conformité d’appareils dans System Center Configuration Manager](/sccm/protect/deploy-use/device-compliance-policies).  

