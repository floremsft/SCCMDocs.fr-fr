---
title: Endpoint Protection | Microsoft Docs
description: "Erfahren Sie, wie Sie Richtlinien für Antischadsoftware und die Sicherheit der Windows-Firewall für Clientcomputer in der Configuration Manager-Hierarchie verwalten."
ms.custom: na
ms.date: 02/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
caps.latest.revision: "11"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 3c31271f3e3ae7aa45da03b3d75fd78242330646
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="endpoint-protection"></a>Endpoint Protection

*Gilt für: System Center Configuration Manager (Current Branch)*

Mithilfe von Endpoint Protection in System Center Configuration Manager können Sie Richtlinien für Antischadsoftware und die Sicherheit der Windows-Firewall für Clientcomputer in Ihrer Configuration Manager-Hierarchie verwalten.  

> [!IMPORTANT]  
>  Sie benötigen eine Lizenz für die Verwendung von Endpoint Protection, damit Sie Clients in der Configuration Manager-Hierarchie verwalten können.  

 Bei der Verwendung von Endpoint Protection mit Configuration Manager ergeben sich für Sie die folgenden Vorteile:  

-   Sie können Antischadsoftware-Richtlinien und Windows-Firewall-Einstellungen erstellen und Windows Defender Advanced Threat Protection für ausgewählte Computergruppen verwalten.  
-   Sie können mit Configuration Manager-Softwareupdates die neuesten Definitionsdateien für Antischadsoftware herunterladen, um Clientcomputer auf dem neuesten Stand zu halten.  
-   Sie können E-Mail-Benachrichtigungen senden, die Überwachung in der Konsole nutzen und Berichte anzeigen, damit Administratoren über erkannte Schadsoftware auf Clientcomputern informiert werden.  

Ab Windows 10 und Windows Server 2016 ist Windows Defender bereits auf den Computern installiert. Bei diesen Betriebssystemen wird bei der Installation des Configuration Manager-Clients ein Verwaltungsclient für Windows Defender installiert. Auf Computern unter Windows 8.1 und früher wird mit dem Configuration Manager-Client auch der Endpoint Protection-Client installiert. Windows Defender und der Endpoint Protection-Client verfügt über folgende Funktionen:  

-   Erkennung von Schadsoftware und Spyware sowie Wiederherstellung  
-   Erkennung von Rootkits und Wiederherstellung  
-   Bewertung kritischer Sicherheitsrisikos und automatische Definitions- und Modulupdates  
-   Erkennung von Sicherheitslücken im Netzwerk über das Netzwerkinspektionssystem  
-   Integration mit Cloud Protection Service, um Microsoft Schadsoftware zu melden. Wenn Sie diesem Dienst beitreten, können vom Endpoint Protection-Client oder Windows Defender die neuesten Definitionen aus dem Microsoft Center zum Schutz vor Malware heruntergeladen werden, sobald nicht identifizierte Schadsoftware auf einem Computer erkannt wird.  

> [!NOTE]  
>  Der Endpoint Protection-Client kann auf einem Server, auf dem Hyper-V ausgeführt wird, sowie auf virtuellen Gastcomputern mit unterstützten Betriebssystemen installiert werden. Endpoint Protection-Aktionen weisen eine integrierte, zufällige Verzögerung auf, damit Schutzdienste nicht gleichzeitig ausgeführt werden und somit eine übermäßige CPU-Auslastung verhindert wird.  

 Darüber hinaus können Sie Endpoint Protection in Configuration Manager zum Verwalten von Windows-Firewalleinstellungen in der Configuration Manager-Konsole nutzen.  

 [Beispielszenario: Verwenden von System Center Endpoint Protection zum Schutz von Computern vor Schadsoftware in System Center Configuration Manager](scenarios-endpoint-protection.md) Endpoint Protection und Windows-Firewall  


## <a name="managing-malware-with-endpoint-protection"></a>Verwalten von Schadsoftware mit Endpoint Protection  
 Mit Endpoint Protection in Configuration Manager können Sie Antischadsoftware-Richtlinien erstellen, in denen Einstellungen für Endpoint Protection-Clientkonfigurationen enthalten sind. Sie können diese Antischadsoftware-Richtlinien auf Clientcomputern bereitstellen und sie im Knoten **Endpoint Protection-Status** unter **Sicherheit** im Arbeitsbereich **Überwachung** oder mithilfe von Configuration Manager-Berichten überwachen.  

 Weitere Informationen:  

-   [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md) ‒ Erstellen, Bereitstellen und Überwachen von Richtlinien für Antischadsoftware mit einer Liste der Einstellungen, die Sie konfigurieren können  

-   [Überwachen von Endpoint Protection in System Center Configuration Manager](monitor-endpoint-protection.md) ‒ Überwachen von Aktivitätsberichten, infizierten Clientcomputern und mehr  

-   [Verwalten von Richtlinien für Antischadsoftware und Firewalleinstellungen für Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-firewall.md) ‒ Auf Clientcomputern gefundene Antischadsoftware korrigieren  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Verwalten der Windows-Firewall mit Endpoint Protection  
 Durch Endpoint Protection in Configuration Manager verfügen Sie über eine grundlegende Verwaltung der Windows-Firewall auf Clientcomputern. Für jedes Netzwerkprofil können Sie die folgenden Einstellungen konfigurieren:  

-   Aktivieren oder Deaktivieren der Windows-Firewall  

-   Blockieren eingehender Verbindungen, einschließlich der in der Liste der zugelassenen Programme aufgeführten Verbindungen  

-   Benachrichtigen des Benutzers, wenn ein neues Programm von der Windows-Firewall blockiert wird  

> [!NOTE]  
>  Von Endpoint Protection wird nur die Verwaltung der Windows-Firewall unterstützt.  


 Weitere Informationen zur Erstellung und Bereitstellung von Windows-Firewallrichtlinien für Endpoint Protection finden Sie unter [Erstellen und Bereitstellen von Windows-Firewallrichtlinien für Endpoint Protection in System Center Configuration Manager](create-windows-firewall-policies.md).  


## <a name="windows-defender-advanced-threat-protection"></a>Windows Defender Advanced Threat Protection

Ab Version 1606 von Configuration Manager (Current Branch) kann Endpoint Protection Windows Defender Advanced Threat Protection (ATP) verwalten und überwachen. Windows Defender ATP ist ein neuer Dienst, der Unternehmen dabei unterstützt, erweiterte Angriffe auf ihre Netzwerke zu entdecken, zu untersuchen, und darauf zu reagieren. Informationen hierzu finden Sie unter [Windows Defender Advanced Threat Protection](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Endpoint Protection-Workflow  
 Das folgende Diagramm bringt Ihnen den Workflow zur Implementierung von Endpoint Protection in Ihrer Configuration Manager-Hierarchie näher.  

 ![Endpoint Protection-Workflow](../media/Endpoint-Protection-Workflow.gif)  

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Endpoint Protection-Client für Macintosh-Computer und Linux-Server  
 System Center Endpoint Protection umfasst einen Endpoint Protection-Client für Linux- und Macintosh-Computer. Diese Clients sind nicht im Lieferumfang von Configuration Manager enthalten. Stattdessen müssen Sie die folgenden Produkte aus dem [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx) herunterladen.  

-   System Center 2012 Endpoint Protection für den Macintosh  

-   System Center 2012 Endpoint Protection für Linux  


> [!IMPORTANT]  
>  Sie müssen ein Microsoft-Volumenlizenz-Kunde sein, damit Sie die Endpoint Protection-Installationsdateien für Linux und den Macintosh herunterladen können.  

 Diese Produkte können nicht über die Configuration Manager-Konsole verwaltet werden. Allerdings wird mit den Installationsdateien ein System Center Operations Manager-Management Pack bereitgestellt, das es Ihnen ermöglicht, den Client für Linux mit Operations Manager zu verwalten.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Abrufen des Endpoint Protection-Clients für Macintosh-Computer und Linux-Server

Gehen Sie folgendermaßen vor, um die Imagedatei mit der Endpoint Protection-Clientsoftware und Dokumentation für Macintosh-Computer und Linux-Server herunterzuladen.
1. Melden Sie sich im [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx) an.
2. Wählen Sie die Registerkarte **Downloads and Keys** (Downloads und Schlüssel) oben auf der Website aus.
3. Filtern Sie nach dem Produkt **System Center Endpoint Protection (Current Branch)**.
4. Klicken Sie auf den Link **Herunterladen**.
5. Klicken Sie auf **Continue**(Weiter). Es sollten mehrere Dateien angezeigt werden, einschließlich eine namens **System Center Endpoint Protection (current branch - version 1606) for Linux OS and Macintosh OS Multilanguage   32/64 bit   1507 MB ISO** (System Center Endpoint Protection (Current Branch –Version 1606) für das Linux- und Macintosh-Betriebssystem Mehrsprachig 32/64 bit 1507 MB ISO).
6. Klicken Sie auf das Pfeilsymbol, um die Datei herunterzuladen. Der Dateiname lautet **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_EptProt_Lin_Mac_MLF_X21-30777.ISO**.

 Weitere Informationen zum Installieren und Verwalten von Endpoint Protection-Clients für Linux und Macintosh-Computer finden Sie in der Dokumentation des jeweiligen Produkts im Ordner **Documentation** .
