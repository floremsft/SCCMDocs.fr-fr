---
title: Aktualisieren von Evaluierungsinstallationen | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie ein Upgrade einer Evaluierungsinstallation auf eine vollständige Installation von System Center Configuration Manager durchführen."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8f951805c2fc25059965c15c94934c0f8546735c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-an-evaluation-installation-of-system-center-configuration-manager-to-a-full-installation"></a>Aktualisieren einer Evaluierungsinstallation auf eine vollständige Installation von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Wenn Sie eine Evaluierungsversion von System Center Configuration Manager installiert haben, wird die Configuration Manager-Konsole nach 180 Tagen für Schreibvorgänge gesperrt, bis Sie das Produkt in Setup auf der Seite **Standortwartung** aktivieren. Sie haben jederzeit vor oder nach Ablauf des 180-tägigen Zeitraums die Möglichkeit, ein Upgrade der Evaluierungsinstallation auf eine Vollversion durchzuführen.  

> [!NOTE]  
>  Wenn Sie von einer Configuration Manager-Konsole aus eine Verbindung mit einer Evaluierungsinstallation von Configuration Manager herstellen, wird in der Titelleiste der Konsole die Anzahl der verbleibende Tage für die Gültigkeit der Evaluierungsinstallation angegeben. Die Tagesangabe wird nicht automatisch aktualisiert und ändert sich nur, wenn Sie eine neue Verbindung mit einem Standort herstellen.  

 Sie können ein Upgrade der folgenden Standorte durchführen, an denen eine Evaluierungsinstallation ausgeführt wird:  

-   Standort der zentralen Verwaltung  
-   Primärer Standort  

Da sekundäre Standorte nicht als Evaluierungsinstallationen behandelt werden, müssen Sie einen sekundären Standort nicht ändern, nachdem für den entsprechenden primären übergeordneten Standort ein Upgrade auf eine Vollversion durchgeführt wurde.  

Voraussetzungen für ein Upgrade einer Evaluierungsversion auf eine lizenzierte Version:  

-   Sie müssen während des Upgrades ein gültiges Produkt verwenden.  
-   Ihr Konto benötigt **Administratorrechte** auf dem Computer, auf dem der Standort installiert ist.  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>So führen Sie ein Upgrade einer Evaluierungsversion von Configuration Manager auf eine lizenzierte Version aus  

1.  Führen Sie auf dem Standortserver im Configuration Manager-Installationsordner (**%path%\BIN\X64**) die Datei **Setup.exe** (Configuration Manager-Setup) aus. Sie müssen die Kopie von Setup ausführen, die sich auf dem Standortserver im Ordner „Configuration Manager“ befindet, da keine Standortwartungsoptionen verfügbar sind, wenn Sie Setup auf dem Installationsmedium ausführen.  
2.  Wählen Sie auf der Seite **Vorbereitung** die Option **Weiter**.  
3.  Wählen Sie auf der Seite **Erste Schritte** die Option **Standortwartung durchführen oder diesen Standort zurücksetzen** aus, und wählen Sie dann **Weiter**.  
4.  Wählen Sie auf der Seite **Standortwartung** die Option **Upgrade von der Evaluation Edition auf eine lizenzierte Edition ausführen** aus. Geben Sie einen gültigen Product Key ein, und wählen Sie dann **Weiter**.  
5.  Lesen und akzeptieren Sie auf der Seite **Microsoft Software-Lizenzbedingungen** die Lizenzbedingungen, und wählen Sie anschließend **Weiter**.  
6.  Wählen Sie auf der Seite **Konfiguration** die Schaltfläche **Schließen**, um den Assistenten zu beenden.  

    > [!NOTE]  
    >  Die Titelleiste einer Configuration Manager-Konsole, die mit dem aktualisierten Standort verbunden bleibt, gibt ggf. an, dass es sich bei dem Standort noch immer um eine Evaluierungsversion handelt, bis Sie eine neue Verbindung zwischen Konsole und Standort herstellen.  
