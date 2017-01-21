---
title: "Tâches courantes de gestion de la conformité des appareils sur les appareils n’exécutant pas le client System Center Configuration Manager | System Center Configuration Manager"
description: "Découvrez les paramètres de compatibilité de System Center Configuration Manager en examinant certains scénarios courants."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 116cca2a-0a98-43fd-ac9e-e3daeddefce3
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f69250fbe51ea8902a0446a613d66be390ea7434


---
# <a name="common-tasks-for-managing-compliance-on-devices-not-running-the-system-center-configuration-manager-client"></a>Tâches courantes de gestion de la conformité des appareils sur les appareils n’exécutant pas le client System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique vous propose une introduction à l’utilisation des paramètres de compatibilité de System Center Configuration Manager à travers des exemples de scénarios courants que vous êtes susceptible de rencontrer.  

 Si vous connaissez déjà les paramètres de compatibilité, vous trouverez une documentation détaillée sur toutes les fonctionnalités que vous utilisez dans la section [Éléments de configuration des appareils gérés sans le client System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md).  

 Avant de commencer, lisez [Bien démarrer avec les paramètres de compatibilité](../../compliance/get-started/get-started-with-compliance-settings.md) pour apprendre les notions de base sur les paramètres de compatibilité, et lisez également [Planifier et configurer les paramètres de compatibilité](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) pour implémenter tous les prérequis.  

## <a name="general-information-for-each-scenario"></a>Informations générales pour chaque scénario  
 Dans chaque scénario, vous allez créer un élément de configuration qui effectue une tâche spécifique. Pour ouvrir l’Assistant Création d’élément de configuration, procédez comme suit :  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Éléments de configuration**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un élément de configuration**.  

4.  Sous l’onglet **Général** de l’Assistant Création d’élément de configuration illustré ci-dessous, nommez et décrivez l’élément de configuration, puis choisissez le type d’élément de configuration approprié pour chaque scénario de cette rubrique.  

     ![Affiche la page Général de l’Assistant Création d’élément de configuration.](/sccm/compliance/plan-design/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-81-and-windows-10-devices-managed-without-the-configuration-manager-client"></a>Scénarios pour appareils Windows 8.1 et Windows 10 gérés sans le client Configuration Manager  

### <a name="scenario-restrict-access-to-the-app-store-on-all-windows-pcs"></a>Scénario : restreindre l’accès à la boutique d’applications sur tous les PC Windows  
 Dans ce scénario, vous êtes l’administrateur informatique d’une société qui gère des informations hautement confidentielles. Pour cette raison, vous limitez les applications que les utilisateurs peuvent installer. Vous souhaitez empêcher les utilisateurs de tous les PC Windows 10 de télécharger des applications à partir du Windows Store. Vous prenez donc les mesures suivantes.  

#### <a name="steps"></a>Étapes  

1.  Dans la page **Général** de l’Assistant Création d’élément de configuration, sélectionnez le type d’élément de configuration **Windows 8.1 et Windows 10** , puis cliquez sur **Suivant**.  

2.  Dans la page **Plateformes prises en charge**, sélectionnez toutes les plateformes Windows 10.  

3.  Dans la page **Paramètres du périphérique** , sélectionnez **Boutique**, puis cliquez sur **Suivant**.  

4.  Dans la page **Boutique** , sélectionnez la valeur **Interdit** pour **Boutique d’applications**.  

5.  Sélectionnez **Résoudre les paramètres non compatibles** pour que la modification s’applique à tous les PC.  

6.  Terminez l’Assistant pour créer l’élément de configuration.  

 Vous pouvez maintenant utiliser les informations contenues dans la rubrique [Tâches courantes de création et de déploiement de bases de référence de configuration](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) pour déployer la configuration que vous avez créée sur les appareils.  

## <a name="scenarios-for-windows-phone-devices-managed-without-the-configuration-manager-client"></a>Scénarios pour appareils Windows Phone gérés sans le client Configuration Manager  

### <a name="scenario-disable-the-use-of-screen-capture-on-a-windows-phone"></a>Scénario : désactiver l’utilisation de la capture d’écran sur un Windows Phone  
 Dans ce scénario, vous utilisez des appareils Windows Phone 8.1 dans votre société. Ces appareils exécutent une application de ventes qui contient des informations sensibles. Pour protéger votre entreprise, vous souhaitez désactiver l’utilisation de la capture d’écran sur l’appareil, car elle pourrait être utilisée pour transmettre des informations sensibles en dehors de l’entreprise.  

1.  Dans la page **Général** de l’Assistant Création d’élément de configuration, sélectionnez le type d’élément de configuration **Windows Phone** , puis cliquez sur **Suivant**.  

2.  Dans la page **Plateformes prises en charge**, sélectionnez les plateformes **Tout Windows Phone 8.1**.  

3.  Dans la page **Paramètres du périphérique** , sélectionnez **Périphérique**, puis cliquez sur **Suivant**.  

4.  Dans la page **Périphérique** , sélectionnez la valeur **Désactivé** pour **Capture d’écran**.  

5.  Sélectionnez **Résoudre les paramètres non compatibles** pour que la modification s’applique à tous les appareils Windows Phone 8.1.  

6.  Terminez l’Assistant pour créer l’élément de configuration.  

 Vous pouvez maintenant utiliser les informations contenues dans la rubrique [Tâches courantes de création et de déploiement de bases de référence de configuration avec System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) pour déployer la configuration que vous avez créée sur les appareils.  

## <a name="scenarios-for-ios-and-mac-os-x-devices-managed-without-the-configuration-manager-client"></a>Scénarios pour appareils iOS et Mac OS X gérés sans le client Configuration Manager  

### <a name="scenario-disable-the-camera-on-ios-devices"></a>Scénario : désactiver l’appareil photo sur les appareils iOS  
 Dans ce scénario, votre entreprise produit des plans pour de nouvelles conceptions de produits. Ces plans contiennent des informations sensibles qui ne doivent pas être divulguées. Étant donné que votre entreprise fournit des iPhones ou des iPads à tous les employés, vous souhaitez désactiver l’utilisation de l’appareil photo sur ces appareils pour éviter leur utilisation pour photographier les plans.  

1.  Dans la page **Général** de l’Assistant Création d’élément de configuration, sélectionnez le type d’élément de configuration **iOS et Mac OS X** , puis cliquez sur **Suivant**.  

2.  Dans la page **Plateformes prises en charge**, sélectionnez toutes les plateformes d’appareils iPhone et iPad.  

3.  Dans la page **Paramètres du périphérique** , sélectionnez **Sécurité**, puis cliquez sur **Suivant**.  

4.  Dans la page **Sécurité** , sélectionnez la valeur **Interdit** pour **Appareil photo**.  

5.  Sélectionnez **Résoudre les paramètres non compatibles** pour que la modification s’applique à tous les appareils iOS.  

6.  Terminez l’Assistant pour créer l’élément de configuration.  

 Vous pouvez maintenant utiliser les informations contenues dans la rubrique [Tâches courantes de création et de déploiement de bases de référence de configuration avec System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) pour déployer la configuration que vous avez créée sur les appareils.  

## <a name="scenarios-for-android-and-samsung-knox-devices-managed-without-the-configuration-manager-client"></a>Scénarios pour les appareils Android et Samsung KNOX gérés sans le client Configuration Manager  

### <a name="scenario-require-a-password-on-all-android-5-devices"></a>Scénario : exiger un mot de passe sur tous les appareils Android 5  
 Dans ce scénario, vous allez créer un élément de configuration uniquement pour les appareils Android 5 qui exige des utilisateurs qu’ils configurent un mot de passe d’au moins six caractères sur leurs appareils. De plus, si un utilisateur entre un mot de passe incorrect à cinq reprises, l’appareil sera effacé.  

1.  Dans la page **Général** de l’Assistant Création d’élément de configuration, sélectionnez le type d’élément de configuration **Android et Samsung KNOX** , puis cliquez sur **Suivant**.  

2.  Dans la page **Plateformes prises en charge**, sélectionnez uniquement **Android 5** (pour que les paramètres soient appliqués uniquement à cette plateforme).  

3.  Dans la page **Paramètres du périphérique** , sélectionnez **Mot de passe**, puis cliquez sur **Suivant**.  

4.  Dans la page **Mot de passe** , configurez les paramètres suivants :  

    -   **Demander des paramètres de mot de passe sur les appareils** > **Requis**  

    -   **Longueur minimale du mot de passe (caractères)** > **6**  

    -   **Nombre d’échecs de tentative de connexion avant que le périphérique soit réinitialisé** > **5**  

5.  Terminez l’Assistant pour créer l’élément de configuration.  

 Vous pouvez maintenant utiliser les informations contenues dans la rubrique [Tâches courantes de création et de déploiement de bases de référence de configuration](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) pour déployer la configuration que vous avez créée sur les appareils.  




<!--HONumber=Nov16_HO1-->


