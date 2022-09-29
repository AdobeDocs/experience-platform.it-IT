---
title: Pacchetti del servizio query
description: Il documento seguente illustra i pacchetti di funzionalità e prodotti disponibili per Query Service ed evidenzia le differenze tra query ad hoc e batch.
source-git-commit: 3d2802ff5cdb359b28da23a05d1d6831cc273a52
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 3%

---

# Pacchetti del servizio query

Questo documento delinea i diversi tipi di funzionalità di creazione pacchetti e di esecuzione delle query disponibili in Query Service.

Adobe Experience Platform Query Service può essere diviso in due funzionalità in base ai pattern di query che possono essere eseguiti:

- **Query ad hoc** sono query SQL utilizzate per esplorare i set di dati acquisiti per la verifica, la convalida, la sperimentazione e così via. Queste query non riscrivono i dati nel data lake di Platform.
- **Query batch** sono query SQL utilizzate per eseguire l&#39;elaborazione post-acquisizione dei set di dati acquisiti. Queste query consentono di pulire, modellare, manipolare e arricchire i dati, i cui risultati vengono riscritti nel data lake di Platform. Queste query possono essere pianificate, gestite e monitorate come processi batch.

Le funzionalità di Query Service vengono inserite in un pacchetto con i seguenti prodotti e componenti aggiuntivi:

- **Applicazioni basate su piattaforma** (Real-time Customer Data Platform, Customer Journey Analytics e Adobe Journey Optimizer): L’accesso a Query Service per eseguire query ad hoc viene fornito fin dall’inizio con ogni variante e livello di applicazioni basate su Platform.
- **[!DNL Data Distiller]** (pacchetto aggiuntivo che può essere acquistato con Adobe Real-Time CDP, Customer Journey Analytics e Adobe Journey Optimizer): L’accesso al servizio query per eseguire query batch viene fornito con [!DNL Data Distiller].

La tabella seguente illustra le adesioni chiave del servizio Query in base alla modalità di creazione dei pacchetti:

| Diritto al servizio query | Pacchetto con applicazioni basate su piattaforma | Confezionato con [!DNL Data Distiller] |
|---|---|---|
| Pattern di query supportato | Solo query ad hoc | Query batch |
| Caso d’uso supportato | <ul><li>&#x200B; di esplorazione</li><li>&#x200B; di rilevamento dati</li><li>Convalida dei dati</li><li>Sperimentazione</li></ul> | <ul><li>Pulizia</li><li>Forma</li><li>Manipolazione</li><li>Arricchimento</li></ul> |
| Semantica supportata | <ul><li>Query SELECT</li></ul> | <ul><li>Query CTAS e ITAS</li></ul> |
| Tempo massimo di esecuzione | 10 minuti | 24 ore |
| Metrica della licenza | **Condivisa utente query**: <ul><li>1 utente simultaneo (Real-time CDP, Adobe Journey Optimizer) &#x200B;</li><li>5 utenti simultanei (Customer Journey Analytics) &#x200B;</li></ul> **Condivisa query**: <ul><li>1 query in esecuzione simultanea (tutte le applicazioni) &#x200B;</li></ul> **Aggiuntivo pacchetto aggiuntivo per utenti di query ad hoc** possono essere acquistati per aumentare le adesioni autorizzate alle query ad hoc dei clienti. <ul><li>+5 utenti simultanei aggiuntivi per confezione</li><li>+1 ulteriore query di esecuzione simultanea per pacchetto</li></ul> | **Orari di calcolo**: <ul><li>Variabile (con ambito in base alle adesioni all&#39;applicazione del cliente)</li></ul> **Orari di calcolo** è una misura del tempo impiegato dal motore Query Service per leggere, elaborare e riscrivere i dati nel data lake quando viene eseguita una query batch. |
| Interfaccia di esecuzione query | <ul><li>Interfaccia utente del servizio query</li><li>Interfaccia utente client di terze parti</li><li>[!DNL PostgresSQL] interfaccia utente client</li></ul> | <ul><li>Interfaccia utente query </li><li>Interfaccia utente client di terze parti</li><li>[!DNL PostgresSQL] interfaccia utente client</li><li>API REST</li></ul> |
| Risultati della query restituiti tramite | Interfaccia utente client | Set di dati derivati memorizzato nel data lake |
| Limite risultati | <ul><li>Interfaccia utente query - 100 righe</li><li>Client di terze parti - 50.000</li><li>[!DNL PostgresSQL] client - 50.000</li></ul> | <ul><li>Interfaccia utente della query (nessun limite massimo per le righe)</li><li>Client di terze parti (nessun limite massimo alle righe)</li><li>[!DNL PostgresSQL] client (nessun limite massimo alle righe)</li><li>API REST (nessun limite massimo alle righe)</li></ul> |
| Capacità set di dati di lettura | Sì | Sì |
| Capacità set di dati in scrittura | No | Sì |
| Capacità di programmazione | No | Sì |
| Capacità di monitoraggio | Sì | Sì |
| Capacità di impostazione dell’avviso query | No | Sì |

{style=&quot;table-layout:auto&quot;}

## Controllo degli accessi

Il controllo degli accessi, ad Experience Platform, viene gestito tramite [Adobe Admin Console](https://adminconsole.adobe.com/) in cui i profili di prodotto collegano gli utenti con autorizzazioni e sandbox. Consulta la sezione [panoramica sul controllo degli accessi](../access-control/home.md) per ulteriori informazioni.

Per utilizzare Query Service, la [!DNL Manage Queries] l’autorizzazione deve essere abilitata in Admin Console. Questa autorizzazione consente agli utenti di eseguire query ad hoc e batch. Istruzioni dettagliate per richiedere l’accesso al profilo di prodotto [!DNL Manage Queries] l&#39;autorizzazione è stata descritta nella [gestire le autorizzazioni per un profilo di prodotto](../access-control/ui/permissions.md) e [gestire gli utenti per un profilo di prodotto](../access-control/ui/users.md) documenti.

Dopo aver acquistato [!DNL Data Distiller] add-on, il [!DNL Write Dataset] l&#39;autorizzazione deve essere concessa. Questa autorizzazione consente [!DNL Data Distiller] per eseguire query batch.

La tabella seguente illustra gli effetti della [!DNL Manage Queries] autorizzazione:

| Autorizzazione | Funzione |
|---|---|
| [!DNL Manage Queries] (senza autorizzazione per la scrittura di dati) | Fornisce l&#39;accesso per eseguire query ad hoc |
| [!DNL Manage Queries] (con autorizzazione per la scrittura di dati) | Fornisce l&#39;accesso per eseguire query batch |

{style=&quot;table-layout:auto&quot;}

## Supporto per sandbox

Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform. Ciascuna istanza di Platform supporta più produzioni e sandbox non di produzione, ciascuna mantenendo la propria libreria di risorse di Platform. Le sandbox non di produzione consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sulle sandbox di produzione. Per ulteriori informazioni sulle sandbox, consulta la sezione [panoramica sulle sandbox](../sandboxes/home.md). Tutte le adesioni al servizio query sono condivise tra tutte le sandbox

## Passaggi successivi

Leggendo questo documento, dovresti avere una migliore comprensione dei diversi tipi di packaging e delle diverse funzionalità di esecuzione delle query disponibili in Query Service. Per ulteriori informazioni su Query Service, ad esempio i casi d’uso noti del settore, consulta la [documentazione del caso d’uso](./use-cases/abandoned-browse.md). Per informazioni più generali, visita il [Panoramica del servizio query](./home.md).
