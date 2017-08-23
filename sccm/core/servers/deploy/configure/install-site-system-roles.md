---
title: Installieren von Standortsystemrollen | Microsoft-Dokumentation
description: "Assistenten unterstützen Sie beim Hinzufügen von Standortsystemrollen zu einem vorhandenen oder neuen Standortsystemserver des Standorts."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 76b070f8e203cc0c751f35e5a4b4904504786c04
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="install-site-system-roles-for-system-center-configuration-manager"></a>Installieren von Standortsystemrollen für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die System Center Configuration Manager-Konsole besitzt zwei Assistenten, die Sie zur Installation von Standortsystemrollen verwenden können:  

-   **Assistent zum Hinzufügen von Standortsystemrollen**: Verwenden Sie diesen Assistenten, um Standortsystemrollen einem vorhandenen Standortsystemserver des Standorts hinzuzufügen.  

-   **Assistent zum Erstellen von Standortsystemservern**: Verwenden Sie diesen Assistenten, um einen neuen Server als Standortsystemserver anzugeben und dann eine oder mehrere Standortsystemrollen auf dem Server zu installieren. Dieser Assistent und der **Assistent zum Hinzufügen von Standortsystemrollen**entsprechen einander bis auf die Tatsache, dass Sie bei diesem Assistenten auf der ersten Seite den Namen des Servers angeben müssen, der verwendet werden soll, sowie den Standort, an dem der Server installiert werden soll.  

Wenn Sie eine Standortsystemrolle auf einem Remotecomputer installieren (einschließlich einer Instanz des SMS-Anbieters), wird das Computerkonto des Remotecomputers einer lokalen Gruppe auf dem Standortserver hinzugefügt. Wenn der Standort auf einem Domänencontroller installiert ist, handelt es sich bei der Gruppe auf dem Standortserver um eine Domänengruppe und nicht um eine lokale Gruppe. In diesem Fall ist die Remote-Standortsystemrolle erst betriebsbereit, wenn der Computer mit der Standortsystemrolle neu gestartet oder das Kerberos-Ticket für das Konto des Remotecomputers aktualisiert wurde. Weitere Informationen finden Sie unter [In System Center Configuration Manager verwendete Konten](../../../../core/plan-design/hierarchy/accounts.md).  

Unmittelbar vor der Installation der Standortsystemrolle überprüft Configuration Manager den Zielcomputer, um sicherzustellen, dass er die Voraussetzungen für die ausgewählten Standortsystemrollen erfüllt. Grundlegendes zum Installieren von Standortsystemrollen:  

-   Wenn Configuration Manager eine Standortsystemrolle standardmäßig installiert, erfolgt die Installation auf dem ersten verfügbaren NTFS-formatierten Laufwerk, auf dem genügend Speicherplatz verfügbar ist. Um zu verhindern, dass Configuration Manager die Installation auf bestimmten Laufwerken durchführt, erstellen Sie eine leere Datei **no_sms_on_drive.sms**. Kopieren Sie sie in den Stammordner des Laufwerks, bevor Sie den Standortsystemserver installieren.  

-   Configuration Manager verwendet das **Standortsystem-Installationskonto** zum Installieren der Standortsystemrollen. Sie geben dieses Konto beim Ausführen des Assistenten zum Erstellen eines neuen Standortsystemservers oder zum Hinzufügen neuer Standortsystemrollen zu einem vorhandenen Standortsystemserver an. Standardmäßig handelt es sich bei diesem Konto um das lokale Systemkonto des Standortservercomputers, doch können Sie auch ein Domänenbenutzerkonto zur Verwendung als Standortsystem-Installationskonto angeben. Weitere Informationen finden Sie unter [In System Center Configuration Manager verwendete Konten](../../../../core/plan-design/hierarchy/accounts.md).  

##  <a name="bkmk_Install"></a> So installieren Sie Standortsystemrollen auf einem vorhandenen Standortsystemserver  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Knoten **Standortkonfiguration**, und klicken Sie dann auf **Server und Standortsystemrollen**. Wählen Sie anschließend den Server aus, den Sie für die neuen Standortsystemrollen verwenden möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Server** auf **Standortsystemrollen hinzufügen**.  

4.  Überprüfen Sie auf der Seite **Allgemein** die Einstellungen, und klicken Sie dann auf **Weiter**.  

    > [!TIP]  
    >  Um vom Internet aus auf die Standortsystemrolle zuzugreifen, stellen Sie sicher, dass Sie einen vollqualifizierten Internetdomänennamen (FQDN) angeben.  

5.  Geben Sie auf der Seite **Proxy** die Einstellungen für einen Proxyserver an, wenn für die auf diesem Standortsystemserver ausgeführten Standortsystemrollen ein Proxyserver erforderlich ist, damit eine Verbindung zu Speicherorten im Internet hergestellt werden kann. Klicken Sie anschließend auf **Weiter**.  

6.  Wählen Sie auf der Seite **Systemrollenauswahl** die Standortsystemrollen aus, die Sie hinzufügen möchten, und klicken Sie dann auf **Weiter**.  

7.  Schließen Sie den Assistenten ab.  

> [!TIP]  
>  Mit dem Windows PowerShell-Cmdlet New-CMSiteSystemServer wird die gleiche Funktion wie mit diesem Verfahren ausgeführt. Weitere Informationen finden Sie unter [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414) in der Cmdlet-Referenzdokumentation von System Center 2012 Configuration Manager SP1.  

## <a name="to-install-site-system-roles-on-a-new-site-system-server"></a>So installieren Sie Standortsystemrollen auf einem neuen Standortsystemserver  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Knoten **Standortkonfiguration**, und klicken Sie dann auf **Server und Standortsystemrollen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Standortsystemserver erstellen**.  

4.  Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für den Standortsystemserver an, und klicken Sie dann auf **Weiter**.  

    > [!TIP]  
    >  Für einen Zugriff auf die neue Standortsystemrolle aus dem Internet ist die Angabe eines Internet-FQDN erforderlich.  

5.  Geben Sie auf der Seite **Proxy** die Einstellungen für einen Proxyserver an, wenn für die auf diesem Standortsystemserver ausgeführten Standortsystemrollen ein Proxyserver erforderlich ist, damit eine Verbindung zu Speicherorten im Internet hergestellt werden kann. Klicken Sie anschließend auf **Weiter**.  

6.  Wählen Sie auf der Seite **Systemrollenauswahl** die Standortsystemrollen aus, die Sie hinzufügen möchten, und klicken Sie dann auf **Weiter**.  

7.  Schließen Sie den Assistenten ab.  

> [!TIP]  
>  Mit dem Windows PowerShell-Cmdlet New-CMSiteSystemServer wird die gleiche Funktion wie mit diesem Verfahren ausgeführt. Weitere Informationen finden Sie unter [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414) in der Cmdlet-Referenzdokumentation von System Center 2012 Configuration Manager SP1.  
