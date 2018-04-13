---
title: Prise en charge de Windows 10
titleSuffix: Configuration Manager
description: Découvrir les versions de Windows 10 prises en charge comme clients ou pour OSD avec System Center Configuration Manager
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 877732c4095438b19a863335a4a0026b7b088b24
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2018
---
# <a name="support-for-windows-10-in-system-center-configuration-manager"></a>Prise en charge de Windows 10 dans System Center Configuration Manager  

*S’applique à : System Center Configuration Manager (Current Branch)*


Découvrez les versions de Windows 10 prises en charge par Configuration Manager, notamment :
 -  Windows 10 comme client Configuration Manager
 -  Kit de déploiement et d'évaluation Windows (ADK) pour Windows 10

## <a name="windows-10-as-a-client"></a>Windows 10 comme client
Configuration Manager tente d’assurer une prise en charge comme client pour chaque nouvelle version de Windows 10 dès que possible après sa publication. Étant donné que les produits ont des calendriers de développement et de publication distincts, la prise en charge assurée par Configuration Manager dépend du moment de leur mise en circulation respective.

Par exemple, une version de Configuration Manager est supprimée de la matrice quand la [prise en charge de cette version](/sccm/core/servers/manage/current-branch-versions-supported) se termine. De même, la prise en charge de versions de Windows 10 comme Enterprise 2015 LTSB or 1511 est supprimée de la matrice quand elles seront retirées de la prise en charge. Pour plus d’informations, consultez [Systèmes d’exploitation dépréciés](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).


-   Les informations suivantes viennent s’ajouter à [Systèmes d’exploitation pris en charge pour les clients et appareils](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
-   Si vous utilisez LTSB (Long Term Servicing Branch) de Configuration Manager, consultez [Configurations prises en charge pour Long Term Servicing Branch](/sccm/core/understand/supported-configurations-for-ltsb).

| Version de Windows 10 | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802 |
|---------------------|-----|-----|-----|
| Enterprise 2015 LTSB            <!--10/14/2025-->   | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| Entreprise 2016 LTSB            <!--10/13/2026-->   | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| 1607   <br />(*voir éditions*)   <!--04/10/2018-->   | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| 1703   <br />(*voir éditions*)   <!--10/09/2018-->   | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| 1709   <br />(*voir éditions*)   <!--04/09/2019-->   | ![Compatibilité descendante](media/blue_compat.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

**Éditions :** Entreprise, Professionnel, Éducation, Professionnel Éducation   

|Clé|
|--|
|![Pris en charge](media/green_check.png) = **Pris en charge**  |
|![À compatibilité descendante](media/blue_compat.png)  = **À compatibilité descendante** : les fonctionnalités de gestion du client existantes devraient fonctionner avec la nouvelle version de Windows 10. Par exemple, l’inventaire matériel, l’inventaire logiciel et les mises à jour logicielles. Nous documentons tous problèmes connus ou mises en garde. <br><br>Cette approche vous offre la possibilité de déployer et de gérer de nouvelles versions de Windows immédiatement avec prise en charge de la compatibilité des applications et sans nécessiter de nouvelle version de mise à jour de Configuration Manager. |
|![Non pris en charge](media/Red_X.png) = **Non pris en charge**|

 > [!NOTE]
 > À compter de la version 1802, Configuration Manager prend en charge le client sur les appareils Windows 10 ARM64. Les fonctionnalités de gestion du client existantes devraient fonctionner avec ces nouveaux appareils, par exemple, l’inventaire matériel et logiciel, les mises à jour logicielles et la gestion des applications. Le déploiement de système d’exploitation n’est pas pris en charge pour le moment. <!-- 1353704 --> 



## <a name="windows-10-adk"></a>Windows 10 ADK
Quand vous déployez des systèmes d’exploitation avec Configuration Manager, le [Windows ADK est une dépendance externe](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) obligatoire.

Le tableau suivant répertorie les versions du Windows 10 ADK que vous pouvez utiliser avec différentes versions de Configuration Manager.

| Version de Windows 10 ADK  | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802   |
|--------------------|-----|-----|-----|
| 1607  | ![Non pris en charge](media/Red_X.png)   | ![Non pris en charge](media/Red_X.png) | ![Non pris en charge](media/Red_X.png) |
| 1703  | ![Pris en charge](media/green_check.png) | ![Compatibilité descendante](media/blue_compat.png) | ![Compatibilité descendante](media/blue_compat.png) |
| 1709  | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |

|Clé|
|--|
|![Prise en charge](media/green_check.png) = **Prise en charge** : Windows recommande d’utiliser le Windows ADK qui correspond à la version de Windows que vous déployez. Par exemple, utilisez le Windows ADK pour Windows 10 version 1703 quand vous déployez Windows 10 version 1703. Pour plus d’informations sur la prise en charge du composant Windows ADK, consultez [Plateformes prises en charge par DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) et [Exigences de l’outil USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
|![Compatibilité descendante](media/blue_compat.png)  = **Compatibilité descendante** : cette combinaison n’a pas été testée, mais elle devrait fonctionner. Nous documentons tous problèmes connus ou mises en garde. |
|![Non pris en charge](media/Red_X.png) = **Non pris en charge**|

 > [!Note]
 > Configuration Manager prend uniquement en charge les composants x86 et amd64 de Windows 10 ADK. Il ne prend actuellement pas en charge les composants arm ou arm64. 