---
title: "Nouveautés dans MDM hybride avec Configuration Manager | Microsoft Docs"
description: "Découvrez les nouvelles fonctionnalités de gestion des appareils mobiles disponibles pour les déploiements hybrides avec Configuration Manager et Intune."
ms.custom: na
ms.date: 06/30/2017
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
ms.translationtype: HT
ms.sourcegitcommit: 1035dbbf944a3a467d637a4a948a75b0946eb711
ms.openlocfilehash: a9e03d4c5b290886bda87fae41e4df362eca1b71
ms.contentlocale: fr-fr
ms.lasthandoff: 07/11/2017

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Nouveautés de la gestion hybride des appareils mobiles avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article fournit des informations sur les nouvelles fonctionnalités de gestion des appareils mobiles disponibles pour les déploiements hybrides avec System Center Configuration Manager et Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilité avec les versions de Configuration Manager  

 Chaque section de cet article répertorie les fonctionnalités hybrides sous trois catégories différentes. Utilisez les indications suivantes pour déterminer la compatibilité des fonctionnalités dans chaque catégorie avec différentes versions de Configuration Manager :  

|Catégories de fonctionnalités|Description|
|-|-|
|**Nouveautés de Microsoft Intune** | En général, toutes les fonctionnalités répertoriées dans cette catégorie doivent fonctionner avec toutes les versions de Configuration Manager, notamment les versions de System Center 2012 R2 Configuration Manager, dans la mesure où ces fonctionnalités nécessitent seulement le service Intune mais aucune fonctionnalité supplémentaire dans Configuration Manager.|
|**Nouveautés de Configuration Manager Technical Preview**| Toutes les fonctionnalités répertoriées dans cette catégorie fonctionnent uniquement avec la version d’évaluation technique spécifiée. Pour tester ces fonctionnalités, vous devez installer la version d’évaluation technique spécifiée dans la description de la fonctionnalité. Pour plus d’informations, consultez [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md).|
|**Nouveautés de Configuration Manager (Current Branch)**| Toutes les fonctionnalités répertoriées dans cette catégorie fonctionnent uniquement avec la version spécifiée de Configuration Manager (Current Branch), comme la version 1511 ou 1602. Si vous utilisez une version antérieure de Configuration Manager pour votre déploiement hybride, vous devez effectuer la mise à niveau vers la version de Configuration Manager (Current Branch) spécifiée dans la description de la fonctionnalité. Pour plus d’informations, consultez [Mettre à niveau vers System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|

## <a name="july-2017"></a>Juillet 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Notification ajoutée pour les versions prises en charge d’Android**

    Une nouvelle notification a été ajoutée pour les versions prises en charge d’Android. Pour plus d’informations, consultez [Fin du support pour Android 4.3 et versions antérieures](#notices).

## <a name="june-2017"></a>Juin 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Changer d’autorité MDM**

  À compter de Configuration Manager version 1610 et de Microsoft Intune version 1705, vous pouvez modifier votre autorité de gestion des appareils mobiles sans avoir à contacter le Support Microsoft et sans devoir annuler l’inscription de vos appareils gérés existants et les réinscrire. Pour plus d’informations, consultez [Changer d’autorité MDM]( /sccm/mdm/deploy-use/change-mdm-authority).

- **Intégration de Managed Browser avec le proxy d’application**

  Intune Managed Browser peut à présent s’intégrer avec le service de proxy d’application Azure AD pour permettre aux utilisateurs d’accéder aux sites web internes, même quand ils travaillent à distance. Les utilisateurs du navigateur entrent simplement l’URL du site comme ils le feraient normalement, et Managed Browser achemine la demande via la passerelle web du proxy d’application proxy. Pour plus d’informations, consultez [Gérer l’accès à Internet à l’aide de stratégies Managed Browser](/intune/app-configuration-managed-browser).

- **L’application Portail d’entreprise pour Android a maintenant une nouvelle expérience utilisateur final pour les stratégies de protection d’application**

  Sur la base des retours des clients, nous avons modifié l’application de portail d’entreprise pour Android afin d’afficher un bouton **Accéder au contenu de l’entreprise**. L’objectif est d’empêcher les utilisateurs finaux d’avoir à passer par le processus d’inscription lorsqu’ils ont seulement besoin d’accéder aux applications qui prennent en charge les stratégies de protection des applications, une fonctionnalité de la gestion des applications mobiles d’Intune. Vous pouvez voir ces modifications sur la page [Nouveautés de l’interface utilisateur de l’application](/intune/whats-new-app-ui).

- **Nouvelle action de menu pour supprimer facilement le portail d’entreprise**

  Sur la base des retours des utilisateurs, l’application de portail d’entreprise pour Android dispose désormais d’une nouvelle action de menu pour initier la suppression du portail d’entreprise à partir de votre appareil. Cette action supprime l’appareil de gestion Intune afin que l’application puisse être supprimée de l’appareil par l’utilisateur. Vous pouvez voir ces modifications sur la page [Nouveautés de l’interface utilisateur de l’application](/intune/whats-new-app-ui) et dans la [documentation utilisateur d’Android](/intune-user-help/unenroll-your-device-from-intune-android).

- **Améliorations apportées à la synchronisation des applications avec Windows 10 Creators Update**

  L’application Portail d’entreprise pour Windows 10 lance désormais automatiquement une synchronisation pour les demandes d’installation d’application pour les appareils avec Windows 10 Creators Update (version 1703). Cela permet de réduire le problème des installations d’application bloquées lorsque l’état est « En attente de synchronisation ». En outre, les utilisateurs peuvent lancer manuellement une synchronisation à partir de l’application. Vous pouvez voir ces modifications sur la page [Nouveautés de l’interface utilisateur de l’application](/intune/whats-new-app-ui).

- **Nouvelle expérience interactive pour le portail d’entreprise Windows 10**

  L’application de portail d’entreprise pour Windows 10 inclut une expérience de procédure pas à pas interactive Intune pour les appareils qui n’ont pas été identifiés ou inscrits. La nouvelle expérience fournit des instructions pas à pas qui guident l’utilisateur lors de l’inscription dans Azure Active Directory (obligatoire pour les fonctionnalités d’accès conditionnel) et l’inscription à la gestion des appareils mobiles (requis pour les fonctionnalités de gestion d’appareils). L’expérience interactive sera accessible à partir de la page d’accueil du portail d’entreprise. Les utilisateurs peuvent continuer à utiliser l’application s’ils ne terminent pas l’inscription, mais seront confrontés à des fonctionnalités limitées.

  Cette mise à jour est uniquement visible sur les appareils exécutant la Mise à jour anniversaire Windows 10 (build 1607) ou une version ultérieure. Vous pouvez voir ces modifications sur la page [Nouveautés de l’interface utilisateur de l’application](/intune/whats-new-app-ui).

- **Améliorations pour les mosaïques de l’application dans l’application de portail d’entreprise pour iOS**

  Nous avons mis à jour le design des mosaïques d’application sur la page d’accueil afin de refléter la couleur de personnalisation que vous définissez pour le portail d’entreprise. Pour plus d’informations, consultez [Nouveautés de l’interface utilisateur de l’application](/intune/whats-new-app-ui).

- **Le sélecteur de compte est désormais disponible pour l’application de portail d’entreprise pour iOS**

  Les utilisateurs d’appareils iOS peuvent voir notre nouveau sélecteur de compte lorsqu’ils se connectent au portail d’entreprise s’ils utilisent leur compte scolaire ou de travail pour se connecter aux autres applications Microsoft. Pour plus d’informations, consultez [Nouveautés de l’interface utilisateur de l’application](/intune/whats-new-app-ui).

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Nouveautés de Configuration Manager Technical Preview 1706

- **Nouveaux paramètres de stratégie de gestion d’application mobile**    

  Les paramètres de stratégie de gestion des applications mobiles (MAM) suivants sont désormais disponibles :

  - **Bloquer la capture d’écran (appareils Android uniquement)** : spécifie que les fonctionnalités de capture d'écran de l'appareil sont bloquées lors de l'utilisation de cette application.
  - **Désactiver la synchronisation des contacts :** empêche l’application d’enregistrer des données sur l’application Contacts native de l’appareil.
  - **Désactiver l’impression :** empêche l’application d’imprimer des données scolaires ou de travail.

  Consultez [Protéger les applications à l’aide des stratégies de protection des applications de Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) pour essayer de nouveaux paramètres de stratégie de protection d’application.

- **Nouveaux paramètres d’élément de configuration Windows** <!-- 1354715 -->    

  De nouveaux éléments de configuration de Windows sont disponibles pour les catégories Paramètres, Appareil, Store et Microsoft Edge. Pour plus d’informations, consultez [Nouveaux paramètres d’élément de configuration Windows](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings).

- **Créer une stratégie de conformité des appareils**    

  Vous pouvez maintenant configurer de nouvelles options pour les stratégies de conformité qui étaient auparavant disponibles uniquement dans la version autonome d’Intune. Pour plus de détails, consultez les [Améliorations apportées aux stratégies de conformité des appareils](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules).

- **Restrictions de l’inscription Android et iOS** <!-- 1290826 -->      

  Les administrateurs peuvent désormais spécifier que les utilisateurs ne peuvent pas inscrire des appareils Android ou iOS personnels dans leur environnement hybride. Cela vous permet de limiter les appareils inscrits aux appareils prédéclarés, appareils d’entreprise ou appareils iOS inscrits avec le programme d’inscription des appareils. Pour plus d’informations, consultez [Restrictions de l’inscription Android et iOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions).

- **Prise en charge des autorités de certification Entrust** <!-- 1350740 -->     

  Configuration Manager prend désormais en charge les autorités de certification Entrust ; Cela permet la remise de certificats PFX pour les appareils inscrits dans Microsoft Intune.    

  Vous pouvez configurer Entrust en tant qu’autorité de certification lors de l’ajout d’un rôle de point d’enregistrement de certificat dans Configuration Manager. Lorsque vous ajoutez un nouveau profil de certificat qui émet des certificats PFX, vous pouvez sélectionner une autorité de certification Microsoft ou Entrust.

  **Problème connu** : dans la Technical Preview 1706, les certificats PFX ne sont pas émis pour les autorités de certification Microsoft. Cela n’affecte pas les certificats PFX importés ou les profils SCEP.

- **Prise en charge de Cisco (IPsec) pour les profils VPN macOS**  <!-- 1321367 -->    

  Vous pouvez créer un profil VPN macOS avec Cisco (IPsec) comme type de connexion. Pour plus d’informations, consultez [Créer des profils VPN](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).


## <a name="april-2017"></a>Avril 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Mes apps disponible pour Managed Browser**

  Mes apps Microsoft bénéficie à présent d’une meilleure prise en charge dans Managed Browser. Les utilisateurs Managed Browser qui ne sont pas ciblés pour la gestion sont directement redirigés vers le service Mes apps, où ils peuvent accéder à leurs applications SaaS configurées par l’administrateur. Les utilisateurs ciblés pour la gestion Intune peuvent toujours accéder à Mes apps à partir du signet Managed Browser intégré.

- **Nouvelles icônes pour Managed Browser et le portail d’entreprise**

  Managed Browser reçoit des icônes mises à jour pour les versions iOS et Android de l’application. La nouvelle icône contient le badge Intune mis à jour qui devient plus cohérent avec les autres applications dans Enterprise Mobility + Security (EM+S). Vous pouvez voir la nouvelle icône Managed Browser dans la page sur les [nouveautés de l’interface utilisateur pour les applications Intune](/intune/whats-new/whats-new-in-intune-app-ui.md).

  Le portail d’entreprise reçoit également des icônes mises à jour pour les versions Android, iOS et Windows de l’application pour améliorer la cohérence avec les autres applications EM+S. Ces icônes seront disponibles progressivement sur les différentes plateformes, sur une période allant d’avril à fin mai.

- **Indicateur de progression de la connexion dans le Portail d’entreprise Android**

  Une mise à jour de l’application Portail d’entreprise Android affiche un indicateur de progression de la connexion lorsque l’utilisateur lance ou rouvre l’application. L’indicateur passe par différents états (en commençant par « Connexion en cours... », « Connexion en cours... », puis « Vérification des exigences de sécurité... ») avant d’autoriser l’utilisateur à accéder à l’application. Vous pouvez voir les nouveaux écrans de l’application Portail d’entreprise pour Android dans la page sur les [nouveautés de l’interface utilisateur pour les applications Intune](/intune/whats-new/whats-new-in-intune-app-ui.md).

- **Bloquer l’accès des applications à SharePoint Online**

  Vous pouvez maintenant créer une stratégie d’accès conditionnel basée sur l’application pour empêcher les applications auxquelles aucune stratégie de protection d’application n’a été appliquée d’accéder à [SharePoint Online](/InTune/deploy-use/mam-ca-for-sharepoint-online). Dans le cadre d’un scénario faisant appel à l’accès conditionnel basé sur l’application, vous pouvez spécifier les applications que vous souhaitez autoriser à accéder à SharePoint Online à l’aide du portail Azure.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Nouveautés de Configuration Manager Technical Preview 1704

- **Configurer des applications Android avec des stratégies de configuration des applications**

  Vous pouvez utiliser des stratégies de configuration des applications disponibles dans System Center Configuration Manager (Configuration Manager) pour distribuer les paramètres préconfigurés quand un utilisateur exécute une application sur des appareils Android for Work. Les stratégies de configuration des applications Android sont disponibles uniquement sur les appareils Android for Work et s’appliquent aux applications approuvées du magasin Play for Work. Pour plus d’informations sur la façon de tester cette fonctionnalité, consultez [Configurer des applications Android avec des stratégies de configuration des applications](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies).

## <a name="march-2017"></a>Mars 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Nouvelle expérience utilisateur pour l’application Portail d’entreprise pour Android**

  L’application Portail d’entreprise pour Android a une interface utilisateur d’apparence plus moderne. Les mises à jour importantes sont :

  - Couleurs : les en-têtes des onglets du portail d’entreprise sont de la couleur définie dans la personnalisation.
  - Applications : dans l’onglet **Applications**, les boutons **Applications à la une** et **Toutes les applications** ont été mis à jour.
  - Rechercher : Dans l’onglet **Applications**, le bouton **Rechercher** est un bouton d’action flottant.
  - Navigation dans les applications : la vue **Toutes les applications** montre une vue à onglets avec **À la une**, **Toutes** et **Catégories** pour faciliter la navigation.
  - Prise en charge : les onglets **Mes appareils** et **Contacter le service informatique** ont été mis à jour de façon à améliorer la lisibilité.

  Pour plus d’informations sur ces modifications, consultez [Mises à jour de l’interface utilisateur pour les applications Intune de l’utilisateur final](/intune/whats-new/whats-new-in-intune-app-ui).

- **Script de signature pour le portail d’entreprise Windows 10**

  Si vous avez besoin de télécharger et charger de façon indépendante l’application Portail d’entreprise Windows 10, vous pouvez désormais utiliser un script pour simplifier et fluidifier le processus de signature des applications pour votre organisation.  Pour télécharger le script et les instructions pour son utilisation, consultez [Script de signature Microsoft Intune pour le portail d’entreprise Windows 10](https://aka.ms/win10cpscript) sur la Galerie TechNet. Pour plus d’informations sur cette annonce, consultez [Mise à jour de votre application Portail d’entreprise Windows 10](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) sur le Blog de l’équipe de support technique Intune.

- **Prise en charge améliorée pour les utilisateurs Android basés en Chine**

  En raison de l’absence du Google Play Store en Chine, les appareils Android doivent obtenir des applications des places de marché chinoises. Le portail d’entreprise prend en charge ce flux de travail en redirigeant les utilisateurs Android en Chine pour télécharger les applications Portail d’entreprise et Outlook à partir de Stores d’applications locaux. Ceci améliore l’expérience utilisateur quand les stratégies d’accès conditionnel sont activées, à la fois pour la gestion des appareils mobiles et pour la gestion des applications mobiles. Les applications Portail d’entreprise et Outlook pour Android sont disponibles sur les magasins d’applications chinois suivants :

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Vérifiez que vos applications de portail d’entreprise sont à jour**

  En décembre 2016, nous avons publié une mise à jour qui permettait d’appliquer l’authentification multifacteur (MFA) sur un groupe d’utilisateurs lors de l’inscription d’un appareil iOS, Android, Windows 8.1+ ou Windows Phone 8.1+. Cette fonctionnalité ne peut pas être utilisée sans certaines versions de référence de l’application Portail d’entreprise pour Android (v5.0.3419.0+) et iOS (v2.1.17+).

  Les fonctionnalités de gestion d’Intune sont en constante évolution et de nombreuses améliorations ont nécessité des mises à jour des applications Portail d’entreprise sur toutes les plateformes prises en charge. Par conséquent, nous vous recommandons d’installer les dernières versions des applications Portail d’entreprise sur les appareils pour bénéficier des améliorations d’Intune et d’une expérience utilisateur optimale.

  >[!Tip]
  > Demandez à vos utilisateurs de configurer la mise à jour automatique des applications sur leurs appareils à partir de l’App Store approprié. Si vous avez rendu l’application Portail d’entreprise Android disponible sur un partage réseau, vous pouvez télécharger la dernière version à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=49140).

- **Microsoft Teams est maintenant activé pour la gestion des applications mobiles sur iOS et Android**

  Les applications Microsoft Teams pour iOS et Android sont désormais activées avec les fonctionnalités de gestion des applications mobiles Intune, ce qui permet à vos équipes de changer librement d’appareil tout en garantissant que les conversations et les données d’entreprise sont protégées à chaque changement. Pour plus d’informations, consultez l’[annonce de Microsoft Teams](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) sur le blog Enterprise Mobility and Security.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Nouveautés de Configuration Manager Technical Preview 1703

- **Prise en charge supplémentaire des scénarios du Programme d’achat en volume (VPP) Apple**

   À compter de la version Technical Preview 1703, vous disposez de la prise en charge des scénarios VPP suivants :

   - Licences d’appareil : les applications prenant en charge les licences d’appareil et qui sont déployées sur des regroupements d’appareils ne nécessitent désormais qu’une seule licence par appareil.  Auparavant, vous deviez utiliser une licence pour chaque utilisateur sur un appareil. Pour plus d’informations, consultez [Déployer des applications iOS achetées en volume sur des regroupements d’appareils](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Utilisation de plusieurs jetons VPP pour un locataire hybride unique avec les deux jetons utilisés pour gérer les applications VPP.
   - Utilisation de jetons scolaires VPP avec la possibilité de faire la distinction entre les jetons d’entreprise et scolaires.

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

Les fonctionnalités suivantes qui étaient précédemment disponibles dans les versions Configuration Manager Technical Preview sont maintenant disponibles dans les déploiements hybrides avec Intune et Configuration Manager (Current Branch) version 1702.

- [Prise en charge d’Android for Work](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [Paramètres de conformité des applications non conformes](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [Création et distribution de certificats PFX et prise en charge de S/MIME](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [es versions Android et iOS ne peuvent plus être ciblées dans les Assistants de création pour la gestion MDM hybride](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

Les fonctionnalités hybrides supplémentaires suivantes sont également incluses dans la version 1702 de Configuration Manager (Current Branch) :

- **Prise en charge améliorée du Programme d’achat en volume Apple (VPP)**

  - Vous pouvez désormais déployer des applications sous licence sur des appareils ainsi que des utilisateurs. En fonction de la capacité des applications à prendre en charge les licences d’appareils, une licence appropriée est réclamée lors du déploiement, comme suit :

    | Version de Configuration Manager | L’application prend-elle en charge les licences d’appareil ? | Type de regroupement de déploiement | Licence demandée |
    |-|-|-|-|
    |Antérieure à 1702|Oui|utilisateur|Licence utilisateur|
    |Antérieure à 1702|Non|utilisateur|Licence utilisateur|
    |Antérieure à 1702|Oui|Appareil|Licence utilisateur|
    |Antérieure à 1702|Non|Appareil|Licence utilisateur|
    |1702 et versions ultérieures|Oui|utilisateur|Licence utilisateur|
    |1702 et versions ultérieures|Non|utilisateur|Licence utilisateur|
    |1702 et versions ultérieures|Oui|Appareil|Licence d’appareil|
    |1702 et versions ultérieures|Non|Appareil|Licence utilisateur|

  - Désormais, vous pouvez également déployer et suivre les applications que vous avez achetées via le Programme d’achat en volume iOS pour l’éducation.

  - Vous pouvez maintenant associer plusieurs jetons de programme d’achat en volume Apple à Configuration Manager.

  Pour plus d’informations sur les applications achetées en volume, consultez [Gérer des applications iOS achetées en volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

- **Prise en charge des applications métier dans Windows Store pour Entreprises**

  Vous pouvez désormais synchroniser des applications métier personnalisées à partir de Windows Store pour Entreprises.

- **Nouveaux outils de surveillance de protection contre les menaces mobiles**

    Vous disposez maintenant de nouveaux moyens pour surveiller l’état de conformité avec votre fournisseur de services de protection contre les menaces mobiles.

    Pour plus d’informations, consultez [Comment surveiller la conformité de la protection contre les menaces mobiles](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).

## <a name="february-2017"></a>Février 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Modernisation du site web du portail d’entreprise**

  Le site web du portail d’entreprise prend en charge les applications destinées aux utilisateurs ne disposant pas d’appareils gérés. Le site web s’aligne sur les autres produits et services Microsoft grâce à un nouveau jeu de couleurs contrastées, des illustrations dynamiques et un « menu hamburger » qui fournit les coordonnées du support technique et des informations sur les appareils gérés existants. La nouvelle page d’accueil réorganisée met en évidence les applications disponibles aux utilisateurs, avec des tapis roulants pour les applications proposées et les applications récemment mises à jour. Vous pouvez trouver des images antérieures et postérieures sur la page [Mises à jour de l’interface utilisateur](/intune/whats-new/whats-new-in-intune-app-ui).

- **Nouvelle adresse du serveur MDM pour les appareils Windows**

  L’adresse du serveur MDM utilisée pour inscrire des appareils Windows et Windows Phone est maintenant enrollment.manage.microsoft.com (au lieu de manage.microsoft.com ). Demandez à votre utilisateur d’employer enrollment.manage.microsoft.com comme adresse du serveur MDM, lors de l’inscription d’un appareil Windows ou Windows Phone. Cette mise à jour requiert également le remplacement d’un enregistrement CNAME DNS qui redirige EnterpriseEnrollment.contoso.com vers manage.microsoft.com, par un enregistrement CNAME DNS qui redirige EnterpriseEnrollment.contoso.com vers EnterpriseEnrollment-s.manage.microsoft.com. Pour plus d’informations sur cette modification, consultez la page http://aka.ms/intuneenrollsvrchange.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Nouveautés de Configuration Manager Technical Preview 1702

- **Prise en charge d’Android for Work**

  Vous pouvez désormais gérer les appareils Android à l’aide d’Android for Work dans les environnements de gestion des appareils mobiles hybrides à l’aide de Configuration Manager Technical Preview 1702. Les appareils Android pris en charge peuvent maintenant être inscrits comme appareils Android for Work, ce qui crée un profil professionnel sur l’appareil sur lequel les applications approuvées dans Play for Work peuvent être déployées. Vous pouvez également configurer et déployer des éléments de configuration, des stratégies de conformité et des profils d’accès aux ressources pour ces appareils. Pour plus d’informations, consultez [Prise en charge d’Android for Work](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Paramètres de conformité des applications non conformes**

  Vous pouvez maintenant créer des règles d’applications non conformes pour les applications Android et iOS dans les stratégies de conformité. Si des appareils disposent des applications spécifiées, ils sont marqués « non conformes » et perdent l’accès aux ressources d’entreprise en fonction des stratégies d’accès conditionnel en place. Pour plus d’informations, consultez [Améliorations apportées aux stratégies de conformité des appareils pour l’accès conditionnel](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **Création et distribution de certificats PFX et prise en charge de S/MIME**

  Vous pouvez désormais créer et déployer des certificats PFX sur les utilisateurs dans un environnement hybride. Ces certificats peuvent ensuite être utilisés pour le chiffrement et le déchiffrement S/MIME par les appareils que l’utilisateur a inscrits. Pour plus d’informations, consultez [Créer des certificats PFX avec prise en charge S/MIME](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Prise en charge des paramètres de configuration supplémentaires iOS**
   
    Vous disposez désormais de 42 paramètres iOS supplémentaires que vous pouvez configurer dans le cadre d’un élément de configuration. La plupart des paramètres (35 au total) ont été ajoutés pour les appareils iOS supervisés. Pour plus d’informations, consultez [Nouveaux paramètres de conformité pour les appareils iOS](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).

## <a name="january-2017"></a>Janvier 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Prise en charge d'Android 7.1.1**

  Intune prend désormais en charge entièrement et gère Android 7.1.1.

- **Résoudre les problèmes dans lesquels des appareils iOS sont inactifs ou la console d’administration ne peut pas communiquer avec eux**

  Lorsque les appareils des utilisateurs perdent le contact avec Intune, vous pouvez utiliser les nouvelles étapes de dépannage pour les aider à récupérer l’accès aux ressources d’entreprise. Voir [Résoudre les problèmes dans lesquels des appareils iOS sont inactifs ou la console d’administration ne peut pas communiquer avec eux](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Nouveautés de Configuration Manager Technical Preview 1701

- **es versions Android et iOS ne peuvent plus être ciblées dans les Assistants de création pour la gestion MDM hybride**

  Depuis Technical Preview 1701, vous n’avez plus besoin de cibler des versions Android et iOS spécifiques quand vous créez des stratégies et des profils pour des appareils gérés par Intune dans le cadre d’une gestion des appareils mobiles (MDM) hybride. Grâce à cette modification, les déploiements hybrides peuvent prendre en charge plus rapidement les nouvelles versions Android et iOS sans avoir besoin d’une nouvelle version de Configuration Manager ou d’une extension. Pour en savoir plus, consultez [Les versions Android et iOS ne peuvent plus être ciblées dans les Assistants de création](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## <a name="notices"></a>Remarques

### <a name="end-of-support-for-android-43-and-lower"></a>Fin du support pour Android 4.3 et versions antérieures
<!---1171127--->
*6 juillet 2017*

Les applications gérées et l’application Portail d’entreprise pour Android nécessiteront Android 4.4 et versions ultérieures accéder aux ressources d’entreprise. Les appareils qui ne sont pas mis à jour avant le début du mois d’octobre ne pourront plus accéder au Portail d’entreprise ou à ces applications. En décembre, tous les appareils inscrits seront mis hors service, provoquant ainsi la perte de l’accès aux ressources d’entreprise. Si vous utilisez des stratégies de protection d’application sans la Gestion des données de référence, les applications ne recevront pas de mises à jour et la qualité de l’expérience diminuera avec le temps.


### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 et System Center 2012 R2 Configuration Manager (RTM) : fin de la prise en charge de la gestion hybride des appareils mobiles le 10 avril 2017
*11 janvier 2017*

La prise en charge de System Center 2012 Configuration Manager SP1 et de System Center 2012 R2 Configuration Manager RTM a pris fin le 12 juillet 2016. Par conséquent, la prise en charge de ces versions se connectant au service Microsoft Intune pour la gestion hybride des appareils mobiles prendra fin le 10 avril 2017. Après cette date, la gestion hybride des appareils mobiles cessera de fonctionner avec ces versions. Les appareils gérés deviendront essentiellement non gérés car le connecteur Intune ne se connectera plus au service Intune. Les données de Configuration Manager (par exemple, les stratégies et les applications) ne seront plus transmises à Intune et les données d’appareil mobile ne parviendront plus à Configuration Manager jusqu’à ce qu’une mise à niveau soit appliquée.

Si vous exécutez un déploiement hybride avec Configuration Manager 2012 SP1 ou R2 RTM, nous vous recommandons de mettre à niveau vers Configuration Manager (Current Branch) ou vers le dernier service pack pris en charge pour Configuration Manager 2012 (R2 SP1 ou SP2) avant le 10 avril 2017 afin d’éviter toute interruption du service.

Ressources supplémentaires :
-   [Mettre à niveau vers System Center Configuration Manager (Current Branch)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [Planification de la mise à niveau vers System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [Planification de la mise à niveau vers System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Chargement du portail d’entreprise Windows Phone 8 obsolète
*25 octobre 2016*

La possibilité de charger une application Portail d’entreprise signée a été supprimée de la console Configuration Manager, car le support technique Intune est déprécié pour Windows 8, Windows Phone 8 et Windows RT, le support pour le portail d’entreprise Windows Phone 8 se termine au mois de novembre.  Les appareils Windows 8, Windows Phone 8 et Windows RT qui sont déjà inscrits continueront à être pris en charge, mais l’inscription d’appareils supplémentaires auprès de ces plateformes ne sera pas prise en charge.


### <a name="see-also"></a>Voir aussi

- [Anciennes fonctionnalités de gestion des appareils mobiles hybride](whats-new-hybrid-archive.md)
- [Nouveautés de MDM dans System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)

