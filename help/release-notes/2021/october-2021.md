---
title: Note sulla versione di Adobe Experience Platform di ottobre 2021
description: Note sulla versione di Adobe Experience Platform di ottobre 2021.
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: 2e41a1716e057cd33e4635c11ba9c3cfc185418a
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 28%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 27 ottobre 2021**

## Aggiornamenti di Experience Platform

Aggiornamenti ad Experience Platform.

### Interfaccia utente {#ui}

L’interfaccia utente di è stata aggiornata con le seguenti modifiche:

| Funzione | Descrizione |
| --- | --- |
| Tema scuro | Utilizza l’interruttore per tema scuro per passare da un tema chiaro a uno scuro nell’interfaccia di Experience Platform. Lo switch si trova nel profilo utente sotto il nome utente e l’e-mail. |
| Attiva/disattiva navigazione a sinistra | Utilizza l’interruttore di navigazione migliorato nella parte superiore dell’intestazione dell’applicazione per mostrare o nascondere il menu che mostra le funzionalità di Experience Platform. Il sistema ricorda l&#39;ultima selezione e mostra solo le funzionalità a cui hai accesso. |
| Visibilità degli accessi | La barra di navigazione a sinistra mostra solo le funzioni a cui sei in grado di accedere. Nelle versioni precedenti di Adobe Experience Platform, gli elementi non disponibili erano visibili, anche se non era possibile accedervi. |

Per ulteriori informazioni, consulta la [Guida dell&#39;interfaccia utente di Experience Platform](../../landing/ui-guide.md).

## Aggiornamenti alle funzioni esistenti

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Origini](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Funzione `contains_key` | È stata introdotta la funzione `contains_key`, che consente di verificare se l&#39;oggetto esiste all&#39;interno dell&#39;origine. Questa funzione sostituisce la funzione `is_set`, che ora è obsoleta. |
| Messaggi di errore | I messaggi di errore restituiti dall&#39;endpoint `/mappingSets/preview` nell&#39;API della preparazione dati sono ora coerenti con i messaggi di errore generati durante il runtime. |

Per ulteriori informazioni su questo servizio, consulta la [[!DNL Data Prep] panoramica](../../data-prep/home.md).

### Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi di Experience Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

| Funzione | Descrizione |
| --- | --- |
| [!DNL Amazon S3] miglioramenti all&#39;origine | È ora possibile utilizzare il parametro `s3SessionToken` per connettere l&#39;account [!DNL Amazon S3] ad Experience Platform utilizzando credenziali di sicurezza temporanee. Questo token consente di fornire agli utenti in ambienti non attendibili l&#39;accesso temporaneo a breve termine alle risorse [!DNL Amazon S3]. Per ulteriori informazioni, consulta la [[!DNL Amazon S3] documentazione](../../sources/connectors/cloud-storage/s3.md#prerequisites). |
| [!DNL Generic REST API] (Beta) | È ora possibile creare una connessione di origine [!DNL Generic REST API] utilizzando l&#39;[[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) per portare dati da un&#39;applicazione REST generica ad Experience Platform. Per ulteriori informazioni, vedere [[!DNL Generic REST API] panoramica](../../sources/connectors/protocols/generic-rest.md). |

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md).
