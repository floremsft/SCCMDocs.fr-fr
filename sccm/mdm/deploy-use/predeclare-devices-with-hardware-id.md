---
title: "Prédéclarer des appareils avec des numéros IMEI ou numéros de série iOS"
description: "Prédéclarez vos appareils d’entreprise avec leur numéro IMEI ou leur numéro de série iOS."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: 3
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5c6cf3c1697b49708aa5192b67b08b700da7dc72
ms.openlocfilehash: 43d67aa664037c6da83260d5ada8e574510a8f7b

---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Prédéclarer des appareils avec des numéros IMEI ou numéros de série iOS

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez identifier des appareils d’entreprise en important leur numéro IMEI (International Mobile Equipment Identity) ou leur numéro de série iOS. Vous pouvez charger un fichier de valeurs séparées par des virgules (.csv) qui contient les numéros IMEI des appareils, ou saisir vous-même les informations sur les appareils.  Les informations importées définissent la **propriété** des appareils inscrits sur **Entreprise** dans les listes d’appareils. Une licence Intune est toujours nécessaire pour chaque utilisateur qui accède au service.  

## <a name="predeclare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Prédéclarer des appareils d’entreprise avec leur numéro IMEI ou leur numéro de série iOS

1.  Dans la console Configuration Manager, accédez à Ressources et Conformité > Vue d’ensemble > Tous les appareils d’entreprise > Appareils prédéclarés, puis cliquez sur Ajouter des appareils prédéclarés. L’Assistant Appareils prédéclarés s’ouvre.
2.  Spécifiez la façon dont vous souhaitez ajouter les informations sur les appareils :
     -  Charger un fichier CSV contenant des numéros IMEI et des informations détaillées
     -  Ajouter manuellement des numéros IMEI et des informations détaillées Pour entrer manuellement les informations, tapez le numéro IMEI ou le numéro de série iOS ainsi que les informations détaillées pour les appareils.

      Pour charger un fichier, accédez au fichier .csv contenant les informations à utiliser pour prédéclarer les appareils d’entreprise. Le fichier doit avoir le format suivant, à l’exclusion de la ligne du haut qui est fournie à titre indicatif uniquement. Chaque ligne doit contenir un numéro IMEI ou un numéro de série iOS. Seuls les numéros de série des appareils iOS peuvent être prédéclarés. Utilisez le numéro IMEI pour les autres plateformes d’appareils. Ce tableau contient des exemples de données :
      | IMEI #  | No de série iOS #  | SE | Détails |
      | :------------ |:---------------|:-----|:-----|
      | 123456789012345    |   | WINDOWS | Appareil d’entreprise Windows|
      |       | A1B2C3D4E5C6 |   iOS |  Appareil d’entreprise iOS|
      | 223456789012345 | E6D5C4B3A210 |   iOS |    Autre appareil iOS|
      | 323456789012345 |        |   iOS |  Troisième appareil iOS|
      | 123456789012346 |         |   Android |     Appareil d’entreprise Android|

    N’incluez pas de ligne d’en-tête dans votre fichier .csv. L’exemple ci-dessus en inclut une par souci de clarification uniquement.

    **Les colonnes peuvent contenir les valeurs suivantes :**    
      - Colonne 1 : numéro IMEI sans espace
      - Colonne 2 : numéro de série iOS
      - Colonne 3 : système d’exploitation de l’appareil :
         - IOS : tous les appareils iOS
         - WINDOWS : inclut les appareils Windows Phone, Windows 10 Mobile et PC Windows
         - ANDROID : tous les appareils Android
      - Colonne 4 - Détails (facultatif) : informations supplémentaires sur l’appareil affichées dans la console Configuration Manager. Colonne limitée à 1 024 caractères.

    Cliquez sur **Suivant**.

3. Passez en revue les résultats de l’importation du fichier. Si un numéro d’appareil avait déjà été importé, Configuration Manager affiche les appareils correspondants et les **détails** de remplacement. Sélectionnez les appareils pour lesquels vous voulez remplacer les détails. Les détails sur un appareil peuvent uniquement être modifiés en réimportant le numéro IMEI ou le numéro de série de l’appareil. Cliquez sur **Suivant** pour continuer ou sur **Retour** pour conserver les détails modifiés, puis terminez l’Assistant.

4. Si l’importation inclut des numéros de série iOS, vous devez attribuer ces appareils à un profil d’inscription. Sélectionnez **Profil d’inscription à affecter** dans la liste des profils disponibles, puis cliquez sur **Suivant**.

5. Cliquez sur **Suivant** pour afficher le résumé, puis terminez l’Assistant.



<!--HONumber=Nov16_HO1-->


