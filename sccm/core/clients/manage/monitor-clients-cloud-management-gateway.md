---
title: Surveiller la passerelle de gestion cloud - Configuration Manager | Microsoft Docs
description: 
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: ef12c9b966a1b83b61243311b30e1a925c20d2e3
ms.openlocfilehash: 4475205c37c20631a189e0c315dc48e288c15ba6

---

# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Surveiller la passerelle de gestion cloud dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Depuis la version 1610, une fois que le service de passerelle de gestion cloud est en cours d’exécution et que les clients se connectent par son intermédiaire, vous pouvez surveiller le trafic réseau et les clients pour vérifier que le service fonctionne comme vous pensez qu’il fonctionne.

## <a name="monitor-clients"></a>Surveiller les clients

Les clients connectés via le service de passerelle de gestion cloud s’affichent dans la console Configuration Manager de la même façon que les clients locaux. Pour plus d’informations, consultez [Guide pratique pour surveiller des clients](monitor-clients.md).

## <a name="monitor-traffic-in-the-console"></a>Surveiller le trafic dans la console

Vous pouvez surveiller le trafic sur la passerelle de gestion cloud à l’aide de la console Configuration Manager :

1. Accédez à **Administration > Services cloud > Passerelle de gestion cloud**.

2. Sélectionnez le service de passerelle de gestion cloud dans le volet Liste.

3. Affichez les informations de trafic dans le volet Détails pour le rôle de connexion de passerelle de gestion cloud et les rôles de système de site auxquels il se connecte.

## <a name="set-up-outbound-traffic-alerts"></a>Configurer des alertes de trafic sortant

Les alertes de trafic sortant vous permettent de savoir quand le trafic est proche d’un niveau de seuil de 14 jours (2 semaines). Vous avez la possibilité de configurer des alertes de trafic quand vous créez le service de passerelle de gestion cloud. Si vous avez ignoré cette partie, vous pouvez toujours configurer les alertes une fois que le service est en cours d’exécution. Vous pouvez également régler les paramètres d’alerte à tout moment.

1. Accédez à **Administration > Services cloud > Passerelle de gestion cloud**.

2. Cliquez avec le bouton droit sur le service de passerelle de gestion cloud dans le volet Liste, puis choisissez **Propriétés**.

3. Cliquez sur l’onglet Alertes, puis choisissez d’activer (ou de désactiver) le seuil et les alertes. Spécifiez ensuite le seuil de 14 jours (en Go) et les pourcentages du seuil pour déclencher les différents niveaux d’alerte.

4. Cliquez sur **OK** quand vous avez terminé.

## <a name="monitor-logs"></a>Surveiller les journaux

Le service de passerelle de gestion cloud génère des entrées dans les fichiers journaux suivants :

-   **Cloudmgr.log** : contient des entrées pour le déploiement du service de passerelle de gestion cloud, l’état du service en cours et les données d’utilisation associées au service.

-   **SMS\_Cloud\_ProxyConnector.log** : contient des entrées pour la configuration des connexions entre le service de passerelle de gestion cloud et le point de connexion de passerelle de gestion cloud.

Pour plus d’informations, consultez [Fichiers journaux dans System Center Configuration Manager](/sccm/core/plan-design/hierarchy/log-files).



<!--HONumber=Jan17_HO4-->


