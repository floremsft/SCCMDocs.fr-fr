---
title: "Einrichten einer hybriden Windows-Geräteverwaltung mit System Center Configuration Manager und Microsoft Intune | Microsoft-Dokumentation"
description: "Richten Sie eine Windows-Geräteverwaltung mit System Center Configuration Manager und Microsoft Intune ein."
ms.custom: na
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: "9"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 47348baeac26bfa2ad5016622fe4dbcb9f572483
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Einrichten einer hybriden Windows-Geräteverwaltung mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Diese Thema erklärt IT-Administratoren, wie sie Ihre Benutzer dazu bringen können, Windows-PCs und mobile Geräte mithilfe von Configuration Manager und Microsoft Intune zu verwalten.

## <a name="enable-windows-device-management"></a>Aktivieren der Windows-Geräteverwaltung
Um die Windows-Geräteverwaltung entweder für PCs oder mobile Geräte zu aktivieren, führen Sie die folgenden Schritte aus:

1.  Bevor Sie die Registrierung einer Plattform einrichten, müssen Sie die Voraussetzungen und Schritte in [Einrichten der hybriden Verwaltung mobiler Geräte](setup-hybrid-mdm.md) erfüllen und ausführen.  
2.  Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Übersicht** > **Clouddienste** > **Microsoft Intune-Abonnements**.  
3.  Klicken Sie im Menüband auf **Plattformen konfigurieren**, und wählen Sie anschließend die Windows-Plattform aus:
    - **Windows** für Windows-PCs und -Laptops, führen Sie dann die folgenden Schritte aus:
      1. Klicken Sie auf der Registerkarte **Allgemeine** auf das Kontrollkästchen **Windows-Registrierung aktivieren**.
      2. Wenn Sie ein Zertifikat zur Codesignatur verwenden und die Unternehmensportal-App bereitstellen, navigieren Sie zum **Codesignaturzertifikat**. Gerätebenutzer können auch die Unternehmensportal-App aus dem Windows Store installieren, oder Sie können die App aus dem Windows Store für Unternehmen ohne Codesignatur bereitstellen.
      3. Sie können auch die [Windows Hello for Business-Einstellungen](windows-hello-for-business-settings.md) konfigurieren.
    - **Windows Phone** für Windows-Telefone und -Tablets, führen Sie dann die folgenden Schritte aus:
      1. Klicken Sie auf der Registerkarte **Allgemein** auf das Kontrollkästchen **Windows Phone 8.1 und Windows 10 Mobile**. Windows Phone 8.0 wird nicht mehr unterstützt.
      2. Wenn Ihr Unternehmen Unternehmens-Apps per Sideload übertragen muss, können Sie das erforderliche Token oder die erforderliche Datei hochladen. Weitere Informationen zum Querladen von Apps finden Sie unter [Erstellen von Windows-Anwendungen mit System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications).
        - **Anwendungsregistrierungstoken**
        - **PFX-Datei**
        - **Keine** Wenn Sie ein Symantec-Zertifikat verwenden, können Sie **Show an alert before Symantec certificates expire** (Warnung anzeigen, bevor Symantec-Zertifikate ablaufen) angeben.
4. Klicken Sie auf **OK** , um das Dialogfeld zu schließen.  Um die Registrierung über das Unternehmensportal zu vereinfachen, sollten Sie einen DNS-Alias für die Registrierung des Geräts erstellen. Sie können Benutzern dann mitteilen, wie sie ihre Geräte registrieren.

## <a name="choose-how-to-enroll-windows-devices"></a>Auswählen, wie Windows-Geräte registriert werden

Sobald Sie Benutzern Intune-Lizenzen zugewiesen haben, können Windows-Geräte ohne zusätzliche Schritte registriert werden, aber Sie können die Registrierung für Benutzer vereinfachen.

Zwei Faktoren bestimmen, wie Sie die Registrierung von Windows-Geräten vereinfachen können:
- **Verwenden Sie Azure Active Directory Premium?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) ist in Enterprise Mobility + Security und in anderen Lizenzierungsplänen enthalten.
- **Welche Versionen von Windows-Clients werden registriert?** <br>Windows 10-Geräte können automatisch durch Hinzufügen eines Geschäfts-oder Schulkontos registriert werden. Frühere Versionen müssen mithilfe der Unternehmensportal-App registriert werden.

||**Azure AD Premium**|**AD (Sonstiges)**|
|----------|---------------|---------------|  
|**Windows 10**|[Automatische Registrierung](#enable-windows-10-automatic-enrollment) |[Benutzerregistrierung](#enable-windows-enrollment-without-azure-ad-premium)|
|**Frühere Windows-Versionen**|[Benutzerregistrierung](#enable-windows-enrollment-without-azure-ad-premium)|[Benutzerregistrierung](#enable-windows-enrollment-without-azure-ad-premium)|

## <a name="enable-windows-10-automatic-enrollment"></a>Aktivieren der automatischen Registrierung von Windows 10

Die automatische Registrierung ermöglicht Benutzern das Registrieren von unternehmenseigenen oder persönlichen Windows 10-PCs und Windows 10-Mobilgeräten in Intune, indem ein Geschäfts-, Uni- oder Schulkonto hinzugefügt und die Verwaltung akzeptiert wird. Ganz einfach. Im Hintergrund registriert der Benutzer das Gerät und verknüpft Azure Active Directory. Nach der Registrierung wird das Gerät mit Intune verwaltet.

**Voraussetzungen**
- Azure Active Directory Premium-Abonnement ([Testabonnement](http://go.microsoft.com/fwlink/?LinkID=816845))
- Microsoft Intune-Abonnement


### <a name="configure-automatic-mdm-enrollment"></a>Konfigurieren der automatischen MDM-Registrierung

1. Melden Sie sich beim [Azure-Verwaltungsportal](https://portal.azure.com) (https://manage.windowsazure.com) an, und wählen Sie **Active Directory** aus.

  ![Screenshot des Azure-Portals](../media/auto-enroll-azure-main.png)

2. Wählen Sie **Mobilität (MDM und MAM)** aus.

  ![Screenshot des Azure-Portals](../media/auto-enroll-mdm.png)

3. Wählen Sie **Microsoft Intune** aus.

  ![Screenshot des Azure-Portals](../media/auto-enroll-intune.png)

4. Konfigurieren Sie den **MDM-Benutzerbereich**. Geben Sie an, welche Geräte welcher Benutzer von Microsoft Intune verwaltet werden sollen. Die Windows 10-Geräte dieser Benutzer werden automatisch für die Verwaltung mit Microsoft Intune registriert.

    - **Keine**
    - **Einige**
    - **Alle**

   ![Screenshot des Azure-Portals](../media/auto-enroll-scope.png)

5. Verwenden Sie die Standardwerte für die folgenden URLs:
    - **URL für MDM-Nutzungsbedingungen**
    - **URL für MDM-Ermittlung**
    - **MDM Compliance-URL**

6. Wählen Sie **Speichern** aus.


Standardmäßig ist die zweistufige Authentifizierung für den Dienst nicht aktiviert. Die zweistufige Authentifizierung wird jedoch empfohlen, wenn Sie ein Gerät registrieren. Bevor die zweistufige Authentifizierung für diesen Dienst erforderlich ist, müssen Sie einen Anbieter für die zweistufige Authentifizierung in Azure Active Directory und Ihre Benutzerkonten konfigurieren. Weitere Informationen finden Sie unter [Erste Schritte mit Azure Multi-Factor Authentication-Server](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

## <a name="enable-windows-enrollment-without-azure-ad-premium"></a>Aktivieren der Windows-Registrierung ohne Azure AD Premium
Sie können Benutzern erlauben, ihre Geräte ohne Verwendung der automatischen Registrierung von Azure AD Premium zu registrieren. Weisen Sie Benutzern Lizenzen zu, damit sie sich registrieren können, sobald sie den privat genutzten Geräten ihre Geschäftskonten hinzugefügt haben oder Ihrer Azure AD mit den firmeneigenen Geräten beigetreten sind. Das Erstellen einer DNS-Alias (CNAME-Eintragstyp) erleichtert Benutzern das Registrieren ihrer Geräte. Wenn Sie DNS CNAME-Ressourceneinträge erstellen, können Benutzer die Verbindung zu Intune herstellen und sich registrieren, ohne den Intune-Servernamen eingeben zu müssen.

### <a name="create-cnames-to-simplify-enrollment"></a>Erstellen von CNAMEs zur Vereinfachung der Registrierung
Erstellen Sie CNAME DNS-Ressourceneinträge für die Domäne des Unternehmens. Wenn die Website Ihres Unternehmens beispielsweise „contoso.com“ heißt, würden Sie einen CNAME im DNS erstellen, der „EnterpriseEnrollment.contoso.com“ an „enterpriseenrollment-s.manage.microsoft.com“ umleitet.

Obwohl das Erstellen eines CNAME-DNS-Eintrags optional ist, ist die Registrierung mit einem CNAME-Eintrag für den Benutzer leichter. Wenn kein CNAME-Eintrag für die Registrierung gefunden wurde, werden Benutzer aufgefordert, manuell den MDM-Servernamen „enrollment.manage.microsoft.com“ einzugeben.

|Typ|Hostname|Verweist auf|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 Stunde|

Wenn Sie mehr als ein UPN-Suffix haben, müssen Sie einen CNAME für jeden Domänennamen erstellen und jeden auf EnterpriseEnrollment-s.manage.microsoft.com zeigen. Wenn z.B. Benutzer bei Contoso name@contoso.com aber auch name@us.contoso.com und name@eu.constoso.com als ihre E-Mail/UPN verwenden, muss der Contoso-DNS-Administrator die folgenden CNAMEs erstellen.

|Typ|Hostname|Verweist auf|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 Stunde|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 Stunde|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 Stunde|

`EnterpriseEnrollment-s.manage.microsoft.com` – Unterstützt eine Umleitung zum Intune-Dienst mit Domänenerkennung anhand des E-Mail-Domänennamens

Die Weitergabe von Änderungen an DNS-Einträgen kann bis zu 72 Stunden dauern. Sie können die DNS-Änderung in Intune erst überprüfen, wenn der DNS-Eintrag weitergegeben wurde.

## <a name="tell-users-how-to-enroll-devices"></a>Benutzern erklären, wie sie Geräte registrieren  

 Nachdem Sie die Einrichtung abgeschlossen haben, müssen Sie Ihre Benutzer informieren, wie sie ihre Geräte registrieren sollen. Anleitungen hierzu finden Sie unter [Informieren der Benutzer über den Einsatz von Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Sie können Benutzer an [Registrieren Ihres Windows-Geräts bei Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows) weiterleiten. Diese Informationen gelten für mobile Geräte, die mit Microsoft Intune und Configuration Manager verwaltet werden.

> [!div class="button"]
[< Vorheriger Schritt](create-service-connection-point.md) [Nächster Schritt >](set-up-additional-management.md)
