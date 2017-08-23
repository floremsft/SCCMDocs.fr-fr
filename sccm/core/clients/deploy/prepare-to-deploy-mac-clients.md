---
title: Vorbereiten der Bereitstellung von Clientsoftware auf Macs | Microsoft-Dokumentation
description: Konfigurationsaufgaben vor dem Bereitstellen des Configuration Manager-Clients auf Mac-Computern.
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
caps.latest.revision: "12"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: b3bb72f81812705b4654e268025074402e89a7cb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Vorbereiten der Bereitstellung von Clientsoftware auf Macs

*Gilt für: System Center Configuration Manager (Current Branch)*

Führen Sie die folgenden Schritte aus, um sicherzustellen, dass Sie zum [Bereitstellen des Configuration Manager-Clients auf Mac-Computern](/sccm/core/clients/deploy/deploy-clients-to-macs) bereit sind. 

## <a name="mac-prerequisites"></a>Voraussetzungen für Mac-Computer

Das Macintosh-Clientinstallationspaket wird nicht mit den Configuration Manager-Medien geliefert. Laden Sie die **Clients für weitere Betriebssysteme** aus dem [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184) herunter.  

**Unterstützte Versionen:**  

-   **Mac OS X 10.6** (Snow Leopard) 

-   **Mac OS X 10.7** (Lion) 

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.9** (Mavericks)  

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)  

## <a name="certificate-requirements"></a>Zertifikatanforderungen
Die Clientinstallation und -verwaltung für Macintosh-Computer erfordert PKI-Zertifikate (Public Key-Infrastruktur). Durch PKI-Zertifikate wird die Kommunikation zwischen den Macintosh-Computern und dem Configuration Manager-Standort mithilfe gegenseitiger Authentifizierung und verschlüsselter Datenübertragungen gesichert. Configuration Manager kann ein Benutzerclientzertifikat mithilfe der Microsoft-Zertifikatdienste mit einer Unternehmenszertifizierungsstelle (CA) sowie den Configuration Manager-Standortsystemrollen für Registrierungsspunkt und Registrierungsproxypunkt anfordern und installieren. Sie können auch unabhängig von Configuration Manager ein Computerzertifikat anfordern und installieren, sofern das Zertifikat die Anforderungen für Configuration Manager erfüllt.   
  
Von Configuration Manager Mac-Clients wird stets eine Zertifikatsperrprüfung durchgeführt. Sie können diese Funktion nicht deaktivieren.  
  
Wenn Mac-Clients den Zertifikatsperrstatus für ein Serverzertifikat nicht bestätigen können, weil die Zertifikatsperrliste nicht gefunden werden kann, ist keine erfolgreiche Verbindung mit Configuration Manager-Standortsystemen möglich. Überprüfen Sie den Entwurf der Zertifikatsperrliste insbesondere für Mac-Clients, die sich in einer anderen Gesamtstruktur als die ausstellende Zertifizierungsstelle befinden, um sicherzustellen, dass ein Sperrlisten-Verteilungspunkt für die Verbindung mit Standortsystemservern von den Mac-Clients gefunden und eine Verbindung damit hergestellt werden kann.  

Legen Sie vor dem Installieren des Configuration Manager-Clients auf einem Macintosh-Computer fest, wie das Clientzertifikat installiert werden soll:  

-   Verwenden der Configuration Manager-Registrierung mithilfe des Tools [CMEnroll](/sccm/core/clients/deploy/deploy-clients-to-macs#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). Die automatische Zertifikatserneuerung wird bei der Anmeldung nicht unterstützt, sodass Sie Macintosh-Computer vor dem Ablaufdatum des installierten Zertifikats erneut anmelden müssen.  

-   [Verwenden einer von Configuration Manager unabhängigen Zertifikatanforderungs- und -installationsmethode](/sccm/core/clients/deploy/deploy-clients-to-macs#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager).  

Weitere Informationen zur Zertifikatanforderung für Macintosh-Clients und zu anderen PKI-Zertifikaten, die zur Unterstützung von Macintosh-Computern erforderlich sind, finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

Macintosh-Clients werden automatisch dem Configuration Manager-Standort zugewiesen, von dem aus sie verwaltet werden. Macintosh-Clients werden als reine Internetclients installiert, selbst wenn die Kommunikation auf das Intranet beschränkt ist. Diese Clientkonfiguration bedeutet, dass die Kommunikation zwischen den Clients und den Standortsystemrollen (Verwaltungspunkte und Verteilungspunkte) am zugewiesenen Standort erfolgt, wenn Sie diese Standortsystemrollen so konfigurieren, dass Clientverbindungen aus dem Internet zulässig sind. Eine Kommunikation mit Standortsystemrollen außerhalb des zugewiesenen Standorts findet auf Macintosh-Computern nicht statt.  

> [!IMPORTANT]  
>  Der Configuration Manager-Client für den Mac kann nicht zum Herstellen der Verbindung mit einem Verwaltungspunkt verwendet werden, der für die Verwendung eines [Datenbankreplikats](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) konfiguriert ist.  


## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Bereitstellen eines Webserverzertifikats für Standortsystemserver  
Wenn diese Standortsysteme nicht darüber verfügen, stellen Sie ein Webserverzertifikat für die Computer mit diesen Standortsystemrollen bereit:  

-   Verwaltungspunkt  

-   Verteilungspunkt  

-   Anmeldungspunkt  

-   Anmeldungsproxypunkt  

Im Webserverzertifikat muss der Internet-FQDN, der in den Eigenschaften des Standortsystems angegeben ist, enthalten sein. Auf den Server muss kein Zugriff über das Internet möglich sein, um Mac-Computer zu unterstützen. Wenn Sie keine internetbasierte Clientverwaltung benötigen, können Sie den Wert des Intranet-FQDN für den Internet-FQDN angeben.  

Geben Sie den Wert des Internet-FQDN für das Standortsystem im Webserverzertifikat für den Verwaltungspunkt, den Verteilungspunkt und den Registrierungsproxypunkt an. 

Eine Beispielbereitstellung, bei der dieses Webserverzertifikat erstellt und installiert wird, finden Sie unter [Bereitstellen des Webserverzertifikats für Standortsysteme, von denen IIS ausgeführt werden](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Bereitstellen eines Clientauthentifizierungszertifikat für Standortsystemserver  
 Wenn diese Standortsysteme nicht darüber verfügen, stellen Sie ein Clientauthentifizierungszertifikat für die Computer mit diesen Standortsystemrollen bereit:  

-   Verwaltungspunkt  

-   Verteilungspunkt  

 Eine Beispielbereitstellung, bei der das Clientzertifikat für Verwaltungspunkte erstellt und installiert wird, finden Sie unter [Bereitstellen des Clientzertifikats für Windows-Computer](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)  

 Eine Beispielbereitstellung, bei der das Clientzertifikat für Verteilungspunkte erstellt und installiert wird, finden Sie unter [Bereitstellen des Clientzertifikats für Verteilungspunkte](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

>[!IMPORTANT]
>  Zum Bereitstellen des Clients auf Geräten mit macOS Sierra muss der Antragstellername des Verwaltungspunktzertifikats ordnungsgemäß konfiguriert werden, z. B. mithilfe des FQDN des Verwaltungspunktservers.

## <a name="prepare-the-client-certificate-template-for-macs"></a>Vorbereiten der Clientzertifikatvorlage für Mac-Computer  

 Die Zertifikatvorlage muss über die Berechtigungen **Lesen** und **Anmelden** für das Benutzerkonto verfügen, mit dem das Zertifikat auf dem Macintosh-Computer angemeldet wird.  

 Informationen hierzu finden Sie unter [Bereitstellen des Clientzertifikats für Macintosh-Computer](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  

## <a name="configure-the-management-point-and-distribution-point"></a>Konfigurieren des Verwaltungspunkts und Verteilungspunkts  
 Konfigurieren Sie Verwaltungspunkte für die folgenden Optionen:  

-   HTTPS  

-   Clientverbindungen aus dem Internet zulassen. Dieser Konfigurationswert wird benötigt, um Macintosh-Computer zu verwalten. Dies bedeutet jedoch nicht, dass Zugriff auf Standortsystemserver über das Internet möglich sein muss.  

-   Verwendung dieses Verwaltungspunkts durch mobile Geräte und Macintosh-Computer zulassen  

 Verteilungspunkte sind zum Installieren des Clients nicht erforderlich. Sie müssen jedoch Verteilungspunkte konfigurieren, um Clientverbindungen aus dem Internet zuzulassen, wenn Sie nach der Installation des Clients auf diesen Computern Software bereitstellen möchten.  

 
### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>So konfigurieren Sie Verwaltungspunkte und Verteilungspunkte für die Unterstützung von Macintosh-Computern  

Bevor Sie das Verfahren anwenden, vergewissern Sie sich, dass der Standortsystemserver, auf dem der Verwaltungspunkt und der Verteilungspunkt ausgeführt werden, mit einem Internet-FQDN konfiguriert ist. Wenn von diesen Servern keine internetbasierte Clientverwaltung unterstützt wird, können Sie den Intranet-FQDN als Wert des Internet-FQDN angeben. 

Die Standortsystemrollen müssen sich an einem primären Standort befinden.  


1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Standortkonfiguration** > **Server und Standortsystemrollen** und anschließend den Server aus, der über die entsprechenden Standortsystemrollen verfügt.  

3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **Verwaltungspunkt**. Klicken Sie auf die **Eigenschaften** der Rolle. Konfigurieren Sie im Dialogfeld **Eigenschaften des Verwaltungspunkts** diese Optionen:  

    1.  Wählen Sie **HTTPS** aus.  

    2.  Wählen Sie **Nur Internetverbindungen zulassen** oder **Intranet- und Internet-Clientverbindungen zulassen** aus. Diese Optionen erfordern einen Internet- oder Intranet-FQDN.  

    3.  Aktivieren Sie **Verwendung dieses Verwaltungspunkts durch mobile Geräte und Macintosh-Computer zulassen**.  

4.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **Verwaltungspunkt**. Klicken Sie auf die **Eigenschaften** der Rolle. Konfigurieren Sie im Dialogfeld **Eigenschaften des Verteilungspunkts** diese Optionen:  

    -   Wählen Sie **HTTPS** aus.  

    -   Wählen Sie **Nur Internetverbindungen zulassen** oder **Intranet- und Internet-Clientverbindungen zulassen** aus. Diese Optionen erfordern einen Internet- oder Intranet-FQDN.  

    -   Klicken Sie auf **Zertifikat importieren**, suchen Sie die exportierte Clientzertifikatdatei für den Verteilungspunkt, und geben Sie das Kennwort an.  

5.  Wiederholen Sie die Schritte 2 bis 4 für alle Verwaltungspunkte und Verteilungspunkte an primären Standorten, die mit Mac-Computern verwendet werden sollen.  

## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Konfigurieren des Anmeldungsproxypunkts und Anmeldungspunkts  
 Sie müssen diese beiden Standortsystemrollen am gleichen Standort installieren. Eine Installation auf dem gleichen Standortsystemserver oder in der gleichen Active Directory-Gesamtstruktur ist jedoch nicht erforderlich.  

 Weitere Informationen zur Platzierung von und den Überlegungen für Standortsystemrollen finden Sie im Abschnitt [Standardsystemrollen](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) unter [Planen für Standortsystemserver und Standortsystemrollen für System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 Mithilfe dieser Verfahren werden die Standortsystemrollen für die Unterstützung von Macintosh-Computern konfiguriert.   

-   [Neuer Standortsystemserver](#new-site-system-server)  

-   [Bestehender Standortsystemserver](#existing-site-system-server)  

###  <a name="new-site-system-server"></a>neuer Standortsystemserver  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** >  **Standortkonfiguration** > **Server und Standortsystemrollen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Standortsystemserver erstellen** aus.  

4.  Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für das Standortsystem an.  Stellen Sie sicher, dass Sie einen Wert für den Internet-FQDN angeben. Wenn über das Internet kein Zugriff auf den Server möglich ist, verwenden Sie den Intranet-FQDN.  

5.  Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen **Anmeldungsproxypunkt** und **Anmeldungspunkt** aus.  

6.  Überprüfen Sie auf der Seite **Anmeldungsproxypunkt** die Einstellungen, und nehmen Sie ggf. Änderungen vor.  

7.  Überprüfen Sie auf der Seite **Anmeldungsproxyeinstellungen** die Einstellungen, und nehmen Sie ggf. Änderungen vor. Schließen Sie anschließend den Assistenten ab.  

### <a name="existing-site-system-server"></a>bestehender Standortsystemserver  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** >  **Standortkonfiguration** > **Server und Standortsystemrollen** und anschließend den Server aus, den Sie zum Unterstützen von Mac-Computern verwenden möchten.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Standortsystemrollen hinzufügen** aus.  

4.  Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für den Standortsystemserver an, und klicken Sie dann auf **Weiter**. Stellen Sie sicher, dass Sie einen Wert für den Internet-FQDN angeben. Wenn über das Internet kein Zugriff auf den Server möglich ist, verwenden Sie den Intranet-FQDN.   

5.  Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen **Anmeldungsproxypunkt** und **Anmeldungspunkt** aus.  

6.  Überprüfen Sie auf der Seite **Anmeldungsproxypunkt** die Einstellungen, und nehmen Sie ggf. Änderungen vor.  

7.  Überprüfen Sie auf der Seite **Anmeldungsproxyeinstellungen** die Einstellungen, und nehmen Sie ggf. Änderungen vor. Schließen Sie anschließend den Assistenten ab.  

## <a name="install-the-reporting-services-point"></a>Installieren Sie den Reporting Services-Punkt.  
 [Installieren Sie den Reporting Services-Punkt](../../../core/servers/manage/configuring-reporting.md), wenn Sie Berichte für Macintosh-Computer ausführen möchten.  

### <a name="next-steps"></a>Nächste Schritte

[Bereitstellen des Configuration Manager-Clients für Macintosh-Computer](/sccm/core/clients/deploy/deploy-clients-to-macs)  