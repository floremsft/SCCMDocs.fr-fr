---
title: Einrichten Ihres Lookout-Abonnements | System Center Configuration Manager
description: "Das vorliegende Thema enthält Details dazu, wie Sie den Lookout-Schutz vor Gerätebedrohungen konfigurieren."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: b777140c753e709f4048a30e63d8ae730d3e8723
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-your-subscription-for--lookout-device-threat-protection"></a>Einrichten Ihres Lookout-Abonnements zum Schutz vor Gerätebedrohungen

*Gilt für: System Center Configuration Manager (Current Branch)*

Für die Vorbereitung Ihres Lookout-Abonnements zum Schutz vor Gerätebedrohungen benötigt der Lookout-Support (enterprisesupport@lookout.com) folgende Informationen zu Ihrem Azure Active Directory-Abonnement (Azure AD). Ihr Lookout Mobility Endpoint Security-Mandant wird Ihrem Azure AD-Abonnement zugeordnet, um Lookout in Intune zu integrieren. 

* **Azure AD-Mandanten-ID**
* **Azure AD-Gruppenobjekt-ID** für einen **vollständigen** Lookout-Konsolenzugriff
* **Azure AD-Gruppenobjekt-ID** für einen **eingeschränkten** Lookout-Konsolenzugriff (optional)

> [!IMPORTANT]
> Ein vorhandener Lookout Mobility Endpoint Security-Mandant, der nicht bereits Ihrem Azure AD-Mandanten zugeordnet ist, kann nicht für die Integration mit Azure AD und Intune verwendet werden. Wenden Sie sich an den Lookout-Support, um einen neuen Lookout Mobility Endpoint Security-Mandanten zu erstellen. Verwenden Sie den neuen Mandanten für die Integration Ihrer Azure AD-Benutzer.

Im folgenden Abschnitt erfahren Sie, wie Sie die Informationen zusammenstellen, die das Lookout-Supportteam benötigt.  

## <a name="get-your-azure-ad-information"></a>Zusammenstellen Ihrer Informationen zu Azure AD
### <a name="azure-ad-tenant-id"></a>Azure AD-Mandanten-ID
Melden Sie sich beim [Azure AD-Verwaltungsportal](https://manage.windowsazure.com) an, und wählen Sie Ihr Abonnement aus. 

![Screenshot der Azure AD-Seite mit dem Namen des Mandanten](media/aad_tenant_name.png) Wenn Sie den Namen Ihres Abonnements auswählen, enthält die resultierende URL die Abonnement-ID.  Wenn Sie Ihre Abonnement-ID nicht finden können, lesen Sie folgenden [Microsoft-Supportartikel](https://support.office.com/en-us/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b?ui=en-US&rs=en-US&ad=US), der Tipps für die Suche nach Ihrer Abonnement-ID enthält.   
### <a name="azure-ad-group-id"></a>Azure AD-Gruppen-ID
Die Lookout-Konsole unterstützt zwei Zugriffsebenen:  
* **Vollzugriff:** Der Azure AD-Administrator kann eine Gruppe für Benutzer erstellen, die Vollzugriff haben, und optional eine Gruppe für Benutzer, die über eingeschränkten Zugriff verfügen.  Nur die Benutzer dieser Gruppen können sich an der **Lookout-Konsole** anmelden.
* **Eingeschränkter Zugriff:** Benutzer dieser Gruppe haben keinen Zugriff auf verschiedene Konfigurations- und Registrierungsmodule in der Lookout-Konsole. Sie verfügen lediglich über Lesezugriff auf das **Sicherheitsrichtlinienmodul** der Lookout-Konsole.  

Weitere Einzelheiten zu den Berechtigungen finden Sie in [ diesem Artikel](https://personal.support.lookout.com/hc/en-us/articles/114094105653) auf der Lookout-Website.

Die **Gruppenobjekt-ID**  befindet sich auf der Seite **Eigenschaften** der Gruppe in der **Azure AD-Verwaltungskonsole**.

![Screenshot der Eigenschaftenseite mit hervorgehobenem GroupID-Feld](media/aad_group_object_id.png)

Nachdem Sie diese Informationen zusammengestellt haben, wenden Sie sich an den Lookout-Support (E-Mail-Adresse: enterprisesupport@lookout.com).

Der Lookout-Support wendet sich an Ihren primären Kontakt, um Ihr Abonnement zu integrieren und Ihr Lookout Enterprise-Konto anhand der von Ihnen gesammelten Informationen zu erstellen.


## <a name="configure-your-subscription-with-lookout-device-threat-protection"></a>Konfigurieren Ihres Lookout-Abonnements zum Schutz vor Gerätebedrohungen
### <a name="step-1-set-up-your-device-threat-protection"></a>Schritt 1: Einrichten des Schutzes vor Gerätebedrohungen
Nachdem Ihr Lookout Enterprise-Konto vom Lookout-Support erstellt wurde, können Sie sich an der Lookout-Konsole anmelden.   Der primäre Kontakt für Ihr Unternehmen erhält eine E-Mail von Lookout, die einen Link mit einer Anmelde-URL enthält: https://aad.lookout.com/les?action=consent

Sie müssen bei Ihrer ersten Anmeldung an der Lookout-Konsole ein Benutzerkonto mit der Azure AD-Rolle des globalen Administrators verwenden, da Lookout diese Informationen benötigt, um Ihren Azure AD-Mandanten zu registrieren.   Bei nachfolgenden Anmeldungen ist diese Ebene der Azure AD-Berechtigungen für die Benutzer nicht erforderlich.  Bei dieser ersten Anmeldung wird eine Zustimmungsseite angezeigt. Wählen Sie **Annehmen** aus, um die Registrierung durchzuführen.

![Screenshot der Seite für die erste Anmeldung an der Lookout-Konsole](media/lookout-initial-login.png)

Nachdem Sie die Bedingungen akzeptiert und ihnen zustimmt haben, werden Sie an die Lookout-Konsole weitergeleitet. Nachfolgende Anmeldungen im Anschluss an die erste Registrierung erfolgen mithilfe folgender URL: https://aad.lookout.com

Wenn Sie bei der Anmeldung Probleme haben, finden Sie weitere Informationen im [Artikel zur Problembehandlung]().

Die nächsten Schritte beschreiben, was Sie tun müssen, um das Lookout-Setup innerhalb der [Lookout-Konsole](https://aad.lookout.com) durchzuführen.

### <a name="step-2-configure-the-intune-connector"></a>Schritt 2: Konfigurieren des Intune-Connectors

1.  Wählen Sie in der Lookout-Konsole aus dem Modul **System** die Registerkarte **Connectors** und anschließend **Intune** aus.

  ![Screenshot der Lookout-Konsole mit der geöffneten Registerkarte „Connectors“ und der hervorgehobenen Intune-Option](media/lookout-setup-intune-connector.png)

2.  Konfigurieren Sie in den Einstellungsoptionen des Connectors die Taktfrequenz in Minuten.  Der Intune-Connector ist nun bereit.  

  ![Screenshot der Registerkarte für die Verbindungseinstellungen mit der konfigurierten Taktfrequenz](media/lookout-connection-settings.png)

### <a name="step-3-configure-enrollment-groups"></a>Schritt 3: Konfigurieren von Registrierungsgruppen
Legen Sie in der Option für die **Registrierungsverwaltung** eine Gruppe von Benutzern fest, deren Geräte mit Lookout registriert werden sollen. Es hat sich bewährt, zunächst einen Test mit einer kleinen Gruppe von Benutzern durchzuführen, um sich mit der Funktionsweise der Integration vertraut zu machen.  Wenn Sie mit den Testergebnissen zufrieden sind, können Sie die Registrierung auf weitere Gruppen von Benutzern ausweiten.

Legen Sie zum Einstieg in die Registrierungsgruppen zunächst eine Azure AD-Sicherheitsgruppe fest. Sie sollte aus Benutzern bestehen, die sich für eine erste Registrierung beim Lookout-Schutz vor Gerätebedrohungen eignen. Nachdem Sie die Gruppe in der Lookout-Konsole in Azure AD erstellt haben, wechseln Sie zur Option **Registrierungsverwaltung**, und fügen Sie der Azure AD-Sicherheitsgruppe den **Anzeigenamen** für die Registrierung hinzu.

Wenn ein Benutzer zu einer Registrierungsgruppe gehört, werden alle in Azure AD erkannten und unterstützten Geräte registriert und sind für den Lookout-Schutz vor Gerätebedrohungen berechtigt.  Beim ersten Öffnen der Lookout for Work-App auf dem unterstützten Gerät wird dieses in Lookout aktiviert.

![Screenshot der Seite mit der Intune Connector-Registrierung](media/lookout-enrollment.png)

Es wird empfohlen, beim Suchen nach neuen Geräten als Zeitintervall den Standardwert (5 Minuten) zu verwenden.

>[!IMPORTANT]
> Beachten Sie bei der Eingabe des Anzeigenamens die Groß- und Kleinschreibung.  Verwenden Sie den **Anzeigenamen** wie auf der Seite **Eigenschaften** der Sicherheitsgruppe im Azure-Portal gezeigt. Beachten Sie in der Abbildung unten, dass auf der Seite **Eigenschaften** der Sicherheitsgruppe für den Anzeigenamen die Camel-Case-Schreibweise gilt.  Der Titel hingegen wird in Kleinbuchstaben angezeigt und sollte nicht für die Eingabe in die Lookout-Konsole verwendet werden.
>![Screenshot des Azure-Portals, Azure Active Directory-Dienst, Eigenschaftenseite](media/aad-group-display-name.png)

Die aktuelle Version weist die folgenden Nachteile auf:  
* Es gibt keine Validierung für die Anzeigenamen der Gruppe.  Verwenden Sie immer den Wert im Feld **ANZEIGENAMEN**, das im Azure-Portal für die Azure AD-Sicherheitsgruppe angezeigt wird.
* Das Erstellen von Gruppen innerhalb anderer Gruppen wird derzeit nicht unterstützt.  Angegebene Azure AD-Sicherheitsgruppen dürfen nur Benutzer und keine verschachtelten Gruppen enthalten.


### <a name="step-4-configure-state-sync"></a>Schritt 4: Konfigurieren der Statussynchronisierung
Geben Sie in der Option **State Sync** (Statussynchronisierung) den Typ der Daten an, die an Intune gesendet werden sollen.  Derzeit müssen Sie sowohl den Geräte- als auch den Bedrohungsstatus aktivieren, damit die Integration von Lookout in Intune ordnungsgemäß ausgeführt wird.  Diese Einstellungen sind standardmäßig aktiviert.
### <a name="step-5-configure-error-report-email-recipient-information"></a>Schritt 5: Konfigurieren der E-Mail-Empfänger von Fehlerberichten
Geben Sie in der Option zur **Fehlerverwaltung** die E-Mail-Adresse der Person ein, die die Fehlerberichte erhalten soll.

![Screenshot der Seite mit der Intune-Connector-Fehlerverwaltung](media/lookout-connector-error-notifications.png)

### <a name="step-6-configure-enrollment-settings"></a>Schritt 6: Konfigurieren der Registrierungseinstellungen
Geben Sie im Modul **System** auf der Seite **Connectors** ein, nach wie vielen Tagen ein Gerät als getrennt gilt.  Getrennte Geräte gelten als nicht konform und dürfen nicht auf Ihre Unternehmensanwendungen zugreifen. Dies wird durch die SCCM-Richtlinien für bedingten Zugriff geregelt. Sie können Werte zwischen 1 und 90 Tagen angeben.

![](media/lookout-console-enrollment-settings.png)

### <a name="step-7-configure-email-notifications"></a>Schritt 7: Konfigurieren von E-Mail-Benachrichtigungen
Wenn Sie bei Bedrohungen E-Mail-Benachrichtigungen erhalten möchten, melden Sie sich an der [Lookout-Konsole](https://aad.lookout.com) mit dem Benutzerkonto an, das die Benachrichtigung erhalten soll. Wählen Sie auf der Registerkarte**Preferences** (Voreinstellungen) im Modul **System** die gewünschten Benachrichtigungen aus, und setzen Sie sie auf **ON** (Ein). Speichern Sie die Änderungen.

![Screenshot der Voreinstellungsseite mit dem angezeigten Benutzerkonto ](media/lookout-email-notifications.png) Wenn Sie keine E-Mail-Benachrichtigungen mehr erhalten möchten, setzen Sie die Benachrichtigungen auf **OFF** (Aus), und speichern Sie die Änderungen.
### <a name="step-8-configure-threat-classification"></a>Schritt 8: Konfigurieren der Bedrohungsklassifizierung
Der Lookout-Schutz vor Gerätebedrohungen sieht unterschiedliche Klassifizierungen mobiler Bedrohungen vor. Mit jeder [Lookout-Bedrohungsklassifizierung](http://personal.support.lookout.com/hc/en-us/articles/114094130693) ist eine standardmäßige Risikostufe verknüpft. Diese kann jederzeit entsprechend den Anforderungen Ihres Unternehmen geändert werden.

![Screenshot der Richtlinienseite, die Bedrohungsarten und Klassifizierungen anzeigt](media/lookout-threat-classification.png)

>[!IMPORTANT]
> Die hier angegebenen Risikostufen stellen einen wichtigen Aspekt des Schutzes vor Gerätebedrohungen dar, denn bei der Intune-Integration wird die Gerätekonformität gemäß den Risikostufen bei Laufzeit berechnet. Anders ausgedrückt: Der Intune-Administrator legt eine Regel in der Richtlinie fest, um ein Gerät als nicht konform zu identifizieren, wenn für das Gerät eine aktive Bedrohung mit folgender Mindeststufe gilt: hoch, mittel oder niedrig. Die Richtlinie zur Bedrohungsklassifizierung im Lookout-Schutz vor Gerätebedrohungen bestimmt auf direkte Art und Weise die Berechnung der Gerätekonformität in Intune.

## <a name="watching-enrollment"></a>Überwachen der Registrierung
Nach Abschluss des Setups beginnt der Lookout-Schutz vor Gerätebedrohung mit der Suche nach Geräten in Azure AD, die den angegebenen Registrierungsgruppen entsprechen.  Informationen zu den registrierten Geräten finden Sie im Gerätemodul.  Der anfängliche Status für Geräte wird als „ausstehend“ angezeigt.  Dieser Status ändert sich, sobald die Lookout for Work-App installiert, geöffnet und auf dem Gerät aktiviert wird.  Weitere Informationen zum Installieren der Lookout for Work-App auf dem Gerät finden Sie unter dem Thema [Configure and deploy Lookout for work apps (Konfigurieren und Bereitstellen von Lookout for Work-Apps)](configure-and-deploy-lookout-for-work-apps.md).
## <a name="next-steps"></a>Nächste Schritte
[Enable Lookout MTP connection in Intune (Aktivieren einer Lookout MTP-Verbindung in Intune)](enable-lookout-connection-in-intune.md)
