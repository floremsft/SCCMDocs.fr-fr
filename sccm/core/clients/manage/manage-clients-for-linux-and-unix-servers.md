---
title: Verwalten von Linux- und UNIX-Clients | Microsoft-Dokumentation
description: Verwalten Sie Clients auf Linux- und UNIX-Servern in System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 506df4f7c7baa5f0586a1ddf0cb02b3de9f4d076
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Verwalten von Clients für Linux- und UNIX-Server in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bei der Verwaltung von Linux- und UNIX-Servern mit System Center Configuration Manager können Sie Sammlungen, Wartungsfenster und Clienteinstellungen zum Verwalten der Server konfigurieren. Darüber hinaus können Sie erzwingen, dass der Client manuell die Clientrichtlinie abruft, obwohl der Configuration Manager-Client für Linux und UNIX über keine Benutzeroberfläche verfügt.

##  <a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 Sie verwenden Sammlungen, um Gruppen von Linux- und UNIX-Servern in der gleichen Weise wie andere Clienttypen zu verwalten. Sammlungen können Sammlungen mit direkter Mitgliedschaft oder abfragebasierte Sammlungen sein. Abfragebasierte Sammlungen identifizieren Clientbetriebssysteme, Hardwarekonfigurationen oder andere in der Standortdatenbank gespeicherte Details zum Client. Mit Sammlungen, die Linux- und UNIX-Server enthalten, können Sie z. B. die folgenden Einstellungen verwalten:  

-   Clienteinstellungen  

-   Softwarebereitstellungen  

-   Erzwingen von Wartungsfenstern  

 Bevor Sie einen Linux- oder UNIX-Client anhand seines Betriebssystems oder der Verteilung identifizieren können, müssen Sie die [Hardwareinventur](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md) des Clients erfassen.  

 Die standardmäßigen Clienteinstellungen für die Hardwareinventur umfassen Informationen zum Betriebssystem eines Clientcomputers. Können Sie die Eigenschaft **Caption** der Klasse **Operating System** verwenden, um das Betriebssystem eines Linux- oder UNIX-Servers zu identifizieren.  

 Details zu Computern, auf denen der Configuration Manager-Client für Linux und UNIX ausgeführt wird, können Sie unter dem Knoten **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** der Configuration Manager-Konsole anzeigen. Im Arbeitsbereich **Bestand und Kompatibilität** der Configuration Manager-Konsole wird der Name des **Betriebssystems** jedes Computers in der Spalte Betriebssystem angezeigt.  

 Linux- und UNIX-Server sind standardmäßig Mitglieder der Sammlung **Alle Systeme** . Es wird empfohlen, benutzerdefinierte Sammlungen zu erstellen, die nur Linux- und UNIX-Server oder einen Teil davon enthalten. Durch benutzerdefinierte Sammlungen können Sie Vorgänge wie das Bereitstellen von Software oder das Zuweisen von Clienteinstellungen auf Gruppen entsprechender Computer verwalten, sodass Sie den Erfolg einer Bereitstellung exakt messen können.   

 Fügen Sie beim Erstellen einer benutzerdefinierten Sammlung für Linux- und UNIX-Server Mitgliedsregelabfragen hinzu, die für das Attribut „Operating System“ das Attribut „Caption“ enthalten. Informationen zum Erstellen von Sammlungen finden Sie unter [Erstellen von Sammlungen in System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

##  <a name="BKMK_MaintenanceWindowsforLnU"></a> Maintenance windows for Linux and UNIX servers  
 Der Configuration Manager-Client für Linux- und UNIX-Server unterstützt die Verwendung von [Wartungsfenstern](../../../core/clients/manage/collections/use-maintenance-windows.md). Diese Unterstützung unterscheidet sich nicht von Windows-basierten Clients.  

##  <a name="BKMK_ClientSettingsforLnU"></a> Client settings for Linux and UNIX servers  
 Sie können [Clienteinstellungen](../../../core/clients/deploy/configure-client-settings.md) für Linux- und UNIX-Server auf die gleiche Weise wie Einstellungen für andere Clients konfigurieren.  

 Standardmäßig gelten die **Client-Agent-Standardeinstellungen** für Linux- und UNIX-Server. Sie können auch benutzerdefinierte Clienteinstellungen erstellen und für Sammlungen von bestimmten Clients bereitstellen.  

 Es gibt keine zusätzlichen Clienteinstellungen, die nur für Linux- und UNIX-Clients gelten. Es gibt jedoch Standardclienteinstellungen, die auf Linux- und UNIX-Clients nicht anwendbar sind. Der Client für Linux und UNIX wendet Einstellungen nur für die von ihm unterstützten Funktionen an.  

 Eine benutzerdefinierte Geräteclienteinstellung, mit der Remotesteuerungseinstellungen aktiviert und konfiguriert werden, wird von den Linux- und UNIX-Servern beispielsweise ignoriert, da der Client für Linux und UNIX die Remotesteuerung nicht unterstützt.  

##  <a name="BKMK_PolicyforLnU"></a> Computer policy for Linux and UNIX servers  
 Der Client für Linux- und UNIX-Server fragt den Standort in regelmäßigen Abständen nach Computerrichtlinien ab, um angeforderte Konfigurationen zu ermitteln und nach Bereitstellungen zu suchen.  

 Sie können auch erzwingen, dass der Client auf einem Linux- oder UNIX-Server Computerrichtlinien sofort abruft. Verwenden Sie hierzu auf dem Server **Stammanmeldedaten** zum Ausführen des folgenden Befehls: **/opt/microsoft/configmgr/bin/ccmexec -rs policy**  

 Details zum Computerrichtlinienabruf werden in die freigegebene Clientprotokolldatei, **scxcm.log**, geschrieben.  

> [!NOTE]  
>  Der Configuration Manager-Client für Linux und UNIX fordert nie Benutzerrichtlinien an und verarbeitet diese nie.  

##  <a name="BKMK_ManageLinuxCerts"></a> How to manage certificates on the client for Linux and UNIX  
 Nach der Installation des Clients für Linux und UNIX können Sie das **certutil** -Tool zum Aktualisieren des Clients mit einem neuen PKI-Zertifikat und zum Importieren einer neuen Zertifikatsperrliste (CRL) verwenden. Bei der Installation des Clients für Linux und UNIX befindet sich dieses Tool im Verzeichnis **/opt/microsoft/configmgr/bin/certutil**. 

 Führen Sie zum Verwalten von Zertifikaten auf jedem Client das certutil-Tool mit einer der folgenden Optionen aus:  

|Option|Weitere Informationen|  
|------------|----------------------|  
|importPFX|Verwenden Sie diese Option, um ein Zertifikat anzugeben, mit dem das derzeit von einem Client verwendete Zertifikat ersetzt werden soll.<br /><br /> Bei Verwendung von **-importPFX** müssen Sie außerdem den **–password**-Befehlszeilenparameter verwenden, um das der PKCS#12-Datei zugeordnete Kennwort anzugeben.<br /><br /> Verwenden Sie **-rootcerts** , um mögliche weitere Anforderungen an das Stammzertifikat anzugeben.<br /><br /> Beispiel: **certutil -importPFX &lt; Pfad zum PKCS#12-Zertifikat > -password &lt;Zertifikatkennwort\> [-rootcerts &lt;durch Komma getrennte Liste der Zertifikate>]**|  
|-importsitecert|Verwenden Sie diese Option, um das Standortserver-Signaturzertifikat auf dem Verwaltungsserver zu aktualisieren.<br /><br /> Beispiel: **certutil -importsitecert &lt;Pfad zum DER-Zertifikat\>**|  
|-importcrl|Verwenden Sie diese Option, um die Zertifikatsperrliste (CRL) auf dem Client mit einem oder mehreren CRL-Dateipfaden zu aktualisieren.<br /><br /> Beispiel: **certutil -importcrl &lt;durch Kommas getrennte CRL-Dateipfade\>**|  
