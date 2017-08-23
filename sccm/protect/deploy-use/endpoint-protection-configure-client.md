---
title: Konfigurieren des Endpoint Protection-Clients | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie benutzerdefinierte Clienteinstellungen für Endpoint Protection konfigurieren, die in der Computersammlung in Ihrer Hierarchie bereitgestellt werden können."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 1488aaa465fb9810bc1b641d41dad95189d37418
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Konfigurieren von benutzerdefinierten Clienteinstellungen für Endpoint Protection

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit diesem Verfahren können benutzerdefinierte Clienteinstellungen für Endpoint Protection konfiguriert werden, die dann auf eine Computersammlung in Ihrer Hierarchie bereitgestellt werden können.

> [!IMPORTANT]
>  Konfigurieren Sie die standardmäßige Endpoint Protection-Clienteinstellungen nur, wenn Sie sicher sind, dass diese Einstellungen auf alle Computer in Ihrer Hierarchie angewendet werden sollen.

## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>So aktivieren Sie Endpoint Protection und konfigurieren benutzerdefinierte Clienteinstellungen

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.

2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Clienteinstellungen**.

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Benutzerdefinierte Geräteclienteinstellungen erstellen**.

4.  Geben Sie im Dialogfeld **Benutzerdefinierte Geräteclienteinstellungen erstellen** einen Namen und eine Beschreibung für die Einstellungsgruppe ein, und wählen Sie dann **Endpoint Protection**aus.

5.  Konfigurieren Sie die Endpoint Protection-Clienteinstellungen, die Sie benötigen. Eine vollständige Liste von Endpoint Protection-Clienteinstellungen, die Sie konfigurieren können, finden Sie im Abschnitt [Clienteinstellungen in Configuration Manager](../../core/clients/deploy/about-client-settings.md).

   > [!IMPORTANT]
   >  Sie müssen die Endpoint Protection-Standortsystemrolle installieren, bevor Sie Clienteinstellungen für Endpoint Protection konfigurieren können.

6.  Klicken Sie auf **OK** , um das Dialogfeld **Benutzerdefinierte Geräteclienteinstellungen erstellen** zu schließen. Die neuen Clienteinstellungen erscheinen im Knoten **Clienteinstellungen** des Arbeitsbereichs **Verwaltung** .

7.  Bevor die benutzerdefinierten Clienteinstellungen verwendet werden können, müssen sie für eine Sammlung bereitgestellt werden. Wählen Sie die benutzerdefinierten Clienteinstellungen aus, die Sie bereitstellen möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Clienteinstellungen** auf **Bereitstellen**.

8.  Wählen Sie im Dialogfeld **Sammlung auswählen** die Sammlung aus, für die Sie die Clienteinstellungen bereitstellen möchten, und klicken Sie dann auf **OK**. Die neue Bereitstellung erscheint im Detailbereich auf der Registerkarte **Bereitstellungen** .

Die Clientcomputer werden beim nächsten Clientrichtliniendownload mit diesen Einstellungen konfiguriert. Zum Initiieren des Richtlinienabrufs für einen einzelnen Client lesen Sie den Abschnitt „Initiieren des Richtlinienabrufs für einen Configuration Manager-Client“ in [Clientverwaltung in System Center Configuration Manager](../../core/clients/manage/manage-clients.md).

## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image-in-configuration-manager"></a>Bereitstellen des Endpoint Protection-Clients in einem Datenträgerabbild in Configuration Manager
Sie können den Endpoint Protection-Client auf einem Computer installieren, den Sie als Datenträgerimagequelle für die Betriebssystembereitstellung von Configuration Manager verwenden möchten. Dieser Computer wird in der Regel als Referenzcomputer bezeichnet. Nach dem Erstellen des Betriebssystemimages können Sie das Image, das Softwarepakete wie End Protection enthalten kann, mithilfe der Configuration Manager-Betriebssystembereitstellung für Ihre Clientcomputer bereitstellen.

Mithilfe der Verfahren in diesem Thema können Sie den Endpoint Protection-Client auf einem Referenzcomputer installieren und konfigurieren

### <a name="prerequisites-for-installing-the-endpoint-protection-client-on-the-reference-computer"></a>Voraussetzungen für die Installation des Endpoint Protection-Clients auf dem Referenzcomputer
Die folgende Liste enthält die erforderlichen Voraussetzungen für die Installation der Endpoint Protection-Clientsoftware auf einem Referenzcomputer.

-   Sie benötigen Zugriff auf das Endpoint Protection-Clientinstallationspaket **scepinstall.exe**. Dieses Paket befindet sich im Ordner **Client** des Microsoft System Center Configuration Manager-Installationsordners auf dem Standortserver.

-   Erstellen Sie eine Richtlinie für Antischadsoftware, und exportieren Sie diese, um sicherzustellen, dass der Endpoint Protection-Client mit der für Ihre Organisation erforderlichen Konfiguration bereitgestellt wird. Bei der manuellen Installation des Endpoint Protection-Clients können Sie dann die zu verwendende Richtlinie für Antischadsoftware angeben. Weitere Informationen finden Sie unter [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md).

   > [!NOTE]
   >  Die **Standardclientrichtlinie für Antischadsoftware** kann nicht exportiert werden.

-   Wenn Sie den Endpoint Protection-Client mit den aktuellsten Definitionen installieren möchten, müssen Sie diese vom [Microsoft Malware Protection Center](http://go.microsoft.com/fwlink/?LinkID=200965) herunterladen.

### <a name="how-to-install-the-endpoint-protection-client-software-on-the-reference-computer"></a>Installieren der Endpoint Protection-Clientsoftware auf dem Referenzcomputer
Sie können den Endpoint Protection-Client über eine Eingabeaufforderung lokal auf dem Referenzcomputer installieren. Hierzu müssen Sie zunächst die Installationsdatei **scepinstall.exe**abrufen. Sie können den Client auch mit einer vorkonfigurierten Richtlinie für Antischadsoftware oder mit einer zuvor exportierten Richtlinie für Antischadsoftware installieren.

## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a>So installieren Sie den Endpoint Protection-Client über eine Eingabeaufforderung

1.  Kopieren Sie die Datei **scepinstall.exe** im Ordner **Client** auf dem System Center Configuration Manager-Installationsmedium auf den Computer, auf dem Sie die Endpoint Protection-Clientsoftware installieren möchten.

2.  Öffnen Sie eine Eingabeaufforderung mit Administratorberechtigungen, navigieren Sie zu dem Ordner, in dem sich die Datei **scepinstall.exe** befindet, und führen Sie dann den folgenden Befehl mit allen erforderlichen Befehlszeileneigenschaften aus:

   ```
   scepinstall.exe
   ```

    Sie können eine der folgenden Befehlszeileneigenschaften angeben:

   |Eigenschaft|Beschreibung|
   |--------------|-----------------|
   |/s|Hiermit wird angegeben, dass eine automatische Installation ausgeführt wird.|
   |/q|Hiermit wird angegeben, dass eine automatische Extraktion der Setup-Dateien ausgeführt wird.|
   |/i|Hiermit wird angegeben, dass eine normale Installation ausgeführt werden soll.|
   |/noreplace|Hiermit wird angegeben, dass Antischadsoftware von Drittanbietern beim Setup nicht deinstalliert wird.|
   |/policy|Hiermit wird die Datei mit der Richtlinie für Antischadsoftware angegeben, die bei der Installation zum Konfigurieren des Clients verwendet werden soll.|
   |/sqmoptin|Hiermit wird angegeben, dass diese Clientsoftwareinstallation für das Programm zur Verbesserung der Benutzerfreundlichkeit angemeldet wurde.|

3.  Befolgen Sie die Anweisungen auf dem Bildschirm, um die Clientinstallation abzuschließen.

4.  Wenn Sie das aktuellste Updatedefinitionspaket heruntergeladen haben, kopieren Sie das Paket auf den Clientcomputer und doppelklicken Sie darauf, um es zu installieren.

   > [!NOTE]
   >  Nach dem Abschluss der Endpoint Protection-Clientinstallation führt der Client automatisch eine Definitionsupdateprüfung aus. Bei erfolgreicher Updateprüfung muss das aktuellste Definitionsupdatepaket nicht manuell installiert werden.

## <a name="to-install-the-client-software-with-an-antimalware-policy-from-the-command-prompt"></a>So installieren Sie die Clientsoftware mit einer Richtlinie für Antischadsoftware über die Eingabeaufforderung

1.  Kopieren Sie die Datei **scepinstall.exe** und die exportierte oder vorkonfigurierte Richtlinie für Antischadsoftware auf den Computer, auf dem Sie die Endpoint Protection-Clientsoftware installieren möchten.

2.  Öffnen Sie eine Eingabeaufforderung mit Administratorberechtigungen, navigieren Sie zu dem Ordner, in dem sich die Datei **scepinstall.exe** und die Richtlinie für Antischadsoftware befindet, und führen Sie dann den folgenden Befehl aus:

   ```
   scepinstall.exe /policy <full path>\<policy file>
   ```

3.  Befolgen Sie die Anweisungen auf dem Bildschirm, um die Clientinstallation abzuschließen.

4.  Wenn Sie das aktuellste Definitionspaket heruntergeladen haben, kopieren Sie das Paket auf den Clientcomputer und doppelklicken Sie darauf, um es zu installieren.

   > [!NOTE]
   >  Nach dem Abschluss der Endpoint Protection-Clientinstallation führt der Client automatisch eine Definitionsupdateprüfung aus. Bei erfolgreicher Updateprüfung muss das aktuellste Definitionsupdatepaket nicht manuell installiert werden.

## <a name="verify-that-the-endpoint-protection-client-is-installed-correctly"></a>Sicherstellen, dass der Endpoint Protection-Client ordnungsgemäß installiert wurde
Überprüfen Sie nach der Installation des Endpoint Protection-Clients auf Ihrem Referenzcomputer, ob der Client ordnungsgemäß funktioniert.

### <a name="to-verify-that-the-endpoint-protection-client-is-installed-correctly"></a>So überprüfen Sie, ob der Endpoint Protection-Client ordnungsgemäß installiert wurde

1.  Öffnen Sie auf dem Referenzcomputer **System Center Endpoint Protection** über den Infobereich von Windows.

2.  Überprüfen Sie im Dialogfeld **System Center Endpoint Protection** auf der Registerkarte **Start**, ob die Einstellung **Ein** für den **Echtzeitschutz** festgelegt wurde.

3.  Überprüfen Sie, ob für **Viren- und Spywaredefinitionen** der Status **Aktuell**angezeigt wird.

4.  Wählen Sie unter **Scanoptionen**den Eintrag **Vollständig**aus, und klicken Sie dann auf **Jetzt scannen**, um sicherzustellen, dass der Referenzcomputer für die Imageerstellung bereit ist.

### <a name="how-to-prepare-the-endpoint-protection-client-for-imaging"></a>Vorbereiten des Endpoint Protection-Clients für die Imageerstellung
Nachdem Sie sichergestellt haben, dass der Endpoint Protection-Client ordnungsgemäß auf dem Referenzcomputer installiert wurde, können Sie den Computer für die Imageerstellung vorbereiten. Führen Sie die folgenden Schritte aus, um den Endpoint Protection-Client für die Imageerstellung vorzubereiten.


Weitere Informationen zur Betriebssystembereitstellung in Configuration Manager finden Sie unter [Verwalten von Betriebssystemimages mit System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images).

### <a name="to-prepare-the-endpoint-protection-client-for-imaging"></a>So bereiten Sie den Endpoint Protection-Client für die Imageerstellung vor

1.  Melden Sie sich beim Referenzcomputer als Benutzer mit Administratorberechtigungen an.

2.  Laden Sie von der TechNet-Website **Windows SysInternals** die Datei für [PsTools](http://go.microsoft.com/fwlink/?LinkId=215263) herunter, und installieren Sie sie.

3.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, navigieren Sie zu dem Ordner, in dem Sie „PsTools“ installiert haben, und geben Sie folgenden Befehl ein:

   ```
   Psexec.exe -s -i regedit.exe
   ```

   > [!IMPORTANT]
   >  Seien Sie bei dieser Ausführung des Registrierungseditors vorsichtig. Wenn in der Datei „PsExec.exe“ die Option „-s“ festgelegt wird, wird der Registrierungseditor mit Berechtigungen des lokalen Systems ausgeführt.

4.  Navigieren Sie im Registrierungs-Editor zu folgenden Registrierungsschlüsseln, und löschen Sie sie.

   > [!IMPORTANT]
   >  Löschen Sie die Registrierungsschlüssel in einem letzten Schritt, bevor vom Referenzcomputer ein Image erstellt wird. Die Registrierungsschlüssel werden beim Starten des Endpoint Protection-Clients erneut erstellt. Bei einem Neustart des Referenzcomputers müssen die Registrierungsschlüssel erneut gelöscht werden.

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID**

Nachdem Sie diese Schritte ausgeführt haben, können Sie den Referenzcomputer für die Imageerstellung vorbereiten. Weitere Informationen zur Betriebssystembereitstellung in Configuration Manager finden Sie unter [Verwalten von Betriebssystemimages mit System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images).

Wenn ein Image bereitgestellt wird, das die Endpoint Protection-Clientsoftware enthält, werden vom Endpoint Protection-Client automatisch Informationen an den dem Computer zugewiesenen Configuration Manager-Standort gesendet, und die für den Clientcomputer relevante Richtlinie wird heruntergeladen und angewendet.
