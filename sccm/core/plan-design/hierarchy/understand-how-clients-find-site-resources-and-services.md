---
title: Trouver des ressources de site | System Center Configuration Manager
description: "Découvrez comment et quand les clients System Center Configuration Manager utilisent l’emplacement du service pour rechercher des ressources de site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5d718d0f9b8c6121f3124a8ade7507c61b7313f2
ms.openlocfilehash: cad4ebd3f8fa275d7d2cad9b2b87c32b971c580d


---
# <a name="understand-how-clients-find-site-resources-and-services-for-system-center-configuration-manager"></a>Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les clients System Center Configuration Manager utilisent un processus appelé **emplacement du service** pour trouver les serveurs de système de site avec lesquels ils peuvent communiquer et qui leur fournissent les services dont ils ont besoin.   Bien comprendre comment et quand les clients utilisent l’emplacement du service pour rechercher des ressources de site peut vous aider à configurer vos sites de manière appropriée pour prendre en charge les opérations des clients.   Ces configurations peuvent nécessiter que le site interagisse avec des configurations de domaine et de réseau telles que les services de domaine Active Directory (AD DS) et DNS, ou que vous utilisiez d’autres configurations plus complexes.  

 Les rôles de système de site qui fournissent des services sont, par exemple, le serveur de base de système de site pour les clients, le point de gestion et les serveurs de système de site supplémentaires avec lesquels le client peut communiquer, tels que les points de distribution et les points de mise à jour logicielle.  



##  <a name="a-namebkmkfunda-fundamentals-of-service-location"></a><a name="bkmk_fund"></a> Fundamentals of service location  
 Quand un client utilise l’emplacement du service pour rechercher un point de gestion avec lequel il peut communiquer, il évalue son emplacement réseau actuel, sa préférence de protocole de communication et son site attribué.  

 **Un client communique avec un point de gestion pour effectuer les opérations suivantes :**  
-   Télécharger des informations sur d’autres points de gestion pour le site, afin de pouvoir générer une liste de points de gestion disponibles pour les cycles ultérieurs d’emplacement du service.  
-   Charger les détails de configuration, tels que l’inventaire et l’état.  
-   Télécharger une stratégie qui définit des configurations sur le client et peut informer celui-ci sur les logiciels qu’il peut ou doit installer, et d’autres tâches connexes.  
-   Demander des informations sur des rôles de système de site supplémentaires qui fournissent les services devant être utilisés par le client, comme des points de distribution de logiciels qu’il peut installer ou des points de mise à jour logicielle à partir desquels obtenir des mises à jour.  

**Un client Configuration Manager effectue une demande d’emplacement du service :**  
-   Toutes les 25 heures de fonctionnement continu  
-   Quand il détecte une modification de sa configuration ou de son emplacement réseau  
-   Quand le service **ccmexec.exe** sur l’ordinateur (le service client de base) démarre  
-   Quand le client doit localiser un rôle de système de site qui fournit un service requis  

**Quand le client essaie de trouver des serveurs qui hébergent des rôles système de site**, il utilise l’emplacement du service pour rechercher un rôle système de site prenant en charge son protocole (HTTP ou HTTPS). Par défaut, les clients utilisent la méthode la plus sûre à leur disposition :  

-   Pour utiliser le protocole HTTPS, vous devez disposer d'une infrastructure à clé publique (PKI) et installer des certificats PKI sur des clients et serveurs. Pour plus d’informations sur la façon d’utiliser des certificats, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

-   Quand vous déployez un rôle de système de site qui utilise Internet Information Services (IIS) et prend en charge les communications des clients, vous devez spécifier si les clients se connectent au système de site à l'aide de HTTP ou HTTPS. Si vous utilisez le protocole HTTP, vous devez également envisager les options de signature et de chiffrement. Pour plus d’informations, consultez [Planification de la signature et du chiffrement](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) dans la rubrique [Planifier la sécurité dans System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md).  

##  <a name="a-namebkmkplanservicelocationa-service-location-and-how-clients-determine-their-assigned-management-point"></a><a name="BKMK_Plan_Service_Location"></a> Emplacement du service et façon dont les clients déterminent leur point de gestion attribué  
Quand un client est attribué pour la première fois à un site principal, il sélectionne un point de gestion par défaut pour ce site. (Les sites principaux prennent en charge plusieurs points de gestion, et chaque client identifie indépendamment un point de gestion comme son point de gestion par défaut.)  Ce point de gestion par défaut devient ensuite le point de gestion attribué de ce client. (Vous pouvez également utiliser des commandes d’installation du client pour définir le point de gestion attribué pour un client au moment de l’installation.)  

-   Le client sélectionne le point de gestion avec lequel communiquer en fonction des configurations actuelles d’emplacement réseau et de groupe de limites du client. Le point de gestion utilisé par le client n’est pas obligatoirement son point de gestion attribué.  

    > [!NOTE]  
    >  Un client utilise toujours le point de gestion attribué pour les messages d’enregistrement et certains messages de la stratégie, même quand d’autres communications sont envoyées à un point de gestion proxy ou local.  

-   Vous pouvez utiliser des points de gestion préférés. Un point de gestion préféré est un point de gestion associé à un groupe de limites en tant que serveur de système de site, semblable à la façon dont les points de distribution ou les points de migration d'état sont associés à un groupe de limites. Si vous activez les points de gestion préférés pour la hiérarchie, lorsqu'un client utilise un point de gestion à partir de son site attribué, il va tenter d'utiliser un point de gestion préféré avant d'utiliser d'autres points de gestion à partir de son site attribué.  

-   Vous pouvez également utiliser les informations du blog suivant sur TechNet.com pour configurer l’affinité de point de gestion. L’affinité de point de gestion remplace le comportement par défaut pour les points de gestion attribués, et permet au client d’utiliser un ou plusieurs points de gestion spécifiques : [affinité de point de gestion](http://blogs.technet.com/b/jchalfant/archive/2014/09/22/management-point-affinity-added-in-configmgr-2012-r2-cu3.aspx).  

Chaque fois qu’un client doit contacter un point de gestion, il consulte une liste de points de gestion connus (appelée **liste PG**), qui est stockée localement dans WMI. Le client crée une liste PG initiale lors de son installation et la met régulièrement à jour avec des détails sur chaque point de gestion de la hiérarchie.  

Quand le client ne trouve pas de point de gestion valide dans sa liste PG, il en recherche dans les sources d'emplacement de service suivantes, dans l'ordre, jusqu'à ce qu'il trouve un point de gestion qu'il peut utiliser :  

1.  Point de gestion  
2.  Services de domaine Active Directory  
3.  DNS  
4.  WINS  

Quand un client a pu localiser et contacter un point de gestion à partir d’une de ces sources, il télécharge la liste actuelle des points de gestion disponibles dans la hiérarchie et met à jour sa liste PG. Cela s'applique aussi bien aux clients qui appartiennent à un domaine qu'à ceux qui n'y appartiennent pas.  

Par exemple, quand un client Configuration Manager sur Internet se connecte à un point de gestion basé sur Internet, ce dernier lui envoie la liste des points de gestion basés sur Internet disponibles sur le site. De même, les clients qui appartiennent à un domaine ou figurent dans des groupes de travail reçoivent également la liste des points de gestion qu'ils peuvent utiliser.  
-   Un client qui n'est pas configuré pour Internet ne reçoit pas de points de gestion exclusivement accessibles sur Internet.  
-   Les clients de groupe de travail configurés pour Internet communiquent uniquement avec des points de gestion accessibles sur Internet.  

##  <a name="a-namebkmkmplista-the-mp-list"></a><a name="BKMK_MPList"></a> La liste PG  
La liste PG est la source d’emplacement de service préférée du client, car c’est une liste hiérarchisée des points de gestion précédemment identifiés par le client. Cette liste est triée par chaque client en fonction de son emplacement réseau au moment où il l'a met à jour, puis stockée localement sur le client dans WMI.  

### <a name="building-the-initial-mp-list"></a>Création de la liste PG initiale  
Pendant l'installation du client, les règles suivantes sont utilisées pour générer la **liste PG**initiale du client :  

-   La liste initiale inclut des points de gestion spécifiés pendant l'installation du client (quand vous utilisez les options **SMSMP**= ou **/MP** ).  
-   Le client recherche dans les services de domaine Active Directory (AD DS) les points de gestion publiés. Pour que le point de gestion soit identifié à partir des services de domaine Active Directory (AD DS), il doit provenir du site attribué du client et avoir la même version de produit que celle du client.  
-   Si aucun point de gestion n'a été spécifié pendant l'installation du client, et si le schéma Active Directory n'est pas étendu, le client recherche des points de gestion publiés dans les services DNS et WINS.  
-   Quand vous créez la liste initiale, les informations sur certains points de gestion de la hiérarchie peuvent ne pas être connues.  

### <a name="organizing-the-management-point-list"></a>Organisation de la liste des points de gestion  
Les clients organisent leur liste de points de gestion selon les classifications suivantes :  

-   **Proxy**: un point de gestion proxy est un point de gestion figurant sur un site secondaire.  
-   **Local** : tout point de gestion associé à l’emplacement réseau actuel du client tel que défini par les limites de site.  
    -   Quand un client appartient à plusieurs groupes de limites, la liste des points de gestion locaux est déterminée en réunissant toutes les limites qui incluent l'emplacement réseau actuel du client.  
    -   En règle générale, les points de gestion de type **Local** sont un sous-ensemble des points de gestion **Attribués** d'un client, sauf si ce dernier se trouve à un emplacement réseau associé à un autre site avec des points de gestion assurant la maintenance de ses groupes de limites.   


-   **Attribué** : tout point de gestion représentant un système de site pour le site attribué du client.  

     Vous pouvez utiliser des points de gestion préférés. Les points de gestion préférés sont des points de gestion à partir d’un site attribué du client qui sont associés à un groupe de limites que le client utilise pour rechercher des serveurs de système de site.  

     Les points de gestion d’un site qui ne sont pas associés à un groupe de limites, ou qui ne sont pas dans un groupe de limites associé à un emplacement réseau actuel du client, ne sont pas considérés comme préférés et sont utilisés lorsque le client ne peut pas identifier un point de gestion préféré disponible.  

### <a name="selecting-a-management-point-to-use"></a>Sélection d'un point de gestion à utiliser  
Pendant une communication classique, un client tente d’utiliser un point de gestion appartenant aux classifications dans l’ordre suivant, en fonction de l’emplacement réseau du client :  

1.  Proxy  
2.  Local  
3.  Attribués  

Toutefois, le client utilise toujours le point de gestion attribué pour les messages d'enregistrement et certains messages de la stratégie, même quand d'autres communications sont envoyées à un point de gestion proxy ou local.  

Dans chaque classification (proxy, local ou attribué), les clients tentent d'utiliser un point de gestion en fonction de certaines préférences, dans l'ordre suivant :  

1.  Compatible HTTPS dans une forêt approuvée ou locale (quand le client est configuré pour la communication HTTPS)  
2.  Compatible HTTPS dans une forêt non approuvée ou non locale (quand le client est configuré pour la communication HTTPS)  
3.  Compatible HTTP dans une forêt approuvée ou locale  
4.  Compatible HTTP dans une forêt non approuvée ou non locale  

Dans l'ensemble des points de gestion triés par préférences, les clients tentent d'utiliser le premier point de gestion de la liste :  

-   Cette liste triée de points de gestion est aléatoire et ne peut pas être ordonnée.  
-   L'ordre de la liste peut varier chaque fois que le client met à jour sa liste de points de gestion.  

Quand un client ne peut pas établir le contact avec le premier point de gestion, il essaie chaque point de gestion successifs de sa liste, en essayant chaque point de gestion préféré de la classification avant d'essayer ceux qui ne le sont pas. Si un client ne parvient pas communiquer avec un point de gestion de la classification, il tente alors de contacter un point de gestion préféré de la classification suivante, et ainsi de suite jusqu'à ce qu'il trouve un point de gestion à utiliser.  

Une fois la communication établie avec un point de gestion, le client continue à utiliser ce même point de gestion jusqu'à ce que :  

-   Au bout de 25 heures, le client sélectionne de manière aléatoire un nouveau point de gestion à utiliser.  
-   Le client a tenté sans succès 5 fois sur une période de 10 minutes de communiquer avec le point de gestion, il sélectionne donc un nouveau point de gestion à utiliser.  

##  <a name="a-namebkmkada-active-directory"></a><a name="bkmk_ad"></a> Active Directory  
Les clients qui appartiennent à un domaine peuvent utiliser les services de domaine Active Directory (AD DS) pour l'emplacement du service. Pour ce faire, les sites doivent [publier des données dans Active Directory](http://technet.microsoft.com/library/hh696543.aspx).  

Les clients peuvent utiliser les services de domaine Active Directory pour l'emplacement du service quand toutes les conditions suivantes sont remplies :  

-   Le [schéma Active Directory est étendu](https://technet.microsoft.com/library/mt345589.aspx) ou a été étendu pour System Center 2012 Configuration Manager.  
-   La [forêt Active Directory est configurée pour la publication](http://technet.microsoft.com/library/hh696542.aspx), de même que les sites Configuration Manager.  
-   L'ordinateur client est membre d'un domaine Active Directory et peut accéder à un serveur de catalogue global.  

Si un client ne peut pas trouver de point de gestion à utiliser pour l'emplacement du service dans AD DS, il tente alors d'utiliser DNS. Les clients qui appartiennent à un domaine peuvent utiliser les services AD DS pour l'emplacement du service. Pour ce faire, les sites doivent [publier des données dans Active Directory](http://technet.microsoft.com/library/hh696543.aspx).  

##  <a name="a-namebkmkdnsa-dns"></a><a name="bkmk_dns"></a> DNS  
Les clients se trouvant sur l'intranet peuvent utiliser DNS pour l'emplacement du service. Pour ce faire, au moins un site d'une hiérarchie doit publier des informations sur les points de gestion dans DNS.  

Envisagez d'utiliser DNS pour l'emplacement du service quand l'une des conditions suivantes est remplie :
-   Le schéma des services de domaine Active Directory n’est pas étendu pour prendre en charge Configuration Manager.
-   Les clients sur intranet se trouvent dans une forêt qui n’est pas activée pour la publication Configuration Manager.  
-   Des clients se trouvent sur des ordinateurs de groupes de travail et ne sont pas configurés pour la gestion des clients uniquement accessibles sur Internet. (Un client de groupe de travail configuré pour Internet communique uniquement avec des points de gestion accessibles sur Internet et n'utilise pas de DNS pour l'emplacement du service).  
-   Vous pouvez [configurer les clients pour rechercher les points de gestion dans les services DNS](http://technet.microsoft.com/library/gg682055).  

Quand un site publie des enregistrements d'emplacement de service pour les points de gestion dans DNS :  

-   La publication est uniquement applicable aux points de gestion qui acceptent les connexions client à partir de l'intranet.  
-   La publication ajoute un enregistrement de ressource d'emplacement du service (SRV RR) dans la zone DNS de l'ordinateur du point de gestion. Une entrée hôte correspondante doit se trouver dans DNS pour cet ordinateur.  

Par défaut, les clients appartenant à un domaine recherchent des enregistrements de point de gestion dans DNS à partir de leur domaine local. Vous pouvez configurer une propriété client qui spécifie un suffixe pour un domaine qui publie des informations de point de gestion dans DNS.  

Pour plus d’informations sur la configuration de la propriété cliente du suffixe DNS, consultez [Guide pratique pour configurer des ordinateurs clients pour trouver des points de gestion à l’aide de la publication DNS dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

Si un client ne peut pas trouver de point de gestion à utiliser pour l'emplacement du service dans DNS, il tente alors d'utiliser WINS.  

### <a name="publish-management-points-to-dns"></a>Publier des points de gestion dans DNS  
Pour publier des points de gestion dans DNS, les deux conditions suivantes doivent être vraies :  

-   Vos serveurs DNS prennent en charge les enregistrements de ressource d'emplacement de service, à l'aide d'une version de BIND qui est au moins la version 8.1.2.  
-   Les noms de domaine complets intranet spécifiés pour les points de gestion dans Configuration Manager ont des entrées d’hôte (par exemple, des enregistrements A) dans DNS.  

> [!IMPORTANT]  
>  La publication DNS Configuration Manager ne prend pas en charge un espace de noms disjoint. En présence d'un espace de noms disjoint, vous pouvez publier manuellement des points de gestion dans DNS ou utiliser l'une des autres méthodes d'emplacement de service décrites dans cette section.  

**Quand vos serveurs DNS prennent en charge les mises à jour automatiques**, vous pouvez configurer Configuration Manager pour qu’il publie automatiquement les points de gestion intranet dans DNS, ou vous pouvez publier manuellement ces enregistrements dans DNS. Lorsque des points de gestion sont publiés dans DNS, leur nom de domaine complet Intranet et leur numéro de port sont publiés dans l'enregistrement d'emplacement de service (SRV). Vous configurez la publication DNS sur un site dans les Propriétés du composant de point de gestion des sites. Pour plus d’informations, consultez [Composants de site pour System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

**Quand la zone DNS a la valeur « Secure only » (Sécurisées uniquement) pour les mises à jour dynamiques**, seul le premier point de gestion pouvant publier dans DNS peut réussir cette action avec les autorisations par défaut.
- Vous pouvez ajouter chaque serveur qui héberge un point de gestion au groupe DnsAdmins pour garantir que ces points de gestion sont autorisés à modifier leurs enregistrements.  
- Si un seul point de gestion peut réussir à publier et modifier son enregistrement DNS, tant que le serveur de ce point de gestion reste intègre, les clients peuvent obtenir la liste complète des points de gestion et trouver leur point de gestion préféré.


**Quand vos serveurs DNS ne prennent pas en charge les mises à jour automatiques, mais prennent en charge les enregistrements d'emplacement de service**, vous pouvez publier manuellement des points de gestion dans DNS. Pour cela, vous devez spécifier manuellement l'enregistrement de la ressource d'emplacement de service (SRV RR) dans DNS.  

Configuration Manager prend en charge la norme RFC 2782 pour les enregistrements d’emplacement de service au format suivant : *_Service._Proto.Nom TTL Classe SRV Priorité Poids Port Cible*  

Pour publier un point de gestion sur Configuration Manager, spécifiez les valeurs suivantes :  

-   **_Service** : entrez **_mssms_mp***_&lt;code_site\>*, où *&lt;code_site\>* est le code site du point de gestion.  
-   **._Proto**: spécifiez **._tcp**.  
-   **.Name**: entrez le suffixe DNS du point de gestion, par exemple **contoso.com**.  
-   **TTL**: entrez **14400**, ce qui correspond à quatre heures.  
-   **Class**: spécifiez **IN** (conformément à la norme RFC 1035).  
-   **Priorité** : ce champ n’est pas utilisé par Configuration Manager.
-   **Poids** : ce champ n’est pas utilisé par Configuration Manager.  
-   **Port**: entrez le numéro de port que le point de gestion utilise, par exemple **80** pour HTTP et **443** pour HTTPS.  

    > [!NOTE]  
    >  Le port d'enregistrement SRV doit correspondre au port de communication utilisé par le point de gestion. Par défaut, le port **80** est utilisé pour les communications HTTP et le port **443** pour les communications HTTPS.  

-   **Cible**: entrez le nom de domaine complet de l'intranet spécifié pour le système de site configuré avec le rôle de site de point de gestion.  

Si vous utilisez le DNS Windows Server, vous pouvez utiliser la procédure suivante pour entrer cet enregistrement DNS pour les points de gestion intranet. Si vous utilisez une autre implémentation de DNS, utilisez les informations de cette section sur les valeurs de champ et consultez la documentation de ce DNS pour adapter cette procédure.  

##### <a name="to-configure-automatic-publishing"></a>Pour configurer la publication automatique :  

1.  Dans la console Configuration Manager, développez **Administration** > **Configuration du site** > **Sites**.  

2.  Sélectionnez votre site, puis cliquez sur **Configurer les composants de site**.  

3.  Sélectionnez **Point de gestion**.  

4.  Sélectionnez les points de gestion à publier. (Cette sélection s'applique à la publication dans AD DS et DNS).  

5.  Cochez la case de publication dans DNS :  

    -   Cette boîte de dialogue vous permet de sélectionner les points de gestion à publier et de publier dans DNS.  

    -   Cette boîte de dialogue ne configure pas la publication dans AD DS.  

##### <a name="to-manually-publish-management-points-to-dns-on-windows-server"></a>Pour publier manuellement des points de gestion dans DNS sur Windows Server  

1.  Dans la console Configuration Manager, spécifiez les noms de domaine complets d'intranet des systèmes de site.  

2.  Dans la console de gestion DNS, sélectionnez la zone DNS de l'ordinateur du point de gestion.  

3.  Vérifiez qu'il existe un enregistrement d'hôte (A ou AAAA) pour le nom de domaine complet d'intranet du système de site. Si cet enregistrement n'existe pas, créez-le.  

4.  À l'aide de l'option **Autres nouveaux enregistrements** , cliquez sur **Emplacement du service (SRV)** dans la boîte de dialogue **Type d'enregistrement de ressource** , cliquez sur **Créer un enregistrement**, entrez les informations suivantes, puis cliquez sur **Terminé**:  

    -   **Domain**: si nécessaire, entrez le suffixe DNS du point de gestion, par exemple **contoso.com**.  
    -   **Service** : tapez **_mssms_mp***_&lt;code_site\>*, où *&lt;code_site\>* est le code de site du point de gestion.  
    -   **Protocol**: entrez **_tcp**.  
    -   **Priorité** : ce champ n’est pas utilisé par Configuration Manager.  
    -   **Poids** : ce champ n’est pas utilisé par Configuration Manager.  
    -   **Port**: entrez le numéro de port que le point de gestion utilise, par exemple **80** pour HTTP et **443** pour HTTPS.  

        > [!NOTE]  
        >  Le port d'enregistrement SRV doit correspondre au port de communication utilisé par le point de gestion. Par défaut, le port **80** est utilisé pour les communications HTTP et le port **443** pour les communications HTTPS.  

    -   **Hôte offrant ce service**: entrez le nom de domaine complet de l'intranet spécifié pour le système de site configuré avec le rôle de site de point de gestion.  

Répétez ces étapes pour chaque point de gestion de l'intranet que vous souhaitez publier dans DNS.  

##  <a name="a-namebkmkwinsa-wins"></a><a name="bkmk_wins"></a> WINS  
En cas d'échec d'autres mécanismes d'emplacement de service, les clients peuvent trouver un point de gestion initial en examinant WINS.  

Par défaut, un site principal publie dans WINS le premier point de gestion du site configuré pour le protocole HTTP et le premier point de gestion configuré pour le protocole HTTPS.  

Si vous ne souhaitez pas que les clients trouvent un point de gestion HTTP dans WINS, configurez les clients avec la propriété CCMSetup.exe Client.msi **SMSDIRECTORYLOOKUP=NOWINS**.  



<!--HONumber=Nov16_HO1-->


