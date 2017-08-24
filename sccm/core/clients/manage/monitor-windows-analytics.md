---
title: Suivre les clients - Utiliser Windows Analytics avec Configuration Manager | Microsoft Docs
description: "Windows Analytics est un ensemble de solutions qui s’exécutent sur Operations Management Suite et qui vous permettent d’obtenir des insights utiles sur l’état actuel de votre environnement en exploitant les données de télémétrie Windows envoyées par les appareils de votre environnement."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
caps.latest.revision: "23"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: adabe8f475eb12dd44005ec07344e8565be20582
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2017
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Utiliser Windows Analytics avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

[Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) est un ensemble de solutions qui s’exécutent sur [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview). Les solutions vous permettent d’obtenir des insights sur l’état actuel de votre environnement. Les appareils de votre environnement envoient des données de télémétrie Windows. Ces données sont exploitées et analysées au moyen de solutions dans le [portail web Operations Management Suite](https://mms.microsoft.com). Dans le cadre d’[Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics), vous pouvez configurer les données pour les rendre directement accessibles dans le nœud de surveillance de la console Configuration Manager en connectant Upgrade Readiness à Configuration Manager.

Les données de télémétrie Windows utilisées par Windows Analytics ne sont pas transférées directement au serveur de site Configuration Manager. Les ordinateurs clients envoient les données de télémétrie Windows au service de télémétrie. Les données pertinentes sont ensuite transférées aux solutions Windows Analytics hébergées dans l’un des espaces de travail OMS de votre organisation. Configuration Manager peut alors soit vous diriger vers les données pertinentes dans le portail web avec des liens en contexte, soit afficher directement les données qui font partie de solutions connectées à Configuration Manager. Vous pouvez également exécuter directement des requêtes sur les données à partir du portail web Operation Management Suite.

>[!Important]
>Les [données de diagnostic et d’utilisation Configuration Manager](../../plan-design/diagnostics/diagnostics-and-usage-data.md), qui sont envoyées à Microsoft à partir du serveur de site Configuration Manager, n’ont rien à voir avec Windows Analytics et la télémétrie Windows.

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Configurer les clients pour envoyer des données à Windows Analytics

Pour que les appareils clients envoient des données à Windows Analytics, ils doivent être configurés avec une clé d’ID commercial associée à l’espace de travail Operations Management Suite qui héberge les données Windows Analytics de votre organisation. Vous devez également configurer les appareils pour qu’ils envoient les données de télémétrie à un niveau approprié pour la ou les solutions que vous souhaitez utiliser. 

### <a name="configure-windows-analytics-client-settings"></a>Configurer les paramètres client Windows Analytics
Pour configurer Windows Analytics, dans la console Configuration Manager, choisissez **Administration** > **Paramètres client**, double-cliquez sur **Créer des paramètres client d’appareil personnalisés par défaut**, puis cochez **Windows Analytics**.  

Accédez à l’onglet des paramètres **Windows Analytics** puis configurez les éléments suivants :
  -  **ID commercial**  
La clé d’ID commercial mappe les informations des appareils que vous gérez à l’espace de travail OMS qui héberge les données Windows Analytics de votre organisation. Si vous avez déjà configuré une clé d’ID commercial avec Upgrade Readiness, utilisez cet ID. Si vous ne disposez pas encore d’une clé ID commercial, consultez [Générer une clé d’ID commercial]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

  -  **Niveau de télémétrie pour les appareils Windows 10**   
Pour plus d’informations sur les données collectées par chaque niveau de télémétrie Windows 10, consultez [Configurer la télémétrie Windows dans votre organisation](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

  -  **Participer à la collecte de données commerciales sur les appareils Windows 7, 8 et 8.1**   
Pour plus d’informations sur les données collectées à partir de ces systèmes d’exploitation quand vous choisissez de participer, téléchargez le fichier .pdf [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) disponible sur le site web de Microsoft.

  -  **Configurer la collecte de données dans Internet Explorer**  
Sur les appareils Windows 8.1 ou antérieur, la collecte de données dans Internet Explorer permet à Upgrade Readiness de détecter les incompatibilités d’application web qui risquent d’entraver la mise à niveau vers Windows 10. La collecte des données dans Internet Explorer peut être activée pour chaque zone internet. Pour plus d’informations sur les zones internet, consultez [À propos des zones de sécurité des URL](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx).

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Utiliser Upgrade Readiness pour identifier les problèmes de compatibilité avec Windows 10

Upgrade Readiness (anciennement Upgrade Analytics) vous permet d’analyser l’état de préparation des appareils et leur compatibilité avec Windows 10. Cette évaluation permet d’optimiser les mises à niveau. Après avoir connecté Configuration Manager à Upgrade Readiness, vous pouvez accéder directement aux données de compatibilité de mise à niveau du client dans la console Configuration Manager. Vous pouvez ensuite cibler des appareils pour la mise à niveau ou la mise à jour dans la liste d’appareils.

Pour plus d’informations sur la configuration de la solution Upgrade Readiness et la connexion à celle-ci, consultez [Upgrade Readiness](../../clients/manage/upgrade/upgrade-analytics.md).

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Utiliser Windows Analytics pour identifier les écarts dans les stratégies de Protection des informations Windows

Les appareils Windows 10 version 1703 et ultérieure configurés avec une stratégie [Protection des informations Windows](https://docs.microsoft.com/en-us/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) envoient des données de télémétrie sur les applications qui accèdent aux données d’entreprise de votre environnement, mais qui ne sont pas prises en compte dans les règles d’application de la stratégie WIP. Il peut s’agir d’applications dont les utilisateurs de votre environnement ont besoin pour rester productifs, mais dont l’accès est bloqué. Il peut donc être utile de savoir que ces applications accèdent à des données d’entreprise dans le cadre de la maintenance de vos stratégies Protection des informations Windows dans Configuration Manager. 

Pour accéder à ces données Protection des informations Windows, utilisez cette [requête Operations Management Suite](https://go.microsoft.com/fwlink/?linkid=849952).