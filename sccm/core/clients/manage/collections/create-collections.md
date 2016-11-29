---
title: "Créer des regroupements | System Center Configuration Manager"
description: "Créez des regroupements dans System Center Configuration Manager pour faciliter la gestion des groupes d’utilisateurs et d’appareils."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f73f0e58b82d1aab1f64f3695dd5c3a61e933d2a


---
# <a name="how-to-create-collections-in-system-center-configuration-manager"></a>Guide pratique pour créer des regroupements dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Créez des regroupements dans System Center Configuration Manager pour représenter des groupements logiques d’utilisateurs et d’appareils. Vous pouvez utiliser des regroupements pour effectuer de nombreuses tâches, telles que gérer les applications, déployer des paramètres de compatibilité ou installer des mises à jour logicielles. Vous pouvez également utiliser des regroupements pour gérer des groupes de paramètres client ou les utiliser avec l’administration basée sur les rôles pour définir les ressources auxquelles un utilisateur administratif peut accéder. Configuration Manager contient plusieurs regroupements intégrés. Pour plus d’informations, consultez [Présentation des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).  

> [!NOTE]  
>  Un regroupement unique peut contenir des utilisateurs ou des appareils, mais pas les deux.  

 Le tableau suivant répertorie les règles que vous pouvez utiliser pour configurer les membres d’un regroupement dans Configuration Manager.  

|Type de règle d'appartenance|Plus d'informations|  
|--------------------------|----------------------|  
|Règle directe|Les règles directes permettent de choisir les utilisateurs ou les ordinateurs à ajouter comme membres à un regroupement. Une règle directe permet de contrôler directement les ressources qui sont membres d'un regroupement. Cette appartenance ne change pas, à moins qu’une ressource soit supprimée de Configuration Manager. Configuration Manager doit avoir découvert les ressources ou vous devez les avoir importées pour pouvoir les ajouter à un regroupement à règle directe. Les regroupements à règle directe ont une charge administrative plus élevée que les regroupements à règle de requête, car vous devez modifier manuellement ce type de regroupement.|  
|Règle de requête|Les règles de requête mettent à jour dynamiquement l’appartenance à un regroupement en fonction d’une requête que Configuration Manager exécute selon une planification. Par exemple, vous pouvez créer un regroupement d'utilisateurs membres de l'unité d'organisation Ressources Humaines dans les services de domaine Active Directory. Contrairement aux regroupements à règle directe, cette appartenance de regroupement est automatiquement mise à jour lorsque de nouveaux utilisateurs sont ajoutés ou supprimés de l'unité d'organisation Ressources Humaines.<br /><br /> Pour examiner des exemples de requêtes que vous pouvez utiliser pour créer des regroupements, consultez [Guide pratique pour créer des requêtes dans System Center Configuration Manager](../../../../core/servers/manage/create-queries.md).|  
|Règle Inclure des regroupements|La règle Inclure des regroupements permet d’inclure les membres d’un autre regroupement dans un regroupement Configuration Manager. L’appartenance au regroupement actif est mise à jour selon une planification si l’appartenance au regroupement inclus a changé.<br /><br /> Vous pouvez ajouter plusieurs règles d’inclusion de regroupement à un regroupement.<br />              **Exemple :** vous créez un regroupement qui comporte deux règles d’inclusion de regroupement. La première règle concerne un regroupement d’ordinateurs portables tandis que la seconde concerne un regroupement d’ordinateurs de bureau. Le nouveau regroupement contient tous les membres du regroupement d’ordinateurs portables et du regroupement d’ordinateurs de bureau.|  
|Règle Exclure des regroupements|La règle Exclure des regroupements permet d’exclure les membres d’un autre regroupement d’un regroupement Configuration Manager. L'appartenance du regroupement actuel est mise à jour selon une planification si l'appartenance du regroupement exclu a été modifiée.<br /><br /> Vous pouvez ajouter plusieurs règles d’exclusion de regroupement à un regroupement. Si un regroupement inclut des règles d'inclusion et d'exclusion de regroupement et qu'il existe un conflit, la règle d'exclusion prévaut sur la règle d'inclusion.<br />              **Exemple :** vous créez un regroupement qui comporte une seule règle d’inclusion de regroupement et une seule règle d’exclusion de regroupement. La règle d’inclusion concerne un regroupement d’ordinateurs de bureau Dell. La règle d’exclusion concerne un regroupement d’ordinateurs qui possèdent moins de 4 Go de RAM. Le nouveau regroupement contient les ordinateurs de bureau Dell qui ont au moins 4 Go de RAM.|  

 Utilisez les procédures suivantes pour créer des regroupements dans Configuration Manager. Vous pouvez aussi importer des regroupements créés sur ce site ou sur un autre site Configuration Manager. Pour plus d’informations sur l’exportation des regroupements, consultez [Guide pratique pour gérer des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

 Pour plus d’informations sur la création de regroupements pour des ordinateurs qui exécutent Linux et UNIX, consultez [Guide pratique pour gérer les clients pour des serveurs Linux et UNIX dans System Center Configuration Manager](../../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md).  

##  <a name="a-namebkmk1a-to-create-a-device-collection"></a><a name="BKMK_1"></a> Pour créer un regroupement d’appareils  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , cliquez sur **Regroupements d’appareils**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un regroupement de périphériques**.  

4.  Sur la page **Général** de l' **Assistant Création d'un regroupement de périphériques**, spécifiez les informations suivantes :  

    -   **Nom**: spécifiez un nom unique pour le regroupement.  

    -   **Commentaire**: décrivez le regroupement.  

    -   **Limitation au regroupement**: cliquez sur **Parcourir** pour sélectionner une limitation au regroupement. Le regroupement que vous créez contiendra uniquement les membres de la limitation au regroupement.  

5.  Sur la page **Règles d'adhésion** de l' **Assistant Création d'un regroupement de périphériques**, spécifiez les informations suivantes :  

    -   Dans la liste **Ajouter une règle** , sélectionnez le type de règle d'adhésion à utiliser pour le regroupement. Vous pouvez configurer plusieurs règles pour chaque regroupement.  

         Utilisez les procédures suivantes pour configurer chaque type de règle d'adhésion.  

        ##### <a name="to-configure-a-direct-rule"></a>Pour configurer une règle directe  

        1.  Sur la page **Rechercher des ressources** de l' **Assistant Création d'une règle d'adhésion directe**, spécifiez les informations suivantes :  

            -   **Classe de ressource**: dans la liste, sélectionnez le type de ressource à rechercher et à ajouter au regroupement. Sélectionnez dans les valeurs **Ressource Système** pour rechercher des données d'inventaire renvoyées par les ordinateurs clients ou **Ordinateur inconnu** pour sélectionner dans les valeurs renvoyées par les ordinateurs inconnus.  

            -   **Nom d’attribut**: dans la liste, sélectionnez l’attribut associé à la classe de ressource sélectionnée à rechercher. Par exemple, si vous souhaitez sélectionner des ordinateurs par leur nom NetBIOS, sélectionnez **Ressource Système** dans la liste **Classe de ressource** et **NetBIOS nom** dans la liste **Nom d'attribut** .  

            -   **Exclure les ressources signalées comme obsolètes** : si un ordinateur client est signalé comme obsolète, n’incluez pas cette valeur dans les résultats de recherche.  

            -   **Exclure les ressources sur lesquelles le client Configuration Manager n’est pas installé** : si les résultats de recherche contiennent une ressource sur laquelle le client Configuration Manager n’est pas installé, cette ressource ne figure pas dans les résultats de recherche.  

            -   **Valeur :** entrez une valeur pour laquelle vous voulez rechercher le nom d’attribut sélectionné. Vous pouvez utiliser le caractère de pourcentage ( **%** ) comme caractère générique. Par exemple, si vous voulez rechercher les ordinateurs dont le nom NetBIOS commence par « M », entrez **M%** dans ce champ.  

        2.  Dans la page **Sélectionner les ressources** de l' **Assistant Création d'une règle d'adhésion directe**, sélectionnez les ressources à ajouter au regroupement dans la liste **Ressources** et cliquez sur **Suivant**.  

        3.  Terminez les opérations dans l' **Assistant Création d'une règle d'adhésion directe**.  

        ##### <a name="to-configure-a-query-rule"></a>Pour configurer une règle de requête  

        1.  Dans la boîte de dialogue **Propriétés de la règle de requête** , définissez les options suivantes :  

            -   **Nom**: spécifiez un nom unique pour la règle de requête.  

            -   **Importer l’instruction de requête** : ouvre la boîte de dialogue **Parcourir la requête** dans laquelle vous pouvez sélectionner une requête Configuration Manager à utiliser comme règle de requête pour le regroupement. Pour plus d’informations sur la création de ces requêtes et pour obtenir des exemples, consultez [Guide pratique pour créer des requêtes dans System Center Configuration Manager](../../../../core/servers/manage/create-queries.md).  

            -   **Classe de ressource :** dans la liste, sélectionnez le type de ressource à rechercher et à ajouter au regroupement. Sélectionnez dans les valeurs **Ressource système** pour rechercher des données d'inventaire renvoyées par les ordinateurs clients ou **Ordinateur inconnu** pour sélectionner dans les valeurs renvoyées par les ordinateurs inconnus.  

            -   **Modifier l’instruction de requête** : ouvre la boîte de dialogue **Propriétés de l’instruction de requête** dans laquelle vous pouvez créer une requête à utiliser comme règle pour le regroupement. Pour plus d’informations sur les requêtes, consultez [Informations techniques de référence sur les requêtes pour System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

        2.  Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés de la règle de requête** et enregistrer la règle de requête d'adhésion.  

        ##### <a name="to-configure-an-include-collection-rule"></a>Pour configurer une règle d'inclusion de regroupements  

        1.  Dans la boîte de dialogue **Sélectionner des regroupements** , sélectionnez les regroupements à inclure dans le nouveau regroupement.  

        2.  Cliquez sur **OK** pour fermer la boîte de dialogue **Sélectionner des regroupements** et enregistrer la règle d'inclusion d'adhésion.  

        ##### <a name="to-configure-an-exclude-collection-rule"></a>Pour configurer une règle d'exclusion de regroupements  

        1.  Dans la boîte de dialogue **Sélectionner des regroupements** , sélectionnez les regroupements à exclure du nouveau regroupement.  

        2.  Cliquez sur **OK** pour fermer la boîte de dialogue **Sélectionner des regroupements** et enregistrer la règle d'exclusion d'adhésion.  

    -   **Utiliser des mises à jour incrémentielles pour ce regroupement** : sélectionnez cette option pour rechercher régulièrement les ressources nouvelles ou modifiées dans l’évaluation de regroupement précédente et mettre à jour l’appartenance au regroupement avec uniquement ces ressources, indépendamment d’une évaluation de regroupement complète. Les mises à jour incrémentielles ont lieu toutes les 10 minutes.  

        > [!IMPORTANT]  
        >  Les regroupements configurés à l'aide de règles de requête qui utilisent les classes suivantes ne prennent pas en charge les mises à jour incrémentielles :  
        >   
        >  -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (pour les regroupements d'utilisateurs uniquement)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (pour les regroupements d'utilisateurs uniquement)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    -   **Planifier une mise à jour complète sur ce regroupement** : sélectionnez cette option pour planifier une évaluation complète régulière de l’appartenance au regroupement.  

6.  Terminez l'Assistant pour créer le regroupement. Le nouveau regroupement figure dans le noeud **Regroupements de périphériques** de l'espace de travail **Biens et conformité** .  

> [!NOTE]  
>  Vous devez actualiser ou recharger la console Configuration Manager pour voir les membres du regroupement. Toutefois, les membres n’apparaissent pas dans le regroupement tant que la première mise à jour planifiée n’est pas effectuée ou que vous ne sélectionnez pas manuellement **Mettre à jour l’adhésion** pour le regroupement. Selon la complexité de la règle de regroupement et le nombre d’entrées dans la base de données Configuration Manager, la mise à jour d’un regroupement peut durer quelques minutes.  

##  <a name="a-namebkmk2a-to-create-a-user-collection"></a><a name="BKMK_2"></a> Pour créer un regroupement d’utilisateurs  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Biens et conformité** , cliquez sur **Regroupements d'utilisateurs**.  

3.  Sur l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un regroupement d'utilisateurs**.  

4.  Sur la page **Général** de l' **Assistant Création d'un regroupement d'utilisateurs**, spécifiez les informations suivantes :  

    -   **Nom**: spécifiez un nom unique pour le regroupement.  

    -   **Commentaire**: décrivez le regroupement.  

    -   **Limitation au regroupement**: cliquez sur **Parcourir** pour sélectionner une limitation au regroupement. Le regroupement que vous créez contiendra uniquement les membres de la limitation au regroupement.  

5.  Sur la page **Règles d'adhésion** de l' **Assistant Création d'un regroupement d'utilisateurs**, spécifiez les informations suivantes :  

    -   dans la liste **Ajouter une règle** , sélectionnez le type de règle d'adhésion à utiliser pour le regroupement. Vous pouvez configurer plusieurs règles pour chaque regroupement.  

         Utilisez les procédures suivantes pour configurer chaque type de règle d'adhésion.  

        ##### <a name="to-configure-a-direct-rule"></a>Pour configurer une règle directe  

        1.  Sur la page **Rechercher des ressources** de l' **Assistant Création d'une règle d'adhésion directe**, spécifiez les informations suivantes :  

            -   **Classe de ressource**: dans la liste, sélectionnez le type de ressource à rechercher et à ajouter au regroupement. Sélectionnez des valeurs **Ressource utilisateur** pour rechercher les informations utilisateur collectées par Configuration Manager ou **Ressource groupe d’utilisateurs** pour rechercher les informations sur les groupes d’utilisateurs collectées par Configuration Manager.  

            -   **Nom d’attribut**: dans la liste, sélectionnez l’attribut associé à la classe de ressource sélectionnée à rechercher. Par exemple, si vous voulez sélectionner des utilisateurs par leur nom d’unité d’organisation (UO), sélectionnez **Ressource utilisateur** dans la liste **Classe de ressource** et **Nom de l’unité d’organisation utilisateur** dans la liste **Nom d’attribut** .  

            -   **Valeur** : entrez une valeur pour laquelle vous voulez rechercher le nom d’attribut sélectionné. Vous pouvez utiliser le caractère de pourcentage ( **%** ) comme caractère générique. Par exemple, si vous voulez rechercher des utilisateurs dans l’unité d’organisation Contoso, entrez **Contoso** dans ce champ.  

        2.  Dans la page **Sélectionner les ressources** de l' **Assistant Création d'une règle d'adhésion directe**, sélectionnez les ressources à ajouter au regroupement dans la liste **Ressources** et cliquez sur **Suivant**.  

        3.  Terminez les opérations dans l' **Assistant Création d'une règle d'adhésion directe**.  

        ##### <a name="to-configure-a-query-rule"></a>Pour configurer une règle de requête  

        1.  Dans la boîte de dialogue **Propriétés de la règle de requête** , définissez les options suivantes :  

            -   **Nom**: spécifiez un nom unique pour la règle de requête.  

            -   **Importer l’instruction de requête** : ouvre la boîte de dialogue **Parcourir la requête** dans laquelle vous pouvez sélectionner une requête Configuration Manager à utiliser comme règle de requête pour le regroupement. Pour plus d’informations sur les requêtes, consultez [Informations techniques de référence sur les requêtes pour System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

            -   **Classe de ressource**: dans la liste, sélectionnez le type de ressource à rechercher et à ajouter au regroupement. Sélectionnez des valeurs **Ressource utilisateur** pour rechercher les informations utilisateur collectées par Configuration Manager ou **Ressource groupe d’utilisateurs** pour rechercher les informations sur les groupes d’utilisateurs collectées par Configuration Manager.  

            -   **Modifier l’instruction de requête** : ouvre la boîte de dialogue **Propriétés de l’instruction de requête** dans laquelle vous pouvez créer une requête à utiliser comme règle pour le regroupement. Pour plus d’informations sur les requêtes, consultez [Informations techniques de référence sur les requêtes pour System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

        2.  Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés de la règle de requête** et enregistrer la règle de requête d'adhésion.  

        ##### <a name="to-configure-an-include-collection-rule"></a>Pour configurer une règle d'inclusion de regroupements  

        1.  Dans la boîte de dialogue **Sélectionner des regroupements** , sélectionnez les regroupements à inclure dans le nouveau regroupement.  

        2.  Cliquez sur **OK** pour fermer la boîte de dialogue **Sélectionner des regroupements** et enregistrer la règle d'inclusion d'adhésion.  

        ##### <a name="to-configure-an-exclude-collection-rule"></a>Pour configurer une règle d'exclusion de regroupements  

        1.  Dans la boîte de dialogue **Sélectionner des regroupements** , sélectionnez les regroupements à exclure du nouveau regroupement.  

        2.  Cliquez sur **OK** pour fermer la boîte de dialogue **Sélectionner des regroupements** et enregistrer la règle d'exclusion d'adhésion.  

    -   **Utiliser des mises à jour incrémentielles pour ce regroupement** : sélectionnez cette option pour rechercher régulièrement les ressources nouvelles ou modifiées dans l’évaluation de regroupement précédente et mettre à jour l’appartenance au regroupement avec uniquement ces ressources, indépendamment d’une évaluation de regroupement complète. Les mises à jour incrémentielles ont lieu toutes les 10 minutes.  

        > [!IMPORTANT]  
        >  Les regroupements configurés à l'aide de règles de requête qui utilisent les classes suivantes ne prennent pas en charge les mises à jour incrémentielles :  
        >   
        >  -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (pour les regroupements d'utilisateurs uniquement)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (pour les regroupements d'utilisateurs uniquement)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    -   **Planifier une mise à jour complète sur ce regroupement** : sélectionnez cette option pour planifier une évaluation complète régulière de l’appartenance au regroupement.  

6.  Terminez l'Assistant pour créer le regroupement. Le nouveau regroupement figure dans le noeud **Regroupements d'utilisateurs** de l'espace de travail **Biens et conformité** .  

> [!NOTE]  
>  Vous devez actualiser ou recharger la console Configuration Manager pour voir les membres du regroupement. Toutefois, les membres n’apparaissent pas dans le regroupement tant que la première mise à jour planifiée n’est pas effectuée ou que vous ne sélectionnez pas manuellement **Mettre à jour l’adhésion** pour le regroupement. Selon la complexité de la règle de regroupement et le nombre d’entrées dans la base de données Configuration Manager, la mise à jour d’un regroupement peut durer quelques minutes.  

##  <a name="a-namebkmk3a-to-import-a-collection"></a><a name="BKMK_3"></a> Pour importer un regroupement  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Biens et conformité** , cliquez sur **Regroupement d'utilisateurs** ou **Regroupements de périphériques**.  

3.  Dans l'onglet **Accueil** dans le groupe **Créer** , cliquez sur **Importer des regroupements**.  

4.  Sur la page **Général** de l' **Assistant Importation de regroupements**, cliquez sur **Suivant**.  

5.  Sur la page **Nom du fichier MOF** , cliquez sur **Parcourir** , puis accédez au fichier MOF qui contient les informations de regroupement à importer.  

    > [!NOTE]  
    >  Le fichier à importer doit avoir été exporté à partir d’un site exécutant la même version de Configuration Manager que celui-ci. Pour plus d’informations sur l’exportation de regroupements, consultez [Guide pratique pour gérer des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

6.  Terminez l'Assistant pour importer le regroupement. Le nouveau regroupement figure dans le nœud **Regroupements d’utilisateurs** ou **Regroupements de périphériques** de l’espace de travail **Ressources et Conformité** .  

> [!NOTE]  
>  Vous devez actualiser ou recharger la console Configuration Manager pour afficher les membres du regroupement récemment importé.  



<!--HONumber=Nov16_HO1-->


