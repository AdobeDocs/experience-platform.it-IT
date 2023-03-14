---
title: Note sulla versione di Adobe Experience Platform - Ottobre 2021
description: Note sulla versione di ottobre 2021 per Adobe Experience Platform.
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 7%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 27 ottobre 2021**

## Aggiornamenti di Experience Platform

Aggiornamenti di Experience Platform.

### Interfaccia utente {#ui}

L’interfaccia utente di è stata aggiornata con le seguenti modifiche:

| Funzione | Descrizione |
| --- | --- |
| Tema scuro | Utilizza l’interruttore per tema scuro per passare da un tema chiaro a uno scuro nell’interfaccia di Platform. Lo switch si trova nel profilo utente sotto il nome utente e l’e-mail. |
| Attiva/disattiva navigazione a sinistra | Utilizza l’interruttore di navigazione migliorato nella parte superiore dell’intestazione dell’applicazione per mostrare o nascondere il menu che mostra le funzionalità degli Experienci Platform. Il sistema ricorda l&#39;ultima selezione e mostra solo le funzionalità a cui hai accesso. |
| Visibilità degli accessi | La barra di navigazione a sinistra mostra solo le funzioni a cui sei in grado di accedere. Nelle versioni precedenti di Adobe Experience Platform, gli elementi non disponibili erano visibili, anche se non era possibile accedervi. |

Consulta la [Guida all’interfaccia utente di Platform](../../landing/ui-guide.md) per ulteriori informazioni.

## Aggiornamenti alle funzioni esistenti

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Origini](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Funzione  di `contains_key` | Il `contains_key` è stata introdotta una funzione che consente di verificare se l’oggetto esiste all’interno dell’origine. Questa funzione sostituisce il `is_set` , che ora è obsoleto. |
| Messaggi di errore | Messaggi di errore restituiti da `/mappingSets/preview` L’endpoint nell’API della preparazione dati è ora coerente con i messaggi di errore generati durante il runtime. |

Consulta la [[!DNL Data Prep] panoramica](../../data-prep/home.md) per ulteriori informazioni su questo servizio.

### Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

| Funzione | Descrizione |
| --- | --- |
| [!DNL Amazon S3] miglioramenti all&#39;origine | Ora puoi utilizzare la `s3SessionToken` parametro per collegare il [!DNL Amazon S3] da un account a Platform utilizzando credenziali di sicurezza temporanee. Questo token consente di fornire un accesso temporaneo a breve termine al tuo [!DNL Amazon S3] agli utenti in ambienti non attendibili. Per ulteriori informazioni, consulta la [[!DNL Amazon S3] documentazione](../../sources/connectors/cloud-storage/s3.md#prerequisites) dello strumento. |
| [!DNL Generic REST API] (Beta) | Ora puoi creare una [!DNL Generic REST API] connessione sorgente tramite [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) per portare i dati da un’applicazione REST generica a Platform. Consulta la [[!DNL Generic REST API] panoramica](../../sources/connectors/protocols/generic-rest.md) per ulteriori informazioni. |
| [!DNL Zoho CRM] (Beta) | Ora puoi creare una [!DNL Zoho CRM] connessione sorgente tramite [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) o [interfaccia utente](../../sources/tutorials/ui/create/crm/zoho.md) per importare i dati dal [!DNL Zoho CRM] da un account a Platform. Consulta la [[!DNL Zoho CRM] panoramica](../../sources/connectors/crm/zoho.md) per ulteriori informazioni. |

Per ulteriori informazioni sulle origini, consulta [panoramica sulle origini](../../sources/home.md).
