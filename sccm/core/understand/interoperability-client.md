---
title: "Utiliser le client d’interopérabilité étendue avec Current Branch "
titleSuffix: Configuration Manager
description: "Découvrez l’utilisation du client depuis Long-Term Servicing Branch dans Configuration Manager avec un site Current Branch."
ms.custom: na
ms.date: 08/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: ba79f2b9cf0cdfc4525645a647dddb624a0a5e5b
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Utiliser le logiciel client Gestionnaire de configuration pour l’interopérabilité étendue avec les futures versions d’un site Current Branch

*S’applique à : System Center Configuration Manager (Current Branch), (Long-Term Servicing Branch)*  

Dans certains cas, il est possible que vos stratégies d’entreprise ne vous permettent pas de mettre à jour régulièrement le client Gestionnaire de configuration sur certains PC. Par exemple, vous devrez peut-être respecter des stratégies de gestion des changements ; de même, l’appareil peut être stratégique.

Vous devez continuer à utiliser la mise à niveau automatique, dans la mesure du possible, pour la majorité de vos clients ; toutefois, à partir de la mise à jour 1610 du Gestionnaire de Configuration, vous pouvez répondre à ces besoins en installant un nouveau client, le client d’interopérabilité étendue, dans une perspective de long terme.

Le client d’interopérabilité étendue est compatible avec les sites Configuration Manager équipés de la version 1610 ou d’une version ultérieure. Il ne doit être utilisée que pour des PC qu’il n’est pas possible de mettre à jour fréquemment, comme des bornes ou des appareils de point de vente. Utilisez le dernier client Gestionnaire de configuration pour tous les autres PC.

## <a name="how-this-scenario-works"></a>Fonctionnement du scénario

En règle générale, quand vous installez une nouvelle mise à jour dans la console pour la branche CB (Current Branch), les clients mettent automatiquement à jour leur logiciel client pour pouvoir utiliser ces nouvelles fonctionnalités.

Avec ce scénario, vous utilisez la branche CB et recevez les nouvelles fonctionnalités et mises à jour. La plupart des clients exécutent le logiciel client à partir de la branche CB et peuvent le mettre à jour avec chaque mise à jour de version que vous installez. Toutefois, sur un sous-ensemble de systèmes critiques qui ne doivent pas recevoir les mises à jour du logiciel client, vous installez le client d’interopérabilité étendue. Ces clients n’installent pas de nouveau logiciel client tant que vous n’y avez pas explicitement déployé de nouvelle version du logiciel client.

>[!IMPORTANT]
>Le site Current Branch doit être équipé de la version 1610 ou d’une version ultérieure.

## <a name="how-to-use-the-eic"></a>Utilisation du client d’interopérabilité étendue

1. Récupérez le client d’interopérabilité étendue (version 5.00.8412) dans le dossier \SMSSETUP\Client du support d’installation de la mise à jour 1606 du Gestionnaire de Configuration. Veillez à copier tout le contenu du dossier.
2. Installez manuellement le client d’interopérabilité étendue sur ces appareils. [En savoir plus sur l’installation manuelle du client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).
3. Excluez ce regroupement des mises à niveau de clients.

>[!TIP]
>Pour rechercher la version 1606 de System Center Configuration Manager dans le Centre de gestion des licences en volume (VLSC), accédez à l’onglet **Téléchargements et clés** du centre [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), recherchez « system center config », puis sélectionnez **System Center Config Mgr (Current Branch et LTSB)**.

## <a name="the-extended-interoperability-client-software"></a>Logiciel client d’interopérabilité étendue

Le client d’interopérabilité étendue sera toujours pris en charge par les versions mises à jour de Configuration Manager Current Branch jusqu’au 18 novembre 2018 au minimum. Après cette date, consultez cette page pour plus d’informations sur le nouveau client d’interopérabilité étendue ou bien l’extension de la prise en charge du client d’interopérabilité étendue actuel.

>[!TIP]
>Le client d’interopérabilité étendue est pris en charge pendant au moins deux ans à partir de la date de publication (consultez la page [Prise en charge de System Center Configuration Manager Current Branch](/sccm/core/servers/manage/current-branch-versions-supported)). Par exemple, la prise en charge du client d’interopérabilité étendue actuel est de deux ans après la mise en production de la version 1610, le 18 novembre 2018.

Envisagez de mettre à jour le client d’interopérabilité étendue sur les appareils que vous gérez avec Current Branch avant que la prise en charge du client n’arrive à expiration. Pour cela, téléchargez une nouvelle version du client auprès de Microsoft, puis déployez ce logiciel client mis à jour sur vos appareils qui utilisent le client d’interopérabilité étendue actuel.

## <a name="limitations-of-the-extended-interoperability-client"></a>Limitations du client d’interopérabilité étendue

- Les mises à jour du logiciel client d’interopérabilité étendue ne sont pas disponibles par le biais des mises à jour dans la console. Des informations supplémentaires pour le déploiement d’un logiciel client mis à jour sont fournies lors de la publication d’un client mis à jour.
- Le client d’interopérabilité étendue prend uniquement en charge les mises à jour logicielles, l’inventaire et les packages et programmes.

## <a name="next-steps"></a>Étapes suivantes

Utilisez les informations du [Guide pratique pour surveiller les clients](/sccm/core/clients/manage/monitor-clients) pour vérifier que les clients sont installés correctement sur les appareils que vous souhaitez.
