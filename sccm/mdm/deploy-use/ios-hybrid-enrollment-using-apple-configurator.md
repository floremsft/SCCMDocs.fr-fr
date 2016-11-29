---
title: "Inscription d’appareils iOS à l’aide d’Apple Configurator pour les déploiements hybrides avec Configuration Manager"
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: 5
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 19f4880d6e7ba3da2e4bcfe725c1c806ee3b3334


---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>Inscription d’appareils iOS à l’aide d’Apple Configurator pour les déploiements hybrides avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les entreprises qui achètent des appareils iOS pour leurs employés peuvent les gérer à l’aide de Microsoft Intune. Vous pouvez préinscrire des appareils iOS en les connectant via un câble USB à un ordinateur Mac qui exécute Apple Configurator. Avant l’inscription, vous devez préparer un profil d’appareil d’entreprise Intune dans la console d’administration Intune et l’exporter vers l’ordinateur Mac. Le processus d’inscription restaure les paramètres d’usine de l’appareil et suit le processus de l’Assistant Configuration pour configurer l’appareil. La procédure qui suit est recommandée pour les appareils iOS dédiés utilisés par un seul utilisateur pour accéder à la messagerie professionnelle et aux ressources de l’entreprise comme les applications.  

##  <a name="a-namebkmksaea-apple-configurator-enrollment-via-setup-assistant"></a><a name="BKMK_SAE"></a> Inscription d’Apple Configurator via l’Assistant Configuration  
 Apple Configurator vous permet de rétablir les paramètres d’usine des appareils iOS et de les préparer de façon à ce que leur nouvel utilisateur puisse les configurer.  Cette méthode implique de connecter l’appareil iOS à un ordinateur Mac via une connexion USB pour configurer l’inscription d’entreprise. Elle suppose que vous utilisez Apple Configurator 2.0.  

 **Conditions préalables**  

-   Accès physique aux appareils iOS  

-   Numéros de série des appareils : [Localisation du numéro de série de votre produit Apple](https://support.apple.com/en-us/HT204308)  

-   Câbles de connexion USB  

-   Ordinateur Mac avec [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017)  

#### <a name="enable-setup-assistant-enrollment-with-configuration-manager-and-intune"></a>Activer l’inscription via l’Assistant Configuration avec Configuration Manager et Intune  

1.  **Ajouter un profil d'inscription des appareils d'entreprise**   
    Dans la console Configuration Manager, dans l’espace de travail **Ressources et Conformité**, développez **Vue d’ensemble**, **Tous les appareils d’entreprise** et **iOS**, puis cliquez sur **Profils d’inscription**. Cliquez sur **Créer un profil** sous l’onglet **Accueil** pour ouvrir l’Assistant Création d’un profil. Configurez les paramètres des pages suivantes :  

    1.  Dans la page **Général**, spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

        -   **Nom** : nom du profil d’inscription d’appareil. (Non visible pour les utilisateurs)  

        -   **Description** : description du profil d'inscription d'appareil. (Non visible pour les utilisateurs)  

        -   **Affinité utilisateur** : spécifie la façon dont les appareils sont inscrits. Pour la plupart des scénarios de l’Assistant Configuration, utilisez **Demander une affinité utilisateur**.  

            -   **Demander une affinité utilisateur**: l’appareil doit être affilié à un utilisateur durant la configuration initiale. Il peut ensuite être autorisé à accéder aux données de l’entreprise et à envoyer des e-mails au nom de cet utilisateur.  

            -   **Pas d'affinité utilisateur**: L'appareil n'est pas affilié à un utilisateur. Utilisez cette affiliation pour les appareils qui effectuent des tâches sans accéder aux données de l'utilisateur local. Les applications nécessitant une affiliation de l'utilisateur ne fonctionneront pas.  

    2.  Dans la page **Programme d’inscription d’appareils**, laissez la case **Configurer les paramètres DEP pour ce profil** cochée, puis cliquez sur **Suivant**.  

    3.  Examinez le résumé, puis cliquez sur Suivant.  

2.  **Ajouter des appareils iOS à inscrire avec l’Assistant Configuration**   
    Dans la console Configuration Manager, dans l’espace de travail **Ressources et Conformité**, développez **Vue d’ensemble**, **Tous les appareils d’entreprise** et **iOS**, puis cliquez sur **Informations sur l’appareil**. Cliquez ensuite sur **Ajouter des appareils**. Vous pouvez ajouter des appareils de deux manières :  

    - Vous pouvez **charger un fichier CSV qui contient les numéros de série et les détails** : créez une liste de valeurs séparées par des virgules (.csv) de deux colonnes sans en-tête, limitée à 5 000 appareils ou 5 Mo par fichier csv. Pour chaque ligne, la première cellule correspond au numéro de série de l’appareil et la deuxième cellule aux détails de l’appareil (facultatif).

  Dans un éditeur de texte, ce fichier .csv s'affiche comme suit :  

    ```  
    0000000,PO 1234  
    111111111,PO 1234  
    ```  

    - Vous pouvez également **ajouter manuellement les numéros de série et les détails** : entrez le numéro de série et les détails d’au maximum cinq appareils.  

    Puis cliquez sur **Suivant**.  

3.  **Sélectionnez les appareils à inscrire**   
    Confirmez les appareils à inscrire. Il n'est pas possible d'importer des numéros de série déjà inscrits ou inscrits par d'autres moyens. Cliquez sur **Suivant** pour continuer.  

4.  **Attribuer un profil**   
    Spécifiez le profil à attribuer aux appareils ajoutés dans la liste des profils disponibles, vérifiez les **Détails du profil d’inscription**, puis cliquez sur **Terminer**. Les appareils ajoutés manuellement peuvent être affectés à tout profil d'inscription, mais les appareils synchronisés avec le programme d'inscription d'appareils doivent être attribués à un profil où ce programme est activé.  

5.  **Sélectionner un profil à déployer sur les appareils iOS**   
    Dans la console Configuration Manager, dans l’espace de travail **Ressources et Conformité**, développez **Vue d’ensemble**, **Tous les appareils d’entreprise** et **iOS**, puis cliquez sur **Profils d’inscription** et sélectionnez le profil d’appareil à déployer sur des appareils mobiles. Cliquez sur **Exporter** dans la barre des tâches. Copiez et enregistrez la valeur **URL de profil**. Vous la chargerez dans Apple Configurator plus tard pour définir le profil Intune utilisé par les appareils iOS.  L’URL du profil d’inscription est valide pendant deux semaines après son exportation. Après deux semaines, vous devez exporter un nouveau fichier d’URL pour inscrire des appareils iOS.  

     Pour prendre en charge Apple Configurator 2, l’URL du profil 2.0 doit être modifiée. Remplacez :  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     par  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```  

6.  **Préparer l’appareil avec Apple Configurator**   
    Les appareils iOS sont connectés à l'ordinateur Mac et inscrits pour la gestion des appareils mobiles.  

    > [!WARNING]  
    >  Les paramètres d'usine des appareils sont rétablis pendant le processus d'inscription.  

    1.  Sur un ordinateur Mac, ouvrez **Apple Configurator 2**.  Dans la barre de menus, cliquez sur **Apple Configurator 2**, puis cliquez sur **Préférences**.  

    2.  Dans le volet Préférences, sélectionnez **Serveurs**, puis cliquez sur le symbole « + » situé sous le volet gauche pour lancer l’Assistant Serveur MDM. Cliquez sur **Suivant**.  

    3.  Entrez le **Nom** et l’**URL d’inscription** du serveur MDM, définis à l’étape 5 ci-dessus. Cliquez sur **Suivant**.  

         Si vous recevez un avertissement à propos des exigences de profil de confiance pour Apple TV, vous pouvez annuler en toute sécurité l’option **Profil de confiance** en cliquant sur le « X » gris. Vous pouvez également ignorer tout avertissement relatif au certificat d’ancrage (ou certificat racine). Pour continuer, cliquez sur **Suivant** jusqu’à la fin de l’exécution de l’Assistant.  

    4.  Dans le volet **Serveurs**, cliquez sur « Modifier » en regard du profil du nouveau serveur. Assurez-vous que l’URL d’inscription correspond exactement à l’URL exportée à partir d’Intune. Entrer à nouveau l’URL d’origine si elle est différente, puis **Enregistrez** le profil d’inscription exporté à partir d’Intune.  

    5.  Connectez les appareils mobiles iOS à l'ordinateur Apple à l'aide d'un adaptateur USB.  

        > [!WARNING]  
        >  Les paramètres d'usine des appareils sont rétablis pendant le processus d'inscription. Il est recommandé de réinitialiser l’appareil et de le mettre sous tension. Les appareils devraient s’afficher sur l’écran Hello lorsque vous démarrez l’Assistant Configuration.  

    6.  Cliquez sur **Préparer**. Dans le volet **Prepare iOS Device** (Préparer l’appareil iOS), sélectionnez **Manual** (Manuel), puis cliquez sur **Suivant**.  

    7.  Dans le volet **Enroll in MDM Server** (Inscription dans un serveur MDM), sélectionnez le nom du serveur que vous avez créé, puis cliquez sur **Suivant**.  

    8.  Dans le volet **Enroll in MDM Server** (Inscription dans un serveur MDM), sélectionnez le nom du serveur que vous avez créé, puis cliquez sur **Suivant**.  

    9. Dans le volet **Create an Organization** (Créer une organisation), choisissez ou créez une **organisation**, puis cliquez sur **Suivant**.  

    10. Dans le volet **Configure iOS Setup Assistant** (Configurer l’Assistant Installation iOS), choisissez les étapes présentées à l’utilisateur, puis cliquez sur **Prepare** (Préparer). Si vous y êtes invité, authentifiez-vous pour mettre à jour les paramètres d’approbation.  

    11. Une fois la préparation de l’appareil iOS terminée, vous pouvez déconnecter le câble USB.  

7.  **Distribuer les appareils**   
    Les appareils sont désormais prêts pour l’inscription d’entreprise. Éteignez les appareils et distribuez-les aux utilisateurs. Quand vous allumez un appareil, l'Assistant Configuration démarre et invite l'utilisateur à identifier son compte professionnel ou scolaire.



<!--HONumber=Nov16_HO1-->


