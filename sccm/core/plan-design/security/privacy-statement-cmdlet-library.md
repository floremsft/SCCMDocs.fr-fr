---
title: "Déclaration de confidentialité pour la bibliothèque d’applets de commande de Configuration Manager"
description: "Découvrez comment Microsoft collecte et utilise les données relatives à la bibliothèque d’applets de commande de System Center Configuration Manager."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: "5"
caps.handback.revision: "0"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: c00bbd176dfef83a3e32d8e6747fd902bebb104b
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/01/2017
---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>Déclaration de confidentialité de System Center Configuration Manager – Bibliothèque d’applets de commande de Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette déclaration de confidentialité couvre les fonctionnalités de la bibliothèque d’applets de commande de System Center Configuration Manager.  

## <a name="usage-data"></a>Données d’utilisation  
 **Descriptif de cette fonctionnalité :**   
La bibliothèque d’applets de commande de System Center Configuration Manager vous permet de gérer une hiérarchie Configuration Manager à l’aide d’applets de commande et de scripts Windows PowerShell. La bibliothèque d’applets de commande collecte des informations sur l’utilisation des applets de commande dans la bibliothèque pour identifier des tendances et des modèles d’utilisation. La bibliothèque d’applets de commande collecte également les types et le nombre d’erreurs que vous rencontrez quand vous utilisez les applets de commande.  

 **Informations collectées, traitées ou transmises :**   
Les données d’utilisation collectées comprennent le démarrage, l’arrêt et l’interruption des applets de commande, l’exécution d’applets de commande déconseillées, et des mesures d’activité pour les opérations du fournisseur Systems Management Server (SMS) qui sont liées aux applets de commande. Ces informations ne permettent pas de vous identifier personnellement.  Les informations collectées sur les erreurs comprennent les erreurs que les applets de commande renvoient ainsi que les détails des erreurs d’exception. Certains rapports détaillés sur les erreurs peuvent contenir par inadvertance des identificateurs individuels, comme le numéro de série d’un appareil connecté à votre ordinateur. La bibliothèque d’applets de commande filtre et rend anonymes les informations dans les rapports d’erreur pour supprimer les identificateurs individuels avant leur transmission à Microsoft.  

 **Utilisation des informations :**   
Nous utilisons ces informations pour améliorer la qualité, la sécurité et l’intégrité des produits et services que nous proposons.  

 **Choix/contrôle :**   
Cette fonctionnalité de données d’utilisation est activée par défaut. La bibliothèque d’applets de commande de System Center Configuration Manager a deux clés de Registre qui contrôlent cette fonctionnalité.  

 Pour la désactiver complètement, vous devez définir les deux valeurs de clé de Registre suivantes, une pour chacun des fournisseurs de suivi d’événements pour Windows (ETW) :  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (désactive la fonctionnalité Données d’utilisation pour le fournisseur du lecteur)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (désactive la fonctionnalité Données d’utilisation pour les applets de commande)  

 Les modifications des paramètres de données d’utilisation sont spécifiques de l’ordinateur sur lequel elles ont été effectuées.  

 Pour en savoir plus sur la configuration des données d’utilisation (collecte), consultez la [Documentation de la bibliothèque d’applets de commande de System Center Configuration Manager](https://technet.microsoft.com/en-us/library/dn958404.aspx).   
