---
title: "Informationen zur Registrierung von Geräten mit der lokalen Verwaltung mobiler Geräte – Configuration Manager | Microsoft-Dokumentation"
description: "Hier erhalten Sie Informationen zur Registrierung von Geräten mit der lokalen Verwaltung mobiler Geräte in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 8c7438c2cc0bc66654eb3e74de10553df53181d9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-users-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Informationen zur Registrierung von Geräten mit der lokalen Verwaltung mobiler Geräte in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit der lokalen Verwaltung mobiler Geräte in System Center Configuration Manager können Benutzer Geräte registrieren, wenn ihnen (über aktualisierte Clienteinstellungen) die Registrierungsberechtigung erteilt wurde und auf ihren Geräten das erforderliche Stammzertifikat für eine vertrauenswürdige Kommunikation mit den Servern installiert ist, auf denen die erforderlichen Standortsystemrollen gehostet werden. Weitere Informationen zum Einrichten der Registrierung finden Sie unter [Einrichten der Geräteregistrierung für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md).  

> [!NOTE]  
>  Configuration Manager Current Branch unterstützt die Registrierung bei der lokalen Verwaltung mobiler Geräte für Geräte, auf denen folgende Betriebssysteme ausgeführt werden:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Microsoft 10 Team \(ab Configuration Manager Version 1602\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

In den folgenden Aufgaben wird erläutert, wie Sie die Registrierung von Computern und Geräten für die lokale Verwaltung mobiler Geräte vornehmen und überprüfen:  

-   [Registrieren eines Windows 10-Computers](#bkmk_enrollDesk)  

-   [Registrieren eines Windows 10 Mobile-Geräts](#bkmk_enrollMob)  

-   [Überprüfen der Geräteregistrierung](#bkmk_verify)  

##  <a name="bkmk_enrollDesk"></a> Registrieren eines Windows 10-Computers  

1.  Wechseln Sie auf einem Computer mit Windows 10 zu **Einstellungen**.  

2.  Klicken Sie auf **Konten**und dann auf **Arbeitsplatzzugriff**.  

3.  Klicken Sie in „Arbeitsplatzzugriff“ unter **Mit Arbeitsplatz oder Schule verbinden**auf **Verbinden**, geben Sie Ihre geschäftliche E-Mail-Adresse ein, und klicken Sie auf **Weiter**.  

4.  Geben Sie den FQDN des Servers ein, auf dem die Standortsystemrolle „Registrierungsproxypunkt“ gehostet wird, und klicken Sie auf **Weiter**.  

5.  Geben Sie in „Mit einem Dienst verbinden“ das Kennwort Ihrer geschäftlichen E-Mail-Adresse ein, und klicken Sie auf **Anmelden**.  

6.  Klicken Sie bei der Frage, ob die Anmeldeinformationen gespeichert werden sollen, auf **Überspringen** . Kurze Zeit später ist Ihr Gerät verbunden.  

##  <a name="bkmk_enrollMob"></a> Registrieren eines Windows 10 Mobile-Geräts  

1.  Wechseln Sie auf einem Windows 10 Mobile-Gerät zu **Einstellungen**.  

2.  Klicken Sie auf **Konten**und dann auf **Arbeitsplatzzugriff**.  

3.  Klicken Sie auf **Verbinden**.  

4.  Geben Sie Ihre geschäftliche E-Mail-Adresse und den FQDN des Servers ein, der die Standortsystemrolle „Anmeldungsproxypunkt“ hostet. Klicken Sie auf **Verbinden**.  

5.  Geben Sie auf dem nächsten Bildschirm Ihre geschäftliche E-Mail-Adresse und das Kennwort ein, und klicken Sie dann auf **Anmelden**. Nach kurzer Zeit wird das Gerät registriert. Klicken Sie auf **Fertig**.  

##  <a name="bkmk_verify"></a> Überprüfen der Geräteregistrierung  
 Sie können überprüfen, ob Geräte in der Configuration Manager-Konsole erfolgreich registriert wurden.  

1.  Starten Sie hierzu die Configuration Manager-Konsole.  

2.  Klicken Sie auf **Bestand und Kompatibilität** > **Übersicht** > **Geräte**erforderlichen Standortsystemrollen benötigt. Das registrierte Gerät wird in der Liste angezeigt.  
