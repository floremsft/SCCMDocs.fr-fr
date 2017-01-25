1.  Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Mises à jour logicielles**.  

2.  Choisissez la mise à jour logicielle à télécharger selon l'une des méthodes suivantes :  

    -   Sélectionnez un ou plusieurs groupes de mises à jour logicielles à partir de **Groupes de mises à jour logicielles**, puis sous l'onglet **Accueil** , dans le groupe **Groupe de mises à jour** , cliquez sur **Télécharger**.  

    -   Sélectionnez une ou plusieurs mises à jour logicielles à partir de **Toutes les mises à jour logicielles**, puis, sous l'onglet **Accueil** , dans le groupe **Mise à jour** , cliquez sur **Télécharger**.  

        > [!NOTE]  
        >  Dans le nœud **Toutes les mises à jour logicielles**, Configuration Manager affiche uniquement les mises à jour logicielles classées selon les critères **Critique** et **Sécurité** qui ont été publiées au cours des 30 derniers jours.  

        > [!TIP]  
        >  Cliquez sur **Ajouter des critères** pour filtrer les mises à jour logicielles qui sont affichées dans le nœud **Toutes les mises à jour logicielles** , enregistrez les critères de recherche que vous utilisez fréquemment, puis gérez les recherches enregistrées sur l'onglet **Rechercher** .  

         L' **Assistant Téléchargement des mises à jour logicielles** s'ouvre.  

3.  Sur la page **Package de déploiement** , configurez les paramètres suivants :  

    1.  **Sélectionner un package de déploiement**: choisissez ce paramètre pour sélectionner un package de déploiement existant pour les mises à jour logicielles incluses dans le déploiement.  

        > [!NOTE]  
        >  Les mises à jour logicielles qui ont déjà été téléchargées dans le package de déploiement sélectionné ne sont pas téléchargées à nouveau.  

    2.  **Créer un package de déploiement**: sélectionnez ce paramètre pour créer un package de déploiement pour les mises à jour logicielles incluses dans le déploiement. Configurez les paramètres suivants :  

        -   **Nom**: spécifie le nom du package de déploiement. Le package doit porter un nom unique qui décrit brièvement son contenu.  Il est limité à 50 caractères.  

        -   **Description**: spécifie la description du package de déploiement. La description du package fournit des informations sur le contenu du package et est limitée à 127 caractères.  

        -   **Source du package**: spécifie l’emplacement des fichiers sources des mises à jour logicielles. Tapez un chemin réseau pour l’emplacement source, par exemple **\\\serveur\nom_partage\chemin**ou cliquez sur **Parcourir** pour rechercher l’emplacement réseau. Vous devez créer le dossier partagé pour les fichiers sources du package de déploiement avant de passer à la page suivante.  

            > [!NOTE]  
            >  L'emplacement source du package de déploiement que vous spécifiez ne peut pas être utilisé par un autre package de déploiement de logiciel.  

            > [!IMPORTANT]  
            >  Le compte d'ordinateur du fournisseur SMS et l'utilisateur qui exécute l'Assistant Téléchargement des mises à jour logicielles nécessitent des autorisations NTFS en **Écriture** sur l'emplacement de téléchargement. Vous devez soigneusement limiter l'accès à l'emplacement de téléchargement pour éviter que des personnes malintentionnées ne falsifient les fichiers sources des mises à jour logicielles.  

            > [!IMPORTANT]  
            >  Une fois que le package de déploiement a été créé par Configuration Manager, vous pouvez modifier l’emplacement source du package de déploiement dans les propriétés du package. Mais le cas échéant, vous devez d'abord copier le contenu à partir de la source du package d'origine vers le nouvel emplacement source du package.  

     Cliquez sur **Suivant**.  

4.  Dans la page **Points de distribution**, spécifiez les points de distribution ou les groupes de points de distribution qui hébergent les fichiers de mises à jour logicielles, puis cliquez sur **Suivant**. Pour plus d’informations sur les points de distribution, consultez [Configurations des points de distribution](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!NOTE]  
    >  La page Points de distribution est disponible uniquement lorsque vous créez un package de déploiement de mises à jour logicielles.  

6.  Dans la page **Paramètres de distribution**, spécifiez les paramètres suivants :  

    -   **Priorité de distribution**: utilisez ce paramètre pour spécifier la priorité de distribution pour le package de déploiement. La priorité de distribution s'applique lorsque le package de déploiement est envoyé aux points de distribution sur les sites enfants. Les packages de déploiement sont envoyés par ordre de priorité : **Haute**, **Moyenne**ou **Faible**. Les packages disposant de priorités identiques sont transmis dans l'ordre dans lequel ils ont été créés. En l'absence de backlog, le package est immédiatement traité quelle que soit sa priorité. Par défaut, les packages sont transmis avec la priorité **Moyenne** .  

    -   **Distribuer le contenu pour ce package vers les points de distribution préférés**: utilisez ce paramètre pour activer la distribution de contenu à la demande vers des points de distribution préférés. Lorsque la distribution est activée, le point de gestion crée un déclencheur pour le gestionnaire de distribution afin de distribuer le contenu à tous les points de distribution préférés lorsqu'un client demande le contenu du package et que le contenu n'est disponible sur aucun point de distribution préféré. Pour plus d’informations sur les points de distribution préférés et sur le contenu à la demande, consultez [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

    -   **Paramètres du point de distribution préparé**: utilisez ce paramètre pour spécifier la manière dont vous voulez distribuer du contenu à des points de distribution préparés. Choisissez l'une des options suivantes :  

        -   **Télécharger automatiquement du contenu lorsque des packages sont affectés à des points de distribution**: utilisez ce paramètre pour ignorer les paramètres de préparation et distribuer du contenu au point de distribution.  

        -   **Télécharger uniquement les modifications de contenu vers le point de distribution**: utilisez ce paramètre pour préparer le contenu initial sur le point de distribution, puis distribuer les modifications apportées au contenu au point de distribution.  

        -   **Copier manuellement le contenu de ce package vers le point de distribution**: utilisez ce paramètre pour toujours préparer le contenu sur le point de distribution. Il s'agit du paramètre par défaut.  

         Pour plus d’informations sur la préparation du contenu sur les points de distribution, consultez [Utiliser du contenu préparé](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

     Cliquez sur **Suivant**.  

6.  Dans la page **Emplacement de téléchargement**, spécifiez l’emplacement où Configuration Manager doit télécharger les fichiers sources des mises à jour logicielles. Si besoin, utilisez les options suivantes :  

    -   **Télécharger les mises à jour logicielles depuis Internet**: sélectionnez ce paramètre pour télécharger les mises à jour logicielles à partir de l’emplacement sur Internet. Il s'agit du paramètre par défaut.  

    -   **Télécharger les mises à jour logicielles à partir d’un emplacement sur le réseau local**: sélectionnez ce paramètre pour télécharger des mises à jour logicielles à partir d’un dossier local ou d’un dossier réseau partagé. Utilisez ce paramètre lorsque l'ordinateur exécutant l'assistant ne dispose d'aucune connexion à Internet.  

        > [!NOTE]  
        >  Lorsque vous utilisez ce paramètre, téléchargez les mises à jour logicielles à partir de n'importe quel ordinateur connecté à Internet, puis copiez les mises à jour logicielles sur le réseau local qui est accessible depuis l'ordinateur exécutant l'Assistant.  

     Cliquez sur **Suivant**.  

7.  Dans la page **Sélection de la langue**, spécifiez les langues des mises à jour logicielles sélectionnées à télécharger, puis cliquez sur **Suivant**. Configuration Manager télécharge les mises à jour logicielles uniquement si elles sont disponibles dans les langues sélectionnées. Les mises à jour logicielles qui ne sont spécifiques à aucune langue sont toujours téléchargées.  

8. Dans la page **Résumé**, vérifiez les paramètres que vous avez sélectionnés dans l’Assistant, puis cliquez sur **Suivant** pour télécharger les mises à jour logicielles.  

9. Dans la page **Dernière étape**, vérifiez que les mises à jour logicielles ont été téléchargées avec succès, puis cliquez sur **Fermer**.  


<!--HONumber=Jan17_HO4-->


