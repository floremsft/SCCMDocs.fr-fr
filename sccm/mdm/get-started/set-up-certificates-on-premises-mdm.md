---
title: Einrichten von Zertifikaten | Microsoft-Dokumentation
description: "Richten Sie in System Center Configuration Manager Zertifikate für vertrauenswürdige Verbindungen für die lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM) ein."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
caps.latest.revision: "27"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 3d695a2a40fd86ad991a26db3dcecbbb9ca186cc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-certificates-for-trusted-communications-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Einrichten von Zertifikaten für vertrauenswürdige Verbindungen für die lokale Verwaltung von Mobilgeräten in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager müssen für vertrauenswürdige Verbindungen mit verwalteten Geräten die Standortsystemrollen „Registrierungspunkt“, „Registrierungsproxypunkt“, „Verteilungspunkt“ und „Geräteverwaltungspunkt“ eingerichtet werden. Alle Standortsystemserver, die eine oder mehrere dieser Rollen hosten, benötigen ein eindeutiges PKI-Zertifikat, das an den Webserver auf dem jeweiligen System gebunden ist. Ein Zertifikat mit demselben Stamm wie das Zertifikat auf den Servern muss außerdem auf verwalteten Geräten gespeichert sein, damit vertrauenswürdige Verbindungen mit ihnen einrichtet werden können.  

 Für zu Domänen gehörende Geräten wird von den Active Directory-Zertifikatdiensten das benötigte Zertifikat mit dem vertrauenswürdigen Stamm automatisch auf allen Geräten installiert. Für Geräte, die keiner Domäne angehören, müssen Sie ein gültiges Zertifikat mit einem vertrauenswürdigen Stamm anderweitig beziehen. Wenn Sie die Standortzertifizierungsstelle als Ihren vertrauenswürdigen Stamm nutzen (der auch von Active Directory für zur Domäne gehörende Geräte verwendet wird), benötigen die Standortsystemserver für den Anmeldungspunkt und Anmeldungsproxypunkt ein Zertifikat, das von dieser Zertifizierungsstelle ausgestellt und an sie gebunden wurde.  

 Auf jedem zu verwaltenden Gerät muss außerdem ein Zertifikat mit demselben Stamm installiert werden, um vertrauenswürdige Verbindungen mit Standortsystemrollen zu unterstützen. Für in einem Massenvorgang registrierte Geräte können Sie das Zertifikat dem Registrierungspaket hinzufügen, das dem Gerät für die Registrierung hinzugefügt wird, wenn das Gerät erstmals vom Benutzer gestartet wird. Für von Benutzern registrierte Geräte müssen Sie das Zertifikat per E-Mail, Download aus dem Internet oder anderer Methode hinzufügen.  

 Als Alternative für nicht zur Domäne gehörige Geräte können Sie den Stamm einer bekannten öffentlichen Zertifizierungsstelle (wie z. B. Verisign oder GoDaddy) zum Ausstellen des Serverzertifikats verwenden. Dadurch wird vermieden, ein Zertifikat manuell auf dem Gerät installieren zu müssen, da die meisten Geräte nativ Verbindungen mit Servern vertrauen, die den denselben Stamm der öffentlichen Zertifizierungsstelle verwenden. Dies ist eine nützliche Alternative für von Benutzern registrierte Geräte, bei denen es nicht möglich, die Zertifikate, denen von der Stammzertifizierungsstelle vertraut wird, auf allen Geräten zu installieren.  

> [!IMPORTANT]  
>  Es gibt viele Methoden zum Einrichten der Zertifikate für vertrauenswürdige Verbindungen zwischen Geräten und den Standortsystemservern für die lokale Verwaltung mobiler Geräte. Die Informationen in diesem Artikel dienen als Beispiel einer der Möglichkeiten. Diese Methode erfordert, dass Sie einen Server an Ihrem Standort mit der Rolle „Active Directory-Zertifikatdienste“ ausführen und dass die Rollendienste „Zertifizierungsstelle“ und „Zertifizierungsstellen-Webregistrierung“ installiert sind. Weitere Informationen und eine Anleitung für diese Windows Server-Rolle finden Sie unter [Active Directory-Zertifikatdienste](http://go.microsoft.com/fwlink/p/?LinkId=115018).  

 Führen Sie die folgenden allgemeinen Schritte durch, um den Configuration Manager-Standort für die SSL-Verbindungen vorzubereiten, die für die lokale Verwaltung mobiler Geräte erforderlich sind:  

-   [Konfigurieren der Zertifizierungsstelle für die Veröffentlichung der Zertifikatsperrliste](#bkmk_configCa)  

-   [Erstellen der Webserver-Zertifikatvorlage bei der Zertifizierungsstelle](#bkmk_certTempl)  

-   [Anfordern des Webserverzertifikats für jede Standortsystemrolle](#bkmk_requestCert)  

-   [Binden des Zertifikats an den Webserver](#bkmk_bindCert)  

-   [Exportieren des Zertifikats mit demselben Stamm wie das Webserverzertifikat](#bkmk_exportCert)  

##  <a name="bkmk_configCa"></a> Konfigurieren der Zertifizierungsstelle für die Veröffentlichung der Zertifikatsperrliste  
 Standardmäßig verwendet die Zertifizierungsstelle LDAP-basierte Zertifikatssperrlisten, die Verbindungen für zur Domäne gehörige Geräte zulassen. Sie müssen der Zertifizierungsstelle HTTP-basierte Zertifikatsperrlisten hinzufügen, damit nicht zur Domäne gehörenden Geräten mithilfe von Zertifikaten vertraut wird, die von der Zertifizierungsstelle ausgestellt wurden. Diese Zertifikate sind für die SSL-Verbindung zwischen den Servern, auf denen die Configuration Manager-Standortsystemrollen gehostet werden, und den Geräten erforderlich, die für die lokale Verwaltung mobiler Geräte registriert sind.  

 Führen Sie die nachstehenden Schritte zum Konfigurieren der Zertifizierungsstelle für die automatische Veröffentlichung von Informationen zu Zertifikatsperrlisten und zum Ausstellen von Zertifikaten aus, die vertrauenswürdige Verbindungen für zur Domäne gehörige und nicht zur Domäne gehörige Geräte zulassen:  

1.  Klicken Sie auf dem Server mit der Zertifizierungsstelle für Ihren Standort auf **Start**  >  **Verwaltung**  >  **Zertifizierungsstelle**.  

2.  Klicken Sie in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **CertificateAuthority** und anschließend auf **Eigenschaften**.  

3.  Klicken Sie in den „CertificateAuthority“-Eigenschaften auf die Registerkarte **Erweiterungen**, stellen Sie sicher, dass **Erweiterung auswählen** auf **Sperrlisten-Verteilungspunkt** festgelegt ist.  

4.  Wählen Sie **http://<DNS-Name des Servers\>/CertEnroll/<Name der Zertifizierungsstelle\><Namenssuffix der Zertifikatsperrliste\><DeltaCRLAllowed\>.crl** aus. Und die folgenden drei Optionen:  

    -   **In Sperrlisten einbeziehen. Wird zur Suche von Deltasperrlisten verwendet.**  

    -   **In CDP-Erweiterung des ausgestellten Zertifikats einbeziehen.**  

    -   **In IDP-Erweiterung ausgestellter CRLs einbeziehen.**  

5.  Klicken Sie auf der Registerkarte **Beendigungsmodul** auf **Eigenschaften...**, und wählen Sie **Veröffentlichen von Zertifikaten im Dateisystem zulassen** aus.  

6.  Klicken Sie auf **OK**, wenn Sie benachrichtigt werden, dass die Active Directory-Zertifikatdienste neu gestartet werden müssen.  

7.  Klicken Sie mit der rechten Maustaste auf **Gesperrte Zertifikate**, klicken Sie auf **Alle Tasks** und anschließend auf **Veröffentlichen**.  

8.  Wählen Sie im Dialogfeld „Zertifikatsperrliste veröffentlichen“ **Nur Deltasperrliste** aus, und klicken Sie anschließend auf **OK**.  

##  <a name="bkmk_certTempl"></a> Erstellen der Webserver-Zertifikatvorlage bei der Zertifizierungsstelle  
 Nach dem Veröffentlichen der neuen Zertifikatsperrliste bei der Zertifizierungsstelle ist der nächste Schritt das Erstellen einer Webserver-Zertifikatvorlage. Diese Vorlage ist erforderlich für das Ausstellen von Zertifikaten für Server, die die Standortsystemrollen „Anmeldungspunkt“, „Anmeldungsproxypunkt“, „Verteilungspunkt“ und „Geräteverwaltungspunkt“ hosten. Diese Server werden SSL-Endpunkte für vertrauenswürdige Verbindungen zwischen Standortsystemrollen und registrierten Geräten.    Gehen Sie folgendermaßen vor, um die Zertifikatvorlage zu erstellen:  

1.  Erstellen Sie eine Sicherheitsgruppe namens **ConfigMgr MDM Servers**, die die Server mit den ausgeführten Standortsystemen enthält, die vertrauenswürdige Verbindungen mit registrierten Geräten erfordern.  

2.  Klicken Sie in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, und klicken Sie anschließend auf **Verwalten**, um die Zertifikatvorlagenkonsole zu laden.  

3.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Name **Webserver**angezeigt wird, und klicken Sie auf **Doppelte Vorlage**.  

4.  Vergewissern Sie sich, dass im Dialogfeld **Doppelte Vorlage** die Option **Windows 2003 Server Enterprise Edition** ausgewählt ist, und klicken Sie dann auf **OK**.  

    > [!IMPORTANT]  
    >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition**aus. Configuration Manager unterstützt keine Windows Server 2008-Zertifikatvorlagen für vertrauenswürdige Verbindungen über HTTPS.  

    > [!NOTE]  
    >  Wenn die Zertifizierungsstelle, die Sie verwenden, unter Windows Server 2012 ausgeführt wird, werden Sie nicht zur Angabe der Zertifikatvorlagenversion aufgefordert, wenn Sie auf **Vorlage duplizieren** klicken. Geben Sie stattdessen auf der Registerkarte **Kompatibilität** die Vorlageneigenschaften wie folgt ein:  
    >   
    >  **Zertifizierungsstelle**: **Windows Server 2003**  
    >   
    >  **Zertifikatempfänger**: **Windows XP/Server 2003**  

5.  Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Vorlagennamen zum Generieren der Webzertifikate ein, die von Configuration Manager-Standortsystemen verwendet werden, beispielsweise **ConfigMgr-MDM-Webserver**.  

6.  Klicken Sie auf der Registerkarte **Antragstellername** auf **Build from Active Directory information** (Aus diesen Active Directory-Informationen erstellen), und geben Sie als Format für den Namen des Antragstellers **DNS-Name** ein. Deaktivieren Sie das Kontrollkästchen des alternativen Antragstellernamens, wenn **Benutzerprinzipalname (UPN)** ausgewählt ist.  

7.  Klicken Sie auf die Registerkarte **Sicherheit** , und entfernen Sie aus den Sicherheitsgruppen **Domänen-Admins** und **Organisations-Admins** die Berechtigung **Anmelden**.  

8.  Klicken Sie auf **Hinzufügen**, geben Sie in das Textfeld **ConfigMgr-MDM-Server** ein, und klicken Sie dann auf **OK**.  

9. Wählen Sie für diese Gruppe die Berechtigung **Anmelden** aus, und lassen Sie die Berechtigung **Lesen** aktiviert.  

10. Klicken Sie auf **OK**, und schließen Sie die Zertifikatvorlagenkonsole.  

11. Klicken Sie in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, klicken Sie auf **Neu**und dann auf **Auszustellende Zertifikatvorlage**.  

12. Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage **ConfigMgr – Verwaltung mobiler Geräte – Webserver** aus, und klicken Sie dann auf **OK**.  

##  <a name="bkmk_requestCert"></a> Anfordern des Webserverzertifikats für jede Standortsystemrolle  
 Zwischen Geräten, die für die lokale Verwaltung mobiler Geräte registriert wurden, und SSL\-Endpunkten, auf denen der Registrierungspunkt, der Registrierungsproxypunkt, der Verteilungspunkt und der Geräteverwaltungspunkt gehostet werden, muss eine Vertrauensstellung bestehen.  In den folgenden Schritten wird beschrieben, wie Sie das Webserverzertifikat für IIS anfordern. Dies muss für jeden Server (SSL-Endpunkt) erfolgen, der eine der für die lokale Verwaltung mobiler Geräte erforderlichen Standortsystemrollen hostet.  

1.  Öffnen Sie auf dem primären Standortserver eine Eingabeaufforderung mit Administratorberechtigung, geben Sie **MMC** ein, und drücken Sie die **EINGABETASTE**.  

2.  Klicken Sie in der MMC auf **Datei**  >  **Snap-In hinzufügen/entfernen**.  

3.  Wählen Sie im Snap-In „Zertifikate“ **Zertifikate** aus. Klicken Sie auf **Hinzufügen**, und wählen Sie **Computerkonto** aus. Klicken Sie auf **Weiter**, anschließend auf **Fertig stellen** und schließlich auf **OK**, um das Fenster „Snap-In hinzufügen/entfernen“ zu schließen.  

4.  Klicken Sie mit der rechten Maustaste auf **Persönlich**. Klicken Sie anschließend auf **Alle Tasks**  >  **Neues Zertifikat anfordern**.  

5.  Klicken Sie im Assistenten für die Zertifikatregistrierung auf **Weiter**, wählen Sie **Active Directory-Registrierungsrichtlinie** aus, und klicken Sie auf **Weiter**.  

6.  Aktivieren Sie das Kontrollkästchen neben dem Webserverzertifikat (**ConfigMgr – Verwaltung mobiler Geräte – Webserver**), und klicken Sie anschließend auf **Registrieren**.  

7.  Sobald das Zertifikat registriert ist, klicken Sie auf **Fertig stellen**.  

 Da jeder Server ein eindeutiges Webserverzertifikat benötigt, müssen Sie diesen Prozess für jeden Server wiederholen, auf dem eine der für die lokale Verwaltung mobiler Geräte erforderlichen Standortsystemrollen gehostet werden.  Wenn ein Server alle Standortsystemrollen hostet, müssen Sie nur ein Webserverzertifikat anfordern.  

##  <a name="bkmk_bindCert"></a> Binden des Zertifikats an den Webserver  
 Das neue Zertifikat muss nun an den Webserver aller Standortsystemserver gebunden werden, auf denen die für die lokale Verwaltung mobiler Geräte erforderlichen Standortsystemrollen gehostet werden. Führen Sie die folgenden Schritte für jeden Server aus, der die Standortsystemrollen „Anmeldungspunkt“ und „Anmeldungsproxypunkt“ hostet. Wenn ein Server alle Standortsystemrollen hostet, müssen Sie die folgenden Schritte nur einmal ausführen. Diese Aufgabe muss nicht für die Standortsystemrollen „Verteilungspunkt“ und „Geräteverwaltungspunkt“ erfolgen, da diese während der Registrierung automatisch das benötigte Zertifikat erhalten.  

1.  Klicken Sie auf dem Server, der den Anmeldungspunkt, Anmeldungsproxypunkt, Verteilungspunkt oder Geräteverwaltungspunkt hostet, auf **Start**  >  **Verwaltung**  >  **IIS-Manager**.  

2.  Navigieren Sie unter „Verbindungen“ zu **Standardwebsite**. Klicken Sie mit der rechten Maustaste darauf, und klicken Sie anschließend auf **Bindungen bearbeiten...**.  

3.  Klicken Sie im Dialogfeld „Websitebindungen“ auf **https**, und klicken Sie anschließend auf **Bearbeiten...**.  

4.  Wählen Sie im Dialogfeld „Websitebindung bearbeiten“ das Zertifikat aus, das Sie zuvor für das **SSL-Zertifikat** registriert haben. Klicken Sie auf **OK** und anschließend auf **Schließen**.  

5.  Wählen Sie in der IIS-Manager-Konsole unter „Verbindungen“ den Webserver aus, und klicken Sie anschließend im rechten Aktionsbereich auf **Neu starten**.  

##  <a name="bkmk_exportCert"></a> Exportieren des Zertifikats mit demselben Stamm wie das Webserverzertifikat  
 Die Active Directory-Zertifikatdienste installieren in der Regel das von der Zertifizierungsstelle benötigte Zertifikat auf allen zur Domäne gehörenden Geräten. Nicht zur Domäne gehörige Geräte können aber ohne Zertifikat von der Stammzertifizierungsstelle nicht mit den Standortsystemrollen kommunizieren. Zum Abrufen des erforderlichen Zertifikats für Geräte zur Kommunikation mit Standortsystemrollen können Sie es mithilfe des Zertifikats exportieren, das an den Webserver gebunden ist.  

 Führen Sie diese Schritte aus, um das Stammzertifikat des Zertifikats des Webservers zu exportieren.  

1.  Klicken Sie im IIS-Manager auf **Standardwebsite** und anschließend im rechten Aktionsbereich auf **Bindungen...**.  

2.  Klicken Sie im Dialogfeld „Websitebindungen“ auf **https** und anschließend auf **Bearbeiten...**.  

3.  Stellen Sie sicher, dass das Webserverzertifikat ausgewählt ist, und klicken Sie auf **Anzeigen...**.  

4.  Klicken Sie in den Eigenschaften des Webserverzertifikats auf **Zertifizierungspfad**, anschließend auf den Stamm am oberen Rand des Zertifizierungspfads und schließlich auf **Zertifikat anzeigen**.  

5.  Klicken Sie in den Eigenschaften des Stammzertifikats auf **Details** und anschließend auf **In Datei kopieren...**.  

6.  Klicken Sie im Assistenten zum Exportieren von Zertifikaten auf **Weiter**.  

7.  Stellen Sie sicher, dass als Format **DER-codierte binäre X.509-Datei (.CER)** ausgewählt ist, und klicken Sie auf **Weiter**.  

8.  Klicken Sie für den Dateinamen auf **Durchsuchen...**, wählen Sie einen Speicherort zum Speichern der Zertifikatdatei, geben Sie der Datei einen Namen, und klicken Sie auf **Speichern**.  

     Zu registrierende Geräte müssen auf diese Datei zugreifen, um das Stammzertifikat zu importieren. Wählen Sie deshalb einen allgemeinen Speicherort, auf den die meisten Computer und Geräte zugreifen können. Sie können die Datei auch erst an einem geeigneten Speicherort speichern (z. B. auf Laufwerk C) und später an einen allgemeinen Speicherort verschieben.  

     Klicken Sie auf **Weiter**.  

9. Überprüfen Sie die Einstellungen, und klicken Sie auf **Fertig stellen**.  
