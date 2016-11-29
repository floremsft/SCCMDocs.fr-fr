---
title: "Afficher les données de diagnostic | System Center Configuration Manager"
description: "Affichez les données d’utilisation et de diagnostic pour vérifier que votre hiérarchie System Center Configuration Manager ne contient aucune information sensible."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5d1382d4912d03fb38bfc2f07edfb361c0ac6139


---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Comment afficher les données d’utilisation et de diagnostic pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez afficher les données d’utilisation et de diagnostic de votre hiérarchie System Center Configuration Manager pour vérifier qu’elle ne contient aucune information sensible ni identifiable. Les données de télémétrie sont résumées et stockées dans la table **TEL_TelemetryResults** de la base de données du site et mises en forme de manière à être utilisables et efficaces en programmation. Les options suivantes vous offrent une vue des données exactes envoyées à Microsoft, mais celles-ci ne sont pas destinées à être utilisées à d’autres fins, telle que l’analyse des données.  

La commande SQL suivante peut être utilisée pour afficher le contenu de cette table et elle affiche les données exactes qui sont envoyées (vous pouvez également exporter ces données dans un fichier texte) :  

-   **SELECT \* FROM TEL_TelemetryResults**  

> [!NOTE]  
>  Avant d’installer la version 1602, la table qui stocke les données de télémétrie est **TelemetryResults**.  

Quand le point de connexion de service est en mode hors connexion, vous pouvez utiliser l’outil de connexion de service pour exporter les données d’utilisation et de diagnostic en cours dans un fichier de valeurs séparées par des virgules (CSV). Exécutez l’outil de connexion de service sur le point de connexion de service avec le paramètre **-Export**.  

##  <a name="a-namebkmkhashesa-one-way-hashes"></a><a name="bkmk_hashes"></a> Hachages unidirectionnels  
Certaines données se composent de chaînes de caractères alphanumériques aléatoires. Configuration Manager utilise des hachages unidirectionnels basés sur l’algorithme SHA-256 pour s’assurer que nous ne collectons pas de données potentiellement sensibles, tout en les conservant dans un état où elles peuvent encore servir à des fins de corrélation et de comparaison. Par exemple, au lieu de collecter les noms des tables dans la base de données de site, un hachage unidirectionnel est capturé pour chaque nom de table. Cela garantit l’invisibilité de tous les noms de tables personnalisés que vous ou des modules complémentaires d’un produit tiers avez créés. Nous pouvons ensuite effectuer le même hachage unidirectionnel des noms des tables SQL fournis par défaut dans le produit et les comparer afin de déterminer l’écart de votre schéma de base de données par rapport aux paramètres par défaut du produit. Cet écart est ensuite utilisé pour améliorer les mises à jour qui nécessitent des modifications du schéma SQL.  

Lorsque vous affichez les données brutes, une valeur hachée apparaît dans chaque ligne de données. Il s’agit de l’ID de hiérarchie. Cette valeur de hachage est utilisée pour s’assurer que les données sont corrélées avec la même hiérarchie, sans identification du client ou de la source.  

#### <a name="to-see-how-the-one-way-hash-works"></a>Pour voir comment fonctionne le hachage unidirectionnel  

1.  Obtenez l’ID de votre hiérarchie en exécutant l’instruction SQL suivante dans SQL Management Studio sur la base de données Configuration Manager : **select [dbo].[fnGetHierarchyID](\)**  

2.  Ensuite, utilisez le script Windows PowerShell suivant pour exécuter le hachage unidirectionnel du GUID obtenu de la base de données. Vous pouvez alors le comparer à l’ID de hiérarchie dans les données brutes pour voir comment nous masquons ces données.  

    ```  
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
         #many of the values we hash are Guids  
         $bytesToHash = $guid.ToByteArray()  
    } else {  
         #otherwise hash as string (unicode)  
         $ue = New-Object System.Text.UnicodeEncoding  
         $bytesToHash = $ue.GetBytes($value)   
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)   
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()    
    # Hash the input   
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)              
    # Base64 encode the result for transport   
    $result = [Convert]::ToBase64String($hashedBytes)    
    return $result   
    ```  



<!--HONumber=Nov16_HO1-->


