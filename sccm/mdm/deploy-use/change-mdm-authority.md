---
title: "Umstellen der MDM-Autorität | Microsoft-Dokumentation"
description: "Erfahren Sie, wie die MDM-Autorität von Configuration Manager (hybrid) auf Intune standalone oder umgekehrt umgestellt wird."
keywords: 
author: dougeby
manager: angrobe
ms.date: 06/02/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: 74b9dbb1ed0172d99956e726fca3aec2b658ce77
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="change-your-mdm-authority"></a>Umstellen der MDM-Autorität
Ab Configuration Manager, Version 1610, und Microsoft Intune, Version 1705, können Sie Ihre MDM-Autorität ohne Unterstützung durch den Microsoft-Support und ohne Aufheben der Registrierung und erneutes Registrieren Ihrer vorhandenen verwalteten Geräte umstellen.

## <a name="change-the-mdm-authority-to-intune-standalone"></a>Umstellen der MDM-Autorität auf Intune standalone
Verwenden Sie diesen Abschnitt, um einen vorhandenen Microsoft Intune-Mandanten, der über die Configuration Manager-Konsole (hybrid) konfiguriert wurde, ohne Aufheben der Registrierung und erneutes Registrieren vorhandener verwalteter Geräte auf Intune standalone umzustellen.

### <a name="key-considerations"></a>Wichtige Überlegungen
Nachdem Sie auf die neue MDM-Autorität umgestellt haben, gibt es wahrscheinlich eine Übergangszeit (bis zu 8 Stunden), bevor das Gerät eingecheckt und mit dem Dienst synchronisiert wird. Sie müssen Einstellungen in der neuen MDM-Autorität (Intune standalone) konfigurieren, um sicherzustellen, dass registrierte Geräte nach der Umstellung weiterhin verwaltet und geschützt werden. Beachten Sie dabei Folgendes:
- Geräte müssen nach der Umstellung eine Verbindung mit dem Dienst herstellen, damit die Einstellungen der neuen MDM-Autorität (Intune standalone) die vorhandenen Einstellungen auf dem Gerät ersetzen.
- Nachdem Sie die MDM-Autorität umgestellt haben, verbleiben einige der grundlegenden Einstellungen (z.B. Profile) aus der vorherigen MDM-Autorität (hybrid) für bis zu 7 Tage auf dem Gerät. Es wird empfohlen, dass Sie Apps und Einstellungen (Richtlinien, Profile, Apps usw.) so bald wie möglich in der neuer MDM-Autorität konfigurieren und die Einstellungen den Benutzergruppen bereitstellen, die Benutzer mit gegenwärtig registrieren Geräten enthalten. Sobald ein Gerät nach der Umstellung der MDM-Autorität eine Verbindung mit dem Dienst herstellt, werden die neuen Einstellungen der neuen MDM-Autorität übertragen, und Lücken bei Verwaltung und Schutz werden verhindert. Alle neuen, gezielten Richtlinien überschreiben vorhandene Richtlinien auf dem Gerät.
- Nachdem Sie auf die neue MDM-Autorität umgestellt haben, kann es bis zu einer Woche dauern, bis die Kompatibilitätsinformationen in der Microsoft Intune-Verwaltungskonsole richtig gemeldet werden. Allerdings sind die Kompatibilitätszustände in Azure Active Directory und auf dem Gerät richtig, sodass das Gerät weiterhin geschützt ist.

### <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Vorbereiten der Umstellung der MDM-Autorität auf Intune standalone
Überprüfen Sie die folgenden Informationen, um die Umstellung der MDM-Autorität vorzubereiten:
- Sie benötigen Configuration Manager, Version 1610 oder höher, damit die Option zum Umstellen der MDM-Autorität verfügbar ist.
- Es kann bis zu 8 Stunden dauern, bis ein Gerät eine Verbindung mit dem Dienst herstellt, nachdem Sie auf die neue MDM-Autorität umgestellt haben.
- Stellen Sie sicher, dass alle Benutzer, die momentan hybrid verwaltet werden, über eine Intune-/EMS-Lizenz verfügen, die ihnen speziell zugewiesen ist, bevor Sie die MDM-Autorität umstellen. Dadurch wird sichergestellt, dass die Benutzer und ihre Geräte nach der Umstellung der MDM-Autorität von Intune standalone verwaltet werden. Weitere Informationen finden Sie unter [Zuweisen von Intune-Lizenzen zu Benutzerkonten](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Stellen Sie sicher, dass dem Konto des Administratorbenutzers eine Intune-/EMS-Lizenz zugewiesen wurde, und vergewissern Sie sich, dass sich das Konto des Administratorbenutzers in Intune anmelden kann, bevor Sie die MDM-Autorität umstellen. Für die MDM-Autorität sollte in der Microsoft Intune-Verwaltungskonsole vor der Umstellung der MDM-Autorität **Auf Configuration Manager setzen** (hybrider Mandant) angezeigt werden.
- Entfernen Sie in der Configuration Manager-Konsole alle Geräteregistrierungs-Manager-Rollen. Wechseln Sie zu **Verwaltung** > **Clouddienste** > **Microsoft Intune-Abonnements**, wählen Sie das Microsoft Intune-Abonnement aus, klicken Sie auf **Eigenschaften**, klicken Sie auf die Registerkarte **Geräteregistrierungs-Manager**, und entfernen Sie alle Geräteregistrierungs-Manager-Rollen.
- Entfernen Sie in der Configuration Manager-Konsole vorhandene Gerätekategorien. Wechseln Sie zu **Bestand und Kompatibilität** > **Übersicht** > **Gerätesammlungen**, wählen Sie **Gerätekategorien verwalten** aus, und entfernen Sie vorhandene Gerätekategorien.
- Während der Umstellung der MDM-Autorität sollte es keine wahrnehmbaren Auswirkungen auf die Endbenutzer geben. Möglicherweise sollten Sie jedoch die Benutzer über die Umstellung informieren, um sicherzustellen, dass ihre Geräte eingeschaltet sind und dass sie kurz nach der Umstellung eine Verbindung mit dem Dienst herstellen. Dadurch wird sichergestellt, dass so viele Geräte wie möglich eine Verbindung herstellen und so bald wie möglich über die neue Autorität beim Dienst registriert werden.
- Wenn Sie vor der Umstellung der MDM-Autorität Configuration Manager (hybrider Mandant) zum Verwalten von iOS-Geräten verwenden, müssen Sie sicherstellen, dass das gleiche Apple Push Notification Service-Zertifikat (APNs), das zuvor in Configuration Manager verwendet wurde, erneuert und wieder zum Einrichten des Mandanten in Intune standalone verwendet wird.

    > [!IMPORTANT]  
    > Wenn ein anderes APNs-Zertifikat für Intune standalone verwendet wird, wird die Registrierung ALLER zuvor registrierten iOS-Geräte aufgehoben, und Sie müssen sie erneut registrieren. Stellen Sie vor der Umstellung der MDM-Autorität sicher, dass Sie genau wissen, welches APNs-Zertifikat zum Verwalten von iOS-Geräten in Configuration Manager verwendet wurde. Suchen Sie nach dem Zertifikat im Apple Push Certificates-Portal (https://identity.apple.com), und stellen Sie sicher, dass der Benutzer, mit dessen Apple-ID das ursprüngliche APNs-Zertifikat erstellt wurde, identifiziert wird und verfügbar ist, um das gleiche APNs-Zertifikat als Teil der Umstellung auf die neue MDM-Autorität zu erneuern.  

### <a name="change-the-mdm-authority-to-intune-standalone"></a>Umstellen der MDM-Autorität auf Intune standalone
Die Umstellung der MDM-Autorität auf Intune standalone umfasst die folgenden allgemeinen Schritte:  
- Verwenden Sie in der Configuration Manager-Konsole die Option **MDM-Autorität auf Microsoft Intune umstellen**, um das vorhandene Microsoft Intune-Abonnement zu entfernen.
- Legen Sie in der Microsoft Intune-Verwaltungskonsole die neue MDM-Autorität auf **Intune** fest.
- Konfigurieren Sie das Apple APNs-Zertifikat mit dem gleichen APNs-Zertifikat, das Sie erneuert haben.
- Konfigurieren Sie in der Microsoft Intune-Verwaltungskonsole die neuen Einstellungen und Apps der neuen MDM-Autorität (Intune), und stellen Sie sie bereit.
- Wenn Geräte das nächste Mal eine Verbindung mit dem Dienst herstellen, werden sie synchronisiert und erhalten die neuen Einstellungen von der neuen MDM-Autorität.

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>So stellen Sie die MDM-Autorität auf Intune standalone um
1.  Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** &gt; **Übersicht** &gt; **Clouddienste** &gt; **Microsoft Intune-Abonnement**, und löschen Sie Ihr vorhandenes Intune-Abonnement.
2.  Wählen Sie **MDM-Autorität auf Microsoft Intune umstellen** aus, und klicken Sie dann auf **Weiter**.

    ![Herunterladen der APNs-Zertifikatanforderung](/sccm/mdm/deploy-use/media/mdm-change-delete-subscription.png)
3.  Melden Sie sich an dem Intune-Mandanten an, den Sie ursprünglich beim Festlegen der MDM-Autorität in Configuration Manager verwendet haben.
4.  Klicken Sie auf **Weiter** , und schließen Sie den Assistenten ab.
5.  Die MDM-Autorität wurde jetzt zurückgesetzt. Das Intune-Abonnement sollte nicht mehr im Knoten „Microsoft Intune-Abonnements“ der Configuration Manager-Konsole angezeigt werden.
6.  Melden Sie sich an der [Microsoft Intune-Verwaltungskonsole](http://manage.microsoft.com) an. Verwenden Sie dazu den gleichen Intune-Mandanten wie zuvor.
7.  Vergewissern Sie sich, dass die MDM-Autorität zurückgesetzt wurde, und legen Sie dann die MDM-Autorität auf **Microsoft Intune** fest. Wenn Sie die MDM-Autorität geändert haben, sollte dies in der Konsole angezeigt werden. Weitere Informationen finden Sie unter [Festlegen der MDM-Autorität](https://docs.microsoft.com/en-us/intune/deploy-use/prerequisites-for-enrollment#step-2-set-mdm-authority).
<!-- [Azure portal](https://docs.microsoft.com/en-us/intune-azure/enroll-devices/set-mdm-authority) -->


### <a name="configure-the-apns-certificate"></a>Konfigurieren des APNs-Zertifikats
Wenn Sie iOS-Geräte verwenden, müssen Sie das APNs-Zertifikat in Intune konfigurieren.

#### <a name="to-configure-the-apns-certificate"></a>So konfigurieren Sie das APNs-Zertifikat
1.  Laden Sie die APNs-Zertifikatanforderung herunter.
    <!--The process is different depending on how you connect to Intune:
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment** &gt; **Apple MDM Push Certificate**, and then select **Download your CSR** to download and save the .csr file locally.   
    <br/>
    **Microsoft Intune administration console**   -->
    Wechseln Sie in der [Microsoft Intune-Verwaltungskonsole](http://manage.microsoft.com) zu **Verwaltung** &gt; **Verwaltung mobiler Geräte** &gt;  **iOS und Mac OS X** &gt; **APNs-Zertifikat hochladen**, und wählen Sie dann **APNS-Zertifikatanforderung herunterladen** aus. Speichern Sie die Zertifikatsignierungsanforderung (CSR-Datei) lokal.
    > [!IMPORTANT]    
    > Sie müssen eine neue Zertifikatsignieranforderung herunterladen. Verwenden Sie keine vorhandene Datei, da dies zu einem Fehler führt.

    ![Herunterladen der APNs-Zertifikatanforderung](/sccm/mdm/deploy-use/media/mdm-change-download-apns-certificate.png)

2.  Wechseln Sie zum [Apple Push Certificates-Portal](http://go.microsoft.com/fwlink/?LinkId=269844), und melden Sie sich mit der **gleichen** Apple-ID an, die verwendet wurde, um zuvor das APNs-Zertifikat zu erstellen und zu erneuern, das Sie in Configuration Manager (hybrid) verwendet haben.

    ![Anmeldeseite des Apple Push Certificates-Portals](/sccm/mdm/deploy-use/media/mdm-change-apns-portal.png)

3.  Wählen Sie das APNs-Zertifikat aus, das Sie in Configuration Manager (hybrid) verwendet haben, und klicken Sie dann auf **Erneuern**.   

    ![Dialogfeld zur APNs-Erneuerung](/sccm/mdm/deploy-use/media/mdm-change-renew-apns.png)

4.  Wählen Sie die APNs-Zertifikatsignieranforderung (CSR-Datei) aus, die Sie lokal heruntergeladen haben, und klicken Sie dann auf **Hochladen**.

    ![Anmeldeseite des Apple Push Certificates-Portals](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)  
5.  Wählen Sie das gleiche APNs-Zertifikat aus, und klicken Sie dann auf **Herunterladen**. Laden Sie das APNs-Zertifikat (PEM) herunter, und speichern Sie die Datei lokal.  

    ![Anmeldeseite des Apple Push Certificates-Portals](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-download.png)

6.  Laden Sie das erneuerte APNs-Zertifikat mit der gleichen Apple-ID wie zuvor auf den Intune-Mandanten hoch.
<!--The process is different depending on how to connect to Intune:  
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment**  &gt; **Apple MDM Push Certificate**, enter your Apple ID in step 3, select the certificate (.pem) file in step 4, and then click **Upload**.     
    <br/>
    **Microsoft Intune administration console**    -->
    In the [Microsoft Intune administration console](http://manage.microsoft.com), go to **Administration** &gt; **Mobile Device Management** &gt; **iOS and Mac OS X** &gt; **Upload an APNs Certificate**, and then choose **Upload the APNs certificate**. Go to the certificate (.pem) file, choose **Open**, and then enter your **Apple ID**.   

    ![Upload the APNs certificate](/sccm/mdm/deploy-use/media/mdm-change-upload-apns-certificate.png)

### <a name="next-steps"></a>Nächste Schritte
Sobald die Umstellung der MDM-Autorität abgeschlossen ist, überprüfen Sie die folgenden Schritte:
- Wenn der Intune-Dienst erkennt, dass die MDM-Autorität eines Mandanten umgestellt wurde, sendet er eine Benachrichtigung an alle registrierten Geräte, damit sie beim Dienst eingecheckt und synchronisiert werden (außerhalb der regelmäßigen geplanten Eincheckvorgänge). Nach der Umstellung der MDM-Autorität für den Mandanten von hybrid auf Intune standalone stellen daher alle Geräte, die eingeschaltet und online sind, eine Verbindung mit dem Dienst her, erhalten die neue MDM-Autorität und werden zukünftig von Intune standalone verwaltet. Es gibt keine Unterbrechung bei Verwaltung und Schutz dieser Geräte.
- Geräte, die während (oder kurz nach) der Umstellung der MDM-Autorität ausgeschaltet oder offline sind, stellen unter der neuen MDM-Autorität eine Verbindung mit dem Dienst her und werden synchronisiert, sobald sie eingeschaltet werden und online sind.  

  Bei iOS-Geräten ist zusätzliche Zeit zum Erneuern und Einrichten des APNs-Zertifikats erforderlich. Daher erhalten iOS-Geräte die ursprüngliche Anforderung zum Einchecken nicht. Selbst wenn iOS-Geräte während (oder kurz nach) der Umstellung der MDM-Autorität eingeschaltet und online sind, gibt es eine Verzögerung von bis zu 8 Stunden (je nach Zeitpunkt des nächsten geplanten regulären Eincheckvorgangs), bevor iOS-Geräte unter der neuen MDM-Autorität beim Dienst registriert werden.    

  > [!IMPORTANT]
  > In der Zeit zwischen der Umstellung der MDM-Autorität und dem Hochladen des erneuerten APNs-Zertifikats in die neue Autorität schlagen neue Registrierungen und Eincheckvorgänge für iOS-Geräte fehl. Aus diesem Grund ist es wichtig, dass Sie das APNs-Zertifikat so bald wie möglich nach der Umstellung der MDM-Autorität überprüfen und in die neue Autorität hochladen.   

- Benutzer können schnell auf die neue MDM-Autorität umstellen, indem sie manuell einen Eincheckvorgang des Geräts beim Dienst starten. Benutzer können dies problemlos mithilfe der Unternehmensportal-App und dem Initiieren einer Überprüfung der Gerätekonformität erreichen.
- Um zu überprüfen, ob nach der Umstellung der MDM-Autorität und dem Einchecken und Synchronisieren der Geräte beim Dienst alles ordnungsgemäß funktioniert, suchen Sie in der [Microsoft Intune-Verwaltungskonsole](http://manage.microsoft.com) nach den Geräten. Die Geräte, die zuvor von Configuration Manager (hybrid) verwaltet wurden, werden jetzt als verwaltete Geräte angezeigt.    
- Es gibt eine Übergangszeit, bis ein Gerät beim Dienst eingecheckt wird, wenn das Gerät während der Umstellung der MDM-Autorität offline war. Um sicherzustellen, dass das Gerät während dieser Übergangszeit geschützt und funktionsfähig bleibt, verbleibt Folgendes für bis zu 7 Tage (oder bis das Gerät eine Verbindung mit der neuen MDM-Autorität herstellt und die neuen Einstellungen empfängt, die die vorhandenen überschreiben) auf dem Gerät:
    - E-Mail-Profil
    - VPN-Profil
    - Zertifikatprofil
    - WLAN-Profil
    - Konfigurationsprofile
- Stellen Sie sicher, dass die neuen Einstellungen, mit denen die vorhandenen Einstellungen überschrieben werden sollen, den gleichen Namen aufweisen wie die vorherigen, damit die alten Einstellungen tatsächlich überschrieben werden. Andernfalls weisen die Geräte möglicherweise redundante Profile und Richtlinien auf.
    > [!TIP]   
    > Es empfiehlt sich, alle Verwaltungseinstellungen und Konfigurationen sowie Bereitstellungen kurz nach Abschluss der Umstellung der MDM-Autorität zu erstellen. Dadurch wird sichergestellt, dass Geräte in der Übergangszeit geschützt und aktiv verwaltet werden.   
-  Führen Sie nach der Umstellung der MDM-Autorität die folgenden Schritte aus, um zu überprüfen, ob neue Geräte erfolgreich bei der neuen Autorität registriert werden:   
    - Registrieren eines neuen Geräts
    - Stellen Sie sicher, dass das neu registrierte Gerät in der Intune-Verwaltungskonsole angezeigt wird.
    - Führen Sie über die Verwaltungskonsole auf dem Gerät eine Aktion aus, z.B. Remotesperre. Wenn sie erfolgreich ist, wird das Gerät durch die neue MDM-Autorität verwaltet.
- Wenn Sie Probleme mit bestimmten Geräten haben, können Sie die Registrierung der Geräte aufheben und sie erneut registrieren, damit sie so schnell wie möglich mit der neuen Autorität verbunden und von ihr verwaltet werden.

<!-- After the change in MDM authority and devices check-in with the service, note the following:      - The updated compliance status of devices will only display in the Azure portal immediately.
- There will be a delay for compliance status of devices to display in the Intune administrative console.-->


## <a name="change-the-mdm-authority-to-configuration-manager-hybrid"></a>Umstellen der MDM-Autorität auf Configuration Manager (hybrid)
Verwenden Sie diesen Abschnitt, um einen vorhandenen Microsoft Intune-Mandanten, der über Intune konfiguriert wurde und dessen MDM-Autorität auf **Microsoft Intune** (standalone) festgelegt ist, ohne Aufheben der Registrierung und erneutes Registrieren vorhandener verwalteter Geräte auf **Configuration Manager** (hybrid) umzustellen.

### <a name="key-considerations"></a>Wichtige Überlegungen
Nachdem Sie auf die neue MDM-Autorität umgestellt haben, gibt es wahrscheinlich eine Übergangszeit (bis zu 8 Stunden), bevor das Gerät eingecheckt und mit dem Dienst synchronisiert wird. Sie müssen Einstellungen in der neuen MDM-Autorität (hybrid) konfigurieren, um sicherzustellen, dass registrierte Geräte nach der Umstellung weiterhin verwaltet und geschützt werden. Beachten Sie dabei Folgendes:
- Geräte müssen nach der Umstellung eine Verbindung mit dem Dienst herstellen, damit die Einstellungen der neuen MDM-Autorität (Intune standalone) die vorhandenen Einstellungen auf dem Gerät ersetzen.
- Nachdem Sie die MDM-Autorität umgestellt haben, verbleiben einige der grundlegenden Einstellungen (z.B. Profile) aus der vorherigen MDM-Autorität (Intune standalone) für bis zu 7 Tage oder bis zur ersten Verbindung des Geräts mit dem Dienst auf dem Gerät. Es wird empfohlen, dass Sie Apps und Einstellungen (Richtlinien, Profile, Apps usw.) so bald wie möglich in der neuer MDM-Autorität (hybrid) konfigurieren und die Einstellungen den Benutzergruppen bereitstellen, die Benutzer mit gegenwärtig registrieren Geräten enthalten. Sobald ein Gerät nach der Umstellung der MDM-Autorität eine Verbindung mit dem Dienst herstellt, werden die neuen Einstellungen der neuen MDM-Autorität übertragen, und Lücken bei Verwaltung und Schutz werden verhindert.

### <a name="prepare-to-change-the-mdm-authority-to-configuration-manager-hybrid"></a>Vorbereiten der Umstellung der MDM-Autorität auf Configuration Manager (hybrid)
Überprüfen Sie die folgenden Informationen, um die Umstellung der MDM-Autorität vorzubereiten:
- Sie benötigen Configuration Manager, Version 1610 oder höher, damit die Option zum Umstellen der MDM-Autorität verfügbar ist.
- Es kann bis zu 8 Stunden dauern, bis ein Gerät eine Verbindung mit dem Dienst herstellt, nachdem Sie auf die neue MDM-Autorität umgestellt haben.
- Erstellen Sie eine Configuration Manager-Benutzersammlung mit allen Benutzern, die zurzeit von Intune standalone verwaltet werden, um Sie beim Einrichten des Intune-Abonnements in der Configuration Manager-Konsole zu nutzen. So können Sie sicherstellen, dass diesen Benutzern und ihren Geräten eine Configuration Manager-Lizenz zugewiesen wird und dass sie nach der Umstellung der MDM-Autorität in der Hybridumgebung verwaltet werden.
- Stellen Sie sicher, dass der IT-Administratorbenutzer auch in dieser Benutzersammlung enthalten ist.  
- Vor der Umstellung wird in der Intune-Verwaltungskonsole für die MDM-Autorität **Auf Microsoft Intune setzen** (Intune standalone) angezeigt.
- Für die MDM-Autorität sollte in der Microsoft Intune-Verwaltungskonsole vor der Umstellung der MDM-Autorität **Auf Microsoft Intune setzen** (eigenständiger Mandant) angezeigt werden.
    > [!NOTE]    
    > Wenn für die MDM-Autorität **Von Intune und Office 365 verwaltet** angezeigt wird, werden Ihre von Office 365 verwalteten MDM-Geräte nicht mehr verwaltet, wenn Sie die MDM-Autorität auf **Configuration Manager** (hybrid) umstellen. Es wird empfohlen, dass Sie die Benutzer für Intune oder Enterprise Mobility Suite lizenzieren, bevor Sie die MDM-Autorität umstellen.   

- Entfernen Sie in der [Microsoft Intune-Verwaltungskonsole](http://manage.microsoft.com) die Geräteregistrierungs-Manager-Rolle. Weitere Informationen finden Sie unter [Löschen eines Geräteregistrierungs-Managers aus Intune](/intune-classic/deploy-use/enroll-corporate-owned-devices-with-the-device-enrollment-manager-in-microsoft-intune#delete-a-device-enrollment-manager-from-intune).
- Deaktivieren Sie alle konfigurierten Gerätegruppenzuordnungen. Weitere Informationen finden Sie unter [Kategorisieren von Geräten mithilfe der Gerätegruppenzuordnung in Microsoft Intune](/intune-classic/deploy-use/categorize-devices-with-device-group-mapping-in-microsoft-intune).
- Während der Umstellung der MDM-Autorität sollte es keine wahrnehmbaren Auswirkungen auf die Endbenutzer geben. Möglicherweise sollten Sie jedoch die Benutzer über die Umstellung informieren, um sicherzustellen, dass ihre Geräte eingeschaltet sind und dass sie kurz nach der Umstellung eine Verbindung mit dem Dienst herstellen. Dadurch wird sichergestellt, dass so viele Geräte wie möglich eine Verbindung herstellen und so bald wie möglich über die neue Autorität beim Dienst registriert werden.
- Wenn Sie vor der Umstellung der MDM-Autorität Intune standalone zum Verwalten von iOS-Geräten verwenden, müssen Sie sicherstellen, dass das gleiche Apple Push Notification Service-Zertifikat (APNs), das zuvor in Intune verwendet wurde, erneuert und wieder zum Einrichten des Mandanten in Configuration Manager (hybrid) verwendet wird.    

    > [!IMPORTANT]  
    > Wenn ein anderes APNs-Zertifikat für die hybride Verwaltung verwendet wird, wird die Registrierung ALLER zuvor registrierten iOS-Geräte aufgehoben, und Sie müssen sie erneut registrieren. Stellen Sie vor der Umstellung der MDM-Autorität sicher, dass Sie genau wissen, welches APNs-Zertifikat zum Verwalten von iOS-Geräten in Intune verwendet wurde. Suchen Sie nach dem Zertifikat im Apple Push Certificates-Portal (https://identity.apple.com), und stellen Sie sicher, dass der Benutzer, mit dessen Apple-ID das ursprüngliche APNs-Zertifikat erstellt wurde, identifiziert wird und verfügbar ist, um das gleiche APNs-Zertifikat als Teil der Umstellung auf die neue MDM-Autorität zu erneuern.  

### <a name="change-the-mdm-authority-to-configuration-manager"></a>Umstellen der MDM-Autorität auf Configuration Manager
Die Umstellung der MDM-Autorität auf Configuration Manager (hybrid) umfasst die folgenden allgemeinen Schritte:  
- Fügen Sie das Microsoft Intune-Abonnement in der Configuration Manager-Konsole hinzu.
- Konfigurieren Sie das Apple APNs-Zertifikat mit dem gleichen APNs-Zertifikat, das Sie erneuert haben.
- Konfigurieren Sie in der Configuration Manager-Verwaltungskonsole die neuen Einstellungen und Apps der neuen MDM-Autorität (hybrid), und stellen Sie sie bereit.
- Wenn Geräte das nächste Mal eine Verbindung mit dem Dienst herstellen, werden sie synchronisiert und erhalten die neuen Einstellungen von der neuen MDM-Autorität.

#### <a name="to-change-the-mdm-authority-to-configuration-manager"></a>So stellen Sie die MDM-Autorität auf Configuration Manager um
1.  Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** &gt; **Übersicht** &gt; **Clouddienste** &gt; **Microsoft Intune-Abonnement**, und wählen Sie aus, dass Sie ein Intune-Abonnement hinzufügen möchten.
2.  Melden Sie sich an dem Intune-Mandanten an, den Sie ursprünglich beim Festlegen der MDM-Autorität in Intune verwendet haben, und klicken Sie auf **Weiter**.
3.  Wählen Sie **MDM-Autorität auf Configuration Manager umstellen** aus, und klicken Sie auf **Weiter**.
4.  Wählen Sie die Benutzersammlung aus, die alle Benutzer enthält, die von der neuen hybriden MDM-Autorität verwaltet werden sollen.
5.  Klicken Sie auf **Weiter** , und schließen Sie den Assistenten ab.  
5.  Die MDM-Autorität wurde jetzt auf **Configuration Manager** umgestellt.
6.  Melden Sie sich an der [Microsoft Intune-Verwaltungskonsole](http://manage.microsoft.com) mit dem gleichen Intune-Mandanten an, und überprüfen Sie, ob die MDM-Autorität in **Auf Configuration Manager setzen** geändert wurde.


### <a name="enable-ios-enrollment"></a>Aktivieren der iOS-Registrierung
Wenn Sie iOS-Geräte verwenden, müssen Sie das APNs-Zertifikat in Configuration Manager konfigurieren.

#### <a name="to-enable-ios-enrollment-and-configure-the-apns-certificate"></a>So aktivieren Sie die iOS-Registrierung und konfigurieren das APNs-Zertifikat

1. **Laden Sie eine Zertifikatsignieranforderung herunter**.

    1.  Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** &gt; **Clouddienste** &gt; **Microsoft Intune-Abonnements**, und wählen Sie **APNs-Zertifikatanforderung erstellen** aus, um das Dialogfeld **APNs-Zertifikatsignieranforderung anfordern** zu öffnen.  
    2.  **Navigieren** Sie zu dem Pfad, um die neue CSR-Datei (Zertifikatsignieranforderung) zu speichern. Speichern Sie die Zertifikatsignierungsanforderung (CSR-Datei) lokal.  
    3.  Klicken Sie auf **Herunterladen**. Die neue CSR-Datei von Microsoft Intune wird heruntergeladen und von Configuration Manager gespeichert.   

    > [!IMPORTANT]
    > Sie müssen eine neue Zertifikatsignieranforderung herunterladen. Verwenden Sie keine vorhandene Datei, da dies zu einem Fehler führt.  

2.  Wechseln Sie zum [Apple Push Certificates-Portal](http://go.microsoft.com/fwlink/?LinkId=269844), und melden Sie sich mit der **gleichen** Apple-ID an, die verwendet wurde, um zuvor das APNs-Zertifikat zu erstellen und zu erneuern, das Sie in Intune standalone verwendet haben.

    ![Anmeldeseite des Apple Push Certificates-Portals](/sccm/mdm/deploy-use/media/mdm-change-apns-portal.png)

3.  Wählen Sie das APNs-Zertifikat aus, das Sie in Intune standalone verwendet haben, und klicken Sie dann auf **Erneuern**.   

    ![Dialogfeld zur APNs-Erneuerung](/sccm/mdm/deploy-use/media/mdm-change-renew-apns.png)

4.  Wählen Sie die APNs-Zertifikatsignieranforderung (CSR-Datei) aus, die Sie lokal heruntergeladen haben, und klicken Sie dann auf **Hochladen**.

    ![Anmeldeseite des Apple Push Certificates-Portals](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)  
5.  Wählen Sie das gleiche APNs-Zertifikat aus, und klicken Sie dann auf **Herunterladen**. Laden Sie das APNs-Zertifikat (PEM) herunter, und speichern Sie die Datei lokal.  

    ![Anmeldeseite des Apple Push Certificates-Portals](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-download.png)

6.  Laden Sie das erneuerte APNs-Zertifikat mit der gleichen Apple-ID wie zuvor auf den hybriden Mandanten hoch.

    1.  Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** &gt; **Clouddienste** &gt; **Microsoft Intune-Abonnement**, und wählen Sie **Plattformen konfigurieren** &gt; **iOS** aus.  
    2.  Wählen Sie im Dialogfeld **Eigenschaften von Microsoft Intune-Abonnement** die Registerkarte **APNs-Zertifikat** aus, und aktivieren Sie das Kontrollkästchen **Registrierung bei iOS und Mac OS X (MDM) aktivieren**.  
    3.  Klicken Sie auf **Durchsuchen**, und wechseln Sie zu der von Apple heruntergeladenen APNs-Zertifikatdatei (CER-Datei). Configuration Manager zeigt die APNs-Zertifikatinformationen an. Klicken Sie auf **OK** , um das APNs-Zertifikat in Intune zu speichern.  

        ![Eigenschaftenseite des Intune-Abonnements – iOS](/sccm/mdm/deploy-use/media/mdm-change-subscription-properties-ios.png)

### <a name="enable-android-enrollment"></a>Aktivieren der Android-Registrierung
1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** &gt; **Clouddienste** &gt; **Microsoft Intune-Abonnement**, und wählen Sie **Plattformen konfigurieren** &gt; **Android** aus.  
2. Wählen Sie **Android-Registrierung aktivieren** aus, und klicken Sie auf **OK**.

### <a name="enable-windows-enrollment"></a>Aktivieren der Windows-Registrierung
1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** &gt; **Clouddienste** &gt; **Microsoft Intune-Abonnement**, und wählen Sie **Plattformen konfigurieren** &gt; **Windows** aus.  
2. Wählen Sie **Windows-Registrierung aktivieren** aus, und klicken Sie auf **OK**.

### <a name="enable-windows-phone-enrollment"></a>Aktivieren der Windows Phone-Registrierung
1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** &gt; **Clouddienste** &gt; **Microsoft Intune-Abonnement**, und wählen Sie **Plattformen konfigurieren** &gt; **Windows Phone** aus.  
2. Wählen Sie die Plattform aus, die Sie aktivieren möchten, und klicken Sie auf **OK**.


### <a name="next-steps"></a>Nächste Schritte
Sobald die Umstellung der MDM-Autorität abgeschlossen ist, überprüfen Sie die folgenden Schritte:
- Wenn der Intune-Dienst erkennt, dass die MDM-Autorität eines Mandanten umgestellt wurde, sendet er eine Benachrichtigung an alle registrierten Geräte, damit sie beim Dienst eingecheckt und synchronisiert werden (außerhalb der regelmäßigen geplanten Eincheckvorgänge). Nach der Umstellung der MDM-Autorität für den Mandanten von Intune standalone auf hybrid stellen daher alle Geräte, die eingeschaltet und online sind, eine Verbindung mit dem Dienst her, erhalten die neue MDM-Autorität und werden zukünftig hybrid verwaltet. Es gibt keine Unterbrechung bei Verwaltung und Schutz dieser Geräte.
- Selbst für Geräte, die während (oder kurz nach) der Umstellung der MDM-Autorität eingeschaltet und online sind, gibt es eine Verzögerung von bis zu 8 Stunden (je nach Zeitpunkt des nächsten geplanten regulären Eincheckvorgangs), bevor Geräte unter der neuen MDM-Autorität beim Dienst registriert werden.    

  > [!IMPORTANT]
  > In der Zeit zwischen der Umstellung der MDM-Autorität und dem Hochladen des erneuerten APNs-Zertifikats in die neue Autorität schlagen neue Registrierungen und Eincheckvorgänge für iOS-Geräte fehl. Aus diesem Grund ist es wichtig, dass Sie das APNs-Zertifikat so bald wie möglich nach der Umstellung der MDM-Autorität überprüfen und in die neue Autorität hochladen.

- Benutzer können schnell auf die neue MDM-Autorität umstellen, indem sie manuell einen Eincheckvorgang des Geräts beim Dienst starten. Benutzer können dies problemlos mithilfe der Unternehmensportal-App und dem Initiieren einer Überprüfung der Gerätekonformität erreichen.
- Um zu überprüfen, ob nach der Umstellung der MDM-Autorität und dem Einchecken und Synchronisieren der Geräte beim Dienst alles ordnungsgemäß funktioniert, suchen Sie in der Configuration Manager-Konsole nach den Geräten. Die Geräte, die zuvor von Intune verwaltet wurden, werden jetzt in der Configuration Manager-Konsole als verwaltete Geräte angezeigt.    
- Es gibt eine Übergangszeit, bis ein Gerät beim Dienst eingecheckt wird, wenn das Gerät während der Umstellung der MDM-Autorität offline war. Um sicherzustellen, dass das Gerät während dieser Übergangszeit geschützt und funktionsfähig bleibt, verbleibt Folgendes für bis zu 7 Tage (oder bis das Gerät eine Verbindung mit der neuen MDM-Autorität herstellt und die neuen Einstellungen empfängt, die die vorhandenen überschreiben) auf dem Gerät:
    - E-Mail-Profil
    - VPN-Profil
    - Zertifikatprofil
    - WLAN-Profil
    - Konfigurationsprofile
- Nachdem Sie auf die neue MDM-Autorität umgestellt haben, kann es bis zu einer Woche dauern, bis die Kompatibilitätsinformationen in der Microsoft Intune-Verwaltungskonsole richtig gemeldet werden. Allerdings sind die Kompatibilitätszustände in Azure Active Directory und auf dem Gerät richtig, sodass das Gerät weiterhin geschützt ist.
- Stellen Sie sicher, dass die neuen Einstellungen, mit denen die vorhandenen Einstellungen überschrieben werden sollen, den gleichen Namen aufweisen wie die vorherigen, damit die alten Einstellungen tatsächlich überschrieben werden. Andernfalls weisen die Geräte möglicherweise redundante Profile und Richtlinien auf.
    > [!TIP]   
    > Es empfiehlt sich, alle Verwaltungseinstellungen und Konfigurationen sowie Bereitstellungen kurz nach Abschluss der Umstellung der MDM-Autorität zu erstellen. Dadurch wird sichergestellt, dass Geräte in der Übergangszeit geschützt und aktiv verwaltet werden.   
-  Führen Sie nach der Umstellung der MDM-Autorität die folgenden Schritte aus, um zu überprüfen, ob neue Geräte erfolgreich bei der neuen Autorität registriert werden:   
    - Registrieren eines neuen Geräts
    - Stellen Sie sicher, dass das neu registrierte Gerät in der Configuration Manager-Konsole angezeigt wird.
    - Führen Sie über die Verwaltungskonsole auf dem Gerät eine Aktion aus, z.B. Remotesperre. Wenn sie erfolgreich ist, wird das Gerät durch die neue MDM-Autorität verwaltet.
- Wenn Sie Probleme mit bestimmten Geräten haben, können Sie die Registrierung der Geräte aufheben und sie erneut registrieren, damit sie so schnell wie möglich mit der neuen Autorität verbunden und von ihr verwaltet werden.
