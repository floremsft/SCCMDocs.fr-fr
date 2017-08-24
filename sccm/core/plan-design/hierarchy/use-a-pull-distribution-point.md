---
title: "Point de distribution d’extraction | Microsoft Docs"
description: "Découvrez les configurations et les limites de l’utilisation d’un point de distribution d’extraction avec System Center Configuration Manager."
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: db5039ff6cb93e3099b096196d49a1f06c315a6b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2017
---
# <a name="use-a-pull-distribution-point-with-system-center-configuration-manager"></a>Utiliser un point de distribution d’extraction avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Un point de distribution d’extraction pour System Center Configuration Manager est un point de distribution standard qui obtient le contenu distribué en le téléchargeant à partir d’un emplacement source tel qu’un client, au lieu de recevoir le contenu du serveur de site.  

 Lorsque vous déployez du contenu sur un grand nombre de points de distribution au niveau d’un site, les points de distribution d’extraction contribuent à réduire la charge de traitement du serveur de site et accélèrent le transfert du contenu vers chaque point de distribution. Pour cela, vous devez décharger le processus de transfert du contenu sur chaque point de distribution à partir du processus du gestionnaire de distribution sur le serveur de site.  

-   Vous configurez des points de distribution comme des points de distribution d’extraction.  

-   Pour chaque point de distribution d’extraction, vous devez spécifier un ou plusieurs points de distribution sources à partir desquels il peut obtenir des déploiements. (Un point de distribution d’extraction ne peut obtenir du contenu qu’à partir d’un point de distribution spécifié comme point de distribution source.)  

-   Quand vous distribuez du contenu vers un point de distribution d’extraction, le serveur de site avertit ce point de distribution, qui lance alors le téléchargement (transfert) du contenu à partir d’un point de distribution source. Chaque point de distribution d’extraction gère individuellement le transfert du contenu en téléchargeant le contenu à partir d’un point de distribution qui possède déjà une copie du contenu.  

Les points de distribution d’extraction prennent en charge les mêmes configurations et fonctionnalités que les points de distribution classiques de Configuration Manager. Par exemple, un point de distribution configuré en tant que point de distribution d'extraction prend en charge l'utilisation de configurations de multidiffusion et PXE, la validation de contenu et la distribution de contenu à la demande. Un point de distribution d'extraction prend en charge les communications des clients HTTP ou HTTPS, gère les mêmes options de certificat que les autres points de distribution et peut être géré individuellement ou en tant que membre d'un groupe de points de distribution.  

> [!IMPORTANT]
> Bien qu’un point de distribution d’extraction prenne en charge les communications par HTTP et HTTPS, lorsque vous utilisez Configuration Manager, vous ne pouvez spécifier que des points de distribution sources configurés pour HTTP. Le Kit de développement logiciel (SDK) Configuration Manager permet de spécifier un point de distribution source configuré pour le protocole HTTPS.  

 **Quand vous distribuez du contenu vers un point de distribution d’extraction, la séquence d’événements est la suivante :**  

-   Dès que du contenu est distribué à un point de distribution d'extraction, sur le serveur de site, le composant Package Transfer Manager vérifie la base de données de site pour confirmer si le contenu est disponible sur un point de distribution source. Si Package Transfer Manager ne peut pas confirmer que le contenu se trouve sur un point de distribution source pour le point de distribution d'extraction, la vérification est répétée toutes les 20 minutes jusqu'à ce que le contenu soit disponible.  

-   Une fois la disponibilité du contenu confirmée par Package Transfer Manager, une notification est adressée au point de distribution d'extraction pour télécharger le contenu. Après avoir reçu cette notification, le point de distribution d'extraction tente de télécharger le contenu auprès de ses points de distribution source.  

-   Une fois le téléchargement du contenu terminé, le point de distribution d'extraction soumet cet état à un point de gestion. Toutefois, si l’état n’est pas reçu après 60 minutes, Package Transfer Manager sort de veille et vérifie auprès du point de distribution d’extraction si le contenu a été téléchargé. Si le téléchargement du contenu est en cours, Package Transfer Manager se met en veille pendant 60 minutes avant de vérifier de nouveau auprès du point de distribution d'extraction. Ce cycle se répète jusqu'à ce que le point de distribution d'extraction termine le transfert du contenu.  

**Vous pouvez configurer un point de distribution d’extraction** pendant l’installation du point de distribution ou après son installation en modifiant les propriétés du rôle de système de site du point de distribution.  

**Vous pouvez supprimer la configuration de point de distribution d’extraction** en modifiant les propriétés du point de distribution. Lorsque vous supprimez la configuration de point de distribution d’extraction, le point de distribution reprend un fonctionnement normal et les prochains transferts de contenu vers le point de distribution sont alors gérés par le serveur de site.  

## <a name="limitations-for-pull-distribution-points"></a>Limitations des points de distribution d’extraction  

-   Un point de distribution cloud ne peut pas être configuré en tant que point de distribution d'extraction.  

-   Un point de distribution sur un serveur de site ne peut pas être configuré en tant que point de distribution d'extraction.  

-   **La configuration de contenu préparé se substitue à la configuration du point de distribution d’extraction**. Un point de distribution d'extraction configuré pour du contenu préparé attend le contenu. Il n’extrait pas de contenu d’un point de distribution source et, comme un point de distribution standard avec la configuration de contenu préparé, il ne reçoit pas de contenu du serveur de site.  

-   **Un point de distribution d’extraction n’utilise pas les limites de taux de transfert configurées** lors du transfert de contenu. Si vous configurez un point de distribution précédemment installé en tant que point de distribution d'extraction, les limites de taux configurées sont enregistrées, mais pas utilisées. Si, par la suite, vous supprimez la configuration du point de distribution d’extraction, les limites de taux configurées sont implémentées selon la configuration précédente.  

    > [!NOTE]  
    >  Lorsqu'un point de distribution est configuré en tant que point de distribution d'extraction, l'onglet **Limites du taux de transfert** n'est pas disponible dans les propriétés du point de distribution.  

-   Un point de distribution d’extraction n’utilise pas les **paramètres de nouvelle tentative** pour la distribution de contenu. Les**Paramètres de nouvelle tentative** peuvent être configurés dans le cadre des **Propriétés du composant de distribution de logiciels** pour chaque site. Pour afficher ou configurer ces propriétés, dans l’espace de travail **Administration** de la console Configuration Manager, développez **Configuration du site**, puis sélectionnez **Sites**. Ensuite, dans le volet des résultats, sélectionnez un site puis, dans l’onglet **Accueil**, sélectionnez **Configurer les composants de site**. Enfin, sélectionnez **Distribution de logiciels**.  

-   Pour transférer du contenu depuis un point de distribution source dans une forêt distante, un client Configuration Manager doit être installé sur l’ordinateur qui héberge le point de distribution d’extraction. Un compte d'accès réseau qui peut accéder au point de distribution source doit être configuré.  

-   Sur un ordinateur configuré comme point de distribution d’extraction et exécutant un client Configuration Manager, la version du client doit correspondre à celle du site Configuration Manager qui installe le point de distribution d’extraction. Le point de distribution d’extraction doit impérativement utiliser le composant CCMFramework qui est commun au point de distribution d’extraction et au client Configuration Manager.  

## <a name="about-source-distribution-points"></a>À propos des points de distribution sources  
 Quand vous configurez le point de distribution d’extraction, vous devez spécifier un ou plusieurs points de distribution sources :  

-   Seuls les points de distribution considérés comme points de distribution source possibles sont affichés.  

-   Un point de distribution d'extraction peut être spécifié en tant que point de distribution source d'un autre point de distribution d'extraction.  

-   Si vous utilisez Configuration Manager, seuls les points de distribution prenant en charge le protocole HTTP peuvent être spécifiés comme des points de distribution sources.  

-   Le Kit de développement logiciel (SDK) Configuration Manager permet de spécifier un point de distribution source configuré pour le protocole HTTPS. Pour utiliser un point de distribution source configuré pour le protocole HTTPS, le point de distribution d’extraction doit se trouver sur l’ordinateur qui exécute le client Configuration Manager.  

Une priorité peut être attribuée à chaque point de distribution figurant dans la liste de points de distribution sources utilisée par le point de distribution d’extraction :  

-   Vous pouvez affecter une priorité distincte à chaque point de distribution source ou affecter la même priorité à plusieurs points de distribution source.  

-   La priorité détermine l'ordre dans lequel le point de distribution d'extraction demande du contenu auprès de ses points de distribution source.  

-   Les points de distribution d'extraction contactent initialement le point de distribution source présentant la valeur de priorité la plus basse.  Si plusieurs points de distribution source présentent la même priorité, le point de distribution d'extraction sélectionne de façon non déterminante l'un des points de distribution source partageant cette priorité.  

-   Si le contenu n’est pas disponible sur une source sélectionnée, le point de distribution d’extraction tente de télécharger le contenu à partir d’un autre point de distribution présentant le même niveau de priorité.  

-   Si le contenu n'est pas disponible sur les points de distribution présentant la priorité donnée, le point de distribution d'extraction essaie de télécharger le contenu auprès du point de distribution présentant le niveau de priorité suivant et continue ainsi jusqu'à trouver le contenu, ou bien le point de distribution d'extraction se met en veille pendant 30 minutes et recommence le processus.  

Quand un point de distribution d’extraction télécharge du contenu à partir d’un point de distribution source, il est considéré comme un client dans la colonne **Client consulté (unique)** du rapport **Résumé de l’utilisation des points de distribution** .  

 Par défaut, un point de distribution d’extraction utilise son **compte d’ordinateur** pour transférer le contenu d’un point de distribution source. Toutefois, lorsque le point de distribution d’extraction transfère du contenu à partir d’un point de distribution source qui se trouve dans une forêt distante, il utilise toujours le compte d’accès réseau. Ce processus nécessite que le client Configuration Manager soit installé sur l’ordinateur et qu’un compte d’accès réseau soit configuré pour utiliser le point de distribution source et ait accès à celui-ci.  

## <a name="about-content-transfers"></a>À propos des transferts de contenu  
 Pour gérer le transfert de contenu, les points de distribution d’extraction utilisent le composant **CCMFramework** du logiciel client Configuration Manager.  

-   Cette infrastructure est installée par **Pulldp.msi** lors de la configuration du point de distribution comme point de distribution d’extraction. Elle n’a pas besoin du client Configuration Manager.  

-   Une fois le point de distribution d'extraction installé, le service CCMExec doit être opérationnel sur l'ordinateur du point de distribution pour permettre au point de distribution d'extraction de fonctionner.  

-   Quand le point de distribution d’extraction transfère du contenu, il utilise le **service de transfert intelligent en arrière-plan** (BITS) et consigne ses opérations dans les fichiers journaux **datatransferservice.log** et **pulldp.log** sur l’ordinateur du point de distribution.  

## <a name="see-also"></a>Voir aussi  
 [Concepts fondamentaux de la gestion de contenu dans System Center Configuration Manager](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   
