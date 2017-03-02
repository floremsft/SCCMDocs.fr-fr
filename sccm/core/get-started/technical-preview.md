---
title: Version Technical Preview pour System Center Configuration Manager | Microsoft Docs
description: "Découvrez la version Technical Preview qui vous permet de tester les nouvelles fonctions et fonctionnalités de System Center Configuration Manager."
ms.custom: na
ms.date: 2/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 4b1daa727477b1273cdbee1bc7e3ac8af5911ff0
ms.openlocfilehash: 4703178c5ce3e23cb9d2e4557466fcec571c2983
ms.lasthandoff: 02/22/2017


---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

**Bienvenue dans System Center Configuration Manager Technical Preview**. Cette rubrique fournit des détails sur la version Preview qui présente de nouvelles fonctions et fonctionnalités que nous développons actuellement. Chaque version Technical Preview inaugure des nouvelles fonctionnalités qui ne sont pas présentes dans la version Current Branch de System Center Configuration Manager au moment où la version Technical Preview est publiée. Ces fonctionnalités seront incluses dans une mise à jour de la version Current Branch, mais avant de finaliser et d’ajouter les fonctionnalités, nous souhaitons que vous puissiez les tester et nous faire part de vos commentaires.  

 S’agissant d’une version Technical Preview, les détails et les fonctionnalités sont susceptibles de changer.  

 Cette rubrique contient des informations qui s’appliquent à toutes les versions Technical Preview et répertorie également chaque nouvelle fonctionnalité ainsi que la version Technical Preview où la fonctionnalité apparaît pour la première fois, par exemple la version 1701 pour le mois de janvier 2017. Ces fonctionnalités sont détaillées dans des rubriques distinctes dédiées à chaque version Preview.  

 Pour plus d’informations sur les nouveautés de la version Current Branch de Configuration Manager, consultez [Nouveautés de System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="a-namebkmkreqsa-requirements-and-limitations-for-the-technical-preview"></a><a name="bkmk_reqs"></a> Configuration requise et limitations pour Technical Preview  

> [!IMPORTANT]     
>  La licence de la version Technical Preview est destinée uniquement aux environnements de laboratoire.  Microsoft peut ne pas fournir de support technique et certaines fonctionnalités peuvent ne pas être disponibles dans la version Preview du logiciel. En outre, la version Preview du logiciel peut utiliser des normes de sécurité, de confidentialité, d’accessibilité, de disponibilité et de fiabilité réduites ou différentes par rapport aux logiciels fournis dans le commerce.  

 La plupart des conditions préalables à l’utilisation du produit sont abordées dans [Configurations prises en charge pour System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). Les exceptions suivantes s'appliquent aux versions Technical Preview :  

-   Chaque installation reste active pendant 90 jours, puis devient inactive.  

-   L'anglais est la seule langue prise en charge.  

-   Seul un site principal autonome est pris en charge. Il n'existe aucune prise en charge pour un site d'administration centrale, plusieurs sites principaux ou des sites secondaires.  

-   Seules les versions suivantes de SQL Server sont prises en charge :  

    -   SQL Server 2016 (sans Service Pack et versions ultérieures)
    -   SQL Server 2014 (sans Service Pack et versions ultérieures)
    -   SQL Server 2012 (avec Service Pack 2 ou version ultérieure)


-   Le site prend en charge jusqu'à 10 clients, qui doivent exécuter l'un des systèmes d'exploitation suivants :  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 8  
      -   Windows 7  


-   Seuls les indicateurs d'installation (commutateurs) suivants sont pris en charge :  

    -   **/silent**  
    -   **/testdbupgrade**  

-   Le cas échéant, des limitations ou des spécifications supplémentaires sont fournies, avec des détails pour chaque version Technical Preview spécifique.  

-   Il n'existe aucune prise en charge pour la migration vers ou à partir de cette préversion.  

-   Il n'existe aucune prise en charge pour la mise à niveau vers cette préversion.  

-   Il n’existe aucune prise en charge de mise à niveau vers une build de production (Current Branch) à partir de cette build de version Preview. Cependant, quand des mises à jour sont disponibles pour une version Preview, vous pouvez les rechercher et les installer à partir du nœud **Mises à jour et maintenance** de la console Configuration Manager. Pour obtenir une vidéo du processus de mise à niveau dans la console, consultez [Installing ConfigMgr Update Packages](https://www.youtube.com/embed/KBd_EGFbUT8) sur youtube.com.  

##  <a name="a-namebkmkinstalla-install-and-update-the-technical-preview"></a><a name="bkmk_install"></a> Installer et mettre à jour la version Technical Preview  
 La version Technical Preview de System Center Configuration Manager se distingue de la version actuelle de System Center Configuration Manager.  

 Pour utiliser la version Technical Preview, vous devez d’abord installer une **version de référence** de la build de la version Technical Preview. Après avoir installé une version de référence, vous pouvez utiliser des **mises à jour dans la console** pour actualiser votre installation avec la version Preview la plus récente.     En règle générale, de nouvelles versions de la version d’évaluation technique sont disponibles chaque mois.

Chaque préversion est prise en charge pendant la durée de disponibilité de trois versions successives. Autrement dit, quand la version 1702 est publiée, la version 1610 n’est plus prise en charge, mais les versions 1611, 1612 et 1701 le sont toujours. Toutefois, si la dernière base de référence n’est plus prise en charge (telle que la version 1610), elle l’est toujours pour l’installation d’un nouveau site Technical Preview, tant que vous mettez ensuite à jour cette installation vers une version prise en charge.

> [!TIP]  
>  Quand vous installez une mise à jour de la version Technical Preview, vous mettez à jour votre installation vers cette nouvelle version Technical Preview.    Une installation de la version Technical Preview n’a jamais la possibilité d’effectuer une mise à niveau vers une installation de la version Current Branch, ni de recevoir des mises à jour de la version Current Branch.  

 **Versions de référence actives de la version Technical Preview :**  
 Vous pouvez installer une version de référence dans un délai d’un an après sa date de publication.

-   **Technical Preview 1610** : Configuration Manager Technical Preview 1610 est disponible à la fois sous la forme d’une mise à jour dans la console pour Configuration Manager Technical Preview et en tant que nouvelle version de référence disponible sur le site web [Centre d’évaluation TechNet](https://www.microsoft.com/en-us/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).




##  <a name="a-namebkmktpfeedbacka-providing-feedback"></a><a name="BKMK_TPFeedback"></a> Envoi de commentaires  
 Nous aimerions avoir votre avis sur nos versions 
Technical Preview. Pour envoyer des commentaires sur les fonctionnalités de chaque préversion, suivez le lien vers notre formulaire de commentaires dans la page [Programme d'évaluation de Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) sur le site Microsoft Connect.  

 Si vous avez des idées sur de nouvelles fonctionnalités que vous aimeriez voir, n'hésitez pas à nous en faire part. Pour soumettre de nouvelles idées et voter pour les idées soumises par d'autres utilisateurs, [visitez notre page dédiée à cet usage](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="a-namebkmktpcapsa-capabilities-delivered-in-technical-previews"></a><a name="bkmk_tpCaps"></a> Fonctionnalités fournies dans les versions Technical Preview  
 Voici la liste des fonctionnalités fournies par chaque version Technical Preview de Configuration Manager.  Les fonctionnalités disponibles à partir d’une version Technical Preview restent disponibles dans les versions ultérieures. De même, les fonctionnalités qui ont été ajoutées à la version System Center Configuration Manager (Current Branch) restent disponibles dans les versions Technical Preview suivantes.  Cliquez sur le contenu de chaque version Technical Preview pour en savoir plus sur une fonctionnalité spécifique.  

 |Fonctionnalité|Version Technical Preview|Version Current Branch|  
 |----------------|---------------------|--------------------|
 |Améliorations des groupes de limites pour les points de mise à jour logicielle | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |![Non ajouté](media/Red_X.gif)  |
 |L’inventaire matériel collecte des informations UEFI | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|![Non ajouté](media/Red_X.gif)  |
 |Améliorations apportées au déploiement des systèmes d’exploitation| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|![Non ajouté](media/Red_X.gif)  |
 |Héberger des mises à jour logicielles sur des points de distribution cloud| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|![Non ajouté](media/Red_X.gif) |
 |Valider les données de l’attestation d’intégrité de l’appareil via des points de gestion| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)|![Non ajouté](media/Red_X.gif) |
 |Connecteur OMS pour Microsoft Azure Government Cloud |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |![Non ajouté](media/Red_X.gif) |
 |Les versions Android et iOS ne peuvent plus être ciblées dans les Assistants de création |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |![Non ajouté](media/Red_X.gif) |
 |Accès aux données de point de terminaison OData |[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![Non ajouté](media/Red_X.gif)|
 |Point de service de l’entrepôt de données |[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|![Non ajouté](media/Red_X.gif)|
 |Outil de nettoyage de la bibliothèque de contenu |[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|![Non ajouté](media/Red_X.gif)|
 |Améliorations apportées à la recherche dans la console |[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|![Non ajouté](media/Red_X.gif)|
 |Empêcher l’installation d’une application si un programme est en cours d’exécution|[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|![Non ajouté](media/Red_X.gif)|
 |Nouvelle notification Windows Hello Entreprise pour les utilisateurs finaux|[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|![Non ajouté](media/Red_X.gif)|
 |Prise en charge de Windows Store pour Entreprises dans Configuration Manager|[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|![Non ajouté](media/Red_X.gif)|
 |Revenir à la page précédente en cas d’échec d’une séquence de tâches|[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|![Non ajouté](media/Red_X.gif)|
 |Prise en charge des fichiers d’installation rapide pour les mises à jour de Windows 10|[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|![Non ajouté](media/Red_X.gif)|
 |Intégration d’Azure Active Directory|[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|![Non ajouté](media/Red_X.gif)|
|Modification de la configuration de l’authentification multifacteur pour l’inscription d’appareils|[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![Non ajouté](media/Red_X.gif)|
|Mise en cache préalable du contenu pour les déploiements et les séquences de tâches |[Version d’évaluation technique 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|![Non ajouté](media/Red_X.gif)|
 |Paramètres de configuration de Windows Defender|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[Version 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Synchronisation de la stratégie de demande à partir de la console administrateur|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[Version 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |Prise en charge de rôles de sécurité supplémentaires pour le nœud Tous les appareils d’entreprise|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[Version 1610](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Accès conditionnel pour les profils VPN Windows 10|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[Version 1610](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |Filtrer par taille de contenu dans les règles de déploiement automatique|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |Fonctionnalité améliorée pour les boîtes de dialogue des logiciels requis|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Refuser les demandes d’applications précédemment approuvées|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Exclure les clients de la mise à niveau automatique|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[Version 1610](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Améliorations apportées à Endpoint Protection|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|![Non ajouté](media/Red_X.gif)|
 |Nombre accru d’appareils inscrits|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#increased-number-of-enrolled-devices)|![Non ajouté](media/Red_X.gif)|
 |Paramètres supplémentaires du programme DEP d’Apple|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[Version 1610](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |Améliorations de l’intégration du Windows Store pour Entreprises à Configuration Manager|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|[Version 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |Nouveaux paramètres de compatibilité pour les éléments de configuration|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[Version 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |Intégration à Upgrade Analytics|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[Version 1610](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Types de connexion natifs pour les profils hybrides VPN Windows 10|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Non ajouté](media/Red_X.gif)|
 |Améliorations pour les groupes de limites|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[Version 1610](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Tableau de bord Gestion des clients Office 365|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[Version 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |Déployer des applications Office 365 sur des clients|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|![Non ajouté](media/Red_X.gif)|
 |Améliorations apportées à la conversion BIOS à UEFI|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[Version 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Graphiques de conformité Intune|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[Version 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|
 |Améliorations apportées à l’étape de séquence de tâches Préparer le client ConfigMgr pour capture|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Améliorations apportées au Centre logiciel|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
 |Améliorations apportées à Asset Intelligence|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![Non ajouté](media/Red_X.gif)|
 |Traduction du clavier de contrôle à distance|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|![Non ajouté](media/Red_X.gif)|
 |Améliorations de la stratégie de mise à niveau de l’édition Windows 10|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[Version 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |Personnalisation des boîtes de dialogue du Centre logiciel|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-center-dialogs)|![Non ajouté](media/Red_X.gif)|  
 |Points de gestion d’appareil multiples pour la gestion des appareils mobiles locale|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Classement automatiquement des appareils dans des regroupements|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Version 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Période de grâce d’application pour les déploiements de mises à jour logicielles et d’applications obligatoires|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Utilisation de Configuration Manager comme programme d’installation géré avec Device Guard|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|![Non ajouté](media/Red_X.gif)|
 |Passerelle de gestion cloud (anciennement Service de proxy cloud)|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway)|  
 |Gestion de l’agent du client Office 365 dans Configuration Manager|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |La variable de séquence de tâches OSDPreserveDriveLetter est déconseillée|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[Version 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |Modifications pour le nœud Mises à jour et maintenance|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |VPN par application pour les appareils Windows 10|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[Version 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |Améliorations apportées à la séquence de tâches Installer les mises à jour logicielles|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Améliorations apportées à l’étape de séquence de tâches Préparer le client ConfigMgr pour capture |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) |
 |Période de grâce pour les déploiements d’applications obligatoires |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|![Non ajouté](media/Red_X.gif)|  
 |Nouvelle expérience pour les actions d’appareils distants |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Applications Windows Store pour Entreprises |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Améliorations générales pour les applications achetées en volume|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Protection des données d’entreprise|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Les utilisateurs finaux peuvent installer des applications à partir du portail d’entreprise |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|![Non ajouté](media/Red_X.gif)|  
 |Nouveaux onglets pour les mises à jour et les systèmes d’exploitation dans le Centre logiciel|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Maintenance de groupe de serveurs |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[Version 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |Prise en charge du service Windows Defender Advanced Threat Protection |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[Version 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |Nouvelles options de redémarrage pour les clients Windows 10 après l’installation de mises à jour logicielles|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |Attestation d’intégrité de l’appareil en local |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |Prédéclarer des appareils d’entreprise avec numéro IMEI ou numéro de série iOS|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[Version 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  
 |Gérer les applications achetées en volume à partir du Windows Store pour Entreprises| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Améliorations apportées à la gestion de Microsoft Passport for Work|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Options permettant aux clients de basculer vers un nouveau point de mise à jour logicielle|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |Paramètres client pour gérer les paramètres du cache du client et le cache d’homologue du client |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|Paramètres client : [Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)<br/>Cache d’homologue : [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache)|  
 |Prise en charge de Passport for Work en tant que Fournisseur de stockage de clés (KSP, Key Storage Provider) |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[Version 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |Attestation d’intégrité de l’appareil en local|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |Paramètre SmartLock pour les appareils Android|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[Version 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 |Améliorations apportées au Centre logiciel|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Améliorations apportées au contrôle à distance|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Personnalisation des tailles de bloc et de fenêtre TFTP RamDisk pour les points de distribution compatibles PXE|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  


 Quand toutes les fonctionnalités d’une version Technical Preview sont disponibles dans la version minimale prise en charge de la version Current Branch, les détails de cette préversion sont supprimés de ce tableau.


## <a name="see-also"></a>Voir aussi  
[Nouveautés de System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Présentation de System Center Configuration Manager](../../core/understand/introduction.md)

