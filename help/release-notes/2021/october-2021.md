---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
source-git-commit: 0c507a26f551af1eb17889e8e77a036e3c106240
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 14%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 27 ottobre 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Origini](#sources)

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| --- | --- |
| [!DNL Amazon S3] miglioramenti alla sorgente | Ora puoi utilizzare la `s3SessionToken` per collegare il [!DNL Amazon S3] su Platform utilizzando credenziali di sicurezza temporanee. Questo token ti consente di fornire accesso temporaneo e a breve termine al tuo [!DNL Amazon S3] risorse per gli utenti in ambienti non attendibili. Consulta la sezione [[!DNL Amazon S3] documentazione](../../sources/connectors/cloud-storage/s3.md#prerequisites) per ulteriori informazioni. |
| [!DNL Generic REST API] (Beta) | Ora puoi creare una [!DNL Generic REST API] connessione di origine tramite [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) o [interfaccia utente](../../sources/tutorials/ui/create/protocols/generic-rest.md) per trasferire dati da un’applicazione REST generica a Platform. Consulta la sezione [[!DNL Generic REST API] panoramica](../../sources/connectors/protocols/generic-rest.md) per ulteriori informazioni. |
| [!DNL Zoho CRM] (Beta) | Ora puoi creare una [!DNL Zoho CRM] connessione di origine tramite [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) o [interfaccia utente](../../sources/tutorials/ui/create/crm/zoho.md) per ottenere i dati dal [!DNL Zoho CRM] a Platform. Consulta la sezione [[!DNL Zoho CRM] panoramica](../../sources/connectors/crm/zoho.md) per ulteriori informazioni. |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
