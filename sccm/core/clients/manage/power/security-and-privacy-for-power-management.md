---
title: "Sécurité et confidentialité pour la gestion de l’alimentation"
titleSuffix: Configuration Manager
description: "Obtenir des informations de sécurité et de confidentialité pour la gestion de l’alimentation dans System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
caps.latest.revision: "5"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 5de0ed261b3069306992eeddb4b71b3fe22f197c
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="security-and-privacy-for-power-management-in-system-center-configuration-manager"></a>Sécurité et confidentialité pour la gestion de l’alimentation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette section contient des informations de sécurité et de confidentialité pour la gestion de l’alimentation dans System Center Configuration Manager.  

## <a name="security-best-practices-for-power-management"></a>Meilleures pratiques de sécurité pour la gestion de l’alimentation  
 Il n'existe aucune meilleure pratique liée à la sécurité pour la gestion de l'alimentation.  

## <a name="privacy-information-for-power-management"></a>Informations de confidentialité pour la gestion de l’alimentation  
 La gestion de l’alimentation utilise des fonctionnalités intégrées à Windows pour surveiller la consommation d’énergie et appliquer des paramètres d’alimentation à des ordinateurs pendant les heures de bureau et les heures creuses. Configuration Manager collecte des informations sur la consommation d’énergie auprès des ordinateurs, incluant des données sur périodes d’utilisation des ordinateurs par les utilisateurs. Bien que Configuration Manager surveille la consommation d’énergie pour un regroupement plutôt que pour chaque ordinateur, un regroupement peut contenir un seul ordinateur. La gestion de l'alimentation n'est pas activée par défaut et doit être configurée par un administrateur.  

 Les informations sur la consommation d’énergie sont stockées dans la base de données Configuration Manager et ne sont pas envoyées à Microsoft. Les informations détaillées sont conservées dans la base de données pendant 31 jours et les informations résumées sont conservées pendant 13 mois. Vous ne pouvez pas configurer l'intervalle de suppression.  

 Avant de configurer la gestion de l'alimentation, pensez à vos besoins en matière de confidentialité.  
