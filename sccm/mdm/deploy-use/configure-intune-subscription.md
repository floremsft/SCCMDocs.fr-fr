---
title: "Configurer votre abonnement Microsoft Intune avec System Center Configuration Manager | Microsoft Docs"
description: "Configurez votre abonnement Microsoft Intune à l’aide de System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99de8fe7-560e-401a-8ab2-6d87d091be17
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 10cc64ae7e4d91f53201c2896b359e77ef04d32d
ms.lasthandoff: 03/06/2017

---
# <a name="configure-your-intune-subscription-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurer votre abonnement Microsoft Intune avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

L’abonnement Intune vous permet de gérer des appareils via Internet. Vous pouvez notamment spécifier le regroupement d’utilisateurs pouvant inscrire des appareils, et définir les informations présentées aux utilisateurs. Lorsque vous créez un abonnement à Microsoft Intune, vous pouvez également ajouter votre marque de société au portail d’entreprise Intune, avec le logo de l’entreprise et des modèles de couleurs personnalisés.

L’abonnement Intune effectue les opérations suivantes :

-   Récupération du certificat dont a besoin le point de connexion de service pour se connecter au service Intune
-   Définition du regroupement d’utilisateurs permettant aux utilisateurs d’inscrire des appareils mobiles
-   Définition et configuration des plateformes mobiles que vous souhaitez prendre en charge

> [!IMPORTANT]
>  La création d’un abonnement pour Microsoft Intune dans Configuration Manager place le point de connexion de service de votre site en « mode en ligne ». Consultez [À propos du point de connexion de service dans System Center Configuration Manager](../../core/servers/deploy/configure/about-the-service-connection-point.md).

## <a name="to-create-the-microsoft-intune-subscription"></a>Pour créer l'abonnement Microsoft Intune

1.  Si vous n’avez pas encore de compte Microsoft Intune, créez-en un sur [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216).  Une fois que vous avez créé votre compte Intune, vous n’avez pas besoin d’y ajouter des utilisateurs ou d’effectuer des configurations de paramètres supplémentaires.

2.  Dans la console Configuration Manager, cliquez sur **Administration**.

3.  Dans l'espace de travail **Administration** , développez **Services cloud**, puis cliquez sur **Abonnements Microsoft Intune**. Sous l'onglet **Accueil** , cliquez sur **Ajouter un abonnement Microsoft Intune**.

![Créer un abonnement Intune](../media/mdm-set-intune.png)

4.  Dans la page **Introduction** de l'Assistant Créer un abonnement Microsoft Intune, lisez le texte et cliquez sur **Suivant**.

5.  Dans la page **Abonnement** , cliquez sur **Se connecter** , puis connectez-vous en utilisant votre compte professionnel ou scolaire. Dans la boîte de dialogue **Définir l’autorité de gestion des appareils mobiles**, cochez la case permettant de gérer uniquement les appareils mobiles à l’aide de Configuration Manager via la console Configuration Manager. Pour poursuivre la procédure d'abonnement, vous devez sélectionner cette option.

    > [!IMPORTANT]
    >  Une fois que vous avez sélectionné Configuration Manager comme autorité de gestion, vous ne pouvez plus définir Microsoft Intune comme autorité de gestion.

6.  Pour prendre connaissance de la déclaration de confidentialité, cliquez sur les liens correspondants. Cliquez ensuite sur **Suivant**.

7.  Sur la page **Général** , spécifiez les options suivantes et cliquez sur **Suivant**.

  -   **Regroupement**: spécifiez un regroupement d'utilisateurs contenant les utilisateurs qui sont appelés à inscrire leurs appareils mobiles.

      > [!NOTE]
      >  Si un utilisateur est supprimé d’un regroupement, l’appareil de l’utilisateur continue d’être géré pendant 24 heures au maximum, le temps que l’enregistrement soit supprimé de la base de données utilisateur.

  -   **Nom de la société**: spécifiez le nom de votre entreprise.

  -   **URL vers la documentation de confidentialité**: si vous publiez des informations de confidentialité sur votre société par le biais d’un lien accessible sur Internet, fournissez un lien auquel les utilisateurs puissent accéder à partir du portail d’entreprise, par exemple http://www.contoso.com/CP_privacy.html. Les informations de confidentialité permettent de donner des précisions sur les informations que les utilisateurs partagent avec votre entreprise.

  -   **Modèle de couleurs pour le portail de la société**: modifiez éventuellement la couleur bleue par défaut des portails d'entreprise.

  -   **Code de site Configuration Manager**: spécifiez le code de site d'un site principal pour gérer les appareils mobiles.

    > [!NOTE]
    >  La modification du code de site affecte uniquement les nouvelles inscriptions et n'affecte pas les appareils inscrits existants.

8.  Dans la page **Coordonnées de contact de l’entreprise**, spécifiez les informations de contact de l’entreprise visibles par les utilisateurs, sous **Contacter le service informatique**, dans l’application Portail d’entreprise. Fournissez les informations de contact de votre entreprise, puis cliquez sur **Suivant**.

9. Dans la page **Logo de l’entreprise**, choisissez d’afficher éventuellement un logo dans le Portail d’entreprise, puis cliquez sur **Suivant**.

10. Effectuez toutes les étapes de l'Assistant.

> [!div class="button"]
[< Étape précédente](confirm-dns.md) [Étape suivante >](terms-and-conditions.md)

