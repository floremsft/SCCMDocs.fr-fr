---
title: Technical Preview pour System Center Configuration Manager
description: "Découvrez la version Technical Preview qui vous permet de tester les nouvelles fonctions et fonctionnalités de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 39a9cde3bd955c84f301d25258b413fecaa4393b
ms.openlocfilehash: 2aa78c20c919d04401f663063860df06c5262048


---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

**Bienvenue dans System Center Configuration Manager Technical Preview**. Cette rubrique fournit des détails sur la version Preview qui présente de nouvelles fonctions et fonctionnalités que nous développons actuellement. Chaque version Technical Preview inaugure des nouvelles fonctionnalités qui ne sont pas présentes dans la version Current Branch de System Center Configuration Manager au moment où la version Technical Preview est publiée. Ces fonctionnalités seront incluses dans une mise à jour de la version Current Branch, mais avant de finaliser et d’ajouter les fonctionnalités, nous souhaitons que vous puissiez les tester et nous faire part de vos commentaires.  

 S’agissant d’une version Technical Preview, les détails et les fonctionnalités sont susceptibles de changer.  

 Cette rubrique contient des informations qui s’appliquent à toutes les versions Technical Preview et répertorie chaque nouvelle fonctionnalité ainsi que la version Technical Preview où apparaît pour la première fois la fonctionnalité, par exemple la version 1512 pour le mois de décembre 2015. Ces fonctionnalités sont détaillées dans des rubriques distinctes dédiées à chaque version Preview.  

 Pour plus d’informations sur les nouveautés de la version Current Branch de Configuration Manager, consultez [Nouveautés de System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="a-namebkmkreqsa-requirements-and-limitations-for-the-technical-preview"></a><a name="bkmk_reqs"></a> Configuration requise et limitations pour Technical Preview  

> [!IMPORTANT]  
>  La licence de la version Technical Preview est destinée uniquement aux environnements de laboratoire.  Microsoft peut ne pas fournir de support technique et certaines fonctionnalités peuvent ne pas être disponibles dans la version Preview du logiciel. En outre, la version Preview du logiciel peut utiliser des normes de sécurité, de confidentialité, d’accessibilité, de disponibilité et de fiabilité réduites ou différentes par rapport aux logiciels fournis dans le commerce.  

 La plupart des conditions préalables à l’utilisation du produit sont abordées dans [Configurations prises en charge pour System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). Les exceptions suivantes s'appliquent aux versions Technical Preview :  

-   Chaque installation reste active pendant 90 jours, puis devient inactive.  

-   L'anglais est la seule langue prise en charge.  

-   Seul un site principal autonome est pris en charge. Il n'existe aucune prise en charge pour un site d'administration centrale, plusieurs sites principaux ou des sites secondaires.  

-   Seules les versions suivantes de SQL Server sont prises en charge :  

    -   SQL Server 2012 avec la mise à jour cumulative 2 ou version ultérieure  

    -   SQL Server 2014  

-   Le site prend en charge jusqu'à 10 clients, qui doivent exécuter l'un des systèmes d'exploitation suivants :  

    -   Windows 7  

    -   Windows 8  

    -   Windows 8.1  

    -   Windows 10  

-   Seuls les indicateurs d'installation (commutateurs) suivants sont pris en charge :  

    -   **/silent**  

    -   **/testdbupgrade**  

-   Le cas échéant, des limitations ou des spécifications supplémentaires sont fournies, avec des détails pour chaque version Technical Preview spécifique.  

-   Il n'existe aucune prise en charge pour la migration vers ou à partir de cette version préliminaire.  

-   Il n'existe aucune prise en charge pour la mise à niveau vers cette version préliminaire.  

-   Il n’existe aucune prise en charge de mise à niveau vers une build de production (Current Branch) à partir de cette build de version Preview. Cependant, quand des mises à jour sont disponibles pour une version Preview, vous pouvez les rechercher et les installer à partir du nœud **Mises à jour et maintenance** de la console Configuration Manager. Pour obtenir une vidéo du processus de mise à niveau dans la console, consultez [Installing ConfigMgr Update Packages](https://www.youtube.com/embed/KBd_EGFbUT8) sur youtube.com.  

##  <a name="a-namebkmkinstalla-install-and-update-the-technical-preview"></a><a name="bkmk_install"></a> Installer et mettre à jour la version Technical Preview  
 La version Technical Preview de System Center Configuration Manager se distingue de la version actuelle de System Center Configuration Manager.  

 Pour utiliser la version Technical Preview, vous devez d’abord installer une **version de référence** de la build de la version Technical Preview. Après avoir installé une version de référence, vous pouvez utiliser des **mises à jour dans la console** pour actualiser votre installation avec la version Preview la plus récente.     En règle générale, de nouvelles versions de la version d’évaluation technique sont disponibles chaque mois.  

> [!TIP]  
>  Quand vous installez une mise à jour de la version Technical Preview, vous mettez à jour votre installation vers cette nouvelle version Technical Preview.    Une installation de la version Technical Preview n’a jamais la possibilité d’effectuer une mise à niveau vers une installation de la version Current Branch, ni de recevoir des mises à jour de la version Current Branch.  

 **Versions de référence actives de la version Technical Preview :**  
 Vous pouvez installer une version de référence dans un délai d’un an après sa date de publication.

-   **Technical Preview 1610** : Configuration Manager Technical Preview 1610 est disponible à la fois sous la forme d’une mise à jour dans la console pour Configuration Manager Technical Preview et en tant que nouvelle version de référence disponible sur le site web [Centre d’évaluation TechNet](https://www.microsoft.com/en-us/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

-   **Technical Preview 1603** en tant que partie intégrante de **System Center Technical Preview 5** : Configuration Manager Technical Preview 1603 est disponible à la fois sous la forme d’une mise à jour dans la console pour Configuration Manager Technical Preview et en tant que nouvelle version de référence incluse dans System Center Technical Preview 5.    Seule la version fournie avec System Center Technical Preview 5 peut être utilisée pour une installation de référence.  

     À propos de la version de référence de [Configuration Manager Technical Preview de System Center Technical Preview 5](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) :  

    -   Le programme d’installation et la console Configuration Manager présentent tous deux cette version sous l’intitulé System Center Configuration Manager Technical Preview 1603.  

    -   Cette version de référence fonctionne comme Configuration Manager Technical Preview 1603, notamment en ce qui concerne la prise en charge des mises à jour dans la console.  


##  <a name="a-namebkmktpfeedbacka-providing-feedback"></a><a name="BKMK_TPFeedback"></a> Envoi de commentaires  
 Nous aimerions avoir votre avis sur nos versions 
Technical Preview. Pour envoyer des commentaires sur les fonctionnaltiés de chaque version préliminaire, suivez le lien vers notre formulaire de commentaires dans la page [Programme d'évaluation de Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) sur le site Microsoft Connect.  

 Si vous avez des idées sur de nouvelles fonctionnalités que vous aimeriez voir, n'hésitez pas à nous en faire part. Pour soumettre de nouvelles idées et voter pour les idées soumises par d'autres utilisateurs, [visitez notre page dédiée à cet usage](http://configurationmanager.uservoice.com).  

##  <a name="a-namebdmktpknownissuesa-general-changes-introduced-in-technical-previews"></a><a name="bdmk_tpknownissues"></a> Modifications générales introduites dans les versions Technical Preview  

-   **Technical Preview 1603 :**  

    -   À partir de Technical Preview 1603, vous pouvez configurer les déploiements de mises à jour logicielles de façon à ce que les clients exécutent une analyse de conformité des mises à jour logicielles immédiatement après avoir installé celles-ci et redémarré. Cela permet au client de vérifier la disponibilité de mises à jour logicielles supplémentaires devenues applicables après le redémarrage, puis de les installer (et devenir ainsi conforme) au cours d’une même fenêtre de maintenance.  

         Pour configurer ce comportement pour un déploiement, dans la page **Expérience utilisateur** de l’Assistant Déploiement des mises à jour logicielles, sélectionnez l’option **Si une mise à jour dans ce déploiement requiert un redémarrage du système, exécuter le cycle d’évaluation du déploiement des mises à jour après le redémarrage**.  

    -   À partir de Technical Preview 1603, le comportement de la variable de séquence de tâches SMSTSRebootDelay a changé. Cette variable spécifie le nombre de secondes à attendre avant le redémarrage de l’ordinateur. Le gestionnaire des séquences de tâches affiche une boîte de dialogue de notification avant le redémarrage si cette variable n’est pas définie sur 0.  
        Lorsque vous configurez une valeur pour cette variable, cette valeur persiste jusqu’à ce que vous en configuriez une nouvelle. Le délai de tous les redémarrages d’ordinateur suivants aura la même valeur. Dans Configuration Manager version 1602 et antérieures, la valeur par défaut (30 secondes) de la variable est rétablie après le redémarrage de l’ordinateur.   Pour plus d’informations, voir [Variables intégrées de séquence de tâches dans System Center Configuration Manager](../../osd/understand/task-sequence-built-in-variables.md).

-   **Technical Preview 1602 :** À compter de Technical Preview 1602, vous pouvez effectuer une mise à niveau sur place du système d’exploitation d’un serveur de système de site qui exécute Windows Server 2008 R2 vers Windows 2012 Server R2.  Quand vous utilisez les procédures de mise à niveau de Windows Server 2012 R2, vous n’avez pas besoin d’effectuer de restauration de serveur de site Configuration Manager après la mise à niveau.  Pour connaître les procédures de mise à niveau, consultez [Options de mise à niveau pour Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx).  

    > [!WARNING]  
    >  Avant de mettre à niveau vers Windows Server 2012 R2, **vous devez désinstaller WSUS 3.2** du serveur.  
    >   
    >  Pour plus d’informations sur cette étape critique, consultez la section Fonctionnalités nouvelles et modifiées de [Vue d’ensemble des services WSUS (Windows Server Update Services)](https://technet.microsoft.com/library/hh852345.aspx) dans la documentation de Windows Server.  

-   **Technical Preview 1601 :** Par défaut, le point de connexion de service est défini en mode en ligne lors de son installation. Il ne prend pas en charge le basculement en mode hors connexion.  





##  <a name="a-namebkmktpcapsa-capabilities-delivered-in-technical-previews"></a><a name="bkmk_tpCaps"></a> Fonctionnalités fournies dans les versions Technical Preview  
 Voici la liste des fonctionnalités fournies par chaque version Technical Preview de Configuration Manager.  Les fonctionnalités disponibles à partir d’une version Technical Preview restent disponibles dans les versions ultérieures. De même, les fonctionnalités qui ont été ajoutées à la version System Center Configuration Manager (Current Branch) restent disponibles dans les versions Technical Preview suivantes.  Cliquez sur le contenu de chaque version Technical Preview pour en savoir plus sur une fonctionnalité spécifique.  

 |Fonctionnalité|Version Technical Preview|Version Current Branch|  
 |----------------|---------------------|--------------------|
 |Filtrer par taille de contenu dans les règles de déploiement automatique|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|![Non ajouté](media/Red_X.gif)|
 |Fonctionnalité améliorée pour les boîtes de dialogue des logiciels requis|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|![Non ajouté](media/Red_X.gif)|
 |Refuser les demandes d’applications précédemment approuvées|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|![Non ajouté](media/Red_X.gif)|
 |Exclure les clients de la mise à niveau automatique|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|![Non ajouté](media/Red_X.gif)|
 |Améliorations apportées à Endpoint Protection|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|![Non ajouté](media/Red_X.gif)|
 |Nombre accru d’appareils inscrits|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#increased-number-of-enrolled-devices)|![Non ajouté](media/Red_X.gif)|
 |Paramètres supplémentaires du programme DEP d’Apple|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|![Non ajouté](media/Red_X.gif)|
 |Améliorations de l’intégration de Windows Store pour Entreprises à Configuration Manager|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|![Non ajouté](media/Red_X.gif)|
 |Nouveaux paramètres de compatibilité pour les éléments de configuration|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|![Non ajouté](media/Red_X.gif)|
 |Intégration à Upgrade Analytics|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|![Non ajouté](media/Red_X.gif)|
 |Types de connexion natifs pour les profils hybrides VPN Windows 10|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Non ajouté](media/Red_X.gif)|
 |Améliorations pour les groupes de limites|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|![Non ajouté](media/Red_X.gif)|
 |Tableau de bord Gestion des clients Office 365|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|![Non ajouté](media/Red_X.gif)|
 |Déployer des applications Office 365 sur des clients|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#ceploy-office-365-apps-to-clients)|![Non ajouté](media/Red_X.gif)|
 |Améliorations apportées à la conversion BIOS à UEFI|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-bios-to-uefi-conversion)|![Non ajouté](media/Red_X.gif)|
 |Graphiques de conformité Intune|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|![Non ajouté](media/Red_X.gif)|
 |Améliorations apportées à l’étape de séquence de tâches Préparer le client ConfigMgr pour capture|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|![Non ajouté](media/Red_X.gif)|
 |Améliorations apportées au Centre logiciel|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|![Non ajouté](media/Red_X.gif)|
 |Améliorations apportées à Asset Intelligence|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![Non ajouté](media/Red_X.gif)|
 |Traduction du clavier de contrôle à distance|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|![Non ajouté](media/Red_X.gif)|
 |Améliorations de la stratégie de mise à niveau de l’édition Windows 10|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|![Non ajouté](media/Red_X.gif)|
 |Personnalisation des boîtes de dialogue du Centre logiciel|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-denter-dialogs)|![Non ajouté](media/Red_X.gif)|  
 |Points de gestion d’appareil multiples pour la gestion des appareils mobiles locale|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Classement automatiquement des appareils dans des regroupements|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Version 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Période de grâce d’application pour les déploiements de mises à jour logicielles et d’applications obligatoires|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|![Non ajouté](media/Red_X.gif)|
 |Utilisation de Configuration Manager comme programme d’installation géré avec Device Guard|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|![Non ajouté](media/Red_X.gif)|
 |Service de proxy cloud|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | ![Non ajouté](media/Red_X.gif)|  
 |Gestion de l’agent du client Office 365 dans Configuration Manager|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |La variable de séquence de tâches OSDPreserveDriveLetter est déconseillée|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[Version 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |Modifications pour le nœud Mises à jour et maintenance|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |VPN par application pour les appareils Windows 10|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[Version 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |Améliorations apportées à la séquence de tâches Installer les mises à jour logicielles|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Améliorations apportées à l’étape de séquence de tâches Préparer le client ConfigMgr pour capture |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|![Non ajouté](media/Red_X.gif) |
 |Période de grâce pour les déploiements d’applications obligatoires |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|![Non ajouté](media/Red_X.gif)|  
 |Nouvelle expérience pour les actions d’appareils distants |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Applications Windows Store pour Entreprises |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Améliorations générales pour les applications achetées en volume|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Protection des données d’entreprise|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Les utilisateurs finaux peuvent installer des applications à partir du portail d’entreprise |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|![Non ajouté](media/Red_X.gif)|  
 |Nouveaux onglets pour les mises à jour et les systèmes d’exploitation dans le Centre logiciel|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Maintenance de groupe de serveurs |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[Version 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |Prise en charge du service Windows Defender Advanced Threat Protection |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[Version 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |Nouvelles options de redémarrage pour les clients Windows 10 après l’installation de mises à jour logicielles|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |Attestation d’intégrité de l’appareil en local |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |Prédéclarer des appareils d’entreprise avec numéro IMEI ou numéro de série iOS|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[Version 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  
 |Gérer les applications achetées en volume à partir du Windows Store pour Entreprises| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Améliorations apportées à la gestion de Microsoft Passport for Work|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Options permettant aux clients de basculer vers un nouveau point de mise à jour logicielle|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |Paramètres client pour gérer les paramètres du cache du client et le cache d’homologue du client |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)|  
 |Prise en charge de Passport for Work en tant que Fournisseur de stockage de clés (KSP, Key Storage Provider) |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[Version 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |Attestation d’intégrité de l’appareil en local|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |Paramètre SmartLock pour les appareils Android|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[Version 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 |Améliorations apportées au Centre logiciel|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Améliorations apportées au contrôle à distance|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Personnalisation des tailles de bloc et de fenêtre TFTP RamDisk pour les points de distribution compatibles PXE|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Améliorations apportées à la gestion des appareils mobiles|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_MDM)|[Version 1602](/sccm/mdm/deploy-use/manage-ios-activation-lock) |  
 |Améliorations apportées au Centre logiciel dans la version 1602|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_SC1601)| [Version 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#client-management)|  
 |Améliorations apportées à la Maintenance de Windows 10|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_Win10Servicing)|[Version 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#operating-system-deployment) |  
 |Améliorations apportées à l’intégration de Microsoft Intune|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_hybrid1)|[Version 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#conditional-access)|  
 |État de connexion du client|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_clientStatus)|[Version 1602](/sccm/core/clients/manage/monitor-clients)|
 |Améliorations de la gestion d’applications|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_appmgmt1601)|[Version 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#application-management)|  
 |Améliorations apportées aux paramètres de conformité|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_compliance1601)|[Version 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#compliance-settings)|  
 |Attestation de l’intégrité des appareils|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_devicehealth)|[Version 1602](/sccm/core/servers/manage/health-attestation))|
 |Surveillance des conditions générales dans la console|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_viewterms)|[Version 1602](/sccm/mdm/deploy-use/terms-and-conditions)|  
 |Améliorations apportées aux paramètres de stratégie Endpoint Protection|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_EPpolicy)|[Version 1602](/sccm/protect/deploy-use/endpoint-antimalware-policies)|  
 |Intégration avec Windows Update for Business dans Windows 10|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_WUfB)|[Version 1602](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|  
 |Gestion des mises à jour du client Office 365 ProPlus via System Center Configuration Manager|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_Office365ProPlus)|[Version 1602](/sccm/sum/deploy-use/manage-office-365-proplus-updates)|  
 |Prise en charge de SQL Server AlwaysOn pour les bases de données hautement disponibles|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_AlwasyOn)|[Version 1602](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)|  
 |Réponse aux demandes d'un cluster de serveurs|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_ClusterServerUpdates)|[Version 1606](/sccm/sum/deploy-use/service-a-server-group)|  
## <a name="see-also"></a>Voir aussi  
[Nouveautés de System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Présentation de System Center Configuration Manager](../../core/understand/introduction.md)



<!--HONumber=Nov16_HO1-->


