---
itle: 'Upgrade clients | Microsoft Docs | Linux UNIX '
description: Upgraden Sie einen Client auf einem Linux- oder UNIX-Server in System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 394ba7c236c05cc90a3d7f99eb6146b15d620f11
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Aktualisieren von Clients für Linux- und UNIX-Server in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können die Version des Clients für Linux und UNIX auf einem Computer auf eine neuere Clientversion aktualisieren, ohne vorher den aktuellen Client zu deinstallieren. Dazu installieren Sie das Installationspaket des neuen Clients auf dem Computer, wobei Sie die Befehlszeileneigenschaft **-keepdb** verwenden. Bei der Installation des Client für Linux und UNIX werden die vorhandenen Clientdaten mit den neuen Clientdateien überschrieben. Die Befehlszeileneigenschaft **-keepdb** bewirkt aber, dass beim Installationsprozess der eindeutige Bezeichner (GUID), die lokale Datenbank mit Informationen und der Zertifikatspeicher des Clients beibehalten werden. Diese Informationen werden dann für die Installation des neuen Clients verwendet.  

 Angenommen, Sie haben einen RHEL5-x64-Computer, auf dem der Client aus der ursprünglichen Version des Configuration Manager-Clients für Linux und UNIX ausgeführt wird. Um diesen Client auf die Clientversion des kumulativen Updates 1 zu aktualisieren, führen Sie das **install**-Skript manuell aus, um das entsprechende Clientpaket aus dem kumulativen Update 1 zu installieren, wobei Sie den Befehlszeilenschalter **-keepdb** hinzufügen. Die Befehlszeile sieht etwa folgendermaßen aus: **./install -mp <Hostname\> -sitecode <Code\> -keepdb ccm-Universal-x64.<Build\>.tar**  

## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Verwenden einer Softwarebereitstellung, um den Client auf Linux- und UNIX-Servern zu aktualisieren  
 Sie können eine Softwarebereitstellung verwenden, um den Client für Linux und UNIX auf eine neue Clientversion zu aktualisieren. Allerdings kann der System Center Configuration Manager-Client das Installationsskript nicht direkt ausführen, um den neuen Client zu installieren, denn bei der Installation eines neuen Clients muss zunächst der aktuelle Client deinstalliert werden. Hierdurch würde der Configuration Manager-Clientprozess, der das Installationsskript ausführt, beendet, bevor mit der Installation des neuen Clients begonnen wird. Damit Sie den neuen Client erfolgreich mit einer Softwarebereitstellung installieren können, müssen Sie die Installation so planen, dass sie zu einem späteren Zeitpunkt gestartet und über die zum Betriebssystem gehörenden Planungsfunktionen ausgeführt wird.  

 Zu diesem Zweck verwenden Sie eine Softwarebereitstellung, in der zunächst die Dateien für das Installationspaket des neuen Clients auf den Clientcomputer kopiert werden und dann ein Skript bereitgestellt und ausgeführt wird, mit dem der Clientinstallationsprozess geplant wird. In dem Skript wird der zum Betriebssystem gehörende **at**-Befehl verwendet, um den Start des Skripts zu verzögern. Dies hat zur Folge, dass das Ausführen des Skripts vom Betriebssystem des Clients und nicht vom Configuration Manager-Client auf dem Computer verwaltet wird. Dadurch wird es der Befehlszeile, die durch das Skript aufgerufen, ermöglicht, zunächst den Configuration Manager-Client zu deinstallieren und anschließend den neuen Client zu installieren, wodurch das Aktualisieren des Clients auf dem Linux- oder UNIX-Computer abgeschlossen wird. Nach Abschluss des Upgrades wird der aktualisierte Client weiterhin von Configuration Manager verwaltet.  

 Gehen Sie wie folgt vor, um eine Softwarebereitstellung zu konfigurieren, mit der der Client für Linux und UNIX aktualisiert wird. In den folgenden Schritten und Beispielen wird ein RHEL5-x64-Computer, auf dem die erste Version des Clients ausgeführt wird, auf die Clientversion des kumulativen Updates 1 aktualisiert.  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>So verwenden Sie eine Softwarebereitstellung, um den Client auf Linux- und UNIX-Servern zu aktualisieren  

1.  Kopieren Sie das neue Clientinstallationspaket auf den Computer, auf dem der Configuration Manager-Client ausgeführt wird, den Sie aktualisieren möchten.  

     Beispielsweise könnten Sie das Clientinstallationspaket und das Installationsskript für das kumulative Update 1 im folgenden Ordner auf dem Clientcomputer ablegen: **/tmp/PATCH**  

2.  Erstellen Sie ein Skript, mit dem der Configuration Manager-Client aktualisiert wird, und legen Sie eine Kopie des Skripts auf dem Clientcomputer in dem Ordner ab, in dem sich die Clientinstallationsdateien aus Schritt 1 befinden.  

     Für das Skript ist kein bestimmter Name erforderlich, es muss aber Befehlszeilen enthalten, die es ermöglichen, die Clientinstallationsdateien aus einem lokalen Ordner auf dem Clientcomputer zu verwenden und das Installationspaket zu installieren, indem die **-keepdb**-Befehlszeileneigenschaft verwendet wird. Sie verwenden die **-keepdb**-Befehlszeileneigenschaft, damit der eindeutige Bezeichner des aktuellen Clients erhalten bleibt, sodass er vom neuen Client verwendet werden kann.  

     Beispielsweise könnten Sie ein Skript namens **upgrade.sh** erstellen, das die folgenden Zeilen enthält, und das Skript dann in den Ordner **/tmp/PATCH** auf dem Clientcomputer kopieren:  

    ```  
    #!/bin/sh  
    #  
    /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

    ```  

3.  Implementieren Sie die Softwarebereitstellung so, dass für jeden Client der integrierte **at** -Befehl verwendet wird, um das Skript **upgrade.sh** auszuführen, wobei dieses nach einer kurzen Verzögerung gestartet wird.  

     Verwenden Sie beispielsweise die folgende Befehlszeile, um das Skript auszuführen: **at -f /tmp/upgrade.sh -m now + 5 minutes**  

 Nachdem der Client das Ausführen des Skripts **upgrade.sh** erfolgreich geplant hat, sendet der Client eine Statusmeldung, in der mitgeteilt wird, dass die Softwarebereitstellung erfolgreich abgeschlossen wurde. Allerdings wird die tatsächlichen Clientinstallation dann nach der Verzögerung durch den Computer verwaltet. Überprüfen Sie nach Abschluss der Clientaktualisierung die Installation, indem Sie sich die Datei **/var/opt/microsoft/scxcm.log** auf dem Clientcomputer ansehen. Darüber hinaus können Sie überprüfen, ob der Client installiert wurde und mit dem Standort kommuniziert, indem Sie die Details für den betreffenden Client unter dem Knoten **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** der Configuration Manager-Konsole anzeigen.  
