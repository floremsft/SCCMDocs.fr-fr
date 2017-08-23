---
title: Verwalten des Zugriffs auf Skype for Business Online | Microsoft-Dokumentation
description: "Enthält Informationen zum Verwenden der Richtlinie für bedingten Zugriff, um Skype for Business Online zu verwalten."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71c44250-626e-482c-8794-434c6aeb2fb1
caps.latest.revision: "6"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: cacb22a85e74a7d9cae75ad907d0206487cd4dc7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-skype-for-business-online-access"></a>Verwalten des Zugriffs auf Skype for Business Online

*Gilt für: System Center Configuration Manager (Current Branch)*


Verwenden Sie die Richtlinie für bedingten Zugriff für  **Skype for Business Online** zum Verwalten des Zugriffs auf Skype for Business Online anhand der Bedingungen, die Sie angeben.  


 Wenn ein Zielbenutzer versucht, Skype for Business Online auf seinem Gerät zu verwenden, wird folgende Bewertung durchgeführt:![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>Voraussetzungen  

-   Aktivieren Sie die moderne Authentifizierung für Skype for Business Online. Füllen Sie dieses [Anmeldeformular](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) aus, um sich für die moderne Authentifizierung zu registrieren.  

-   Alle Ihre Endbenutzer müssen Skype for Business Online verwenden. Wenn Sie eine Bereitstellung sowohl mit Skype for Business Online als auch Skype for Business haben, wird die Richtlinie für bedingten Zugriff nicht für Endbenutzer angewendet.  

-   Das Gerät, das Zugriff auf Skype for Business Online benötigt, muss folgende Voraussetzungen erfüllen:  

    -   Es muss ein Android- oder iOS-Gerät sein.  

    -   Es muss bei Intune registriert sein.  

    -   Es muss mit allen bereitgestellten Konformitätsrichtlinien kompatibel sein.  

 Der Gerätestatus wird in Azure Active Directory gespeichert. Die Anwendung gewährt oder blockiert den Zugriff entsprechend den von Ihnen angegebenen Bedingungen.  
Wenn eine Bedingung nicht erfüllt wird, erhält der Benutzer bei der Anmeldung die folgenden Meldungen:  

-   Wenn das Gerät nicht bei Intune oder in Azure Active Directory registriert ist, wird eine Meldung mit Anweisungen zum Installieren der Unternehmensportal-App und zum Registrieren des Geräts angezeigt.  

-   Wenn das Gerät nicht kompatibel ist, wird eine Meldung angezeigt, die den Benutzer zum Intune-Unternehmensportal oder der Unternehmensportal-App weiterleitet. Hier finden sie Informationen zum Problem und zu dessen Lösung.  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>Konfigurieren des bedingten Zugriffs für Skype for Business Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Schritt 1: Konfigurieren von Active Directory-Sicherheitsgruppen  
 Bevor Sie beginnen, konfigurieren Sie Azure Active Directory-Sicherheitsgruppen für die bedingte Zugriffsichtlinie. Sie können diese Gruppen im Office 365 Admin Center konfigurieren. Die Gruppen beinhalten die Benutzer, für die die Richtlinie gelten soll oder die davon ausgeschlossen sind. Bei Benutzern, für die eine Richtlinie gelten soll, muss jedes von ihnen verwendete Gerät die Richtlinie erfüllen, damit sie auf Ressourcen zugreifen können.  

 Sie können zwei Typen von Gruppen angeben, die für die Skype for Business-Richtlinie verwendet werden sollen:  

-   Zielgruppen – Gruppen von Benutzern, für die die Richtlinie gelten soll  

-   Ausgenommene Gruppen – Gruppen von Benutzern, die von der Richtlinie ausgenommen sind (optional)  
    Benutzer, die in beiden Gruppen enthalten sind, werden von der Richtlinie ausgenommen.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Schritt 2: Konfigurieren und Bereitstellen einer Kompatibilitätsrichtlinie  
 Wichtig ist, dass Sie für alle Geräte, für die die Skype for Business Online-Richtlinie gelten soll, eine Kompatibilitätsrichtlinie erstellen und bereitstellen.  

 Ausführliche Informationen zum Konfigurieren der Kompatibilitätsrichtlinie finden Sie unter [Verwalten von Kompatibilitätsrichtlinien für Geräte in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!NOTE]  
>  Wenn Sie keine Kompatibilitätsrichtlinie bereitgestellt haben und dann die Skype for Business Online-Richtlinie aktivieren, wird allen Zielgeräten der Zugriff erlaubt, sofern sie bei Intune registriert sind.  

 Fahren Sie mit Schritt 3 fort.  

### <a name="step-3-configure-the-skype-for-business-online-policy"></a>Schritt 3: Konfigurieren der Skype for Business Online-Richtlinie  
 Anschließend konfigurieren Sie die Richtlinie so, dass nur verwaltete und kompatible Geräte auf Skype for Business Online zugreifen dürfen. Diese Richtlinie wird in Azure Active Directory gespeichert.  

1.  Klicken Sie in der [Microsoft Intune-Verwaltungskonsole](https://manage.microsoft.com)auf **Richtlinie** > **Bedingter Zugriff** > **Skype for Business Online Richtlinie**.  

     ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2.  Wählen Sie **Richtlinie für bedingten Zugriff aktivieren** aus.  

3.  Unter **Anwendungszugriff**können Sie optional eine bedingte Zugriffsrichtlinie auf Folgendes anwenden:  

    -   iOS  

    -   Android  

4.  Klicken Sie unter **Zielgruppen**auf **Ändern** , um die Active Directory-Sicherheitsgruppen auszuwählen, für die die Richtlinie gelten soll. Sie können dies für alle Benutzer oder nur für ausgewählte Benutzergruppen festlegen.  

5.  Klicken Sie unter **Ausgenommene Gruppen**optional auf **Ändern** , um die Active Directory-Sicherheitsgruppen auszuwählen, die von dieser Richtlinie ausgenommen werden.  

6.  Klicken Sie abschließend auf **Speichern**.  

 Sie haben jetzt den bedingten Zugriff für Skype for Business Online konfiguriert. Die Richtlinie für bedingten Zugriff wird sofort wirksam und muss nicht explizit bereitgestellt werden.  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>Überwachen der Richtlinien für Konformität und bedingten Zugriff  
 Im Arbeitsbereich „Gruppen“ können Sie den Status beim bedingten Zugriff Ihrer Geräte anzeigen.  

 Wählen Sie eine beliebige Gruppe von Mobilgeräten und anschließend auf der Registerkarte **Geräte** einen der folgenden **Filter**aus:  

-   **Geräte, die nicht bei AAD registriert sind** – Diese Geräte werden für Skype for Business Online blockiert.  

-   **Geräte, die nicht kompatibel sind** – Diese Geräte werden für Skype for Business Online blockiert.  

-   **Geräte, die bei AAD registriert und kompatibel sind** – Diese Geräte können auf Skype for Business Online zugreifen.  

### <a name="see-also"></a>Weitere Informationen:  

 [Manage device compliance policies in System Center Configuration Manager (Verwalten von Kompatibilitätsrichtlinien für Geräte in System Center Configuration Manager)](../../protect/deploy-use/device-compliance-policies.md)
