---
title: Prise en charge de Windows 10
titleSuffix: Configuration Manager
description: "Découvrez-en plus sur les versions de Windows 10 prises en charge comme clients ou pour OSD avec System Center Configuration Manager."
ms.custom: na
ms.date: 10/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: "5"
author: brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8ce7230a3aa64b78937b305fee4dc8e3f38abead
ms.sourcegitcommit: f9c38b87fcd543ab8a5d7a7f446b42fd3e55450c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2017
---
# <a name="support-for-windows-10-for-system-center-configuration-manager"></a>Prise en charge de Windows 10 pour System Center Configuration Manager  

*S’applique à : System Center Configuration Manager (Current Branch)*


 Cette rubrique détaille les versions de Windows 10 utilisables avec les différentes versions de System Center Configuration Manager Current Branch. Les opérations à effectuer sont les suivantes :
 -  Windows 10 comme client Configuration Manager.
 -  Windows ADK (Kit de déploiement et d’évaluation Windows) pour Windows 10.

## <a name="windows-10-as-a-client"></a>Windows 10 comme client
Configuration Manager tente d’assurer la prise en charge en tant que client de chaque nouvelle version de Windows 10 dès que possible après sa publication. Étant donné que les produits ont des calendriers de développement et de publication distincts, la prise en charge assurée par Configuration Manager dépend du moment de leur mise en circulation respective.

Par exemple, une version de Configuration Manager sera supprimée de la matrice lorsque la [prise en charge de cette version](/sccm/core/servers/manage/current-branch-versions-supported) se termine. De même, la prise en charge de versions de Windows 10 comme Enterprise 2015 LTSB or 1511 sera supprimée de la matrice lorsqu’elles seront retirées de la prise en charge. Pour plus d’informations, consultez [Systèmes d’exploitation déconseillés](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems).

-   Les informations suivantes viennent s’ajouter à [Systèmes d’exploitation pris en charge pour les clients et appareils](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
-   Si vous utilisez LTSB (Long Term Servicing Branch) de Configuration Manager, consultez [Configurations prises en charge pour Long Term Servicing Branch](/sccm/core/understand/supported-configurations-for-ltsb).

|Version de Windows 10                    |Configuration Manager 1610          |    Configuration Manager 1702          |    Configuration Manager 1706 |
|---------------------|-----|-----|-----|
|Entreprise 2015 LTSB                   |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |
|Entreprise 2016 LTSB                   |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |
|1607   <br />(également appelée Mise à jour anniversaire)<br />(*voir éditions*)   |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png)            |![Pris en charge](media/green_check.png) |
|1703   <br />(également appelée Creators Update)<br />(*voir éditions*)      |![Non pris en charge](media/Red_X.png)   |![Compatibilité descendante](media/blue_compat.png) |![Pris en charge](media/green_check.png) |
|1709   <br />(également appelée Fall Creators Update)<br />(*voir éditions*) |![Non pris en charge](media/Red_X.png)   |![Non pris en charge](media/Red_X.png)   |![Compatibilité descendante](media/blue_compat.png) |



**Éditions :** Entreprise, Professionnel, Éducation, Professionnel Éducation   

|Clé|
|--|
|![Prise en charge](media/green_check.png) = **Prise en charge**  |
|![Pas de prise en charge](media/blue_compat.png)  = **Compatibilité descendante** : cela signifie que les fonctionnalités de gestion du client existantes (inventaire matériel, inventaire logiciel, mises à jour logicielles, etc.) doivent fonctionner avec la nouvelle version de Windows 10. Les mises en garde ou problèmes connus seront documentés. <br><br>Cette approche vous offre la possibilité de déployer et de gérer de nouveaux builds Windows dès le premier jour avec prise en charge de la compatibilité des applications sans nécessiter de nouvelle version de mise à jour de Configuration Manager. |
|![Prise en charge](media/Red_X.png) = **Pas de prise en charge**|


## <a name="windows-10-adk"></a>Windows 10 ADK
Quand vous déployez des systèmes d’exploitation avec Configuration Manager, le [Windows ADK est une dépendance externe](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) obligatoire.

Le tableau suivant répertorie les versions du Windows 10 ADK que vous pouvez utiliser avec différentes versions de Configuration Manager.

|Version de Windows 10 ADK  |Configuration Manager 1610 |Configuration Manager 1702   |Configuration Manager 1706 |
|--------------------|-----|-----|-----|
|1607  |![Pris en charge](media/green_check.png)           |![Compatibilité descendante](media/blue_compat.png) |![Non pris en charge](media/Red_X.png)|
|1703  |![Non pris en charge](media/Red_X.png)             |![Pris en charge](media/green_check.png)            |![Pris en charge](media/green_check.png) |  
|1709  |![Non pris en charge](media/Red_X.png)             |![Non pris en charge](media/Red_X.png)              |![Pris en charge](media/green_check.png) |  

|Clé|
|--|
|![Prise en charge](media/green_check.png) = **Prise en charge** : Windows recommande d’utiliser le Windows ADK qui correspond à la version de Windows que vous déployez. Par exemple, utilisez le Windows ADK pour Windows 10 version 1703 quand vous déployez Windows 10 version 1703.  |
|![Compatibilité descendante](media/blue_compat.png)  = **Compatibilité descendante** : cette combinaison n’a pas été testée, mais elle devrait fonctionner. Les mises en garde ou problèmes connus seront documentés. |
|![Prise en charge](media/Red_X.png) = **Pas de prise en charge**|
