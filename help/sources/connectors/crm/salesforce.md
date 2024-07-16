---
title: Panoramica del connettore Source Salesforce
description: Scopri come collegare Salesforce a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 5d28db34edd377269e8710b1741098a08616ae5f
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# [!DNL Salesforce]

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un sistema CRM di terze parti. Il supporto per i provider di gestione delle relazioni con i clienti include [!DNL Salesforce].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

## Mappatura campo da [!DNL Salesforce] a XDM

Per stabilire una connessione di origine tra [!DNL Salesforce] e Platform, i campi dati di origine [!DNL Salesforce] devono essere mappati sui campi XDM di destinazione appropriati prima di essere acquisiti in Platform.

Per informazioni dettagliate sulle regole di mappatura dei campi tra [!DNL Salesforce] set di dati e Platform, consulta:

- [Contatti](../adobe-applications/mapping/salesforce.md#contact)
- [Lead](../adobe-applications/mapping/salesforce.md#lead)
- [Account](../adobe-applications/mapping/salesforce.md#account)
- [Opportunità](../adobe-applications/mapping/salesforce.md#opportunity)
- [Ruoli di contatto opportunità](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campagne](../adobe-applications/mapping/salesforce.md#campaign)
- [Membri della campagna](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Relazione contatto account](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## Configurare l&#39;utilità di generazione automatica dello spazio dei nomi e dello schema [!DNL Salesforce]

Per utilizzare l&#39;origine [!DNL Salesforce] come parte di [!DNL B2B-CDP], è necessario prima impostare un&#39;utilità [!DNL Postman] per generare automaticamente gli spazi dei nomi e gli schemi [!DNL Salesforce]. La documentazione seguente fornisce ulteriori informazioni sulla configurazione dell&#39;utilità [!DNL Postman]:

- È possibile scaricare la raccolta di utilità di generazione automatica dello spazio dei nomi e dello schema e l&#39;ambiente da questo [archivio GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Per informazioni sull&#39;utilizzo delle API di Platform, inclusi i dettagli su come raccogliere i valori per le intestazioni richieste e leggere chiamate API di esempio, consulta la guida introduttiva [alle API di Platform](../../../landing/api-guide.md).
- Per informazioni su come generare le credenziali per le API di Platform, consulta l&#39;esercitazione su [autenticazione e accesso alle API di Experience Platform](../../../landing/api-authentication.md).
- Per informazioni sulla configurazione di [!DNL Postman] per le API di Platform, consulta l&#39;esercitazione su [configurazione della console per sviluppatori e  [!DNL Postman]](../../../landing/postman.md).

Con una console per sviluppatori Platform e [!DNL Postman] configurati, puoi iniziare ad applicare i valori di ambiente appropriati all&#39;ambiente [!DNL Postman].

La tabella seguente contiene valori di esempio e informazioni aggiuntive sul popolamento dell&#39;ambiente [!DNL Postman]:

| Variable | Descrizione | Esempio |
| --- | --- | --- |
| `CLIENT_SECRET` | Identificatore univoco utilizzato per generare `{ACCESS_TOKEN}`. Per informazioni su come recuperare `{CLIENT_SECRET}`, consulta il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md). | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Il JSON Web Token (JWT) è una credenziale di autenticazione utilizzata per generare {ACCESS_TOKEN}. Per informazioni su come generare `{JWT_TOKEN}`, consulta il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md). | `{JWT_TOKEN}` |
| `API_KEY` | Identificatore univoco utilizzato per autenticare le chiamate alle API Experience Platform. Per informazioni su come recuperare `{API_KEY}`, consulta il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md). | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Il token di autorizzazione necessario per completare le chiamate alle API Experience Platform. Per informazioni su come recuperare `{ACCESS_TOKEN}`, consulta il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md). | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Il contenitore `global` contiene tutte le classi, i gruppi di campi dello schema, i tipi di dati e gli schemi standard forniti dal partner Adobe e Experience Platform. Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su `global`. | `global` |
| `PRIVATE_KEY` | Credenziali utilizzate per autenticare l&#39;istanza [!DNL Postman] in Experience Platform API. Per istruzioni su come recuperare {PRIVATE_KEY}, consulta il tutorial sulla configurazione di Developer Console e [configurazione di Developer Console e [!DNL Postman]](../../../landing/postman.md). | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Credenziali utilizzate per l&#39;integrazione in Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management System (IMS) fornisce il framework per l’autenticazione nei servizi Adobe. Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Entità aziendale che può possedere o concedere in licenza prodotti e servizi e consentire l&#39;accesso ai propri membri. Per istruzioni su come recuperare le informazioni di `{ORG_ID}`, consulta il tutorial su [come configurare la console per sviluppatori e  [!DNL Postman]](../../../landing/postman.md). | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nome della partizione sandbox virtuale in uso. | `prod` |
| `TENANT_ID` | ID utilizzato per garantire che le risorse create abbiano lo spazio dei nomi corretto e siano contenute all’interno dell’organizzazione. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | L’endpoint URL a cui stai effettuando chiamate API. Questo valore è fisso ed è sempre impostato su: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | ID univoco dell&#39;account [!DNL Marketo]. Per informazioni su come recuperare `munchkinId`, consulta il tutorial su [autenticazione dell&#39;istanza](../adobe-applications/marketo/marketo-auth.md). [!DNL Marketo]  | `123-ABC-456` |
| `sfdc_org_id` | L&#39;ID organizzazione per l&#39;account [!DNL Salesforce]. Per ulteriori informazioni sull&#39;acquisizione dell&#39;ID organizzazione [!DNL Salesforce], consulta la [[!DNL Salesforce] guida](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) seguente. | `00D4W000000FgYJUA0` |
| `has_abm` | Valore booleano che indica se sei abbonato a [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Valore booleano che indica se sei abbonato a [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

### Esecuzione degli script

Dopo aver configurato la raccolta [!DNL Postman] e l&#39;ambiente, è ora possibile eseguire lo script tramite l&#39;interfaccia [!DNL Postman].

Nell&#39;interfaccia [!DNL Postman], selezionare la cartella principale dell&#39;utilità di generazione automatica, quindi selezionare **[!DNL Run]** dall&#39;intestazione superiore.

![cartella-radice](../../images/tutorials/create/salesforce/root-folder.png)

Viene visualizzata l&#39;interfaccia [!DNL Runner]. Da qui, assicurarsi che tutte le caselle di controllo siano selezionate, quindi selezionare **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

In caso di esito positivo, la richiesta crea gli spazi dei nomi e gli schemi B2B in base alle specifiche beta.

## Connetti [!DNL Salesforce] a Platform tramite API

La documentazione seguente fornisce informazioni su come connettere [!DNL Salesforce] a Platform tramite API o tramite l&#39;interfaccia utente:

- [Creare una connessione di base Salesforce utilizzando l’API del servizio Flow](../../tutorials/api/create/crm/salesforce.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine CRM utilizzando l’API del servizio Flusso](../../tutorials/api/collect/crm.md)

## Connetti [!DNL Salesforce] a Platform tramite l&#39;interfaccia utente

- [Creare una connessione sorgente Salesforce nell’interfaccia utente](../../tutorials/ui/create/crm/salesforce.md)
- [Creare un flusso di dati per una connessione CRM nell’interfaccia utente](../../tutorials/ui/dataflow/crm.md)
