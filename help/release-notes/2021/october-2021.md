---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
source-git-commit: da9204f1581832d6885acd64387cf7e83c4b012a
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 9%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 27 ottobre 2021**

## Aggiornamenti ad Experience Platform

Aggiornamenti ad Experience Platform.

### Interfaccia utente {#ui}

L’interfaccia utente è stata aggiornata con le seguenti modifiche:

| Funzione | Descrizione |
| --- | --- |
| Tema scuro | Utilizza lo switch Tema scuro per alternare tra temi chiari e scuri nell’interfaccia di Platform. Lo switch si trova nel profilo utente sotto nome utente ed e-mail. |
| Attiva/disattiva la navigazione a sinistra | Utilizza l’interruttore di navigazione migliorato nella parte superiore dell’intestazione dell’applicazione per mostrare o nascondere il menu che mostra le funzionalità dell’Experience Platform. Il sistema ricorda l’ultima selezione e mostra solo le funzionalità a cui hai accesso. |
| Visibilità degli accessi | La barra di navigazione a sinistra mostra solo le funzioni accessibili. Nelle versioni precedenti di Adobe Experience Platform, gli elementi non disponibili erano visibili, anche se non era possibile accedervi. |

Consulta la sezione [Guida all’interfaccia utente di Platform](../../landing/ui-guide.md) per saperne di più.

## Aggiornamenti alle funzioni esistenti

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Origini](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Funzione  di `contains_key` | La `contains_key` è stata introdotta una funzione che consente di verificare se l&#39;oggetto esiste all&#39;interno dell&#39;origine. Questa funzione sostituisce la `is_set` , che è ora obsoleto. |
| Messaggi di errore | Messaggi di errore restituiti da `/mappingSets/preview` L’endpoint nell’API di preparazione dati ora è coerente con i messaggi di errore generati durante il runtime. |

Consulta la sezione [[!DNL Data Prep] panoramica](../../data-prep/home.md) per ulteriori informazioni su questo servizio.

### Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| --- | --- |
| [!DNL Amazon S3] miglioramenti alla sorgente | Ora puoi utilizzare la `s3SessionToken` per collegare il [!DNL Amazon S3] su Platform utilizzando credenziali di sicurezza temporanee. Questo token ti consente di fornire accesso temporaneo e a breve termine al tuo [!DNL Amazon S3] risorse per gli utenti in ambienti non attendibili. Consulta la sezione [[!DNL Amazon S3] documentazione](../../sources/connectors/cloud-storage/s3.md#prerequisites) per ulteriori informazioni. |
| [!DNL Generic REST API] (Beta) | Ora puoi creare una [!DNL Generic REST API] connessione di origine tramite [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) per trasferire dati da un’applicazione REST generica a Platform. Consulta la sezione [[!DNL Generic REST API] panoramica](../../sources/connectors/protocols/generic-rest.md) per ulteriori informazioni. |
| [!DNL Zoho CRM] (Beta) | Ora puoi creare una [!DNL Zoho CRM] connessione di origine tramite [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) o [interfaccia utente](../../sources/tutorials/ui/create/crm/zoho.md) per ottenere i dati dal [!DNL Zoho CRM] a Platform. Consulta la sezione [[!DNL Zoho CRM] panoramica](../../sources/connectors/crm/zoho.md) per ulteriori informazioni. |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).