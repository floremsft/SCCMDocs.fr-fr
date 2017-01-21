---
title: "Créer des applications Windows | Documents Microsoft"
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
ms.sourcegitcommit: 557888d1f1f899e3198c430bbe5ccdd44178f824
ms.openlocfilehash: 9c80cc42f9ce6775067a89a9f5a63c1bf4a0c7ca

---
# <a name="create-windows-applications-with-system-center-configuration-manager"></a>Créer des applications Windows avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

En plus des autres exigences et procédures System Center Configuration Manager à observer pour créer une application, vous devez aussi prendre en compte les éléments suivants au moment de créer et déployer des applications pour des appareils Windows.  

## <a name="general-considerations"></a>Éléments généraux à prendre en compte  
 Configuration Manager prend en charge le déploiement des types de fichiers d’application suivants :  

|Type d'appareil|Types de fichiers pris en charge|  
|-----------------|---------------------|  
|Windows RT et Windows RT 8.1|*.appx, \*.appxbundle|  
|Windows 8.1 et versions ultérieures inscrit en tant qu’appareil mobile|*.appx, \*.appxbundle|  

 Les actions de déploiement suivantes sont prises en charge :  

|Type d'appareil|Actions prises en charge|  
|-----------------|-----------------------|  
|Windows 8.1 et versions ultérieures|disponible, obligatoire, désinstaller|  
|Windows RT|disponible, obligatoire, désinstaller|  

## <a name="support-for-universal-windows-platform-uwp-apps"></a>Prise en charge des applications de plateforme Windows universelle (UWP)  
 Les appareils Windows 10 n’ont pas besoin d’une clé de chargement indépendant pour installer des applications métier. Pour que le chargement indépendant soit activé, la clé de Registre **HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps** doit avoir la valeur 1.  

 Si cette clé de Registre n’est pas configurée, Configuration Manager lui affecte automatiquement la valeur **1** la première fois que vous déployez une application sur l’appareil. Si vous avez défini cette valeur sur **0**, Configuration Manager ne peut pas changer automatiquement la valeur et le déploiement d’applications métier échoue.  

 Les applications métier de la plateforme Windows universelle doivent être signées avec un certificat de signature de code approuvé sur chaque appareil sur lequel l’application est déployée. Vous pouvez utiliser des certificats issus d’une infrastructure PKI interne ou un certificat issu d’un certificat racine public tiers installé sur l’appareil.  

 Sur les appareils Windows 10 Mobile, vous pouvez utiliser un certificat de code de signature non Symantec pour signer les applications **.appx** universelles. Pour les applications **.xap** , mais aussi les packages **.appx** générés pour Windows Phone 8.1 que vous voulez installer sur des appareils Windows 10 Mobile, vous devez utiliser un certificat de code de signature Symantec.  

## <a name="deploy-windows-installer-apps-to-enrolled-windows-10-pcs"></a>Déployer des applications Windows Installer sur des PC Windows 10 inscrits  
 Le type de programme d’installation **Windows Installer via MDM (\*.msi)** vous permet de créer et déployer des applications Windows Installer sur des PC inscrits qui exécutent Windows 10.  

 Tenez compte des points suivants quand vous utilisez ce type de programme d’installation :  

-   Vous ne pouvez charger qu’un seul fichier avec l’extension .msi.  

-   Le code de produit et la version de produit du fichier sont utilisés pour la détection d’applications.  

-   Le comportement de redémarrage par défaut de l’application est utilisé. Configuration Manager ne contrôle pas cette fonctionnalité.  

-   Les packages MSI par utilisateur sont installés pour un seul utilisateur.  

-   Les packages MSI par ordinateur sont installés pour tous les utilisateurs sur l’appareil.  

-   Les mises à jour d’application sont prises en charge quand les codes de produit MSI de toutes les versions sont identiques.  



<!--HONumber=Dec16_HO3-->


