---
title: "Sécurité et confidentialité des regroupements | Microsoft Docs"
description: "Obtenir les bonnes pratiques de sécurité et de confidentialité des regroupements dans System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
caps.latest.revision: 5
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 3379494824804c6be5c051c67a79d25e7eed88f0
ms.contentlocale: fr-fr
ms.lasthandoff: 12/16/2016


---
# <a name="security-and-privacy-for-collections-in-system-center-configuration-manager"></a>Sécurité et confidentialité pour les regroupements dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique contient les bonnes pratiques en matière de sécurité et les informations de confidentialité pour les regroupements dans System Center Configuration Manager.  

 Il n'existe aucune information de confidentialité spécifique pour les regroupements dans Configuration Manager. Les regroupements sont des conteneurs pour les ressources, telles que les utilisateurs et les appareils. L'appartenance à un regroupement dépend souvent des informations recueillies par Configuration Manager pendant le fonctionnement standard. Par exemple, en utilisant les informations sur les ressources qui ont été collectées à partir de la découverte ou de l'inventaire, un regroupement peut être configuré pour renfermer les appareils qui répondent aux critères spécifiés. Les regroupements peuvent également reposer sur les informations d'état actuelles pour les opérations de gestion de client, telles que le déploiement de logiciels et la vérification de la compatibilité. En plus de ces regroupements basés sur des requêtes, les utilisateurs administratifs peuvent également ajouter des ressources aux regroupements.  

 Pour plus d'informations sur les regroupements, voir [Présentation des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md). Pour plus d'informations sur les bonnes pratiques en matière de sécurité et les informations de confidentialité pour les opérations Configuration Manager qui peuvent être utilisées pour configurer l'appartenance à des regroupements, voir [Bonnes pratiques en matière de sécurité et informations de confidentialité pour System Center Configuration Manager](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md).  

## <a name="security-best-practices-for-collections"></a>Meilleures pratiques de sécurité pour les regroupements  
 Utilisez la meilleure pratique de sécurité suivante pour les regroupements.  

|Meilleure pratique de sécurité|Plus d'informations|  
|----------------------------|----------------------|  
|Lorsque vous exportez ou importez un regroupement à l'aide d'un fichier au format d'objet géré (MOF) qui est enregistré dans un emplacement réseau, sécurisez l'emplacement et le canal de réseau.|Veillez à restreindre l'accès au dossier réseau.<br /><br /> Utilisez la signature SMB ou IPsec entre l'emplacement réseau et le serveur de site pour empêcher un intrus de falsifier les données de regroupement exportées. Utilisez IPsec pour chiffrer les données sur le réseau afin d'éviter la divulgation d'informations.|  

### <a name="security-issues-for-collections"></a>Problèmes de sécurité pour les regroupements  
 Les regroupements présentent les problèmes de sécurité suivants :  

-   Si vous utilisez des variables de regroupement, les administrateurs locaux peuvent lire des informations potentiellement sensibles.  

     Les variables de regroupement peuvent être utilisées lorsque vous déployez un système d'exploitation.  

