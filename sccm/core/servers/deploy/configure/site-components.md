---
title: "Standortkomponenten für Configuration Manager | Microsoft-Dokumentation"
description: "Erfahren Sie, wie Standortkomponenten so konfiguriert werden, dass sich das Verhalten von Standortsystemrollen und die Statusberichterstellung des Standorts ändert."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 83550fbf0ef1f9adb0bb2c51a4f3c26a7500d352
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="site-components-for-system-center-configuration-manager"></a>Standortkomponenten für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

An jedem System Center Configuration Manager-Standort können Sie Standortkomponenten konfigurieren, um das Verhalten von Standortsystemrollen und die Statusberichterstellung des Standorts zu ändern. Konfigurationen von Standortkomponenten gelten für einen Standort sowie für jede Instanz einer anwendbaren Standortsystemrolle am Standort.  

## <a name="about-site-components"></a>Informationen zu Standortkomponenten  
 Die meisten Optionen für die verschiedenen Standortkomponenten sind bei Anzeige in der Configuration Manager-Konsole selbsterklärend. Allerdings können die folgenden Details Ihnen bei der Erläuterung einiger komplexerer Konfigurationen helfen oder Sie auf zusätzliche Inhalte mit Erklärungen verweisen.  

### <a name="software-distribution"></a>Softwareverteilung  

-   **Inhaltsverteilungseinstellungen:** Sie können Einstellungen eingeben, die ändern, wie der Standortserver Inhalte an seine Verteilungspunkte überträgt. Wenn Sie die Werte der Einstellungen für die gleichzeitige Verteilung erhöhen, kann die Inhaltsverteilung mehr Netzwerkbandbreite nutzen.  

-   **Netzwerkzugriffskonto:** Informationen zum Einrichten und Verwenden des Netzwerkzugriffskontos finden Sie unter [Netzwerkzugriffskonto](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA).  

### <a name="software-update-point"></a>Softwareupdatepunkt  

-   Informationen zu den Konfigurationsoptionen für die Softwareupdatepunkt-Komponente finden Sie unter [Installieren eines Softwareupdatepunkts](../../../../sum/get-started/install-a-software-update-point.md).  

### <a name="management-point"></a>Verwaltungspunkt  

-   **Verwaltungspunkte:** Sie können den Standort so einrichten, dass Informationen zu seinen Verwaltungspunkten in Active Directory-Domänendiensten veröffentlicht werden.  

     Verwaltungspunkte werden von Configuration Manager-Clients verwendet, um Dienste zu suchen und Standortinformationen wie Zugehörigkeit zu Begrenzungsgruppen und PKI-Zertifikat-Auswahloptionen zu finden. Clients verwenden auch Verwaltungspunkte, um nach anderen Verwaltungspunkten am Standort sowie nach Verteilungspunkte zu suchen, von denen Software heruntergeladen werden kann. Bei Clients werden Verwaltungspunkte darüber hinaus verwendet, um Standortzuweisungen abzuschließen, Clientrichtlinien herunterzuladen und ihre Clientinformationen hochzuladen.  

     Die sicherste Methode zum Suchen von Verwaltungspunkten besteht für Clients darin, sie in den Active Directory-Domänendiensten zu veröffentlichen. Daher wählen Sie in der Regel alle funktionsfähigen Verwaltungspunkte für die Veröffentlichung in den Active Directory-Domänendiensten aus. Für diese Dienstidentifizierungsmethode muss jedoch Folgendes erfüllt sein:

     - Das Schema wird für Configuration Manager erweitert.
     - Es gibt einen **System Management**-Container mit entsprechenden Sicherheitsberechtigungen für den Standortserver zum Veröffentlichen in diesen Container.
     - Der Configuration Manager-Standort ist zur Veröffentlichung in Active Directory-Domänendiensten eingerichtet.
     - Clients gehören derselben Active Directory-Gesamtstruktur an wie die Gesamtstruktur des Standortservers.  

     Wenn es für Clients im Intranet nicht möglich ist, Verwaltungspunkte mithilfe von Active Directory-Domänendiensten zu suchen, verwenden Sie stattdessen die [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns)-Veröffentlichung.  

 Allgemeine Informationen zur Dienstidentifizierung durch Clients finden Sie unter [Understand how clients find site resources and services for System Center Configuration Manager (Informationen dazu, wie Clients nach Standortressourcen und -diensten für System Center Configuration Manager suchen)](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   **Ausgewählte Intranetverwaltungspunkte in DNS veröffentlichen:** Geben Sie diese Option an, wenn Clients im Intranet Verwaltungspunkte aus Active Directory-Domänendiensten nicht finden können. Stattdessen können sie einen DNS-Ressourceneintrag zur Dienstidentifizierung (SRV RR) verwenden, um einen Verwaltungspunkt am ihnen zugewiesenen Standort zu finden.  

    Damit in Configuration Manager Intranetverwaltungspunkte in DNS veröffentlicht werden können, müssen die beiden folgenden Bedingungen erfüllt sein:  

    -   Ihre DNS-Server verfügen mindestens über die BIND-Version 8.1.2.  

    -   Ihre DNS-Server sind für automatische Updates eingerichtet und unterstützen Ressourceneinträge zur Dienstidentifizierung.  

    -   Zu den angegebenen vollständig qualifizierte Domänennamen (FQDNs) für die Verwaltungspunkte in Configuration Manager müssen Hosteinträge (A- oder AAA-Datensätze) in DNS vorhanden sein.  

    > [!WARNING]  
    >  Damit von Clients in DNS veröffentlichte Verwaltungspunkte gefunden werden können, müssen Sie die Clients einem bestimmten Standort zuweisen, anstatt die automatische Standortzuweisung zu verwenden. Richten Sie diese Clients so aus, dass sie den Standortcode mit dem Domänensuffix ihres Verwaltungspunkts verwenden. Weitere Informationen finden Sie im Abschnitt [Suchen von Verwaltungspunkten](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points) unter [Zuweisen von Clients zu einem Standort in System Center Configuration Manager](/sccm/core/clients/deploy/assign-clients-to-a-site).  

     Wenn es für Configuration Manager-Clients nicht möglich ist, Verwaltungspunkte mithilfe von Active Directory-Domänendiensten oder DNS im Intranet zu finden, wird [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins) verwendet. Der erste für einen Standort installierte Verwaltungspunkt wird automatisch in WINS veröffentlicht, wenn er für das Zulassen von HTTP-Clientverbindungen im Intranet eingerichtet wird.  

### <a name="status-reporting"></a>Statusberichterstattung  

-   Diese Einstellungen dienen zum direkten Einrichten der Detailebene, die in Statusberichte von Standorten und Clients einbezogen wird.  

### <a name="email-notification"></a>E-Mail-Benachrichtigung  

-   Geben Sie Konto- und E-Mail-Serverdetails an, um Configuration Manager das Senden von E-Mail-Benachrichtigungen zu Warnungen zu ermöglichen.  

### <a name="collection-membership-evaluation"></a>Auswertung der Sammlungsmitgliedschaft  

-   Verwenden Sie diesen Task, um die Häufigkeit der inkrementellen Auswertung der Sammlungsmitgliedschaft festzulegen. Bei der inkrementellen Auswertung wird eine Sammlungsmitgliedschaft nur mit neuen oder geänderten Ressourcen aktualisiert.  

### <a name="edit-the-site-components-at-a-site"></a>So bearbeiten Sie die Standortkomponenten auf einem Standort  

Gehen Sie folgendermaßen vor, um Standortkomponenten zu bearbeiten:

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Standortkonfiguration** > **Standorte**, und wählen Sie den Standort mit den Standortkomponenten aus, die Sie konfigurieren möchten.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Standortkomponenten konfigurieren**. Wählen Sie dann die Standortkomponente aus, die sie konfigurieren möchten.  

##  <a name="BKMK_ServiceMgr"></a> Verwalten von Standortkomponenten mit dem Dienst-Manager für Configuration Manager  
Mit dem Dienst-Manager für Configuration Manager können Sie Configuration Manager-Dienste steuern und den Status von Configuration Manager-Diensten oder -Arbeitsthreads (zusammen als Configuration Manager-Komponenten bezeichnet) anzeigen. Grundlegendes zu Configuration Manager-Komponenten:  

-   Komponenten können auf beliebigen Standortsystemen ausgeführt werden.  

-   Komponenten werden auf dieselbe Weise verwaltet wie Dienste in Windows. Sie können die Configuration Manager-Komponenten starten, beenden, anhalten, fortsetzen oder abfragen.  

Ein Configuration Manager-Dienst wird bei von ihm angeforderten Aktionen ausgeführt (üblicherweise, wenn eine Konfigurationsdatei in die Eingangsbox einer Komponente geschrieben wird). Wenn Sie die an einem Vorgang beteiligte Komponente identifizieren müssen, können Sie mithilfe des Dienst-Managers für Configuration Manager verschiedene Dienste und Threads bearbeiten. Dann können Sie die sich daraus im Verhalten von Configuration Manager ergebende Änderung sehen. Sie können beispielsweise Configuration Manager-Dienste einzeln beenden, bis eine bestimmte Reaktion beseitigt ist. So können Sie bestimmen, welcher Dienst das Verhalten verursacht.  

> [!TIP]  
>  Mithilfe des folgenden Verfahrens können Sie das Verhalten von Configuration Manager-Komponenten bearbeiten.  

### <a name="use-the-configuration-manager-service-manager"></a>So verwenden Sie den Dienst-Manager für Configuration Manager  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung** >  **Systemstatus** und anschließend auf **Komponentenstatus**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Komponente** auf **Starten**. Wählen Sie dann **Dienst-Manager für Configuration Manager** aus.  

3.  Wenn der Dienst-Manager für Configuration Manager geöffnet wird, stellen Sie eine Verbindung mit dem zu verwaltenden Standort her.  

     Wenn der zu verwaltende Standort nicht angezeigt wird, klicken Sie auf **Standort**, klicken Sie auf **Verbinden**, und geben Sie dann den Namen des Standortservers für den gewünschten Standort ein.  

4.  Erweitern Sie den Standort, und wechseln Sie zu **Komponenten** oder **Server**, je nachdem, wo die zu verwaltenden Komponenten sich befinden.  

5.  Wählen Sie im rechten Fensterbereich eine oder mehrere Komponenten aus. Klicken Sie dann im Menü **Komponente** auf **Abfrage**, um den Status Ihrer Auswahl zu aktualisieren.  

6.  Nachdem der Status der Komponente aktualisiert wurde, verwenden Sie eine der vier aktionsbasierten Optionen im Menü **Komponente**, um das Verhalten der Komponente zu ändern. Nachdem eine Aktion angefordert wurde, müssen Sie die Komponente abfragen, um den neuen Status der Komponente anzuzeigen.  

7.  Schließen Sie den Dienst-Manager für Configuration Manager, wenn Sie das Bearbeiten des Betriebsstatus der Komponenten abgeschlossen haben.  
