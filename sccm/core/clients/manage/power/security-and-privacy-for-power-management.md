---
title: "Sécurité et confidentialité pour la gestion de l’alimentation | Microsoft Docs"
description: "Obtenir des informations de sécurité et de confidentialité pour la gestion de l’alimentation dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: f72059973057e707f58cb6b7aa495226b6c1962c


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



<!--HONumber=Dec16_HO3-->


