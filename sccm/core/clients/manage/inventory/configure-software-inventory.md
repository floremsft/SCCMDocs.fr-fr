---
title: Konfigurieren einer Softwareinventur | Microsoft-Dokumentation
description: "Konfigurieren Sie die Softwareinventur, und schließen Sie Ordner aus der Softwareinventur in Configuration Manager aus."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: e60cec71c425e5e42d450cbeee366528d4b42405
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Konfigurieren der Softwareinventur in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

 Mithilfe dieses Verfahrens werden die Clientstandardeinstellungen für die Softwareinventur konfiguriert. Sie gilt für alle Computer in der Hierarchie. Wenn Sie diese Einstellungen nur auf manche Computer anwenden möchten, erstellen Sie eine benutzerdefinierte Geräteclienteinstellung und weisen diese einer Sammlung mit den Computern zu, auf denen Sie die Softwareinventur verwenden möchten. Weitere Informationen zum Erstellen benutzerdefinierter Geräteeinstellungen finden Sie unter [Konfigurieren von Geräteclienteinstellungen in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

## <a name="to-configure-software-inventory"></a>So konfigurieren Sie die Softwareinventur  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

5.  Wählen Sie im Dialogfeld **Standardeinstellungen** die Option **Softwareinventur** aus.  

6.  Konfigurieren Sie in der Liste **Geräteeinstellungen** die folgenden Werte:  

    -   **Softwareinventur für Clients aktivieren** – Wählen Sie in der Dropdownliste **Wahr** aus.  

    -   **Zeitplan für die Softwareinventur und Dateisammlung planen** – Konfiguriert das Intervall, in dem der Client Softwareinventur und Dateien sammelt.   

7.  Konfigurieren Sie die erforderlichen Clienteinstellungen. Eine Liste der Clienteinstellungen für Softwareinventur, die Sie konfigurieren können, finden Sie im Abschnitt [Softwareinventur](../../../../core/clients/deploy/about-client-settings.md#software-inventory) des Themas [Clienteinstellungen in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

 Die Clientcomputer werden beim nächsten Clientrichtliniendownload mit diesen Einstellungen konfiguriert. Informationen zum Initiieren des Abrufens von Richtlinien für einen einzelnen Client finden Sie unter [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  


## <a name="to-exclude-folders-from-software-inventory"></a>So schließen Sie Ordner aus der Softwareinventur aus  

1.  Erstellen Sie mit "Notepad.exe" eine leere Datei namens **Skpswi.dat**.  

2.  Klicken Sie mit der rechten Maustaste auf die Datei **Skpswi.dat** , und klicken Sie dann auf **Eigenschaften**. Wählen Sie in den Dateieigenschaften für die Datei "Skpswi.dat" das Attribut **Ausgeblendet** aus.  

3.  Platzieren Sie die Datei **Skpswi.dat** im Stammverzeichnis jeder Clientfestplatte oder Ordnerstruktur, die von der Softwareinventur ausgeschlossen werden soll.  

> [!NOTE]  
>  Die Softwareinventur inventarisiert das Clientlaufwerk nicht noch einmal, außer diese Datei wird vom Laufwerk auf dem Clientcomputer gelöscht.