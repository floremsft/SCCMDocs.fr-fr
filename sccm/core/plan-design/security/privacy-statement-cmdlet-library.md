---
title: "Déclaration de confidentialité de System Center Configuration Manager – Bibliothèque d’applets de commande de Configuration Manager"
description: "Découvrez comment Microsoft collecte et utilise les données relatives à la bibliothèque d’applets de commande System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 88d11aaed4a0e6575cb859f5dfc3ac425bd2bf38


---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>Déclaration de confidentialité de System Center Configuration Manager – Bibliothèque d’applets de commande de Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette déclaration de confidentialité couvre les fonctionnalités de la bibliothèque d’applets de commande de System Center Configuration Manager.  

## <a name="usage-data"></a>Données d’utilisation  
 **Ce que permet cette fonctionnalité :**   
La bibliothèque d’applets de commande de System Center Configuration Manager vous permet de gérer une hiérarchie Configuration Manager à l’aide d’applets de commande et de scripts Windows PowerShell. La bibliothèque d’applets de commande collecte des informations sur l’utilisation des applets de commande de la bibliothèque afin d’identifier des tendances et des modèles d’utilisation.  La bibliothèque d’applets de commande collecte également les types et le nombre d’erreurs que vous rencontrez lors de l’utilisation des applets de commande.  

 **Informations collectées, traitées ou transmises :**   
Les données d’utilisation collectées comprennent le démarrage, l’arrêt et l’interruption des applets de commande, l’exécution d’applets de commande déconseillées et des mesures d’activité pour les opérations du fournisseur SMS en relation avec les applets de commande. Ces informations ne permettent pas de vous identifier personnellement.  Les informations collectées sur les erreurs comprennent les erreurs retournées par les applets de commande et le détail des erreurs d’exception. Certains rapports détaillés sur les erreurs peuvent contenir par inadvertance des identificateurs individuels, par exemple, le numéro de série d’un appareil connecté à votre ordinateur. La bibliothèque d’applets de commande filtre et rend anonymes les informations contenues dans les rapports d’erreur pour supprimer tous les identificateurs individuels avant leur transmission à Microsoft.  

 **Utilisation des informations :**   
Nous utilisons ces informations pour améliorer la qualité, la sécurité et l’intégrité des produits et services que nous proposons.  

 **Choix/contrôle :**   
Cette fonctionnalité Données d’utilisation est activée par défaut. La bibliothèque d’applets de commande de System Center Configuration Manager inclut deux clés de Registre pour contrôler cette fonctionnalité.  

 Pour la désactiver complètement, vous devez définir les deux valeurs de clé de Registre suivantes, une pour chacun des fournisseurs de suivi d’événements pour Windows (ETW) :  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (désactive la fonctionnalité Données d’utilisation pour le fournisseur du lecteur)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (désactive la fonctionnalité Données d’utilisation pour les applets de commande)  

 Les modifications des paramètres de données d’utilisation sont spécifiques de l’ordinateur sur lequel elles ont été effectuées.  

 Pour plus d’informations sur la configuration des données d’utilisation (collecte), consultez la [Documentation de la bibliothèque d’applets de commande de System Center Configuration Manager](https://technet.microsoft.com/en-us/library/dn958404.aspx).  

## <a name="update-check"></a>Vérification de mise à jour  
 **Ce que permet cette fonctionnalité :**   
La bibliothèque d’applets de commande de System Center Configuration Manager vérifie automatiquement chaque jour si des mises à jour de la bibliothèque sont disponibles, et vous indique de télécharger la bibliothèque mise à jour.  

 **Informations collectées, traitées ou transmises :**   
La vérification de mise à jour de la bibliothèque d’applets de commande télécharge un petit fichier texte à partir du Centre de téléchargement Microsoft pour vérifier la version.   Ce fichier n’est pas stocké localement.  La bibliothèque d’applets de commande ne met pas automatiquement à niveau le logiciel.  

 **Utilisation des informations :**   
Nous utilisons ces informations pour améliorer la qualité, la sécurité et l’intégrité des produits et services que nous proposons.  

 **Choix/contrôle :**   
La vérification de mise à jour est activée par défaut.  La bibliothèque d’applets de commande de System Center Configuration Manager inclut les applets de commande suivantes pour contrôler la fonctionnalité de notification de mise à jour :  

-   `Get-CMCmdletUpdateCheck` obtient la configuration de la fonctionnalité de mise à jour et indique si la stratégie de l’utilisateur est remplacée par la stratégie système.  

-   `Send-CMCmdletUpdateCheck` vous permet d’effectuer une vérification de mise à jour non planifiée. Une vérification non planifiée ne tient pas compte des paramètres de stratégie.  

-   `Set-CMCmdletUpdateCheck` configure les paramètres de vérification de mise à jour selon l’utilisateur ou le système. Vous devez avoir ouvert une session en tant qu’administrateur pour définir les paramètres système.  

 Pour plus d’informations sur la configuration de la vérification de mise à jour, consultez la [Documentation de la bibliothèque d’applets de commande de System Center Configuration Manager](https://technet.microsoft.com/en-us/library/dn958404.aspx).  



<!--HONumber=Nov16_HO1-->


