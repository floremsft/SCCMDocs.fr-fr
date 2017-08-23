---
title: "Änderungen gegenüber Configuration Manager 2012 | Microsoft-Dokumentation "
description: "Identifizieren Sie die Änderungen und neuen Funktionen in System Center Configuration Manager im Vergleich zu System Center 2012 Configuration Manager."
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
caps.latest.revision: "51"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0a3eb93a99533a1569d8f72ca01d6dfcdc75da20
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="what39s-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>Änderungen in System Center Configuration Manager im Vergleich zu System Center 2012 Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


 System Center Configuration Manager Current Branch bringt wichtige Änderungen von System Center 2012 Configuration Manager mit sich. In diesem Thema werden die wichtigsten Änderungen und neue Funktionen in der Baselineversion 1511 von System Center Configuration Manager beschrieben. Informationen zu Änderungen, die in nachfolgenden Updates für System Center Configuration Manager eingeführt werden, finden Sie unter [Neuerungen in inkrementellen Versionen von System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).



 Das Release vom Dezember 2015 von System Center Configuration Manager (Version 1511) war die erste Veröffentlichung von Configuration Manager von Microsoft. Er wird in der Regel als System Center Configuration Manager (Current Branch) bezeichnet. *Current Branch* bedeutet, dass es sich um eine Version handelt, die inkrementelle Updates des Produkts unterstützt. Sie bietet auch die Möglichkeit, zwischen diesem Release und früheren Releases von Configuration Manager zu unterscheiden.  

 System Center Configuration Manager:  

-   Im Produktnamen wird, anders als bei früheren Versionen wie Configuration Manager 2007 oder System Center 2012 Configuration Manager, kein Jahr und keine Produkt-ID verwendet.

-   Inkrementelle produktinterne Updates, sogenannte Updateversionen werden unterstützt. Das erste Release war Version 1511. Nachfolgende Versionen werden mehrmals im Jahr als konsoleninterne Updates veröffentlicht, z.B. Version 1610.
-   Wird mithilfe einer Baselineversion installiert. Während 1511 die ursprüngliche Baselineversion war, werden neue Baselineversionen auch von Zeit zu Zeit veröffentlicht, wie z.B. 1702. Baselineversionen können zur Installation eines neuen System Center Configuration Manager-Standorts und einer neuen Hierarchie oder zum Upgrade von einer unterstützten Version von Configuration Manager 2012 verwendet werden.




##  <a name="bkmk_updates"></a> Konsoleninterne Updates für Configuration Manager  
 System Center Configuration Manager verwendet eine konsoleninterne Wartungsmethode namens **Updates und Wartung**, mit der Sie empfohlene Updates leicht finden und installieren können.  

 Einige Versionen stehen nur als Updates für vorhandene Standorte (innerhalb der Configuration Manager-Konsole) zur Verfügung und können nicht zur Installation neuer Configuration Manager-Standorte verwendet werden.   
Das Update 1610 beispielsweise ist nur in der Configuration Manager-Konsole verfügbar. Es wird verwendet, um einen Standort zu aktualisieren, der bereits eine Version von System Center Configuration Manager ausführt.

Eine Updateversion wird in regelmäßigen Abständen als neue Baselineversion (z.B. Update 1702) veröffentlicht. Diese Art von Update kann zur Installation einer neuen Hierarchie verwendet werden, sodass Sie nicht mit einer älteren Baselineversion (z.B. 1511) beginnen und viele Upgrades bis hin zur neuesten Version durchführen müssen.


Weitere Informationen zum Verwenden von Updates finden Sie unter [Updates für System Center Configuration Manager](../../../core/servers/manage/updates.md).  
Weitere Informationen zu Baselines finden Sie in den Abschnitten zu [Basis- und Updateversionen](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions).

##  <a name="bkmk_servicepoint"></a> Neue Standortsystemrolle: Dienstverbindungspunkt  
 Der **Microsoft Intune-Connector** wird durch eine neue Standortsystemrolle ersetzt, die zusätzliche Funktionalität ermöglicht, den **Dienstverbindungspunkt**. Aufgaben des Dienstverbindungspunkts:  

-   Ersetzt den Microsoft Intune-Connector, wenn Sie Intune in die lokale Verwaltung mobiler Geräte von System Center Configuration Manager integrieren.  

-   Dient als Kontaktpunkt für Geräte, die Sie verwalten.  

-   Lädt Nutzungsdaten zu Ihrer Bereitstellung in den Microsoft-Clouddienst hoch.  

-   Macht Updates, die für Ihre Bereitstellung gelten, innerhalb der Configuration Manager-Konsole verfügbar.  

Diese Standortsystemrolle unterstützt sowohl Online- als auch Offline-Betriebsmodi. Weitere Informationen finden Sie unter [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

##  <a name="bkmk_usage"></a> Sammeln von Verwendungsdaten  
 System Center Configuration Manager sammelt Nutzungsdaten zu Ihren Standorten und Ihrer Infrastruktur. Der Dienstverbindungspunkt sammelt diese Informationen und übermittelt sie an den Microsoft-Clouddienst. Configuration Manager muss aktiviert werden, damit Updates für Ihre Bereitstellung heruntergeladen werden, die für die von Ihnen verwendete Version von Configuration Manager gelten. Wenn Sie den Dienstverbindungspunkt einrichten, können Sie Folgendes angeben: Die Ebene der Daten, die gesammelt werden, und ob diese Daten automatisch (Onlinemodus) oder manuell (Offlinemodus) übermittelt werden.  

 Weitere Informationen finden Sie unter [Ebenen und Einstellungen für Nutzungsdaten](../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

##  <a name="bkmk_AMT"></a> Unterstützung für Intel Active Management Technology (AMT)  
 Mit System Center Configuration Manager wurde der native Support für AMT-basierte Computer in der Configuration Manager-Konsole entfernt. AMT-basierte Computer werden weiterhin vollständig verwaltet, wenn Sie das [Intel SCS-Add-On für Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html) verwenden. Über das Add-On haben Sie Zugriff auf die neuesten AMT-Verwaltungsfunktionen. Gleichzeitig werden die Beschränkungen aufgehoben, die vor der Einbindung dieser Änderungen durch Configuration Manager eingeführt wurden.  

Das Entfernen integrierter AMT für System Center Configuration Manager umfasst die Out-of-Band-Verwaltung. Die Standortsystemrolle des Out-of-Band-Verwaltungspunkts wird nicht mehr verwendet und ist nicht mehr verfügbar.  

Beachten Sie, dass die Out-of-Band-Verwaltung in System Center 2012 Configuration Manager von dieser Änderung nicht betroffen ist.

##  <a name="bkmk_out"></a> Veraltete Funktionalität  
 Einige Funktionen, wie z.B. native auf [Unterstützung für Intel Active Management Technology (AMT)](#bkmk_AMT)-basierende Computer, wurden über die Configuration Manager-Konsole entfernt. Andere Funktionen, wie der Netzwerkzugriffsschutz, wurden vollständig entfernt. Darüber hinaus werden einige ältere Microsoft-Produkte wie Windows Vista, Windows Server 2008 und SQL Server 2008 nicht mehr unterstützt.  

 Eine Liste der veralteten Features finden Sie unter [Entfernte und veraltete Features für System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

 Details zu unterstützten Produkten, Betriebssystemen und Konfigurationen finden Sie unter [Unterstützte Konfigurationen für System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md).  

## <a name="client-deployment"></a>Clientbereitstellung  
 System Center Configuration Manager führt eine neue Funktion zum Testen neuer Versionen des Configuration Manager-Clients ein, bevor der Rest des Standorts mit der neuen Software aktualisiert wird. Sie können eine Präproduktionssammlung einrichten, in der ein neuer Client als Pilot getestet wird. Sobald Sie mit der neuen Clientsoftware in der Präproduktion zufrieden sind, können Sie den Client heraufstufen, um den Rest des Standorts mit der neuen Version zu aktualisieren.  

 Weitere Informationen zum Testen von Clients finden Sie unter [Testen von Clientupgrades in einer Präproduktionssammlung in System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

## <a name="operating-system-deployment"></a>Betriebssystembereitstellung  

Beachten Sie die folgenden Änderungen der Betriebssystembereitstellung:

-   Im Tasksequenzerstellungs-Assistenten, **Upgrade an operating system from upgrade package** (Durchführen eines Upgrades für ein Betriebssystem mit einem Upgradepaket), ist ein neuer Tasksequenztyp verfügbar. Er erstellt die Schritte für das Upgrade von Computern von Windows 7, Windows 8 oder Windows 8.1 auf Windows 10. Weitere Informationen finden Sie unter [Upgrade Windows to the latest version with System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Der Windows PE-Peercache ist jetzt verfügbar, wenn Sie Betriebssysteme bereitstellen. Computer, auf denen eine Tasksequenz zum Bereitstellen eines Betriebssystems ausgeführt wird, können mithilfe des Windows PE-Peercaches Inhalte von einem lokalen Peer (einer Peercachequelle) abrufen, anstatt sie von einem Verteilungspunkt herunterzuladen. Auf diese Weise können Sie WAN-Datenverkehr in Zweigstellenszenarios minimieren, wenn kein lokaler Verteilungspunkt vorhanden ist. Weitere Informationen finden Sie unter [Prepare Windows PE peer cache to reduce WAN traffic in System Center Configuration Manager](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).  

-   Sie können nun den Zustand von Windows as a Service in Ihrer Umgebung anzeigen. Sie können auch Wartungspläne erstellen, um Bereitstellungsringe zu bilden und sicherzustellen, dass Windows 10 Current Branch-Computer auf dem neuesten Stand gehalten werden, wenn neue Builds veröffentlicht werden. Darüber hinaus können Sie Warnungen anzeigen, wenn sich Windows 10-Clients dem Ende des Supports für ihren Build von Current Branch (CB) oder Current Branch for Business (CBB) nähern. Weitere Informationen finden Sie unter [Manage Windows as a service using System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

## <a name="application-management"></a>Anwendungsverwaltung  

Beachten Sie die folgenden Änderungen der Anwendungsverwaltung:

-   System Center Configuration Manager ermöglicht Ihnen das Bereitstellen von UWP-Apps (universelle Windows-Plattform) für Geräte mit Windows 10 und höher. Informationen finden Sie unter [Erstellen von Windows-Anwendungen mit System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Das Softwarecenter weist einen neuen, modernen Look auf. Apps, die bisher nur im Anwendungskatalog angezeigt wurden (für Benutzer verfügbare Apps), werden jetzt im Softwarecenter auf der Registerkarte „Anwendungen“ angezeigt. Dadurch sind diese Bereitstellungen leichter auffindbar, und Benutzer müssen nicht auf den Anwendungskatalog verweisen. Außerdem ist kein Browser mit Silverlight-Unterstützung mehr erforderlich. Informationen finden Sie unter [Planen und Konfigurieren der Anwendungsverwaltung in System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   Mit dem neuen Anwendungstyp „Windows Installer über MDM“ können Sie Windows Installer-basierte Apps auf registrierten PCs unter Windows 10 erstellen und bereitstellen. Informationen finden Sie unter [Erstellen von Windows-Anwendungen mit System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Wenn Sie eine Anwendung für eine unternehmensinterne iOS-App entwickeln, müssen Sie nur die Installationsdatei (.ipa) für die App angeben. Sie müssen nicht mehr eine entsprechende Eigenschaftenlistendatei (.plist) angeben. Informationen finden Sie unter [Erstellen von iOS-Anwendungen mit System Center Configuration Manager](../../../apps/get-started/creating-ios-applications.md).  

-   Um in Configuration Manager 2012 einen Link zu einer App im Windows Store anzugeben, können Sie entweder den Link direkt angeben oder zu einem Remotecomputer navigieren, auf dem die App installiert ist. In System Center Configuration Manager können Sie weiterhin den Link direkt eingeben. Doch anstatt zu einem Referenzcomputer zu navigieren, können Sie in der Configuration Manager-Konsole den Store direkt nach der App durchsuchen.  

## <a name="software-updates"></a>Softwareupdates  

Beachten Sie die folgenden Änderungen von Softwareupdates:

-   System Center Configuration Manager kann nun den Unterschied zwischen Methoden der Softwareupdateverwaltung für Computer erkennen. Insbesondere kann System Center Configuration Manager jetzt einen Computer mit Windows 10, der sich für die Verwaltung von Softwareupdates mit Windows Update for Business (WUfB) verbindet, von einem Computer unterscheiden, der für die Verwaltung von Softwareupdates mit Windows Server Update Services (WSUS) verbunden ist. Das **UseWUServer**-Attribut ist neu und gibt an, ob der Computer mit WUfB verwaltet wird. Sie können diese Einstellung in einer Sammlung verwenden, um diese Computer aus der Verwaltung von Softwareupdates zu entfernen. Weitere Informationen finden Sie unter [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   Jetzt können Sie den WSUS-Bereinigungstask von der Configuration Manager-Konsole aus planen und ausführen. Wenn Sie in den Eigenschaften von **Softwareupdatepunkt-Komponente** die Ausführung der WSUS-Bereinigungsaufgabe auswählen, wird sie bei der nächsten Softwareupdatesynchronisierung ausgeführt. Die abgelaufenen Softwareupdates werden auf dem WSUS-Server auf den Status „Abgelehnt“ festgelegt, und der Windows Update-Agent auf Computern durchsucht diese Softwareupdates daraufhin nicht mehr. Weitere Informationen finden Sie unter [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md).  

## <a name="compliance-settings"></a>Kompatibilitätseinstellungen  

Beachten Sie die folgenden Änderungen von Konformitätseinstellungen:

-   System Center Configuration Manager verbessert den Workflow zum Erstellen von Konfigurationselementen. Wenn Sie jetzt ein Konfigurationselement erstellen und unterstützte Plattformen auswählen, sind nur die für die Plattform relevanten Einstellungen verfügbar. Informationen finden Sie unter [Erste Schritte mit Kompatibilitätseinstellungen in System Center Configuration Manager](../../../compliance/get-started/get-started-with-compliance-settings.md).  

-   Der **Assistent zum Erstellen von Konfigurationselementen** erleichtert die Auswahl des Konfigurationselementtyps, den Sie erstellen möchten. Darüber hinaus sind neue und aktualisierte Konfigurationselemente für Folgendes verfügbar:  

    -   Mit dem Configuration Manager-Client verwaltete Windows 10-Geräte  

    -   Mit dem Configuration Manager-Client verwaltete Max OS X-Geräte  

    -   Mit dem Configuration Manager-Client verwaltete Windows Desktop- und Servercomputer  

    -   Ohne den Configuration Manager-Client verwaltete Windows 8.1- und Windows 10-Geräte  

    -   Ohne den Configuration Manager-Client verwaltete Windows Phone-Geräte  

    -   Ohne den Configuration Manager-Client verwaltete iOS- und Mac OS X-Geräte  

    -   Ohne den Configuration Manager-Client verwaltete Android- und Samsung KNOX Standard-Geräte  

 Informationen finden Sie unter [Erstellen von Konfigurationselementen in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items.md).  

-   Unterstützung für die Verwaltung von Einstellungen auf Mac OS X-Computern, die entweder mit Microsoft Intune registriert oder mithilfe des Configuration Manager-Clients verwaltet werden. Informationen finden Sie unter [Erstellen von Konfigurationselementen für iOS- und Mac OS X-Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden](../../../compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md).  

## <a name="protect-data-and-site-infrastructure"></a>Schützen der Daten und Standortinfrastruktur  
Mit System Center Configuration Manager können Sie die Integration in Windows Hello for Business (früher Microsoft Passport für Windows) durchführen. Windows Hello for Business ist eine alternative Anmeldemethode, die Active Directory oder ein Azure Active Directory-Konto verwendet, um ein Kennwort, eine Smartcard oder eine virtuelle Smartcard auf Geräten mit Windows 10 zu ersetzen. Informationen finden Sie unter [Windows Hello for Business-Einstellungen in System Center Configuration Manager](../../../protect/deploy-use/windows-hello-for-business-settings.md).

## <a name="mobile-device-management-with-microsoft-intune"></a>Verwaltung mobiler Geräte mit Microsoft Intune  
 System Center Configuration Manager bietet Verbesserungen an der Umgebung zur Verwaltung mobiler Geräte, wie z.B.:  

-   Festlegen der Begrenzung der Anzahl von Geräten, die ein Benutzer registrieren kann  

-   Angeben von Geschäftsbedingungen, die Benutzer im Unternehmensportal akzeptieren müssen, bevor sie die App registrieren oder nutzen können  

-   Hinzufügen einer Verwaltungsrolle für die Geräteregistrierung zur Unterstützung der Verwaltung einer großen Anzahl von Geräten  

Weitere Informationen zu Funktionen zur Verwaltung mobiler Geräte mit Configuration Manager und Intune finden Sie unter [Hybride Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

## <a name="on-premises-mobile-device-management"></a>Lokale Verwaltung mobiler Geräte  
 Sie können nun mobile Geräte mithilfe der lokalen Configuration Manager-Infrastruktur verwalten. Alle Geräteverwaltungs- und sonstigen Verwaltungsdaten werden lokal verarbeitet und sind nicht Teil von Microsoft Intune oder anderer Clouddienste. Diese Art von Gerätemanagement erfordert keine Clientsoftware. Configuration Manager verwaltet Geräte mit Funktionen, die in die Gerätebetriebssysteme integriert sind.  

 Weitere Informationen finden Sie unter [Verwalten mobiler Geräte mithilfe lokaler Infrastruktur in System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).
