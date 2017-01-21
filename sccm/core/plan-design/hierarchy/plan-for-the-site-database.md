---
title: "Planifier la base de données du site | System Center Configuration Manager"
description: "Tenez compte de la base de données du site et son rôle serveur quand vous planifiez votre hiérarchie System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 40ebfaa9b82a65a6265f0c031dbbd0bcdb85da6e


---
# <a name="plan-for-the-site-database-for-system-center-configuration-manager"></a>Planifier la base de données du site pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Le serveur de bases de données du site est un ordinateur qui exécute une version prise en charge de Microsoft SQL Server qui stocke des informations pour les sites Configuration Manager. Chaque site d’une hiérarchie Configuration Manager contient une base de données du site et un serveur qui est attribué au rôle serveur de la base de données du site.  

-   Pour les sites d’administration centrale et les sites principaux, vous pouvez installer SQL Server sur le serveur de site, ou vous pouvez installer SQL Server sur un ordinateur autre que le serveur de site.  

-   Pour les sites secondaires, vous pouvez utiliser SQL Server Express plutôt que de procéder à l’installation complète de SQL Server. Toutefois, le serveur de base de données doit être exécuté sur le serveur de site secondaire.  

Si vous utilisez un ordinateur de serveur de base de données distante, vérifiez que la connexion réseau qui intervient est une connexion réseau à large bande passante et haute disponibilité. Cela s'explique par le fait que le serveur de site et certains rôles de système de site doivent communiquer en permanence avec le SQL Server qui héberge la base de données de site.  


**Lorsque vous sélectionnez un emplacement de serveur de base de données distant, tenez compte des éléments suivants :**  

-   La quantité de bande passante requise pour les communications avec le serveur de base de données dépend de l'association de nombreuses configurations de site et de client. Par conséquent, la bande passante réelle requise ne peut pas être déterminée correctement.  

-   Chaque ordinateur qui exécute le fournisseur SMS et qui se connecte à la base de données du site augmente les besoins en bande passante réseau.  

-   L'ordinateur qui exécute SQL Server doit se trouver dans un domaine qui entretient une relation d'approbation bidirectionnelle avec le serveur de site et tous les ordinateurs exécutant le fournisseur SMS.  

-   Vous ne pouvez pas utiliser un SQL Server en cluster pour le serveur de base de données de site lorsque la base de données de site se trouve au même emplacement que le serveur de site.  


Généralement, un serveur de système de site prend en charge des rôles système de site à partir d’un seul site Configuration Manager. Toutefois, vous pouvez utiliser différentes instances de SQL Server sur des serveurs en cluster ou non, exécutant SQL Server, pour héberger une base de données à partir de différents sites Configuration Manager. Pour prendre en charge des bases de données à partir de différents sites, vous devez configurer chaque instance de SQL Server afin qu'elle utilise des ports uniques pour la communication.  


**Les configurations SQL Server suivantes peuvent servir à héberger la base de données du site :**  

-   Instance par défaut de SQL Server  

-   Une instance nommée sur un seul ordinateur exécutant SQL Server  

-   Une instance nommée sur une instance en cluster de SQL Server  

-   Un groupe de disponibilité SQL Server AlwaysOn (depuis la version 1602)


**Conditions préalables pour la base de données du site :**  

-   Pour héberger la base de données du site, SQL Server doit remplir les conditions requises décrites dans [Prise en charge des versions de SQL Server pour System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  



<!--HONumber=Nov16_HO1-->


