---
title: "Installieren von Rollen für die lokale Verwaltung mobiler Geräte – Configuration Manager | Microsoft-Dokumentation"
description: "Installieren Sie Standortsystemrollen für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
caps.latest.revision: "9"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 4913606e2f8a36e0004f711b24ecd836d0485124
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="install-site-system-roles-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Installieren von Standortsystemrollen für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die lokale Verwaltung mobiler Geräte für System Center Configuration Manager erfordert die folgenden Standortsystemrollen in der Infrastruktur Ihres Configuration Manager-Standorts:  

-   Anmeldungspunkt  

-   Anmeldungsproxypunkt  

-   Verteilungspunkt  

-   Geräteverwaltungspunkt  

-   Dienstverbindungspunkt  

 Wenn Sie die lokale Verwaltung mobiler Geräte zu Ihrer Organisation hinzufügen, in der die meisten PCs und Geräte mithilfe der Configuration Manager-Clientsoftware verwaltet werden, sind möglicherweise bereits die meisten Standortsystemrollen im Rahmen der vorhandenen Infrastruktur installiert. Falls nicht, gehen Sie auf die Seite [Hinzufügen von Standortsystemrollen für System Center Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md), um Informationen zu erhalten, wie Sie diese zu Ihrem Standort hinzufügen.  

> [!NOTE]  
>  Wenn Sie Datenbankreplikate mit Ihrer Standortsystemrolle „Geräteverwaltungspunkt“ verwenden, können sich neu registrierte Geräte anfänglich so lange nicht mit dem Geräteverwaltungspunkt verbinden, bis das Datenbankreplikat mit diesem synchronisiert wurde. Dieser Verbindungsfehler tritt auf, da das Datenbankreplikat nicht über die Informationen zum neu registrierten Gerät verfügt, die für eine erfolgreiche Verbindung erforderlich sind. Replikate werden alle 5 Minuten synchronisiert, weshalb Geräte in den ersten 5 Minuten nach der Registrierung (meist bei zwei Verbindungsversuchen) keine Verbindung herstellen können. Im Anschluss kann sich das Gerät erfolgreich verbinden.  

 Unabhängig davon, ob Sie vorhandene Standortsystemrollen verwenden oder neue hinzufügen, müssen Sie die Rollen konfigurieren, damit sie zum Verwalten moderner Geräte verwendet werden können. Führen Sie die folgenden Schritte aus, um den Verteilungs- und Geräteverwaltungspunkt zu konfigurieren, damit diese für die lokale Verwaltung mobiler Geräte ordnungsgemäß funktionieren:  

> [!NOTE]  
>  Der aktuelle Branch von Configuration Manager unterstützt nur Intranetverbindungen von Geräten mit den Verteilungs- und Geräteverwaltungspunkten für die lokale Verwaltung mobiler Geräte. Wenn Sie jedoch auch Mac OS X-Computer verwalten, erfordern diese Clients Internetverbindungen mit diesen Standortsystemrollen. Wenn Sie in diesem Fall die Eigenschaften des Verteilungspunkts und Geräteverwaltungspunkts konfigurieren, sollten Sie stattdessen die Einstellung **Intranet- und Internetverbindungen zulassen** verwenden.  

### <a name="to-configure-site-system-roles-to-manage-modern-devices"></a>So konfigurieren Sie Standortsystemrollen für die Verwaltung moderner Geräte:  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Übersicht** > **Standortkonfiguration** > **Server und Standortsystemrollen**.  

2.  Wählen Sie den Standortsystemserver mit dem zu konfigurierenden Verteilungspunkt oder Geräteverwaltungspunkt aus, öffnen Sie die Eigenschaften für **Standortsystem**, und stellen Sie sicher, dass ein FQDN angegeben ist. Klicken Sie auf **OK**.  

3.  Öffnen Sie die Eigenschaften für die Standortsystemrolle „Verteilungspunkt“. Vergewissern Sie sich auf der Registerkarte „Allgemein“, dass **HTTPS** ausgewählt ist, und wählen Sie **Nur Intranet-Clientverbindungen zulassen** aus.  

     Wenn Sie Macintosh-Computer auch separat mit dem Configuration Manager-Client verwalten, verwenden Sie stattdessen die Option **Intranet- und Internetverbindungen zulassen**.  

    > [!NOTE]  
    >  Für Intranetverbindungen konfigurierte Verteilungspunkte erfordern entsprechend konfigurierte Standortgrenzen. Der aktuelle Branch von Configuration Manager unterstützt nur IPv4-Bereichsgrenzen für die lokale Verwaltung mobiler Geräte. Informationen zum Konfigurieren von Bereichsgrenzen finden Sie unter [Definieren von Standortgrenzen und Begrenzungsgruppen für Configuration Manager](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

4.  Klicken Sie auf das Kontrollkästchen neben **Mobilen Geräten die Verbindung mit diesem Verteilungspunkt gestatten**, und klicken Sie dann auf **OK**.  

5.  Öffnen Sie die Eigenschaften für die Standortsystemrolle „Verwaltungspunkt“. Vergewissern Sie sich auf der Registerkarte „Allgemein“, dass **HTTPS** ausgewählt ist, und wählen Sie **Nur Intranet-Clientverbindungen zulassen** aus.  

     Wenn Sie Macintosh-Computer auch separat mit dem Configuration Manager-Client verwalten, verwenden Sie stattdessen die Option **Intranet- und Internetverbindungen zulassen**.  

6.  Klicken Sie auf das Kontrollkästchen neben **Verwendung dieses Verwaltungspunkts durch mobile Geräte und Macintosh-Computer zulassen**. Klicken Sie auf **OK**.  

     Dadurch wird der Verwaltungspunkt faktisch zu einem Geräteverwaltungspunkt.  

 Nachdem die Standortsystemrollen hinzugefügt und für die Verwaltung von modernen Geräte konfiguriert wurden, müssen Sie die Server konfigurieren, die die Rollen als vertrauenswürdige Endpunkte für die Registrierung und die Kommunikation mit verwalteten Geräten hosten. Weitere Informationen finden Sie unter [Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager (Einrichten von Zertifikaten für vertrauenswürdige Verbindungen für die lokale Verwaltung von mobilen Geräten in System Center Configuration Manager)](../../mdm/get-started/set-up-certificates-on-premises-mdm.md).  
