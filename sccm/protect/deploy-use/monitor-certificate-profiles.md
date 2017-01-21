---
title: Surveiller des profils de certificat | Microsoft Docs
description: "Découvrez comment surveiller l’état de compatibilité des profils de certificat System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
caps.latest.revision: 7
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 34e1f57798a9745303dd6d03a8b4362c01c5efbb


---
# <a name="how-to-monitor-certificate-profiles-in-system-center-configuration-manager"></a>Comment surveiller des profils de certificat dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Une fois que vous avez déployé des profils de certificat System Center Configuration Manager auprès d’utilisateurs dans votre hiérarchie, vous pouvez utiliser les procédures suivantes pour surveiller l’état de compatibilité du profil de certificat :  

-   [Comment afficher les résultats de compatibilité dans la console Configuration Manager](#BKMK_console)  

-   [Comment afficher les résultats de compatibilité à l'aide de rapports](#BKMK_Reports)  

##  <a name="a-namebkmkconsolea-how-to-view-compliance-results-in-the-configuration-manager-console"></a><a name="BKMK_console"></a> Comment afficher les résultats de compatibilité dans la console Configuration Manager  
 Utilisez cette procédure pour afficher des détails sur la compatibilité des profils de certificat déployés dans la console System Center Configuration Manager.  

> [!NOTE]  
>  Pour surveiller la compatibilité des certificats SCEP, n'utilisez pas la console Configuration Manager. Utilisez plutôt les rapports, comme décrit dans [How to View Compliance Results by Using Reports](#BKMK_Reports). Utilisez notamment les rapports de certificat sous le nœud des rapports **Accès aux ressources de l’entreprise**.  
>   
>  -   Historique d'émission des certificats  
> -   Liste de biens dont la date d'expiration des certificats approche  
> -   Liste de biens par état d'émission de certificat  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Pour afficher les résultats de compatibilité dans la console Configuration Manager  

1.  Dans la console System Center Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , cliquez sur **Déploiements**.  

3.  Dans la liste **Déploiements** , sélectionnez le déploiement du profil de certificat dont vous souhaitez vérifier les informations de compatibilité.  

4.  Vous pouvez consulter un résumé des informations relatives à la compatibilité du profil de certificat sur la page principale. Pour afficher des informations plus détaillées, sélectionnez le profil de certificat puis, dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Afficher l'état** pour ouvrir la page **État du déploiement** .  

     La page **État du déploiement** contient les onglets suivants :  

    -   **Compatible**: affiche la compatibilité du profil de certificat en fonction du nombre de ressources concernées. Vous pouvez double-cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** de l'espace de travail **Ressources et Conformité** . Ce nœud contient tous les utilisateurs qui sont compatibles avec le profil de certificat. Le volet **Détails du bien** affiche également les utilisateurs compatibles avec ce profil. Double-cliquez sur un utilisateur de la liste pour afficher des informations supplémentaires.  

        > [!IMPORTANT]  
        >  Un profil de certificat n'est pas évalué s'il n'est pas applicable sur un périphérique client. Toutefois, il est retourné comme conforme.  

    -   **Erreur**: affiche une liste de toutes les erreurs pour le déploiement du profil de certificat sélectionné en fonction du nombre de biens concernés. Vous pouvez double-cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** de l'espace de travail **Ressources et Conformité** . Ce nœud contient tous les utilisateurs qui ont généré des erreurs avec ce profil. Lorsque vous sélectionnez un utilisateur, le volet **Détails du bien** affiche les utilisateurs qui sont concernés par le problème sélectionné. Double-cliquez sur un utilisateur de la liste pour afficher des informations supplémentaires sur le problème.  

    -   **Non compatible**: affiche une liste de toutes les règles non compatibles au sein du profil de certificat en fonction du nombre de biens concernés. Vous pouvez double-cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** de l'espace de travail **Ressources et Conformité** . Ce nœud contient tous les utilisateurs qui ne sont pas compatibles avec ce profil. Lorsque vous sélectionnez un utilisateur, le volet **Détails du bien** affiche les utilisateurs qui sont concernés par le problème sélectionné. Double-cliquez sur un utilisateur de la liste pour afficher des informations supplémentaires sur le problème.  

    -   **Inconnu**: affiche une liste de tous les utilisateurs qui n'ont pas signalé de compatibilité pour le déploiement du profil de certificat sélectionné avec l'état du client actuel des appareils.  

5.  Sur la page **État du déploiement** , vous pouvez consulter des informations détaillées sur la compatibilité du profil de certificat déployé. Un nœud temporaire est créé sous le nœud **Déploiements** qui vous aide à retrouver rapidement ces informations.  

     L'état de l'inscription du certificat s'affiche sous la forme d'un numéro. Le tableau suivant permet de comprendre ce que chaque numéro signifie :  

    |État de l'inscription|Description|  
    |-----------------------|-----------------|  
    |0x00000001|L'inscription a réussi et le certificat a été émis.|  
    |0x00000002|La demande a été soumise et l'inscription est en attente, ou la demande a été émise hors bande.|  
    |0x00000004|L'inscription doit être différée.|  
    |0x00000010|Une erreur s'est produite.|  
    |0x00000020|L'état de l'inscription est inconnu.|  
    |0x00000040|Les informations d'état ont été ignorées. Cela peut se produire si une autorité de certification HYPERLINK « http://msdn.microsoft.com/en-us/windows/ms721572" \l "_security_certification_authority_gly » n'est pas valide ou n'a pas été sélectionnée pour la surveillance.|  
    |0x00000100|L'inscription a été refusée.|  

##  <a name="a-namebkmkreportsa-how-to-view-compliance-results-by-using-reports"></a><a name="BKMK_Reports"></a> Comment afficher les résultats de compatibilité à l'aide de rapports

 Les paramètres de compatibilité de System Center Configuration Manager incluent des rapports intégrés que vous pouvez utiliser pour analyser des informations sur les profils de certificat. La catégorie de ces rapports est **Gestion de la conformité et des paramètres**.  

> [!IMPORTANT]  
>  Vous devez utiliser un caractère générique (%) lorsque vous utilisez les paramètres **Filtre de périphérique** et **Filtre d'utilisateur** dans les rapports des paramètres de compatibilité.  

 Pour plus d’informations sur la configuration de la génération de rapports dans System Center Configuration Manager, consultez [Génération de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).  



<!--HONumber=Dec16_HO3-->


