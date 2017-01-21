---
title: Emplacement source du contenu | System Center Configuration Manager
description: "Découvrez comment utiliser les paramètres System Center Configuration Manager qui permettent aux clients d’obtenir du contenu sur un réseau lent."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70b5cbc0-64ba-49bd-8b34-fb4c09b2b95b
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 667010fedb37770d4105fc30f098a231292969fd

---
# <a name="content-source-location-scenarios-in-system-center-configuration-manager"></a>Scénarios d’emplacement source du contenu dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, vous pouvez utiliser une combinaison de différents paramètres pour définir de quelle manière et à quel emplacement les clients peuvent obtenir du contenu sur un réseau lent. Les combinaisons possibles déterminent l’emplacement du contenu utilisé par les clients, et si les clients peuvent utiliser un emplacement de secours quand la source de contenu préférée n’est pas disponible.  



**Les trois paramètres suivants définissent le comportement quand des clients demandent du contenu :**

-  **Autoriser un emplacement source de secours pour le contenu** (activé ou non activé) : vous pouvez activer cette option sous l’onglet Groupes de limites d’un point de distribution.  Elle permet au client d’utiliser un point de distribution configuré en tant qu’emplacement de secours quand le contenu n’est pas disponible sur un point de distribution préféré.  

 - **Comportement du déploiement pour la vitesse de connexion du réseau** : chaque déploiement est configuré avec l’un des comportements suivants à utiliser quand la connexion au point de distribution est lente :  

    -   **Télécharger le contenu à partir du point de distribution et l’exécuter localement**  

    -   **Ne pas télécharger de contenu** : cette option est utilisée uniquement quand un client utilise un emplacement de secours pour obtenir du contenu.  

    La vitesse de connexion pour un point de distribution est configurée sous l’onglet Références d’un groupe de limites, et est spécifique de celui-ci.  

 -  **Distribution de package à la demande** (vers les points de distribution préférés) : cette option est activée quand vous sélectionnez l’option **Distribuer le contenu pour ce package vers les points de distribution préférés** sous l’onglet Paramètres de distribution des propriétés d’un package ou d’une application. Quand cette option est activée, elle indique à Configuration Manager de copier automatiquement le contenu vers un point de distribution préféré n’ayant pas encore le contenu après qu’un client a demandé celui-ci à un point de distribution.  


 **Les conditions préalables suivantes s’appliquent à tous les scénarios :**


-   Le contenu est disponible sur un point de distribution de secours.  

-   Les points de distribution sont en ligne et accessibles.  


## <a name="scenario-1"></a>Scénario 1  
 S’applique lorsque les configurations suivantes existent :  

-   **Le contenu est disponible sur un point de distribution préféré**  

-   **Autoriser les actions de secours** : non activé  

-   **Comportement du déploiement pour un réseau lent** : n’importe quelle configuration  


**Détails :** (La configuration de la distribution de package à la demande ne s’applique pas dans ce scénario.)  

1.  Le client envoie une requête de contenu au point de gestion.  

2.  Le point de gestion envoie une liste d'emplacements de contenu au client avec les points de distribution préférés comprenant du contenu.  

3.  Le client télécharge le contenu à partir d'un point de distribution préféré sur la liste.  

## <a name="scenario-2"></a>Scénario 2  
 Les configurations suivantes existent :  

-   **Le contenu est disponible sur un point de distribution préféré**  

-   **Autoriser les actions de secours** : activé  

-   **Comportement du déploiement pour un réseau lent** : ne pas télécharger de contenu  


**Détails :** (La configuration de la distribution de package à la demande ne s’applique pas dans ce scénario.)  

1.  Le client envoie une requête de contenu au point de gestion. Le client inclut un indicateur avec la requête indiquant que les points de distribution de secours sont autorisés.  

2.  Le point de gestion envoie une liste d'emplacements de contenu au client avec les points de distribution préférés et les points de distribution de secours comprenant du contenu.  

3.  Le client télécharge le contenu à partir d'un point de distribution préféré sur la liste.  

## <a name="scenario-3"></a>Scénario 3  
 Les configurations suivantes existent :  

-   **Le contenu est disponible sur un point de distribution préféré**  

-   **Autoriser les actions de secours** : activé  

-   **Comportement du déploiement pour un réseau lent** : télécharger et installer le contenu  


**Détails :** (La configuration de la distribution de package à la demande ne s’applique pas dans ce scénario.)  

1.  Le client envoie une requête de contenu au point de gestion. Le client inclut un indicateur avec la requête indiquant que les points de distribution de secours sont autorisés.  

2.  Le point de gestion envoie une liste d'emplacements de contenu au client avec les points de distribution préférés et les points de distribution de secours comprenant du contenu.  

3.  Le client télécharge le contenu à partir d'un point de distribution préféré sur la liste.  

## <a name="scenario-4"></a>Scénario 4  
 Les configurations suivantes existent :  

-   **Le contenu n’est pas disponible sur un point de distribution préféré**  

-   **Distribuer le contenu pour ce package vers les points de distribution préférés** : non activé  

-   **Autoriser les actions de secours** : non activé  

-   **Comportement du déploiement pour un réseau lent** : n’importe quelle configuration  


**Détails :**  

1.  Le client envoie une demande de contenu au point de gestion.  

2.  Le point de gestion envoie une liste d'emplacements de contenu au client avec les points de distribution préférés comprenant du contenu. Il n'y a aucun point de distribution préféré dans la liste.  

3.  Le client échoue et affiche le message **Contenu indisponible** , puis passe en mode de nouvelle tentative. Une nouvelle demande de contenu est émise toutes les heures.  

## <a name="scenario-5"></a>Scénario 5  
 Les configurations suivantes existent :  

-   **Le contenu n’est pas disponible sur un point de distribution préféré**  

-   **Distribuer le contenu pour ce package vers les points de distribution préférés** : non activé  

-   **Autoriser les actions de secours** : activé  

-   **Comportement du déploiement pour un réseau lent** : ne pas télécharger de contenu  


**Détails :**  

1.  Le client envoie une requête de contenu au point de gestion. Le client inclut un indicateur avec la requête indiquant que les points de distribution de secours sont autorisés.  

2.  Le point de gestion envoie une liste d'emplacements de contenu au client avec les points de distribution préférés et les points de distribution de secours comprenant du contenu. Si aucun point de distribution préféré n'intègre le contenu, il figure dans au moins un point de distribution de secours.  

3.  Le contenu n’est pas téléchargé, car la propriété de déploiement appliquée quand le client utilise un point de distribution de secours est définie sur **Ne pas télécharger de contenu** (option utilisée quand des clients attendent une action de secours pour obtenir le contenu). Le client échoue et affiche le message **Contenu indisponible** , puis passe en mode de nouvelle tentative. Le client envoie une nouvelle requête de contenu toutes les heures.  

## <a name="scenario-6"></a>Scénario 6  
 Les configurations suivantes existent :  

-   **Le contenu n’est pas disponible sur un point de distribution préféré**  

-   **Distribuer le contenu pour ce package vers les points de distribution préférés** : non activé  

-   **Autoriser les actions de secours** : activé  

-   **Comportement du déploiement pour un réseau lent** : télécharger et installer le contenu  


**Détails :**  

1.  Le client envoie une requête de contenu au point de gestion. Le client inclut un indicateur avec la requête indiquant que les points de distribution de secours sont activés.  

2.  Le point de gestion envoie une liste d'emplacements de contenu au client avec les points de distribution préférés et les points de distribution de secours comprenant du contenu. Si aucun point de distribution préféré n'intègre le contenu, il figure dans au moins un point de distribution de secours.  

3.  Le contenu est téléchargé depuis un point de distribution de secours de la liste, car la propriété de déploiement appliquée lorsque le client utilise un point de distribution de secours est définie sur **Télécharger et installer le contenu**.  

## <a name="scenario-7"></a>Scénario 7  
 Les configurations suivantes existent :  

-   **Le contenu n’est pas disponible sur un point de distribution préféré**  

-   **Distribuer le contenu pour ce package vers les points de distribution préférés** : activé  

-   **Autoriser les actions de secours** : non activé  

-   **Comportement du déploiement pour un réseau lent** : n’importe quelle configuration  


**Détails :**  

1.  Le client envoie une requête de contenu au point de gestion.  

2.  Le point de gestion envoie une liste d'emplacements de contenu au client avec les points de distribution préférés comprenant du contenu. Aucun point de distribution préféré n'a le contenu.  

3.  Le client échoue et affiche le message **Contenu indisponible** , puis passe en mode de nouvelle tentative. Une nouvelle requête de contenu est lancée toutes les heures.  

4.  Le point de gestion crée un déclencheur afin que le Gestionnaire de distribution distribue le contenu à tous les points de distribution préférés pour le client ayant lancé la requête de contenu.  

5.  Le Gestionnaire de distribution distribue le contenu à tous les points de distribution préférés. Dans la plupart des cas, le contenu est correctement distribué aux points de distribution préférés dans l’heure.  

6.  Une nouvelle demande de contenu est adressée par le client au point de gestion.  

7.  Le point de gestion envoie une liste d'emplacements de contenu au client avec les points de distribution préférés comprenant du contenu. Le client télécharge le contenu à partir d'un point de distribution préféré sur la liste.  

## <a name="scenario-8"></a>Scénario 8  
 Les configurations suivantes existent :  

-   **Le contenu n’est pas disponible sur un point de distribution préféré**  

-   **Distribuer le contenu pour ce package vers les points de distribution préférés** : activé  

-   **Autoriser les actions de secours** : activé  

-   **Comportement du déploiement pour un réseau lent** : ne pas télécharger de contenu  


**Détails :**  

1.  Le client envoie une requête de contenu au point de gestion. Le client inclut un indicateur avec la requête indiquant que les points de distribution de secours sont autorisés.  

2.  Le point de gestion envoie une liste d'emplacements de contenu au client avec les points de distribution préférés et les points de distribution de secours comprenant du contenu. Si aucun point de distribution préféré n'intègre le contenu, il figure dans au moins un point de distribution de secours.  

3.  Le contenu n'est pas téléchargé, car la propriété de déploiement appliquée lorsque le client utilise un point de distribution de secours est définie sur **Ne pas télécharger**. Le client échoue et affiche le message **Contenu indisponible** , puis passe en mode de nouvelle tentative. Le client envoie une nouvelle requête de contenu toutes les heures.  

4.  Le point de gestion crée un déclencheur afin que le Gestionnaire de distribution distribue le contenu à tous les points de distribution préférés pour le client ayant lancé la requête de contenu.  

5.  Le Gestionnaire de distribution distribue le contenu à tous les points de distribution préférés. Dans la plupart des cas, le contenu est correctement distribué aux points de distribution préférés dans l’heure.  

6.  Une nouvelle demande de contenu est adressée par le client au point de gestion.  

7.  Le point de gestion envoie une liste d'emplacements de contenu au client avec les points de distribution préférés comprenant du contenu.  

8.  Le client télécharge le contenu à partir d'un point de distribution préféré sur la liste.  

## <a name="scenario-9"></a>Scénario 9  
 Les configurations suivantes existent :  

-   **Le contenu n’est pas disponible sur un point de distribution préféré**  

-   **Distribuer le contenu pour ce package vers les points de distribution préférés** : activé  

-   **Autoriser les actions de secours** : activé  

-   **Comportement du déploiement pour un réseau lent** : télécharger et installer le contenu  


**Détails :**  

1.  Le client envoie une requête de contenu au point de gestion. Le client inclut un indicateur avec la requête indiquant que les points de distribution de secours sont autorisés.  

2.  Le point de gestion envoie une liste d'emplacements de contenu au client avec les points de distribution préférés et les points de distribution de secours comprenant du contenu. Si aucun point de distribution préféré n'intègre le contenu, il figure dans au moins un point de distribution de secours.  

3.  Le contenu est téléchargé depuis un point de distribution de secours de la liste, car la propriété de déploiement appliquée lorsque le client utilise un point de distribution de secours est définie sur **Télécharger et installer le contenu**. Ce paramètre de déploiement permet à un client devant utiliser un emplacement de contenu de secours d’obtenir le contenu à partir de cet emplacement.  

4.  Le point de gestion crée un déclencheur afin que le Gestionnaire de distribution distribue le contenu à tous les points de distribution préférés pour le client ayant lancé la requête de contenu.  

5.  Le Gestionnaire de distribution distribue le contenu à tous les points de distribution préférés, ce qui permet à des clients supplémentaires d’obtenir le contenu sans utiliser de point de distribution de secours.  



<!--HONumber=Nov16_HO1-->


