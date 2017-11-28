---
title: "Créer et déployer une stratégie Windows Defender Application Guard"
titleSuffix: Configuration Manager
description: "Créez et déployez une stratégie Windows Defender Application Guard."
ms.custom: na
ms.date: 11/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 
caps.latest.revision: "5"
author: ErikjeMS
ms.author: erikje
manager: angrobe
ms.openlocfilehash: db2508e5bbd1435fce432b6ef98d7968e68ea5ab
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="create-and-deploy-windows-defender-application-guard-policy----1351960---"></a>Créer et déployer une stratégie Windows Defender Application Guard <!-- 1351960 -->

Vous pouvez créer et déployer des stratégies [Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) à l’aide de la protection du point de terminaison Configuration Manager. Ces stratégies permettent de protéger vos utilisateurs en ouvrant les sites web non approuvés dans un conteneur isolé et sécurisé qui n’est pas accessible par les autres parties du système d’exploitation.

## <a name="prerequisites"></a>Conditions préalables

Pour créer et déployer une stratégie Windows Defender Application Guard, vous devez utiliser la mise à jour Windows 10 Fall Creators Update. De plus, les appareils Windows 10 sur lesquels vous déployez la stratégie doivent être configurés avec une stratégie d’isolement réseau. Pour plus d’informations, consultez [Vue d’ensemble de Windows Defender Application Guard](https://docs.microsoft.com/en-us/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview). Cette fonctionnalité fonctionne uniquement avec les versions actuelles de Windows 10 Insider. Pour la tester, vos clients doivent exécuter une version récente de Windows 10 Insider.


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Créez une stratégie et parcourez les paramètres disponibles :

1. Dans la console Configuration Manager, choisissez **Ressources et Conformité**.
2. Dans l’espace de travail **Biens et conformité**, choisissez **Vue d’ensemble** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une stratégie Windows Defender Application Guard**.
4. À l’aide du [billet de blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97) comme référence, vous pouvez parcourir et configurer les paramètres disponibles.
5. Dans la page **Définition du réseau**, spécifiez l’identité d’entreprise et définissez les limites du réseau de votre entreprise.

    > [!NOTE]
    > Les PC Windows 10 stockent une seule liste d’isolements réseau sur le client. Vous pouvez créer deux types différents de listes d’isolement réseau et les déployer sur le client :
    >
    >  - Un depuis Protection des informations Windows
    >  - Un depuis Windows Defender Application Guard
    >
    > Si vous déployez les deux stratégies, les listes d’isolements réseau doivent correspondre. Si vous déployez des listes qui ne correspondent pas au même client, le déploiement échoue. Pour plus d’informations, consultez la [documentation sur la protection des informations Windows](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
    > 
    > 

6. Lorsque vous avez terminé, terminez l’assistant et déployez la stratégie sur un ou plusieurs appareils Windows 10.

## <a name="next-steps"></a>Étapes suivantes
Pour en savoir plus sur Windows Defender Application Guard, consultez [ce billet de blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). En outre, pour en savoir plus sur le mode autonome de Windows Defender Application Guard, consultez [ce billet de blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).
