---
title: "Synchroniser à distance la stratégie sur des appareils inscrits auprès d’Intune"
titleSuffix: Configuration Manager
description: "Découvrir comment synchroniser la stratégie sur des appareils inscrits auprès d’Intune à partir de la console Configuration Manager"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
caps.latest.revision: "18"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: a03ba69c679bcfdc54744314c7a4cb3ef8b2a7a0
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Synchroniser à distance la stratégie sur des appareils inscrits auprès d’Intune à partir de la console Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Vous pouvez demander une synchronisation de la stratégie pour un appareil mobile inscrit auprès d’Intune à partir de la console Configuration Manager. Cela vous évite de devoir demander une synchronisation dans l’application Portail d’entreprise sur l’appareil. 

Pour cela :

1.  Sélectionnez un appareil sous **Actifs et Conformité** > **Vue d’ensemble** > **Appareils**.
2.  Cliquez sur **Envoyer une demande de synchronisation** dans le menu **Actions de l’appareil à distance**.


Au bout de cinq à dix minutes, toutes les modifications apportées à la stratégie sont synchronisées avec l’appareil. Vous pouvez afficher des informations sur l’état de la demande de synchronisation dans une nouvelle colonne des affichages d’appareil, appelée **État de la synchronisation à distance**, ainsi que dans la section des données de découverte de la boîte de dialogue **Propriétés** de chaque appareil.
