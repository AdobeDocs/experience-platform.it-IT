---
title: Note sulla versione di Adobe Experience Platform - Ottobre 2022
description: Note sulla versione di ottobre 2022 per Adobe Experience Platform.
source-git-commit: e9a7c0561277be21aab1c699a1bc07b793684525
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 8%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 26 ottobre 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Origini](#sources)

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- | 
| Disponibilità beta dell’origine Adobe Workfront | Utilizza la [Origine Adobe Workfront](../../sources/connectors/adobe-applications/workfront.md) per dare Experience Platform ai dati Workfront ed eseguire casi d&#39;uso, ad esempio la combinazione dei record di lavoro con dati di terze parti, l&#39;applicazione di analisi storiche e di serie temporali sui record di lavoro e l&#39;esecuzione di query sui dati di lavoro utilizzando SQL standard. Per ulteriori informazioni, consulta la guida su [creazione di una connessione sorgente Workfront nell’interfaccia utente](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |
| Disponibilità beta dell’origine Oracle Service Cloud | Utilizza l’origine Oracle Service Cloud per acquisire i dati dall’account Oracle Service Cloud all’Experience Platform. Per ulteriori informazioni, consulta la documentazione sul [Origine Oracle Service Cloud](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Per ulteriori informazioni sulle origini, consulta la sezione [panoramica di origini](../../sources/home.md).