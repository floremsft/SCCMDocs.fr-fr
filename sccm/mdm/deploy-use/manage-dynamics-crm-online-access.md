---
title: Verwalten des Dynamics CRM Online-Zugriffs | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie den Zugriff auf Microsoft Dynamics CRM Online von iOS- und Android-Geräten über den bedingten Zugriff mit Microsoft Intune steuern."
ms.custom: na
ms.date: 03/05/2017
ms.reviewer: na
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bfc4c51-b25c-4c70-b81e-8a3b6ddf02c8
caps.latest.revision: "5"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: bd00f12ae3bc14a34d24c22c3d5277d275d51e85
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-dynamics-crm-online-access-in-system-center-configuration-manager"></a>Verwalten des Dynamics CRM Online-Zugriffs in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können den Zugriff auf Microsoft Dynamics CRM Online von iOS- und Android-Geräten über den bedingten Zugriff mit Microsoft Intune steuern.  Der bedingte Zugriff in Intune besteht aus zwei Komponenten:
* [Gerätekompatibilitätsrichtlinie](../../protect/deploy-use/device-compliance-policies.md) – Sie muss erfüllt werden, damit das Gerät als kompatibel gilt.
* [Richtlinie für den bedingten Zugriff](../../protect/deploy-use/manage-access-to-services.md) – Hiermit legen Sie fest, welche Bedingungen das Gerät erfüllen muss, um auf den Dienst zugreifen zu können.

Weitere Informationen zum bedingten Zugriff finden Sie im Artikel [Manage access to services (Verwalten des Zugriffs auf Dienste)](../../protect/deploy-use/manage-access-to-services.md).


Wenn Zielbenutzer versuchen, die Dynamics CRM-App auf ihrem Gerät zu verwenden, wird folgende Bewertung durchgeführt:

![Das Diagramm zeigt, welche Entscheidungspunkte verwendet werden, um zu bestimmen, ob ein Gerät Zugriff auf einen Dienst erhält oder ob es blockiert wird.](media/mdm-ca-dynamics-crm-flow-diagram.png)

Ein Gerät, das Zugriff auf Dynamics CRM Online benötigt, muss folgende Voraussetzungen erfüllen:
* Es muss ein **Android-** oder **iOS-**Gerät sein.
* Es muss bei Microsoft Intune **registriert** sein.
* Es muss mit allen bereitgestellten Microsoft Intune-Kompatibilitätsrichtlinien **kompatibel** sein.

Der Gerätestatus wird in Azure Active Directory gespeichert. Die Anwendung gewährt oder blockiert den Zugriff entsprechend den von Ihnen angegebenen Bedingungen.

Wenn eine Bedingung nicht erfüllt wird, erhält der Benutzer bei der Anmeldung die folgenden Meldungen:
* Wenn das Gerät nicht bei Microsoft Intune oder in Azure Active Directory registriert ist, wird eine Meldung mit Anweisungen zum Installieren der Unternehmensportal-App und zum Registrieren des Geräts angezeigt.
* Wenn das Gerät nicht kompatibel ist, wird eine Meldung angezeigt, die den Benutzer zum Microsoft Intune-Unternehmensportal oder der Unternehmensportal-App weiterleitet. Hier finden Sie Informationen zum Problem und zu dessen Lösung.

## <a name="configure-conditional-access-for-dynamics-crm-online"></a>Konfigurieren des bedingten Zugriffs für Dynamics CRM Online  
### <a name="step-1-configure-active-directory-security-groups"></a>Schritt 1: Konfigurieren von Active Directory-Sicherheitsgruppen

Bevor Sie beginnen, konfigurieren Sie Azure Active Directory-Sicherheitsgruppen für die bedingte Zugriffsichtlinie. Sie können diese Gruppen im **Office 365 Admin Center** konfigurieren. Diese Gruppen werden verwendet, um festzulegen, für welche Benutzer die Richtlinie gelten soll und welche Benutzer davon ausgenommen sind. Bei Benutzern, für die eine Richtlinie gelten soll, muss jedes von ihnen verwendete Gerät die Richtlinie erfüllen, damit sie auf Ressourcen zugreifen können.

Sie können zwei Typen von Gruppen angeben, die für die Dynamics CRM-Richtlinie verwendet werden sollen:
* **Zielgruppen**: Gruppen von Benutzern, für die die Richtlinie gelten soll
* **Ausgenommene Gruppen**: Gruppen von Benutzern, die von der Richtlinie ausgenommen sind

Benutzer, die in beiden Gruppen enthalten sind, werden von der Richtlinie ausgenommen.

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Schritt 2: Konfigurieren und Bereitstellen einer Kompatibilitätsrichtlinie
Sie müssen zunächst eine Kompatibilitätsrichtlinie für alle Geräte [erstellen und bereitstellen](../../protect/deploy-use/device-compliance-policies.md), die von der Richtlinie betroffen sind. Dies sind alle Geräte, die von den Benutzern in den Zielgruppen verwendet werden.

> [!NOTE]
> Wenn Kompatibilitätsrichtlinien für Microsoft Intune-Gruppen bereitgestellt werden, gelten Richtlinien für den bedingten Zugriff für Azure Active Directory-Sicherheitsgruppen.

> [!IMPORTANT]
> Wenn Sie keine Kompatibilitätsrichtlinie bereitgestellt haben, werden die Geräte als „kompatibel“ behandelt.

Fahren Sie mit Schritt 3 fort.
### <a name="step-3-configure-the-dynamics-crm-policy"></a>Schritt 3: Konfigurieren der Richtlinie für Dynamics CRM
Anschließend konfigurieren Sie die Richtlinie so, dass nur verwaltete und kompatible Geräte auf Dynamics CRM zugreifen dürfen. Diese Richtlinie wird in Azure Active Directory gespeichert.

1.  Wählen Sie in der Microsoft Intune-Verwaltungskonsole **Richtlinie > Bedingter Zugriff > Dynamics CRM** aus.

     ![Screenshot der Seite zur Richtlinie für den bedingten Zugriff auf Dynamics CRM Online](media/mdm-ca-dynamics-crm-policy-configuration.png)

2.  Wählen Sie **Richtlinie für bedingten Zugriff aktivieren** aus.
3.  Unter **Anwendungszugriff**können Sie optional eine bedingte Zugriffsrichtlinie auf Folgendes anwenden:
  * **iOS**
  * **Android**
4.  Wählen Sie unter **Zielgruppen** die Option **Ändern** aus, um die Active Directory-Sicherheitsgruppen auszuwählen, für die die Richtlinie gelten soll. Sie können dies für alle Benutzer oder nur für ausgewählte Benutzergruppen festlegen.
5.  Wählen Sie unter **Ausgenommene Gruppen** optional **Ändern** aus, um die Active Directory-Sicherheitsgruppen auszuwählen, die von dieser Richtlinie ausgenommen werden.
6.  Wählen Sie abschließend **Speichern** aus.

Sie haben jetzt den bedingten Zugriff für Dynamics CRM konfiguriert. Die Richtlinie für bedingten Zugriff wird sofort wirksam und muss nicht explizit bereitgestellt werden.
##  <a name="monitor-the-compliance-and-conditional-access-policies"></a>Überwachen der Richtlinien für Konformität und bedingten Zugriff

Im Arbeitsbereich **Gruppen** können Sie den Status beim bedingten Zugriff Ihrer Geräte anzeigen.

Wählen Sie eine beliebige Gruppe von Mobilgeräten und anschließend auf der Registerkarte **Geräte** einen der folgenden **Filter**aus:
* **Geräte, die nicht bei AAD registriert sind**: Diese Geräte werden für Dynamics CRM blockiert.
* **Geräte, die nicht kompatibel sind**: Diese Geräte werden für Dynamics CRM blockiert.
* **Geräte, die bei AAD registriert und kompatibel sind**: Diese Geräte können auf Dynamics CRM zugreifen.

###  <a name="see-also"></a>Weitere Informationen:
[Verwalten des Zugriffs auf E-Mail](../../protect/deploy-use/manage-email-access.md)

[Verwalten des SharePoint Online-Zugriffs](../../protect/deploy-use/manage-sharepoint-online-access.md)

[Verwalten des Zugriffs auf Skype for Business Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)
