---
title: Setup-Downloadprogramm | Microsoft-Dokumentation
description: "Erfahren Sie mehr über diese eigenständige Anwendung, die sicherstellen soll, dass Ihre Standortinstallation aktuelle Versionen der wichtigsten Installationsdateien verwendet."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b72148ecc16141843178cbd220fe021fab8be992
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="setup-downloader-for-system-center-configuration-manager"></a>Setup-Downloadprogramm für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bevor Sie das Setup zum Installieren oder Upgraden eines System Center Configuration Manager-Standorts ausführen, können Sie die eigenständige Setup-Downloadanwendung für die zu installierende Version von Configuration Manager verwenden, um aktualisierte Setupdateien herunterzuladen.  

Die Verwendung aktualisierter Setupdateien stellt sicher, dass für Ihre Standortinstallation aktuelle Versionen der wichtigsten Installationsdateien verwendet werden. Übersicht:   
-   Wenn Sie das Setup-Downloadprogramm zum Herunterladen von Dateien vor dem Starten des Setups verwenden, geben Sie einen Ordner zum Speichern der Dateien an.  
-   Das Konto, mit dem Sie das Setup-Downloadprogramm ausführen, benötigt **Vollzugriff**-Berechtigungen für den Downloadordner.  
-   Beim Ausführen von Setup zum Installieren oder Aktualisieren eines Standorts können Sie das Setup anweisen, diese lokale Kopie von Dateien zu verwenden, die Sie zuvor heruntergeladen haben. Dies verhindert, dass das Setup eine Verbindung mit Microsoft herstellen muss, wenn Sie die Installation oder das Upgrade des Standorts starten.  
-   Sie können die gleiche lokale Kopie der Setupdateien für nachfolgende Standortinstallationen oder -upgrades verwenden.  

Die folgenden Dateitypen werden vom Setup-Downloadprogramm heruntergeladen:  
-   Erforderliche verteilbare Dateien  
-   Sprachpakete  
-   Die neuesten Produktupdates für Setup  

Sie haben zwei Optionen zum Ausführen des Setup-Downloadprogramms:
- Die Anwendung mit der Benutzeroberfläche ausführen
- Die Anwendung für Befehlszeilenoptionen an einer Eingabeaufforderung ausführen


## <a name="run-setup-downloader-with-the-user-interface"></a>Führen Sie das Setup-Downloadprogramm auf der Benutzeroberfläche aus  

1.  Öffnen Sie auf einem Computer mit Internetzugriff den Windows-Explorer, und wechseln Sie zu **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**.  

2.  Doppelklicken Sie auf **Setupdl.exe**, um das Setup-Downloadprogramm zu öffnen.   

3. Geben Sie den Pfad zu dem Ordner mit den aktuellen Installationsdateien an, und klicken Sie dann auf **Herunterladen**. Das Setup-Downloadprogramm überprüft die Dateien im Downloadordner. Es werden nur die Dateien heruntergeladen, die fehlen oder die neuer sind als vorhandene Dateien. Es werden Unterordner für die heruntergeladenen Sprachen und weitere erforderliche Unterordner erstellt.  

4.  Überprüfen Sie die Downloadergebnisse anhand der Datei **ConfigMgrSetup.log** im Stammverzeichnis von Laufwerk C.  

## <a name="run-setup-downloader-from-a-command-prompt"></a>Starten Sie das Setup-Downloadprogramm mithilfe einer Eingabeaufforderung.  

1.  Gehen Sie in einem Eingabeaufforderungsfenster auf **&lt;*Configuration Manager-Installationsmedium*\>\SMSSETUP\BIN\X64**.   

2.  Führen Sie **Setupdl.exe** aus, um das Setup-Downloadprogramm zu öffnen.

    Sie können die folgenden Befehlszeilenoptionen mit **Setupdl.exe** verwenden:   

    -   **/VERIFY**: Verwenden Sie diese Option, um die Dateien im Downloadordner einschließlich der Sprachdateien zu überprüfen. Überprüfen Sie anhand der Liste in der Datei ConfigMgrSetup.log im Stammverzeichnis des Laufwerks C, welche Dateien veraltet sind. Wenn Sie diese Option verwenden, werden keine Dateien heruntergeladen.  

    -   **/VERIFYLANG**: Verwenden Sie diese Option, um die Sprachdateien im Downloadordner zu überprüfen. Überprüfen Sie anhand der Liste in der Datei ConfigMgrSetup.log im Stammverzeichnis des Laufwerks C, welche Sprachdateien veraltet sind.

    -   **/LANG**: Verwenden Sie diese Option, um nur die Sprachdateien in den Downloadordner herunterzuladen.  

    -   **/NOUI**: Verwenden Sie diese Option, um das Setup-Downloadprogramm zu starten, ohne die Benutzeroberfläche anzuzeigen. Sie müssen dann den **Downloadpfad** als Teil der Befehlszeile bei der Eingabeaufforderung angeben.  

    -   **&lt;Downloadpfad\>**: Sie können den Pfad zum Downloadordner angeben, um den Überprüfungs- oder den Downloadvorgang automatisch zu starten. Wenn Sie die Option **/NOUI** verwenden, müssen Sie den Downloadpfad angeben. Geschieht dies nicht, müssen Sie den Pfad angeben, sobald das Setup-Downloadprogramm geöffnet wird. Wenn der Ordner nicht vorhanden ist, wird er vom Setup-Downloadprogramm erstellt.  

    Beispielbefehle:

    -   **setupd &lt;Downloadpfad\>**  

        -   Das Setup-Downloadprogramm wird gestartet. Die Dateien im angegebenen Downloadordner werden überprüft, und nur fehlende Dateien oder Dateien mit aktuelleren Versionen werden heruntergeladen.     

    -   **setupdl /VERIFY &lt;Downloadpfad\>**  

        -   Das Setup-Downloadprogramm wird gestartet. Die Dateien im angegebenen Downloadordner werden überprüft.  

    -   **setupdl /NOUI &lt;Downloadpfad\>**  

        -   Das Setup-Downloadprogramm wird gestartet. Die Dateien im angegebenen Downloadordner werden überprüft, und nur fehlende oder aktuellere Dateien werden heruntergeladen.  

    -   **setupdl /LANG &lt;Downloadpfad\>**  

        -   Das Setup-Downloadprogramm wird gestartet. Die Sprachdateien im angegebenen Downloadordner werden überprüft, und nur fehlende oder aktuellere Sprachdateien werden heruntergeladen.  

    -   **setupdl /VERIFY**  

        -   Das Setup-Downloadprogramm wird gestartet. Anschließend müssen Sie den Pfad für den Downloadordner angeben. Nachdem Sie auf **Überprüfen** geklickt haben, werden die Dateien im Downloadordner vom Setup-Downloadprogramm überprüft.  

3.  Überprüfen Sie die Downloadergebnisse anhand der Datei **ConfigMgrSetup.log** im Stammverzeichnis von Laufwerk C.
