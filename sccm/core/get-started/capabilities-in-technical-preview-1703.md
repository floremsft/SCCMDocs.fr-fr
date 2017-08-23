---
title: "Funktionen in Technical Preview 1703 für Configuration Manager"
description: "Erfahren Sie mehr über die Funktionen, die mit Technical Preview für System Center Configuration Manager, Version 1703, zur Verfügung stehen."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: bb1b96a56db68dcea22270855b899ba3a90afd0d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1703-for-system-center-configuration-manager"></a>Funktionen in Technical Preview 1703 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Technical Preview)*

In diesem Artikel werden die Funktionen erläutert, die in Technical Preview für System Center Configuration Manager, Version 1703, zur Verfügung stehen. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen, und zu erfahren, wie Sie Updates zwischen Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.    


**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Bereitstellen per Volumenlizenz erworbener iOS-Apps in Gerätesammlungen

Sie können jetzt sowohl Geräten als auch Benutzern lizenzierte Apps bereitstellen. Je nachdem, inwieweit die App Gerätelizenzierungen unterstützt, wird eine entsprechende Lizenz wie folgt beansprucht:

|||||
|-|-|-|-|
|Configuration Manager-Version|Unterstützt die App Gerätelizenzierung?|Typ der Bereitstellungssammlung|Beanspruchte Lizenz|
|Früher als 1702|Ja|Benutzer|Benutzerlizenz|
|Früher als 1702|Nein|Benutzer|Benutzerlizenz|
|Früher als 1702|Ja|Gerät|Benutzerlizenz|
|Früher als 1702|Nein|Gerät|Benutzerlizenz|
|1702 und höher|Ja|Benutzer|Benutzerlizenz|
|1702 und höher|Nein|Benutzer|Benutzerlizenz|
|1702 und höher|Ja|Gerät|Gerätelizenz|
|1702 und höher|Nein|Gerät|Benutzerlizenz|

Weitere Informationen zu iOS-Apps, die über ein Volumenprogramm erworben wurden, finden Sie unter [Verwalten von iOS-Apps, die über ein Volumenprogramm erworben wurden](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

## <a name="direct-links-to-applications-in-software-center"></a>Direkte Links zu Anwendungen im Softwarecenter

Sie können jetzt Endbenutzern einen direkten Link zu einer Anwendung im Softwarecenter bereitstellen. Dies bedeutet, dass sie nicht mehr das Softwarecenter öffnen und nach einer Anwendung suchen müssen, bevor Sie sie installieren können. Dies ist nur für Configuration Manager-Anwendungen verfügbar, nicht für Pakete und Programme oder Tasksequenzen.

### <a name="try-it-out"></a>Probieren Sie es aus                 

Verwenden Sie das folgende URL-Format, um das Softwarecenter für eine bestimmte Anwendung zu öffnen:

**Softwarecenter:SoftwareId=*Application Identifier***

### <a name="how-to-get-the-application-identifier-of-an-application"></a>So rufen Sie den Anwendungsbezeichner einer Anwendung ab

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.
2.  Erweitern Sie im Arbeitsbereich „Softwarebibliothek“ den Knoten **Anwendungsverwaltung**, und klicken Sie dann auf **Anwendungen**.
3.  Klicken Sie mit der rechten Maustaste in der Ansicht **Anwendungen** auf eine der Spaltenüberschriften, und wählen Sie anschließend **Eindeutige CI-ID** aus der Liste aus. Sie sehen, dass die eindeutige ID jeder Anwendung jetzt in der Liste angezeigt wird.
4.  Beachten Sie die **Eindeutige CI-ID** der Anwendung, für die Sie einen Link bereitstellen möchten, z.B.: **ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2**.
5.  Entfernen Sie dann den Text, der auf die Anwendungs-GUID folgt. In diesem Fall ist es **/2**. Dadurch bleibt der Anwendungsbezeichner übrig.
6.  Um die Erstellung des Links abzuschließen, stellen Sie ihr **Softwarecenter:SoftwareID=** voran. Mit dem obigen Beispiel sieht der schlussendliche Link folgendermaßen aus: **Softwarecenter:SoftwareId= ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**.

Mithilfe dieses Links können Endbenutzer Softwarecenter direkt für die von Ihnen angegebene Anwendung öffnen.


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>PFX-Zertifikate für Configuration Manager-Windows-Clientcomputer

Sie können nun PFX-Zertifikatprofile bereitstellen, die Sie für Configuration Manager-Clientcomputer unter Windows 10 importiert haben.

### <a name="try-it-out"></a>Probieren Sie es aus

Verwenden Sie die Anweisungen unter [Erstellen von PFX-Zertifikatprofilen](/sccm/mdm/deploy-use/create-pfx-certificate-profiles), um ein PFX-Profil zu importieren, das Profil bereitzustellen, und dann zu überprüfen, ob das Zertifikat für den Zielbenutzer installiert wurde.



## <a name="configure-azure-services-wizard"></a>Konfigurieren des Azure Dienste-Assistenten
Technical Preview 1703 führt den Assistenten **zum Konfigurieren von Azure-Diensten** ein. Dieser Assistent bietet eine allgemeine Konfigurationserfahrung, die die einzelnen Workflows mit den Clouddiensten ersetzt, die Sie mit Configuration Manager verwenden. Dies erfolgt mithilfe einer **Azure Web-App**, um das Abonnement und Konfigurationsdetails bereitzustellen, die Sie andernfalls jedes Mal eingeben müssen, wenn Sie eine neue Configuration Manager-Komponente oder einen -Dienst mit Azure einrichten.

Mit Technical Preview 1703 wird nur Windows Store for Business (WSfB) mit diesem Assistenten konfiguriert.  Andere Clouddienste werden mithilfe ihrer eigenen Workflows konfiguriert.

-   Verwenden Sie die Informationen in diesem Preview-Thema, um die Konfigurationsschritte im Abschnitt [Einrichten der Synchronisierung mit Windows Store für Unternehmen](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#set-up-windows-store-for-business-synchronization) des Current Branch-Themas [Verwalten von Apps aus dem Windows Store für Unternehmen mit System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) zu ersetzen.

-   Weitere Informationen zu Web-Apps, finden Sie unter [Authentifizierung und Autorisierung in Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview), und [Web-Apps – Übersicht](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

### <a name="prerequisites-and-planning"></a>Erforderliche Komponenten und Planung
Wenn Sie eine Verbindung zwischen Configuration Manager und dem Windows Store für Unternehmen herstellen, müssen Sie einen Ordner angeben, in dem App-Inhalte, die aus dem Store synchronisiert werden, gespeichert werden. Um sicherzustellen, dass es sich um einen sicheren Ordner handelt, und dass der Inhalt auf Geräten bereitgestellt werden kann, müssen Sie sichergehen, dass die folgenden Berechtigungen vorhanden sind:
-   Der Computer, auf dem Sie die Standortsystemrolle „Dienstverbindungspunkt“ installieren (der Standort der obersten Ebene in der Hierarchie), muss über Lese- und Schreibberechtigungen für den Ordner verfügen, den Sie bei der Verwendung des Kontos **Computer$** angegeben haben.  

-   Der Autor der App muss über Leseberechtigungen für den angegebenen Ordner verfügen.  

-   Das Konto **Computer$** jedes Computers, der eine Instanz des SMS-Anbieters hostet, muss den angegebenen Ordner verwenden können.

Registrieren Sie Configuration Manager über Webanwendung oder Web-API als Verwaltungstool in Azure Active Directory. Dadurch kann die Client-ID erstellt werden, die Sie später benötigen werden.

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>Verwenden des Assistenten zum Konfigurieren des WSfB-Clouddiensts

1. Wechseln Sie in der Konsole zu **Verwaltung** > **Übersicht** > **Cloud Services Management** (Verwaltung der Clouddienste) > **Azure** > **Azure-Dienste**, und wählen Sie dann **Configure Azure Services** (Azure-Dienste konfigurieren) aus, um den **Azure-Dienste-Assistenten** zu starten.

2. Wählen Sie auf der Seite **Azure-Dienste** den Dienst aus, den Sie konfigurieren möchten, und klicken Sie dann auf **Weiter**. Mit dieser Vorschau kann nur WSfB konfiguriert werden.

3. Geben Sie auf der Seite **Allgemein** einen Anzeigenamen für den **Azure-Dienstnamen** und eine optionale Beschreibung ein, und klicken Sie dann auf **Weiter**.

4. Auf der **App** Seite geben Sie Ihre Azure-Umgebung an und klicken dann auf **Durchsuchen**, um das Fenster „Server-App“ zu öffnen.

5. Wählen Sie im Fenster **Server App** (Server-App) die Server-App aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.
Server-Apps sind Azure-Web-Apps, die Konfigurationen für Ihr Azure-Konto enthalten, einschließlich Ihrer Mandanten-ID, Client-ID und eines geheimen Schlüssels für Clients. Wenn Sie nicht über eine verfügbare Server-App verfügen, verwenden Sie eine der folgenden:
  - **Erstellen**: Um eine neue Server-App zu erstellen, klicken Sie auf **Erstellen**. Geben Sie einen Anzeigenamen für die App und den Mandanten an. Nachdem Sie sich bei Azure angemeldet haben, erstellt Configuration Manager daraufhin die Web-App in Azure für Sie, einschließlich der Client-ID und des geheimen Schlüssels für den Gebrauch mit der Web-App. Später können Sie diese im Azure-Portal anzeigen.
  - **Importieren**: Um eine Web-App zu verwenden, die in Ihrem Azure-Abonnement bereits vorhanden ist, klicken Sie auf **Importieren**. Stellen Sie einen Anzeigenamen für die App und den Mandanten bereit, und geben Sie dann die Mandanten-ID, Client-ID und den geheimen Schlüssel für die Web-App an, die Configuration Manager verwenden soll. Nachdem Sie die Informationen **überprüft** haben, klicken Sie auf **OK**, um fortzufahren.  </br></br>

6. Überprüfen Sie die Seite **Informationen**, und schließen Sie alle zusätzlichen Schritte und Konfigurationen so wie angegeben ab. Diese Konfigurationen sind erforderlich, um den Dienst mit Configuration Manager zu verwenden.
So konfigurieren Sie z.B. WSfB:

  1. In Azure müssen Sie Configuration Manager als eine Web-Anwendung oder eine Web-API registrieren und die Client-ID notieren. Außerdem geben Sie einen Clientschlüssel für die Verwendung durch das Verwaltungstool (das ist Configuration Manager) an.

  2.    In der WSfB-Konsole müssen Sie Configuration Manager als Speicherverwaltungstool angeben, Unterstützung für Offline-lizenzierte Apps aktivieren und anschließen mindestens eine App kaufen.   </br>

  Klicken Sie zum Fortfahren auf **Weiter**.

7. Schließen Sie auf der Seite **App Configurations** (App-Konfigurationen) die Konfigurationen für den App-Katalog und die Sprache für diesen Dienst ab, und klicken Sie dann auf **Weiter**.
8. Nach Abschluss des Assistenten zeigt die Configuration Manager-Konsole, dass Sie **Windows Store for Business** als **Clouddiensttyp** konfiguriert haben.

Jetzt können Sie den Rest des [Current Branch-Inhalts](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) für das Verwalten von Apps von WSfB zum Synchronisieren, Erstellen und Bereitstellen sowie zum Überwachen von Windows Store for Business-Apps verwenden.

### <a name="modify-a-cloud-service-configuration"></a>Ändern einer Clouddienstkonfiguration
Sie können die Eigenschaften eines Clouddiensts anzeigen und bearbeiten, um die Konfiguration zu ändern.

Wechseln Sie in der Konsole zu **Verwaltung** > **Übersicht** > **Cloud Services Management** (Verwaltung der Clouddienste) > **Azure** > **Azure-Dienste**, und wählen Sie dann **Configure Azure Services** (Azure-Dienste konfigurieren) au, wählen Sie einen Clouddienst aus und anschließend **Eigenschaften**.

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Konvertieren von BIOS zu UEFI während eines direkten Upgrades
Windows 10 Creators Update führt ein einfaches Konvertierungstool ein, womit der Prozess der Neupartitionierung der Festplatte für UEFI-aktivierte Hardware automatisiert werden kann und das Konvertierungstool in den direkten Upgradeprozess von Windows 7 zu Windows 10 integriert werden kann. Wenn Sie dieses Tool mit Ihrer Tasksequenz des Betriebssystemupgrades und dem OEM-Tool kombinieren, der die Firmware von BIOS zu UEFI konvertiert, können Sie Ihre Computer von BIOS zu UEFI während eines direkten Upgrades zu Windows 10 Creators Update konvertieren. Weitere Informationen finden Sie unter [Task sequence steps to manage BIOS to UEFI conversion (Tasksequenzschritte für das Verwalten einer Konvertierung von BIOS zu UEFI)](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

## <a name="collapsible-task-sequence-groups"></a>Reduzierbare Tasksequenzgruppen
Diese Version bietet die Möglichkeit zum Erweitern und Reduzieren von Tasksequenzgruppen. Sie können einzelne Gruppen erweitern oder reduzieren oder alle Gruppen auf einmal erweitern oder reduzieren.


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>Clienteinstellungen zum Konfigurieren von Windows Analytics für Upgrade Readiness
Ab dieser Version können Sie Clienteinstellungen für Geräte verwenden, um die Konfiguration der Windows-Telemetrie zu vereinfachen, die zur Verwendung von [Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics)-Lösungen wie z.B. [Upgradebereitschaft](/sccm/core/clients/manage/upgrade/upgrade-analytics) mit Configuration Manager erforderlich ist. Configuration Manager kann Daten aus Windows Analytics abrufen, die wertvolle Informationen über den aktuellen Zustand Ihrer Umgebung liefern. Diese Informationen basieren auf den Windows-Telemetriedaten, die von Ihren Clientcomputern gemeldet werden. Windows-Telemetriedaten werden von Clientcomputern an den Windows-Telemetriedienst gemeldet, und dann werden relevante Daten an Windows Analytics-Lösungen übertragen, die in einem der OMS-Arbeitsbereiche Ihrer Organisation gehostet werden. Die Upgradebereitschaft ist eine Windows Analytics-Lösung, die Sie bei der Priorisierung von Entscheidungen über Windows-Upgrades für Ihre verwalteten Geräte unterstützt.

Informationen zu Einstellungen für Windows-Telemetriedaten finden Sie unter [Konfigurieren der Windows-Telemetrie in Ihrem Unternehmen](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).

### <a name="prerequisites"></a>Voraussetzungen
- Sie müssen Ihren Standort zur Verwendung des Clouddiensts für die Upgradebereitschaft konfiguriert haben. Weitere Informationen finden Sie unter [Upgradebereitschaft](/sccm/core/clients/manage/upgrade/upgrade-analytics).

### <a name="configure-windows-analytics-client-settings"></a>Konfigurieren von Clienteinstellungen für Windows Analytics
Wechseln Sie zum Konfigurieren von Windows Analytics in der Configuration Manager-Konsole zu **Verwaltung** > **Clienteinstellungen**, doppelklicken Sie auf **Benutzerdefinierte Clienteinstellungen für Geräte erstellen**, und aktivieren Sie dann **Windows Analytics**.  

Wechseln Sie zur Registerkarte mit den Einstellungen für **Windows Analytics**, und konfigurieren Sie Folgendes:
- **Kommerzielle ID**  
Der Schlüssel „Kommerzielle ID“ ordnet Informationen der von Ihnen verwalteten Geräte zu dem OMS-Arbeitsbereich zu, der die Windows Analytics-Daten Ihrer Organisation hostet. Wenn Sie bereits einen kommerziellen ID-Schlüssel für die Verwendung mit der Upgradebereitschaft konfiguriert haben, verwenden Sie diese ID. Wenn Sie noch nicht über einen kommerziellen ID-Schlüssel verfügen, finden Sie weitere Informationen unter [Generieren des kommerziellen ID-Schlüssels]( https://technet.microsoft.com /itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

- Festlegen einer **Telemetriestufe für Windows 10-Geräte**   
Informationen darüber, was auf jeder Telemetriestufe von Windows 10 gesammelt wird, finden Sie unter [Konfigurieren der Windows-Telemetrie in Ihrem Unternehmen]( https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

- **Abonnieren Sie die Sammlung kommerzieller Daten auf Geräten unter Windows 7, 8 und 8.1**   
Informationen zu gesammelten Daten von diesen Betriebssystemen bei der Anmeldung, finden Sie in der PDF-Datei [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields (Appraiser-Telemetrieereignisse und -felder unter Windows 7, Windows 8 und 8.1)](https://go.microsoft.com/fwlink/?LinkID=822965).

- **Konfigurieren der Datensammlung von Internet Explorer**: Auf Geräten unter Windows 8.1 oder früher kann die Internet Explorer-Datensammlung es der Upgradebereitschaft ermöglichen, Inkompatibilitäten von Web-Apps zu erkennen, die ein reibungsloses Upgrade auf Windows 10 verhindern könnten. Die Internet Explorer-Datensammlung kann für einzelne Internetzonen aktiviert werden. Weitere Informationen zu Internetzonen finden Sie unter [About URL Security Zones](https://msdn.microsoft.com/en-us/library/ms537183(v=vs.85).aspx) (Informationen zu URL-Sicherheitszonen).