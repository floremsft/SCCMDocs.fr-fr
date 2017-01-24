---
title: "Gérer les mises à jour d’Office 365 ProPlus | Microsoft Docs"
description: "Configuration Manager synchronise les mises à jour du client Office 365 du catalogue WSUS vers le serveur de site de façon à rendre les mises à jour disponibles pour un déploiement sur les clients."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 11/10/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
translationtype: Human Translation
ms.sourcegitcommit: 5415bfa0ac4af14891a9445cdeab6a4509fffc38
ms.openlocfilehash: 630ccdf7b7f45a88586c9ab530c164985267bec9

---

# <a name="manage-office-365-proplus-updates-with-configuration-manager"></a>Gérer les mises à jour d’Office 365 ProPlus avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

À compter de Configuration Manager version 1602, Configuration Manager permet de gérer les mises à jour du client Office 365 en utilisant le flux de travail de gestion des mises à jour logicielles. Lorsque Microsoft publie une nouvelle mise à jour du client Office 365 sur le réseau de distribution contenu (CDN) d’Office, Microsoft publie également un package de mise à jour sur Windows Server Update Services (WSUS). Après que Configuration Manager a synchronisé la mise à jour du client Office 365 du catalogue WSUS vers le serveur de site, la mise à jour est disponible pour un déploiement sur les clients.

## <a name="office-365-client-management-dashboard"></a>Tableau de bord Gestion des clients Office 365  
À partir de Configuration Manager version 1610, le tableau de bord de gestion des clients Office 365 est disponible dans la console Configuration Manager. Pour afficher le tableau de bord, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des clients Office 365**.

<!--- >[!NOTE]
>In the **What's New** workspace in the Configuration Manager console, the new dashboard is incorrectly named **Office 365 Servicing dashboard**. --->

Le tableau de bord affiche des graphiques pour les éléments suivants :

- Nombre de clients Office 365
- Versions du client Office 365
- Langues du client Office 365
- Canaux du client Office 365     
Pour plus d’informations, consultez [Présentation des canaux de mise à jour pour Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

En haut du tableau de bord, utilisez le paramètre de liste déroulante **Regroupement** pour filtrer les données de tableau de bord selon les membres d’un regroupement spécifique.

<!---
 On the upper-right side of the dashboard, click **Office 365 Installer** to start the Office 365 Client Installation Wizard to deploy Office 365 apps to clients. For details, see [Deploy Office 365 apps to clients](#deploy-office-365-apps-to-clients).
- On the middle-right side of the dashboard, click **Create an ADR** to open the Automatic Deployment Rule Wizard to create a new automatic deployment rule (ADR). To create an ADR for Office 365 apps, select **Office 365 Client** when you choose the product. For more information, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- On the lower-right side of the dashboard, click **Create Client Agent Settings** to open Client Agent settings. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings).
--->

#### <a name="to-deploy-office-365-updates-with-configuration-manager"></a>Pour déployer les mises à jour d’Office 365 avec Configuration Manager
Procédez comme suit pour déployer les mises à jour d’Office 365 avec le Gestionnaire de Configuration :

1.  [Vérifiez la configuration requise](https://technet.microsoft.com/library/mt628083.aspx) pour utiliser Configuration Manager en vue de gérer les mises à jour du client Office 365 dans la section **Configuration requise pour utiliser Configuration Manager afin de gérer les mises à jour du client Office 365** de la rubrique.  

2.  [Configurez les points de mise à jour logicielle](../get-started/configure-classifications-and-products.md) pour synchroniser les mises à jour du client Office 365. Définissez **Mises à jour** en guise de classification et sélectionnez **Office 365 Client** en guise de produit. Vous pouvez être amené à synchroniser les mises à jour logicielles au moins une fois avant que le produit Office 365 Client puisse être sélectionné. Vous devez synchroniser les mises à jour logicielles après avoir configuré les points de mise à jour logicielle pour utiliser la classification **Mises à jour**.  

3.  Habilitez les clients Office 365 à recevoir des mises à jour de Configuration Manager. Pour cela, vous pouvez utiliser les paramètres du client Configuration Manager ou la stratégie de groupe. Employez l’une des méthodes suivantes pour activer le client :  
    - Méthode 1 : à compter de Configuration Manager version 1606, vous pouvez utiliser le paramètre du client Configuration Manager pour gérer l’agent Office 365 Client. Après avoir configuré ce paramètre et déployé les mises à jour d’Office 365, l’agent client Configuration Manager communique avec l’agent Office 365 Client de façon à télécharger les mises à jour d’Office 365 à partir d’un point de distribution et ensuite à les installer. Configuration Manager dresse l’inventaire des paramètres du client Office 365 ProPlus.
      1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Vue d’ensemble** > **Paramètres client**.  

      2.  Ouvrez les paramètres d’appareil appropriés pour activer l’agent client. Pour plus d’informations sur les paramètres par défaut et personnalisés du client, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Cliquez sur **Mises à jour logicielles** et sélectionnez **Oui** pour le paramètre **Activer la gestion de l’agent Office 365 Client**.  

    - Méthode 2 : [Habilitez les clients Office 365 à recevoir les mises à jour](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient) de Configuration Manager via l’outil Déploiement d’Office ou la stratégie de groupe.  

4. [Déployez les mises à jour d’Office 365](deploy-software-updates.md) sur les clients.  

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->



<!--HONumber=Dec16_HO3-->


