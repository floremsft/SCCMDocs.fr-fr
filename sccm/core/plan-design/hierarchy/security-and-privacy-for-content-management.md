---
title: "Sicherheit und Datenschutz für Content Management | Microsoft-Dokumentation"
description: "Optimieren von Sicherheit und Datenschutz für Content Management in System Center Configuration Manager."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: c4b9d13079c313879c6d43b10867c616fa962668
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-content-management-for-system-center-configuration-manager"></a>Sicherheit und Datenschutz für die Inhaltsverwaltung für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält Sicherheits- und Datenschutzinformationen für Content Management in System Center Configuration Manager. Lesen Sie es in Verbindung mit den folgenden Themen:  

-   [Sicherheit und Datenschutz für die Anwendungsverwaltung in System Center Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

-   [Security and privacy for software updates in System Center Configuration Manager (Sicherheit und Datenschutz für Softwareupdates in System Center Configuration Manager)](/sccm/sum/plan-design/security-and-privacy-for-software-updates)  

-   [Security and privacy for operating system deployment in System Center Configuration Manager (Sicherheit und Datenschutz für die Betriebssystembereitstellung in System Center Configuration Manager)](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  

##  <a name="BKMK_Security_ContentManagement"></a> Bewährte Sicherheitsmethoden für die Inhaltsverwaltung  
 Wenden Sie die folgenden bewährten Sicherheitsmethoden bei der Inhaltsverwaltung an:  

 **Ziehen Sie für Verteilungspunkte im Intranet die Vor- und Nachteile von HTTPS und HTTP in Betracht**: In den meisten Szenarios bietet die Verwendung von HTTP und Paketzugriffskonten für die Autorisierung mehr Sicherheit als die Verwendung von HTTPS mit Verschlüsselung, aber ohne Autorisierung. Wenn die Inhalte allerdings vertrauliche Daten umfassen, die bei der Übertragung verschlüsselt werden sollen, verwenden Sie HTTPS.  

-   **Wenn Sie für einen Verteilungspunkt HTTPS verwenden**, werden in Configuration Manager keine Paketzugriffskonten verwendet, um den Zugriff auf die Inhalte zu autorisieren. Stattdessen werden die Inhalte bei der Übermittlung über das Netzwerk verschlüsselt.  

-   **Wenn Sie für einen Verteilungspunkt HTTP verwenden**, können Sie Paketzugriffskonten zur Autorisierung verwenden. Allerdings werden die Inhalte bei der Übermittlung über das Netzwerk nicht verschlüsselt.  


**Wenn Sie für den Verteilungspunkt ein PKI-Clientauthentifizierungszertifikat anstelle eines selbstsignierten Zertifikats verwenden, sollten Sie die Zertifikatdatei (.pfx) mit einem sicheren Kennwort schützen. Wenn Sie die Datei im Netzwerk speichern, sollten Sie den Netzwerkkanal beim Importieren der Datei in Configuration Manager sichern**: Wenn für das Importieren des Clientauthentifizierungszertifikats, das der Verteilungspunkt für die Kommunikation mit Verwaltungspunkten verwenden, ein Kennwort erforderlich ist, ist das Zertifikat vor Angriffen geschützt. Verwenden Sie Server Message Block (SMB)-Signaturen oder IPsec zwischen Netzwerkspeicherort und Standortserver, um einen Angreifer an der Manipulation der Zertifikatdatei zu hindern.  

**Die Verteilungspunktrolle vom Server entfernen**: Ein Verteilungspunkt wird standardmäßig auf demselben Server wie der Standortserver installiert. Für Clients ist die direkte Kommunikation mit dem Standortserver nicht erforderlich. Daher empfiehlt es sich zur Verringerung des Angriffsrisikos, die Verteilungspunktrolle anderen Standortsystemen zuzuweisen und vom Standortserver zu entfernen.  

**Inhalte auf Paketzugriffsebene sichern**: Die Verteilungspunktfreigabe erteilt allen Benutzern Lesezugriff. Verwenden Sie Paketzugriffskonten, wenn der Verteilungspunkt für HTTP konfiguriert ist, um festzulegen, welche Benutzer auf den Inhalt zugreifen können. Dies gilt nicht für cloudbasierte Verteilungspunkte, von denen Paketzugriffskonten nicht unterstützt werden. Weitere Informationen zu Paketzugriffskonten finden Sie unter [Verwalten von Konten für den Zugriff auf Inhalt](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).


**Wenn Configuration Manager beim Hinzufügen der Standortsystemrolle „Verteilungspunkt“ IIS installiert, sollten Sie die HTTP-Umleitung und die IIS-Verwaltungsskripts und -tools entfernen, sobald die Installation des Verteilungspunkts abgeschlossen ist**: Der Verteilungspunkt erfordert weder die HTTP-Umleitung noch IIS-Verwaltungsskripts und -tools. Entfernen Sie diese Rollendienste für die Webserverrolle (IIS), um das Angriffsrisiko zu verringern.  Weitere Informationen zu den Rollendiensten für die Webserverrolle (IIS) für Verteilungspunkte finden Sie unter [Voraussetzungen für Standorte und Standortsysteme](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  

**Paketzugriffsberechtigungen beim Erstellen von Pakten festlegen**: Änderungen der Zugriffskonten für die Paketdateien treten erst nach dem erneuten Bereitstellen des Pakets in Kraft. Legen Sie die Paketzugriffsberechtigungen daher beim Neuerstellen eines Pakets sorgfältig fest. Dies ist besonders wichtig, wenn das Paket groß ist oder an viele Verteilungspunkte verteilt wird und wenn die Netzwerkbandbreite zur Verteilung von Inhalten beschränkt ist.  

**Zugriffskontrollen zum Schützen von Medien mit vorab bereitgestelltem Inhalt implementieren**: Vorab bereitgestellter Inhalt wird komprimiert, aber nicht verschlüsselt. Ein Angreifer könnte die Dateien lesen und ändern, bevor sie auf Geräte heruntergeladen werden. Manipulierte Inhalte werden von Configuration Manager-Clients abgelehnt, aber dennoch heruntergeladen.  

**Importieren Sie vorab bereitgestellten Inhalt ausschließlich mithilfe des ExtractContent-Befehlszeilentools (ExtractContent.exe), das in Configuration Manager enthalten ist, und stellen Sie sicher, dass es von Microsoft signiert ist**: Verwenden Sie zum Vermeiden von Manipulation und Rechteerweiterungen ausschließlich das autorisierte Befehlszeilentool, das im Lieferumfang von Configuration Manager enthalten ist.  

**Den Kommunikationskanal zwischen dem Standortserver und dem Paketquellspeicherort sichern**: Verwenden Sie für die Kommunikation zwischen dem Standortserver und dem Paketquellspeicherort IPsec- oder SMB-Signaturen für die Erstellung von Anwendungen und Paketen. Dadurch verhindern Sie die Manipulation der Quelldateien durch einen Angreifer.  

**Wenn Sie nach der Installation von Verteilungspunktrollen die Standortkonfigurationsoption ändern, sodass sie statt einer Standardwebsite eine benutzerdefinierte verwendet, sollten Sie die virtuellen Standardverzeichnisse entfernen**: Configuration Manager entfernt die alten virtuellen Standardverzeichnisse nicht, wenn Sie anstelle der Standardwebsite eine benutzerdefinierte Website verwenden. Entfernen Sie die virtuellen Verzeichnisse, die ursprünglich von Configuration Manager unter der Standardwebsite erstellt wurden:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**Ihre Abonnementdetails und -zertifikate für cloudbasierte Verteilungspunkte schützen**: Wenn Sie cloudbasierte Verteilungspunkte verwenden, müssen Sie die wertvollen Elemente wie den Benutzernamen und das Kennwort für Ihr Azure-Abonnement, das Azure-Verwaltungszertifikat und das Dienstzertifikat für cloudbasierte Verteilungspunkte schützen. Speichern Sie die Zertifikate an einem sicheren Ort. Verwenden Sie IPsec oder SMB-Signaturen zwischen dem Standortsystemserver und dem Quellspeicherort, wenn Sie beim Konfigurieren des cloudbasierten Verteilungspunkts über das Netzwerk auf die Zertifikate zugreifen.  

**Für cloudbasierte Verteilungspunkte: Überwachen Sie im Hinblick auf die Dienstkontinuität das Ablaufdatum der Zertifikate**: Configuration Manager warnt Sie nicht, wenn die importierten Zertifikate für die Verwaltung cloudbasierter Verteilungspunkte kurz vor dem Ablaufen sind. Sie müssen die Ablaufdaten unabhängig von Configuration Manager überwachen und sicherstellen, dass Sie die Zertifikate erneuern und die neuen Zertifikate vor dem Ablaufdatum importieren. Dies ist besonders wichtig, wenn Sie für Configuration Manager ein cloudbasiertes Verteilungspunkt-Dienstzertifikat von einer externen Zertifizierungsstelle erwerben, weil Sie möglicherweise mehr Zeit zum Beschaffen eines erneuerten Zertifikats benötigen.  

 Wenn eines der Zertifikate abläuft, wird vom Clouddienste-Manager die Statusmeldung mit der ID **9425** generiert, und die Datei CloudMgr.log enthält den Eintrag, dass das Zertifikat abgelaufen ist (**is in expired state**). Das Ablaufdatum wird im UTC-Format (Coordinated Universal Time) angegeben.  

## <a name="security-considerations-for-content-management"></a>Sicherheitsüberlegungen für Content Management  
Bei der Planung von Content Management sollten Sie Folgendes berücksichtigen:  

-   Clients überprüfen Inhalte erst nach dem Herunterladen.  

     Configuration Manager-Clients überprüfen den Hashwert von Inhalten erst nach dem Herunterladen in ihren Clientcache. Wenn ein Angreifer die Liste der herunterzuladenden Dateien oder die Inhalte selbst manipuliert, kann für das Herunterladen auf den Client eine erhebliche Netzwerkbandbreite erforderlich sein, jedoch müssen die Inhalte dann aufgrund des ungültigen Hashwerts verworfen werden.  

-   Wenn Sie cloudbasierte Verteilungspunkte verwenden, wird der Zugriff auf den Inhalt automatisch auf Ihr Unternehmen beschränkt, und Sie können diese Beschränkung nicht auf Benutzer oder Gruppen erweitern.  

-   Wenn Sie cloudbasierte Verteilungspunkte verwenden, werden Clients vom Verwaltungspunkt authentifiziert. Anschließend wird über ein Configuration Manager-Token auf cloudbasierte Verteilungspunkte zugegriffen. Das Token ist acht Stunden lang gültig. Wenn Sie einen Client sperren, weil er nicht mehr vertrauenswürdig ist, kann dieser also noch so lange Inhalte von einem cloudbasierten Verteilungspunkt herunterladen, bis der Gültigkeitszeitraum des Tokens abgelaufen ist. Vom Verwaltungspunkt wird dann kein weiteres Token für den Client ausgegeben, weil der Client gesperrt ist.  

     Wenn Sie verhindern möchten, dass ein gesperrter Client innerhalb dieses Zeitfensters von acht Stunden Inhalte herunterlädt, können Sie den Clouddienst beenden. Verwenden Sie dazu in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** unter **Hierarchiekonfiguration** den Knoten **Cloud**.  

##  <a name="BKMK_Privacy_ContentManagement"></a> Datenschutzinformationen zur Inhaltsverwaltung  
 Configuration Manager speichert keine Benutzerdaten in Inhaltsdateien, obwohl ein Administrator die Möglichkeit hätte, dies zu tun.  

 Berücksichtigen Sie beim Konfigurieren der Inhaltsverwaltung Ihre Datenschutzanforderungen.  
