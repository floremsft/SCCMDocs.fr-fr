---
title: Configurer Asset Intelligence | System Center Configuration Manager
description: Configurez Asset Intelligence dans System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 43e04a447b03885286c6c7201afb4d1b7a10aa91


---
# <a name="configure-asset-intelligence-in-system-center-configuration-manager"></a>Configurer Asset Intelligence dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous devez effectuer un certain nombre d’étapes de configuration avant de pouvoir utiliser Asset Intelligence dans System Center Configuration Manager pour inventorier et gérer les licences logicielles utilisées dans l’entreprise.  

## <a name="steps-to-configure-asset-intelligence"></a>Étapes de configuration d’Asset Intelligence  
 Pour collecter les données d'inventaire pour les rapports Asset Intelligence, vous devez activer l'agent du client d'inventaire matériel. Pour plus d’informations sur l’activation de l’agent du client d’inventaire matériel, consultez [Comment étendre l’inventaire matériel dans System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

|Étape|Détails|Informations complémentaires|  
|----------|-------------|----------------------|  
|**Étape 1**: Activer les classes de création de rapports d’inventaire matériel Asset Intelligence|La collecte des informations Asset Intelligence n’est pas automatiquement activée à l’installation de Configuration Manager. Pour activer Asset Intelligence, au moins une des classes de création de rapports d'inventaire matériel requises sur lesquelles reposent les rapports Asset Intelligence doit être activée.|Pour plus d’informations, consultez la procédure suivante dans cette rubrique : [Enable Asset Intelligence hardware inventory reporting classes](#BKMK_EnableAssetIntelligence).|  
|**Étape 2**: Installer un point de synchronisation Asset Intelligence|Le rôle de système de site du point de synchronisation Asset Intelligence permet de connecter des sites Configuration Manager à System Center Online pour synchroniser les informations du catalogue Asset Intelligence. Le point de synchronisation Asset Intelligence peut uniquement être installé sur un système de site de niveau supérieur dans la hiérarchie Configuration Manager. De plus, il a besoin d’un accès Internet pour se synchroniser avec System Center Online via le port TCP 443.<br /><br /> Outre le téléchargement des nouvelles informations du catalogue Asset Intelligence, le point de synchronisation Asset Intelligence peut envoyer les informations de titres de logiciels personnalisés à System Center Online à des fins de catégorisation. Microsoft considère tous les titres de logiciels envoyés à System Center Online pour être catégorisés comme des informations publiques. Par conséquent, vous devez vérifier que les titres de logiciels personnalisés ne contiennent pas d'informations confidentielles ou propriétaires. Pour plus d’informations sur la demande de catégorisation des titres de logiciels, consultez [Demander une mise à jour du catalogue pour les logiciels sans catégorie](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).|Pour plus d’informations, consultez la procédure suivante dans cette rubrique : [Install an Asset Intelligence Synchronization Point](#BKMK_InstallAssetIntelligenceSynchronizationPoint).|  
|**Étape 3**: Activer l’audit des événements de connexion réussie|Quatre rapports Asset Intelligence affichent des informations extraites des journaux d'événements de sécurité Windows sur les ordinateurs client. Si les paramètres du journal des événements de sécurité ne sont pas configurés pour consigner tous les événements de connexion réussie, ces rapports ne contiennent aucune donnée, même si la classe de rapport d'inventaire matériel appropriée est activée. Pour activer l'agent du client d'inventaire matériel en vue de répertorier les informations requises par ces rapports, vous devez d'abord modifier les paramètres du journal des événements de sécurité Windows sur les clients afin de consigner tous les événements de connexion réussie et activer la classe de rapport d'inventaire matériel **SMS_SystemConsoleUser** .|Pour plus d’informations, consultez les procédures suivantes dans cette rubrique : [Enable auditing of success logon events](#BKMK_EnableSuccessLogonEvents).|  
|**Étape 4**: Importer les informations de licence de logiciel|L'Assistant Importer des licences logicielles permet d'importer les informations MVLS (Microsoft Volume Licensing) et les déclarations de licence générales vers le catalogue Asset Intelligence.<br /><br /> La déclaration de licence MVLS contient des informations sur les droits de licence ou le nombre de licences achetées pour les produits Microsoft.<br /><br /> Une déclaration de licence générale contient des informations sur les licences achetées pour n'importe quel éditeur.|Pour plus d’informations, consultez les procédures suivantes dans cette rubrique : [Import software license information](#BKMK_ImportSoftwareLicenseInformation).|  
|**Étape 5**: Configurer les tâches de maintenance Asset Intelligence|Les tâches de maintenance suivantes sont associées à Asset Intelligence. Par défaut, les deux tâches de maintenance sont activées et configurées dans une planification par défaut.<br /><br /> **Vérifier le titre de l’application à l’aide des informations d’inventaire**: cette tâche de maintenance vérifie si le nom du logiciel indiqué dans l’inventaire logiciel est rapproché du nom du logiciel figurant dans le catalogue Asset Intelligence.<br /><br /> **Résumer les données du logiciel installé**: cette tâche de maintenance fournit les informations affichées dans l’espace de travail **Ressources et Conformité** , dans le nœud **Logiciels inventoriés** , sous le nœud **Asset Intelligence** . Quand la tâche s’exécute, Configuration Manager compte les titres de logiciels inventoriés sur le site principal.|Pour plus d’informations, consultez les procédures suivantes dans cette rubrique : [Configure Asset Intelligence maintenance tasks](#BKMK_ConfigureMaintenanceTasks).|  

> [!NOTE]  
>  La tâche de maintenance **Résumer les données du logiciel installé** est disponible uniquement sur les sites principaux.  

## <a name="supplemental-procedures-for-configuring-asset-intelligence"></a>Procédures supplémentaires pour configurer Asset Intelligence  
 Utilisez les informations suivantes pour les étapes décrites dans le tableau précédent.  

###  <a name="a-namebkmkenableassetintelligencea-enable-asset-intelligence-hardware-inventory-reporting-classes"></a><a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 Pour activer Asset Intelligence sur les sites Configuration Manager, vous devez activer au moins une des classes de création de rapports d’inventaire matériel Asset Intelligence. Vous pouvez activer les classes sur la page d'accueil **Asset Intelligence** ou, dans l'espace de travail **Administration** , dans le nœud **Paramètres client** , dans les propriétés des paramètres client. Utilisez l'une des procédures suivantes pour activer les classes de création de rapports d'inventaire matériel Asset Intelligence.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>Pour activer les classes de création de rapports d'inventaire matériel Asset Intelligence depuis la page d'accueil Asset Intelligence  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Biens et conformité** , cliquez sur **Asset Intelligence**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Asset Intelligence** , cliquez sur **Modifier les classes d'inventaire**. La boîte de dialogue **Modifier les classes d'inventaire** s'ouvre.  

4.  Pour activer la création de rapports Asset Intelligence, sélectionnez **Activer toutes les classes de création de rapports Asset Intelligence** ou **Activer uniquement les classes de création de rapports Asset Intelligence sélectionnées**et sélectionnez au moins une classe de création de rapports dans les classes affichées.  

    > [!NOTE]  
    >  Les rapports Asset Intelligence qui dépendent des classes d'inventaire matériel que vous activez en utilisant cette procédure n'affichent pas de données tant que les clients n'ont pas établi et retourné un inventaire matériel.  

5.  Cliquez sur **OK** pour activer les classes de création de rapports d'inventaire matériel Asset Intelligence sélectionnées.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>Pour activer les classes de création de rapports d'inventaire matériel Asset Intelligence depuis les propriétés des paramètres client  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Paramètres client**, puis sélectionnez **Paramètres d'agent client par défaut**.  

    > [!NOTE]  
    >  Si vous avez créé des paramètres client personnalisés, vous pouvez sélectionner ces paramètres à la place des paramètres client par défaut.  

3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**. La boîte de dialogue des **propriétés des paramètres client** s'affiche.  

4.  Cliquez sur **Inventaire matériel**, puis sur **Définir des classes**. La boîte de dialogue **Classes d'inventaire matériel** s'ouvre.  

5.  Cliquez sur **Filtrer par catégorie**, puis sur **Classes de création de rapports Asset Intelligence**. La liste des classes est actualisée avec uniquement les classes de création de rapports d'inventaire matériel Asset intelligence.  

6.  Sélectionnez au moins une classe de création de rapports dans la liste des classes de création de rapports Asset Intelligence.  

    > [!NOTE]  
    >  Les rapports Asset Intelligence qui dépendent des classes d'inventaire matériel que vous activez en utilisant cette procédure n'affichent pas de données tant que les clients n'ont pas établi et retourné un inventaire matériel.  

7.  Cliquez sur **OK** pour activer les classes de création de rapports d'inventaire matériel Asset Intelligence sélectionnées.  

###  <a name="a-namebkmkinstallassetintelligencesynchronizationpointa-install-an-asset-intelligence-synchronization-point"></a><a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  
 Utilisez la procédure suivante pour installer un rôle de système de site de point de synchronisation Asset Intelligence.  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>Pour installer un rôle de système de site de point de synchronisation Asset Intelligence  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Serveurs et rôles de système de site**.  

3.  Ajoutez le rôle de système de site du point de synchronisation Asset Intelligence à un serveur de système de site nouveau ou existant en utilisant l'étape correspondante :  

    -   **Nouveau serveur de système de site**: sous l’onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un serveur de système de site**. L'Assistant Création de serveur de système de site s'ouvre.  

        > [!NOTE]  
        >  Par défaut, quand Configuration Manager installe un rôle système de site, les fichiers d’installation sont installés sur le premier disque dur formaté NTFS disponible qui a le plus d’espace disque libre. Pour empêcher Configuration Manager d’effectuer l’installation sur des disques particuliers, créez un fichier vide « No_sms_on_drive.sms » et copiez-le dans le dossier racine du disque avant d’installer le serveur de système de site.  

    -   **Serveur de système de site existant**: cliquez sur le serveur sur lequel vous souhaitez installer le rôle de système de site de point de synchronisation Asset Intelligence. Lorsque vous cliquez sur un serveur, la liste des rôles de système de site déjà installés sur le serveur s'affiche dans le panneau des détails.  

         Sur l'onglet **Accueil** , dans le groupe **Serveur** , cliquez sur **Ajouter des rôles de système de site**. L'Assistant Ajout de rôles de système de site s'ouvre.  

4.  Sur la page **Général** , spécifiez les paramètres généraux du serveur de système de site. Lorsque vous ajoutez le point de synchronisation Asset Intelligence à un serveur de système de site existant, vérifiez les valeurs qui ont été précédemment configurées.  

5.  Sur la page **Sélection du rôle système** , sélectionnez **Point de synchronisation Asset Intelligence** dans la liste des rôles disponibles, puis cliquez sur **Suivant**.  

6.  Sur la page des **paramètres de connexion du point de synchronisation Asset Intelligence** , cliquez sur **Suivant**.  

     Par défaut, le paramètre **Utiliser ce point de synchronisation Asset Intelligence** est sélectionné et ne peut pas être configuré sur cette page. Comme System Center Online accepte le trafic réseau uniquement sur le port TCP 443, le paramètre de **numéro de port SSL** ne peut pas être défini dans cette page de l'Assistant.  

7.  Éventuellement, vous pouvez spécifier un chemin d'accès au fichier de certificat (.pfx) d'authentification System Center Online et cliquer sur **Suivant**. En règle générale, vous ne spécifiez pas un chemin d'accès pour le certificat, car le certificat de connexion est préparé automatiquement pendant l'installation du rôle de site.  

8.  Sur la page **Paramètres du serveur proxy** , indiquez si le point de synchronisation Asset Intelligence doit utiliser un serveur proxy lors de la connexion à System Center Online pour synchroniser le catalogue et si des données d'identification doivent être utilisées pour se connecter au serveur proxy. Ensuite, cliquez sur **Suivant**.  

    > [!WARNING]  
    >  Si un serveur proxy est nécessaire pour la connexion à System Center Online, le certificat de connexion peut être également supprimé si le mot de passe du compte d'utilisateur expire pour le compte défini pour l'authentification du serveur proxy.  

9. Sur la page **Calendrier des synchronisations** , indiquez si vous souhaitez synchroniser le catalogue Asset Intelligence dans un calendrier. Lorsque vous activez le calendrier des synchronisations, vous pouvez définir un calendrier de synchronisation simple ou personnalisé. Pendant la synchronisation planifiée, le point de synchronisation Asset Intelligence se connecte à System Center Online pour récupérer le dernier catalogue Asset Intelligence. Vous pouvez synchroniser manuellement le catalogue Asset Intelligence depuis le nœud Asset Intelligence dans la console Configuration Manager. Pour savoir comment synchroniser manuellement le catalogue Asset Intelligence, consultez la section [Pour synchroniser manuellement le catalogue Asset Intelligence](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) dans la rubrique [Opérations pour Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).  

10. Sur la page **Résumé** de l'Assistant Nouveau rôle de site, vérifiez les paramètres que vous avez spécifiés pour vérifier qu'ils sont corrects avant de poursuivre. Pour modifier des paramètres, cliquez sur **Précédent** jusqu'à ce que vous reveniez à la page appropriée, effectuez la modification et revenez à la page **Résumé** .  

###  <a name="a-namebkmkenablesuccesslogoneventsa-enable-auditing-of-success-logon-events"></a><a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 Utilisez la procédure suivante pour configurer les paramètres d'ouverture de session de la stratégie de sécurité des ordinateurs pour activer l'audit des événements associés aux ouvertures de session qui aboutissent.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>Pour activer la journalisation des événements associés aux ouvertures de session qui aboutissent en utilisant une stratégie de sécurité locale  

1.  Sur un ordinateur client Configuration Manager, cliquez sur **Démarrer**, pointez sur **Outils d’administration**, puis cliquez sur **Stratégie de sécurité locale**.  

2.  Dans la boîte de dialogue **Stratégie de sécurité locale** , sous **Paramètres de sécurité**, développez **Stratégies locales**, puis cliquez sur **Stratégie d'audit**.  

3.  Dans le volet des résultats, double-cliquez sur **Auditer les événements de connexion**, sélectionnez la case à cocher **Succès** et cliquez sur **OK**.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>Pour activer la journalisation des événements d'ouverture de session qui aboutissent en utilisant une stratégie de sécurité du domaine Active Directory  

1.  Sur un ordinateur contrôleur de domaine, cliquez sur **Démarrer**, pointez sur **Outils d'administration**, puis cliquez sur **Stratégie de sécurité du domaine**.  

2.  Dans la boîte de dialogue **Stratégie de sécurité locale** , sous **Paramètres de sécurité**, développez **Stratégies locales**, puis cliquez sur **Stratégie d'audit**.  

3.  Dans le volet des résultats, double-cliquez sur **Auditer les événements de connexion**, sélectionnez la case à cocher **Succès** et cliquez sur **OK**.  

###  <a name="a-namebkmkimportsoftwarelicenseinformationa-import-software-license-information"></a><a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 Les sections suivantes décrivent les procédures permettant d’importer des informations de licences logicielles Microsoft et générales dans la base de données de site Configuration Manager en utilisant l’Assistant Importer des licences logicielles. Lorsque vous importez des informations de licence de logiciel vers la base de données de site depuis des fichiers de déclaration de licence, le compte de l'ordinateur serveur de site doit disposer des autorisations **Contrôle intégral** pour le système de fichiers NTFS du partage de fichiers utilisé pour importer les informations de licence de logiciel.  

> [!IMPORTANT]  
>  Les informations de licence logicielle importées dans la base de données de site remplacent les informations existantes. Vérifiez que le fichier d'informations de licence logicielle que vous utilisez avec Assistant Importer des licences logicielles contient la liste complète des informations de licence logicielle nécessaires.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>Pour importer des informations de licence logicielle vers le catalogue Asset Intelligence  

1.  Dans l'espace de travail **Biens et conformité** , cliquez sur **Asset Intelligence**.  

2.  Dans l'onglet **Accueil** , dans le groupe **Asset Intelligence** , cliquez sur **Importer des licences logicielles**. L'Assistant Importer des licences logicielles s'ouvre.  

3.  Dans la page **Bienvenue** , cliquez sur **Suivant**.  

4.  Sur la page **Importer** , spécifiez si vous importez un fichier MVLS (Microsoft Volume Licensing) (.xml ou .csv) ou un fichier de déclaration de licence générale (.csv). Pour plus d'informations sur la création d'un fichier de déclaration de licence générale, voir [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) plus loin dans cette rubrique.  

    > [!WARNING]  
    >  Pour télécharger un fichier MVLS de format .csv que vous pouvez importer vers le catalogue Asset Intelligence, consultez [Centre de gestion des licences en volume Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=226547). Pour accéder à ces informations, vous devez disposer d'un compte enregistré sur le site Web. Vous devez contacter votre responsable de compte Microsoft pour plus d'informations sur la façon d'obtenir votre fichier MVLS de format .xml.  

5.  Entrez le chemin d'accès UNC du fichier de déclaration de licence ou cliquez sur **Parcourir** pour sélectionner un dossier réseau partagé et un fichier.  

    > [!NOTE]  
    >  Le dossier partagé doit être correctement sécurisé pour empêcher tout accès non autorisé au fichier d'informations de licence. En outre, le compte de l'ordinateur sur lequel l'Assistant est exécuté doit avoir les autorisations de contrôle intégral sur le partage contenant le fichier d'importation de licence.  

6.  Sur la page **Résumé** , vérifiez les informations que vous avez spécifiées pour vous assurer qu'elles sont correctes avant de poursuivre. Si vous souhaitez apporter des modifications, cliquez sur **Précédent** pour revenir à la page **Importer** .  

###  <a name="a-namebkmkcreategenerallicensestatementa-create-a-general-license-statement-information-file-for-import"></a><a name="BKMK_CreateGeneralLicenseStatement"></a> Create a general license statement information file for import  
 Une déclaration de licence générale peut également être importée vers le catalogue Asset Intelligence en utilisant un fichier d'importation de licence de format .csv (délimité par des virgules) créé manuellement.  

> [!NOTE]  
>  Seuls les champs **Nom**, **Éditeur**, **Version**et **Quantité effective** sont requis, mais ils doivent tous être entrés sur la première ligne du fichier d'importation de licence. Tous les champs de date doivent être affichés dans le format suivant : mois/jour/année, par exemple, 08/04/2008.  

 Asset Intelligence fait correspondre les produits que vous spécifiez dans la déclaration de licence générale en utilisant le nom du produit et la version du produit, mais pas le nom de l'éditeur. Vous devez utiliser un nom de produit dans la déclaration de licence générale qui correspond exactement au nom de produit stocké dans la base de données du site. Asset Intelligence utilise le nombre **Quantité effective** donné dans la déclaration de licence générale et le compare au nombre de produits installés trouvés dans l’inventaire Configuration Manager.  

> [!TIP]  
>  Pour obtenir la liste complète des noms de produits stockés dans la base de données du site Configuration Manager, exécutez la requête suivante sur la base de données du site : SELECT ProductName0 FROM v_GS_INSTALLED_SOFTWARE.  

 Vous pouvez spécifier les versions exactes pour un produit ou spécifier une partie de la version, comme par exemple uniquement la version principale. Les exemples suivants présentent les correspondances de version obtenues pour une entrée de version de déclaration générale de licence pour un produit spécifique.  

|Entrée de déclaration de licence générale|Correspondance avec les entrées de la base de données de site|  
|-------------------------------------|------------------------------------|  
|Name: "MySoftware", ProductVersion0:"2"|ProductName0: "Mysoftware", ProductVersion0: "2.01.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.02.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.10.1234"|  
|Name: "MySoftware", Version "2.05"|ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"|  
|Name: "Mysoftware", Version "2"<br /><br /> Name: "Mysoftware", Version "2.05"|Erreur lors de l'importation. L'importation échoue lorsque plusieurs entrées correspondent à la même version du produit.|  

 La procédure suivante décrit la création d'un fichier d'importation de déclaration de licence générale avec Microsoft Excel.  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>Pour créer un fichier d'importation de déclaration de licence générale à l'aide de Microsoft Excel  

1.  Ouvrez Microsoft Excel et créez une nouvelle feuille de calcul.  

2.  Sur la première ligne de la nouvelle feuille de calcul, saisissez tous les noms de champs de données des licences logicielles.  

3.  À partir de la deuxième ligne, entrez les informations de licence logicielle requises. Assurez-vous que tous les champs de données des licences logicielles requis sont saisis sur les lignes suivantes pour chaque licence logicielle qui doit être importée. Le nom de logiciel saisi dans la feuille de calcul doit être le même que le nom de logiciel affiché dans l'Explorateur de ressources pour un ordinateur client, après avoir exécuté l'inventaire matériel.  

4.  Dans le menu **Fichier** , cliquez sur **Enregistrer sous**, puis enregistrez le fichier au format .csv.  

5.  Copiez le fichier .csv dans le partage de fichiers utilisé pour l'importation des informations de licence logicielle dans le catalogue Asset Intelligence.  

6.  Dans la console Configuration Manager, utilisez l’Assistant Importer des licences logicielles pour importer le nouveau fichier d’informations de licence .csv créé.  

7.  Générez le **rapport de rapprochement des licences logicielles tierces (licence 15A)** d’Asset Intelligence pour vérifier que les informations de licence ont bien été importées dans le catalogue Asset Intelligence.  

> [!NOTE]  
>  Pour obtenir un exemple de fichier de licence logicielle générale que vous pouvez utiliser à des fins de test, consultez [Exemple de fichier d’importation de licence générale Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### <a name="sample-table-to-describe-software-licenses"></a>Exemple de tableau utilisé pour décrire des licences logicielles  
 Lors de la création d'un fichier d'importation de déclaration de licence générale, les informations figurant dans le tableau suivant peuvent être utilisées pour décrire les licences logicielles à importer dans le catalogue Asset Intelligence.  

|Nom de la colonne|Type de données|Obligatoire|Exemple|  
|-----------------|---------------|--------------|-------------|  
|Nom|Jusqu'à 255 caractères|Oui|Nom du logiciel|  
|Éditeur|Jusqu'à 255 caractères|Oui|Éditeur du logiciel|  
|Version|Jusqu'à 255 caractères|Oui|Version du logiciel|  
|Langage|Jusqu'à 255 caractères|Oui|Langue du logiciel|  
|Quantité effective|Valeur entière|Oui|Nombre de licences achetées|  
|Numéro BC|Jusqu'à 255 caractères|Non|Informations sur les BC|  
|Nom du revendeur|Jusqu'à 255 caractères|Non|Informations sur le revendeur|  
|Date d'achat|Date au format suivant : MM/JJ/AAAA|Non|Date d'achat de la licence|  
|Achat de la prise en charge|Valeur en bits|Non|0 ou 1 (0 pour Oui, 1 pour Non)|  
|Date d'expiration de la prise en charge|Date au format suivant : MM/JJ/AAAA|Non|Date de fin de la prise en charge achetée|  
|Commentaires|Jusqu'à 255 caractères|Non|Commentaires facultatifs|  

###  <a name="a-namebkmkconfiguremaintenancetasksa-configure-asset-intelligence-maintenance-tasks"></a><a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 Les tâches de maintenance suivantes sont disponibles pour Asset Intelligence :  

-   **Vérifier le titre de l’application à l’aide des informations d’inventaire**: cette tâche de maintenance vérifie si le nom du logiciel indiqué dans l’inventaire logiciel est rapproché du nom du logiciel figurant dans le catalogue Asset Intelligence. Par défaut, cette tâche est activée et planifiée pour être exécutée le samedi entre 00 h 00 et 5 h 00. Cette tâche de maintenance est uniquement disponible sur le site de niveau supérieur de la hiérarchie Configuration Manager.  

-   **Résumer les données du logiciel installé**: cette tâche de maintenance fournit les informations affichées dans l’espace de travail **Ressources et Conformité** , dans le nœud **Logiciels inventoriés** , sous le nœud **Asset Intelligence** . Quand la tâche s’exécute, Configuration Manager compte les titres de logiciels inventoriés sur le site principal. Par défaut, cette tâche est activée et planifiée pour être exécutée tous les jours entre 00 h 00 et 5 h 00. Cette tâche de maintenance est disponible uniquement sur les sites principaux.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>Pour configurer les tâches de maintenance Asset Intelligence  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Sites**.  

3.  Sélectionnez le site sur lequel vous allez configurer la tâche de maintenance Asset Intelligence.  

    > [!NOTE]  
    >  La tâche de maintenance **Résumer les données du logiciel installé** est disponible uniquement sur les sites principaux.  

4.  Dans l'onglet **Accueil** , dans le groupe **Paramètres** , cliquez sur **Maintenance de site**. Une liste de toutes les tâches de maintenance de site disponibles s'affiche.  

5.  Sélectionnez la tâche de maintenance souhaitée, puis cliquez sur **Modifier** pour modifier les paramètres.  

6.  Activez et configurez la tâche de maintenance. Pour réduire les interférences avec le fonctionnement du site, il est recommandé de définir la période en dehors des heures de pointe du site. La période représente l'intervalle de temps au cours duquel la tâche peut être exécutée. Elle est définie par les paramètres **Démarrer après** et **Heure de début au plus tard** spécifiés dans la boîte de dialogue **Propriétés de la tâche** .  

    > [!WARNING]  
    >  Vous pouvez lancer immédiatement la tâche en sélectionnant le jour actuel et en réglant la valeur **Démarrer après** quelques minutes après le moment présent.  

7.  Cliquez sur **OK** pour enregistrer vos paramètres. La tâche est désormais exécutée conformément à sa planification.  

    > [!NOTE]  
    >  Si l’exécution d’une tâche échoue à la première tentative, Configuration Manager retente de l’exécuter jusqu’à la réussite de l’opération ou l’expiration de la période d’exécution planifiée.  



<!--HONumber=Nov16_HO1-->


