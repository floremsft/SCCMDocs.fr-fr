---
title: Modifier et remplacer des applications | System Center Configuration Manager
description: "Travaillez avec des versions d’application System Center Configuration Manager et remplacez des applications."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30170d70-489f-47f7-bebf-9ed0115db26b
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ae6440375d6e801ac9c3932872ec1367d9c601a8


---
# <a name="how-to-revise-and-supersede-applications-in-system-center-configuration-manager"></a>Comment modifier et remplacer des applications dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans cette rubrique, vous allez apprendre à utiliser des versions d’application System Center Configuration Manager et à remplacer des applications par une nouvelle version.  

##  <a name="application-revisions"></a>Modification d’une application  
 Lorsque vous apportez des modifications à une application ou à un type de déploiement contenu dans une application, Configuration Manager crée une nouvelle révision de l’application. Vous pouvez afficher l'historique des révisions de chaque application. Vous pouvez également afficher les propriétés de chaque révision, restaurer une révision précédente d'une application ou supprimer une ancienne révision.  

### <a name="to-display-an-application-revision-history"></a>Pour afficher un historique des révisions d'application  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**, puis cliquez sur l’application de votre choix.  

3.  Dans l'onglet **Accueil** , dans le groupe **Application** , cliquez sur **Historique de révision** pour ouvrir la boîte de dialogue **Historique de révision de l'application** .  

### <a name="to-view-an-application-revision"></a>Pour afficher une révision d'application  

1.  Dans la boîte de dialogue **Historique de révision de l'application** , sélectionnez une révision d'application et cliquez sur **Afficher**.  

2.  Dans la boîte de dialogue **Propriétés** , examinez les propriétés de l'application sélectionnée.  

    > [!NOTE]  
    >  Les propriétés d'application affichées sont en lecture seule.  

3.  Fermez la boîte de dialogue **Propriétés** .  

### <a name="to-restore-an-application-revision"></a>Pour restaurer une révision d'application  

1.  Dans la boîte de dialogue **Historique de révision de l'application** , sélectionnez une révision d'application et cliquez sur **Restaurer**.  

2.  Dans la boîte de dialogue **Confirmer la restauration de la révision** , cliquez sur **Oui** pour restaurer la révision d'application choisie.  

### <a name="to-delete-an-application-revision"></a>Pour supprimer une révision d'application  

1.  Dans la boîte de dialogue **Historique de révision de l'application** , sélectionnez une révision d'application et cliquez sur **Supprimer**.  

2.  Dans la boîte de dialogue **Supprimer la révision d'application** , cliquez sur **Oui**.  

> [!IMPORTANT]  
>  Pour que vous puissiez supprimer la révision d'application actuelle, l'application doit avoir été mise hors service et elle ne doit pas contenir de référence.  

##  <a name="application-supersedence"></a>Remplacement d’une application  
 La fonctionnalité de gestion d'applications dans Gestionnaire de configuration vous permet de mettre à niveau ou de remplacer des applications existantes à l’aide d'une relation de remplacement. Lorsque vous remplacez une application, vous pouvez spécifier un nouveau type de déploiement qui remplacera le type de déploiement de l'application remplacée. Vous pouvez aussi indiquer si vous souhaitez mettre à niveau ou désinstaller l'application remplacée avant l'installation de l'application de remplacement.  

> [!IMPORTANT]  
>  Lorsque l'option de désinstallation du type de déploiement remplacé est sélectionnée, un type de déploiement ne peut pas être remplacé par un type de déploiement qui a été déployé sur un autre type de regroupement.  Par exemple, un type de déploiement qui a été déployé sur un regroupement de périphériques ne peut pas être remplacé par un type de déploiement qui a été déployé sur un regroupement d'utilisateurs si l'option de désinstallation du type de déploiement remplacé est sélectionnée.  

### <a name="decide-whether-to-upgrade-or-replace-an-application"></a>Décider s'il faut mettre à niveau ou remplacer une application  
 Vous spécifiez s'il faut remplacer ou mettre à niveau une application dans la boîte de dialogue **Spécifier les relations de remplacement** de la boîte de dialogue de propriétés de l'application. Le type de remplacement varie selon que vous sélectionnez ou non l'option **Désinstaller** dans cette boîte de dialogue :  

-   Si vous souhaitez procéder à une mise à jour vers une version plus récente de la même application (avec le même ID d'application), ne cochez **pas** l'option **Désinstaller**.  

-   Si vous souhaitez installer une autre application (avec un ID d'application différent), sélectionnez **Désinstaller**. Vous devrez supprimer la version obsolète de l'application.  

### <a name="superseding-dependent-applications"></a>Remplacement des applications dépendantes  
 Dans cet exemple, le terme **application maître** fait référence à l’application que vous déployez et qui contient les dépendances.  

 Vous pouvez créer une relation de remplacement qui met à jour l’application dépendante vers une nouvelle version.  

1.  Assurez-vous que la nouvelle application dépendante et l'application dépendante d'origine sont dans le même groupe de dépendance de l'application maître.  

2.  Créez une relation de remplacement qui remplace l'application dépendante d'origine par la nouvelle application dépendante.  

 Durant les nouvelles installations de l'application maître, la nouvelle application dépendante sera installée. Les installations existantes de l'application maître seront mises à jour avec la nouvelle application dépendante.  

 Le résultat final est que tous les déploiements de l'application maître utiliseront la nouvelle application dépendante.  

### <a name="further-considerations"></a>Autres considérations  

-   Vous pouvez spécifier plusieurs relations de remplacement pour les applications dépendantes. L'application dépendante la plus élevée dans la chaîne de remplacement est installée.  

-   Les applications dépendantes doivent être déployées sur l'appareil où l'application maître est installée, sinon l'installation de l'application dépendante échoue.  

-   Pour les nouvelles installations de l'application maître, quand vous avez plusieurs dépendances, l'ordre de dépendance détermine quelle version de l'application dépendante est installée.  

### <a name="specify-a-supersedence-relationship"></a>Pour spécifier une relation de remplacement  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**, puis cliquez sur l’application qui en remplacera une autre.  

3.  Sous l'onglet **Accueil**, dans le groupe **Propriétés**, cliquez sur **Propriétés** pour ouvrir la boîte de dialogue **Propriétés** de <nom_application>.  

4.  Sous l’onglet **Remplacement** de la boîte de dialogue *Propriétés de ***<nom_application\>**, cliquez sur **Ajouter**.  

5.  Dans la boîte de dialogue **Spécifier une relation de remplacement** , cliquez sur **Parcourir**.  

6.  Dans la boîte de dialogue **Choisir une application** , sélectionnez l'application que vous souhaitez remplacer, puis cliquez sur **OK**.  

7.  Dans la boîte de dialogue **Spécifier une relation de remplacement** , sélectionnez le type de déploiement qui remplacera le type de déploiement de l'application remplacée.  

    > [!NOTE]  
    >  Par défaut, le nouveau type de déploiement ne désinstallera pas le type de déploiement de l'application remplacée. Ce scénario est couramment utilisé lorsque vous souhaitez déployer une mise à niveau vers une application existante. Sélectionnez **Désinstaller** pour supprimer le type de déploiement existant avant d'installer le nouveau type de déploiement. Si vous décidez de mettre à niveau une application, veillez à tester au préalable cette mise à niveau dans un environnement de laboratoire.  

8.  Cliquez sur **OK** pour fermer la boîte de dialogue **Spécifier une relation de remplacement** .  

9. Cliquez sur **OK** pour fermer la boîte de dialogue *Propriétés de ***<nom_application\>**.  

### <a name="to-display-applications-that-supersede-the-current-application"></a>Pour afficher les applications qui remplacent l'application en cours  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Gestion d'applications**, cliquez sur **Applications**, puis cliquez sur l'application souhaitée.  

3.  Sous l'onglet **Accueil**, dans le groupe **Propriétés**, cliquez sur **Propriétés** pour ouvrir la boîte de dialogue *Propriétés de ***<nom_application\>**.  

4.  Sous l'onglet **Références** de la boîte de dialogue *Propriétés de ***<nom_application\>**, sélectionnez **Applications qui remplacent cette application** dans la liste déroulante **Type de relation**.  

5.  Consultez la liste des applications qui remplacent l'application sélectionnée, puis cliquez sur **OK** pour fermer la boîte de dialogue *Propriétés de ***<nom_application\>**.  



<!--HONumber=Nov16_HO1-->


