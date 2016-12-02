---
title: "Planification des tâches de migration | System Center Configuration Manager"
description: "Utilisez des tâches de migration pour configurer les données que vous souhaitez migrer vers votre environnement System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a70bfbd4-757a-4468-9312-1c3b373ef9fc
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 21e00064a8ecad3dd1c24b7f02bd0a8a8c36924f


---
# <a name="planning-a-migration-job-strategy-in-system-center-configuration-manager"></a>Planification d’une stratégie pour les tâches de migration dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez des tâches de migration pour configurer les données spécifiques que vous souhaitez migrer vers votre environnement System Center Configuration Manager. Les tâches de migration identifient les objets que vous envisagez de migrer, et elles s'exécutent sur le site de niveau supérieur dans votre hiérarchie de destination. Vous pouvez configurer une ou plusieurs tâches de migration par site source. Cela vous permet de migrer tous les objets simultanément ou des sous-ensembles limités de données avec chaque tâche.  

 Vous pouvez créer des tâches de migration une fois que Configuration Manager a collecté avec succès les données d’un ou de plusieurs sites à partir de la hiérarchie source. Vous pouvez migrer des données dans n'importe quel ordre à partir des sites source contenant des données. Avec un site source Configuration Manager 2007, vous ne pouvez migrer les données qu’à partir du site où un objet a été créé. Avec les sites sources exécutant System Center 2012 Configuration Manager ou une version ultérieure, toutes les données que vous pouvez migrer sont disponibles sur le site de niveau supérieur de la hiérarchie source.  

 Avant de migrer des clients entre hiérarchies, vérifiez que les objets que les clients utilisent ont été migrés et que ces objets sont disponibles dans la hiérarchie de destination. Par exemple, quand vous effectuez une migration à partir d’une hiérarchie source Configuration Manager 2007 SP2, vous pouvez recevoir une publication pour du contenu déployé sur un regroupement personnalisé contenant un client. Dans ce cas, vous devez migrer le regroupement, la publication et le contenu associé avant de migrer le client. En effet, lorsque le contenu, le regroupement et la publication ne sont pas migrés avant la migration du client, ces données ne peut pas être associées au client dans la hiérarchie de destination. Si un client n'est pas associé aux données liées à une publication et à un contenu exécutés précédemment, le contenu peut être proposé au client pour l'installation dans la hiérarchie de destination, ce qui peut être inutile. Si le client est migré après la migration des données, il est associé à ce contenu et à cette publication, et sauf si la publication est récurrente, le contenu n'est plus proposé pour la publication migrée.  

 Pour certains objets, la migration des données de la hiérarchie source vers la hiérarchie de destination ne suffit pas. Par exemple, pour pouvoir migrer les mises à jour logicielles des clients vers votre hiérarchie de destination, vous devez déployer un point de mise à jour logicielle actif dans la hiérarchie de destination, configurer le catalogue des produits et synchroniser le point de mise à jour logicielle avec un service WSUS (Windows Server Update Services).  

 Utilisez les sections suivantes pour planifier vos tâches de migration.  

-   [Types de tâche de migration](#Types_of_Migration)  

-   [Planification générale de toutes les tâches de migration](#About_Migration_Jobs)  

-   [Planification des tâches de migration de regroupements](#About_Collection_Migration)  

-   [Planification des tâches de migration d’objets](#About_Object_Migration)  

-   [Planification des tâches de migration d’objets déjà migrés](#About_Object_Migrations)  

##  <a name="a-nametypesofmigrationa-types-of-migration-jobs"></a><a name="Types_of_Migration"></a> Types de tâches de migration  
 Configuration Manager prend en charge les types de tâche de migration suivants. Chaque type de tâche est conçu pour vous aider à définir les objets à inclure dans cette tâche.  

 **Migration de regroupements** (prise en charge uniquement pour la migration à partir de Configuration Manager 2007 SP2) - Migrez des objets liés aux regroupements de votre choix. Par défaut, la migration d'un regroupement inclut tous les objets qui sont associés aux membres du regroupement. Vous pouvez exclure des instances d'objet spécifiques lors de l'utilisation d'une tâche de migration de regroupement.  

 **Migration d’objets** - Migrez des objets individuels de votre choix. Vous sélectionnez uniquement les données à migrer.  

 **Migration d’objets déjà migrés** - Migrez des objets que vous avez déjà migrés, quand ces objets ont été mis à jour dans la hiérarchie source après leur dernière migration.  

###  <a name="a-nameobjectsthatcanmigratea-objects-that-you-can-migrate"></a><a name="Objects_that_can_migrate"></a> Objets que vous pouvez migrer  
 Tous les objets ne peuvent pas migrer en fonction du type de tâche de migration. La liste suivant indique le type des objets que vous pouvez migrer à l’aide de chaque type de tâche de migration.  

> [!NOTE]  
>  Les tâches de migration de regroupements sont disponibles uniquement quand vous migrez des objets à partir d’une hiérarchie source Configuration Manager 2007 SP2.  

 **Types de tâche que vous pouvez utiliser pour migrer chaque objet :**  

-   **Publications** (disponibles pour une migration à partir des sites sources Configuration Manager 2007 pris en charge)  

    -   Migration du regroupement  

-   **Catalogue Asset Intelligence**  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Configuration matérielle requise pour Asset Intelligence**  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Liste de logiciels Asset Intelligence**  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Limites**  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Bases de référence de configuration**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Éléments de configuration**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Fenêtres de maintenance**  

    -   Migration du regroupement  

-   **Images de démarrage de déploiement du système d’exploitation**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Packages de pilotes de déploiement du système d’exploitation**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Pilotes de déploiement du système d’exploitation**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Images de déploiement du système d’exploitation**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Packages de déploiement du système d’exploitation**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Packages de distribution de logiciels**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Règles de contrôle de logiciel**  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Packages de déploiement de mises à jour logicielles**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Modèles de déploiement de mises à jour logicielles**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Déploiements de mises à jour logicielles**  

    -   Migration du regroupement  

-   **Listes de mises à jour logicielles**  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Séquences de tâches**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Packages d’applications virtuelles**  

    -   Migration du regroupement  

    -   Migration d'objet  

    > [!IMPORTANT]  
    >  Bien que vous puissiez migrer un package d'application virtuelle en utilisant la migration d'objet, vous ne pouvez pas le migrer en utilisant le type de tâche de migration **Migration d'objets migrés précédemment**. Vous devez plutôt supprimer le package d'application virtuelle migré du site de destination, puis créer une tâche de migration pour migrer l'application virtuelle.  

##  <a name="a-nameaboutmigrationjobsa-general-planning-for-all-migration-jobs"></a><a name="About_Migration_Jobs"></a> Planification générale de toutes les tâches de migration  
 Utilisez l'Assistant Création de tâche de migration pour créer une tâche de migration pour migrer des objets vers votre hiérarchie de destination. Le type de tâche de migration que vous créez détermine les objets pouvant être migrés. Vous pouvez créer et utiliser plusieurs tâches de migration pour migrer des données à partir du même site source ou de plusieurs sites source. L'utilisation d'un type de tâche de migration n'empêche pas l'utilisation d'un autre type de tâche de migration.  

 Une fois la tâche de migration exécutée, son état devient **Terminé** , et vous ne pouvez plus la réexécuter. Toutefois, vous pouvez créer une tâche de migration pour migrer les objets migrés par la tâche d'origine, sans compter que la nouvelle tâche de migration peut inclure des objets supplémentaires également. Lorsque vous créez des tâches de migration supplémentaires, les objets déjà migrés s'affichent avec l'état **Migré**. Vous pouvez sélectionner ces objets pour les migrer de nouveau, mais, si les objets n'ont pas été mis à jour dans la hiérarchie source, il est inutile de les migrer de nouveau. Si un objet a été mis à jour dans la hiérarchie source après sa migration, vous pouvez identifier l'objet lorsque vous utilisez le type de tâche de migration **Objets modifiés après la migration**.  

 Vous pouvez supprimer une tâche de migration avant son exécution. Cependant, une fois qu’une tâche de migration a été effectuée, elle reste visible dans la console Configuration Manager et ne peut pas être supprimée. Chaque tâche de migration effectuée, ou qui n’a pas encore été exécutée, reste visible dans la console Configuration Manager jusqu’à ce que le processus de migration soit fini et que vous ayez nettoyé les données de migration.  

> [!NOTE]  
>  Après avoir terminé la migration en utilisant l'action **Nettoyer les données de migration** , vous pouvez reconfigurer la même hiérarchie comme hiérarchie source actuelle pour visualiser de nouveau les objets migrés précédemment.  

 Pour afficher les objets contenus dans une tâche de migration au sein de la console Configuration Manager, sélectionnez la tâche de migration, puis cliquez sur l’onglet **Objets dans la tâche**.  

 Utilisez les informations dans les sections suivantes pour planifier toutes les tâches de migration.  

### <a name="data-selection"></a>Sélection de données  
 Lorsque vous créez une tâche de migration de regroupement, vous devez sélectionner au moins un regroupement. Après avoir sélectionné les regroupements, l'Assistant Création de tâche de migration affiche les objets associés aux regroupements. Par défaut, tous les objets associés aux regroupements sélectionnés sont migrés, mais vous pouvez désélectionner les objets à ne pas migrer avec la tâche. Lorsque vous désélectionnez un objet ayant des objets dépendants, ces derniers sont également désélectionnés. Tous les objets désélectionnés sont ajoutés à une liste d'exclusion. Les objets dans une liste d'exclusion sont éliminés de la sélection automatique pour les prochaines tâches de migration. Vous devez modifier manuellement la liste d'exclusion pour supprimer les objets qui doivent être sélectionnés automatiquement pour les tâches de migration suivantes.  

### <a name="site-ownership-for-migrated-content"></a>Propriétaire de site pour le contenu migré  
 Lorsque vous migrez du contenu pour des déploiements, vous devez attribuer l'objet de contenu à un site dans la hiérarchie de destination. Ce site devient alors le propriétaire de ce contenu dans la hiérarchie de destination. Bien que le site de niveau supérieur de votre hiérarchie de destination soit le site qui migre les métadonnées du contenu, c'est le site attribué qui accède aux fichiers source d'origine du contenu dans le réseau.  

 Pour réduire la bande passante réseau utilisée lors de la migration, transférez la propriété du contenu au site disponible le plus proche. Dans la mesure où les informations sur le contenu sont partagées globalement dans System Center Configuration Manager, elles sont disponibles sur tous les sites.  

 Bien que les informations sur le contenu soient partagées sur tous les sites de la hiérarchie de destination en utilisant la réplication de base de données, le contenu que vous affectez à un site principal et que vous déployez ensuite sur des points de distribution sur d'autres sites principaux est transféré en utilisant la réplication basée sur les fichiers. Ce transfert est routé via le site administration centrale, puis vers chaque site principal supplémentaire. En centralisant les packages que vous planifiez de distribuer vers plusieurs sites principaux avant la migration ou au cours de la migration lorsque vous définissez un site comme propriétaire du contenu, vous pouvez réduire les transferts de données sur les réseaux à faible bande passante.  

### <a name="configure-role-based-administration-security-scopes-for-migrated-data"></a>Configurer des étendues de sécurité de l’administration basée sur des rôles pour les données migrées  
 Lorsque vous migrez des données vers une hiérarchie de destination, vous devez affecter une ou plusieurs étendues de sécurité d'administration basée sur des rôles aux objets dont les données sont migrées. Ainsi, seuls les utilisateurs administratifs appropriés peuvent accéder à ces données après la migration. Les étendues de sécurité que vous spécifiez sont définies par la tâche de migration et sont appliquées à chaque objet migré par cette tâche. Si vous voulez appliquer des étendues de sécurité différentes à différents groupes d'objets et affecter ces étendues au cours de la migration, vous devez migrer les différents groupes d'objets en utilisant différentes tâches de migration.  

 Avant de configurer une tâche de migration, passez en revue la section relative au fonctionnement de l’administration basée sur des rôles dans System Center Configuration Manager et, si nécessaire, configurez une ou plusieurs étendues de sécurité pour les données à migrer afin de définir les utilisateurs autorisés à accéder aux objets migrés dans la hiérarchie de destination.  

 Pour plus d’informations sur les étendues de sécurité et l’administration basée sur des rôles, consultez [Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

### <a name="review-migration-actions"></a>Vérification des actions de migration  
 Quand vous configurez une tâche de migration, l’Assistant Création de tâche de migration affiche une liste des actions à effectuer pour garantir la réussite de la migration, ainsi qu’une liste des actions entreprises par Configuration Manager pendant la migration des données sélectionnées. Lisez attentivement ces informations pour vérifier le résultat attendu.  

### <a name="scheduling-migration-jobs"></a>Planification des tâches de migration  
 Par défaut, une tâche de migration s'exécute immédiatement après sa création. Toutefois, vous pouvez spécifier le moment d'exécution de la tâche de migration lorsque vous créez la tâche ou ultérieurement en modifiant les propriétés de la tâche. Vous pouvez planifier l'exécution de la tâche de migration comme suit.  

-   Exécuter la tâche maintenant  

-   Exécuter la tâche à une heure de début spécifique  

-   Ne pas exécuter la tâche  

### <a name="specify-conflict-resolution-for-migrated-data"></a>Spécifier la résolution des conflits de données migrées  
 Par défaut, les tâches de migration ne remplacent pas les données dans la base de données de destination, à moins que vous configuriez la tâche de migration pour qu'elle ignore ou remplace les données déjà migrées vers la base de données de destination.  

##  <a name="a-nameaboutcollectionmigration-a-planning-for-collection-migration-jobs"></a><a name="About_Collection_Migration "></a> Planification des tâches de migration de regroupements  
 Les tâches de migration de regroupements sont disponibles uniquement quand vous migrez des données à partir d’une hiérarchie source qui exécute une version prise en charge de Configuration Manager 2007. Vous devez spécifier un ou plusieurs regroupements à migrer lorsque vous utilisez la migration basée sur le regroupement. Pour chaque regroupement que vous spécifiez, la tâche de migration sélectionne automatiquement tous les objets associés pour les migrer. Par exemple, si vous sélectionnez un regroupement d'utilisateurs, les membres du regroupement sont identifiés et vous pouvez migrer les déploiements associés au regroupement. Vous pouvez également sélectionner d'autres objets de déploiement à migrer associés à ces membres. Tous ces éléments sélectionnés sont ajoutés à la liste des objets qui peuvent être migrés.  

 Quand vous migrez un regroupement, System Center Configuration Manager migre également les paramètres du regroupement, notamment les fenêtres de maintenance et les variables du regroupement. Toutefois, il ne peut pas migrer les paramètres du regroupement pour la préparation du client AMT.  

 Utilisez les informations dans les sections suivantes pour comprendre les configurations supplémentaires qui peuvent s'appliquer aux tâches de migration basées sur le regroupement.  

### <a name="excluding-objects-from-collection-migration-jobs"></a>Exclusion d’objets d’une tâche de migration de regroupement  
 Vous pouvez exclure des objets d'une tâche de migration de regroupement. Lorsque vous excluez un objet d'une tâche de migration de regroupement, l'objet est ajouté à une liste d'exclusion globale qui contient tous les objets que vous avez exclus des tâches de migration créées pour un site source dans la hiérarchie source actuelle. Les objets dans la liste d'exclusion peuvent toujours être migrés dans les tâches suivantes, mais ils ne sont pas inclus automatiquement lorsque vous créez une tâche de migration basée sur le regroupement.  

 Vous pouvez modifier la liste d'exclusion pour supprimer des objets que vous avez exclus. Lorsque vous supprimez un objet de la liste d'exclusion, il est automatiquement sélectionné lorsqu'un regroupement associé est défini lors de la création d'une tâche de migration.  

### <a name="unsupported-collections"></a>Regroupements non pris en charge  
 Configuration Manager peut migrer les regroupements d’utilisateurs par défaut, les regroupements d’appareils et la plupart des regroupements personnalisés à partir d’une hiérarchie source Configuration Manager 2007. Toutefois, Configuration Manager ne peut pas migrer les regroupements qui contiennent des utilisateurs et des appareils dans le même regroupement.  

 Vous ne pouvez pas migrer les regroupements suivants :  

-   Un regroupement qui contient des utilisateurs et des périphériques.  

-   Un regroupement qui contient une référence à un regroupement correspondant à un type de ressource différent. tel qu'un regroupement de périphériques ayant un sous-regroupement ou un lien à un regroupement d'utilisateurs. Dans cet exemple, seul le regroupement de niveau supérieur migre.  

-   Un regroupement qui contient une règle d'inclusion d'ordinateurs inconnus. Le regroupement est migré, mais la règle d'inclusion d'ordinateurs inconnus n'est pas migrée.  

### <a name="empty-collections"></a>Regroupements vides  
 Un regroupement vide est un regroupement qui n'a aucune ressource associée. Quand Configuration Manager migre un regroupement vide, il convertit le regroupement en dossier organisationnel qui ne contient aucun utilisateur ou appareil. Ce dossier est créé avec le nom du regroupement vide sous le nœud **Regroupement d’utilisateurs** ou **Regroupement d’appareils** dans l’espace de travail **Ressources et Conformité** dans la console Configuration Manager.  

### <a name="linked-collections-and-subcollections"></a>Regroupements liés et sous-regroupements  
 Quand vous migrez des regroupements liés à d’autres regroupements ou ayant des sous-regroupements, Configuration Manager crée un dossier sous le nœud **Regroupements d’utilisateurs** ou **Regroupements d’appareils** en plus des regroupements et sous-regroupements liés.  

### <a name="collection-dependencies-and-include-objects"></a>Dépendances de regroupements et inclusion d’objets  
 Lorsque vous spécifiez un regroupement à migrer dans l'Assistant Création de tâche de migration, tous les regroupements qui en dépendent sont automatiquement sélectionnés pour être inclus dans la tâche. Ce comportement garantit que toutes les ressources nécessaires sont disponibles après la migration.  

 Exemple : Vous sélectionnez un regroupement pour les périphériques qui exécutent Windows 7 et qui est nommé **Win_7**. Ce regroupement est limité à un regroupement contenant tous vos systèmes d'exploitation client et nommé **All_Clients**. Le regroupement **All_Clients** sera automatiquement sélectionné pour la migration.  

### <a name="collection-limiting"></a>Limitation au regroupement  
 Avec System Center Configuration Manager, les regroupements sont des données globales et sont évalués au niveau de chaque site de la hiérarchie. Par conséquent, pensez à limiter l’étendue d’un regroupement après sa migration. Pendant la migration, vous pouvez identifier un regroupement à partir de la hiérarchie de destination à utiliser pour limiter l'étendue du regroupement que vous migrez, de sorte que le regroupement migré n'inclut pas de membres imprévus.  

 Par exemple, dans Configuration Manager 2007, les regroupements sont évalués au niveau du site qui les crée et au niveau des sites enfants. Une publication peut être déployée vers un site enfant seulement, et cela limiterait l'étendue de cette publication à ce site enfant. En comparaison, avec System Center Configuration Manager, les regroupements sont évalués au niveau de chaque site, et les publications associées sont ensuite évaluées pour chaque site. La limitation au regroupement vous permet d'affiner les membres du regroupement à partir d'un autre regroupement afin d'éviter l'ajout de membres du regroupement imprévus.  

### <a name="site-code-replacement"></a>Remplacement du code de site  
 Quand vous migrez un regroupement contenant des critères qui identifient un site Configuration Manager 2007, vous devez spécifier un site spécifique dans la hiérarchie de destination. Cela garantit que le regroupement migré reste fonctionnel dans votre environnement de destination et que son étendue n'augmente pas.  

### <a name="specify-behavior-for-migrated-advertisements"></a>Spécifier le comportement pour les publications migrées  
 Par défaut, les tâches de migration basée sur des regroupements désactivent les publications qui migrent vers la hiérarchie de destination. Cela inclut tous les programmes qui sont associés à la publication. Quand vous créez une tâche de migration basée sur un regroupement et contenant des publications, l’option **Activer les programmes à déployer dans Configuration Manager après la migration d’une publication** apparaît dans la page **Paramètres** de l’Assistant Création de tâche de migration. Si vous sélectionnez cette option, les programmes associés aux publications sont activés après qu'ils ont migré. Nous vous conseillons de ne pas sélectionner cette option mais d'activer plutôt les programmes une fois qu'ils ont migré si vous pouvez vérifier les clients qui les recevront.  

> [!NOTE]  
>  L’option **Activer les programmes à déployer dans Configuration Manager après la migration d’une publication** s’affiche uniquement quand vous créez une tâche de migration basée sur un regroupement et lorsque la tâche de migration contient des publications.  

 Pour activer un programme après la migration, désactivez l'option **Désactiver ce programme sur les ordinateurs qui le publient** sur l'onglet **Avancé** des propriétés du programme.  

##  <a name="a-nameaboutobjectmigrationa-planning-for-object-migration-jobs"></a><a name="About_Object_Migration"></a> Planification des tâches de migration d’objets  
 Contrairement à la migration des regroupements, vous devez sélectionner chaque objet et instance d'objet que vous souhaitez migrer. Vous pouvez sélectionner des objets individuels, par exemple les publications d’une hiérarchie Configuration Manager 2007, ou une publication d’une hiérarchie System Center 2012 Configuration Manager ou System Center Configuration Manager, afin de les ajouter à la liste d’objets à migrer pour une tâche de migration spécifique. Tous les objets que vous n'ajoutez pas à la liste de migration ne sont pas migrés vers le site de destination par la tâche de migration d'objet.  

 Les tâches de migration basées sur un objet ne sont associées à aucune autre configuration supplémentaire à planifier au-delà de celles applicables à toutes les tâches de migration.  

##  <a name="a-nameaboutobjectmigrationsa-planning-for-previously-migrated-object-migration-jobs"></a><a name="About_Object_Migrations"></a> Planification des tâches de migration d’objets déjà migrés  
 Si un objet que vous avez déjà migré vers la hiérarchie de destination est mis à jour dans la hiérarchie source, vous pouvez migrer de nouveau l'objet en utilisant le type de tâche **Objets modifiés après la migration** . Par exemple, lorsque vous renommez ou mettez à jour les fichiers source d'un package dans la hiérarchie source, la version du package est incrémentée dans la hiérarchie source. Après l'incrémentation de version du package, le package peut être identifié pour la migration par ce type de tâche.  

 Ce type de tâche est similaire au type de migration d'objet, à l'exception du fait que lorsque vous sélectionnez des objets à migrer, vous pouvez choisir uniquement parmi des objets qui ont été mis à jour après avoir été migrés par une tâche de migration précédente.  

 Lorsque vous sélectionnez ce type de tâche, le comportement de résolution des conflits sur la page **Paramètres** de l'Assistant Création de tâche de migration est configuré pour remplacer les objets migrés précédemment et ce paramètre ne peut pas être modifié.  

> [!NOTE]  
>  Cette tâche de migration peut identifier les objets qui sont automatiquement mis à jour par hiérarchie source, en plus des objets mis à jour par un utilisateur administratif.  



<!--HONumber=Nov16_HO1-->


