---
title: Version Technical Preview pour System Center Configuration Manager | Microsoft Docs
description: "Découvrez la version Technical Preview qui vous permet de tester les nouvelles fonctions et fonctionnalités de System Center Configuration Manager."
ms.custom: na
ms.date: 4/3/2017
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
ms.sourcegitcommit: 9b31fab8fa93195c60e9026e2df99311aa6e328f
ms.openlocfilehash: 61d4b7017769609caf8fcb8fcdd510f5a0b5b712
ms.lasthandoff: 04/03/2017


---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

**Bienvenue dans System Center Configuration Manager Technical Preview**. Cette rubrique fournit des détails sur la version Preview qui présente de nouvelles fonctions et fonctionnalités que nous développons actuellement. Chaque version Technical Preview inaugure des nouvelles fonctionnalités qui ne sont pas présentes dans la version Current Branch de System Center Configuration Manager au moment où la version Technical Preview est publiée. Ces fonctionnalités seront incluses dans une mise à jour de la version Current Branch, mais avant de finaliser et d’ajouter les fonctionnalités, nous souhaitons que vous puissiez les tester et nous faire part de vos commentaires.  

 S’agissant d’une version Technical Preview, les détails et les fonctionnalités sont susceptibles de changer.  

 Cette rubrique contient des informations qui s’appliquent à toutes les versions Technical Preview et répertorie également chaque nouvelle fonctionnalité ainsi que la version Technical Preview où la fonctionnalité apparaît pour la première fois, par exemple la version 1701 pour le mois de janvier 2017. Ces fonctionnalités sont détaillées dans des rubriques distinctes dédiées à chaque version Preview.  

 Pour plus d’informations sur les nouveautés de la version Current Branch de Configuration Manager, consultez [Nouveautés de System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Configuration requise et limitations pour Technical Preview  

> [!IMPORTANT]     
>  La licence de la version Technical Preview est destinée uniquement aux environnements de laboratoire.  Microsoft peut ne pas fournir de support technique et certaines fonctionnalités peuvent ne pas être disponibles dans la version Preview du logiciel. En outre, la version Preview du logiciel peut utiliser des normes de sécurité, de confidentialité, d’accessibilité, de disponibilité et de fiabilité réduites ou différentes par rapport aux logiciels fournis dans le commerce.  

 La plupart des prérequis du produit sont abordés dans [Configurations prises en charge pour System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). Les exceptions suivantes s'appliquent aux versions Technical Preview :  

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


-   Par défaut, lorsque vous utilisez la préversion technique, le point de connexion de service est défini en mode en ligne lors de son installation. Il ne prend pas en charge le basculement en mode hors connexion.

-   Le cas échéant, des limitations ou des spécifications supplémentaires sont fournies, avec des détails pour chaque version Technical Preview spécifique.  

-   Il n'existe aucune prise en charge pour la migration vers ou à partir de cette préversion.  

-   Il n'existe aucune prise en charge pour la mise à niveau vers cette préversion.  

-   Il n’existe aucune prise en charge de mise à niveau vers une build de production (Current Branch) à partir de cette build de version Preview. Cependant, quand des mises à jour sont disponibles pour une version Preview, vous pouvez les rechercher et les installer à partir du nœud **Mises à jour et maintenance** de la console Configuration Manager. Pour obtenir une vidéo du processus de mise à niveau dans la console, consultez [Installing ConfigMgr Update Packages](https://www.youtube.com/embed/KBd_EGFbUT8) sur youtube.com.  

##  <a name="bkmk_install"></a> Installer et mettre à jour la version Technical Preview  
 La version Technical Preview de System Center Configuration Manager se distingue de la version actuelle de System Center Configuration Manager.  

 Pour utiliser la version Technical Preview, vous devez d’abord installer une **version de référence** de la build de la version Technical Preview. Après avoir installé une version de référence, vous pouvez utiliser des **mises à jour dans la console** pour actualiser votre installation avec la version Preview la plus récente.     En règle générale, de nouvelles versions de la version d’évaluation technique sont disponibles chaque mois.

Chaque préversion est prise en charge pendant la durée de disponibilité de trois versions successives. Autrement dit, quand la version 1702 est publiée, la version 1610 n’est plus prise en charge, mais les versions 1611, 1612 et 1701 le sont toujours. Quand une base de référence n’est plus prise en charge (comme version 1610), elle l’est toujours pour l’installation d’un nouveau site Technical Preview jusqu’à ce qu’une nouvelle version de base de référence soit disponible, tant que vous mettez ensuite à jour cette installation vers une version prise en charge. Lors de la mise à jour, si vous ne voyez pas la version la plus récente disponible dans la console, mettez à jour vers la dernière version proposée, puis répétez ce processus jusqu’à pouvoir installer la version la plus récente de la version Technical Preview.

> [!TIP]  
>  Quand vous installez une mise à jour de la version Technical Preview, vous mettez à jour votre installation vers cette nouvelle version Technical Preview.    Une installation de la version Technical Preview n’a jamais la possibilité d’effectuer une mise à niveau vers une installation de la version Current Branch, ni de recevoir des mises à jour de la version Current Branch.  

**Versions de référence actives de la version Technical Preview :**  
Vous pouvez installer une version de référence dans un délai d’un an après sa date de publication. Toutefois, lorsque vous installez un nouveau site Technical Preview, nous vous recommandons d’utiliser la dernière version de base de référence disponible.
-  **Technical Preview 1703** : Configuration Manager Technical Preview 1703 est disponible à la fois sous la forme d’une mise à jour dans la console pour Configuration Manager Technical Preview et en tant que nouvelle version de référence disponible sur le site web Centre d’évaluation TechNet.

-  **Technical Preview 1610** : Configuration Manager Technical Preview 1610 est disponible à la fois sous la forme d’une mise à jour dans la console pour Configuration Manager Technical Preview et en tant que version de référence. Si vous disposez du support d’installation 1610, nous vous recommandons de télécharger la version 1703 et d’installer cette version à la place.




##  <a name="BKMK_TPFeedback"></a> Envoi de commentaires  
 Nous aimerions avoir votre avis sur nos versions 
Technical Preview. Pour envoyer des commentaires sur les fonctionnalités de chaque préversion, suivez le lien vers notre formulaire de commentaires dans la page [Programme d'évaluation de Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) sur le site Microsoft Connect.  

 Si vous avez des idées sur de nouvelles fonctionnalités que vous aimeriez voir, n'hésitez pas à nous en faire part. Pour soumettre de nouvelles idées et voter pour les idées soumises par d'autres utilisateurs, [visitez notre page dédiée à cet usage](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Fonctionnalités fournies dans les versions Technical Preview  
 Voici la liste des fonctionnalités fournies par chaque version Technical Preview de Configuration Manager.  Les fonctionnalités disponibles à partir d’une version Technical Preview restent disponibles dans les versions ultérieures. De même, les fonctionnalités qui ont été ajoutées à la version System Center Configuration Manager (Current Branch) restent disponibles dans les versions Technical Preview suivantes.  Cliquez sur le contenu de chaque version Technical Preview pour en savoir plus sur une fonctionnalité spécifique.  

 |Fonctionnalité|Version Technical Preview|Version Current Branch|  
 |----------------|---------------------|--------------------|
 |Déployer des applications iOS achetées en volume sur des regroupements d’appareils|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#deploy-volume-purchased-ios-apps-to-device-collections)|[Version 1702](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)|
 |Liens directs vers des applications dans le Centre logiciel|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#direct-links-to-applications-in-software-center)|![Non ajouté](media/Red_X.gif)
 |Certificats PFX pour les ordinateurs clients Configuration Manager exécutant Windows|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#pfx-certificates-for-configuration-manager-windows-client-computers)|![Non ajouté](media/Red_X.gif)|
 |Assistant Configuration des services Azure|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#configure-azure-services-wizard)|![Non ajouté](media/Red_X.gif)|
 |Convertir de BIOS en UEFI dans une séquence de tâches de mise à niveau du système d’exploitation| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#convert-from-bios-to-uefi-during-an-in-place-upgrade) |[Version 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)|
 |Groupes de séquences de tâches réductibles| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#collapsible-task-sequence-groups) |![Non ajouté](media/Red_X.gif)|
 |Paramètres du client pour configurer Windows Analytics pour Upgrade Readiness | [Tech Preview 1703](capabilities-in-technical-preview-1703.md#client-settings-to-configure-windows-analytics-for-upgrade-readiness) |![Non ajouté](media/Red_X.gif)|
 |Nouveaux paramètres de compatibilité pour les appareils iOS|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#new-compliance-settings-for-ios-devices)|[Version 1702](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)|
 |Créer des certificats PFX avec prise en charge S/MIME|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#create-pfx-certificates-with-s-mime-support)|[Version 1702](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |Vérifier si des fichiers exécutables sont en cours d’exécution avant d’installer une application|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#check-for-running-executable-files-before-installing-an-application)|[Version 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Envoyer des commentaires à partir de la console Configuration Manager | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#send-feedback-from-the-configuration-manager-console)    |[Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#send-feedback-from-the-configuration-managercconsole)  |
 |Modifications pour les mises à jour et la maintenance  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#changes-for-updates-and-servicing)  |[Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#changes-for-updates-and-servicing) |
 |Améliorations de Cache d’homologue  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#peer-cache-improvements) |[Version 1702](/sccm/core/plan-design/hierarchy/client-peer-cache)|
 |Utiliser Azure Active Directory  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |![Non ajouté](media/Red_X.gif)|
 |Améliorations apportées aux stratégies de conformité des appareils avec accès conditionnel | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#conditional-access-device-compliance-policy-improvements) |[Version 1702](/sccm/mdm/deploy-use/create-compliance-policy)|
 |Alerte de version du client de logiciel anti-programme malveillant | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert) |[Version 1702](/sccm/protect/deploy-use/endpoint-configure-alerts?branch=live#alert-for-outdated-malware-client)|
 |Évaluation de la conformité des mises à jour Windows Update for Business | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |![Non ajouté](media/Red_X.gif)|
 |Améliorations apportées aux paramètres du Centre logiciel et aux messages de notification pour les séquences de tâches à fort impact|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert)|[Version 1702](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)|
 |Prise en charge d’Android for Work| [Tech Preview 1702](capabilities-in-technical-preview-1702.md#android-for-work-support) |[Version 1702](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-for-work-enrollment)|
 |Améliorations des groupes de limites pour les points de mise à jour logicielle | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |[Version 1702](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)  |
 |L’inventaire matériel collecte des informations UEFI | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|[Version 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#hardware-inventory-collects-uefi-information) |
 |Améliorations apportées au déploiement des systèmes d’exploitation| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|[Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment) |
 |Héberger des mises à jour logicielles sur des points de distribution cloud| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|![Non ajouté](media/Red_X.gif) |
 |Valider les données de l’attestation d’intégrité de l’appareil via des points de gestion| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)| [Version 1702](/sccm/core/servers/manage/health-attestation) |
 |Connecteur OMS pour Microsoft Azure Government Cloud |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |[Version 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig) |
 |Les versions Android et iOS ne peuvent plus être ciblées dans les Assistants de création |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |![Non ajouté](media/Red_X.gif) |
 |Accès aux données de point de terminaison OData |[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![Non ajouté](media/Red_X.gif)|
 |Point de service de l’entrepôt de données |[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|[Version 1702](/sccm/core/servers/manage/data-warehouse)|
 |Outil de nettoyage de la bibliothèque de contenu |[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|[Version 1702](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) |
 |Améliorations apportées à la recherche dans la console |[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|[Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-for-in-console-search)|
 |Empêcher l’installation d’une application si un programme est en cours d’exécution|[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|[Version 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Nouvelle notification Windows Hello Entreprise pour les utilisateurs finaux|[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|![Non ajouté](media/Red_X.gif)|
 |Prise en charge de Windows Store pour Entreprises dans Configuration Manager|[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|![Non ajouté](media/Red_X.gif)|
 |Revenir à la page précédente en cas d’échec d’une séquence de tâches|[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|[Version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment)|
 |Prise en charge des fichiers d’installation rapide pour les mises à jour de Windows 10|[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|[Version 1702](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)|
 |Intégration d’Azure Active Directory|[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|![Non ajouté](media/Red_X.gif)|
 |Modification de la configuration de l’authentification multifacteur pour l’inscription d’appareils|[Version d’évaluation technique 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![Non ajouté](media/Red_X.gif)|
 |Mise en cache préalable du contenu pour les déploiements et les séquences de tâches |[Version d’évaluation technique 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|[Version 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
 |Paramètres de configuration de Windows Defender|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[Version 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Synchronisation de la stratégie de demande à partir de la console administrateur|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[Version 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |Prise en charge de rôles de sécurité supplémentaires pour le nœud Tous les appareils d’entreprise|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[Version 1610](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Accès conditionnel pour les profils VPN Windows 10|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[Version 1610](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |Filtrer par taille de contenu dans les règles de déploiement automatique|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |Fonctionnalité améliorée pour les boîtes de dialogue des logiciels requis|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Refuser les demandes d’applications précédemment approuvées|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Exclure les clients de la mise à niveau automatique|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[Version 1610](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Améliorations apportées à Endpoint Protection|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|[Version 1610](/sccm/protect/deploy-use/endpoint-antimalware-policies#cloud-protection-service)|
 |Nombre accru d’appareils inscrits|[Tech Preview 1609](/sccm/mdm/deploy-use/enable-platform-enrollment)|[Version 1610](/sccm/mdm/deploy-use/enable-platform-enrollment)|
 |Paramètres supplémentaires du programme DEP d’Apple|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[Version 1610](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |Améliorations de l’intégration du Windows Store pour Entreprises à Configuration Manager|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|[Version 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |Nouveaux paramètres de compatibilité pour les éléments de configuration|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[Version 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |Intégration à Upgrade Analytics|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[Version 1610](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Types de connexion natifs pour les profils hybrides VPN Windows 10|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Non ajouté](media/Red_X.gif)|
 |Améliorations pour les groupes de limites|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[Version 1610](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Tableau de bord Gestion des clients Office 365|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[Version 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |Déployer des applications Office 365 sur des clients|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|[Version 1702](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)|
 |Améliorations apportées à la conversion BIOS à UEFI|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[Version 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Graphiques de conformité Intune|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[Version 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|
 |Améliorations apportées à l’étape de séquence de tâches Préparer le client ConfigMgr pour capture|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Améliorations apportées au Centre logiciel|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
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

