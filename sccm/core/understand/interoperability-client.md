---
title: "Utiliser le client d’interopérabilité étendue avec Current Branch | System Center Configuration Manager"
description: "Découvrez l’utilisation du client depuis Long-Term Servicing Branch dans Configuration Manager avec un site Current Branch."
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
Robots: NOINDEX,NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: 45ef4be7bf0b1c2e99f25ac398265bb71489c17e
ms.openlocfilehash: a97eb7a637611ba269cf8f16635b8165c19283f1

---
# <a name="use-the-client-software-from-the-version-1606-baseline-media-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Utiliser le logiciel client issu du support de la base de référence de la version 1606 pour l’interopérabilité étendue avec les futures versions d’un site Current Branch

*S’applique à : System Center Configuration Manager (Current Branch), (Long-Term Servicing Branch)*  

Vous pouvez utiliser le logiciel client Configuration Manager pour les ordinateurs Windows (client.msi) à partir du support DVD de la base de référence de la version 1606 que vous obtenez avec System Center 2016 ou à partir d’une version de System Center Configuration Manager (Current Branch et Long-Term Servicing Branch 1606) pour gérer les appareils appartenant à un site Current Branch. Ce client s’appelle le client d’interopérabilité étendue.

## <a name="how-this-scenario-works"></a>Fonctionnement de ce scénario :
En règle générale, quand vous installez une nouvelle mise à jour dans la console pour la branche CB (Current Branch), les clients mettent automatiquement à jour leur logiciel client pour pouvoir utiliser ces nouvelles fonctionnalités.

Avec ce scénario, vous utilisez la branche CB et recevez les nouvelles fonctionnalités et mises à jour. La plupart des clients exécutent le logiciel client à partir de la branche CB et peuvent le mettre à jour avec chaque mise à jour de version que vous installez. Toutefois, sur un sous-ensemble de systèmes critiques qui ne doivent pas recevoir les mises à jour du logiciel client, vous installez le client d’interopérabilité étendue. Ces clients n’installent pas le nouveau logiciel client tant que vous n’avez pas explicitement déployé une nouvelle version du logiciel client pour eux.

D’autres informations sur la façon d’empêcher les clients Current Branch de se mettre à jour automatiquement quand vous installez une nouvelle version de Configuration Manager seront disponibles avec la version Current Branch 1610.

Le site Current Branch doit exécuter la version 1606 ou ultérieure.

## <a name="the-extended-interoperability-client-software"></a>Logiciel client d’interopérabilité étendue
Quand vous utilisez le client d’interopérabilité étendue de System Center 2016 ou System Center Configuration Manager (Current Branch et Long-Term Servicing Branch 1606) avec un site Current Branch, le client est pris en charge pendant deux ans à l’issue de la disponibilité générale de la version du 12 octobre 2016.

Envisagez de mettre à jour le client d’interopérabilité étendue sur les appareils que vous gérez avec Current Branch avant que la prise en charge du client n’arrive à expiration. Pour cela, vous téléchargez une nouvelle version du client auprès de Microsoft, puis vous déployez ce logiciel client mis à jour sur vos appareils qui utilisent le client d’interopérabilité étendue actuel.

**Limitations du client d’interopérabilité étendue :**
-   Les mises à jour du logiciel client d’interopérabilité étendue ne sont pas disponibles par le biais des mises à jour dans la console. Des informations supplémentaires pour le déploiement d’un logiciel client mis à jour seront fournies lors de la publication d’un client mis à jour.

## <a name="identify-the-client-version-you-use"></a>Identifier la version du client que vous utilisez
Voici les principales versions du client disponibles pour Current Branch et LTSB :

|Version du client|Branche et version |  
|----------------|---------------------|
|5.00.8325.xxxx |   - Current Branch 1511|
|5.00.8355.xxxx |- Current Branch 1602|
|5.00.8412.1307 |- Current Branch 1606 </br> - Current Branch 1606 avec le correctif cumulatif 1606 (KB3186654)</br>- Client d’interopérabilité étendue issu du support de la base de référence de la version 1606|  

Sur le client, vous pouvez afficher sa version sous l’onglet **Général** de l’applet du Panneau de configuration de Configuration Manager.

Sous l’onglet **Composants** de l’applet, certains composants affichent des valeurs différentes. Par exemple, pour une version du client 8412.1307, certains composants peuvent comporter une indication 5.00.8412.**1000** ou 5.00.8412.**1006**.  Une différence dans les quatre derniers chiffres de certains composants est normale et n’indique pas une défaillance du composant de mise à jour vers la version actuelle du client.



<!--HONumber=Nov16_HO1-->


