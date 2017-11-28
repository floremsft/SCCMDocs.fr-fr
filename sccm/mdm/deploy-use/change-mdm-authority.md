---
title: "Changer d’autorité MDM"
titleSuffix: Configuration Manager
description: "Découvrez comment changer l’autorité MDM en passant de Configuration Manager (hybride) à la version autonome d’Intune"
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/17/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: c61a44cce443a7ff210a626d114068691541aaae
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="change-your-mdm-authority"></a>Changer d’autorité MDM
À compter de Configuration Manager version 1610, vous pouvez modifier votre autorité MDM sans avoir à contacter le Support Microsoft et sans devoir annuler l’inscription de vos appareils gérés existants et les réinscrire. Cet article décrit les étapes à suivre pour modifier un client Microsoft Intune déjà configuré et le faire passer de la console Configuration Manager (hybride) à la version autonome d’Intune. Lorsque vous effectuez les étapes décrites dans cet article, les appareils sont gérés par Microsoft Intune dans le [portail Azure](https://portal.azure.com). 

> [!Note]    
> Si vous souhaitez modifier un locataire Microsoft Intune existant, dont l’autorité MDM est définie sur Intune, pour le passer sur Configuration Manager (hybride), consultez [Changer l’autorité MDM](https://docs.microsoft.com/intune-classic/deploy-use/change-mdm-authority).

> [!Important]    
> Cet article concerne le changement d’autorité de gestion des appareils mobiles (MDM) dans le cas où aucun utilisateur n’a fait l’objet d’une migration. Pour la changer après avoir [migré un sous-ensemble d’utilisateurs](migrate-hybridmdm-to-intunesa.md), consultez la page [Changer d’autorité MDM](migrate-change-mdm-authority.md).

## <a name="key-considerations"></a>Principales considérations
Après le passage à la nouvelle autorité MDM, une période de transition (jusqu'à huit heures) peut survenir avant que l’appareil n’effectue l’archivage et ne se synchronise avec le service. Vous devrez configurer les paramètres de la nouvelle autorité MDM (version autonome d’Intune) pour vous assurer que les appareils inscrits continueront d’être gérés et protégés après le changement. Tenez compte des éléments suivants :
- Les appareils doivent se connecter au service après le changement afin que les paramètres de la nouvelle autorité MDM (version autonome d’Intune) remplacent les paramètres existants sur l’appareil.
- Après avoir changé d’autorité MDM, certains des paramètres de base (tels que les profils) de l’autorité MDM précédente (hybride) restent sur l’appareil pendant sept jours. Il est recommandé de configurer les applications et les paramètres (stratégies, profils, applications, etc.) dès que possible dans la nouvelle autorité MDM. Déployez également les paramètres sur les groupes d’utilisateurs contenant ceux qui possèdent des appareils déjà inscrits. Dès qu’un appareil se connecte au service après le changement d’autorité MDM, il reçoit les nouveaux paramètres de la nouvelle autorité MDM. Toutes les stratégies qui viennent d’être ciblées remplacent les stratégies existantes sur l’appareil.
- Après la sélection de la nouvelle autorité MDM, une semaine peut être nécessaire avant que les données de conformité s’affichent correctement dans le [portail Azure](https://portal.azure.com). Cependant, les états de conformité dans Azure Active Directory et sur l’appareil resteront corrects et l’appareil sera ainsi toujours protégé.
- Les appareils qui n’ont pas d’utilisateurs associés (en général, lorsque vous utilisez le Programme d’inscription des appareils iOS ou des scénarios d’inscription en bloc) ne sont pas migrés vers la nouvelle autorité MDM. Pour ces appareils, vous devez contacter le support afin d’obtenir de l’aide pour déplacer ces appareils vers la nouvelle autorité MDM.

## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Se préparer à utiliser la version autonome d’Intune comme autorité MDM
Passez en revue les informations suivantes pour préparer le passage à l’autorité MDM :
- Vous devez disposer de Configuration Manager 1610 ou version ultérieure pour pouvoir changer d’autorité MDM.
- Après le passage à la nouvelle autorité MDM, la connexion d’un appareil au service peut prendre jusqu’à huit heures.
- Assurez-vous que tous les utilisateurs actuellement gérés par un système hybride disposent d’une licence Intune/EMS qui leur a été attribuée avant le changement d’autorité MDM. Cette licence garantit que l’utilisateur et ses appareils sont gérés par la version autonome d’Intune après le changement d’autorité MDM. Pour plus d’informations, consultez [Attribuer des licences Intune à vos comptes d’utilisateur](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Assurez-vous que le compte d’utilisateur administrateur dispose d’une licence Intune/EMS et vérifiez que le compte d’utilisateur administrateur peut se connecter à Intune avant le changement d’autorité MDM. L’autorité MDM devrait afficher **Définir sur Configuration Manager** (locataire hybride) dans Intune dans le [portail Azure](https://portal.azure.com) avant le changement d’autorité MDM.
- Le changement d’autorité MDM ne devrait avoir aucun impact significatif sur les utilisateurs finaux. 

## <a name="change-the-mdm-authority-to-intune-standalone"></a>Utiliser la version autonome d’Intune comme autorité MDM
Le processus pour utiliser la version autonome d’Intune comme autorité MDM comprend les étapes principales suivantes :  
- Dans la console Configuration Manager, utilisez l’option **Utiliser la version autonome d’Intune comme autorité MDM** pour supprimer l’abonnement Microsoft Intune existant.
- Dans Intune dans le [portail Azure](https://portal.azure.com), configurez et déployez les nouveaux réglages et les nouvelles applications à partir de la nouvelle autorité MDM (Intune).
- La prochaine fois qu’ils se connecteront au service, les appareils se synchroniseront et recevront les nouveaux paramètres à partir de la nouvelle autorité MDM.

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>Pour utiliser la version autonome d’Intune comme autorité MDM
1. Dans la console Configuration Manager, accédez à **Administration** &gt; **Vue d’ensemble** &gt; **Services Cloud** &gt; **Abonnement Microsoft Intune**, puis supprimez votre abonnement Intune existant.
2. Sélectionnez **Utiliser Microsoft Intune comme autorité MDM**, puis cliquez sur **Suivant**.
   ![Télécharger la demande de certificat APNs](./media/mdm-change-delete-subscription.png)
3. Ouvrez une session dans le locataire Intune que vous avez utilisé lorsque vous avez défini pour la première fois l’autorité MDM dans Configuration Manager.
4. Cliquez sur **Suivant** pour terminer l'Assistant.
5. L’autorité MDM a maintenant la valeur **Microsoft Intune**. L’abonnement Intune ne devrait plus apparaître dans le nœud des abonnements Microsoft Intune de la console Configuration Manager. 
6. Pour vérifier que l’autorité MDM est définie, effectuez les étapes suivantes : a. Connectez-vous au [portail Azure](https://portal.azure.com) avec le locataire Intune que vous avez utilisé précédemment. 
    b. Choisissez **Autres services** > **Surveillance + Gestion** > **Intune** > **Inscription de l’appareil**. L’autorité MDM s’affiche dans la section en haut à droite du panneau **Vue d’ensemble**. 

## <a name="next-steps"></a>Étapes suivantes
Une fois le changement d’autorité MDM effectué, passez en revue les étapes suivantes :
- Lorsque le service Intune détecte que l’autorité MDM d’un locataire a changé, il envoie un message de notification à tous les appareils inscrits pour archiver et se synchroniser avec le service (ces opérations sont effectuées en dehors de l’enregistrement régulier planifié). Par conséquent, une fois que l’autorité MDM du locataire est passée de hybride à la version autonome d’Intunetous les appareils sous tension et en ligne se connecteront au service, recevront la nouvelle autorité MDM et seront désormais gérés par la version autonome d’Intune. Il n’y aura aucune interruption au niveau de la gestion et de la protection de ces appareils.
- Les appareils hors tension ou hors ligne pendant (ou juste après) le changement d’autorité MDM se connectent et se synchronisent avec le service sous la nouvelle autorité MDM quand ils sont sous tension et en ligne.  
- Les utilisateurs peuvent rapidement basculer vers la nouvelle autorité MDM en lançant manuellement un enregistrement de l’appareil vers le service. Les utilisateurs peuvent facilement effectuer cette opération à l’aide de l’application du portail d’entreprise, en lançant une vérification de conformité d’appareil.
- Pour confirmer que tout fonctionne correctement une fois les appareils enregistrés et synchronisés avec le service après le changement d’autorité MDM, recherchez les appareils dans le [portail Azure](https://portal.azure.com). Les appareils précédemment gérés par Configuration Manager (hybride) apparaîtront désormais en tant qu’appareils gérés dans Intune.    
- Il existe une période temporaire pendant laquelle un appareil est hors ligne lors du changement d’autorité MDM et lorsque cet appareil s’enregistre auprès du service. Pour que l’appareil reste protégé et opérationnel pendant cet intervalle, les profils suivants restent dessus pendant sept jours maximum (ou jusqu’à ce que l’appareil se connecte à la nouvelle autorité MDM et reçoive les nouveaux paramètres qui remplaceront les paramètres existants) :
    - Profil de messagerie
    - Profil VPN
    - Profil de certificat
    - Profil Wi-Fi
    - Profils de configuration
- Vérifiez que les nouveaux paramètres destinés à remplacer les paramètres existants portent le même nom que les précédents pour s’assurer que les anciens paramètres sont remplacés. Sinon, les appareils risquent de contenir des stratégies et des profils redondants.    

  > [!TIP]   
  > Il est recommandé de créer tous les paramètres de gestion et toutes les configurations, ainsi que les déploiements, peu de temps après le changement d’autorité MDM. Cela permet de s’assurer que les appareils sont protégés et activement gérés pendant la période temporaire.   
-  Après avoir modifié l’autorité MDM, procédez comme suit pour confirmer que les nouveaux appareils sont inscrits correctement auprès de la nouvelle autorité :   
    - Inscrire un nouvel appareil
    - Assurez-vous que l’appareil qui vient d’être inscrit s’affiche sur le [portail Azure](https://portal.azure.com).
    - Effectuez une action, par exemple un verrouillage à distance, à partir du [portail Azure](https://portal.azure.com) sur l’appareil. Si elle réussit, l’appareil est géré par la nouvelle autorité MDM.
- Si vous rencontrez des problèmes avec des appareils spécifiques, vous pouvez annuler l’inscription puis réinscrire ces appareils pour les connecter à la nouvelle autorité et les gérer dès que possible.