---
title: "Créer un regroupement MDM"
titleSuffix: Configuration Manager
description: "Créez un regroupement MDM via System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
caps.latest.revision: "18"
caps.handback.revision: "0"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: f8b865c48f6c69fe1cfd7221273b09f5557075e9
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>Créer un regroupement MDM via System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Un regroupement d’utilisateurs Configuration Manager est obligatoire pour spécifier les utilisateurs qui peuvent inscrire des appareils dans la gestion. Vous pouvez utiliser seulement des regroupements d’utilisateurs (au lieu de regroupements d’appareils ) car les licences Intune sont affectées par utilisateur.

> [!NOTE]
> Pour inscrire des appareils avec Intune, vous n’avez pas besoin d’affecter des licences aux utilisateurs dans le portail Office 365 ou dans le portail Azure Active Directory. Vous devez seulement inclure les utilisateurs dans un regroupement qui est associé à l’abonnement Intune (dans une [étape ultérieure](configure-intune-subscription.md)).

À des fins de test, vous pouvez configurer une **règle directe** et ajouter des utilisateurs spécifiques qui peuvent inscrire des appareils. Dans la console Configuration Manager, choisissez **Ressources et Conformité** > **Regroupements d’utilisateurs**, cliquez sur l’onglet **Accueil** > **Créer** un groupe, puis cliquez sur **Créer un regroupement d’utilisateurs**. Pour une distribution plus large, utilisez **Règle de requête** et définissez des utilisateurs. Pour plus d’informations sur les regroupements, consultez [Guide pratique pour créer des regroupements](https://technet.microsoft.com/library/mt629371.aspx).

![Créer un regroupement d’utilisateurs pour MDM](../media/mdm-create-user-collection.png)

> [!div class="button"]
[Étape suivante >](confirm-dns.md)
