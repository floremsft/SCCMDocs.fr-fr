---
title: "Configurer l’inventaire logiciel | System Center Configuration Manager"
description: "Configurez l’inventaire logiciel et un dossier d’exclusion de l’inventaire dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: cc226259-0e28-410a-94d3-223bdc948818
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5f30eb754832fcc259caf853dc33ccfcb82cf8bc


---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Guide pratique pour configurer l’inventaire logiciel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez créer un fichier masqué appelé **Skpswi.dat** et le placer à la racine du disque dur d’un client pour l’exclure de l’inventaire logiciel System Center Configuration Manager. Vous pouvez également placer ce fichier à la racine de n'importe quelle structure de dossiers que vous souhaitez exclure de l'inventaire logiciel. Cette procédure peut être utilisée pour désactiver l'inventaire logiciel sur une station de travail unique ou sur un client de serveur, tel qu'un serveur de fichiers volumineux.  

> [!NOTE]  
>  L'inventaire logiciel n'effectue pas un nouvel inventaire du lecteur de client à moins que le fichier ne soit supprimé du lecteur sur l'ordinateur client.  

### <a name="to-exclude-folders-from-software-inventory"></a>Pour exclure des dossiers d'un inventaire logiciel  

1.  Dans Notepad.exe, créez un fichier vide intitulé **Skpswi.dat**.  

2.  Cliquez avec le bouton droit sur le fichier **Skpswi.dat** et cliquez sur **Propriétés**. Dans les propriétés du fichier Skpswi.dat, sélectionnez l'attribut **Masqué** .  

3.  Placez le fichier **Skpswi.dat** à la racine du disque dur ou de la structure de dossiers de chaque client que vous souhaitez exclure de l'inventaire logiciel.  



<!--HONumber=Nov16_HO1-->


