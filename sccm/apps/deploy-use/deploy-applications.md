---
title: Bereitstellen von Anwendungen | Microsoft-Dokumentation
description: "Erstellen Sie einen Bereitstellungstyp, oder simulieren Sie die Bereitstellung für eine Anwendung mithilfe von System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
caps.latest.revision: "10"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f704d1b0ec48e3a7bbea784a7c18de77b21cd0ee
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Bereitstellen von Anwendungen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bevor Sie eine System Center Configuration Manager-Anwendung bereitstellen können, müssen Sie mindestens einen Bereitstellungstyp für die Anwendung erstellen. Weitere Informationen zum Erstellen von Anwendungen und Bereitstellungstypen finden Sie unter [Create applications (Erstellen von Anwendungen)](/sccm/apps/deploy-use/create-applications).

 Sie können eine Anwendungsbereitstellung auch simulieren. Bei dieser Art der Bereitstellung wird die Anwendbarkeit einer Anwendungsbereitstellung auf Computern getestet, ohne die Anwendung zu installieren oder zu deinstallieren. Bei einer simulierten Bereitstellung werden die Erkennungsmethode, Anforderungen und Abhängigkeiten für einen Bereitstellungstyp ausgewertet. Anschließend wird ein Bericht mit den Ergebnissen im Arbeitsbereich **Überwachung** unter dem Knoten **Bereitstellungen** ausgegeben. Weitere Informationen finden Sie unter [Simulate application deployments (Simulieren von Anwendungsbereitstellungen)](/sccm/apps/deploy-use/simulate-application-deployments).

> [!IMPORTANT]
>  Sie können erforderliche Anwendungen bereitstellen (installieren oder deinstallieren), jedoch keine Pakete oder Softwareupdates. MDM-registrierte Geräte unterstützen ebenfalls keine simulierten Bereitstellungen, Einstellungen für Benutzerfreundlichkeit oder Zeitplanung.

## <a name="deploy-an-application"></a>Bereitstellen einer Anwendung

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen**.

2.  Wählen Sie in der Liste **Anwendungen** die Anwendung aus, die Sie bereitstellen möchten. Klicken Sie dann auf die **Home** Registerkarte der **Bereitstellung** auf **Bereitstellen**.

### <a name="specify-general-information-about-the-deployment"></a>Angeben allgemeiner Informationen zur Bereitstellung

Geben Sie im Assistenten zum Bereitstellen von Software auf der Seite **Allgemein** die folgenden Informationen an:

- **Software**  
Hier wird die Anwendung angezeigt, die bereitgestellt werden soll. Sie können auf **Durchsuchen** klicken, um eine andere Anwendung auszuwählen.
- **Sammlung**  
Klicken Sie auf **Durchsuchen**, um die Sammlung auszuwählen, in der Sie die Anwendung bereitstellen möchten.
- **Standard-Verteilungspunktgruppen verwenden, die dieser Sammlung zugeordnet sind**  
Wählen Sie diese Option aus, wenn Sie den Anwendungsinhalt in der Standard-Verteilungspunktgruppe der Sammlung speichern möchten. Wenn die ausgewählte Sammlung keiner Verteilungspunktgruppe zugeordnet ist, ist diese Option ausgegraut.
- **Automatically distribute content for dependencies (Inhalt automatisch für Abhängigkeiten bereitstellen)**  
Wenn diese Option aktiviert ist, und Bereitstellungstypen in der Anwendung Abhängigkeiten enthalten, wird der Inhalt der abhängigen Anwendung ebenfalls an Verteilungspunkte gesendet.

    >[!IMPORTANT]
    > Wenn Sie ein Update der abhängigen Anwendung ausführen, nachdem die primäre Anwendung bereitgestellt wurde, wird neuer Inhalt für die Abhängigkeit nicht automatisch verteilt.

- **Kommentare (optional)**  
Geben Sie bei Bedarf eine Beschreibung für diese Bereitstellung ein.

### <a name="specify-content-options-for-the-deployment"></a>Angeben von Inhaltsoptionen für die Bereitstellung

Klicken Sie auf der Seite **Inhalt** auf **Hinzufügen**, um den dieser Bereitstellung zugeordneten Inhalt Verteilungspunkten oder Verteilungspunktgruppen hinzuzufügen. Wenn Sie auf der Seite **Allgemein** die Option **Use default distribution points associated to this collection** (Standard-Verteilungspunktgruppen verwenden, die dieser Sammlung zugeordnet sind) aktiviert haben, wird diese Option automatisch aufgefüllt, und kann nur von einem Mitglied der Sicherheitsrolle „Anwendungsadministrator“ geändert werden.

### <a name="specify-deployment-settings"></a>Angeben von Bereitstellungseinstellungen

Geben Sie im Assistenten zum Bereitstellen von Software auf der Seite **Bereitstellungseinstellungen** die folgenden Informationen an:

- **Aktion**  
Wählen Sie in der Dropdownliste aus, ob diese Bereitstellung zum **Installieren** oder **Deinstallieren** der Anwendung dienen soll.

    > [!NOTE]
    >  Wenn eine Anwendung zweimal auf einem Gerät bereitgestellt wird, einmal mit der Aktion **Installieren** und einmal mit der Aktion **Deinstallieren**, hat die Anwendungsbereitstellung mit der Aktion **Installieren** höhere Priorität.

Sie können die Aktion einer Bereitstellung nicht mehr ändern, nachdem sie erstellt wurde.

- **Zweck**  
Wählen Sie in der Dropdownliste eine der folgenden Optionen aus:
    - **Verfügbar**  
    Wenn die Anwendung für einen Benutzer bereitgestellt wird, ist sie für den Benutzer im Softwarecenter als veröffentlichte Anwendung sichtbar, und er kann sie bei Bedarf installieren.
    - **Erforderlich**  
    Die Anwendung wird gemäß dem konfigurierten Zeitplan automatisch bereitgestellt. Wenn der Bereitstellungsstatus nicht ausgeblendet ist, kann jede Person, die die Anwendung verwendet, den Bereitstellungsstatus nachverfolgen, und die Anwendung vor Ablauf der Frist über das Softwarecenter installieren.

    > [!NOTE]   
    >  Wenn als Bereitstellungsaktion **Deinstallieren**ausgewählt wurde, wird als Bereitstellungszweck automatisch **Erforderlich** festgelegt, und die Einstellung kann nicht geändert werden.  

- **Automatische Bereitstellung nach Zeitplan unabhängig von Benutzeranmeldung**  
Wählen Sie diese Option bei der Bereitstellung für einen Benutzer aus, um die Anwendung für die primären Geräte des Benutzers bereitzustellen. Bei dieser Einstellung ist es nicht erforderlich, dass sich der Benutzer vor der Ausführung der Bereitstellung anmeldet. Wählen Sie diese Option nicht, wenn Benutzereingaben erforderlich sind, um die Installation abzuschließen. Diese Option ist nur verfügbar, wenn der Bereitstellungszweck auf **Erforderlich**festgelegt ist.

- **Aktivierungspakete senden**  
Wenn der Bereitstellungszweck auf **Erforderlich** festgelegt und diese Option ausgewählt wird, wird vor der Installation der Bereitstellung ein Aktivierungspaket an den Computer gesendet. Dieses Paket aktiviert den Computer zum Installationsstichtag. Sie können diese Option nur verwenden, wenn Computer und Netzwerke für Wake-On-LAN konfiguriert sind.
- **Clients mit einer getakteten Internetverbindung dürfen den Inhalt nach dem Installationsstichtag herunterladen (Zusatzkosten können anfallen)**  
Diese Option ist nur für Bereitstellungen mit dem Zweck **Erforderlich** verfügbar.
- **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box** (Alle ausgeführten Dateien, die Sie in der Registerkarte „Installationsverhalten“ im Dialogfeld zu den Bereitstellungstyp-Eigenschaften spezifiziert haben, werden automatisch beendet)  
Weitere Informationen darüber, wie Sie eine Liste der ausführbaren Dateien konfigurieren, die die Installation einer Anwendung verhindern können, finden Sie weiter unten in diesem Thema unter **How to check for running executable files before installing an application** (Vorgehensweise: Vor der Installation einer Anwendung nach ausgeführten Dateien suchen).
- **Genehmigung durch Administrator erforderlich, wenn Benutzer diese Anwendung anfordern**  
Wenn diese Option ausgewählt ist, muss der Administrator jede Benutzeranforderung für die Anwendung genehmigen, bevor sie installiert werden kann. Diese Option ist ausgegraut, wenn der Zweck der Bereitstellung **Erforderlich** lautet, oder wenn die Anwendung für eine Gerätesammlung bereitgestellt wird.

    > [!NOTE]
    >  Genehmigungsanforderungen für Anwendungen werden im Arbeitsbereich **Softwarebibliothek** unter **Anwendungsverwaltung** im Knoten **Genehmigungsanforderungen** angezeigt. Wenn eine Anforderung nicht innerhalb von 45 Tagen genehmigt wird, wird sie entfernt. Außerdem können ausstehende Genehmigungsanforderungen durch eine Neuinstallation des Configuration Manager-Client abgebrochen werden.
    >  Nachdem Sie eine Anwendung für die Installation genehmigt haben, können Sie anschließend auswählen, die Anforderung zu verweigern, indem Sie in der Configuration Manager-Konsole auf **Verweigern** klicken (bisher war diese Schaltfläche nach der Genehmigung ausgegraut).
    >  Diese Aktion führt nicht dazu, dass die Anwendung auf allen Geräten deinstalliert wird, sondern hindert Benutzer daran, neue Kopien der Anwendung aus dem Softwarecenter herunterzuladen.

- **Automatically upgrade any superseded version of this application**  (Jede abgelöste Version dieser Anwendung automatisch aktualisieren)  
Wenn diese Option ausgewählt ist, wird jede abgelöste Version der Anwendung auf die neuere Anwendung aktualisiert.

### <a name="specify-scheduling-settings-for-the-deployment"></a>Angeben von Einstellungen zur Zeitplanung der Bereitstellung

Stellen Sie im Assistenten zum Bereitstellen von Software auf der Seite **Zeitplanung** die Zeit ein, wann diese Anwendung für Clientgeräte bereitgestellt oder verfügbar gemacht wird.
Welche Optionen auf dieser Seite verfügbar sind, ist davon abhängig, ob die Bereitstellungsaktion auf **Verfügbar** oder **Erforderlich**gesetzt ist.

In einigen Fällen empfiehlt es sich, Benutzern über die von Ihnen angegebenen Fristen hinaus mehr Zeit zum Installieren von erforderlichen Anwendungsbereitstellungen oder Softwareupdates zu geben. Dies ist normalerweise erforderlich, wenn ein Computer für einen längeren Zeitraum ausgeschaltet war, und eine große Anzahl von Anwendungen oder Updatebereitstellungen installieren muss. Wenn z.B. ein Benutzer aus dem Urlaub zurückgekehrt ist, muss er möglicherweise sehr lange warten, bis überfällige Anwendungsbereitstellungen installiert werden. Sie können jetzt eine zwingende Toleranzperiode definieren, um dieses Problem zu lösen. Dafür müssen Sie die Configuration Manager-Clienteinstellungen für eine Sammlung bereitstellen.

Führen Sie folgende Aktionen aus, um die Karenzzeit zu konfigurieren:

- Auf der Seite **Computer-Agent** der Clienteinstellungen müssen Sie die neue Eigenschaft **Karenzzeit für Erzwingung nach Bereitstellungsfrist (Stunden)** mit einem Wert zwischen **1** und **120** Stunden konfigurieren.
- Aktivieren Sie auf der Seite **Zeitplanung** in einer neuen erforderlichen Anwendungsbereitstellung oder in den Eigenschaften einer vorhandenen Bereitstellung das Kontrollkästchen **Delay enforcement of this deployment according to user preferences, up to the grace period defined in client settings** (Erzwingung dieser Bereitstellung entsprechend den Benutzervoreinstellungen verzögern, bis zu der Toleranzperiode, die in den Clienteinstellungen definiert ist). Alle Bereitstellungen, für die dieses Kästchen ausgewählt ist, und die für Geräte vorgesehen sind, für die Sie ebenfalls die Clienteinstellungen bereitgestellt haben, werden die Toleranzperiode verwenden.

Nach Ablauf der Installationsfrist wird die Anwendung im ersten nicht geschäftlichen Fenster installiert, das der Benutzer in der Toleranzperiode konfiguriert hat. Der Benutzer kann jedoch weiterhin das Software Center öffnen und die Anwendung zu einem beliebigen Zeitpunkt installieren. Nach Ablauf der Toleranzperiode wird die Erzwingung auf normales Verhalten für überfällige Bereitstellungen zurückgesetzt.

Wenn die bereitgestellte Anwendung eine andere Anwendung ablöst, können Sie den Stichtag festlegen, an dem bei Benutzern die neue Anwendung installiert wird. Verwenden Sie dafür die Einstellung **Installationsstichtag**, um für Benutzer mit abgelösten Anwendungen ein Upgrade auszuführen.

### <a name="specify-user-experience-settings-for-the-deployment"></a>Angeben von Einstellungen für die Benutzerfreundlichkeit der Bereitstellung


Geben Sie im Assistenten zum Bereitstellen von Software auf der Seite **Benutzerfreundlichkeit** an, wie Benutzer mit der Anwendungsinstallation interagieren können.

Beim Bereitstellen von Anwendungen für Windows Embedded-Geräte mit Schreibfilteraktivierung können Sie angeben, dass die Anwendung im temporären Overlay gespeichert und die Änderungen später übernommen werden sollen. Sie können auch angeben, dass die Änderungen am Installationsstichtag oder während eines Wartungsfensters übernommen werden sollen. Falls die Änderungen am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden, ist ein Neustart erforderlich. Die Änderungen werden auf dem Gerät beibehalten.

>[!NOTE]
    >  Stellen Sie beim Bereitstellen einer Anwendung auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert ist. Weitere Informationen zur Verwendung von Wartungsfenstern beim Bereitstellen von Anwendungen auf Windows Embedded-Geräten finden Sie unter [Erstellen von Windows Embedded-Anwendungen](../../apps/get-started/creating-windows-embedded-applications.md).
    > Die Optionen **Softwareinstallation** und **Systemneustart (falls dieser zum Abschluss der Installation erforderlich ist)** werden nicht verwendet, wenn der Bereitstellungszweck auf **Verfügbar**gesetzt ist. Sie können auch die Ebene für die Benutzerbenachrichtigung bei der Anwendungsinstallation konfigurieren.

### <a name="specify-alert-options-for-the-deployment"></a>Angeben von Optionen zu Warnungen für die Bereitstellung

Stellen Sie im Assistenten zum Bereitstellen von Software auf der Seite **Warnungen** ein, wie Warnungen von Configuration Manager und System Center Operations Manager für diese Bereitstellung generiert werden. Sie können Schwellenwerte für Berichtswarnungen konfigurieren und die Berichterstattung für die Dauer der Bereitstellung deaktivieren.

### <a name="associate-the-deployment-with-an-ios-app-configuration-policy"></a>Zuordnen der Bereitstellung zu einer iOS-App-Konfigurationsrichtlinie

Klicken Sie auf der Seite **App Configuration Policies** (App-Konfigurationsrichtlinien) auf **Neu**, um diese Bereitstellung einer iOS-App-Konfigurationsrichtlinie zuzuordnen (sofern Sie eine solche erstellt haben). Weitere Informationen zu diesen Richtlinientypen finden Sie unter [Konfigurieren von Apps mit Konfigurationsrichtlinien für Apps](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).

### <a name="finish-up"></a>Fertig stellen

Überprüfen Sie im Assistenten zum Bereitstellen von Software auf der Seite **Zusammenfassung** die Aktionen, die für die Bereitstellung ausgeführt werden. Klicken Sie auf **Weiter**, um den Assistenten abzuschließen.

Die neue Bereitstellung wird anschließend im Arbeitsbereich **Überwachung** im Knoten **Bereitstellungen** in der Liste **Bereitstellungen** angezeigt. Sie können die Eigenschaften dieser Bereitstellung bearbeiten oder die Bereitstellung auf der Registerkarte **Bereitstellungen** des Anwendungsdetailbereichs löschen.

## <a name="delete-an-application-deployment"></a>Löschen einer Anwendungsbereitstellung

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen**.
3.  Wählen Sie in der Liste **Anwendungen** die Anwendung aus, die die Bereitstellung enthält, die Sie löschen möchten.
4.  Wählen Sie auf der Registerkarte **Bereitstellungen** in der Liste *<Anwendungsname\>* die zu löschende Anwendungsbereitstellung aus. Klicken Sie auf der Registerkarte **Bereitstellung** in der Gruppe **Bereitstellung** dann auf **Löschen**.

Wenn Sie eine Anwendungsbereitstellung löschen, werden bereits installierte Instanzen der Anwendung nicht entfernt. Sie müssen diese Anwendungen mit **Deinstallieren** auf Computern bereitstellen, um sie zu entfernen. Wenn Sie eine Anwendungsbereitstellung löschen oder eine Ressource aus der Sammlung entfernen, in der Sie die Bereitstellung vornehmen, wird diese im Softwarecenter nicht mehr angezeigt.

## <a name="user-notifications-for-required-deployments"></a>Benutzerbenachrichtigungen für erforderliche Bereitstellungen
Wenn Sie erforderliche Software von der Einstellung **Warten und erinnern** erhalten, Können Sie aus der folgenden Dropdownliste von Werten auswählen:
- **Später**  
Gibt an, dass Benachrichtigungen basierend auf den in den Client-Agent-Einstellungen konfigurierten Benachrichtigungseinstellungen geplant sind.
- **Feste Zeit**  
Gibt an, dass die Benachrichtigung nach der ausgewählten Zeit erneut angezeigt wird. Wenn Sie z.B. 30 Minuten auswählen, wird die Benachrichtigung in 30 Minuten erneut angezeigt.

![Computer-Agentseite in den Client-Agenteinstellungen](media/ComputerAgentSettings.png)

Die maximale Wartezeit basiert immer auf den Benachrichtigungswerten, die in den Einstellungen des Client-Agents zu jedem Zeitpunkt der Bereitstellung konfiguriert sind. Wenn zum Beispiel die Einstellung **Deployment deadline greater than 24 hours, remind users every (hours)** (Bereitstellungsstichtag in mehr als 24 Stunden, Benutzer erinnern alle (Stunden)) auf der Seite **Computer-Agent** auf 10 Stunden festgelegt ist, und das Dialogfeld mehr als 24 Stunden vor Ablauf der Frist gestartet wird, erhalten Sie einen Satz an Warteoptionen von bis zu, aber nie mehr als 10 Stunden. Wenn sich der Stichtag nähert, wird das Dialogfeld weniger Optionen anzeigen. Dies stimmt mit den entsprechenden Client-Agenteinstellungen für jede Komponente der Bereitstellungszeit überein.

Darüber hinaus fällt bei Bereitstellungen mit hohem Risiko, z.B. einer Tasksequenz, die ein Betriebssystem bereitstellen, die Benachrichtigung des Benutzers deutlicher aus. Immer wenn Sie benachrichtigt werden, dass eine kritische Softwarewartung erforderlich ist, wird anstatt einer vorübergehenden Benachrichtigung in der Taskleiste ein Dialogfeld wie das folgende auf Ihrem Computer angezeigt:

![Erforderlicher Softwaredialog](media/client-toast-notification.png)

## <a name="how-to-check-for-running-executable-files-before-installing-an-application"></a>So prüfen Sie auf ausgeführte ausführbare Dateien, bevor Sie eine Anwendung installieren

>[!Tip]
>Seit der Version 1702 ist das ein vorab veröffentlichtes Feature. Informationen zur Aktivierung finden Sie unter [Features der Vorabversion in System Center Configuration Manager](https://docs.microsoft.com/sccm/core/servers/manage/pre-release-features).

Sie können auf der Registerkarte **Installationsverhalten** im Dialogfeld **Eigenschaften** eines Bereitstellungstyps eine von mehreren ausführbaren Dateien festlegen, die die Installation des Bereitstellungstyps verhindert, wenn sie ausgeführt wird. Der Benutzer muss die ausgeführte ausführbare Datei schließen bevor der Bereitstellungstyp installiert werden kann – die Datei kann aber auch automatisch für Bereitstellungen mit dem Zweck „Erforderlich“ geschlossen werden. So konfigurieren Sie dies:

1. Öffnen Sie das Dialogfeld **Eigenschaften** für jeden Bereitstellungstyp.
2. Klicken Sie auf der Registerkarte **Installationsverhalten** des Dialogfelds *<deployment type name>* **Eigenschaften** auf **Hinzufügen**.
3. Geben Sie im Dialogfeld **Ausführbare Datei hinzufügen oder bearbeiten** den Namen der ausführbaren Datei an, die bei der Ausführung die Installation der Anwendung blockiert. Optional können Sie auch einen Anzeigenamen für die Anwendung eingeben, damit Sie sie leichter identifizieren können.
4. Klicken Sie auf **OK** und schließen Sie das Dialogfeld *<deployment type name>* **Eigenschaften**.
5. Wenn Sie als Nächstes auf der Seite **Bereitstellungseinstellungen** des Assistenten zum Bereitstellen von Software eine Anwendung bereitstellen, wählen Sie **Ausgeführte ausführbare Dateien automatisch schließen, die im Eigenschaftendialogfeld des Bereitstellungstyps auf der Registerkarte „Installationsverhalten“ angegeben wurden** aus. Führen Sie anschließend die Bereitstellung der Anwendung fort.

Nachdem die Anwendung Client-PCs erreicht, gilt Folgendes:

- Wenn die Anwendung als **Verfügbar** bereitgestellt wurde und ein Endbenutzer versucht, sie zu installieren, wird er dazu aufgefordert, alle ausgeführten ausführbaren von Ihnen festgelegte Dateien zu schließen, bevor er mit der Installation fortfahren kann.

- Wenn die Anwendung als **Erforderlich** bereitgestellt wurde, und die Option **Ausgeführte ausführbare Dateien automatisch schließen, die im Eigenschaftendialogfeld des Bereitstellungstyps auf der Registerkarte "Installationsverhalten" angegeben wurden** ausgewählt ist, wird dem Endbenutzer ein Dialogfeld angezeigt, das ihn darüber informiert, dass ausführbare, von Ihnen festgelegte Dateien automatisch geschlossen werden, wenn die Frist der Installation abgelaufen ist. Sie können diese Dialogfelder unter **Clienteinstellungen** > **Computer-Agent** zeitlich festlegen. Wenn Sie nicht möchten, dass der Endbenutzer diese Meldungen sieht, wählen Sie auf der Registerkarte **User Experience** (Benutzererfahrung) der Bereitstellungseigenschaften **In Softwarecenter und allen Benachrichtigungen ausblenden** aus.

- Wenn die Anwendung als **Erforderlich** bereitgestellt wurde, und die Option **Ausgeführte ausführbare Dateien automatisch schließen, die im Eigenschaftendialogfeld des Bereitstellungstyps auf der Registerkarte "Installationsverhalten" angegeben wurden** nicht ausgewählt ist, schlägt die Installation der Anwendung fehl, wenn mindestens eine der angegebenen Anwendungen ausgeführt wird.

## <a name="for-more-information"></a>Weitere Informationen

   -  [Einstellungen zum Verwalten von Bereitstellungen mit hohem Risiko](../../protect/understand/settings-to-manage-high-risk-deployments.md)  
   -  [Konfigurieren von Clienteinstellungen](../../core/clients/deploy/configure-client-settings.md)
