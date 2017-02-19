---
title: Configurer les alertes Endpoint Protection | Microsoft Docs
description: "Découvrez comment configurer les alertes Endpoint Protection dans System Center Configuration Manager."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 9b20b50843cadc478d5b75a276d2a24aea30f2ff
ms.openlocfilehash: 6e7b080c1e1876c0ccef9ce6568ce88b65dfca87


---

#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Configurer des alertes pour Endpoint Protection dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Vous pouvez configurer des alertes Endpoint Protection dans Microsoft System Center Configuration Manager pour avertir les utilisateurs administratifs quand des événements spécifiques, comme une infection par un logiciel malveillant, se produisent dans votre hiérarchie. Les notifications s’affichent dans le tableau de bord Endpoint Protection, dans la console Configuration Manager, dans le nœud **Alertes** de l’espace de travail **Surveillance**. Elles peuvent aussi être envoyées par e-mail à des utilisateurs spécifiés.

 Utilisez les étapes suivantes et les procédures supplémentaires de cette rubrique pour configurer des alertes pour Endpoint Protection dans Configuration Manager.

> [!IMPORTANT]
>  Vous devez disposer de l’autorisation **Appliquer la sécurité** pour les regroupements pour pouvoir configurer des alertes Endpoint Protection.

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Étapes de configuration des alertes pour Endpoint Protection dans Configuration Manager

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.

2.  Dans l'espace de travail **Ressources et Conformité** , cliquez sur **Regroupements d’appareils**.

3.  Dans la liste **Regroupements d’appareils** , sélectionnez le regroupement pour lequel vous voulez configurer des alertes, puis cliquez sur **Propriétés** dans le groupe **Propriétés** sous l’onglet **Accueil**.

    > [!NOTE]
    >  Vous ne pouvez pas configurer d'alertes pour les regroupements d'utilisateurs.

4.  Sous l’onglet **Alertes** de la boîte de dialogue *Propriétés de***<Nom du regroupement\>**, sélectionnez **Afficher ce regroupement dans le tableau de bord Endpoint Protection** si vous voulez afficher des détails sur les opérations anti-programme malveillant pour ce regroupement dans l’espace de travail **Surveillance** de la console Configuration Manager.

    > [!NOTE]
    >  Cette option n'est pas disponible pour le regroupement **Tous les systèmes** .

5.  Sous l’onglet **Alertes** de la boîte de dialogue *Propriétés de***<Nom du regroupement\>**, cliquez sur **Ajouter**.

6.  Dans la section **Générer une alerte lorsque ces conditions s’appliquent** de la boîte de dialogue **Ajouter de nouvelles alertes de regroupement**, sélectionnez les alertes que doit générer Configuration Manager lorsque les événements Endpoint Protection spécifiés se produisent, puis cliquez sur **OK**.

7.  Dans la liste  **Conditions** de l’onglet **Alertes**, sélectionnez chaque alerte Endpoint Protection, puis spécifiez ce qui suit :

    -   **Nom d’alerte** : acceptez le nom par défaut ou entrez un nouveau nom pour l’alerte.

    -   **Gravité d’alerte** : dans la liste, sélectionnez le niveau d’alerte à afficher dans la console Configuration Manager.

8.  Selon l’alerte que vous sélectionnez, spécifiez les informations supplémentaires suivantes :

    -   **Détection d’un programme malveillant** : cette alerte est générée si un logiciel malveillant est détecté sur un ordinateur du regroupement que vous surveillez. Le **seuil de détection des programmes malveillants** indique les niveaux de détection auxquels cette alerte est générée :

        -   **Haute - Toutes les détections** : l’alerte est générée quand un programme malveillant est détecté sur un ou plusieurs ordinateurs du regroupement spécifié, quelle que soit l’action qu’exécute le client Endpoint Protection.

        -   **Moyenne - Détectée, action en attente** : l’alerte est générée quand un programme malveillant est détecté sur un ou plusieurs ordinateurs du regroupement spécifié, et que vous devez le supprimer manuellement.

        -   **Faible - Détectée, toujours active** : l’alerte est générée quand un programme malveillant est détecté sur un ou plusieurs ordinateurs du regroupement spécifié, et qu’il est toujours actif.

    -   **Apparition d’un programme malveillant** : cette alerte est générée si un programme malveillant spécifié est détecté sur un pourcentage donné d’ordinateurs du regroupement que vous surveillez.

        -   **Pourcentage d’ordinateurs sur lesquels un programme malveillant a été détecté** : l’alerte est générée quand le pourcentage d’ordinateurs avec un programme malveillant détecté dans le regroupement est supérieur au pourcentage que vous spécifiez. Spécifiez un pourcentage compris entre **1** et **99**.

            > [!NOTE]
            >  La valeur du pourcentage est basée sur le nombre d’ordinateurs du regroupement, mais exclut les ordinateurs sur lesquels aucun client Configuration Manager n’est installé. Il inclut les ordinateurs sur lesquels le client Endpoint Protection n’est pas encore installé.

    -   **Détection de logiciel malveillant répétée** : cette alerte est générée si un logiciel malveillant spécifique est détecté un nombre spécifié de fois sur un nombre spécifié d’heures sur les ordinateurs du regroupement que vous surveillez. Spécifiez les informations suivantes pour configurer cette alerte :

        -   **Nombre de fois où un programme malveillant a été détecté :** l’alerte est générée quand le nombre de détections d’un même programme malveillant sur les ordinateurs du regroupement est supérieur au nombre d’occurrences spécifié. Spécifiez un nombre compris entre **2** et **32**.

        -   **Intervalle de détection (heures) :** spécifiez l’intervalle de détection (en heures) au cours duquel le nombre de détections de programme malveillant doit être exécuté. Spécifiez un nombre compris entre **1** et **168**.

    -   **Détection de plusieurs logiciels malveillants** : cette alerte est générée si le nombre de types de programmes malveillants détectés pendant un nombre d’heures donné sur les ordinateurs du regroupement que vous surveillez est supérieur au nombre défini. Spécifiez les informations suivantes pour configurer cette alerte :

        -   **Nombre de types de programmes malveillants détectés :** l’alerte est générée quand le nombre spécifié de types différents de programmes malveillants sur les ordinateurs du regroupement est détecté. Spécifiez un nombre compris entre **2** et **32**.

        -   **Intervalle de détection (heures) :** spécifiez l’intervalle de détection, en heures, au cours duquel le nombre de détections de programme malveillant doit être exécuté. Spécifiez un nombre compris entre **1** et **168**.

9. Cliquez sur **OK** pour fermer la boîte de dialogue *Propriétés de***<Nom du regroupement\>**.  

> [!div class="button"]
[Étape suivante >](endpoint-definition-updates.md)

> [!div class="button"]
[Retour >](endpoint-protection-site-role.md)



<!--HONumber=Feb17_HO1-->


