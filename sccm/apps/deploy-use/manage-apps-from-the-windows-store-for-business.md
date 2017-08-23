---
title: "Verwalten von Apps aus dem Windows Store für Unternehmen | Microsoft-Dokumentation"
description: "Verwalten Sie Apps aus dem Windows Store für Unternehmen, und stellen Sie sie mithilfe von System Center Configuration Manager bereit."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: "11"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 369b6a82a20a90ca534f9484c0be71096dd35a30
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Verwalten von Apps aus dem Windows Store für Unternehmen mit System Center Configuration Manager
Im [Windows Store für Unternehmen](https://www.microsoft.com/business-store) können Sie Windows-Apps für Ihre Organisation finden, und entweder einzeln oder per Volumenlizenz erwerben. Indem Sie den Store mit Configuration Manager verbinden, können Sie die Liste der erworbenen Apps mit Configuration Manager synchronisieren. Sie können anschließend diese Apps in der Configuration Manager-Konsole anzeigen und sie bereitstellen, wie Sie jede andere App bereitstellen würden.


## <a name="online-and-offline-apps"></a>Online- und Offline-Apps

Der Windows Store für Unternehmen unterstützt zwei Typen von Apps:

- **Online** – Dieser Lizenztyp setzt voraus, dass Benutzer und Geräte mit dem Store verbunden sind, um eine App und ihre Lizenz zu erhalten. Windows 10-Geräte müssen in die Azure Active Directory-Domäne eingebunden sein.
- **Offline** – Sie können Apps und Lizenzen zwischenspeichern und sie direkt in ihren lokalen Netzwerken bereitstellen, ohne eine Verbindung zum Store herzustellen oder ohne eine Internetverbindung.

[Erfahren Sie mehr](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview?f=255&MSPPError=-2147217396) über den Windows Store für Unternehmen.

Configuration Manager unterstützt die Verwaltung von Apps aus dem Windows Store für Unternehmen sowohl auf Windows 10-Geräten, auf denen der Configuration Manager-Client ausgeführt wird, als auch auf Windows 10-Geräten, die bei Microsoft Intune registriert sind (sogenannte Mischkonfiguration). Configuration Manager bietet die folgenden Funktionen für Online- und Offline-Apps.

> [!IMPORTANT]
> Um diese Funktion verwenden zu können, muss auf den Windows 10-Geräten das Release vom November 2015 (1511) oder höher ausgeführt werden.


|Funktion|Offline-Apps|Online-Apps|
|------------|------------|------------|
|Synchronisieren von App-Daten mit Configuration Manager<br>(Synchronisierung erfolgt alle 24 Stunden)|Ja|Ja|
|Erstellen von Configuration Manager-Anwendungen aus Store-Apps|Ja|Ja|
|Unterstützung für kostenlose Apps aus dem Store|Ja|Ja|
|Unterstützung für kostenpflichtige Apps aus dem Store|Nein|Ja|
|Unterstützen von erforderlichen Bereitstellungen für Benutzer- oder Gerätesammlungen|Ja|Ja|
|Unterstützen von verfügbaren Bereitstellungen für Benutzer- oder Gerätesammlungen|Ja|Ja|
|Unterstützung von branchenspezifischen Apps aus dem Store|Ja|Ja|

Um online-lizenzierte Apps für Windows 10-PCs mit dem Configuration Manager-Client bereitzustellen, müssen sie Windows 10 Creators Update oder höher ausführen.

## <a name="deploying-online-apps-using-the-windows-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>Bereitstellen von Online-Apps mithilfe von Windows Store für Unternehmen mit PCs, die den Configuration Manager-Client ausführen
Vor der Bereitstellung von Windows Store für Unternehmen-Apps auf PCs, die den vollständigen Configuration Manager-Client ausführen, ist Folgendes zu beachten:

- Für die vollständige Funktionalität muss auf PCs Windows 10 Creators Update oder höher ausgeführt werden.
- PCs müssen mit dem Arbeitsplatz Azure Active Directory verknüpft sein und sich im gleichen AAD-Mandanten befinden, in dem Sie Windows Store für Unternehmen als Verwaltungstool registriert haben.
- Wenn PCs mit dem integrierten Administratorkonto angemeldet sind, können sie nicht auf Windows Store für Unternehmen-Apps zugreifen.
- PCs benötigen eine aktive Internetverbindung zum Windows Store für Unternehmen.

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>Hinweise für PCs mit früheren Versionen von Windows 10
Auf PCs mit einer früheren Version von Windows 10 als Creators Update (mit dem Configuration Manager-Client) gelten die folgenden Funktionen:


- Wenn die Installation erzwungen wird, entweder vom Benutzer, der die Anwendung installiert, von der Anwendung, die ihren Stichtag für die Installation erreicht, oder durch eine erneute Bewertung nach der Installation für erforderliche Bereitstellungen:
    - Die Anwendung wird durch den Start der Windows Store für Unternehmen-App „erzwungen“. 
    - Endbenutzer müssen dann die Installation aus dem Store abschließen, bevor die App installiert wird.
    - Der Status der Anwendung in der Configuration Manager-Konsole meldet den Fehler „Die Windows Store-App wurde auf dem Client-PC geöffnet und wartet auf den Abschluss der Installation durch den Benutzer“.
- Im nächsten Evaluierungszyklus für die Anwendung:
    - Wenn die Anwendung vom Endbenutzer aus dem Store installiert wurde, meldet die Anwendung den Status **Erfolg**. 
    - Wenn der Endbenutzer nicht versucht hat, die Anwendung aus dem Store zu installieren:
        - Erforderliche Bereitstellungen versuchen, den Store zu starten und die Installation der Anwendung erneut zu erzwingen.
        - Verfügbare Bereitstellungen werden nicht erneut erzwungen.

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>Weitere Hinweise für PCs mit früheren Versionen von Windows 10:

- Sie können keine branchenspezifischen Apps aus dem Windows Store für Unternehmen bereitstellen.
- Wenn Sie kostenpflichtige Apps aus dem Store bereitstellen, müssen Endbenutzer sich im Store anmelden und die App selbst erwerben.
- Wenn Sie eine Gruppenrichtlinie bereitgestellt haben, die den Zugriff auf die Benutzerversion von Windows Store deaktiviert, funktionieren Bereitstellungen aus dem Windows Store für Unternehmen nicht, auch wenn der Windows Store für Unternehmen aktiviert ist.


## <a name="set-up-windows-store-for-business-synchronization"></a>Einrichten der Synchronisierung mit Windows Store für Unternehmen

### <a name="for-configuration-manager-versions-prior-to-1706"></a>Für Versionen des Configuration Manager vor 1706

**Registrieren Sie Configuration Manager über „Webanwendung und/oder Web-API“ als Verwaltungstool in Azure Active Directory. Durch diese Aktion erhalten Sie eine Client-ID, die Sie später benötigen.**
1. Wählen Sie im Active Directory-Knoten, [https://manage.windowsazure.com](https://manage.windowsazure.com), Ihr Azure Active Directory aus, und klicken Sie anschließend auf **Anwendungen** > **Hinzufügen**.
2.  Klicken Sie auf **Eine von meinem Unternehmen entwickelte Anwendung hinzufügen**.
3.  Geben Sie einen Namen für die Anwendung ein, wählen Sie **Webanwendung** und/oder **Web-API** aus, und klicken Sie anschließend auf den Pfeil **Weiter**.
4.  Geben Sie die gleiche URL für die **Registrierungs-URL** und die **App-ID-URI** ein. Dabei kann es sich um eine beliebige URL handeln, die nicht in eine reale Adresse aufgelöst werden muss. Sie können z.B. *https://yourdomain/sccm* eingeben.
5.  Schließen Sie den Assistenten ab.

**Erstellen eines Clientschlüssels für das registrierte Verwaltungstool in Azure Active Directory**
1.  Markieren Sie die Anwendung, die Sie erstellt haben, und klicken Sie auf **Konfigurieren**.
2.  Wählen Sie unter **Schlüssel** eine Dauer aus der Liste aus, und klicken Sie anschließend auf **Speichern**. Diese Aktion erstellt einen neuen Clientschlüssel. Verlassen Sie diese Seite nicht, bevor Sie Windows Store für Unternehmen erfolgreich in Configuration Manager eingebunden haben.

**Konfigurieren von Configuration Manager als Speicherverwaltungstool im Windows Store für Unternehmen**
1.  Öffnen Sie [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools), und melden Sie sich nach entsprechender Aufforderung an.
2.  Akzeptieren Sie gegebenenfalls die Nutzungsbedingungen.
3.  Klicken Sie unter **Verwaltungstools** auf **Verwaltungstool hinzufügen**.
4.  Geben Sie unter **Tool nach Namen suchen** den Namen der App ein, die Sie zuvor in AAD erstellt haben, und klicken Sie anschließend auf **Hinzufügen**.
5.  Klicken Sie neben der Anwendung, die Sie importiert haben, auf **Aktivieren**.
6.  Wählen Sie auf der Seite **Verwalten > Kontoinformationen** die Option **Offline lizenzierte Apps anzeigen** aus, wenn Sie den Einkauf offline lizenzierter Anwendungen zulassen möchten.

**Hinzufügen des Store-Kontos zu Configuration Manager**

1. Stellen Sie sicher, dass Sie mindestens eine App aus dem Windows Store für Unternehmen erworben haben. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** den Eintrag **Clouddienste**, und klicken Sie dann auf **Windows Store für Unternehmen**.
2.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Windows Store für Unternehmen** auf **Windows Store für Unternehmen-Konto hinzufügen**. 
3.  Fügen Sie Mandanten-ID, Client-ID und Clientschlüssel aus Azure Active Directory hinzu, und schließen Sie den Assistenten ab.
4. Sobald Sie fertig sind, wird das von Ihnen konfigurierte Konto in der Liste **Windows Store für Unternehmen** der Configuration Manager-Konsole aufgeführt.

### <a name="for-configuration-manager-version-1706-and-later"></a>Für Versionen des Configuration Manager ab 1706 und höher

1. Wechseln Sie in der Konsole zu **Verwaltung** > **Übersicht** > **Cloud Services Management** (Verwaltung der Clouddienste) > **Azure** > **Azure-Dienste**, und wählen Sie dann **Configure Azure Services** (Azure-Dienste konfigurieren) aus, um den **Azure-Dienste-Assistenten** zu starten.
2. Wählen Sie auf der Seite **Azure-Dienste** den Dienst aus, den Sie konfigurieren möchten, und klicken Sie dann auf **Weiter**.
3. Geben Sie auf der Seite **Allgemein** einen Anzeigenamen für den Azure-Dienstnamen und eine optionale Beschreibung ein, und klicken Sie dann auf **Weiter**.
4. Auf der **App** Seite geben Sie Ihre Azure-Umgebung an und klicken dann auf **Durchsuchen**, um das Fenster **Server-App** zu öffnen.
5. Wählen Sie im Fenster **Server-App** die Server-App aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**. Server-Apps sind Azure-Web-Apps, die Konfigurationen für Ihr Azure-Konto enthalten, einschließlich Ihrer Mandanten-ID, Client-ID und eines geheimen Schlüssels für Clients. Wenn Sie nicht über eine verfügbare Server-App verfügen, verwenden Sie eine der folgenden:
    - **Erstellen**: Um eine neue Server-App zu erstellen, klicken Sie auf **Erstellen**. Geben Sie einen Anzeigenamen für die App und den Mandanten an. Nachdem Sie sich bei Azure angemeldet haben, erstellt Configuration Manager daraufhin die Web-App in Azure für Sie, einschließlich der Client-ID und des geheimen Schlüssels für den Gebrauch mit der Web-App. Später können Sie diese im Azure-Portal anzeigen.
    - **Importieren**: Um eine Web-App zu verwenden, die in Ihrem Azure-Abonnement bereits vorhanden ist, klicken Sie auf **Importieren**. Stellen Sie einen Anzeigenamen für die App und den Mandanten bereit, und geben Sie dann die Mandanten-ID, Client-ID und den geheimen Schlüssel für die Web-App an, die Configuration Manager verwenden soll. Nachdem Sie die Informationen **überprüft** haben, klicken Sie auf **OK**, um fortzufahren. 
6. Überprüfen Sie die Seite **Informationen**, und schließen Sie alle zusätzlichen Schritte und Konfigurationen so wie angegeben ab. Diese Konfigurationen sind erforderlich, um den Dienst mit Configuration Manager zu verwenden. Beispielsweise um den Windows Store für Unternehmen zu konfigurieren:
    - In Azure müssen Sie Configuration Manager als eine Web-Anwendung oder eine Web-API registrieren und die Client-ID notieren. Außerdem geben Sie einen Clientschlüssel für die Verwendung durch das Verwaltungstool (das ist Configuration Manager) an.
    - In der Konsole des Windows Store für Unternehmen müssen Sie Configuration Manager als Speicherverwaltungstool angeben, Unterstützung für Offline-lizenzierte Apps aktivieren und anschließen mindestens eine App kaufen. 
7. Klicken Sie zum Fortfahren auf **Weiter**.
8. Schließen Sie auf der Seite **App Configurations** (App-Konfigurationen) die Konfigurationen für den App-Katalog und die Sprache für diesen Dienst ab, und klicken Sie dann auf **Weiter**.
9. Nach Abschluss des Assistenten zeigt die Configuration Manager-Konsole, dass Sie **Windows Store for Business** als **Clouddiensttyp** konfiguriert haben.




## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>Erstellen und Bereitstellen einer Configuration Manager-Anwendung aus einer App aus dem Windows Store für Unternehmen
1.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** der Configuration Manager-Konsole **Anwendungsmanagement**, und klicken Sie anschließend auf **Lizenzinformationen für Store-Apps**.
2.  Wählen Sie zunächst die App aus, die Sie bereitstellen möchten. Klicken Sie anschließend auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Anwendung erstellen**.
Eine Configuration Manager-App wird erstellt, die eine App aus dem Windows Store für Unternehmen enthält. Sie können diese Anwendung wie jede andere Configuration Manager-Anwendung bereitstellen und überwachen.

> [!IMPORTANT]
> Für Geräte, die bei Intune registriert sind, stehen bereitgestellte Apps nur für diejenigen Benutzer zur Verfügung, die sie ursprünglich registriert haben. Andere Benutzer können nicht auf die App zugreifen.

## <a name="next-steps"></a>Nächste Schritte

Erweitern Sie im Arbeitsbereich **Softwarebibliothek** die Option **Anwendungsmanagement**, und klicken Sie anschließend auf **Lizenzinformationen für Store-Apps**.

Sie können für jede von Ihnen verwaltete Store-App Informationen anzeigen, wie den Namen, die Plattform, die Anzahl der Lizenzen, die Sie für diese App besitzen, sowie die Anzahl der Lizenzen, die Ihnen zur Verfügung stehen.
