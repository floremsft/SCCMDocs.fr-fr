---
title: "Inscrire des appareils appartenant aux utilisateurs pour les déploiements hybrides avec Configuration Manager | Microsoft Docs"
description: "Découvrez les différentes méthodes d’inscription des appareils appartenant aux utilisateurs pour les déploiements hybrides avec Configuration Manager."
ms.custom: na
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bdaa8a7-6a64-4b0e-b617-309dcd912c45
caps.latest.revision: "13"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 56bd6bfd900a8ecbb149392de62889970ddedb60
ms.sourcegitcommit: 40f2a4e3cc546e6bfd10f195a8e87af2b0780928
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/08/2017
---
# <a name="enroll-user-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Inscrire des appareils appartenant aux utilisateurs pour les déploiements hybrides avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les appareils appartenant à l’utilisateur peuvent être soumis à la gestion en les inscrivant, un processus souvent appelé « BYOD » ou « Apportez votre propre appareil ». Les utilisateurs effectuent ceci en installant l’application Portail d’entreprise et en se connectant sur l’appareil (iOS, Mac OS et Android), ou en ajoutant un compte professionnel ou scolaire à l’appareil et en se joignant à un domaine (Windows). Ce processus inscrit l’appareil auprès d’Intune, ce qui donne à l’utilisateur l’accès aux ressources gérées par Intune et laisse Intune gérer certains paramètres de l’appareil, comme demander un code PIN.

Pour soumettre des appareils à la gestion, vous devez d’abord, en tant qu’administrateur, [configurer la gestion des appareils mobiles](setup-hybrid-mdm.md) et [activer l’inscription](enable-platform-enrollment.md). Une fois l’inscription activée, les utilisateurs peuvent inscrire leurs propres appareils. Consultez [Guide pratique pour informer vos utilisateurs finaux sur Microsoft Intune](https://docs.microsoft.com/intune/end-user-educate) pour des considérations et des procédures à partager avec vos utilisateurs.

Les entreprises ou les établissements scolaires qui achètent des appareils peuvent bénéficier de programmes qui vous permettent de [gérer des appareils d’entreprise](enroll-company-owned-devices.md).
