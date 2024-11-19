---
keywords: Experience Platform;home;argomenti popolari;Adobe Experience Platform;guida api;guida api piattaforma;introduzione a piattaforma;guida per sviluppatori
solution: Experience Platform
title: Guida introduttiva alle API di Adobe Experience Platform
description: Adobe Experience Platform fornisce servizi API strettamente collegati tra loro. Questa guida contiene informazioni sui servizi disponibili, le intestazioni richieste per le operazioni CRUD, i messaggi di errore, le raccolte Postman e le chiamate API di esempio.
role: Developer
feature: API
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 0%

---

# Guida introduttiva alle API di Adobe Experience Platform

Adobe Experience Platform è sviluppato secondo la filosofia &quot;API first&quot;. Utilizzando le API di Platform, puoi eseguire in modo programmatico operazioni CRUD di base (Crea, Leggi, Aggiorna, Elimina) sui dati, ad esempio la configurazione di attributi calcolati, l’accesso a dati/entità, l’esportazione di dati, l’eliminazione di dati o batch non necessari e altro ancora.

Le API di ciascun servizio Experience Platform condividono tutte lo stesso set di intestazioni di autenticazione e utilizzano sintassi simili per le operazioni CRUD. La guida seguente illustra i passaggi necessari per iniziare a utilizzare le API di Platform.

## Autenticazione e intestazioni

Per effettuare correttamente le chiamate agli endpoint di Platform, è necessario completare l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API di Experience Platform, come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### Intestazione sandbox

Tutte le risorse in Experience Platform sono isolate in specifiche sandbox virtuali. Le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- `x-sandbox-name: {SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in Platform, consulta la [documentazione di panoramica sulle sandbox](../sandboxes/home.md).

### Intestazione content-type

Tutte le richieste con un payload nel corpo della richiesta (ad esempio chiamate POST, PUT e PATCH) devono includere un&#39;intestazione `Content-Type`. I valori accettati sono specifici per ogni endpoint API. Se è necessario un valore `Content-Type` specifico per un endpoint, il relativo valore verrà visualizzato nelle richieste API di esempio fornite dalle [guide API per i singoli servizi Platform](#api-guides).

## Nozioni di base sulle API di Experience Platform

Le API di Adobe Experience Platform utilizzano diverse tecnologie e sintassi di base importanti da comprendere per gestire in modo efficace le risorse di Platform.

Per ulteriori informazioni sulle tecnologie API di base utilizzate da Platform, inclusi gli oggetti schema JSON di esempio, visita la [guida Experience Platform API Fundals](api-fundamentals.md).

## Raccolte Postman, ad Experience Platform API

Postman è una piattaforma di collaborazione per lo sviluppo di API che consente di configurare ambienti con variabili preimpostate, condividere raccolte API, semplificare le richieste CRUD e altro ancora. La maggior parte dei servizi API di Platform dispone di raccolte Postman che possono essere utilizzate per facilitare l’esecuzione di chiamate API.

Per ulteriori informazioni su Postman, tra cui la configurazione di un ambiente, un elenco delle raccolte disponibili e le modalità di importazione delle raccolte, visita la [documentazione di Platform Postman](postman.md).

## Lettura delle chiamate API di esempio {#sample-api}

I formati delle richieste variano a seconda dell’API della piattaforma in uso. Il modo migliore per imparare a strutturare le chiamate API è seguire gli esempi forniti nella documentazione del particolare servizio Platform che stai utilizzando.

La documentazione di [!DNL Experience Platform] mostra le chiamate API di esempio in due modi diversi. Innanzitutto, la chiamata viene presentata nel suo formato **API**, una rappresentazione di modello che mostra solo l&#39;operazione (GET, POST, PUT, PATCH, DELETE) e l&#39;endpoint utilizzato (ad esempio, `/global/classes`). Alcuni modelli mostrano anche la posizione delle variabili per illustrare come deve essere formulata una chiamata, ad esempio `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Le chiamate vengono quindi visualizzate come comandi cURL in una **Richiesta**, che include le intestazioni necessarie e il &quot;percorso base&quot; completo necessario per interagire correttamente con l&#39;API. Il percorso di base deve essere preaperto a tutti gli endpoint. Ad esempio, l&#39;endpoint `/global/classes` sopra indicato diventa `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Vedrai il formato/modello di richiesta API in tutta la documentazione e, quando effettuerai chiamate alle API di Platform, è previsto l’utilizzo del percorso completo mostrato nella richiesta di esempio.

### Esempio di richiesta API

Di seguito è riportato un esempio di richiesta API che dimostra il formato che incontrerai nella documentazione.

**Formato API**

Il formato API mostra l’operazione (GET) e l’endpoint utilizzati. Le variabili sono indicate da parentesi graffe (in questo caso, `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Richiesta**

In questo esempio di richiesta, alle variabili del formato API vengono assegnati valori effettivi nel percorso della richiesta. Inoltre, tutte le intestazioni richieste vengono visualizzate come valori di intestazione di esempio o come variabili in cui devono essere incluse informazioni sensibili (come token di sicurezza e ID di accesso).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta illustra cosa ci si aspetta di ricevere in seguito a una chiamata all’API con esito positivo, in base alla richiesta inviata. A volte la risposta viene troncata per motivi di spazio, il che significa che è possibile visualizzare ulteriori informazioni o informazioni aggiuntive rispetto a quelle visualizzate nell’esempio.

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

## Messaggi di errore

La [Guida alla risoluzione dei problemi di Platform](troubleshooting.md#errors-and-troubleshooting) fornisce un elenco di errori che possono verificarsi quando si utilizza un servizio Experience Platform.

Per le guide alla risoluzione dei problemi sui singoli servizi Platform, vedere la [directory per la risoluzione dei problemi dei servizi](troubleshooting.md#service-troubleshooting-directory).

Per ulteriori informazioni su endpoint specifici nelle API di Platform, incluse le intestazioni richieste e i corpi delle richieste, consulta le [guide API di Platform](#api-guides).

## Guide API di Platform {#api-guides}

| Guida API | Descrizione |
| --- | --- |
| [[!DNL Access Control] Guida API](.././access-control/api/getting-started.md) | L&#39;endpoint API [!DNL Access Control] può recuperare i criteri correnti in vigore per un utente su determinate risorse all&#39;interno di una sandbox specificata. Tutte le altre funzionalità di controllo degli accessi vengono fornite tramite [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [Guida API per l&#39;acquisizione in batch](.././ingestion/batch-ingestion/api-overview.md) | L&#39;API [!DNL Data Ingestion] di Adobe Experience Platform consente di acquisire dati in Platform come file batch. I dati da acquisire possono essere i dati di profilo provenienti da un file flat in un sistema di gestione delle relazioni con i clienti (ad esempio un file Parquet) o i dati conformi a uno schema noto nel registro dello schema (XDM). |
| [[!DNL Catalog Service] Guida API](.././catalog/api/getting-started.md) | L&#39;API [!DNL Catalog Service] consente agli sviluppatori di gestire i metadati del set di dati in Adobe Experience Platform. Ciò include le posizioni dei dati, le fasi di elaborazione, gli errori che si sono verificati durante l’elaborazione e i rapporti sui dati. |
| [[!DNL Data Access] Guida API](.././data-access/api.md) | L&#39;API [!DNL Data Access] consente agli sviluppatori di recuperare informazioni sui set di dati acquisiti in Experience Platform. Ciò include l’accesso e il download di file di set di dati, il recupero di informazioni sull’intestazione, l’elenco dei batch con errori e di quelli riusciti e il download di file CSV/Parquet di anteprima. |
| [[!DNL Dataset Service] Guida API](.././data-governance/labels/dataset-api.md) | L’API Servizio set di dati consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separata dall’API Catalog Service che gestisce i metadati dei set di dati. |
| [[!DNL Data Hygiene API guide]](../hygiene/api/overview.md) | L&#39;API [!DNL Data Hygiene] consente di correggere o eliminare in modo programmatico i dati personali archiviati dei clienti in Adobe Experience Platform, nonché di pianificare le date di scadenza per i set di dati. |
| [[!DNL Edge Network Server] Guida API](../server-api/overview.md) | [!DNL Edge Network Server API] può essere utilizzato per diversi casi di utilizzo di raccolta dati, personalizzazione, pubblicità e marketing. [!DNL Server API] può essere utilizzato su server, dispositivi [!DNL IoT], set-top box e molti altri dispositivi. |
| [[!DNL Identity Service] Guida API](.././identity-service/api/getting-started.md) | L&#39;API [!DNL Identity Service] consente agli sviluppatori di gestire l&#39;identificazione dei clienti in tempo reale, tra dispositivi e canali diversi, utilizzando grafici di identità in Adobe Experience Platform. |
| [[!DNL MTLS Service API guide]](../data-governance/mtls-api/overview.md) | L&#39;API [!DNL MTLS Service] ti consente di recuperare in modo sicuro i certificati pubblici rilasciati da Adobe per la tua organizzazione. |
| [[!DNL Observability Insights] Guida API](.././observability/api/overview.md) | [!DNL Observability Insights] è un&#39;API RESTful che consente agli sviluppatori di esporre metriche chiave di osservabilità in Adobe Experience Platform. Queste metriche forniscono informazioni approfondite sulle statistiche di utilizzo di Platform, sui controlli di integrità per i servizi di Platform, sulle tendenze storiche e sugli indicatori di prestazioni per le varie funzionalità di Platform. |
| [[!DNL Policy Service] Guida API](.././data-governance/api/overview.md) <br> (governance dei dati) | L&#39;API [!DNL Policy Service] consente di creare e gestire etichette e criteri di utilizzo dei dati per determinare quali azioni di marketing possono essere eseguite sui dati che contengono determinate etichette di utilizzo dei dati. Per applicare etichette ai set di dati e ai campi, consulta la guida [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) |
| [[!DNL Privacy Service] Guida API](.././privacy-service/api/getting-started.md) | L&#39;API [!DNL Privacy Service] consente agli sviluppatori di creare e gestire le richieste dei clienti di accedere o eliminare i propri dati personali nelle applicazioni Experience Cloud, in conformità con le normative legali sulla privacy. |
| [[!DNL Query Service] Guida API](.././query-service/api/getting-started.md) | L&#39;API [!DNL Query Service] consente agli sviluppatori di eseguire query sui dati Adobe Experience Platform utilizzando SQL standard. |
| [[!DNL Real-Time Customer Profile] Guida API](.././profile/api/overview.md) | L’API Profilo cliente in tempo reale consente agli sviluppatori di esplorare e utilizzare i dati del profilo, tra cui la visualizzazione dei profili, la creazione e l’aggiornamento dei criteri di unione, l’esportazione o il campionamento dei dati del profilo e l’eliminazione dei dati del profilo che non sono più necessari o che sono stati aggiunti per errore. |
| [Guida alle API Sandbox](.././sandboxes/api/getting-started.md) | L’API Sandbox consente agli sviluppatori di gestire in modo programmatico gli ambienti sandbox virtuali isolati in Adobe Experience Platform. |
| [[!DNL Schema Registry] Guida API](.././xdm/api/overview.md) <br> (XDM) | L&#39;API [!DNL Schema Registry] consente agli sviluppatori di gestire in modo programmatico tutti gli schemi e le relative risorse Experience Data Model (XDM) in Adobe Experience Platform. |
| [[!DNL Segmentation Service] Guida API](.././segmentation/api/overview.md) | L&#39;API [!DNL Segmentation Service] consente agli sviluppatori di gestire programmaticamente le operazioni di segmentazione in Adobe Experience Platform. Ciò include la creazione di segmenti e la generazione di tipi di pubblico dai dati dei profili cliente in tempo reale. |
| [[!DNL Sensei Machine Learning] Guida API](.././data-science-workspace/api/getting-started.md) <br> (Data Science Workspace) | L&#39;API [!DNL Sensei Machine Learning] fornisce un meccanismo che consente ai data scientist di organizzare e gestire i servizi di machine learning (ML) dall&#39;onboarding degli algoritmi, alla sperimentazione e alla distribuzione dei servizi. |

Per ulteriori informazioni su endpoint e operazioni specifici disponibili per ciascun servizio, consulta la [documentazione di riferimento API](https://www.adobe.com/go/platform-api-reference-en) sull&#39;Adobe I/O.

## Passaggi successivi

Questo documento presenta le intestazioni richieste, le guide disponibili e fornisce un esempio di chiamata API. Ora che disponi dei valori di intestazione necessari per effettuare chiamate API su Adobe Experience Platform, seleziona un endpoint API da esplorare dalla tabella [Guide API di Platform](#api-guides).

Per le risposte alle domande frequenti, fare riferimento alla [Guida alla risoluzione dei problemi di Platform](troubleshooting.md).

Per configurare un ambiente Postman ed esplorare le raccolte Postman disponibili, fare riferimento alla [guida di Platform Postman](postman.md).
