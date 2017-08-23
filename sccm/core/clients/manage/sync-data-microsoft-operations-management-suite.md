---
title: 'Synchronisieren von Daten | Microsoft-Dokumentation | Microsoft Operations Management Suite '
description: Synchronisieren Sie Daten aus System Center Configuration Manager mit Microsoft Operations Management Suite.
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: "9"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 608a9893011c6500d5d4cd2f756a124db66b1858
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
#  <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Synchronisieren von Daten von System Center Configuration Manager mit der Microsoft Operations Management Suite

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können den **Assistenten für Azure-Dienste** zum Konfigurieren der Verbindung zwischen Configuration Manager und dem Clouddienst Operations Management Suite (OMS) verwenden. Ab Version 1706 ersetzt der Assistent vorherige Workflows zum Konfigurieren dieser Verbindung. Informationen zu früheren Versionen finden Sie unter [Sync data from Configuration Manager to the Microsoft Operations Management Suite (1702 and earlier) (Synchronisieren von Daten von System Center Configuration Manager mit der Microsoft Operations Management Suite (1702 und früher))](#Sync-data-from-Configuration-Manager-to-the-Microsoft-Operations-Management-Suite-(1702-and-earlier)).

-   Der Assistent dient zum Konfigurieren von Clouddiensten für Configuration Manager wie OMS, Windows Store für Unternehmen (WSfB) und Azure Active Directory (Azure AD).  

-   Configuration Manager verbindet sich mit OMS für Funktionen wie [Log Analytics](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) oder [Upgradebereitschaft](/sccm/core/clients/manage/upgrade/upgrade-analytics).

## <a name="prerequisites-for-the-oms-connector"></a>Voraussetzungen für den OMS-Connector
Die Voraussetzungen zum Konfigurieren einer Verbindung mit OMS unterscheiden sich nicht von denjenigen, die [für die Current Branch-Version 1702 dokumentiert sind](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites). Diese Informationen werden hier wiederholt:  

-   Bevor Sie den OMS-Connector in Configuration Manager installieren, müssen Sie Configuration Manager mit Berechtigungen für OMS bereitstellen. Sie müssen insbesondere den *Zugriff als Mitwirkender* in der Azure-*Ressourcengruppe* gewähren, die den OMS-Protokollanalyse-Arbeitsbereich enthält. Die Vorgehensweisen dazu werden im Protokollanalysen-Inhalt dokumentiert. Informationen finden Sie in der OMS-Dokumentation unter [Bereitstellen von Configuration Manager mit Berechtigungen für OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms).

-   Der OMS-Connector muss auf dem Computer installiert werden, der einen [Dienstverbindungspunkt](/sccm/core/servers/deploy/configure/about-the-service-connection-point) hostet, der sich in [Onlinemodus](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation) befindet.

-   Sie müssen Microsoft Monitoring Agent für OMS auf den Dienstverbindungspunk zusammen mit den OMS-Connector installieren. Der Agent und der OMS-Connector müssen so konfiguriert werden, dass sie den gleichen **OMS-Arbeitsbereich** nutzen. In der OMS-Dokumentation unter [Herunterladen und Installieren des Agents](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) finden Sie Informationen zur Installation des Agents.
-   Nachdem Sie den Connector und den Agent installiert haben, müssen Sie OMS für die Verwendung von Configuration Manager-Daten konfigurieren. Dazu gehen Sie im OMS-Portal unter [Importieren von Sammlungen](/azure/log-analytics/log-analytics-sccm#import-collections).

## <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Verwenden des Assistenten für Azure-Dienste zum Konfigurieren der Verbindung mit OMS

1.  Wechseln Sie in der Konsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Azure-Dienste**, und wählen Sie dann **Azure-Dienste konfigurieren** auf der Registerkarte **Start** im Menüband aus, um den **Assistenten für Azure-Dienste** zu starten.

2.  Wählen Sie auf der Seite **Azure-Dienste** den Clouddienst „Operation Management Suite“ aus. Geben Sie einen Anzeigenamen für den **Azure-Dienstnamen** und eine optionale Beschreibung ein, und klicken Sie dann auf **Weiter**.

3.  Geben Sie auf der Seite **App** Ihre Azure-Umgebung an (die Technical Preview unterstützt nur die öffentliche Cloud). Klicken Sie dann auf **Durchsuchen**, um das Server-App-Fenster zu öffnen.

4.  Wählen Sie eine Web-App aus:

    -   **Importieren**: Um eine Web-App zu verwenden, die in Ihrem Azure-Abonnement bereits vorhanden ist, klicken Sie auf **Importieren**. Stellen Sie einen Anzeigenamen für die App und den Mandanten bereit, und geben Sie dann die Mandanten-ID, Client-ID und den geheimen Schlüssel für die Web-App an, die Configuration Manager verwenden soll. Nachdem Sie die Informationen **überprüft** haben, klicken Sie auf **OK**, um fortzufahren.   

    > [!NOTE]   
    > Bei Konfiguration von OMS in dieser Preview-Version unterstützt OMS nur die Funktion *Importieren* für eine Web-App. Das Erstellen einer neuen Web-App wird nicht unterstützt. Sie können auch keine vorhandene App für OMS wiederverwenden.

5.  Wenn Sie alle anderen Schritte erfolgreich ausgeführt haben, werden die Informationen auf dem Bildschirm **OMS-Verbindungskonfiguration** automatisch auf dieser Seite angezeigt. Informationen zu den Verbindungseinstellungen müssen für Ihr **Azure-Abonnement**, die **Azure-Ressourcengruppe** und den **Operations Management Suite-Arbeitsbereich** angezeigt werden.

6.  Der Assistent stellt eine Verbindung mit dem OMS-Dienst unter Verwendung der von Ihnen eingegebenen Informationen her. Wählen Sie die Gerätesammlungen aus, die Sie mit OMS synchronisieren möchten, und klicken Sie dann auf **Hinzufügen**.

7.  Überprüfen Sie die Verbindungseinstellungen auf dem Bildschirm **Zusammenfassung**, und wählen Sie dann **Weiter** aus. Auf dem Bildschirm **Status** wird der Verbindungsstatus angezeigt. Anschließend sollte **Abgeschlossen** angezeigt werden.

8.  Nach Abschluss des Assistenten zeigt die Configuration Manager-Konsole, dass Sie **Operation Management Suite** als **Clouddiensttyp** konfiguriert haben.

## <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite-1702-and-earlier"></a>Synchronisieren von Daten von System Center Configuration Manager mit der Microsoft Operations Management Suite (1702 und früher)


*Applies to: System Center Configuration Manager (1702 and prior versions)* (Gilt für: System Center Configuration Manager (Version 1702 und früher)

Sie können nun mit dem Microsoft Operations Management Suite-Connector (OMS) Daten, z.B. Ihre Sammlungen, von System Center Configuration Manager mit den OMS-Protokollanalyseressourcen in Microsoft Azure synchronisieren. Dadurch werden Daten aus der Configuration Manager-Bereitstellung in OMS sichtbar dargestellt.
> [!TIP]
> Der OMS-Connector ist ein vorab veröffentlichtes Feature. Weitere Informationen erhalten Sie unter [Use pre-release features from updates (Verwenden von vorab veröffentlichten Features von Updates)](/sccm/core/servers/manage/pre-release-features).

Ab Version 1702 können Sie den OMS-Connector für die Verbindung mit einem OMS-Arbeitsbereich verwenden, der sich in der Microsoft Azure Government-Cloud befindet. Dazu müssen Sie eine Konfigurationsdatei ändern, bevor Sie den OMS-Connector installieren. Weitere Informationen finden Sie unter [Verwenden des OMS-Connectors mit der Azure Government-Cloud](#fairfaxconfig) in diesem Thema.

### <a name="prerequisites"></a>Voraussetzungen
- Bevor Sie den OMS-Connector in Configuration Manager installieren, müssen Sie Configuration Manager mit Berechtigungen für OMS bereitstellen. Sie müssen insbesondere den *Zugriff als Mitwirkender* in der Azure-*Ressourcengruppe* gewähren, die den OMS-Protokollanalyse-Arbeitsbereich enthält. Die Vorgehensweisen dazu werden im Protokollanalysen-Inhalt dokumentiert. Informationen finden Sie in der OMS-Dokumentation unter [Bereitstellen von Configuration Manager mit Berechtigungen für OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms).

- Der OMS-Connector muss auf dem Computer installiert werden, der einen [Dienstverbindungspunkt](/sccm/core/servers/deploy/configure/about-the-service-connection-point) hostet, der sich in [Onlinemodus](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation) befindet.

  Wenn Sie OMS mit einem eigenständigen primären Standort verbunden haben und planen, Ihrer Umgebung einen Standort der zentralen Verwaltung hinzuzufügen, müssen Sie die aktuelle Verbindung löschen und anschließend den Connector am neuen Standort der zentralen Verwaltung erneut konfigurieren.

- Sie müssen Microsoft Monitoring Agent für OMS auf den Dienstverbindungspunk zusammen mit den OMS-Connector installieren.  Der Agent und der OMS-Connector müssen so konfiguriert werden, dass sie den gleichen **OMS-Arbeitsbereich** nutzen. In der OMS-Dokumentation unter [Herunterladen und Installieren des Agents](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) finden Sie Informationen zur Installation des Agents.

- Nachdem Sie den Connector und den Agent installiert haben, müssen Sie OMS für die Verwendung von Configuration Manager-Daten konfigurieren.  Dazu gehen Sie im OMS-Portal unter [Importieren von Sammlungen](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections).



### <a name="install-the-oms-connector"></a>Installieren des OMS-Connectors  
1. Konfigurieren Sie in der Configuration Manager-Konsole Ihre [Hierarchie zur Verwendung von Features der Vorabversion](/sccm/core/servers/manage/pre-release-features), und aktivieren Sie die Verwendung des OMS-Connectors.  

2. Navigieren Sie als nächstes zu **Verwaltung** > **Clouddienste** > **OMS-Connector**. Klicken Sie im Menüband auf „Verbindung mit Operations Management Suite erstellen“. Daraufhin wird der **Assistent für die Verbindung mit der Operations Management Suite** geöffnet. Wählen Sie **Weiter** aus.  


3.  Vergewissern Sie sich auf der Seite **Allgemein**, dass Sie folgende Informationen besitzen, und wählen Sie **Weiter** aus.  
  - Configuration Manager wurde als „Webanwendung und/oder Web-API”-Verwaltungstool registriert, und Sie haben die [Client-ID dieser Registrierung](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).  
  - Für das registrierte Verwaltungstool in Azure Active Directory wurde ein Clientschlüssel erstellt.  

  - Im Azure Management Portal wurde die registrierte Web-App mit der Berechtigung bereitgestellt, auf OMS zuzugreifen, wie in [Provide Configuration Manager with permissions to OMS (Bereitstellen von Configuration Manager mit Berechtigungen für OMS)](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) beschrieben.  

4.  Konfigurieren Sie auf der Seite **Azure Active Directory** Ihre Verbindungseinstellungen zu OMS, indem Sie **Mandant**, **Client-ID** und **Geheimer Schlüssel** angeben und dann **Weiter** auswählen.  

5.  Auf der Seite **OMS-Verbindungskonfiguration** geben Sie die Verbindungseinstellungen ein, indem Sie **Azure-Abonnement**, **Azure-Ressourcengruppe** und **Operations Management Suite-Arbeitsbereich** angeben.  Der Arbeitsbereich muss mit dem Arbeitsbereich übereinstimmen, der für den Microsoft-Verwaltungs-Agent konfiguriert ist, der auf dem Dienstverbindungspunkt installiert ist.  

6.  Überprüfen Sie die Verbindungseinstellungen auf der Seite **Zusammenfassung**, und wählen Sie dann **Weiter** aus. Auf der Seite **Status** wird der Verbindungsstatus angezeigt. Anschließend sollte **Abgeschlossen** angezeigt werden.

Nachdem Sie Configuration Manager mit OMS verbunden haben, können Sie Sammlungen hinzufügen oder entfernen und die Eigenschaften der OMS-Verbindung anzeigen.

### <a name="verify-the-oms-connector-properties"></a>Überprüfen der Eigenschaften des OMS-Connectors
1.  Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Clouddienste**, und wählen Sie dann **OMS-Connector** aus, um die Seite **OMS-Verbindung**** zu öffnen.
2.  Auf dieser Seite befinden sich zwei Registerkarten:
  - **Azure Active Directory:**   
    Diese Registerkarte zeigt **Mandant**, **Client-ID**, **Client secret key expiration** (Ablauf des geheimen Clientschlüssels) an und ermöglicht Ihnen zu Überprüfen, ob Ihr geheimer Clientschlüssel abgelaufen ist.

  - **OMS-Verbindungseigenschaften:**  
    Diese Registerkarte zeigt **Azure-Abonnement**, **Azure-Ressourcengruppe**, **Operations Management Suite-Arbeitsbereich** und eine Liste der **Gerätesammlungen, für die die Operations Management Suite Daten abrufen kann**. Geben Sie mithilfe der Schaltfläche **Hinzufügen** und **Entfernen** an, welche Sammlungen zulässig sind.

### <a name="fairfaxconfig"> </a> Verwenden des OMS-Connectors mit der Azure Government-Cloud


1.  Bearbeiten Sie auf jedem Computer, auf dem die Configuration Manager-Konsole installiert ist, die folgende Konfigurationsdatei, damit sie auf die Government-Cloud zeigt: ***&lt;Installationspfad_von_Configuration_Manager>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **Bearbeitungen:**

    Ändern Sie den Wert für die Einstellung *FairFaxArmResourceID* in „https://management.usgovcloudapi.net/“.

   - **Original:**&lt; setting name="FairFaxArmResourceId" serializeAs="String">   
      &lt;value>&lt;/value>   
      &lt;/setting>

   - **Bearbeitet:**     
      &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value>https://management.usgovcloudapi.net/&lt;/value>  
      &lt;/setting>

  Ändern Sie den Wert für die Einstellung *FairFaxAuthorityResource* in „https://login.microsoftonline.com/“.

  - **Original:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>&lt;/value>

    - **Bearbeitet:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>https://login.microsoftonline.com/&lt;/value>

2.  Nachdem Sie die Datei mit den zwei Änderungen gespeichert haben, starten Sie die Configuration Manager-Konsole auf demselben Computer neu, und installieren Sie anschließend den OMS-Connector über die Konsole. Verwenden Sie für die Installation des Connectors die Informationen in [Synchronisieren von Daten von System Center Configuration Manager mit der Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite), und wählen Sie den **Operations Management Suite-Arbeitsbereich** aus, der sich in der Microsoft Azure Government-Cloud befindet.

3.  Nach der erfolgreichen Installation des OMS-Connectors steht Ihnen die Verbindung zur Government-Cloud von jeder Konsole aus zur Verfügung, die sich mit dem Standort verbindet.
