---
title: Erstellen von SCEP-Zertifikatprofilen | Microsoft-Dokumentation
description: "Erfahren Sie mehr über die Verwendung von Zertifikatprofilen, um für verwaltete Geräten die Zertifikate bereitzustellen, die sie in System Center Configuration Manager benötigen."
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
caps.latest.revision: "16"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 1e00804d27ecef2aadd8bfa395db1919c46243ee
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-certificate-profiles"></a>Erstellen von Zertifikatprofilen

*Gilt für: System Center Configuration Manager (Current Branch)*


Verwenden Sie Zertifikatprofile in Configuration Manager (SCCM), um für verwaltete Geräte die Zertifikate bereitzustellen, die sie für den Zugriff auf Unternehmensressourcen benötigen. Legen Sie vor de Erstellen von Zertifikatprofilen die Zertifikatinfrastruktur wie unter [Erstellen von Zertifikatprofilen in System Center Configuration Manager](certificate-infrastructure.md) erklärt fest.  

Dieses Thema beschreibt, wie Sie vertrauenswürdige Stamm- und SCEP-Zertifikatprofile erstellen. Wenn Sie die PFX-Zertifikatprofile erstellen möchten, sollten Sie den Artikel [Erstellen von PFX-Zertifikatprofilen](../../protect/deploy-use/create-pfx-certificate-profiles.md) lesen.

Erstellen eines Zertifikatprofils:

1.  Starten Sie den Assistenten zum Erstellen von Zertifikatprofilen.
1.  Stellen Sie allgemeine Informationen zum Zertifikat bereit.
1.  Konfigurieren Sie ein Zertifikat über eine vertrauenswürdige Zertifizierungsstelle (CA).  
1.  Konfigurieren Sie die SCEP-Zertifikatinformationen (nur für SCEP-Zertifikate).  
1.  Geben Sie die unterstützten Plattformen für das Zertifikatprofil an.


## <a name="start-the-create-certificate-profile-wizard"></a>Starten Sie den Assistenten zum Erstellen von Zertifikatprofilen.  

1.  Klicken Sie in der System Center Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, den **Zugriff auf Unternehmensressourcen**, und klicken Sie dann auf **Zertifikatprofile**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Zertifikatprofil erstellen**.  

## <a name="provide-general-information-about-the-certificate-profile"></a>Bereitstellen von allgemeinen Informationen zum Zertifikatprofil  

Geben Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Zertifikatprofilen die folgenden Informationen an:  

-   **Name**: Geben Sie einen eindeutigen Namen für das Zertifikatprofil ein. Sie können maximal 256 Zeichen verwenden.  

-   **Beschreibung**: Geben Sie eine Beschreibung mit einem Überblick über das Zertifikatprofil sowie weitere relevante Informationen ein, die der Identifikation des Profils in der System Center Configuration Manager-Konsole dienen. Sie können maximal 256 Zeichen verwenden.  

-   **Geben Sie den Typ des Zertifikatprofils an, das Sie erstellen möchten**: Wählen Sie einen der folgenden Typen für das Zertifikatprofil aus:  

-   **Vertrauenswürdiges Zertifikat der Zertifizierungsstelle**: Wählen Sie diesen Typ für das Zertifikatprofil aus, falls Sie ein Zertifikat einer vertrauenswürdigen Stamm- oder Zwischenzertifizierungsstelle bereitstellen möchten, um eine Vertrauenskette zu bilden, wenn der Benutzer oder das Gerät ein anderes Gerät authentifizieren muss. Hierbei könnte es sich etwa um einen RADIUS-Server (Remote Authentication Dial-In User Service) oder einen VPN-Server (Virtual Private Network) handeln. Darüber hinaus müssen Sie ein Profil mit einem vertrauenswürdigen Zertifikat der Zertifizierungsstelle konfigurieren, bevor Sie ein SCEP-Zertifikatprofil erstellen können. In diesem Fall muss das vertrauenswürdige Zertifikat der Zertifizierungsstelle das vertrauenswürdige Stammzertifikat für die Zertifizierungsstelle sein, von der das Zertifikat für den Benutzer oder das Gerät ausgestellt wird.  

-   **Einstellungen für Simple Certificate Enrollment-Protokoll (SCEP)**: Wählen Sie diesen Typ für das Zertifikatprofil aus, wenn Sie mit dem Simple Certificate Enrollment-Protokoll und dem Rollendienst „Registrierungsdienst für Netzwerkgeräte“ ein Zertifikat für einen Benutzer oder ein Gerät anfordern möchten.

-   **Privater Informationsaustausch – PKCS #12 (.PFX)-Einstellungen – Importieren**: Wählen Sie diese Option aus, um ein PFX-Zertifikat zu importieren. Weitere Informationen zum Erstellen eines PFX-Zertifikats finden Sie unter [Import PFX certificate profiles (Importieren von PFX-Zertifikatprofilen)](/sccm/mdm/deploy-use/import-pfx-certificate-profiles.md).

-   **Personal Information Exchange PKCS #12 (PFX) settings - Create** (Privater Informationsaustausch PKCS #12 (PFX): Einstellungen: Erstellen): Wählen Sie diese Option aus, um PFX-Zertifikate zu verarbeiten, die eine Zertifizierungsstelle verwenden. Weitere Informationen zum Erstellen von PFX-Zertifikaten finden Sie unter [Erstellen von PFX-Zertifikatprofilen](/sccm/mdm/deploy-use/create-pfx-certificate-profiles.md).


## <a name="configure-a-trusted-ca-certificate"></a>Konfigurieren eines vertrauenswürdigen Zertifikats der Zertifizierungsstelle  

> [!IMPORTANT]  
>  Sie müssen mindestens ein Profil mit einem vertrauenswürdigen Zertifikat der Zertifizierungsstelle konfigurieren, bevor Sie ein SCEP-Zertifikatprofil erstellen können.    
>  
>  Wenn Sie einen dieser Werte nach der Bereitstellung des Zertifikats ändern, wird ein neues Zertifikat angefordert:
>  -  Schlüsselspeicheranbieter
>  -  Name der Zertifikatvorlage
>  -  Zertifikattyp
>  -  Format des Antragstellernamens
>  -  Alternativer Antragstellername
>  -  Gültigkeitsdauer des Zertifikats
>  -  Schlüsselverwendung
>  -  Schlüsselgröße
>  -  Erweiterte Schlüsselverwendung
>  -  Zertifikat der Stammzertifizierungsstelle

1.  Geben Sie auf der Seite **Vertrauenswürdiges Zertifikat der Zertifizierungsstelle** des Assistenten zum Erstellen von Zertifikatprofilen die folgenden Informationen an:  

 -   **Zertifikatdatei**: Klicken Sie auf **Importieren** , und navigieren Sie dann zu der Zertifikatdatei, die Sie verwenden möchten.  

 -   **Zielspeicher**: Wählen Sie für Geräte, die mehr als einen Zertifikatspeicher haben, den Speicherort des Zertifikats aus. Bei Geräten, die nur einen Speicher haben, wird diese Einstellung ignoriert.  

2.  Stellen Sie mit dem Wert **Zertifikatfingerabdruck** sicher, dass Sie das richtige Zertifikat importiert haben.  


## <a name="configure-scep-certificate-information-only-for-scep-certificates"></a>Konfigurieren von SCEP-Zertifikatinformationen (nur für SCEP-Zertifikate)  

1.  Geben Sie auf der Seite **SCEP-Server** des Assistenten zum Erstellen von Zertifikatprofilen die URLs für die NDES-Server ein, die über SCEP Zertifikate ausstellen. Sie können auswählen, dass eine NDES-URL auf Basis der Konfiguration des Zertifikatregistrierungspunkt-Standortsystemservers automatisch zugewiesen wird, oder Sie können die URLs manuell hinzufügen.  

2.  Schließen Sie die Seite **SCEP Enrollment** (SCEP-Anmeldung) des Assistenten zum Erstellen von Zertifikatprofilen ab.

 -  **Wiederholungen**: Geben Sie an, wie häufig vom Gerät automatisch versucht werden soll, das Zertifikat beim Server mit dem Registrierungsdienst für Netzwerkgeräte anzufordern. Mit dieser Einstellung wird das Szenario unterstützt, bei dem eine Zertifikatanforderung von einem Zertifizierungsstellen-Manager genehmigt werden muss, bevor sie akzeptiert wird. Sie wird üblicherweise in Umgebungen mit hoher Sicherheit oder in Fällen verwendet, in denen eine eigenständige ausstellende Zertifizierungsstelle statt einer Unternehmenszertifizierungsstelle eingesetzt wird. Sie können diese Einstellung auch für Testzwecke nutzen, sodass Sie die Optionen der Zertifikatanforderung prüfen können, bevor die Zertifikatanforderung von der ausstellenden Zertifizierungsstelle verarbeitet wird. Verwenden Sie diese Einstellung zusammen mit der Einstellung **Wiederholungsverzögerung (Minuten)** .  

 -   **Wiederholungsverzögerung (Minuten)**: Geben Sie das Intervall in Minuten zwischen den Anmeldeversuchen an, wenn die Genehmigung durch einen Zertifizierungsstellen-Manager benötigt wird, bevor die Zertifikatanforderungen von der ausstellenden Zertifizierungsstelle verarbeitet werden. Wenn Sie zu Testzwecken die Genehmigung eines Managers nutzen, sollten Sie einen niedrigen Wert angeben, damit Sie nach der Genehmigung der Zertifikatanforderung nicht zu lange auf die Wiederholung der Anforderung durch das Gerät warten müssen. Wenn Sie die Genehmigung eines Managers in einem Produktionsnetzwerk nutzen, sollten Sie dagegen einen höheren Wert angeben, damit der Zertifizierungsstellenadministrator ausreichend Zeit zum Überprüfen und Genehmigen bzw. Verweigern ausstehender Genehmigungen hat.  

 -   **Erneuerungsschwellenwert (%)**: Geben Sie den Prozentsatz der Zertifikatgültigkeitsdauer an, die verbleibt, bevor das Gerät eine Erneuerung des Zertifikats anfordert.  

 -   **Schlüsselspeicheranbieter**: Geben Sie an, wo der Schlüssel für das Zertifikat gespeichert wird. Wählen Sie einen der folgenden Werte aus:  

   -   **Auf Trusted Platform Module (TPM) installieren, falls vorhanden**: Installiert den Schlüssel auf dem TPM. Wenn das TPM nicht vorhanden ist, wird der Schlüssel im Speicheranbieter für den Softwareschlüssel installiert.  

   -   **Auf Trusted Platform Module (TPM) installieren, andernfalls Fehler**: Installiert den Schlüssel auf dem TPM. Wenn das TPM nicht vorhanden ist, schlägt die Installation fehl.  

   -   **In Windows Hello for Business installieren, andernfalls Fehler**: Diese Option ist für Windows 10 Desktop- und Mobile-Geräte verfügbar. Dadurch wird der Schlüssel zu **Windows Hello for Business** angemeldet, der in [Windows Hello für Business-Einstellungen in System Center Configuration Manager](../../protect/deploy-use/windows-hello-for-business-settings.md) beschrieben wird. Diese Option ermöglicht es Ihnen außerdem, bei der Registrierung von Geräten die **mehrstufige Authentifizierung zu erfordern** , bevor für diese Geräte Zertifikate ausgestellt werden. Weitere Informationen finden Sie unter [Schützen von Windows-Geräten mit mehrstufiger Authentifizierung](https://technet.microsoft.com/library/dn889751.aspx) .

   > [!NOTE]  
   > 
   > Wenn ein Benutzer eine Windows Hello for Business-PIN erstellt, sendet Windows eine Benachrichtigung, auf die Configuration Manager lauscht. So kann Configuration Manager schnell erkennen, welche Benutzer eine Windows Hello-PIN erstellt haben. Configuration Manager kann diesen Benutzern dann auch neue Zertifikate ausstellen, wenn Windows Hello als Schlüsselspeicheranbieter in einem Zertifikatprofil dient.  

   -   **Im Softwareschlüsselspeicher-Anbieter installieren**: Installiert den Schlüssel im Speicheranbieter für den Softwareschlüssel.  

 -   **Geräte für die Zertifikatregistrierung**: Wenn das Zertifikatprofil in einer Benutzersammlung bereitgestellt wird, wählen Sie aus, ob die Zertifikatregistrierung nur auf dem primären Gerät des Benutzers oder auf allen Geräten, bei denen der Benutzer sich anmeldet, zulässig sein soll. Wenn das Zertifikatprofil in einer Gerätesammlung bereitgestellt wird, wählen Sie aus, ob die Zertifikatregistrierung nur für den primären Benutzer des Geräts oder für alle Benutzer, die sich bei dem Gerät anmelden, zulässig sein soll.  

3.  Geben Sie auf der Seite **Zertifikateigenschaften** des Assistenten zum Erstellen von Zertifikatprofilen die folgenden Informationen an:  

 -   **Name der Zertifikatvorlage**: Klicken Sie auf **Durchsuchen** , um den Namen der Zertifikatvorlage auszuwählen, der im Registrierungsdienst für Netzwerkgeräte konfiguriert ist und der einer ausstellenden Zertifizierungsstelle hinzugefügt wurde. Damit Sie Zertifikatvorlagen durchsuchen können, muss das Benutzerkonto, mit dem Sie die System Center Configuration Manager-Konsole ausführen, über die Leseberechtigung für die Zertifikatvorlage verfügen. Wenn Sie **Durchsuchen**nicht verwenden können, geben Sie alternativ den Namen der Zertifikatvorlage ein.  

 > [!IMPORTANT]
 >   
 >  Sind im Namen der Zertifikatvorlage Nicht-ASCII-Zeichen enthalten (beispielsweise Zeichen aus dem chinesischen Alphabet), dann wird das Zertifikat nicht bereitgestellt. Damit sichergestellt ist, dass das Zertifikat bereitgestellt wird, müssen Sie zunächst eine Kopie der Zertifikatvorlage auf die Zertifizierungsstelle kopieren und diese Kopie dann unter Verwendung von ASCII-Zeichen umbenennen.  

   Beachten Sie je nachdem, ob Sie zur Zertifikatvorlage navigieren oder den Namen des Zertifikats eingeben, Folgendes:  

 -   Wenn Sie zur Auswahl des Zertifikatvorlagennamens zur Zertifikatvorlage navigieren, werden einige Felder auf der Seite automatisch aus der Zertifikatvorlage aufgefüllt. In einigen Fällen können Sie diese Werte erst ändern, wenn Sie eine andere Zertifikatvorlage auswählen.  

 -   Wenn Sie den Namen der Zertifikatvorlage eingeben, stellen Sie sicher, dass der Name genau mit einer der in der Registrierung des Servers mit dem Registrierungsdienst für Netzwerkgeräte aufgeführten Zertifikatvorlagen übereinstimmt. Achten Sie darauf, dass Sie den Namen der Zertifikatvorlage und nicht den Anzeigenamen der Zertifikatvorlage angeben.  

   Navigieren Sie zu dem Schlüssel „HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP“, um die Namen von Zertifikatvorlagen zu suchen. Die Zertifikatvorlagen werden als Werte für **EncryptionTemplate**, **GeneralPurposeTemplate**und **SignatureTemplate**aufgeführt. Standardmäßig ist der Wert für die drei Zertifikatvorlagen **IPSECIntermediateOffline**. Dieser Wert entspricht dem Anzeigenamen **IPSec (Offlineanforderung)**.  

   > [!WARNING]  
   > 
   >  Da die Inhalte der Zertifikatvorlage von System Center Configuration Manager nicht überprüft werden können, wenn Sie den Namen der Zertifikatvorlage eingeben, statt zu ihm zu navigieren, können Sie möglicherweise Optionen auswählen, die von der Zertifikatvorlage nicht unterstützt werden. Dies führt zu einem Fehler bei der Zertifikatanforderung. In diesem Fall wird in der Datei CPR.log eine Fehlermeldung für w3wp.exe angezeigt, die besagt, dass der Vorlagenname in der Zertifikatsignieranforderung (CSR) und die Abfrage nicht übereinstimmen.  
   >   
   >  Wenn Sie den Namen der Zertifikatvorlage eingeben, der für den Wert **GeneralPurposeTemplate** angegeben ist, müssen Sie für dieses Zertifikatprofil die Optionen **Schlüsselverschlüsselung** und **Digitale Signatur** auswählen. Wenn Sie in diesem Zertifikatprofil jedoch nur die Option **Schlüsselverschlüsselung** aktivieren möchten, geben Sie den Namen der Zertifikatvorlage für den Schlüssel **EncryptionTemplate** an. Wenn Sie in diesem Zertifikatprofil dagegen nur die Option **Digitale Signatur** aktivieren möchten, geben Sie den Namen der Zertifikatvorlage für den Schlüssel **SignatureTemplate** an.  

 -   **Zertifikattyp**: Wählen Sie aus, ob das Zertifikat für ein Gerät oder einen Benutzer bereitgestellt wird.  
 -   **Format des Antragstellernamens**: Wählen Sie in der Liste aus, wie System Center Configuration Manager den Antragstellernamen in der Zertifikatanforderung automatisch erstellt. Wenn das Zertifikat für einen Benutzer bestimmt ist, können Sie auch die E-Mail-Adresse des Benutzers im Antragstellernamen einschließen. 
    
   > [!NOTE]  
   > 
   > Durch Auswahl der **IMEI-Nummer** oder **Seriennummer** können Sie zwischen verschiedenen Geräten unterscheiden, die dem gleichen Benutzer gehören. Bei diesen Geräten kann z.B. der allgemeine Name identisch sein, nicht aber die IMEI-Nummer oder Seriennummer. Wenn das Gerät keine IMEI- oder Seriennummer meldet, wird das Zertifikat mit dem allgemeinen Namen ausgegeben.

 -   **Alternativer Antragstellername**: Geben Sie an, wie die Werte für den alternativen Antragstellernamen (Subject Alternative Name, SAN) in der Zertifikatanforderung von System Center Configuration Manager automatisch erstellt werden sollen. Beispiel: Wenn Sie einen Benutzerzertifikattyp ausgewählt haben, könnten Sie in den alternativen Antragstellernamen den Benutzerprinzipalnamen (User Principal Name, UPN) aufnehmen.  Wenn das Clientzertifikat für die Authentifizierung bei einem Netzwerkrichtlinienserver verwendet werden soll, müssen Sie den alternativen Antragstellernamen auf den Benutzerprinzipalnamen festlegen.  

   > [!NOTE]  
   >  - Von iOS-Geräten werden beschränkte Formate des Antragstellernamens und alternative Antragstellernamen in SCEP-Zertifikaten unterstützt. Wenn Sie ein nicht unterstütztes Format angeben, werden Zertifikate auf iOS-Geräten nicht registriert. Wenn Sie ein SCEP-Zertifikatprofil für die Bereitstellung auf iOS-Geräten konfigurieren, verwenden Sie den **allgemeinen Namen** für **Format des Antragstellernamens**und den **DNS-Namen**, die **E-Mail-Adresse** oder den **UPN** für **Alternativer Antragstellername**.  

 -   **Gültigkeitsdauer des Zertifikats**: Wenn Sie den Befehl „certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE“ auf der ausstellenden Zertifizierungsstelle ausgeführt haben, die eine benutzerdefinierte Gültigkeitsdauer ermöglicht, können Sie die verbleibende Dauer bis zum Ablauf des Zertifikats angeben. Weitere Informationen zu diesem Befehl finden Sie im Thema [Certificate infrastructure in System Center Configuration Manager (Zertifikatinfrastruktur in System Center Configuration Manager)](../../protect/deploy-use/certificate-infrastructure.md).  

   Sie können einen niedrigeren Wert als den für die Gültigkeitsdauer in der angegebenen Zertifikatvorlage angeben, aber keinen höheren. Beispiel: Wenn die Gültigkeitsdauer des Zertifikats in der Zertifikatvorlage zwei Jahre beträgt, können Sie als Wert ein Jahr angeben, aber nicht fünf Jahre. Zudem muss der Wert niedriger als die verbleibende Gültigkeitsdauer des Zertifikats der ausstellenden Zertifizierungsstelle sein.  

 -   **Schlüsselverwendung**: Geben Sie Schlüsselverwendungsoptionen für das Zertifikat an. Sie können unter folgenden Optionen wählen:  

        -   **Schlüsselverschlüsselung**: Lässt den Schlüsselaustausch nur zu, wenn der Schlüssel verschlüsselt ist.  

        -   **Digitale Signatur**: Lässt den Schlüsselaustausch nur zu, wenn der Schlüssel durch eine digitale Signatur geschützt ist.  

   Wenn Sie eine Zertifikatvorlage über **Durchsuchen**ausgewählt haben, können Sie diese Einstellungen eventuell erst dann ändern, wenn Sie eine andere Zertifikatvorlage ausgewählt haben.  

   Die ausgewählte Zertifikatvorlage muss mit mindestens einer der beiden oben angegebenen Optionen zur Schlüsselnutzung konfiguriert sein. Andernfalls wird die Meldung **Schlüsselverwendung in CSR und Abfrage stimmen nicht überein** in der Protokolldatei **Crp.log**für den Zertifikatregistrierungspunkt aufgeführt.  


   -   **Schlüsselgröße (Bits)**: Wählen Sie die Größe des Schlüssels in Bit.  

   -   **Erweiterte Schlüsselverwendung**: Klicken Sie auf **Auswählen**, um Werte für den beabsichtigten Zweck des das Zertifikats hinzuzufügen. In den meisten Fällen erfordert das Zertifikat **Clientauthentifizierung** , damit der Benutzer bzw. das Gerät auf einem Server authentifiziert werden kann. Sie können jedoch nach Bedarf weitere Schlüsselverwendungen hinzufügen.  


   -   **Hashalgorithmus**: Wählen Sie einen der verfügbaren Hashalgorithmustypen, der für dieses Zertifikat verwendet werden soll. Wählen Sie die höchste Sicherheitsebene aus, die die verbundenen Geräten unterstützen.  

   > [!NOTE]  
   > 
   >  **SHA-2** unterstützt SHA-256, SHA-384 und SHA-512. **SHA-3** unterstützt nur SHA-3.  

   -   **Zertifikat der Stammzertifizierungsstelle**: Klicken Sie auf **Auswählen** , um ein Profil für ein Stamm-Zertifizierungsstellenzertifikat auszuwählen, das Sie zuvor konfiguriert und für den Benutzer oder das Gerät bereitgestellt haben. Dieses Zertifizierungsstellenzertifikat muss das Stammzertifikat für die Zertifizierungsstelle sein, die das Zertifikat ausstellt, das Sie in diesem Zertifikatprofil konfigurieren.  

   > [!IMPORTANT]  
   >  Wenn Sie ein Zertifikat der Stammzertifizierungsstelle angeben, das dem Benutzer oder Gerät nicht bereitgestellt wurde, wird die Anforderung des Zertifikats, das Sie in diesem Zertifikatprofil konfigurieren, von System Center Configuration Manager nicht eingeleitet.  


##  <a name="specify-supported-platforms-for-the-certificate-profile"></a>Angeben von unterstützten Plattformen für das Zertifikatprofil  

1. Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten zum Erstellen von Zertifikatprofilen die Betriebssysteme aus, unter denen das Zertifikatprofil installiert wird. Alternativ klicken Sie auf **Alle auswählen** , um das Zertifikatprofil unter allen verfügbaren Betriebssystemen zu installieren.
2. Prüfen Sie die **Übersichtsseite** des Assistenten, und wählen Sie **Fertig stellen** aus. 
 
 
Das neue Zertifikatprofil wird im Knoten **Zertifikatprofile** im Arbeitsbereich **Bestand und Kompatibilität** angezeigt und steht zur Bereitstellung für Benutzer oder Geräte wie unter [How to deploy profiles in System Center Configuration Manager (Bereitstellen von Profilen in System Center Configuration Manager)](deploy-wifi-vpn-email-cert-profiles.md) beschrieben zur Verfügung.  