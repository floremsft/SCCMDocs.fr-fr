---
title: "Sécurité et confidentialité pour les requêtes | Microsoft Docs"
description: "Maîtrisez les bonnes pratiques en matière de sécurité et de confidentialité quand vous recherchez des informations dans la base de données du site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e42b13c68ecaeac94245838c2f42e2790799de2b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Sécurité et confidentialité pour les requêtes dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, les requêtes vous permettent de récupérer des informations à partir de la base de données du site selon les critères que vous spécifiez. Configuration Manager collecte les informations de base de données de site pendant le fonctionnement standard. Par exemple, en utilisant les informations qui ont été collectées à partir de la découverte ou de l’inventaire, une requête peut être configurée pour identifier des périphériques qui répondent aux critères spécifiés.  

 Pour plus d’informations sur les requêtes, consultez [Présentation des requêtes dans System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Pour plus d’informations sur les bonnes pratiques en matière de sécurité et les informations de confidentialité pour les opérations Configuration Manager qui collectent les informations que vous pouvez récupérer à l’aide de requêtes, consultez [Sécurité et confidentialité pour System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Meilleures pratiques relatives à la sécurité pour les requêtes  
 Utilisez les meilleures pratiques de sécurité suivantes pour les requêtes.  

|Meilleure pratique de sécurité|Plus d'informations|  
|----------------------------|----------------------|  
|Lorsque vous exportez ou importez une requête qui est enregistrée dans un emplacement réseau, sécurisez l'emplacement et le canal de réseau.|Veillez à restreindre l'accès au dossier réseau.<br /><br /> Utilisez la signature SMB ou IPsec entre l’emplacement réseau et le serveur de site pour empêcher un intrus de falsifier les données de la requête avant leur importation.|  

## <a name="see-also"></a>Voir aussi  
 [Informations techniques de référence sur les requêtes pour System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)
