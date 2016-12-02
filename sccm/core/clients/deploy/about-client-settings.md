---
title: "Paramètres client | System Center Configuration Manager"
description: "Sélectionnez les paramètres client à l’aide de la console d’administration de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: 15
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: cbe052891c55dd0c0d58c6e65d783314b0ec8ce9

---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>À propos des paramètres client dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Tous les paramètres client dans System Center Configuration Manager se gèrent dans la console Configuration Manager à partir du nœud **Paramètres client** de l’espace de travail **Administration**. Un ensemble de paramètres par défaut est fourni avec Configuration Manager. Lorsque vous modifiez les paramètres client par défaut, ces paramètres sont appliqués à tous les clients de la hiérarchie. Vous pouvez également configurer des paramètres client personnalisés, qui remplacent les paramètres client par défaut lorsque vous les affectez à des regroupements. Pour plus d'informations sur la configuration des paramètres client, voir [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

 La plupart des paramètres client sont explicites. Consultez les sections suivantes pour obtenir des informations supplémentaires sur les paramètres client qui pourraient nécessiter des informations avant d'être configurés.  

##  <a name="a-namebkmkbitsa-background-intelligent-transfer"></a><a name="BKMK_BITS"></a> Transfert intelligent en arrière-plan  

-   **Limiter la bande passante réseau maximale pour les transferts BITS en arrière-plan**  

     Si cette option est configurée sur **Vrai** ou **Oui**, la limitation de bande passante BITS est utilisée par les clients Configuration Manager.  

-   **Heure de début de la fenêtre de limitation**  

     Spécifiez l'heure de début en heure locale de la fenêtre de limitation BITS.  

-   **Heure de fin de la fenêtre de limitation**  

     Spécifiez l'heure de fin en heure locale de la fenêtre de limitation BITS. Si cette valeur est identique à la valeur **Heure de début de la fenêtre de limitation**, la limitation BITS est toujours activée.  

-   **Taux de transfert maximal dans la fenêtre de limitation (Kbit/s)**  

     Spécifiez le taux de transfert maximal en Kbits/s qui peut être utilisé par les clients Configuration Manager au cours de la fenêtre de limitation BITS spécifiée.  

-   **Autoriser les téléchargements BITS en dehors de la fenêtre de limitation**  

     Sélectionnez cette option pour autoriser les téléchargements BITS en dehors de la fenêtre de limitation. Cette option permet aux clients Configuration Manager d’utiliser des paramètres BITS distincts en dehors de la fenêtre spécifiée.  

-   **Taux de transfert maximal en dehors de la fenêtre de limitation (Kbit/s)**  

     Spécifiez le taux de transfert maximal en Kbits/s qui est utilisé par les clients Configuration Manager en dehors de la fenêtre de limitation BITS spécifiée. Cette option peut être configurée uniquement lorsque vous avez choisi d'autoriser la limitation BITS en dehors de la fenêtre spécifiée.  

##  <a name="a-namebkmkclientpolicydevicesettingsa-client-policy"></a><a name="BKMK_ClientPolicyDeviceSettings"></a> Stratégie du client  

-   **Intervalle d'interrogation de stratégie client (minutes)**  

     Spécifiez la fréquence à laquelle les clients Configuration Manager suivants téléchargent la stratégie client :  

    -   Ordinateurs Windows (par exemple, ordinateurs de bureau, serveurs, ordinateurs portables)  

    -   Appareils mobiles inscrits par Configuration Manager  

    -   Ordinateurs Mac  

    -   Ordinateurs qui exécutent Linux ou UNIX  

-   **Activer l'interrogation de la stratégie utilisateur sur les clients**  

     Si vous configurez ce paramètre sur **Vrai** ou **Oui**, et si Configuration Manager a découvert l’utilisateur, les clients Configuration Manager sur les ordinateurs reçoivent des applications et des programmes qui sont ciblés sur l’utilisateur connecté. Pour plus d’informations sur la découverte des utilisateurs, consultez [Découverte d’utilisateurs Active Directory dans Configuration Manager](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).  

     Étant donné que le catalogue d'applications reçoit la liste des logiciels disponibles pour les utilisateurs à partir du serveur de site, ce paramètre ne doit pas être configuré sur **Vrai** ou **Oui** pour que les utilisateurs voient et demandent des applications à partir du catalogue d'applications. Toutefois, si ce paramètre est défini sur **Faux** ou **Non**, ce qui suit ne fonctionne pas lorsque les utilisateurs utilisent le catalogue d'applications.  

    -   Les utilisateurs ne peuvent pas installer les applications qu’ils voient dans le catalogue des applications.  

    -   Les utilisateurs ne verront pas les notifications concernant leurs demandes d'approbation d'application. Au lieu de cela, ils doivent actualiser le catalogue d'applications et vérifier l'état d'approbation.  

    -   Les utilisateurs ne recevront pas de révisions et de mises à jour pour les applications qui sont publiées dans le catalogue d'applications. Toutefois, ils verront les modifications apportées aux informations de l'application dans le catalogue d'applications.  

    -   Si vous supprimez le déploiement d'une application après que le client a installé l'application en question à partir du catalogue d'applications, les clients continuent à vérifier que l'application est installée pendant une durée qui peut atteindre 2 jours.  

     En outre, lorsque ce paramètre est défini sur **Faux** ou **Non**, les utilisateurs ne recevront pas les applications requises que vous déployez sur les utilisateurs ou toute autre opération de gestion contenue dans les stratégies utilisateur.  

     Ce paramètre s'applique aux utilisateurs lorsque leur ordinateur se trouve sur l'Intranet et Internet ; il doit être configuré sur **Vrai** ou **Oui** si vous souhaitez également activer les stratégies utilisateur sur Internet.  

-   **Autoriser les demandes de stratégie utilisateur depuis des clients Internet**  

     Lorsque le client et le site sont configurés pour la gestion de client basée sur Internet et si vous configurez cette option sur **Vrai** ou **Oui** alors que les conditions suivantes s'appliquent, les utilisateurs reçoivent une stratégie utilisateur lorsque leur ordinateur se trouve sur Internet :  

    -   Le paramètre client **Activer la stratégie utilisateur sur les clients** a la valeur **Vrai** ou **Activer la stratégie utilisateur sur les clients** est configuré sur **Oui**.  

    -   Le point de gestion basé sur Internet authentifie correctement l'utilisateur à l'aide de l'authentification Windows (Kerberos ou NTLM).  

     Si vous laissez cette option configurée sur la valeur **Faux** ou **Non**, ou si l'une des conditions échoue, un ordinateur sur Internet recevra uniquement les stratégies ordinateur. Dans ce cas, les utilisateurs peuvent toujours voir, demander et installer des applications à partir d'un catalogue d'applications basé sur Internet. Si ce paramètre est configuré sur **Faux** ou **Non** mais que **Activer la stratégie utilisateur sur les clients** est configuré sur **Vrai** ou que **Activer la stratégie utilisateur sur les clients** est configuré sur **Oui**, les utilisateurs ne reçoivent pas les stratégies utilisateur tant que l'ordinateur n'est pas connecté à l'intranet.  

     Pour plus d’informations sur la gestion des clients sur Internet, consultez [Éléments à prendre en considération pour les communications de clients à partir d’Internet ou d’une forêt non approuvée](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) dans [Communications entre points de terminaison dans System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

    > [!NOTE]  
    >  Les demandes d'approbation d'application des utilisateurs ne requièrent pas de stratégies utilisateur ou l'authentification utilisateur.  

##  <a name="a-namebkmkcompliancea-compliance-settings"></a><a name="BKMK_Compliance"></a> Compliance Settings  

-   **Planifier l'évaluation de compatibilité**  

     Cliquez sur **Calendrier** pour créer le calendrier par défaut proposé aux utilisateurs lorsqu'ils déploient une ligne de base de configuration. Cette valeur peut être configurée pour chaque ligne de base dans la boîte de dialogue **Déployer la ligne de base de la configuration** .  

-   **Activer les données et profils utilisateurs**  

     Sélectionnez **Oui** si vous souhaitez déployer des éléments de configuration de profils et données utilisateurs sur les ordinateurs Windows 8 dans votre hiérarchie.  

     Pour plus d’informations sur les données et profils utilisateur, consultez [Guide pratique pour créer des éléments de configuration de données et profils utilisateur dans System Center Configuration Manager](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md).  

##  <a name="a-namebkmkcomputeragentdevicesettingsa-computer-agent"></a><a name="BKMK_ComputerAgentDeviceSettings"></a> Agent ordinateur  

-   **Point de site Web du catalogue d'applications par défaut**  

     Configuration Manager utilise ce paramètre pour connecter les utilisateurs au catalogue d’applications du Centre logiciel. Vous pouvez spécifier un serveur qui héberge le point de site Web du catalogue d'applications par son nom NetBIOS ou son nom de domaine complet, spécifier la détection automatique ou spécifier une URL pour les déploiements personnalisés. Dans la plupart des cas, la détection automatique est le meilleur choix car elle offre les avantages suivants :  

    -   les clients reçoivent automatiquement un point de site Web du catalogue d'applications à partir de leur site, si leur site contient un point de site Web du catalogue d'applications ;  

    -   la protection contre un serveur non autorisé car les points de site Web du catalogue d'applications sur l'Intranet qui sont configurés pour HTTPS sont préférés aux points de site Web du catalogue d'applications qui ne sont pas configurés pour HTTPS ;  

    -   lorsque les clients sont configurés pour la gestion des clients basés sur l'Intranet et Internet, ils reçoivent un point de site Web du catalogue d'applications basé sur Internet lorsqu'ils se trouvent sur Internet et un point de site Web du catalogue d'applications basé sur l'Intranet lorsqu'ils se trouvent sur l'Intranet.  

     La détection automatique ne garantit pas que les clients recevront un point de site Web du catalogue d'applications qui est le plus proche d'eux. Vous pouvez décider de ne pas utiliser **Détecter automatiquement** pour les raisons suivantes :  

    -   vous voulez configurer manuellement le serveur le plus proche pour les clients ou vous assurer qu'ils ne connectent pas à un serveur via une connexion réseau lente ;  

    -   vous souhaitez contrôler quels clients se connectent à quel serveur, pour des raisons professionnelles ou de performances ou à des fins de tests ;  

    -   vous ne souhaitez pas patienter jusqu'à 25 heures ou attendre une modification du réseau pour que les clients soient configurés avec un autre point de site Web du catalogue d'applications.  

     Si vous spécifiez le point de site Web du catalogue d'applications au lieu d'utiliser la détection automatique, spécifiez le nom NetBIOS plutôt que le nom de domaine complet Intranet pour éviter que les informations d'identification soient demandées aux utilisateurs lorsqu'ils se connectent au catalogue d'applications sur l'Intranet. Pour utiliser le nom NetBIOS, les conditions suivantes doivent s'appliquer :  

    -   Le nom NetBIOS est spécifié dans les propriétés du point du site Web du catalogue d'applications.  

    -   Vous utilisez WINS ou tous les clients sont dans le même domaine que le point de site Web du catalogue d'applications.  

    -   Le point de site Web du catalogue d'applications est configuré pour les connexions client HTTP ou il est configuré pour les connexions client HTTPS et le certificat du serveur web contient le nom NetBIOS.  

     En règle générale, les utilisateurs sont invités à saisir leurs informations d'identification lorsque l'URL contient un nom de domaine complet mais pas lorsque l'URL est un nom NetBIOS. Les utilisateurs doivent s'attendre à être toujours invités à saisir leurs informations d'identification lorsqu'ils se connectent à partir d'Internet, car cette connexion doit utiliser le nom de domaine complet Internet. Si les utilisateurs sont invités à saisir leurs informations d'identification lorsqu'ils sont connectés à Internet, assurez-vous que le serveur qui exécute le point de site Web du catalogue d'applications puisse se connecter à un contrôleur de domaine pour le compte de l'utilisateur, de sorte que l'utilisateur puisse être authentifié à l'aide de Kerberos.  

    > [!NOTE]  
    >  Fonctionnement de la détection automatique :  
    >   
    >  le client effectue une demande d'emplacement de service à un point de gestion. S'il existe un point de site Web du catalogue d'applications dans le même site que le client, ce serveur est donné au client en tant que le serveur du catalogue d'applications à utiliser. Lorsqu'il existe plusieurs points de site Web du catalogue d'applications disponibles dans le site, un serveur HTTPS est prioritaire sur un serveur qui n'est pas activé pour le protocole HTTPS. Après ce filtrage, tous les clients reçoivent l’un des serveurs à utiliser comme catalogue d’applications ; Configuration Manager n’équilibre pas la charge entre plusieurs serveurs. Lorsque le site du client ne contient pas de point de site Web du catalogue d'applications, le point de gestion renvoie de manière non déterministique un point de site Web du catalogue d'applications à partir de la hiérarchie.  
    >   
    >  Lorsque le client se trouve sur l'Intranet, si le point de site Web du catalogue d'applications sélectionné est configuré avec un nom NetBIOS pour l'URL du catalogue d'applications, les clients reçoivent ce nom NetBIOS plutôt que le nom de domaine complet Intranet. Lorsque le client est détecté sur Internet, seul le nom de domaine complet Internet est donné au client.  
    >   
    >  Le client effectue cette demande d'emplacement de service toutes les 25 heures ou chaque fois qu'il détecte un changement de réseau. Par exemple, si le client passe de l'Intranet à Internet et si le client peut localiser un point de gestion basé sur Internet, le point de gestion basé sur Internet fournit aux clients des serveurs de points de site Web du catalogue d'applications basé sur Internet.  

-   **Ajoute un site Web du catalogue d'applications par défaut à la zone des sites de confiance d'Internet Explorer**  

     Si cette option est configurée sur **Vrai** ou **Oui**, l'URL actuelle du site Web du catalogue d'applications par défaut est automatiquement ajoutée à la zone des sites approuvés dans Internet Explorer sur les clients.  

     Ce paramètre garantit que le paramètre Internet Explorer en mode protégé n'est pas activé. Si le mode protégé est activé, le client Configuration Manager peut ne pas être en mesure d’installer des applications à partir du catalogue d’applications. Par défaut, la zone des sites de confiance prend également en charge l'ouverture de session utilisateur pour le catalogue d'applications, ce qui requiert l'authentification Windows.  

     Si vous laissez cette option définie sur **Faux**, les clients Configuration Manager peuvent ne pas être en mesure d’installer des applications à partir du catalogue d’applications, sauf si ces paramètres Internet Explorer sont configurés dans une autre zone pour l’URL du catalogue d’applications que les clients utilisent.  

    > [!NOTE]  
    >  Chaque fois que Configuration Manager ajoute un catalogue d’applications par défaut à la zone de sites de confiance, une ancienne URL du catalogue d’applications par défaut ajoutée avant l’ajout de cette nouvelle entrée est supprimée.  
    >   
    >  Configuration Manager ne peut pas ajouter l’URL si elle est déjà spécifiée dans l’une des zones de sécurité. Dans ce cas, vous devez supprimer l'URL de l'autre zone ou configurer manuellement les paramètres Internet Explorer requis.  

-   **Autoriser les applications Silverlight à s'exécuter en mode de confiance élevé**  

     Ce paramètre doit avoir la valeur **Oui** si les utilisateurs exécutent le client Configuration Manager et utilisent le catalogue d’applications.  

     Si vous modifiez ce paramètre, il prend effet au prochain chargement du navigateur par les utilisateurs ou lorsqu'ils actualisent la fenêtre du navigateur actuellement ouverte.  

     Pour plus d’informations sur ce paramètre, consultez [Certificats pour Microsoft Silverlight 5 et mode de confiance élevée requis pour le catalogue d’applications](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5) dans [Sécurité et confidentialité pour la gestion des applications dans System Center Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

-   **Nom d'organisation affiché dans le Centre logiciel**  

     Tapez le nom que les utilisateurs voient dans le Centre logiciel. Ces informations personnalisées aident les utilisateurs à identifier cette application comme une source approuvée.  

-   **Utiliser le nouveau Centre logiciel**  

     Si ce paramètre est activé, tous les ordinateurs clients ciblés par ces paramètres client utiliseront le nouveau Centre logiciel qui affiche les applications accessibles à l’utilisateur qui étaient précédemment accessibles uniquement dans le catalogue des applications Silverlight.  

     Toutefois, les rôles de système de site Point du site web du catalogue des applications et Point de service web du catalogue des applications sont toujours requis pour que les applications accessibles à l’utilisateur apparaissent dans le Centre logiciel .  

     Pour plus d’informations, consultez [Planifier et configurer la gestion des applications dans System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   **Autorisations d'installation**  

    > [!WARNING]  
    >  Ce paramètre s'applique au catalogue des applications et au Centre logiciel. Ce paramètre n'a aucun effet lorsque les utilisateurs utilisent le portail d'entreprise.  

     Configurez la manière dont les utilisateurs peuvent lancer l'installation des logiciels, des mises à jour logicielles et des séquences de tâches :  

    -   **Tous les utilisateurs**: les utilisateurs connectés à un ordinateur client avec toutes les autorisations à l’exception de l’autorisation Invité peuvent lancer l’installation des logiciels, mises à jour logicielles et séquences de tâches.  

    -   **Administrateurs uniquement**: les utilisateurs connectés à un ordinateur client doivent être membres du groupe Administrateurs local pour lancer l’installation des logiciels, mises à jour logicielles et séquences de tâches.  

    -   **Administrateurs et utilisateurs principaux uniquement**: les utilisateurs connectés à un ordinateur client doivent être membres du groupe Administrateurs local ou être des utilisateurs principaux de l’ordinateur pour lancer l’installation des logiciels, mises à jour logicielles et séquences de tâches.  

    -   **Aucun utilisateur**: aucun utilisateur connecté à un ordinateur client ne peut lancer l’installation des logiciels, mises à jour logicielles et séquences de tâches. Les déploiements requis pour l'ordinateur sont toujours installés à la date d'échéance et les utilisateurs ne peuvent pas lancer l'installation des logiciels à partir du catalogue d'applications ou du Centre logiciel.  

-   **Interrompre l'entrée du code confidentiel BitLocker au redémarrage**  

     Si l'entrée du code confidentiel BitLocker est configurée sur les ordinateurs, cette option peut contourner la nécessité d'entrer un code confidentiel lorsque l'ordinateur redémarre après l'installation d'un logiciel.  

    -   **Toujours** : Configuration Manager suspend temporairement l’obligation de BitLocker d’entrer un code confidentiel au prochain démarrage de l’ordinateur après l’installation d’un logiciel nécessitant un redémarrage de l’ordinateur. Ce paramètre s’applique uniquement aux redémarrages d’ordinateur lancés par Configuration Manager et il ne suspend pas l’obligation de saisir le code confidentiel BitLocker lorsque l’utilisateur redémarre l’ordinateur. L'obligation de saisir un code confidentiel BitLocker reprend après le démarrage de Windows.  

    -   **Jamais** : Configuration Manager ne suspend pas l’obligation de BitLocker de saisir un code confidentiel au prochain démarrage de l’ordinateur après avoir installé un logiciel qui nécessite un redémarrage. Dans ce cas, l'installation du logiciel ne peut être finalisée que lorsque l'utilisateur entre le code confidentiel pour terminer le processus de démarrage standard et charger Windows.  

-   **D’autres logiciels gèrent le déploiement d’applications et de mises à jour logicielles**  

     Activez cette option uniquement si l'une des conditions suivantes s'applique :  

    -   Vous utilisez une solution de fabricant qui nécessite l'activation de ce paramètre.  

    -   Vous utilisez le kit de développement logiciel (SDK) Configuration Manager pour gérer les notifications d’agent client et l’installation d’applications et de mises à jour logicielles.  

    > [!WARNING]  
    >  Si vous sélectionnez cette option lorsque aucune de ces conditions ne s'applique, les mises à jour logicielles et les applications requises ne seront pas installées sur les clients. Ce paramètre n'empêche pas les utilisateurs d'installer des applications à partir du catalogue d'applications ou empêche l'installation des packages, programmes et séquences de tâches sur les ordinateurs clients.  

-   **Stratégie d'exécution de PowerShell**  

     Configurez la façon dont les clients Configuration Manager peuvent exécuter des scripts Windows PowerShell. Ces scripts sont souvent utilisés pour la détection dans les éléments de configuration de paramètres de conformité, mais ils peuvent également être envoyés dans un déploiement sous la forme d'un script standard.  

    -   **Ignorer** : le client Configuration Manager ignore la configuration Windows PowerShell sur l’ordinateur client afin que les scripts non signés puissent s’exécuter.  

    -   **Restreint** : le client Configuration Manager utilise la configuration Windows PowerShell actuelle sur l’ordinateur client, qui détermine si les scripts non signés peuvent s’exécuter.  

    -   **Toutes signées** : le client Configuration Manager exécute les scripts uniquement s’ils sont signés par un éditeur approuvé. Cette restriction s'applique indépendamment de la configuration Windows PowerShell actuelle sur l'ordinateur client.  

     Cette option requiert au minimum la version 2.0 de Windows PowerShell et la valeur par défaut est **Toutes signées**.  

    > [!TIP]  
    >  Si les scripts non signés ne parviennent pas à s’exécuter en raison de ce paramètre client, Configuration Manager signale cette erreur ainsi :  
    >   
    >  -   ID de l’erreur **0X87D00327** et description **Le script n’est pas signé** en tant qu’erreur d’état de déploiement dans l’espace de travail **Surveillance** de la console Configuration Manager.  
    > -   Codes d'erreur et descriptions **0X87D00327** et **Le script n'est pas signé** ou **0X87D00320** et **L'environnement d'exécution de scripts n'a pas encore été installé** avec le type d'erreur **Erreur de découverte** dans les rapports, notamment **Détails des erreurs des éléments de configuration dans la ligne de base de configuration d'un composant**.  
    > -   Message **Script is not signed (Error: 87D00327; Source: CCM)** dans le fichier **DcmWmiProvider.log** .  

-   **Désactiver la randomisation des échéances**  

     Ce paramètre détermine si le client utilise un délai d'activation pouvant aller jusqu'à deux heures pour installer les mises à jour logicielles nécessaires lorsque la date limite est atteinte. Par défaut, le délai d'activation est désactivé.  

     Pour les scénarios d’infrastructure VDI (Virtual Desktop Infrastructure), ce délai peut permettre de distribuer le traitement par le processeur et le transfert de données pour un ordinateur doté de plusieurs ordinateurs virtuels qui exécutent le client Configuration Manager. Même si vous n'utilisez pas d'infrastructure VDI, si de nombreux clients installent les même mises à jour en même temps, cela peut augmenter l'utilisation du processeur de manière négative sur le serveur de site, ralentir les points de distribution et réduire considérablement la bande passante réseau disponible.  

     Si les mises à jour logicielles nécessaires doivent être installées sans délai lorsque la date limite configurée est atteinte, sélectionnez **Oui** pour ce paramètre.  

##  <a name="a-namebkmkcomputerrestartdevicesettingsa-computer-restart"></a><a name="BKMK_ComputerRestartDeviceSettings"></a> Redémarrage de l'ordinateur  
 Lorsque vous spécifiez ces paramètres de redémarrage de l'ordinateur, assurez-vous que la valeur de l'intervalle de notification temporaire du redémarrage et la valeur de l'intervalle du compte à rebours final sont plus courtes que la fenêtre de maintenance la plus courte appliquée à l'ordinateur.  

 Pour plus d’informations sur les fenêtres de maintenance, consultez [Comment utiliser les fenêtres de maintenance dans System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

##  <a name="a-namebkmkendpointprotectiondevicesettingsa-endpoint-protection"></a><a name="BKMK_EndpointProtectionDeviceSettings"></a> Endpoint Protection  

-   **Gérer le client Endpoint Protection sur les ordinateurs clients**  

     Sélectionnez **Vrai** ou **Oui** si vous souhaitez gérer les clients Endpoint Protection existants sur des ordinateurs de la hiérarchie.  

     Sélectionnez cette option si vous avez déjà installé le client Endpoint Protection et que vous souhaitez le gérer avec Configuration Manager.  

     De plus, sélectionnez cette option si vous voulez créer un script de désinstallation d’une solution anti-programme malveillant existante, installer le client Endpoint Protection et déployer ce script en utilisant une application ou un package et un programme Configuration Manager.  

-   **Installer le client Endpoint Protection sur les ordinateurs clients**  

     Sélectionnez **Vrai** ou **Oui** pour installer et activer le client Endpoint Protection sur les ordinateurs clients où il n’est pas déjà installé.  

    > [!NOTE]  
    >  Si le client Endpoint Protection est déjà installé, la sélection de la valeur **Faux** ou **Non** ne désinstalle pas le client Endpoint Protection. Pour désinstaller le client Endpoint Protection, définissez le paramètre client **Gérer le client Endpoint Protection sur les ordinateurs clients** sur **Faux** ou **Non**, puis déployez un package et un programme pour désinstaller le client Endpoint Protection.  

-   **Pour les appareils Windows Embedded munis de filtres d'écriture, valider l'installation du client Endpoint Protection (nécessite un redémarrage)**  

     Sélectionnez **Oui** pour désactiver le filtre d'écriture sur l'appareil Windows Embedded et le redémarrer. Cela valide l'installation sur l'appareil.  

     Si vous spécifiez **Non** , le client est installé sur un segment de recouvrement temporaire qui est effacé lorsque l'appareil est redémarré. Dans ce scénario, le client Endpoint Protection n'est pas validé jusqu'à ce qu'une autre installation valide les modifications apportées à l'appareil. Il s'agit du paramètre par défaut.  

-   **Supprimer tout redémarrage de l’ordinateur requis après l’installation du client Endpoint Protection**  

     Sélectionnez **Vrai** ou **Oui** pour supprimer le redémarrage de l’ordinateur s’il est requis après l’installation du client Endpoint Protection.  

    > [!IMPORTANT]  
    >  Si le client Endpoint Protection nécessite un redémarrage de l'ordinateur et que ce paramètre a la valeur **Faux**, le redémarrage a lieu sans tenir compte des fenêtres de maintenance que vous avez configurées.  

-   **Durée pendant laquelle les utilisateurs sont autorisés à différer un redémarrage nécessaire pour terminer l’installation de Endpoint Protection (heures)**  

     Spécifiez le nombre d’heures de report du démarrage de l’ordinateur par les utilisateurs si cela est requis après l’installation du client Endpoint Protection. Cette option peut être configurée uniquement si l’option **Supprimer tout redémarrage d’ordinateur requis après l’installation du client Endpoint Protection** a la valeur **Faux**.  

-   **Désactiver les autres sources (telles que Microsoft Windows Update, Microsoft Windows Server Update Services ou les partages UNC) pour la mise à jour initiale des définitions sur les ordinateurs clients**  

     Sélectionnez **Vrai** ou **Oui** si vous voulez que Configuration Manager installe uniquement la mise à jour de définition initiale sur les ordinateurs clients. Ce paramètre peut s'avérer pratique pour éviter les connexions réseau inutiles et réduire la bande passante réseau pendant l'installation initiale de la mise à jour de définition.  

##  <a name="a-namebkmkhardwareinventorydevicesettingsa-hardware-inventory"></a><a name="BKMK_HardwareInventoryDeviceSettings"></a> Inventaire matériel  

-   **Taille maximale du fichier MIF personnalisé (Ko)**  

     Spécifiez la taille maximale, en kilo-octets (Ko), autorisée pour chaque fichier Management Information Format (MIF) personnalisé qui sera collecté sur un client lors d'un cycle d'inventaire matériel. Si tous les fichiers MIF dépassent cette taille, ils ne seront pas traités par l’inventaire matériel de Configuration Manager. Vous pouvez spécifier une taille comprise entre 1 et 5 000 Ko. Par défaut, cette valeur est définie à 250 Ko. Ce paramètre n'affecte pas la taille du fichier de données d'inventaire matériel ordinaire.  

    > [!NOTE]  
    >  Ce paramètre est disponible uniquement dans les paramètres client par défaut.  

-   **Classes d'inventaire matériel**  

     Dans Configuration Manager, vous pouvez étendre les informations matérielles que vous recueillez auprès de clients sans modifier manuellement le fichier sms_def.mof. Cliquez sur **Définir des classes** pour étendre l’inventaire matériel de Configuration Manager. Pour plus d’informations, consultez [Guide pratique pour configurer l’inventaire matériel dans System Center Configuration Manager](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

-   **Collecter des fichiers MIF**  

     Utilisez ce paramètre pour spécifier si vous souhaitez collecter des fichiers MIF (Managed Information Format) à partir de clients Configuration Manager pendant l’inventaire matériel.  

     Pour qu'un fichier MIF soit collecté par un inventaire matériel, il doit se trouver à l'emplacement approprié sur l'ordinateur client. Par défaut, l'emplacement des fichiers doit respecter les conditions suivantes :  

    -   Les fichiers IDMIF doivent se trouver dans le dossier Windows\System32\CCM\Inventory\Idmif .  

    -   Les fichiers NOIDMIF doivent se trouver dans le dossier Windows\System32\CCM\Inventory\Noidmif .  

    > [!NOTE]  
    >  Ce paramètre est disponible uniquement dans les paramètres client par défaut.  

##  <a name="a-namebkmkmeteredinternetconnetionssettingsa-metered-internet-connections"></a><a name="BKMK_MeteredInternetConnetionsSettings"></a> Connexions Internet facturées à l'usage  
 Vous pouvez gérer la manière dont les ordinateurs clients Windows 8 communiquent avec les sites Configuration Manager quand ils utilisent des connexions Internet facturées à l’usage. Les fournisseurs Internet facturent parfois en fonction de la quantité de données que vous envoyez et recevez lorsque vous utilisez une connexion Internet facturée à l'usage.  

> [!NOTE]  
>  Le paramètre client configuré n'est pas appliqué aux ordinateurs clients Windows 8 dans les scénarios suivants :  
>   
>  -   L’ordinateur se trouve sur une connexion de données itinérante : le client Configuration Manager n’exécute aucune opération nécessitant le transfert de données vers des sites Configuration Manager.  
> -   Les propriétés de la connexion réseau Windows sont configurées pour une connexion non facturée à l’usage : le client Configuration Manager se comporte comme s’il existait une connexion Internet non facturée à l’usage et transfère donc les données vers les sites Configuration Manager.  

-   **Communication des clients sur des connexions Internet facturées à l’usage**  

     Dans la liste déroulante, choisissez une des valeurs suivantes pour les ordinateurs clients Windows 8 :  

    -   **Autoriser**: toutes les communications client sont autorisées via la connexion Internet facturée à l’usage, sauf si l’appareil client utilise une connexion de données itinérante.  

    -   **Limite**: seules les communications client suivantes sont autorisées via la connexion Internet facturée à l’usage :  

        -   Récupération de stratégie client  

        -   Messages d'état du client à envoyer au site  

        -   Demandes d'installation de logiciels à l'aide du catalogue des applications  

        -   Déploiements requis (lorsque la date limite d'installation est atteinte)  

        > [!IMPORTANT]  
        >  Si un utilisateur lance l'installation d'un logiciel à partir du Centre logiciel ou du catalogue des applications, celle-ci est toujours autorisée, quels que soient les paramètres de la connexion Internet facturée à l'usage.  

         Si la limite de transfert de données est atteinte pour la connexion Internet facturée à l’usage, le client ne tente plus de communiquer avec les sites Configuration Manager.  

    -   **Bloc** : le client Configuration Manager n’essaie pas de communiquer avec les sites Configuration Manager quand il est sur une connexion Internet limitée. Il s'agit de la valeur par défaut.  

##  <a name="a-namebkmkpowmgmtdevicesettingsa-power-management"></a><a name="BKMK_PowMgmtDeviceSettings"></a> Gestion de l'alimentation  

-   **Autoriser les utilisateurs à exclure leur appareil de la gestion de l'alimentation**  

     Dans la liste déroulante, sélectionnez **Vrai** ou **Oui** pour autoriser les utilisateurs du Centre logiciel à exclure leur ordinateur de tous les paramètres de gestion de l'alimentation configurés.  

-   **Autoriser le proxy de mise en éveil**  

     Spécifiez **Oui** pour compléter le paramètre d'éveil par appel réseau du site lorsqu'il est configuré pour les paquets monodiffusion.  

     Pour plus d’informations sur le proxy de mise en éveil, consultez [Planifier la sortie de veille des clients dans System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    > [!WARNING]  
    >  N'activez pas le proxy de mise en éveil dans un réseau de production sans d'abord comprendre comment il fonctionne et l'évaluer dans un environnement de test.  

-   **Numéro de port du proxy de mise en éveil (UDP)**  

     Conservez la valeur par défaut pour le numéro de port que les ordinateurs du gestionnaire utilisent pour envoyer des paquets de mise en éveil aux ordinateurs en veille, ou remplacez-la par la valeur de votre choix.  

     Le numéro de port indiqué ici est configuré automatiquement pour les clients qui exécutent le Pare-feu Windows lorsque vous configurez l'option **Exception du Pare-feu Windows pour le proxy de mise en éveil** . Si les clients exécutent un autre pare-feu, vous devez le configurer manuellement pour qu'il autorise le numéro de port UDP spécifié pour ce paramètre.  

-   **Numéro de port Wake On LAN (UDP)**  

     Conservez la valeur par défaut (9), sauf si vous avez modifié le numéro du port Wake On LAN (UDP) sous l'onglet **Ports**des **Propriétés** du site.  

    > [!IMPORTANT]  
    >  Ce numéro doit correspondre au numéro figurant dans les **Propriétés**du site. Si vous modifiez ce numéro en un seul emplacement, sachez qu'il n'est pas actualisé automatiquement à l'autre emplacement.  

##  <a name="a-namebkmkremotetoolsdevicesettingsa-remote-tools"></a><a name="BKMK_RemoteToolsDeviceSettings"></a> Outils de contrôle à distance  

-   **Activer le contrôle à distance sur des clients** et **Profils d'exception de pare-feu**  

     Indiquez si le contrôle à distance Configuration Manager est activé pour tous les ordinateurs clients qui reçoivent ces paramètres client. Cliquez sur **Configurer** pour activer le contrôle à distance et éventuellement configurer les paramètres du pare-feu afin d'autoriser le contrôle à distance pour travailler sur des ordinateurs clients.  

     Le contrôle à distance est désactivé par défaut.  

    > [!IMPORTANT]  
    >  Si les paramètres de pare-feu ne sont pas configurés, le contrôle à distance risque de ne pas fonctionner correctement.  

-   **Les utilisateurs peuvent modifier les paramètres de stratégie ou de notification dans le Centre logiciel**  

     Indiquez si les utilisateurs peuvent modifier les options de contrôle à distance à partir du Centre logiciel.  

-   **Autoriser le contrôle à distance d'un ordinateur autonome**  

     Indiquez si un administrateur peut utiliser le contrôle à distance pour accéder à un ordinateur client qui est déconnecté ou verrouillé. Seul un ordinateur connecté et déverrouillé peut être contrôlé à distance lorsque ce paramètre est désactivé.  

-   **Inviter l'utilisateur à autoriser le contrôle à distance**  

     Indiquez si l'ordinateur client affichera un message demandant l'autorisation de l'utilisateur avant d'autoriser une session de contrôle à distance.  

-   **Accorder l'autorisation de contrôle à distance au groupe Administrateurs local**  

     Indiquez si les administrateurs locaux sur le serveur qui lance la connexion de contrôle à distance peuvent établir des sessions de contrôle à distance vers des ordinateurs clients.  

-   **Niveau d'accès autorisé**  

     Spécifiez le niveau d'accès de contrôle à distance autorisé. Vous pouvez choisir :  

    -   Contrôle intégral  

    -   Afficher uniquement  

    -   aucune.  

-   **Observateurs autorisés**  

     Cliquez sur **Définir des observateurs** pour ouvrir la boîte de dialogue **Configurer le paramètre client** et spécifiez les noms des utilisateurs Windows qui peuvent établir des sessions de contrôle à distance vers des ordinateurs client.  

-   **Afficher l'icône de notification de session sur la barre des tâches**  

     Sélectionnez cette option pour afficher une icône sur la barre des tâches d'ordinateurs client pour indiquer qu'une session de contrôle à distance est active.  

-   **Afficher la barre de connexion de session**  

     Sélectionnez cette option pour afficher une barre de connexion de session de haute visibilité sur les ordinateurs client pour indiquer qu'une session de contrôle à distance est active.  

-   **Émettre un signal sonore sur le client**  

     Sélectionnez cette option afin d'utiliser le son pour indiquer qu'une session de contrôle à distance est active sur un ordinateur client. Vous pouvez émettre un son lorsque la session se connecte ou se déconnecte ou vous pouvez émettre un son à plusieurs reprises pendant la session.  

-   **Gérer les paramètres de l'Assistance à distance non sollicités**  

     Sélectionnez cette option pour autoriser Configuration Manager à gérer les sessions d’assistance à distance non sollicitées.  

     Les sessions d'assistance à distance non sollicitées correspondent aux cas où l'utilisateur de l'ordinateur client ne lance pas la session par le biais d'une demande d'assistance.  

-   **Gérer les paramètres de l'Assistance à distance sollicités**  

     Sélectionnez cette option pour autoriser Configuration Manager à gérer les sessions d’assistance à distance sollicitées.  

     Les sessions d'assistance à distance sollicitées sont utilisées dans un cas où l'utilisateur de l'ordinateur client transmet une requête à l'administrateur dans le but de bénéficier d'une assistance à distance.  

-   **Niveau d'accès de l'Assistance à distance**  

     Sélectionnez le niveau d’accès à attribuer aux sessions d’assistance à distance lancées à partir de la console Configuration Manager.  

    > [!NOTE]  
    >  L'utilisateur de l'ordinateur client doit toujours autoriser l'ouverture d'une session d'assistance à distance.  

-   **Gérer les paramètres du Bureau à distance**  

     Sélectionnez cette option pour autoriser Configuration Manager à gérer les sessions Bureau à distance des ordinateurs.  

-   **Autoriser la connexion des observateurs autorisés à l'aide d'une connexion Bureau à distance**  

     Sélectionnez cette option pour permettre aux utilisateurs spécifiés dans la liste des observateurs autorisés d'être ajoutés au groupe d'utilisateurs locaux Bureau à distance sur les ordinateurs clients.  

-   **Exiger l'authentification au niveau du réseau sur les ordinateurs exécutant le système d'exploitation Windows Vista et versions ultérieures**  

     Sélectionnez cette option plus sécurisée si vous souhaitez utiliser l'authentification au niveau du réseau pour établir des connexions Bureau à distance avec les ordinateurs clients qui exécutent Windows Vista ou une version ultérieure. L'authentification au niveau du réseau nécessite au départ moins de ressources d'ordinateur distant, car l'authentification des utilisateurs se termine avant l'établissement de la connexion Bureau à distance. Cette méthode est plus sûre, car elle contribue à protéger l'ordinateur des utilisateurs et logiciels malveillants, et réduit le risque d'attaque par déni de service.  

##  <a name="a-namebkmksoftwaredeploymentdevicesettingsa-software-deployment"></a><a name="BKMK_SoftwareDeploymentDeviceSettings"></a> Déploiement logiciel  

-   **Planifier la réévaluation des déploiements**  

     Configurez une planification pour la réévaluation des règles de spécifications par Configuration Manager pour tous les déploiements. La valeur par défaut est tous les 7 jours.  

    > [!IMPORTANT]  
    >  Nous recommandons de ne pas modifier cette valeur à une valeur inférieure à la valeur par défaut, car cela peut affecter négativement les performances de votre réseau et des ordinateurs clients.  

     Vous pouvez également lancer cette action à partir d’un ordinateur client Configuration Manager en sélectionnant l’action **Cycle d’évaluation du déploiement de l’application** sous l’onglet **Actions** de **Configuration Manager** dans le Panneau de configuration.  

##  <a name="a-namebkmksoftinventorydevicesettingsa-software-inventory"></a><a name="BKMK_SoftInventoryDeviceSettings"></a> Inventaire logiciel  

-   **Détails sur le rapport d'inventaire**  

     Spécifiez le niveau d'informations sur les fichiers à inventorier. Vous pouvez inventorier des informations sur un fichier uniquement, sur le produit associé au fichier ou toutes les informations sur le fichier.  

-   **Inventorier ces types de fichiers**  

     Si vous souhaitez spécifier les types de fichiers à inventorier, cliquez sur **Définir des types** , puis configurez les options suivantes dans la boîte de dialogue **Configurer le paramètre client** :  

    > [!NOTE]  
    >  Si plusieurs paramètres client personnalisés sont appliqués à un ordinateur, l'inventaire renvoyé par chaque paramètre est fusionné.  

    -   Cliquez sur l'icône Nouveau pour ajouter un nouveau type de fichier à l'inventaire, puis spécifiez les informations suivantes dans la boîte de dialogue **Propriétés du fichier inventorié**  

    -   **Nom** : définissez le nom du fichier à inventorier. Vous pouvez utiliser le caractère **\*** pour représenter une chaîne de texte et le caractère **?** pour représenter n'importe quel caractère. Par exemple, si vous souhaitez inventorier tous les fichiers portant l’extension .doc, spécifiez le nom de fichier **\*.doc**.  

    -   **Emplacement** : cliquez sur **Définir** pour ouvrir la boîte de dialogue **Propriétés du chemin d'accès** . Vous pouvez configurer l'inventaire logiciel pour rechercher le fichier défini sur tous les disques durs des clients, effectuer une recherche dans un chemin donné (tel que **C:\Folder**), rechercher une variable (telle que *%windir%*) et exécuter une recherche dans tous les sous-dossiers dans le chemin indiqué.  

    -   **Exclure les fichiers chiffrés et compressés** : lorsque vous sélectionnez cette option, tous les fichiers qui ont été compressés ou chiffrés ne sont pas inventoriés.  

    -   **Exclure les fichiers dans le répertoire Windows** : lorsque vous sélectionnez cette option, tous les fichiers dans le répertoire Windows et ses sous-répertoires ne seront pas inventoriés.  

    -   Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés du fichier inventorié** .  

    -   Ajoutez tous les fichiers à inventorier et cliquez sur **OK** pour fermer la boîte de dialogue **Configurer le paramètre client** .  

-   **Collecter des fichiers**  

     Si vous souhaitez collecter des fichiers stockés sur les ordinateurs clients, cliquez sur **Définir des fichiers** , puis configurez les options suivantes :  

    > [!NOTE]  
    >  Si plusieurs paramètres client personnalisés sont appliqués à un ordinateur, l'inventaire renvoyé par chaque paramètre est fusionné.  

    -   Dans la boîte de dialogue **Configurer le paramètre client** , cliquez sur l'icône Nouveau pour ajouter un fichier à collecter.  

    -   Dans la boîte de dialogue **Propriétés du fichier collecté** , fournissez les informations suivantes :  

    -   **Nom** : définissez le nom du fichier à collecter. Vous pouvez utiliser le caractère **\*** pour représenter une chaîne de texte et le caractère **?** pour représenter n'importe quel caractère.  

    -   **Emplacement** : cliquez sur **Définir** pour ouvrir la boîte de dialogue **Propriétés du chemin d'accès** . Vous pouvez configurer l'inventaire logiciel pour rechercher le fichier à collecter sur tous les disques durs des clients, effectuer une recherche dans un chemin donné (tel que **C:\Folder**), rechercher une variable (telle que *%windir%*) et exécuter une recherche dans tous les sous-dossiers dans le chemin indiqué.  

    -   **Exclure les fichiers chiffrés et compressés** : lorsque vous sélectionnez cette option, tous les fichiers qui ont été compressés ou chiffrés ne sont pas collectés.  

    -   **Arrêter le regroupement de fichiers lorsque la taille totale dépasse (Ko) :** définissez la taille de fichier (en Ko) au-delà de laquelle aucun autre des fichiers définis sous **Nom** ne sera collecté.  

        > [!NOTE]  
        >  Le serveur de site recueille les cinq dernières versions modifiées des fichiers collectés et les enregistre dans le répertoire *&lt;répertoire_installation_ConfigMgr\>***\Inboxes\Sinv.box\Filecol**. Si un fichier n'a pas été modifié depuis le dernier inventaire logiciel, il n'est pas recollecté.  
        >   
        >  Les fichiers de plus de 20 Mo ne sont pas collectés par l'inventaire logiciel.  
        >   
        >  La valeur **Taille maximale pour tous les fichiers regroupés (Ko) :** dans la boîte de dialogue **Configurer le paramètre client** indique la taille maximale de tous les fichiers regroupés. Lorsque cette taille est atteinte, la collecte de fichiers s'arrête. Tous les fichiers déjà regroupés sont conservés et envoyés au serveur de site.  

        > [!IMPORTANT]  
        >  Si vous configurez l'inventaire logiciel pour regrouper un grand nombre de fichiers volumineux, vous risquez d'affecter négativement les performances du serveur de site et du réseau.  

         Pour plus d’informations sur l’affichage des fichiers collectés, consultez [Guide pratique pour utiliser l’Explorateur de ressources pour afficher l’inventaire logiciel dans System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    -   Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés du fichier collecté** .  

    -   Ajoutez tous les fichiers à regrouper et cliquez sur **OK** pour fermer la boîte de dialogue **Configurer le paramètre client** .  

-   **Définir des noms**  

     Lors d'un inventaire logiciel, les noms des fabricants et des produits sont extraits des informations d'en-tête des fichiers installés sur les clients du site. Du fait que ces noms ne sont pas systématiquement normalisés dans les informations d'en-tête de fichier, lorsque vous affichez les informations de l'inventaire logiciel dans l'Explorateur de ressources ou exécutez des requêtes, différentes versions du même nom de fabricant ou de produit peuvent parfois apparaître. Si vous souhaitez normaliser ces noms d'affichage, cliquez sur **Définir des noms** et configurez les éléments suivants dans la boîte de dialogue **Configurer le paramètre client** .  

    -   **Type de nom :** l’inventaire logiciel recueille des informations sur les produits et les fabricants. Dans la liste déroulante, indiquez si vous souhaitez configurer des noms complets pour un **fabricant** ou un **produit**.  

    -   **Nom complet :** spécifie le nom complet que vous souhaitez utiliser à la place des noms dans la liste **Noms inventoriés** . Vous pouvez cliquer sur l'icône Nouveau pour spécifier un nouveau nom complet.  

    -   **Noms inventoriés :** cliquez sur l'icône Nouveau pour ajouter un nouveau nom inventorié qui sera remplacé dans l'inventaire logiciel par le nom sélectionné dans la liste **Nom complet** . Vous pouvez ajouter plusieurs noms qui seront remplacés.  

##  <a name="a-namebkmksoftwareupdatesdevicesettinga-software-updates"></a><a name="BKMK_SoftwareUpdatesDeviceSetting"></a> mises à jour logicielles  

-   **Activer les mises à jour logicielles sur les clients**  

     Utilisez ce paramètre pour activer les mises à jour logicielles sur les clients Configuration Manager. Si vous désactivez ce paramètre, Configuration Manager supprime les stratégies de déploiement existantes du client. Lorsque vous réactivez ce paramètre, le client télécharge la stratégie de déploiement actuelle.  

    > [!IMPORTANT]  
    >  Si vous désactivez ce paramètre, les stratégies NAP et les stratégies de paramètres de compatibilité qui s'appuient sur le paramètre d'appareil des mises à jour logicielles ne fonctionneront plus.  

-   **Calendrier d'analyse des mises à jour logicielles**  

     utilisez ce paramètre pour indiquer la fréquence d'exécution d'une analyse d'évaluation de la conformité des mises à jour logicielles par le client. L'analyse d'évaluation de la conformité détermine l'état des mises à jour logicielles sur le client (par exemple, requis ou installé). Pour plus d’informations sur l’évaluation de la conformité, consultez [Évaluation de la conformité des mises à jour logicielles](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

     Un calendrier simple est utilisé par défaut et l'analyse de la conformité démarre tous les 7 jours. Vous pouvez choisir de créer un calendrier personnalisé pour spécifier une date et une heure exactes de début, d'utiliser UTC ou l'heure locale et de configurer l'intervalle de récurrence d'un jour spécifique de la semaine.  

    > [!NOTE]  
    >  Si vous spécifiez un intervalle inférieur à une journée, Configuration Manager rétablit automatiquement la valeur par défaut (1 jour).  

    > [!WARNING]  
    >  L'heure de début réelle sur les ordinateurs clients est l'heure de début plus une durée aléatoire de deux heures maximum. Ceci évite que les ordinateurs clients lancent l'analyse et se connectent à Windows Server Update Services (WSUS) sur le serveur du point de mise à jour logicielle actif en même temps.  

-   **Planifier la réévaluation du déploiement**  

     Utilisez ce paramètre pour configurer la fréquence à laquelle l’agent client des mises à jour logicielles réévalue les mises à jour logicielles pour en déterminer l’état de l’installation sur les ordinateurs clients Configuration Manager. Si des mises à jour ayant été préalablement installées ne se trouvent plus sur les ordinateurs clients mais sont toujours requises, elles sont réinstallées. Le calendrier de réévaluation du déploiement doit être réglé conformément à la stratégie de l'entreprise en matière de conformité des mises à jour logicielles, que les utilisateurs aient la possibilité ou non de désinstaller des mises à jour logicielles, etc., et en tenant compte du fait que chaque cycle de réévaluation du déploiement entraîne une activité du réseau et des processeurs des ordinateurs clients. Un calendrier simple est utilisé par défaut et l'analyse de la réévaluation du déploiement démarre tous les 7 jours.  

    > [!NOTE]  
    >  Si vous spécifiez un intervalle inférieur à une journée, Configuration Manager rétablit automatiquement la valeur par défaut (1 jour).  

-   **Dès que l'échéance d'un déploiement de mise à jour logicielle est atteinte, installer tous les autres déploiements de mise à jour logicielle avec une échéance pendant une période de temps spécifiée**  

     Utilisez ce paramètre pour installer toutes les mises à jour logicielles dans les déploiements requis dont les échéances ont lieu pendant une période spécifiée. Lorsque l'échéance pour un déploiement de mises à jour logicielles obligatoire est atteinte, l'installation commence sur les clients pour les mises à jour logicielles du déploiement. Ce paramètre détermine si l'installation des mises à jour logicielles définies dans d'autres déploiements obligatoires dont l'échéance est configurée pour la même période doit également être lancée.  

     Utilisez ce paramètre pour accélérer l'installation des mises à jour logicielles pour les mises à jour logicielles requises, accroître potentiellement la sécurité, réduire potentiellement l'affichage des notifications et réduire potentiellement les redémarrages du système sur les ordinateurs clients. Par défaut, ce paramètre n'est pas activé.  

-   **Durée pendant laquelle tous les déploiements en attente avec une échéance dans cette période seront également installés**  

     Utilisez ce paramètre pour spécifier le laps de temps pour le paramètre précédent. Vous pouvez entrer une valeur comprise entre 1 et 23 heures et entre 1 et 365 jours. Par défaut, ce paramètre est configuré pour 7 jours.  

##  <a name="a-namebkmkuserdeviceaffinitydevicesettingsa-user-and-device-affinity"></a><a name="BKMK_UserDeviceAffinityDeviceSettings"></a> Affinité entre utilisateur et appareil  

-   **Seuil d'utilisation de l'affinité entre utilisateur et appareil (minutes)**  

     Spécifiez le nombre de minutes avant que Configuration Manager ne crée un mappage d’affinité entre utilisateur et appareil.  

-   **Seuil d'utilisation de l'affinité entre utilisateur et appareil (jour)**  

     Spécifiez une période (en jours) pendant laquelle le seuil de l'affinité basé sur l'utilisation est mesuré.  

    > [!NOTE]  
    >  Par exemple, si le **Seuil d'utilisation de l'affinité entre utilisateur et appareil (minutes)** est défini sur **60** minutes et que le **Seuil d'utilisation de l'affinité entre utilisateur et appareil (jours)** est défini sur **5** jours, l'utilisateur doit utiliser l'appareil pendant 60 minutes sur une période de 5 jours pour pouvoir créer automatiquement une affinité entre utilisateur et appareil.  

-   **Configurer automatiquement l'affinité entre utilisateur et appareil à partir des données d'utilisation**  

     Sélectionnez **Vrai** ou **Oui** pour permettre à Configuration Manager de créer automatiquement des affinités entre appareil et utilisateur à partir des données d’utilisation recueillies.  

## <a name="client-cache-settings"></a>Paramètres du cache du client

- **Configurer la taille du cache du client**

  Le dossier du cache du client permet de stocker les fichiers temporaires utilisés pour installer des applications et des programmes sur les ordinateurs Windows. À compter de la version 1606, sélectionnez **Oui** pour spécifier la taille du dossier du cache du client en utilisant les paramètres **Taille maximale du cache**. Si la valeur est **Non**, la taille du dossier du cache du client s’élève par défaut à 5 120 Mo.

  D’autres propriétés du cache du client peuvent être définies pendant l’installation du client. Pour plus d'informations, voir [Configure the Client Cache for Configuration Manager Clients](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

- **Taille maximale du cache (Mo)**

  À compter de la version 1606, spécifiez la taille maximale du dossier du cache du client en mégaoctets.

- **Taille maximale du cache (pourcentage du disque)** (à partir de la version 1606)

  À compter de la version 1606, spécifiez la taille maximale du dossier du cache du client en pourcentage de la taille du disque.

##  <a name="a-namebkmkmobiledevicesusersettingsa-mobile-devices"></a><a name="BKMK_MobileDevicesUserSettings"></a> Appareils mobiles  

-   **Profil d'inscription d'appareil mobile**  

     Afin de configurer ce paramètre, vous devez d'abord définir le paramètre **Autoriser les utilisateurs à inscrire des appareils mobiles** sur **Vrai**. Vous pouvez ensuite cliquer sur **Définir un profil** pour spécifier un profil d'inscription contenant des informations sur le modèle de certificat à utiliser lors du processus d'inscription, le site contenant un point d'inscription et un point proxy d'inscription, ainsi que le site qui sera chargé de gérer l'appareil après l'inscription.  

    > [!IMPORTANT]  
    >  Assurez-vous d'avoir configuré un modèle de certificat à utiliser pour l'inscription d'appareils mobiles avant de pouvoir configurer cette option.  

##  <a name="a-namebkmkenrollmentusersettingsa-enrollment"></a><a name="BKMK_EnrollmentUserSettings"></a> Inscription  

-   **Profil d'inscription d'appareil mobile**  

     Afin de configurer ce paramètre, vous devez définir le paramètre **Autoriser les utilisateurs à inscrire des appareils mobiles et des ordinateurs Mac** sur **Oui**. Vous pouvez ensuite cliquer sur **Définir un profil** pour spécifier un profil d'inscription contenant des informations sur le modèle de certificat à utiliser lors du processus d'inscription, le site contenant un point d'inscription et un point proxy d'inscription, ainsi que le site qui sera chargé de gérer l'appareil après l'inscription.  

    > [!IMPORTANT]  
    >  Avant de configurer cette option, vous devez voir configuré un modèle de certificat à utiliser pour l'inscription de l'appareil mobile ou du certificat de client Mac.  

##  <a name="a-namebkmkuserdeviceaffinityusersettingsa-user-and-device-affinity"></a><a name="BKMK_UserDeviceAffinityUserSettings"></a> Affinité entre utilisateur et appareil  

-   **Autoriser les utilisateurs à définir leurs appareils principaux**  

     Spécifiez si les utilisateurs sont autorisés à identifier leurs propres appareils principaux à partir du catalogue d'applications dans l'onglet **Mes appareils** .  



<!--HONumber=Nov16_HO1-->


