---
title: "Unterstützung von Proxyservern | Microsoft-Dokumentation"
description: "Erfahren Sie mehr zur Unterstützung der von Standortsystemservern und Clients verwendeten Proxyserver durch System Center Configuration Manager."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: dc36be47310d2c2178c974a2b503d0b5f9f6e2ec
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="proxy-server-support-in-system-center-configuration-manager"></a>Unterstützung von Proxyservern in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sowohl System Center Configuration Manager-Standortsystemserver als auch Clients können einen Proxyserver verwenden.  

## <a name="site-system-servers"></a>Standortsystemserver  
Sind für Standortsystemrollen Verbindungen mit dem Internet erforderlich, können Sie die Rollen so konfigurieren, dass sie einen Proxyserver verwenden.  

-   Ein Computer, der einen Standortsystemserver hostet, unterstützt eine einzelne Proxyserverkonfiguration, die von allen Standortsystemrollen auf diesem Computer freigegeben wurde. Wenn Sie getrennte Proxyserver für verschiedene Rollen oder Instanzen einer Rolle benötigen, müssen Sie diese Rollen auf separaten Standortsystemservern platzieren.  

-   Wenn Sie neue Proxyservereinstellungen für einen Standortsystemserver konfigurieren, für den es bereits eine Proxyserverkonfiguration gibt, wird die ursprüngliche Konfiguration überschrieben.  

-   Verbindungen zum Proxy verwenden das Konto **System** des Computers, der die Standortsystemrolle hostet.  

Die folgenden Standortsystemrollen stellen eine Verbindung mit dem Internet her und benötigen möglicherweise einen Proxyserver.  Mit einer Ausnahme verwenden Standortsystemrollen, die dies können, einen Proxy ohne zusätzliche Konfiguration. Die Ausnahme ist der Softwareupdatepunkt. Die folgende Liste enthält Informationen zu den zusätzlichen Konfigurationen, die für einen Softwareupdatepunkt erforderlich sind:  

**Asset Intelligence-Synchronisierungspunkt:** Diese Standortsystemrolle stellt eine Verbindung mit Microsoft her und verwendet eine Proxyserverkonfiguration auf dem Computer, auf dem der Asset Intelligence-Synchronisierungspunkt gehostet wird.  

**Cloudbasierter Verteilungspunkt:** Um einen Proxyserver für einen cloudbasierten Verteilungspunkt einzurichten, richten Sie den Proxy auf dem primären Standort ein, der den cloudbasierten Verteilungspunkt verwaltet.  

Für diese Konfiguration gilt für den primären Standortserver Folgendes:  

-   Er muss in der Lage sein, eine Verbindung mit Microsoft Azure herzustellen, um Inhalte für den Verteilungspunkt einzurichten, zu überwachen und zu verteilen.  

-   Er verwendet das Systemkonto dieses Computers, um die Verbindung herzustellen.  

-   Er verwendet den Standardwebbrowser dieses Computers.  

Sie können keinen Proxyserver auf dem cloudbasierten Verteilungspunkt in Microsoft Azure einrichten.  

**Cloudverbindungspunkt:** Diese Standortsystemrolle stellt eine Verbindung mit dem Configuration Manager-Clouddienst her, um Versionsupdates für Configuration Manager herunterzuladen, und verwendet einen Proxyserver, der auf dem Computer konfiguriert ist, der den Dienstverbindungspunkt hostet.  

**Der Exchange Server-Connector:** Diese Standortsystemrolle stellt eine Verbindung mit einem Exchange Server her und verwendet eine Proxyserverkonfiguration auf dem Computer, auf dem der Exchange Server-Connector gehostet wird.  

**Dienstverbindungspunkt:** Für diese Standortsystemrolle wird eine Verbindung mit Microsoft Intune hergestellt, und es wird eine Proxyserverkonfiguration auf dem Computer verwendet, auf dem der Dienstverbindungspunkt gehostet wird.  

**Softwareupdatepunkt:** Diese Standortsystemrolle kann den Proxy zur Verbindung mit Microsoft Update verwenden, um Patches herunterzuladen und Informationen zu Updates zu synchronisieren. Softwareupdatepunkte verwenden nur dann einen Proxy für die folgenden Optionen, wenn Sie diese Option beim Einrichten des Softwareupdatepunkts aktivieren:  

-   **Verwenden von Proxyserver beim Synchronisieren von Softwareupdates**  

-   **Proxyserver beim Herunterladen von Inhalt mithilfe der Regeln zur automatischen Bereitstellung verwenden** (Obwohl sie zur Verwendung verfügbar ist, wird diese Einstellung von Softwareupdatepunkten in sekundären Standorten nicht verwendet.)  

Konfigurieren Sie die Proxyservereinstellungen im Assistenten zum Hinzufügen von Standortsystemrollen auf der Seite „Aktiver Softwareupdatepunkt“ oder in **Eigenschaften der Softwareupdatepunktkomponente** auf der Registerkarte **Allgemein**.  

-   Die Proxyservereinstellungen werden nur dem Softwareupdatepunkt am Standort zugeordnet.  

-   Proxyserveroptionen sind nur verfügbar, wenn bereits ein Proxyserver für den Standortsystemserver eingerichtet ist, der den Softwareupdatepunkt hostet.  

> [!NOTE]  
>  Das Konto **System** für den Server, auf dem die automatische Bereitstellungsregel erstellt wurde, wird bei der Ausführung der automatischen Bereitstellungsregeln standardmäßig zum Herstellen der Verbindung mit dem Internet und zum Herunterladen von Softwareupdates verwendet.  
>   
>  Wenn dieses Konto keine Verbindung mit dem Internet herstellen kann, können keine Softwareupdates heruntergeladen werden. In diesem Fall wird der Datei „ruleengine.log“ der folgende Eintrag hinzugefügt: **Fehler beim Herunterladen des Updates aus dem Internet. Fehler = 12007**.  

#### <a name="to-set-up-the-proxy-server-for-a-site-system-server"></a>So richten Sie den Proxyserver für einen Standortsystemserver ein  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie dann **Server- und Standortsystemrollen**.  

2.  Wählen Sie den Standortsystemserver aus, den Sie bearbeiten möchten, klicken Sie im Detailbereich mit der rechten Maustaste auf **Standortsystem**, und wählen Sie **Eigenschaften**.  

3.  Wählen Sie unter Eigenschaften des Standortsystems die Registerkarte **Proxy** aus, und richten Sie die Proxyeinstellungen für diesen primären Standortserver ein.  

4.  Wählen Sie **OK**, um die neue Proxyserverkonfiguration zu speichern.  
