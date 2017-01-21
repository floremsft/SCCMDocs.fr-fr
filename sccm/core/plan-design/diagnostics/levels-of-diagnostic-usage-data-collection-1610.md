---
title: "Données de diagnostic pour 1610 | System Center Configuration Manager"
description: "En savoir plus sur les niveaux des données de diagnostic et d’utilisation collectées par System Center Configuration Manager version 1610."
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eb20eb90-bcc0-41de-bfea-638ea470c0dd
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: 6b4af705fa148261634d38dbb2df9988c5672180
ms.openlocfilehash: df8a4c84da8e73aae2455e5f5af26d097449cddd

---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1610-of-system-center-configuration-manager"></a>Niveaux de collecte des données de diagnostic et d’utilisation pour la version 1610 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager version 1610 collecte trois niveaux de données d’utilisation et de diagnostic : **De base**, **Étendu** et **Complet**. Par défaut, cette fonctionnalité est définie sur le niveau Étendu. Les sections suivantes fournissent des détails supplémentaires sur les données collectées à chaque niveau.

Les modifications par rapport aux versions précédentes sont indiquées par ***[Nouveau]***, ***[Mis à jour]***, ***[Supprimé]*** ou ***[Déplacé]***.


> [!IMPORTANT]
>  Configuration Manager ne collecte pas les codes de sites ou noms de sites, les adresses IP, les noms d’utilisateur ou d’ordinateur, les adresses physiques ni les adresses e-mail aux niveaux De base et Étendu. Les informations au niveau Complet ne sont pas collectées dans un but précis (elles peuvent être incluses dans des informations de diagnostic avancées telles que des fichiers journaux ou des instantanés de la mémoire) et ne sont pas utilisées par Microsoft pour vous identifier, vous contacter ou à des fins publicitaires.

##  <a name="a-namebkmkchangea-how-to-change-the-level"></a><a name="bkmk_change"></a> Modification du niveau
 Les administrateurs disposant d’une étendue administrative basée sur des rôles incluant les autorisations **Modification** sur la classe d’objets **Site** peuvent modifier le niveau des données collectées dans les paramètres des données de diagnostic et d’utilisation de la console Configuration Manager.

Depuis la version 1610, vous pouvez modifier le niveau de collecte des données à partir de la console en accédant à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Sites**. Ouvrez **Paramètres de hiérarchie**, puis sélectionnez le niveau de données que vous souhaitez utiliser.  

##  <a name="a-namebkmklevel1a-level-1---basic"></a><a name="bkmk_level1"></a> Niveau 1 - De base
 Le niveau De base comprend les données relatives à votre hiérarchie. Il est nécessaire pour aider à améliorer votre expérience d’installation ou de mise à niveau, ainsi que pour aider à déterminer quelles mises à jour Configuration Manager s’appliquent à votre hiérarchie.

 Pour System Center Configuration Manager version 1610, ce niveau inclut les éléments suivants :


 -   Informations d’installation :
      - Build, type d’installation, modules linguistiques et fonctionnalités que vous avez activés  

      -   État et erreurs du déploiement du package de mise à jour, progression du téléchargement et erreurs au niveau des conditions préalables    

      -  Version du script après mise à niveau

      -  Utilisation de l’anneau rapide de mise à jour

    -  ***[Nouveau]*** Utilisation en préversion, type de support de configuration, type de branche

    - ***[Nouveau]*** Date d’expiration de Software Assurance


-   Métriques de performances de base de données (informations sur le traitement de la réplication, procédures stockées SQL Server les plus utilisées par processeur et utilisation des disques)

-   Configuration de base de données simple (processeurs, configuration du cluster, configuration des vues distribuées)

-   Schéma de base de données Configuration Manager (hachage de toutes les définitions d’objet)

-   Nombre de versions du client Configuration Manager et de versions du système d’exploitation

-   Nombre et système d’exploitation des appareils gérés et stratégies définies par le connecteur Exchange

-   Nombre de paramètres régionaux et de langues du client

-   Nombre d’appareils Windows 10 par branche et build

-   Données de la hiérarchie des sites Configuration Manager de base (liste des sites, type, version, état, nombre de clients et fuseau horaire)

-   Informations de serveur de système de site de base (rôles de système de site utilisés, état SSL et Internet, système d’exploitation, processeurs, ordinateur physique ou machine virtuelle)

-   Statistiques de découverte d’utilisateurs de base (nombre de découvertes d’utilisateurs, tailles minimale/maximale/moyenne de groupe)

-   Informations de protection de point de terminaison de base (versions du client de logiciel anti-programme malveillant)

-   Nombres de types d’application et de déploiement de base (nombre total d’applications, nombre total d’applications avec plusieurs types de déploiement, nombre total d’applications avec des dépendances, nombre total d’applications remplacées, nombre de technologies de déploiement en cours d’utilisation)

-   Nombres d’OSD de base (images)

-   Types de point de distribution et de point de gestion et informations de configuration de base (protégés, préparés, PXE, de multidiffusion, d’état SSL, points de distribution pairs/d’extraction, compatibles MDM, compatibles SSL, etc.)

-   Statistiques de télémétrie (à l’exécution, runtime, erreurs)

-  Niveau de télémétrie configuré, mode (en ligne ou hors connexion) et configuration de la mise à jour rapide

-  Utilisation de la découverte du réseau (activée ou désactivée)
-  Console d'administration :

     -  Statistiques sur les connexions de la console (version, langue, référence (SKU) et architecture du SE ; mémoire système, nombre de processeurs logiques, ID du site de connexion, versions .NET installées et modules linguistiques de la console)    


- Version SQL, niveau du Service Pack, édition, ID de classement, jeu de caractères


##  <a name="a-namebkmklevel2a-level-2---enhanced"></a><a name="bkmk_level2"></a> Niveau 2 – Étendu
Le niveau Étendu est configuré par défaut après l’installation. Ce niveau comprend les données collectées au niveau De base, ainsi que les données propres aux fonctionnalités (fréquence et durée d’utilisation), les paramètres du client Configuration Manager (nom du composant, état et paramètres tels que les intervalles d’interrogation) et les informations de base sur les mises à jour logicielles.

Ce niveau est recommandé, car il fournit à Microsoft les données minimales requises pour apporter des améliorations utiles dans les futures versions des produits et services. Ce niveau ne collecte pas les noms des objets (sites, utilisateurs, ordinateur ou objets), les informations des objets relatifs à la sécurité ni les vulnérabilités telles que le nombre de systèmes nécessitant des mises à jour logicielles.

Pour System Center Configuration Manager version 1610, ce niveau inclut les éléments suivants :

-   **Gestion des applications :**  

    -    Informations de base d’utilisation/de ciblage pour les types de déploiement utilisés au sein de l’organisation (ciblé utilisateur ou appareil, nécessaire ou disponible, applications universelles)  

    -   Informations de déploiement d’application (installation/désinstallation, approbation requise, interaction utilisateur activée/désactivée, dépendance, remplacement)  

    -   Statistiques de demande d’application disponibles  

    -   Nombre de packages par type  

    -   Nombre d’applicabilités de l’application par système d’exploitation  

    -   Nombre de déploiements de package/programme  

    -   Nombre d’environnements App-V et propriétés de déploiement  

    -   Nombre de licences d’application Windows 10 concédées  

    -   Nombre minimal/maximal/moyen de déploiements d’applications par utilisateur/appareil par période

    -   Type et durée de fenêtre de maintenance  

    -  Statistiques de taille et de complexité des stratégies d’applications

    - ***[Mis à jour]*** Nombre d’applications Windows Store pour Entreprises et statistiques de synchronisation (notamment un résumé des types d’applications, l’état des applications sous licence ainsi que le nombre d’applications sous licence en ligne et hors connexion)  

    - Statistiques des groupes de limites (combien de rapides, lents, nombre par groupe)

    - Options de configuration MSI et nombres

    - Conditions requises pour les applications (nombre de conditions intégrées référencées en fonction de la technologie de déploiement)

    - Remplacement des applications, profondeur de chaîne maximale

    - Utilisation d’UDA, mode de création

    - ***[Nouveau]*** Statistiques d’approbation de l’application et fréquence d’utilisation



-   **Client :**  

    -   Liste/nombre d’agents clients activés  

    -   Nombre d’installations de client à partir de chaque type d’emplacement source  

    -   Nombre d’échecs d’installation de client  

    -  ***[Mis à jour]*** Mise à niveau automatique du client : configuration du déploiement, notamment le test du client et l’utilisation de l’exclusion (client d’interopérabilité étendue)

    -  Statistiques d’intégrité du client et récapitulatif des problèmes principaux

    - Âge du BIOS en années

    - Âge du système d’exploitation en mois

    - Nombre d’actions du Centre logiciel

    - Version du client AMT (Active Management Technology)

    - Erreurs de téléchargement de déploiement des clients

    - État des actions de notification du client (nombre d’exécutions de chaque action, nombre maximal de clients ciblés, taux de réussite moyen)

    - Méthodes de déploiement utilisées pour le client, nombre de clients par méthode de déploiement

    - Configuration de la taille du cache du client

    - ***[Nouveau]*** Nombre de classes d’inventaire matériel, règles d’inventaire logiciel et règles de regroupement de fichiers




- **Services cloud :**

  - Nombre de regroupements synchronisés avec OMS

  -  État d’activation du connecteur cloud OMS

  - ***[Nouveau]*** Configuration et statistiques d’utilisation de la passerelle de gestion cloud

  - ***[Nouveau]*** Nombre de connecteurs Upgrade Analytics




- **Regroupements :**

    -  Statistiques d’évaluation des regroupements (temps de requête, nombre de regroupements attribués et non attribués, nombres par type, substitution d’ID et utilisation des règles)

    - Regroupements sans déploiement

    - Utilisation des ID de regroupement (ne pas manquer d’ID)



-   **Paramètres de compatibilité :**  

    -   Nombre d’éléments de configuration par type  

    -   Informations de la ligne de base de configuration de base (nombre, nombre de déploiements et nombre de références)  

    -   Nombre de déploiements faisant référence à des paramètres intégrés (avec capture du paramètre de correction)  

    -   Nombre de règles et de déploiements créés pour les paramètres personnalisés (avec capture du paramètre de correction)  
    -   Nombre de modèles SCEP (Simple Certificate Enrollment Protocol), VPN, Wi-Fi, de certificat (.pfx) et de stratégie de conformité déployés

    -  Nombre de déploiements de certificat SCEP, VPN, Wi-Fi, certificat (.pfx) et stratégie de conformité par plateforme

    - Stratégie Passport for Work (créée, déployée)



-   **Contenu :**  

    -   Nombre de limites par type  

    -   Informations sur les groupes de limites (nombre de limites et de systèmes de site attribués à chaque groupe de limites)  

    - ***[Nouveau]*** Relations de groupes de limites et configuration de secours

    -   Informations sur les groupes de points de distribution (nombre de packages et de points de distribution attribués à chaque groupe de points de distribution)  

    -   Informations sur la configuration des point de distribution (utilisation de la fonction Branch Cache, surveillance des points de distribution)  

    -   Informations de configuration du gestionnaire de distribution (threads, délai de nouvelle tentative, nombre de nouvelles tentatives, paramètres de point de distribution d’extraction)  

    - ***[Nouveau]*** Nombre de clients du cache d’homologue et statistiques d’utilisation

    - ***[Nouveau]*** Statistiques de téléchargement du contenu client


-   **Endpoint Protection :**  

    -   Utilisation des stratégies du Pare-feu Windows et de logiciel anti-programme malveillant Endpoint Protection (nombre de stratégies uniques attribuées au groupe, ne comprend pas les informations sur les paramètres inclus dans la stratégie)  

    -   Erreurs de déploiement Endpoint protection (nombre de codes d’erreur de déploiement de stratégie Endpoint Protection)  

    -   Nombre de regroupements sélectionnés pour être affichés dans le tableau de bord Endpoint Protection  

    -   Nombre d’alertes configurées pour la fonctionnalité Endpoint Protection  

    - Stratégies ATP (nombre de stratégies, statut de déploiement)


- **Migration :**

  -   Nombre d’objets migrés (utilisation de l’Assistant Migration)



-   **Gestion des appareils mobiles (MDM) :**  

    -   ***[Mis à jour]*** Nombre de commandes émises (verrouiller, réinitialiser, mettre hors service et Synchroniser maintenant) d’actions d’appareil mobile  

    -   Nombre d’appareils mobiles gérés par Configuration Manager et Microsoft Intune et méthode d’inscription (en bloc, basée sur l’utilisateur)  

    -   Vérification dans la durée des appareils mobiles quant aux statistiques et au calendrier d’interrogation des appareils mobiles  

    -   Nombre de stratégies d’appareil mobile  

    -   Nombre d’utilisateurs avec plusieurs appareils mobiles inscrits  

-   **Dépannage de Microsoft Intune :**

    -   Nombre et taille des messages d’état, de statut, d’inventaire, RDR, DDR, UDX, d’état de locataire, POL, LOG, de certificat, CRP, de resynchronisation, CFD, RDO, BEX, ISM et de compatibilité téléchargés à partir de Microsoft Intune

    -   Nombre et taille des messages d’actions d’appareil (réinitialiser, mettre hors service, verrouiller), de télémétrie et de données répliqués vers Microsoft Intune

    -   Statistiques de synchronisation utilisateur complète et différentielle pour Microsoft Intune


-   **Gestion des appareils mobiles (MDM) locale :**  

    -   Statistiques de réussite/échec de déploiement pour les déploiements d’applications de gestion MDM locale  

    -   Nombre de profils et de packages d’inscription en bloc Windows 10  



-   **Déploiement du système d'exploitation :**  

    -   Nombre d’images de démarrage, de pilotes, de packages de pilotes, de points de distribution en multidiffusion, de points de distribution compatibles PXE et de séquences de tâches  

    -   Nombre d’utilisations des étapes de séquence de tâches

    - ***[Nouveau]*** Nombre de stratégies de mise à niveau d’édition



-   **Mises à jour du site :**

    - Versions des correctifs logiciels de Configuration Manager installés




-   **Mises à jour logicielles :**  

    -   Nombre total/moyen de regroupements comportant des déploiements de mises à jour logicielles et le nombre maximal/moyen de mises à jour déployées  

    -   Nombre de règles de déploiement automatique liées à la synchronisation  

    -   Nombre de règles de déploiement automatique qui créent de nouvelles mises à jour ou ajoutent des mises à jour à un groupe existant  

    -   Différentiels de disponibilité et d’échéance utilisés dans les règles de déploiement automatique  

    -   Nombre moyen et maximal d’attributions par mise à jour  

    -   Nombre de mises à jour créées et déployées à l’aide de System Center Update Publisher  

    -   Nombre de groupes et d’attributions de mises à jour  

    -   Nombre de packages de mises à jour et nombre maximal/minimal/moyen de points de distribution ciblés par les packages  

    -   Nombre de groupes de mises à jour et nombre minimal/maximal/moyen de mises à jour par groupe  

    -   Nombre de mises à jour et pourcentage de mises à jour déployées, expirées, remplacées, téléchargées et contenant des CLUF  

    -   Codes d’erreur d’analyse des mises à jour et nombre d’ordinateurs  

    -   Calendriers d’analyse et d’évaluation des mises à jour client  

    -   Planification de la synchronisation du point de mise à jour logicielle  

    -   Nombre de règles de déploiement automatique avec plusieurs déploiements  

    -   Configurations utilisées pour les plans de maintenance actifs de Windows 10  

    -   Versions de contenu du tableau de bord Windows 10  

    -   Nombre de clients Windows 10 qui utilisent Windows Update for Business  

    -   Statistiques d’application de correctifs logiciels au cluster  

    -   Nombre de mises à jour Office 365 déployées  

    -   Classifications synchronisées par le point de mise à jour logicielle

    -   Statistiques d’équilibrage de charge du point de mise à jour logicielle

    -  ***[Nouveau]*** Configuration des mises à jour rapides de Windows 10




-   **Données de performances/SQL :**  

    -   Nombre des plus grandes tables de base de données  

    -   ***[Mis à jour]*** Informations sur les réplicas SQL AlwaysOn, utilisation et état d’intégrité

    -  Période de rétention du suivi des modifications SQL

    - Types de découverte, activés et planifiés (complète, incrémentielle)

    - Statistiques opérationnelles de découverte (nombre d’objets trouvés)

    - Problèmes de performances du suivi des modifications SQL, période de rétention et état de nettoyage automatique



- **Divers**

    - Nombre de sites avec WOL

    - ***[Nouveau]*** Statistiques de performances et d’utilisation des rapports  



##  <a name="a-namebkmklevel3a-level-3---full"></a><a name="bkmk_level3"></a> Niveau 3 – Complet
Le niveau Complet inclut toutes les données des niveaux De base et Étendu. Il inclut également des informations supplémentaires sur Endpoint Protection, les pourcentages de compatibilité des mises à jour et les informations de mise à jour logicielle.  Ce niveau peut également inclure des informations de diagnostic avancées telles que des fichiers système et des instantanés de la mémoire, qui peuvent inclure des informations personnelles qui existaient dans la mémoire ou les fichiers journaux au moment de la capture.

Pour System Center Configuration Manager version 1610, ce niveau inclut les éléments suivants :

-   Statistiques d’évaluation et d’actualisation des regroupements

-   Récapitulatif de l’intégrité Endpoint Protection (y compris le nombre de clients protégés, présentant un risque, inconnus et non pris en charge)

-   Configuration de la stratégie Endpoint Protection

-   Informations de déploiement de mise à jour logicielle (pourcentage de déploiements ciblés avec le client ou l’heure UTC, suppression du démarrage nécessaire, facultative ou en mode silencieux)

-   Compatibilité globale des déploiements de mise à jour logicielle

-   Informations sur le calendrier d’évaluation de règle de déploiement automatique

-   Nombres et codes d’erreur de déploiement de mise à jour logicielle

-   Nombre minimal/maximal/moyen de clients inactifs dans les regroupements de déploiements de mise à jour logicielle

-   Nombre de groupes avec des mises à jour logicielles ayant expiré

-   Nombre minimal/maximal/moyen de mises à jour logicielles par package

-   Pourcentages de réussite d’analyse des mises à jour logicielles

-   Nombre minimal/maximal/moyen d’heures depuis la dernière analyse des mises à jour logicielles

-    Produits des mises à jour logicielles synchronisés par le point de mise à jour logicielle
-    Paramètres de compatibilité : détails de configuration des modèles SCEP, VPN, Wi-Fi et stratégie de conformité

-    Type de stratégies d’accès conditionnel EAS (bloquer ou mettre en quarantaine) pour les appareils gérés par Intune

-   50 premières unités centrales dans l’environnement

-   Pack de configuration DCM pour l’utilisation de SCCM

-   Code de produit MSI (quelles sont les applications courantes que les clients déploient)

-   Récapitulatif d’intégrité ATP

-   Détails des erreurs d’installation du déploiement des clients

- ***[Nouveau]*** Détails de l’application du Windows Store pour Entreprises (liste de non-agrégation des applications synchronisées, dont l’ID de l’application, l’état (en ligne ou hors connexion) et le nombre total de licences achetées)



<!--HONumber=Dec16_HO3-->


