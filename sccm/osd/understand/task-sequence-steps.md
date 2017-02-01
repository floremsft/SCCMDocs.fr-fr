---
title: "Étapes de séquence de tâches - Configuration Manager | Microsoft Docs"
description: "Découvrez les différentes étapes de séquence de tâches que vous pouvez ajouter à une séquence de tâches Configuration Manager."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
caps.latest.revision: 26
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 89158debdf4c345a325feeb608db2215a88ed81b
ms.openlocfilehash: 94eeddd161448aff6e1c7afa542b0cbef1ad4d77


---
# <a name="task-sequence-steps-in-system-center-configuration-manager"></a>Étapes de séquence de tâches dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous trouverez ci-dessous les différentes étapes de séquence de tâches qui peuvent être ajoutées à une séquence de tâches Configuration Manager. Pour plus d’informations sur la modification d’une séquence de tâches, consultez [Modifier une séquence de tâches](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  


##  <a name="a-namebkmkapplydataimagea-apply-data-image-task-sequence-step"></a><a name="BKMK_ApplyDataImage"></a> Étape de séquence de tâches Appliquer l’image de données  
 L'étape de séquence de tâches **Appliquer l'image de données** permet de copier l'image de données sur la partition de destination indiquée.  

 Cette étape est exécutée uniquement sous Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches de cette action, consultez [Variables d’action de séquence de tâches](task-sequence-action-variables.md).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Package d’images**  
 Cliquez sur **Parcourir** pour préciser le **package d'images**que doit utiliser cette étape de la séquence de tâches. Sélectionnez le package à installer dans la boîte de dialogue **Sélectionner un package** . Les informations des propriétés associées à chaque package d'images s'affichent en bas de la boîte de dialogue **Sélectionner un package** . Utilisez la liste déroulante pour choisir l' **image** que vous souhaitez installer à partir du **package d'images**sélectionné.  

> [!NOTE]  
>  L'action de la séquence de tâches traite l'image en tant que fichier de données et n'effectue aucune configuration nécessaire pour le redémarrage de l'image en tant que système d'exploitation.  

 **Destination**  
 Spécifie une partition formatée et un disque dur existants, une lettre de lecteur logique précise ou le nom d'une variable de séquence de tâches contenant la lettre de lecteur logique.  

-   **Prochaine partition disponible** : utilisez la partition séquentielle suivante qui n’a pas été précédemment ciblée par une action Appliquer le système d’exploitation ou Appliquer l’image de données dans cette séquence de tâches.  

-   **Disque et partition spécifiques** : sélectionnez le numéro de **disque** (à partir de 0) et le numéro de **partition** (à partir de 1).  

-   **Lettre de lecteur logique spécifique** : spécifiez la **lettre de lecteur** attribuée à la partition par Windows PE. Remarque : cette lettre de lecteur peur être différente de la lettre de lecteur que le système d'exploitation récemment déployé attribuera.  

-   **Lettre de lecteur logique stockée dans une variable** : spécifiez la variable de séquence de tâches contenant la lettre de lecteur attribuée à la partition par Windows PE. Cette variable est généralement définie dans la section Avancé de la boîte de dialogue **Propriétés de la partition** pour l'action de séquence de tâches **Formater et partitionner le disque** .  

 **Supprimer l’intégralité du contenu de la partition avant d’appliquer l’image**  
 Précise que tous les fichiers de la partition cible seront supprimés avant l'installation de l'image. Si vous ne supprimez pas le contenu de la partition, cette étape peut être utilisée pour appliquer le contenu supplémentaire à une partition précédemment ciblée.  

##  <a name="a-namebkmkapplydriverpackagea-apply-driver-package"></a><a name="BKMK_ApplyDriverPackage"></a> Appliquer le package de pilotes  
 Utilisez l'étape de séquence de tâches **Appliquer le package de pilotes** pour télécharger tous les pilotes du package de pilotes et les installer sur le système d'exploitation Windows.

 L'étape de séquence de tâches **Appliquer le package de pilotes** rend disponibles tous les pilotes d'appareils d'un package de pilotes pour l'utilisation avec Windows. Vous pouvez ajouter cette étape à une séquence de tâches entre les étapes **Appliquer le système d'exploitation**  et **Configurer Windows et ConfigMgr** pour que les pilotes de périphérique du package de pilotes soient disponibles sous Windows. Généralement, l'étape **Appliquer le package de pilotes** est placée après l'étape de séquence de tâches **Appliquer automatiquement les pilotes** . L'étape de séquence de tâches **Appliquer le package de pilotes** est également utile avec des scénarios de déploiement de médias autonomes.  

 Assurez-vous que les pilotes de périphérique identiques sont placés dans un package de pilotes et distribuez-les aux points de distribution appropriés. Une fois qu’ils sont distribués, les ordinateurs client Configuration Manager peuvent les installer. Par exemple, vous pouvez placer tous les pilotes de périphérique d'un fabricant dans un package de pilotes, puis distribuer le package aux points de distribution à un emplacement où les ordinateurs associés peuvent y accéder.

 Cette étape est utile pour les médias autonomes et pour les administrateurs souhaitant installer un ensemble spécifique de pilotes, y compris des pilotes d'appareils qu'une analyse Plug-and-Play ne détecte pas (par exemple les imprimantes réseau).  

 Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Appliquer le package de pilotes](task-sequence-action-variables.md#BKMK_ApplyDriverPackage).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Package de pilotes**  
 Spécifiez le package de pilotes qui contient les pilotes d'appareils nécessaires en cliquant sur **Parcourir** pour ouvrir la boîte de dialogue **Sélectionner un package** . Spécifiez un package existant à rendre disponible. Les propriétés du package associé s'affichent dans la partie inférieure de la boîte de dialogue.  

 **Sélectionner le pilote de stockage de masse au sein du package devant être installé avant la configuration sur les systèmes d’exploitation antérieurs à Windows Vista**  
 Spécifiez les pilotes de stockage de masse nécessaires aux installations des systèmes d'exploitation antérieurs à Windows Vista.  

 **Pilote**  
 Sélectionnez le fichier du pilote de stockage de masse à installer avant la configuration des déploiements des systèmes d'exploitation antérieurs à Windows Vista. La liste déroulante est complétée à partir du package spécifié.  

 **Modèle**  
 Spécifiez l'appareil critique au démarrage nécessaire aux déploiements des systèmes d'exploitation antérieurs à Windows Vista.  

 **Effectuer une installation autonome des pilotes non signés sur les versions de Windows le permettant**  
 Sélectionnez cette option pour autoriser Windows à installer les pilotes non signés sur l'ordinateur de référence.  

##  <a name="a-namebkmkapplynetworksettingsa-apply-network-settings-step"></a><a name="BKMK_ApplyNetworkSettings"></a> Étape Appliquer les paramètres réseau  
 L'étape de séquence de tâches **Appliquer les paramètres réseau** permet de spécifier les informations de configuration du réseau ou du groupe de travail pour l'ordinateur de destination. Les valeurs spécifiées sont stockées au format approprié d'un fichier de réponses afin d'être utilisées par le programme d'installation Windows lors de l'exécution de l'étape de séquence de tâches **Configurer Windows et ConfigMgr** .  

 Cette étape de séquence de tâches s'exécute dans un système d'exploitation standard ou Windows PE. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Appliquer les paramètres réseau](task-sequence-action-variables.md#BKMK_ApplyNetworkSettings).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Joindre un groupe de travail**  
 Sélectionnez cette option pour que l'ordinateur de destination fasse partie du groupe de travail spécifié. Entrez le nom du groupe de travail sur la ligne **Groupe de travail** . Cette valeur peut être remplacée par la valeur capturée par l'étape de séquence de tâches **Capturer les paramètres réseau** .  

 **Joindre un domaine**  
 Sélectionnez cette option pour que l'ordinateur de destination fasse partie du domaine spécifié. Spécifiez ou accédez au domaine, tel que *fabricam.com*. Spécifiez un chemin d’accès LDAP (Lightweight Directory Access Protocol) à une unité d’organisation ou accédez-y (par ex. LDAP//OU=computers, DC=Fabricam.com, C=com).  

 **Compte**  
 Cliquez sur **Définir** pour spécifier un compte bénéficiant des autorisations nécessaires pour associer l'ordinateur au domaine. Dans la boîte de dialogue **Compte d’utilisateur Windows** , vous pouvez entrer le nom d’utilisateur au format suivant : **Domaine\Utilisateur** .  

 **Paramètres de carte**  
 Spécifiez les configurations réseau pour chaque carte réseau dans l'ordinateur. Cliquez sur **Nouveau** pour ouvrir la boîte de dialogue **Paramètres réseau** , puis spécifiez les paramètres réseau. Si les paramètres réseau ont été capturés dans une précédente étape de séquence de tâches **Capturer les paramètres réseau** , les paramètres précédents sont appliqués à la carte réseau et les paramètres spécifiés dans cette étape ne sont pas appliqués. Si les paramètres réseau n'ont pas été capturés au préalable, les paramètres spécifiés à l'étape **Appliquer les paramètres réseau** sont appliqués aux cartes réseau dans l'ordre d'énumération des appareils Windows.  

##  <a name="a-namebkmkapplyoperatingsystemimagea-apply-operating-system-image"></a><a name="BKMK_ApplyOperatingSystemImage"></a> Appliquer l’image du système d’exploitation  
 Utilisez l'étape de séquence de tâches **Appliquer l'image du système d'exploitation** pour installer un système d'exploitation sur l'ordinateur de destination. Cette étape de séquence de tâches exécute un ensemble d'actions selon qu'elle utilise une image de système d'exploitation ou un package d'installation de système d'exploitation pour installer le système d'exploitation.  

 L'étape **Appliquer l'image du système d'exploitation** effectue les actions suivantes lorsqu'une image de système d'exploitation est utilisée.  

1.  Supprime tout le contenu sur le volume cible sauf les fichiers situés sous le dossier spécifié par la variable de séquence de tâches &#95;SMSTSUserStatePath.  

2.  Extrait le contenu des fichiers .wim spécifiés sur la partition de destination indiquée.  

3.  Prépare le fichier de réponses :  

    1.  Crée un nouveau fichier de réponses par défaut du programme d'installation Windows (sysprep.inf ou unattend.xml) pour le système d'exploitation en cours de déploiement.  

    2.  Fusionne les valeurs figurant éventuellement dans le fichier réponse fourni par l'utilisateur.  

4.  Copie les chargeurs de démarrage Windows dans la partition active.  

5.  Configure boot.ini ou BCD (Boot Configuration Database) pour référencer le système d'exploitation nouvellement installé.  

 L'étape **Appliquer l'image du système d'exploitation** effectue les actions suivantes lorsqu'un package d'installation de système d'exploitation est utilisé.  

1.  Supprime tout le contenu sur le volume cible sauf les fichiers situés sous le dossier spécifié par la variable de séquence de tâches &#95;SMSTSUserStatePath.  

2.  Prépare le fichier de réponses :  

    1.  Crée un nouveau fichier de réponses contenant les valeurs standard produites par Configuration Manager.  

    2.  Fusionne les valeurs figurant éventuellement dans le fichier réponses fourni par l'utilisateur.  

> [!NOTE]  
>  L'installation proprement dite de Windows est déclenchée par l'étape de séquence de tâches **Configurer Windows et ConfigMgr** . À l'issue de l'exécution de l'action de séquence de tâches **Appliquer le système d'exploitation** , la variable OSDTargetSystemDrive est réglée sur la lettre de lecteur de la partition contenant les fichiers de système d'exploitation.  

 Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Appliquer l’image du système d’exploitation](task-sequence-action-variables.md#BKMK_ApplyOperatingSystem).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   **Accéder au contenu directement depuis le point de distribution**:  

     Utilisez cette option pour spécifier si vous souhaitez que la séquence de tâches accède à l'image du système d'exploitation directement depuis le point de distribution. Par exemple, vous pouvez utiliser cette option lorsque vous déployez des systèmes d'exploitation sur des appareils intégrés ayant une capacité de stockage limitée. Lorsque cette option est sélectionnée, vous devez également configurer les paramètres de partage du package sous l'onglet **Accès aux données** des propriétés du package.  

    > [!NOTE]  
    >  Ce paramètre remplace l'option de déploiement configurée dans la page **Points de distribution** de l' **Assistant Déploiement logiciel** uniquement pour l'image de système d'exploitation spécifiée lors de cette étape, et non tout le contenu de l'ensemble de la séquence de tâches.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Appliquer le système d’exploitation à partir d’une image capturée**  
 Installer une image du système d'exploitation qui a été précédemment capturée. Cliquez sur **Parcourir** pour ouvrir la boîte de dialogue **Sélectionner un package** , puis sélectionnez le package d'image existant à installer. Si plusieurs images sont associées au **Package d'images**spécifié, utilisez la liste déroulante pour spécifier l'image associée utilisée pour ce déploiement. Vous pouvez afficher des informations de base sur chaque image existante en cliquant sur l'image en question.  

 **Appliquer l’image du système d’exploitation à partir d’une source d’installation d’origine**  
 Installe un système d'exploitation à l'aide d'une source d'installation d'origine. Cliquez sur **Parcourir** pour ouvrir la boîte de dialogue **Sélectionner un package d'installation de système d'exploitation** , puis sélectionnez le package d'installation du système d'exploitation existant à utiliser. Vous pouvez afficher des informations de base sur chaque source d'image existante en cliquant sur l'image source en question. Les propriétés de la source d'image associée s'affichent dans le volet des résultats dans la partie inférieure de la boîte de dialogue. Si plusieurs éditions sont associées au package spécifié, utilisez la liste déroulante pour spécifier l' **Édition** associée qui est utilisée.  

 **Utiliser un fichier de réponse Sysprep ou autonome pour une installation personnalisée**  
 Utilisez cette option pour fournir un fichier de réponses d'installation Windows (**unattend.xml**, **unattend.txt**ou **sysprep.inf**) selon la version du système d'exploitation et la méthode d'installation. Le fichier que vous spécifiez peut inclure toutes les options de configuration standard prises en charge par les fichiers de réponse. Par exemple, vous pouvez l'utiliser pour spécifier la page d'accueil par défaut d'Internet Explorer. Vous devez spécifier le package qui comprend le fichier de réponses et le chemin d'accès associé au fichier dans le package.  

> [!NOTE]  
>  Le fichier de réponses d'installation Windows que vous fournissez peut contenir des variables de séquence de tâches incorporées au format %*varname*%, « varname » correspondant au nom de la variable. La chaîne %*varname*% sera remplacée par les valeurs réelles de la variable dans l'action de séquence de tâches **Configurer Windows et ConfigMgr** . Toutefois, notez qu'il n'est pas possible d'utiliser des variables de séquence de tâches incorporées dans les champs exclusivement numériques d'un fichier de réponses unattend.xml.  

 Si vous n'indiquez pas de fichier de réponses d'installation Windows, cette action de séquence de tâches génère automatiquement un fichier de réponses.  

 **Destination**  
 Spécifie une partition formatée et un disque dur existants, une lettre de lecteur logique précise ou le nom d'une variable de séquence de tâches contenant la lettre de lecteur logique.  

-   **Prochaine partition disponible** : utilisez la partition séquentielle suivante qui n’a pas été précédemment ciblée par une action Appliquer le système d’exploitation ou Appliquer l’image de données dans cette séquence de tâches.  

-   **Disque et partition spécifiques** : sélectionnez le numéro de **disque** (à partir de 0) et le numéro de **partition** (à partir de 1).  

-   **Lettre de lecteur logique spécifique** : spécifiez la **lettre de lecteur** attribuée à la partition par Windows PE. Remarque : cette lettre de lecteur peur être différente de la lettre de lecteur que le système d'exploitation récemment déployé attribuera.  

-   **Lettre de lecteur logique stockée dans une variable** : spécifiez la variable de séquence de tâches contenant la lettre de lecteur attribuée à la partition par Windows PE. Cette variable est généralement définie dans la section Avancé de la boîte de dialogue **Propriétés de la partition** pour l'action de séquence de tâches **Formater et partitionner le disque** .  

##  <a name="a-namebkmkapplywindowssettingsa-apply-windows-settings"></a><a name="BKMK_ApplyWindowsSettings"></a> Appliquer les paramètres Windows  
 Utilisez l'étape de séquence de tâches **Appliquer les paramètres Windows** pour configurer les paramètres Windows de l'ordinateur de destination. Les valeurs spécifiées sont stockées au format approprié d'un fichier de réponses afin d'être utilisées par le programme d'installation Windows lors de l'exécution de l'étape de séquence de tâches **Configurer Windows et ConfigMgr** .  

 Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Appliquer les paramètres Windows](task-sequence-action-variables.md#BKMK_ApplyWindowsSettings).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court, défini par l'utilisateur, qui décrit l'action effectuée dans cette étape  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Nom d’utilisateur**  
 Spécifiez le nom d'utilisateur inscrit qui est associé à l'ordinateur de destination. Cette valeur peut être remplacée par la valeur capturée par l'action de séquence de tâches **Capturer les paramètres Windows** .  

 **Nom de l’organisation**  
 Spécifiez le nom de l'organisation inscrite qui est associé à l'ordinateur de destination. Cette valeur peut être remplacée par la valeur capturée par l'action de séquence de tâches **Capturer les paramètres Windows** .  

 **Clé du produit**  
 Spécifiez la clé du produit qui est utilisée pour l'installation de Windows sur l'ordinateur de destination.  

 **Licence serveur**  
 Spécifiez le mode de licence serveur. Vous pouvez sélectionner le mode **Par serveur** ou **Par utilisateur** . Si vous sélectionnez le mode de licence Par serveur, vous devrez également spécifier le nombre maximal de connexions autorisées selon les termes de votre contrat de licence. Sélectionnez **Ne pas spécifier** si l'ordinateur de destination n'est pas un serveur ou si vous ne souhaitez pas spécifier le mode de licence.  

 **Nombre maximal de connexions**  
 Spécifiez le nombre maximal de connexions disponibles pour cet ordinateur comme spécifié dans votre accord de licence.  

 **Générer de façon aléatoire le mot de passe de l’administrateur local et désactiver le compte sur toutes les plates-formes prises en charge (recommandé)**  
 Sélectionnez cette option si vous souhaitez qu'un mot de passe d'administrateur local soit généré de façon aléatoire. Elle crée un mot de passe d'administrateur local et fait se désactiver le compte sur les plates-formes prises en charge.  

 **Activer le compte et spécifier le mot de passe de l’administrateur local**  
 Sélectionnez cette option pour activer le compte d'administrateur local et créer le mot de passe correspondant. Entrez le mot de passe dans la ligne **Mot de passe** et confirmez-le dans la ligne **Confirmer le mot de passe** .  

 **Fuseau horaire**  
 Spécifiez le fuseau horaire à configurer sur l'ordinateur de destination. Cette valeur peut être remplacée par la valeur capturée par l'étape de séquence de tâches **Capturer les paramètres Windows** .  

##  <a name="a-namebkmkautoapplydriversa-auto-apply-drivers"></a><a name="BKMK_AutoApplyDrivers"></a> Appliquer automatiquement les pilotes  
 Utilisez l'étape de séquence de tâches **Appliquer automatiquement les pilotes** pour faire correspondre et installer des pilotes dans le cadre du déploiement du système d'exploitation.  

 L'étape de séquence de tâches **Appliquer automatiquement les pilotes** effectue les actions suivantes :  

1.  Analyse le matériel et localise les ID Plug-and-Play de tous les appareils présents sur le système.  

2.  Envoie la liste des appareils et leurs ID Plug-and-Play au point de gestion. Celui-ci retourne une liste de pilotes compatibles pour chaque périphérique provenant du catalogue de pilotes. Le point de gestion prend en compte tous les pilotes, quel que soit le package de pilotes dans lequel ils se trouvent. Seuls les pilotes correspondant à la catégorie de pilotes spécifiée et ceux qui ne sont pas marqués comme désactivés sont pris en compte.  

3.  Pour chaque périphérique, le client choisit le pilote le plus approprié au système d'exploitation sur lequel il est déployé et qui se trouve sur un point de distribution accessible.  

4.  Le ou les pilotes sélectionnés sont téléchargés à partir d'un point de distribution et préparés sur le système d'exploitation cible.  

    1.  Pour les installations à base d’image, les pilotes sont placés dans le magasin de pilotes du système d’exploitation.  

    2.  Pour les installations basées sur la configuration, le programme d'installation Windows est configuré avec les informations permettant de localiser les pilotes.  

5.  Lorsque l'action de séquence de tâches **Configurer Windows et ConfigMgr** s'exécute et que Windows démarre pour la première fois, il localise les pilotes préparés par cette action.  

> [!IMPORTANT]
>  L’étape de séquence de tâches **Appliquer automatiquement les pilotes** ne peut pas être utilisée avec un média autonome, car le programme d’installation Windows ne disposera d’aucune connexion au site Configuration Manager.

Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Appliquer automatiquement les pilotes](task-sequence-action-variables.md#BKMK_AutoApplyDrivers).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Installer uniquement les pilotes compatibles les plus appropriés**  
 Indique que l'étape de séquence de tâches installe uniquement le pilote le plus approprié pour chaque périphérique matériel détecté.  

 **Installer tous les pilotes compatibles**  
 Indique que l'étape de séquence de tâches installe tous les pilotes compatibles pour chaque périphérique matériel détecté et autorise le programme d'installation Windows à choisir le meilleur pilote. Cette option utilise davantage de bande passante réseau et d'espace disque car elle télécharge davantage de pilotes, mais un meilleur pilote est éventuellement sélectionné.  

 **Considérer les pilotes de toutes les catégories**  
 Indique que l'action de séquence de tâches recherche toutes les catégories de pilotes disponibles pour les pilotes d'appareils appropriés.  

 **Limiter la correspondance des pilotes aux pilotes des catégories sélectionnées uniquement**  
 Indique que l'action de séquence de tâches recherche les pilotes de périphérique dans les catégories de pilote indiquées pour les pilotes d'appareils appropriés.  

 **Effectuer une installation autonome des pilotes non signés sur les versions de Windows le permettant**  
 Autorise cette action de la séquence de tâches à installer des pilotes d'appareils Windows non signés.  

> [!IMPORTANT]  
>  Cette option ne s'applique pas aux systèmes d'exploitation sur lesquels la stratégie de signature de pilotes ne peut pas être configurée.  

##  <a name="a-namebkmkcapturenetworksettingsa-capture-network-settings"></a><a name="BKMK_CaptureNetworkSettings"></a> Capturer les paramètres réseau  
 L'étape de la séquence de tâches **Capturer les paramètres réseau** permet de capturer les paramètres réseau Microsoft de l'ordinateur exécutant la séquence de tâches. Les paramètres sont enregistrés dans des variables de séquence de tâches qui remplacent les paramètres par défaut que vous configurez à l'étape de séquence de tâches **Appliquer les paramètres réseau** .  

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Capturer les paramètres réseau](task-sequence-action-variables.md#BKMK_CaptureNetworkSettings).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Spécifie un nom court défini par l'utilisateur qui décrit l'action entreprise à cette étape.  

 **Description**  
 Fournit davantage d'informations sur l'action effectuée à cette étape.  

 **Migrer l’appartenance au groupe de travail ou au domaine**  
 Capture les informations d'appartenance du domaine et du groupe de travail de l'ordinateur de destination.  

 **Migrer la configuration de la carte réseau**  
 Capture la configuration de la carte réseau de l'ordinateur de destination. Les informations capturées sont constituées des paramètres réseau globaux, du nombre de cartes et des paramètres réseau associés à chaque carte. Les paramètres sont constitués de paramètres associés à DNS, WINS, IP et aux filtres de port.  

##  <a name="a-namebkmkcaptureoperatingsystemimagea-capture-operating-system-image"></a><a name="BKMK_CaptureOperatingSystemImage"></a> Capturer l’image du système d’exploitation  
 Utilisez l'étape de séquence de tâches **Capturer l'image du système d'exploitation** pour capturer une ou plusieurs images à partir d'un ordinateur de référence et les stocke dans un fichier .WIM sur le partage réseau spécifié. L’Assistant Ajout d’un package d’image de système d’exploitation peut ensuite être utilisé pour importer ce fichier .WIM dans Configuration Manager et ainsi permettre le déploiement de systèmes d’exploitation à base d’image.  

 Chaque volume (lecteur) sur l'ordinateur de référence est capturé en tant qu'image distincte dans le fichier .WIM. Si l'ordinateur référencé comporte des volumes multiples, le fichier .WIM obtenu contiendra une image distincte pour chaque volume. Seuls les volumes formatés au format NTFS ou FAT32 sont capturés. Les volumes d'un autre format et les volumes USB sont ignorés.  

 Le système d’exploitation installé sur l’ordinateur de référence doit être une version de Windows prise en charge par Configuration Manager et doit avoir été préparé à l’aide de l’outil SysPrep. Le volume du système d'exploitation installé et le volume de démarrage doivent correspondre.  

 Vous devez également entrer un compte Windows qui dispose d'autorisations en écriture au partage réseau que vous avez sélectionné.  

 Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Capturer l’image du système d’exploitation](task-sequence-action-variables.md#BKMK_CaptureOperatingSystemImage).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Cible**  
 Nom de chemin du système de fichiers menant à l’emplacement qu’utilise Configuration Manager pour stocker l’image de système d’exploitation capturée.  

 **Description**  
 Description facultative définie par l'utilisateur de l'image du système d'exploitation capturée qui est stockée dans le fichier WIM.  

 **Version**  
 Numéro de version facultatif défini par l'utilisateur à attribuer à l'image du système d'exploitation capturée. Cette valeur peut représenter n'importe quelle combinaison de lettres et de chiffres et est stockée dans le fichier WIM.  

 **Créé par**  
 (facultatif) Nom de l'utilisateur qui a créé l'image du système d'exploitation et qui est stocké dans le fichier WIM.  

 **Compte Capturer l’image du système d’exploitation**  
 Vous devez entrer le compte Windows qui dispose des droits d'accès au partage réseau que vous avez spécifié. Cliquez sur **Définir** pour indiquer le nom de ce compte Windows.  

##  <a name="a-namebkmkcaptureuserstatea-capture-user-state"></a><a name="BKMK_CaptureUserState"></a> Capturer l’état utilisateur  
 L'étape de la séquence de tâches **Capturer l'état utilisateur** permet d'utiliser l'outil de migration de l'état utilisateur (USMT) pour capturer l'état et les paramètres utilisateur de l'ordinateur exécutant la séquence de tâches. Cette étape de séquence de tâches est utilisée avec l'étape de séquence de tâches **Restaurer l'état utilisateur** . Dans USMT 3.0.1 et ultérieur, cette option chiffre toujours le magasin d’état USMT au moyen d’une clé de chiffrement générée et gérée par Configuration Manager.  

 Pour plus d’informations sur la gestion de l’état utilisateur pendant le déploiement de systèmes d’exploitation, consultez [Gérer l’état utilisateur](../get-started/manage-user-state.md).  

 Vous pouvez aussi utiliser l’étape de séquence de tâches **Capturer l’état utilisateur** avec les étapes de séquence de tâches **Demander le magasin d’état** et **Libérer le magasin d’état** si vous voulez enregistrer les paramètres d’état sur un point de migration d’état ou les restaurer à partir d’un point de migration d’état dans le site Configuration Manager.  

 L'étape de séquence de tâches **Capturer l'état utilisateur** permet de contrôler un sous-ensemble des options USMT les plus couramment utilisées. D'autres options de ligne de commande peuvent être spécifiées au moyen de la variable de séquence de tâches OSDMigrateAdditionalCaptureOptions.  

 Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Capturer l’état utilisateur](task-sequence-action-variables.md#BKMK_CaptureUserState).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Package de l’outil de migration de l’état utilisateur**  
 Entrez le package Configuration Manager qui contient la version de l’outil USMT pour cette étape de séquence de tâches pour l’utiliser pendant la capture des paramètres et de l’état utilisateur. Ce package ne requiert pas de programme. Lorsque l'étape de séquence de tâches est exécutée, la séquence de tâches utilise la version de l'outil de migration de l'état utilisateur du package que vous indiquez. Spécifiez un package contenant la version 32 bits ou x64 de USMT en fonction de l'architecture du système d'exploitation à partir duquel vous capturez l'état.  

 **Capturer tous les profils utilisateur présentant les options standard**  
 Sélectionnez cette option pour migrer toutes les informations des profils utilisateur. Cette option est activée par défaut.  

 Si vous sélectionnez cette option sans sélectionner l’option Restaurer les profils utilisateur de l’ordinateur local dans l’étape de séquence de tâches Restaurer l’état utilisateur, la séquence de tâches échouera, car Configuration Manager ne peut pas migrer les nouveaux comptes sans leur attribuer des mots de passe. De même, si vous faites appel à l'Assistant **Nouvelle séquence de tâches** et créez une séquence de tâches pour **Installer un package d'images existant**, la séquence de tâches obtenue prend par défaut la valeur Capturer tous les profils utilisateur présentant les options standard, mais ne sélectionne pas l'option Restaurer les profils utilisateur de l'ordinateur local (c.-à-d. des comptes qui sont pas des comptes de domaine).  

 Sélectionnez **Restaurer les profils utilisateur de l'ordinateur local** et spécifiez un mot de passe pour le compte à migrer. Dans une séquence de tâches qui a été manuellement créée, ce paramètre est disponible sous l'étape Restaurer l'état utilisateur. Dans une séquence de tâches créée à l'aide de l'Assistant **Nouvelle séquence de tâches** , ce paramètre est disponible sur la page de l'assistant d'étape **Restaurer les fichiers et paramètres utilisateur** .  

 Si vous ne disposez d'aucun compte d'utilisateur local, ceci ne s'applique pas.  

 **Personnaliser la façon dont les profils utilisateur sont capturés**  
 Sélectionnez cette option pour indiquer une migration de fichiers de profils personnalisée. Cliquez sur **Fichiers** pour sélectionner les fichiers de configuration pour l'outil de migration de l'état utilisateur à utiliser avec cette étape. Vous devez indiquer un fichier .xml personnalisé contenant les règles qui définissent les fichiers de l'état utilisateur à migrer.  

 **Cliquez ici pour sélectionner les fichiers de configuration :**  
 Sélectionnez cette option pour sélectionner les fichiers de configuration dans le package USMT que vous souhaitez utiliser pour capturer les profils utilisateur. Cliquez sur le bouton **Fichiers** pour lancer la boîte de dialogue **Fichiers de configuration** . Pour indiquer un fichier de configuration, entrez son nom sur la ligne **Nom de fichier** , puis cliquez sur le bouton **Ajouter** .  

 **Activer la journalisation documentée**  
 Activez cette option pour générer des informations de fichiers journaux plus détaillées. Lors de la capture de l'état, le fichier Scanstate.log est généré et stocké par défaut dans le dossier de journalisation de la séquence de tâches du dossier \windows\system32\ccm\logs .  

 **Ignorer les fichiers utilisant le système de fichiers chiffrés (EFS)**  
 Activez cette option si vous souhaitez ignorer la capture des fichiers chiffrés au moyen d'EFS (Encrypted File System, Système de fichiers chiffrés), y compris les fichiers de profils. Selon le système d'exploitation et la version d'USMT, les fichiers chiffrés peuvent ne pas être accessibles après la restauration. Pour plus d'informations, consultez la documentation d'USMT.  

 **Copier en utilisant l’accès au système de fichiers**  
 Activez cette option pour spécifier les paramètres suivants :  

-   **Continuer si certains fichiers ne peuvent pas être capturés**: activez ce paramètre pour continuer le processus de migration même si certains fichiers ne peuvent pas être capturés. Si vous désactivez cette option et qu'un fichier ne peut pas être capturé, l'étape de la séquence de tâches échouera. Cette option est activée par défaut.  

-   **Capturer localement en utilisant les liens au lieu de copier les fichiers**: activez ce paramètre pour utiliser des liens physiques NTFS pour capturer les fichiers.  

     Pour plus d'informations sur la migration de données à l'aide de liens directs, consultez [Magasin de migration de lien direct](http://go.microsoft.com/fwlink/p/?LinkId=240222)  

-   **Capturer en mode hors-ligne (Windows PE uniquement)**: activez ce paramètre pour capturer l’état utilisateur dans Windows PE au lieu du système d’exploitation complet.  

 **Capturer en utilisant Volume Copy Shadow Service (VSS)**  
 Cette option vous permet de capturer des fichiers même s’ils sont verrouillés pour modification par une autre application.  

##  <a name="a-namebkmkcapturewindowssettingsa-capture-windows-settings"></a><a name="BKMK_CaptureWindowsSettings"></a> Capturer les paramètres Windows  
 Utilisez l'étape de la séquence de tâches **Capturer les paramètres Windows** pour capturer les paramètres Windows de l'ordinateur exécutant la séquence de tâches. Les paramètres sont enregistrés dans des variables de séquence de tâches qui remplacent les paramètres par défaut que vous configurez à l'étape de séquence de tâches **Appliquer les paramètres Windows** .  

 Cette étape de séquence de tâches s'exécute dans Windows PE ou un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Capturer les paramètres Windows](task-sequence-action-variables.md#BKMK_CaptureWindowsSettings).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Migrer le nom de l’ordinateur**  
 Sélectionnez cette option pour capturer le nom NetBIOS de l'ordinateur.  

 **Migrer les noms d’organisations et d’utilisateurs inscrits**  
 Sélectionnez cette option pour capturer les noms de l'utilisateur enregistré et de l'organisation à partir de l'ordinateur.  

 **Migrer le fuseau horaire**  
 Sélectionnez cette option pour capturer le paramètre de fuseau horaire sur l'ordinateur.  

##  <a name="a-namebkmkcheckreadinessa-check-readiness"></a><a name="BKMK_CheckReadiness"></a> Vérifier la préparation  
 Utilisez la séquence de tâches **Vérifier la préparation** pour vérifier que l'ordinateur cible remplit les conditions requises spécifiées pour le déploiement.  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape. Pour cette étape, ne sélectionnez pas ce paramètre, sinon l'étape n'enregistre que les vérifications de préparation et la séquence de tâches ne s'arrête pas en cas d'échec d'une vérification.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Garantir une mémoire minimum (Mo)**  
 Sélectionnez ce paramètre pour vérifier que la quantité de mémoire, en mégaoctets, installée sur l'ordinateur cible atteint ou dépasse la taille spécifiée. Ce paramètre est activé par défaut.  

 **Garantir une vitesse de processeur minimum (MHz)**  
 Sélectionnez ce paramètre pour vérifier que la vitesse du processeur, en mégahertz (MHz), installée sur l'ordinateur cible atteint ou dépasse la taille spécifiée. Ce paramètre est activé par défaut.  

 **Garantir un espace disque libre minimum (Mo)**  
 Sélectionnez ce paramètre pour vérifier que la quantité d'espace disque disponible, en mégaoctets, sur l'ordinateur cible atteint ou dépasse la taille spécifiée.  

 **S’assurer que le SE à actualiser est**  
 Sélectionnez ce paramètre pour vérifier que le système d'exploitation installé sur l'ordinateur cible remplit la condition que vous spécifiez. Par défaut, ce paramètre est sélectionné avec la valeur **CLIENT**.  

##  <a name="a-namebkmkconnecttonetworkfoldera-connect-to-network-folder"></a><a name="BKMK_ConnectToNetworkFolder"></a> Se connecter à un dossier réseau  
 Utilisez l'action de la séquence de tâches **Connexion à un dossier réseau** pour établir une connexion avec un dossier réseau partagé.  

 Cette étape de séquence de tâches s'exécute dans un système d'exploitation standard ou Windows PE. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Se connecter à un dossier réseau](task-sequence-action-variables.md#BKMK_ConnecttoNetworkFolder).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

##  <a name="a-namebkmkconvertdisktodynamica-convert-disk-to-dynamic"></a><a name="BKMK_ConvertDisktoDynamic"></a> Convertir en disque dynamique  
 Utilisez la séquence de tâches **Convertir en disque dynamique** pour convertir un disque physique de type standard en disque dynamique.  

 Cette étape s'exécute dans un système d'exploitation standard ou Windows PE. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Convertir en disque dynamique](task-sequence-action-variables.md#BKMK_ConvertDisk).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Numéro du disque**  
 Numéro du disque physique à convertir.  

##  <a name="a-namebkmkdisablebitlockera-disable-bitlocker"></a><a name="BKMK_DisableBitLocker"></a> Désactiver BitLocker  
 Utilisez l'étape de la séquence de tâches **Désactiver BitLocker** pour désactiver le chiffrement BitLocker sur le disque du système d'exploitation actuel ou sur un lecteur spécifique. Cette action laisse les protecteurs de clé visibles en texte clair sur le disque dur, mais elle ne déchiffre pas le contenu du lecteur. En conséquence, cette action est terminée presque instantanément.  

> [!NOTE]  
>  Le chiffrement de lecteur BitLocker propose un cryptage de bas niveau du contenu d'un volume de disque.  

 Si vous avez plusieurs lecteurs chiffrés, vous devez désactiver BitLocker sur chaque lecteur de données avant de désactiver BitLocker sur le lecteur du système d'exploitation.  

 Cette étape s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE.  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Spécifie un nom court défini par l'utilisateur qui décrit l'action entreprise à cette étape.  

 **Description**  
 Fournit davantage d'informations sur l'action effectuée à cette étape.  

 **Lecteur du système d’exploitation actuel**  
 Désactive BitLocker sur le disque du système d'exploitation courant.  

 **Lecteur spécifique**  
 Désactive BitLocker sur un disque spécifique. Dans la liste déroulante, sélectionnez le disque sur lequel BitLocker est désactivé.  

##  <a name="a-namebkmkdownloadpackagecontenta-download-package-content"></a><a name="BKMK_DownloadPackageContent"></a> Télécharger le contenu du package  
 Utilisez l’étape de séquence de tâches **Télécharger le contenu du package** pour télécharger un des types de package suivants :  

-   Images du système d'exploitation  

-   Packages de mise à niveau du système d’exploitation  

-   Packages de pilotes  

-   Packages  

 Cette étape fonctionne bien dans une séquence de tâches pour mettre à niveau un système d’exploitation dans les scénarios suivants :  

-   Pour utiliser une seule séquence de tâches de mise à niveau qui peut fonctionner avec les plateformes x86 et x64. Pour cela, incluez deux étapes **Télécharger le contenu du package** dans le groupe **Préparer pour la mise à niveau** avec des conditions pour détecter l’architecture du client et télécharger uniquement le package de mise à niveau de système d’exploitation approprié. Configurez chaque étape **Télécharger le contenu du package** pour utiliser la même variable et utilisez cette variable pour le chemin du support à l’étape **Mettre à niveau le système d’exploitation** .  

-   Pour télécharger dynamiquement un package de pilotes applicable, utilisez deux étapes **Télécharger le contenu du package** avec des conditions pour détecter le type de matériel approprié pour chaque package de pilotes. Configurez chaque étape **Télécharger le contenu du package** pour utiliser la même variable et utilisez cette variable pour la valeur **Contenu intermédiaire** dans la section des pilotes à l’étape **Mettre à niveau le système d’exploitation** .  

Cette étape s'exécute dans un système d'exploitation standard ou Windows PE. Toutefois, la possibilité d’enregistrer le package dans le cache du client Configuration Manager n’est pas prise en charge dans WinPE.

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Spécifie un nom court défini par l'utilisateur qui décrit l'action entreprise à cette étape.  

 **Description**  
 Fournit davantage d'informations sur l'action effectuée à cette étape.  

 Icône**Sélectionner un package**  
 Cliquez sur l’icône pour sélectionner le package à télécharger. Après avoir sélectionné un package, vous pouvez cliquer une nouvelle fois sur l’icône pour choisir un autre package.  

 **Placez à l’emplacement suivant**  
 Choisissez d’enregistrer le package à l’un des emplacements suivants :  

-   **Répertoire de travail de séquence de tâches**  

-   **Cache du client Configuration Manager**: vous utilisez cette option pour stocker le contenu dans le cache du client. Cela permet au client de servir de source de cache homologue pour d’autres clients de cache homologue. Pour plus d’informations, consultez [Préparer la mise en cache d’homologue Windows PE pour réduire le trafic WAN](../get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

-   **Chemin personnalisé**  

 **Enregistrez le chemin d’accès en tant que variable**  
 Vous pouvez enregistrer le chemin en tant que variable que vous pouvez utiliser dans une autre étape de séquence de tâches. Quand il existe plusieurs packages, Configuration Manager ajoute un suffixe numérique au nom de la variable. Par exemple, si vous spécifiez une variable %*mon_contenu*% en tant que variable personnalisée, il s’agit de la racine du stockage de tout le contenu référencé (qui peut correspondre à plusieurs packages). Quand vous faites référence à la variable dans une étape de sous-séquence, comme Mettre à niveau le système d’exploitation, elle est utilisée avec un suffixe numérique. Dans cet exemple, nous avons %*mon_contenu01*% ou %*mon_contenu02*% où le nombre correspond à l’ordre d’apparition du package dans cette étape.  

 **En cas d’échec de téléchargement d’un package, continuer le téléchargement des autres packages de la liste**  
 Spécifie que si le téléchargement d’un package échoue, le package suivant dans la liste est sélectionné et son téléchargement démarré.  

##  <a name="a-namebkmkenablebitlockera-enable-bitlocker"></a><a name="BKMK_EnableBitLocker"></a> Activer BitLocker  
 Utilisez l'étape de séquence de tâches **Activer BitLocker** pour activer le chiffrement BitLocker sur au moins deux partitions sur le disque dur. La première partition active contient le code d'amorçage Windows. Une autre partition contient le système d'exploitation. La partition d'amorçage ne doit pas être chiffrée.  

 Utilisez l'étape de séquence de tâches **Préconfigurer BitLocker** pour activer BitLocker sur un lecteur dans Windows PE. Pour plus d'informations, voir la section [Préconfigurer BitLocker](#BKMK_PreProvisionBitLocker) de cette rubrique.  

> [!NOTE]  
>  Le chiffrement de lecteur BitLocker propose un cryptage de bas niveau du contenu d'un volume de disque.  

 L'étape **Activer BitLocker** s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Activer BitLocker](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

 Le Module de plateforme sécurisée (TPM) doit être à l'état suivant lorsque vous spécifiez **TPM uniquement**, **TPM et clé de démarrage sur USB** ou **TPM et code confidentiel**pour que vous puissiez effectuer l'étape **Activer BitLocker** :  

-   Permis  

-   Activé  

-   Propriété autorisée  

 L'étape de la séquence de tâches peut terminer toute initialisation d'un module de plateforme sécurisée (TPM) restante, car les étapes restantes ne requièrent ni une présence physique ni des redémarrages de l'ordinateur. Les étapes d'initialisation d'un module de plate-forme sécurisée (TPM) restantes qui peuvent être terminées de manière transparente par **Activer BitLocker** (le cas échéant) incluent :  

-   Créer une paire de clés de validité  

-   Créer une valeur d'autorisation du propriétaire et la déposer dans Active Directory, qui doit avoir été développé afin de prendre en charge cette valeur.  

-   Se définir comme propriétaire  

-   Créer la clé racine de stockage ou la réinitialiser si elle existe déjà mais qu'elle est incompatible.  

 Si vous voulez que l'étape **Activer BitLocker** soit mise en attente et qu'elle ait lieu après la fin du processus de chiffrement du disque et avant de passer à l'étape suivante de la séquence de tâches, activez la case à cocher **Attente** . Si vous n'activez pas la case à cocher **Attente** , le processus de chiffrement du disque est effectué en arrière-plan et l'exécution de la séquence de tâches passe immédiatement à l'étape suivante.  

 BitLocker peut être utilisé pour chiffrer plusieurs lecteurs sur un système d'ordinateurs (système d'exploitation et lecteurs de données). Pour chiffrer un lecteur de données, le système d'exploitation doit déjà être chiffré et le processus de chiffrement doit être terminé, car les protecteurs de clé des lecteurs de données sont stockés sur le lecteur du système d'exploitation. Par conséquent, si vous chiffrez le lecteur du système d'exploitation et le lecteur de données lors du même processus, l'option d'attente doit être sélectionnée pour l'étape qui active BitLocker sur le lecteur du système d'exploitation.  

 Si le disque est déjà chiffré mais que BitLocker est désactivé, Activer BitLocker active de nouveau le ou les protecteurs des clés. Cette opération sera pratiquement immédiate. Dans ce cas, il n'est pas nécessaire de chiffrer de nouveau le disque.  

 Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Activer BitLocker](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Indique un nom descriptif pour cette étape de séquence de tâches.  

 **Description**  
 Permet, si vous le souhaitez, d'entrer une description de cette étape de séquence de tâches.  

 **Lecteur à chiffrer**  
 Indique le lecteur à chiffrer. Pour chiffrer le lecteur du système d'exploitation actuel, sélectionnez **Lecteur du système d'exploitation actuel** , puis configurez l'une des options suivantes de gestion des clés :  

-   **TPM uniquement**: sélectionnez cette option pour utiliser uniquement le module de plateforme sécurisée (TPM).  

-   **Clé de démarrage sur USB uniquement**: sélectionnez cette option pour utiliser une clé de démarrage stockée sur une clé USB. Lorsque vous sélectionnez cette option, BitLocker verrouille le processus de démarrage normal jusqu'à ce qu'un périphérique USB contenant une clé de démarrage BitLocker soit connecté à l'ordinateur.  

-   **TPM et clé de démarrage sur USB**: sélectionnez cette option pour utiliser le module TPM et une clé de démarrage stockée sur une clé USB. Lorsque vous sélectionnez cette option, BitLocker verrouille le processus de démarrage normal jusqu'à ce qu'un périphérique USB contenant une clé de démarrage BitLocker soit connecté à l'ordinateur.  

-   **TPM et code confidentiel**: sélectionnez cette option pour utiliser le module TPM et un numéro d’identification personnel (code confidentiel). Lorsque vous sélectionnez cette option, BitLocker verrouille le processus de démarrage normal jusqu'à ce que l'utilisateur fournisse le code confidentiel.  

 Pour chiffrer un lecteur de données spécifique autre qu'un lecteur de système d'exploitation, sélectionnez **Lecteur spécifique**, puis sélectionnez le lecteur dans la liste.  

 **Emplacement de création de la clé de récupération**  
 Pour indiquer l'emplacement où est créé le mot de passe de récupération, sélectionnez **Dans Active Directory** pour déposer le mot de passe dans Active Directory. Si vous sélectionnez cette option, vous devez étendre Active Directory au site afin que les informations de récupération BitLocker associées soient enregistrées. Vous pouvez décider de ne pas créer de mot de passe en sélectionnant **Ne pas créer de clé de récupération**. Toutefois, la création d'un mot de passe est recommandée.  

 **Attendez que BitLocker termine le processus de chiffrement des lecteurs avant de poursuivre l’exécution de la séquence de tâches**  
 Sélectionnez cette option pour exécuter le chiffrement de lecteur BitLocker avant d'exécuter la séquence de tâches suivante. Si elle est sélectionnée, le volume de disque entier est chiffré avant que l'utilisateur puisse se connecter à l'ordinateur.  

 Le processus de chiffrement peut prendre des heures dans le cas du chiffrement d'un disque dur de taille importante. Si vous ne sélectionnez pas cette option, la séquence de tâches débutera immédiatement.  

##  <a name="a-namebkmkformatandpartitiondiska-format-and-partition-disk"></a><a name="BKMK_FormatandPartitionDisk"></a> Formater et partitionner le disque  
 Utilisez l'étape de la séquence de tâches **Formater et partitionner le disque** pour formater et partitionner un disque spécifié sur l'ordinateur de destination.  

> [!IMPORTANT]  
>  Chaque paramètre défini pour cette étape de la séquence de tâches s'applique à un seul disque spécifié. Pour formater et partitionner un autre disque sur l'ordinateur de destination, vous devez ajouter à la séquence de tâches une étape supplémentaire **Formater et partitionner le disque** .  

 Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Formater et partitionner le disque](task-sequence-action-variables.md#BKMK_FormatPartitionDisk).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Numéro du disque**  
 Numéro de disque physique à formater. Le numéro se base sur le classement d'énumération du disque Windows.  

 **Type du disque**  
 Le type du disque formaté. Deux options sont disponibles dans la liste déroulante :  

-   Standard (MBR) – Secteur de démarrage principal.  

-   GPT – Table de partition GUID  

> [!NOTE]  
>  Si vous passez le type de disque de **Standard (MBR)** à **GPT**, et si la structure de la partition contient une partition étendue, toutes les partitions étendues et logiques seront supprimées de la structure. Un message vous invite à confirmer l'opération avant de valider le changement de type de disque.  

 **Volume**  
 Informations spécifiques sur la partition ou le volume à créer, notamment :  

-   Nom  

-   Espace disque restant  

 Pour créer une partition, cliquez sur **Nouveau** pour ouvrir la boîte de dialogue **Propriétés de la partition** . Vous pouvez indiquer le type de partition et la taille, et préciser s'il s'agit d'une partition de démarrage. Pour modifier une partition existante, cliquez sur la partition à modifier puis sur le bouton Propriétés. Pour plus d'informations sur la façon de configurer des partitions de disque dur, consultez l'une des ressources suivantes :  

-   [Configurer des partitions de disque dur UEFI/GPT](http://go.microsoft.com/fwlink/?LinkID=272104)  

-   [Configurer des partitions de disque dur BIOS/MBR](http://go.microsoft.com/fwlink/?LinkId=272105)  

 Pour supprimer une partition, sélectionnez-la, puis cliquez sur **Supprimer**.  

##  <a name="a-namebkmkinstallapplicationa-install-application"></a><a name="BKMK_InstallApplication"></a> Installer l’application  
 Utilisez l'étape de séquence de tâches **Installer l'application** pour installer des applications dans le cadre de la séquence de tâches. Cette étape peut installer un ensemble d'applications spécifiées par l'étape de séquence de tâches ou un ensemble d'applications spécifiées par une liste dynamique de variables de séquence de tâches. Lorsque cette étape est exécutée, l'installation de l'application commence immédiatement sans attendre un intervalle d'interrogation de stratégie.  

 Les applications installées doivent répondre aux critères suivants :  

-   L’application doit avoir un type de déploiement Windows Installer ou Programme d’installation de script. Les types de déploiement Package d’application Windows (fichier .appx) ne sont pas pris en charge.  

-   Il doit être exécuté sous le compte système local et non le compte d'utilisateur.  

-   Il ne doit pas interagir avec le Bureau. Le programme doit s'exécuter en mode silencieux ou en mode sans assistance.  

-   Il ne doit pas lancer un redémarrage seul. L'application doit demander un redémarrage à l'aide du code de redémarrage standard 3010, qui est un code de sortie. Ceci garantit que la séquence de tâches gérera correctement le redémarrage. Si l'application renvoie un code de sortie 3010, le moteur de séquences de tâches sous-jacent effectue le redémarrage. Après le redémarrage, la séquence de tâches se poursuit automatiquement.  

 Lorsque l'étape **Installer l'application** s'exécute, l'application vérifie l'applicabilité des règles de spécification et la méthode de détection sur les types de déploiement de l'application. Selon les résultats de cette vérification, l'application installe le type de déploiement applicable. Si un type de déploiement contient des dépendances, le type de déploiement dépendant est évalué et installé dans le cadre de l'étape Installer l'application. Les dépendances d'application ne sont pas prises en charge pour les médias autonomes.  

> [!NOTE]  
>  Pour installer une application qui en remplace une autre, les fichiers de contenu de l'application remplacée doivent être disponibles, sinon l'étape échoue. Par exemple, Microsoft Visio 2010 est installé sur un client ou dans une image capturée. Lorsque l'étape de séquence de tâches Installer l'application est exécutée pour installer Microsoft Visio 2013, les fichiers de contenu de Microsoft Visio 2010 (l'application remplacée) doivent être disponibles sur un point de distribution, sinon la séquence de tâches échoue. Un client ou une image capturée sans Microsoft Visio installé terminera l'installation de Microsoft Visio 2013 sans vérifier la présence des fichiers de contenu de Microsoft Visio 2010.  

> [!NOTE]
> Vous pouvez utiliser les variables intégrées SMSTSMPListRequestTimeoutEnabled et SMSTSMPListRequestTimeout pour activer et spécifier le délai d’attente (en millisecondes) d’une séquence de tâche avant qu’elle tente à nouveau d’installer une application ou une mise à jour logicielle après l’échec de la récupération de la liste de points de gestion auprès des services de localisation. Pour plus d’informations, consultez [Variables intégrées de séquence de tâches](task-sequence-built-in-variables.md).

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE.  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Indiquez qu'il faut réessayer cette étape si l'ordinateur redémarre de façon inattendue. Vous pouvez également spécifier le nombre de nouvelles tentatives après un redémarrage.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Installer les applications suivantes**  
 Ce paramètre spécifie les applications installées dans l'ordre dans lequel elles sont spécifiées.  

 Configuration Manager éliminera toutes les applications désactivées ou les applications avec les paramètres suivants. Ces applications n'apparaissent pas dans la boîte de dialogue **Sélectionner l'application à installer** .  

-   Uniquement quand un utilisateur a ouvert une session  

-   Exécuter avec les droits utilisateur  

 **Installer les applications en fonction de la liste de variables dynamiques**  
 Ce paramètre spécifie le nom de base d'un ensemble de variables de séquence de tâches qui sont définies pour un regroupement ou un ordinateur. Ces variables spécifient les applications qui seront installées pour ce regroupement ou cet ordinateur. Chaque nom de variable comprend son nom de base courant plus un suffixe numérique commençant par 01. La valeur de chaque variable doit contenir le nom de l'application et rien d'autre.  

 Pour les applications à installer en utilisant une liste de variables dynamiques, le paramètre suivant doit être activé sous l’onglet **Général** de la boîte de dialogue **Propriétés** de l’application : **Autoriser cette application à être installée à partir de l’action de la séquence de tâches Installer l’application plutôt que de la déployer manuellement**.  

> [!NOTE]  
>  Vous ne pouvez pas installer d'applications à l'aide d'une liste de variables dynamiques pour les déploiements de média autonome.  

 Par exemple, pour installer une application unique à l'aide d'une variable de séquence de tâches nommée AA01, vous indiquez la variable suivante :  

|Nom de la variable :|Valeur de la variable|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

 Pour installer deux applications, vous indiqueriez les variables suivantes :  

|Nom de la variable :|Valeur de la variable|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

 Les conditions suivantes affectent ce qui est installé :  

-   Si la valeur d'une variable contient d'autres informations que le nom de l'application. Cette application n'est pas installée et la séquence de tâches continue.  

-   Si aucune variable avec le nom de base et le suffixe «&01; » spécifiés n'est détectée, aucune application n'est installée. Quand vous sélectionnez **Continuer en cas d’erreur** sous l’onglet Options de l’étape de séquence de tâches, la séquence de tâches se poursuit quand l’installation d’une application échoue. Lorsque le paramètre n'est pas sélectionné, la séquence de tâches échoue et n'installe pas les autres applications.  

 **Si l’installation d’une application échoue, continuer d’installer les autres applications de la liste**  
 Ce paramètre spécifie que l'étape se poursuit si l'installation d'une application individuelle échoue. Si ce paramètre est spécifié, la séquence de tâches continue indépendamment des erreurs d'installation renvoyées. Si ce paramètre n'est pas spécifié et qu'une installation échoue, l'étape de séquence de tâches s'interrompt immédiatement.  

##  <a name="a-namebkmkinstalldeploymenttoolsa-install-deployment-tools"></a><a name="BKMK_InstallDeploymentTools"></a> Installer les outils de déploiement  
 Utilisez l’étape de séquence de tâches **Installer les outils de déploiement** pour installer le package Configuration Manager qui contient les outils de déploiement Sysprep.  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Package Sysprep**  
 Ce paramètre permet de spécifier le package Configuration Manager qui contient les outils de déploiement Sysprep pour les systèmes d’exploitation suivants :  

-   Windows XP SP3  

-   Windows XP X64 SP2  

-   Windows Server 2003 SP2  

##  <a name="a-namebkmkinstallpackagea-install-package"></a><a name="BKMK_InstallPackage"></a> Installer le package

 Utilisez l'étape de séquence de tâches **Installer le package** pour installer des logiciels dans le cadre de la séquence de tâches. Lorsque cette étape est exécutée, l'installation commence immédiatement sans attendre un intervalle d'interrogation de stratégie.  

 Le logiciel installé doit répondre aux critères suivants :  

-   Il doit être exécuté sous le compte système local et non le compte d'utilisateur.  

-   Il ne doit pas interagir avec le Bureau. Le programme doit s'exécuter en mode silencieux ou en mode sans assistance.  

-   Il ne doit pas lancer un redémarrage seul. Le logiciel doit demander un redémarrage à l'aide du code de redémarrage standard 3010, qui est un code de sortie. Ceci garantit que la séquence de tâches gérera correctement le redémarrage. Si le logiciel retourne un code de sortie 3010, le moteur de séquences de tâches sous-jacent effectue le redémarrage. La séquence de tâches continue automatiquement après celui-ci.  

 Les programmes qui utilisent l'option **Exécuter un autre programme en premier** pour installer un programme dépendant ne sont pas pris en charge lors du déploiement d'un système d'exploitation. Si l'option **Exécuter un autre programme en premier** est activée pour le logiciel et que le programme dépendant a déjà été exécuté sur l'ordinateur de destination, le programme dépendant sera exécuté et la séquence de tâches continuera. En revanche, si le programme dépendant n'a pas déjà été exécuté sur l'ordinateur de destination, l'étape de la séquence de tâches échouera.  

> [!NOTE]  
>  Le site d'administration centrale ne dispose pas des stratégies de configuration de client requises pour activer l'agent de distribution logicielle au cours de l'exécution de la séquence de tâches. Lorsque vous créez un média autonome pour une séquence de tâches sur le site d'administration centrale et que la séquence de tâches contient une étape **Installer le package** , l'erreur suivante peut apparaître dans le fichier CreateTsMedia.log :  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>   
>  Dans le cas de médias autonomes contenant une étape Installer le package, vous devez créer le média autonome sur un site principal sur lequel l'agent de distribution logicielle est activé ou insérer une étape **Exécuter la ligne de commande** entre l'étape **Configurer Windows et Configuration Manager** et la première étape **Installer le package** . L'étape **Exécuter la ligne de commande** exécute une commande de ligne de commande WMIC pour activer l'agent de distribution logicielle avant l'exécution de la première étape Installer le package. Vous pouvez utiliser la ligne de commande suivante dans l'étape **Exécuter la ligne de commande** de votre séquence de tâches :  
>   
>  **Ligne de commande** : **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  
>   
>  Pour plus d’informations sur la création d’un média autonome, consultez [Créer un média autonome](../deploy-use/create-stand-alone-media.md).  

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE.  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Installer un seul package logiciel**  
 Ce paramètre permet de spécifier un package logiciel Configuration Manager. L'étape attend que l'installation soit terminée.  

 **Installer les packages logiciels en fonction de la liste de variables dynamiques**  
 Ce paramètre spécifie le nom de base d'un ensemble de variables de séquence de tâches qui sont définies pour un regroupement ou un ordinateur. Ces variables spécifient les packages qui seront installés pour ce regroupement ou cet ordinateur. Chaque nom de variable comprend son nom de base courant plus un suffixe numérique commençant par 001. La valeur de chaque variable doit contenir un ID de package et le nom du logiciel séparés par deux-points.  

 Pour les logiciels à installer en utilisant une liste de variables dynamiques, le paramètre suivant doit être activé sous l’onglet **Avancé** de la boîte de dialogue **Propriétés** du package : **Autoriser l’installation de ce programme depuis la séquence de tâches d’installation du package sans le déployer**.  

> [!NOTE]  
>  Vous ne pouvez pas installer de packages logiciels à l'aide d'une liste de variables dynamiques pour les déploiements de média autonome.  

 Par exemple, pour installer un package logiciel unique à l'aide d'une variable de séquence de tâches nommée AA001, vous indiquez la variable suivante :  

|Nom de la variable :|Valeur de la variable|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

 Pour installer trois packages logiciels, vous indiqueriez les variables suivantes :  

|Nom de la variable :|Valeur de la variable|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

 Les conditions suivantes affectent ce qui est installé :  

-   Si la valeur d'une variable n'est pas créée au format approprié ou n'indique pas un ID et un nom d'application valides, l'installation du logiciel échoue.  

-   Si l'ID de package contient des caractères en minuscules, l'installation de ce logiciel échoue.  

-   Si aucune variable avec le nom de base et le suffixe «&001; » spécifiés n'est détectée, aucun package n'est installé et la séquence de tâches continue.  

 **Si l’installation d’un package logiciel échoue, continuer d’installer les autres packages de la liste**  
 Ce paramètre spécifie que l'étape se poursuit si l'installation d'un package logiciel individuel échoue. Si ce paramètre est spécifié, la séquence de tâches continue indépendamment des erreurs d'installation renvoyées. Si ce paramètre n'est pas spécifié et qu'une installation échoue, l'étape de séquence de tâches s'interrompt immédiatement.  

##  <a name="a-namebkmkinstallsoftwareupdatesa-install-software-updates"></a><a name="BKMK_InstallSoftwareUpdates"></a> Installer les mises à jour logicielles  
 L'étape de séquence de tâches **Installer les mises à jour logicielles** permet d'installer les mises à jour logicielles sur l'ordinateur de destination. L'ordinateur de destination n'est pas évalué pour déterminer les mises à jour logicielles applicables avant l'exécution de cette séquence de tâches. À ce stade, l’ordinateur de destination est évalué pour déterminer les mises à jour logicielles comme n’importe quel autre client géré par Configuration Manager. En particulier, cette étape n'installe que les mises à jour logicielles destinées aux regroupements dont l'ordinateur est actuellement membre.  
>  [!IMPORTANT]
>Nous vous recommandons vivement d’installer la dernière version de l’Agent Windows Update pour obtenir de meilleures performances lors de l’utilisation de l’étape de séquence de tâches Installer les mises à jour logicielles.
>* Pour Windows 7, consultez [l’article de la Base de connaissances 3161647](https://support.microsoft.com/kb/3161647).
>* Pour Windows 8, consultez [l’article de la Base de connaissances 3163023](https://support.microsoft.com/kb/3163023).

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE. Pour plus d'informations sur les variables de séquences de tâches de cette action de séquence de tâches, consultez [Variables d’action de séquence de tâches Installer les mises à jour logicielles](task-sequence-action-variables.md#BKMK_InstallSoftwareUpdates).

 > [!NOTE]
 > Vous pouvez utiliser les variables intégrées SMSTSMPListRequestTimeoutEnabled et SMSTSMPListRequestTimeout pour activer et spécifier le délai d’attente (en millisecondes) d’une séquence de tâche avant qu’elle tente à nouveau d’installer une application ou une mise à jour logicielle après l’échec de la récupération de la liste de points de gestion auprès des services de localisation. Pour plus d’informations, consultez [Variables intégrées de séquence de tâches](task-sequence-built-in-variables.md).

> [!NOTE]
>Sous l’onglet des options, vous pouvez configurer une nouvelle tentative de cette séquence de tâches si l’ordinateur redémarre de façon inattendue. Par exemple, une installation de mise à jour logicielle qui redémarre automatiquement l’ordinateur. À compter de Configuration Manager 1602, vous pouvez configurer la variable SMSTSWaitForSecondReboot pour spécifier le temps (en secondes) pendant lequel la séquence de tâches doit rester suspendue après le redémarrage de l’ordinateur lors de l’installation de mises à jour logicielles. Pour plus d’informations, consultez [Variables intégrées de séquence de tâches](task-sequence-built-in-variables.md).

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Indiquez qu'il faut réessayer cette étape si l'ordinateur redémarre de façon inattendue. Vous pouvez également spécifier le nombre de nouvelles tentatives après un redémarrage.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Nécessaires pour l’installation – Mises à jour logicielles obligatoires seulement**  
 Sélectionnez cette option pour installer toutes les mises à jour logicielles signalées dans Configuration Manager comme étant obligatoires pour les ordinateurs de destination qui reçoivent la séquence de tâches. Les mises à jour logicielles obligatoires possèdent des échéances d'installation définies par l'administrateur.  

 **Disponibles pour l’installation – Toutes les mises à jour logicielles**  
 Sélectionnez cette option pour installer toutes les mises à jour logicielles disponibles ciblant le regroupement Configuration Manager appelé à recevoir la séquence de tâches. Toutes les mises à jour logicielles disponibles seront installées sur les ordinateurs de destination.  

 **Évaluer les mises à jour logicielles à partir des résultats d’analyse en mémoire cache**  
À compter de Configuration Manager version 1606, vous pouvez effectuer une analyse complète des mises à jour logicielles au lieu d’utiliser les résultats d’analyse en mémoire cache. Par défaut, la séquence de tâches utilise les résultats mis en cache. Vous pouvez décocher la case pour que le client se connecte au point de mise à jour logicielle pour traiter et télécharger le dernier catalogue de mises à jour logicielles. Vous pouvez sélectionnez cette option quand vous utilisez une séquence de tâches pour [capturer et créer une image de système d’exploitation](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md), où vous savez qu’il y aura un grand nombre de mises à jour logicielles, surtout si la plupart auront des dépendances (besoin d’installer X avant qu’Y n’apparaisse comme applicable). Quand vous désactivez ce paramètre et que vous déployez la séquence de tâches sur un grand nombre de clients, ils se connectent tous au point de mise à jour logicielle en même temps. Cela peut entraîner des problèmes de performances pendant le processus et le téléchargement du catalogue. Dans la plupart des cas, nous vous recommandons d’utiliser le paramètre par défaut.

Une nouvelle variable de séquence de tâches, SMSTSSoftwareUpdateScanTimeout, a été introduite dans Configuration Manager version 1606 pour vous permettre de contrôler le délai d’attente pour la recherche des mises à jour logicielles pendant l’étape Installer les mises à jour logicielles. La valeur par défaut est de 30 minutes. Pour plus d’informations, consultez [Variables intégrées de séquence de tâches](task-sequence-built-in-variables.md).


##  <a name="a-namebkmkjoindomainorworkgroupa-join-domain-or-workgroup"></a><a name="BKMK_JoinDomainorWorkgroup"></a> Joindre le domaine ou le groupe de travail  
 L'étape de séquence de tâches **Joindre le domaine ou le groupe de travail** permet d'ajouter l'ordinateur de destination à un groupe de travail ou à un domaine.  

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE. Pour plus d'informations sur les variables de séquences de tâches de cette action de séquence de tâches, consultez [Variables de l’action de séquence de tâches Joindre le domaine ou le groupe de travail](task-sequence-action-variables.md#BKMK_JoinDomainWorkgroup).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Joindre un groupe de travail**  
 Sélectionnez cette option pour que l'ordinateur de destination fasse partie du groupe de travail spécifié. S'il est actuellement membre d'un domaine, la sélection de cette option le fera redémarrer.  

 **Joindre un domaine**  
 Sélectionnez cette option pour que l'ordinateur de destination fasse partie du domaine spécifié.  

 Facultatif : entrez ou accédez à une unité d'organisation du domaine spécifié pour que l'ordinateur s'y joigne. Si celui-ci est actuellement membre d'un autre domaine ou groupe de travail, cela le fera redémarrer. Si l'ordinateur est déjà membre d'une autre unité d'organisation, les services de domaine Active Directory ne vous permettent pas de modifier l'unité d'organisation et ce paramètre est ignoré.  

 **Entrez le compte autorisé à joindre le domaine**  
 Cliquez sur **Définir** pour entrer un compte et un mot de passe ayant les autorisations pour joindre le domaine. Le compte doit être entré au format suivant :  

 *Domaine\compte*  

## <a name="a-namebkmkprepareconfigmgrclientforcapturea-prepare-configmgr-client-for-capture"></a><a name="BKMK_PrepareConfigMgrClientforCapture"></a> Préparer le client ConfigMgr pour capture  
Utilisez l’étape **Préparer le client ConfigMgr pour capture** pour supprimer le client Configuration Manager ou configurer le client sur l’ordinateur de référence afin de le préparer pour la capture pendant le processus de création d’image.

À partir de Configuration Manager version 1610, l’étape de préparation du client ConfigMgr supprime complètement le client Configuration Manager, au lieu de supprimer uniquement des informations clés. Lorsque la séquence de tâches déploie l’image capturée du système d’exploitation, elle installe un nouveau client Configuration Manager chaque fois.  

Avant Configuration Manager version 1610, cette étape effectuait les tâches suivantes :  

-   Supprime du fichier smscfg.ini présent dans le répertoire Windows la section des propriétés de configuration du client. Celles-ci comprennent des informations spécifiques au client, par exemple le GUID Configuration Manager, ainsi que d’autres identificateurs clients.  

-   Supprime tous les certificats d’ordinateur SMS ou Configuration Manager.  

-   Supprime le cache du client Configuration Manager.  

-   Efface la variable de site attribuée au client Configuration Manager.  

-   Supprime toutes les stratégies Configuration Manager locales.  

-   Supprime la clé racine approuvée du client Configuration Manager.  

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE.  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

##  <a name="a-namebkmkpreparewindowsforcapturea-prepare-windows-for-capture"></a><a name="BKMK_PrepareWindowsforCapture"></a> Préparer Windows pour capture  
 Utilisez l'étape de séquence de tâches **Préparer Windows pour capture** pour spécifier les options Sysprep à utiliser lors de la capture d'une image de système d'exploitation sur l'ordinateur de référence. Cette action de séquence de tâches exécute Sysprep, puis redémarre l'ordinateur dans l'image de démarrage Windows PE spécifiée pour la séquence de tâches. L'ordinateur de référence ne doit pas être lié à un domaine pour que cette action s'effectue correctement.  

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE. Pour plus d'informations sur les variables de séquences de tâches de cette action de séquence de tâches, consultez [Variables d’action de séquence de tâches Préparer Windows pour capture](task-sequence-action-variables.md#BKMK_PrepareWindowsCapture).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Créer automatiquement la liste des pilotes de stockage de masse**  
 Sélectionnez cette option pour demander à Sysprep de générer automatiquement une liste de pilotes de stockage de masse à partir de l'ordinateur de référence. Cette option active l'option des pilotes de stockage de masse dans le fichier sysprep.inf sur l'ordinateur de référence. Pour plus d'informations à propos de ce paramètre, reportez-vous à la documentation de Sysprep.  

 **Ne pas réinitialiser l’indicateur d’activation**  
 Choisissez cette option pour empêcher Sysprep de réinitialiser l'indicateur d'activation du produit.  

##  <a name="a-namebkmkpreprovisionbitlockera-pre-provision-bitlocker"></a><a name="BKMK_PreProvisionBitLocker"></a> Préconfigurer BitLocker  
 Utilisez l'étape de séquence de tâches **Préconfigurer BitLocker** pour activer BitLocker sur un lecteur dans Windows PE. Seul l'espace disque utilisé étant chiffré, l'opération de chiffrement est beaucoup plus rapide. Vous appliquez les options de gestion de clés à l'aide de l'étape de séquence de tâches [Activer BitLocker](#BKMK_EnableBitLocker) une fois le système d'exploitation installé. Cette étape est exécutée uniquement sous Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard.  

> [!IMPORTANT]  
>  Pour préconfigurer BitLocker, vous devez déployer au minimum le système d'exploitation Windows 7 et le module de plateforme sécurisée doit être pris en charge et activé sur l'ordinateur.  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Spécifiez un nom court défini par l'utilisateur qui décrit l'action entreprise à cette étape.  

 **Description**  
 Spécifiez des informations détaillées sur l'action effectuée lors de cette étape.  

 **Appliquer BitLocker au lecteur spécifié**  
 Spécifiez le lecteur pour lequel vous souhaitez activer BitLocker. Seul l'espace utilisé sur le lecteur est chiffré.  

 **Ignorer cette étape pour les ordinateurs n’ayant pas un module de plateforme sécurisée ou lorsque celui-ci n’est pas activé**  
 Sélectionnez cette option pour ignorer le chiffrement de lecteur quand le matériel ne prend pas en charge le module de plateforme sécurisée ou quand celui-ci n'est pas activé. Par exemple, vous pouvez utiliser cette option lorsque vous déployez un système d'exploitation sur une machine virtuelle.  

##  <a name="a-namebkmkreleasestatestorea-release-state-store"></a><a name="BKMK_ReleaseStateStore"></a> Libérer le magasin d’état  
 Utilisez l'étape de séquence de tâches **Libérer le magasin d'état** pour informer le point de migration d'état que l'opération de capture ou de restauration est terminée. Cette étape est utilisée avec les étapes de séquences de tâches **Demander le magasin d'état**, **Capturer l'état utilisateur**et **Restaurer l'état utilisateur** pour migrer les données sur l'état de l'utilisateur à l'aide d'un point de migration de l'état et de l'outil de migration de l'état utilisateur (USMT).  

 Pour plus d’informations sur la gestion de l’état utilisateur pendant le déploiement de systèmes d’exploitation, consultez [Gérer l’état utilisateur](../get-started/manage-user-state.md).  

 Si vous avez demandé l'accès à un point de migration d'état pour capturer l'état utilisateur dans l'étape de séquence de tâches **Demander le magasin d'état**  , cette étape informe le point de migration d'état que le processus de capture est terminé et que les données sur l'état utilisateur peuvent être restaurées. Le point de migration de l'état définit les autorisations de contrôle d'accès de l'état de capture pour qu'il ne soit accessible (en lecture seule) qu'à l'ordinateur de restauration.  

 Si vous avez demandé l'accès à un point de migration de l'état pour restaurer l'état utilisateur dans l'étape de la séquence de tâches **Demander le magasin d'état** , cette étape informe le point de migration de l'état que le processus de restauration est terminé. À ce stade, les paramètres de conservation que vous avez définis pour le point de migration de l'état sont activés.  

> [!IMPORTANT]  
>  Une bonne pratique consiste à définir **Continuer en cas d'erreur** pour toutes les étapes de séquence de tâches situées entre les étapes **Demander le magasin d'état** et **Libérer le magasin d'état** afin que chaque action de séquence de tâches **Demander le magasin d'état** corresponde à une action de séquence de tâches **Libérer le magasin d'état** .  

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE. Pour plus d'informations sur les variables de séquences de tâches de cette action de séquence de tâches, consultez [Variables d’action de séquence de tâches Libérer le magasin d’état](task-sequence-action-variables.md#BKMK_ReleaseStateStore).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

##  <a name="a-namebkmkrequeststatestorea-request-state-store"></a><a name="BKMK_RequestStateStore"></a> Demander le magasin d’état  
 L'étape de séquence de tâches **Demander le magasin d'état** permet de demander l'accès à un point de migration d'état lors de la capture ou de la restauration de l'état d'un ordinateur.  

 Pour plus d’informations sur la gestion de l’état utilisateur pendant le déploiement de systèmes d’exploitation, consultez [Gérer l’état utilisateur](../get-started/manage-user-state.md).  

 Vous pouvez utiliser l'étape de séquence de tâches **Demander le magasin d'état** avec les étapes de séquences de tâches **Libérer le magasin d'état**, **Capturer l'état utilisateur**et **Restaurer l'état utilisateur** pour migrer l'état de l'ordinateur à l'aide d'un point de migration de l'état et de l'outil de migration de l'état utilisateur (User State Migration Tool, USMT).  

> [!NOTE]  
>  Si vous venez d'établir un nouveau rôle de site de point de migration d'état (SMP), vous devez attendre jusqu'à une heure avant que celui-ci soit disponible pour le stockage de l'état utilisateur. Pour accélérer ce processus, vous pouvez ajuster un paramètre de propriété du point de migration d'état afin de déclencher une mise à jour du fichier de contrôle de site.  

 Cette étape de séquence de tâches s'exécute dans un système d'exploitation standard et dans Windows PE pour USMT en mode hors connexion. Pour plus d’informations sur les variables de séquence de tâches de cette action, consultez [Variables d’action de séquence de tâches Demander le magasin d’état](task-sequence-action-variables.md#BKMK_RequestState).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Capturer l’état à partir de l’ordinateur**  
 Localise un point de migration d'état qui répond aux conditions de configuration minimale requise configurées dans les paramètres de point de migration d'état (nombre maximal de clients et espace disque disponible minimal) mais ne garantie pas la disponibilité de l'espace au moment de la migration. La sélection de cette option fera une demande d'accès à un point de migration d'état afin de capturer un état et des paramètres utilisateur sur un ordinateur cible.  

 Si plusieurs points de migration d’état sont activés sur le site Configuration Manager, cette étape de séquence de tâches permet de rechercher un point de migration d’état qui dispose d’espace disque en demandant au point de gestion du site une liste des points de migration d’état, puis en évaluant chaque point afin d’en trouver un qui réponde aux conditions de configuration minimale requise.  

 **Restaurer l’état à partir d’un autre ordinateur**  
 Sélectionnez cette option si vous souhaitez accéder à un point de migration d'état pour restaurer un état et des paramètres utilisateur précédemment capturés sur un ordinateur de destination.  

 Si le site Configuration Manager comporte plusieurs points de migration d’état, cette étape de séquence de tâches recherche le point de migration d’état sur lequel l’état de l’ordinateur de destination a été stocké.  

 **Nombre de tentatives**  
 Nombre de fois que cette étape de séquence de tâches tente de rechercher un point de migration d'état approprié avant d'échouer.  

 **Délai de nouvelle tentative (en secondes)**  
 Durée en secondes pendant laquelle l'étape de séquence de tâches attend entre chaque tentative.  

 **Si le compte d’ordinateur ne parvient pas à se connecter au magasin d’état, utiliser le compte d’accès réseau.**  
 Indique que les informations d’identification du compte d’accès réseau de Configuration Manager sont utilisées pour se connecter au point de migration d’état si le client Configuration Manager ne parvient pas à accéder au magasin d’état SMP via le compte d’ordinateur. Cette option est moins sécurisée car d'autres ordinateurs peuvent utiliser le compte d'accès réseau pour accéder à votre état stocké, mais elle peut s'avérer nécessaire si l'ordinateur de destination n'est pas lié à un domaine.  

##  <a name="a-namebkmkrestartcomputera-restart-computer"></a><a name="BKMK_RestartComputer"></a> Redémarrer l’ordinateur  
 L'étape de séquence de tâches **Redémarrer l'ordinateur** permet de redémarrer l'ordinateur exécutant la séquence de tâches. Ceci fait, l'ordinateur passe automatiquement à l'étape suivante dans la séquence.  

 Cette étape peut être exécutée dans un système d'exploitation standard ou Windows PE. Pour plus d’informations sur les variables de séquence de tâches de cette action, consultez [Variables d’action de séquence de tâches Redémarrer l’ordinateur](task-sequence-action-variables.md#BKMK_RestartComputer).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **L’image de démarrage attribuée à cette séquence de tâches**  
 Sélectionnez cette option pour que l'ordinateur de destination utilise l'image de démarrage qui est attribuée à la séquence de tâches. L'image de démarrage sera utilisée pour exécuter des étapes de séquence de tâches ultérieures qui sont exécutées dans Windows PE.  

 **Le système d’exploitation par défaut installé actuellement**  
 Sélectionnez cette option pour que l'ordinateur de destination redémarre sous le système d'exploitation installé.  

 **Notifier l’utilisateur avant de redémarrer**  
 Sélectionnez cette option pour afficher une notification indiquant à l'utilisateur que l'ordinateur de destination sera redémarré. Cette option est activée par défaut.  

 **Message de notification**  
 Entrez un message de notification qui s'affiche à l'attention de l'utilisateur avant le redémarrage de l'ordinateur de destination.  

 **Délai d’affichage du message**  
 Indiquez la durée en secondes dont dispose l'utilisateur avant le redémarrage de l'ordinateur de destination. Elle est de&60; (soixante) secondes par défaut.  

##  <a name="a-namebkmkrestoreuserstatea-restore-user-state"></a><a name="BKMK_RestoreUserState"></a> Restaurer l’état utilisateur  
 Utilisez l'étape de séquence de tâches **Restaurer l'état utilisateur** pour lancer l'outil de migration de l'état utilisateur (USMT) afin de restaurer l'état et les paramètres utilisateur sur l'ordinateur de destination. Cette étape de séquence de tâches est utilisée avec l'étape de séquence de tâches **Capturer l'état utilisateur** .  

 Pour plus d’informations sur la gestion de l’état utilisateur pendant le déploiement de systèmes d’exploitation, consultez [Gérer l’état utilisateur](../get-started/manage-user-state.md).  

 Vous pouvez aussi utiliser l’étape de séquence de tâches **Restaurer l’état utilisateur** avec les étapes de séquence de tâches **Demander le magasin d’état** et **Libérer le magasin d’état** si vous voulez enregistrer les paramètres d’état sur un point de migration d’état ou les restaurer à partir d’un point de migration d’état dans le site Configuration Manager. Dans USMT 3.0 et versions supérieures, cette option déchiffre toujours le magasin d’état USMT au moyen d’une clé de chiffrement générée et gérée par Configuration Manager.  

 L'étape de séquence de tâches **Restaurer l'état utilisateur** permet de contrôler un sous-ensemble des options USMT les plus couramment utilisées. D'autres options de ligne de commande peuvent être spécifiées au moyen de la variable de séquence de tâches OSDMigrateAdditionalRestoreOptions.  

> [!IMPORTANT]  
>  Si vous utilisez l’étape de séquence de tâches **Restaurer l’état utilisateur** dans un but non lié à un scénario de déploiement de système d’exploitation, ajoutez immédiatement l’étape de séquence de tâches [Redémarrage de l'ordinateur](#BKMK_RestartComputer) après l’étape de séquence de tâches **Restaurer l’état utilisateur** .  

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE. Pour plus d’informations sur les variables de séquence de tâches de cette action, consultez [Variables d’action de séquence de tâches Restaurer l’état utilisateur](task-sequence-action-variables.md#BKMK_RestoreUserState).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Spécifie un nom court défini par l'utilisateur qui décrit l'action entreprise à cette étape.  

 **Description**  
 Fournit des informations plus détaillées sur l'action effectuée dans cette étape.  

 **Package de l’outil de migration de l’état utilisateur**  
 Entrez le package Configuration Manager qui contient la version de l’outil USMT pour cette étape afin de l’utiliser pendant la restauration des paramètres et de l’état utilisateur. Ce package ne requiert pas de programme. Lorsque l'étape de séquence de tâches est exécutée, la séquence de tâches utilise la version de l'outil de migration de l'état utilisateur du package que vous indiquez. Spécifiez un package contenant la version 32 bits ou x64 d'USMT en fonction de l'architecture du système d'exploitation vers lequel vous restaurez l'état.  

 **Restaurer tous les profils utilisateur capturés présentant des options standard**  
 Restaure les profils utilisateur capturés qui présentent des options standard. Pour personnaliser les options à restaurer, sélectionnez **Personnaliser la façon dont les profils utilisateur sont capturés**.  

 **Personnaliser la restauration des profils utilisateur**  
 Permet de personnaliser les fichiers à restaurer sur l'ordinateur de destination. Cliquez sur **Fichiers** pour spécifier les fichiers de configuration du package USMT à utiliser pour restaurer les profils utilisateur. Pour ajouter un fichier de configuration, entrez le nom du fichier dans le champ **Nom de fichier** , puis cliquez sur **Ajouter**. Les fichiers de configuration qui seront utilisés pour cette opération sont présentés dans le volet Fichiers. Le fichier .xml que vous spécifiez définit le fichier utilisateur à restaurer.  

 **Restaurer les profils utilisateur de l’ordinateur local**  
 Restaure les profils utilisateur de l'ordinateur local (c.-à-d. les profils autre que les profils utilisateur de domaine). Vous devez attribuer de nouveaux mots de passe aux comptes d'utilisateurs locaux car les mots de passe d'origine des comptes d'utilisateurs locaux ne peuvent pas être migrés. Entrez le nouveau mot de passe dans le champ **Mot de passe** , puis confirmez le mot de passe dans le champ **Confirmer le mot de passe** .  

 **Continuer si certains fichiers ne peuvent pas être restaurés**  
 Poursuit le processus de restauration de l'état utilisateur et des paramètres correspondants, même si certains fichiers ne peuvent pas être restaurés. Cette option est activée par défaut. Si vous la désactivez et que des erreurs surviennent lors de la restauration des fichiers, l'étape de la séquence de tâches s'interrompt immédiatement en erreur et tous les fichiers ne seront pas restaurés.  

 **Activer la journalisation documentée**  
 Activez cette option pour générer des informations de fichiers journaux plus détaillées. Lors de la restauration de l'état, le fichier Loadstate.log est généré et stocké par défaut dans le dossier de journalisation de la séquence de tâches du dossier \windows\system32\ccm\logs .  

##  <a name="a-namebkmkruncommandlinea-run-command-line"></a><a name="BKMK_RunCommandLine"></a> Exécuter la ligne de commande  
 L'étape de séquence de tâches **Exécuter la ligne de commande** permet d'exécuter une ligne de commande spécifiée.  

 Cette étape peut être exécutée dans un système d'exploitation standard ou Windows PE. Pour plus d'informations sur les variables de séquences de tâches de cette action de séquence de tâches, consultez [Variables d’action de séquence de tâches Exécuter la ligne de commande](task-sequence-action-variables.md#BKMK_RunCommand).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Spécifie un nom court, défini par l'utilisateur, qui décrit la ligne de commande exécutée.  

 **Description**  
 Spécifie des informations plus détaillées sur la ligne de commande exécutée.  

 **Ligne de commande**  
 Indique la ligne de commande exécutée. Ce champ doit obligatoirement être renseigné. Le fait d’inclure des extensions de noms de fichiers est une bonne pratique, par exemple, .vbs et .exe. Intégrez tous les fichiers de paramètres requis, les options des lignes de commande ou les commutateurs.  

 Si le nom de fichier est spécifié sans extension, Configuration Manager essaie les extensions .com, .exe et .bat. Si le nom de fichier a une extension, mais qu’il ne s’agit pas d’un fichier exécutable, Configuration Manager essaie d’appliquer une association locale. Par exemple, si la ligne de commande est readme.gif, Configuration Manager démarre l’application spécifiée sur l’ordinateur de destination pour ouvrir les fichiers .gif.  

 Exemples :  

 **setup.exe /a**  

 **cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat**  

> [!NOTE]  
>  Les actions de ligne de commande comme la redirection de la sortie, la canalisation ou la copie (voir exemple précédent) doivent être précédées de la commande **cmd.exe /c** pour s’exécuter correctement.  

 **Désactiver la redirection du système de fichiers 64 bits**  
 Par défaut, dans un système d'exploitation 64 bits, l'exécutable de la ligne de commande est localisé et exécuté au moyen d'un redirecteur de système de fichiers WOW64, ce qui permet de trouver les versions 32 bits des exécutables et les DLL du système d'exploitation.  La sélection de cette option désactive l'utilisation du redirecteur de système de fichiers WOW64, ce qui permet de trouver les versions natives 64 bits des exécutables et les DLL du système d'exploitation.  Cette option est sans effet dans un système d'exploitation 32 bits.  

 **Démarrer dans**  
 Spécifie le dossier exécutable pour le programme, comprenant jusqu'à 127 caractères. Ce dossier peut être un chemin d'accès absolu sur l'ordinateur de destination ou un chemin d'accès relatif au dossier du point de distribution qui contient le package. Ce champ est facultatif.  

 Exemples :  

 **c:\officexp**  

 **i386**  

> [!NOTE]  
>  Le bouton **Parcourir** permet de rechercher des fichiers et des dossiers sur l'ordinateur local. Tous les éléments que vous sélectionnez de cette manière doivent également exister sur l'ordinateur de destination au même emplacement et avec les mêmes noms de fichiers et de dossiers.  

 **Package**  
 Quand, sur la ligne de commande, vous spécifiez des fichiers ou des programmes qui ne sont pas déjà présents sur l’ordinateur de destination, sélectionnez cette option pour spécifier le package Configuration Manager qui contient les fichiers appropriés. Le package n'exige pas de programme. Cette option n'est pas nécessaire si le fichier spécifié existe sur l'ordinateur de destination.  

 **Délai**  
 Permet de spécifier une valeur qui représente le délai d’exécution de la ligne de commande autorisé par Configuration Manager. Cette valeur est comprise entre 1 et 999 minutes. La valeur par défaut est 15 minutes.  

 Cette option est désactivée par défaut.  

> [!IMPORTANT]  
>  Si vous entrez une durée insuffisante au bon déroulement de l'étape Exécuter la ligne de commande de la séquence de tâches, cette étape échoue et risque d'entraîner l'échec de toute la séquence de tâches, en fonction des autres paramètres de contrôle. Si le délai expire, Configuration Manager met un terme au processus en ligne de commande.  

 **Exécuter cette étape en tant que compte suivant**  
 Spécifie que la ligne de commande est exécutée en tant que compte d'utilisateur Windows et non en tant que compte système local.  

> [!NOTE]  
>  Quand vous spécifiez un autre compte pour cette étape et que celle-ci intervient après une étape d’installation du système d’exploitation, le compte doit être ajouté à l’ordinateur pour permettre l’exécution de scripts ou de commandes simples, et le profil du compte d’utilisateur Windows doit être restauré pour exécuter des programmes plus complexes, tels que des fichiers MSI.  

 **Compte**  
 Spécifie le compte d'utilisateur Windows Exécuter en tant que pour la ligne de commande de la séquence de tâches à exécuter par cette action. La ligne de commande s'exécute avec les autorisations du compte spécifié Cliquez sur **Définir** pour spécifier le compte de domaine ou le compte d'utilisateur local.  

> [!IMPORTANT]  
>  Si une action de séquence de tâches **Exécuter la ligne de commande** spécifiant un compte d'utilisateur est exécutée dans Windows PE, elle échoue car ce dernier ne peut être associé à un domaine. L'échec est enregistré dans le fichier smsts.log.  

##  <a name="a-namebkmkrunpowershellscripta-run-powershell-script"></a><a name="BKMK_RunPowerShellScript"></a> Exécuter le script PowerShell  
 Utilisez l'étape de séquence de tâches **Exécuter le script PowerShell** pour exécuter un script PowerShell spécifié.  

 Cette étape peut être exécutée dans un système d'exploitation standard ou Windows PE. Pour exécuter cette étape dans Windows PE, PowerShell doit être activé dans l'image de démarrage. Vous pouvez activer Windows PowerShell (WinPE-PowerShell) à partir de l'onglet **Composants facultatifs** dans les propriétés de l'image de démarrage. Pour plus d’informations sur la modification d’une image de démarrage, consultez [Gérer les images de démarrage](../get-started/manage-boot-images.md).  

> [!NOTE]  
>  PowerShell n'est pas activé par défaut sur les systèmes d'exploitation Windows Embedded.  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Spécifie un nom court, défini par l'utilisateur, qui décrit la ligne de commande exécutée.  

 **Description**  
 Spécifie des informations plus détaillées sur la ligne de commande exécutée.  

 **Package**  
 Indique le package Configuration Manager qui contient le script PowerShell. Un package peut contenir plusieurs scripts PowerShell.  

 **Nom du script**  
 Spécifie le nom du script PowerShell à exécuter. Ce champ doit obligatoirement être renseigné.  

 **Paramètres**  
 Spécifie les paramètres à passer au script Windows PowerShell. Configurez les paramètres comme si vous les ajoutiez au script Windows PowerShell à partir d'une ligne de commande.  

> [!IMPORTANT]  
>  Spécifiez les paramètres consommés par le script, et non pour la ligne de commande Windows PowerShell.  
>   
>  L'exemple suivant contient des paramètres valides :  
>   
>  **-MyParameter1 MyValue1 -MyParameter2 MyValue2**  
>   
>  L'exemple suivant contient des paramètres non valides. Les éléments en gras sont des paramètres de ligne de commande Windows PowerShell (-nologo et -executionpolicy unrestricted). Ils ne sont pas consommés par le script.  
>   
>  **-nologo-executionpolicy unrestricted-File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2**  

 **Stratégie d'exécution de PowerShell**  
 L'option Stratégie d'exécution de PowerShell vous permet de déterminer les scripts Windows PowerShell (le cas échéant) qui pourront s'exécuter sur l'ordinateur. Choisissez l'une des stratégies d'exécution suivantes :  

-   **AllSigned**: seuls les scripts signés par un éditeur approuvé peuvent être exécutés.  

-   **Undefined**: aucune stratégie d’exécution n’est définie. .  

-   **Bypass**: charge tous les fichiers de configuration et exécute tous les scripts. Si vous exécutez un script non signé qui a été téléchargé depuis Internet, vous n'êtes pas invité à fournir d'autorisation avant son exécution.  

> [!IMPORTANT]  
>  PowerShell 1.0 ne prend pas en charge les stratégies d'exécution Non défini et Ignorer.  

##  <a name="a-namebkmksetdynamicvariablesa-set-dynamic-variables"></a><a name="BKMK_SetDynamicVariables"></a> Définir des variables dynamiques  
 Utilisez l'étape de séquence de tâches **Définir des variables dynamique** pour effectuer les opérations suivantes :  

1.  Recueillir des informations à partir de l'ordinateur et de l'environnement où il réside, puis définir des variables de séquence de tâches spécifiées avec les informations.  

2.  Évaluer les règles définies et définir des variables de séquence de tâches en fonction des variables et des valeurs configurées pour les règles avec la valeur true.  

 La séquence de tâches définit automatiquement les variables de séquence de tâches en lecture seule suivantes :  

 -   &#95;SMSTSMake  

 -   &#95;SMSTSModel  

 -   &#95;SMSTSMacAddresses  

 -   &#95;SMSTSIPAddresses  

 -   &#95;SMSTSSerialNumber  

 -   &#95;SMSTSAssetTag  

 -   &#95;SMSTSUUID  

 Cette étape peut être exécutée dans un système d'exploitation standard ou Windows PE. Pour plus d’informations sur les variables de séquence de tâches, consultez [Variables d’action de séquence de tâches](task-sequence-action-variables.md).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

**Nom**  
 Nom court défini par l'utilisateur pour cette étape de séquence de tâches.  

**Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

**Règles dynamiques et variables**  
 Pour définir une variable dynamique à utiliser dans la séquence de tâches, vous pouvez ajouter une règle, puis spécifier une valeur pour chaque variable que vous spécifiez pour la règle ou ajouter une ou plusieurs variables à définir sans ajouter de règle. Lorsque vous ajoutez une règle, vous pouvez choisir parmi les catégories suivantes :  

 -   **Ordinateur**: utilisez cette catégorie de règle pour évaluer des valeurs d’étiquette d’inventaire, d’UUID, de numéro de série ou d’adresse MAC. Vous pouvez définir plusieurs valeurs et si l'une d'elles est true, la règle est évaluée comme vraie. Par exemple, la règle suivante est évaluée comme vraie si le numéro de série est 5892087, que l'adresse MAC soit égale ou non à 26-78-13-5A-A4-22.  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

-   **Emplacement**: utilisez cette catégorie de règle pour évaluer des valeurs de passerelle par défaut.  

-   **Marque et modèle**: utilisez cette catégorie de règle pour évaluer les valeurs de marque et de modèle d’un ordinateur. La marque et le modèle doivent tous deux être évalués comme vrais pour que la règle soit évaluée comme vraie.   

    À partir de Configuration Manager version 1610, vous pouvez spécifier un astérisque (*****) et un point d’interrogation (**?**) comme caractères génériques, où ***** correspond à plusieurs caractères et **?** correspond à un caractère unique. Par exemple, la chaîne « DELL*900? » correspond à DELL-ABC-9001 et DELL9009.

-   **Variable de séquence de tâches**: utilisez cette catégorie de règle pour ajouter une variable de séquence de tâches, une condition et une valeur à évaluer. La règle est évaluée comme vraie quand la valeur définie pour la variable remplit la condition spécifiée.  

Vous pouvez spécifier une ou plusieurs variables qui seront définies pour une règle évaluée comme vraie ou définir des variables sans utiliser de règle. Vous pouvez sélectionner parmi des variables existantes ou créer une variable personnalisée.  

 -   **Variables de séquence de tâches existantes**: utilisez ce paramètre pour sélectionner une ou plusieurs variables dans la liste des variables de séquence de tâches existantes. Les variables tableau ne peuvent pas être sélectionnées.  

 -   **Variables de séquence de tâches personnalisées**: utilisez ce paramètre pour définir une variable de séquence de tâches personnalisée. Vous pouvez également spécifier une variable de séquence de tâches existante. Cela est utile pour spécifier un tableau de variables existant, tel qu'OSDAdapter, car les tableaux de variables ne figurent pas dans la liste des variables de séquence de tâches existantes.  

Après avoir sélectionné les variables pour une règle, vous devez fournir une valeur pour chaque variable. Lorsque la règle est évaluée comme vraie, la variable est définie à la valeur spécifiée. Pour chaque variable, vous pouvez sélectionner **Valeur secrète** pour masquer la valeur de la variable. Par défaut, certaines variables existantes (telles que la variable de séquence de tâches OSDCaptureAccountPassword) masquent les valeurs.  

> [!IMPORTANT]  
>  Quand vous importez une séquence de tâches lors de l'étape Définir des variables dynamiques et que l'option **Valeur secrète** est sélectionnée pour la valeur de la variable, la valeur est supprimée lorsque vous importez la séquence de tâches. Ainsi, vous devez réentrer la valeur de la variable dynamique après avoir importé la séquence de tâches.  

##  <a name="a-namebkmksettasksequencevariablea-set-task-sequence-variable"></a><a name="BKMK_SetTaskSequenceVariable"></a> Définir la variable de séquence de tâches  
 Utilisez l'étape de séquence de tâches **Définir la variable de séquence de tâches** pour définir la valeur d'une variable qui est utilisée avec la séquence de tâches.  

 Cette étape peut être exécutée dans un système d'exploitation standard ou Windows PE. Les variables de séquence de tâches sont lues par les actions et en déterminent le comportement. Pour plus d’informations sur les variables de séquence de tâches spécifiques, consultez [Variables d’action de séquence de tâches](task-sequence-action-variables.md).  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur pour cette étape de séquence de tâches.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Variable de séquence de tâches**  
 Nom défini par l'utilisateur pour la variable de la séquence de tâches.  

 **Valeur**  
 Valeur associée à la variable de la séquence de tâches. La valeur peut être une autre variable de séquence de tâches dans la syntaxe %<nom_variable\>%.  

##  <a name="a-namebkmksetupwindowsandconfigmgra-setup-windows-and-configmgr"></a><a name="BKMK_SetupWindowsandConfigMgr"></a> Configurer Windows et ConfigMgr  
 Utilisez l'étape de séquence de tâches **Configurer Windows et ConfigMgr** pour effectuer la transition de Windows PE vers le nouveau système d'exploitation. Cette étape de séquence de tâches est obligatoire dans tout déploiement de système d'exploitation, elle installe le client Configuration Manager dans le nouveau système d’exploitation et prépare la poursuite de l’exécution de la séquence de tâches dans le nouveau système d’exploitation.  

 Cette étape est exécutée uniquement sous Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches de cette action de séquence de tâches, consultez [Variables d’action de séquence de tâches Configurer Windows et ConfigMgr](task-sequence-action-variables.md#BKMK_SetupWindows).  

 L’action de séquence de tâches **Configurer Windows et Configuration Manager** remplace les variables de répertoire de sysprep.inf ou unattend.xml, comme %WINDIR% et %ProgramFiles%, par le répertoire d’installation Windows°PE X:\Windows. Les variables de séquence de tâches spécifiées au moyen de ces variables d'environnement seront ignorées.  

 Utilisez cette étape de séquence de tâches pour effectuer les actions suivantes :  

1.  Préliminaires : Windows PE  

    1.  Effectue la substitution de variable de séquence de tâches dans le fichier unattend.xml.  

    2.  Télécharge le package qui contient le client Configuration Manager et le place dans l’image déployée.  

2.  Configuration de Windows  

    1.  Installation à base d'image.  

        1.  Désactive le client Configuration Manager dans l’image (autrement dit, le démarrage automatique est désactivé pour le service du client Configuration Manager).  

        2.  Met à jour le Registre dans l'image déployée pour garantir que le système d'exploitation déployé démarre en utilisant la même lettre de lecteur que celle figurant sur l'ordinateur de référence.  

        3.  Redémarre dans le système d'exploitation déployé.  

        4.  La mini-installation de Windows s'exécute en utilisant le fichier sysprep.inf ou unattend.xml spécifié précédemment et dont toutes les interactions avec l'utilisateur sont supprimées. Remarque : si **Appliquer les paramètres réseau** indique qu’il faut joindre un domaine, cette information se trouve dans le fichier sysprep.inf ou unattend.xml et la mini-installation de Windows effectue la jonction.  

    2.  Installation avec Setup.exe.  Exécute le fichier Setup.exe qui suit le processus d’installation de Windows classique :  

        1.  Copie le package d'installation du système d'exploitation spécifié dans une séquence de tâches **Appliquer le système d'exploitation** précédente sur le disque dur.  

        2.  Redémarre dans le système d'exploitation qui vient d'être déployé.  

        3.  La mini-installation de Windows s'exécute en utilisant le fichier sysprep.inf ou unattend.xml spécifié précédemment et dont tous les paramètres d'interface avec l'utilisateur sont supprimés. Remarque : si **Appliquer les paramètres réseau** indique qu’il faut joindre un domaine, cette information se trouve dans le fichier sysprep.inf ou unattend.xml et la mini-installation de Windows effectue la jonction.  

3.  Configurer le client Configuration Manager  

    1.  Une fois la mini-installation de Windows terminée, la séquence de tâches reprend à l’aide de setupcomplete.cmd.  

    2.  Active ou désactive le compte d'administrateur local en fonction de l'option sélectionnée dans l'étape **Appliquer les paramètres Windows** .  

    3.  Installe le client Configuration Manager en utilisant le package précédemment téléchargé (1.b) et les propriétés d’installation spécifiées dans l’éditeur de séquence de tâches. Le client est installé en « mode de préparation » afin de l'empêcher de traiter les requêtes des nouvelles stratégies avant la fin de la séquence de tâches.  

    4.  Attend que le client soit totalement opérationnel.  

    5.  Si l'ordinateur fonctionne dans un environnement doté de la protection d'accès réseau, le client vérifie l'existence de mises à jour requises et les installe afin qu'elles soient toutes présentes avant que la séquence de tâches continue son exécution.  

4.  La séquence de tâches continue son exécution en passant à l'étape suivante.  

> [!NOTE]  
>  L'action de séquence de tâches **Configurer Windows et ConfigMgr** est responsable de l'exécution de la stratégie de groupe sur l'ordinateur nouvellement installé. La stratégie de groupe est appliquée après la fin de la séquence de tâches.  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Ne sélectionnez pas l'option permettant de continuer la séquence de tâches si une erreur se produit pendant l'exécution de l'étape. Si une erreur se produit, la séquence de tâches échoue, que vous ayez sélectionné ou non ce paramètre.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Spécifie un nom court défini par l'utilisateur qui décrit l'action entreprise à cette étape.  

 **Description**  
 Spécifie des informations supplémentaires sur l'action effectuée à cette étape.  

 **Package client**  
 Indique le package d’installation du client Configuration Manager qui sera utilisé par cette séquence de tâches. Cliquez sur **Parcourir** et sélectionnez le package d’installation du client que vous souhaitez utiliser pour installer le client Configuration Manager.  

 **Utiliser le package client de préproduction quand il est disponible**  
 Spécifie que, si un package client de préproduction est disponible, la séquence de tâches l’utilise à la place du package client de production. En règle générale, le client de préproduction est une version plus récente testée dans l’environnement de production. Cliquez sur **Parcourir** et sélectionnez le package d’installation du client de préproduction que vous souhaitez utiliser pour installer le client Configuration Manager.  

 **Propriétés d’installation**  
 L'attribution de site et la configuration par défaut sont automatiquement spécifiées par l'action de la séquence de tâches. Ce champ permet de spécifier les propriétés d'installation supplémentaires à utiliser lorsque vous installez le client. Pour entrer plusieurs propriétés d'installation, séparez-les par un espace.  

 Vous pouvez spécifier des options de ligne de commande à utiliser lors de l'installation du client. Par exemple, vous pouvez entrer **/skipprereq: silverlight.exe** pour informer CCMSetup.exe de ne pas installer le composant requis Microsoft Silverlight. Pour plus d’informations sur les options de ligne de commande disponibles pour CCMSetup.exe, consultez [À propos des propriétés d’installation du client](../../core/clients/deploy/about-client-installation-properties.md).  

##  <a name="a-namebkmkupgradeosa-upgrade-operating-system"></a><a name="BKMK_UpgradeOS"></a> Mettre à niveau le système d’exploitation  
 Utilisez l’étape de séquence de tâches **Mettre à niveau le système d’exploitation** pour mettre à niveau un système d’exploitation Windows 7, Windows 8, Windows 8.1 ou Windows 10 existant vers Windows 10.  

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE.  

### <a name="details"></a>Détails  
 Dans l'onglet **Propriétés** pour cette étape, vous pouvez configurer les paramètres décrits dans cette section.  

 En outre, utilisez l'onglet **Options** pour effectuer les actions suivantes :  

-   Désactiver l'étape.  

-   Spécifier si la séquence de tâches continue en cas d'erreur pendant l'exécution de l'étape.  

-   Spécifier des conditions qui doivent être remplies pour que l'étape s'exécute.  

 **Nom**  
 Nom court défini par l'utilisateur qui décrit l'action effectuée dans cette étape.  

 **Description**  
 Informations plus détaillées sur l'action effectuée dans cette étape.  

 **Package de mise à niveau**  
 Sélectionnez cette option pour spécifier le package de mise à niveau de système d’exploitation Windows 10 à utiliser pour la mise à niveau.  

 **Chemin source**  
 Spécifie un chemin local ou réseau vers le support Windows 10 utilisé (correspond à l’option de ligne de commande /installFrom). Vous pouvez également spécifier une variable, comme %mycontentpath% ou %DPC01%. Quand vous utilisez une variable pour le chemin source, elle doit être spécifiée plus tôt dans la séquence de tâches. Par exemple, si vous utilisez l’étape [Télécharger le contenu du package](#BKMK_DownloadPackageContent) dans la séquence de tâches, vous pouvez spécifier une variable pour l’emplacement du package de mise à niveau du système d’exploitation. Ensuite, vous pouvez utiliser cette variable pour le chemin source de cette étape.  

 **Édition**  
 Spécifiez l’édition au sein du support du système d’exploitation à utiliser pour la mise à niveau.  

 **Clé du produit**  
 Spécifier la clé de produit à appliquer au processus de mise à niveau  

 **Fournir le contenu du pilote suivant à l’installation de Windows pendant la mise à niveau**  
 Sélectionnez ce paramètre pour ajouter des pilotes à l’ordinateur de destination pendant le processus de mise à niveau (correspond à l’option de ligne de commande /InstallDriver). Les pilotes doivent être compatibles avec Windows 10. Spécifiez l’une des options suivantes :  

-   **Package de pilotes** : cliquez sur **Parcourir** et sélectionnez un package de pilotes existant dans la liste.  

-   **Contenu intermédiaire** : sélectionnez cette option pour spécifier l’emplacement du package de pilotes. Vous pouvez spécifier un dossier local, un chemin réseau ou une variable de séquence de tâches. Quand vous utilisez une variable pour le chemin source, elle doit être spécifiée plus tôt dans la séquence de tâches. Par exemple, en utilisant l’étape [Télécharger le contenu du package](task-sequence-steps.md#BKMK_DownloadPackageContent).  

 **Délai d’expiration (minutes)**  
 Indique le nombre de minutes pendant lesquelles le programme d’installation doit s’exécuter avant que Configuration Manager fasse échouer l’étape de séquence de tâches.  

 **Effectuer une analyse de compatibilité d’installation de Windows sans démarrer la mise à niveau**  
 Spécifie l’exécution de l’analyse de compatibilité de l’installation de Windows sans démarrer le processus de mise à niveau (correspond à l’option de ligne de commande /Compat ScanOnly). Vous devez quand même déployer toute la source de d’installation quand vous utilisez cette option. Le programme d’installation renvoie un code de sortie suite à l’analyse. Le tableau suivant indique certains des codes de sortie les plus courants.  

|Code de sortie|Détails|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Aucun problème de compatibilité (« réussite »).|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0XC1900208)|Problèmes de compatibilité pouvant donner lieu à une action.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|Le choix de migration sélectionné n’est pas disponible. Par exemple, une mise à niveau depuis Entreprise vers Professionnel.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Non éligible pour Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0XC190020E)|Espace disque disponible insuffisant.|  

 Pour plus d’informations sur ce paramètre, consultez [Options de ligne de commande du programme d’installation de Windows](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx).  

 **Ignorer les messages de compatibilité révocables**  
 Spécifie que le programme d’installation a terminé l’installation, en ignorant tous les messages de compatibilité révocables (correspond à l’option de ligne de commande /Compat IgnoreWarning).  

 **Mettre à jour dynamiquement l’installation de Windows avec Windows Update**  
 Spécifie si le programme d’installation effectue les opérations de mise à jour dynamique, comme la recherche, le téléchargement et l’installation des mises à jour (correspond à l’option de ligne de commande /DynamicUpdate). Ce paramètre n’est pas compatible avec les mises à jour logicielles Configuration Manager, mais il peut être activé quand vous gérez les mises à jour à l’aide de WSUS (autonome) ou Windows Update.  

 **Remplacer la stratégie et utiliser Microsoft Update par défaut**: sélectionnez ce paramètre pour remplacer temporairement la stratégie locale, en temps réel, pour exécuter des opérations de mise à jour dynamique et permettre à l’ordinateur d’obtenir des mises à jour par le biais de Windows Update.  



<!--HONumber=Jan17_HO4-->


