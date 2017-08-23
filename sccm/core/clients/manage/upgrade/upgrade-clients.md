---
title: Aktualisieren von Clients | Microsoft-Dokumentation
description: "Enthält Informationen über das Aktualisieren von Clients in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 4b80e0e688dd6482bc9a7fe111607e258071f45a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-clients-in-system-center-configuration-manager"></a>Aktualisieren von Clients in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Es gibt verschiedene Methoden zum Upgrade der Clientsoftware von System Center Configuration Manager auf Windows-Computern, UNIX- und Linux-Servern sowie Macintosh-Computern. Die Vor- und Nachteile der einzelnen Methoden sind nachfolgend beschrieben.  

> [!TIP]  
>  Wenn Sie ein Upgrade Ihrer Serverinfrastruktur von einer früheren Version von Configuration Manager durchführen \(z.B. Configuration Manager 2007 oder System Center 2012 Configuration Manager\), empfiehlt es sich, das Serverupgrade einschließlich der Installation sämtlicher Branchupdates vollständig abzuschließen, bevor Sie ein Upgrade der Configuration Manager-Clients durchführen. Auf diese Weise erhalten Sie auch die aktuellste Version der Clientsoftware.  

## <a name="group-policy-installation"></a>Gruppenrichtlinieninstallation  
 **Unterstützte Clientplattformen:** Windows  

 **Vorteile**  

-   Erfordert keine Ermittlung von Computern als Voraussetzung für die Aktualisierung des Clients.  

-   Kann für neue Clientinstallationen oder für Aktualisierungen verwendet werden.  

-   Clientinstallationseigenschaften, die in Active Directory-Domänendienste veröffentlicht wurden, können von Computern gelesen werden.  

-   Erfordert keine Konfiguration oder Wartung eines Installationskontos für den betreffenden Clientcomputer.  

 **Nachteile**  

-   Kann ein hohes Netzwerkverkehrsaufkommen verursachen, wenn Sie eine große Anzahl von Clients upgraden.  

-   Wenn das Active Directory-Schema nicht für Configuration Manager erweitert wurde, müssen Sie die Clientinstallationseigenschaften mithilfe von [Gruppenrichtlinieneinstellungen](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP) den Computern des Standorts hinzufügen.  


## <a name="logon-script-installation"></a>Anmeldeskriptinstallation  
 **Unterstützte Clientplattformen:** Windows  

 **Vorteile**  

-   Erfordert keine Ermittlung von Computern als Voraussetzung für die Installation des Clients.  

-   Kann für neue Clientinstallationen oder für Aktualisierungen verwendet werden.  

-   Unterstützt die Verwendung von Befehlszeileneigenschaften für CCMSetup.  

 **Nachteile**  

-   Kann ein hohes Netzwerkverkehrsaufkommen verursachen, wenn Sie in kurzer Zeit eine große Anzahl von Clients aktualisieren.  

-   Die Aktualisierung aller Clientcomputer kann lange dauern, wenn Benutzer sich nicht regelmäßig beim Netzwerk anmelden.  

 Weitere Informationen finden Sie unter [Installieren von Configuration Manager-Clients mithilfe von Anmeldeskripts](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  

## <a name="manual-installation"></a>Manuelle Installation  
 **Unterstützte Clientplattformen:** Windows, UNIX/Linux, Mac OS X  

 **Vorteile**  

-   Erfordert keine Ermittlung von Computern als Voraussetzung für die Aktualisierung des Clients.  

-   Kann zu Testzwecken verwendet werden.  

-   Unterstützt die Verwendung von Befehlszeileneigenschaften für CCMSetup.  

 **Nachteile**  

-   Keine Automatisierung, daher zeitaufwändig.  

 Weitere Informationen finden Sie unter den folgenden Themen:  

-   [How to Install Configuration Manager Clients Manually (Manuelles Installieren von Configuration Manager-Clients)](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [How to upgrade clients for Linux and UNIX servers in System Center Configuration Manager (Aktualisieren von Clients für Linux- und UNIX-Server in System Center Configuration Manager)](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

-   [How to upgrade clients on Mac computers in System Center Configuration Manager (Aktualisieren von Clients auf Macintosh-Computern in System Center Configuration Manager)](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>Upgrade-Installation (Anwendungsverwaltung)  
 **Unterstützte Clientplattformen:** Windows  

> [!NOTE]  
>  Mit dieser Methode können keine Upgrades von Configuration Manager 2007-Clients durchgeführt werden. In diesem Szenario können Sie den Configuration Manager-Client als Paket vom Configuration Manager 2007-Standort bereitstellen, oder Sie können das automatische Clientupgrade verwenden, wobei automatisch ein Paket erstellt und bereitgestellt wird, das die aktuellste Clientversion enthält.  

 **Vorteile**  

-   Unterstützt die Verwendung von Befehlszeileneigenschaften für CCMSetup.  

 **Nachteile**  

-   Kann ein hohes Netzwerkverkehrsaufkommen verursachen, wenn Sie den Client auf große Sammlungen verteilen.  

-   Kann nur verwendet werden, um Clientsoftware auf Computern zu aktualisieren, die ermittelt und dem Standort zugewiesen wurden.  

 Weitere Informationen finden Sie unter [Installieren von Configuration Manager-Clients mithilfe eines Pakets und Programms](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp).  

## <a name="automatic-client-upgrade"></a>Automatisches Clientupgrade  

> [!NOTE]  
>  Kann verwendet werden, um ein Upgrade von Configuration Manager 2007-Clients auf System Center Configuration Manager-Clients auszuführen. Ein Configuration Manager 2007-Client kann einem Configuration Manager-Standort zugewiesen werden, allerdings können keine anderen Aktionen außer dem automatischen Clientupgrade durchgeführt werden.  

 **Unterstützte Clientplattformen:** Windows  

 **Vorteile**  

-   Kann verwendet werden, um Clients eines Standorts automatisch auf die neueste Version zu aktualisieren.  

-   Erfordert minimalen Verwaltungsaufwand.  

 **Nachteile**  

-   Kann nur für ein Upgrade der Clientsoftware verwendet werden, nicht für die Installation eines neuen Clients.  

-   Nicht geeignet für das gleichzeitige Upgrade zahlreicher Clients.  

-   Gilt für alle Clients in der Hierarchie, die einem Standort zugewiesen sind. Kann nicht auf Sammlungen begrenzt werden.  

-   Begrenzte Planungsoptionen  

 Weitere Informationen finden Sie unter [Aktualisieren von Clients für Windows-Computer in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="client-testing"></a>Testen von Clients  
 **Unterstützte Clientplattformen:** Windows  

 **Vorteile**  

-   Kann zum Testen neuer Clientversionen in einer kleineren Präproduktionssammlung verwendet werden.  

-   Nach Abschluss der Tests werden Clients in der Präproduktionsphase auf die Produktionsebene heraufgestuft und automatisch am gesamten Configuration Manager-Standort aktualisiert.  

 **Nachteile**  

-   Kann nur für ein Upgrade der Clientsoftware verwendet werden, nicht für die Installation eines neuen Clients.  

 [Testen von Clientupgrades in einer Präproduktionssammlung in System Center Configuration Manager](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  
