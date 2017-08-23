---
title: "Bewährte Methoden für Softwareupdates | Microsoft-Dokumentation"
description: "Verwenden Sie diese bewährten Methoden für Softwareupdates in System Center Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: 5df20f3703442de1be6220ca2770e182e330c036
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-software-updates-in-system-center-configuration-manager"></a>Bewährte Methoden für Softwareupdates in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält bewährte Methoden für Softwareupdates in System Center Configuration Manager. Diese sind nach den bewährten Methoden für die Erstinstallation und den bewährten Methoden für den laufenden Betrieb sortiert.  

## <a name="installation-best-practices"></a>Bewährte Methoden für die Installation  
 Verwenden Sie die folgenden bewährten Methoden für die Installation von Softwareupdates in Configuration Manager.  

### <a name="use-a-shared-wsus-database-for-software-update-points"></a>Verwenden einer freigegebenen WSUS-Datenbank für Softwareupdatepunkte  
 Wenn Sie an einem primären Standort mehrere Softwareupdatepunkte installieren, sollten Sie für jeden Softwareupdatepunkt einer Active Directory-Gesamtstruktur die gleiche WSUS-Datenbank verwenden. Bei Nutzung derselben Datenbank können Sie die negativen Auswirkungen auf die Client- und Netzwerkleistung, die sich ergeben können, wenn Clients zu einem neuen Softwareupdatepunkt wechseln, erheblich abmildern. Wenn ein Client zu einem neuen Softwareupdatepunkt wechselt, der eine Datenbank gemeinsam mit dem alten Softwareupdatepunkt nutzt, wird weiterhin eine Deltaüberprüfung ausgeführt. Diese Überprüfung ist jedoch weit weniger umfangreich als bei einem WSUS-Server mit eigener Datenbank.  

> [!IMPORTANT]  
>  Bei Verwendung einer freigegebenen WSUS-Datenbank für Softwareupdatepunkte müssen Sie auch die lokalen WSUS-Inhaltsordner freigeben.  

 Weitere Informationen zum Wechseln des Softwareupdatepunkts finden Sie im Abschnitt [Software update point switching (Wechseln des Softwareupdatepunkts)](../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching) im Thema [Plan for software updates in System Center Configuration Manager (Planen von Softwareupdates in Configuration Manager)](../../sum/plan-design/plan-for-software-updates.md).  

### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-of-these-to-use-a-named-instance-and-the-other-to-use-the-default-instance-of-sql-server"></a>Wenn SQL Server sowohl von Configuration Manager als auch von WSUS verwendet wird, konfigurieren Sie eines der Systeme für die Verwendung einer benannten Instanz und das andere für die Verwendung der SQL Server-Standardinstanz.  
 Wenn SQL Server und eine SQL Server-Instanz von den Configuration Manager- und WSUS-Datenbanken gemeinsam verwendet werden, lässt sich die Ressourcennutzung zwischen den beiden Anwendungen nur schwer bestimmen. Sie können Ressourcennutzungsprobleme, die mit der jeweiligen Anwendung möglicherweise auftreten, einfacher diagnostizieren und behandeln, wenn Sie unterschiedliche SQL Server-Instanzen für Configuration Manager und WSUS verwenden.  

### <a name="specify-the-store-updates-locally-setting-for-the-wsus-installation"></a>Aktivieren der Einstellung „Updates lokal speichern“ für die WSUS-Installation  
 Wählen Sie beim Installieren von WSUS die Einstellung **Updates lokal speichern** aus. Wenn diese Einstellung aktiviert ist, werden die Lizenzbedingungen für Softwareupdates während des Synchronisierungsprozesses heruntergeladen und auf der lokalen Festplatte des WSUS-Servers gespeichert. Wenn diese Einstellung nicht ausgewählt wird, kann die Kompatibilität bei Softwareupdates mit Lizenzbedingungen von den Clientcomputern möglicherweise nicht überprüft werden. Beim Installieren des Softwareupdatepunkts wird von WSUS Synchronization Manager standardmäßig alle 60 Minuten überprüft, ob diese Einstellung aktiviert ist.  

## <a name="operational-best-practices"></a>Bewährte Betriebsmethoden  
 Wenden Sie die folgenden bewährten Methoden an, wenn Sie Softwareupdates verwenden:  

### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a>Begrenzen von Softwareupdates auf 1.000 pro Softwareupdatebereitstellung  
 Sie müssen die Anzahl von Softwareupdates in einer einzelnen Softwareupdatebereitstellung auf 1.000 begrenzen. Wenn Sie eine automatische Bereitstellungsregel erstellen, achten Sie darauf, dass die von Ihnen angegebenen Kriterien nicht zu mehr als 1.000 Softwareupdates führen. Wenn Sie Softwareupdates manuell bereitstellen, wählen Sie höchstens 1.000 Updates zur Bereitstellung aus.  

### <a name="create-a-new-software-update-group-each-time-an-automatic-deployment-rule-runs-for-patch-tuesday-and-for-general-deployment"></a>Erstellen einer neuen Softwareupdategruppe bei jedem Ausführen einer automatischen Bereitstellungsregel („Patch-Dienstag“) und für allgemeine Bereitstellungen  
 Softwareupdatebereitstellungen sind auf 1.000 Softwareupdates begrenzt. Wenn Sie eine automatische Bereitstellungsregel erstellen, geben Sie an, ob bei jedem Ausführen der Regel eine vorhandene Softwareupdategruppe verwendet oder eine neue Softwareupdategruppe erstellt werden soll. Wenn Sie bestimmte Kriterien in einer automatischen Bereitstellungsregel angeben, die zu mehreren Softwareupdates führen, und die Regel nach einem wiederkehrenden Zeitplan ausgeführt wird, sollten Sie festlegen, dass bei jeder Ausführung der Regel eine neue Softwareupdategruppe erstellt wird. So wird verhindert, dass für die Bereitstellung der Grenzwert von 1.000 Softwareupdates pro Bereitstellung überschritten wird.  

### <a name="use-an-existing-software-update-group-for-automatic-deployment-rules-for-endpoint-protection-definition-updates"></a>Verwenden einer vorhandenen Softwareupdategruppe bei automatischen Bereitstellungsregeln für Endpoint Protection-Definitionsupdates  
 Verwenden Sie stets eine vorhandene Softwareupdategruppe, wenn Sie eine automatische Bereitstellungsregel verwenden, um Definitionsupdates für Endpoint Protection häufig bereitzustellen. Andernfalls werden im Laufe der Zeit möglicherweise Hunderte von Softwareupdategruppen erstellt. Normalerweise legen die Herausgeber von Definitionsupdates fest, dass diese ablaufen, wenn sie von vier neueren Updates abgelöst wurden. Daher enthält die Softwareupdategruppe, die von der automatischen Bereitstellungsregel erstellt wird, niemals mehr als vier Definitionsupdates dieses Herausgebers: ein aktives und drei abgelöste.  

## <a name="see-also"></a>Siehe auch  
 [Plan for software updates in System Center Configuration Manager (Planen von Softwareupdates in System Center Configuration Manager)](../../sum/plan-design/plan-for-software-updates.md)
