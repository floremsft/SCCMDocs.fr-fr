---
title: "Créer des applications Windows | System Center Configuration Manager"
description: "Examinez les éléments à prendre en compte quand vous créez et déployez des applications pour appareils Windows."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f776e624c7fff5f52b573e5066a6e7d20396ce91

---
# <a name="create-windows-applications-with-system-center-configuration-manager"></a>Créer des applications Windows avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

En plus des autres exigences et procédures System Center Configuration Manager à observer pour créer une application, vous devez aussi prendre en compte les éléments suivants au moment de créer et déployer des applications pour des appareils Windows.  

## <a name="general-considerations"></a>Éléments généraux à prendre en compte  
 Configuration Manager prend en charge le déploiement des types d’applications suivants :  

|Type d'appareil|Fichiers pris en charge|  
|-----------------|---------------------|  
|Windows RT et Windows RT 8.1|*.appx, \*.appxbundle|  
|Windows 8.1 et versions ultérieures inscrit en tant qu’appareil mobile|*.appx, \*.appxbundle|  

 Les actions de déploiement suivantes sont prises en charge :  

|Type d'appareil|Actions prises en charge|  
|-----------------|-----------------------|  
|Windows 8.1 et versions ultérieures|Disponible, Obligatoire. Désinstaller|  
|Windows RT|Disponible, Obligatoire, Désinstaller|  

## <a name="support-for-universal-windows-platform-uwp-apps"></a>Prise en charge des applications de plateforme Windows universelle (UWP)  
 Les appareils Windows 10 n’ont pas besoin d’une clé de sideloading pour installer des applications métier. Cependant, la clé de Registre **HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps** doit avoir la valeur 1 pour activer le sideloading.  

 Si cette clé de Registre n’est pas configurée, Configuration Manager lui attribue automatiquement la valeur **1** la première fois que vous déployez une application sur l’appareil. Si vous avez défini la valeur **0**, Configuration Manager ne peut pas modifier automatiquement la valeur et le déploiement d’applications métier échoue.  

 Les applications métier de plateforme Windows universelle doivent être signées avec un certificat de code de signature approuvé sur chaque appareil sur lequel l’application est déployée. Vous pouvez utiliser des certificats issus d’une infrastructure PKI interne ou un certificat issu d’un certificat racine public tiers installé sur l’appareil.  

 Sur les appareils Windows 10 Mobile, vous pouvez utiliser un certificat de code de signature non Symantec pour signer les applications **.appx** universelles. Pour les applications **.xap** , mais aussi les packages **.appx** générés pour Windows Phone 8.1 que vous voulez installer sur des appareils Windows 10 Mobile, vous devez utiliser un certificat de code de signature Symantec.  

## <a name="deploy-windows-installer-apps-to-enrolled-windows-10-pcs"></a>Déployer des applications Windows Installer sur des PC Windows 10 inscrits  
 Le type de programme d’installation **Windows Installer via MDM (\*.msi)** vous permet de créer et déployer des applications Windows Installer sur des PC inscrits qui exécutent Windows 10.  

 Tenez compte des points suivants quand vous utilisez ce type de programme d’installation :  

-   Vous ne pouvez charger qu’un seul fichier avec l’extension .msi.  

-   Le code de produit et la version de produit du fichier sont utilisés pour la détection d’applications.  

-   Le comportement de redémarrage par défaut de l’application sera utilisé. Configuration Manager ne contrôle pas cette fonctionnalité.  

-   Les packages MSI par utilisateur sont installés pour un utilisateur unique.  

-   Les packages MSI par ordinateur sont installés pour tous les utilisateurs sur l’appareil.  

-   Les mises à jour d’application sont prises en charge quand les codes de produit MSI de toutes les versions sont identiques.  



<!--HONumber=Nov16_HO1-->


