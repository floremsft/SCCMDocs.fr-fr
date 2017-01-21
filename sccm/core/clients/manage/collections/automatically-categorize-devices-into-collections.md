---
title: Classer automatiquement des appareils dans des regroupements | Microsoft Docs
description: Classez automatiquement des appareils dans des regroupements avec System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: d5ef7260bcc2ab9cc56d8fed530a406aa1045c5a

---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>Classer automatiquement des appareils dans des regroupements avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez créer des catégories d’appareils, qui permettent de placer automatiquement les appareils dans des regroupements d’appareils quand vous utilisez Configuration Manager avec Microsoft Intune. Les utilisateurs sont alors invités à choisir une catégorie d’appareils quand ils inscrivent un appareil dans Intune. Vous pouvez en outre modifier la catégorie d’un appareil à partir de la console Configuration Manager.

> [!IMPORTANT]  
    >  Cette fonctionnalité est opérationnelle avec la version de **juin 2016** de Microsoft Intune. Vérifiez que vous avez effectué la mise à jour vers cette version avant d’essayer ces procédures.

## <a name="create-device-categories"></a>Créer des catégories d’appareils

1.  Dans l’espace de travail **Ressources et Conformité** de la console Configuration Manager, développez **Vue d’ensemble**, puis cliquez sur **Regroupements d’appareils**.
2.  Sous l’onglet **Accueil**, dans le groupe **Regroupements d’appareils**, cliquez sur **Gérer les catégories d’appareils**.
3.  Dans la boîte de dialogue **Gérer les catégories d’appareils**, vous pouvez créer, modifier ou supprimer des catégories.

## <a name="associate-a-collection-with-a-device-category"></a>Associer un regroupement à une catégorie d’appareils

Quand vous associez un regroupement à une catégorie d’appareils, tous les appareils de la catégorie que vous spécifiez sont ajoutés à ce regroupement.

> [!IMPORTANT]  
    >  Vous ne pouvez pas ajouter une règle de catégorie d’appareils à un regroupement intégré comme **Tous les systèmes**.

1.  Sous l’onglet **Règles d’adhésion** de la boîte de dialogue **Propriétés** pour un regroupement d’appareils, cliquez sur **Ajouter une règle** > **Règle de catégorie d’appareils**.
2.  Dans la boîte de dialogue **Sélectionner des catégories d’appareils**, sélectionnez une ou plusieurs catégories d’appareils à appliquer à tous les appareils du regroupement.
3.  Fermez la boîte de dialogue **Sélectionner des catégories d’appareils** et celle des propriétés du regroupement.


## <a name="change-the-category-of-a-device"></a>Changer la catégorie d’un appareil

1.  Dans l’espace de travail **Ressources et Conformité** de la console Configuration Manager, développez **Vue d’ensemble**, puis cliquez sur **Appareils**.
2.  Sélectionnez un appareil dans la liste **Appareils** et, sous l’onglet **Accueil**, dans le groupe **Appareil**, cliquez sur **Changer la catégorie**.
3.  Dans la boîte de dialogue **Modifier la catégorie d’appareils**, choisissez la catégorie à appliquer à cet appareil, puis cliquez sur **OK**.

## <a name="view-which-category-a-device-belongs-to"></a>Afficher la catégorie à laquelle appartient un appareil

1.  Dans l’espace de travail **Ressources et Conformité** de la console Configuration Manager, développez **Vue d’ensemble**, puis cliquez sur **Appareils**.
2.  Dans la liste **Appareils**, la catégorie est affichée dans la colonne **Catégorie d’appareil**.
> [!TIP]  
    >  Si la colonne **Catégorie d’appareil** n’est pas affichée, cliquez avec le bouton droit sur l’en-tête de l’une des colonnes dans la liste **Appareils** (comme **Nom**), puis sélectionnez **Catégorie d’appareil**.

Si vous affectez un appareil à une catégorie, puis supprimez par la suite cette catégorie, le rapport **Liste des appareils inscrits par utilisateur dans Microsoft Intune** affichera un GUID dans la colonne **Catégorie d’appareil** au lieu d’un nom de catégorie.



<!--HONumber=Dec16_HO3-->


