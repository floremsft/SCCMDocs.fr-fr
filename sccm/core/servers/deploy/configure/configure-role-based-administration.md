---
title: "Configurer l’administration basée sur des rôles | System Center Configuration Manager"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 8c67fb351fff7f362ca3845c2cc67d222b6477b8


---
# <a name="configure-role-based-administration-for-system-center-configuration-manager"></a>Configurer l’administration basée sur des rôles pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, l’administration basée sur des rôles combine des rôles de sécurité, des étendues de sécurité et des regroupements attribués pour définir l’étendue administrative de chaque utilisateur administratif. L’étendue administrative inclut les objets qu’un utilisateur administratif peut afficher dans la console Configuration Manager et les tâches associées à ces objets que cet utilisateur est autorisé à exécuter. Les configurations d'administration basée sur des rôles s'appliquent à chaque site dans une hiérarchie.  

 Si vous n’êtes pas encore familiarisé avec les concepts de l’administration basée sur des rôles, consultez [Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Les informations figurant dans les procédures suivantes peuvent vous aider à créer et à configurer une administration basée sur des rôles ainsi que les paramètres de sécurité correspondants.  

-   [Créer des rôles de sécurité personnalisés](#BKMK_CreateSecRole)  

-   [Configurer des rôles de sécurité](#BKMK_ConfigSecRole)  

-   [Configurer des étendues de sécurité pour un objet](#BKMK_ConfigSecScope)  

-   [Configurer des regroupements pour gérer la sécurité](#BKMK_ConfigColl)  

-   [Créer un utilisateur administratif](#BKMK_Create_AdminUser)  

-   [Modifier l’étendue administrative d’un utilisateur administratif](#BKMK_ModAdminUser)  

##  <a name="a-namebkmkcreatesecrolea-create-custom-security-roles"></a><a name="BKMK_CreateSecRole"></a> Créer des rôles de sécurité personnalisés  
 Configuration Manager fournit plusieurs rôles de sécurité intégrés. Si vous avez besoin de rôles de sécurité supplémentaires, vous pouvez créer un rôle de sécurité personnalisé à l'aide d'une copie d'un rôle de sécurité existant, que vous modifiez par la suite. Vous pouvez créer un rôle de sécurité personnalisé pour accorder aux utilisateurs administratifs les autorisations de sécurité supplémentaires dont ils ont besoin et qui ne figurent pas dans le rôle de sécurité actuellement attribué. Un rôle de sécurité personnalisé permet de leur accorder uniquement les autorisations dont ils ont besoin sans pour autant leur attribuer un rôle de sécurité avec plus d'autorisations que nécessaire.  

 Pour créer un rôle de sécurité à l'aide d'un rôle de sécurité existant en tant que modèle, procédez comme suit.  

#### <a name="to-create-custom-security-roles"></a>Pour créer des rôles de sécurité personnalisés  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Sécurité**, puis cliquez sur **Rôles de sécurité**.  

     Utilisez l'une des procédures suivantes pour créer le rôle de sécurité :  

    -   Pour créer un rôle de sécurité personnalisé, effectuez les actions suivantes :  

        1.  Sélectionnez un rôle de sécurité existant à utiliser comme source pour le nouveau rôle de sécurité.  

        2.  Dans l'onglet **Accueil** , dans le groupe **Rôle de sécurité** , cliquez sur **Copier**. Vous créez ainsi une copie du rôle de sécurité source.  

        3.  Dans l'Assistant Copier le rôle de sécurité, spécifiez un **Nom** pour le nouveau rôle de sécurité personnalisé.  

        4.  Dans **Attributions d'opérations de sécurité**, développez chaque nœud **Opérations de sécurité** pour afficher les actions disponibles.  

        5.  Pour modifier le paramètre d'une opération de sécurité, cliquez sur la flèche vers le bas dans la colonne **Valeur** , puis sélectionnez **Oui** ou **Non**.  

            > [!CAUTION]  
            >  Lorsque vous configurez un rôle de sécurité personnalisé, assurez-vous que ne pas accorder des autorisations dont les utilisateurs administratifs associés au nouveau rôle de sécurité n'ont pas besoin. Par exemple, la valeur **Modifier** pour l'opération de sécurité **Rôles de sécurité** accorde aux utilisateurs administratifs l'autorisation de modifier tout rôle accessible, même s'ils ne sont pas associés à ce rôle de sécurité.  

        6.  Après avoir configuré les autorisations, cliquez sur **OK** pour enregistrer le nouveau rôle de sécurité.  

    -   Pour importer un rôle de sécurité exporté à partir d’une autre hiérarchie Configuration Manager, effectuez les actions suivantes :  

        1.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Importer un rôle de sécurité**.  

        2.  Spécifiez le fichier .xml contenant la configuration de rôle de sécurité que vous souhaitez importer, puis cliquez sur **Ouvrir** pour terminer la procédure et enregistrer le rôle de sécurité.  

            > [!NOTE]  
            >  Après avoir importé un rôle de sécurité, vous pouvez en modifier les propriétés pour changer les autorisations d'objet associées au rôle de sécurité.  

##  <a name="a-namebkmkconfigsecrolea-configure-security-roles"></a><a name="BKMK_ConfigSecRole"></a> Configurer des rôles de sécurité  
 Les groupes d'autorisations de sécurité définis pour un rôle de sécurité sont appelés des attributions d'opérations de sécurité. Les attributions d'opérations de sécurité représentent une association de types d'objet et d'actions disponibles pour chaque type d'objet. Vous pouvez modifier les opérations de sécurité disponibles pour tout rôle de sécurité personnalisé, mais vous ne pouvez pas modifier les rôles de sécurité intégrés qui sont fournis par Configuration Manager.  

 Utilisez la procédure suivante pour modifier les opérations de sécurité pour un rôle de sécurité.  

#### <a name="to-modify-security-roles"></a>Pour modifier des rôles de sécurité  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Sécurité**, puis cliquez sur **Rôles de sécurité**.  

3.  Sélectionnez le rôle de sécurité personnalisé à modifier.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Cliquez sur l'onglet **Autorisations** .  

6.  Dans **Attributions d'opérations de sécurité**, développez chaque nœud **Opérations de sécurité** pour afficher les actions disponibles.  

7.  Pour modifier le paramètre d'une opération de sécurité, cliquez sur la flèche vers le bas dans la colonne **Valeur** , puis sélectionnez **Oui** ou **Non**.  

    > [!CAUTION]  
    >  Lorsque vous configurez un rôle de sécurité personnalisé, assurez-vous que ne pas accorder des autorisations dont les utilisateurs administratifs associés au nouveau rôle de sécurité n'ont pas besoin. Par exemple, la valeur **Modifier** pour l'opération de sécurité **Rôles de sécurité** accorde aux utilisateurs administratifs l'autorisation de modifier tout rôle accessible, même s'ils ne sont pas associés à ce rôle de sécurité.  

8.  Après avoir terminé la configuration des attributions d'opérations de sécurité, cliquez sur **OK** pour enregistrer le nouveau rôle de sécurité.  

##  <a name="a-namebkmkconfigsecscopea-configure-security-scopes-for-an-object"></a><a name="BKMK_ConfigSecScope"></a> Configurer des étendues de sécurité pour un objet  
 L'association d'une étendue de sécurité pour un objet est gérée à partir de l'objet et non à partir de l'étendue de sécurité. Les seules configurations directes prises en charge par l'étendue de sécurité sont les modifications apportées à son nom et à sa description. Pour modifier le nom et la description d'une étendue de sécurité lorsque vous affichez les propriétés d'étendue de sécurité, vous devez disposer de l'autorisation **Modifier** pour l'objet sécurisable **Étendues de sécurité** .  

 Quand vous créez un objet dans Configuration Manager, il est associé à chaque étendue de sécurité qui est associée aux rôles de sécurité du compte utilisé pour créer l’objet si ces rôles de sécurité fournissent l’autorisation **Créer** ou l’autorisation **Définir l’étendue de sécurité**. Une fois l'objet créé, vous pouvez modifier les étendues de sécurité associées.  

 Par exemple, un rôle de sécurité accordant l'autorisation de créer un groupe de limites vous est attribué. Lorsque vous créez un groupe de limites, vous ne disposez pas d'option à laquelle vous pouvez attribuer des étendues de sécurité spécifiques. Au lieu de cela, les étendues de sécurité disponibles des rôles de sécurité auxquels vous êtes associé sont attribués automatiquement au nouveau groupe de limites. Après l'enregistrement du nouveau groupe de limites, vous pouvez modifier les étendues de sécurité associées au nouveau groupe limites.  

 Utilisez la procédure suivante pour configurer les étendues de sécurité attribuées à un objet.  

#### <a name="to-configure-security-scopes-for-an-object"></a>Pour configurer des étendues de sécurité pour un objet  

1.  Dans la console Configuration Manager, sélectionnez un objet prenant en charge l’attribution à une étendue de sécurité.  

2.  Dans l'onglet **Accueil** , dans le groupe **Classer** , cliquez sur **Définir des étendues de sécurité**.  

3.  Dans la boîte de dialogue **Définir des étendues de sécurité** , activez ou désactivez les étendues de sécurité auxquelles cet objet est associé. Chaque objet prenant en charge des étendues de sécurité doit être attribué à une étendue de sécurité au moins.  

4.  Cliquez sur **OK** pour enregistrer les étendues de sécurité attribuées.  

    > [!NOTE]  
    >  Lorsque vous créez un objet, vous pouvez l'attribuer à plusieurs étendues de sécurité. Pour modifier le nombre d'étendues de sécurité associées à l'objet, vous devez modifier cette attribution une fois que l'objet a été créé.  

##  <a name="a-namebkmkconfigcolla-configure-collections-to-manage-security"></a><a name="BKMK_ConfigColl"></a> Configurer des regroupements pour gérer la sécurité  
 Aucune procédure de configuration de regroupements n'est disponible pour l'administration basée sur des rôles. Il n'existe pas de configuration d'administration basée sur des rôles pour les regroupements ; à la place, vous attribuez des regroupements à un utilisateur administratif lorsque vous configurez ce dernier. Les opérations de sécurité du regroupement qui sont activées dans les rôles de sécurité attribués aux utilisateurs déterminent les autorisations d'un utilisateur administratif en ce qui concerne les regroupements et les ressources du regroupement (membres du regroupement).  

 Lorsqu'un utilisateur administratif dispose d'autorisations sur un regroupement, il dispose également d'autorisations sur des regroupements limités à ce regroupement. Par exemple, votre organisation utilise un regroupement nommé Tous les postes de travail, et il existe un regroupement nommé Tous les bureaux en Amérique du Nord qui est limité au regroupement Tous les postes de travail. Si un utilisateur administratif dispose des autorisations sur Tous les postes de travail, il dispose également des mêmes autorisations sur le regroupement Tous les bureaux en Amérique du Nord. De plus, un utilisateur administratif ne peut pas utiliser l'autorisation **Supprimer** ou **Modifier** sur un regroupement qui lui est directement attribué ; il peut toutefois utiliser ces autorisations sur les regroupements limités à ce regroupement. Basé sur l'exemple précédent, l'utilisateur administratif peut supprimer ou modifier le regroupement Tous les bureaux en Amérique du Nord, mais il ne peut pas supprimer ou modifier le regroupement Tous les postes de travail.  

##  <a name="a-namebkmkcreateadminusera-create-a-new-administrative-user"></a><a name="BKMK_Create_AdminUser"></a> Créer un utilisateur administratif  
 Pour accorder aux personnes ou aux membres d’un groupe de sécurité l’accès pour gérer Configuration Manager, créez un utilisateur administratif dans Configuration Manager et spécifiez le compte Windows de l’utilisateur ou du groupe d’utilisateurs. Au moins un rôle de sécurité et une étendue de sécurité doivent être attribués à chaque utilisateur administratif dans Configuration Manager. Vous pouvez également attribuer des regroupements pour limiter l'étendue administrative de l'utilisateur administratif.  

 Utilisez les procédures suivantes pour créer de nouveaux utilisateurs administratifs.  

#### <a name="to-create-a-new-administrative-user"></a>Pour créer un nouvel utilisateur administratif  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Sécurité**, puis cliquez sur **Utilisateurs administratifs**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Ajouter un utilisateur ou un groupe**.  

4.  Cliquez sur **Parcourir** , puis sélectionnez le compte d'utilisateur ou le groupe à utiliser pour ce nouvel utilisateur administratif.  

    > [!NOTE]  
    >  Pour l'administration basée sur la console, seuls les utilisateurs du domaine ou les groupes de sécurité peuvent devenir des utilisateurs administratifs.  

5.  Pour les **Rôles de sécurité associés**, cliquez sur **Ajouter** pour ouvrir la liste des rôles de sécurité disponibles, cochez la case d'un ou plusieurs rôles de sécurité, puis cliquez sur **OK**.  

6.  Sélectionnez l'une des deux options suivantes pour définir le comportement de l'objet sécurisable pour le nouvel utilisateur :  

    -   **Tous les objets sécurisables pertinents pour les rôles de sécurité auxquels ils sont associés**: cette option associe l’utilisateur administratif à l’étendue de sécurité **Tout** ainsi qu’aux regroupements intégrés de niveau racine pour **Tous les systèmes**et **Tous les utilisateurs et groupes d’utilisateurs** . Les rôles de sécurité attribués à l'utilisateur définissent l'accès aux objets. Les nouveaux objets créés par cet utilisateur administratif sont attribués à l'étendue de sécurité **Par défaut** .  

    -   **Seuls les objets sécurisables dans les étendues de sécurité ou les regroupements spécifiés**: par défaut, cette option associe l’utilisateur administratif avec l’étendue de sécurité **Par défaut** et les regroupements **Tous les systèmes** et **Tous les utilisateurs et groupes d’utilisateurs** . Toutefois, les étendues de sécurité et les regroupements réels sont limités à ceux qui sont associés au compte que vous avez utilisé pour créer le nouvel utilisateur administratif. Cette option prend en charge l'ajout ou la suppression d'étendues de sécurité et de regroupements pour personnaliser l'étendue administrative de l'utilisateur administratif.  

    > [!IMPORTANT]  
    >  Les options précédentes associent chaque étendue de sécurité et regroupement attribué à chaque rôle de sécurité attribué à l'utilisateur administratif. Une troisième option, **Seuls les objets sécurisables définis par les rôles de sécurité de l'utilisateur administratif**peut être utilisée pour associer des rôles de sécurité individuels à des étendues de sécurité et des regroupements spécifiques. Cette troisième option est disponible après la création du nouvel utilisateur administratif, lorsque vous modifiez l'utilisateur administratif.  

7.  Selon l'option sélectionnée à l'étape 6, effectuez l'action suivante :  

    -   Si vous avez sélectionné **Tous les objets sécurisables pertinents pour les rôles de sécurité auxquels ils sont associés**, cliquez sur **OK** pour terminer cette procédure.  

    -   Si vous avez sélectionné **Seuls les objets sécurisables dans des étendues de sécurité ou des regroupements spécifiés**, vous pouvez cliquer sur **Ajouter** pour sélectionner des regroupements ou des étendues de sécurité supplémentaires, ou sélectionner un ou plusieurs objets dans la liste, puis cliquer sur **Supprimer** pour les supprimer. Cliquez sur **OK** pour terminer cette procédure.  

##  <a name="a-namebkmkmodadminusera-modify-the-administrative-scope-of-an-administrative-user"></a><a name="BKMK_ModAdminUser"></a> Modifier l’étendue administrative d’un utilisateur administratif  
 Vous pouvez modifier l'étendue administrative d'un utilisateur administratif en ajoutant ou en supprimant des rôles de sécurité, des étendues de sécurité et des regroupements associés à l'utilisateur. Chaque utilisateur administratif doit être associé à au moins un rôle de sécurité et une étendue de sécurité. Vous devrez peut-être affecter un ou plusieurs regroupements à l'étendue administrative de l'utilisateur. La plupart des rôles de sécurité interagissent avec les regroupements et ne fonctionnent pas correctement sans regroupement attribué.  

 Lorsque vous modifiez un utilisateur administratif, vous pouvez modifier le comportement des objets sécurisables au niveau de leur association avec les rôles de sécurité attribués. Les trois comportements que vous pouvez sélectionner sont les suivants :  

-   **Tous les objets sécurisables pertinents pour les rôles de sécurité auxquels ils sont associés**: cette option associe l’utilisateur administratif à l’étendue **Tout** ainsi qu’aux regroupements intégrés de niveau racine pour **Tous les systèmes**et **Tous les utilisateurs et groupes d’utilisateurs**. Les rôles de sécurité attribués à l'utilisateur définissent l'accès aux objets.  

-   **Seuls les objets sécurisables dans les étendues de sécurité ou les regroupements spécifiés**: cette option associe l’utilisateur administratif aux mêmes étendues de sécurité et regroupements qui sont associés au compte que vous utilisez pour configurer l’utilisateur administratif. Cette option prend en charge l'ajout ou la suppression de rôles de sécurité et de regroupements pour personnaliser l'étendue administrative de l'utilisateur administratif.  

-   **Seuls les objets sécurisables définis par les rôles de sécurité de l’utilisateur administratif**: cette option permet de créer des associations spécifiées entre des rôles de sécurité individuels et des étendues de sécurité et regroupements spécifiques pour l’utilisateur.  

    > [!NOTE]  
    >  Cette option est disponible uniquement lorsque vous modifiez les propriétés d'un utilisateur administratif.  

La configuration actuelle du comportement de l'objet sécurisable modifie le processus qui vous permet d'attribuer des rôles de sécurité supplémentaires. Utilisez les procédures suivantes, basées sur les différentes options des objets sécurisables, pour vous aider à gérer un utilisateur administratif.  

 Utilisez la procédure suivante pour afficher et gérer la configuration des objets sécurisables pour un utilisateur administratif :  

#### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>Pour afficher et gérer le comportement de l'objet sécurisable pour un utilisateur administratif  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Sécurité**, puis cliquez sur **Utilisateurs administratifs**.  

3.  Sélectionnez l'utilisateur administratif à modifier.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Cliquez sur l'onglet **Étendues de sécurité** pour afficher la configuration actuelle des objets sécurisables pour cet utilisateur administratif.  

6.  Pour modifier le comportement de l'objet sécurisable, sélectionnez une nouvelle option pour le comportement de l'objet sécurisable. Après avoir modifié cette configuration, consultez la procédure appropriée pour obtenir des instructions supplémentaires afin de configurer des étendues de sécurité et des regroupements ainsi que des rôles de sécurité pour cet utilisateur administratif.  

7.  Cliquez sur **OK** pour terminer la procédure.  

 Utilisez la procédure suivante pour modifier un utilisateur administratif pour lequel le comportement de l'objet sécurisable est paramétré sur **Tous les objets sécurisables pertinents pour les rôles de sécurité auxquels ils sont associés**:  

#### <a name="option-all-securable-objects-that-are-relevant-to-their-associated-security-roles"></a>Option : Tous les objets sécurisables pertinents pour les rôles de sécurité auxquels ils sont associés  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Sécurité**, puis cliquez sur **Utilisateurs administratifs**.  

3.  Sélectionnez l'utilisateur administratif à modifier.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Cliquez sur l'onglet **Étendues de sécurité** pour confirmer que l'utilisateur administratif est configuré pour **Tous les objets sécurisables pertinents pour les rôles de sécurité auxquels ils sont associés**.  

6.  Pour modifier les rôles de sécurité attribués, cliquez sur l'onglet **Rôles de sécurité** .  

    -   Pour attribuer des rôles de sécurité supplémentaires à cet utilisateur administratif, cliquez sur **Ajouter**, cochez la case de chaque rôle de sécurité supplémentaire que vous souhaitez attribuer, puis cliquez sur **OK**.  

    -   Pour supprimer des rôles de sécurité, sélectionnez un ou plusieurs rôles de sécurité dans la liste, puis cliquez sur **Supprimer**.  

7.  Pour modifier le comportement de l'objet sécurisable, cliquez sur l'onglet **Étendues de sécurité** et sélectionnez une nouvelle option pour le comportement de l'objet sécurisable. Après avoir modifié cette configuration, consultez la procédure appropriée pour obtenir des instructions supplémentaires afin de configurer des étendues de sécurité et des regroupements ainsi que des rôles de sécurité pour cet utilisateur administratif.  

    > [!NOTE]  
    >  Lorsque le comportement de l'objet sécurisable est défini sur **Tous les objets sécurisables pertinents pour les rôles de sécurité auxquels ils sont associés**, vous ne pouvez pas ajouter ni supprimer d'étendues de sécurité ou de regroupements spécifiques.  

8.  Cliquez sur **OK** pour terminer cette procédure.  

 Utilisez la procédure suivante pour modifier un utilisateur administratif pour lequel le comportement de l'objet sécurisable est paramétré sur **Seuls les objets sécurisables dans des étendues de sécurité ou des regroupements spécifiés**.  

#### <a name="option-only-securable-objects-in-specified-security-scopes-or-collections"></a>Option : Seuls les objets sécurisables dans des étendues de sécurité ou des regroupements spécifiés  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Sécurité**, puis cliquez sur **Utilisateurs administratifs**.  

3.  Sélectionnez l'utilisateur administratif à modifier.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Cliquez sur l'onglet **Étendues de sécurité** pour confirmer que l'utilisateur est configuré pour **Seuls les objets sécurisables dans des étendues de sécurité ou des regroupements spécifiés**.  

6.  Pour modifier les rôles de sécurité attribués, cliquez sur l'onglet **Rôles de sécurité** .  

    -   Pour attribuer des rôles de sécurité supplémentaires à cet utilisateur, cliquez sur **Ajouter**, cochez la case de chaque rôle de sécurité supplémentaire que vous souhaitez affecter, puis cliquez sur **OK**.  

    -   Pour supprimer des rôles de sécurité, sélectionnez un ou plusieurs rôles de sécurité dans la liste, puis cliquez sur **Supprimer**.  

7.  Pour modifier les étendues de sécurité et les regroupements associés aux rôles de sécurité, cliquez sur l'onglet **Étendues de sécurité** .  

    -   Pour associer de nouvelles étendues de sécurité ou de nouveaux regroupements à tous les rôles de sécurité qui sont attribués à cet utilisateur administratif, cliquez sur **Ajouter** et sélectionnez l'une des quatre options. Si vous sélectionnez **Étendue de sécurité** ou **Regroupement**, cochez la case d'un ou plusieurs objets pour terminer cette sélection, puis cliquez sur **OK**.  

    -   Pour supprimer une étendue de sécurité ou un regroupement, sélectionnez l'objet, puis cliquez sur **Supprimer**.  

8.  Cliquez sur **OK** pour terminer cette procédure.  

 Utilisez la procédure suivante pour modifier un utilisateur administratif pour lequel le comportement de l'objet sécurisable est paramétré sur **Seuls les objets sécurisables déterminés par les rôles de sécurité de l'utilisateur administratif**.  

#### <a name="option-only-securable-objects-as-determined-by-the-security-roles-of-the-administrative-user"></a>Option : Seuls les objets sécurisables déterminés par les rôles de sécurité de l’utilisateur administratif  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Sécurité**, puis cliquez sur **Utilisateurs administratifs**.  

3.  Sélectionnez l'utilisateur administratif à modifier.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Cliquez sur l'onglet **Étendues de sécurité** pour confirmer que l'utilisateur administratif est configuré sur **Seuls les objets sécurisables dans des étendues de sécurité ou des regroupements spécifiés**.  

6.  Pour modifier les rôles de sécurité attribués, cliquez sur l'onglet **Rôles de sécurité** .  

    -   Pour attribuer des rôles de sécurité supplémentaires à cet utilisateur administratif, cliquez sur **Ajouter**. Dans la boîte de dialogue **Ajouter un rôle de sécurité** , sélectionnez un ou plusieurs rôles de sécurité disponibles, cliquez sur **Ajouter**, puis sélectionnez un type d'objet à associer aux rôles de sécurité sélectionnés. Si vous sélectionnez **Étendue de sécurité** ou **Regroupement**, cochez la case d'un ou plusieurs objets pour terminer cette sélection, puis cliquez sur **OK**.  

        > [!NOTE]  
        >  Vous devez configurer au moins une étendue sécurité avant que les rôles de sécurité sélectionnés puissent être attribués à l'utilisateur administratif. Lorsque vous sélectionnez plusieurs rôles de sécurité, chaque étendue de sécurité et regroupement que vous configurez est associé à chacun des rôles de sécurité sélectionnés.  

    -   Pour supprimer des rôles de sécurité, sélectionnez un ou plusieurs rôles de sécurité dans la liste, puis cliquez sur **Supprimer**.  

7.  Pour modifier les étendues de sécurité et les regroupements associés à un rôle de sécurité spécifique, cliquez sur l'onglet **Étendues de sécurité** , sélectionnez le rôle de sécurité, puis cliquez sur **Modifier**.  

    -   Pour associer de nouveaux objets à ce rôle de sécurité, cliquez sur **Ajouter**, puis sélectionnez un type d'objet à associer aux rôles de sécurité sélectionnés. Si vous sélectionnez **Étendue de sécurité** ou **Regroupement**, cochez la case d'un ou plusieurs objets pour terminer cette sélection, puis cliquez sur **OK**.  

        > [!NOTE]  
        >  Vous devez configurer au moins une étendue de sécurité.  

    -   Pour supprimer une étendue de sécurité ou un regroupement associé à ce rôle de sécurité, sélectionnez l'objet et cliquez sur **Supprimer**.  

    -   Lorsque vous avez terminé de modifier les objets associés, cliquez sur **OK**.  

8.  Cliquez sur **OK** pour terminer cette procédure.  

    > [!CAUTION]  
    >  Lorsqu'un rôle de sécurité accorde aux utilisateurs administratifs l'autorisation de déployer un regroupement, ces utilisateurs administratifs peuvent distribuer des objets depuis n'importe quelle étendue de sécurité pour laquelle il disposent d'autorisations de **Lecture** , même si cette étendue de sécurité est associée à un rôle de sécurité différent.  



<!--HONumber=Nov16_HO1-->


