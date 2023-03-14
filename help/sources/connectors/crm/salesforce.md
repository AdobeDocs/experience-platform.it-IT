---
keywords: Experience Platform;home;argomenti comuni;schema crm;CRM;salesforce;Salesforce;crm;CRM;home;popular topic;crm schema;CRM;salesforce;Salesforce
solution: Experience Platform
title: Panoramica del connettore di origine Salesforce
description: Scopri come collegare Salesforce a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 0%

---

# [!DNL Salesforce] connettore

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un sistema CRM di terze parti. Il supporto per i provider CRM include [!DNL Salesforce].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Consulta la [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Mappatura campi da [!DNL Salesforce] a XDM

Per stabilire una connessione di origine tra [!DNL Salesforce] e Platform, [!DNL Salesforce] i campi dati di origine devono essere mappati sui campi XDM di destinazione appropriati prima di essere acquisiti in Platform.

Per informazioni dettagliate sulle regole di mappatura dei campi tra [!DNL Salesforce] Set di dati e Platform:

- [Contatti](../adobe-applications/mapping/salesforce.md#contact)
- [Lead](../adobe-applications/mapping/salesforce.md#lead)
- [Account](../adobe-applications/mapping/salesforce.md#account)
- [Opportunità](../adobe-applications/mapping/salesforce.md#opportunity)
- [Ruoli di contatto opportunità](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campagne](../adobe-applications/mapping/salesforce.md#campaign)
- [Membri della campagna](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Relazione contatto account](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## Configurare [!DNL Salesforce] utilità di generazione automatica dello spazio dei nomi e dello schema

Per utilizzare [!DNL Salesforce] origine come parte di [!DNL B2B-CDP], devi prima impostare un [!DNL Postman] per generare automaticamente [!DNL Salesforce] spazi dei nomi e schemi. La seguente documentazione fornisce informazioni aggiuntive sulla configurazione di [!DNL Postman] utilità:

- È possibile scaricare la raccolta di utilità di generazione automatica dello spazio dei nomi e dello schema e l&#39;ambiente da questo [Archivio GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Per informazioni sull’utilizzo delle API di Platform, compresi i dettagli su come raccogliere i valori per le intestazioni richieste e leggere le chiamate API di esempio, consulta la guida su [introduzione alle API di Platform](../../../landing/api-guide.md).
- Per informazioni su come generare le credenziali per le API di Platform, consulta l’esercitazione su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md).
- Per informazioni su come impostare [!DNL Postman] per le API di Platform, consulta l’esercitazione su [configurazione della console per sviluppatori e [!DNL Postman]](../../../landing/postman.md).

Con una console per sviluppatori di Platform e [!DNL Postman] , è ora possibile iniziare ad applicare i valori di ambiente appropriati al [!DNL Postman] ambiente.

La tabella seguente contiene valori di esempio e informazioni aggiuntive sulla compilazione del [!DNL Postman] ambiente:

| Variable | Descrizione | Esempio |
| --- | --- | --- |
| `CLIENT_SECRET` | Un identificatore univoco utilizzato per generare il `{ACCESS_TOKEN}`. Guarda il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md) per informazioni su come recuperare `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Il JSON Web Token (JWT) è una credenziale di autenticazione utilizzata per generare il {ACCESS_TOKEN}. Guarda il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md) per informazioni su come generare `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Identificatore univoco utilizzato per autenticare le chiamate alle API Experience Platform. Guarda il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md) per informazioni su come recuperare `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Il token di autorizzazione necessario per completare le chiamate alle API Experience Platform. Guarda il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md) per informazioni su come recuperare `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Riguardo a [!DNL Marketo], questo valore è fisso ed è sempre impostato su: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Il `global` contenitore contiene tutte le classi, i gruppi di campi di schema, i tipi di dati e gli schemi standard forniti dal partner Adobe e Experience Platform. Riguardo a [!DNL Marketo], questo valore è fisso ed è sempre impostato su `global`. | `global` |
| `PRIVATE_KEY` | Una credenziale utilizzata per autenticare [!DNL Postman] per Experience Platform le API. Consulta il tutorial sulla configurazione di Developer Console e [configurazione della console per sviluppatori e [!DNL Postman]](../../../landing/postman.md) per istruzioni su come recuperare {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Credenziali utilizzate per l&#39;integrazione in Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management System (IMS) fornisce il framework per l’autenticazione nei servizi Adobe. Riguardo a [!DNL Marketo], questo valore è fisso ed è sempre impostato su: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Entità aziendale che può possedere o concedere in licenza prodotti e servizi e consentire l&#39;accesso ai propri membri. Guarda il tutorial su [configurazione della console per sviluppatori e [!DNL Postman]](../../../landing/postman.md) per istruzioni su come recuperare `{ORG_ID}` informazioni. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nome della partizione sandbox virtuale in uso. | `prod` |
| `TENANT_ID` | ID utilizzato per garantire che le risorse create abbiano lo spazio dei nomi corretto e siano contenute all’interno dell’organizzazione IMS. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | L’endpoint URL a cui stai effettuando chiamate API. Questo valore è fisso ed è sempre impostato su: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | L’ID univoco per il tuo [!DNL Marketo] account. Guarda il tutorial su [autenticazione del [!DNL Marketo] istanza](../adobe-applications/marketo/marketo-auth.md) per informazioni su come recuperare `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | L’ID organizzazione per il tuo [!DNL Salesforce] account. Vedi quanto segue [[!DNL Salesforce] guida](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) per ulteriori informazioni sull’acquisizione di [!DNL Salesforce] ID organizzazione. | `00D4W000000FgYJUA0` |
| `has_abm` | Valore booleano che indica se sei abbonato a [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Valore booleano che indica se sei abbonato a [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

### Esecuzione degli script

Con [!DNL Postman] e dell&#39;ambiente, è ora possibile eseguire lo script tramite il [!DNL Postman] di rete.

In [!DNL Postman] selezionare la cartella principale dell&#39;utilità di generazione automatica, quindi selezionare **[!DNL Run]** dall’intestazione in alto.

![root-folder](../../images/tutorials/create/salesforce/root-folder.png)

Il [!DNL Runner] viene visualizzata l&#39;interfaccia. Da qui, accertati che tutte le caselle di controllo siano selezionate, quindi seleziona **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

In caso di esito positivo, la richiesta crea gli spazi dei nomi e gli schemi B2B in base alle specifiche beta.

## Connetti [!DNL Salesforce] alla piattaforma utilizzando le API

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL Salesforce] in Platform tramite API o l’interfaccia utente:

- [Creare una connessione di base Salesforce utilizzando l’API del servizio Flow](../../tutorials/api/create/crm/salesforce.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine CRM utilizzando l’API del servizio Flusso](../../tutorials/api/collect/crm.md)

## Connetti [!DNL Salesforce] a Platform tramite l’interfaccia utente

- [Creare una connessione sorgente Salesforce nell’interfaccia utente](../../tutorials/ui/create/crm/salesforce.md)
- [Creare un flusso di dati per una connessione CRM nell’interfaccia utente](../../tutorials/ui/dataflow/crm.md)
