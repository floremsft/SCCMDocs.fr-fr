---
title: "Créer des applications Windows Phone | Documents Microsoft"
description: "Examinez les éléments à prendre en compte quand vous créez et déployez des applications pour des appareils Windows Phone."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 866113ff-efd0-40d2-ac3a-2edd49732a24
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 557888d1f1f899e3198c430bbe5ccdd44178f824
ms.openlocfilehash: 5cd1ba42afd13e98565d24d1ec8a3ee209e8532c


---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>Créer des applications Windows Phone à l’aide de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

En plus des autres exigences et procédures System Center Configuration Manager à observer pour créer une application, vous devez aussi prendre en compte les éléments suivants au moment de créer et déployer des applications pour des appareils Windows Phone.  

## <a name="general-considerations"></a>Éléments généraux à prendre en compte  
 Configuration Manager prend en charge le déploiement des types de fichiers d’application suivants :  

|Type d'appareil|Types de fichiers pris en charge|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8.1|.xap, .appx, .appxbundle|  

 Les actions de déploiement suivantes sont prises en charge :  

|Type d'appareil|Actions prises en charge|  
|-----------------|-----------------------|  
|Windows Phone 8 et Windows Phone 8.1|disponible, obligatoire, désinstaller|  

## <a name="steps-to-deploy-the-latest-windows-phone-company-portal-app-with-supersedence"></a>Étapes de déploiement de la dernière version de l’application de portail d’entreprise Windows Phone avec remplacement  
 Le tableau suivant présente la procédure, des détails et des informations complémentaires pour créer et déployer la dernière version de l'application de portail d'entreprise Windows Phone 8.  

|Étape|Plus d'informations|  
|----------|----------------------|  
|**Étape 1 :** obtenir la dernière application de portail d’entreprise.|Téléchargez l' [application du portail d'entreprise Windows Phone 8](http://go.microsoft.com/fwlink/?LinkId=268440).|  
|**Étape 2 :** signer l’application de portail d’entreprise avec votre certificat Symantec.|Pour plus d’informations sur la façon de signer l’application de portail d’entreprise, consultez [Configurer la gestion des appareils Windows Phone et Windows 10 Mobile hybrides avec System Center Configuration Manager et Microsoft Intune](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Étape 3 :** Créer une application avec la version la plus récente de l’application de portail d’entreprise et spécifier une relation de remplacement.|Pour plus d’informations, consultez [Créer des applications](../../apps/deploy-use/create-applications.md) et [Réviser et remplacer des applications](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Étape 4 :** ajouter l’application à l’Assistant Créer un abonnement Windows Intune.|Pour plus d’informations, consultez [Configurer la gestion des appareils Windows Phone et Windows 10 Mobile hybrides avec System Center Configuration Manager et Microsoft Intune](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Étape 5 :** supprimer le déploiement qui est automatiquement créé lorsque vous avez ajouté l’application de portail d’entreprise à l’Assistant Créer un abonnement Microsoft Intune.|L’abonnement Microsoft Intune a créé un déploiement automatique de cette application, car ce déploiement ne prendra pas en charge le remplacement.|  
|**Étape 6 :** Créer un déploiement de l’application. Dans la page **Paramètres de déploiement** de l’**Assistant Déploiement logiciel**, cochez la case **Mettre automatiquement à niveau toutes les versions remplacées de cette application**.|Créez un nouveau déploiement avec le remplacement à l'aide de l'application que vous avez créée avec la relation de remplacement.|  
|**Étape 7 (facultative) :** Par défaut, les applications de remplacement s’installent sur les appareils au bout de sept jours. Pour déployer l’application de portail d’entreprise plus tôt sur les appareils inscrits auparavant, définissez le paramètre **Planifier la réévaluation des déploiements** sur une valeur inférieure.<br /><br /> Si vous affectez à cette valeur une valeur inférieure à la valeur par défaut, cela peut affecter négativement les performances de votre réseau et des ordinateurs clients.|Aucune information supplémentaire.|  



<!--HONumber=Dec16_HO1-->


