---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine di archiviazione Google Cloud nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Creare un connettore di origine di archiviazione Google Cloud nell&#39;interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente su base programmata. Questa esercitazione fornisce i passaggi per la creazione di un connettore sorgente Google Cloud Storage (in seguito denominato &quot;GCS&quot;) tramite l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione di base GCS, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/cloud-storage.md).

### Formati di file supportati

Experience Platform supporta i seguenti formati di file da acquisire da archivi esterni:

* Valori separati da delimitatore (DSV): Il supporto per i file di dati in formato DSV è attualmente limitato ai valori separati da virgole. Il valore delle intestazioni dei campi all&#39;interno dei file formattati DSV deve essere costituito solo da caratteri alfanumerici e caratteri di sottolineatura. In futuro verrà fornito il supporto per i file DSV generali.
* JavaScript Object Notation (JSON): I file di dati formattati JSON devono essere conformi a XDM.
* Parquet Apache: I file di dati in formato parquet devono essere conformi a XDM.

### Raccogli credenziali richieste

Per accedere ai dati GCS sulla piattaforma, è necessario fornire un ID **chiave di** accesso GCS valido e un **Segreto**. Per ulteriori informazioni su come ottenere questi valori, consulta la guida <a href="https://cloud.google.com/docs/authentication/production" target="_blank">all’autenticazione da</a> server a server per Google Cloud.

## Collegamento dell&#39;account GCS

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti di seguito per creare una nuova connessione di base in entrata per collegare l&#39;account GCS alla piattaforma.

Accedi ad <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi seleziona **Origini** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro *Origini* . Nella schermata *Catalogo* sono visualizzate diverse sorgenti con cui è possibile creare connessioni di base in entrata e ogni origine mostra il numero di connessioni di base esistenti ad esse associate.

Nella categoria *Cloud Storage* , selezionate **Google Cloud Storage** per esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione dell’origine selezionata e le opzioni per connettersi alla relativa documentazione o per connettersi all’origine. Per creare una nuova connessione di base in entrata, fate clic su **Connetti sorgente**.

![](../../../../images/tutorials/create/google-cloud-storage/sources-catalog.png)

Viene visualizzata la finestra di dialogo _Connetti a Google Cloud Storage_ . Nel modulo di input, fornite alla connessione di base un nome, una descrizione facoltativa e le credenziali GCS. Al termine, fate clic su **Connect** , quindi consentite un po&#39; di tempo per l&#39;impostazione della nuova connessione di base.

![](../../../../images/tutorials/create/google-cloud-storage/gcs-credentials.png)

Una volta stabilita la connessione di base, puoi continuare con la sezione successiva e configurare un flusso di dati per l&#39;inserimento di dati in Platform.

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione di base al tuo account GCS. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati nella piattaforma](../../dataflow/cloud-storage.md).