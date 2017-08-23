---
title: "Upgraden von macOS-Clients – Configuration Manager | Microsoft-Dokumentation"
description: Upgraden Sie Clients auf Macintosh-Computern in System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
caps.latest.revision: "10"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 502116b66fc14914ca0606ae416e82202824de7a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-system-center-configuration-manager"></a>Aktualisieren von Clients auf Macintosh-Computern in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Befolgen Sie die oben beschriebenen allgemeinen Schritte, um den Client für Macintosh-Computer mithilfe einer System Center Configuration Manager-Anwendung zu aktualisieren. Alternativ können Sie auch die Macintosh-Clientinstallationsdatei herunterladen, in einen freigegebenen Netzwerkpfad oder einen lokalen Ordner auf dem Macintosh-Computer kopieren und dann die Benutzer auffordern, die Installation manuell auszuführen.  

> [!NOTE]  
>  Stellen Sie vor der Ausführung dieser Schritte sicher, dass Ihr Macintosh-Computer die Voraussetzungen erfüllt. Informationen hierzu finden Sie unter [Supported operating systems for clients and devices for System Center Configuration Manager (Unterstützte Betriebssysteme für Clients und Geräte für System Center Configuration Manager)](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

## <a name="step-1-download-the-latest-mac-client-installation-file-from-the-microsoft-download-center"></a>Schritt 1: Herunterladen der aktuellen Macintosh-Clientinstallationsdatei aus dem Microsoft Download Center  
 Der Macintosh-Client für Configuration Manager wird nicht auf den Configuration Manager-Installationsmedien bereitgestellt und muss aus dem Microsoft Download Center heruntergeladen werden. Die Macintosh-Clientinstallationsdateien sind in einer Windows Installer-Datei mit dem Namen ConfigmgrMacClient.msi enthalten.  

 Diese Datei steht im [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=525184)als Download zur Verfügung.  

## <a name="step-2-run-the-downloaded-installation-file-to-create-the-mac-client-installation-file"></a>Schritt 2: Ausführen der heruntergeladenen Installationsdatei zum Erstellen der Macintosh-Clientinstallationsdatei  
 Führen Sie auf einem Computer unter Windows die heruntergeladene Datei **ConfigmgrMacClient.msi** aus, um die Macintosh-Clientinstallationsdatei mit dem Namen **Macclient.dmg**zu entpacken. Nach dem Entpacken der Dateien befindet sich diese Datei standardmäßig im Ordner **C:\Programme (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client** auf dem Windows-Computer.  

## <a name="step-3-extract-the-client-installation-files"></a>Schritt 3: Extrahieren der Clientinstallationsdateien  
 Kopien Sie die Datei Macclient.dmg in eine Netzwerkfreigabe oder einen lokalen Ordner auf dem Macintosh-Computer. Stellen Sie dann auf dem Macintosh-Computer die Datei Macclient.dmg bereit, und öffnen Sie sie. Kopieren Sie die Dateien in einen Ordner auf dem Macintosh-Computer.  

## <a name="step-4-create-a-cmmac-file-that-can-be-used-to-create-an-application"></a>Schritt 4: Erstellen einer CMMAC-Datei zum Erstellen einer Anwendung  

1.  Erstellen Sie mit dem Tool **CMAppUtil** (aus dem Ordner **Tools** der Macintosh-Clientinstallationsdateien) eine CMMAC-Datei aus dem Clientinstallationspaket. Diese Datei wird zum Erstellen der Configuration Manager-Anwendung verwendet.  

2.  Kopieren Sie die neue Datei **CMClient.pkg.cmmac** an einen Speicherort, der für den Computer verfügbar ist, auf dem die Configuration Manager-Konsole läuft.  

 Weitere Informationen finden Sie unter [Zusätzliche Verfahren zum Erstellen und Bereitstellen von Anwendungen für Macintosh-Computer](/sccm/apps/get-started/creating-mac-computer-applications#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers).  

## <a name="step-5-create-and-deploy-an-application-containing-the-mac-client-files"></a>**Schritt 5**: Erstellen und Bereitstellen einer Anwendung mit den Macintosh-Clientdateien  

1.  Erstellen Sie in der Configuration Manager-Konsole eine Anwendung aus der Datei **CMClient.pkg.cmmac**, die die Clientinstallationsdateien enthält.  

2.  Stellen Sie diese Anwendung auf Macintosh-Computern in Ihrer Hierarchie bereit.  

 Weitere Informationen finden Sie unter [Erstellen von Anwendungen für Macintosh-Computer mit System Center Configuration Manager](../../../../apps/get-started/creating-mac-computer-applications.md).  

## <a name="step-6-users-install-the-latest-client"></a>Schritt 6: Installieren des aktuellen Clients durch Benutzer  
 Benutzer von Macintosh-Clients werden informiert, dass ein Update für den Configuration Manager-Client verfügbar ist und installiert werden muss. Nachdem die Benutzer den Client installiert haben, müssen sie ihren Macintosh-Computer neu starten.  

 Nach dem Neustart des Computers wird automatisch der Assistent für die Computeranmeldung ausgeführt, um ein neues Benutzerzertifikat anzufordern.  

 Wenn Sie die Configuration Manager-Registrierung nicht verwenden, sondern das Clientzertifikat unabhängig von Configuration Manager installieren, finden Sie weitere Informationen unter [Konfigurieren des aktualisierten Clients für die Verwendung eines vorhandenen Zertifikats](#BKMK_UpgradingClient_MachineEnrollment).  

##  <a name="BKMK_UpgradingClient_MachineEnrollment"></a> Configure the upgraded client to use an existing certificate  
 Führen Sie das folgende Verfahren aus, um zu verhindern, dass der Assistent für die Computeranmeldung ausgeführt wird, und den aktualisierten Client für die Verwendung eines vorhandenen Clientzertifikats zu konfigurieren.  

-   Erstellen Sie in der Configuration Manager-Konsole ein Konfigurationselement mit dem Typ **Mac OS X**.  

-   Fügen Sie diesem Konfigurationselement eine Einstellung mit dem Einstellungstyp **Skript**hinzu.  

-   Fügen Sie der Einstellung das folgende Skript hinzu:  

    ```  
    #!/bin/sh  
    echo "Starting script\n"  
    echo "Changing directory to MAC Client\n"  
    cd /Users/Administrator/Desktop/'MAC Client'/  
    echo "Import root cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
    echo "Using openssl to convert pfx to a crt\n"  
    /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
    echo "Adding trust to root cert\n"  
    /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
    echo "Import client cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
    echo "Executing ccmclient with MP\n"  
    sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
    echo "Editing Plist file\n"  
    sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
    echo "Changing directory to CCM\n"  
    cd /Library/'Application Support'/Microsoft/CCM/  
    echo "Making connection to the server\n"  
    sudo open ./CCMClient  
    echo "Ending Script\n"  
    exit  

    ```  

-   Fügen Sie das Konfigurationselement einer Konfigurationsbaseline hinzu, und stellen Sie dann die Konfigurationsbaseline auf allen Macintosh-Computern bereit, auf denen ein Zertifikat unabhängig von Configuration Manager installiert wird.  

 Weitere Informationen zum Erstellen und Bereitstellen von Konfigurationselementen für Macintosh-Computer finden Sie unter [Erstellen von Konfigurationselementen für Mac OS X-Geräte, die mit dem System Center Configuration Manager-Client verwaltet werden](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) und [Bereitstellen von Konfigurationsbaselines in System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md).  
