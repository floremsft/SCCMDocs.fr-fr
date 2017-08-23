---
title: Upgrade Readiness | System Center Configuration Manager
description: "Integrieren Sie Upgrade Readiness mit Configuration Manager. Greifen Sie auf Daten zur Upgradekompatibilität in Ihrer Administratorkonsole zu. Führen Sie Upgrades oder Wartungen von Geräten aus."
keywords: 
author: mattbriggs
ms.author: mabrigg
manager: angerobe
ms.date: 7/31/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: b1f4cd4a6f19a02d2b2dc3f9a841aeeb2a1403dd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>Integrieren von Upgrade Readiness mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit Upgrade Readiness (ehemals Upgrade Analytics) können Sie die Gerätebereitschaft unter Windows 10 bewerten und analysieren. Integrieren Sie Upgrade Readiness mit Configuration Manager, um auf Daten zur Kompatibilität von Clientupgrades in der Configuration Manager-Verwaltungskonsole zuzugreifen. Dort können Sie auch Geräte aus der Geräteliste für ein Upgrade oder Wartungsaufgaben auswählen.

Upgrade Readiness ist eine Lösung in der Microsoft Operations Management Suite (OMS). Erfahren Sie mehr über Upgrade Readiness in [Get started with Upgrade Readiness (Erste Schritte mit Upgrade Readiness)](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).

## <a name="configure-clients"></a>Konfigurieren von Clients

Es gibt mehrere Konfigurationsschritte, die Sie durchführen müssen, um sicherzustellen, dass Ihre Clients für Upgrade Readiness Daten bereitstellen können:

-  Konfigurieren Sie Clienttelemetrieeinstellungen wie unter [Konfigurieren der Windows-Telemetrie in Ihrem Unternehmen](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization) beschrieben.
-  Installieren Sie die KB-Artikel, die im Abschnitt *Deploy the compatibility update and related KBs (Bereitstellen der Kompatibilitätsaktualisierung und entsprechende KB-Artikel)* des Themas [Get started with Upgrade Readiness (Erste Schritte mit Upgrade Readiness)](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness) beschrieben werden.

    > [!NOTE]
    > Sie können ein Skript zur Automatisierung vieler Clientsetupaufgaben herunterladen. Weitere Informationen zu diesem Skript finden Sie im Abschnitt *Run the Upgrade Readiness deployment script (Ausführen des Bereitstellungsskripts für Upgrade Readiness)* des Themas [Get started with Upgrade Readiness (Erste Schritte mit Upgrade Readiness)](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).

## <a name="connect-to-upgrade-readiness"></a>Verbinden mit Upgrade Readiness

### <a name="prerequisites"></a>Voraussetzungen

Ab der Current Branch-Version 1706 kommt der Assistent für Azure-Dienste zum Einsatz, um die Konfiguration der von Ihnen verwendeten Azure-Dienste mit Configuration Manager zu vereinfachen. Um den Assistenten verwenden zu können, müssen Sie eine Azure-Web-App konfigurieren. Weitere Informationen finden Sie unter [Assistent für Azure-Dienste](/sccm/core/servers/deploy/configureazure-services-wizard).

### <a name="use-the-azure-wizard-to-create-the-connection"></a>Verwenden des Assistenten für Azure-Dienste zum Erstellen der Verbindung

1.  Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** den Eintrag **Clouddienste**, und klicken Sie dann auf **Azure-Dienste**.
2.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Azure-Dienste** auf **Azure-Dienste konfigurieren**.
3.  Geben Sie einen Namen auf der Seite "Azure-Dienste" ein. Sie können auch eine Beschreibung eingeben. Wählen Sie dann **Connector für Upgradebereitschaft**, und klicken Sie auf **Weiter**.
4.  Geben Sie Ihre Azure-Umgebung auf der Seite "App" an. Klicken Sie auf **Durchsuchen**, um eine Server-App einzurichten.
5.  Klicken Sie auf **Importieren**, um sich mit Ihrer Web-App in Azure zu verbinden.
    -  Geben Sie den **Namen des Azure AD-Mandanten** ein.
    -  Geben Sie die **ID des Azure AD-Mandanten** ein.
    -  Geben Sie den **Anwendungsnamen** ein.
    -  Geben Sie die **Client-ID** ein.
    -  Geben Sie den **geheimen Schlüssel** ein.
    -  Wählen Sie das Datum für den **Ablauf des geheimen Schlüssels** aus.
    -  Geben Sie eine URL für die **Anwendungs-ID-URI** ein.
    -  Klicken Sie auf **Überprüfen**und dann auf **OK**.

6.  Geben Sie auf der Seite "Konfiguration" die Verbindung mit Upgradebereitschaft an. Legen Sie die folgenden Werte fest:  
    -  Azure-Abonnements
    -  Azure-Ressourcengruppe
    -  Windows Analytics-Arbeitsbereich
8.  Klicken Sie auf **Weiter**. Sie können die Verbindung auf der Seite "Zusammenfassung" überprüfen. 

## <a name="complete-upgrade-readiness-tasks"></a>Abschließen von Upgrade Readiness-Aufgaben  

Nachdem Sie die Verbindung erstellt haben, können Sie diese Aufgaben wie unter [Get started with Upgrade Readiness (Erste Schritte mit Upgradebereitschaft)](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness) beschrieben ausführen.  

1. Fügen Sie dem OMS-Arbeitsbereich den Upgrade Readiness-Dienst hinzu.  
2. Generieren Sie eine kommerzielle ID.  
3. Abonnieren Sie Upgrade Readiness.   

## <a name="use-the-upgrade-readiness-deployment-script"></a>Verwenden des Bereitstellungsskripts von Upgrade Readiness  

Sie können zahlreiche Aufgaben von Upgrade Readiness über das Microsoft **Upgrade Readiness deployment script (Upgrade Readiness-Bereitstellungsskript)** automatisieren sowie Probleme mit der Freigabe von Daten lösen.  
Das Bereitstellungsskript von Upgrade Readiness bietet folgende Möglichkeiten:  

- Legt den kommerziellen ID-Schlüssel und die Schlüssel „CommercialDataOptIn“ + „RequestAllAppraiserVersions“ fest  
- Stellt sicher, dass Computernutzer für Microsoft Daten bereitstellen können  
- Überprüft, ob für den Computer ein Neustart aussteht   
- Stellt sicher, dass die neueste Version des 10.0.x-Pakets der KB installiert ist (10.0.14913 oder nachfolgenden Versionen erforderlich).  
- Aktiviert den ausführlichen Modus zur Problembehandlung (sofern aktiviert)  
- Initiiert die Sammlung von Telemetriedaten, die Microsoft für die Bewertung der Upgradebereitschaft Ihres Unternehmens benötigt  
- Zeigt, wenn aktiviert, den Fortschritt des Skripts in einem Befehlszeilenfenster an. So werden Sie über erfolgreiche oder fehlgeschlagene Schritte informiert, und/oder es wird in die Protokolldatei geschrieben.  

## <a name="to-run-the-upgrade-readiness-deployment-script"></a>So führen Sie das Upgrade Readiness-Bereitstellungsskript aus:  

1. Laden Sie das [Upgrade Readiness deployment script (Upgrade Readiness-Bereitstellungsskript)](https://go.microsoft.com/fwlink/?LinkID=822966&clcid=0x409) herunter, und extrahieren Sie die Datei „UpgradeReadiness.zip“. Die Dateien im Ordner **Diagnostics** sind nur dann erforderlich, wenn Sie das Skript im Problembehandlungsmodus ausführen möchten.  
2. Bearbeiten Sie diese Parameter in „RunConfig.bat“:  
- Speicherort für Protokollinformationen. Beispiel: %SystemDrive%\URDiagnostics. Sie können die Protokollinformationen auf einer Remotedateifreigabe oder in einem lokalen Verzeichnis speichern. Wenn das Skript die Protokolldatei für den angegebenen Pfad nicht erstellen kann, werden die Protokolldateien auf dem Laufwerk mit dem Windows-Verzeichnis erstellt.  
- Kommerzieller ID-Schlüssel  
- Standardmäßig sendet das Skript die Protokollinformationen in die Konsole und die Protokolldatei. Verwenden Sie eine der folgenden Optionen, um das Standardverhalten zu ändern:  
    - logMode = 0 Protokoll, nur in die Konsole  
    - logMode = 1 Protokoll, in die Datei und die Konsole  
    - logMode = 2 Protokolle, nur in die Datei  
    - Setzen Sie für die Problembehandlung den Eintrag **IsVerboseLogging** auf **$true**, um Protokollinformationen zu generieren, die bei der Diagnose von Problemen hilfreich sein können. Der Eintrag **IsVerboseLogging** ist standardmäßig auf **$false** eingestellt. Vergewissern Sie sich, dass der Diagnoseordner im gleichen Verzeichnis installiert ist wie das Skript, das diesen Modus verwendet.  
    - Benachrichtigen Sie Benutzer, wenn sie ihren Computer neu starten müssen. Diese Eigenschaft ist standardmäßig nicht aktiviert.  

3. Nachdem Sie die Parameter in „RunConfig.bat“ bearbeitet haben, führen Sie das Skript als Administrator an.  


## <a name="view-microsoft-upgrade-readiness-properties-in-configuration-manager"></a>Anzeigen der Eigenschaften von Microsoft Upgrade Readiness in Configuration Manager  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Cloud Services**, und wählen Sie **OMS Connector** (OMS-Connector) aus, um die Seite **OMS Connection Properties** (OMS-Verbindungseigenschaften) zu öffnen.  

2.  Auf dieser Seite befinden sich zwei Registerkarten:
  * Die Registerkarte **Azure Active Directory** zeigt **Mandant**, **Client-ID**, **Client secret key expiration** (Ablauf des geheimen Clientschlüssels) an und ermöglicht Ihnen zu **Überprüfen**, ob **Geheimer Clientschlüssel** abgelaufen ist.
  * Die Registerkarte **Upgrade Readiness** zeigt Ihr **Azure-Abonnement**, die **Azure-Ressourcengruppe** und den **Operations Management Suite-Arbeitsbereich** an.

## <a name="view-and-use-the-upgrade-information"></a>Anzeigen und verwenden der Upgradeinformationen

Nachdem Sie Upgrade Readiness mit Configuration Manager integriert haben, können Sie die Analyse der Upgradebereitschaft Ihrer Clients anzeigen und entsprechende Maßnahmen ergreifen.

1. Wählen Sie in der Configuration Manager-Konsole die Optionen **Überwachung** > **Übersicht** > **Upgrade Readiness** aus.
2. Überprüfen Sie die Daten, einschließlich des Status der Upgradebereitschaft und des Prozentsatzes an Windows-Geräten, die Telemetriedaten melden.
3. Sie können das Dashboard zum Anzeigen von Daten für Geräte in bestimmten Sammlungen filtern.
4. Sie können Geräte in einem bestimmten Upgradebereitschaftsstatus anzeigen und eine dynamische Sammlung für sie erstellen. Wenn die Geräte dazu bereit sind, können Sie ein Upgrade ausführen oder entsprechende Maßnahmen ergreifen, um sie in den passenden Bereitschaftsstatus zu versetzen.

## <a name="create-a-connection-to-upgrade-readiness-1702-and-earlier"></a>Erstellen einer Verbindung mit Upgradebereitschaft (1702 und früher)

Vor der Branch-Version 1706 von Configuration Manager waren folgende Schritte erforderlich, um eine Verbindung mit Upgradebereitschaft herzustellen.

### <a name="prerequisites"></a>Voraussetzungen

- Um der Configuration Manager-Umgebung eine Verbindung hinzuzufügen, müssen Sie zunächst einen [Dienstverbindungspunkt](/sccm/core/servers/deploy/configure/about-the-service-connection-point) in einem [Onlinemodus](https://azure.microsoft.com/documentation/articles/resource-group-create-service-principal-portal/) konfigurieren. Wenn Sie Ihrer Umgebung eine Verbindung hinzufügen, wird auch der Microsoft Monitoring Agent auf dem Computer installiert, auf dem die Standortsystemrolle ausgeführt wird.
- Registrieren Sie Configuration Manager als „Webanwendung und/oder Web-API”-Verwaltungstool, und rufen Sie die [Client-ID dieser Registrierung](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/) ab.
- Erstellen Sie für das registrierte Verwaltungstool in Azure Active Directory einen Clientschlüssel.
- Geben Sie der registrierten Web-App im Azure-Portal Zugriff auf OMS, wie unter [Bereitstellen von Configuration Manager mit Berechtigungen für OMS](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms) beschrieben.

    > [!IMPORTANT]
    > Achten Sie beim Konfigurieren der OMS-Zugriffsberechtigung darauf, dass Sie die Rolle **Mitwirkender** auswählen, und weisen Sie ihr Berechtigungen für die Ressourcengruppe der registrierten App zu.

### <a name="create-the-connection"></a>Erstellen der Verbindung

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Clouddienste** > **Upgrade Readiness Connector** > **Verbindung mit Upgrade Analytics erstellen** aus, um den **Assistent für das Hinzufügen einer Upgrade Analytics-Verbindung** zu starten.
3.  Geben Sie auf dem Bildschirm **Azure Active Directory** zunächst den **Mandanten**, die **Client-ID** und den **geheimen Clientschlüssel** ein, und wählen Sie anschließend **Weiter** aus.
4.  Geben Sie auf dem Bildschirm **Upgrade Readiness** die Verbindungseinstellungen ein, indem Sie Ihr **Azure-Abonnement**, die **Azure-Ressourcengruppe** und den **Operations Management Suite-Arbeitsbereich** angeben.
5.  Überprüfen Sie die Verbindungseinstellungen auf dem Bildschirm **Zusammenfassung**, und wählen Sie dann **Weiter** aus.

    > [!NOTE]
    > Sie müssen Upgrade Readiness mit dem Standort der obersten Ebene in der Hierarchie verbinden. Wenn Sie Upgrade Readiness mit einem eigenständigen primären Standort verbinden und dann Ihrer Umgebung einen Standort der zentralen Verwaltung hinzufügen, müssen Sie die OMS-Verbindung in der neuen Hierarchie löschen und neu erstellen.
