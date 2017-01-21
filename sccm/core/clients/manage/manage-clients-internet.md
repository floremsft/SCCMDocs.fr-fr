---
title: "Gérer les clients | Internet | Passerelle de gestion cloud | Microsoft Docs"
description: 
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: e71ae1f654fcf3dd8c57a299c727588eed26ccac

---

# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Gérer les clients sur Internet avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

En général, dans Configuration Manager, la plupart des ordinateurs et serveurs gérés se trouvent physiquement sur le même réseau d’entreprise ou privé interne que les serveurs de système de site qui exécutent des fonctions de gestion. Toutefois, vous pouvez gérer les ordinateurs clients en dehors de votre réseau d’entreprise s’ils sont connectés à Internet sans obliger les clients à se connecter via des réseaux privés virtuels pour atteindre les serveurs de système de site.

Configuration Manager fournit deux façons de gérer les clients connectés à Internet :

-   Passerelle de gestion cloud

-   Gestion des clients basés sur Internet

## <a name="cloud-management-gateway"></a>Passerelle de gestion cloud

Depuis la version 1610, Configuration Manager présente la passerelle de gestion cloud. Cette nouvelle méthode fournit un moyen de gérer les clients Internet en combinant un service cloud déployé sur Microsoft Azure et un nouveau rôle de système de site qui communique avec ce service. Les clients utilisent ensuite le service pour communiquer avec Configuration Manager.

Avantages :

-   Aucun investissement n’est nécessaire pour l’infrastructure supplémentaire.

-   L’infrastructure locale n’est pas exposée sur Internet.

-   Les machines virtuelles du cloud qui exécutent le service sont entièrement gérées par Azure et ne nécessitent aucune maintenance.

-   Installation et configuration faciles dans la console Configuration Manager.

Inconvénients :

-   Coût de l’abonnement au cloud.

-   Données de gestion envoyées via le service cloud.

Pour plus d’informations, consultez [Planifier la passerelle de gestion cloud](plan-cloud-management-gateway.md).

## <a name="internet-based-client-management"></a>Gestion des clients basés sur Internet

Cette méthode s’appuie sur les serveurs de système de site Internet avec lesquels les clients communiquent à des fins de gestion. Elle nécessite que les clients et serveurs de système de site soient configurés pour une gestion basée sur Internet.

Avantages :

-   Aucune dépendance du service cloud.

-   Aucun coût supplémentaire associé à un abonnement au cloud.

-   Contrôle total des serveurs et rôles assurant le service.

Inconvénients :

-   Un investissement est nécessaire pour l’infrastructure supplémentaire.

-   Frais généraux et coût opérationnel de l’infrastructure supplémentaire.

-   L’infrastructure doit être exposée sur Internet.

Pour plus d’informations, consultez [Planifier la gestion des clients basés sur Internet](plan-internet-based-client-management.md).



<!--HONumber=Dec16_HO3-->


