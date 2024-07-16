---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;sorgente connettori;sorgenti sdk;sdk;SDK
title: Guida API per le origini self-service (SDK Batch)
description: Questo documento fornisce una panoramica del processo di creazione di una nuova origine, inclusi i passaggi su come recuperare, scrivere e inviare una nuova specifica di connessione utilizzando l’API del servizio Flusso.
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Guida API per le origini self-service (SDK Batch)

Questo documento fornisce una panoramica del processo di creazione di una nuova origine, inclusi i passaggi su come scrivere e inviare una nuova specifica di connessione utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da diverse origini in Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful che consentono di impostare facilmente le connessioni sorgente a vari provider di dati. Queste connessioni di origine ti consentono di autenticare i sistemi di terze parti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

L&#39;API [!DNL Flow Service] fornisce diversi endpoint che consentono di gestire in modo programmatico le specifiche di connessione e flusso per una nuova origine che si sta integrando tramite Self-Service Sources (Batch SDK).

## Crea una nuova specifica di connessione

Il primo passaggio nella configurazione di una nuova origine consiste nel creare una nuova specifica di connessione.

Le specifiche di connessione restituiscono le proprietà del connettore di un&#39;origine. Includono specifiche di autenticazione relative alla creazione delle connessioni di base e di origine e un ID di specifica di connessione fisso assegnato a una determinata origine. Le specifiche di connessione sono indipendenti dal tenant e dall’organizzazione. Una specifica di connessione tipica contiene informazioni di base su una determinata origine e tre sezioni distinte: `authSpec`, `sourceSpec` e `exploreSpec`.

Per istruzioni dettagliate, consulta la guida su [creazione di una nuova specifica di connessione](./create.md). Per informazioni sulle proprietà e i valori utilizzati per una specifica di connessione, inclusi i dettagli sulla configurazione dell&#39;autenticazione, le specifiche di origine ed esplorazione, vedere il [documento sulle opzioni di configurazione](../config/config.md).

## Aggiorna specifiche di flusso

Dopo aver creato correttamente una specifica di connessione, è necessario aggiungere la specifica di flusso `RestStorageToAEP` per consentire all&#39;origine di creare un flusso di dati.

Le specifiche di flusso contengono informazioni che definiscono un flusso, inclusi gli ID di connessione di origine e di destinazione supportati, le specifiche di trasformazione da applicare ai dati e i parametri di programmazione necessari per generare un flusso.

Per istruzioni dettagliate, vedere la guida all&#39;aggiornamento delle [specifiche di flusso](./update-flow-specs.md).

## Aggiornare le specifiche di connessione

È possibile aggiornare le specifiche di connessione effettuando una richiesta PUT all&#39;API [!DNL Flow Service]. Per ulteriori informazioni, consulta la guida sull&#39;[aggiornamento delle specifiche di connessione](./update-connection-specs.md).

## Invia l&#39;origine

Per inviare ad Experience Platform l&#39;origine per l&#39;integrazione, è necessario prima completare l&#39;intero flusso di lavoro API [!DNL Flow Service] per le origini per garantire il corretto funzionamento dell&#39;origine. Se l’origine viene eseguita correttamente, puoi procedere e contattare il rappresentante dell’Adobe per la verifica e la promozione. Per ulteriori informazioni, consulta la guida su [verifica e invio dell&#39;origine](./submit.md)

## Passaggi successivi

Per iniziare a utilizzare l&#39;API [!DNL Flow Service] e creare una nuova origine tramite Self-Serve Sources (Batch SDK), leggere la [guida introduttiva](./getting-started.md), quindi selezionare una delle guide degli endpoint per informazioni su come utilizzare endpoint specifici.
