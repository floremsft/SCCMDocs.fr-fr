---
title: 'Hardwareinventur | Microsoft-Dokumentation | Linux und UNIX '
description: "Erfahren Sie, wie Sie Hardwareinventur für Linux und UNIX in System Center Configuration Manager verwenden."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
caps.latest.revision: "6"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: b6776fbe0cfca23244d767cffd554a2ef4567a2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="hardware-inventory-for-linux-and-unix-in-system-center-configuration-manager"></a>Hardwareinventur für Linux und UNIX in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Der System Center Configuration Manager-Client für Linux und UNIX unterstützt die Hardwareinventur. Nach dem Erfassen der Hardwareinventur können Sie den Bestand im Ressourcen-Explorer oder in Configuration Manager-Berichten anzeigen und diese Informationen dazu verwenden, um Abfragen und Sammlungen zu erstellen, die die folgenden Vorgänge ermöglichen:  

-   Softwarebereitstellung  

-   Erzwingen von Wartungsfenstern  

-   Bereitstellen benutzerdefinierter Clienteinstellungen  

 Bei der Hardwareinventur für Linux- und UNIX-Server wird ein standardbasierter CIM-Server (Common Information Model) verwendet. Der CIM-Server wird als Softwaredienst (oder Daemon) ausgeführt und stellt eine Verwaltungsinfrastruktur bereit, die auf DMTF-Standards (Distributed Management Task Force) basiert. Der CIM-Server bietet ähnliche Funktionen wie die CIM-Funktionen der Windows-Verwaltungsinfrastruktur (Windows Management Infrastructure, WMI), die auf Windows-basierten Computern verfügbar sind.  

 Ab dem kumulativen Update 1 verwendet der Client für Linux und UNIX die Open Source-Version von **omiserver** , Version 1.0.6, der **Open Group**. (Vor dem kumulativen Update 1 hat der Client **nanowbem** als CIM-Server verwendet).  

 Der CIM-Server wird im Rahmen des Clients für Linux und UNIX installiert. Der Client für Linux und UNIX kommuniziert direkt mit dem CIM-Server und verwendet nicht die WS-MAN-Schnittstelle des CIM-Servers. Der WS-MAN-Port auf dem CIM-Server ist deaktiviert, wenn der Client installiert wird. Microsoft hat den CIM-Server entwickelt, der jetzt über das OMI-Projekt (Open Management Infrastructure) als Open Source verfügbar ist. Weitere Informationen zum Open Management Infrastructure-Projekt finden Sie auf der [The Open Group](http://go.microsoft.com/fwlink/p/?LinkId=262317) -Website.  

 Die Hardwareinventur auf Linux- und UNIX-Servern erfolgt durch die Zuordnung von vorhandenen Win32-WMI-Klassen und -Eigenschaften zu entsprechenden Klassen und Eigenschaften für Linux- und UNIX-Server. Diese 1:1-Zuordnung von Klassen und Eigenschaften ermöglicht das Integrieren der Hardwareinventur für Linux und UNIX in Configuration Manager. Es werden Inventurdaten von Linux- und UNIX-Servern zusammen mit dem Bestand von Windows-basierten Computern in der Configuration Manager-Konsole und in Berichten angezeigt. Dadurch wird eine konsistente heterogene Verwaltung ermöglicht.  

> [!TIP]  
>  Mit dem **Beschriftung** -Wert für die **Betriebssystem** -Klasse können Sie verschiedene Linux- und UNIX-Betriebssysteme in Abfragen und Sammlungen identifizieren.  

##  <a name="BKMK_ConfigHardwareforLnU"></a> Konfigurieren der Hardwareinventur für Linux- und UNIX-Server  
 Sie können die standardmäßigen Clienteinstellungen verwenden oder benutzerdefinierte Clienteinstellungen erstellen, um die Hardwareinventur zu konfigurieren. Wenn Sie benutzerdefinierte Clientgeräteeinstellungen verwenden, können Sie die Klassen und Eigenschaften konfigurieren, die Sie nur von Ihren Linux- und UNIX-Servern erfassen möchten. Sie können auch benutzerdefinierte Zeitpläne für die Erfassung von vollständigen und Deltainventuren von Ihren Linux- und UNIX-Servern verwenden.  

 Der Client für Linux und UNIX unterstützt die folgenden Hardwareinventurklassen, die auf Linux- und UNIX-Servern verfügbar sind:  

-   Win32_BIOS  

-   Win32_ComputerSystem  

-   Win32_DiskDrive  

-   Win32_DiskPartition  

-   Win32_NetworkAdapter  

-   Win32_NetworkAdapterConfiguration  

-   Win32_OperatingSystem  

-   Win32_Process  

-   Win32_Service  

-   Win32Reg_AddRemovePrograms  

-   SMS_LogicalDisk  

-   SMS_Processor  

 Nicht alle Eigenschaften für diese Inventurklassen sind für Linux- und UNIX-Computer in Configuration Manager aktiviert.  

##  <a name="BKMK_OperationsforHardwareforLnU"></a> Vorgänge für die Hardwareinventur  
 Nachdem Sie die Hardwareinventur von den Linux- und UNIX-Servern erfasst haben, können Sie diese Informationen auf dieselbe Weise wie den Bestand anzeigen, den Sie von anderen Computern erfassen:  

-   Verwenden des Ressourcen-Explorers zum Anzeigen von detaillierten Hardwareinventurinformationen von Linux- und UNIX-Servern  

-   Erstellen von Abfragen auf Basis von bestimmten Hardwarekonfigurationen  

-   Erstellen von abfragebasierten Sammlungen, die auf bestimmten Hardwarekonfigurationen basieren  

-   Ausführen von Berichten, die bestimmte Details zu Hardwarekonfigurationen anzeigen  

 Die Hardwareinventur auf einem Linux- oder UNIX-Server wird gemäß dem Zeitplan ausgeführt, den Sie in den Clienteinstellungen konfigurieren. Diese erfolgt standardmäßig alle sieben Tage. Der Client für Linux und UNIX unterstützt sowohl vollständige Inventurzyklen als auch Deltainventurzyklen.  

 Sie können den Client auf einem Linux- oder UNIX-Server auch zwingen, die Hardwareinventur unmittelbar durchzuführen. Verwenden Sie zum Ausführen der Hardwareinventur auf einem Client die **Stamm** anmeldeinformationen, um den folgenden Befehl zum Starten eines Hardwareinventurzyklusses auszuführen: **/opt/microsoft/configmgr/bin/ccmexec -rs hinv**  

 Aktionen für die Hardwareinventur werden in die Clientprotokolldatei **scxcm.log**eingegebenen.  

##  <a name="BKMK_CustomHINVforLinux"></a> Gewusst wie: Verwenden der Open Management Infrastructure zum Erstellen einer benutzerdefinierten Hardwareinventur  
 Der Client für Linux und UNIX unterstützt die benutzerdefinierte Hardwareinventur, die Sie mithilfe der Open Management Infrastructure (OMI) erstellen können. Führen Sie dazu die folgenden Schritte aus:  

1.  Erstellen eines benutzerdefinierten Inventuranbieters mithilfe der OMI-Quelle  

2.  Konfigurieren von Computern für die Verwendung des neuen Anbieters zum Melden des Bestands  

3.  Aktivieren von Configuration Manager zur Unterstützung des neuen Anbieters  

###  <a name="BKMK_LinuxProvider"></a> Erstellen Sie einen benutzerdefinierten Hardwareinventuranbieter für Linux- und UNIX-Computer:  
 Verwenden Sie **OMI Source – v.1.0.6**, und befolgen Sie die Anweisungen im Handbuch für die ersten Schritte mit OMI, um einen benutzerdefinierten Hardwareinventuranbieter für den Configuration Manager-Client für Linux und UNIX zu erstellen. Dieser Prozess umfasst das Erstellen einer MOF-Datei (Managed Object Format), die das Schema für den neuen Anbieter definiert. Später importieren Sie die MOF-Datei in Configuration Manager, um die Unterstützung der neuen benutzerdefinierten Inventurklasse zu aktivieren.  

 Sowohl „OMI Source – v.1.0.6“ als auch das Handbuch für die ersten Schritte mit OMI können auf der [The Open Group](http://go.microsoft.com/fwlink/p/?LinkId=262317) -Website heruntergeladen werden. Sie finden diese Downloads auf der Registerkarte für **Dokumente** der folgenden Webseite der Website „OpenGroup.org“: [Open Management Infrastructure (OMI)](http://go.microsoft.com/fwlink/p/?LinkId=286805).  

###  <a name="BKMK_AddProvidertoLinux"></a> Konfigurieren Sie jeden Computer, der Linux oder UNIX ausführt, mit dem benutzerdefinierten Hardwareinventuranbieter:  
 Nachdem Sie einen benutzerdefinierten Inventuranbieter erstellt haben, müssen Sie die Anbieterbibliotheksdatei auf jeden Computer kopieren und dann registrieren, der über zu erfassendes Inventar verfügt.  

1.  Kopieren Sie die Anbieterbibliothek auf jeden Linux- und UNIX-Computer, von dem Sie Inventar erfassen möchten. Der Name des der Anbieterbibliothek ähnelt dem Folgenden: **XYZ_MyProvider.so**  

2.  Dann wird auf jedem Linux- und UNIX-Computer die Anbieterbibliothek mit dem OMI-Server registriert. Der OMI-Server wird auf dem Computer installiert, wenn Sie den Configuration Manager-Client für Linux und UNIX installieren, aber Sie müssen benutzerdefinierte Anbieter manuell registrieren. Verwenden Sie die folgende Befehlszeile zum Registrieren des Anbieters: **/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so**  

3.  Nachdem Sie den neuen Anbieter registriert haben, testen Sie den Anbieter mithilfe des **omicli** -Tools. Das **omicli**-Tool wird auf jeden Linux- und UNIX-Computer installiert, wenn Sie den Configuration Manager-Client für Linux und UNIX installieren. Führen Sie z. B. den folgenden Befehl auf dem Computer aus, wobei **XYZ_MyProvider** den Namen des erstellten Anbieters angibt: **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     Informationen zu **omicli** und zum Testen von benutzerdefinierten Anbietern finden Sie im Handbuch zu den ersten Schritten mit OMI.  

> [!TIP]  
>  Verwenden Sie die Softwareverteilung, um benutzerdefinierte Anbieter bereitzustellen und auf jedem Linux- und UNIX-Clientcomputer zu registrieren.  

###  <a name="BKMK_AddLinuxProvidertoCM"></a> Aktivieren Sie die neue Inventurklasse in Configuration Manager:  
 Bevor Configuration Manager den Bestand melden kann, der vom neuen Anbieter auf Linux- und UNIX-Computern gemeldet wird, müssen Sie die MOF-Datei (Managed Object Format) importieren, die das Schema des benutzerdefinierten Anbieters definiert.  

 Informationen zum Import einer benutzerdefinierte MOF-Datei in Configuration Manager finden Sie unter [Konfigurieren der Hardwareinventur in System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
