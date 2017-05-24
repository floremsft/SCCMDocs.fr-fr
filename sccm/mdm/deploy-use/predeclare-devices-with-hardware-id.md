---
title: "Prédéclarer des appareils avec des numéros IMEI ou numéros de série iOS | Microsoft Docs"
description: "Prédéclarez vos appareils d’entreprise avec leur numéro IMEI ou leur numéro de série iOS."
ms.custom: na
ms.date: 03/24/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: 3
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: e6833951db27b227a3ca22925e9d9f4c3fc443fc
ms.openlocfilehash: e8606b8a9268a0a0668b75070cf35894f4794123
ms.contentlocale: fr-fr
ms.lasthandoff: 05/17/2017

---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Prédéclarer des appareils avec des numéros IMEI ou numéros de série iOS

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez identifier des appareils d’entreprise en important leur numéro IMEI (International Mobile Equipment Identity) ou leur numéro de série iOS. Vous pouvez charger un fichier de valeurs séparées par des virgules (.csv) contenant les numéros IMEI des appareils ou saisir manuellement les informations sur les appareils.  Les informations importées définissent la **propriété** des appareils inscrits sur **Entreprise** dans les listes d’appareils. Une licence Intune reste nécessaire pour chaque utilisateur qui accède au service.  

Lorsque vous téléchargez des numéros de série d’appareils iOS appartenant à l’entreprise, ils doivent être associés à un profil d’inscription d’entreprise. Les appareils doivent être ensuite inscrits à l’aide du programme d’inscription des appareils Apple (DEP) ou d’Apple Configurator pour qu’ils apparaissent comme appartenant à l’entreprise.

## <a name="how-to-predeclare-corporate-owned-devices"></a>Comment prédéclarer des appareils d’entreprise

1.    Dans la console Configuration Manager, accédez à **Actifs et Conformité** > **Vue d’ensemble** > **Tous les appareils d’entreprise** > **Predeclared devices** (Appareils prédéclarés).

2.  Cliquez sur **Create Predeclared Devices** (Créer des appareils prédéclarés). L’Assistant Create Predeclared Devices (Création d’appareils prédéclarés) s’ouvre.

3.    Choisissez la façon dont vous souhaitez ajouter les informations sur les appareils :

     -    **Charger un fichier CSV contenant des numéros IMEI ou numéros de série et des informations détaillées**

        Pour cette option, cliquez sur **Parcourir** pour spécifier le fichier .csv contenant les informations à utiliser pour prédéclarer les appareils d’entreprise. Le fichier .csv doit être formaté correctement. Pour plus d’informations, consultez [Format pour le chargement des fichiers .csv](#format-for-uploading-csv-files).

     -    **Ajouter manuellement des numéros IMEI ou numéros de série et des informations détaillées**

        Pour entrer manuellement les informations, tapez le numéro IMEI ou le numéro de série iOS ainsi que les informations détaillées pour les appareils. Corrigez les éventuels avertissements ou erreurs avant de continuer.

    Cliquez sur **Suivant**.

4. Si vous avez chargé un fichier .csv, passez en revue les résultats de l’importation du fichier. Si un numéro d’appareil avait déjà été importé, Configuration Manager affiche les appareils correspondants et les **détails** de remplacement. Sélectionnez les appareils pour lesquels vous voulez remplacer les détails. Les détails sur un appareil peuvent uniquement être modifiés en réimportant le numéro IMEI ou le numéro de série de l’appareil.

  Si vous choisissez d’entrer manuellement le numéro, remplissez le formulaire pour les appareils que vous souhaitez prédéclarer.

  Cliquez sur **Suivant** pour continuer.

4. Si votre liste inclut des numéros de série iOS, sélectionnez **Profil d’inscription à affecter** dans la liste des profils disponibles, puis cliquez sur **Suivant**.

5. Cliquez sur **Suivant** pour passer en revue les détails, puis à nouveau sur **Suivant** pour charger les données.

6. Cliquez sur **Fermer** pour terminer.

## <a name="format-for-uploading-csv-files"></a>Format pour le chargement des fichiers .csv

Le fichier .csv que vous utilisez pour identifier des appareils par numéro IMEI ou numéro de série doit avoir le format suivant, à l’exception de la ligne supérieure fournie à titre indicatif uniquement. Chaque ligne doit contenir un numéro d’identification : un numéro IMEI ou un numéro de série iOS. Vous pouvez spécifier ces deux numéros. Les numéros IMEI peuvent être utilisés pour les appareils Android, iOS et Windows. Les numéros de série iOS sont également pris en charge.  Ce tableau contient des exemples de données :

| Numéro IMEI  | Numéro de série iOS  | SE | Détails |
|------------ |---------------|-----|-----|
| 123456789012345    |   | WINDOWS | Appareil d’entreprise Windows|
|   | A1B2C3D4E5C6 | IOS |     Appareil d’entreprise iOS|
| 223456789012345 | E6D5C4B3A210 |   IOS |     Autre appareil iOS|
| 323456789012345 |        |   IOS |     Troisième appareil iOS|
| 123456789012346 |         |   ANDROID |     Appareil d’entreprise Android|

N’incluez pas de ligne d’en-tête dans votre fichier .csv. L’exemple suivant montre les mêmes données au format CSV :

```
123456789012345,,WINDOWS,Company-owned Windows device
,A1B2C3D4E5C6,IOS,Company-owned iOS device
223456789012345,E6D5C4B3A210,IOS,Another iOS device
323456789012345,,IOS,A third iOS device
123456789012346,,ANDROID,Company-owned Android device
```

Les colonnes du fichier .csv acceptent les valeurs suivantes :

| Colonne 1 | Colonne 2 | Colonne 3 | Colonne 4 |
|---|---|---|---|
|Numéro IMEI sans espace | Numéro de série iOS | IOS, WINDOWS ou ANDROID | Détails facultatifs sur l’appareil (1 024 caractères au maximum) |

