---
title: "Créer et exécuter des scripts avec Configuration Manager | Microsoft Docs"
description: "Créez et exécutez des scripts sur les appareils clients avec Configuration Manager."
ms.custom: na
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 4c90617890ba3751a7215e9ac54042d64cc1a227
ms.sourcegitcommit: 96b79fa091f44e8e6ac5652f6cbbb4b873a8bad9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2017
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Créer et exécuter des scripts PowerShell à partir de la console Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans Configuration Manager, outre utiliser des packages et des programmes pour déployer des scripts, vous pouvez utiliser les fonctionnalités ci-après pour effectuer les actions suivantes :

- Importer des scripts PowerShell dans Configuration Manager
- Modifier les scripts à partir de la console Configuration Manager (pour les scripts non signés uniquement)
- Marquer les scripts comme Approuvés ou Refusés pour améliorer la sécurité
- Exécuter des scripts sur des collections d’ordinateurs clients Windows, et des ordinateurs Windows gérés localement. Vous ne pouvez pas déployer des scripts : ils sont exécutés presque immédiatement sur les appareils clients.
- Examinez les résultats retournés par le script dans la console Configuration Manager.

>[!TIP]
>Dans cette version de Configuration Manager, les scripts sont une fonctionnalité en préversion. Pour activer les scripts, consultez [Fonctionnalités en préversion dans System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## <a name="prerequisites"></a>Conditions préalables

Pour exécuter des scripts PowerShell, le client doit exécuter PowerShell version 3.0 ou ultérieure. Toutefois, si un script que vous exécutez contient des fonctionnalités d’une version ultérieure de PowerShell, le client sur lequel vous exécutez le script doit exécuter cette version.

Les clients Configuration Manager doivent exécuter le client à partir de la version Release 1706 ou ultérieure pour exécuter des scripts.

Pour utiliser des scripts, vous devez être membre du rôle de sécurité Configuration Manager approprié.

- Pour importer et créer des scripts, votre compte doit avoir les autorisations **Créer** pour les **Scripts SMS** dans le rôle de sécurité **Administrateur complet**.
- Pour approuver ou refuser des scripts, votre compte doit avoir les autorisations **Approuver** pour les **Scripts SMS** dans le rôle de sécurité **Administrateur complet**.
- Pour exécuter des scripts, votre compte doit avoir les autorisations **Exécuter des scripts** pour les **Collections** dans le rôle de sécurité **Gestionnaire de paramètres de conformité**.

Pour plus d'informations sur les rôles de sécurité de Configuration Manager, voir [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration).

Par défaut, les utilisateurs ne peuvent pas approuver un script qu'ils ont créé. Étant donné que les scripts sont puissants, flexibles et peuvent être déployés sur de nombreux appareils, vous pouvez séparer les rôles entre la personne qui crée le script et celle qui l’approuve. Ces rôles procurent un niveau supplémentaire de sécurité par rapport à l’exécution d’un script sans supervision. Vous pouvez désactiver cette approbation secondaire, pour faciliter le test.

## <a name="allow-users-to-approve-their-own-scripts"></a>Autoriser les utilisateurs à approuver leurs propres scripts

1. Dans la console Configuration Manager, cliquez sur **Administration**.
2. Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Sites**.
3. Dans la liste des sites, sélectionnez votre site, puis, dans l’onglet **accueil**, sous le groupe **Sites**, cliquez sur **Paramètres de hiérarchie**.
4. Dans l’onglet **Général** de la boîte de dialogue **Propriétés des paramètres de hiérarchie**, décochez la case **Ne pas autoriser les auteurs à approuver leurs propres scripts**.

>[!IMPORTANT]
>En tant que bonne pratique, vous ne devriez pas autoriser un auteur de script à approuver ses propres scripts. Cette autorisation ne devrait être accordée que dans un environnement de laboratoire. Veuillez mesurer minutieusement l’impact qu’aurait la modification de ce paramètre dans un environnement de production.

## <a name="import-and-edit-a-script"></a>Importer et modifier un script

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.
2. Dans l'espace de travail **Bibliothèque de logiciels** , cliquez sur **Scripts**.
3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un script**.
4. Dans la page **Script** de l’assistant **Créer un script**, configurez les paramètres éléments suivants :
    - **Nom de script** : entrez un nom pour le script. Vous pouvez créer plusieurs scripts portant le même nom, mais utiliser des noms en double complique la recherche d’un script spécifique dans la console Configuration Manager.
    - **Langage de script** : seuls les scripts PowerShell sont pris en charge.
    - **Importer** : importez un script PowerShell dans la console. Le script s’affiche dans le champ **Script**.
    - **Effacer**  : supprime le script en cours du champ Script.
    - **Script** : affiche le script actuellement importé. Vous pouvez modifier le script dans ce champ si nécessaire.
5. Effectuez toutes les étapes de l'Assistant. Le nouveau script s’affiche dans la liste **Script** avec l’état **En attente d’approbation**. Avant de pouvoir exécuter ce script sur les appareils clients, vous devez l’approuver.

### <a name="script-examples"></a>Exemples de scripts

Voici quelques exemples de scripts utilisables avec cette fonctionnalité.

#### <a name="create-a-folder"></a>Créer un dossier

*New-Item "c:\scripts" -type folder name*


#### <a name="create-a-file"></a>Créer un fichier

*New-Item c:\scripts\nouveau_fichier.txt -type file name*


## <a name="approve-or-deny-a-script"></a>Approuver ou refuser un script

Avant de pouvoir exécuter un script, il doit être approuvé. Pour approuver un script :

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.
2. Dans l'espace de travail **Bibliothèque de logiciels** , cliquez sur **Scripts**.
3. Dans la liste **Script**, sélectionnez le script que vous souhaitez approuver ou refuser puis, dans l’onglet **Accueil**, sous le groupe **Script**, cliquez sur **Approuver/Refuser**.
4. Dans la boîte de dialogue **Approuver ou refuser le script**, **Approuvez** ou **Refusez** le script et entrez éventuellement un commentaire sur votre décision. Si vous refusez un script, il ne peut pas être exécuté sur les appareils clients.
5. Effectuez toutes les étapes de l'Assistant. Dans la liste **Script**, la colonne **État d’approbation** change en fonction de votre action.

## <a name="run-a-script"></a>Exécuter un script
Une fois approuvé, un script peut être exécuté sur une collection que vous choisissez.

1. Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.
2. Dans l’espace de travail Ressources et Conformité, cliquez sur **Regroupements de périphériques**.
3. Dans la liste **Collections d’appareils**, cliquez sur la collection d’appareils sur laquelle vous souhaitez exécuter le script.
4. Sous l'onglet **Accueil**, dans le groupe **Tous les systèmes**, cliquez sur **Exécuter le script**.
5. Sur la page **Script** de l’assistant **Exécuter le Script**, choisissez un script dans la liste. Seuls les scripts approuvés sont affichés.
6. Cliquez sur **Suivant**, puis complétez l’Assistant.

>[!IMPORTANT]
>Le script dispose alors d’une heure pour s’exécuter. S’il ne s’exécute pas (par exemple, si l’ordinateur est mis hors tension) durant cette période, vous devez le réexécuter.

>[!IMPORTANT]
>Le script est exécuté en tant que compte d’ordinateur ou compte du système sur le ou les clients ciblés. Ce compte n’a qu’un accès réseau limité. L’accès à des emplacements et systèmes distants par le script doit être configuré en tenant compte de cela.

## <a name="next-steps"></a>Étapes suivantes

Après avoir exécuté un script sur les appareils clients, utilisez cette procédure pour surveiller la réussite de l’opération.

1. Dans la console Configuration Manager, cliquez sur **Surveillance**.
2. Dans la liste **Surveillance**, cliquez sur **État du script**.
3. Dans la liste **État du script**, vous pouvez voir les résultats pour chaque script que vous avez exécuté sur des appareils clients. Un code de sortie de script de **0** indique généralement que le script a été exécuté avec succès.
