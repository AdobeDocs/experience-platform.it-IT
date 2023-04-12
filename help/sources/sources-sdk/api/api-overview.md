---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
title: Guida all’API per le sorgenti self-service (SDK per batch)
description: Questo documento fornisce una panoramica del processo di creazione di una nuova origine, inclusi i passaggi su come recuperare, scrivere e inviare una nuova specifica di connessione utilizzando l’API Servizio di flusso.
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Guida all’API per le sorgenti self-service (SDK per batch)

Questo documento fornisce una panoramica del processo di creazione di una nuova origine, inclusi i passaggi su come scrivere e inviare una nuova specifica di connessione utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie sorgenti all’interno di Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful che consente di impostare con facilità le connessioni sorgente a vari provider di dati. Queste connessioni di origine consentono di autenticare i sistemi di terze parti, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

La [!DNL Flow Service] API fornisce diversi endpoint che consentono di gestire in modo programmatico le specifiche di connessione e flusso per una nuova origine che si sta integrando tramite Origini self-service (SDK batch).

## Creare una nuova specifica di connessione

Il primo passaggio nella configurazione di una nuova origine consiste nel creare una nuova specifica di connessione.

Le specifiche di connessione restituiscono le proprietà del connettore di un&#39;origine. Includono specifiche di autenticazione relative alla creazione delle connessioni di base e di origine e un ID di specifica di connessione fisso assegnato a una particolare origine. Le specifiche di connessione sono agnostiche del tenant e dell’organizzazione. Una specifica di connessione tipica contiene informazioni di base su una determinata origine, oltre a tre sezioni distinte: `authSpec`, `sourceSpec`e `exploreSpec`.

Per istruzioni dettagliate, consulta la guida su [creazione di una nuova specifica di connessione](./create.md). Per informazioni sulle proprietà e i valori utilizzati per una specifica di connessione, compresi i dettagli sulla configurazione dell&#39;autenticazione, dell&#39;origine e dell&#39;esplorazione delle specifiche, vedere la [documento sulle opzioni di configurazione](../config/config.md).

## Aggiornare le specifiche di flusso

Una volta creata correttamente una specifica di connessione, è necessario aggiungere la `RestStorageToAEP` specifica di flusso per consentire alla sorgente di creare un flusso di dati.

Le specifiche di flusso contengono informazioni che definiscono un flusso, inclusi gli ID di connessione di origine e di destinazione supportati, le specifiche di trasformazione necessarie per essere applicate ai dati e i parametri di pianificazione necessari per generare un flusso.

Per istruzioni dettagliate, consulta la guida su [aggiornamento delle specifiche di flusso](./update-flow-specs.md).

## Aggiorna le specifiche di connessione

È possibile apportare aggiornamenti alle specifiche di connessione effettuando una richiesta PUT al [!DNL Flow Service] API. Consulta la guida su [aggiornamento delle specifiche di connessione](./update-connection-specs.md) per ulteriori informazioni.

## Invia l&#39;origine

Per inviare ad Experience Platform l&#39;origine per l&#39;integrazione, devi prima completare l&#39;intero [!DNL Flow Service] Flusso di lavoro API per le sorgenti per garantire il corretto funzionamento della sorgente. Se l&#39;origine viene eseguita correttamente, è possibile procedere e contattare il proprio rappresentante Adobe per la verifica e la promozione. Consulta la guida su [verifica e invio della sorgente](./submit.md) per ulteriori informazioni

## Passaggi successivi

Per iniziare a utilizzare [!DNL Flow Service] API e crea una nuova origine tramite Origini self-service (SDK batch), leggi il [guida introduttiva](./getting-started.md) quindi seleziona una delle guide dell’endpoint per scoprire come utilizzare endpoint specifici.
