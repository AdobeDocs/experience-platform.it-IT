---
keywords: Experience Platform;home;argomenti popolari;Adobe Experience Platform;guida API;guida API Platform;introduzione alla piattaforma;guida per gli sviluppatori
solution: Experience Platform
title: Guida introduttiva alle API di Adobe Experience Platform
topic-legacy: api guide
description: Adobe Experience Platform fornisce servizi API strettamente collegati tra loro. Questa guida contiene informazioni sui servizi disponibili, sulle intestazioni richieste per le operazioni CRUD, sui messaggi di errore, sulle raccolte Postman e sulle chiamate API di esempio.
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 0%

---

# Guida introduttiva alle API di Adobe Experience Platform

Adobe Experience Platform si sviluppa sotto una filosofia &quot;API first&quot;. Utilizzando le API di Platform, puoi eseguire in modo programmatico operazioni CRUD di base (Crea, Leggi, Aggiorna, Elimina) in base ai dati, come la configurazione di attributi calcolati, l’accesso a dati/entità, l’esportazione di dati, l’eliminazione di dati o batch non necessari e altro ancora.

Le API per ogni servizio Experience Platform condividono tutti lo stesso set di intestazioni di autenticazione e utilizzano sintassi simili per le loro operazioni CRUD. La guida seguente illustra i passaggi necessari per iniziare a utilizzare le API di Platform.

## Autenticazione e intestazioni

Per effettuare correttamente le chiamate agli endpoint di Platform, devi completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API di Experience Platform, come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

### Intestazione Sandbox

Tutte le risorse in Experience Platform sono isolate in sandbox virtuali specifiche. Le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- `x-sandbox-name: {SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in Platform, consulta la documentazione [panoramica sandbox](../sandboxes/home.md).

### Intestazione del tipo di contenuto

Tutte le richieste con un payload nel corpo della richiesta (come le chiamate POST, PUT e PATCH) devono includere un’intestazione `Content-Type`. I valori accettati sono specifici per ogni endpoint API. Se è necessario un valore `Content-Type` specifico per un endpoint, il relativo valore verrà mostrato nelle richieste API di esempio fornite dalle guide API [per i singoli servizi Platform](#api-guides).

## Experience Platform di base API

Le API di Adobe Experience Platform utilizzano diverse tecnologie e sintassi di base importanti per gestire in modo efficace le risorse di Platform.

Per ulteriori informazioni sulle tecnologie API sottostanti che Platform utilizza, inclusi gli oggetti dello schema JSON, visita la guida [Experience Platform API Fondamentals](api-fundamentals.md) .

## Raccolte Postman per API di Experience Platform

Postman è una piattaforma di collaborazione per lo sviluppo API che consente di configurare ambienti con variabili preimpostate, condividere raccolte API, semplificare le richieste CRUD e altro ancora. La maggior parte dei servizi API di Platform dispone di raccolte Postman che possono essere utilizzate per facilitare l’esecuzione di chiamate API.

Per ulteriori informazioni su Postman e su come impostare un ambiente, un elenco delle raccolte disponibili e come importare le raccolte, visita la [documentazione di Platform Postman](postman.md).

## Lettura di chiamate API di esempio {#sample-api}

I formati di richiesta variano a seconda dell’API Platform utilizzata. Il modo migliore per strutturare le chiamate API è seguire gli esempi forniti nella documentazione del particolare servizio Platform che utilizzi.

La documentazione relativa a [!DNL Experience Platform] mostra gli esempi di chiamate API in due modi diversi. Innanzitutto, la chiamata viene presentata nel suo **formato API**, una rappresentazione di modello che mostra solo l’operazione (GET, POST, PUT, PATCH, DELETE) e l’endpoint utilizzato (ad esempio, `/global/classes`). Alcuni modelli mostrano anche la posizione delle variabili per illustrare come deve essere formulata una chiamata , ad esempio `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Le chiamate vengono quindi visualizzate come comandi cURL in una **Richiesta**, che include le intestazioni necessarie e il &quot;percorso base&quot; completo necessario per interagire con successo con l&#39;API. Il percorso di base deve essere pre-apposto a tutti gli endpoint. Ad esempio, il punto finale `/global/classes` sopra indicato diventa `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Vedrai il formato/modello di richiesta API in tutta la documentazione e devi utilizzare il percorso completo mostrato nella richiesta di esempio quando effettui chiamate alle API di Platform.

### Esempio di richiesta API

Di seguito è riportato un esempio di richiesta API che dimostra il formato che verrà mostrato nella documentazione.

**Formato API**

Il formato API mostra l’operazione (GET) e l’endpoint utilizzati. Le variabili sono indicate da parentesi graffe (in questo caso, `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Richiesta**

In questa richiesta di esempio, alle variabili del formato API vengono dati i valori effettivi nel percorso della richiesta. Inoltre, tutte le intestazioni richieste sono mostrate come valori di intestazione di esempio o come variabili in cui devono essere incluse informazioni sensibili (come token di sicurezza e ID di accesso).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta illustra cosa ci si aspetta di ricevere in seguito a una chiamata all’API riuscita, in base alla richiesta inviata. Talvolta la risposta viene troncata per lo spazio, il che significa che è possibile visualizzare ulteriori informazioni o informazioni aggiuntive rispetto a quelle visualizzate nell’esempio.

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

La [Guida alla risoluzione dei problemi della piattaforma](troubleshooting.md#errors-and-troubleshooting) fornisce un elenco di errori che possono verificarsi durante l&#39;utilizzo di un servizio Experience Platform.

Per le guide alla risoluzione dei problemi sui singoli servizi di Platform, consulta la [directory per la risoluzione dei problemi dei servizi](troubleshooting.md#service-troubleshooting-directory).

Per ulteriori informazioni su endpoint specifici nelle API di Platform, comprese le intestazioni e i corpi di richiesta richiesti, consulta le [Guide API della piattaforma](#api-guides).

## Guide API della piattaforma {#api-guides}

| Guida all’API | Descrizione |
| --- | --- |
| [[!DNL Access Control] Guida all’API](.././access-control/api/getting-started.md) | L’endpoint API [!DNL Access Control] può recuperare i criteri correnti applicati da un utente per determinate risorse all’interno di una sandbox specifica. Tutte le altre funzionalità di controllo degli accessi sono disponibili tramite [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [Guida all’API per l’acquisizione in batch](.././ingestion/batch-ingestion/api-overview.md) | L’API Adobe Experience Platform [!DNL Data Ingestion] ti consente di acquisire dati in Platform come file batch. I dati da acquisire possono essere i dati di profilo di un file flat in un sistema CRM (ad esempio un file Parquet) o dati conformi a uno schema noto nel Registro di sistema dello schema (XDM). |
| [[!DNL Catalog Service] Guida all’API](.././catalog/api/getting-started.md) | L’ API [!DNL Catalog Service] consente agli sviluppatori di gestire i metadati del set di dati in Adobe Experience Platform. Ciò include le posizioni dei dati, le fasi di elaborazione, gli errori verificatisi durante l’elaborazione e i rapporti sui dati. |
| [[!DNL Data Access] Guida all’API](.././data-access/api.md) | L’ API [!DNL Data Access] consente agli sviluppatori di recuperare informazioni sui set di dati acquisiti all’interno di Experience Platform. Ciò include l&#39;accesso e il download di file di set di dati, il recupero delle informazioni di intestazione, l&#39;elenco dei batch con errore e con esito positivo e il download di file CSV/parquet di anteprima. |
| [[!DNL Dataset Service] Guida all’API](.././data-governance/labels/dataset-api.md) | L’API del servizio Dataset consente di applicare e modificare le etichette di utilizzo per i set di dati. Fa parte delle funzionalità del catalogo dati di Adobe Experience Platform, ma è separato dall’API del servizio catalogo che gestisce i metadati del set di dati. |
| [[!DNL Flow Service] Guida API](.././sources/tutorials/api/create-dataset-base-connection.md) <br>  (Origini e Destinazioni) | L’ API [!DNL Flow Service] viene utilizzata per raccogliere e centralizzare i dati da varie sorgenti e viene utilizzata per creare e attivare i dati in diverse destinazioni all’interno di Adobe Experience Platform. Il servizio fornisce un’API RESTful da cui è possibile connettere tutte le origini supportate. |
| [[!DNL Identity Service] Guida all’API](.././identity-service/api/getting-started.md) | L’ API [!DNL Identity Service] consente agli sviluppatori di gestire l’identificazione dei clienti tra dispositivi, tra canali e in tempo quasi reale utilizzando grafici di identità in Adobe Experience Platform. |
| [[!DNL Observability Insights] Guida all’API](.././observability/api/overview.md) | [!DNL Observability Insights] è un’API RESTful che consente agli sviluppatori di esporre le metriche di osservabilità chiave in Adobe Experience Platform. Queste metriche forniscono informazioni approfondite sulle statistiche di utilizzo di Platform, sui controlli di integrità per i servizi Platform, sulle tendenze della cronologia e sugli indicatori di prestazioni per varie funzionalità di Platform. |
| [[!DNL Policy Service] Guida API](.././data-governance/api/overview.md) <br>  (governance dei dati) | L’ [!DNL Policy Service] API ti consente di creare e gestire le etichette e i criteri di utilizzo dei dati per determinare quali azioni di marketing possono essere intraprese rispetto ai dati che contengono alcune etichette di utilizzo dei dati. Per applicare etichette ai set di dati e ai campi, consulta la guida [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) |
| [[!DNL Privacy Service] Guida all’API](.././privacy-service/api/getting-started.md) | L’ [!DNL Privacy Service] API consente agli sviluppatori di creare e gestire le richieste dei clienti per accedere o eliminare i propri dati personali tra le applicazioni Experience Cloud, in conformità alle normative sulla privacy legali. |
| [[!DNL Query Service] Guida all’API](.././query-service/api/getting-started.md) | L’ API [!DNL Query Service] consente agli sviluppatori di eseguire query sui dati Adobe Experience Platform utilizzando SQL standard. |
| [[!DNL Real-time Customer Profile] Guida all’API](.././profile/api/overview.md) | L’API Profilo cliente in tempo reale consente agli sviluppatori di esplorare e lavorare con i dati del profilo, inclusa la visualizzazione dei profili, la creazione e l’aggiornamento di criteri di unione, l’esportazione o il campionamento dei dati del profilo e l’eliminazione dei dati del profilo che non sono più necessari o sono stati aggiunti per errore. |
| [Guida all’API per sandbox](.././sandboxes/api/getting-started.md) | L’API Sandbox consente agli sviluppatori di gestire in modo programmatico gli ambienti sandbox virtuali isolati in Adobe Experience Platform. |
| [[!DNL Schema Registry] Guida API](.././xdm/api/overview.md) <br>  (XDM) | L’ API [!DNL Schema Registry] consente agli sviluppatori di gestire in modo programmatico tutti gli schemi e le relative risorse Experience Data Model (XDM) all’interno di Adobe Experience Platform. |
| [[!DNL Segmentation Service] Guida all’API](.././segmentation/api/overview.md) | L’ API [!DNL Segmentation Service] consente agli sviluppatori di gestire in modo programmatico le operazioni di segmentazione in Adobe Experience Platform. Ciò include la creazione di segmenti e la generazione di tipi di pubblico dai dati del profilo cliente in tempo reale. |
| [[!DNL Sensei Machine Learning] Guida API](.././data-science-workspace/api/getting-started.md) <br>  (Data Science Workspace) | L’ API [!DNL Sensei Machine Learning] offre agli scienziati dei dati un meccanismo per organizzare e gestire i servizi di apprendimento automatico (ML) dall’onboarding degli algoritmi, dalla sperimentazione e dalla distribuzione dei servizi. |

Per ulteriori informazioni su endpoint e operazioni specifici disponibili per ogni servizio, consulta la [documentazione di riferimento API](http://www.adobe.com/go/platform-api-reference-en) sull&#39;Adobe I/O.

## Passaggi successivi

Questo documento illustra le intestazioni richieste, le guide disponibili e fornisce un esempio di chiamata API. Ora che disponi dei valori di intestazione necessari per effettuare chiamate API su Adobe Experience Platform, seleziona un endpoint API da esplorare dalla tabella [Guide API della piattaforma](#api-guides).

Per le risposte alle domande frequenti, consulta la [Guida alla risoluzione dei problemi della piattaforma](troubleshooting.md).

Per configurare un ambiente Postman ed esplorare le raccolte Postman disponibili, consulta la [Guida Postman della piattaforma](postman.md).
