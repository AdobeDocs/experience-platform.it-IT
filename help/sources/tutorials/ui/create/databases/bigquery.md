---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine Google Big Query nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 75ba0bce7ce070af851bbf7e220dbf08febc4c20
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Creare un connettore di origine Google Big Query nell&#39;interfaccia utente

> [!NOTE]
> Il connettore Google BigQuery è in versione beta. Le funzioni e la documentazione sono soggette a modifiche.

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente su base programmata. Questa esercitazione fornisce i passaggi per la creazione di un connettore sorgente Google Big Query (di seguito &quot;GBQ&quot;) tramite l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione di base GBQ, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per accedere al tuo account GBQ su Piattaforma, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `project` | L&#39;ID progetto del progetto BigQuery predefinito con cui eseguire la query. |
| `clientID` | Il valore ID utilizzato per generare il token di aggiornamento. |
| `clientSecret` | Il valore segreto utilizzato per generare il token di aggiornamento. |
| `refreshToken` | Token di aggiornamento ottenuto da Google utilizzato per autorizzare l&#39;accesso a BigQuery. |

Per ulteriori informazioni su questi valori, consulta [questo documento](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)GBQ.

## Collegamento dell’account GBQ

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti di seguito per creare una nuova connessione di base in entrata per collegare l&#39;account GBQ a Platform.

Accedi ad <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi seleziona **Origini** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro *Origini* . Nella schermata *Catalogo* sono visualizzate diverse sorgenti con cui è possibile creare connessioni di base in entrata e ogni origine mostra il numero di connessioni di base esistenti ad esse associate.

Nella categoria *Database* , selezionate **Google Big Query** per visualizzare una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione della sorgente selezionata e le opzioni per collegarsi alla sorgente o visualizzare la documentazione. Per creare una nuova connessione di base in entrata, selezionate l&#39;origine **** Connect.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

Viene visualizzata la pagina *Connetti a Google Big Query* . In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **Nuovo account**. Nel modulo di input visualizzato, fornite alla connessione di base un nome, una descrizione facoltativa e le credenziali GBQ. Al termine, selezionate **Connect** , quindi concedete un po&#39; di tempo per stabilire la nuova connessione di base.

![](../../../../images/tutorials/create/google-big-query/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account GBQ con cui desiderate connettervi, quindi selezionate **Avanti** per continuare.

![](../../../../images/tutorials/create/google-big-query/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione di base al tuo account GBQ. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati nella piattaforma](../../dataflow/databases.md).