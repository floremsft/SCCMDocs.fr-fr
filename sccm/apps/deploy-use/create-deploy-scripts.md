---
title: "Créer et exécuter des scripts"
titleSuffix: Configuration Manager
description: "Créez et exécutez des scripts Powershell sur les appareils clients."
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: BrucePerlerMS
ms.author: bruceper
manager: angrobe
ms.openlocfilehash: 964f6d39c4c1afc82ff4336821740923d27cd569
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Créer et exécuter des scripts PowerShell à partir de la console Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Nous avons désormais mieux intégré la possibilité d’exécuter des scripts Powershell avec System Center Configuration Manager. Powershell a l’avantage de créer des scripts automatisés et sophistiqués, qui sont compris et partagés par une large communauté. Les scripts simplifient la création d’outils personnalisés pour administrer des logiciels et vous permettent d’accomplir des tâches courantes rapidement, plus facilement et avec plus de cohérence.

Avec cette intégration dans System Center Configuration Manager, vous pouvez utiliser la fonctionnalité *Exécuter les scripts* pour effectuer les opérations suivantes :

- Créer et modifier des scripts à utiliser avec Configuration Manager.
- Gérer l’utilisation des scripts par le biais de rôles et d’étendues de sécurité.  
- Exécuter des scripts sur des regroupements des PC Windows individuels gérés localement.
- Obtenir des résultats de script agrégés rapides des appareils clients.
- Surveiller l’exécution des scripts et afficher les résultats de la création de rapports à partir de la sortie des scripts.

>[!IMPORTANT]
>Étant donné la puissance des scripts, nous vous rappelons de les utiliser avec précaution. Nous avons intégré des protections supplémentaires pour vous aider, à savoir des rôles et des étendues séparés. Vérifiez que les scripts sont exacts avant de les exécuter, puis confirmez qu’ils proviennent d’une source approuvée pour empêcher l’exécution involontaire de scripts. Soyez attentif aux caractères étendus ou toute autre obfuscation et informez-vous sur la sécurisation des scripts.

>[!TIP]
>Introduits avec la version 1706, les scripts PowerShell sont une fonctionnalité en préversion. Pour activer les scripts, consultez [Fonctionnalités en préversion dans System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## <a name="prerequisites"></a>Prérequis

- Pour exécuter des scripts PowerShell, le client doit exécuter PowerShell version 3.0 ou ultérieure. Toutefois, si un script que vous exécutez contient des fonctionnalités d’une version ultérieure de PowerShell, le client sur lequel vous exécutez le script doit exécuter cette version de PowerShell.
- Les clients Configuration Manager doivent exécuter le client à partir de la version Release 1706 ou ultérieure pour exécuter des scripts.
- Pour utiliser des scripts, vous devez être membre du rôle de sécurité Configuration Manager approprié.
- Pour importer et créer des scripts, votre compte doit avoir des autorisations **Créer** pour les **scripts SMS** dans le rôle de sécurité **Administrateur complet**.
- Pour approuver ou refuser des scripts, votre compte doit avoir des autorisations **Approuver** pour les **scripts SMS** dans le rôle de sécurité **Administrateur complet**.
- Pour exécuter des scripts, votre compte doit avoir les autorisations **Exécuter des scripts** pour les **Collections** dans le rôle de sécurité **Gestionnaire de paramètres de conformité**.

Pour plus d'informations sur les rôles de sécurité de Configuration Manager, voir [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration).

## <a name="limitations"></a>Limitations

La fonctionnalité Exécuter les scripts prend actuellement en charge :

- Langages de script : PowerShell
- Types de paramètres : entier et chaîne

## <a name="run-script-authors-and-approvers"></a>Auteurs et approbateurs de scripts

La fonctionnalité Exécuter les scripts utilise les concepts d’*auteur de script* et d’*approbateur de script* comme rôles distincts pour l’implémentation et l’exécution d’un script. La distinction des rôles d’auteur et d’approbateur permet à l’outil puissant qu’est la fonctionnalité Exécuter les scripts de bénéficier d’un contrôle de processus important.

### <a name="scripts-roles-control"></a>Contrôle des rôles des scripts

Par défaut, les utilisateurs ne peuvent pas approuver un script qu'ils ont créé. Étant donné que les scripts sont puissants, flexibles et peuvent être déployés sur de nombreux appareils, vous pouvez séparer les rôles entre la personne qui crée le script et celle qui l’approuve. Ces rôles procurent un niveau supplémentaire de sécurité par rapport à l’exécution d’un script sans supervision. Vous pouvez désactiver cette approbation secondaire, pour faciliter le test.

### <a name="approve-or-deny-a-script"></a>Approuver ou refuser un script

Les scripts doivent être approuvés, par le rôle d’*approbateur de script*, pour pouvoir être exécutés. Pour approuver un script :

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.
2. Dans l'espace de travail **Bibliothèque de logiciels** , cliquez sur **Scripts**.
3. Dans la liste **Script**, sélectionnez le script que vous souhaitez approuver ou refuser puis, dans l’onglet **Accueil**, sous le groupe **Script**, cliquez sur **Approuver/Refuser**.
4. Dans la boîte de dialogue **Approuver ou refuser le script**, **approuvez** ou **refusez** le script et entrez éventuellement un commentaire sur votre décision.  Si vous refusez un script, il ne peut pas être exécuté sur les appareils clients. <br>
![Script - Approbation](./media/run-scripts/RS-approval.png)
5. Effectuez toutes les étapes de l'Assistant. Dans la liste **Script**, la colonne **État d’approbation** change en fonction de votre action.

### <a name="allow-users-to-approve-their-own-scripts"></a>Autoriser les utilisateurs à approuver leurs propres scripts

Cette approbation est principalement utilisée pour la phase de test du développement de scripts.

1. Dans la console Configuration Manager, cliquez sur **Administration**.
2. Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Sites**.
3. Dans la liste des sites, sélectionnez votre site, puis, dans l’onglet **accueil**, sous le groupe **Sites**, cliquez sur **Paramètres de hiérarchie**.
4. Dans l’onglet **Général** de la boîte de dialogue **Propriétés des paramètres de hiérarchie**, décochez la case **Ne pas autoriser les auteurs à approuver leurs propres scripts**.

>[!IMPORTANT]
>En tant que bonne pratique, vous ne devriez pas autoriser un auteur de script à approuver ses propres scripts. Cette autorisation ne devrait être accordée que dans un environnement de laboratoire. Mesurez minutieusement l’impact qu’aurait la modification de ce paramètre dans un environnement de production.

## <a name="security-scopes"></a>Étendues de sécurité
*(Fonctionnalité introduite avec la version 1710)*  
La fonctionnalité Exécuter les scripts utilise des étendues de sécurité, fonctionnalité de Configuration Manager, pour contrôler la création et l’exécution des scripts par le biais d’étiquettes représentant des groupes d’utilisateurs. Pour plus d’informations sur l’utilisation des étendues de sécurité, consultez [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="create-a-script"></a>Créer un script

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.
2. Dans l'espace de travail **Bibliothèque de logiciels** , cliquez sur **Scripts**.
3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un script**.
4. Dans la page **Script** de l’assistant **Créer un script**, configurez les paramètres éléments suivants :
    - **Nom de script** : entrez un nom pour le script. Vous pouvez créer plusieurs scripts portant le même nom, mais utiliser des noms en double complique la recherche d’un script spécifique dans la console Configuration Manager.
    - **Langage de script** : seuls les scripts PowerShell sont pris en charge.
    - **Importer** : importez un script PowerShell dans la console. Le script s’affiche dans le champ **Script**.
    - **Effacer**  : supprime le script en cours du champ Script.
    - **Script** : affiche le script actuellement importé. Vous pouvez modifier le script dans ce champ si nécessaire.
1. Effectuez toutes les étapes de l'Assistant. Le nouveau script s’affiche dans la liste **Script** avec l’état **En attente d’approbation**. Avant de pouvoir exécuter ce script sur les appareils clients, vous devez l’approuver.

## <a name="script-parameters"></a>Paramètres de script
*(Fonctionnalité introduite avec la version 1710)*  
L’ajout de paramètres à un script offre une flexibilité accrue à votre travail. Voici les possibilités actuelles de la fonctionnalité Exécuter les scripts avec des paramètres de script pour des types de données *Chaîne* et *Entier*. Les listes des valeurs prédéfinies sont également disponibles. Si votre script comporte des types de données non pris en charge, vous obtenez un avertissement.

Dans la boîte de dialogue **Créer un script**, cliquez sur **Paramètres de script** sous **Script**.

Chacun des paramètres de votre script a sa propre boîte de dialogue pour l’ajout d’autres informations et la validation.

### <a name="parameter-validation"></a>Validation du paramètre

Chaque paramètre inclus dans votre script a une boîte de dialogue **Propriétés du paramètre de script** qui vous permet d’ajouter la validation de ce paramètre. Après avoir ajouté la validation, vous devez obtenir des erreurs si vous entrez une valeur pour un paramètre qui ne satisfait pas à sa validation.

#### <a name="example-firstname"></a>Exemple : FirstName

Dans cet exemple, vous êtes en mesure de définir les propriétés du paramètre de chaîne *FirstName*. Remarquez le champ facultatif pour **Erreur personnalisée**. Ce champ s’avère utile pour ajouter des instructions propres au champ spécifique ainsi que vos instructions destinées à l’utilisateur sur son interaction avec le paramètre de chaîne, *FirstName*, dans ce cas.

![Paramètres de script - chaîne](./media/run-scripts/RS-parameters-string.png)

## <a name="script-examples"></a>Exemples de scripts

Voici quelques exemples de scripts utilisables avec cette fonctionnalité.

### <a name="create-a-folder"></a>Créer un dossier

``` powershell
New-Item "c:\scripts" -type folder name
```

### <a name="create-a-file"></a>Créer un fichier

```powershell
New-Item "c:\scripts\new_file.txt" -type file name
```

### <a name="ping-a-given-computer"></a>Effectuer un test ping sur un ordinateur donné

Ce script accepte une chaîne et l’utilise en tant que paramètre pour une opération *ping*.

``` powershell
Param
(
 [String][Parameter(Mandatory=$True, Position=1)] $Computername
)

Ping $Computername
```

### <a name="get-battery-status"></a>Obtenir l’état de la batterie

Ce script utilise WMI pour interroger l’ordinateur sur l’état de sa batterie.

``` powershell
Write-Output (Get-WmiObject -Class Win32_Battery).BatteryStatus

```

## <a name="run-a-script"></a>Exécuter un script

Une fois approuvé, un script peut être exécuté sur une collection que vous choisissez. Une fois que l’exécution de votre script commence, il est lancé rapidement via un système de priorité élevée, puis exécuté dans un délai d’une heure. Les résultats du script sont retournés à l’aide d’un système de message d’état plus lent.

1. Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.
2. Dans l’espace de travail Ressources et Conformité, cliquez sur **Regroupements d’appareils**.
3. Dans la liste **Collections d’appareils**, cliquez sur la collection d’appareils sur laquelle vous souhaitez exécuter le script.
4. Sous l'onglet **Accueil**, dans le groupe **Tous les systèmes**, cliquez sur **Exécuter le script**.
5. Sur la page **Script** de l’assistant **Exécuter le Script**, choisissez un script dans la liste. Seuls les scripts approuvés sont affichés.
6. Cliquez sur **Suivant**, puis complétez l’Assistant.

>[!IMPORTANT]
>Si un script ne s’exécute pas dans le délai d’une heure, parce qu’un client cible est par exemple désactivé, vous devez le réexécuter.

### <a name="target-machine-execution"></a>Exécution de la machine cible
Le script est exécuté en tant que compte *système* ou *d’ordinateur* sur les clients ciblés. Ce compte dispose d’un accès réseau limité. L’accès à des emplacements et systèmes distants par le script doit être provisionné en conséquence.

## <a name="work-flow-and-monitoring"></a>Flux de travail et surveillance

Voici ce à quoi la fonctionnalité Exécuter les scripts ressemble en tant que flux de travail : créer, approuver, exécuter et surveiller.

![Exécuter les scripts - flux de travail](./media/run-scripts/RS-run-scripts-work-flow.png)

### <a name="script-monitoring"></a>Surveillance des scripts

Une fois que vous avez lancé l’exécution d’un script sur un regroupement d’appareils, utilisez la procédure suivante pour surveiller l’opération. Depuis la version 1710, vous êtes en mesure de surveiller un script en temps réel pendant qu’il s’exécute et vous pouvez également revenir au rapport d’une exécution du script donnée.

1. Dans la console Configuration Manager, cliquez sur **Surveillance**.
2. Dans la liste **Surveillance**, cliquez sur **État du script**. ![Surveillance de script - état de l’exécution du script](./media/run-scripts/RS-monitoring-three-bar.png)
3. Dans la liste **État du script**, vous pouvez voir les résultats pour chaque script que vous avez exécuté sur des appareils clients. Un code de sortie de script de **0** indique généralement que le script a été exécuté avec succès.

## <a name="see-also"></a>Voir aussi

- [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration)
