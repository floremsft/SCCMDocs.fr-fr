---
title: Endpoint Protection | Microsoft Docs
description: "Apprenez à gérer les stratégies de logiciel anti-programme malveillant et la sécurité du Pare-feu Windows pour les ordinateurs clients de votre hiérarchie Configuration Manager."
ms.custom: na
ms.date: 02/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
caps.latest.revision: 11
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: ae60eb25383f4bd07faaa1265185a471ee79b1e9
ms.openlocfilehash: 3c31271f3e3ae7aa45da03b3d75fd78242330646
ms.contentlocale: fr-fr
ms.lasthandoff: 05/17/2017


---
# <a name="endpoint-protection"></a>Endpoint Protection

*S’applique à : System Center Configuration Manager (Current Branch)*

Endpoint Protection dans System Center Configuration Manager vous permet de gérer les stratégies de logiciel anti-programme malveillant et la sécurité du Pare-feu Windows pour les ordinateurs clients de votre hiérarchie Configuration Manager.  

> [!IMPORTANT]  
>  Vous devez détenir une licence pour pouvoir utiliser Endpoint Protection pour gérer les clients dans votre hiérarchie Configuration Manager.  

 L’utilisation d’Endpoint Protection avec Configuration Manager présente les avantages suivants :  

-   Configuration des stratégies de logiciel anti-programme malveillant, des paramètres du Pare-feu Windows et gestion du service Protection avancée contre les menaces Windows Defender sur certains groupes d’ordinateurs  
-   Utilisation des mises à jour logicielles Configuration Manager pour télécharger les derniers fichiers de définitions de logiciel anti-programme malveillant pour tenir à jour les ordinateurs clients  
-   Envoi de notifications par courrier électronique, utilisation de la surveillance dans la console et affichage de rapports pour informer les utilisateurs administratifs qu’un logiciel malveillant a été détecté sur des ordinateurs clients  

Windows Defender est déjà installé sur les ordinateurs Windows 10 et Windows Server 2016. Pour ces systèmes d’exploitation, un client de gestion pour Windows Defender est installé lorsque le client Configuration Manager est installé. Sur les ordinateurs Windows 8.1 et antérieurs, le client Endpoint Protection est installé avec le client Configuration Manager. Windows Defender et le client Endpoint Protection offrent les possibilités suivantes :  

-   Détection des logiciels malveillants et des logiciels espions et mesures correctives  
-   Détection des rootkits et mesures correctives  
-   Évaluation des vulnérabilités critiques et mises à jour automatiques des définitions et du moteur  
-   Détection des vulnérabilités réseau via le système NIS (Network Inspection System)  
-   Intégration à Cloud Protection Service pour signaler les logiciels malveillants à Microsoft. Quand vous rejoignez ces services, le client Endpoint Protection ou Windows Defender peut télécharger les dernières définitions à partir du Centre de protection contre les programmes malveillants lorsqu’un logiciel malveillant non identifié est détecté sur un ordinateur.  

> [!NOTE]  
>  Le client Endpoint Protection peut être installé sur un serveur qui exécute Hyper-V et sur les machines virtuelles invitées dotées d’un système d’exploitation pris en charge. Pour éviter une utilisation excessive du processeur, les actions Endpoint Protection ont un délai randomisé intégré qui empêche les services de protection de s’exécuter simultanément.  

 De plus, Endpoint Protection dans Configuration Manager vous permet de gérer les paramètres du Pare-feu Windows dans la console Configuration Manager.  

 [Exemple de scénario : utilisation de System Center Endpoint Protection pour protéger des ordinateurs contre les programmes malveillants dans System Center Configuration Manager](scenarios-endpoint-protection.md) Endpoint Protection et le Pare-feu Windows.  


## <a name="managing-malware-with-endpoint-protection"></a>Gestion des logiciels malveillants avec Endpoint Protection  
 Endpoint Protection dans Configuration Manager vous permet de créer des stratégies de logiciel anti-programme malveillant qui contiennent des paramètres pour les configurations de client Endpoint Protection. Vous pouvez ensuite déployer ces stratégies sur les ordinateurs clients et les surveiller dans le nœud **État Endpoint Protection** sous **Sécurité** dans l’espace de travail **Surveillance** ou à l’aide des rapports Configuration Manager.  

 Informations complémentaires :  

-   [Comment créer et déployer des stratégies anti-programme malveillant pour Endpoint Protection dans System Center Configuration Manager](endpoint-antimalware-policies.md) : créez, déployer et surveillez des stratégies de logiciel anti-programme malveillant à partir de la liste des paramètres que vous pouvez configurer.  

-   [Comment surveiller Endpoint Protection dans System Center Configuration Manager](monitor-endpoint-protection.md) : surveillance des rapports d’activité, des ordinateurs clients infectés et bien plus encore.  

-   [Comment gérer les stratégies de logiciel anti-programme malveillant et les paramètres de pare-feu pour Endpoint Protection dans System Center Configuration Manager](endpoint-antimalware-firewall.md) : prenez des mesures correctives contre les programmes malveillants détectés sur les ordinateurs clients.  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Gestion du pare-feu Windows avec Endpoint Protection  
 Endpoint Protection dans Configuration Manager assure une gestion de base du Pare-feu Windows sur les ordinateurs clients. Pour chaque profil de réseau, vous pouvez :  

-   Activer ou désactiver le pare-feu Windows.  

-   Bloquer les connexions entrantes, y compris celles figurant dans la liste des programmes autorisés.  

-   Avertir l'utilisateur lorsque le pare-feu Windows bloque un nouveau programme.  

> [!NOTE]  
>  Endpoint Protection prend en charge la gestion du pare-feu Windows uniquement.  


 Pour plus d’informations sur la création et le déploiement de stratégies de Pare-feu Windows pour Endpoint Protection, consultez [Guide pratique pour créer et déployer des stratégies de Pare-feu Windows pour Endpoint Protection dans System Center Configuration Manager](create-windows-firewall-policies.md).  


## <a name="windows-defender-advanced-threat-protection"></a>Windows Defender Advanced Threat Protection

À compter de la version 1606 de Configuration Manager (Current Branch), Endpoint Protection facilite la gestion et la surveillance du service Windows Defender Advanced Threat Protection (ATP). Ce nouveau service aide les entreprises à détecter, analyser et contrer les attaques avancées ciblant leurs réseaux. Consultez [Protection avancée contre les menaces Windows Defender](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Flux de travail Endpoint Protection  
 Utilisez le diagramme suivant pour comprendre le flux de travail qui permet d’implémenter Endpoint Protection dans votre hiérarchie Configuration Manager.  

 ![Flux de travail Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)  

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Client Endpoint Protection pour les ordinateurs Mac et les serveurs Linux  
 System Center Endpoint Protection comprend un client Endpoint Protection pour Linux et pour les ordinateurs Mac. Ces clients ne sont pas fournis avec Configuration Manager. Vous devez télécharger les produits suivants à partir du [Centre de gestion des licences en volume Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

-   System Center 2012 Endpoint Protection pour Mac  

-   System Center 2012 Endpoint Protection pour Linux  


> [!IMPORTANT]  
>  Vous devez être client d’une licence en volume Microsoft pour télécharger les fichiers d’installation d’Endpoint Protection pour Linux et Mac.  

 Ces produits ne peuvent pas être gérés à partir de la console Configuration Manager. Toutefois, un pack d’administration System Center Operations Manager, fourni avec les fichiers d’installation, vous permet de gérer le client pour Linux à l’aide d’Operations Manager.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Guide pratique pour obtenir le client Endpoint Protection pour les ordinateurs Mac et les serveurs Linux

Procédez comme suit pour télécharger le fichier image contenant le logiciel client Endpoint Protection et la documentation pour les ordinateurs Mac et les serveurs Linux.
1. Connectez-vous au [Centre de gestion des licences en volume Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. Sélectionnez l’onglet **Téléchargements et clés** situé en haut du site web.
3. Filtrez sur le produit **System Center Endpoint Protection (Current Branch)**.
4. Cliquez sur le lien vers **Télécharger**
5. Cliquez sur **Continuer**. Vous devez voir plusieurs fichiers, dont un nommé : **System Center Endpoint Protection (current branch - version 1606) for Linux OS and Macintosh OS Multilanguage   32/64 bit   1507 MB ISO**.
6. Cliquez sur l’icône de flèche pour télécharger le fichier. Le nom de fichier est **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_EptProt_Lin_Mac_MLF_X21-30777.ISO**.

 Pour plus d’informations sur l’installation et la gestion des clients Endpoint Protection sur les ordinateurs Mac et Linux, utilisez la documentation qui accompagne ces produits, disponible dans le dossier **Documentation** .

