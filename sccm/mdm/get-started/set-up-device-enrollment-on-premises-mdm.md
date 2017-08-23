---
title: "Einrichten der Geräteregistrierung | Microsoft-Dokumentation"
description: "Erteilen Sie Benutzern die Berechtigung zum Registrieren ihrer Geräte für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
caps.latest.revision: "10"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 16d4106d486d821b7ce92a1de65ebb04469d18de
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-device-enrollment-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Einrichten der Geräteregistrierung für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Damit Benutzer ihre Geräte für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager registrieren können, müssen Sie ihnen die entsprechende Berechtigung erteilen. Führen Sie die folgenden Schritte aus, um Benutzern die Berechtigung zum Registrieren von Geräten zu erteilen:

-   [Erstellen Sie ein Registrierungsprofil, mit dem Benutzer moderne Geräte registrieren können.](#bkmk_createProf)  

-   [Einrichten zusätzlicher Clienteinstellungen für registrierte Geräte](#bkmk_addClient)  

-   [Aktivieren von Benutzern für den Erhalt des Anmeldungsprofils für moderne Geräte](#bkmk_enableUsers)  

-   [Speichern des Stammzertifikats auf zu registrierenden Geräten](#bkmk_storeCert)  

##  <a name="bkmk_createProf"></a> Erstellen Sie ein Registrierungsprofil, mit dem Benutzer moderne Geräte registrieren können.  
 Damit die Einstellungen, die den Benutzern die Registrierung moderner Geräte ermöglichen, per Pushübertragung bereitgestellt werden, können Sie ein neues Registrierungsprofil zu den Standardclienteinstellungen hinzufügen, das auf alle erkannten Benutzer am Configuration Manager-Standort angewendet wird.  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Übersicht** > **Clienteinstellungen**, öffnen Sie **Clientstandardeinstellungen**, und wählen Sie **Registrierung** aus.  

2.  Geben Sie unter den Geräteeinstellungen das Abrufintervall für moderne Geräte an.  

3.  Wählen Sie unter den Benutzereinstellungen für die Option **Benutzern die Registrierung moderner Geräte gestatten** die Einstellung **Ja**aus.  

4.  Klicken Sie neben **Registrierungsprofil für modernes Gerät** auf **Profil festlegen...** und auf **Erstellen...**  

5.  Geben Sie in „Anmeldungsprofil erstellen“ einen Namen für das Anmeldungsprofil ein, und wählen Sie den Verwaltungsstandortcode aus, den Benutzer mit dem Anmeldungsprofil verwenden sollen. Klicken Sie mehrmals auf **OK** , um die Seite „Standardeinstellungen“ zu verlassen.  

> [!NOTE]  
>  Wenn Sie das Anmeldungsprofil für eine Teilmenge der ermittelten Benutzer bereitstellen möchten, können Sie eine Benutzersammlung verwenden und benutzerdefinierte Clienteinstellungen erstellen, die für diese Sammlung bereitgestellt werden. Informationen zum Erstellen benutzerdefinierter Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md)  

##  <a name="bkmk_addClient"></a> Einrichten zusätzlicher Clienteinstellungen für registrierte Geräte  
 Neben dem Einrichten des Registrierungsprofils für moderne Geräte können Sie zusätzliche Clienteinstellungen für die Konfiguration von Geräten einrichten, wenn sie registriert sind.  Informationen zum Einrichten von Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

 Nicht alle Clienteinstellungen sind für die lokale Verwaltung mobiler Geräte verfügbar. Von Current Branch von Configuration Manager werden die folgenden Clienteinstellungen für die lokale Verwaltung mobiler Geräte unterstützt:  

-   Registrierung: Diese Einstellungen geben das Registrierungsprofil für verwaltete Geräte an. Weitere Informationen zum Einrichten eines Registrierungsprofils finden Sie unter [Einrichten der Geräteregistrierung für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager](#bkmk_createProf).  

-   Clientrichtlinie: Diese Einstellungen geben die Häufigkeit für das Herunterladen der Clientrichtlinie auf das Gerät an. Einstellungen für die Zielgruppenadressierung von Benutzern können Sie auch mit dem Richtlinienabruf aktivieren. Weitere Informationen zu den Clientrichtlinieneinstellungen finden Sie im Abschnitt „Clientrichtlinie“ in dem Artikel [Informationen zu Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

-   Softwarebereitstellung: Durch diese Einstellung wird das Intervall für die Bewertung von Clientgeräten für Softwarebereitstellungen festgelegt. Weitere Informationen zu den Einstellungen für die Softwarebereitstellung finden Sie im Abschnitt „Softwarebereitstellung“ in dem Artikel [Informationen zu Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

    > [!NOTE]  
    >  Bei der lokalen Verwaltung mobiler Geräte können die Einstellungen für die Softwarebereitstellung nur als Standardclienteinstellungen verwendet werden. Die Einstellungen für die Softwarebereitstellung können in Current Branch von Configuration Manager nicht mit benutzerdefinierten Clienteinstellungen verwendet werden.  

##  <a name="bkmk_enableUsers"></a> Aktivieren von Benutzern für den Erhalt des Anmeldungsprofils für moderne Geräte  
 Damit Benutzer die geänderten Clienteinstellungen mit dem Registrierungsprofil für die lokale Verwaltung mobiler Geräte erhalten, müssen diese von der Active Directory-Ermittlungsmethode ermittelt werden. Führen Sie die Ermittlung für Active Directory-Benutzer aus, um sicherzustellen, dass alle erforderlichen Personen das Anmeldungsprofil erhalten. Anweisungen zum Ermitteln der Benutzer finden Sie unter [Run discovery for System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

##  <a name="bkmk_storeCert"></a> Speichern des Stammzertifikats auf zu registrierenden Geräten  
 Benutzer mit Geräten, die Domänen angehören, verfügen voraussichtlich bereits über das erforderliche Stammzertifikat für die vertrauenswürdige Kommunikation mit den Servern, die die Standortsystemrollen hosten, da der Stamm im Rahmen der Domänenzuordnung mit Active Directory ausgestellt wurde. Für nicht der Domäne angehörende Computer und mobile Geräte muss das Stammzertifikat manuell auf dem Gerät installiert sein, damit die Registrierung erfolgen kann. Diese Geräte verfügen nicht automatisch über das erforderliche Stammzertifikat.  

 Die exportierte Zertifikatsdatei muss für die manuelle Installation auf dem Gerät bereitgestellt werden. Dies kann per E-Mail, OneDrive, SD-Karte, USB-Thumbdrive oder über eine andere geeignete Methode erfolgen.  

 Bei dem Stammzertifikat, das Sie auf den Geräten verwenden sollten, handelt es sich um das in [Exportieren des Zertifikats mit dem Webserverzertifikat entsprechendem Stamm](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert) exportierte Zertifikat.  

1.  Suchen Sie die Stammzertifikatdatei auf dem zu registrierenden Gerät, und doppelklicken Sie dann auf die Datei.  

2.  Klicken Sie im Zertifikatfenster auf **Zertifikat installieren...**.  

3.  Wählen Sie im Zertifikatimport-Assistenten die Option **Lokaler Computer**aus, und klicken Sie auf **Weiter**.  

4.  Klicken Sie im Fenster „Benutzerkontensteuerung“ auf **Ja**.  

5.  Wählen Sie die Option **Alle Zertifikate in folgendem Speicher speichern**aus, und klicken Sie auf **Durchsuchen**.  

6.  Klicken Sie nacheinander auf **Vertrauenswürdige Stammzertifizierungsstellen**, **OK**und dann auf **Weiter**.  

7.  Klicken Sie auf **Fertig stellen**.  
