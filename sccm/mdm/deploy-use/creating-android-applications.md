---
title: "Créer des applications Android | Documents Microsoft"
description: "Examinez les éléments à prendre en compte quand vous créez et déployez des applications pour appareils Android."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 3d90b2cb1e255b9e8827a991779024ccecde9646
ms.lasthandoff: 03/06/2017

---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>Créer des applications Android avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une application System Center Configuration Manager inclut un ou plusieurs types de déploiement, qui comprennent les fichiers d’installation et informations nécessaires pour déployer le logiciel sur un appareil. Le type de déploiement contient également des règles spécifiant à quel moment et selon quelle méthode le logiciel est déployé.  

 Vous pouvez créer des applications à l'aide des méthodes suivantes :  

-   Créer automatiquement les types d'application et de déploiement en lisant les fichiers d'installation de l'application.  

-   Créer manuellement l'application, puis ajouter des types de déploiement ultérieurement.  

-   Importer une application à partir d’un fichier.  

Pour connaître les étapes requises pour créer des types de déploiement et applications Configuration Manager, voir [Démarrer l’Assistant Création d’une application](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard). De plus, gardez à l’esprit les considérations suivantes lorsque vous créez et déployez des applications pour des appareils Android.  

## <a name="general-considerations"></a>Éléments généraux à prendre en compte

Configuration Manager prend en charge le déploiement des types d’applications suivants pour Android :

|Type d'appareil|Fichiers pris en charge|
|-|-|
|Android|.apk|

Les actions de déploiement suivantes sont prises en charge :

|Type d'appareil|Actions prises en charge|
|-|-|
|Android|**Disponible**, **Obligatoire**. L’utilisateur doit donner son consentement pour l’installation et la désinstallation.

