---
title: Choisir quelle branche utiliser | System Center Configuration Manager
description: "Découvrez les différences entre les branches disponibles de System Center Configuration Manager."
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bbaaf9ed876f7693ea831be7c787dba904197a62
ms.openlocfilehash: 3957e854e980246c410f7de27caed9d66fc4829f


---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>Quelle branche de Configuration Manager dois-je utiliser ?

*S’applique à : System Center Configuration Manager (Current Branch), (Long-Term Servicing Branch), (version d’évaluation technique)*


Depuis octobre 2016, il existe trois branches disponibles de System Center Configuration Manager. Utilisez cette rubrique pour mieux choisir la branche qui vous convient.

## <a name="current-branch-of-system-center-configuration-manager"></a>Branche Current Branch de System Center Configuration Manager
Il s’agit d’une branche sous licence pour une utilisation dans un environnement de production dans lequel vous souhaitez pouvoir obtenir les dernières fonctionnalités. Il s’agit de la branche à utiliser lorsque vous disposez d’un des éléments suivants : System Center Datacenter, System Center Standard, System Center Configuration Manager ou les droits d’abonnement équivalents.  Pour plus d’informations sur les options de licence et Software Assurance, consultez [Licences et branches pour System Center Configuration Manager](learn-more-editions.md).


>  [!TIP]
> La branche Current Branch peut également être installée comme édition d’évaluation ne nécessitant pas de licence. Une édition d’évaluation peut être utilisée pendant 180 jours et prend en charge la mise à niveau vers une édition avec licence de Current Branch.

La branche Current Branch est mise à jour plusieurs fois par an avec de nouvelles fonctionnalités. Chaque version de mise à jour est prise en charge pour un (1) an après sa publication. Vous devez effectuer la mise à jour vers une version plus récente de Current Branch ou avant l’expiration de ce délai d’un (1) an. Les mises à jour vers des versions plus récentes sont proposées sous forme de mises à jour dans la console.

Pour installer Current Branch comme nouveau site ou mise à niveau à partir de *System Center 2012 Configuration Manager avec Service Pack 2* ou de *System Center 2012 R2 Configuration Manager avec Service Pack 1*, vous utilisez un [média de référence](/sccm/core/servers/manage/updates#baseline-and-update-versions) pour System Center Configuration Manager, qui se présente sous la forme d’un DVD avec System Center 2016 ou qui est disponible dans le cadre d’une version autonome de System Center Configuration Manager. L’accès à ce média dépend de la manière dont vous avez acquis la licence de System Center Configuration Manager.

Vous pouvez également utiliser le média de référence pour installer un nouveau site comme édition d’évaluation de Current Branch. Si vous souhaitez installer une édition d’évaluation uniquement, vous pouvez obtenir le logiciel à partir du site web [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

>  [!NOTE]
> Vous utilisez uniquement le média de référence pour installer des sites pour une nouvelle hiérarchie Configuration Manager. Si vous avez déjà installé une version de référence telle que la version 1511, des mises à jour dans la console vous permettent de mettre à jour vos sites vers une nouvelle version, telle que 1606.
>
> Les sites mis à jour à l’aide de mises à jour dans la console sont équivalents au nouveau site installé à l’aide du média de référence.
>
> Pour plus d’informations, consultez [Mises à jour pour System Center Configuration Manager](/sccm/core/servers/manage/updates).

**Caractéristiques de Current Branch :**
- Elle reçoit des [mises à jour dans la console](/sccm/core/servers/manage/install-in-console-updates) qui mettent à votre disposition de nouvelles fonctionnalités.
- Elle reçoit des mises à jour dans la console qui offrent des correctifs de sécurité et de qualité aux fonctionnalités existantes.
- Elle prend en charge les mises à jour hors bande lorsque cela est nécessaire. Consultez [Utiliser l’outil Inscription de la mise à jour](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes) ou [Utiliser le programme d’installation de correctif logiciel](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).
- Elle peut interagir avec Microsoft Intune, une autre infrastructure et d’autres services cloud.
- Elle prend en charge la [migration des données](/sccm/core/migration/migrate-data-between-hierarchies) vers et à partir d’autres installations de Configuration Manager.
- Elle prend en charge la mise à niveau à partir de versions précédentes de Configuration Manager.
- Elle prend en charge l’installation en tant qu’installation d’évaluation, à partir de laquelle vous pourrez ultérieurement effectuer une mise à niveau vers une installation sous licence.

La version 1511 était la version initiale de Current Branch. Les mises à jour ultérieures incluent les versions 1602, 1606, etc. Chaque version est prise en charge pendant un an et Microsoft vous recommande d’effectuer la mise à jour vers la dernière version peu après sa publication. Vous pouvez attendre jusqu’à une année avant d’effectuer la mise à jour vers une version plus récente et vous pouvez également ignorer une mise à jour pour installer la dernière version disponible. Comme chaque version est cumulative, si vous ignorez une mise à jour et installez la version la plus récente, vous bénéficiez tout de même de l’ensemble des fonctionnalités et améliorations apportées par les versions précédentes.

Pour plus d’informations, consultez [Prise en charge des versions Current Branch](/sccm/core/servers/manage/current-branch-versions-supported).

**Options de mise à jour :**
- Avec la Software Assurance active, vous pouvez installer des mises à jour dans la console pour les versions Current Branch.  
- Il n’existe aucune option permettant de convertir Current Branch en version d’évaluation technique. Les versions d’évaluation technique sont des installations distinctes qui ne nécessitent pas de licence.
- Il n’existe aucune option permettant de convertir votre version Current Branch en LTSB (Long-Term Servicing Branch). Vous devez désinstaller Current Branch, puis installer LTSB comme nouvelle installation.

##  <a name="long-term-servicing-branch-ltsb-of-system-center-configuration"></a>Branche LTSB (Long-Term Servicing Branch) de System Center Configuration
Il s’agit d’une branche sous licence à utiliser en production pour les clients Configuration Manager qui utilisent Current Branch et ont autorisé Configuration Manager Software Assurance (SA) ou leurs droits d’abonnement équivalents à expirer après le 1er octobre 2016.  Pour plus d’informations sur la Software Assurance et les options de licence, consultez [Licences et branches pour System Center Configuration Manager](learn-more-editions.md).

La branche LTSB ne reçoit pas de mises à jour dans la console fournissant de nouvelles fonctionnalités ou mettant à jour les fonctionnalités existantes. Toutefois, des correctifs de sécurité critiques sont fournis.

Pour installer la branche LTSB sous la forme d’un nouveau site ou d’une mise à niveau à partir d’un site Configuration Manager 2012 pris en charge, utilisez le [média de référence](/sccm/core/servers/manage/updates#baseline-and-update-versions) de la version 1606, que vous obtenez sous forme de DVD avec la version System Center 2016 ou System Center Configuration Manager (Current Branch et Long-Term Servicing Branch 1606). Vous pouvez utiliser le média de référence pour installer un nouveau site qui exécute la version 1606 de Current Branch ou un nouveau site qui exécute Long-Term Servicing Branch.

> [!TIP]  
> Pour en savoir plus sur System Center 2016, consultez la [documentation de System Center 2016](https://technet.microsoft.com/system-center-docs/System-Center-2016). Cette documentation indique également comment obtenir System Center 2016, qui requiert un contrat de licence Microsoft ou des droits similaires.  Vous pouvez également obtenir une version d’évaluation de System Center 2016 à partir du site [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).

**Fonctionnalités de la branche LTSB :**
-   Elle reçoit des mises à jour dans la console qui fournissent des correctifs de sécurité critiques.
- Elle fournit une option d’installation lorsque votre contrat SA ou vos droits équivalents sur Configuration Manager ont expiré.
- Elle prend en charge la mise à niveau (conversion) vers Current Branch lorsque vous disposez d’un contrat SA en cours ou de droits équivalents sur Configuration Manager.

**Limitations :**  
La branche LTSB est basée sur la version 1606 de Current Branch et présente les limitations suivantes :
- Vous bénéficiez pendant 10 ans de mises à jour de sécurité critiques pour la branche LTSB après sa mise à disposition générale (octobre 2016), après quoi le support de cette branche expire.  Pour plus d’informations sur la politique de support, consultez la page [Politique de support Microsoft](https://support.microsoft.com/en-us/lifecycle).
- Elle prend en charge une liste limitée de systèmes d’exploitation serveur et client et les technologies associées telles que les versions de SQL Server.  Pour plus d’informations sur ce qui est pris en charge avec cette branche, consultez [Configurations prises en charge pour la branche LTSB](supported-configurations-for-ltsb.md).
- Elle ne reçoit pas de mises à jour pour les nouvelles fonctionnalités.
- Elle ne prend pas en charge l’ajout d’un abonnement Microsoft Intune, ce qui vous empêche d’utiliser :
  - Intune dans une configuration de gestion des appareils mobiles hybride ;
 - Gestion des appareils mobiles locale
-   Elle ne prend pas en charge l’utilisation des plans de maintenance ni du tableau de bord de maintenance de Windows 10. Elle ne prend pas non plus en charge la branche CB (Current Branch) et la branche CBB (Current Branch for Business) de Windows 10.
- Elle ne prend pas en charge les futures versions de Windows 10 LTSB ni de Windows Server.
-   Elle ne prend pas en charge Asset Intelligence.
-   Elle ne prend pas en charge les points de distribution basés sur le cloud.
-   Elle ne prend pas en charge la prise en charge pour Exchange Online en tant que connecteur Exchange.
-   Elle ne prend en charge aucune fonctionnalité de la version préliminaire.



**Options de mise à jour :**
- Vous pouvez convertir votre installation LTSB en installation Current Branch. La conversion en On-premises MDM est prise en charge avant ou après l’expiration du support de la branche LTSB.

  Pour effectuer la conversion, vous devez disposer d’un contrat Software Assurance actif avec Microsoft.  Pour plus d’informations, suivez les liens ci-dessous :
  - [Mettre à niveau Long-Term Servicing Branch vers Current Branch](convert-to-current-branch.md)
  - [Licences et branches pour System Center Configuration Manager](learn-more-editions.md)
  - [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#baseline-and-update-versions) dans [Mises à jour pour Configuration Manager](/sccm/core/servers/manage/updates)
- Il n’existe aucune option permettant de convertir la branche LTSB vers une version d’évaluation technique. Les versions d’évaluation technique sont des installations distinctes qui ne nécessitent pas de licence.
-   Vous ne pouvez pas mettre à niveau une édition d’évaluation de Current Branch vers une installation LTSB.


## <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview pour System Center Configuration Manager
La version d’évaluation technique a été conçue pour être utilisée dans un environnement lab dans lequel vous souhaitez découvrir et tester les dernières fonctionnalités développées pour Configuration Manager. La version d’évaluation technique n’est pas prise en charge dans un environnement de production et n’exige pas que vous disposiez d’un contrat de licence Software Assurance.

Pour installer un nouveau site qui exécute la version d’évaluation technique, utilisez le dernier [média de référence de la version d’évaluation technique de System Center Configuration Manager](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview). Après avoir installé la version d’évaluation technique, de nouvelles versions sont proposées chaque mois en tant que mises à jour dans la console.

**Fonctionnalités de la version d’évaluation technique :**
-  Elle est basée sur les versions de référence récentes de Current Branch.
-  Elle reçoit des mises à jour dans la console pour mettre à jour votre installation vers la dernière version d’évaluation technique.
-  Elle inclut de nouvelles fonctionnalités qui sont en cours de développement et pour lesquelles nos développeurs souhaitent vos commentaires.
-  Elle reçoit des mises à jour qui s’appliquent uniquement à la branche de version d’évaluation technique.

**Limitations :**
-  [La prise en charge est limitée](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview), avec seulement un site principal et jusqu’à 10 clients.  
-  Elle ne peut pas être mise à niveau vers une branche CB ou LTSB.
-  Elle ne prend pas en charge l’utilisation de la migration pour importer ou exporter des données vers une autre installation de Configuration Manager.
-  Elle ne prend pas en charge la mise à niveau à partir d’une version précédente de Configuration Manager.
-  Elle ne gère pas l’installation comme installation d’évaluation.

Les fonctionnalités initialement introduites dans une version d’évaluation technique sont souvent ajoutées à Current Branch dans une mise à jour ultérieure.  Chaque nouvelle version d’évaluation technique inclut les fonctionnalités des versions d’évaluation technique précédentes, même après que ces fonctionnalités ont été ajoutées à Current Branch.

Pour plus d’informations, consultez [Version d’évaluation technique pour System Center Configuration Manager](/sccm/core/get-started/technical-preview).

**Options de mise à jour :**
-   Vous pouvez installer toute mise à jour dans la console pour une nouvelle version d’évaluation technique.
-   Il n’existe aucune option permettant de convertir une version d’évaluation technique en CB ou LTSB.



<!--HONumber=Nov16_HO1-->


