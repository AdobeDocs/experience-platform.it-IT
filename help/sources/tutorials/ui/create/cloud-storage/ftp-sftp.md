---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore sorgente FTP o SFTP nell’interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Creare un connettore sorgente FTP o SFTP nell’interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente su base programmata. Questa esercitazione fornisce i passaggi per creare un connettore sorgente FTP o SFTP utilizzando l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione FTP o SFTP valida, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/cloud-storage.md).

### Formati di file supportati

Experience Platform supporta i seguenti formati di file da acquisire da origini esterne:

* Valori separati da delimitatore (DSV): Il supporto per i file di dati formattati DSV è attualmente limitato ai valori separati da virgole (CSV). Il valore delle intestazioni dei campi all&#39;interno dei file formattati DSV deve essere costituito solo da caratteri alfanumerici e caratteri di sottolineatura. In futuro verrà fornito il supporto per la DSV.
* JavaScript Object Notation (JSON): I file di dati formattati JSON devono essere conformi a XDM.
* Parquet Apache: I file di dati in formato parquet devono essere conformi a XDM.

### Raccogli credenziali richieste

Per accedere al server FTP o SFTP sulla piattaforma, è necessario fornire il nome **** host del server, un nome **** utente e una **password**.

## Connessione al server

Con le credenziali del server, puoi seguire i passaggi descritti di seguito per creare una nuova connessione di base in ingresso per collegare il server FTP o SFTP alla piattaforma.

Accedi ad <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi seleziona **Origini** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro delle origini. Nella schermata *Catalogo* sono visualizzate diverse sorgenti con cui è possibile creare connessioni di base in entrata e ogni origine mostra il numero di connessioni di base esistenti ad esse associate.

Nella categoria *Cloud Storage* , selezionate **FTP** o **SFTP** per esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione dell’origine selezionata e delle opzioni per visualizzarne la documentazione o per collegarsi all’origine. Per creare una nuova connessione di base in entrata, fate clic su **Connetti sorgente**.

![](../../../../images/tutorials/create/sftp/sftp_sources_catalog.png)

Nel modulo di input, fornire alla connessione di base un nome, una descrizione facoltativa e le credenziali FTP o SFTP. Infine, fate clic su **Connect** , quindi lasciate che sia possibile stabilire una nuova connessione di base.

![](../../../../images/tutorials/create/sftp/sftp_credentials.png)

Una volta stabilita una connessione di base con il server FTP o SFTP, puoi continuare con la sezione successiva e configurare un flusso di dati per l&#39;importazione di dati in Piattaforma.

## Passaggi successivi

Seguendo questa esercitazione hai stabilito una connessione al server FTP o SFTP. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati nella piattaforma](../../dataflow/cloud-storage.md).
