---
title: Versions Technical Preview
titleSuffix: Configuration Manager
description: "Découvrez la version Technical Preview qui vous permet de tester les nouvelles fonctions et fonctionnalités de System Center Configuration Manager."
ms.custom: na
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 975bd66bb86efb133ccd7017295e8108558f633d
ms.sourcegitcommit: db9978135d7a6455d83dbe4a5175af2bdeaeafd8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/22/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

**Bienvenue dans System Center Configuration Manager Technical Preview**. Cette rubrique fournit des détails sur la préversion qui présente de nouvelles fonctions et fonctionnalités que nous développons actuellement. Chaque version Technical Preview inaugure de nouvelles fonctionnalités qui ne sont pas présentes dans la version Current Branch de Configuration Manager au moment où la version Technical Preview est publiée. Ces fonctionnalités seront incluses dans une mise à jour de la version Current Branch, mais avant de finaliser et d’ajouter les fonctionnalités, nous souhaitons que vous puissiez les tester et nous faire part de vos commentaires.  

 Comme il s’agit d’une version Technical Preview, les détails et les fonctionnalités sont susceptibles de changer.  

 Cet article contient des informations qui s’appliquent à toutes les versions Technical Preview. Il répertorie également chaque nouvelle fonctionnalité ainsi que la version Technical Preview où la fonctionnalité apparaît pour la première fois, par exemple la version 1801 pour le mois de janvier 2018. Ces fonctionnalités sont détaillées dans des rubriques distinctes dédiées à chaque préversion.  

 Pour plus d’informations sur les nouveautés de la version Current Branch de Configuration Manager, consultez [Nouveautés de System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Configuration requise et limitations pour Technical Preview  

> [!IMPORTANT]     
>  La licence de la version Technical Preview est destinée uniquement aux environnements de laboratoire.  Microsoft peut ne pas fournir de services de support technique, et certaines fonctionnalités peuvent ne pas être disponibles dans la préversion du logiciel. De plus, la préversion du logiciel peut utiliser des standards de sécurité, de confidentialité, d’accessibilité, de disponibilité et de fiabilité réduites ou différentes par rapport aux logiciels fournis dans le commerce.  

 La plupart des prérequis du produit sont abordés dans [Configurations prises en charge pour System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). Les exceptions suivantes s'appliquent aux versions Technical Preview :  

-   Chaque installation reste active pendant 90 jours, puis devient inactive.  

-   L'anglais est la seule langue prise en charge.


-   Seuls les indicateurs d'installation (commutateurs) suivants sont pris en charge :  

    -   **/silent**  
    -   **/testdbupgrade**    


-   Par défaut, quand vous utilisez la version Technical Preview, le point de connexion de service est installé en mode en ligne. Le basculement en mode hors connexion n’est pas pris en charge.

-   Les articles dédiés à chaque version Technical Preview décrivent les limitations ou les spécifications supplémentaires, le cas échéant.

-   Il n'existe aucune prise en charge pour la migration vers ou à partir de cette préversion.  

-   Il n'existe aucune prise en charge pour la mise à niveau vers cette préversion.  

-   Il n’existe aucune prise en charge de mise à niveau vers une build de production (Current Branch) à partir de cette build de version Preview. Cependant, quand des mises à jour sont disponibles pour une version Preview, vous pouvez les rechercher et les installer à partir du nœud **Mises à jour et maintenance** de la console Configuration Manager. Pour obtenir une vidéo du processus de mise à niveau dans la console, consultez [Installing ConfigMgr Update Packages](https://www.youtube.com/embed/KBd_EGFbUT8) sur youtube.com.  
-   Seul un site principal autonome est pris en charge. Il n'existe aucune prise en charge pour un site d'administration centrale, plusieurs sites principaux ou des sites secondaires.  

Les produits et technologies suivants sont pris en charge par cette branche de Configuration Manager. Toutefois, leur inclusion dans ce contenu n’implique pas une extension de prise en charge d’un produit ou d’une version au-delà de leur cycle de vie individuel. L’utilisation de produits qui ont dépassé leur cycle de vie n’est pas prise en charge avec Configuration Manager. Pour plus d’informations sur les politiques de support Microsoft, consultez le site web [Politique de support Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

-   Seules les versions suivantes de SQL Server sont prises en charge :  

    -   SQL Server 2017 (avec mise à jour cumulative 2 et ultérieure) à compter de Configuration Manager version 1710
    -   SQL Server 2016 (sans Service Pack et versions ultérieures)
    -   SQL Server 2014 (avec Service Pack 1 et version ultérieure)
    -   SQL Server 2012 (avec Service Pack 3 ou version ultérieure)


-   Le site prend en charge jusqu’à 10 clients, qui doivent exécuter l’une des versions suivantes de Windows :  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

##  <a name="bkmk_install"></a> Installer et mettre à jour la version Technical Preview  
 La version Technical Preview de System Center Configuration Manager se distingue de la version actuelle de System Center Configuration Manager.  

 Pour utiliser la version Technical Preview, vous devez d’abord installer une **version de référence** de la build de la version Technical Preview. Après avoir installé une version de base de référence, vous pouvez utiliser des **mises à jour dans la console** pour actualiser votre installation avec la préversion la plus récente. En règle générale, de nouvelles versions Technical Preview sont disponibles chaque mois.

Chaque préversion est prise en charge pendant la durée de disponibilité de trois versions successives. Autrement dit, quand la version 1708 est publiée, la version 1704 n’est plus prise en charge, mais les versions 1705, 1706 et 1707 le sont toujours. Quand une base de référence n’est plus prise en charge, elle l’est toujours pour l’installation d’un nouveau site Technical Preview jusqu’à ce qu’une nouvelle version de base de référence soit disponible, à condition que vous mettez ensuite à jour cette installation avec une version prise en charge. Effectuez une mise à jour avec la version la plus récente, puis répétez ce processus jusqu’à ce que vous puissiez installer la version la plus récente de la version Technical Preview.

> [!TIP]  
>  Quand vous installez une mise à jour de la version Technical Preview, vous mettez à jour votre installation vers cette nouvelle version Technical Preview.    Une installation de la version Technical Preview n’a jamais la possibilité d’effectuer une mise à niveau vers une installation de la version Current Branch, ni de recevoir des mises à jour de la version Current Branch.  

**Versions de référence actives de la version Technical Preview :**
   
Vous pouvez installer une version de référence dans un délai d’un an après sa date de publication. Toutefois, lorsque vous installez un nouveau site Technical Preview, nous vous recommandons d’utiliser la dernière version de base de référence disponible.
-  **Technical Preview 1711** : Configuration Manager Technical Preview 1711 est disponible à la fois sous la forme d’une mise à jour dans la console et en tant que nouvelle version de référence. Téléchargez les versions de référence [à partir du Centre d’évaluation TechNet](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).


##  <a name="BKMK_TPFeedback"></a> Envoi de commentaires  
 Faites-nous part de vos commentaires sur les capacités de nos versions Technical Preview. Pour plus d’informations, consultez [Commentaires produit](../understand/find-help.md#product-feedback).

Si vous avez des idées sur de nouvelles fonctionnalités que vous aimeriez voir, n’hésitez pas à nous en faire part. Pour soumettre de nouvelles idées et voter pour les idées soumises par d'autres utilisateurs, [visitez notre page dédiée à cet usage](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Fonctionnalités fournies dans la dernière version Technical Preview  
Voici la liste des fonctionnalités fournies par la version Technical Preview de Configuration Manager la plus récente.  Les fonctionnalités disponibles dans une version Technical Preview antérieure restent disponibles dans les versions ultérieures. De même, les fonctionnalités qui ont été ajoutées à la version Current Branch de Configuration Manager restent disponibles dans les versions Technical Preview.  Cliquez sur le contenu de chaque version Technical Preview pour en savoir plus sur une fonctionnalité spécifique.  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1801"></a>Technical Preview version 1801
- [Créer des déploiements par phases](capabilities-in-technical-preview-1801.md#create-phased-deployments) <!-- 1357405 --> 
- [Rapports de cogestion](capabilities-in-technical-preview-1801.md#co-management-reporting) <!-- 1356648 --> 
- [Améliorations apportées à la planification de l’évaluation des règles de déploiement automatique](capabilities-in-technical-preview-1801.md#improvements-to-automatic-deployment-rule-evaluation-schedule) <!-- 1357133 --> 
- [Réaffecter un point de distribution](capabilities-in-technical-preview-1801.md#reassign-distribution-point) <!-- 1306937 --> 
- [Améliorations apportées à l’inventaire matériel](capabilities-in-technical-preview-1801.md#improvements-to-hardware-inventory) <!-- 1357389 --> 
- [Améliorations apportées aux paramètres des clients pour le Centre logiciel](capabilities-in-technical-preview-1801.md#improvements-to-client-settings-for-software-center) <!-- 1355146 --> 
- [Nouveaux paramètres pour Windows Defender Application Guard](capabilities-in-technical-preview-1801.md#new-settings-for-windows-defender-application-guard) <!-- 1356256 --> 
- [Améliorations apportées à l’exécution de scripts](capabilities-in-technical-preview-1801.md#improvements-to-run-scripts) <!-- 1236459 --> 




## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>Fonctionnalités fournies dans les versions Technical Preview prises en charge récentes
Voici la liste des fonctionnalités fournies avec les versions Technical Preview de Configuration Manager précédentes qui sont encore prises en charge. 

<!-- This is the full list of new features in the past three TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Fonctionnalité |Version Technical Preview |Version Current Branch|  
 |----------------|---------------------|--------------------|
 |Ne pas mettre automatiquement à niveau les applications remplacées <!-- 1351266 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#do-not-automatically-upgrade-superseded-applications)  |![Non ajouté](media/Red_X.gif)    | 
 |Installer plusieurs applications dans le Centre logiciel <!-- 1357126 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#install-multiple-applications-in-software-center)  |![Non ajouté](media/Red_X.gif)    |
 |Changement dans l’installation du client Configuration Manager <!-- 1356195 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-in-the-configuration-manager-client-install)  |![Non ajouté](media/Red_X.gif)    | 
 |Changement dans le tableau de bord des appareils Surface <!-- 1355788 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-to-the-surface-device-dashboard)  |![Non ajouté](media/Red_X.gif)    | 
 |Améliorations apportées au tableau de bord Gestion des clients Office 365 <!-- 1357281 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-office-365-client-management-dashboard)  |![Non ajouté](media/Red_X.gif)    | 
 |Améliorations apportées à la console Configuration Manager <!-- 1357280,1357282 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-the-configuration-manager-console)  |![Non ajouté](media/Red_X.gif)    | 
 |Améliorations apportées au déploiement de système d’exploitation <!-- SMS 500897 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-operating-system-deployment)  |![Non ajouté](media/Red_X.gif)    | 
 |Exécuter l’étape de la séquence de tâches <!-- 1261338 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |[Version 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence)    |
 |Autoriser l’interaction utilisateur durant l’installation d’une application <!-- 1356976 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |![Non ajouté](media/Red_X.gif)    |
 |Télémétrie Windows 10 pour Windows Analytics Device Health <!--1356148 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health) |[Version 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#reporting)    |
 |Amélioration des icônes du Centre logiciel <!-- 1356194 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#software-center-no-longer-distorts-icons-larger-than-250x250) |[Version 1710](/sccm/apps/plan-design/plan-for-and-configure-application-management#supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center)    |
 |Vérifier auprès du Centre logiciel la conformité des périphériques cogérés<!-- 1356374 -->|[Tech Preview 1710](capabilities-in-technical-preview-1710.md#check-compliance-from-software-center-for-co-managed-devices)|[Version 1710](/sccm/core/clients/manage/co-management-overview)    |
 |Prise en charge limitée des certificats CNG<!-- 1356191 -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md#limited-support-for-cng-certificates)|[Version 1710](/sccm/core/plan-design/network/cng-certificates-overview)    |
 |Prise en charge d’Exploit Guard<!--1355468 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#support-for-exploit-guard) |[Version 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)    |
 |Descriptions améliorées pour les redémarrages d’ordinateur en attente   <!-- 1356283  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[Version 1710](/sccm/core/clients/manage/manage-clients)    |
 |Modifications des stratégies Device Guard   <!-- 1355092  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[Version 1710](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)    |
 |Configurer et déployer des stratégies Windows Defender Application Guard   <!-- 1351960  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[Version 1710](/sccm/protect/deploy-use/create-deploy-application-guard-policy)    |
 |Améliorations du déploiement de scripts PowerShell à partir de Configuration Manager <!-- 1236459 -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md#improvements-for-deploying-powershell-scripts-from-configuration-manager) | [Version 1710](/sccm/apps/deploy-use/create-deploy-scripts)
 

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Fonctionnalités fournies dans les versions Technical Preview précédentes
Voici la liste des fonctionnalités spécifiques fournies avec les versions Technical Preview de Configuration Manager précédentes. Ces fonctionnalités restent disponibles dans les versions ultérieures, mais ne sont pas encore disponibles dans une version Current Branch. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |Fonctionnalité |Version Technical Preview |  
 |----------------|---------------------|
 |Expérience de profil VPN améliorée dans la console Configuration Manager <!-- 1313282 --> | [Tech Preview 1709](capabilities-in-technical-preview-1709.md) |
 |Management insights  <!-- 1353967 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#management-insights)|
 |Tableau de bord Surface <!-- 1355788 --> |[Tech Preview 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|
 |Rôle serveur site haute disponibilité <!-- 1128774 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |Prise en charge du démarrage réseau PXE pour IPv6 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |Évaluation de l’attestation de l’intégrité des appareils pour les stratégies de conformité pour l’accès conditionnel <!-- 1235616 -->|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|
 |Utiliser Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Évaluation de la conformité des mises à jour Windows Update pour Entreprise <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |Accès aux données de point de terminaison OData <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |Améliorations apportées à Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |Les utilisateurs finaux peuvent installer des applications à partir du portail d’entreprise <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>Voir aussi  
[Nouveautés de System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Présentation de System Center Configuration Manager](../../core/understand/introduction.md)
