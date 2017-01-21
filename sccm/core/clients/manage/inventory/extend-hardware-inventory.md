---
title: "Étendre l’inventaire matériel | System Center Configuration Manager"
description: "Découvrez différentes façons d’étendre l’inventaire matériel dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
caps.latest.revision: 10
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: 4a42e266c4152145a4a1c291804ff98934671692


---
# <a name="how-to-extend-hardware-inventory-in-system-center-configuration-manager"></a>Comment étendre l’inventaire matériel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

L’inventaire matériel System Center Configuration Manager lit les informations concernant les appareils sur les PC Windows en utilisant WMI (Windows Management Instrumentation). WMI est l'implémentation Microsoft de WBEM (Web-based Enterprise Management) qui est une norme sectorielle pour l'accès aux informations de gestion dans un environnement d'entreprise. Dans les versions précédentes de Configuration Manager, vous pouviez étendre l'inventaire matériel en modifiant le fichier sms_def.mof fichier sur le serveur de site. Ce fichier contenait une liste de classes WMI qui pouvaient être lues par l’inventaire matériel de Configuration Manager. En modifiant ce fichier, vous pouviez activer et désactiver les classes existantes et également créer des classes à inventorier.  

 Le fichier Configuration.mof permet de définir les classes de données qui doivent faire l’objet d’un inventaire matériel sur le client. Il n’a pas été modifié depuis Configuration Manager 2012. Vous pouvez créer des classes de données pour inventorier les classes de données de référentiel WMI existantes ou personnalisées ou les clés de Registre présentes sur les systèmes clients.  

 Le fichier Configuration.mof définit également et inscrit les fournisseurs WMI d'accéder aux informations de périphérique durant l'inventaire matériel. L'enregistrement des fournisseurs définit le type de fournisseur à utiliser et les classes prises en charge par le fournisseur.  

 Quand les clients Configuration Manager demandent une stratégie, par exemple, pendant leur intervalle d’interrogation standard de stratégie client, le fichier Configuration.mof est joint au corps de la stratégie. Ce fichier est ensuite téléchargé et compilé par les clients. Lorsque vous ajoutez, modifiez ou supprimez des classes de données à partir du fichier Configuration.mof, les clients compilent automatiquement ces modifications sont apportées aux classes de données liées au stock. Aucune autre action n’est requise pour inventorier les classes de données nouvelles ou modifiées sur les clients Configuration Manager. Ce fichier se trouve dans **<emplacement_installation_CM\>\Inboxes\clifiles.src\hinv\\\** sur les serveurs de site principal.  

 Dans Configuration Manager, le fichier sms_def.mof n’a plus besoin d’être modifié comme c’était le cas dans Configuration Manager 2007. Au lieu de cela, vous pouvez activer et désactiver des classes WMI, et ajouter de nouvelles classes que l’inventaire matériel collectera, à l’aide des paramètres client. Configuration Manager permet d’étendre l’inventaire matériel à l’aide des méthodes ci-dessous.  

> [!NOTE]  
>  Si vous avez modifié manuellement le fichier Configuration.mof pour ajouter des classes d’inventaire personnalisées, ces modifications sont remplacées quand vous effectuez la mise à jour vers la version 1602. Pour continuer à utiliser des classes personnalisées après la mise à jour, vous devez les ajouter à la section « Added extensions » du fichier Configuration.mof après la mise à jour vers 1602.  
> En revanche, vous ne devez rien modifier au-dessus de cette section, car la modification de ces sections est réservée à Configuration Manager. Une sauvegarde de votre fichier Configuration.mof personnalisé se trouve dans :  
> **<répertoire_installation_CM\>\data\hinvarchive\\**.  

|Méthode|Informations complémentaires|  
|------------|----------------------|  
|Activer ou désactiver les classes d'inventaire existantes|Vous pouvez activer ou désactiver les classes d’inventaire par défaut utilisées par Configuration Manager ou créer des paramètres client personnalisés qui permettent de collecter différentes classes d’inventaire matériel à partir des regroupements de clients spécifiés. Pour plus d’informations, consultez la procédure [Pour activer ou désactiver les classes existantes d'inventaire](#BKMK_Enable) dans cette rubrique.|  
|Ajouter une nouvelle classe d'inventaire|Vous pouvez ajouter une nouvelle classe d'inventaire à partir de l'espace de noms WMI d'un autre périphérique. Pour plus d’informations, consultez la procédure [Pour ajouter une nouvelle classe d'inventaire](#BKMK_Add) dans cette rubrique.|  
|Importer et exporter des classes d'inventaire matériel|Vous pouvez importer et exporter des fichiers MOF (Managed Object Format) qui contiennent des classes d’inventaire à partir de la console Configuration Manager. Pour plus d’informations, consultez les procédures [Pour importer des classes d'inventaire matériel](#BKMK_Import) et [Pour exporter des classes d'inventaire matériel](#BKMK_Export) dans cette rubrique.|  
|Créer des fichiers NOIDMIF|Utilisez des fichiers NOIDMIF pour collecter des informations sur les appareils clients qui ne peuvent pas être inventoriés par Configuration Manager. Par exemple, vous pouvez souhaiter recueillir des informations numéros de périphérique actif qui existe uniquement en tant qu'étiquette sur le périphérique. Inventaire NOIDMIF est automatiquement associé à l'appareil client collectées à partir de. Pour plus d'informations, consultez [Pour créer des fichiers NOIDMIF](#BKMK_NOIDMIF) dans cette rubrique.|  
|Créer les fichiers IDMIF|Utilisez des fichiers IDMIF pour collecter des informations sur les ressources de votre organisation qui ne sont associées à aucun client Configuration Manager, par exemple, les projecteurs, les photocopieurs et les imprimantes réseau. Pour plus d'informations, consultez [Pour créer des fichiers IDMIF](#BKMK_IDMIF) dans cette rubrique.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Procédures pour étendre l’inventaire matériel  
 Utilisez les procédures suivantes pour étendre l’inventaire matériel, comme décrit dans le tableau précédent.  

 Ces procédures vous aident à configurer les paramètres client par défaut pour l'inventaire matériel et elles s'appliquent à tous les clients de votre hiérarchie. Pour appliquer ces paramètres à certains clients uniquement, créez un paramètre de périphérique client personnalisé et affectez-le à un regroupement qui contient les périphériques à inventorier. Pour plus d'informations sur la création de paramètres client personnalisés, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="a-namebkmkenablea-to-enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a> Pour activer ou désactiver les classes existantes d'inventaire  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Paramètres client**.  

3.  Cliquez sur **Paramètres client par défaut**.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Dans la boîte de dialogue **Paramètres client par défaut** , cliquez sur **Inventaire matériel**.  

6.  Dans la liste **Paramètres du périphérique** , cliquez sur **Définir des classes**.  

7.  Dans la boîte de dialogue **Classes d'inventaire matériel** , sélectionnez ou désélectionnez les classes et les propriétés de classe que doit collecter l'inventaire matériel. Vous pouvez développer une classe pour sélectionner ou désélectionner des propriétés individuelles dans la classe. Utilisez le champ **Rechercher des classes d'inventaire** pour rechercher des classes individuelles.  

    > [!IMPORTANT]  
    >  Quand vous ajoutez de nouvelles classes à l’inventaire matériel Configuration Manager, la taille du fichier d’inventaire collecté et envoyé au serveur de site augmente. Cela peut nuire aux performances de votre réseau et du site Configuration Manager. Activez uniquement les classes d'inventaire à collecter.  

8.  Cliquez sur **OK** pour enregistrer vos modifications et fermer la boîte de dialogue **Classes d'inventaire matériel** .  

###  <a name="a-namebkmkadda-to-add-a-new-inventory-class"></a><a name="BKMK_Add"></a> Pour ajouter une nouvelle classe d'inventaire  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

    > [!IMPORTANT]  
    >  Vous pouvez uniquement ajouter des classes d'inventaire à partir du serveur de niveau supérieur dans la hiérarchie et en modifiant les paramètres client par défaut. Cette option n'est pas disponible lorsque vous créez des paramètres de périphérique personnalisés.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Paramètres client**.  

3.  Cliquez sur **Paramètres client par défaut**.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Dans la boîte de dialogue **Paramètres client par défaut** , cliquez sur **Inventaire matériel**.  

6.  Dans la liste **Paramètres du périphérique** , cliquez sur **Définir des classes**.  

7.  Dans la boîte de dialogue **Classes d'inventaire matériel** , cliquez sur **Ajouter**.  

8.  Dans la boîte de dialogue **Ajouter une classe d'inventaire matériel** , cliquez sur **Ajouter**.  

9. Dans la boîte de dialogue **Connexion à Windows Management Instrumentation (WMI)** , définissez le nom de l'ordinateur depuis lequel vous allez extraire les classes WMI et l'espace de noms WMI à utiliser pour récupérer les classes. Si vous souhaitez récupérer toutes les classes sous l'espace de noms WMI spécifié, cliquez sur **Récursive**. Si l'ordinateur auquel vous vous connectez n'est pas l'ordinateur local, fournissez les informations d'identification d'un compte autorisé à accéder à WMI sur l'ordinateur distant.  

10. Cliquez sur **Connexion**.  

11. Dans la boîte de dialogue **Ajouter une classe d’inventaire matériel**, dans la liste des **classes d’inventaire**, sélectionnez les classes WMI à ajouter à l’inventaire matériel Configuration Manager.  

12. Si vous souhaitez modifier les informations sur la classe WMI sélectionnée, cliquez sur **Modifier**et dans la boîte de dialogue **Qualificatifs de classe** , fournissez les informations suivantes :  

    -   **Nom complet** : permet d’indiquer un nom convivial pour la classe qui s’affiche dans l’Explorateur de ressources.  

    -   **Propriétés** : définissez l’unité dans laquelle s’affiche chaque propriété de la classe WMI.  

     Vous pouvez également désigner des propriétés comme propriété de clé pour identifier de façon unique chaque instance de la classe. Si aucune clé n'est définie pour la classe et que plusieurs instances de la classe sont signalées par le client, seule la dernière instance trouvée est stockée dans la base de données.  

     Lorsque vous avez terminé de configurer les propriétés, cliquez sur **OK** pour fermer la boîte de dialogue **Qualificatifs de classe** .  

13. Cliquez sur OK pour fermer la boîte de dialogue **Ajouter une classe d'inventaire matériel**  

14. Cliquez sur **OK** pour fermer la boîte de dialogue **Classes inventaire matériel**  

15. Cliquez sur **OK** pour fermer la boîte de dialogue **Paramètres client par défaut** .  

###  <a name="a-namebkmkimporta-to-import-hardware-inventory-classes"></a><a name="BKMK_Import"></a> Pour importer des classes d'inventaire matériel  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Paramètres client**.  

3.  Cliquez sur **Paramètres client par défaut**.  

    > [!IMPORTANT]  
    >  Vous pouvez importer uniquement des classes d'inventaire lorsque vous modifiez les paramètres par défaut du client. Toutefois, vous pouvez utiliser des paramètres client personnalisés pour importer des informations qui ne contient pas un changement de schéma, telles que la modification de la propriété d'une classe existante à partir de **True** à **False**.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Dans la boîte de dialogue **Paramètres client par défaut** , cliquez sur **Inventaire matériel**.  

6.  Dans la liste **Paramètres du périphérique** , cliquez sur **Définir des classes**.  

7.  Dans la boîte de dialogue **Classes d'inventaire matériel** , cliquez sur **Importer**.  

8.  Dans le **importer** boîte de dialogue, sélectionnez le Format MOF (Managed Object) fichier que vous souhaitez importer, puis cliquez sur **OK**.  

9. Dans la boîte de dialogue **Résumé d'importation** , passez en revue les éléments qui seront importés, puis cliquez sur **Importer**.  

###  <a name="a-namebkmkexporta-to-export-hardware-inventory-classes"></a><a name="BKMK_Export"></a> Pour exporter des classes d'inventaire matériel  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Paramètres client**.  

3.  Cliquez sur **Paramètres client par défaut**.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Dans la boîte de dialogue **Paramètres client par défaut** , cliquez sur **Inventaire matériel**.  

6.  Dans la liste **Paramètres du périphérique** , cliquez sur **Définir des classes**.  

7.  Dans la boîte de dialogue **Classes d'inventaire matériel** , cliquez sur **Exporter**.  

    > [!NOTE]  
    >  Lorsque vous exportez des classes, toutes les classes sélectionnées sont exportées.  

8.  Dans la boîte de dialogue **Exporter** , spécifiez le fichier MOF (Managed Object Format) vers lequel vous voulez exporter les classes, puis cliquez sur **Enregistrer**.  

## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Comment utiliser les fichiers MIF (Management Information Format) pour étendre l’inventaire matériel  
 Utilisez des fichiers MIF (Management Information Format) pour étendre les informations d’inventaire matériel recueillies auprès des clients par Configuration Manager. Au cours de l'inventaire matériel, les informations stockées dans les fichiers MIF sont ajoutées au rapport d'inventaire du client et stockées dans la base de données de site. Vous pourrez utiliser les données depuis cet emplacement de la même manière que vous utilisez les données d'inventaire du client par défaut. Il existe deux types de fichiers MIF, NOIDMIF et IDMIF. 

> [!IMPORTANT]  
>  Avant d’ajouter les informations de fichiers MIF à la base de données Configuration Manager, vous devez créer ou importer des informations de classe pour eux. Pour plus d’informations, consultez les sections [Pour ajouter une nouvelle classe d'inventaire](#BKMK_Add) et [Pour importer des classes d'inventaire matériel](#BKMK_Import) de cette rubrique.  

###  <a name="a-namebkmknoidmifa-to-create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a> Pour créer des fichiers NOIDMIF  
 Les fichiers NOIDMIF permettent d’ajouter des informations à un inventaire matériel de client qui normalement ne peut pas être collecté par Configuration Manager et est associé à un appareil client particulier. Par exemple, de nombreuses sociétés affectent à chaque ordinateur de l'organisation un numéro de composant, puis les classent à la main. Quand vous créez un fichier NOIDMIF, ces informations peuvent être ajoutées à la base de données Configuration Manager et être utilisées pour les requêtes et la génération de rapports. Pour plus d’informations sur la création de fichiers NOIDMIF, consultez la documentation du Kit de développement logiciel (SDK) Configuration Manager.  

> [!IMPORTANT]  
>  Lorsque vous créez un fichier NOIDMIF, il doit être enregistré dans un format codé ANSI. Les fichiers NOIDMIF enregistrés au format encodé UTF-8 ne peuvent pas être lus par Configuration Manager.  

 Après avoir créé un fichier NOIDMIF, enregistrez-le dans le dossier *%windir%***\System32\CCM\Inventory\Noidmifs** dossier sur chaque client. Configuration Manager collecte les informations des fichiers NODMIF de ce dossier lors du prochain cycle d’inventaire matériel planifié.  

###  <a name="a-namebkmkidmifa-to-create-idmif-files"></a><a name="BKMK_IDMIF"></a> Pour créer des fichiers IDMIF  
 Les fichiers IDMIF permettent d’ajouter à la base de données Configuration Manager des informations sur les ressources qui ne pourraient normalement pas être inventoriées par Configuration Manager et qui ne sont associées à aucun appareil client particulier. Par exemple, vous pouvez utiliser des fichiers IDMIF pour recueillir des informations sur les projecteurs, lecteurs de DVD, photocopieurs ou autres équipements qui ne contiennent pas de client Configuration Manager. Pour plus d’informations sur la création de fichiers IDMIF, consultez la documentation du Kit de développement logiciel (SDK) Configuration Manager.  

 Après avoir créé un fichier IDMIF, stockez-le dans le dossier *%windir%***\System32\CCM\Inventory\Idmifs** dossier sur les ordinateurs clients. Configuration Manager collecte les informations de ce fichier lors du prochain cycle d’inventaire matériel planifié. Vous devez déclarer de nouvelles classes pour les informations contenues dans le fichier en les ajoutant ou en les important.  

> [!NOTE] 
> Les fichiers MIF peuvent contenir de grandes quantités de données et le regroupement de ces données pourrait affecter négativement les performances de votre site. Activez la collecte de fichiers MIF uniquement quand cela est nécessaire et configurez l’option **Taille maximale du fichier MIF personnalisé (Ko)** dans les paramètres d’inventaire matériel. Pour plus d’informations, consultez [Présentation de l’inventaire matériel dans System Center Configuration Manager](introduction-to-hardware-inventory.md).



<!--HONumber=Nov16_HO1-->


