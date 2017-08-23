---
title: "Funktionen in Technical Preview 1701 für Configuration Manager"
description: "Erfahren Sie mehr zu Funktionen, die in Technical Preview 1701 für System Center Configuration Manager zur Verfügung stehen."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b330c97a0853d1673f1cf7e0691891b72407fa51
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1701-for-system-center-configuration-manager"></a>Funktionen in Technical Preview 1701 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Technical Preview)*



In diesem Artikel werden die Funktionen erläutert, die in Technical Preview 1701 für System Center Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen, und zu erfahren, wie Sie Updates zwischen Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.    


**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>Verbesserungen bei Begrenzungsgruppen für Softwareupdatepunkte
Ab dieser Preview-Version verwenden Sie Begrenzungsgruppen, um Clients Softwareupdatepunkten zuzuordnen. Dies ist Teil der Bestrebungen, die Änderungen an Begrenzungsgruppen auszuweiten, sodass Begrenzungsgruppen zusätzliche Standortsystemrollen verwalten können.  Die ersten Änderungen an Begrenzungsgruppen wurden in Technical Preview 1609 und der Current Branch-Version 1610 eingeführt.  

In dieser Preview-Version können Sie das neue Verhalten der Begrenzungsgruppe nutzen, um zu verwalten, welche Softwareupdatepunkte ein Client verwenden kann. Dabei gehen Sie ähnlich vor wie bei der Verwaltung der von einem Client nutzbaren Verteilungspunkte:  

- Sie konfigurieren Begrenzungsgruppen, um einen oder mehrere Server zuzuordnen, die einen Softwareupdatepunkt hosten.
- Clients, die einen neuen Softwareupdatepunkt suchen, werden versuchen, einen Punkt zu verwenden, der ihrer aktuellen Begrenzungsgruppe zugeordnet ist.
- Wenn ein Client seinen aktuellen Softwareupdatepunkt nicht erreicht und auch in seiner aktuellen Begrenzungsgruppe keinen Softwareupdatepunkt findet, verwendet er ein Fallbackverhalten, um den Pool der zur Verfügung stehenden Softwareupdatepunkte zu erweitern.    

Weitere Informationen zu Begrenzungsgruppen finden Sie unter [Begrenzungsgruppen](/sccm/core/servers/deploy/configure/boundary-groups) in der Hilfe für die Current Branch-Version.

In dieser Preview sind die Begrenzungsgruppen für Softwareupdatepunkte jedoch nur teilweise implementiert. Sie können Softwareupdatepunkte hinzufügen und benachbarte Begrenzungsgruppen mit Softwareupdatepunkten konfigurieren, aber sie können die Fallbackzeit für Softwareupdatepunkte noch nicht ändern – d.h. es dauert zwei Stunden, bis ein Client einen Fallback einleitet.

Nachfolgend wird das Verhalten von Softwareupdatepunkten in dieser Technical Preview beschrieben:  

-   **Neue Clients verwenden Begrenzungsgruppen, um Softwareupdatepunkte auszuwählen.** Ein Client, den Sie nach der Installation von Version 1701 installieren, wählt einen Softwareupdatepunkt aus denjenigen aus, die der Begrenzungsgruppe des Clients zugeordnet sind.

  Dies ersetzt das vorherige Verhalten, bei dem die Clients zufällig einen Softwareupdatepunkt aus der Liste derer auswählten, die sich die Gesamtstruktur der Clients teilen.   

-   **Bereits installierte Clients verwenden so lange ihren aktuellen Softwareupdatepunkt, bis sie einen Fallback ausführen, um einen neuen zu finden.**
Bestehende Clients, die bereits über einen Softwareupdatepunkt verfügen, werden diesen weiterhin verwenden, bis sie einen Fallback ausführen. Dies betrifft auch Softwareupdatepunkte, die nicht der aktuellen Begrenzungsgruppe des Clients zugeordnet sind. Sie versuchen nicht sofort, in ihrer aktuellen Begrenzungsgruppe einen Softwareupdatepunkt zu suchen und diesen zu verwenden.

  Ein Client, der bereits über einen Softwareupdatepunkt verfügt, zeigt dieses neue Begrenzungsgruppenverhalten erst, nachdem er erfolglos versucht hat, seinen aktuellen Softwareupdatepunkt zu erreichen, und einen Fallback gestartet hat.
Der verzögerte Wechsel zu diesem neuen Verhalten ist Absicht. Dies liegt daran, dass der Wechsel eines Softwareupdatepunkts einen großen Teil der Netzwerkbandbreite in Anspruch nimmt, da der Client Daten mit dem neuen Softwareupdatepunkt synchronisiert. Die Verzögerung beim Übergang vermeidet eine Komplettauslastung Ihres Netzwerk, da nicht alle Ihre Clients gleichzeitig auf den neuen Softwareupdatepunkt wechseln.

-   **Konfigurationen der Fallbackzeit:** In dieser Technical Preview können Sie nicht konfigurieren, wann ein Client einen Fallback ausführen soll, um nach einem neuen Softwareupdatepunkt zu suchen. Dazu zählen auch die Konfigurationen für **Fallback times (in minutes)** (Fallbackzeit (in Minuten)) und **Never fallback** (Niemals einen Fallback ausführen), die Sie möglicherweise für andere Begrenzungsgruppenbeziehungen konfigurieren möchten.

  Die Clients behalten stattdessen ihr aktuelles Verhalten bei, d.h. sie versuchen zwei Stunden lang, sich mit ihrem aktuellen Softwareupdatepunkt zu verbinden, bevor Sie einen Fallback ausführen, um einen anderen verfügbaren Softwareupdatepunkt zu finden.

  Wenn ein Client die Fallbackfunktion verwendet, greift er auf die Begrenzungsgruppenkonfigurationen für den Fallback zurück, um einen Pool verfügbarer Softwareupdatepunkte zu erstellen. Dieser Pool enthält alle Softwareupdatepunkte der *aktuellen Begrenzungsgruppe*, der *benachbarten Begrenzungsgruppe* und der *standardmäßigen Standortbegrenzungsgruppe* des Clients.

- **Konfigurieren der standardmäßigen Standortbegrenzungsgruppe:**  
 Ziehen Sie in Erwägung, einen Softwareupdatepunkt zu *Default-Site-Boundary-Group&lt;Standortcode>* hinzuzufügen. Dadurch können auch Clients, die nicht Mitglieder einer anderen Begrenzungsgruppe sind, einen Fallback ausführen, um einen Softwareupdatepunkt zu suchen.


Verwenden Sie zum Verwalten von Softwareupdatepunkten die [Prozeduren aus der Dokumentation zur Current Branch-Version](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#procedures-for-boundary-groups), aber denken Sie daran, dass ggf. konfigurierte Fallbackzeiten noch nicht auf Softwareupdatepunkte angewendet werden.


## <a name="hardware-inventory-collects-uefi-information"></a>Die Hardwareinventur sammelt UEFI-Informationen
Ihnen stehen eine neue Hardwareinventurklasse (**SMS_Firmware**) und eine neue Eigenschaft (**UEFI**) zur Verfügung, mit der Sie bestimmen können, ob ein Computer im UEFI-Modus startet. Wenn ein Computer im UEFI-Modus gestartet wird, ist die Eigenschaft **UEFI** auf **TRUE** festgelegt. Dies ist bei der Hardwareinventur standardmäßig aktiviert. Weitere Informationen zur Hardwareinventur finden Sie unter [How to configure hardware inventory (Konfigurieren der Hardwareinventur)](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="improvements-to-operating-system-deployment"></a>Verbesserungen bei der Betriebssystembereitstellung
Basierend auf dem Feedback von Benutzern haben wir die folgenden Verbesserungen an der Betriebssystembereitstellung vorgenommen.
- [**Unterstützung einer größeren Zahl von Anwendungen für den Tasksequenzschritt „Anwendungen installieren“**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t): Im Tasksequenzschritt **Anwendungen installieren** können Sie nun bis zu 99 Anwendungen installieren. Vorher war maximal die Installation von neun Anwendungen möglich.
- [**Auswählen mehrerer Apps im Tasksequenzschritt „Apps installieren“**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step): Wenn Sie im Tasksequenz-Editor Anwendungen zum Tasksequenzschritt „Apps installieren“ hinzufügen, können Sie im Bereich **Zu installierende Anwendung auswählen** nun mehrere Anwendungen hinzufügen.
- [**Gültigkeitszeitraum für eigenständige Medien**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media): Beim Erstellen eines eigenständigen Mediums stehen Ihnen nun neue Optionen zur Verfügung, mit denen Sie optional den Beginn und das Ende des Gültigkeitszeitraums dieses Mediums festlegen können. Standardmäßig sind diese Einstellungen deaktiviert. Vor der Ausführung des eigenständigen Mediums werden die Datums- und Zeitangaben für den Zeitraum mit der Systemzeit auf dem Computer verglichen. Wenn die Systemzeit vor der Startzeit oder hinter der Ablaufzeit liegt, wird das eigenständige Medium nicht gestartet. Diese Optionen sind auch über das PowerShell-Cmdlet „New-CMStandaloneMedia“ verfügbar.
- [**Unterstützung für zusätzlichen Inhalt in eigenständigen Medien**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic): In eigenständigen Medien wird nun zusätzlicher Inhalt unterstützt. Wählen Sie Pakete, Treiberpakete und Anwendungen aus, die auf den Medien zusätzlich zum anderen Inhalt bereitgestellt werden sollen, auf den in der Tasksequenz verwiesen wird. Bisher wurde nur der Inhalt auf eigenständigen Medien bereitgestellt, auf den in der Tasksequenz verwiesen wurde.
- [**Konfigurierbares Timeout für den Tasksequenzschritt „Treiber automatisch anwenden“**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout): Ihnen stehen im Tasksequenzschritt „Treiber automatisch anwenden“ neue Tasksequenzvariablen für die Konfiguration des Timeoutwerts bei Anfragen gegenüber dem HTTP-Katalog zur Verfügung. Die folgenden Variablen und Standardwerte (in Sekunden) sind verfügbar:
   - SMSTSDriverRequestResolveTimeOut Default: 60
   - SMSTSDriverRequestConnectTimeOut Default: 60
   - SMSTSDriverRequestSendTimeOut Default: 60
   - SMSTSDriverRequestReceiveTimeOut Default: 480
- [**Anzeige der Paket-ID in Tasksequenzschritten**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste): Jeder Tasksequenzschritt, der auf ein Paket, ein Treiberpaket, ein Betriebssystemimage, ein Startimage oder ein Betriebssystem-Upgradepaket verweist, zeigt nun die Paket-ID des Objekts an, auf das verwiesen wird. Wenn in einem Tasksequenzschritt auf eine Anwendung verwiesen wird, wird die Objekt-ID angezeigt.
- **Nachverfolgung des Windows 10 ADK anhand der Buildversion**: Das Windows 10 ADK wird nun anhand der Buildversion nachverfolgt, um eine kontrollierte Anpassung von Windows 10-Startimages zu gewährleisten. Wird beispielsweise das Windows ADK für Windows 10 in der Version 1607 verwendet, so können nur Startimages mit Version 10.0.14393 in der Konsole angepasst werden. Ausführliche Informationen zum Anpassen von WinPE-Versionen finden Sie unter [Startimages anpassen](/sccm/osd/get-started/customize-boot-images).
- **Quellpfad des Standard-Startimages nicht mehr änderbar**: Standard-Startimages werden von Configuration Manager verwaltet, und ihr Quellpfad kann nicht mehr über die Configuration Manager-Konsole oder über das Configuration Manager SDK geändert werden. Sie können weiterhin einen benutzerdefinierten Quellpfad für benutzerdefinierte Startimages konfigurieren.

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>Hosten von Softwareupdates auf cloudbasierten Verteilungspunkten
Ab dieser Preview-Version können Sie Softwareupdatepakete auf cloudbasierten Verteilungspunkten hosten. Da Sie Ihre Clients jedoch so konfigurieren können, dass Softwareupdates direkt von Microsoft Update heruntergeladen werden, sollten Sie bedenken, dass durch die Bereitstellung eines Softwareupdatepakets auf einem cloudbasierten Verteilungspunkt zusätzliche Kosten anfallen können.

Weitere Informationen zur Verwendung von cloudbasierten Verteilungspunkten finden Sie unter [Verwenden eines cloudbasierten Verteilungspunkts](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) in der Hilfe für die Current Branch-Version von Configuration Manager.

## <a name="validate-device-health-attestation-data-via-management-points"></a>Daten zum Nachweis der Geräteintegrität über Verwaltungspunkte überprüfen

Ab dieser Preview-Version können Sie Verwaltungspunkte so konfigurieren, dass damit für den cloudbasierten oder lokalen Dienst zum Integritätsnachweis Berichtsdaten zum Nachweis der Geräteintegrität überprüft werden können. Über die neue Registerkarte **Erweiterte Optionen** im Dialogfeld **Eigenschaften für Verwaltungspunktkomponenten** können Sie die **URL des lokalen Diensts zum Nachweis der Geräteintegrität** **Hinzufügen**, **Bearbeiten** oder **Entfernen**. Sie können auch **Benutzerdefinierte Geräteeinstellungen** für den Client-Agent angeben, für den die Einstellung **Use on-premises Health Attestation Service** (Lokalen Dienst zum Integritätsnachweis verwenden) verwendet werden soll.  Wenn Sie diese Einstellung auf **Ja** setzen, können Berichte statt an den cloudbasierten Dienst auch an den lokalen Verwaltungspunkt gesendet werden.

### <a name="try-it-out"></a>Probieren Sie es aus

- **Aktivieren des lokalen Integritätsnachweises für Geräte auf einem Verwaltungspunkt**<br>  Navigieren Sie in der Configuration Manager-Konsole zum Verwaltungspunkt, öffnen Sie **Eigenschaften für Verwaltungspunktkomponenten**, und klicken Sie anschließend auf die Registerkarte **Erweiterte Optionen**. Klicken Sie auf **Hinzufügen**, und geben Sie unter **On-premises device health attestation service URLs** (URLs des lokalen Dienst zum Integritätsnachweis) die lokale URL ein (z.B. https://10.10.10.10).
- **Aktivieren der Berichterstattung über Integritätsnachweise an den lokalen Verwaltungspunkt für den Client-Agent** <br>Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Clienteinstellungen** aus, und klicken Sie doppelt auf **benutzerdefinierte Geräteeinstellungen**, oder legen Sie sie ggf. erst fest. Wählen Sie **Computer-Agent** aus, und legen Sie die Einstellung **Use on-premises Health Attestation Service** (Lokalen Dienst zum Integritätsnachweis verwenden) auf **Ja** fest. Wenn die Einstellung **Enable communication with Device Health Attestation Service** (Kommunikation mit dem Dienst zum Nachweis der Geräteintegrität zulassen) auf **Ja** und die Einstellung **Use on-premises Health Attestation Service** (Lokalen Dienst zum Integritätsnachweis verwenden) auf **Nein** festgelegt ist, wird der Verwaltungspunkt den cloudbasierten Dienst zum Nachweis der Geräteintegrität verwenden.

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>Verwenden des OMS-Connectors für die Microsoft Azure Government-Cloud
Ab dieser Technical Preview können Sie den OMS-Connector (Microsoft Operations Management) verwenden, um eine Verbindung mit einem OMS-Arbeitsbereich herzustellen, der sich in der Microsoft Azure Government-Cloud befindet.  

Hierzu bearbeiten Sie eine Konfigurationsdatei, damit sie auf die Government-Cloud zeigt, und installieren anschließend den OMS-Connector.

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>Einrichten eines OMS-Connectors für die Microsoft Azure Government-Cloud
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

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Android- und iOS-Versionen werden nicht mehr über den Erstellungsassistenten für hybrides MDM erreicht

Ab dieser Technical Preview für hybride mobile Geräteverwaltung (MDM) müssen Sie nicht mehr bestimmte Android- und iOS-Versionen auswählen, wenn Sie neue Richtlinien und Profile für mit Intune verwaltete Geräte erstellen wollen. Stattdessen wählen Sie einen der folgenden Gerätetypen aus:

- Android
- Samsung KNOX Standard 4.0 und höher
- iPhone
- iPad

Diese Änderung wirkt sich auf den Assistenten beim Erstellen der folgenden Elemente aus:

- Konfigurationselemente
- Kompatibilitätsrichtlinien
- Zertifikatprofile
- E-Mail-Profile
- VPN-Profile
- WLAN-Profile

Durch diese Änderung können Hybridbereitstellungen schneller neue Android und iOS-Versionen unterstützen, ohne eine neue Configuration Manager-Version oder -Erweiterung zu benötigen. Sobald eine neue Version in Intune standalone unterstützt wird, können Benutzer ihre mobilen Geräte auf diese Version upgraden.

Um Probleme beim Upgrade von vorherigen Configuration Manager-Versionen zu vermeiden, kann auf andere Versionen des mobilen Betriebssystems den Eigenschaftsseiten für diese Elemente zugegriffen werden. Sollten Sie nur auf eine bestimmte Version abzielen, können Sie das neue Element erstellen und diesem dann auf dessen Eigenschaftsseite eine bestimmte Version zuweisen.
