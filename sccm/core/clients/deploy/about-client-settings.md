---
title: "Paramètres du client"
titleSuffix: Configuration Manager
description: "Choisissez les paramètres client à l’aide de la console d’administration de System Center Configuration Manager."
ms.custom: na
ms.date: 01/05/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: "15"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 230d608c9ebc8126d7d8e18f7211875a2155bb7b
ms.sourcegitcommit: ac9268e31440ffe91b133c2ba8405d885248d404
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/08/2018
---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>À propos des paramètres client dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez gérer tous les paramètres client dans la console Configuration Manager à partir du nœud **Paramètres client** de l’espace de travail **Administration**. Configuration Manager est fourni avec un ensemble de paramètres par défaut. Quand vous modifiez les paramètres client par défaut, ces paramètres sont appliqués à tous les clients de la hiérarchie. Vous pouvez également configurer des paramètres client personnalisés, qui remplacent les paramètres client par défaut quand vous les affectez à des regroupements. Pour plus d’informations, consultez [Guide pratique pour configurer les paramètres client](../../../core/clients/deploy/configure-client-settings.md).  
 

## <a name="background-intelligent-transfer-service"></a>Service de transfert intelligent en arrière-plan (BITS)  

-   **Limiter la bande passante réseau maximale pour les transferts BITS en arrière-plan**   </br>
   Quand cette option est **Oui**, les clients utilisent la limitation de bande passante BITS. Pour configurer les autres paramètres de ce groupe, vous devez activer ce paramètre. 

-   **Heure de début de la fenêtre de limitation**   </br>
   Spécifiez l’heure locale de début de la fenêtre de limitation BITS.  

-   **Heure de fin de la fenêtre de limitation**   </br>
   Spécifiez l’heure locale de fin de la fenêtre de limitation BITS. Si elle est égale à l’**Heure de début de la fenêtre de limitation**, la limitation BITS est toujours activée.  

-   **Taux de transfert maximal dans la fenêtre de limitation (Kbit/s)** </br>
    Spécifie le taux de transfert maximal que les clients peuvent utiliser pendant la fenêtre.  

-   **Autoriser les téléchargements BITS en dehors de la fenêtre de limitation**   </br>
   Permet aux clients d’utiliser des paramètres BITS distincts en dehors de la fenêtre spécifiée.  

-   **Taux de transfert maximal en dehors de la fenêtre de limitation (Kbit/s)**   </br>
   Spécifiez le taux de transfert maximal que les clients utilisent en dehors de la fenêtre de limitation BITS.  



## <a name="client-cache-settings"></a>Paramètres du cache du client

- **Configurer BranchCache** </br>
  Utilisez ce paramètre pour configurer l’ordinateur client pour [Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache). Pour autoriser la mise en cache BranchCache sur le client, définissez **Activer BranchCache** sur **Oui**.

    - **Activer BranchCache** </br>
    Active BranchCache sur les ordinateurs clients.

    - **Taille maximale du cache BranchCache (pourcentage du disque)** </br>
    Pourcentage du disque que vous autorisez BranchCache à utiliser. 

- **Configurer la taille du cache du client** </br>
  Le cache du client Configuration Manager sur les ordinateurs Windows stocke les fichiers temporaires utilisés pour installer des applications et des programmes. Si cette option a la valeur **Non**, la taille par défaut est de 5 120 Mo.</br>
    Choisissez **Oui**, puis spécifiez :
    - **Taille maximale du cache (Mo)**
    - **Taille maximale du cache (pourcentage du disque)** </br>
    La taille du cache du client augmente jusqu’à la taille maximale en mégaoctets (Mo) ou au pourcentage du disque, *selon la valeur la moins élevée des deux*. 

- **Permettre au client Configuration Manager exécutant le système d’exploitation complet de partager du contenu** </br>
    Active le [cache d’homologue](/sccm/core/plan-design/hierarchy/client-peer-cache) pour les clients Configuration Manager. Choisissez **Oui**, puis spécifiez les informations relatives au port par lequel le client communique avec l’ordinateur homologue. 
    - **Port pour la diffusion réseau initiale** (par défaut : 8004)
    - **Port pour le téléchargement de contenu à partir d’un pair** (par défaut : 8003) </br>
    Configuration Manager configure automatiquement les règles de Pare-feu Windows pour autoriser ce trafic. Si vous utilisez un autre pare-feu, vous devez configurer manuellement des règles pour autoriser ce trafic.




## <a name="client-policy"></a>Stratégie du client  

-   **Intervalle d'interrogation de stratégie client (minutes)**  </br>
     Spécifie la fréquence à laquelle les clients Configuration Manager suivants téléchargent la stratégie client :  
      -   Ordinateurs Windows (par exemple, ordinateurs de bureau, serveurs, ordinateurs portables)  
      -   Appareils mobiles inscrits par Configuration Manager  
      -   Ordinateurs Mac  
      -   Ordinateurs qui exécutent Linux ou UNIX  

-   **Activer la stratégie utilisateur sur les clients**   </br>
   Quand vous affectez la valeur **Oui** à cette option et que vous utilisez la [découverte d’utilisateurs](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), les clients reçoivent les applications et programmes destinés à l’utilisateur connecté.  

    Le catalogue d’applications reçoit la liste des logiciels disponibles pour les utilisateurs à partir du serveur de site. Ainsi, ce paramètre ne doit pas obligatoirement être **Oui** pour que les utilisateurs voient et demandent des applications au catalogue d’applications. Si ce paramètre a la valeur **Non**, les comportements suivants ne fonctionnent pas quand les utilisateurs utilisent le catalogue d’applications :  

      -   Les utilisateurs ne peuvent pas installer les applications qu’ils voient dans le catalogue des applications.  

      -   Les utilisateurs ne voient pas les notifications concernant leurs demandes d’approbation d’application. Au lieu de cela, ils doivent actualiser le catalogue d'applications et vérifier l'état d'approbation.  

      -   Les utilisateurs ne reçoivent pas de révisions et de mises à jour pour les applications qui sont publiées dans le catalogue d’applications. Les utilisateurs voient les modifications apportées aux informations de l’application dans le catalogue d’applications.  

      -   Si vous supprimez le déploiement d’une application après que le client a installé l’application en question à partir du catalogue d’applications, les clients continuent à vérifier que l’application est installée pendant une durée qui peut atteindre deux jours.  

    En outre, quand ce paramètre est **Non**, les utilisateurs ne reçoivent pas les applications requises que vous déployez sur les utilisateurs. Ils ne reçoivent pas non plus d’autres tâches de gestion dans les stratégies utilisateur.  

    Ce paramètre s’applique aux utilisateurs si leur ordinateur se trouve sur l’intranet et Internet. Il doit avoir la valeur **Oui** si vous souhaitez également activer les stratégies utilisateur sur Internet.  

-   **Autoriser les demandes de stratégie utilisateur depuis des clients Internet**   </br>
   Affectez la valeur **Oui** à ce paramètre pour que les utilisateurs reçoivent la stratégie utilisateur sur les ordinateurs basés sur Internet. Les conditions suivantes doivent également s’appliquer :  

      -   Le client et le site sont configurés pour la gestion des clients basés sur Internet

      -   Le paramètre **Activer la stratégie utilisateur sur les clients** est **Oui**  

      -   Le point de gestion basé sur Internet authentifie correctement l’utilisateur à l’aide de l’authentification Windows (Kerberos ou NTLM)  

       Si vous affectez la valeur **Non** à cette option, ou si l’une des conditions ci-dessus n’est pas remplie, un ordinateur sur Internet reçoit uniquement les stratégies ordinateur. Dans ce cas, les utilisateurs peuvent toujours voir, demander et installer des applications à partir d'un catalogue d'applications basé sur Internet. Si ce paramètre est **Non**, mais que **Activer la stratégie utilisateur sur les clients** est **Oui**, les utilisateurs ne reçoivent les stratégies utilisateur qu’une fois l’ordinateur connecté à intranet.  

       Pour plus d’informations sur la gestion des clients sur Internet, consultez [Éléments à prendre en considération pour les communications de clients à partir d’Internet ou d’une forêt non approuvée](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

      > [!NOTE]  
      >  Les demandes d'approbation d'application des utilisateurs ne requièrent pas de stratégies utilisateur ou l'authentification utilisateur.  


## <a name="cloud-services"></a>Services cloud

-   **Autoriser l’accès au point de distribution cloud** </br>
    Configurez ce paramètre sur **Oui** pour que les clients obtienne le contenu à partir d’un point de distribution cloud. Ce paramètre ne nécessite pas que l’appareil soit basé sur Internet.

-    **Inscrire automatiquement les nouveaux appareils joints au domaine Windows 10 auprès d’Azure Active Directory** </br> Quand vous configurez Azure Active Directory pour prendre en charge la jointure hybride, Configuration Manager configure les appareils Windows 10 pour cette fonctionnalité. Pour plus d’informations, consultez [Guide pratique pour configurer des appareils hybrides joints à Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

-   **Autoriser les clients à utiliser une passerelle de gestion cloud** </br>
    Par défaut, tous les clients Internet itinérants utilisent n’importe quelle [passerelle de gestion cloud](/sccm/core/clients/manage/plan-cloud-management-gateway) disponible. Vous pouvez affecter la valeur **Non** à ce paramètre par exemple quand vous souhaitez limiter l’étendue du service, comme lors d’un projet pilote, ou pour réduire les coûts.



##  <a name="compliance-settings"></a>Paramètres de conformité  

-   **Activer l'évaluation de compatibilité sur les clients** </br>
    Configurez ce paramètre sur **Oui** pour configurer les autres paramètres de ce groupe.
 
-   **Planifier l'évaluation de compatibilité**   </br>
     Cliquez sur **Planifier** pour créer le calendrier par défaut pour les déploiements de la base de référence de configuration. Cette valeur est configurable pour chaque ligne de base dans la boîte de dialogue **Déployer la ligne de base de la configuration**.  

-   **Activer les données et profils utilisateurs**   </br>
     Choisissez **Oui** si vous souhaitez déployer des éléments de configuration de [données et de profils utilisateur](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md).



## <a name="computer-agent"></a>Agent ordinateur  
-   Notifications à l’utilisateur pour les déploiements obligatoires </br>
    Pour plus d’informations sur les trois paramètres suivants, consultez [Notifications à l’utilisateur pour les déploiements obligatoires](/sccm/apps/deploy-use/deploy-applications#user-notifications-for-required-deployments) :
    -   **Échéance du déploiement supérieure à 24 heures, effectuer un rappel à l’utilisateur toutes les (heures)**
    -   **Échéance du déploiement inférieure à 24 heures, effectuer un rappel à l’utilisateur toutes les (heures)**  </br>
    -   **Échéance du déploiement inférieure à 1 heure, effectuer un rappel à l’utilisateur toutes les (minutes)**  </br>

-   **Point de site Web du catalogue d'applications par défaut**   </br>
     Configuration Manager utilise ce paramètre pour connecter les utilisateurs au catalogue d’applications du Centre logiciel. Cliquez sur **Définir un site Web** pour spécifier un serveur qui héberge le point du site web du catalogue d’applications. Entrez son nom NetBIOS ou son nom de domaine complet, spécifiez la détection automatique, ou spécifiez une URL pour les déploiements personnalisés. Dans la plupart des cas, la détection automatique est le meilleur choix car elle offre les avantages suivants :  

    -   Si le site a un point du site web du catalogue d’applications, les clients reçoivent automatiquement un point du site web du catalogue d’applications à partir de leur site.  

    -   Le client préfère les points de site web du catalogue d’applications activés HTTPS sur l’intranet aux serveurs HTTP-uniquement. Cette fonctionnalité offre une protection contre les serveurs non autorisés.

    -   Le point de gestion donne aux clients Internet un point de site web du catalogue d’applications basé sur Internet. Le point de gestion donne aux clients intranet un point du site web du catalogue d’applications basé sur intranet.  

     La détection automatique ne garantit pas que les clients recevront le point du site web du catalogue d’applications le plus proche. Vous pouvez décider de ne pas utiliser **Détecter automatiquement** pour les raisons suivantes :  

     -   Vous voulez configurer manuellement le serveur le plus proche pour les clients ou vous assurer qu'ils ne connectent pas à un serveur via une connexion réseau lente.  

     -   Vous souhaitez contrôler quels clients se connectent à quel serveur. Cette configuration convient pour des raisons professionnelles ou de performances ou à des fins de tests.  

     -   Vous ne souhaitez pas patienter jusqu’à 25 heures ou attendre une modification du réseau pour que les clients utilisent un autre point du site web du catalogue d’applications.  

     Si vous spécifiez le point de site web du catalogue d’applications au lieu d’utiliser la détection automatique, spécifiez le nom NetBIOS plutôt que le nom de domaine complet de l’intranet. Cette configuration réduit la probabilité que le navigateur web invite l’utilisateur à fournir des informations d’identification quand il accède à un catalogue d’applications basé sur intranet. Pour utiliser le nom NetBIOS, les conditions suivantes doivent s'appliquer :  

     -   Le nom NetBIOS est spécifié dans les propriétés du point du site Web du catalogue d'applications.  

     -   Vous utilisez WINS ou tous les clients sont dans le même domaine que le point du site web du catalogue des applications.  

     -   Vous configurez le point du site web du catalogue d’applications pour les connexions clientes HTTP, ou vous configurez le serveur pour HTTPS et le certificat du serveur web a le nom NetBIOS.  

     En règle générale, les utilisateurs sont invités à entrer leurs informations d’identification quand l’URL contient un nom de domaine complet, mais pas quand l’URL est un nom NetBIOS. Les utilisateurs doivent s'attendre à être toujours invités à saisir leurs informations d'identification lorsqu'ils se connectent à partir d'Internet, car cette connexion doit utiliser le nom de domaine complet Internet. Quand vous utilisez un client basé sur Internet et que le navigateur web invite l’utilisateur à fournir des informations d’identification, vérifiez que le point du site web du catalogue d’applications peut se connecter à un contrôleur de domaine pour le compte de l’utilisateur. Cette configuration permet à l’utilisateur de s’authentifier à l’aide de Kerberos.  

    > [!NOTE]  
    >  Fonctionnement de la détection automatique :  
    >   
    >  le client effectue une demande d'emplacement de service à un point de gestion. S'il existe un point de site Web du catalogue d'applications dans le même site que le client, ce serveur est donné au client en tant que le serveur du catalogue d'applications à utiliser. Si plusieurs point du site web du catalogue des applications sont disponibles dans le site, un serveur HTTPS est prioritaire sur un serveur qui n’est pas activé pour le protocole HTTPS. Après ce filtrage, tous les clients reçoivent l’un des serveurs à utiliser comme catalogue d’applications ; Configuration Manager n’équilibre pas la charge entre plusieurs serveurs. Quand le site du client ne contient pas de point du site web du catalogue des applications, le point de gestion retourne de manière non déterministique un point du site web du catalogue des applications à partir de la hiérarchie.  
    >   
    >  Pour les clients basés sur intranet, si vous configurez le point du site web du catalogue d’applications avec un nom NetBIOS pour l’URL du catalogue d’applications, le point de gestion donne aux clients ce nom NetBIOS plutôt que le nom de domaine complet de l’intranet. Pour les clients basés sur Internet, le point de gestion donne uniquement le nom de domaine complet Internet au client.  
    >   
    >  Le client effectue cette demande d'emplacement de service toutes les 25 heures ou chaque fois qu'il détecte un changement de réseau. Par exemple, si le client passe de l’intranet à Internet et qu’il peut localiser un point de gestion basé sur Internet, celui-ci fournit aux clients des serveurs de points du site web du catalogue d’applications basés sur Internet.  

-   **Ajoute un site Web du catalogue d'applications par défaut à la zone des sites de confiance d'Internet Explorer**   </br>
     Si cette option a la valeur **Oui**, le client ajoute automatiquement l’URL actuelle du site web du catalogue d’applications par défaut à la zone des sites de confiance dans Internet Explorer.  

     Ce paramètre garantit que le paramètre Internet Explorer en mode protégé n'est pas activé. Si le mode protégé est activé, le client Configuration Manager peut ne pas être en mesure d’installer des applications à partir du catalogue d’applications. Par défaut, la zone des sites de confiance prend également en charge l'ouverture de session utilisateur pour le catalogue d'applications, ce qui requiert l'authentification Windows.  

     Si vous conservez la valeur **Non** pour cette option, les clients Configuration Manager risquent de ne pas pouvoir installer des applications à partir du catalogue d’applications. Une autre méthode consiste à configurer ces paramètres Internet Explorer dans une autre zone pour l’URL du catalogue d’applications utilisée par les clients.  

    > [!NOTE]  
    >  Chaque fois que Configuration Manager ajoute un catalogue d’applications par défaut à la zone de sites de confiance, Configuration Manager supprime toute URL du catalogue d’applications ajoutée précédemment.  
    >   
    >  Si l’URL est déjà spécifiée dans l’une des zones de sécurité, Configuration Manager ne peut pas l’ajouter. Dans ce cas, vous devez supprimer l’URL de l’autre zone ou configurer manuellement les paramètres Internet Explorer nécessaires.  

-   **Autoriser les applications Silverlight à s'exécuter en mode de confiance élevé**   </br>
     Ce paramètre doit être **Oui** pour que les utilisateurs utilisent le catalogue d’applications.  

     Si vous modifiez ce paramètre, il prend effet au prochain chargement du navigateur par les utilisateurs ou lorsqu'ils actualisent la fenêtre du navigateur actuellement ouverte.  

     Pour plus d’informations sur ce paramètre, consultez [Certificats pour Microsoft Silverlight 5 et mode de confiance élevée obligatoires pour le catalogue des applications](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5).  

-   **Nom d'organisation affiché dans le Centre logiciel**   </br>
     Tapez le nom que les utilisateurs voient dans le Centre logiciel. Ces informations personnalisées aident les utilisateurs à identifier cette application comme une source approuvée.  

-   **Utiliser le nouveau Centre logiciel**   </br>
     Si vous affectez la valeur **Oui** à ce paramètre client, tous les ordinateurs clients utilisent le nouveau Centre logiciel. Le Centre logiciel répertorie les applications accessibles à l’utilisateur qui étaient auparavant uniquement disponibles dans le catalogue d’applications. Le catalogue d’applications nécessite Silverlight, qui n’est pas un prérequis pour le nouveau Centre logiciel.   

     Les rôles de système de site Point du site web du catalogue des applications et Point de service web du catalogue des applications sont toujours exigés pour que les applications accessibles à l’utilisateur apparaissent dans le Centre logiciel.  

     Pour plus d’informations, consultez [Planifier et configurer la gestion des applications](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   **Activer la communication avec le service d’attestation d’intégrité**  </br>
    Configurez ce paramètre sur **Oui** pour que les appareils Windows 10 utilisent [l’attestation d’intégrité](/sccm/core/servers/manage/health-attestation). Quand vous activez ce paramètre, le paramètre suivant est également disponible pour la configuration.

    -   **Utiliser le service d’attestation d’intégrité local** </br>
        Configurez ce paramètre sur **Oui** pour que les appareils utilisent un service local. Configurez ce paramètre sur **non** pour que les appareils utilisent le service cloud de Microsoft.  

-   **Autorisations d'installation**   </br>
    > [!WARNING]  
    >  Ce paramètre s'applique au catalogue des applications et au Centre logiciel. Ce paramètre n’a aucun effet quand les utilisateurs utilisent le portail d’entreprise.  

     Configurez la manière dont les utilisateurs peuvent lancer l'installation des logiciels, des mises à jour logicielles et des séquences de tâches :  

    -   **Tous les utilisateurs** : les utilisateurs disposant de toutes les autorisations, sauf Invité  

    -   **Administrateurs uniquement** : les utilisateurs doivent être membres du groupe Administrateurs local  

    -   **Administrateurs et utilisateurs principaux uniquement**: les utilisateurs doivent être membres du groupe Administrateurs local ou des utilisateurs principaux de l’ordinateur  

    -   **Aucun utilisateur**: aucun utilisateur connecté à un ordinateur client ne peut lancer l’installation des logiciels, mises à jour logicielles et séquences de tâches. Les déploiements requis pour l’ordinateur sont toujours installés à la date d’échéance. Les utilisateurs ne peuvent pas lancer l’installation du logiciel à partir du catalogue d’applications ou du Centre logiciel.  

-   **Interrompre l'entrée du code confidentiel BitLocker au redémarrage**  </br>
     Si les ordinateurs exigent une entrée de code PIN BitLocker, cette option contourne la nécessité d’entrer un code PIN quand l’ordinateur redémarre après l’installation d’un logiciel.  

    -   **Toujours**: Configuration Manager suspend temporairement BitLocker après l'installation d'un logiciel nécessitant un redémarrage de l'ordinateur et qu’un redémarrage a été effectué. Ce paramètre s’applique uniquement à un redémarrage de l’ordinateur lancé par Configuration Manager. Il ne suspend pas l’obligation d’entrer le code PIN BitLocker quand l’utilisateur redémarre l’ordinateur. L’obligation d’entrer un code PIN BitLocker reprend après le démarrage de Windows.

    -   **Jamais**: Configuration Manager ne suspend pas BitLocker au prochain démarrage de l'ordinateur après avoir installé un logiciel qui nécessite un redémarrage. Dans ce cas, l'installation du logiciel ne peut être finalisée que lorsque l'utilisateur entre le code confidentiel pour terminer le processus de démarrage standard et charger Windows.

-   **D’autres logiciels gèrent le déploiement d’applications et de mises à jour logicielles**  </br>
     Activez cette option uniquement si l'une des conditions suivantes s'applique :  

    -   Vous utilisez une solution de fabricant qui nécessite l'activation de ce paramètre.  

    -   Vous utilisez le kit de développement logiciel (SDK) Configuration Manager pour gérer les notifications d’agent client et l’installation d’applications et de mises à jour logicielles.  

    > [!WARNING]  
    >  Si vous choisissez cette option quand aucune de ces conditions ne s’applique, le client n’installe pas les mises à jour logicielles et les applications exigées. Ce paramètre n’empêche pas les utilisateurs d’installer des applications à partir du catalogue d’applications, et n’empêche pas l’installation des packages, programmes et séquences de tâches.  

-   **Stratégie d'exécution de PowerShell**  </br>
     Configurez la façon dont les clients Configuration Manager peuvent exécuter des scripts Windows PowerShell. Ces scripts sont souvent utilisés pour la détection dans les éléments de configuration de paramètres de conformité. Ils peuvent également être envoyés dans un déploiement sous la forme d’un script standard.  

    -   **Ignorer** : le client Configuration Manager ignore la configuration Windows PowerShell sur l’ordinateur client afin que les scripts non signés puissent s’exécuter.  

    -   **Restreint** : le client Configuration Manager utilise la configuration Windows PowerShell actuelle sur l’ordinateur client. Cette configuration détermine si les scripts non signés peuvent s’exécuter.  

    -   **Toutes signées** : le client Configuration Manager exécute les scripts uniquement s’ils sont signés par un éditeur approuvé. Cette restriction s'applique indépendamment de la configuration Windows PowerShell actuelle sur l'ordinateur client.  

     Cette option nécessite au minimum la version 2.0 de Windows PowerShell. La valeur par défaut est **Toutes signées**.  

    > [!TIP]  
    >  Si les scripts non signés ne parviennent pas à s’exécuter en raison de ce paramètre client, Configuration Manager signale cette erreur ainsi :  
    >   
    > -   L’espace de travail **Surveillance** dans la console affiche l’ID d’erreur d’état de déploiement **0x87D00327** et la description **Le script n’est pas signé**  
    > -   Les rapports affichent le type d’erreur **Erreur de découverte**, puis le code d’erreur **0x87D00327** et la description **Le script n’est pas signé** ou le code d’erreur  **0x87D00320** et la description **L’environnement d’exécution de scripts n’a pas encore été installé**. Exemple de rapport : **Détails des erreurs des éléments de configuration dans la base de référence de configuration d’un composant**.  
    > -   Le fichier **DcmWmiProvider.log** affiche le message **Le script n’est pas signé (Erreur : 87D00327; Source : CCM)**.  

-   **Afficher les notifications de nouveaux déploiements**  </br>
     Choisissez **Oui** pour afficher une notification pour les déploiements disponibles moins d’une semaine.  Ce message s’affiche à chaque démarrage de l’agent du client.

-   **Désactiver la randomisation des échéances**  </br>
     Quand la date limite est atteinte, ce paramètre détermine si le client utilise un délai d’activation pouvant aller jusqu’à deux heures pour installer les mises à jour logicielles requises. Par défaut, le délai d'activation est désactivé.  

     Pour les scénarios d’infrastructure VDI (Virtual Desktop Infrastructure), ce délai aide à distribuer le traitement par le processeur et le transfert de données pour un ordinateur hôte doté de plusieurs machines virtuelles. Même si vous n’utilisez pas d’infrastructure VDI, si de nombreux clients installent les même mises à jour en même temps, cela peut augmenter l’utilisation du processeur sur le serveur de site. Ce comportement peut également ralentir les points de distribution et réduire considérablement la bande passante réseau disponible.  

     Si les clients doivent installer des mises à jour logicielles requises à l’échéance du déploiement sans délai, configurez ce paramètre sur **Oui**. 

-   **Période de grâce pour la mise en œuvre après l’échéance du déploiement (en heures)** </br>
     Si vous souhaitez accorder aux utilisateurs plus de temps pour installer les déploiements de mises à jour logicielles ou d’applications obligatoires au-delà de l’échéance, configurez ce paramètre sur **Oui**. Cette période de grâce est destinée au scénario dans lequel un ordinateur est hors tension pendant une durée prolongée et l’utilisateur doit installer de nombreux déploiements d’applications ou de mises à jour. Par exemple, si un utilisateur rentre de congés, il peut être amené à patienter longtemps pendant que le client installe les déploiements d’applications en retard. 

     Définissez une période de grâce comprise entre une et 120 heures. Utilisez ce paramètre conjointement avec la propriété de déploiement **Différer la mise en œuvre de ce déploiement selon les préférences de l’utilisateur**. Pour plus d’informations, consultez [Déployer des applications](/sccm/apps/deploy-use/deploy-applications).



##  <a name="computer-restart"></a>Redémarrage de l’ordinateur  
 Les paramètres suivants doivent être inférieurs à la durée de la fenêtre de maintenance la plus courte appliquée à l’ordinateur.  

 Pour plus d’informations sur les fenêtres de maintenance, consultez [Comment utiliser les fenêtres de maintenance dans System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

-   **Afficher une notification temporaire à l’utilisateur indiquant l’intervalle avant la fermeture de la session de l’utilisateur ou le redémarrage de l’ordinateur (minutes)**
-   **Afficher une boîte de dialogue que l’utilisateur ne peut pas fermer, indiquant l’intervalle de compte à rebours avant la fermeture de la session de l’utilisateur ou le redémarrage de l’ordinateur (minutes)**



##  <a name="endpoint-protection"></a>Endpoint Protection  
>  [!Tip]   
> En plus des informations suivantes, vous pouvez trouver d’autres détails sur l’utilisation des paramètres du client Endpoint Protection dans [Exemple de scénario : utilisation de System Center Endpoint Protection pour protéger des ordinateurs contre les programmes malveillants dans System Center Configuration Manager](/sccm/protect/deploy-use/scenarios-endpoint-protection).

-   **Gérer le client Endpoint Protection sur les ordinateurs clients**  </br>
     Choisissez **Oui** si vous souhaitez gérer les clients Endpoint Protection et Windows Defender existants sur des ordinateurs de la hiérarchie.  

     Choisissez cette option si vous avez déjà installé le client Endpoint Protection et que vous souhaitez le gérer avec Configuration Manager.  Cette installation distincte inclut un processus sous forme de script utilisant un programme et un package ou une application Configuration Manager.

-   **Installer le client Endpoint Protection sur les ordinateurs clients**   </br>
     Choisissez **Oui** pour installer et activer le client Endpoint Protection sur les ordinateurs clients qui ne l’exécutent pas encore.  

    > [!NOTE]  
    >  Si le client Endpoint Protection est déjà installé, le fait de choisir la valeur **Non** ne désinstalle pas le client Endpoint Protection. Pour désinstaller le client Endpoint Protection, affectez au paramètre client **Gérer le client Endpoint Protection sur les ordinateurs clients** la valeur **Non**. Ensuite, déployez un package et un programme pour désinstaller le client Endpoint Protection.  

-   **Supprimer automatiquement le logiciel anti-programmes malveillants installé avant Endpoint Protection** </br>
    Configurez ce paramètre sur **Oui** pour que le client Endpoint Protection tente de désinstaller les autres applications anti-programmes malveillants. La présence de plusieurs clients anti-programmes malveillants sur le même appareil peut générer un conflit et affecter les performances du système.

-   **Autoriser l’installation du client Endpoint Protection et redémarrer en dehors des fenêtres de maintenance. Celles-ci doivent être d’une durée minimale de 30 minutes pour l’installation du client** </br>
    Configurez ce paramètre sur **Oui** pour remplacer les comportements d’installation par défaut avec des fenêtres de maintenance. Ce paramètre satisfait aux besoins de l’entreprise en ce qui concerne la priorité de la maintenance du système pour des raisons de sécurité. 

-   **Pour les appareils Windows Embedded munis de filtres d’écriture, valider l’installation du client Endpoint Protection (nécessite un redémarrage)**  </br>
     Choisissez **Oui** pour désactiver le filtre d’écriture sur l’appareil Windows Embedded et le redémarrer. Cette action valide l’installation sur l’appareil.  

     Si vous configurez ce paramètre sur **Non**, le client est installé sur une superposition temporaire qui est effacée lors du redémarrage de l’appareil. Dans ce scénario, le client Endpoint Protection n’est entièrement installé que lorsqu’une autre installation valide les modifications apportées à l’appareil. Il s’agit de la configuration par défaut.  

-   **Supprimer tout redémarrage de l’ordinateur requis après l’installation du client Endpoint Protection**  </br>
     Choisissez **Oui** pour ignorer le redémarrage de l’ordinateur s’il est nécessaire après l’installation du client Endpoint Protection.  

    > [!IMPORTANT]  
    >  Si le client Endpoint Protection nécessite un redémarrage de l’ordinateur et que ce paramètre est **Non**, l’ordinateur redémarre quelle que soit la fenêtre de maintenance configurée.  

-   **Durée pendant laquelle les utilisateurs sont autorisés à différer un redémarrage nécessaire pour terminer l’installation de Endpoint Protection (heures)**  </br>
     Si un redémarrage est nécessaire après l’installation du client Endpoint Protection, ce paramètre spécifie le nombre d’heures duquel les utilisateurs sont autorisés à différer le redémarrage. Ce paramètre exige que le paramètre **Supprimer tout redémarrage d’ordinateur requis après l’installation du client Endpoint Protection** soit **Non**.  

-   **Désactiver les autres sources (telles que Microsoft Windows Update, Microsoft Windows Server Update Services ou les partages UNC) pour la mise à jour initiale des définitions sur les ordinateurs clients**  </br>
     Choisissez **Oui** si vous souhaitez que Configuration Manager installe uniquement la mise à jour de définition initiale sur les ordinateurs clients. Ce paramètre peut s'avérer pratique pour éviter les connexions réseau inutiles et réduire la bande passante réseau pendant l'installation initiale de la mise à jour de définition.  



##  <a name="enrollment"></a>Inscription

-   **Intervalle d’interrogation pour clients hérités de périphériques mobiles** </br>
    Cliquez sur **Déf. un interv.** pour spécifier la durée, en minutes ou heures, d’interrogation de la stratégie par les appareils mobiles hérités. Ces appareils incluent des plateformes telles que Windows CE, Mac OS X et Unix ou Linux.

-   **Fréquence d’interrogation des appareils récents (minutes)** </br>
    Entrez l’intervalle d’interrogation (en minutes) de la stratégie par les appareils récents. Ce paramètre concerne les appareils Windows 10 gérés par le biais de la gestion des appareils mobiles locale.

-   **Autoriser les utilisateurs à inscrire des appareils mobiles et des ordinateurs Mac** </br>
    Pour activer l’inscription des appareils hérités par l’utilisateur, configurez ce paramètre sur **Oui**, puis configurez le paramètre suivant :

    -   **Profil d’inscription** </br>
        Cliquez sur **Définir un profil** pour créer ou sélectionner un profil d’inscription. Pour plus d’informations, consultez [Configurer les paramètres client pour l’inscription](/sccm/core/clients/deploy/deploy-clients-to-macs#configure-client-settings-for-enrollment).

-   **Autoriser les utilisateurs à inscrire des appareils récents** </br>
    Pour activer l’inscription des appareils récents par l’utilisateur, configurez ce paramètre sur **Oui**, puis configurez le paramètre suivant :

    -   **Profil d’inscription des appareils récents** </br>
        Cliquez sur **Définir un profil** pour créer ou sélectionner un profil d’inscription. Pour plus d’informations, consultez [Créer un profil d’inscription qui permet aux utilisateurs d’inscrire des appareils récents](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm#bkmk_createProf).



##  <a name="hardware-inventory"></a>Inventaire matériel  

-   **Activer l’inventaire matériel sur les clients** </br>
    Par défaut, ce paramètre est défini sur **Oui**. Pour plus d’informations, consultez [Présentation de l’inventaire matériel](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).

-   **Calendrier de l’inventaire matériel** </br>
    Cliquez sur **Planifier** pour régler la fréquence à laquelle les clients exécutent le cycle d’inventaire matériel. Par défaut, ce cycle se produit tous les sept jours.

-   **Délai aléatoire maximal (minutes)** </br>
    Spécifiez le nombre maximal de minutes pour la définition d’un délai aléatoire du cycle d’inventaire matériel par le client Configuration Manager, par rapport à la planification définie. Cette fonctionnalité de randomisation parmi tous les clients aide à équilibrer la charge d’inventaire sur le serveur de site. Vous pouvez spécifier une valeur comprise entre 0 et 480 minutes. Par défaut, cette valeur est définie sur 240 minutes (quatre heures).

-   **Taille maximale du fichier MIF personnalisé (Ko)**  </br>
     Spécifiez la taille maximale, en kilo-octets (Ko), autorisée pour chaque fichier Management Information Format (MIF) personnalisé recueilli par le client lors d’un cycle d’inventaire matériel. L’agent d’inventaire matériel Configuration Manager ne traite pas les fichiers MIF personnalisés qui dépassent cette taille. Vous pouvez spécifier une taille comprise entre 1 et 5 120 Ko. Par défaut, cette valeur est définie à 250 Ko. Ce paramètre n'affecte pas la taille du fichier de données d'inventaire matériel ordinaire.  

    > [!NOTE]  
    >  Ce paramètre est disponible uniquement dans les paramètres client par défaut.  

-   **Classes d'inventaire matériel**  </br>
     Cliquez sur **Déf. classes** pour étendre les informations matérielles que vous recueillez auprès des clients sans modifier manuellement le fichier sms_def.mof. Pour plus d’informations, consultez [Guide pratique pour configurer l’inventaire matériel](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

-   **Collecter des fichiers MIF**  </br>
     Utilisez ce paramètre pour spécifier si vous souhaitez collecter des fichiers MIF à partir de clients Configuration Manager pendant l’inventaire matériel.  

     Pour qu’un fichier MIF soit collecté par un inventaire matériel, il doit se trouver à l’emplacement approprié sur l’ordinateur client. Par défaut, les fichiers se trouvent aux chemins suivants :  

    -   Les **fichiers IDMIF** doivent être dans le dossier Windows\System32\CCM\Inventory\Idmif. 

    -   Les **fichiers NOIDMIF** doivent être dans le dossier Windows\System32\CCM\Inventory\Noidmif.

    > [!NOTE]  
    >  Ce paramètre est disponible uniquement dans les paramètres client par défaut.

   

##  <a name="metered-internet-connections"></a>Connexions Internet facturées à l’usage  
 Gérez la façon dont les ordinateurs Windows 8 et versions ultérieures utilisent des connexions Internet facturées à l’usage pour communiquer avec Configuration Manager. Les fournisseurs Internet facturent parfois en fonction de la quantité de données que vous envoyez et recevez lorsque vous utilisez une connexion Internet facturée à l'usage.  

> [!NOTE]  
>  Le paramètre client configuré n’est pas appliqué dans les scénarios suivants :  
>   
> -   L’ordinateur se trouve sur une connexion de données itinérante : le client Configuration Manager n’exécute aucune tâche nécessitant le transfert de données vers des sites Configuration Manager.  
> -   Les propriétés de la connexion réseau Windows sont configurées pour une connexion non facturée à l’usage : le client Configuration Manager se comporte comme si la connexion n’était pas facturée à l’usage, et transfère donc les données vers le site.  

-   **Communication des clients sur des connexions Internet facturées à l’usage**  </br>
     Choisissez l’une des options suivantes pour ce paramètre :  

    -   **Autoriser**: toutes les communications client sont autorisées via la connexion Internet facturée à l’usage, sauf si l’appareil client utilise une connexion de données itinérante.  

    -   **Limite**: seules les communications client suivantes sont autorisées via la connexion Internet facturée à l’usage :  

        -   Récupération de stratégie client  

        -   Messages d'état du client à envoyer au site  

        -   Demandes d'installation de logiciels à l'aide du catalogue des applications  

        -   Déploiements requis (lorsque la date limite d'installation est atteinte)  

        > [!IMPORTANT]  
        >  Le client autorise toujours les installations de logiciels à partir du Centre logiciel ou du catalogue des applications, quels que soient les paramètres de la connexion Internet facturée à l’usage.  

         Si la limite de transfert de données est atteinte pour la connexion Internet facturée à l’usage, le client n’essaie plus de communiquer avec les sites Configuration Manager.  

    -   **Bloc** : le client Configuration Manager n’essaie pas de communiquer avec les sites Configuration Manager quand il est sur une connexion Internet limitée. Il s’agit de l’option par défaut.  



##  <a name="power-management"></a>Gestion de l'alimentation  

-   **Autoriser la gestion de l’alimentation des périphériques** </br>
    Configurez ce paramètre sur **Oui** pour activer la gestion de l’alimentation sur les clients. Pour plus d’informations, consultez [Présentation de la gestion de l’alimentation](/sccm/core/clients/manage/power/introduction-to-power-management).

-   **Autoriser les utilisateurs à exclure leur appareil de la gestion de l'alimentation**  </br>
     Choisissez **Oui** pour permettre aux utilisateurs du Centre logiciel d’exclure leur ordinateur des paramètres de gestion de l’alimentation configurés.  

-   **Autoriser le proxy de mise en éveil** </br> 
     Spécifiez **Oui** pour compléter le paramètre d'éveil par appel réseau du site lorsqu'il est configuré pour les paquets monodiffusion.  

     Pour plus d’informations sur le proxy de mise en éveil, consultez [Planifier la sortie de veille des clients dans System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    > [!WARNING]  
    >  N'activez pas le proxy de mise en éveil dans un réseau de production sans d'abord comprendre comment il fonctionne et l'évaluer dans un environnement de test.  

    Ensuite, configurez les paramètres supplémentaires suivants en fonction des besoins :

    -   **Numéro de port du proxy de mise en éveil (UDP)**  </br>
         Numéro du port utilisé par les clients pour envoyer des paquets de réveil aux ordinateurs en état de veille. Conservez le port par défaut 25536 ou remplacez-le par le numéro de votre choix.  

    -   **Numéro de port Wake On LAN (UDP)** </br> 
         Conservez la valeur par défaut (9), sauf si vous avez modifié le numéro du port Wake On LAN (UDP) sous l’onglet **Ports**des **Propriétés** du site.  

        > [!IMPORTANT]  
        >  Ce numéro doit correspondre au numéro figurant dans les **Propriétés**du site. Si vous modifiez ce numéro dans un seul emplacement, sachez qu’il n’est pas actualisé automatiquement dans l’autre emplacement.  

    -   **Exception du pare-feu Windows Defender pour le proxy de mise en éveil** </br>
         Le client Configuration Manager configure automatiquement le numéro de port du proxy de mise en éveil sur les appareils qui exécutent le Pare-feu Windows Defender. Cliquez sur **Configurer** pour spécifier les profils de pare-feu souhaités.

        Si les clients exécutent un autre pare-feu, vous devez le configurer manuellement pour autoriser le **Numéro de port du proxy de mise en éveil (UDP)**.  
        
    -   **Préfixes IPv6 si nécessaires pour DirectAccess ou d’autres périphériques réseau intervenants. Spécifiez plusieurs entrées en utilisant une virgule** </br>
        Entrez les préfixes IPv6 nécessaires pour que le proxy de mise en éveil fonctionne sur votre réseau.



##  <a name="remote-tools"></a>Outils de contrôle à distance  

-   **Activer le contrôle à distance sur des clients** et **Profils d'exception de pare-feu**  </br>
     Cliquez sur **Configurer** pour activer la fonctionnalité de contrôle à distance de Configuration Manager. Vous pouvez éventuellement configurer les paramètres du pare-feu pour autoriser le contrôle à distance sur des ordinateurs clients.  

     Le contrôle à distance est désactivé par défaut.  

    > [!IMPORTANT]  
    >  Si les paramètres de pare-feu ne sont pas configurés, le contrôle à distance risque de ne pas fonctionner correctement.  

-   **Les utilisateurs peuvent modifier les paramètres de stratégie ou de notification dans le Centre logiciel**  </br>
     Indiquez si les utilisateurs peuvent modifier les options de contrôle à distance à partir du Centre logiciel.  

-   **Autoriser le contrôle à distance d'un ordinateur autonome**  </br>
     Indiquez si un administrateur peut utiliser le contrôle à distance pour accéder à un ordinateur client qui est déconnecté ou verrouillé. Seul un ordinateur connecté et déverrouillé peut être contrôlé à distance quand ce paramètre est désactivé.  

-   **Inviter l'utilisateur à autoriser le contrôle à distance**  </br>
     Choisissez si l’ordinateur client affiche un message demandant l’autorisation de l’utilisateur avant d’autoriser une session de contrôle à distance.  

-   **Demander à l’utilisateur l’autorisation de transférer le contenu du Presse-papiers partagé** </br>
    Donnez à vos utilisateurs la possibilité d’accepter ou de refuser des transferts de fichiers avant de transférer le contenu du Presse-papiers partagé dans une session de contrôle à distance. Les utilisateurs n’ont besoin d’accorder l’autorisation qu’une seule fois par session tandis que l’observateur ne peut pas s’accorder l’autorisation d’effectuer le transfert de fichiers.

-   **Accorder l'autorisation de contrôle à distance au groupe Administrateurs local**  </br>
     Indiquez si les administrateurs locaux sur le serveur qui lance la connexion de contrôle à distance peuvent établir des sessions de contrôle à distance vers des ordinateurs client.  

-   **Niveau d'accès autorisé**  </br>
     Spécifiez le niveau d’accès de contrôle à distance à accorder. Choisissez parmi les paramètres suivants :  
    - **Aucun accès**
    - **Afficher uniquement**
    - **Contrôle intégral**  

-   **Observateurs autorisés des options de contrôle à distance et d’assistance à distance**  </br>
     Cliquez sur **Définir des observateurs** pour spécifier les noms des utilisateurs Windows qui peuvent établir des sessions de contrôle à distance vers des ordinateurs clients.  

-   **Afficher l'icône de notification de session sur la barre des tâches**  </br>
     Configurez ce paramètre sur **Oui** pour afficher une icône dans la barre des tâches de Windows du client quand une session de contrôle à distance est en cours.  

-   **Afficher la barre de connexion de session**  </br>
     Configurez ce paramètre sur **Oui** pour afficher une barre de connexion de session de haute visibilité sur les clients quand une session de contrôle à distance est en cours.  

-   **Émettre un signal sonore sur le client**  </br>
     Configurez ce paramètre pour utiliser le son pour indiquer qu’une session de contrôle à distance est en cours sur un ordinateur client. Sélectionnez l'une des options suivantes :
    - **Aucun signal sonore**
    - **Début et fin de session** (par défaut)
    - **Fréquemment au cours d’une session**  

-   **Gérer les paramètres de l'Assistance à distance non sollicités**  </br>
     Configurez ce paramètre sur **Oui** pour autoriser Configuration Manager à gérer les sessions d’assistance à distance non sollicitées.  

     Dans une session d’assistance à distance non sollicitée, l’utilisateur de l’ordinateur client n’a pas demandé d’assistance pour lancer la session.  

-   **Gérer les paramètres de l'Assistance à distance sollicités**  </br>
     Configurez ce paramètre sur **Oui** pour autoriser Configuration Manager à gérer les sessions d’assistance à distance sollicitées.  

     Dans une session d’assistance à distance sollicitée, l’utilisateur de l’ordinateur client envoie une demande d’assistance à distance à l’administrateur.  

-   **Niveau d'accès de l'Assistance à distance**  </br>
     Choisissez le niveau d’accès à attribuer aux sessions d’assistance à distance lancées à partir de la console Configuration Manager.  Sélectionnez l'une des options suivantes :
    - **Aucun** (par défaut)
    - **Affichage à distance**
    - **Contrôle intégral**

    > [!NOTE]  
    >  L'utilisateur de l'ordinateur client doit toujours autoriser l'ouverture d'une session d'assistance à distance.  

-   **Gérer les paramètres du Bureau à distance**  </br>
     Configurez ce paramètre sur **Oui** pour autoriser Configuration Manager à gérer les sessions Bureau à distance des ordinateurs.  

-   **Autoriser la connexion des observateurs autorisés à l'aide d'une connexion Bureau à distance**  </br>
     Configurez ce paramètre sur **Oui** pour ajouter les utilisateurs spécifiés dans la liste des observateurs autorisés au groupe d’utilisateurs locaux Bureau à distance sur les clients.  

-   **Exiger l'authentification au niveau du réseau sur les ordinateurs exécutant le système d'exploitation Windows Vista et versions ultérieures**  </br>
     Configurez ce paramètre sur **Oui** pour utiliser l’authentification au niveau du réseau afin d’établir des connexions Bureau à distance aux ordinateurs clients. L’authentification au niveau du réseau nécessite moins de ressources d’ordinateur distant, car l’authentification des utilisateurs se termine avant l’établissement de la connexion Bureau à distance. L’authentification au niveau du réseau est une configuration plus sécurisée. Elle contribue à protéger l’ordinateur des utilisateurs ou logiciels malveillants, et réduit le risque d’attaque par déni de service.  



## <a name="software-center"></a>Centre logiciel

-   **Sélectionnez ces nouveaux paramètres pour spécifier des informations sur l’entreprise** </br>
    Configurez ce paramètre sur **Oui**, puis spécifiez les paramètres suivants pour personnaliser le Centre logiciel et l’adapter à votre organisation :

    - **Nom de la société** </br>
        Entrez le nom d’organisation visible par les utilisateurs dans le Centre logiciel.
    - **Modèle de couleurs pour le Centre logiciel** </br>
        Cliquez sur **Sélectionner une couleur** pour définir la couleur principale utilisée par le Centre logiciel.
    - **Sélectionner un logo pour le Centre logiciel** </br>
        Cliquez sur **Parcourir** pour sélectionner une image à afficher dans le Centre logiciel. Le logo doit être de type JPEG, PNG ou BMP et au format 400 x 100 pixels, avec une taille maximale de 750 Ko. Le nom de fichier du logo ne doit pas contenir d’espace. <!--SMS.503731 space in filename, noticed BMP missing as filetype-->

-   Visibilité de l’onglet Centre logiciel </br>
    Affectez la valeur **Oui** aux paramètres supplémentaires de ce groupe pour afficher les onglets suivants dans le Centre logiciel :
    - **Applications**
    - **Mises à jour**
    - **Systèmes d’exploitation**
    - **État de l’installation**
    - **Conformité de l’appareil**
    - **Options**

    Par exemple, si votre organisation n’utilise pas de stratégies de conformité et que vous souhaitez masquer l’onglet Conformité de l’appareil dans le Centre logiciel, affectez la valeur **Non** à l’onglet **Activer l’onglet Conformité de l’appareil**.



## <a name="software-deployment"></a>Déploiement logiciel  

-   **Planifier la réévaluation des déploiements**  </br>
     Configurez une planification pour la réévaluation des règles de spécifications par Configuration Manager pour tous les déploiements. La valeur par défaut est tous les sept jours.  

    > [!IMPORTANT]  
    >  Nous vous recommandons de ne pas choisir une valeur inférieure à la valeur par défaut, Un calendrier de réévaluation plus agressif affecte négativement les performances de votre réseau et des ordinateurs clients.  

     Pour lancer cette action à partir d’un client, choisissez le **Cycle d’évaluation du déploiement de l’application** sous l’onglet **Actions** du panneau de configuration de **Configuration Manager**.  



##  <a name="software-inventory"></a>Inventaire logiciel  

-   **Activer l’inventaire logiciel sur les clients** </br>
    Par défaut, ce paramètre est défini sur **Oui**. Pour plus d’informations, consultez [Présentation de l’inventaire logiciel](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).

-   **Planifier l’inventaire logiciel et le regroupement de fichiers** </br>
    Cliquez sur **Planifier** pour régler la fréquence à laquelle les clients exécutent les cycles de regroupement de fichiers et d’inventaire logiciel. Par défaut, ce cycle se produit tous les sept jours.

-   **Détails sur le rapport d'inventaire**  </br>
     Spécifiez l’un des niveaux d’informations de fichiers suivants à inventorier :
    - **Fichier uniquement**
    - **Produit uniquement**
    - **Détails complets** (par défaut)

-   **Inventorier ces types de fichiers**  </br>
     Si vous souhaitez spécifier les types de fichiers à inventorier, cliquez sur **Définir des types**, puis configurez les options suivantes :  

    > [!NOTE]  
    >  Si plusieurs paramètres clients personnalisés sont appliqués à un ordinateur, l’inventaire retourné par chaque paramètre est fusionné.  

    -   Cliquez sur l’icône **Nouveau** pour ajouter un nouveau type de fichier à l’inventaire. Ensuite, spécifiez les informations suivantes dans la boîte de dialogue **Propriétés du fichier inventorié** :  

        -   **Nom** : définissez le nom du fichier à inventorier. Utilisez un astérisque (**&#42;**) comme caractère générique pour représenter une chaîne de texte et un point d’interrogation (**?**) pour représenter n’importe quel caractère. Par exemple, si vous souhaitez inventorier tous les fichiers portant l’extension .doc, spécifiez le nom de fichier **\*.doc**.  

        -   **Emplacement** : cliquez sur **Définir** pour ouvrir la boîte de dialogue **Propriétés du chemin d’accès**. Configurez l’inventaire logiciel pour rechercher le fichier défini sur tous les disques durs des clients, effectuer une recherche à un emplacement donné (tel que **C:\Dossier**) ou rechercher une variable (telle que *%windir%*). Vous pouvez également exécuter une recherche dans tous les sous-dossiers du chemin indiqué.  

        -   **Exclure les fichiers chiffrés et compressés** : quand vous choisissez cette option, tous les fichiers compressés ou chiffrés ne sont pas inventoriés.  

        -   **Exclure des fichiers dans le dossier Windows** : quand vous choisissez cette option, tous les fichiers dans le dossier Windows et ses sous-répertoires ne sont pas inventoriés.  

    -   Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés du fichier inventorié** .  

    -   Ajoutez tous les fichiers à inventorier, puis cliquez sur **OK** pour fermer la boîte de dialogue **Configurer le paramètre client**.  

-   **Collecter des fichiers**  </br>
     Si vous souhaitez collecter des fichiers stockés à partir d’ordinateurs clients, cliquez sur **Définir des fichiers**, puis configurez les paramètres suivants :  

    > [!NOTE]  
    >  Si plusieurs paramètres clients personnalisés sont appliqués à un ordinateur, l’inventaire retourné par chaque paramètre est fusionné.  

    -   Dans la boîte de dialogue **Configurer le paramètre client**, cliquez sur l’icône **Nouveau** pour ajouter un fichier à collecter.  

    -   Dans la boîte de dialogue **Propriétés du fichier collecté** , fournissez les informations suivantes :  

        -   **Nom** : définissez le nom du fichier à collecter. Utilisez un astérisque (**&#42;**) comme caractère générique pour représenter une chaîne de texte et un point d’interrogation (**?**) pour représenter n’importe quel caractère.  

        -   **Emplacement** : cliquez sur **Définir** pour ouvrir la boîte de dialogue **Propriétés du chemin d’accès**. Configurez l’inventaire logiciel pour rechercher le fichier à collecter sur tous les disques durs des clients, effectuer une recherche à un emplacement donné (tel que **C:\Dossier**) ou rechercher une variable (telle que *%windir%*). Vous pouvez également exécuter une recherche dans tous les sous-dossiers du chemin indiqué.  

        -   **Exclure les fichiers chiffrés et compressés** : quand vous choisissez cette option, tous les fichiers compressés ou chiffrés ne sont pas collectés.  

        -   **Arrêter le regroupement de fichiers lorsque la taille totale dépasse (Ko)** : spécifiez la taille de fichier, en Ko, au-delà de laquelle le client arrête la collecte des fichiers spécifiés.  

          > [!NOTE]  
          >  Le serveur de site collecte les cinq dernières versions modifiées des fichiers collectés et les enregistre dans le répertoire *&lt;répertoire_installation_ConfigMgr\>*\Inboxes\Sinv.box\Filecol. Si un fichier n’a pas changé depuis le dernier cycle d’inventaire logiciel, le fichier n’est pas recollecté.  
          >   
          >  L’inventaire logiciel ne collecte pas les fichiers de plus de 20 Mo.  
          >   
          >  La valeur **Taille maximale pour tous les fichiers regroupés (Ko)** dans la boîte de dialogue **Configurer le paramètre client** indique la taille maximale de tous les fichiers collectés. Quand cette taille est atteinte, la collecte de fichiers s’arrête. Tous les fichiers déjà regroupés sont conservés et envoyés au serveur de site.  

          > [!IMPORTANT]
          >  Si vous configurez l’inventaire logiciel pour collecter un grand nombre de fichiers volumineux, vous risquez d’affecter négativement les performances du serveur de site et du réseau.  

        Pour plus d’informations sur l’affichage des fichiers collectés, consultez [Guide pratique pour utiliser l’Explorateur de ressources pour afficher l’inventaire logiciel](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    -   Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés du fichier collecté** .  

    -   Ajoutez tous les fichiers à collecter, puis cliquez sur **OK** pour fermer la boîte de dialogue **Configurer le paramètre client**.  

-   **Définir des noms**  </br>
     L’agent d’inventaire logiciel récupère le nom du fabricant et du produit à partir des informations d’en-tête de fichier. Ces noms ne sont pas systématiquement normalisés dans les informations d’en-tête de fichier. Quand vous affichez l’inventaire logiciel dans l’Explorateur de ressources, des versions différentes du même nom de fabricant ou de produit peuvent apparaître. Pour normaliser ces noms complets, cliquez sur **Définir des noms**, puis configurez les paramètres suivants :  

    -   **Type de nom**  : l’inventaire logiciel collecte des informations sur les produits et les fabricants. Choisissez si vous souhaitez configurer des noms complets pour un **Fabricant** ou un **Produit**.  

    -   **Nom complet** : spécifiez le nom complet que vous souhaitez utiliser à la place des noms dans la liste **Noms inventoriés**. Cliquez sur l’icône **Nouveau** pour spécifier un nouveau nom complet.  

    -   **Noms inventoriés**: cliquez sur l’icône **Nouveau** pour ajouter un nom inventorié. Ce nom est remplacé dans l’inventaire logiciel par le nom choisi dans la liste **Nom complet**. Vous pouvez ajouter plusieurs noms à remplacer.  



##  <a name="software-metering"></a>Contrôle de logiciel

-   **Activer le contrôle de logiciel sur les clients** </br>
    Par défaut, ce paramètre est défini sur **Oui**. Pour plus d’informations, consultez [Contrôle de logiciel](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering#configure-software-metering).

-   **Planifier le regroupement de données** </br>
    Cliquez sur **Planifier** pour régler la fréquence à laquelle les clients exécutent le cycle de contrôle de logiciel. Par défaut, ce cycle se produit tous les sept jours.



##  <a name="software-updates"></a>Mises à jour logicielles  

-   **Activer les mises à jour logicielles sur les clients**  </br>
     Utilisez ce paramètre pour activer les mises à jour logicielles sur les clients Configuration Manager. Quand vous désactivez ce paramètre, Configuration Manager supprime les stratégies de déploiement existantes du client. Lorsque vous réactivez ce paramètre, le client télécharge la stratégie de déploiement actuelle.  

    > [!IMPORTANT]  
    >  Quand vous désactivez ce paramètre, les stratégies de conformité qui reposent sur les mises à jour logicielles ne fonctionnent plus.  

-   **Calendrier d'analyse des mises à jour logicielles**  </br>
     Cliquez sur **Planifier** pour spécifier la fréquence à laquelle le client lance une analyse de la conformité. Cette analyse détermine l’état des mises à jour logicielles sur le client (par exemple, requise ou installée). Pour plus d’informations sur l’évaluation de la conformité, consultez [Évaluation de la conformité des mises à jour logicielles](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

     Par défaut, cette analyse utilise un calendrier simple pour une exécution tous les sept jours. Vous pouvez créer un calendrier personnalisé pour spécifier une date et une heure exactes de début, utiliser le temps universel coordonné (UTC) ou l’heure locale, et configurer l’intervalle de récurrence pour un jour spécifique de la semaine.  

    > [!NOTE]  
    >  Si vous spécifiez un intervalle inférieur à une journée, Configuration Manager rétablit automatiquement la valeur par défaut (une journée).  

    > [!WARNING]  
    >  L’heure de début réelle sur les ordinateurs clients est l’heure de début plus une durée aléatoire de deux heures maximum. Cette fonctionnalité de randomisation empêche les ordinateurs clients de lancer l’analyse et de se connecter simultanément au point de mise à jour logicielle actif.  

-   **Planifier la réévaluation du déploiement**  </br>
     Cliquez sur **Planifier** pour configurer la fréquence à laquelle l’agent client des mises à jour logicielles réévalue les mises à jour logicielles pour en déterminer l’état de l’installation sur les ordinateurs clients Configuration Manager. Quand des mises à jour logicielles préalablement installées ne sont plus disponibles sur les clients, mais sont toujours requises, le client réinstalle les mises à jour logicielles.

     Ajustez cette planification en fonction de la stratégie de l’entreprise relative à la conformité des mises à jour logicielles et du droit des utilisateurs à désinstaller des mises à jour logicielles. Chaque cycle de réévaluation du déploiement provoque une activité processeur sur l’ordinateur client et le réseau. Par défaut, ce paramètre utilise un calendrier simple pour lancer l’analyse de réévaluation du déploiement tous les sept jours.  

    > [!NOTE]  
    >  Si vous spécifiez un intervalle inférieur à une journée, Configuration Manager rétablit automatiquement la valeur par défaut (une journée).  

-   **Dès que l’échéance d’un déploiement de mise à jour logicielle est atteinte, installer tous les autres déploiements de mise à jour logicielle avec une échéance pendant une période de temps spécifiée**  </br>
     Configurez ce paramètre sur **Oui** pour installer toutes les mises à jour à partir des déploiements requis dont les échéances ont lieu pendant une période spécifiée. Quand un déploiement de mises à jour logicielles requis atteint une échéance, le client lance l’installation des mises à jour logicielles du déploiement. Ce paramètre détermine s’il faut installer des mises à jour logicielles d’autres déploiements requis dont l’échéance tombe dans le délai spécifié.  

     Utilisez-le pour accélérer l’installation des mises à jour logicielles requises. Ce paramètre peut aussi accroître la sécurité du client, diminuer les notifications de l’utilisateur final et diminuer le nombre de redémarrages du client. Par défaut, ce paramètre a la valeur **Non** et n’est donc pas activé.  

-   **Durée pendant laquelle tous les déploiements en attente avec une échéance dans cette période seront également installés**  </br>
     Utilisez ce paramètre pour spécifier le laps de temps pour le paramètre précédent. Vous pouvez entrer une valeur comprise entre 1 et 23 heures et entre 1 et 365 jours. Par défaut, ce paramètre est configuré pour sept jours.  

-   **Activer l’installation des fichiers d’installation rapide sur les clients** </br>
    Configurez ce paramètre sur **Oui** pour permettre aux clients d’utiliser des fichiers d’installation rapide. Pour plus d’informations, consultez [Gérer les fichiers d’installation rapide pour les mises à jour de Windows 10](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

    -   **Port utilisé pour télécharger du contenu pour les fichiers d’installation rapide** </br>
        Ce paramètre configure le port local permettant à l’écouteur HTTP de télécharger le contenu express. Par défaut, il s’agit du port 8005. Vous n’avez pas besoin d’ouvrir ce port dans le pare-feu du client.

-   **Activer la gestion de l’agent Office 365 Client** </br>
    Utilisez ce paramètre pour activer la gestion de l’agent Office 365 Client. Quand vous choisissez **Oui**, vous pouvez configurer les paramètres d’installation d’Office 365, télécharger des fichiers à partir de réseaux de distribution de contenu (CDN) Office et déployer les fichiers en tant qu’application dans Configuration Manager. Pour plus d’informations, consultez [Gérer Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).



## <a name="state-messaging"></a>Messagerie d’état

-   **Cycle de diffusion des messages d’état (en minutes)**  </br>
     Spécifie la fréquence à laquelle les clients signalent les messages d’état. La valeur par défaut est de 15 minutes.



##  <a name="user-and-device-affinity"></a>Affinité entre utilisateur et appareil  

-   **Seuil d'utilisation de l'affinité entre utilisateur et appareil (minutes)**  </br>
     Spécifiez le nombre de minutes avant que Configuration Manager ne crée un mappage d’affinité entre utilisateur et appareil.  La valeur par défaut est de 2880 minutes (deux jours).

-   **Seuil d'utilisation de l'affinité entre utilisateur et appareil (jour)**  </br>
     Spécifiez le nombre de jours durant lesquels le client mesure le seuil de l’affinité d’appareil basée sur l’utilisation.  Par défaut, cette valeur est de 30 jours.

    > [!NOTE]  
    >  Par exemple, si vous réglez **Seuil d’utilisation de l’affinité entre utilisateur et périphérique (minutes)** sur **60** minutes et **Seuil d’utilisation de l’affinité entre utilisateur et périphérique (jours)** sur **5** jours, l’utilisateur doit utiliser l’appareil pendant 60 minutes sur une période de cinq jours pour créer une affinité automatique avec l’appareil.  

-   **Configurer automatiquement l'affinité entre utilisateur et appareil à partir des données d'utilisation**  </br>
     Choisissez **Oui** pour créer une affinité automatique entre appareil et utilisateur en fonction des informations d’utilisation recueillies par Configuration Manager.  

-   **Autoriser les utilisateurs à définir leurs appareils principaux** </br>
    Quand ce paramètre est **Oui**, les utilisateurs peuvent identifier leurs propres appareils principaux dans le Centre logiciel.



## <a name="windows-analytics"></a>Windows Analytics

Pour plus d’informations sur ces paramètres, consultez [Configurer les clients pour envoyer des données à Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).
    
