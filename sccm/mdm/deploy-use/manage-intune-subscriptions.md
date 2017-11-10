---
title: "Gérer un abonnement Intune"
titleSuffix: Configuration Manager
description: "Gérez un abonnement Microsoft Intune associé à System Center Configuration Manager."
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b494767-68c1-47b1-9a86-591bff0ad491
caps.latest.revision: "18"
caps.handback.revision: "0"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: a6bb27adeddc366526df699b69e95c6e7d6482ae
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="manage-an-intune-subscription-associated-with-system-center-configuration-manager"></a>Gérer un abonnement Microsoft Intune associé à System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Si vous ajoutez un abonnement Microsoft Intune (abonnement d’essai ou payant) à Configuration Manager, et si vous devez ensuite passer à un autre abonnement Intune, vous devez supprimer l’**abonnement Microsoft Intune** et le **point de connexion de service** dans la console Configuration Manager avant de pouvoir ajouter un nouvel abonnement.

> [!NOTE]
> Vous ne pouvez configurer qu’un seul abonnement Intune à la fois dans la fonction de gestion des appareils mobiles hybride.

## <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Comment supprimer un abonnement Intune de Configuration Manager

> [!IMPORTANT]
>  Tout le contenu, dont les inscriptions des utilisateurs, les stratégies et les déploiements d’applications configurés pour les appareils gérés par l’abonnement Intune, est supprimé quand vous supprimez l’abonnement.

1.  Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Services cloud** > **Abonnements Microsoft Intune**.

2.  Cliquez avec le bouton droit sur l’**abonnement Microsoft Intune** répertorié, puis cliquez sur **Supprimer**.

3.   Dans l’Assistant, cliquez sur **Remove Microsoft Intune Subscription from Configuration Manager** (Supprimer l’abonnement Microsoft Intune de Configuration Manager), sur **Suivant**, puis à nouveau sur **Suivant** pour supprimer l’abonnement.


## <a name="how-to-remove-the-service-connection-point-role"></a>Comment supprimer le rôle de point de connexion de service

1.  Accédez à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Serveurs et rôles de système de site**.

2.  Sélectionnez le serveur hébergeant le rôle **Point de connexion de service**.

3.  Dans la liste **Rôles système de site**, sélectionnez **Point de connexion de service**, puis cliquez sur **Supprimer le rôle** dans le ruban. Confirmez que vous souhaitez supprimer le rôle. Le point de connexion de service est supprimé.

Vous pouvez à présent créer un nouveau point de connexion de service, ajouter un nouvel abonnement Intune à Configuration Manager et définir Configuration Manager comme autorité de gestion des appareils mobiles.

## <a name="how-to-change-mdm-authority-to-intune"></a>Comment définir l’autorité MDM sur Intune
À compter de Configuration Manager version 1610 et de Microsoft Intune version 1705, vous pouvez modifier votre autorité de gestion des appareils mobiles sans avoir à contacter le Support Microsoft et sans devoir annuler l’inscription de vos appareils gérés existants et les réinscrire. Pour plus d’informations, consultez [Changer d’autorité MDM](/sccm/mdm/deploy-use/change-mdm-authority).
