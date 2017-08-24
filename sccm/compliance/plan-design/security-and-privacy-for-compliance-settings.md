---
title: "Sécurité et confidentialité des paramètres de compatibilité | Microsoft Docs"
description: "En savoir plus sur les bonnes pratiques en matière de sécurité pour les paramètres de compatibilité dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1c409244-6778-4970-a99c-d2508c9cf62b
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e7dc554ffcd23978eed44819b525f6cc239b2135
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-compliance-settings-in-system-center-configuration-manager"></a>Sécurité et confidentialité des paramètres de compatibilité dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


## <a name="security-best-practices-for-compliance-settings"></a>Meilleures pratiques de sécurité pour les paramètres de compatibilité  

|Meilleure pratique de sécurité|Plus d'informations|  
|----------------------------|----------------------|  
|Ne surveillez pas les données sensibles.|Afin d'éviter la divulgation d'informations, ne configurez pas les éléments de configuration pour surveiller les informations potentiellement sensibles.|  
|Ne configurez pas les règles de compatibilité qui utilisent des données pouvant être modifiées par les utilisateurs finaux.|Si vous créez une règle de compatibilité en fonction des données que les utilisateurs peuvent modifier, telles que les paramètres de Registre pour les choix de configuration, les résultats ne sont pas fiables.|  
|Importez des packs de configuration Microsoft System Center et d’autres données de configuration à partir de sources externes uniquement s’ils possèdent une signature numérique valide d’un éditeur approuvé.|Les données de configuration publiées peuvent être signées de façon numérique. Vous pouvez ainsi vérifier la source de publication et vous assurer que les données n’ont pas été falsifiées. Si la vérification de la signature numérique échoue, vous en êtes averti et le système vous invite également à poursuivre l’importation. N'importez pas les données non signées si vous ne pouvez pas vérifier leur source et leur intégrité.|  
|Mettez en œuvre des contrôles d'accès pour protéger les ordinateurs de référence.|Assurez-vous que, quand un utilisateur administratif configure un paramètre de Registre ou de système de fichiers en naviguant vers un ordinateur de référence, cet ordinateur n’avait pas été compromis.|  
|Sécurisez le canal de communication lorsque vous naviguez vers un ordinateur de référence.|Pour empêcher la falsification des données quand elles sont transférées sur le réseau, utilisez la sécurité du protocole Internet (IPsec) ou le bloc de message serveur (SMB) entre l’ordinateur qui exécute la console Configuration Manager et l’ordinateur de référence.|  
|Veillez à restreindre et surveiller les utilisateurs administratifs auxquels le rôle de sécurité basé sur le rôle Gestionnaire de paramètres de compatibilité a été accordé.|Les utilisateurs administratifs auxquels le rôle **Gestionnaire de paramètres de compatibilité** a été accordé peuvent déployer des éléments de configuration vers tous les périphériques et tous les utilisateurs de la hiérarchie. Les éléments de configuration peuvent être très puissants et inclure, par exemple, des scripts et la reconfiguration du Registre.|  

## <a name="privacy-information-for-compliance-settings"></a>Informations de confidentialité pour les paramètres de compatibilité  
 Vous pouvez utiliser les paramètres de compatibilité pour évaluer si vos périphériques client sont compatibles avec les éléments de configuration que vous déployez dans les lignes de base de configuration. Certains paramètres peuvent être corrigés automatiquement s'ils ne sont pas compatibles. Les informations de compatibilité sont transmises au serveur de site par le point de gestion et stockées dans la base de données de site. Les informations sont chiffrées lorsque les périphériques les envoient au point de gestion mais ne sont pas stockées au format chiffré dans la base de données de site. Les informations sont conservées dans la base de données jusqu'à ce que la tâche de maintenance de site **Supprimer les données de gestion de configuration anciennes** les supprime tous les 90 jours. Vous pouvez configurer l'intervalle de suppression. Les informations de compatibilité ne sont pas transmises à Microsoft.  

 Par défaut, les périphériques n’évaluent pas les paramètres de compatibilité. En outre, vous devez configurer les éléments de configuration et les lignes de base de configuration, puis les déployer vers les périphériques.  
