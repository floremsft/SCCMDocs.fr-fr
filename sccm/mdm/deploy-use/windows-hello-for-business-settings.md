---
title: Windows Hello for Business-Einstellungen | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Windows Hello for Business in System Center Configuration Manager integrieren.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0593c07-5dd7-4d23-a0d8-d30165f49ef7
caps.latest.revision: "17"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: a97b3d97eb302e4133b0a79a8c7e27004872c8b1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager-hybrid"></a>Windows Hello for Business-Einstellungen in System Center Configuration Manager (hybrid)

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit System Center Configuration Manager können Sie die Integration in Windows Hello for Business (früher Microsoft Passport für Windows) durchführen, eine alternative Anmeldemethode für Windows 10-Geräte. Hello for Business verwendet Active Directory oder ein Azure Active Directory-Konto, um ein Kennwort, eine Smartcard oder eine virtuelle Smartcard zu ersetzen.  

Mit Hello for Business können Sie anstelle eines Kennworts eine **Benutzeraktion** zur Anmeldung verwenden. Eine Benutzeraktion kann eine einfache PIN, eine biometrische Authentifizierung oder ein externes Gerät wie ein Fingerabdruckleser sein.  

 Configuration Manager kann auf zwei Wegen in Windows Hello for Business integriert werden:  

-   Sie können mithilfe von Configuration Manager steuern, welche Aktionen von Benutzern zum Anmelden verwendet werden können.  

-   Sie können Authentifizierungszertifikate im Windows Hello for Business-Schlüsselspeicheranbieter (Key Storage Provider; KSP) speichern. Weitere Informationen finden Sie unter [Zertifikatprofile](create-pfx-certificate-profiles.md).  

- Sie können Richtlinien von „Windows Hello for Business“ für Windows 10-Geräte bereitstellen, die in eine Domäne eingebunden sind und auf denen der Configuration Manager-Client ausgeführt wird. Diese Konfiguration wird unter [Konfigurieren von Windows Hello for Business auf einer Domäne angehörenden Windows 10-Geräten](../../protect/deploy-use/windows-hello-for-business-settings.md#configure-windows-hello-for-business-on-domain-joined-windows-10-devices) beschrieben. Bei Verwendung von Configuration Manager mit Intune (Hybrid) können Sie diese Einstellungen auf Windows 10- und Windows 10 Mobile-Geräten, aber nicht auf Geräten konfigurieren, die zu einer Domäne gehören und auf denen der Configuration Manager-Client ausgeführt wird.   

Weitere Informationen zur Konfigurierung von Windows Hello for Business-Einstellungen finden Sie unter [Windows Hello for Business-Einstellungen in System Center Configuration Manager](../../protect/deploy-use/windows-hello-for-business-settings.md).

## <a name="configure-windows-hello-for-business-settings-hybrid"></a>Konfigurieren von Windows Hello for Business-Einstellungen (hybrid)  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Clouddienste** > **Microsoft Intune-Abonnements**.  

3.  Wählen Sie aus der Liste Ihr Microsoft Intune-Abonnement aus. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Abonnement** auf **Plattformen konfigurieren** > **Windows (MDM)**.  

4.  Wählen Sie auf der Registerkarte **Windows Hello for Business** des Dialogfelds **Microsoft Intune-Abonnementeigenschaften** aus folgenden Werten aus, die Auswirkungen auf alle registrierten Windows 10- und Windows 10 Mobile-Geräte haben:  

    -   **Windows Hello for Business auf registrierten Geräten deaktivieren** oder **Windows Hello for Business auf registrierten Geräten aktivieren** : Aktiviert oder deaktiviert die Verwendung von Windows Hello for Business auf allen registrierten Windows 10 und Windows 10 Mobile-Geräten.  

    -   **Trusted Platform Module (TPM) verwenden** : Ein Trusted Platform Module-Chip (TPM) bietet eine zusätzliche Sicherheitsebene für Daten. Wählen Sie einen der folgenden Werte aus:  

        -   **Erforderlich** (Standard) – Nur Geräte mit verfügbarem TPM können Windows Hello for Business bereitstellen.  

        -   **Bevorzugt** – Geräte versuchen zunächst, ein TPM zu verwenden. Wenn diese Option nicht verfügbar ist, können sie die Softwareverschlüsselung verwenden.  

    -   **Mindestlänge für PIN anfordern** : Geben Sie die Mindestanzahl von Zeichen an, die für die Windows Hello for Business-PIN erforderlich ist. Sie müssen mindestens vier Zeichen verwenden (der Standardwert ist sechs Zeichen).  

    -   **Höchstlänge für PIN anfordern** : Geben Sie die maximale Anzahl von Zeichen an, die für die Windows Hello for Business-PIN zulässig ist. Sie können bis zu 127 Zeichen verwenden.  

    -   **Kleinbuchstaben in PIN vorschreiben** : Gibt an, ob in der Windows Hello for Business-PIN Kleinbuchstaben verwendet werden müssen. Wählen Sie aus:  

        -   **Zulässig** – Benutzer können in ihrer PIN Kleinbuchstaben verwenden.  

        -   **Erforderlich** – Benutzer müssen in ihre PIN mindestens einen Kleinbuchstaben einbeziehen.  

        -   **Nicht zulässig** – (Standardeinstellung) Benutzer dürfen in ihrer PIN keine Kleinbuchstaben verwenden.  

    -   **Großbuchstaben in PIN vorschreiben** : Gibt an, ob in der Windows Hello for Business-PIN Großbuchstaben verwendet werden müssen. Wählen Sie aus:  

        -   **Zulässig** – Benutzer können in ihrer PIN Großbuchstaben verwenden.  

        -   **Erforderlich** – Benutzer müssen in ihre PIN mindestens einen Großbuchstaben einbeziehen.  

        -   **Nicht zulässig** – (Standardeinstellung) Benutzer dürfen in ihrer PIN keine Großbuchstaben verwenden.  

    -   **Sonderzeichen anfordern** : Gibt die Verwendung von Sonderzeichen in der PIN an. Wählen Sie aus:  

        -   **Zulässig** – Benutzer können in ihrer PIN Sonderzeichen verwenden.  

        -   **Erforderlich** – Benutzer müssen in ihre PIN mindestens ein Sonderzeichen einbeziehen.  

        -   **Nicht zulässig,** (Standard) – Benutzer dürfen keine Sonderzeichen in ihrer PIN verwenden (dies trifft auch zu, wenn die Einstellung nicht konfiguriert ist).  

         Sonderzeichen umfassen: **! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**.  

    -   **PIN-Ablauf (in Tagen) anfordern**: Gibt die Anzahl der Tage an, bevor die Geräte-PIN geändert werden muss. Die Standardeinstellung ist 41 Tage.  

    -   **Wiederverwendung vorheriger PINs verhindern** : Verwenden Sie diese Einstellung, um die Wiederverwendung zuvor verwendeter PINs einzuschränken. Standardmäßig können die letzten fünf PINs nicht erneut verwendet werden.  

    -   **Biometrische Erkennung aktivieren** : Aktiviert die biometrische Authentifizierung, z.B. die Gesichtserkennung oder Fingerabdrücke, als Alternative zu einer PIN für Windows Hello for Business. Benutzer müssen für den Fall dennoch eine PIN konfigurieren, dass die biometrische Authentifizierung fehlschlägt.  

         Wenn diese Eigenschaft auf **Aktiviert**festgelegt ist, lässt Windows Hello for Business die biometrische Authentifizierung zu.  Wenn diese Eigenschaft auf **Deaktiviert**festgelegt ist, verhindert Windows Hello for Business die biometrische Authentifizierung (für alle Kontotypen).  

    -   **Erweitertes Antispoofing verwenden, falls verfügbar** : Konfiguriert, ob das erweiterte Antispoofing auf Geräten verwendet wird, die diese Option unterstützen.  

         Wenn diese Option auf **Aktiviert**festgelegt ist, fordert Windows von allen Benutzern die Verwendung von Antispoofing für Gesichtsmerkmale, sofern dies unterstützt wird.  

    -   **** : Wenn diese Option auf **Aktiviert**festgelegt ist, können die Benutzer eine Remote-Version von Hello for Business als tragbares Begleitgerät für die Authentifizierung von Desktopcomputern verwenden. Der Desktopcomputer muss mit Azure Active Directory verknüpft sein, und das Begleitgerät muss mit einer Windows Hello for Business-PIN konfiguriert werden.  

5.  Klicken Sie zum Abschluss auf **OK**.  

### <a name="see-also"></a>Weitere Informationen:  
 [Schützen der Daten und Standortinfrastruktur mit System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)

 [Verwalten der Überprüfung der Identität mit Windows Hello for Business](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport).  
