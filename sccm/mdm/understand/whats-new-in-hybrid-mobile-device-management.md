---
title: "Nouveautés de la gestion hybride des appareils mobiles | Documents Microsoft"
description: "Découvrez les nouvelles fonctionnalités de gestion des appareils mobiles disponibles pour les déploiements hybrides avec System Center Configuration Manager et Intune."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: 40
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 69d3e7d51911d6195c2f62a5e81c0faca38ed306
ms.openlocfilehash: a8fd3c24f3267ea451f4c94854e8577046efaeca
ms.lasthandoff: 02/27/2017

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Nouveautés de la gestion hybride des appareils mobiles avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article fournit des informations sur les nouvelles fonctionnalités de gestion des appareils mobiles disponibles pour les déploiements hybrides avec System Center Configuration Manager et Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilité avec les versions de Configuration Manager  

 Chaque section de cet article répertorie les fonctionnalités hybrides sous 3 catégories différentes. Utilisez les indications suivantes pour déterminer la compatibilité des fonctionnalités dans chaque catégorie avec différentes versions de Configuration Manager :  

|Catégories de fonctionnalités|Description|
|-|-|
|**Nouveautés de Microsoft Intune** | En général, toutes les fonctionnalités répertoriées dans cette catégorie doivent fonctionner avec toutes les versions de Configuration Manager, notamment les versions de System Center 2012 R2 Configuration Manager, dans la mesure où ces fonctionnalités nécessitent seulement le service Intune mais aucune fonctionnalité supplémentaire dans Configuration Manager.|
|**Nouveautés de Configuration Manager Technical Preview**| Toutes les fonctionnalités répertoriées dans cette catégorie fonctionnent uniquement avec la version d’évaluation technique spécifiée. Pour tester ces fonctionnalités, vous devez installer la version d’évaluation technique spécifiée dans la description de la fonctionnalité. Pour plus d’informations, consultez [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md).|
|**Nouveautés de Configuration Manager (Current Branch)**| Toutes les fonctionnalités répertoriées dans cette catégorie fonctionnent uniquement avec la version spécifiée de Configuration Manager (Current Branch), comme la version 1511 ou 1602. Si vous utilisez une version antérieure de Configuration Manager pour votre déploiement hybride, vous devez effectuer la mise à niveau vers la version de Configuration Manager (Current Branch) spécifiée dans la description de la fonctionnalité. Pour plus d’informations, consultez [Mettre à niveau vers System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|

## <a name="new-hybrid-features-in-february-2017"></a>Nouvelles fonctionnalités hybrides disponibles à partir de février 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

Les fonctionnalités Intune suivantes introduites en février 2017 fonctionnent dans les déploiements hybrides :

- **Modernisation du site web du portail d’entreprise**

  Le site web du portail d’entreprise prend en charge les applications destinées aux utilisateurs ne disposant pas d’appareils gérés. Le site web s’aligne sur les autres produits et services Microsoft grâce à un nouveau jeu de couleurs contrastées, des illustrations dynamiques et un « menu hamburger » qui fournit les coordonnées du support technique et des informations sur les appareils gérés existants. La nouvelle page d’accueil réorganisée met en évidence les applications disponibles aux utilisateurs, avec des tapis roulants pour les applications proposées et les applications récemment mises à jour. Vous pouvez trouver des images antérieures et postérieures sur la page [Mises à jour de l’interface utilisateur](/intune/whats-new/whats-new-in-intune-app-ui).

- **Nouvelle adresse du serveur MDM pour les appareils Windows**

  L’adresse du serveur MDM utilisée pour inscrire des appareils Windows et Windows Phone est maintenant enrollment.manage.microsoft.com (au lieu de manage.microsoft.com ). Demandez à votre utilisateur d’employer enrollment.manage.microsoft.com comme adresse du serveur MDM, lors de l’inscription d’un appareil Windows ou Windows Phone. Cette mise à jour requiert également le remplacement d’un enregistrement CNAME DNS qui redirige EnterpriseEnrollment.contoso.com vers manage.microsoft.com, par un enregistrement CNAME DNS qui redirige EnterpriseEnrollment.contoso.com vers EnterpriseEnrollment-s.manage.microsoft.com. Pour plus d’informations sur cette modification, consultez la page http://aka.ms/intuneenrollsvrchange.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Nouveautés de Configuration Manager Technical Preview 1702

- **Prise en charge d’Android for Work**

  Vous pouvez désormais gérer les appareils Android à l’aide d’Android for Work dans les environnements de gestion des appareils mobiles hybrides à l’aide de Configuration Manager Technical Preview 1702. Les appareils Android pris en charge peuvent maintenant être inscrits comme appareils Android for Work, ce qui crée un profil professionnel sur l’appareil sur lequel les applications approuvées dans Play for Work peuvent être déployées. Vous pouvez également configurer et déployer des éléments de configuration, des stratégies de conformité et des profils d’accès aux ressources pour ces appareils.

- **Paramètres de conformité des applications non conformes**

  Vous pouvez maintenant créer des règles d’applications non conformes pour les applications Android et iOS dans les stratégies de conformité. Si des appareils disposent des applications spécifiées, ils sont marqués « non conformes » et perdent l’accès aux ressources d’entreprise en fonction des stratégies d’accès conditionnel en place.

- **Création et distribution de certificats PFX et prise en charge de S/MIME**

  Vous pouvez désormais créer et déployer des certificats PFX sur les utilisateurs dans un environnement hybride. Ces certificats peuvent ensuite être utilisés pour le chiffrement et le déchiffrement S/MIME par les appareils que l’utilisateur a inscrits.

## <a name="new-hybrid-features-in-january-2017"></a>Nouvelles fonctionnalités hybrides en janvier 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

Les fonctionnalités Intune suivantes introduites en janvier 2017 fonctionnent dans les déploiements hybrides :

- **Prise en charge d'Android 7.1.1**

  Intune prend désormais en charge entièrement et gère Android 7.1.1.

- **Résoudre les problèmes dans lesquels des appareils iOS sont inactifs ou la console d’administration ne peut pas communiquer avec eux**

  Lorsque les appareils des utilisateurs perdent le contact avec Intune, vous pouvez utiliser les nouvelles étapes de dépannage pour les aider à récupérer l’accès aux ressources d’entreprise. Voir [Résoudre les problèmes dans lesquels des appareils iOS sont inactifs ou la console d’administration ne peut pas communiquer avec eux](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Nouveautés de Configuration Manager Technical Preview 1701

- **es versions Android et iOS ne peuvent plus être ciblées dans les Assistants de création pour la gestion MDM hybride**

  Depuis Technical Preview 1701, vous n’avez plus besoin de cibler des versions Android et iOS spécifiques quand vous créez des stratégies et des profils pour des appareils gérés par Intune dans le cadre d’une gestion des appareils mobiles (MDM) hybride. Grâce à cette modification, les déploiements hybrides peuvent prendre en charge plus rapidement les nouvelles versions Android et iOS sans avoir besoin d’une nouvelle version de Configuration Manager ou d’une extension. Pour en savoir plus, consultez [Les versions Android et iOS ne peuvent plus être ciblées dans les Assistants de création](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## <a name="new-hybrid-features-in-december-2016"></a>Nouvelles fonctionnalités hybrides en décembre 2016

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

Les fonctionnalités Intune suivantes introduites en décembre 2016 fonctionnent dans les déploiements hybrides :

- **L’authentification multifacteur sur l’inscription est déplacée dans le portail Azure**

  Auparavant, vous deviez accéder à la console Intune ou à la console Configuration Manager pour définir l’authentification multifacteur pour les inscriptions Intune. Avec cette fonctionnalité mise à jour, vous vous connectez maintenant au [portail Microsoft Azure] (https://manage.windowsazure.com) en utilisant vos informations d’identification Intune et vous configurez les paramètres de l’authentification multifacteur via Azure AD. Pour plus d’informations, consultez [Authentification multifacteur pour Microsoft Intune] (https://aka.ms/mfa_ad).

- **Application Portail d’entreprise pour Android maintenant disponible en Chine**

  L’application Portail d’entreprise pour Android est maintenant disponible en Chine. En raison de l’absence de Google Play Store en Chine, les appareils Android doivent obtenir les applications des places de marché d’applications chinoises. L’application Portail d’entreprise pour Android est disponible pour téléchargement sur les magasins suivants :

  -    [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  -    [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  -    [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  -    [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)
  -    [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)

  L’application Portail d’entreprise pour Android utilise Google Play Services pour communiquer avec le service Microsoft Intune. Comme Google Play Services n’est pas encore disponible en Chine, la réalisation des tâches suivantes peut prendre jusqu’à 8 heures.

  | Configuration de la console d’administration de Configuration Manager | Application Portail d’entreprise Intune pour Android | Site web du portail d’entreprise Intune |
  |----|----|----|        
  | Mettre hors service/réinitialiser (supprimer toutes les données)    | Supprimer un appareil distant | Supprimer un appareil (local et distant) |
  | Mettre hors service/réinitialiser (supprimer les données d’entreprise)    | Réinitialiser un appareil | Réinitialiser un appareil|
  | Déploiements d’applications nouvelles ou mises à jour | Installer des applications métier disponibles | Réinitialisation du code secret d’un appareil|
  | Verrouillage à distance    | | |
  | Réinitialiser le code secret | | |        


## <a name="new-hybrid-features-in-november-2016"></a>Nouvelles fonctionnalités hybrides en novembre 2016

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

Les fonctionnalités Intune suivantes introduites en novembre 2016 fonctionnent dans les déploiements hybrides :

- **Nouveau portail d’entreprise Microsoft Intune disponible pour les appareils Windows 10**

  Microsoft a publié une nouvelle [application Portail d’entreprise pour les appareils Windows 10](https://www.microsoft.com/store/apps/9wzdncrfj3pz). Cette application, qui tire parti du nouveau format Windows 10 universel, fournit une nouvelle expérience utilisateur qui est identique sur tous les appareils Windows 10, qu’il s’agisse de PC ou de mobiles, tout en offrant exactement les mêmes fonctionnalités que celles fournies par les applications Portail d’entreprise précédentes.

  La nouvelle application tire parti des fonctionnalités de la plateforme, comme l’authentification unique (SSO) et l’authentification basée sur les certificats sur les appareils Windows 10. L’application est disponible auprès du Windows Store en tant que mise à niveau des installations existantes de portail d’entreprise Windows 8.1 et de portail d’entreprise Windows Phone 8.1. Pour plus d’informations, consultez le [blog de l’équipe de support Intune](http://aka.ms/intunecp_universalapp).

  La nouvelle application Portail d’entreprise affiche également toutes les applications du Windows Store pour Entreprises marquées comme étant **disponibles** dans la console Configuration Manager.


### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

Les fonctionnalités suivantes qui étaient précédemment disponibles dans les versions Configuration Manager Technical Preview sont maintenant disponibles dans les déploiements hybrides avec Intune et Configuration Manager (Current Branch) version 1610.

* [Paramètres supplémentaires et expérience améliorée pour les éléments de configuration](/sccm/core/plan-design/changes/whats-new-in-version-1610#new-compliance-settings-for-configuration-items)
* [Paramètres supplémentaires pour les profils DEP](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Applications payantes dans le Windows Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Types de connexion natifs pour les profils VPN Windows 10](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Graphiques de conformité Intune](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [Demande de synchronisation de stratégie à partir de la console](/sccm/mdm/deploy-use/sync-intune-device)
* [Paramètres de configuration de Windows Defender](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

Les fonctionnalités hybrides supplémentaires suivantes sont également incluses dans la version 1610 de Configuration Manager (Current Branch) :

- **Nombre accru d’appareils inscrits**

  Vous pouvez maintenant permettre aux utilisateurs d’inscrire jusqu’à 15 appareils. La limite précédente était de 5 appareils par utilisateur.


- **Prise en charge supplémentaire de la sécurité**

  En plus d’Administrateur complet, les rôles de sécurité intégrés suivants ont maintenant un accès complet aux éléments dans le nœud Appareils d’entreprise, notamment Appareils prédéclarés, Profils d’inscription iOS et Profils d’inscription Windows :

    - Gestionnaire de ressources
    - Gestionnaire d’accès aux ressources de l’entreprise

  L’accès en lecture seule à ces zones de la console Configuration Manager est toujours accordé au rôle Analyste en lecture seule.

- **Accès VPN à déclenchement automatique à partir d’applications de protection des informations Windows**

  Vous pouvez ajouter un domaine principal de protection des informations Windows aux profils VPN de Windows 10 qui provoque le déclenchement automatique d’une connexion VPN par les applications associées quand elles sont exécutées sur l’appareil. Cette option est disponible seulement quand vous choisissez un type de connexion natif.

- **Accès conditionnel pour les profils VPN Windows 10**

    Vous pouvez maintenant exiger que les appareils Windows 10 inscrits dans Azure Active Directory soient conformes pour pouvoir avoir un accès VPN via les profils VPN Windows 10 créés dans la console Configuration Manager. Ceci est possible via la nouvelle case à cocher **Activer l’accès conditionnel pour cette connexion VPN** dans la page Méthode d’authentification de l’Assistant Profil VPN et les propriétés de profil VPN pour les profils VPN Windows 10. Cette option est disponible seulement quand vous choisissez un type de connexion natif.

    Vous pouvez également spécifier un certificat distinct pour l’authentification unique si vous activez l’accès conditionnel pour le profil.


## <a name="notices"></a>Remarques

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 et System Center 2012 R2 Configuration Manager (RTM) : fin de la prise en charge de la gestion hybride des appareils mobiles le 10 avril 2017

*11 janvier 2017*

La prise en charge de System Center 2012 Configuration Manager SP1 et de System Center 2012 R2 Configuration Manager RTM a pris fin le 12 juillet 2016. Par conséquent, la prise en charge de ces versions se connectant au service Microsoft Intune pour la gestion hybride des appareils mobiles prendra fin le 10 avril 2017. Après cette date, la gestion hybride des appareils mobiles cessera de fonctionner avec ces versions. Les appareils gérés deviendront essentiellement non gérés car le connecteur Intune ne se connectera plus au service Intune. Les données de Configuration Manager (par exemple, les stratégies et les applications) ne seront plus transmises à Intune et les données d’appareil mobile ne parviendront plus à Configuration Manager jusqu’à ce qu’une mise à niveau soit appliquée.

Si vous exécutez un déploiement hybride avec Configuration Manager 2012 SP1 ou R2 RTM, nous vous recommandons de mettre à niveau vers Configuration Manager (Current Branch) ou vers le dernier service pack pris en charge pour Configuration Manager 2012 (R2 SP1 ou SP2) avant le 10 avril 2017 afin d’éviter toute interruption du service.

Ressources supplémentaires :
-    [Mettre à niveau vers System Center Configuration Manager (Current Branch)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-    [Planification de la mise à niveau vers System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-    [Planification de la mise à niveau vers System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Chargement du portail d’entreprise Windows Phone 8 obsolète
*25 octobre 2016*

La possibilité de charger une application Portail d’entreprise signée a été supprimée de la console Configuration Manager, car le support technique Intune est déprécié pour Windows 8, Windows Phone 8 et Windows RT, le support pour le portail d’entreprise Windows Phone 8 se termine au mois de novembre.  Les appareils Windows 8, Windows Phone 8 et Windows RT qui sont déjà inscrits continueront à être pris en charge, mais l’inscription d’appareils supplémentaires auprès de ces plateformes ne sera pas prise en charge.


### <a name="see-also"></a>Voir aussi

- [Anciennes fonctionnalités de gestion des appareils mobiles hybride](whats-new-hybrid-archive.md)
- [Nouveautés de MDM dans System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)

