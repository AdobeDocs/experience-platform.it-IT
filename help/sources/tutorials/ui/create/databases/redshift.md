---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore sorgente Amazon Redshift nell’interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---


# Creare un connettore sorgente Amazon Redshift nell’interfaccia utente

>Le selezioni del menu [!NOTE]
>Il connettore Amazon Redshift è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in  Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per la creazione di un connettore sorgente Amazon Redshift (in seguito denominato &quot;Redshift&quot;) tramite l&#39;interfaccia utente di Platform.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione di base Redshift, è possibile ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per accedere al tuo account Redshift su Platform, devi fornire i seguenti valori:

| **Credenziali** | **Descrizione** |
| -------------- | --------------- |
| `server` | Server associato al tuo account Redshift. |
| `username` | Il nome utente associato al tuo account Redshift. |
| `password` | La password associata al tuo account Redshift. |
| `database` | Il database Redshift a cui si accede. |

Per ulteriori informazioni su come iniziare, consultare [questo documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)Redshift.

## Collegamento dell&#39;account Redshift

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti di seguito per creare una nuova connessione di base in ingresso per collegare il tuo account Redshift ad Platform.

Accedete a <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi selezionate **Origini** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro *Origini* . Nella schermata *Catalogo* sono visualizzate diverse sorgenti con cui è possibile creare connessioni di base in entrata e ogni origine mostra il numero di connessioni di base esistenti ad esse associate.

Nella categoria *Database* , selezionate **Amazon Redshift** per esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione della sorgente selezionata e le opzioni per collegarsi alla sorgente o visualizzare la documentazione. Per creare una nuova connessione di base in entrata, selezionate l&#39;origine **** Connect.

![](../../../../images/tutorials/create/redshift/catalog.png)

Viene visualizzata la pagina *Connetti ad Amazon Redshift* . In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **Nuovo account**. Nel modulo di input visualizzato, specificare la connessione di base con un nome, una descrizione facoltativa e le credenziali di spostamento. Al termine, selezionate **Connect** , quindi concedete un po&#39; di tempo per stabilire la nuova connessione di base.

![](../../../../images/tutorials/create/redshift/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account Redshift con cui desiderate connettervi, quindi selezionate **Avanti** per continuare.

![](../../../../images/tutorials/create/redshift/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione di base all&#39;account Redshift. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati in Platform](../../dataflow/databases.md).