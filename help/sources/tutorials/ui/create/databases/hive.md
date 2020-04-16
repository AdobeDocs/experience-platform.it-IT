---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un Apache Hive sul connettore di origine Azure HDInsights nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 9bc9e369c7141ab70d7f7e6deffe9e0ad92ca92e

---


# Creare un Apache Hive sul connettore di origine Azure HDInsights nell&#39;interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente su base programmata. Questa esercitazione fornisce i passaggi per creare un Apache Hive sul connettore di origine Azure HDInsights utilizzando l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione Hive valida, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/databases.md)

### Raccogli credenziali richieste

Per accedere al tuo account Hive sulla piattaforma, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Indirizzo IP o nome host del server Hive. |
| `username` | Il nome utente utilizzato per accedere al server Hive. |
| `password` | La password che corrisponde all&#39;utente. |

Per ulteriori informazioni su come iniziare, consulta [questo documento](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted)Hive.

## Collegamento dell&#39;account Hive

Dopo aver raccolto le credenziali necessarie, puoi seguire i passaggi descritti di seguito per creare un nuovo account Hive per la connessione alla piattaforma.

Accedi ad <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi seleziona **Origini** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro *Origini* . Nella schermata *Catalogo* sono visualizzate una varietà di origini per le quali è possibile creare un account in ingresso. Ogni origine mostra il numero di account e flussi di dati esistenti associati a tali account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Nella categoria *Database* , selezionare **Hive** per visualizzare una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione della sorgente selezionata e le opzioni per collegarsi alla sorgente o visualizzare la documentazione. Per creare una nuova connessione in entrata, selezionate **Connetti sorgente**.

![catalogo](../../../../images/tutorials/create/hive/catalog.png)

Viene visualizzata la pagina *Connetti a Hive* . In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **Nuovo account**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali Hive per la connessione. Al termine, selezionate **Connect** , quindi concedete un po&#39; di tempo per la creazione del nuovo account.

![connect](../../../../images/tutorials/create/hive/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account Hive con cui desiderate connettervi, quindi selezionate **Avanti** per continuare.

![esistenti](../../../../images/tutorials/create/hive/existing.png)

## Passaggi successivi

Seguendo questa esercitazione hai stabilito una connessione con il tuo account Hive. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati nella piattaforma](../../dataflow/databases.md).