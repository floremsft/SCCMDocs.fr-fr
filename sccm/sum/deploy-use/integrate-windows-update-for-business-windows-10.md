---

title: "Intégration à Windows Update for Business dans Windows 10 | Configuration Manager"
description: "Utilisez Windows Update for Business pour tenir à jour les appareils Windows 10 de votre organisation connectés au service Windows Update."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: c4c6e50d0e1a34653226369cffdc0bde905398fc


---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>Intégration avec Windows Update for Business dans Windows 10

*S’applique à : System Center Configuration Manager (Current Branch)*

Windows Update for Business (WUfB) vous permet de garantir la mise à jour des appareils Windows 10 de votre organisation avec les mécanismes de sécurité et les fonctionnalités Windows les plus récents quand ces appareils se connectent directement au service Windows Update (WU). Configuration Manager peut faire la distinction entre les ordinateurs Windows 10 qui utilisent WUfB et WSUS pour obtenir les mises à jour logicielles.  

 Certaines fonctionnalités de Configuration Manager ne sont plus disponibles quand les clients Configuration Manager sont configurés pour recevoir des mises à jour de Windows Update, notamment WUfB ou Windows Insiders :  

-   Rapports de conformité Windows Update :  

    -   Configuration Manager ne sera pas au courant des mises à jour publiées sur Windows Update. Les clients Configuration Manager configurés pour les mises à jour reçues à partir de Windows Update indiquent **inconnu** pour ces mises à jour dans la console Configuration Manager.  

    -   La résolution des problèmes liés à l’état de conformité global est difficile, car l’état **inconnu** concernait auparavant uniquement les clients qui n’avaient pas signalé leur état d’analyse à WSUS.  Maintenant, il inclut également les clients Configuration Manager qui reçoivent les mises à jour de Windows Update.  

    -   L’accès conditionnel (pour les ressources d’entreprise) basé sur l’état de conformité de mise à jour ne fonctionnera pas comme prévu pour les clients qui reçoivent des mises à jour de Windows Update, car ils ne respecteront jamais la conformité de Configuration Manager.  

    -   La conformité des mises à jour de définition fait partie des rapports de conformité de mise à jour globaux et ne fonctionnera pas non plus comme prévu.  La conformité des mises à jour de définition fait également partie de l’évaluation de l’accès conditionnel.  

-   Les rapports Endpoint Protection globaux pour Defender basés sur l’état de conformité de mise à jour retourneront des résultats incorrects en raison des données d’analyse manquantes.  

-   Configuration Manager ne pourra pas déployer les mises à jour Microsoft, telles qu’Office, Internet Explorer et Visual Studio, vers les clients qui sont connectés à WUfB pour recevoir des mises à jour.  

-   Configuration Manager ne pourra pas déployer les mises à jour tierces publiées dans WSUS et gérées par le biais de Configuration Manager vers les clients qui sont connectés à WUfB pour recevoir des mises à jour.  

-   Le déploiement de client complet Configuration Manager qui utilise l’infrastructure de mises à jour logicielles ne fonctionnera pas pour les clients qui sont connectés à WUfB pour recevoir des mises à jour.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Identifier les clients qui utilisent WUfB pour Windows 10  
 Appliquez la procédure suivante pour identifier les clients qui utilisent WUfB pour obtenir les mises à niveau et les mises à jour Windows 10, configurez ces clients pour cesser d’utiliser WSUS pour obtenir les mises à jour, et déployez un paramètre d’agent client pour désactiver le flux de travail des mises à jour logicielles pour ces clients.  

 **Conditions préalables**  

-   Clients qui exécutent Windows 10 Desktop Pro ou Windows 10 Édition Entreprise version 1511 ou ultérieure  

-   [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) est déployé et les clients utilisent WUfB pour obtenir les mises à niveau et les mises à jour Windows 10.  

#### <a name="to-identify-clients-that-use-wufb"></a>Pour identifier les clients qui utilisent WUfB  

1.  Désactivez l’Agent Windows Update, s’il était précédemment activé, afin qu’il n’effectue pas l’analyse par rapport à WSUS.   
    La clé de Registre **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer** peut être définie pour indiquer si l’ordinateur effectue l’analyse par rapport à Windows Update ou à WSUS.  Lorsque la valeur est 2, il n’effectue pas l’analyse par rapport à WSUS.  

2.  Il existe un nouvel attribut, **UseWUServer**, sous le nœud **Windows Update** dans l’Explorateur de ressources Configuration Manager.  

3.  Créez un regroupement basé sur l’attribut **UseWUServer** pour tous les ordinateurs connectés via WUFB pour les mises à jour et les mises à niveau.  

4.  Créez un paramètre d’agent du client pour désactiver le flux de travail des mises à jour logicielles et déployer le paramètre sur le regroupement d’ordinateurs connectés directement à WUFB.  

5.  Les ordinateurs qui sont gérés via WUFB affichent **Inconnu** dans l’état de conformité et ne sont pas comptabilisés dans le pourcentage de conformité global.  



<!--HONumber=Nov16_HO1-->


