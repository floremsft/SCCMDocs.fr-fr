---
title: "Erstellen und Bereitstellen einer Gerätekonformitätsrichtlinie | Microsoft-Dokumentation"
description: "Erfahren Sie, wie Sie eine Gerätekonformitätsrichtlinie in System Center Configuration Manager erstellen und bereitstellen."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0fd76043-d7ee-423d-8c5f-aa7e9ed58ce0
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
robots: noindex
ms.openlocfilehash: 6630d0170df22f46f14df241ffd8d48266c69263
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-and-deploy-a-device-compliance-policy"></a>Erstellen und Bereitstellen einer Gerätekonformitätsrichtlinie

*Gilt für: System Center Configuration Manager (Current Branch)*


## <a name="create-a-compliance-policy"></a>Erstellen einer Konformitätsrichtlinie

1.  Wählen Sie in der System Center Configuration Manager-Konsole **Bestand und Kompatibilität** aus.

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, und wählen Sie **Kompatibilitätsrichtlinien**.

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** **Kompatibilitätsrichtlinie erstellen**.

4.  Geben Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Kompatibilitätsrichtlinien die folgenden Informationen an:

  * **Name**. Geben Sie einen eindeutigen Namen für die Konformitätsrichtlinie ein. Sie können bis zu 256 Zeichen verwenden.

  * **Beschreibung**. Geben Sie eine Beschreibung ein, die Ihnen einen Überblick über das VPN-Profil verschafft und dabei behilflich ist, das Profil in der Configuration Manager-Konsole zu ermitteln. Sie können bis zu 256 Zeichen verwenden.

  * **Typ der Konformitätsrichtlinie**. Wählen Sie den Richtlinientyp, den Sie erstellen möchten, auf Grundlage der Tatsache aus, ob Ihr Gerät von Configuration Manager verwaltet wird. Dies trifft auf Version  oder höher zu.<br /><br /> Wählen Sie für Geräte, die von Intune verwaltet werden, die Option **Compliance rules for devices managed without configuration manager client** (Kompatibilitätsregeln für Geräte, die ohne den Configuration Manager-Client verwaltet werden). Bei Wahl dieser Option können Sie auch den Typ der Plattform auswählen, dem Sie diese Richtlinie zuweisen möchten.

  * **Schweregrad der Nichtkompatibilität für Berichte**. Geben Sie den Schweregrad an, der gemeldet wird, wenn diese Konformitätsrichtlinie als nicht konform ausgewertet wird. Die verfügbaren Schweregrade sind:

     * **Keiner**. Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.
     * **Information**. Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** für Configuration Manager-Berichte gemeldet.   
     * **Warnung**. Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** für Configuration Manager-Berichte gemeldet.
     * **Kritisch**. Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet.
     * **Kritisch mit Ereignis**. Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Dieser Schweregrad wird zudem im Anwendungsereignisprotokoll als Windows-Ereignis protokolliert.      

5.  Wählen Sie auf der Seite **Unterstützte Plattformen** die Geräteplattformen, für die diese Kompatibilitätsrichtlinie ausgewertet wird, oder wählen Sie **Alle auswählen**, um alle Geräteplattformen auszuwählen. Folgende Plattformen werden unterstützt: Windows 7, Windows 8.1 und Windows 10; Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 und Windows Server 2016.

6.  Auf der Seite **Regeln** definieren Sie eine oder mehrere Regeln, die die Konfiguration bestimmen, die Geräte aufweisen müssen, um als kompatibel eingestuft zu werden. Wenn Sie eine Kompatibilitätsrichtlinie erstellen, sind einige Regeln standardmäßig aktiviert, die Sie aber bearbeiten oder löschen können. Eine vollständige Liste aller Regeln finden Sie unter „Regeln für Kompatibilitätsrichtlinien“ weiter unten in diesem Thema.

  > [!NOTE]  
  >  Auf Windows-PCs wird die Windows-Betriebssystemversion 8.1 als Version 6.3 gemeldet (anstelle von 8.1). Wenn die Betriebssystem-Versionsregel für Windows auf die Version Windows 8.1 festgelegt ist, wird das betreffende Gerät als nicht kompatibel gemeldet, selbst wenn auf ihm Windows 8.1 installiert ist. Stellen Sie deshalb sicher, dass Sie in den Regeln für das minimal oder maximal zulässige Betriebssystem die richtige *gemeldete* Version von Windows festlegen. Die Versionsnummer muss derjenigen entsprechen, die durch den **winver**-Befehl zurückgegeben wird. Bei Windows Phones tritt dieses Problem nicht auf. Dort wird als Version wie erwartet 8.1 gemeldet. Für Windows-PCs mit dem Betriebssystem Windows 10 muss die Version auf **10.0** plus OS-Buildnummer festgelegt werden, die vom Befehl **winver** zurückgegeben wird.

7.  Überprüfen Sie auf der Seite **Zusammenfassung** des Assistenten die von Ihnen festgelegten Einstellungen, und schließen Sie dann den Assistenten ab.

 Die neue Richtlinie wird im Knoten **Kompatibilitätsrichtlinien** im Arbeitsbereich **Bestand und Kompatibilität** angezeigt.

## <a name="deploy-a-compliance-policy"></a>Bereitstellen einer Konformitätsrichtlinie

1.  Wählen Sie in der Configuration Manager-Konsole **Bestand und Kompatibilität** aus.

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, und wählen Sie **Kompatibilitätsrichtlinien**.

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** die Option **Bereitstellen** aus.

4.  Wählen Sie im Dialogfeld **Kompatibilitätsrichtlinien bereitstellen** die Option **Durchsuchen**, um die Benutzersammlung auszuwählen, für die Sie die Richtlinie bereitstellen möchten.

     Darüber hinaus können Sie Optionen auswählen, um Warnungen zu generieren, wenn die Richtlinie nicht befolgt wird, und Sie können den Zeitplan festlegen, gemäß dem diese Richtlinie auf Kompatibilität ausgewertet wird.

5.  Wählen Sie abschließend **OK** aus.

## <a name="monitor-the-compliance-policy"></a>Überwachen der Konformitätsrichtlinie

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>So zeigen Sie Kompatibilitätsergebnisse in der Configuration Manager-Konsole an

1.  Wählen Sie in der Configuration Manager-Konsole die Option **Überwachung** aus.

2.  Wählen Sie im Arbeitsbereich **Überwachung** die Option **Bereitstellungen**.

3.  Wählen Sie in der Liste **Bereitstellungen** die Kompatibilitätsrichtlinienbereitstellung aus, für die Sie die Kompatibilitätsinformationen prüfen möchten.

4.  Zusammenfassende Informationen zur Kompatibilität der Richtlinienbereitstellung finden Sie auf der Hauptseite. Wählen Sie zum Anzeigen ausführlicherer Informationen die Bereitstellung aus, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Status anzeigen**, um die Seite **Bereitstellungsstatus** anzuzeigen.

    Die Seite **Bereitstellungsstatus** enthält die folgenden Registerkarten:

    -   **Kompatibel**. Zeigt die Kompatibilität mit der Richtlinie basierend auf der Anzahl der betroffenen Bestände an. Sie können eine Regel wählen, um unter dem Knoten **Benutzer** oder **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** einen temporären Knoten zu erstellen, in dem alle Benutzer oder Geräte enthalten sind, die mit dieser Regel kompatibel sind. Im Bereich **Bestandsdetails** werden die Benutzer oder Geräte angezeigt, die mit der Richtlinie kompatibel sind. Doppelklicken Sie auf einen Benutzer oder ein Gerät in der Liste, um weitere Informationen anzuzeigen.

    -   **Fehler**. Zeigt eine Liste aller Fehler für die ausgewählte Bereitstellung der Richtlinie basierend auf der Anzahl der betroffenen Bestände an. Sie können eine Regel wählen, um unter dem Knoten **Benutzer** oder **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** einen temporären Knoten zu erstellen, in dem alle Benutzer oder Geräte enthalten sind, durch die mit dieser Regel Fehler generiert wurden. Wenn Sie einen Benutzer oder ein Gerät auswählen, werden im Bereich **Bestandsdetails** die Benutzer oder Geräte angezeigt, die von einem Problem betroffen sind. Doppelklicken Sie auf einen Benutzer oder ein Gerät in der Liste, um weitere Informationen zum Problem anzuzeigen.

    -   **Nicht kompatibel**. Zeigt eine Liste aller nicht kompatiblen Regeln innerhalb der Richtlinie basierend auf der Anzahl der betroffenen Bestände an. Sie können eine Regel wählen, um unter dem Knoten **Benutzer** oder **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** einen temporären Knoten zu erstellen, in dem alle Benutzer oder Geräte enthalten sind, die mit dieser Regel nicht kompatibel sind. Wenn Sie einen Benutzer oder ein Gerät auswählen, werden im Bereich **Bestandsdetails** die Benutzer oder Geräte angezeigt, die von einem Problem betroffen sind. Doppelklicken Sie auf einen Benutzer oder ein Gerät in der Liste, um weitere Informationen zu diesem Problem anzuzeigen.

    -   **Unbekannt**. Zeigt eine Liste aller Benutzer und Geräte an, für die keine Kompatibilität mit der ausgewählten Richtlinienbereitstellung zusammen mit dem aktuellen Clientstatus von Geräten gemeldet wurde.

#### <a name="to-monitor-the-compliance-status-of-an-individual-device"></a>So überwachen Sie den Konformitätsstatus eines einzelnen Geräts

1.  Wählen Sie in der Configuration Manager-Konsole den Arbeitsbereich **Bestand und Konformität**.

2.  Wählen Sie **Geräte**.

3.  Klicken Sie mit der rechten Maustaste auf eine der Spalten, um mehr Spalten zu aktivieren.

  Sie können die folgenden Spalten hinzufügen:

  - **Azure Active Directory-Geräte-ID**.  Eindeutiger Bezeichner für das Gerät in Azure Active Directory.

  - **Kompatibilität: Fehlerdetails**.  Ausführliche Fehlermeldung, wenn beim End-to-End-Prozess ein Fehler auftritt. Wenn diese Spalte leer ist, bedeutet dies, dass keine Fehler gefunden wurden und der Konformitätsstatus erfolgreich gemeldet wurde.

  - **Kompatibilität: Fehlerort**.  Weitere Informationen zu dem Ort, an dem ein Kompatibilitätsfehler auftrat. Wenn diese Spalte leer ist, bedeutet dies, dass keine Fehler gefunden wurden und der Konformitätsstatus erfolgreich gemeldet wurde. Beispiele, wo ein Fehler im Kompatibilitätsprozess auftreten könnte: 
      - ConfigMgr-Client
      - Verwaltungspunkt
      - Intune
      - Azure Active Directory
<br></br>
  - **Kompatibilität: Zeitpunkt der Überprüfung**. Wann die Kompatibilität zuletzt überprüft wurde.

  - **Kompatibilität: Zeitpunkt der Festlegung**. Letzte Aktualisierung der Kompatibilität mit Azure Active Directory.

  - **Kompatibel mit bedingtem Zugriff**.  Ob der Computer mit Richtlinien für bedingten Zugriff kompatibel ist oder nicht.

  > [!IMPORTANT]
  > Diese Spalten werden standardmäßig nicht angezeigt.

#### <a name="to-view-intune-compliance-policies-charts"></a>Anzeigen von Diagrammen zu Konformitätsrichtlinien von Intune
1. Wählen Sie ab Version 1610 von Configuration Manager in der Configuration Manager-Konsole **Überwachung**.

2. Wechseln Sie im Arbeitsbereich **Überwachung** zu **Übersicht** > **Konformitätseinstellungen** > **Konformitätsrichtlinien**.

   Die folgenden Diagramme werden angezeigt:

    - **Gerätekompatibilität insgesamt**. Zeigt die Gesamtkonformität von Geräten für alle Konformitätsrichtlinien.
    - **Hauptgründe für Inkompatibilität**. Zeigt an, mit welchen Richtlinien Geräte vorwiegend nicht kompatibel sind.

3. Wählen Sie einen Bereich in einem beliebigen Diagramm, um einen Drilldown zu einer Liste der Geräte innerhalb dieser Kategorie auszuführen.

#### <a name="to-view-a-health-attestation-report"></a>So zeigen Sie einen Integritätsnachweisbericht an

1.  Wählen Sie ab Version 1602 von Configuration Manager in der Configuration Manager-Konsole **Überwachung**.

2.  Wählen Sie zum Anzeigen eines Übersichtsberichts mit dem aktuellen Status von Geräten, angeordnet nach Konformitätsstatus, **Sicherheit** und anschließend **Integritätsnachweis**.

3.  Wählen Sie zum Anzeigen eines Berichts, in dem alle Geräte und die Integritätsnachweisattribute aufgeführt sind, **Sicherheit** und anschließend **Integritätsnachweis**.

## <a name="compliance-policy-rules"></a>Regeln für Kompatibilitätsrichtlinien
* **Kennworteinstellungen auf mobilen Geräten erforderlich**. Sie können festlegen, dass Benutzer ein Kennwort eingeben müssen, bevor sie auf ihr Gerät zugreifen können.

  **Unterstützt auf:**
    * Windows Phone 8+
    * iOS 6+
    * Android 4.0+
    * Samsung KNOX Standard 4.0+

* **Kennwort zum Entsperren eines inaktiven Geräts anfordern** (Update 1602). Sie können festlegen, dass Benutzer für den Zugriff auf ein gesperrtes Gerät ein Kennwort eingeben müssen.

  **Unterstützt auf:**
  * Windows Phone 8+
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Minuten Inaktivität vor Anforderung des Kennworts** (Update 1602). Sie können die Leerlaufzeit festlegen, nach der ein Benutzer sein Kennwort erneut eingeben muss. Legen Sie den Wert auf eine der verfügbaren Optionen fest: **1 Minute**, **5 Minuten**, **15 Minuten**, **30 Minuten**, **1 Stunde**.

  Diese Regel muss mit der Option **Kennwort zum Entsperren eines inaktiven Geräts anfordern** verwendet werden. Der hier festgelegte Wert bestimmt, wann das Gerät als inaktiv betrachtet und gesperrt wird. Wenn **Kennwort zum Entsperren eines inaktiven Geräts anfordern** auf **True** gesetzt ist, muss der Benutzer ein Kennwort für den Zugriff auf das gesperrte Gerät eingeben.

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows RT/8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Automatische Updates erforderlich** (Update 1602). Sie können anfordern, dass Geräte mit Windows 8.1 oder höher Updates automatisch installieren, und Sie können die Klasse der Updates angeben.

  Der Wert sollte auf **Kein** festgelegt werden, um eine automatische Installation zu verhindern, auf **Empfohlen** , um alle empfohlenen Updates automatisch zu installieren oder auf **Wichtig** , um nur Updates zu installieren, die als wichtig eingestuft wurden.

  **Unterstützt auf:**
  * Windows Phone 8+

* **Einfache Kennwörter zulassen**. Sie können Benutzern erlauben, einfache Kennwörter wie „1234“ oder „1111“ zu verwenden. Diese Einstellung ist standardmäßig deaktiviert.

  **Unterstützt auf:**
  * Windows Phone 8+
  * iOS 6+

* **Minimale Kennwortlänge**. Sie können die Mindestanzahl an Ziffern oder Zeichen angeben, die das Benutzerkennwort enthalten muss (standardmäßig 6).

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

  >[!NOTE]
  >Für Geräte, die Windows ausführen und mit einem Microsoft-Konto gesichert sind, ist keine korrekte Auswertung mit der Konformitätsrichtlinie möglich, wenn **Minimale Kennwortlänge** größer als 8 Zeichen oder die **Minimale Anzahl von Zeichensätzen:** größer als 2 ist.

* **Dateiverschlüsselung auf mobilem Gerät**. Sie können festlegen, dass das Gerät verschlüsselt sein muss, um eine Verbindung mit Ressourcen herstellen zu können. Geräte unter Windows Phone 8 werden automatisch verschlüsselt. Geräte unter iOS werden verschlüsselt, wenn Sie die Einstellung **Kennworteinstellungen auf mobilen Geräte erforderlich**konfigurieren. Diese Einstellung ist standardmäßig aktiviert.

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Gerät darf nicht per Jailbreak oder Rooting manipuliert worden sein**. Wenn Sie diese Einstellung aktivieren, sind Jailbreak- oder Rooting-Geräte (iOS bzw. Android) nicht kompatibel. Diese Einstellung ist standardmäßig deaktiviert.

  **Unterstützt auf:**
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **E-Mail-Profil muss von Intune verwaltet werden**. Wenn Sie diese Option auf **Ja** festlegen, muss das Gerät das E-Mail-Profil verwenden, das ihm bereitgestellt wurde. Das Gerät gilt als nicht kompatibel, wenn das E-Mail-Profil nicht für dieselbe Benutzergruppe bereitgestellt wird, für die die Kompatibilitätsrichtlinie gilt.

  Es wird ebenso als nicht kompatibel gemeldet, wenn der Benutzer bereits ein E-Mail-Konto auf dem Gerät eingerichtet hat, das mit dem Intune-E-Mail-Profil übereinstimmt, das auf dem Gerät bereitgestellt wurde. Intune kann das vom Benutzer bereitgestellte Profil in diesem Fall nicht überschreiben und daher nicht verwalten. Der Benutzer kann die Kompatibilität seines Geräts herstellen, indem er die vorhandenen E-Mail-Einstellungen entfernt, sodass Intune das verwaltete E-Mail-Profil installieren kann.

  Weitere Informationen zu E-Mail-Profilen finden Sie unter [Aktivieren des Zugriffs auf Unternehmens-E-Mail mithilfe von E-Mail-Profilen in Microsoft Intune](https://technet.microsoft.com/library/dn800672.aspx). Diese Einstellung ist standardmäßig deaktiviert.

  **Unterstützt auf:**
  * iOS 6+

* **E-Mail-Profil**. Wenn **E-Mail-Konto muss von Intune verwaltet werden** aktiviert ist, wählen Sie **Auswählen**, um das E-Mail-Profil auszuwählen, von dem Geräte verwaltet werden müssen. Das E-Mail-Profil muss auf dem Gerät vorhanden sein.

  **Unterstützt auf:**
  * iOS 6+

* **Minimal erforderliches Betriebssystem**. Wenn ein Gerät die von Ihnen festgelegten Minimalanforderungen an die Betriebssystemversion nicht erfüllt, wird es als nicht kompatibel gemeldet. Ein Link mit Informationen zur Vorgehensweise beim Upgraden wird angezeigt. Die Benutzer können ein Upgrade des Geräts durchführen und anschließend auf die Unternehmensressourcen zugreifen.

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Maximal zulässige Betriebssystemversion**. Wenn ein Gerät eine neuere Betriebssystemversion verwendet, als Sie in der Regel festlegen, wird der Zugriff auf Unternehmensressourcen gesperrt, und der Benutzer wird gebeten, sich an den IT-Administrator zu wenden. Solange Sie die Regel nicht ändern und die betreffende Betriebssystemversion zulassen, kann das Gerät nicht auf Unternehmensressourcen zugreifen.

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Geräte müssen als fehlerfrei gemeldet werden** (Update 1602). Sie können eine Regel festlegen, die fordert, dass Windows 10-Geräte in neuen oder vorhandenen Kompatibilitätsrichtlinien als fehlerfrei gemeldet werden müssen. Wenn Sie diese Einstellung aktivieren, werden Windows 10-Geräte vom Integritätsnachweisdienst (Health Attestation Service, HAS) auf die folgenden Kriterien untersucht:

  - **BitLocker ist aktiviert**. Wenn BitLocker aktiviert ist, kann das Gerät Daten, die auf dem Laufwerk gespeichert sind, vor unbefugtem Zugriff schützen, wenn das Gerät ausgeschaltet wird oder in den Ruhezustand wechselt.

   Die Windows BitLocker-Laufwerkverschlüsselung verschlüsselt alle Daten, die auf dem Windows-Betriebssystemvolume gespeichert sind. BitLocker verwendet das TPM, um Windows-Betriebssystem und Benutzerdaten zu schützen. TPM stellt sicher, dass ein Computer auch dann nicht manipuliert wird, wenn er unbeaufsichtigt gelassen, verloren oder gestohlen wird.
   
   Wenn der Computer mit einem kompatiblen TPM ausgestattet ist, verwendet BitLocker das TPM zum Sperren der Verschlüsselungsschlüssel, die die Daten schützen. Daher kann erst auf die Schlüssel zugegriffen werden, nachdem das TPM den Zustand des Computers überprüft hat.

  - **Codeintegrität ist aktiviert**. Codeintegrität ist ein Feature zum Überprüfen der Integrität von Treibern oder Systemdateien, sobald diese in den Arbeitsspeicher geladen werden. Codeintegrität erkennt, ob ein nicht signierter Treiber oder eine nicht signierte Systemdatei in den Kernel geladen wird. Außerdem wird erkannt, ob eine Systemdatei durch böswillige, von einem Benutzerkonto mit Administratorrechten ausgeführte Software geändert wurde.

  - **Sicherer Start ist aktiviert**. Wenn der sichere Start aktiviert ist, wird das System gezwungen, in einem vom Hersteller als vertrauenswürdig eingestuften Zustand zu starten. Bei aktiviertem sicheren Start müssen auch die Kernkomponenten, die zum Starten des Computers verwendet werden, über ordnungsgemäße kryptografische Signaturen verfügen, denen das Unternehmen vertraut, das das Gerät hergestellt hat. Die UEFI-Firmware überprüft dies, bevor sie den Computer starten lässt. Wenn Dateien so manipuliert wurden, dass ihre Signatur nicht mehr stimmt, startet das System nicht.

  - **Early-launch antimalware is enabled** (Frühstart-Antischadsoftware ist aktiviert). Diese Einstellung gilt nur für PCs. Dieses Feature bietet Schutz für Computer in Ihrem Netzwerk, sobald diese gestartet und bevor Treiber von Drittanbietern initialisiert werden.
  
   Diese Regel ist standardmäßig deaktiviert.

  Informationen zur Funktionsweise des Integritätsnachweisdiensts finden Sie unter [HealthAttestation CSP](https://msdn.microsoft.com/library/dn934876.aspx)(HealthAttestation-Kryptografiedienstanbieter).

  **Unterstützt auf:**
  * Windows 10 und Windows 10 Mobile

- **Apps, die auf dem Gerät nicht installiert werden können**. Wenn Benutzer Apps installieren, die sich auf der Administratorliste der nicht kompatiblen Apps befinden, werden diese blockiert, wenn versucht wird, auf Geschäftsmails oder andere Geschäftsressourcen, die den bedingten Zugriff unterstützen, zuzugreifen. Für diese Regel wird der Name der App benötigt; wenn Sie eine App auf diese Administratorliste der nicht kompatiblen Apps setzen möchten, benötigen Sie dafür zusätzlich die App-ID. Ebenso kann der App-Herausgeber hinzugefügt werden; dies ist jedoch nicht zwingend notwendig.

    **Unterstützt auf:**
      * iOS 6+
      * Android 4.0+
      * Samsung KNOX Standard 4.0+
<br></br>
* **Erforderlicher Kennworttyp**. Legen Sie fest, ob Benutzer ein alphanumerisches oder numerisches Kennwort erstellen müssen. Bei alphanumerischen Kennwörtern legen Sie außerdem die erforderliche Mindestzahl an Zeichen fest. Die vier Zeichengruppen sind Kleinbuchstaben, Großbuchstaben, Symbole und Zahlen.

    **Unterstützt auf:**
    * Windows Phone 8+
    * Windows 8.1+
    * iOS 6+
<br></br>
* **USB-Debugging auf Gerät blockieren**. Sie müssen diese Einstellungen nicht konfigurieren, da USB-Debuggen bereits auf Android for Work-Geräten deaktiviert ist.

    **Unterstützt auf:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Apps von unbekannten Quellen blockieren**. Fordert an, dass Geräte die Installation von Apps aus unbekannten Quellen verhindern. Sie müssen diese Einstellung nicht konfigurieren, da Android for Work-Geräte die Installation aus unbekannten Quellen stets einschränken.

    **Unterstützt auf:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Bedrohungsüberprüfung für Apps erzwingen**. Diese Einstellung gibt an, dass die Funktion „Apps überprüfen“ auf dem Gerät aktiviert ist. 

    **Unterstützt auf:**
    * Android 4.2 bis 4.4
    * Samsung KNOX Standard 4.0+

### <a name="find-an-app-id"></a>Finden einer App-ID

Eine App-ID ist ein Bezeichner, der die App in den Anwendungsdiensten Apple und Google eindeutig identifiziert. Ein Beispiel ist „com.contoso.myapp“. So finden Sie eine:

- **Android**
    - Die App-ID finden Sie in der URL des Google Play Stores, die für die Erstellung der App verwendet wurde. Eine Beispiel-App-ID ist: *…?id=com.companyname.appname&hl=en*.

- **iOS**
    1. In der URL des iTunes-Stores finden Sie die ID-Nummer, Beispiel: */id875948587?mt=8*.

    2. Wechseln Sie in einem Webbrowser zur folgenden URL, und ersetzen Sie die Nummer durch die ID-Nummer, die Sie gerade gefunden haben (in diesem Fall im vorherigen Beispiel): „https://itunes.apple.com/lookup?id=875948587“.

    3. Laden Sie die Textdatei herunter und öffnen Sie sie.
  
    4. Suchen Sie nach dem Text **bundleId**.

    Eine Beispiel-App-ID ist: „*bundleId*“:„*com.companyname.appname*“. 

