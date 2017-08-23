---
title: "Benutzeraffinität für hybridverwaltete Geräte in Configuration Manager | Microsoft-Dokumentation"
description: "Konfigurieren der Benutzeraffinität für verwaltete Geräte in Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5d520a7-e9e5-40ee-91f9-f2684214beb6
caps.latest.revision: "6"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: d039792a88b9e7704f37718a88f841dd9216d1b1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="user-affinity-for-hybrid-managed-devices-in-configuration-manager"></a>Benutzeraffinität für hybridverwaltete Geräte in Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Beim Konfigurieren von Profilen für firmeneigene Geräte kann der Administrator angeben, ob die verwalteten Geräte *Benutzeraffinität* haben können, die einen bestimmten Benutzer mit dem Gerät identifiziert.  

##  <a name="BKMK_iOSCP"></a> Verwaltete Geräte mit Benutzeraffinität  
 Auf mit **user affinity** konfigurierten Geräten kann die Unternehmensportal-App installiert und ausgeführt werden, um Apps herunterzuladen und Geräte zu verwalten. Sobald Benutzer ihre Geräte erhalten haben, müssen Sie verschiedene zusätzliche Schritte ausführen, um den Setup-Assistenten abzuschließen und die Unternehmensportal-App zu installieren.  

#### <a name="how-to-enroll-ios-devices-with-user-affinity"></a>Registrieren von iOS-Geräten mit Benutzeraffinität  

1.  Wenn Benutzer ihr neues Gerät zum ersten Mal einschalten, werden sie aufgefordert, den Setup-Assistenten zu durchlaufen. Das Registrierungsprofil kann angeben, dass während des Setups eine Eingabeaufforderung für Anmeldeinformationen angezeigt werden soll. Sie müssen die Anmeldeinformationen (d.h. den eindeutigen persönlichen Namen oder UPN) verwenden, die ihrem Abonnement in Intune zugeordnet sind.  

2.  Während des Setups können Benutzer auch zur Eingabe einer Apple ID aufgefordert werden. Eine Apple ID muss angegeben werden, damit das Gerät das Unternehmensportal installieren kann. Eine Apple ID kann auch nach Abschluss des Setups im iOS-Menü **Einstellungen** angegeben werden.  

3.  Nach Abschluss des Setups muss auf dem Gerät die Unternehmensportal-App aus dem App Store installiert werden, z.B. [Unternehmensportal-App](https://itunes.apple.com/us/app/id719171358).  

4.  Der Benutzer kann sich nun mit dem eindeutigen persönlichen Namen, der beim Setup des Geräts verwendet wurde, am Unternehmensportal anmelden.  

5.  Nach der Anmeldung wird der Benutzer aufgefordert, sein Gerät zu registrieren. Der erste Schritt besteht im **Identifizieren des Geräts**. Die App zeigt eine Liste von iOS-Geräten, die bereits vom Unternehmen registriert und dem Intune-Konto des Benutzers zugewiesen wurden. Wählen Sie das entsprechende Gerät aus.  

     Wenn das Gerät nicht bereits vom Unternehmen registriert wurde, wählen Sie „Neues Gerät“, um den standardmäßigen Registrierungsvorgang fortzusetzen.  

6.  Auf dem nächsten Bildschirm muss der Benutzer die Seriennummer des neuen Geräts bestätigen. Der Benutzer kann auf den Link „Seriennummer bestätigen“ tippen, um zum Bestätigen der Seriennummer die App „Einstellungen“ zu starten. Der Benutzer muss dann die letzten 4 Zeichen der Seriennummer in die Unternehmensportal-App eingeben.  

     Dieser Schritt dient zum Überprüfen, ob das Gerät das vom Unternehmen in Intune registrierte Gerät ist. Wenn die Seriennummer des Geräts nicht übereinstimmt, wurde der falsche Gerät ausgewählt. Kehren Sie zum vorherigen Bildschirm zurück, und wählen Sie ein anderes Gerät aus.  

7.  Nachdem die Seriennummer überprüft wurde, wird die Unternehmensportal-App zur Unternehmensportal-Website umgeleitet, um die Registrierung abzuschließen. Anschließend wird der Benutzer aufgefordert, zur App zurückzukehren.  

8.  Die Registrierung ist damit abgeschlossen. Sie können nun die Funktionen des Geräts in vollem Umfang nutzen.  

##  <a name="BKMK_noUA"></a> Verwaltete Geräte ohne Benutzeraffinität  
 Auf mit **no user affinity** konfiguriert wurden, unterstützen sie auch das Unternehmensportal nicht. Die App sollte auf solchen Geräten nicht installiert werden. Das Unternehmensportal ist für Benutzer gedacht, die über Anmeldeinformationen ihres Unternehmens verfügen und Zugriff auf personalisierte Unternehmensressourcen (z. B. E-Mail) benötigen. Geräte, die **ohne Benutzeraffinität** registriert wurden, bieten keine Anmeldung für dedizierte Benutzer. Kiosk-, Verkaufsstellen- (POS-) oder gemeinsam genutzte Geräte sind typisch Anwendungsfälle für Geräte, die ohne Benutzeraffinität registriert werden. Wenn Benutzeraffinität erforderlich ist, muss vor der Registrierung des Geräts in dessen Registrierungsprofil **Benutzeraffinität** ausgewählt worden sein. Zum Ändern des Affinitätsstatus eines Geräts müssen Sie das Gerät abkoppeln und erneut registrieren.
