---
title: "Configurer les paramètres client | System Center Configuration Manager"
description: "Sélectionnez les paramètres client dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: 5
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9e3162e04da90748379145e37f6b378badab97d3

---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>Guide pratique pour configurer les paramètres client dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous gérez tous les paramètres client dans System Center Configuration Manager à partir du nœud **Paramètres client** de l’espace de travail **Administration** de la console Configuration Manager. Modifiez les paramètres par défaut lorsque vous souhaitez configurer des paramètres pour tous les utilisateurs et appareils de la hiérarchie ne disposant pas de paramètres personnalisés. Si vous souhaitez appliquer différents paramètres à certains utilisateurs ou appareils, créez des paramètres personnalisés et déployez-les vers les regroupements.  

> [!NOTE]  
>  Vous pouvez également utiliser des éléments de configuration pour gérer des clients afin d'évaluer, de suivre et de corriger la conformité de la configuration des appareils. Pour plus d’informations, consultez [Garantir la conformité des appareils avec System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

##  <a name="a-namebkmkdefaultclientsettingsa-how-to-configure-the-default-client-settings"></a><a name="BKMK_DefaultClientSettings"></a> Comment configurer les paramètres client par défaut  

 Utilisez la procédure suivante pour configurer les paramètres client par défaut, pour tous les clients de la hiérarchie.  

#### <a name="to-configure-the-default-client-settings"></a>Pour configurer les paramètres client par défaut  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Paramètres client**, puis sélectionnez **Paramètres client par défaut**.  

3.  Sous l'onglet **Accueil** , cliquez sur **Propriétés**.  

4.  Consultez et configurez les paramètres client pour chaque groupe de paramètres dans le volet de navigation. Pour plus d’informations sur chaque paramètre, consultez [À propos des paramètres client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).  

5.  Cliquez sur **OK** pour fermer la boîte de dialogue **Paramètres client par défaut** .  

 Les ordinateurs client sont configurés avec ces paramètres lorsqu'ils téléchargent la stratégie client. Pour lancer une récupération de stratégie pour un seul client, consultez [Lancer une récupération de stratégie pour un client Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) dans [Comment gérer les clients dans System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="a-namebkmkcustomclientsettingsa-how-to-create-and-deploy-custom-client-settings"></a><a name="BKMK_CustomClientSettings"></a> Comment créer et déployer des paramètres client personnalisés  
 Utilisez la procédure suivante pour configurer et déployer des paramètres personnalisés pour un regroupement sélectionné d'utilisateurs ou d'appareils. Lorsque vous déployez ces paramètres personnalisés, ceux-ci remplacent les paramètres client par défaut.  

> [!NOTE]  
>  Avant de débuter cette procédure, assurez-vous que vous disposez d'un regroupement qui contient les utilisateurs ou les appareils qui nécessitent ces paramètres client personnalisés.  

#### <a name="to-configure-and-deploy-custom-client-settings"></a>Pour configurer et déployer des paramètres client personnalisés  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Paramètres client**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer des paramètres client personnalisés**, puis cliquez sur l'une des options suivantes, selon que vous souhaitez créer des paramètres client personnalisés pour des appareils ou pour des utilisateurs :  

    -   **Créer des paramètres d'appareil client personnalisés**  

    -   **Créer des paramètres utilisateur client personnalisés**  

4.  Dans la boîte de dialogue **Créer des paramètres d'appareil client personnalisés** ou **Créer des paramètres utilisateur client personnalisés** , spécifiez un nom unique pour les paramètres personnalisés et une description facultative.  

5.  Cochez une ou plusieurs des cases disponibles, qui affichent un groupe de paramètres.  

6.  Cliquez sur les premiers paramètres du groupe dans le volet de navigation, puis affichez et configurez les paramètres personnalisés disponibles. Répétez cette procédure pour les autres paramètres du groupe. Pour plus d’informations sur chaque paramètre client, consultez [À propos des paramètres client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).  

7.  Cliquez sur **OK** pour fermer la boîte de dialogue **Créer des paramètres de périphérique client personnalisés** ou **Créer des paramètres utilisateur client personnalisés** .  

8.  Sélectionnez le paramètre client personnalisé que vous venez de créer. Sous l'onglet **Accueil** , dans le groupe **Paramètres client** , cliquez sur **Déployer**.  

9. Dans la boîte de dialogue **Sélectionner un regroupement** , sélectionnez le regroupement contenant les appareils ou les utilisateurs que vous souhaitez configurer en utilisant les paramètres par défaut, puis cliquez sur **OK**. Vous pouvez vérifier le regroupement sélectionné en cliquant sur l'onglet **Déploiements** du volet d'informations.  

10. Consultez l'ordre du paramètre client personnalisé que vous venez de créer. Lorsque vous disposez de plusieurs paramètres client personnalisés, ceux-ci sont appliqués en fonction de leur numéro. En cas de conflit, le paramètre dont le numéro d'ordre est le plus petit remplace les autres paramètres. Pour changer la position du paramètre, sur l'onglet **Accueil** , dans le groupe **Paramètres client** , cliquez sur **Déplacer l'élément vers le haut** ou **Déplacer l'élément vers le bas**.  

 Les ordinateurs client sont configurés avec ces paramètres lorsqu'ils téléchargent la stratégie client. Pour lancer une récupération de stratégie pour un seul client, consultez [Lancer une récupération de stratégie pour un client Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) dans [Comment gérer les clients dans System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="a-namebkmkresultantclientsettingsa-how-to-view-resultant-client-settings"></a><a name="BKMK_ResultantClientSettings"></a> Comment afficher les paramètres client qui en résultent  
 Lorsque plusieurs paramètres client sont déployés sur le même appareil, utilisateur ou groupe d'utilisateurs, la définition des priorités et la combinaison des paramètres peuvent être complexes. Pour afficher les paramètres résultants du client calculés, procédez comme suit.  

#### <a name="to-view-the-resultant-client-settings"></a>Pour afficher les paramètres résultants du client  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et conformité** , cliquez sur **Périphériques**, **Utilisateurs**ou **Regroupements d'utilisateurs**.  

3.  Sélectionnez un appareil, un utilisateur ou un groupe d'utilisateurs, puis dans le groupe **Paramètres client** , sélectionnez **Paramètres résultants du client**.  Vous pouvez également cliquer avec le bouton droit sur l'appareil, l'utilisateur ou le groupe d'utilisateurs, sélectionner **Paramètres client**et cliquer sur **Paramètres résultants du client**.  

4.  Sélectionnez un paramètre client dans le volet gauche pour afficher les paramètres résultants.  

    > [!NOTE]  
    >  Pour afficher les paramètres résultants du client, l'utilisateur connecté doit disposer d'un accès en lecture aux paramètres client.  

    > [!NOTE]  
    >  Les paramètres résultants affichés sont en lecture seule. Pour modifier des paramètres, procédez comme décrit ci-dessus.  



<!--HONumber=Nov16_HO1-->


