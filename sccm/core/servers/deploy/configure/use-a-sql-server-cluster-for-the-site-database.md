---
title: SQL Server-Cluster | Microsoft-Dokumentation
description: "Hosten Sie mithilfe eines SQL Server-Clusters die Standortdatenbank von System Center Configuration Manager. Enthält Informationen zu unterstützten Optionen."
ms.custom: na
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 53f119bbb1f8827a9c23c8b747840350bbb92790
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="use-a-sql-server-cluster-for-the-system-center-configuration-manager-site-database"></a>Verwenden eines SQL Server-Clusters für die Standortdatenbank von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


 Sie können mithilfe eines SQL Server-Clusters die Standortdatenbank von System Center Configuration Manager verwalten. Die Standortdatenbank wird als einzige Standortsystemrolle in einem Servercluster unterstützt.  

> [!IMPORTANT]  
>  Erfolgreiche Einrichtung von SQL Server-Clustern beruht auf Dokumentation und Verfahren in der SQL Server-Dokumentationsbibliothek.  

 Ein Cluster kann Failoverunterstützung ermöglichen und die Zuverlässigkeit der Standortdatenbank verbessern. Er bietet allerdings keine zusätzlichen Vorteile in puncto Verarbeitung oder Lastenausgleich. Die Leistung kann sogar beeinträchtigt werden, da der Standortserver den aktiven Knoten des SQL Server-Clusters suchen muss, bevor eine Verbindung mit der Standortdatenbank hergestellt werden kann.  

 Bevor Sie Configuration Manager installieren, müssen Sie den SQL Server-Cluster so konfigurieren, dass er Configuration Manager unterstützt. (Siehe die Voraussetzungen weiter unten in diesem Abschnitt.)  

 Beim Configuration Manager-Setup wird der Windows VSS Writer auf jedem physischen Computerknoten des Microsoft Windows Server-Clusters installiert. Dies unterstützt die Wartungsaufgabe **Standortserver sichern**.  

 Nach der Installation des Standorts überprüft Configuration Manager den Clusterknoten stündlich auf Änderungen. Configuration Manager verwaltet automatisch alle gefundenen Änderungen, die sich auf die Installation von Configuration Manager-Komponenten auswirken (wie z.B. ein Knotenfailover oder das Hinzufügen eines neuen Knotens zum SQL Server-Cluster).  

## <a name="supported-options-for-using-a-sql-server-failover-cluster"></a>Unterstützte Optionen für das Verwenden eines SQL Server-Failoverclusters

Die folgenden Optionen werden für SQL Server-Failovercluster unterstützt, die als Standortdatenbank verwendet werden:

-   Cluster mit Einzelinstanz  

-   Konfiguration mit mehreren Instanzen  

-   Mehrere aktive Knoten  

-   Sowohl eine benannte als auch eine Standardinstanz  

Beachten Sie die folgenden Voraussetzungen:  

-   Die Standortdatenbank muss remote vom Standortserver installiert werden. (Der Cluster kann nicht den Standortsystemserver enthalten.)  

-   Sie müssen der Gruppe „Lokale Administratoren“ jedes Servers im Cluster das Computerkonto des Standortservers hinzufügen.  

-   Zur Unterstützung der Kerberos-Authentifizierung muss das Netzwerkkommunikationsprotokoll **TCP/IP** für die Netzwerkverbindung jedes SQL Server-Clusterknotens aktiviert sein. **Named Pipes** ist nicht erforderlich, kann jedoch zur Behandlung von Problemen bei der Kerberos-Authentifizierung verwendet werden. Die Netzwerkprotokolleinstellungen werden im **SQL Server-Konfigurations-Manager** unter **SQL Server-Netzwerkkonfiguration** konfiguriert.  

-   Wenn Sie eine PKI nutzen und für die Standortdatenbank einen SQL Server-Cluster verwenden, finden Sie Informationen zu spezifischen Zertifikatanforderungen unter „PKI-Zertifikatanforderungen für Configuration Manager“.  

Beachten Sie die folgenden Einschränkungen:  

-   **Installation und Konfiguration:**  

    -   Sekundäre Standorte können keinen SQL Server-Cluster verwenden.  

    -   Die Option zur Angabe nicht standardmäßiger Dateispeicherorte für die Standortdatenbank ist nicht verfügbar, wenn Sie einen SQL Server-Cluster angeben.  

-   **SMS-Anbieter:**  

    -   Die Installation einer Instanz des SMS-Anbieters in einem SQL Server-Cluster oder auf einem Computer, der als gruppierter SQL Server-Knoten ausgeführt wird, wird nicht unterstützt.  

-   **Optionen für die Replikation von Daten:**  

    -   Wenn Sie **Verteilte Ansichten**verwenden, können Sie zum Hosten der Standortdatenbank keinen SQL Server-Cluster verwenden.  

-   **Sicherung und Wiederherstellung:**  

    -   Configuration Manager unterstützt nicht die Data Protection Manager (DPM)-Sicherung für einen SQL Server-Cluster, der eine benannte Instanz verwendet. Er unterstützt jedoch die DPM-Sicherung auf einem SQL Server-Cluster, der die Standardinstanz von SQL Server verwendet.  

## <a name="prepare-a-clustered-sql-server-instance-for-the-site-database"></a>So bereiten Sie eine gruppierte SQL Server-Instanz als Standortdatenbank vor  

Hier die wichtigsten Aufgaben, um die Standortdatenbank vorzubereiten:

-   Erstellen Sie den virtuellen SQL Server-Cluster, der die Standortdatenbank hosten soll, in einer vorhandenen Windows Server-Clusterumgebung. Spezifische Informationen zum Installieren und Konfigurieren eines SQL Server-Clusters finden Sie in der Dokumentation zu Ihrer SQL Server-Version. Wenn Sie beispielsweise SQL Server 2008 R2 verwenden, lesen Sie [Installieren eines SQL Server 2008 R2-Failoverclusters](http://go.microsoft.com/fwlink/p/?LinkId=240231).  

-   Sie können bei jedem Computer im SQL Server-Cluster eine Datei im Stammordner jedes Laufwerks ablegen, auf dem Configuration Manager keine Standortkomponenten installieren soll. Die Datei sollte **NO_SMS_ON_DRIVE.SMS** genannt werden. Standardmäßig installiert Configuration Manager an jedem physischen Knoten einige Komponenten, um Vorgänge wie Sicherungen zu unterstützen.  

-   Fügen Sie der Gruppe **Lokale Administratoren** jedes Windows Server-Clusterknotencomputers das Computerkonto des Standortservers hinzu.  

-   Weisen Sie in der virtuellen SQL Server-Instanz dem Benutzerkonto, das das Configuration Manager-Setup ausführt, die SQL Server-Rolle **sysadmin** zu.  

### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>So installieren Sie einen neuen Standort mithilfe eines SQL Server-Clusters  
 Führen Sie zum Installieren eines Standorts, der eine gruppierte Standortdatenbank verwendet, das Configuration Manager-Setup gemäß Ihrem normalen Prozess für die Installation eines Standorts mit der folgenden Änderung durch:  

-   Geben Sie auf der Seite **Datenbankinformationen** den Namen der virtuellen SQL Server-Clusterinstanz an, von der die Standortdatenbank gehostet wird. Die virtuelle Instanz ersetzt den Namen des Computers, auf dem SQL Server ausgeführt wird.  

    > [!IMPORTANT]  
    >  Wenn Sie den Namen der virtuellen SQL Server-Clusterinstanz eingeben, geben Sie nicht den vom Windows Server-Cluster erstellten virtuellen Windows Server-Namen ein. Wenn Sie den virtuellen Windows Server-Namen verwenden, wird die Standortdatenbank auf der lokalen Festplatte des aktiven Windows Server-Clusterknotens installiert. Dies verhindert ein erfolgreiches Failover, sollte der Knoten ausfallen.  
